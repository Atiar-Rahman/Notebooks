
ভালো — এখন আমরা **train / val / test (3-way split)** করবো।

⚠️ খুব গুরুত্বপূর্ণ:  
তোমার ক্লিপগুলো একই ভিডিও থেকে এসেছে (sliding window)।  
তাই **video-wise split** করা উচিত, না হলে data leakage হবে।

আমি তোমাকে leakage-free professional version দিচ্ছি।

---

# 🎯 Final Target Structure

```
output_clips_split/
 ├── train/
 │    ├── Normal/
 │    └── Suspicious/
 ├── val/
 │    ├── Normal/
 │    └── Suspicious/
 └── test/
      ├── Normal/
      └── Suspicious/
```

---

# ✅ Recommended Split Ratio

```
Train = 70%
Val   = 15%
Test  = 15%
```

তুমি চাইলে ratio change করতে পারবে।

---

# ✅ Leakage-Free Video-wise Split Script

```python
import os
import shutil
import random
from collections import defaultdict

INPUT_ROOT = "/media/atiar/Volume D/Final/output_clips"
OUTPUT_ROOT = "/media/atiar/Volume D/Final/output_clips_split"

TRAIN_RATIO = 0.7
VAL_RATIO = 0.15
TEST_RATIO = 0.15

RANDOM_SEED = 42
random.seed(RANDOM_SEED)

for class_name in ["Normal", "Suspicious"]:
    class_path = os.path.join(INPUT_ROOT, class_name)
    clips = os.listdir(class_path)

    # ---- Group clips by video name ----
    video_dict = defaultdict(list)
    for clip in clips:
        video_name = clip.split("_clip")[0]
        video_dict[video_name].append(clip)

    videos = list(video_dict.keys())
    random.shuffle(videos)

    total_videos = len(videos)
    train_end = int(total_videos * TRAIN_RATIO)
    val_end = train_end + int(total_videos * VAL_RATIO)

    train_videos = videos[:train_end]
    val_videos = videos[train_end:val_end]
    test_videos = videos[val_end:]

    splits = {
        "train": train_videos,
        "val": val_videos,
        "test": test_videos
    }

    # ---- Create folders ----
    for split in ["train", "val", "test"]:
        os.makedirs(os.path.join(OUTPUT_ROOT, split, class_name), exist_ok=True)

    # ---- Move clips ----
    for split, video_list in splits.items():
        for video in video_list:
            for clip in video_dict[video]:
                src = os.path.join(class_path, clip)
                dst = os.path.join(OUTPUT_ROOT, split, class_name, clip)
                shutil.move(src, dst)

    print(f"\n{class_name}")
    print(f"Train videos: {len(train_videos)}")
    print(f"Val videos:   {len(val_videos)}")
    print(f"Test videos:  {len(test_videos)}")

print("\nTrain/Val/Test split completed successfully!")
```

---

# 🔥 Why This Is Correct

✔ Same video → same split  
✔ No data leakage  
✔ Reproducible (fixed random seed)  
✔ Production-ready

---

# ⚠️ Important

যদি original dataset রাখতে চাও, তাহলে:

```python
shutil.copytree(src, dst)
```

ব্যবহার করো `shutil.move()` এর বদলে।

---

# 📊 Pro Tip (Research Level)

Paper publish বা serious training করলে:

- Train: 70%
    
- Val: 15%
    
- Test: 15%
    
- Report only test accuracy
    
- Tune only on validation
    

---

তুমি কি PyTorch ব্যবহার করছো?  
চাইলে আমি তোমার folder structure অনুযায়ী custom Dataset class বানিয়ে দিতে পারি।