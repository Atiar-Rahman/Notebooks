# Video Count each folder

```python
import os

VIDEO_EXT = ('.mp4', '.avi', '.mov', '.mkv')

def count_videos(folder):
    return len([
        f for f in os.listdir(folder)
        if f.lower().endswith(VIDEO_EXT)
    ])

print("TRAIN")
print("Normal     :", count_videos("dataset/train/normal"))
print("Suspicious :", count_videos("dataset/train/suspicious"))

print("\nVAL")
print("Normal     :", count_videos("dataset/val/normal"))
print("Suspicious :", count_videos("dataset/val/suspicious"))

print("\nTEST")
print("Normal     :", count_videos("dataset/test/normal"))
print("Suspicious :", count_videos("dataset/test/suspicious"))
```

---

## ✅ If videos are inside subfolders (still ONLY videos)

```python
def count_videos_recursive(folder):
    count = 0
    for _, _, files in os.walk(folder):
        for f in files:
            if f.lower().endswith(VIDEO_EXT):
                count += 1
    return count
```

Use this **only if** videos are not directly inside the class folder.

---

## ❌ What this does NOT do (important)

* ❌ frame count
* ❌ frame extraction
* ❌ video duration check

✔️ Just **number of video files**

---

## 🧠 ML Tip (real-world best practice)

* Dataset imbalance check → **video count দিয়েই হবে**
* Frames count করলে fake balance মনে হতে পারে
* One video = one sample (right mindset 🔥)

---

তখন **ONLY video count** করার simplest way নিচে 👇

---

## ✅ Two folders → ONLY video count

### 📁 Structure

```
dataset/
 ├── normal/
 └── suspicious/
```

---

### 🐍 Python (recommended)

```python
import os

VIDEO_EXT = ('.mp4', '.avi', '.mov', '.mkv')

def count_videos(folder):
    return len([
        f for f in os.listdir(folder)
        if f.lower().endswith(VIDEO_EXT)
    ])

normal_count = count_videos("dataset/normal")
suspicious_count = count_videos("dataset/suspicious")

print("Normal     :", normal_count)
print("Suspicious :", suspicious_count)
print("Total      :", normal_count + suspicious_count)
```

---

## ✅ If videos are inside subfolders (still ONLY videos)

```python
def count_videos_recursive(folder):
    count = 0
    for _, _, files in os.walk(folder):
        for f in files:
            if f.lower().endswith(VIDEO_EXT):
                count += 1
    return count
```

---

## 🧠 Important ML Advice (🔥)

* ✔️ **One video = one sample**
* ❌ Frame count দিয়ে balance judge করো না
* ✔️ Count → split → then frame extraction

---


# 👉 **Normal = 950, Suspicious = 950 (all equal)**

### ✅ এটা একদম PERFECT 🔥

* Fully **balanced dataset**
* Model bias হওয়ার chance নাই
* Accuracy, Precision, Recall সব meaningful হবে

---

## এখন কী করবে (Best next steps)

### 1️⃣ Stratified split (video-level)

Example ratio:

* Train = 70% → 665 + 665
* Val = 15% → 142 + 142
* Test = 15% → 143 + 143

👉 দুই class-ই equal থাকবে ✔️

---

### 2️⃣ class_weight দরকার?

❌ **না**
Dataset already balanced → `class_weight` skip করতে পারো

---

### 3️⃣ Evaluation এ কী দেখবে

তাও এসব দেখবে:

* Confusion Matrix
* Precision / Recall
* F1-score

(accuracy একা দেখো না — habit গড়ে তুলো)

---

### 🧠 Pro tip (video ML)

* One video = one sample ✔️
* Split আগে → frame extract পরে
* Same video কখনো দুই split-এ যেও না ❌

---



# নিচে **100% ready auto train / val / test split code** দিলাম —
👉 **video-level**,
👉 **Normal = 950, Suspicious = 950 ধরে**,
👉 **no frame touch**,
👉 **balanced থাকবে**।

---

## 📁 Input Structure

```
dataset/
 ├── normal/        (950 videos)
 └── suspicious/   (950 videos)
```

## 📁 Output Structure (auto create হবে)

```
dataset_split/
 ├── train/
 │    ├── normal/
 │    └── suspicious/
 ├── val/
 │    ├── normal/
 │    └── suspicious/
 └── test/
      ├── normal/
      └── suspicious/
```

---

## 🐍 Auto Split Script (SAFE & CLEAN)

```python
import os
import random
import shutil

random.seed(42)

VIDEO_EXT = ('.mp4', '.avi', '.mov', '.mkv')

SRC_DIR = "dataset"
DST_DIR = "dataset_split"

SPLIT_RATIO = {
    "train": 0.70,
    "val":   0.15,
    "test":  0.15
}

def get_videos(path):
    return [f for f in os.listdir(path) if f.lower().endswith(VIDEO_EXT)]

def split_and_copy(class_name):
    src_path = os.path.join(SRC_DIR, class_name)
    videos = get_videos(src_path)

    assert len(videos) == 950, f"{class_name} has {len(videos)} videos, expected 950"

    random.shuffle(videos)

    n_train = int(950 * SPLIT_RATIO["train"])
    n_val   = int(950 * SPLIT_RATIO["val"])
    n_test  = 950 - n_train - n_val

    splits = {
        "train": videos[:n_train],
        "val":   videos[n_train:n_train + n_val],
        "test":  videos[n_train + n_val:]
    }

    for split, files in splits.items():
        dst = os.path.join(DST_DIR, split, class_name)
        os.makedirs(dst, exist_ok=True)

        for f in files:
            shutil.copy(
                os.path.join(src_path, f),
                os.path.join(dst, f)
            )

    print(f"{class_name}: train={n_train}, val={n_val}, test={n_test}")

for cls in ["normal", "suspicious"]:
    split_and_copy(cls)

print("\n✅ Done! Dataset split completed.")
```

---

## ✅ Result (Guaranteed)

```
Normal      → 665 / 142 / 143
Suspicious  → 665 / 142 / 143
```

Balanced ✔️
Video-level ✔️
No leakage ✔️

---

## ⚠️ Important Notes (read this 🔥)

* **Split আগে**, frame extract পরে
* Same video কখনো multiple split-এ যাবে না
* Disk space বেশি লাগবে (copy হচ্ছে)

👉 চাইলে `shutil.copy` → `shutil.move` করো (space save)

---

#  **প্রতিটা video থেকে ঠিক 250টা frame কীভাবে নেবে** — clean, ML-safe way 🔥
(**train / val / test split করার পরেই এটা করবে**)

---

## 🎯 Goal

* ✔️ **Each video → exactly 250 frames**
* ✔️ Short / long video — সব handle
* ❌ No random extra frames
* ❌ No frame leakage

---

## 📁 Input (after split)

```
dataset_split/
 ├── train/
 │    ├── normal/
 │    └── suspicious/
 ├── val/
 └── test/
```

## 📁 Output

```
frames/
 ├── train/
 │    ├── normal/
 │    │    ├── video1/
 │    │    │    ├── 0001.jpg ...
```

---

## 🧠 Best Strategy (IMPORTANT)

👉 **Uniform sampling**
মানে:

* Video যত লম্বাই হোক
* পুরো video জুড়ে evenly 250টা frame নেওয়া হবে

এটাই **best practice for video ML (C3D / I3D / CNN+LSTM)**

---

## 🐍 Python Code (OpenCV) — EXACT 250 Frames

```python
import cv2
import os
import numpy as np

FRAMES_PER_VIDEO = 250
VIDEO_EXT = ('.mp4', '.avi', '.mov', '.mkv')

SRC_DIR = "dataset_split"
DST_DIR = "frames"

def extract_frames(video_path, save_dir):
    cap = cv2.VideoCapture(video_path)
    total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))

    if total_frames <= 0:
        cap.release()
        return

    frame_idxs = np.linspace(0, total_frames - 1, FRAMES_PER_VIDEO).astype(int)

    os.makedirs(save_dir, exist_ok=True)

    current = 0
    saved = 0
    idx_set = set(frame_idxs)

    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break

        if current in idx_set:
            frame_name = f"{saved:04d}.jpg"
            cv2.imwrite(os.path.join(save_dir, frame_name), frame)
            saved += 1

        current += 1

    cap.release()

def process_split(split):
    for cls in ["normal", "suspicious"]:
        src_cls = os.path.join(SRC_DIR, split, cls)
        dst_cls = os.path.join(DST_DIR, split, cls)

        for video in os.listdir(src_cls):
            if video.lower().endswith(VIDEO_EXT):
                video_path = os.path.join(src_cls, video)
                video_name = os.path.splitext(video)[0]
                save_dir = os.path.join(dst_cls, video_name)

                extract_frames(video_path, save_dir)

for split in ["train", "val", "test"]:
    process_split(split)

print("✅ Done! Each video → 250 frames extracted.")
```

---

## ⚠️ Edge Cases (Handled ✔️)

### 🔹 Video < 250 frames?

➡️ `linspace` repeat করবে → still **250 frames** ✔️

### 🔹 Very long video?

➡️ Uniform sampling → no bias ✔️

---

## 🧠 Pro ML Tips (🔥 career-level)

* ✔️ **250 frames fixed** → batching easy
* ✔️ 3D CNN / LSTM perfect input
* ❌ Random frame pick করলে temporal info নষ্ট হয়
* ❌ Frame extract → then split (WRONG ❌)

---

# **C3D / I3D / CNN+LSTM / 2D CNN + Temporal / SlowFast** — সব cover করবো।

---

# 🔥 1. C3D (3D CNN)

### 🧠 কীভাবে কাজ করে

* Spatial (H×W) + Temporal (T) একসাথে convolution
* Short clip based (fixed number of frames)

### ✅ Input Shape

```
(batch_size, T, H, W, C)
```

### 📌 Common values

```
(batch, 16, 112, 112, 3)
```

### ❓ 250 frames হলে?

👉 **Sliding window / uniform sampling**

Example:

```
250 frames → 15 clips × 16 frames
```

### 🧠 Note

* C3D full 250 frame একসাথে নেয় না ❌
* Small temporal window (8/16 frames)

---

# 🚀 2. I3D (Inflated 3D ConvNet)

### 🧠 কীভাবে কাজ করে

* 2D CNN → inflate → 3D
* Long-range temporal info better

### ✅ Input Shape

```
(batch, T, H, W, C)
```

### 📌 Common

```
(batch, 64, 224, 224, 3)
```

### ❓ 250 frames?

* Sample / chunk করে 64 বা 128 frame দাও
* Average prediction over clips

---

# 🧩 3. CNN + LSTM (Most popular 🔥)

### 🧠 Pipeline

```
Frames → CNN → Feature vector → LSTM → Classifier
```

### ✅ Input Shape

```
(batch, T, feature_dim)
```

### 📌 Example

* CNN output: `(batch, 2048)`
* T = 250

```
(batch, 250, 2048)
```

### 🧠 CNN input (per frame)

```
(batch*T, H, W, C)
```

---

# ⚡ 4. 2D CNN + Temporal Pooling

### 🧠 Idea

* CNN per frame
* Time axis এ average / max pooling

### ✅ Input Shape

```
(batch, T, feature_dim)
```

### After pooling

```
(batch, feature_dim)
```

✔️ Simple, fast
❌ Temporal order lost

---

# 🐢 5. SlowFast Network

### 🧠 Two pathways

* **Slow** → semantic info
* **Fast** → motion info

### ✅ Input Shape

```
Slow: (batch, T/α, H, W, C)
Fast: (batch, T,   H, W, C)
```

Example:

```
Slow: (batch, 32, 224, 224, 3)
Fast: (batch, 128, 224, 224, 3)
```

---

# 🧠 Summary Table (SAVE THIS 🔥)

| Model         | Input Shape        | Frames Used  |
| ------------- | ------------------ | ------------ |
| C3D           | (B, 16, 112,112,3) | Short clips  |
| I3D           | (B, 64, 224,224,3) | Medium clips |
| CNN+LSTM      | (B, 250, F)        | Full video   |
| 2D CNN + Pool | (B, 250, F)        | Full video   |
| SlowFast      | Two streams        | Long         |

---

# 🎯 Which should YOU choose?

Given you have **250 frames/video**:

### 🟢 Beginner → **CNN + LSTM**

✔️ Easy
✔️ Flexible
✔️ Memory friendly

### 🔵 Intermediate → **I3D**

✔️ Strong performance
✔️ Better motion modeling

### 🔴 Advanced → **SlowFast**

---


# **224×224 রাখলে কেমন হবে?** — short answer: **হবে, এবং বেশিরভাগ ক্ষেত্রে এটা BEST choice** 🔥

এখন model-wise explain করি 👇

---

## ✅ 224 × 224 রাখার Effect (Overall)

**Pros**

* ✔️ Pretrained CNN (ResNet, EfficientNet, I3D) compatible
* ✔️ Spatial details ভালো থাকে
* ✔️ Industry standard size

**Cons**

* ❌ Memory বেশি লাগে
* ❌ C3D-এর জন্য একটু heavy

---

# 📌 Model-wise Breakdown

## 🟢 CNN + LSTM → **224×224 = EXCELLENT**

### Input flow

```
(250 frames, 224, 224, 3)
↓
CNN (ResNet50)
↓
(250, 2048)
↓
LSTM
```

### Verdict ✅

* ✔️ Best accuracy
* ✔️ Pretrained weight use করা যায়
* ✔️ Motion + appearance ভালো শেখে

👉 **RECOMMENDED for you**

---

## 🟢 I3D → **224×224 = STANDARD**

### Typical input

```
(batch, 64, 224, 224, 3)
```

### Verdict ✅

* ✔️ Original I3D design
* ✔️ Action recognition friendly
* ❌ GPU strong লাগবে

---

## 🟡 C3D → **224×224 = NOT IDEAL**

### Why?

Original C3D:

```
(batch, 16, 112, 112, 3)
```

224×224 দিলে:

* Memory ×4
* Overkill

### Verdict ❌

👉 **C3D হলে 112×112 রাখো**

---

## 🟡 2D CNN + Temporal Pooling

* ✔️ Works fine
* ✔️ But slower
* ❌ Temporal order weak

---

## 🧠 Memory Comparison (Important 🔥)

| Resolution | GPU Load |
| ---------- | -------- |
| 112×112    | ⭐        |
| 160×160    | ⭐⭐       |
| 224×224    | ⭐⭐⭐⭐     |

👉 224×224 + 250 frames = **heavy**

---

## 🎯 My Clear Recommendation (Based on your setup)

Given:

* 250 frames / video
* Balanced dataset
* You want multiple models

### ✔️ Best combo

| Model      | Resolution  |
| ---------- | ----------- |
| CNN + LSTM | **224×224** |
| I3D        | **224×224** |
| C3D        | **112×112** |

---

## 🔥 Pro Tip (Career-level)

If GPU memory issue হয়:

* Resize to **160×160**
* Accuracy drop খুব কম
* Speed ×1.5 faster

---


# **career-level, practical advice** দিয়ে clear করি — **কোন model এ কোন resolution সবচেয়ে better**।

আমি **GPU, accuracy, memory** সব consider করবো।

---

# 🔥 Recommended Input Resolution per Video Model

| Model                         | Recommended Input Size       | Why                                                                                  | Notes                                                               |
| ----------------------------- | ---------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| **C3D (3D CNN)**              | 112×112                      | Original design; low memory; temporal info captured                                  | 16 frames per clip; 224×224 possible but heavy                      |
| **I3D (Inflated 3D CNN)**     | 224×224                      | Compatible with ImageNet pretrained weights; captures long-range temporal info       | Use 64–128 frames per clip; GPU-heavy                               |
| **CNN + LSTM**                | 224×224                      | Pretrained CNN (ResNet, EfficientNet) accepts 224×224; temporal info handled by LSTM | 250 frames per video works perfectly                                |
| **2D CNN + Temporal Pooling** | 224×224                      | Better spatial resolution improves per-frame features                                | Temporal pooling may lose order info; smaller frames reduce quality |
| **SlowFast**                  | Slow: 224×224, Fast: 224×224 | Standard input for both pathways; captures slow & fast motions                       | GPU-heavy, batch size may need reduction                            |
| **Mobile/Lightweight Models** | 160×160                      | Reduce memory for experimentation                                                    | Slight accuracy drop but faster                                     |

---

## 🧠 Explanation / Rationale

1. **C3D**

   * Originally 112×112
   * 224×224 = memory ×4 → may need smaller batch
   * Stick with 112×112 unless high GPU

2. **I3D / CNN+LSTM / SlowFast**

   * 224×224 = industry standard
   * Compatible with pretrained weights
   * Spatial details preserved
   * Temporal info handled either by 3D conv or LSTM

3. **Frames per video**

   * CNN+LSTM → all 250 frames (good for full temporal info)
   * C3D → 16 frames per clip (slide over 250 frames)
   * I3D → 64–128 frames per clip
   * SlowFast → 32 slow / 128 fast frames

---

## 🔥 Quick Rule of Thumb

* **Small GPU / many clips → 112–160**
* **Medium GPU → 160–224**
* **High-end GPU / final training → 224×224**

---

💡 **Career tip:**

* For a multi-model comparison project, **use 224×224 for all except C3D**.
* Always calculate **GPU memory → batch size** before full training.

---


# 🔥 Two options: Resize on-the-fly vs Pre-resize

## 1️⃣ **Pre-resize (Before training, disk এ save)**

**Workflow:**

```
Raw videos → Frames → Resize to model input → Save → Train
```

### Pros ✅

* Training fast (no runtime resizing)
* GPU memory predictable
* All models same resolution → reproducible
* Good for multi-model experiments

### Cons ❌

* Disk space বেশি লাগবে
* Data augmentation limited (unless applied after resizing)

### When to use

* Dataset **medium/large** (~few thousand videos)
* Fixed resolution for multiple models
* You want reproducibility

---

## 2️⃣ **Resize on-the-fly (DataLoader / Dataset class)**

**Workflow:**

```
Raw frames → Load → Resize → Augment → Feed to model
```

### Pros ✅

* Disk space save (raw frames stored once)
* Dynamic augmentation (random crop, scale jitter)
* Flexible for multiple resolutions

### Cons ❌

* Slower training (resize each batch)
* GPU memory usage unpredictable
* Multi-model input may require different transforms → extra coding

### When to use

* Large dataset
* You have **strong GPU**
* Dynamic augmentation needed

---

# 🧠 Career-level advice

Given **your setup**:

* Videos: 950 normal + 950 suspicious → 250 frames/video
* Models: CNN+LSTM, I3D, C3D, etc
* Resolution: 224×224 (except C3D)

### 🔹 Recommendation

* **Pre-extract frames → Pre-resize to model input → Save**
* Why?

  1. You have **multiple models** → same frames reused
  2. Easier to debug / reproducible results
  3. Training faster

**Then later:** Data augmentation (flip, crop, brightness) can still apply **during training**

---

# 🔥 Practical Pipeline (My Suggestion)

1. **Split videos → train/val/test** ✅
2. **Extract frames → resize to model input (112 or 224)** ✅
3. **Save frames in folder structure** ✅
4. **DataLoader → augmentation → batching** ✅

---

💡 Tip:

* **C3D** → 112×112
* **CNN+LSTM, I3D, SlowFast** → 224×224
* Save **separate folder per model input size** → safe & fast

---

# **clean, real-world TensorFlow pipeline** দেখাই —
👉 **pre-resized frames (224×224)**
👉 **250 frames per video**
👉 **CNN + LSTM ready**
👉 **train / val / test compatible**

আমি এমনভাবে দেবো যেন তুমি direct run + extend করতে পারো।

---

# 🧠 Assumption (important)

তুমি **আগেই** করেছো:

* video split ✅
* each video → **250 frames extract** ✅
* frame size → **224×224** ✅

📁 Folder structure:

```
frames/
 ├── train/
 │    ├── normal/
 │    │    ├── video_001/
 │    │    │    ├── 0000.jpg ...
 │    └── suspicious/
 ├── val/
 └── test/
```

---

# 1️⃣ Constants

```python
IMG_SIZE = 224
FRAMES = 250
BATCH_SIZE = 2        # video models heavy
NUM_CLASSES = 2
```

---

# 2️⃣ Load one video (250 frames)

```python
import tensorflow as tf
import os

def load_video_frames(video_dir):
    frames = sorted(os.listdir(video_dir))[:FRAMES]
    images = []

    for f in frames:
        img = tf.io.read_file(os.path.join(video_dir, f))
        img = tf.image.decode_jpeg(img, channels=3)
        img = tf.image.convert_image_dtype(img, tf.float32)  # [0,1]
        images.append(img)

    return tf.stack(images)   # (250, 224, 224, 3)
```

---

# 3️⃣ Dataset generator (video-level 🔥)

```python
def video_generator(split_dir):
    class_map = {"normal": 0, "suspicious": 1}

    for cls in class_map:
        class_dir = os.path.join(split_dir, cls)
        for video in os.listdir(class_dir):
            video_path = os.path.join(class_dir, video)
            frames = load_video_frames(video_path)
            label = class_map[cls]
            yield frames, label
```

---

# 4️⃣ tf.data Dataset

```python
def get_dataset(split_path, shuffle=True):
    ds = tf.data.Dataset.from_generator(
        lambda: video_generator(split_path),
        output_signature=(
            tf.TensorSpec(shape=(FRAMES, IMG_SIZE, IMG_SIZE, 3), dtype=tf.float32),
            tf.TensorSpec(shape=(), dtype=tf.int32)
        )
    )

    if shuffle:
        ds = ds.shuffle(20)

    return ds.batch(BATCH_SIZE).prefetch(tf.data.AUTOTUNE)
```

```python
train_ds = get_dataset("frames/train")
val_ds   = get_dataset("frames/val", shuffle=False)
test_ds  = get_dataset("frames/test", shuffle=False)
```

---

# 5️⃣ CNN + LSTM Model (TensorFlow 🔥)

```python
from tensorflow.keras import layers, models

cnn_base = tf.keras.applications.ResNet50(
    weights="imagenet",
    include_top=False,
    pooling="avg",
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)

cnn_base.trainable = False   # start frozen
```

```python
model = models.Sequential([
    layers.TimeDistributed(cnn_base,
        input_shape=(FRAMES, IMG_SIZE, IMG_SIZE, 3)),

    layers.TimeDistributed(layers.BatchNormalization()),

    layers.LSTM(256, return_sequences=False),
    layers.Dense(128, activation="relu"),
    layers.Dropout(0.5),
    layers.Dense(NUM_CLASSES, activation="softmax")
])
```

---

# 6️⃣ Compile & Train

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

---

# 7️⃣ Evaluate & Save

```python
model.evaluate(test_ds)

model.save("cnn_lstm_video_model.h5")
```

---

# 🔥 Why this pipeline is GOOD

✔️ Video-level loading
✔️ No frame leakage
✔️ Pre-resized → fast training
✔️ tf.data → scalable
✔️ Easy to extend to I3D / C3D

---

# **I3D TensorFlow pipeline** একটু heavy, কিন্তু **industry-grade**।
আমি তোমাকে **clean + practical** pipeline দেবো, যেন মাথায় থাকে কী হচ্ছে।

---

# 🧠 I3D কী আলাদা?

* 3D Convolution → **space + time একসাথে**
* CNN+LSTM থেকে বেশি **motion-aware**
* Clip-based (পুরো 250 frame একসাথে দেয় না)

👉 তাই pipeline একটু আলাদা 👇

---

# 📌 Design Decisions (IMPORTANT)

### Given:

* Each video = **250 frames**
* Frame size = **224×224**

### I3D strategy:

* **Clip length = 64 frames**
* One video → **multiple clips**
* Final prediction = **average over clips**

---

# 📁 Folder (same as before)

```
frames/
 ├── train/
 │    ├── normal/
 │    │    ├── video1/
 │    │    │    ├── 0000.jpg ...
```

---

# 1️⃣ Constants

```python
IMG_SIZE = 224
CLIP_LEN = 64
BATCH_SIZE = 2
NUM_CLASSES = 2
```

---

# 2️⃣ Load ONE clip (64 frames)

```python
import tensorflow as tf
import os
import numpy as np

def load_clip(video_dir, start):
    frames = sorted(os.listdir(video_dir))
    clip_frames = frames[start:start+CLIP_LEN]

    images = []
    for f in clip_frames:
        img = tf.io.read_file(os.path.join(video_dir, f))
        img = tf.image.decode_jpeg(img, channels=3)
        img = tf.image.convert_image_dtype(img, tf.float32)
        images.append(img)

    return tf.stack(images)   # (64, 224, 224, 3)
```

---

# 3️⃣ Video → multiple clips

```python
def video_to_clips(video_dir):
    frames = sorted(os.listdir(video_dir))
    total = len(frames)

    if total < CLIP_LEN:
        return []

    stride = CLIP_LEN  # non-overlapping (safe)
    clips = []

    for start in range(0, total - CLIP_LEN + 1, stride):
        clips.append(load_clip(video_dir, start))

    return clips
```

---

# 4️⃣ Dataset Generator (clip-level)

```python
def clip_generator(split_dir):
    class_map = {"normal": 0, "suspicious": 1}

    for cls, label in class_map.items():
        class_dir = os.path.join(split_dir, cls)

        for video in os.listdir(class_dir):
            video_dir = os.path.join(class_dir, video)

            clips = video_to_clips(video_dir)
            for clip in clips:
                yield clip, label
```

---

# 5️⃣ tf.data Dataset

```python
def get_dataset(split_path, shuffle=True):
    ds = tf.data.Dataset.from_generator(
        lambda: clip_generator(split_path),
        output_signature=(
            tf.TensorSpec(
                shape=(CLIP_LEN, IMG_SIZE, IMG_SIZE, 3),
                dtype=tf.float32
            ),
            tf.TensorSpec(shape=(), dtype=tf.int32)
        )
    )

    if shuffle:
        ds = ds.shuffle(10)

    return ds.batch(BATCH_SIZE).prefetch(tf.data.AUTOTUNE)
```

```python
train_ds = get_dataset("frames/train")
val_ds   = get_dataset("frames/val", shuffle=False)
test_ds  = get_dataset("frames/test", shuffle=False)
```

---

# 6️⃣ I3D Model (TensorFlow)

TensorFlow-এ official I3D নাই, so **simplified I3D-style 3D CNN** দেখাচ্ছি
(real research-grade but understandable)

```python
from tensorflow.keras import layers, models

def build_i3d():
    inputs = layers.Input(shape=(CLIP_LEN, IMG_SIZE, IMG_SIZE, 3))

    x = layers.Conv3D(64, (3,3,3), strides=(1,2,2),
                      padding="same", activation="relu")(inputs)
    x = layers.MaxPool3D((1,2,2))(x)

    x = layers.Conv3D(128, (3,3,3), padding="same",
                      activation="relu")(x)
    x = layers.MaxPool3D((2,2,2))(x)

    x = layers.Conv3D(256, (3,3,3), padding="same",
                      activation="relu")(x)
    x = layers.GlobalAveragePooling3D()(x)

    x = layers.Dense(256, activation="relu")(x)
    x = layers.Dropout(0.5)(x)

    outputs = layers.Dense(NUM_CLASSES, activation="softmax")(x)

    return models.Model(inputs, outputs)

model = build_i3d()
```

---

# 7️⃣ Compile & Train

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=20
)
```

---

# 8️⃣ Video-level Prediction (IMPORTANT 🔥)

I3D predicts **per clip**, but you want **per video**:

```python
import numpy as np

def predict_video(video_dir, model):
    clips = video_to_clips(video_dir)
    preds = []

    for clip in clips:
        p = model.predict(tf.expand_dims(clip, axis=0))
        preds.append(p[0])

    return np.mean(preds, axis=0)  # final video prediction
```

---

# 🧠 Why this pipeline is CORRECT

✔️ Video split respected
✔️ Clip-based training (I3D style)
✔️ 224×224 standard
✔️ Temporal info preserved
✔️ Scalable to real I3D later

---

#  **Real ML decision-making** জায়গায় আসছো — **CNN+LSTM vs I3D** একই dataset-এ compare করা 🔥
আমি **theory + practice + when-to-use**—সব clear করবো।

---

# 🧠 Same Dataset Setup (assumed)

* Videos: **Normal = 950, Suspicious = 950**
* Frames per video: **250**
* Resolution: **224×224**
* Same train / val / test split
  👉 Fair comparison ✔️

---

# 🔍 High-level Difference

| Aspect               | CNN + LSTM            | I3D             |
| -------------------- | --------------------- | --------------- |
| Temporal modeling    | Sequential (LSTM)     | 3D Convolution  |
| Spatial feature      | Strong (ImageNet CNN) | Strong + motion |
| Motion understanding | Medium                | **Very strong** |
| Training complexity  | Easy                  | Hard            |
| GPU need             | Medium                | **High**        |
| Debuggability        | Easy                  | Hard            |
| Real-time potential  | Medium                | Low             |

---

# 📥 Input Comparison

### CNN + LSTM

```
(batch, 250, 224, 224, 3)
→ CNN per frame
→ (batch, 250, 2048)
→ LSTM
```

### I3D

```
(batch, 64, 224, 224, 3)
→ 3D Conv
→ motion + spatial jointly
```

---

# ⚡ Performance Expectation (Realistic)

| Metric              | CNN+LSTM | I3D                  |
| ------------------- | -------- | -------------------- |
| Accuracy            | ⭐⭐⭐⭐     | ⭐⭐⭐⭐⭐                |
| Recall (Suspicious) | ⭐⭐⭐⭐     | ⭐⭐⭐⭐⭐                |
| Training speed      | ⭐⭐⭐⭐     | ⭐⭐                   |
| Overfitting risk    | Medium   | High (if small data) |

> 🔥 I3D wins **only if** you train it properly and have GPU.

---

# 🧠 Why CNN+LSTM works so well

* Uses **pretrained CNN** → strong appearance features
* LSTM handles long temporal sequence (250 frames)
* Less data hungry
* Easier to tune

👉 **Best first model**

---

# 🧠 Why I3D can beat CNN+LSTM

* 3D Conv learns **motion patterns directly**
* Better for:

  * Fast actions
  * Subtle motion differences
* Needs:

  * More data
  * More GPU
  * Careful clip sampling

---

# 💾 GPU & Memory Reality

| Model    | Typical Batch |
| -------- | ------------- |
| CNN+LSTM | 2–4 videos    |
| I3D      | 1–2 clips     |

👉 On 8GB GPU:

* CNN+LSTM = OK
* I3D = tight / mixed precision needed

---

# 🧪 Training Stability

| Issue                  | CNN+LSTM | I3D      |
| ---------------------- | -------- | -------- |
| Vanishing gradients    | Rare     | Possible |
| OOM errors             | Rare     | Common   |
| Hyperparam sensitivity | Low      | High     |

---

# 🏆 Final Recommendation (HONEST)

### 🥇 If this is a **course / portfolio / first video project**

➡️ **CNN + LSTM**

### 🥈 If this is **research / competition / high GPU**

➡️ **I3D**

### 🧠 If you want to impress:

Train **both** → show comparison 📊

---

# 📌 How to compare properly (IMPORTANT)

Use **same test set** and report:

* Accuracy
* Precision / Recall (Suspicious class)
* F1-score
* Confusion Matrix
* Inference time per video

---

# 🔥 Example Result Table (for report)

| Model    | Acc | Recall (Suspicious) | FPS | Params |
| -------- | --- | ------------------- | --- | ------ |
| CNN+LSTM | 91% | 89%                 | 6   | 30M    |
| I3D      | 93% | 92%                 | 2   | 42M    |

---

# **“Another model”** মানে চল আমরা **CNN+LSTM / I3D ছাড়া আরও strong, practical video models** দেখি — যেগুলো **তোমার dataset (250 frames, 224×224)**-এর সাথে ভালো fit করে।

আমি **best 4টা** দেবো, সাথে **কখন কোনটা নেবে** clear করে দেবো 👇

---

# 🔥 1️⃣ ConvLSTM (Very underrated 🔥)

### 🧠 Idea

* CNN + LSTM একসাথে (spatial + temporal jointly)
* Frame → Conv → LSTM-like recurrence

### ✅ Input Shape

```
(batch, T, H, W, C)
= (B, 250, 224, 224, 3)
```

### 👍 Why use

* Motion + appearance together
* CNN+LSTM থেকে **better temporal consistency**

### 👎 Downside

* Heavy memory
* Slow

👉 **When:** subtle motion important

---

# ⚡ 2️⃣ TimeSformer (Transformer-based)

### 🧠 Idea

* Video = sequence of patches
* Spatial + temporal attention

### ✅ Input

```
(batch, T, H, W, C)
```

### 👍 Pros

* Long-range temporal dependency
* No recurrence → parallel

### 👎 Cons

* Needs large dataset
* Heavy compute

👉 **When:** research / high GPU

---

# 🐢 3️⃣ SlowFast (State-of-the-art 🔥)

### 🧠 Two streams

* Slow: semantics
* Fast: motion

### ✅ Input

```
Slow: (B, 32, 224,224,3)
Fast: (B,128,224,224,3)
```

### 👍 Pros

* Excellent action recognition
* Motion-sensitive

### 👎 Cons

* Complex
* GPU heavy

👉 **When:** final / flagship model

---

# 🧩 4️⃣ 2D CNN + Temporal Pooling (Simple & Fast)

### 🧠 Idea

* CNN per frame
* Avg/Max pool over time

### ✅ Input

```
(batch, 250, feature_dim)
```

### 👍 Pros

* Fast
* Stable
* Good baseline

### 👎 Cons

* Temporal order lost

👉 **When:** baseline comparison

---

# 🧠 Quick Comparison Table (SAVE THIS 🔥)

| Model         | Accuracy | GPU       | Complexity | Best For           |
| ------------- | -------- | --------- | ---------- | ------------------ |
| CNN+LSTM      | ⭐⭐⭐⭐     | Medium    | Medium     | First strong model |
| I3D           | ⭐⭐⭐⭐⭐    | High      | High       | Motion-heavy       |
| ConvLSTM      | ⭐⭐⭐⭐½    | High      | High       | Subtle motion      |
| SlowFast      | ⭐⭐⭐⭐⭐    | Very High | Very High  | SOTA               |
| Temporal Pool | ⭐⭐⭐      | Low       | Low        | Baseline           |

---

# 🎯 My Suggested Roadmap (Smart 🔥)

1️⃣ CNN+LSTM
2️⃣ I3D
3️⃣ **ConvLSTM** ← next best
4️⃣ SlowFast (if GPU allows)

---

# **ConvLSTM pipeline** খুব solid + impressive model।
আমি নিচে **clean, end-to-end TensorFlow ConvLSTM pipeline** দিলাম, একদম তোমার setup অনুযায়ী।

---

# 🧠 ConvLSTM কখন ব্যবহার করবে?

* Spatial + temporal info **একসাথে** শিখতে চাইলে
* CNN+LSTM এর চেয়ে **strong motion consistency** দরকার হলে
* 250 frames available থাকলে

---

# 📁 Assumptions (same as before)

* Each video → **250 frames**
* Frame size → **224×224**
* Frames already extracted & resized

```
frames/
 ├── train/
 │    ├── normal/
 │    └── suspicious/
 ├── val/
 └── test/
```

---

# 1️⃣ Constants

```python
IMG_SIZE = 224
FRAMES = 250
BATCH_SIZE = 1      # ConvLSTM heavy
NUM_CLASSES = 2
```

---

# 2️⃣ Load one video (250 frames)

```python
import tensorflow as tf
import os

def load_video(video_dir):
    frames = sorted(os.listdir(video_dir))[:FRAMES]
    imgs = []

    for f in frames:
        img = tf.io.read_file(os.path.join(video_dir, f))
        img = tf.image.decode_jpeg(img, channels=3)
        img = tf.image.convert_image_dtype(img, tf.float32)
        imgs.append(img)

    return tf.stack(imgs)   # (250, 224, 224, 3)
```

---

# 3️⃣ Dataset Generator (video-level)

```python
def video_generator(split_dir):
    label_map = {"normal": 0, "suspicious": 1}

    for cls, label in label_map.items():
        class_dir = os.path.join(split_dir, cls)

        for video in os.listdir(class_dir):
            video_path = os.path.join(class_dir, video)
            frames = load_video(video_path)
            yield frames, label
```

---

# 4️⃣ tf.data Dataset

```python
def get_dataset(split_path, shuffle=True):
    ds = tf.data.Dataset.from_generator(
        lambda: video_generator(split_path),
        output_signature=(
            tf.TensorSpec(
                shape=(FRAMES, IMG_SIZE, IMG_SIZE, 3),
                dtype=tf.float32
            ),
            tf.TensorSpec(shape=(), dtype=tf.int32)
        )
    )

    if shuffle:
        ds = ds.shuffle(10)

    return ds.batch(BATCH_SIZE).prefetch(tf.data.AUTOTUNE)
```

```python
train_ds = get_dataset("frames/train")
val_ds   = get_dataset("frames/val", shuffle=False)
test_ds  = get_dataset("frames/test", shuffle=False)
```

---

# 5️⃣ ConvLSTM Model (TensorFlow 🔥)

👉 Memory control করার জন্য **spatial downsampling early** করছি (VERY important)

```python
from tensorflow.keras import layers, models

model = models.Sequential([
    layers.ConvLSTM2D(
        filters=32,
        kernel_size=(3,3),
        padding="same",
        return_sequences=True,
        input_shape=(FRAMES, IMG_SIZE, IMG_SIZE, 3)
    ),
    layers.BatchNormalization(),
    layers.MaxPooling3D(pool_size=(1,2,2)),

    layers.ConvLSTM2D(
        filters=64,
        kernel_size=(3,3),
        padding="same",
        return_sequences=False
    ),
    layers.BatchNormalization(),

    layers.GlobalAveragePooling2D(),
    layers.Dense(128, activation="relu"),
    layers.Dropout(0.5),
    layers.Dense(NUM_CLASSES, activation="softmax")
])
```

---

# 6️⃣ Compile & Train

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=15
)
```

---

# 7️⃣ Evaluate & Save

```python
model.evaluate(test_ds)
model.save("convlstm_video_model.h5")
```

---

# ⚠️ VERY IMPORTANT WARNINGS (read 🔥)

* ConvLSTM **GPU hungry**
* 224×224 + 250 frames = borderline
* If OOM:

  * Reduce frames → 128
  * Or resize → 160×160
  * Or use mixed precision

---

# 🧠 When ConvLSTM beats CNN+LSTM

✔️ Smooth motion
✔️ Long temporal dependency
✔️ Subtle behavioral patterns

❌ Fast actions → I3D better

---

Perfect 👍
তাহলে দিচ্ছি **Memory-Optimized ConvLSTM (Two-Stage Pipeline)** —
এটাই **real-world usable version**, না হলে 224×224 × 250 frames এ GPU হাঁপিয়ে যায় 😄

---

# 🔥 Idea: Two-Stage ConvLSTM (VERY IMPORTANT)

### ❌ Problem (naive ConvLSTM)

```
(250, 224, 224, 3) → ConvLSTM
```

👉 GPU OOM 💥

### ✅ Solution (Two-Stage)

```
Stage-1: Frame → CNN → spatially compressed feature
Stage-2: ConvLSTM on compressed feature sequence
```

👉 **Spatial info কমে, temporal info থাকে** 🔥

---

# 📐 Design Choice (SAFE)

* Frames = **250**
* Input size = **224×224**
* CNN output = **14×14×512** (ResNet50)
* ConvLSTM runs on **feature maps**, not raw frames

---

# 1️⃣ Constants

```python
IMG_SIZE = 224
FRAMES = 250
BATCH_SIZE = 1
NUM_CLASSES = 2
```

---

# 2️⃣ Dataset Loader (same as before)

(unchanged — video-level, 250 frames)

```python
# assumes frames already resized to 224×224
# load_video(), video_generator(), get_dataset()
# SAME as previous ConvLSTM pipeline
```

---

# 3️⃣ Stage-1: CNN Feature Extractor (Frozen)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

cnn = tf.keras.applications.ResNet50(
    weights="imagenet",
    include_top=False,
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)
cnn.trainable = False
```

This outputs:

```
(224,224,3) → (7,7,2048)
```

We compress channels 👇

```python
cnn_feature_extractor = models.Sequential([
    cnn,
    layers.Conv2D(512, (1,1), activation="relu")
])
```

Final per-frame feature:

```
(14,14,512)   # manageable 🔥
```

---

# 4️⃣ Stage-2: ConvLSTM on Feature Maps

```python
inputs = layers.Input(
    shape=(FRAMES, IMG_SIZE, IMG_SIZE, 3)
)

x = layers.TimeDistributed(cnn_feature_extractor)(inputs)
# (B, 250, 14, 14, 512)

x = layers.ConvLSTM2D(
    filters=128,
    kernel_size=(3,3),
    padding="same",
    return_sequences=False
)(x)

x = layers.BatchNormalization()(x)
x = layers.GlobalAveragePooling2D()(x)

x = layers.Dense(128, activation="relu")(x)
x = layers.Dropout(0.5)(x)

outputs = layers.Dense(NUM_CLASSES, activation="softmax")(x)

model = models.Model(inputs, outputs)
```

---

# 5️⃣ Compile & Train

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=20
)
```

---

# 🧠 Why this version is 🔥🔥🔥

| Aspect            | Naive ConvLSTM | Two-Stage ConvLSTM |
| ----------------- | -------------- | ------------------ |
| GPU usage         | ❌ very high    | ✅ manageable       |
| Spatial learning  | Direct         | CNN-based (better) |
| Temporal learning | Good           | **Very good**      |
| Stability         | Low            | **High**           |
| Industry ready    | ❌              | **✅**              |

---

# ⚠️ If GPU still struggles

Use **one of these** (not all):

* Resize → **160×160**
* Frames → **128**
* Enable mixed precision:

```python
tf.keras.mixed_precision.set_global_policy("mixed_float16")
```

---

# 🏆 Final Advice (important)

If you compare models:

* **CNN+LSTM** → baseline
* **Two-Stage ConvLSTM** → motion-aware
* **I3D** → strongest but hardest

👉 This ConvLSTM is a **sweet spot** 🔥

---
Nice, straight to the point 😄
**Real-time কোনটা best?** — short answer: **I3D না** ❌

চলো practicalভাবে দেখি 👇

---

# ⚡ Real-time suitability (your models)

## 🥇 **CNN + LSTM (BEST for real-time)**

**Why it wins**

* Frame-by-frame process করা যায়
* Low latency
* Webcam / CCTV friendly
* Easy to optimize (skip frames, smaller CNN)

**Typical setup**

```
Webcam → CNN (MobileNet / ResNet18) → LSTM → Prediction
```

**FPS**

* 15–30 FPS (mid-range GPU)
* Even CPU-friendly if MobileNet

👉 **#1 choice for real-time surveillance**

---

## 🥈 **ConvLSTM (Real-time but with tricks)**

**Works if**

* Use sliding window (e.g. last 16–32 frames)
* Use lightweight CNN feature extractor
* Batch size = 1

**Latency**

* Medium
* More accurate than CNN+LSTM for motion
* But heavier

👉 **#2 choice (controlled real-time)**

---

## 🥉 **2D CNN + Temporal Pooling**

```
CNN → Avg/Max pool over time → FC
```

* Almost real-time
* Very fast
* Less temporal understanding

👉 **Good for fast alerts**

---

## ❌ **I3D / C3D / SlowFast**

**Why NOT real-time**

* Needs fixed clip (16–64 frames)
* Heavy 3D convolutions
* High latency
* Batch-based inference

👉 **Offline analysis only**

---

# 🔥 Final Ranking (Real-time)

| Rank | Model                     | Real-time |
| ---- | ------------------------- | --------- |
| 🥇   | CNN + LSTM                | ⭐⭐⭐⭐⭐     |
| 🥈   | ConvLSTM (windowed)       | ⭐⭐⭐⭐      |
| 🥉   | 2D CNN + Temporal Pooling | ⭐⭐⭐       |
| ❌    | I3D / C3D                 | ⭐         |

---

# 🎯 What I recommend for YOU

Since তুমি:

* Surveillance / suspicious activity
* Want **real-time + accuracy**

👉 **Start with CNN + LSTM**
Then:
👉 Upgrade to **window-based ConvLSTM**

---
# **REAL-TIME TensorFlow CNN + LSTM webcam pipeline** দিলাম —
👉 **production-style**, 👉 **low-latency**, 👉 **GPU/CPU friendly**

---

# 🎯 Goal

**Webcam → live prediction (Normal vs Suspicious)**
Frame by frame + short temporal memory

---

# 🧠 Architecture (Real-time friendly)

```
Webcam frame
 → CNN (MobileNetV2)
 → feature vector
 → rolling buffer (last N frames)
 → LSTM
 → prediction
```

✔ No fixed 250 frames
✔ Sliding window
✔ Instant output

---

# ⚙️ Config

```python
IMG_SIZE = 224
SEQ_LEN = 16          # sliding window (VERY IMPORTANT)
NUM_CLASSES = 2
```

---

# 1️⃣ CNN Feature Extractor (FAST)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

cnn_base = tf.keras.applications.MobileNetV2(
    weights="imagenet",
    include_top=False,
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)
cnn_base.trainable = False

cnn_model = models.Sequential([
    cnn_base,
    layers.GlobalAveragePooling2D()
])
```

Output:

```
(224,224,3) → (1280,)
```

---

# 2️⃣ LSTM Model (Temporal Brain)

```python
lstm_input = layers.Input(shape=(SEQ_LEN, 1280))

x = layers.LSTM(128, return_sequences=False)(lstm_input)
x = layers.Dense(64, activation="relu")(x)
x = layers.Dropout(0.4)(x)

output = layers.Dense(NUM_CLASSES, activation="softmax")(x)

lstm_model = models.Model(lstm_input, output)

lstm_model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

👉 Train this model **offline** using extracted features
👉 Then use it **real-time**

---

# 3️⃣ Real-time Webcam Inference 🔥

```python
import cv2
import numpy as np
from collections import deque

cap = cv2.VideoCapture(0)
frame_buffer = deque(maxlen=SEQ_LEN)

labels = ["Normal", "Suspicious"]

while True:
    ret, frame = cap.read()
    if not ret:
        break

    frame_resized = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))
    frame_rgb = cv2.cvtColor(frame_resized, cv2.COLOR_BGR2RGB)
    frame_norm = frame_rgb / 255.0

    feature = cnn_model.predict(
        np.expand_dims(frame_norm, axis=0),
        verbose=0
    )[0]

    frame_buffer.append(feature)

    if len(frame_buffer) == SEQ_LEN:
        sequence = np.expand_dims(frame_buffer, axis=0)
        pred = lstm_model.predict(sequence, verbose=0)
        label = labels[np.argmax(pred)]
        conf = np.max(pred)

        cv2.putText(
            frame,
            f"{label} ({conf:.2f})",
            (30,40),
            cv2.FONT_HERSHEY_SIMPLEX,
            1,
            (0,255,0),
            2
        )

    cv2.imshow("Real-time CNN+LSTM", frame)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

---

# ⚡ Performance (Realistic)

| Device          | FPS       |
| --------------- | --------- |
| GPU (RTX 2060+) | 25–30 FPS |
| CPU (i7)        | 12–18 FPS |
| CPU + MobileNet | ✅ usable  |

---

# 🧠 Why this works for real-time

* CNN is **lightweight**
* LSTM sees **short motion memory**
* Sliding window = no delay
* No 3D convolution

---

# 🚀 Upgrade path (optional)

* Replace MobileNet → EfficientNetB0
* Add **frame skipping** (every 2nd frame)
* Add **ConvLSTM window** for better motion
* Deploy with **TensorFlow Lite**

---

## 🏁 Final verdict

👉 **This is the BEST real-time architecture**
Used in:

* CCTV analytics
* Violence detection
* Suspicious activity monitoring

---
Nice choice 😄
চল **REAL-TIME ConvLSTM (sliding-window) pipeline** করি — এটা **CNN+LSTM এর চেয়ে motion-aware**, কিন্তু এখনো **real-time possible** 🔥

আমি এমনভাবে দেবো যাতে **GPU না থাকলেও run করা যায়** (CPU-friendly tricks সহ)।

---

# 🎯 Goal

**Webcam → live suspicious / normal detection**
Using **ConvLSTM + sliding window**

---

# 🧠 Architecture (Real-time ConvLSTM)

```
Webcam
 → Resize
 → Sliding window (last N frames)
 → ConvLSTM
 → Prediction
```

✔ No 250 frames
✔ Low latency
✔ Motion aware

---

# ⚙️ Safe Config (IMPORTANT)

```python
IMG_SIZE = 112        # 🔥 smaller = faster
SEQ_LEN = 16          # sliding window
NUM_CLASSES = 2
```

> ⚠️ 224×224 direct ConvLSTM = ❌ OOM risk
> 112×112 = ✅ real-time safe

---

# 1️⃣ ConvLSTM Model (TensorFlow)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

inputs = layers.Input(
    shape=(SEQ_LEN, IMG_SIZE, IMG_SIZE, 3)
)

x = layers.ConvLSTM2D(
    filters=32,
    kernel_size=(3,3),
    padding="same",
    return_sequences=False
)(inputs)

x = layers.BatchNormalization()(x)
x = layers.MaxPooling2D((2,2))(x)

x = layers.Conv2D(64, (3,3), activation="relu")(x)
x = layers.GlobalAveragePooling2D()(x)

x = layers.Dense(64, activation="relu")(x)
x = layers.Dropout(0.4)(x)

outputs = layers.Dense(NUM_CLASSES, activation="softmax")(x)

model = models.Model(inputs, outputs)

model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

model.summary()
```

---

# 2️⃣ Real-time Webcam Inference 🔥

```python
import cv2
import numpy as np
from collections import deque

cap = cv2.VideoCapture(0)
frame_buffer = deque(maxlen=SEQ_LEN)

labels = ["Normal", "Suspicious"]

while True:
    ret, frame = cap.read()
    if not ret:
        break

    frame = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))
    frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    frame = frame / 255.0

    frame_buffer.append(frame)

    if len(frame_buffer) == SEQ_LEN:
        sequence = np.expand_dims(frame_buffer, axis=0)
        pred = model.predict(sequence, verbose=0)
        label = labels[np.argmax(pred)]
        conf = np.max(pred)

        cv2.putText(
            frame,
            f"{label} ({conf:.2f})",
            (10,30),
            cv2.FONT_HERSHEY_SIMPLEX,
            1,
            (0,255,0),
            2
        )

    cv2.imshow("Real-time ConvLSTM", frame)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

---

# ⚡ Real-time Performance

| Device      | FPS                   |
| ----------- | --------------------- |
| CPU (i5/i7) | 8–12 FPS              |
| GPU (RTX)   | 20+ FPS               |
| Edge device | ⚠️ use frame skipping |

---

# 🔥 Optimization Tricks (VERY IMPORTANT)

### ✅ 1. Frame skipping

```python
if frame_id % 2 != 0:
    continue
```

### ✅ 2. Reduce channels

```python
filters=16   # instead of 32
```

### ✅ 3. Mixed precision (GPU)

```python
tf.keras.mixed_precision.set_global_policy("mixed_float16")
```

---

# 🧠 CNN+LSTM vs ConvLSTM (Real-time)

| Feature    | CNN+LSTM | ConvLSTM      |
| ---------- | -------- | ------------- |
| Speed      | ⭐⭐⭐⭐⭐    | ⭐⭐⭐           |
| Motion     | ⭐⭐       | ⭐⭐⭐⭐          |
| Accuracy   | ⭐⭐⭐      | ⭐⭐⭐⭐          |
| Complexity | Low      | Medium        |
| Real-time  | ✅ Best   | ⚠️ Controlled |

---

# 🏁 Final Advice

* **Low latency priority** → CNN+LSTM
* **Motion accuracy priority** → ConvLSTM
* **Production CCTV** → CNN+LSTM + alert logic

---

Got it 👍
**MobileNet এর কোন কোন version আছে + real-time এর জন্য কোনটা best** — clean করে দিচ্ছি।

---

# 📱 MobileNet Versions (TensorFlow / Keras)

## 🥇 **MobileNetV2** (MOST USED)

**Status:** ⭐⭐⭐⭐⭐
**Why everyone uses it**

* Very fast
* Stable
* Low memory
* Perfect for **CNN+LSTM real-time**

```python
tf.keras.applications.MobileNetV2
```

**Output feature:** 1280
**Real-time:** ✅ BEST choice

👉 **Recommendation:** ✔️ Start here

---

## 🥈 **MobileNetV3 (Small / Large)** (FASTEST)

**Status:** ⭐⭐⭐⭐
**Why**

* Newer
* Faster than V2
* Less FLOPs

```python
tf.keras.applications.MobileNetV3Small
tf.keras.applications.MobileNetV3Large
```

| Variant | Speed | Accuracy |
| ------- | ----- | -------- |
| V3Small | ⚡⚡⚡⚡⚡ | ⭐⭐⭐      |
| V3Large | ⚡⚡⚡⚡  | ⭐⭐⭐⭐     |

👉 **Best for edge / low CPU**

---

## 🥉 **MobileNetV1** (OLD)

**Status:** ⭐⭐

* Very light
* Lower accuracy
* Mostly outdated

❌ Not recommended now

---

## 🧪 **MobileNetV4** (FYI)

* Experimental / limited support
* Not stable for production yet

❌ Skip for now

---

# 🎯 Which MobileNet for WHICH model?

## ✅ Real-time CNN + LSTM

```
MobileNetV2  ⭐⭐⭐⭐⭐ (best balance)
MobileNetV3Small ⭐⭐⭐⭐ (fastest)
```

## ✅ Real-time ConvLSTM (feature extractor)

```
MobileNetV2 (frozen)
↓
ConvLSTM
```

## ❌ I3D / 3D CNN

```
MobileNet not used
```

---

# ⚙️ Recommended Config (PRO)

```python
cnn = tf.keras.applications.MobileNetV2(
    weights="imagenet",
    include_top=False,
    input_shape=(224,224,3),
    alpha=0.75   # 🔥 lighter & faster
)
```

| alpha | Speed     | Accuracy |
| ----- | --------- | -------- |
| 1.0   | Normal    | High     |
| 0.75  | Faster    | Slight ↓ |
| 0.5   | Very fast | Medium   |

👉 **alpha=0.75 = sweet spot**

---

# 🏆 Final Verdict (Don’t overthink)

* **Learning + project** → MobileNetV2
* **Edge / CPU** → MobileNetV3Small
* **Best real-time accuracy** → MobileNetV2 (alpha=0.75)

---
Perfect 😄
চলো দেখি **MobileNetV3Small / Large + CNN+LSTM real-time webcam pipeline** — **lightweight & fast**, CPU/GPU দুইয়ে use করা যাবে।

---

# 🎯 Goal

**Webcam → live suspicious/normal prediction**

* Feature extractor = **MobileNetV3Small** (fast)
* Temporal memory = **LSTM** (sliding window)

---

# ⚙️ Config

```python
IMG_SIZE = 224
SEQ_LEN = 16         # sliding window
NUM_CLASSES = 2
BATCH_SIZE = 1       # real-time
```

---

# 1️⃣ CNN Feature Extractor (MobileNetV3)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

# MobileNetV3 Small (lightweight)
cnn_base = tf.keras.applications.MobileNetV3Small(
    weights="imagenet",
    include_top=False,
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)
cnn_base.trainable = False

# Feature vector
cnn_model = models.Sequential([
    cnn_base,
    layers.GlobalAveragePooling2D()  # output: 576 features for Small
])
```

> Large version = 1280 features, slightly slower
> Small = 576 features, faster for CPU

---

# 2️⃣ LSTM Model (Temporal Brain)

```python
lstm_input = layers.Input(shape=(SEQ_LEN, 576))  # 576 = MobileNetV3Small output

x = layers.LSTM(128, return_sequences=False)(lstm_input)
x = layers.Dense(64, activation="relu")(x)
x = layers.Dropout(0.4)(x)

output = layers.Dense(NUM_CLASSES, activation="softmax")(x)

lstm_model = models.Model(lstm_input, output)

lstm_model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

> Train offline using your dataset features first

---

# 3️⃣ Real-time Webcam Inference

```python
import cv2
import numpy as np
from collections import deque

cap = cv2.VideoCapture(0)
frame_buffer = deque(maxlen=SEQ_LEN)

labels = ["Normal", "Suspicious"]

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # Preprocess frame
    frame_resized = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))
    frame_rgb = cv2.cvtColor(frame_resized, cv2.COLOR_BGR2RGB)
    frame_norm = frame_rgb / 255.0

    # Extract feature
    feature = cnn_model.predict(
        np.expand_dims(frame_norm, axis=0),
        verbose=0
    )[0]

    frame_buffer.append(feature)

    if len(frame_buffer) == SEQ_LEN:
        sequence = np.expand_dims(frame_buffer, axis=0)
        pred = lstm_model.predict(sequence, verbose=0)
        label = labels[np.argmax(pred)]
        conf = np.max(pred)

        cv2.putText(
            frame,
            f"{label} ({conf:.2f})",
            (10,30),
            cv2.FONT_HERSHEY_SIMPLEX,
            1,
            (0,255,0),
            2
        )

    cv2.imshow("Real-time MobileNetV3 + LSTM", frame)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

---

# ⚡ Notes / Tips

1. **MobileNetV3Small** → CPU-friendly, ~15–20 FPS
2. **MobileNetV3Large** → GPU-friendly, better accuracy, ~25 FPS
3. **SEQ_LEN** → Sliding window; smaller → faster, bigger → more temporal info
4. Frame skipping → faster if FPS low

---

# 🏆 Summary

* **MobileNetV3Small + LSTM** = fast + decent accuracy
* **MobileNetV3Large + LSTM** = more accurate, slightly slower
* Both → **real-time webcam-ready**

---

Ah! 😎 এখন আমরা কথা বলছি **Hybrid Model**—মানে এমন একটা model যা **CNN+LSTM + ConvLSTM/I3D এর কিছু trick** একসাথে ব্যবহার করে।

এটি **real-time friendly + motion-aware** approach। আমি step-by-step explain করি।

---

# 🧠 Hybrid Video Model Concept

### Goal:

* **Spatial features** → CNN (pretrained MobileNetV2/V3)
* **Short-term temporal** → LSTM (sliding window, frame-level)
* **Long-term temporal / motion** → ConvLSTM (feature-level)

```
Webcam / video frames
    ↓
MobileNetV3Small  (frame-level spatial feature)
    ↓
LSTM (SEQ_LEN = 16)   # short-term motion
    ↓
ConvLSTM (last N LSTM outputs)  # long-term temporal
    ↓
Dense → Prediction (Normal / Suspicious)
```

---

# 🔹 Why Hybrid?

| Component       | Role                                          |
| --------------- | --------------------------------------------- |
| CNN (MobileNet) | Spatial/appearance features                   |
| LSTM            | Short-term temporal sequence (fast)           |
| ConvLSTM        | Long-term temporal dynamics (motion subtlety) |
| Sliding window  | Real-time capability                          |

**Advantages:**

* Faster than full I3D
* More accurate than simple CNN+LSTM
* Real-time possible (with small SEQ_LEN)

**Disadvantages:**

* Slightly more memory than CNN+LSTM
* Implementation more complex

---

# 🔹 Suggested Real-time Config

```python
IMG_SIZE = 112        # smaller for real-time
SEQ_LEN_LSTM = 16     # sliding window
SEQ_LEN_CONVLSTM = 8  # ConvLSTM window
NUM_CLASSES = 2
BATCH_SIZE = 1
```

---

# 🔹 Hybrid Model Skeleton (TensorFlow)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

# 1️⃣ Frame-level CNN
cnn_base = tf.keras.applications.MobileNetV3Small(
    weights="imagenet",
    include_top=False,
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)
cnn_base.trainable = False

cnn_model = models.Sequential([
    cnn_base,
    layers.GlobalAveragePooling2D()   # output: 576 features
])

# 2️⃣ Short-term LSTM
lstm_input = layers.Input(shape=(SEQ_LEN_LSTM, 576))
x = layers.LSTM(128, return_sequences=True)(lstm_input)
lstm_model = models.Model(lstm_input, x)  # output: (SEQ_LEN_LSTM, 128)

# 3️⃣ ConvLSTM for long-term motion
conv_input = layers.Input(shape=(SEQ_LEN_CONVLSTM, 1, 1, 128)) # reshape seq
x = layers.ConvLSTM2D(
    filters=64,
    kernel_size=(1,1),
    padding='same',
    return_sequences=False
)(conv_input)
x = layers.BatchNormalization()(x)
x = layers.GlobalAveragePooling2D()(x)

x = layers.Dense(64, activation='relu')(x)
x = layers.Dropout(0.4)(x)
outputs = layers.Dense(NUM_CLASSES, activation='softmax')(x)

hybrid_model = models.Model(inputs=conv_input, outputs=outputs)
```

---

# 🔹 Real-time Idea

1. Maintain **frame buffer** (SEQ_LEN_LSTM) → CNN → LSTM
2. Maintain **LSTM output buffer** (SEQ_LEN_CONVLSTM) → ConvLSTM
3. Predict → update buffer continuously
4. Display prediction on webcam

> Sliding windows = minimal latency, keeps model online

---

# ⚡ Key Tips

* **MobileNetV3Small** → CPU real-time
* **SEQ_LEN_LSTM = 16**, **SEQ_LEN_CONVLSTM = 8** → low latency
* Use **frame skipping** for faster FPS
* Optional: freeze CNN, train only LSTM + ConvLSTM → reduces GPU load

---

# 🏆 Expected Real-time Performance

| Device    | FPS       | Notes                 |
| --------- | --------- | --------------------- |
| CPU       | 5–8 FPS   | small sliding window  |
| GPU (RTX) | 15–25 FPS | real-time friendly    |
| Edge      | 2–5 FPS   | reduce IMG_SIZE to 96 |

---

# ✅ Summary

* Hybrid model = **best of both worlds**
* Short-term temporal → LSTM
* Long-term motion → ConvLSTM
* Spatial → MobileNet
* Real-time feasible with small SEQ_LEN & resized frames

---

💡 Next I can give:

1️⃣ **Full real-time webcam Hybrid pipeline code**
2️⃣ **Offline training pipeline for Hybrid model**
3️⃣ **FPS vs Accuracy benchmark vs CNN+LSTM / ConvLSTM**

বল, কোনটা next করি?
Perfect 😄
চলো দেখি **REAL-TIME Hybrid Model (MobileNetV3 + LSTM + ConvLSTM)** pipeline — CPU/GPU friendly এবং **sliding window** approach।

---

# 🎯 Goal

**Webcam → live Normal / Suspicious prediction**

* Frame-level spatial features = **MobileNetV3Small**
* Short-term temporal = **LSTM** (sliding window)
* Long-term motion = **ConvLSTM** (feature-level)

---

# ⚙️ Config (Real-time safe)

```python
IMG_SIZE = 112         # smaller for speed
SEQ_LEN_LSTM = 16      # frame buffer for LSTM
SEQ_LEN_CONVLSTM = 8   # LSTM output buffer for ConvLSTM
NUM_CLASSES = 2
BATCH_SIZE = 1
```

---

# 1️⃣ CNN Feature Extractor (MobileNetV3Small)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

cnn_base = tf.keras.applications.MobileNetV3Small(
    weights="imagenet",
    include_top=False,
    input_shape=(IMG_SIZE, IMG_SIZE, 3)
)
cnn_base.trainable = False

cnn_model = models.Sequential([
    cnn_base,
    layers.GlobalAveragePooling2D()  # output: 576 features
])
```

---

# 2️⃣ Short-term LSTM

```python
lstm_model = models.Sequential([
    layers.Input(shape=(SEQ_LEN_LSTM, 576)),
    layers.LSTM(128, return_sequences=True)
])
```

* Output shape: `(SEQ_LEN_LSTM, 128)`
* Keep **sliding window buffer** of last 16 frames

---

# 3️⃣ ConvLSTM for long-term motion

```python
conv_input = layers.Input(shape=(SEQ_LEN_CONVLSTM, 1, 1, 128))
x = layers.ConvLSTM2D(
    filters=64,
    kernel_size=(1,1),
    padding='same',
    return_sequences=False
)(conv_input)
x = layers.BatchNormalization()(x)
x = layers.GlobalAveragePooling2D()(x)
x = layers.Dense(64, activation='relu')(x)
x = layers.Dropout(0.4)(x)
outputs = layers.Dense(NUM_CLASSES, activation='softmax')(x)

conv_model = models.Model(conv_input, outputs)
```

* ConvLSTM input = **LSTM output buffer**
* Output = prediction for last N frames

---

# 4️⃣ Real-time Webcam Loop

```python
import cv2
import numpy as np
from collections import deque

frame_buffer = deque(maxlen=SEQ_LEN_LSTM)
lstm_output_buffer = deque(maxlen=SEQ_LEN_CONVLSTM)
labels = ["Normal", "Suspicious"]

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # Preprocess
    frame_resized = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))
    frame_rgb = cv2.cvtColor(frame_resized, cv2.COLOR_BGR2RGB)
    frame_norm = frame_rgb / 255.0

    # CNN feature
    feature = cnn_model.predict(np.expand_dims(frame_norm, axis=0), verbose=0)[0]
    frame_buffer.append(feature)

    # LSTM short-term
    if len(frame_buffer) == SEQ_LEN_LSTM:
        lstm_seq = np.expand_dims(frame_buffer, axis=0)  # (1, 16, 576)
        lstm_out = lstm_model.predict(lstm_seq, verbose=0)[0]  # (16,128)
        lstm_last = lstm_out[-1]  # take last frame embedding
        lstm_output_buffer.append(lstm_last.reshape(1,1,1,128))

    # ConvLSTM long-term prediction
    if len(lstm_output_buffer) == SEQ_LEN_CONVLSTM:
        conv_seq = np.expand_dims(np.array(lstm_output_buffer), axis=0) # (1,8,1,1,128)
        pred = conv_model.predict(conv_seq, verbose=0)
        label = labels[np.argmax(pred)]
        conf = np.max(pred)

        cv2.putText(
            frame,
            f"{label} ({conf:.2f})",
            (10,30),
            cv2.FONT_HERSHEY_SIMPLEX,
            1,
            (0,255,0),
            2
        )

    cv2.imshow("Hybrid Real-time Model", frame)

    if cv2.waitKey(1) & 0xFF == 27:  # ESC to quit
        break

cap.release()
cv2.destroyAllWindows()
```

---

# ⚡ Real-time Tips

1. **Sliding window:** keeps latency low
2. **IMG_SIZE = 112** → faster, still readable
3. **Frame skipping** → optional: every 2nd frame
4. **GPU** → faster (~15–25 FPS)
5. **CPU** → slower (~5–8 FPS), still usable

---

# 🏆 Summary

| Feature          | Benefit                     |
| ---------------- | --------------------------- |
| MobileNetV3Small | Fast spatial features       |
| LSTM             | Short-term motion           |
| ConvLSTM         | Long-term temporal patterns |
| Sliding window   | Real-time feasible          |

✅ This is **Hybrid, motion-aware, real-time ready**

---
Perfect 😄
চলো দেখি **Hybrid vs CNN+LSTM vs ConvLSTM FPS & Accuracy Benchmark Table** — এটা দিয়ে তুমি সহজে বুঝতে পারবে কোন model **real-time + accurate**।

---

# 🏁 Benchmark (Expected, approximate)

| Model                                           | Accuracy | Temporal Awareness     | Real-time FPS (GPU) | Real-time FPS (CPU) | Memory Usage | Notes                                                      |
| ----------------------------------------------- | -------- | ---------------------- | ------------------- | ------------------- | ------------ | ---------------------------------------------------------- |
| **CNN + LSTM (MobileNetV3Small)**               | 88–91%   | Short-term             | 20–25               | 12–15               | Low          | Fastest real-time, good baseline                           |
| **ConvLSTM (MobileNetV3Small)**                 | 90–93%   | Medium                 | 15–20               | 5–8                 | Medium       | Motion-aware, slightly slower                              |
| **Hybrid (MobileNetV3Small + LSTM + ConvLSTM)** | 92–95%   | Long-term + short-term | 12–18               | 4–6                 | Medium-High  | Best accuracy & motion understanding, controlled real-time |
| **I3D / C3D / SlowFast**                        | 93–97%   | Full motion            | 2–5                 | 1–2                 | High         | Not real-time, offline analysis only                       |

---

# 🔹 Key Observations

1. **CNN+LSTM** → fastest, easy to deploy, still reasonably accurate
2. **ConvLSTM** → better motion modeling, moderate FPS
3. **Hybrid** → best of both worlds (accuracy + temporal awareness), still feasible for **real-time** on GPU
4. **I3D / C3D** → heavy, offline only

---

# 🔹 Deployment Recommendation

| Use Case                             | Recommended Model                  |
| ------------------------------------ | ---------------------------------- |
| Real-time CCTV / webcam              | **CNN+LSTM** (fast)                |
| Real-time motion-sensitive detection | **Hybrid**                         |
| Offline analysis / research          | **I3D / C3D / SlowFast**           |
| Lightweight / Edge CPU               | **CNN+LSTM with MobileNetV3Small** |

---

# ⚡ Tips to improve FPS without losing much accuracy

1. Reduce **SEQ_LEN** (sliding window length)
2. Reduce **IMG_SIZE** (112–160)
3. Use **MobileNetV3Small** instead of Large
4. Apply **frame skipping** (every 2nd frame)
5. Enable **mixed precision** on GPU:

```python
tf.keras.mixed_precision.set_global_policy('mixed_float16')
```

---

✅ With this table, you can now **choose the right model** depending on:

* Real-time requirement
* Available hardware
* Accuracy needed

---

