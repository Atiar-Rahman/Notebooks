
## 0) কী বানাচ্ছি?

ধরি, আমাদের কাছে ছবি আছে (যেমন: **cats vs dogs**) আর আমরা ছবিটা কোন ক্লাস সেটা predict করতে চাই।

---

## 1) প্রজেক্ট স্ট্রাকচার

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

👉 Keras নিজে থেকেই folder নামকে label ধরে নেয়।

---

## 2) প্রয়োজনীয় লাইব্রেরি ইন্সটল

```bash
pip install tensorflow matplotlib numpy
```

---

## 3) লাইব্রেরি ইমপোর্ট

```python
import tensorflow as tf
from tensorflow.keras import layers, models
import matplotlib.pyplot as plt
```

---

## 4) ডেটা লোড ও প্রিপ্রসেসিং

```python
img_size = (224, 224)
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
print(class_names)
```

### Normalization (খুব জরুরি)

```python
normalization_layer = layers.Rescaling(1./255)

train_ds = train_ds.map(lambda x, y: (normalization_layer(x), y))
val_ds   = val_ds.map(lambda x, y: (normalization_layer(x), y))
test_ds  = test_ds.map(lambda x, y: (normalization_layer(x), y))
```

---

## 5) CNN মডেল বানানো

```python
model = models.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(224,224,3)),
    layers.MaxPooling2D(),

    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Conv2D(128, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Flatten(),
    layers.Dense(128, activation='relu'),
    layers.Dense(len(class_names), activation='softmax')
])
```

---

## 6) Model Compile

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

---

## 7) Model Train

```python
history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

---

## 8) Accuracy & Loss গ্রাফ

```python
plt.plot(history.history['accuracy'], label='train_acc')
plt.plot(history.history['val_accuracy'], label='val_acc')
plt.legend()
plt.show()
```

---

## 9) Test ডেটায় Evaluate

```python
test_loss, test_acc = model.evaluate(test_ds)
print("Test accuracy:", test_acc)
```

---

## 10) নতুন ছবি দিয়ে Prediction

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

## 11) Model Save & Load

```python
model.save("cnn_model.h5")

# load
model = tf.keras.models.load_model("cnn_model.h5")
```

---

## পুরো পাইপলাইন এক লাইনে

**Images → Resize → Normalize → CNN → Softmax → Class Prediction**

---

যদি তুমি চাও:

- ✅ **Data Augmentation**
    
- ✅ **Pretrained CNN (ResNet, VGG, MobileNet)**
    
- ✅ **PyTorch version**
    
- ✅ **Bangla comments সহ কোড**
    


---

# ✅ PART–1: Data Augmentation (Overfitting কমাতে)

### কেন দরকার?

ডেটা কম হলে CNN মুখস্থ করে ফেলে।  
Augmentation একই ছবিকে ঘুরিয়ে–পাল্টিয়ে নতুন ডেটা বানায়।

---

## 1️⃣ Data Augmentation Layer

```python
data_augmentation = tf.keras.Sequential([
    layers.RandomFlip("horizontal"),
    layers.RandomRotation(0.1),
    layers.RandomZoom(0.1),
    layers.RandomContrast(0.1),
])
```

👉 এগুলো **শুধু training সময় কাজ করে**, test/val এ না।

---

## 2️⃣ Normalization Layer

```python
normalization = layers.Rescaling(1./255)
```

---

# ✅ PART–2: Pretrained CNN (Transfer Learning)

আমরা ব্যবহার করবো:

- **MobileNetV2** (হালকা, ফাস্ট)
    
- **ResNet50** (ডিপ, পাওয়ারফুল)
    
- **VGG16** (সহজ, কিন্তু ভারী)
    

---

# 🔹 Option A: MobileNetV2 (Most Popular)

## 3️⃣ Base Model লোড

```python
base_model = tf.keras.applications.MobileNetV2(
    input_shape=(224,224,3),
    include_top=False,
    weights="imagenet"
)

base_model.trainable = False  # feature extractor
```

---

## 4️⃣ Full Model বানানো

```python
inputs = layers.Input(shape=(224,224,3))
x = data_augmentation(inputs)
x = normalization(x)

x = base_model(x, training=False)
x = layers.GlobalAveragePooling2D()(x)
x = layers.Dense(128, activation='relu')(x)
x = layers.Dropout(0.5)(x)

outputs = layers.Dense(len(class_names), activation='softmax')(x)

model = tf.keras.Model(inputs, outputs)
```

---

## 5️⃣ Compile

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

---

## 6️⃣ Train

```python
history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

---

# 🔥 PART–3: Fine Tuning (Accuracy আরও বাড়াতে)

## 7️⃣ Top Layers Unfreeze

```python
base_model.trainable = True

for layer in base_model.layers[:-30]:
    layer.trainable = False
```

---

## 8️⃣ Re-Compile (LOW LR)

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-5),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

---

## 9️⃣ Fine Tune Train

```python
model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)
```

---

# 🔹 Option B: ResNet50 (Just change base model)

```python
base_model = tf.keras.applications.ResNet50(
    input_shape=(224,224,3),
    include_top=False,
    weights="imagenet"
)
```

बाकি কোড **একই থাকবে**।

---

# 🔹 Option C: VGG16 (Simple but Heavy)

```python
base_model = tf.keras.applications.VGG16(
    input_shape=(224,224,3),
    include_top=False,
    weights="imagenet"
)
```

⚠️ VGG slow + বেশি RAM খায়

---

# 📊 Comparison (Quick)

|Model|Speed|Accuracy|Use Case|
|---|---|---|---|
|MobileNet|⚡ Fast|⭐⭐⭐⭐|Mobile / Low GPU|
|ResNet|🐢 Medium|⭐⭐⭐⭐⭐|Best accuracy|
|VGG|🐌 Slow|⭐⭐⭐|Learning purpose|

---

# ✅ Final Pipeline (Industry Style)

```
Image
 → Data Augmentation
 → Normalization
 → Pretrained CNN
 → GlobalAvgPooling
 → Dense + Dropout
 → Softmax
 → Prediction
```

---

যদি চাও, আমি পরের ধাপে দেখাতে পারি:

- 📈 Confusion Matrix + Precision/Recall
    
- 🧠 Custom CNN vs Pretrained comparison
    
- 🚀 PyTorch version
    
- 📂 Kaggle-ready full notebook
    

---------

চল ঠিক আছে 😎 এবার **image classification-এর জন্য Confusion Matrix, Precision, Recall** দেখাই। আমরা ধরে নেবো তুমি আগের **pretrained CNN (MobileNetV2)** মডেল ট্রেইন করে ফেলেছ।

---

# 1️⃣ Test Dataset থেকে Prediction নেওয়া

```python
import numpy as np

# সব test images & labels একত্র করা
y_true = np.concatenate([y for x, y in test_ds], axis=0)

# Prediction
y_pred_prob = model.predict(test_ds)
y_pred = np.argmax(y_pred_prob, axis=1)
```

---

# 2️⃣ Confusion Matrix বানানো

```python
from sklearn.metrics import confusion_matrix
import seaborn as sns
import matplotlib.pyplot as plt

cm = confusion_matrix(y_true, y_pred)

plt.figure(figsize=(6,5))
sns.heatmap(cm, annot=True, fmt="d", cmap="Blues", xticklabels=class_names, yticklabels=class_names)
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix")
plt.show()
```

🔹 এতে তুমি দেখতে পারবে কোন ক্লাস গুলো বেশি ভুল হচ্ছে।

---

# 3️⃣ Precision, Recall, F1 Score

```python
from sklearn.metrics import classification_report

report = classification_report(y_true, y_pred, target_names=class_names)
print(report)
```

Output দেখাবে প্রতিটি ক্লাসের জন্য:

- **Precision** = ভুলভাবে predict না করে সঠিক predict করার হার
    
- **Recall** = আসল positive detect করার হার
    
- **F1-score** = Precision + Recall-এর harmonic mean
    

---

# 4️⃣ Quick Interpretation

- Confusion Matrix: বড় diagonal → ভালো accuracy
    
- Precision high, Recall low → model strict, কিছু positive মিস করছে
    
- Recall high, Precision low → model অনেক positive ধরে ফেলছে, কিছু ভুল predict করছে
    

---

# 5️⃣ Optional: Per-class Plot

```python
import matplotlib.pyplot as plt
import numpy as np

accuracy_per_class = cm.diagonal()/cm.sum(axis=1)
plt.bar(class_names, accuracy_per_class)
plt.ylabel("Per-class Accuracy")
plt.show()
```

---

এভাবে তুমি পুরো **evaluation pipeline** পেয়ে যাবে, যা **real-world production-ready**।

💡 যদি চাও, আমি এখন দেখাতে পারি **Custom Python function বানিয়ে single-shot metric & confusion matrix draw করার জন্য**, যাতে তুমি এক লাইনেই সব test dataset চেক করতে পারো।

তুমি কি সেটা চাইছ?

----