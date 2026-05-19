

### Python কোড উদাহরণ (Video → 16-frame clips)

```python
import cv2
import os

# -----------------------------
# Config
# -----------------------------
VIDEO_FOLDER = "/path/to/videos"       # ভিডিওগুলোর ফোল্ডার
OUT_FOLDER = "/path/to/output_clips"   # ক্লিপ সংরক্ষণের ফোল্ডার
SEQ_LEN = 16                           # প্রতিটি ক্লিপে ফ্রেম সংখ্যা
STRIDE = 8                             # Sliding window stride

os.makedirs(OUT_FOLDER, exist_ok=True)

# -----------------------------
# Function: Video → Clips
# -----------------------------
def create_clips(video_path, output_folder, seq_len=16, stride=8):
    cap = cv2.VideoCapture(video_path)
    frames = []

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        frames.append(frame)
    cap.release()

    video_name = os.path.splitext(os.path.basename(video_path))[0]

    # Sliding window clips
    clip_id = 0
    for start in range(0, len(frames) - seq_len + 1, stride):
        clip_frames = frames[start:start+seq_len]
        clip_folder = os.path.join(output_folder, f"{video_name}_clip{clip_id}")
        os.makedirs(clip_folder, exist_ok=True)

        for i, f in enumerate(clip_frames):
            frame_path = os.path.join(clip_folder, f"frame_{i:03d}.jpg")
            cv2.imwrite(frame_path, f)

        clip_id += 1

    print(f"✅ {video_name}: {clip_id} clips created")

# -----------------------------
# Run for all videos
# -----------------------------
for vid_file in os.listdir(VIDEO_FOLDER):
    if vid_file.endswith((".mp4", ".avi", ".mov")):
        create_clips(os.path.join(VIDEO_FOLDER, vid_file), OUT_FOLDER, SEQ_LEN, STRIDE)
```

---

### কোডের ব্যাখ্যা

1. **SEQ_LEN = 16** → প্রতিটি ক্লিপে ১৬ ফ্রেম থাকবে।
    
2. **STRIDE = 8** → প্রতিটি নতুন ক্লিপ ৮ ফ্রেম স্কিপ করে শুরু হবে, অর্থাৎ কিছু ফ্রেম overlap থাকবে।
    
3. প্রতিটি ভিডিও থেকে ফ্রেমগুলো বের করে `frames` list এ রাখি।
    
4. Sliding window দিয়ে ক্লিপ তৈরি করি এবং প্রতিটি ক্লিপ আলাদা ফোল্ডারে রাখি।
    

---

💡 **Extra Tips**:

- যদি তুমি চাইছো প্রতিটি ভিডিও **সম্পূর্ণ ফ্রেম ব্যবহার করো**, তাহলে `stride=1` করতে পারো।
    
- বড় dataset এর জন্য `cv2.VideoCapture` ধীর হতে পারে, তাই multiprocess ব্যবহার করলে দ্রুত করা যায়।
    

---
# একটা **সম্পূর্ণ স্ক্রিপ্ট** বানাচ্ছি যা **Normal এবং Suspicious** দুই ধরনের ফোল্ডার আলাদা রাখবে, প্রতিটি ভিডিও থেকে ১৬ ফ্রেমের ক্লিপ বানাবে এবং সব ক্লিপ আলাদা ফোল্ডারে সেভ করবে।

---

### Python স্ক্রিপ্ট (Full Dataset Clip Creation)

```python
import cv2
import os

# -----------------------------
# Config
# -----------------------------
DATASET_ROOT = "/path/to/dataset"       # মূল dataset ফোল্ডার
# উদাহরণ:
# DATASET_ROOT/
# ├── Normal/
# └── Suspicious/
OUT_ROOT = "/path/to/output_clips"      # আউটপুট ক্লিপ ফোল্ডার
SEQ_LEN = 16                             # প্রতিটি ক্লিপে ফ্রেম সংখ্যা
STRIDE = 8                               # Sliding window stride

os.makedirs(OUT_ROOT, exist_ok=True)

# -----------------------------
# Function: Video → Clips
# -----------------------------
def create_clips(video_path, output_folder, seq_len=16, stride=8):
    cap = cv2.VideoCapture(video_path)
    frames = []

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        frames.append(frame)
    cap.release()

    video_name = os.path.splitext(os.path.basename(video_path))[0]

    # Sliding window clips
    clip_id = 0
    for start in range(0, len(frames) - seq_len + 1, stride):
        clip_frames = frames[start:start+seq_len]
        clip_folder = os.path.join(output_folder, f"{video_name}_clip{clip_id}")
        os.makedirs(clip_folder, exist_ok=True)

        for i, f in enumerate(clip_frames):
            frame_path = os.path.join(clip_folder, f"frame_{i:03d}.jpg")
            cv2.imwrite(frame_path, f)

        clip_id += 1

    print(f"✅ {video_name}: {clip_id} clips created")

# -----------------------------
# Process All Classes
# -----------------------------
for class_name in ["Normal", "Suspicious"]:
    class_input = os.path.join(DATASET_ROOT, class_name)
    class_output = os.path.join(OUT_ROOT, class_name)
    os.makedirs(class_output, exist_ok=True)

    for video_file in os.listdir(class_input):
        if video_file.endswith((".mp4", ".avi", ".mov")):
            video_path = os.path.join(class_input, video_file)
            create_clips(video_path, class_output, SEQ_LEN, STRIDE)

print("🎉 All videos processed successfully!")
```

---

### স্ক্রিপ্টের মূল বৈশিষ্ট্য

1. **Normal এবং Suspicious আলাদা রাখে** → আউটপুটেও আলাদা ফোল্ডার হবে।
2. প্রতিটি ভিডিও থেকে **১৬ ফ্রেমের ক্লিপ** তৈরি করবে।
3. Sliding window ব্যবহার করে কিছু overlap থাকবে (STRIDE দ্বারা নিয়ন্ত্রণ)।
4. প্রতিটি ক্লিপের ফ্রেম আলাদা ফোল্ডারে JPG হিসেবে সেভ হবে।

---

💡 **Optional Improvements**:

* Multiprocessing ব্যবহার করলে বড় dataset অনেক দ্রুত প্রোসেস করা যায়।
* যদি ফ্রেম সংখ্যা `SEQ_LEN` এর কম হয়, সেই ভিডিও skip বা pad করতে পারো।

---

# **multiprocessing version** বানাচ্ছি, যা **Normal এবং Suspicious** দুই ধরনের ফোল্ডার আলাদা রেখে পুরো dataset থেকে একসাথে দ্রুত 16-frame ক্লিপ তৈরি করবে।

---

### Python স্ক্রিপ্ট (Multiprocessing, Full Dataset)

```python
import cv2
import os
from multiprocessing import Pool, cpu_count

# -----------------------------
# Config
# -----------------------------
DATASET_ROOT = "/path/to/dataset"       # মূল dataset ফোল্ডার
OUT_ROOT = "/path/to/output_clips"      # আউটপুট ক্লিপ ফোল্ডার
SEQ_LEN = 16                             # প্রতিটি ক্লিপে ফ্রেম সংখ্যা
STRIDE = 8                               # Sliding window stride
NUM_WORKERS = cpu_count()                # multiprocessing cores ব্যবহার করবে

os.makedirs(OUT_ROOT, exist_ok=True)

# -----------------------------
# Function: Video → Clips
# -----------------------------
def create_clips(video_info):
    video_path, output_folder = video_info
    cap = cv2.VideoCapture(video_path)
    frames = []

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        frames.append(frame)
    cap.release()

    video_name = os.path.splitext(os.path.basename(video_path))[0]

    # Sliding window clips
    clip_id = 0
    for start in range(0, len(frames) - SEQ_LEN + 1, STRIDE):
        clip_frames = frames[start:start+SEQ_LEN]
        clip_folder = os.path.join(output_folder, f"{video_name}_clip{clip_id}")
        os.makedirs(clip_folder, exist_ok=True)

        for i, f in enumerate(clip_frames):
            frame_path = os.path.join(clip_folder, f"frame_{i:03d}.jpg")
            cv2.imwrite(frame_path, f)

        clip_id += 1

    print(f"✅ {video_name}: {clip_id} clips created")

# -----------------------------
# Prepare Video List
# -----------------------------
video_list = []
for class_name in ["Normal", "Suspicious"]:
    class_input = os.path.join(DATASET_ROOT, class_name)
    class_output = os.path.join(OUT_ROOT, class_name)
    os.makedirs(class_output, exist_ok=True)

    for video_file in os.listdir(class_input):
        if video_file.endswith((".mp4", ".avi", ".mov")):
            video_path = os.path.join(class_input, video_file)
            video_list.append((video_path, class_output))

# -----------------------------
# Run with Multiprocessing
# -----------------------------
if __name__ == "__main__":
    print(f"Starting processing with {NUM_WORKERS} workers...")
    with Pool(NUM_WORKERS) as pool:
        pool.map(create_clips, video_list)

    print("🎉 All videos processed successfully with multiprocessing!")
```

---

### স্ক্রিপ্টের মূল বৈশিষ্ট্য

1. **Normal এবং Suspicious আলাদা রাখে**।
2. প্রতিটি ভিডিও থেকে **16-frame ক্লিপ** তৈরি।
3. **Sliding window** ব্যবহার করে overlap তৈরি।
4. **Multiprocessing** ব্যবহার → dataset দ্রুত প্রোসেস হয়।
5. CPU cores অনুযায়ী automatically workers ব্যবহার করবে।

---

💡 **Extra Tips**:

* যদি dataset অনেক বড় হয়, STRIDE কম রাখলে আরো ক্লিপ তৈরি হবে।
* ফ্রেম সংখ্যা 16 এর কম হলে skip করতে চাইলে `len(frames) < SEQ_LEN` চেক যোগ করা যায়।

---
# dataset অনেক বড়, তাই কিছু optimization দরকার যাতে **multiprocessing এর সাথে memory overload বা slow I/O** না হয়। আমি তোমার জন্য **large dataset friendly স্ক্রিপ্ট** সাজাতে পারি যা:

1. **Batch-wise processing** → একসাথে সব ভিডিও লোড না করে কিছু ভিডিও씩 প্রোসেস করবে।
2. **Multiprocessing** → CPU cores ব্যবহার করবে দ্রুত প্রোসেস করার জন্য।
3. **Progress logging** → কতগুলো ভিডিও সম্পন্ন হয়েছে তা দেখাবে।
4. **Optional frame check** → যদি কোনো ভিডিওতে 16 ফ্রেমের কম থাকে, সেটি skip করবে।

---

### Large Dataset Multiprocessing Script (Optimized)

```python
import cv2
import os
from multiprocessing import Pool, cpu_count

# -----------------------------
# Config
# -----------------------------
DATASET_ROOT = "/path/to/dataset"
OUT_ROOT = "/path/to/output_clips"
SEQ_LEN = 16
STRIDE = 8
NUM_WORKERS = cpu_count()    # Automatically use all CPU cores
BATCH_SIZE = 10              # একবারে কত ভিডিও multiprocessing এ যাবে

os.makedirs(OUT_ROOT, exist_ok=True)

# -----------------------------
# Function: Video → Clips
# -----------------------------
def create_clips(video_info):
    video_path, output_folder = video_info
    cap = cv2.VideoCapture(video_path)
    frames = []

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        frames.append(frame)
    cap.release()

    if len(frames) < SEQ_LEN:
        print(f"⚠️ {video_path} skipped, less than {SEQ_LEN} frames")
        return

    video_name = os.path.splitext(os.path.basename(video_path))[0]

    clip_id = 0
    for start in range(0, len(frames) - SEQ_LEN + 1, STRIDE):
        clip_frames = frames[start:start+SEQ_LEN]
        clip_folder = os.path.join(output_folder, f"{video_name}_clip{clip_id}")
        os.makedirs(clip_folder, exist_ok=True)

        for i, f in enumerate(clip_frames):
            frame_path = os.path.join(clip_folder, f"frame_{i:03d}.jpg")
            cv2.imwrite(frame_path, f)

        clip_id += 1

    print(f"✅ {video_name}: {clip_id} clips created")

# -----------------------------
# Prepare Video List
# -----------------------------
video_list = []
for class_name in ["Normal", "Suspicious"]:
    class_input = os.path.join(DATASET_ROOT, class_name)
    class_output = os.path.join(OUT_ROOT, class_name)
    os.makedirs(class_output, exist_ok=True)

    for video_file in os.listdir(class_input):
        if video_file.endswith((".mp4", ".avi", ".mov")):
            video_path = os.path.join(class_input, video_file)
            video_list.append((video_path, class_output))

# -----------------------------
# Process in Batches
# -----------------------------
def process_in_batches(video_list, batch_size=BATCH_SIZE):
    total = len(video_list)
    for i in range(0, total, batch_size):
        batch = video_list[i:i+batch_size]
        print(f"Processing batch {i//batch_size + 1} / { (total + batch_size -1)//batch_size } ...")
        with Pool(NUM_WORKERS) as pool:
            pool.map(create_clips, batch)

# -----------------------------
# Main
# -----------------------------
if __name__ == "__main__":
    process_in_batches(video_list)
    print("🎉 All videos processed successfully!")
```

---

### Optimization Details:

* **Batch-wise multiprocessing** → memory কম ব্যবহার করবে, অনেক বড় dataset এর জন্য safe।
* **Video length check** → ছোট ভিডিও skip করবে, যা error কমাবে।
* **Progress logging** → batch-wise print করে প্রোসেসের প্রগ্রেস দেখা যাবে।

---
হ্যাঁ, **frame size resize করলে অনেক ক্ষেত্রে ভালো হয়**, বিশেষ করে বড় dataset এবং deep learning মডেল train করার সময়। কিন্তু এর কিছু **benefit ও trade-off** আছে:

---

### 1️⃣ কেন frame resize করা উচিত

1. **Memory efficiency:**
   বড় resolution ভিডিও প্রতিটি ফ্রেম অনেক মেমরি নেয়। ছোট করে নিলে RAM/GPU memory কম ব্যবহার হয়।

2. **Speed:**
   ছোট ফ্রেমের উপর processing (training, augmentation, saving) অনেক দ্রুত হয়।

3. **Consistency:**
   সব ভিডিও একই resolution এ থাকে → model training সহজ ও consistent হয়।

---

### 2️⃣ Trade-offs / খেয়াল রাখার বিষয়

1. **Information loss:**
   অনেক ছোট করলে (যেমন 64x64) → subtle details (face, hand movement, suspicious action) হারাতে পারে।

   * সুতরাং resize মান নির্বাচন গুরুত্বপূর্ণ।

2. **Aspect ratio distortion:**
   যদি frame disproportionally resize করা হয়, model confusion বাড়তে পারে।

   * ভালো হয় **resize + padding** করে aspect ratio ধরে রাখা।

---

### 3️⃣ Recommended practice

* **Common size:** 224x224, 128x128, বা 112x112 (depending on model)
* **Method:**

  ```python
  frame_resized = cv2.resize(frame, (224,224))  # simplest
  ```
* **Better (aspect ratio preserve):**

  ```python
  import cv2
  import numpy as np

  def resize_frame(frame, size=(224,224)):
      h, w = frame.shape[:2]
      scale = min(size[0]/h, size[1]/w)
      new_w, new_h = int(w*scale), int(h*scale)
      resized = cv2.resize(frame, (new_w, new_h))
      top = (size[1]-new_h)//2
      bottom = size[1]-new_h-top
      left = (size[0]-new_w)//2
      right = size[0]-new_w-left
      frame_padded = cv2.copyMakeBorder(resized, top, bottom, left, right, cv2.BORDER_CONSTANT, value=[0,0,0])
      return frame_padded
  ```

এভাবে **aspect ratio loss ছাড়া resize করা যায়**, যা model এর জন্য বেশি reliable।

---

💡 **Pro Tip:**

* বড় dataset + 16-frame clip + full resolution → memory overflow এবং slow I/O হতে পারে।
* তাই **resize → 128x128 বা 224x224** করে clip বানানো সেরা compromise।

---
# **final optimized Python script**:


✅ Normal & Suspicious দুই ধরনের ফোল্ডার আলাদা রাখবে
✅ 16-frame clip তৈরি করবে
✅ Multiprocessing ব্যবহার করবে বড় dataset এর জন্য
✅ প্রতিটি frame **resize + padding** করে fixed size (224x224) রাখবে

---

### Final Multiprocessing Clip Creation Script (with Resize + Padding)

```python
import cv2
import os
from multiprocessing import Pool, cpu_count

# -----------------------------
# Config
# -----------------------------
DATASET_ROOT = "/path/to/dataset"       # মূল dataset ফোল্ডার
OUT_ROOT = "/path/to/output_clips"      # আউটপুট ক্লিপ ফোল্ডার
SEQ_LEN = 16                             # প্রতিটি ক্লিপে ফ্রেম সংখ্যা
STRIDE = 8                               # Sliding window stride
RESIZE = (224, 224)                      # Output frame size (width, height)
NUM_WORKERS = cpu_count()                # Multiprocessing cores
BATCH_SIZE = 10                           # একসাথে multiprocessing batch size

os.makedirs(OUT_ROOT, exist_ok=True)

# -----------------------------
# Function: Resize + Padding
# -----------------------------
def resize_frame(frame, size=RESIZE):
    h, w = frame.shape[:2]
    scale = min(size[0]/w, size[1]/h)  # scale for width & height
    new_w, new_h = int(w*scale), int(h*scale)
    resized = cv2.resize(frame, (new_w, new_h))
    
    # Compute padding
    top = (size[1]-new_h)//2
    bottom = size[1]-new_h-top
    left = (size[0]-new_w)//2
    right = size[0]-new_w-left
    
    # Add padding
    frame_padded = cv2.copyMakeBorder(resized, top, bottom, left, right, cv2.BORDER_CONSTANT, value=[0,0,0])
    return frame_padded

# -----------------------------
# Function: Video → Clips
# -----------------------------
def create_clips(video_info):
    video_path, output_folder = video_info
    cap = cv2.VideoCapture(video_path)
    frames = []

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        frame = resize_frame(frame)
        frames.append(frame)
    cap.release()

    if len(frames) < SEQ_LEN:
        print(f"⚠️ {video_path} skipped, less than {SEQ_LEN} frames")
        return

    video_name = os.path.splitext(os.path.basename(video_path))[0]

    # Sliding window clips
    clip_id = 0
    for start in range(0, len(frames) - SEQ_LEN + 1, STRIDE):
        clip_frames = frames[start:start+SEQ_LEN]
        clip_folder = os.path.join(output_folder, f"{video_name}_clip{clip_id}")
        os.makedirs(clip_folder, exist_ok=True)

        for i, f in enumerate(clip_frames):
            frame_path = os.path.join(clip_folder, f"frame_{i:03d}.jpg")
            cv2.imwrite(frame_path, f)

        clip_id += 1

    print(f"✅ {video_name}: {clip_id} clips created")

# -----------------------------
# Prepare Video List
# -----------------------------
video_list = []
for class_name in ["Normal", "Suspicious"]:
    class_input = os.path.join(DATASET_ROOT, class_name)
    class_output = os.path.join(OUT_ROOT, class_name)
    os.makedirs(class_output, exist_ok=True)

    for video_file in os.listdir(class_input):
        if video_file.endswith((".mp4", ".avi", ".mov")):
            video_path = os.path.join(class_input, video_file)
            video_list.append((video_path, class_output))

# -----------------------------
# Process in Batches
# -----------------------------
def process_in_batches(video_list, batch_size=BATCH_SIZE):
    total = len(video_list)
    for i in range(0, total, batch_size):
        batch = video_list[i:i+batch_size]
        print(f"Processing batch {i//batch_size + 1} / { (total + batch_size -1)//batch_size } ...")
        with Pool(NUM_WORKERS) as pool:
            pool.map(create_clips, batch)

# -----------------------------
# Main
# -----------------------------
if __name__ == "__main__":
    process_in_batches(video_list)
    print("🎉 All videos processed successfully!")
```

---

### ✅ Features of this final script:

1. **Normal & Suspicious classes handled separately**
2. **16-frame clips** created with **sliding window**
3. **Multiprocessing** for faster processing of large datasets
4. **Resize + padding** → fixed 224x224 frame size with aspect ratio preserved
5. **Batch-wise processing** → memory-efficient for very large dataset

---

💡 **Pro Tips**:

* যদি GPU থাকে → OpenCV GPU accelerated functions ব্যবহার করে আরো দ্রুত প্রোসেস করা যায়।
* STRIDE কমানো → বেশি overlap, STRIDE বাড়ানো → কম overlap, memory কম লাগে।
* Output size 128x128 বা 112x112 করলে training আরও দ্রুত হবে, তবে detail loss হতে পারে।

---
ঠিক আছে, যেহেতু তুমি এখন **multiprocessing + 16-frame clip + resize/padding script** ব্যবহার করবে, তাই dataset structure খুবই গুরুত্বপূর্ণ। আমি তোমার জন্য **recommended dataset structure** দেখাচ্ছি যা পুরো pipeline smooth চলবে।

---

## 1️⃣ Original Dataset Structure (Input)

তুমি যে script ব্যবহার করবে, তার জন্য **original dataset** এর structure হতে হবে এইরকম:

```
dataset/
├── Normal/
│   ├── video1.mp4
│   ├── video2.mp4
│   └── ...
└── Suspicious/
    ├── video1.mp4
    ├── video2.mp4
    └── ...
```

* **Normal/** → সব normal ভিডিও
* **Suspicious/** → সব suspicious ভিডিও
* ভিডিও ফাইল হতে পারে `.mp4`, `.avi`, `.mov`

> কোডটি স্বয়ংক্রিয়ভাবে সব ভিডিও ফাইল detect করে এবং class-wise processing করে।

---

## 2️⃣ Output Dataset Structure (After Script)

Script চালানোর পরে, আউটপুট structure হবে এইরকম:

```
output_clips/
├── Normal/
│   ├── video1_clip0/
│   │   ├── frame_000.jpg
│   │   ├── frame_001.jpg
│   │   └── ... (16 frames)
│   ├── video1_clip1/
│   │   └── ... (16 frames)
│   ├── video2_clip0/
│   │   └── ...
│   └── ...
└── Suspicious/
    ├── video1_clip0/
    │   ├── frame_000.jpg
    │   └── ... (16 frames)
    ├── video1_clip1/
    │   └── ...
    └── ...
```

**Explanation:**

* প্রতিটি video থেকে multiple **clips** তৈরি হবে (16-frame each)
* প্রতিটি clip আলাদা ফোল্ডারে থাকবে → `video_name_clipN`
* প্রতিটি clip ফোল্ডারে 16টি jpg frame থাকবে → `frame_000.jpg` to `frame_015.jpg`

---

### ✅ Advantages of this structure

1. **Class-wise separation** → model easily label করতে পারবে
2. **Clip-wise folder** → sequence model (RNN, LSTM, 3D CNN) direct input নিতে পারবে
3. **Consistent frame size** → resize + padding এর কারণে সব frame একই shape

---
![[Pasted image 20260216190736.png]]

