ঠিক আছে 👍 তুমি চাইছো **train / val / test split–এর পরে কতগুলো clip আছে** check করতে।

এটা খুব সহজভাবে Python দিয়ে করা যায়। আমরা video-wise split অনুযায়ী group করা clip–গুলো **গণনা করবো**।

---

# ✅ Example Script

```python
import os

OUTPUT_ROOT = "/media/atiar/Volume D/Final/output_clips_split"

splits = ["train", "val", "test"]
classes = ["Normal", "Suspicious"]

for split in splits:
    total_clips = 0
    print(f"\n=== {split.upper()} ===")
    for cls in classes:
        class_dir = os.path.join(OUTPUT_ROOT, split, cls)
        if not os.path.exists(class_dir):
            continue
        clips = os.listdir(class_dir)
        n_clips = len(clips)
        total_clips += n_clips
        print(f"{cls}: {n_clips} clips")
    print(f"Total clips in {split}: {total_clips}")
```

---

# 🔹 Output Example

ধরো split করার পরে:

```
=== TRAIN ===
Normal: 84 clips
Suspicious: 28 clips
Total clips in train: 112

=== VAL ===
Normal: 18 clips
Suspicious: 6 clips
Total clips in val: 24

=== TEST ===
Normal: 18 clips
Suspicious: 6 clips
Total clips in test: 24
```

এখানে তুমি সহজেই verify করতে পারো **clip distribution**।

---

# ⚡ Extra Tip

- যদি তুমি oversample করো minority class, তখন train clip count অনেক বেশি হবে।
    
- Val ও Test **oversample করবেন না**, তাই realistic distribution থাকে।
    

---

ঠিক আছে, আমি তোমার জন্য একটি **complete Python script** বানাচ্ছি যা করবে:

1. Train / Val / Test split অনুযায়ী **clip count দেখাবে**
    
2. **Duplicate clip** আছে কি না চেক করবে (একই clip একাধিক split-এ থাকলে warning দেবে)
    

এটি video-wise split কে leak-free রাখবে।

---

# ✅ Full Script: Clip Count + Duplicate Check

```python
import os
from collections import defaultdict

OUTPUT_ROOT = "/media/atiar/Volume D/Final/output_clips_split"

splits = ["train", "val", "test"]
classes = ["Normal", "Suspicious"]

# 1️⃣ Clip counter
clip_counts = defaultdict(dict)

# 2️⃣ Track all clips to detect duplicates
all_clips = {}

print("\n=== Clip Count per Split ===")

for split in splits:
    total_clips = 0
    for cls in classes:
        class_dir = os.path.join(OUTPUT_ROOT, split, cls)
        if not os.path.exists(class_dir):
            clip_counts[split][cls] = 0
            continue
        clips = os.listdir(class_dir)
        n_clips = len(clips)
        total_clips += n_clips
        clip_counts[split][cls] = n_clips

        # Check duplicates
        for clip in clips:
            if clip in all_clips:
                print(f"⚠️ Duplicate clip found: {clip} in {split}/{cls} AND {all_clips[clip]}")
            else:
                all_clips[clip] = f"{split}/{cls}"

    print(f"{split.upper()} → {total_clips} clips (Normal: {clip_counts[split]['Normal']}, Suspicious: {clip_counts[split]['Suspicious']})")

print("\n✅ Total clips checked:", len(all_clips))
print("Duplicate clip check completed!")
```

---

# 🔹 What this script does

1. প্রতিটি split এবং class-এর clip গোনে
    
2. সব clip name একটি dictionary–তে রাখে
    
3. যদি clip আগের কোনো split/class-এ থাকে → warning দেখায়
    
4. শেষ পর্যন্ত মোট unique clip সংখ্যা দেখায়
    

---

# 🔹 Output Example

```
=== TRAIN ===
train → 112 clips (Normal: 84, Suspicious: 28)

=== VAL ===
val → 24 clips (Normal: 18, Suspicious: 6)

=== TEST ===
test → 24 clips (Normal: 18, Suspicious: 6)

✅ Total clips checked: 160
Duplicate clip check completed!
```

⚠️ যদি duplicate থাকে:

```
⚠️ Duplicate clip found: video1_clip0 in val/Suspicious AND train/Normal
```

---

💡 **Tip:**

- এই script চালানোর আগে নিশ্চিত হও **video-wise split হয়েছে**
    
- একই clip multiple split-এ গেলে model evaluation invalid হবে
    

---

একদম ঠিক! ✅

তোমার বক্তব্যের মূল টার্গেট হলো **duplicate clip check করা**, কারণ যদি একই clip একাধিক split-এ থাকে → **model evaluation invalid হবে**।

এই জন্য আমাদের workflow হওয়া উচিত:

---

# 🔹 Step 1: Video-wise split verification

1. প্রতিটি clip থেকে **video name** বের করো:
    
    ```python
    video_name = clip.split("_clip")[0]
    ```
    
2. একই video name যদি একাধিক split-এ থাকে → warning
    
    - কারণ video-wise split fail হয়েছে → leakage ঘটছে
        

---

# 🔹 Step 2: Clip-wise duplicate check

1. সব clip নাম collect করো dictionary বা set-এ
    
2. যদি clip আগের split/class-এ থাকে → print warning
    

---

# 🔹 Combined Check Script (Video-wise + Clip duplicate)

```python
import os
from collections import defaultdict

OUTPUT_ROOT = "/media/atiar/Volume D/Final/output_clips_split"
splits = ["train", "val", "test"]
classes = ["Normal", "Suspicious"]

all_clips = {}
all_videos = defaultdict(dict)  # split -> video_name -> class

print("\n=== Checking for duplicate clips and video-wise split ===\n")

for split in splits:
    for cls in classes:
        class_dir = os.path.join(OUTPUT_ROOT, split, cls)
        if not os.path.exists(class_dir):
            continue
        clips = os.listdir(class_dir)

        for clip in clips:
            # --- Clip-wise duplicate check ---
            if clip in all_clips:
                print(f"⚠️ Duplicate clip found: {clip} in {split}/{cls} AND {all_clips[clip]}")
            else:
                all_clips[clip] = f"{split}/{cls}"

            # --- Video-wise split check ---
            video_name = clip.split("_clip")[0]
            if video_name in all_videos:
                # check if video already in another split
                for s in all_videos:
                    if video_name in all_videos[s] and s != split:
                        print(f"⚠️ Video-wise split violation: {video_name} clips in both {s} and {split}")
            # store video
            all_videos[split][video_name] = cls

print("\n✅ Check completed!")
print(f"Total unique clips: {len(all_clips)}")
```

---

# 🔹 What it does

1. **Clip duplicate check** → same clip multiple split-এ আছে কিনা
    
2. **Video-wise split check** → same video multiple split-এ আছে কিনা
    
3. Warning print করে problem গুলো
    

---

💡 এই script চালানো উচিত **train/val/test split করার পরে**।

- যদি warning আসে → split ঠিক করতে হবে
    
- কোন clip বা video multiple split-এ গেলে remove/relocate করতে হবে
    

---

যদি চাও, আমি তোমার আগের **split + balance + duplicate check** সব একসাথে **একটি final ready-to-run script** বানিয়ে দিতে পারি।  
এতে সব automatically হবে।

চাও কি আমি সেটা বানাই?