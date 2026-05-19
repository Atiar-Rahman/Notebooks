
Perfect 👍 — **subfolder থাকলে কোনো সমস্যা নেই**, বরং এটা **best practice** 👌
তবে split script–টা একটু smart হতে হবে।

আমি তোমাকে **subfolder-safe Train → Val auto split script** দিচ্ছি 👇

---

## 🗂️ Your current structure (assumed)

```
dataset/
 ├── train/
 │    ├── normal/
 │    │     ├── frame_001.png
 │    │     └── ...
 │    └── suspicious/
 │          ├── arson/
 │          │     ├── frame_001.png
 │          │     └── ...
 │          ├── robbery/
 │          ├── assault/
 │          └── ...
 └── test/
```

👉 Goal:

* `normal/` → split normally
* `suspicious/*/` → **each subfolder separately split**
* Same structure maintain

---

## 🧠 What this script guarantees

✔️ Subfolder structure preserved
✔️ No filename conflict
✔️ Class ratio roughly same
✔️ TensorFlow compatible

---

## 🧪 Train → Val Split Script (Supports Subfolders)

```python
import os
import shutil
import random

# ================= CONFIG =================
SOURCE_DIR = "dataset/train"
VAL_DIR = "dataset/val"
VAL_RATIO = 0.2
SEED = 42
# =========================================

random.seed(SEED)
os.makedirs(VAL_DIR, exist_ok=True)

def split_folder(src_dir, dst_dir, val_ratio):
    images = [f for f in os.listdir(src_dir)
              if os.path.isfile(os.path.join(src_dir, f))]
    random.shuffle(images)

    val_count = int(len(images) * val_ratio)
    os.makedirs(dst_dir, exist_ok=True)

    for img in images[:val_count]:
        shutil.move(
            os.path.join(src_dir, img),
            os.path.join(dst_dir, img)
        )

    return val_count


for class_name in os.listdir(SOURCE_DIR):
    class_path = os.path.join(SOURCE_DIR, class_name)

    if not os.path.isdir(class_path):
        continue

    # normal class (no subfolders)
    if class_name != "suspicious":
        val_class_dir = os.path.join(VAL_DIR, class_name)
        moved = split_folder(class_path, val_class_dir, VAL_RATIO)
        print(f"{class_name}: {moved} images moved")

    # suspicious class (with subfolders)
    else:
        for sub in os.listdir(class_path):
            sub_path = os.path.join(class_path, sub)
            if not os.path.isdir(sub_path):
                continue

            val_sub_dir = os.path.join(VAL_DIR, class_name, sub)
            moved = split_folder(sub_path, val_sub_dir, VAL_RATIO)
            print(f"suspicious/{sub}: {moved} images moved")

print("\n✅ Train → Validation split done (subfolder-safe)!")
```

---

## 🗂️ After split (final structure)

```
dataset/
 ├── train/
 │    ├── normal/
 │    └── suspicious/
 │         ├── arson/
 │         ├── robbery/
 │         └── ...
 ├── val/
 │    ├── normal/
 │    └── suspicious/
 │         ├── arson/
 │         ├── robbery/
 │         └── ...
 └── test/
```

---

## ⚠️ TensorFlow Labeling (Important)

When you load with:

```python
image_dataset_from_directory("dataset/train")
```

TensorFlow will assign:

```
normal      → label 0
suspicious  → label 1
```

Subfolders (`arson`, `robbery`) **ignored as labels** — perfect 👍

---

## 🔥 TL;DR

| Question                 | Answer              |
| ------------------------ | ------------------- |
| Suspicious subfolder OK? | ✅ Yes               |
| Rename needed?           | ❌ No                |
| Conflict risk?           | ❌ No                |
| Script change needed?    | ✅ Yes (given above) |

---

চাও তো next আমি দিতে পারি:

* 🔹 **Train-only balancing script (binary)**
* 🔹 **tf.data optimized loader (cache/prefetch)**
* 🔹 **End-to-end CNN training code (64×64)**

বল — পরের ধাপ কোনটা? 🚀
