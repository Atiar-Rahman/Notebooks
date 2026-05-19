```python
import tensorflow as tf
from tensorflow import keras

# =========================================
# 1. CREATE DATASET
# =========================================

IMG_SIZE = (224, 224)
BATCH_SIZE = 32

train_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/train",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)

val_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/val",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)

# Optional: improve performance
AUTOTUNE = tf.data.AUTOTUNE

train_ds = train_ds.prefetch(AUTOTUNE)
val_ds = val_ds.prefetch(AUTOTUNE)

# =========================================
# 2. BUILD MODEL
# =========================================

model = keras.Sequential([
    keras.layers.Rescaling(1./255, input_shape=(224,224,3)),

    keras.layers.Conv2D(32, 3, activation="relu"),
    keras.layers.MaxPooling2D(),

    keras.layers.Conv2D(64, 3, activation="relu"),
    keras.layers.MaxPooling2D(),

    keras.layers.Flatten(),

    keras.layers.Dense(128, activation="relu"),
    keras.layers.Dense(2, activation="softmax")
])

# =========================================
# 3. COMPILE MODEL
# =========================================

model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

# =========================================
# 4. TRAIN MODEL
# =========================================

history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)

# =========================================
# 5. SAVE MODEL
# =========================================

model.save("my_model.keras")

print("Model Saved!")

# ==========================================================
# ==========================================================
#        LATER / NEXT SESSION
# ==========================================================
# ==========================================================

import tensorflow as tf
from tensorflow import keras

# =========================================
# 6. LOAD DATASET AGAIN
# =========================================

IMG_SIZE = (224, 224)
BATCH_SIZE = 32

train_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/train",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)

val_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/val",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)

AUTOTUNE = tf.data.AUTOTUNE

train_ds = train_ds.prefetch(AUTOTUNE)
val_ds = val_ds.prefetch(AUTOTUNE)

# =========================================
# 7. LOAD SAVED MODEL
# =========================================

model = keras.models.load_model("my_model.keras")

print("Model Loaded!")

# =========================================
# 8. CONTINUE TRAINING
# =========================================

history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)

# =========================================
# 9. SAVE AGAIN
# =========================================

model.save("my_model_v2.keras")

print("Training Continued & Model Saved!")
```

হ্যাঁ, অবশ্যই আগের মতো same `image_size` রাখতে হবে।

যদি model প্রথমে train করা হয়:

```python id="s3aj4d"
image_size=(224,224)
```

তাহলে পরে continue training-এর সময়ও:

```python id="r4g5x8"
image_size=(224,224)
```

দিতেই হবে।

---

কারণ model-এর input shape fixed থাকে।

উদাহরণ:

```python id="c65h4i"
input_shape=(224,224,3)
```

এখন যদি পরে:

```python id="mz9w7l"
image_size=(128,128)
```

দেন, তাহলে error আসবে:

* shape mismatch
* incompatible input shape

---

## Same রাখতে হবে যেগুলো

✅ image size
✅ color mode (RGB/Grayscale)
✅ number of classes
✅ label format
✅ preprocessing

---

## Example

### First training

```python id="4r3v8f"
image_size=(224,224)
```

### Continue training

```python id="ns6q2m"
image_size=(224,224)
```

এটাই correct।


হ্যাঁ, যতটা সম্ভব আগের preprocessing/property একই রাখা উচিত।
বিশেষ করে যেগুলো model input-এর সাথে সম্পর্কিত।

## ✅ খুব গুরুত্বপূর্ণ যেগুলো same রাখতে হবে

### 1. Image size

```python id="1g6m0y"
image_size=(224,224)
```

---

### 2. Color mode

আগে যদি RGB হয়:

```python id="h91p6f"
color_mode="rgb"
```

তাহলে পরে grayscale দিলে চলবে না।

---

### 3. Rescaling / normalization

আগে যদি:

```python id="y9x8r1"
layers.Rescaling(1./255)
```

ব্যবহার করেন, পরে training-এও same রাখতে হবে।

---

### 4. Label mode

আগে যদি:

```python id="0r6t3x"
label_mode="int"
```

তাহলে পরে one-hot এ change করলে loss mismatch হতে পারে।

---

### 5. Class order

Folder/class order change করা যাবে না।

উদাহরণ:

```id="5c7m8d"
cats/
dogs/
```

পরে:

```id="n2w4k9"
dogs/
cats/
```

করলে label উল্টে যেতে পারে।

---

# ⚠️ Optional things (same না হলেও চলে)

এগুলো change করলেও সাধারণত সমস্যা হয় না:

* batch_size
* shuffle=True/False
* cache/prefetch
* augmentation strength

---

# Safe rule ✅

যে code দিয়ে প্রথম dataset বানিয়েছিলেন, সেটাই copy করে আবার ব্যবহার করুন।
তাহলে compatibility issue হবে না।
হ্যাঁ, ঠিক তাই ✅

যদি আপনি full model save করে থাকেন:

```python id="frbxg5"
model.save("my_model.keras")
```

তাহলে পরে শুধু:

```python id="f0v6ci"
model = keras.models.load_model("my_model.keras")
```

এরপর সরাসরি:

```python id="s8fkgx"
model.fit(train_ds, validation_data=val_ds, epochs=5)
```

করলেই হবে।

❌ আবার `compile()` লাগবে না।

---

## Complete minimal example

```python id="8z4mp2"
from tensorflow import keras

# dataset again
train_ds = ...
val_ds = ...

# load model
model = keras.models.load_model("my_model.keras")

# continue training
model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)
```

এটাই correct workflow।


হ্যাঁ, কয়েকটা গুরুত্বপূর্ণ practical বিষয় আছে যেগুলো অনেক সময় পরে সমস্যা বাঁচায়:

---

## ✅ 1. Epoch continue হয় না automatically

ধরুন আগে:

```python id="lf2c6i"
epochs=5
```

train করেছেন।

পরে আবার:

```python id="9qq1h9"
epochs=5
```

দিলে নতুন করে 1→5 দেখাবে।
কিন্তু weights আগের trained অবস্থাতেই থাকবে।

যদি display continue করতে চান:

```python id="k9zj4g"
model.fit(
    train_ds,
    validation_data=val_ds,
    initial_epoch=5,
    epochs=10
)
```

---

## ✅ 2. Best practice → checkpoint save

```python id="4u1r5n"
checkpoint = keras.callbacks.ModelCheckpoint(
    "best_model.keras",
    save_best_only=True
)
```

---

## ✅ 3. TensorFlow version খুব বেশি change না করাই ভালো

Different TF/Keras version এ মাঝে মাঝে load issue আসে।

---

## ✅ 4. `.keras` format use করুন

সবচেয়ে recommended:

```python id="mwz6a7"
model.save("model.keras")
```

`.h5` থেকেও better।

---

## ✅ 5. Dataset path same না হলেও চলে

শুধু structure compatible হতে হবে।

---

## ✅ 6. Optimizer state restore হয়

তাই learning momentum continue থাকে।

---

## ⚠️ 7. Custom layer থাকলে

Load করার সময়:

```python id="wdq7pz"
load_model(..., custom_objects={...})
```

লাগতে পারে।

---

## ✅ 8. GPU/CPU change সাধারণত সমস্যা না

CPU তে save করে GPU তে load করা যায়।

---

## ✅ 9. Continue training এর আগে evaluate করা ভালো

```python id="nqewd7"
model.evaluate(val_ds)
```

তাহলে বুঝবেন model ঠিকমতো load হয়েছে কিনা।

---

## ✅ 10. Save history separately চাইলে

```python id="x0v1aj"
import pickle

with open("history.pkl", "wb") as f:
    pickle.dump(history.history, f)
```

---

সবচেয়ে important তিনটা:

✅ same preprocessing
✅ same input shape
✅ no need to compile again (full model save হলে)
তাহলে total training হবে **আরও ১০ epoch**, অর্থাৎ আগের ৫ + নতুন ১০ = মোট ১৫ epoch equivalent training।

উদাহরণ:

### আগে

```python id="skz6ux"
model.fit(..., epochs=5)
```

এতে epoch চলেছে:

```id="0z0cpj"
1/5 → 5/5
```

---

### পরে

```python id="8zk6b8"
model.fit(..., epochs=10)
```

এখন আবার দেখাবে:

```id="j4l66e"
1/10 → 10/10
```

কিন্তু এটা নতুন model না — আগের trained weights থেকেই continue করবে।

---

## `initial_epoch` না দিলে কী হয়?

শুধু display/reset হয়।
Training reset হয় না।

---

## Difference

### Without `initial_epoch`

```python id="i5fy1q"
model.fit(epochs=10)
```

Display:

```id="l3i7dh"
Epoch 1/10
```

---

### With `initial_epoch`

```python id="kll2x0"
model.fit(
    initial_epoch=5,
    epochs=10
)
```

Display:

```id="4g5tyx"
Epoch 6/10
```

---

## Important

`epochs` মানে “শেষ পর্যন্ত কত epoch চলবে”।

তাই:

```python id="8rd4o2"
initial_epoch=5,
epochs=10
```

মানে শুধু 6→10 চলবে (আরও ৫ epoch)।

---

## Summary

| Situation                               | কী হবে                |
| --------------------------------------- | --------------------- |
| আগে 5, পরে `epochs=10`                  | আরও 10 epoch train    |
| আগে 5, পরে `initial_epoch=5, epochs=10` | আরও 5 epoch train     |
| `initial_epoch` না দিলে                 | শুধু counter reset হয় |

হ্যাঁ, এই part-এ (save → load → continue training) কিছু **advanced কিন্তু খুব কাজে লাগে এমন জিনিস** আছে। এগুলো জানলে পরে error/bug অনেক কম হবে।

---

## 🔥 1. Learning rate change করা (important)

Continue training করার সময় অনেকেই LR কমায়:

```python id="lr1"
from tensorflow import keras

model.compile(
    optimizer=keras.optimizers.Adam(learning_rate=1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

👉 এটা optional, কিন্তু fine-tuning এ খুব common

---

## 🔥 2. Fine-tuning (pretrained model হলে)

যদি CNN/transfer learning use করো:

```python id="ft1"
base_model.trainable = True
```

বা কিছু layer freeze:

```python id="ft2"
for layer in base_model.layers[:-10]:
    layer.trainable = False
```

---

## 🔥 3. Dataset shuffle গুরুত্বপূর্ণ

Continue training এ shuffle রাখা ভালো:

```python id="ds1"
train_ds = train_ds.shuffle(1000)
```

---

## 🔥 4. Mixed precision (fast training)

GPU থাকলে:

```python id="mp1"
from tensorflow.keras import mixed_precision

mixed_precision.set_global_policy("mixed_float16")
```

---

## 🔥 5. Checkpoint + resume best practice

```python id="cp1"
checkpoint = keras.callbacks.ModelCheckpoint(
    "best.keras",
    save_best_only=True,
    monitor="val_accuracy"
)
```

---

## 🔥 6. Early stopping (overfitting avoid)

```python id="es1"
early_stop = keras.callbacks.EarlyStopping(
    monitor="val_loss",
    patience=3,
    restore_best_weights=True
)
```

---

## 🔥 7. Real resume training (best way)

Save + load + continue:

```python id="rt1"
model = keras.models.load_model("model.keras")

model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

👉 চাইলে:

```python id="rt2"
initial_epoch=5
```

use করলে clean tracking হয়

---

## ⚠️ Common mistakes (খুব important)

❌ image size change
❌ label order change
❌ different preprocessing
❌ different class names
❌ forgetting normalization

---

## 🧠 Golden rule

👉 “Model load করলে weights same থাকে, কিন্তু dataset আবার same pipeline দিয়ে বানাতে হয়।”

---

যদি চান, আমি আপনার জন্য **real production-ready training pipeline template (CNN + callbacks + save + resume)** একদম clean করে বানিয়ে দিতে পারি।
ঠিক আছে, একদম **step-by-step “আগে কী ছিল → পরে কী করা উচিত”** সহজভাবে দেখাচ্ছি যাতে confusion না থাকে।

---

# 🧠 STEP 1: FIRST TRAINING (আগে যা করেছিলেন)

## 🔹 Dataset তৈরি

```python id="s1"
train_ds = image_dataset_from_directory("dataset/train", image_size=(224,224))
val_ds   = image_dataset_from_directory("dataset/val", image_size=(224,224))
```

## 🔹 Model build

```python id="s2"
model = keras.Sequential([...])
```

## 🔹 Compile (VERY IMPORTANT)

```python id="s3"
model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

## 🔹 Train

```python id="s4"
model.fit(train_ds, validation_data=val_ds, epochs=5)
```

## 🔹 Save

```python id="s5"
model.save("model.keras")
```

---

# 🧠 STEP 2: LATER (RE-TRAIN / CONTINUE)

## 🔹 AGAIN dataset তৈরি করতে হবে (IMPORTANT ❗)

```python id="s6"
train_ds = image_dataset_from_directory("dataset/train", image_size=(224,224))
val_ds   = image_dataset_from_directory("dataset/val", image_size=(224,224))
```

👉 SAME image_size + SAME preprocessing must

---

## 🔹 Load model

```python id="s7"
model = keras.models.load_model("model.keras")
```

---

## 🔥 STEP 3: এখন কী change করবেন?

### ❌ 1. compile → usually NOT needed

```python id="s8"
# NOT required if full model saved
```

---

### ❗ BUT (optional change)

👉 যদি learning improve করতে চান:

```python id="s9"
model.compile(
    optimizer=keras.optimizers.Adam(1e-4),  # smaller LR
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

---

## 🔹 STEP 4: Continue training

```python id="s10"
model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

---

# ⚠️ STEP 5: কী কী SAME রাখতে হবে

সবচেয়ে important 👇

## MUST SAME:

* image_size = (224,224)
* color mode (RGB)
* label format
* class order (folder order)
* preprocessing (rescale / normalization)

---

## 🔥 STEP 6: কী কী change করা যায়

### ✔ safe changes:

* epochs increase
* learning rate change
* callbacks add
* batch size (sometimes)

---

# 🧠 FINAL SIMPLE RULE

👉 **Model load = weights ready**
👉 **Dataset = আবার same way বানাতে হবে**
👉 **Compile = only if needed (optional)**
👉 **Fit = continue training**

---

# 🚀 SUPER SIMPLE SUMMARY

| Step       | Must do again?  |
| ---------- | --------------- |
| Dataset    | ✅ Yes           |
| Model load | ✅ Yes           |
| Compile    | ❌ No (optional) |
| Fit        | ✅ Yes           |
| Image size | ❌ MUST same     |

---

যদি চাও, আমি তোমার জন্য একটা **“perfect checklist for every training project”** বানিয়ে দিতে পারি যেটা follow করলে আর কখনও error হবে না।
