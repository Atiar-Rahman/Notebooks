**সম্পূর্ণ Image Classification + Data Augmentation + Pretrained CNN + Evaluation (Confusion Matrix, Precision/Recall)** **একটি pipeline আকারে** সাজাতে পারি, যাতে একবার রান করলেই সব হয়ে যায়।

আমি একদম শুরু থেকে শেষ পর্যন্ত workflow বানাচ্ছি।

---

# ✅ Complete Pipeline (TensorFlow/Keras)

```python
# 1️⃣ Libraries
import tensorflow as tf
from tensorflow.keras import layers, models
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix, classification_report
import seaborn as sns

# 2️⃣ Parameters
img_size = (224,224)
batch_size = 32

# 3️⃣ Load Dataset
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

# 4️⃣ Data Augmentation + Normalization
data_augmentation = tf.keras.Sequential([
    layers.RandomFlip("horizontal"),
    layers.RandomRotation(0.1),
    layers.RandomZoom(0.1),
    layers.RandomContrast(0.1),
])
normalization = layers.Rescaling(1./255)

train_ds = train_ds.map(lambda x,y: (normalization(x),y))
val_ds = val_ds.map(lambda x,y: (normalization(x),y))
test_ds = test_ds.map(lambda x,y: (normalization(x),y))

# 5️⃣ Pretrained Base Model
base_model = tf.keras.applications.MobileNetV2(
    input_shape=(224,224,3),
    include_top=False,
    weights="imagenet"
)
base_model.trainable = False

# 6️⃣ Build Model
inputs = layers.Input(shape=(224,224,3))
x = data_augmentation(inputs)
x = base_model(x, training=False)
x = layers.GlobalAveragePooling2D()(x)
x = layers.Dense(128, activation='relu')(x)
x = layers.Dropout(0.5)(x)
outputs = layers.Dense(len(class_names), activation='softmax')(x)
model = tf.keras.Model(inputs, outputs)

# 7️⃣ Compile
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

# 8️⃣ Train
history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)

# 9️⃣ Optional Fine-tuning
base_model.trainable = True
for layer in base_model.layers[:-30]:
    layer.trainable = False

model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-5),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

history_finetune = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)

# 🔟 Evaluate on Test
test_loss, test_acc = model.evaluate(test_ds)
print("Test Accuracy:", test_acc)

# 1️⃣1️⃣ Confusion Matrix
y_true = np.concatenate([y for x,y in test_ds], axis=0)
y_pred_prob = model.predict(test_ds)
y_pred = np.argmax(y_pred_prob, axis=1)

cm = confusion_matrix(y_true, y_pred)
plt.figure(figsize=(6,5))
sns.heatmap(cm, annot=True, fmt="d", cmap="Blues", xticklabels=class_names, yticklabels=class_names)
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix")
plt.show()

# 1️⃣2️⃣ Precision, Recall, F1
print(classification_report(y_true, y_pred, target_names=class_names))
```

---

# ✅ Pipeline Flow

```
Images → Load → Resize → Normalize → Data Augmentation
      → Pretrained CNN (MobileNetV2)
      → GlobalAveragePooling → Dense → Dropout → Softmax
      → Train → Fine-tune
      → Evaluate → Test Accuracy
      → Confusion Matrix + Precision/Recall
```

---

এই এক পাইপলাইন চালালে:

1. Data Augmentation হয়ে যাবে
2. Pretrained CNN ব্যবহার হবে
3. Model train + fine-tune হবে
4. Test set evaluation + Confusion Matrix + Precision/Recall report দেখাবে

---




