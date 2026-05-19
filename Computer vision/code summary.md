```python
import os

import glob

import random

from collections import defaultdict

from PIL import Image

import numpy as np

from tqdm import tqdm

  

import torch

import torch.nn as nn

from torch.utils.data import Dataset, DataLoader

import torchvision.transforms as T

import torchvision.models as models

import torch.optim as optim
```


# Explain:
কোডে ব্যবহৃত **সকল package/module** একদম সহজ ভাষায় ব্যাখ্যা করছি—**কেন দরকার**, **কি কাজ করে**, এবং **কোথায় ব্যবহার হয়**।

---

# ✅ **1. `os`**

### ✔ কেন দরকার?

ফাইল ও ফোল্ডার নিয়ে কাজ করার জন্য।

### ✔ কি কাজ করে?

- Path join → `os.path.join()`
    
- Directory list → `os.listdir()`
    
- File exists check → `os.path.exists()`
    

### ✔ কোথায় ব্যবহার?

Dataset folder থেকে image path নেওয়া।

---

# ✅ **2. `glob`**

### ✔ কেন দরকার?

Wildcard ব্যবহার করে ফোল্ডার থেকে নির্দিষ্ট ফাইল match করে এনে দেয়।

### ✔ কি কাজ করে?

- `glob.glob("*.jpg")` → সব `.jpg` ফাইল return করে
    

### ✔ কোথায় ব্যবহার?

Dataset লোড করার সময় সব ছবি একসঙ্গে path নেওয়া।

---

# ✅ **3. `random`**

### ✔ কেন দরকার?

Shuffling, random splitting ইত্যাদি কাজে।

### ✔ কি কাজ করে?

- Random choice: `random.choice()`
    
- Random shuffle: `random.shuffle()`
    

### ✔ কোথায় ব্যবহার?

Train/Val split বা random image pick করতে।

---

# ✅ **4. `collections.defaultdict`**

### ✔ কেন দরকার?

Dictionary যেটির default value auto সেট হয়।

### ✔ কি কাজ করে?

```
d = defaultdict(list)
d[key].append(value)
```

Key না থাকলে নিজে থেকে list তৈরি করে।

### ✔ কোথায় ব্যবহার?

Class-wise files store করতে।

---

# ✅ **5. `PIL.Image` (Pillow library)**

### ✔ কেন দরকার?

Image open, resize, convert ইত্যাদি কাজ করার জন্য।

### ✔ কি কাজ করে?

- `Image.open(file)`
    
- Image resize
    
- Convert to numpy array
    

### ✔ কোথায় ব্যবহার?

Image load → transform করার আগে।

---

# ✅ **6. `numpy` (`np`)**

### ✔ কেন দরকার?

Numeric operations, array operations, tensor conversion, preprocessing।

### ✔ কি কাজ করে?

- Image → array convert
    
- Normalize
    
- Matrix calculation
    

### ✔ কোথায় ব্যবহার?

Image data numpy array এ convert করতে।

---

# ✅ **7. `tqdm`**

### ✔ কেন দরকার?

Loop এর progress bar দেখানোর জন্য।

### ✔ কি কাজ করে?

```
for x in tqdm(list):
    ...
```

Loop এ progress bar দেখায় → user-friendly।

---

# ---------------------------------------------

# 🔥 **PYTORCH MODULES**

# ---------------------------------------------

---

# ✅ **8. `torch`**

### ✔ কেন দরকার?

PyTorch Framework – Deep Learning এর সব কাজ এর মাধ্যমেই হয়।

### ✔ কি কাজ করে?

- Tensors
    
- GPU computation (`.cuda()`)
    
- Neural network training
    

---

# ✅ **9. `torch.nn`**

### ✔ কেন দরকার?

Neural Network বানানোর জন্য বিভিন্ন layers দেওয়া আছে।

### ✔ কি কাজ করে?

- `nn.Linear`
    
- `nn.Conv2d`
    
- `nn.ReLU`
    
- `nn.CrossEntropyLoss`
    

### ✔ কোথায় ব্যবহার?

Model architecture তৈরি করতে।

---

# ✅ **10. `torch.utils.data.Dataset`**

### ✔ কেন দরকার?

Custom dataset class তৈরি করতে।

### ✔ কি কাজ করে?

Dataset → PyTorch style এ load করতে সাহায্য করে।

---

# ✅ **11. `torch.utils.data.DataLoader`**

### ✔ কেন দরকার?

Batch, shuffle, parallel loading সব করতে।

### ✔ কি কাজ করে?

Dataset → batch করে model এ দেয়।

---

# ---------------------------------------------

# 🖼 **IMAGE TRANSFORMS**

---

# ✅ **12. `torchvision.transforms` (`T`)**

### ✔ কেন দরকার?

Image preprocessing/augmentation।

### ✔ কি কাজ করে?

- Resize
    
- Normalize
    
- RandomFlip
    
- ToTensor
    

Example:

```
T.ToTensor()
T.Resize((224, 224))
T.Normalize(mean, std)
```

---

# ---------------------------------------------

# 🤖 **MODELS**

---

# ✅ **13. `torchvision.models`**

### ✔ কেন দরকার?

Pretrained CNN models ব্যবহার করতে।

### ✔ কি কাজ করে?

- ResNet
    
- VGG
    
- MobileNet
    
- EfficientNet
    

Example:

```
model = models.resnet18(pretrained=True)
```

---

# ---------------------------------------------

# 🧠 **OPTIMIZER**

---

# ✅ **14. `torch.optim`**

### ✔ কেন দরকার?

Model training করার সময় parameters update করতে।

### ✔ কি কাজ করে?

- SGD
    
- Adam
    
- RMSProp
    

Example:

```
optim.Adam(model.parameters(), lr=0.001)
```

---

# 🎯 **Summary Table**

| Package     | কেন দরকার?        | কাজ               |
| ----------- | ----------------- | ----------------- |
| os          | File path         | Directory manage  |
| glob        | File search       | All image paths   |
| random      | Shuffle           | Random split      |
| defaultdict | Auto dict init    | Class-wise list   |
| PIL         | Image open        | Preprocessing     |
| numpy       | Array operations  | Conversion        |
| tqdm        | Progress bar      | Training loop UI  |
| torch       | Main DL framework | Tensors & GPU     |
| nn          | Model layers      | Build model       |
| Dataset     | Custom dataset    | Load image        |
| DataLoader  | Batch, shuffle    | Fast loading      |
| transforms  | Preprocessing     | Resize, normalize |
| models      | Pretrained models | ResNet etc        |
| optim       | Optimizers        | Weight update     |

---


```python
# ---------------------------

# CONFIG

# ---------------------------

DATA_DIR = "final_dataset" # base dir

SEQ_LEN = 8 # number of frames per sample (temporal window)

FRAME_SIZE = 224 # input size for CNN (ResNet default)

BATCH_SIZE = 8

NUM_WORKERS = 4

EPOCHS = 20

LR = 1e-4

WEIGHT_DECAY = 1e-5

DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

MODEL_SAVE_PATH = "best_cnn_lstm.pth"

RANDOM_SEED = 42

  

# Whether to use a pretrained CNN and whether to freeze its weights

PRETRAINED = True

FREEZE_CNN = False
```

# Explain
নীচে তোমার CONFIG অংশে থাকা **PRETRAINED** এবং **FREEZE_CNN** এর সম্পূর্ণ ব্যাখ্যা দিচ্ছি—**কেন দরকার**, **কখন ব্যবহার করা হয়**, এবং **কোন পরিস্থিতিতে কোনটা অন রাখবে**।

---

# 🔥 CONFIG PARAMETERS EXPLAINED (PRETRAINED & FREEZE_CNN)

## ✅ **1. `PRETRAINED = True`**

### ✔ এর মানে কী?

তোমার CNN (যেমন ResNet, EfficientNet) **ImageNet pretrained weights** দিয়ে load হবে।

### ✔ কেন ব্যবহার করা হয়?

ImageNet শেখানো model:

- Already edge, shape, texture চেনে
    
- Low data হলেও ভালো accuracy দেয়
    
- Training দ্রুত converge হয়
    
- কম GPU, কম epoch প্রয়োজন
    

### ✔ কখন ON রাখা উচিত?

| পরিস্থিতি                          | PRETRAINED = True রাখবে? |
| ---------------------------------- | ------------------------ |
| Dataset ছোট                        | ✔ হ্যাঁ                  |
| Training data কম                   | ✔ হ্যাঁ                  |
| High accuracy চাই শুরুতেই          | ✔ হ্যাঁ                  |
| CNN+LSTM video classifier বানাচ্ছো | ✔ অবশ্যই                 |
| GPU কম/slow                        | ✔ হ্যাঁ                  |

### ✔ কখন OFF করা উচিত?

PRETRAINED = False যদি:

- নিজের dataset খুব বড় (১০ লাখ+ image)
    
- New domain (e.g. medical, satellite), যেখানে ImageNet pretraining কাজে কম লাগে
    
- Model সম্পূর্ণ scratch থেকে train করার ইচ্ছে থাকলে
    

---

---

# ⭐ 2. `FREEZE_CNN = False`

### ✔ এর মানে কী?

**Freeze CNN** = CNN backbone train হবে না  
(only LSTM + FC layer train হবে)

### ✔ কেন Freeze করা হয়?

- Train faster
    
- কম GPU usage
    
- কম data হলেও overfitting কম হয়
    

### ✔ Freeze করলে কি হয়?

- CNN শুধু feature extractor
    
- LSTM + classifier train হয়
    
- CNN weights fixed থাকে (update হয় না)
    

---

# 🧠 কখন Freeze করা উচিত?

| পরিস্থিতি                | FREEZE_CNN = True রাখবে?     |
| ------------------------ | ---------------------------- |
| Dataset ছোট              | ✔ হ্যাঁ → Overfitting কম     |
| GPU কম                   | ✔ হ্যাঁ → Training দ্রুত হবে |
| শুধু LSTM train করতে চাও | ✔ হ্যাঁ                      |
| Pretrained CNN use করছো  | ✔ Hah →                      |

**Common rule:**  
_Pretrained দিলে mostly freeze রাখা হয় শুরুতে।_

---

---

# 🧠 কখন Freeze Off (trainable) রাখা উচিত? → `FREEZE_CNN = False`

| পরিস্থিতি                                 | FREEZE_CNN = False রাখবে? |
| ----------------------------------------- | ------------------------- |
| Dataset বড়                                | ✔ হ্যাঁ                   |
| CNN কে নিজের dataset এ fine-tune করতে চাও | ✔ হ্যাঁ                   |
| Better accuracy দরকার                     | ✔ হ্যাঁ                   |
| Pretrained features যথেষ্ট না             | ✔ হ্যাঁ                   |

### Example:

Action recognition, gesture detection, fall detection →  
**Temporal + spatial features দুইটাই দরকার → CNN train করতে দেবে (freeze=False)**

---

# 🎯 Summary (Best Practice)

| Condition                | PRETRAINED | FREEZE_CNN |
| ------------------------ | ---------- | ---------- |
| Small dataset            | True       | True       |
| Medium dataset           | True       | False      |
| Large dataset            | Optional   | False      |
| GPU কম                   | True       | True       |
| High accuracy চাই        | True       | False      |
| Medical/Satellite images | False/True | False      |

---

# ✨ তোমার সেটিং (Recommended)

তোমার config এ দেওয়া আছে:

```
PRETRAINED = True
FREEZE_CNN = False
```

এটা action/video classification + LSTM pipeline এর জন্য **best combination**:

- Pretrained CNN → strong feature extractor
    
- Freeze=False → CNN fine-tune হবে তোমার dataset এ → accuracy বেড়ে যাবে
    

Fantastic choice ✔

---



```python
  

# ---------------------------

# Utilities: grouping frames by video prefix

# ---------------------------

def group_frames_by_video(folder_path):

"""

Given folder_path containing many jpg files named like "video1.mp4_f120.jpg",

returns dict: {video_prefix: [fullpath1, fullpath2, ...]}

"""

files = sorted(glob.glob(os.path.join(folder_path, "*.jpg")))

groups = defaultdict(list)

for f in files:

name = os.path.basename(f)

# extract prefix before "_f" (robust)

if "_f" in name:

prefix = name.split("_f")[0]

else:

# fallback: take whole name without extension

prefix = os.path.splitext(name)[0]

groups[prefix].append(f)

# sort each group's frames by filename (so temporal order is preserved)

for k in groups:

groups[k] = sorted(groups[k])

return groups
```


# Explain
**`group_frames_by_video()`**  
একদম **লাইন–বাই–লাইন**, **সহজ ভাষায়**, **কোথায়/কেন ব্যবহার হয়** — সম্পূর্ণ ব্যাখ্যা দিলাম।

---

# ✅ **Function: `group_frames_by_video` (Line-by-Line Explanation)**

```python
def group_frames_by_video(folder_path):
```

### ✔ কি করছে?

- একটি ফোল্ডার path নেয় যেখানে অনেকগুলো `.jpg` frame আছে
    
- এগুলোকে ভিডিও অনুযায়ী group করে dictionary return করবে।
    

---

```python
    """
    Given folder_path containing many jpg files named like "video1.mp4_f120.jpg",
    returns dict: {video_prefix: [fullpath1, fullpath2, ...]}
    """
```

### ✔ Documentation / comment:

- Input: এমন ফোল্ডার যেখানে frame files এর নাম এই রকম:  
    `video1.mp4_f120.jpg`
    
- Output: dictionary  
    `{ "video1.mp4": [frame1_path, frame2_path, ...] }`
    

---

```python
    files = sorted(glob.glob(os.path.join(folder_path, "*.jpg")))
```

### ✔ কি করছে?

1. `os.path.join(folder_path, "*.jpg")`  
    → folder-এর সব `.jpg` ফাইল match করবে
    
2. `glob.glob(...)`  
    → সেই ফাইলগুলোর list return করবে
    
3. `sorted(...)`  
    → alphabetically sort করবে
    

**কেন sorting?**  
Frame sequence missing হলে proper order important।

---

```python
    groups = defaultdict(list)
```

### ✔ কি করছে?

- একটি dictionary বানাচ্ছে
    
- যেখানে প্রতিটি key (video name) এর value হবে **একটি list**।
    

**defaultdict(list)** মানে:  
key না থাকলেও automatic empty list দিয়ে শুরু করবে।

---

```python
    for f in files:
```

### ✔ কি করছে?

- প্রতিটি frame file এর উপর loop।
    

---

```python
        name = os.path.basename(f)
```

### ✔ কি করছে?

- Full path থেকে শুধুমাত্র file name বের করছে  
    যেমন: `"final_dataset/video1.mp4_f120.jpg"` → `"video1.mp4_f120.jpg"`
    

---

```python
        # extract prefix before "_f" (robust)
        if "_f" in name:
            prefix = name.split("_f")[0]
```

### ✔ কেন করা হচ্ছে?

Frame file নামের structure:

```
video1.mp4_f120.jpg
```

এখানে:

- `video1.mp4` = video name
    
- `_f120` = frame number (frame 120)
    

**Split logic:**  
`name.split("_f")` → `["video1.mp4", "120.jpg"]`

তাই prefix = `"video1.mp4"`  
অর্থাৎ ভিডিওর নাম।

---

```python
        else:
            # fallback: take whole name without extension
            prefix = os.path.splitext(name)[0]
```

### ✔ কেন fallback?

যদি `_f` পাওয়া না যায় (rare cases):

- পুরো নাম থেকে extension বাদ দিয়ে prefix নেয়।
    

Example:  
`image123.jpg` → `image123`

---

```python
        groups[prefix].append(f)
```

### ✔ কি করছে?

- এই ভিডিওর prefix key তে frame file path add করছে।
    

Example:

```
groups["video1.mp4"] = [
   "video1.mp4_f1.jpg",
   "video1.mp4_f2.jpg",
   ...
]
```

---

```python
    # sort each group's frames by filename (so temporal order is preserved)
    for k in groups:
        groups[k] = sorted(groups[k])
```

### ✔ কেন আরেকবার sort?

যদি frame naming disorder থাকে:

- `_f1.jpg`, `_f10.jpg`, `_f2.jpg` alphabetical এ ভুল হয়
    
- তাই নিশ্চিত করার জন্য প্রতিটি ভিডিওর frame list আবার sort করা হয়।
    

---

```python
    return groups
```

### ✔ Output:

একটি dictionary return করে:

```
{
  "video1.mp4": [
      "/path/video1.mp4_f1.jpg",
      "/path/video1.mp4_f2.jpg",
      ...
  ],
  "video2.mp4": [...],
  ...
}
```

---

# 🎯 **Where Is This Function Used?**

এই function সাধারণত এই জায়গায় ব্যবহার হয়:

✔ LSTM বা CNN-LSTM Model এ  
✔ Video dataset কে frames হিসাবে process করতে  
✔ প্রতি ভিডিওর frames sequentially load করতে  
✔ SEQ_LEN অনুযায়ী frame window তৈরি করতে  
✔ Video-level prediction এর জন্য frame grouping দরকার

----



```python
# ---------------------------

# Dataset

# ---------------------------

class VideoFrameSequenceDataset(Dataset):

"""

Create sequence windows from grouped frames of videos.

Each sample is a tensor of shape (SEQ_LEN, C, H, W) and a label (0 or 1).

"""

def __init__(self, root_dir, split="train", seq_len=8, transforms=None, balance=True):

"""

root_dir layout:

root_dir/Normal/{split}/*.jpg

root_dir/Suspicious/{split}/*.jpg

"""

super().__init__()

self.seq_len = seq_len

self.transforms = transforms

  

# Build grouped lists per class

self.data = [] # list of tuples: (list_of_frame_paths_in_window, label)

classes = {"Normal": 0, "Suspicious": 1}

for cls_name, label in classes.items():

folder = os.path.join(root_dir, cls_name, split)

if not os.path.exists(folder):

continue

groups = group_frames_by_video(folder) # dict: video_prefix -> [frames]

# for each group we produce multiple windows

for prefix, frames in groups.items():

n = len(frames)

if n == 0:

continue

if n < seq_len:

# pad by repeating last frame (or loop) to make length = seq_len

padded = frames + [frames[-1]] * (seq_len - n)

self.data.append((padded, label))

else:

# create sliding windows with stride = seq_len//2 (overlap)

stride = max(1, seq_len // 2)

for start in range(0, n - seq_len + 1, stride):

window = frames[start:start + seq_len]

self.data.append((window, label))

# also include last window that ends at last frame to cover tail

if (n - seq_len) % stride != 0:

window = frames[-seq_len:]

self.data.append((window, label))

  

# Optionally balance by undersampling majority class

if balance:

self._balance()

  

def _balance(self):

# find counts per label and undersample the larger to match smaller

by_label = defaultdict(list)

for item in self.data:

by_label[item[1]].append(item)

counts = {lbl: len(lst) for lbl, lst in by_label.items()}

if len(counts) < 2:

return

min_count = min(counts.values())

new_data = []

for lbl, lst in by_label.items():

random.shuffle(lst)

new_data.extend(lst[:min_count])

random.shuffle(new_data)

self.data = new_data

  

def __len__(self):

return len(self.data)

  

def __getitem__(self, idx):

frame_paths, label = self.data[idx]

frames = []

for p in frame_paths:

img = Image.open(p).convert("RGB")

if self.transforms:

img = self.transforms(img)

frames.append(img) # each is CxHxW tensor

# stack -> shape (SEQ_LEN, C, H, W)

frames = torch.stack(frames, dim=0)

return frames, torch.tensor(label, dtype=torch.long)
```


# Explain
নীচে তোমার **`VideoFrameSequenceDataset`** class-টি **লাইন-বাই-লাইন**, **কোথায় ব্যবহৃত হয়**, **কেন দরকার**, এবং **কি উদ্দেশ্যে**—এই তিনটি দিক থেকে সম্পূর্ণ ব্যাখ্যা দিচ্ছি।

---

# 🔥 **Dataset Class Explained (When, Where, Why Needed)**

এই class মূলত **video frames → sequence tensor** তৈরি করার জন্য ব্যবহৃত হয়, যাতে **CNN → LSTM** video classification model train করা যায়।

---

# --------------------------------------------------

# ✅ **Class Definition**

# --------------------------------------------------

```python
class VideoFrameSequenceDataset(Dataset):
```

### ✔ What?

PyTorch dataset class → custom video frame loader।

### ✔ Why needed?

- PyTorch DataLoader এ কাজ করার জন্য
    
- video কে frame sequence করে model-এ পাঠানোর জন্য
    

### ✔ Where used?

`DataLoader(dataset, batch_size)` এ load করার সময়।

---

```python
    """
    Create sequence windows from grouped frames of videos.
    Each sample is a tensor of shape (SEQ_LEN, C, H, W) and a label (0 or 1).
    """
```

### ✔ Why needed?

Model expects fixed-length sequence → (8 frames)

### ✔ Where used?

Training ও validation pipeline-এ।

---

# --------------------------------------------------

# ✅ ****init**()**

# --------------------------------------------------

```python
def __init__(self, root_dir, split="train", seq_len=8, transforms=None, balance=True):
```

### ✔ What?

Dataset initialize করা।

### ✔ Why needed?

- কোন folder থেকে frames নেবে
    
- train/test split অনুযায়ী load
    
- sequence length maintain
    
- data balancing
    

### ✔ When used?

Dataset তৈরি করার সময়:

```python
trainset = VideoFrameSequenceDataset(DATA_DIR, split="train")
```

---

```python
super().__init__()
```

### ✔ Why?

PyTorch Dataset parent class initialize করে।

---

```python
self.seq_len = seq_len
self.transforms = transforms
```

### ✔ Why?

- frames কতগুলো নেবে
    
- কোন preprocessing apply হবে (resize, normalize ইত্যাদি)
    

---

### 📂 **Folder Structure Explanation**

```python
root_dir/Normal/train/*.jpg
root_dir/Normal/test/*.jpg

root_dir/Suspicious/train/*.jpg
root_dir/Suspicious/test/*.jpg
```

### ✔ Why this split?

Supervised learning → label needed

---

```python
self.data = [] 
```

### ✔ Why?

অবশেষে সব sample এখানে store হবে:

```
[(list_of_frames, label), (list_of_frames, label)...]
```

---

```python
classes = {"Normal": 0, "Suspicious": 1}
```

### ✔ Why?

Two-class classifier → label encoding needed  
Video classification output হবে 0 বা 1।

---

# --------------------------------------------------

# 🔍 **Frame Grouping**

# --------------------------------------------------

```python
folder = os.path.join(root_dir, cls_name, split)
```

বর্তমান class এবং split অনুযায়ী folder path।

---

```python
groups = group_frames_by_video(folder)
```

### ✔ Where?

আগে তোমার লেখা utility function।

### ✔ Why?

এক ভিডিওর সব frames grouping করতে:

```
video1.mp4_f1.jpg
video1.mp4_f2.jpg
video1.mp4_f3.jpg

→ groups["video1.mp4"] = [frame1, frame2, frame3]
```

---

# --------------------------------------------------

# 🔄 **Window (Sequence) Creation**

# --------------------------------------------------

## 👉 Case-1: frame count < seq_len

```python
if n < seq_len:
    padded = frames + [frames[-1]] * (seq_len - n)
    self.data.append((padded, label))
```

### ✔ Why?

Some videos have fewer frames → LSTM requires fixed length.  
So last frame repeat করে fixed length তৈরি।

### ✔ When?

Short video inputs.

---

## 👉 Case-2: Enough frames → sliding windows

```python
stride = max(1, seq_len // 2)
```

### ✔ Why?

Overlap windows → more training samples  
Example: seq_len = 8 → stride = 4

---

```python
for start in range(0, n - seq_len + 1, stride):
    window = frames[start:start + seq_len]
    self.data.append((window, label))
```

### ✔ Why?

From long video, multiple sequences generate করা:

Frames: f1 f2 f3 ... f20  
Window-1 → f1–f8  
Window-2 → f4–f12  
Window-3 → f8–f16  
Window-4 → f12–f20

---

```python
# include last leftover window
if (n - seq_len) % stride != 0:
    window = frames[-seq_len:]
    self.data.append((window, label))
```

### ✔ Why?

শেষের frames যেন বাদ না পড়ে।

---

# --------------------------------------------------

# ⚖️ **Balancing Function**

# --------------------------------------------------

```python
if balance:
    self._balance()
```

### ✔ Why?

Dataset balanced না হলে:

- Model majority class বেশি শিখবে
    
- Accuracy misleading হবে
    

So undersample করে equal করা হয়।

---

### 🔍 _balance() Explained

```python
by_label = defaultdict(list)
```

Label অনুযায়ী grouping।

---

```python
counts = {lbl: len(lst) for lbl, lst in by_label.items()}
min_count = min(counts.values())
```

Smallest class find।

---

```python
new_data.extend(lst[:min_count])
```

সব class কে equal করা হয়।  
Undersampling → Overfitting কমে।

---

# --------------------------------------------------

# 📌 **len**()

# --------------------------------------------------

```python
def __len__(self):
    return len(self.data)
```

### ✔ Why?

PyTorch DataLoader জানতে চায় dataset size।

---

# --------------------------------------------------

# 📌 **getitem**()

# --------------------------------------------------

```python
frame_paths, label = self.data[idx]
```

এক sample load করা।

---

```python
img = Image.open(p).convert("RGB")
```

### ✔ Why?

- Frame load
    
- Ensure RGB format (some JPEG might be grayscale)
    

---

```python
if self.transforms:
    img = self.transforms(img)
```

### ✔ Why?

- Resize
    
- Normalize
    
- Convert To Tensor
    
- Data augmentation (rotation, flip, crop)
    

---

```python
frames.append(img)
```

একটি sample = frames list

---

```python
frames = torch.stack(frames, dim=0)
```

### ✔ Why?

Convert list → tensor shape:

```
(SEQ_LEN, C, H, W)
```

Model input format.

---

```python
return frames, torch.tensor(label, dtype=torch.long)
```

### ✔ Why?

Model training requires tensor labels.

---

# 🎯 Summary Table

| অংশ             | কেন দরকার               | কোথায় ব্যবহৃত          |
| --------------- | ----------------------- | ---------------------- |
| Frame grouping  | এক ভিডিওর frames সংগ্রহ | sliding windows বানাতে |
| Sliding window  | sequence তৈরি           | LSTM input             |
| Padding         | short videos handle     | fixed length           |
| Balance         | class imbalance fix     | training stability     |
| Transforms      | preprocessing           | CNN input              |
| Return sequence | (8 × 3 × 224 × 224)     | CNN-LSTM model         |

---


```python
# ---------------------------

# Transforms

# ---------------------------

train_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.RandomHorizontalFlip(),

T.ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),

])

  

eval_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),

])
```


# Explain

নীচে তোমার **Transforms 부분**–টি সম্পূর্ণভাবে **when, where, why needed**—এই তিনটি দিক থেকে পরিষ্কারভাবে ব্যাখ্যা করে দিচ্ছি।

---

# 🧩 **TRANSFORMS — When, Where, Why Needed**

Transforms হল **preprocessing + data augmentation**।  
Image model → CNN (ResNet) ইনপুট হিসেবে **tensor** এবং **fixed size** চায়, তাই transform দরকার।

---

# -----------------------------------------------------------------

# 🔥 TRAIN TRANSFORMS (Training Time)

# -----------------------------------------------------------------

```python
train_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.RandomHorizontalFlip(),
    T.ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
])
```

### 📌 WHEN USED?

Training data load করার সময়:

```python
trainset = VideoFrameSequenceDataset(..., transforms=train_transforms)
```

---

# 🧠 WHERE USED?

Inside dataset:

```python
if self.transforms:
    img = self.transforms(img)
```

---

# 📌 WHY NEEDED? (Line by Line)

---

## 1️⃣ `T.Resize((FRAME_SIZE, FRAME_SIZE))`

### ✔ Why?

- CNN (ResNet) fixed-size input চায় → 224×224
    
- বিভিন্ন ভিডিওতে বিভিন্ন আকারের frame থাকে → resize করতে হয়
    

### ✔ When?

সব training ও validation frame।

---

## 2️⃣ `T.RandomHorizontalFlip()`

### ✔ Why?

Data Augmentation  
Randomly left-right flip → Model more robust  
Examples:

- Suspicious activity left/right direction হোক—model confuse না হয়
    

### ✔ When?

Only **training time**, never in eval.

---

## 3️⃣ `T.ColorJitter(...)`

### ✔ Why?

Real-world videos এর light conditions always same নয়

- Darkness
    
- Bright sunlight
    
- Different camera sensors  
    এগুলোতে robust করতে।
    

### ✔ When?

Training only  
(Not for validation/test because output deterministic হতে হবে)

---

## 4️⃣ `T.ToTensor()`

### ✔ Why?

PIL image → PyTorch tensor (C×H×W)  
Pixel values change:

- [0..255] → [0..1]
    

### ✔ When?

Every frame, always।

---

## 5️⃣ `T.Normalize(mean, std)`

### ✔ Why?

Normalize করে model faster converge করতে পারে  
Pretrained ResNet expects:

```
mean = [0.485, 0.456, 0.406]
std  = [0.229, 0.224, 0.225]
```

These are ImageNet statistics.

### ✔ When?

Every input on training, validation, test.

---

# -----------------------------------------------------------------

# 🌟 EVALUATION TRANSFORMS (Validation/Test)

# -----------------------------------------------------------------

```python
eval_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
])
```

---

# 🧐 WHY NO FLIP OR COLORJITTER HERE?

### Because evaluation must be **deterministic & stable**:

❌ No Random Flip  
❌ No Color Jitter  
Otherwise validation accuracy random হয়ে যাবে।

---

# 🎯 Summary Table

| Transform            | Train | Eval | Why Needed                        |
| -------------------- | ----- | ---- | --------------------------------- |
| Resize               | ✔     | ✔    | Fixed size for CNN                |
| RandomHorizontalFlip | ✔     | ❌    | Data augmentation                 |
| ColorJitter          | ✔     | ❌    | Robust to lighting changes        |
| ToTensor             | ✔     | ✔    | PyTorch tensor format             |
| Normalize            | ✔     | ✔    | Match pretrained CNN expectations |

---

```python 
# ---------------------------

# Model: ResNet (feature extractor) + LSTM + classifier

# ---------------------------

class CNNEncoder(nn.Module):

def __init__(self, embed_size=512, pretrained=True, freeze=False):

super().__init__()

resnet = models.resnet18(pretrained=pretrained)

# remove last fc

modules = list(resnet.children())[:-1] # remove FC layer

self.backbone = nn.Sequential(*modules) # outputs (B, 512, 1, 1)

self.embed_size = embed_size

if freeze:

for p in self.backbone.parameters():

p.requires_grad = False

  

def forward(self, x):

# x: (B, C, H, W)

feat = self.backbone(x) # (B, 512, 1, 1)

feat = feat.view(feat.size(0), -1) # (B, 512)

return feat # (B, feature_dim)
```


# Explain
Below is a **clear, deep, beginner-friendly explanation** of your `CNNEncoder` class:

---

# ✅ **Why CNN + LSTM?**

This model is designed for **video classification / action recognition**.

- **CNN (ResNet18)** extracts spatial features from each video frame  
    → e.g., edges, colors, textures, shapes, objects
    
- **LSTM** processes the **sequence of frame features**  
    → learns motion patterns over time
    
- **Classifier** predicts the final class.
    

So your `CNNEncoder` is the **feature extractor**.

---

# 🔍 **Explain the CNNEncoder Class (When, Where, Why)**

## ✅ **Where is this used?**

- Inside your main model before the LSTM.
    
- For each frame of the video, CNNEncoder produces a **feature vector of size 512**.
    

Used pipeline:

```
Frame → CNNEncoder → (feature vector) → LSTM → classifier
```

---

# 🟥 **Breakdown of the Code**

## 1️⃣ `class CNNEncoder(nn.Module):`

You define a PyTorch neural network module for CNN-based feature extraction.

---

## 2️⃣ `resnet = models.resnet18(pretrained=pretrained)`

### **Why needed?**

- You load **ResNet18**, a CNN trained on **ImageNet**.
    
- Pretrained helps because it already knows:
    
    - edges
        
    - corners
        
    - textures
        
    - objects (dog, person, hand, ball, etc.)
        

This dramatically accelerates training and improves accuracy.

### **When used?**

- During training & evaluation, every time you pass a frame.
    

### **Where?**

- In `__init__()` to construct the CNN backbone.
    

---

## 3️⃣ `modules = list(resnet.children())[:-1]`

### **What this does?**

- ResNet18 has many layers ending with a final `FC` classification layer.
    
- You remove the last layer (`fc`) because:  
    ✔ we do not want ImageNet classification  
    ✔ we only want its **feature vector**
    

ResNet output normally:

```
(B, 1000) → 1000 ImageNet classes
```

After removing FC:

```
(B, 512, 1, 1) → feature vector
```

### **Why needed?**

- You want to extract _generic_ feature vectors, not classify.
    

---

## 4️⃣ `self.backbone = nn.Sequential(*modules)`

You rebuild ResNet without the last fully connected layer.

---

## 5️⃣ Freezing the backbone (optional)

```
if freeze:
    for p in self.backbone.parameters():
        p.requires_grad = False
```

### **Why freeze?**

To **speed up training** and avoid overfitting if:

- your dataset is small
    
- the model overfits easily
    
- GPU resources are limited
    

Frozen → Only LSTM + classifier learn.

### **When to freeze?**

- When training small datasets, e.g., < 10k images or small video dataset.
    

---

## 6️⃣ `def forward(self, x):`

This defines how the model processes a frame.

### **Input**

`x`: batch of frames  
shape → `(B, 3, H, W)`

### Step-by-step:

---

## 7️⃣ `feat = self.backbone(x)`

ResNet processes the images.

Output:

```
(B, 512, 1, 1)
```

This means:

- 512 filters
    
- each reduced to 1×1 (global average pooling)
    

---

## 8️⃣ `feat = feat.view(feat.size(0), -1)`

Flatten to:

```
(B, 512)
```

This is now a **feature vector per frame**, ready for LSTM.

### **Why needed?**

LSTM cannot understand images.  
It only understands sequences of vectors (numbers).

So CNN encodes images → vector representation  
Then LSTM encodes motion → temporal representation

---

# 🟩 Summary: Why CNNEncoder is Needed?

| Purpose                     | Explanation                                      |
| --------------------------- | ------------------------------------------------ |
| **Extract visual features** | Turns raw images into meaningful feature vectors |
| **Use pretrained ResNet**   | Faster training, higher accuracy                 |
| **Remove FC layer**         | We don’t want ImageNet classification            |
| **Flatten output**          | LSTM needs 2D shape: `(Batch, FeatureSize)`      |
| **Optionally freeze CNN**   | Speeds up training and reduces overfitting       |

---

# 🟦 Practical Example

### Input:

1 frame → CNNEncoder  
Output: 512-dimensional vector

### Example:

```
Frame 1 → [512 numbers]
Frame 2 → [512 numbers]
Frame 3 → [512 numbers]
...
```

These feature vectors go into the LSTM to learn motion.

---


```python
class CNNLSTMModel(nn.Module):

def __init__(self, feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False):

super().__init__()

self.feat_dim = feat_dim

self.cnn = CNNEncoder(pretrained=PRETRAINED, freeze=FREEZE_CNN)

self.lstm = nn.LSTM(input_size=feat_dim,

hidden_size=lstm_hidden,

num_layers=lstm_layers,

batch_first=True,

bidirectional=bidirectional)

factor = 2 if bidirectional else 1

self.classifier = nn.Sequential(

nn.Linear(lstm_hidden * factor, 128),

nn.ReLU(),

nn.Dropout(0.5),

nn.Linear(128, num_classes)

)

  

def forward(self, x):

# x: (B, SEQ_LEN, C, H, W)

B, S, C, H, W = x.shape

x = x.view(B * S, C, H, W) # (B*S, C, H, W)

feats = self.cnn(x) # (B*S, feat_dim)

feats = feats.view(B, S, -1) # (B, S, feat_dim)

out, _ = self.lstm(feats) # (B, S, hidden)

# use last time-step

last = out[:, -1, :] # (B, hidden*dir)

logits = self.classifier(last) # (B, num_classes)

return logits
```


# Explain
Below is a **super-clean, beginner-friendly, interview-friendly breakdown** of your **CNN + LSTM model** — **when, where, why each part is needed.**

---

# 🧠 **What This Model Does**

This is a **video classification / action recognition model**.

- **CNN (ResNet)** → understands _each frame_
    
- **LSTM** → understands _motion over time_ (frame sequence)
    
- **Classifier** → predicts final category (e.g., fight / non-fight)
    

---

# 🔍 **Explain the CNNLSTMModel Class**

---

# 1️⃣ Constructor (`__init__`)

```
class CNNLSTMModel(nn.Module):
```

You define a deep learning architecture for **sequence of frames**.

---

## ✳️ `self.cnn = CNNEncoder(...)`

### **Where?**

Used inside training and evaluation.

### **When?**

Called once for **every frame** in the video.

### **Why needed?**

- CNN extracts **spatial features** from each image.
    
- Converts image (3×H×W) → 512-dim feature vector.
    

Without CNN, LSTM would receive raw images → impossible.

---

## ✳️ LSTM layer

```
self.lstm = nn.LSTM(input_size=feat_dim,
                    hidden_size=lstm_hidden,
                    num_layers=lstm_layers,
                    batch_first=True,
                    bidirectional=bidirectional)
```

### **Where?**

Applied after all frame features are extracted.

### **When?**

Every forward pass on a batch of videos.

### **Why needed?**

LSTM learns **temporal patterns (motion)**, for example:

- punching movement
    
- running
    
- waving
    
- falling
    
- suspicious activity
    

CNN sees individual _frames_  
LSTM sees _movement between frames_

---

## ✳️ Bidirectional Option

```
factor = 2 if bidirectional else 1
```

### Why needed?

Bidirectional LSTM can see:

- forward time
    
- backward time
    

Useful if entire video is available.

---

## ✳️ Classifier (FC layers)

```
self.classifier = nn.Sequential(
    nn.Linear(lstm_hidden * factor, 128),
    nn.ReLU(),
    nn.Dropout(0.5),
    nn.Linear(128, num_classes)
)
```

### **Where?**

After LSTM produces final sequence output.

### **Why needed?**

Transforms LSTM output → predicted class.

Breakdown:

- `Linear` → dense layer for representation learning
    
- `ReLU` → non-linear activation
    
- `Dropout` → avoid overfitting
    
- Final `Linear` → output probabilities / logits
    

---

# 2️⃣ Forward Pass (`forward()`)

```
def forward(self, x):
```

Input:

```
(Batch, Seq_len, C, H, W)
```

Example: (8 videos, 20 frames each)

---

## Step 1: Combine batch with sequence

```
x = x.view(B * S, C, H, W)
```

### **Where?**

Before feeding into CNN.

### **Why needed?**

CNN expects:

```
(BATCH, 3, H, W)
```

Not:

```
(BATCH, SEQ, 3, H, W)
```

So we stack all frames like:

```
(B*S) frames → feed into CNN at once
```

---

## Step 2: CNN extracts features

```
feats = self.cnn(x)     # (B*S, feat_dim)
```

### **Why needed?**

This converts each frame into a **vector** of size 512.

Now the LSTM can process temporal sequences.

---

## Step 3: Reshape back into sequence format

```
feats = feats.view(B, S, -1)
```

Output shape:

```
(Batch, Sequence, Feature_dim)
```

### **Why needed?**

LSTM expects sequential input:

```
[feat1, feat2, feat3, ...]
```

---

## Step 4: Feed into LSTM

```
out, _ = self.lstm(feats)
```

### Output:

```
out: (B, S, hidden_size)
```

### **Why needed?**

LSTM extracts **temporal context**, e.g.,  
“How are objects moving across frames?”

---

## Step 5: Use only the last time step

```
last = out[:, -1, :]
```

### **Why needed?**

The final frame representation contains:

- accumulated temporal memory
    
- summary of whole sequence
    

Perfect for final classification.

---

## Step 6: Classifier

```
logits = self.classifier(last)
```

### **Why needed?**

Convert hidden representation → class logits.

---

# ⭐ Final Output

```
Return logits → (Batch, num_classes)
```

Example for 2 classes:

```
[1.5, -0.8] → predict class 0
```

---

# 🟦 Full Summary (1 Minute Revision)

| Part            | Purpose                               |
| --------------- | ------------------------------------- |
| CNNEncoder      | Extracts features from frames         |
| LSTM            | Learns temporal motion from sequences |
| Linear Layers   | Final classification                  |
| Flatten/Reshape | Fit tensors for CNN and LSTM          |
| Last LSTM step  | Best summary of whole video           |
| Logits          | Output predictions                    |

This architecture is used in:

- action recognition
    
- violence detection
    
- gesture recognition
    
- human activity recognition
    
- video anomaly detection
    

---


```python
# ---------------------------

# Train / Eval helpers

# ---------------------------

def accuracy(preds, labels):

preds = torch.argmax(preds, dim=1)

return (preds == labels).float().mean().item()

  
  

def train_epoch(model, loader, criterion, optimizer):

model.train()

running_loss = 0.0

running_acc = 0.0

for frames, labels in tqdm(loader, desc="Train", leave=False):

frames = frames.to(DEVICE) # (B, S, C, H, W)

labels = labels.to(DEVICE)

optimizer.zero_grad()

outputs = model(frames)

loss = criterion(outputs, labels)

loss.backward()

torch.nn.utils.clip_grad_norm_(model.parameters(), 5.0)

optimizer.step()

  

running_loss += loss.item() * frames.size(0)

running_acc += accuracy(outputs.detach().cpu(), labels.detach().cpu()) * frames.size(0)

  

n = len(loader.dataset)

return running_loss / n, running_acc / n
```

# Explain
Below is a **deeply detailed and beginner-friendly explanation** of your **train helper functions**, line by line — _why needed, when used, where it fits in the pipeline_.

---

# ✅ 1. **accuracy(preds, labels)**

```
def accuracy(preds, labels):
    preds = torch.argmax(preds, dim=1)
    return (preds == labels).float().mean().item()
```

### 🔹 **`torch.argmax(preds, dim=1)`**

- `preds` = model outputs (logits), shape: `(BATCH, NUM_CLASSES)`
    
- You choose the **index with highest logit**
    
- Example:  
    `[1.2, -0.8] → class 0`.
    

### 🔹 `(preds == labels)`

- Compares prediction vs. true label → returns tensor of booleans `[True, False, ...]`.
    

### 🔹 `.float().mean()`

- Converts True=1, False=0
    
- Mean gives accuracy for the batch.
    

### 🔹 `.item()`

- Convert tensor → Python float.
    

### **📌 When used?**

- During both **training** and **validation** to measure performance.
    

### **📌 Why needed?**

- Loss alone doesn’t show how many predictions are correct; accuracy is easier to interpret.
    

---

# ✅ 2. **train_epoch()**

```
def train_epoch(model, loader, criterion, optimizer):
```

This runs **one full training epoch** on the training DataLoader.

---

## 🔹 `model.train()`

```
model.train()
```

### **Why needed?**

Turns ON:

- dropout
    
- batchnorm learning
    
- gradient updates
    

Without this, your model behaves like eval mode → training becomes wrong.

---

## 🔹 Initialize accumulators

```
running_loss = 0.0
running_acc = 0.0
```

### Why needed?

To compute average loss & accuracy over the entire epoch.

---

## 🔹 Loop over all batches

```
for frames, labels in tqdm(loader, desc="Train", leave=False):
```

### Where?

DataLoader returns:

- `frames` → (B, Seq_len, C, H, W)
    
- `labels` → class ID
    

### Why needed?

Iterating batch-by-batch:

- reduces GPU memory load
    
- allows gradient updates many times per epoch
    

`tqdm` gives progress bar.

---

## 🔹 Move data to GPU/CPU

```
frames = frames.to(DEVICE)
labels = labels.to(DEVICE)
```

### Why needed?

Model is on GPU → data must also be on same device.

---

## 🔹 Reset gradients

```
optimizer.zero_grad()
```

### Why needed?

PyTorch accumulates gradients by default.  
This clears previous gradients before backprop.

---

## 🔹 Forward pass

```
outputs = model(frames)
```

### Why needed?

Model predicts logits for each video.

---

## 🔹 Compute loss

```
loss = criterion(outputs, labels)
```

Common criterion:

- CrossEntropyLoss for classification
    

Loss tells _how wrong_ predictions are.

---

## 🔹 Backpropagation

```
loss.backward()
```

Computes gradients of model parameters.

---

## 🔹 Gradient clipping

```
torch.nn.utils.clip_grad_norm_(model.parameters(), 5.0)
```

### Why needed?

LSTMs are vulnerable to **exploding gradients**.  
Clipping prevents training instability.

---

## 🔹 Update weights

```
optimizer.step()
```

Updates parameters using computed gradients.

---

## 🔹 Accumulate loss

```
running_loss += loss.item() * frames.size(0)
```

### Why multiply by batch size?

To compute **total loss for entire dataset**, not average per batch.

---

## 🔹 Accumulate accuracy

```
running_acc += accuracy(outputs.detach().cpu(), labels.detach().cpu()) * frames.size(0)
```

### Why `detach()`?

- Prevent gradient tracking
    
- Reduce memory usage
    

### Why `.cpu()`?

Accuracy function operates on CPU.

---

## 🔹 Compute epoch averages

```
n = len(loader.dataset)
return running_loss / n, running_acc / n
```

### Why?

You collected:

- **total loss**
    
- **total accuracy**
    

So divide by total number of samples to get averages.

---

# 🎯 **Final Summary (Short Version)**

| Code part           | Why needed?                 | When used?         |
| ------------------- | --------------------------- | ------------------ |
| `model.train()`     | Enables training mode       | Beginning of epoch |
| `zero_grad()`       | Clear old gradients         | Before backward()  |
| `forward()`         | Get predictions             | Every batch        |
| `criterion`         | Compute loss                | Every batch        |
| `loss.backward()`   | Compute gradients           | Every batch        |
| `clip_grad_norm_`   | Prevent exploding gradients | Every batch        |
| `optimizer.step()`  | Update model weights        | Every batch        |
| `accuracy()`        | Calculate % correct         | After prediction   |
| Accumulate loss/acc | To compute epoch averages   | Every batch        |
| Return avg metrics  | For logs & evaluation       | End of epoch       |

---


```python
def eval_epoch(model, loader, criterion):

model.eval()

running_loss = 0.0

running_acc = 0.0

with torch.no_grad():

for frames, labels in tqdm(loader, desc="Eval", leave=False):

frames = frames.to(DEVICE)

labels = labels.to(DEVICE)

outputs = model(frames)

loss = criterion(outputs, labels)

running_loss += loss.item() * frames.size(0)

running_acc += accuracy(outputs.detach().cpu(), labels.detach().cpu()) * frames.size(0)

n = len(loader.dataset)

return running_loss / n, running_acc / n
```


# Explain
Below is a **line-by-line explanation** of your **eval_epoch()** function — with clear explanations of **when, where, and why** each line is needed.

---

# ✅ **eval_epoch(model, loader, criterion)**

Used **during validation/testing** to measure model performance **without training**.

```
def eval_epoch(model, loader, criterion):
```

- `model` → your CNN-LSTM
    
- `loader` → validation DataLoader
    
- `criterion` → loss function (CrossEntropyLoss)
    

---

# 🔹 **model.eval()**

```
model.eval()
```

### ✅ Why needed?

- Turns OFF:
    
    - dropout
        
    - batchnorm updates
        
- Ensures consistent evaluation.
    

### 📌 When?

Before running validation or testing.

---

# 🔹 Initialize counters

```
running_loss = 0.0
running_acc = 0.0
```

### Why?

To accumulate total loss & accuracy over all validation samples.

---

# 🔹 Disable gradient calculation

```
with torch.no_grad():
```

### Why needed?

- Evaluation does NOT require gradients
    
- Saves **memory**
    
- Makes inference **faster**
    
- Prevents unwanted gradient accumulation
    

### When?

During validation/testing only.

---

# 🔹 Loop over all validation batches

```
for frames, labels in tqdm(loader, desc="Eval", leave=False):
```

### Why?

To evaluate every sample in validation set.

### What?

- `frames` → shape `(B, Seq, C, H, W)`
    
- `labels` → ground truth class
    
- `tqdm` → progress bar
    

---

# 🔹 Move data to GPU/CPU

```
frames = frames.to(DEVICE)
labels = labels.to(DEVICE)
```

### Why?

Model and data must be on same device (CPU or GPU).

---

# 🔹 Forward pass only (no backward)

```
outputs = model(frames)
```

### Why?

We need model predictions for validation loss & accuracy.

No gradient here because we are inside `torch.no_grad()`.

---

# 🔹 Compute loss

```
loss = criterion(outputs, labels)
```

### Why?

To measure how far predictions are from true labels.

---

# 🔹 Accumulate total loss

```
running_loss += loss.item() * frames.size(0)
```

### Why multiply by batch size?

Because:

- Loss returned is **average per batch**
    
- To compute total loss over entire dataset, we scale it by number of samples in this batch.
    

---

# 🔹 Accumulate accuracy

```
running_acc += accuracy(outputs.detach().cpu(), labels.detach().cpu()) * frames.size(0)
```

### Why `detach()`?

- Remove tensor from computational graph
    
- Necessary to prevent PyTorch from tracking gradients
    

### Why `.cpu()`?

Accuracy function runs on CPU to avoid GPU overhead.

### Why multiply by batch size?

Same reason as loss → to compute dataset-wide average accuracy.

---

# 🔹 Compute number of samples

```
n = len(loader.dataset)
```

### Why?

To calculate average metrics over the whole dataset.

---

# 🔹 Return average loss and accuracy

```
return running_loss / n, running_acc / n
```

### Why?

We accumulated totals → now convert to **mean values per sample**.

These two values are used to:

- log validation performance
    
- compare models
    
- save best model
    

---

# 🎯 Summary Table

|Code|Why Needed?|When?|
|---|---|---|
|`model.eval()`|Disable dropout, batchnorm|Before evaluation|
|`torch.no_grad()`|No gradient → faster, less memory|Entire validation pass|
|`outputs = model(frames)`|Make predictions|Each batch|
|`criterion(outputs, labels)`|Compute validation loss|Each batch|
|Accumulate loss/acc|For averaging|Each batch|
|Return averages|Monitoring & early stopping|End of validation|

---



```python
# ---------------------------

# Main training script

# ---------------------------

def main():

random.seed(RANDOM_SEED)

torch.manual_seed(RANDOM_SEED)

  

# datasets and loaders

train_ds = VideoFrameSequenceDataset(DATA_DIR, split="train", seq_len=SEQ_LEN, transforms=train_transforms)

val_ds = VideoFrameSequenceDataset(DATA_DIR, split="val", seq_len=SEQ_LEN, transforms=eval_transforms, balance=False)

print("Train samples:", len(train_ds), "Val samples:", len(val_ds))

  

train_loader = DataLoader(train_ds, batch_size=BATCH_SIZE, shuffle=True, num_workers=NUM_WORKERS, pin_memory=True)

val_loader = DataLoader(val_ds, batch_size=BATCH_SIZE, shuffle=False, num_workers=NUM_WORKERS, pin_memory=True)

  

# model

model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)

model = model.to(DEVICE)

  

criterion = nn.CrossEntropyLoss()

optimizer = optim.Adam(filter(lambda p: p.requires_grad, model.parameters()), lr=LR, weight_decay=WEIGHT_DECAY)

scheduler = optim.lr_scheduler.ReduceLROnPlateau(optimizer, mode="max", factor=0.5, patience=3)

  

best_val_acc = 0.0

for epoch in range(1, EPOCHS + 1):

print(f"\nEpoch {epoch}/{EPOCHS}")

train_loss, train_acc = train_epoch(model, train_loader, criterion, optimizer)

val_loss, val_acc = eval_epoch(model, val_loader, criterion)

  

print(f"Train Loss: {train_loss:.4f} | Train Acc: {train_acc:.4f}")

print(f"Val Loss: {val_loss:.4f} | Val Acc: {val_acc:.4f}")

  

scheduler.step(val_acc)

  

# save best

if val_acc > best_val_acc:

best_val_acc = val_acc

torch.save({

"epoch": epoch,

"model_state": model.state_dict(),

"optimizer_state": optimizer.state_dict(),

"val_acc": val_acc

}, MODEL_SAVE_PATH)

print(f"Saved best model (val_acc={val_acc:.4f}) -> {MODEL_SAVE_PATH}")

  

print("Training finished. Best val acc:", best_val_acc)

  
  

if __name__ == "__main__":

main()
```


# Explain

Below is a **fully expanded, clear, line-by-line explanation** of your **main training script** — including **when**, **where**, and **why** each line is needed.

---

# ✅ **MAIN TRAINING SCRIPT — FULL EXPLANATION**

```
def main():
```

Defines the main function that executes the entire training pipeline.

---

# 🔹 **Set Random Seeds**

```
    random.seed(RANDOM_SEED)
    torch.manual_seed(RANDOM_SEED)
```

### Why?

To ensure **reproducibility** → same dataset splitting, same weight initialization, same results every run.

### When?

At the very beginning of training.

---

# 🔹 **Create Training Dataset**

```
    train_ds = VideoFrameSequenceDataset(DATA_DIR, split="train", seq_len=SEQ_LEN, transforms=train_transforms)
```

### Why?

Loads video frames → groups → sequences → labeled data  
Applies **data augmentation** for generalization.

### When?

Before training starts.

---

# 🔹 **Create Validation Dataset**

```
    val_ds = VideoFrameSequenceDataset(DATA_DIR, split="val", seq_len=SEQ_LEN, transforms=eval_transforms, balance=False)
```

### Why?

Validation should NOT be augmented  
`balance=False` → keep real data distribution  
Used to monitor model performance.

---

# 🔹 **Print Dataset Counts**

```
    print("Train samples:", len(train_ds), "Val samples:", len(val_ds))
```

Good debugging step → helps confirm correct dataset loading.

---

# 🔹 **Create DataLoaders**

```
    train_loader = DataLoader(train_ds, batch_size=BATCH_SIZE, shuffle=True, num_workers=NUM_WORKERS, pin_memory=True)
```

### Why?

- Loads training samples in batches
    
- `shuffle=True` ensures better generalization
    
- `num_workers` loads data in parallel
    
- `pin_memory=True` speeds CPU→GPU transfer
    

---

```
    val_loader = DataLoader(val_ds, batch_size=BATCH_SIZE, shuffle=False, num_workers=NUM_WORKERS, pin_memory=True)
```

### Why?

- Validation should NOT shuffle
    
- Keeps same ordering for consistent evaluation
    

---

# 🔹 **Initialize Model**

```
    model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)
```

### Why?

Creates your CNN + LSTM hybrid model.

---

# 🔹 Move Model to GPU/CPU

```
    model = model.to(DEVICE)
```

### Why?

Training must occur on GPU if available.

---

# 🔹 Loss Function

```
    criterion = nn.CrossEntropyLoss()
```

### Why?

This is the standard classification loss for 2-class problems.

---

# 🔹 Optimizer (Adam)

```
    optimizer = optim.Adam(filter(lambda p: p.requires_grad, model.parameters()), lr=LR, weight_decay=WEIGHT_DECAY)
```

### Why?

- Adam works well with CNNs + LSTMs
    
- `filter(lambda p: p.requires_grad)` excludes frozen CNN parameters if freeze=True
    
- `weight_decay` adds L2 regularization (reduces overfitting)
    

---

# 🔹 Learning Rate Scheduler

```
    scheduler = optim.lr_scheduler.ReduceLROnPlateau(optimizer, mode="max", factor=0.5, patience=3)
```

### Why?

Automatically reduces LR when validation accuracy stops improving.

### When?

After each epoch.

---

# 🔹 Track Best Accuracy

```
    best_val_acc = 0.0
```

To save the best model.

---

# 🔹 Training Loop

```
    for epoch in range(1, EPOCHS + 1):
```

Runs training for the specified number of epochs.

---

# 🔹 Print progress

```
        print(f"\nEpoch {epoch}/{EPOCHS}")
```

---

# 🔹 Train for one epoch

```
        train_loss, train_acc = train_epoch(model, train_loader, criterion, optimizer)
```

### Why?

Runs forward + backward passes  
Updates weights

---

# 🔹 Evaluate on validation set

```
        val_loss, val_acc = eval_epoch(model, val_loader, criterion)
```

### Why?

Monitors performance  
Used for early stopping / model saving

---

# 🔹 Print results

```
        print(f"Train Loss: {train_loss:.4f} | Train Acc: {train_acc:.4f}")
        print(f"Val   Loss: {val_loss:.4f} | Val   Acc: {val_acc:.4f}")
```

---

# 🔹 Update Learning Rate Scheduler

```
        scheduler.step(val_acc)
```

### Why?

Reduce learning rate if validation accuracy stalls.

---

# 🔹 Save Best Model

```
        if val_acc > best_val_acc:
            best_val_acc = val_acc
            torch.save({
                "epoch": epoch,
                "model_state": model.state_dict(),
                "optimizer_state": optimizer.state_dict(),
                "val_acc": val_acc
            }, MODEL_SAVE_PATH)
            print(f"Saved best model (val_acc={val_acc:.4f}) -> {MODEL_SAVE_PATH}")
```

### Why?

- Prevents overfitting
    
- Saves best performing model
    
- Can resume training later because optimizer state is stored too.
    

---

# 🔹 Final Print

```
    print("Training finished. Best val acc:", best_val_acc)
```

---

# 🔹 Script Entry Point

```
if __name__ == "__main__":
    main()
```

### Why needed?

Ensures main() runs only when you execute the script directly, not when imported.

---




---------------

# Accuracy test


```python
import torch

from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

# from train_cnn_lstm import CNNLSTMModel, VideoFrameSequenceDataset, eval_transforms, SEQ_LEN, DATA_DIR

  

# ---------------------------

# Setup

# ---------------------------

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

  

# ---------------------------

# Load TEST Dataset

# final_dataset/Normal/test/*.jpg

# final_dataset/Suspicious/test/*.jpg

# ---------------------------

test_ds = VideoFrameSequenceDataset(

DATA_DIR,

split="test",

seq_len=SEQ_LEN,

transforms=eval_transforms,

balance=False

)

  

test_loader = torch.utils.data.DataLoader(

test_ds,

batch_size=1, # 1 sequence per batch

shuffle=False,

num_workers=2

)

  

print("Total Test Samples:", len(test_ds))

  

# ---------------------------

# Load Model

# ---------------------------

model = CNNLSTMModel(

feat_dim=512,

lstm_hidden=256,

lstm_layers=1,

num_classes=2,

bidirectional=False

).to(device)

  

checkpoint = torch.load("best_cnn_lstm.pth", map_location=device)

  

model.load_state_dict(checkpoint["model_state"])

model.eval()

  

# ---------------------------

# Evaluation Loop

# ---------------------------

all_preds = []

all_labels = []

  

with torch.no_grad():

for frames, labels in test_loader:

frames = frames.to(device) # (B=1, S, C, H, W)

labels = labels.to(device)

  

outputs = model(frames)

_, preds = torch.max(outputs, 1)

  

all_preds.extend(preds.cpu().numpy())

all_labels.extend(labels.cpu().numpy())

  

# ---------------------------

# Metrics

# ---------------------------

acc = accuracy_score(all_labels, all_preds)

prec = precision_score(all_labels, all_preds, zero_division=0)

rec = recall_score(all_labels, all_preds, zero_division=0)

f1 = f1_score(all_labels, all_preds, zero_division=0)

  

print(f"\n----- TEST METRICS -----")

print(f"Accuracy: {acc:.4f}")

print(f"Precision: {prec:.4f}")

print(f"Recall: {rec:.4f}")

print(f"F1-Score: {f1:.4f}")
```


# Explain
Here’s a **line-by-line explanation** of your **test/evaluation script** — including **when, where, and why** each part is used:

---

# ✅ 1. **Imports**

```python
import torch
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
# from train_cnn_lstm import CNNLSTMModel, VideoFrameSequenceDataset, eval_transforms, SEQ_LEN, DATA_DIR
```

### **Why**

- `torch` → load model, tensors, GPU support
    
- `sklearn.metrics` → compute evaluation metrics (accuracy, precision, recall, F1-score)
    
- Commented import → assumes CNNLSTMModel and dataset are defined elsewhere
    

### **When**

- At the very start of the script
    

---

# ✅ 2. **Setup device**

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```

### **Why**

- Detects GPU if available; otherwise CPU
    
- Needed for moving both **model** and **data** to the same device
    

---

# ✅ 3. **Load Test Dataset**

```python
test_ds = VideoFrameSequenceDataset(
    DATA_DIR,
    split="test",
    seq_len=SEQ_LEN,
    transforms=eval_transforms,
    balance=False
)
```

### **Why**

- Loads video frame sequences for testing
    
- `split="test"` → ensures only test data is used
    
- `transforms=eval_transforms` → standard resize & normalization, no augmentation
    
- `balance=False` → keep original distribution
    

---

```python
test_loader = torch.utils.data.DataLoader(
    test_ds,
    batch_size=1,              # 1 sequence per batch
    shuffle=False,
    num_workers=2
)
```

### **Why**

- `batch_size=1` → evaluates one video sequence at a time
    
- `shuffle=False` → keep deterministic order for metrics
    
- `num_workers=2` → parallel data loading
    

---

```python
print("Total Test Samples:", len(test_ds))
```

### **Why**

- Quick check to ensure the dataset is loaded correctly
    

---

# ✅ 4. **Load Model**

```python
model = CNNLSTMModel(
    feat_dim=512,
    lstm_hidden=256,
    lstm_layers=1,
    num_classes=2,
    bidirectional=False
).to(device)
```

### **Why**

- Creates model architecture
    
- Moves model to **GPU or CPU** as detected
    

---

```python
checkpoint = torch.load("best_cnn_lstm.pth", map_location=device)
```

### **Why**

- Loads previously saved **best model weights**
    
- `map_location=device` → ensures compatibility with GPU or CPU
    

---

```python
model.load_state_dict(checkpoint["model_state"])
model.eval()
```

### **Why**

- Loads weights into model
    
- `model.eval()` → disables dropout/batchnorm for evaluation
    

---

# ✅ 5. **Evaluation Loop**

```python
all_preds = []
all_labels = []
```

### **Why**

- Store predictions & true labels for metric calculation
    

---

```python
with torch.no_grad():
```

### **Why**

- Disable gradient computation → reduces memory usage and speeds up evaluation
    

---

```python
    for frames, labels in test_loader:
        frames = frames.to(device)        # (B=1, S, C, H, W)
        labels = labels.to(device)
```

### **Why**

- Move **input data** to the same device as the model
    

---

```python
        outputs = model(frames)
        _, preds = torch.max(outputs, 1)
```

### **Why**

- `outputs` → logits from model `(1, num_classes)`
    
- `torch.max(outputs, 1)` → chooses class with highest probability
    
- `_` → max value, `preds` → predicted class index
    

---

```python
        all_preds.extend(preds.cpu().numpy())
        all_labels.extend(labels.cpu().numpy())
```

### **Why**

- Move data to CPU
    
- Convert tensors to numpy arrays
    
- Store all predictions & labels for **final metric calculation**
    

---

# ✅ 6. **Compute Metrics**

```python
acc = accuracy_score(all_labels, all_preds)
prec = precision_score(all_labels, all_preds, zero_division=0)
rec = recall_score(all_labels, all_preds, zero_division=0)
f1 = f1_score(all_labels, all_preds, zero_division=0)
```

### **Why**

- `accuracy_score` → % of correct predictions
    
- `precision_score` → TP / (TP+FP), high → less false positives
    
- `recall_score` → TP / (TP+FN), high → less false negatives
    
- `f1_score` → harmonic mean of precision & recall
    
- `zero_division=0` → prevents errors when a class has no predictions
    

---

# ✅ 7. **Print Metrics**

```python
print(f"\n----- TEST METRICS -----")
print(f"Accuracy:  {acc:.4f}")
print(f"Precision: {prec:.4f}")
print(f"Recall:    {rec:.4f}")
print(f"F1-Score:  {f1:.4f}")
```

### **Why**

- Gives a quick summary of model performance on **unseen test data**
    

---

# 🎯 **Summary**

|Step|Why|When|
|---|---|---|
|Load dataset|Get sequences of test frames|Before evaluation|
|DataLoader|Load batches efficiently|During evaluation|
|Load model|Restore trained weights|Before evaluation|
|model.eval()|Disable dropout/batchnorm|Before forward pass|
|torch.no_grad()|Disable gradients|During evaluation|
|Forward pass|Get predictions|Every batch|
|torch.max|Select predicted class|Every batch|
|Store preds/labels|For metrics|Every batch|
|sklearn.metrics|Compute performance|After evaluation|

---

```python
import torch

from sklearn.metrics import roc_curve, auc

import matplotlib.pyplot as plt

  

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model.eval()

  

all_probs = []

all_labels = []

  

with torch.no_grad():

for images, labels in test_loader: # <-- your test loader name

images = images.to(device)

labels = labels.to(device)

  

outputs = model(images)

probs = torch.softmax(outputs, dim=1)[:, 1] # probability of class 1

  

all_probs.extend(probs.cpu().numpy())

all_labels.extend(labels.cpu().numpy())

  

# Calculate ROC curve

fpr, tpr, thresholds = roc_curve(all_labels, all_probs)

roc_auc = auc(fpr, tpr)

  

# Plot ROC

plt.figure(figsize=(6, 5))

plt.plot(fpr, tpr, linewidth=2, label=f"ROC curve (AUC = {roc_auc:.4f})")

plt.plot([0, 1], [0, 1], 'k--') # Diagonal line

plt.xlabel("False Positive Rate")

plt.ylabel("True Positive Rate")

plt.title("ROC Curve - Suspicious Detection")

plt.legend()

plt.grid(True)

plt.show()
```


# Explain
Here’s a **line-by-line explanation** of your **ROC curve plotting script** — including **when, where, and why** each line is used:

---

# ✅ 1. **Imports**

```python
import torch
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt
```

### **Why**

- `torch` → for tensor operations, moving data to GPU/CPU, forward pass
    
- `roc_curve` → computes False Positive Rate (FPR) & True Positive Rate (TPR)
    
- `auc` → calculates area under the ROC curve (AUC)
    
- `matplotlib.pyplot` → plots the ROC curve
    

### **When**

- At the start of the script before evaluation
    

---

# ✅ 2. **Set Device**

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```

### **Why**

- Ensures model & tensors are on same device (GPU or CPU)
    

---

# ✅ 3. **Set Model to Evaluation Mode**

```python
model.eval()
```

### **Why**

- Disables dropout & batchnorm updates
    
- Ensures consistent predictions during evaluation
    

---

# ✅ 4. **Prepare Lists to Store Probabilities and Labels**

```python
all_probs = []
all_labels = []
```

### **Why**

- We need predicted probabilities for **ROC curve**
    
- Also need true labels to compare predictions
    

---

# ✅ 5. **Evaluation Loop (No Gradients)**

```python
with torch.no_grad():
```

### **Why**

- Disable gradient tracking → saves memory, speeds up inference
    

---

```python
    for images, labels in test_loader:   # <-- your test loader name
        images = images.to(device)
        labels = labels.to(device)
```

### **Why**

- Move batch data to GPU/CPU
    
- `test_loader` iterates over sequences of frames (batch size can be 1 or more)
    

---

```python
        outputs = model(images)
        probs = torch.softmax(outputs, dim=1)[:, 1]  # probability of class 1
```

### **Why**

- `outputs` → raw logits from model `(batch_size, num_classes)`
    
- `torch.softmax(outputs, dim=1)` → converts logits to probabilities
    
- `[:, 1]` → extract probability of **class 1** (Suspicious)
    
- **ROC curve requires probabilities, not discrete predictions**
    

---

```python
        all_probs.extend(probs.cpu().numpy())
        all_labels.extend(labels.cpu().numpy())
```

### **Why**

- Move tensors to CPU
    
- Convert to numpy arrays
    
- Append to lists for **full test set**
    

---

# ✅ 6. **Calculate ROC Curve**

```python
fpr, tpr, thresholds = roc_curve(all_labels, all_probs)
roc_auc = auc(fpr, tpr)
```

### **Why**

- `roc_curve` → calculates FPR and TPR at multiple thresholds
    
- `auc(fpr, tpr)` → computes **area under the curve** → single number performance metric
    

---

# ✅ 7. **Plot ROC Curve**

```python
plt.figure(figsize=(6, 5))
```

- Creates a figure with size 6x5 inches
    

---

```python
plt.plot(fpr, tpr, linewidth=2, label=f"ROC curve (AUC = {roc_auc:.4f})")
```

- Plot ROC curve
    
- `label` shows AUC on legend
    
- `linewidth=2` → thicker line for clarity
    

---

```python
plt.plot([0, 1], [0, 1], 'k--')  # Diagonal line
```

- Plots a **random classifier line** (FPR=TPR) as reference
    
- `'k--'` → black dashed line
    

---

```python
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.title("ROC Curve - Suspicious Detection")
plt.legend()
plt.grid(True)
plt.show()
```

### **Why**

- `xlabel`/`ylabel` → label axes
    
- `title` → explain plot
    
- `legend` → show AUC
    
- `grid(True)` → makes plot easier to read
    
- `plt.show()` → display plot
    

---

# ✅ **Summary / Key Points**

|Step|Why|Notes|
|---|---|---|
|Collect probabilities (`softmax`)|Needed for ROC|Must be continuous scores|
|Collect true labels|Compare predictions|Same order as probabilities|
|`roc_curve`|Compute FPR, TPR|Uses probabilities at multiple thresholds|
|`auc`|Single-number metric|0.5 = random, 1 = perfect|
|Plot|Visualize classifier performance|Helps detect imbalance, threshold selection|

---

This script is **critical** for **binary classification evaluation** because ROC & AUC are **threshold-independent metrics**, unlike accuracy.

---


```python
from sklearn.metrics import precision_recall_curve, average_precision_score

import matplotlib.pyplot as plt

precision, recall, _ = precision_recall_curve(all_labels, all_probs)

ap_score = average_precision_score(all_labels, all_probs)

plt.figure(figsize=(6, 5))

plt.plot(recall, precision, linewidth=2, label=f"AP = {ap_score:.4f}")

plt.xlabel("Recall")

plt.ylabel("Precision")

plt.title("Precision–Recall Curve")

plt.grid(True)

plt.legend()

plt.show()
```

# Explain

Sure! Let’s go **line by line** and explain your code clearly, including **what each line does, why it’s needed, and when you should use it**. Your code plots a **Precision–Recall (PR) curve** and calculates the **Average Precision (AP) score**, which is very common in classification tasks, especially with imbalanced datasets.

---

```python
from sklearn.metrics import precision_recall_curve, average_precision_score
```

- **What it does:** Imports two functions from scikit-learn.
    
    - `precision_recall_curve`: Computes precision and recall values for different probability thresholds.
        
    - `average_precision_score`: Computes the area under the precision-recall curve (AP score).
        
- **Why it’s needed:** These metrics help evaluate **binary classification models**, especially when your dataset is **imbalanced** (e.g., one class is much smaller than the other).
    
- **When to use:** Whenever you want to **analyze precision vs recall trade-off** instead of just using accuracy. Accuracy can be misleading in imbalanced datasets.
    

---

```python
import matplotlib.pyplot as plt
```

- **What it does:** Imports the `matplotlib.pyplot` module to plot graphs.
    
- **Why it’s needed:** PR curves are visual, so we need a plotting library.
    
- **When to use:** Any time you want to **visualize model performance** in Python.
    

---

```python
precision, recall, _ = precision_recall_curve(all_labels, all_probs)
```

- **What it does:** Computes **precision and recall values** at different thresholds.
    
    - `all_labels`: True labels (0 or 1) for your test set.
        
    - `all_probs`: Predicted probabilities (between 0 and 1) from your model.
        
    - `_`: Thresholds used internally to calculate precision and recall; often ignored.
        
- **Why it’s needed:** PR curves show how precision changes as recall changes for **different probability thresholds**.
    
- **When to use:** Whenever you want to **visualize model performance beyond a single threshold** (like 0.5).
    

---

```python
ap_score = average_precision_score(all_labels, all_probs)
```

- **What it does:** Computes **Average Precision (AP)**, a single number summarizing the PR curve.
    
- **Why it’s needed:**
    
    - AP is like **area under the PR curve**.
        
    - Higher AP means better balance between precision and recall across thresholds.
        
- **When to use:** To **quantify model performance** for comparison between models.
    

---

```python
plt.figure(figsize=(6, 5))
```

- **What it does:** Creates a new figure for plotting, with a size of **6x5 inches**.
    
- **Why it’s needed:** Helps control the **size of the plot** so labels and curves are readable.
    
- **When to use:** Always use when creating new plots to ensure **consistent sizing**.
    

---

```python
plt.plot(recall, precision, linewidth=2, label=f"AP = {ap_score:.4f}")
```

- **What it does:** Plots **precision vs recall**.
    
    - `recall` on the x-axis, `precision` on the y-axis.
        
    - `linewidth=2`: Makes the curve thicker for better visibility.
        
    - `label=f"AP = {ap_score:.4f}"`: Shows AP score in the legend (formatted to 4 decimal places).
        
- **Why it’s needed:** Shows **trade-off between precision and recall**. The legend helps summarize model performance in one number.
    
- **When to use:** Always when plotting PR curves to **make them informative**.
    

---

```python
plt.xlabel("Recall")
plt.ylabel("Precision")
```

- **What it does:** Labels the **x-axis** as Recall and **y-axis** as Precision.
    
- **Why it’s needed:** Without axis labels, the plot would be **confusing**.
    
- **When to use:** Always label axes for clarity.
    

---

```python
plt.title("Precision–Recall Curve")
```

- **What it does:** Adds a title to the plot.
    
- **Why it’s needed:** Makes the plot **self-explanatory** when presenting or saving it.
    
- **When to use:** Always title your plots.
    

---

```python
plt.grid(True)
```

- **What it does:** Turns on the **grid** in the plot.
    
- **Why it’s needed:** Makes it easier to **read values** from the curve.
    
- **When to use:** Optional but recommended for clarity.
    

---

```python
plt.legend()
```

- **What it does:** Shows the **legend** with the AP score.
    
- **Why it’s needed:** Helps identify which curve corresponds to which model or metric.
    
- **When to use:** Essential if you have **multiple curves** or want to display metrics.
    

---

```python
plt.show()
```

- **What it does:** Displays the plot in a **window or notebook**.
    
- **Why it’s needed:** Without this, the plot **won’t appear** in scripts (though in Jupyter Notebook, plots sometimes auto-display).
    
- **When to use:** Always use at the end of plotting.
    

---

✅ **Summary / Use Case:**

- **When to use:** Binary classification tasks, especially with imbalanced classes (fraud detection, disease prediction, etc.).
    
- **Why:** PR curve shows the trade-off between **precision** (how many predicted positives are correct) and **recall** (how many actual positives are detected). AP score summarizes the curve in **one number**.
    
- **Result:** Helps evaluate models better than accuracy in skewed datasets.
    

---

```python
from sklearn.metrics import roc_auc_score

  

auc_score = roc_auc_score(all_labels, all_probs)

print("AUC Score:", round(auc_score, 4))
```

# Explain
Sure! Let’s break this **line by line**, explaining **what each line does, why it’s needed, and when you should use it**. This snippet calculates the **AUC score**, which is a popular metric for evaluating **binary classifiers**.

---

```python
from sklearn.metrics import roc_auc_score
```

- **What it does:** Imports the `roc_auc_score` function from scikit-learn.
    
- **Why it’s needed:** `roc_auc_score` computes the **Area Under the Receiver Operating Characteristic (ROC) Curve**, which measures the ability of a classifier to **distinguish between positive and negative classes**.
    
- **When to use:** Whenever you want a **single numeric metric** to summarize your model’s performance across all classification thresholds. This is especially important for **imbalanced datasets**.
    

---

```python
auc_score = roc_auc_score(all_labels, all_probs)
```

- **What it does:** Computes the **AUC (Area Under the Curve) score**.
    
    - `all_labels`: True labels for your dataset (0 or 1 for binary classification).
        
    - `all_probs`: Predicted probabilities for the positive class (values between 0 and 1).
        
- **Why it’s needed:** The AUC score tells you how well your model ranks positive samples higher than negative ones.
    
    - **AUC = 1.0:** Perfect classifier.
        
    - **AUC = 0.5:** Random guessing.
        
    - **AUC < 0.5:** Worse than random (possible label or model issue).
        
- **When to use:** Use AUC when you want to **evaluate the ranking quality** of your classifier, not just accuracy at a fixed threshold.
    

---

```python
print("AUC Score:", round(auc_score, 4))
```

- **What it does:** Prints the AUC score, rounded to 4 decimal places for readability.
    
- **Why it’s needed:** Makes the score **human-readable** and easy to interpret.
    
- **When to use:** Always print or log metrics when evaluating a model, so you can **compare different models** or **track performance**.
    

---

✅ **Summary / Use Case:**

- **Purpose:** Evaluates how well a model can distinguish positive vs negative classes **over all thresholds**.
    
- **Why:** More informative than accuracy for **imbalanced datasets**, because it considers **true positive rate vs false positive rate**.
    
- **Result:** Produces a **single number** between 0 and 1 summarizing classifier performance.
    

---


```python
import torch

import cv2

import numpy as np

import matplotlib.pyplot as plt

  

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model.eval()

  

# -------------------------

# Correct target layer

# -------------------------

target_layer = model.cnn.backbone[7][-1].conv2 # last conv of ResNet18 backbone

  

gradients = []

activations = []

  

def save_gradient(module, grad_input, grad_output):

gradients.append(grad_output[0])

  

def save_activation(module, input, output):

activations.append(output)

  

# Register hooks

target_layer.register_forward_hook(save_activation)

target_layer.register_backward_hook(save_gradient)

  

# Sample frame from test_loader

img, label = next(iter(test_loader))

img = img[0][0].unsqueeze(0).to(device) # first frame of first sequence

  

# Forward pass through CNN only

cnn_out = model.cnn(img)

  

# Backward for "Suspicious" class

score = cnn_out[0, 1]

model.cnn.zero_grad()

score.backward()

  

# Grad-CAM computation

grad = gradients[-1].cpu().detach().numpy()[0]

act = activations[-1].cpu().detach().numpy()[0] # <-- detach added

  

weights = np.mean(grad, axis=(1, 2))

cam = np.zeros(act.shape[1:], dtype=np.float32)

  

for i, w in enumerate(weights):

cam += w * act[i]

  

cam = np.maximum(cam, 0)

cam = cv2.resize(cam, (224, 224))

cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)

  

# Convert input tensor to numpy image

image = img.cpu().numpy()[0].transpose(1, 2, 0)

image = (image - image.min()) / (image.max() - image.min())

  

# Overlay heatmap

heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)

heatmap = heatmap / 255.0

overlay = 0.4 * heatmap + 0.6 * image

overlay = overlay / overlay.max()

  

plt.figure(figsize=(7,6))

plt.imshow(overlay)

plt.title("Grad-CAM - CNNEncoder")

plt.axis("off")

plt.show()
```

# Explain
Absolutely! Let’s go **line by line** and explain your Grad-CAM code, including **what each line does, why it’s needed, and when to use it**. Grad-CAM is a technique to **visualize which parts of an image the CNN is focusing on** for a particular class prediction.

---

```python
import torch
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

- **What it does:** Imports necessary libraries.
    
    - `torch`: For PyTorch tensors, models, and gradients.
        
    - `cv2`: OpenCV for image processing and resizing.
        
    - `numpy`: Numerical computations.
        
    - `matplotlib.pyplot`: For plotting the final heatmap.
        
- **Why it’s needed:** All these libraries are essential for **forward/backward passes, gradient computation, and visualization**.
    
- **When to use:** Always in deep learning visualization pipelines.
    

---

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model.eval()
```

- **What it does:**
    
    - Sets the **device** to GPU if available, else CPU.
        
    - Switches the model to **evaluation mode** (`eval`) so layers like dropout or batchnorm behave consistently.
        
- **Why it’s needed:** Ensures **correct forward pass** during inference/visualization.
    
- **When to use:** Anytime you’re evaluating or visualizing a trained model.
    

---

```python
# -------------------------
# Correct target layer
# -------------------------
target_layer = model.cnn.backbone[7][-1].conv2  # last conv of ResNet18 backbone
```

- **What it does:** Selects the **last convolutional layer** of the CNN backbone.
    
- **Why it’s needed:** Grad-CAM requires **feature maps from the last conv layer** because they retain **spatial information** useful for localization.
    
- **When to use:** Always target a **deep convolutional layer**, not fully connected layers.
    

---

```python
gradients = []
activations = []
```

- **What it does:** Initializes lists to **store gradients and activations** during forward/backward passes.
    
- **Why it’s needed:** Grad-CAM combines gradients (importance) with activations (feature maps).
    
- **When to use:** Before registering hooks.
    

---

```python
def save_gradient(module, grad_input, grad_output):
    gradients.append(grad_output[0])
```

- **What it does:** Defines a function to **store gradients** from the backward pass.
    
- **Why it’s needed:** Grad-CAM needs gradients **w.r.t. target class** to compute importance weights.
    
- **When to use:** Always when registering backward hooks.
    

---

```python
def save_activation(module, input, output):
    activations.append(output)
```

- **What it does:** Defines a function to **store activations** from the forward pass.
    
- **Why it’s needed:** Grad-CAM uses **activations from the target layer** to highlight spatial regions.
    
- **When to use:** Always when registering forward hooks.
    

---

```python
# Register hooks
target_layer.register_forward_hook(save_activation)
target_layer.register_backward_hook(save_gradient)
```

- **What it does:** Hooks connect your functions to the layer:
    
    - `forward_hook` → stores activations.
        
    - `backward_hook` → stores gradients.
        
- **Why it’s needed:** Allows you to **capture intermediate computations** without modifying the model.
    
- **When to use:** Always when implementing Grad-CAM.
    

---

```python
# Sample frame from test_loader
img, label = next(iter(test_loader))
img = img[0][0].unsqueeze(0).to(device)  # first frame of first sequence
```

- **What it does:**
    
    - Extracts the first frame from your test data.
        
    - Adds batch dimension (`unsqueeze(0)`) and sends tensor to device.
        
- **Why it’s needed:** PyTorch models expect **batch dimension** and the correct **device**.
    
- **When to use:** Anytime you select a **single sample for visualization**.
    

---

```python
# Forward pass through CNN only
cnn_out = model.cnn(img)
```

- **What it does:** Passes the image through the CNN encoder (without the classifier).
    
- **Why it’s needed:** Grad-CAM focuses on **CNN feature maps**, not final fully connected layers.
    
- **When to use:** Always when you want **activation maps**.
    

---

```python
# Backward for "Suspicious" class
score = cnn_out[0, 1]
model.cnn.zero_grad()
score.backward()
```

- **What it does:**
    
    - Selects the output **score of class 1 ("Suspicious")**.
        
    - Clears previous gradients (`zero_grad`).
        
    - Backpropagates to compute **gradients w.r.t activations**.
        
- **Why it’s needed:** Grad-CAM uses **gradients of the target class** to weigh feature maps.
    
- **When to use:** Always when visualizing a **specific class**.
    

---

```python
# Grad-CAM computation
grad = gradients[-1].cpu().detach().numpy()[0]
act  = activations[-1].cpu().detach().numpy()[0]   # <-- detach added
```

- **What it does:**
    
    - Converts PyTorch tensors to **NumPy arrays**.
        
    - `grad` = gradient maps, `act` = activation maps.
        
- **Why it’s needed:** NumPy arrays are required for **element-wise operations** like weighting.
    
- **When to use:** Before computing Grad-CAM map.
    

---

```python
weights = np.mean(grad, axis=(1, 2))
cam = np.zeros(act.shape[1:], dtype=np.float32)
```

- **What it does:**
    
    - Computes **importance weights** for each channel by averaging gradients over spatial dimensions.
        
    - Initializes empty CAM map.
        
- **Why it’s needed:** Grad-CAM formula: `CAM = sum(weights * activations)`.
    
- **When to use:** Always in Grad-CAM computation.
    

---

```python
for i, w in enumerate(weights):
    cam += w * act[i]
```

- **What it does:** Combines activations with weights to compute **class-specific heatmap**.
    
- **Why it’s needed:** Highlights regions **most responsible** for the class prediction.
    
- **When to use:** Essential step in Grad-CAM.
    

---

```python
cam = np.maximum(cam, 0)
cam = cv2.resize(cam, (224, 224))
cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)
```

- **What it does:**
    
    - `np.maximum(cam, 0)`: ReLU to remove negative values.
        
    - Resize CAM to **input image size**.
        
    - Normalize to **0–1** range for visualization.
        
- **Why it’s needed:** Prepares heatmap for overlay.
    
- **When to use:** Always before visualizing.
    

---

```python
# Convert input tensor to numpy image
image = img.cpu().numpy()[0].transpose(1, 2, 0)
image = (image - image.min()) / (image.max() - image.min())
```

- **What it does:**
    
    - Converts PyTorch tensor to **H×W×C NumPy image**.
        
    - Normalizes image between 0–1 for overlay.
        
- **Why it’s needed:** Ensures **heatmap blends correctly** with the original image.
    
- **When to use:** Always before overlay.
    

---

```python
# Overlay heatmap
heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)
heatmap = heatmap / 255.0
overlay = 0.4 * heatmap + 0.6 * image
overlay = overlay / overlay.max()
```

- **What it does:**
    
    - Converts CAM to **color map** (JET) for better visualization.
        
    - Combines heatmap and original image with transparency (`0.4 * heatmap + 0.6 * image`).
        
    - Normalizes final overlay.
        
- **Why it’s needed:** Visualizes **regions the model is focusing on**.
    
- **When to use:** Always for interpretability of predictions.
    

---

```python
plt.figure(figsize=(7,6))
plt.imshow(overlay)
plt.title("Grad-CAM - CNNEncoder")
plt.axis("off")
plt.show()
```

- **What it does:** Plots the **Grad-CAM overlay**.
    
    - `figsize`: Sets figure size.
        
    - `axis("off")`: Hides axis ticks.
        
    - `title`: Labels plot.
        
- **Why it’s needed:** Makes the **visualization clear and interpretable**.
    
- **When to use:** Always at the end of Grad-CAM to **display results**.
    

---

✅ **Summary:**  
This code computes **Grad-CAM** for a single frame, highlighting **image regions important for class prediction**. Useful for:

- Understanding model behavior
    
- Debugging CNNs
    
- Making models **interpretable**
    

---



```python
import torch

import cv2

import numpy as np

import matplotlib.pyplot as plt

  

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model.eval()

  

# -------------------------

# Choose target layer in CNNEncoder

# -------------------------

target_layer = model.cnn.backbone[7][-1].conv2 # last conv layer of ResNet18

  

gradients = []

activations = []

  

def save_gradient(module, grad_input, grad_output):

gradients.append(grad_output[0])

  

def save_activation(module, input, output):

activations.append(output)

  

# Register hooks

target_layer.register_forward_hook(save_activation)

target_layer.register_backward_hook(save_gradient)

  

# Get one sequence from test_loader

sequence, label = next(iter(test_loader)) # sequence shape: (B, SEQ_LEN, C, H, W)

sequence = sequence.to(device)

  

SEQ_LEN = sequence.shape[1]

  

for t in range(SEQ_LEN):

img = sequence[0, t].unsqueeze(0) # frame t

  

# Clear previous hooks

gradients = []

activations = []

  

# Forward

cnn_out = model.cnn(img)

  

# Zero grads before backward

model.cnn.zero_grad()

  

# Backward for suspicious class

score = cnn_out[0, 1]

score.backward()

  

# Extract grad + activation

grad = gradients[-1].cpu().detach().numpy()[0]

act = activations[-1].cpu().detach().numpy()[0]

  

# Grad-CAM

weights = np.mean(grad, axis=(1, 2))

cam = np.zeros(act.shape[1:], dtype=np.float32)

for i, w in enumerate(weights):

cam += w * act[i]

  

cam = np.maximum(cam, 0)

cam = cv2.resize(cam, (224, 224))

cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)

  

# Overlay

image = img.cpu().numpy()[0].transpose(1, 2, 0)

image = (image - image.min()) / (image.max() - image.min())

  

heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)

heatmap = heatmap / 255.0

overlay = 0.4 * heatmap + 0.6 * image

overlay = overlay / overlay.max()

  

plt.figure(figsize=(5,5))

plt.imshow(overlay)

plt.title(f"Grad-CAM - Frame {t+1}")

plt.axis("off")

plt.show()
```

# Explain
Sure! Let’s go **line by line** for your **video sequence Grad-CAM code**, explaining **what it does, why it’s needed, and when to use it**. This version computes Grad-CAM for **each frame in a video sequence**, instead of a single image.

---

```python
import torch
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

- **What it does:** Imports libraries:
    
    - `torch` → for model, tensors, gradients
        
    - `cv2` → OpenCV, image resizing and color maps
        
    - `numpy` → numerical operations
        
    - `matplotlib.pyplot` → plotting heatmaps
        
- **Why it’s needed:** These are standard tools for **deep learning and visualization**.
    
- **When to use:** Always when computing Grad-CAM or visualizing CNN outputs.
    

---

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model.eval()
```

- **What it does:**
    
    - Chooses **GPU if available**, otherwise CPU.
        
    - Sets the model in **evaluation mode** (`eval()`) so dropout and batchnorm work properly.
        
- **Why it’s needed:** Grad-CAM requires **inference mode** to avoid randomness during forward pass.
    
- **When to use:** Before computing Grad-CAM on any model.
    

---

```python
# -------------------------
# Choose target layer in CNNEncoder
# -------------------------
target_layer = model.cnn.backbone[7][-1].conv2  # last conv layer of ResNet18
```

- **What it does:** Chooses the **last convolutional layer** of your CNN backbone.
    
- **Why it’s needed:** Grad-CAM requires **feature maps with spatial info** from deep layers.
    
- **When to use:** Always pick a **convolutional layer near the end** of the CNN.
    

---

```python
gradients = []
activations = []
```

- **What it does:** Initializes lists to store **gradients and activations** for each frame.
    
- **Why it’s needed:** Grad-CAM formula needs these values.
    
- **When to use:** Before registering hooks.
    

---

```python
def save_gradient(module, grad_input, grad_output):
    gradients.append(grad_output[0])
```

- **What it does:** Stores **gradients during backward pass**.
    
- **Why it’s needed:** Grad-CAM uses **gradients to weigh channels of activation maps**.
    
- **When to use:** Register as a backward hook.
    

---

```python
def save_activation(module, input, output):
    activations.append(output)
```

- **What it does:** Stores **activations during forward pass**.
    
- **Why it’s needed:** Grad-CAM multiplies gradients with activations to generate the heatmap.
    
- **When to use:** Register as a forward hook.
    

---

```python
# Register hooks
target_layer.register_forward_hook(save_activation)
target_layer.register_backward_hook(save_gradient)
```

- **What it does:** Connects your save functions to the target layer.
    
- **Why it’s needed:** Captures **intermediate outputs** without modifying the model.
    
- **When to use:** Always before forward/backward passes for Grad-CAM.
    

---

```python
# Get one sequence from test_loader
sequence, label = next(iter(test_loader))  # sequence shape: (B, SEQ_LEN, C, H, W)
sequence = sequence.to(device)
SEQ_LEN = sequence.shape[1]
```

- **What it does:**
    
    - Gets one **video sequence** and its label.
        
    - Moves sequence to GPU/CPU.
        
    - Gets sequence length.
        
- **Why it’s needed:** Grad-CAM will be computed for **each frame in the sequence**.
    
- **When to use:** When visualizing model predictions on **video or sequence data**.
    

---

```python
for t in range(SEQ_LEN):
    img = sequence[0, t].unsqueeze(0)  # frame t
```

- **What it does:** Iterates over each frame and selects frame `t` from the first sequence.
    
- **Why it’s needed:** We want Grad-CAM for **every frame**.
    
- **When to use:** For **video/temporal CNNs or CNN+RNN models**.
    

---

```python
    # Clear previous hooks
    gradients = []
    activations = []
```

- **What it does:** Resets lists before computing Grad-CAM for a new frame.
    
- **Why it’s needed:** Gradients and activations **accumulate in hooks**, so you must clear them.
    
- **When to use:** Always at the start of a new forward/backward cycle.
    

---

```python
    # Forward
    cnn_out = model.cnn(img)
```

- **What it does:** Passes the current frame through the CNN encoder.
    
- **Why it’s needed:** Grad-CAM uses the **activations from this forward pass**.
    
- **When to use:** For each frame individually.
    

---

```python
    # Zero grads before backward
    model.cnn.zero_grad()
```

- **What it does:** Clears **previous gradients**.
    
- **Why it’s needed:** PyTorch **accumulates gradients**, so you must reset them for each frame.
    
- **When to use:** Before each backward pass.
    

---

```python
    # Backward for suspicious class
    score = cnn_out[0, 1]
    score.backward()
```

- **What it does:**
    
    - Selects the score for class 1 (e.g., "Suspicious").
        
    - Computes **gradients w.r.t activations**.
        
- **Why it’s needed:** Grad-CAM uses these gradients to **weight feature maps**.
    
- **When to use:** Always when targeting a **specific class**.
    

---

```python
    # Extract grad + activation
    grad = gradients[-1].cpu().detach().numpy()[0]
    act  = activations[-1].cpu().detach().numpy()[0]
```

- **What it does:** Converts tensors to **NumPy arrays** for processing.
    
- **Why it’s needed:** Grad-CAM computation is easier in NumPy.
    
- **When to use:** Always after forward/backward passes.
    

---

```python
    # Grad-CAM
    weights = np.mean(grad, axis=(1, 2))
    cam = np.zeros(act.shape[1:], dtype=np.float32)
    for i, w in enumerate(weights):
        cam += w * act[i]
```

- **What it does:** Computes **weighted sum of activations**.
    
    - `weights = mean gradient` per channel.
        
    - Multiply each activation map by its weight and sum.
        
- **Why it’s needed:** Highlights areas **contributing most** to the target class.
    
- **When to use:** Core step in Grad-CAM.
    

---

```python
    cam = np.maximum(cam, 0)
    cam = cv2.resize(cam, (224, 224))
    cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)
```

- **What it does:**
    
    - ReLU to remove negatives.
        
    - Resize CAM to **input frame size**.
        
    - Normalize to **0–1**.
        
- **Why it’s needed:** Prepares heatmap for overlay visualization.
    
- **When to use:** Always before overlay.
    

---

```python
    # Overlay
    image = img.cpu().numpy()[0].transpose(1, 2, 0)
    image = (image - image.min()) / (image.max() - image.min())
```

- **What it does:** Converts frame to NumPy and normalizes.
    
- **Why it’s needed:** Ensure **overlay works correctly**.
    

---

```python
    heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)
    heatmap = heatmap / 255.0
    overlay = 0.4 * heatmap + 0.6 * image
    overlay = overlay / overlay.max()
```

- **What it does:**
    
    - Converts CAM to **color heatmap**.
        
    - Combines with frame using transparency.
        
- **Why it’s needed:** Visualizes **model attention on frame**.
    

---

```python
    plt.figure(figsize=(5,5))
    plt.imshow(overlay)
    plt.title(f"Grad-CAM - Frame {t+1}")
    plt.axis("off")
    plt.show()
```

- **What it does:** Displays the **Grad-CAM overlay for the current frame**.
    
- **Why it’s needed:** Allows **frame-by-frame inspection** of model focus.
    

---

✅ **Summary:**  
This code computes Grad-CAM for **each frame in a video sequence**, making it possible to **track where the CNN is looking over time**. Useful for:

- Video anomaly detection
    
- Temporal attention visualization
    
- Debugging CNN+RNN or CNN+Transformer models
    

---


```python
import torch

import cv2

import numpy as np

import matplotlib.pyplot as plt

  

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model.eval()

  

# Choose target layer in CNNEncoder

target_layer = model.cnn.backbone[7][-1].conv2

  

gradients = []

activations = []

  

def save_gradient(module, grad_input, grad_output):

gradients.append(grad_output[0])

  

def save_activation(module, input, output):

activations.append(output)

  

# Register hooks

target_layer.register_forward_hook(save_activation)

target_layer.register_backward_hook(save_gradient)

  

# Pick first frame from first sequence

sequence, label = next(iter(test_loader))

sequence = sequence.to(device)

img = sequence[0, 0].unsqueeze(0)

  

gradients = []

activations = []

  

# Forward pass

cnn_out = model.cnn(img)

model.cnn.zero_grad()

  

# Backward for "Suspicious" class

score = cnn_out[0, 1] # index 1 = Suspicious

score.backward()

  

# Extract gradients and activations

grad = gradients[-1].cpu().detach().numpy()[0]

act = activations[-1].cpu().detach().numpy()[0]

  

# Compute Grad-CAM

weights = np.mean(grad, axis=(1, 2))

cam = np.zeros(act.shape[1:], dtype=np.float32)

for i, w in enumerate(weights):

cam += w * act[i]

  

cam = np.maximum(cam, 0)

cam = cv2.resize(cam, (224, 224))

cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)

  

# -----------------------------

# Show heatmap only

# -----------------------------

plt.figure(figsize=(5,5))

plt.imshow(cam, cmap='jet') # use 'jet' for classic Grad-CAM color

plt.title("Grad-CAM Heatmap")

plt.axis("off")

plt.colorbar() # optional: show intensity scale

plt.show()
```


# Explain
Sure! Let’s go **line by line** and explain this Grad-CAM code that visualizes **only the heatmap** for a single frame, including **what, why, and when** for each part.

---

```python
import torch
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

- **What it does:** Imports necessary libraries.
    
    - `torch` → PyTorch for tensors, model, and gradient computations.
        
    - `cv2` → OpenCV for image resizing and color maps.
        
    - `numpy` → Array operations for Grad-CAM computation.
        
    - `matplotlib.pyplot` → For plotting the heatmap.
        
- **Why it’s needed:** Essential for computing Grad-CAM and visualizing results.
    
- **When to use:** Always when implementing Grad-CAM in Python.
    

---

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model.eval()
```

- **What it does:**
    
    - Chooses **GPU** if available, else CPU.
        
    - Puts the model in **evaluation mode** to deactivate dropout/batchnorm randomness.
        
- **Why it’s needed:** Grad-CAM uses a **deterministic forward pass**, so eval mode is required.
    
- **When to use:** Always before running inference or visualization.
    

---

```python
# Choose target layer in CNNEncoder
target_layer = model.cnn.backbone[7][-1].conv2
```

- **What it does:** Selects the **last convolutional layer** in the CNN backbone.
    
- **Why it’s needed:** Grad-CAM uses **activations from deep conv layers** because they retain spatial information.
    
- **When to use:** Always pick a **deep conv layer** for Grad-CAM.
    

---

```python
gradients = []
activations = []
```

- **What it does:** Initializes lists to store **gradients and activations**.
    
- **Why it’s needed:** Grad-CAM combines **gradients (importance)** with **activations (feature maps)**.
    

---

```python
def save_gradient(module, grad_input, grad_output):
    gradients.append(grad_output[0])
```

- **What it does:** Function to **store gradients during backward pass**.
    
- **Why it’s needed:** Grad-CAM weights each activation channel using **gradient importance**.
    

---

```python
def save_activation(module, input, output):
    activations.append(output)
```

- **What it does:** Function to **store activations during forward pass**.
    
- **Why it’s needed:** Grad-CAM multiplies activations with gradient weights to produce the heatmap.
    

---

```python
# Register hooks
target_layer.register_forward_hook(save_activation)
target_layer.register_backward_hook(save_gradient)
```

- **What it does:** Attaches hooks to the target layer.
    
    - Forward hook → saves activations.
        
    - Backward hook → saves gradients.
        
- **Why it’s needed:** Captures **intermediate outputs** without modifying the model.
    

---

```python
# Pick first frame from first sequence
sequence, label = next(iter(test_loader))
sequence = sequence.to(device)
img = sequence[0, 0].unsqueeze(0)
```

- **What it does:**
    
    - Fetches one sequence from the test loader.
        
    - Selects the **first frame** of the sequence.
        
    - Adds **batch dimension** (`unsqueeze(0)`) and moves tensor to device.
        
- **Why it’s needed:** Grad-CAM works on **one input sample at a time**.
    

---

```python
gradients = []
activations = []
```

- **What it does:** Clears previous activations and gradients.
    
- **Why it’s needed:** Hooks accumulate values; clearing ensures **fresh Grad-CAM computation**.
    

---

```python
# Forward pass
cnn_out = model.cnn(img)
model.cnn.zero_grad()
```

- **What it does:**
    
    - Passes the frame through the CNN encoder to get features.
        
    - Clears previous gradients before backward pass.
        
- **Why it’s needed:** Forward pass captures **activations**, backward will compute **gradients**.
    

---

```python
# Backward for "Suspicious" class
score = cnn_out[0, 1]   # index 1 = Suspicious
score.backward()
```

- **What it does:**
    
    - Selects the output score for the **target class** ("Suspicious").
        
    - Computes **gradients of the score w.r.t activations**.
        
- **Why it’s needed:** Grad-CAM uses **gradients to weigh feature maps**.
    

---

```python
# Extract gradients and activations
grad = gradients[-1].cpu().detach().numpy()[0]
act  = activations[-1].cpu().detach().numpy()[0]
```

- **What it does:** Converts PyTorch tensors to **NumPy arrays**.
    
- **Why it’s needed:** NumPy arrays are easier for **matrix operations** in Grad-CAM computation.
    

---

```python
# Compute Grad-CAM
weights = np.mean(grad, axis=(1, 2))
cam = np.zeros(act.shape[1:], dtype=np.float32)
for i, w in enumerate(weights):
    cam += w * act[i]
```

- **What it does:**
    
    - Computes **importance weights** for each channel by averaging gradients over spatial dimensions.
        
    - Weighted sum of activations creates **class-specific heatmap**.
        
- **Why it’s needed:** Core step of Grad-CAM formula: highlight regions contributing to target class.
    

---

```python
cam = np.maximum(cam, 0)
cam = cv2.resize(cam, (224, 224))
cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)
```

- **What it does:**
    
    - ReLU: keep only positive contributions.
        
    - Resize CAM to **input image size** (224×224).
        
    - Normalize to **0–1** range.
        
- **Why it’s needed:** Prepares **heatmap for visualization**.
    

---

```python
# -----------------------------
# Show heatmap only
# -----------------------------
plt.figure(figsize=(5,5))
plt.imshow(cam, cmap='jet')  # use 'jet' for classic Grad-CAM color
plt.title("Grad-CAM Heatmap")
plt.axis("off")
plt.colorbar()  # optional: show intensity scale
plt.show()
```

- **What it does:**
    
    - Plots the **Grad-CAM heatmap** alone (without overlay on image).
        
    - `cmap='jet'` gives classic Grad-CAM colors (blue→red).
        
    - `colorbar()` shows intensity scale of attention.
        
- **Why it’s needed:** Helps visually identify **which regions the CNN is focusing on** for the target class.
    

---

✅ **Summary:**  
This code computes **Grad-CAM for a single frame** and displays **only the heatmap**, highlighting areas important for the "Suspicious" class. It’s useful for:

- Understanding CNN focus
    
- Model interpretability
    
- Debugging misclassifications
    

---



```python
import torch

from PIL import Image

import torchvision.transforms as T

# from train_cnn_lstm import CNNLSTMModel # Make sure this file is in the same folder or PYTHONPATH

  

# -------------------------------

# Config

# -------------------------------

DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"

SEQ_LEN = 8

FRAME_SIZE = 224

  

classes = {0: "Normal", 1: "Suspicious"}

  

# -------------------------------

# Transform for evaluation

# -------------------------------

eval_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406],

std=[0.229, 0.224, 0.225]),

])

  

# -------------------------------

# Preprocess frames function

# -------------------------------

def preprocess_frames(frame_paths):

frames = []

for p in frame_paths:

img = Image.open(p).convert("RGB")

img = eval_transforms(img)

frames.append(img)

frames = torch.stack(frames, dim=0) # (SEQ_LEN, C, H, W)

frames = frames.unsqueeze(0) # add batch dimension: (1, SEQ_LEN, C, H, W)

return frames

  

# -------------------------------

# Load model

# -------------------------------

model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)

model = model.to(DEVICE)

  

checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)

model.load_state_dict(checkpoint["model_state"])

model.eval()

  

# -------------------------------

# Predict function

# -------------------------------

def predict(frame_paths):

input_tensor = preprocess_frames(frame_paths).to(DEVICE)

with torch.no_grad():

outputs = model(input_tensor)

probs = torch.softmax(outputs, dim=1)

pred_class = torch.argmax(probs, dim=1).item()

return classes[pred_class], probs.cpu().numpy()

  

# -------------------------------

# Example usage

# -------------------------------

# Provide a list of 8 frame paths (adjust according to your frames)

frame_paths = [

"/home/atiar/Downloads/video to frame/output/Suspicious/Abuse001_x264.mp4_f1850.jpg",

"/home/atiar/Downloads/video to frame/output/Suspicious/Abuse014_x264.mp4_f1270.jpg",

"/home/atiar/Downloads/video to frame/output/Suspicious/Assault002_x264.mp4_f1140.jpg",

"/home/atiar/Downloads/video to frame/output/Suspicious/Burglary073_x264.mp4_f370.jpg",

"/home/atiar/Downloads/video to frame/output/Suspicious/Shooting033_x264.mp4_f20.jpg",

"/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos_027_x264.mp4_f2840.jpg",

"/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos308_x264.mp4_f578640.jpg",

"/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos633_x264.mp4_f390840.jpg",

]

  

pred_class, probs = predict(frame_paths)

print("Predicted class:", pred_class)

print("Class probabilities:", probs)
```

# Explain

Absolutely! Let’s go **line by line** and explain your **CNN-LSTM video frame classification code**, including **what it does, why it’s needed, and when to use it**. This script predicts whether a sequence of frames is “Normal” or “Suspicious.”

---

```python
import torch
from PIL import Image
import torchvision.transforms as T
# from train_cnn_lstm import CNNLSTMModel  # Make sure this file is in the same folder or PYTHONPATH
```

- **What it does:** Imports necessary libraries.
    
    - `torch` → For model, tensors, GPU support.
        
    - `PIL.Image` → To load image frames.
        
    - `torchvision.transforms` → Preprocessing transformations.
        
    - `CNNLSTMModel` → Your custom CNN-LSTM model class.
        
- **Why it’s needed:** You need **image loading, preprocessing, and model definition** to predict video sequences.
    
- **When to use:** At the beginning of the script for **all dependencies**.
    

---

```python
# -------------------------------
# Config
# -------------------------------
DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")
MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"
SEQ_LEN = 8
FRAME_SIZE = 224

classes = {0: "Normal", 1: "Suspicious"}
```

- **What it does:** Sets configuration parameters:
    
    - `DEVICE`: Use GPU if available, otherwise CPU.
        
    - `MODEL_PATH`: Path to the trained model checkpoint.
        
    - `SEQ_LEN`: Number of frames per sequence (input to model).
        
    - `FRAME_SIZE`: Resize frames to 224×224 pixels.
        
    - `classes`: Maps numeric class labels to readable strings.
        
- **Why it’s needed:** Provides **flexible configuration** for preprocessing and prediction.
    
- **When to use:** Always at the top for **easy parameter adjustment**.
    

---

```python
# -------------------------------
# Transform for evaluation
# -------------------------------
eval_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406],
                std=[0.229, 0.224, 0.225]),
])
```

- **What it does:** Defines **image preprocessing pipeline**.
    
    - `Resize`: Ensures consistent input size for the CNN.
        
    - `ToTensor`: Converts PIL image to PyTorch tensor.
        
    - `Normalize`: Uses **ImageNet mean/std** because CNN backbone was likely pretrained.
        
- **Why it’s needed:** Neural networks require **normalized tensors** of consistent size.
    
- **When to use:** Always before passing frames to the model.
    

---

```python
# -------------------------------
# Preprocess frames function
# -------------------------------
def preprocess_frames(frame_paths):
    frames = []
    for p in frame_paths:
        img = Image.open(p).convert("RGB")
        img = eval_transforms(img)
        frames.append(img)
    frames = torch.stack(frames, dim=0)  # (SEQ_LEN, C, H, W)
    frames = frames.unsqueeze(0)         # add batch dimension: (1, SEQ_LEN, C, H, W)
    return frames
```

- **What it does:** Converts a list of frame paths into a **batch tensor** ready for the model.
    
    - Loads image, converts to RGB.
        
    - Applies transforms.
        
    - Stacks frames along **sequence dimension**.
        
    - Adds **batch dimension**.
        
- **Why it’s needed:** The CNN-LSTM expects input shape **(B, SEQ_LEN, C, H, W)**.
    
- **When to use:** Always before feeding frames into the model.
    

---

```python
# -------------------------------
# Load model
# -------------------------------
model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)
model = model.to(DEVICE)
```

- **What it does:**
    
    - Instantiates the **CNN-LSTM model** with the specified feature and LSTM parameters.
        
    - Moves model to **GPU/CPU**.
        
- **Why it’s needed:** Must create a model instance before loading weights.
    
- **When to use:** Before loading checkpoint or making predictions.
    

---

```python
checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)
model.load_state_dict(checkpoint["model_state"])
model.eval()
```

- **What it does:**
    
    - Loads saved checkpoint.
        
    - Loads the trained **weights** into the model.
        
    - Switches model to **evaluation mode**.
        
- **Why it’s needed:** Ensures **deterministic predictions** using the trained model.
    
- **When to use:** Always when using a pretrained model.
    

---

```python
# -------------------------------
# Predict function
# -------------------------------
def predict(frame_paths):
    input_tensor = preprocess_frames(frame_paths).to(DEVICE)
    with torch.no_grad():
        outputs = model(input_tensor)
        probs = torch.softmax(outputs, dim=1)
        pred_class = torch.argmax(probs, dim=1).item()
    return classes[pred_class], probs.cpu().numpy()
```

- **What it does:**
    
    - Preprocesses frames.
        
    - Uses `torch.no_grad()` to **disable gradient computation** (saves memory).
        
    - Passes input through model to get **logits**.
        
    - Converts logits to **probabilities** using `softmax`.
        
    - Picks the **predicted class**.
        
    - Returns human-readable class and probabilities.
        
- **Why it’s needed:** Encapsulates **end-to-end prediction** in one function.
    
- **When to use:** Every time you want to predict a **sequence of frames**.
    

---

```python
# -------------------------------
# Example usage
# -------------------------------
# Provide a list of 8 frame paths (adjust according to your frames)
frame_paths = [
    "/home/atiar/Downloads/video to frame/output/Suspicious/Abuse001_x264.mp4_f1850.jpg",
    "/home/atiar/Downloads/video to frame/output/Suspicious/Abuse014_x264.mp4_f1270.jpg",
    "/home/atiar/Downloads/video to frame/output/Suspicious/Assault002_x264.mp4_f1140.jpg",
    "/home/atiar/Downloads/video to frame/output/Suspicious/Burglary073_x264.mp4_f370.jpg",
    "/home/atiar/Downloads/video to frame/output/Suspicious/Shooting033_x264.mp4_f20.jpg",
    "/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos_027_x264.mp4_f2840.jpg",
    "/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos308_x264.mp4_f578640.jpg",
    "/home/atiar/Downloads/video to frame/output/Normal/Normal_Videos633_x264.mp4_f390840.jpg",
]
```

- **What it does:** Lists **paths to 8 frames** to form one sequence.
    
- **Why it’s needed:** The CNN-LSTM requires **exactly SEQ_LEN frames**.
    
- **When to use:** Always when testing/predicting on real video sequences.
    

---

```python
pred_class, probs = predict(frame_paths)
print("Predicted class:", pred_class)
print("Class probabilities:", probs)
```

- **What it does:**
    
    - Calls `predict()` to classify the frame sequence.
        
    - Prints **predicted class** (Normal/Suspicious).
        
    - Prints **class probabilities** for both classes.
        
- **Why it’s needed:** Outputs human-readable **prediction and confidence**.
    
- **When to use:** After preparing frame sequences.
    

---

✅ **Summary:**  
This script:

1. Loads a trained **CNN-LSTM** model.
    
2. Preprocesses a sequence of video frames.
    
3. Runs inference to classify sequence as **Normal or Suspicious**.
    
4. Returns **predicted class and class probabilities**.
    

---

```python
import cv2

import torch

from PIL import Image

import torchvision.transforms as T

from collections import deque

# from train_cnn_lstm import CNNLSTMModel # make sure this is available

  

# -------------------------------

# Config

# -------------------------------

DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"

SEQ_LEN = 8

FRAME_SIZE = 224

classes = {0: "Normal", 1: "Suspicious"}

  

# -------------------------------

  

# Transform for webcam frames

# -------------------------------

eval_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406],

std=[0.229, 0.224, 0.225]),

])

  

# -------------------------------

# Load model

# -------------------------------

model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)

model = model.to(DEVICE)

checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)

model.load_state_dict(checkpoint["model_state"])

model.eval()

  

# -------------------------------

# Preprocess single frame

# -------------------------------

def preprocess_frame(frame):

img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))

img = eval_transforms(img)

return img

  

# -------------------------------

# Webcam prediction

# -------------------------------

cap = cv2.VideoCapture(0) # use 0 for default webcam

frame_buffer = deque(maxlen=SEQ_LEN) # store last SEQ_LEN frames

  

while True:

ret, frame = cap.read()

if not ret:

break

  

# preprocess and add to buffer

frame_tensor = preprocess_frame(frame)

frame_buffer.append(frame_tensor)

  

# once we have SEQ_LEN frames, make prediction

if len(frame_buffer) == SEQ_LEN:

seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE) # (1, SEQ_LEN, C, H, W)

with torch.no_grad():

outputs = model(seq_tensor)

probs = torch.softmax(outputs, dim=1)

pred_class = torch.argmax(probs, dim=1).item()

label = classes[pred_class]

confidence = probs[0, pred_class].item()

  

# display prediction on frame

cv2.putText(frame, f"{label} ({confidence*100:.1f}%)",

(10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (0,0,255), 2)

  

cv2.imshow("Live Prediction", frame)

  

# quit on 'q' key

if cv2.waitKey(1) & 0xFF == ord('q'):

break

  

cap.release()

cv2.destroyAllWindows()
```


# Explain
Absolutely! Let’s go **line by line** for your **real-time webcam CNN-LSTM prediction code**, explaining **what it does, why it’s needed, and when to use it**. This script predicts “Normal” or “Suspicious” from a live webcam feed.

---

```python
import cv2
import torch
from PIL import Image
import torchvision.transforms as T
from collections import deque
# from train_cnn_lstm import CNNLSTMModel  # make sure this is available
```

- **What it does:** Imports all necessary libraries:
    
    - `cv2` → OpenCV for webcam capture and displaying frames.
        
    - `torch` → PyTorch for model inference.
        
    - `PIL.Image` → Convert OpenCV frames to PIL format for transforms.
        
    - `torchvision.transforms` → Preprocessing like resize and normalization.
        
    - `deque` → Efficiently store last `SEQ_LEN` frames in a buffer.
        
- **Why it’s needed:** Webcam input needs **frame capture, preprocessing, and buffering** for sequence models.
    

---

```python
# -------------------------------
# Config
# -------------------------------
DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")
MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"
SEQ_LEN = 8
FRAME_SIZE = 224
classes = {0: "Normal", 1: "Suspicious"}
```

- **What it does:** Sets configuration:
    
    - `DEVICE` → GPU if available.
        
    - `MODEL_PATH` → Path to trained CNN-LSTM model.
        
    - `SEQ_LEN` → Number of frames for LSTM input.
        
    - `FRAME_SIZE` → Resize input frames to 224×224.
        
    - `classes` → Map numeric outputs to human-readable labels.
        
- **Why it’s needed:** Makes code **flexible** for different sequences or models.
    

---

```python
# Transform for webcam frames
eval_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406],
                std=[0.229, 0.224, 0.225]),
])
```

- **What it does:** Defines **preprocessing pipeline** for webcam frames.
    
    - Resize → ensure CNN input size.
        
    - ToTensor → convert frame to PyTorch tensor.
        
    - Normalize → match CNN backbone’s pretrained stats.
        
- **Why it’s needed:** Neural networks require **normalized tensors of consistent size**.
    

---

```python
# Load model
model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)
model = model.to(DEVICE)
checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)
model.load_state_dict(checkpoint["model_state"])
model.eval()
```

- **What it does:**
    
    - Instantiates **CNN-LSTM** model.
        
    - Loads pretrained **weights**.
        
    - Moves model to **GPU/CPU**.
        
    - Switches to **evaluation mode**.
        
- **Why it’s needed:** Prepares model for **real-time inference**.
    

---

```python
# Preprocess single frame
def preprocess_frame(frame):
    img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
    img = eval_transforms(img)
    return img
```

- **What it does:** Converts a webcam frame to a **preprocessed tensor**:
    
    - `cv2` reads frames in BGR → convert to RGB.
        
    - Convert to PIL → apply `eval_transforms`.
        
- **Why it’s needed:** LSTM model expects **tensors of shape (C, H, W) with normalization**.
    

---

```python
# Webcam prediction
cap = cv2.VideoCapture(0)  # use 0 for default webcam
frame_buffer = deque(maxlen=SEQ_LEN)  # store last SEQ_LEN frames
```

- **What it does:**
    
    - Opens webcam.
        
    - Creates a **buffer (deque)** to store the last `SEQ_LEN` frames for LSTM input.
        
- **Why it’s needed:** LSTM requires a **sequence of frames**, not single frames.
    

---

```python
while True:
    ret, frame = cap.read()
    if not ret:
        break
```

- **What it does:**
    
    - Reads frames continuously from the webcam.
        
    - If frame read fails (`ret=False`), exit loop.
        
- **Why it’s needed:** Ensures **continuous capture** and handles webcam errors.
    

---

```python
    # preprocess and add to buffer
    frame_tensor = preprocess_frame(frame)
    frame_buffer.append(frame_tensor)
```

- **What it does:**
    
    - Preprocess frame.
        
    - Append to `frame_buffer` (old frames automatically removed if buffer full).
        
- **Why it’s needed:** LSTM needs **exactly SEQ_LEN frames** to predict.
    

---

```python
    # once we have SEQ_LEN frames, make prediction
    if len(frame_buffer) == SEQ_LEN:
        seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE)  # (1, SEQ_LEN, C, H, W)
```

- **What it does:**
    
    - Stack frames in buffer into **sequence tensor**.
        
    - Add **batch dimension** → shape `(1, SEQ_LEN, C, H, W)`.
        
    - Move tensor to GPU/CPU.
        
- **Why it’s needed:** CNN-LSTM requires **batch + sequence + channel + height + width** input.
    

---

```python
        with torch.no_grad():
            outputs = model(seq_tensor)
            probs = torch.softmax(outputs, dim=1)
            pred_class = torch.argmax(probs, dim=1).item()
            label = classes[pred_class]
            confidence = probs[0, pred_class].item()
```

- **What it does:**
    
    - `torch.no_grad()` → disables gradient calculation (saves memory & speeds up).
        
    - Forward pass through model → get logits.
        
    - Convert logits to **probabilities** using `softmax`.
        
    - Pick **predicted class** and its **confidence**.
        
- **Why it’s needed:** Produces **real-time class prediction with probability**.
    

---

```python
        # display prediction on frame
        cv2.putText(frame, f"{label} ({confidence*100:.1f}%)", 
                    (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (0,0,255), 2)
```

- **What it does:** Draws **label and confidence** on the webcam frame.
    
- **Why it’s needed:** Gives **visual feedback** to the user.
    
- **When to use:** Always for **live display**.
    

---

```python
    cv2.imshow("Live Prediction", frame)
```

- **What it does:** Shows **the current webcam frame with prediction overlay**.
    
- **Why it’s needed:** Displays **real-time predictions**.
    

---

```python
    # quit on 'q' key
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

- **What it does:**
    
    - Waits 1 ms for a key press.
        
    - If `'q'` is pressed, exits loop.
        
- **Why it’s needed:** Allows **safe exit from live webcam feed**.
    

---

```python
cap.release()
cv2.destroyAllWindows()
```

- **What it does:**
    
    - Releases the webcam resource.
        
    - Closes all OpenCV windows.
        
- **Why it’s needed:** Prevents **camera lock** and frees system resources.
    

---

✅ **Summary:**

This script:

1. Captures frames from a **webcam in real-time**.
    
2. Buffers **SEQ_LEN frames** for the CNN-LSTM model.
    
3. Predicts **Normal or Suspicious** for every sequence.
    
4. Displays **prediction and confidence overlayed** on the live feed.
    

---


```python
import cv2

import torch

from PIL import Image

import torchvision.transforms as T

from collections import deque

import numpy as np

# from train_cnn_lstm import CNNLSTMModel # your model class

  

# -------------------------------

# Config

# -------------------------------

DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"

SEQ_LEN = 8

FRAME_SIZE = 224

classes = {0: "Normal", 1: "Suspicious"}

  

# -------------------------------

# Transform

# -------------------------------

eval_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406],

std=[0.229, 0.224, 0.225]),

])

  

# -------------------------------

# Load model

# -------------------------------

model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)

checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)

model.load_state_dict(checkpoint["model_state"])

model = model.to(DEVICE)

model.eval()

  

# -------------------------------

# Preprocess single frame

# -------------------------------

def preprocess_frame(frame):

img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))

img = eval_transforms(img)

return img

  

# -------------------------------

# Grad-CAM hooks

# -------------------------------

gradients = []

activations = []

  

def save_gradient(module, grad_input, grad_output):

gradients.append(grad_output[0])

  

def save_activation(module, input, output):

activations.append(output)

  

# Choose a CNN layer to inspect

target_layer = model.cnn.backbone[-1] # last layer of ResNet18 backbone

target_layer.register_forward_hook(save_activation)

target_layer.register_backward_hook(save_gradient)

  

# -------------------------------

# Webcam setup

# -------------------------------

cap = cv2.VideoCapture(0)

frame_buffer = deque(maxlen=SEQ_LEN)

  

while True:

ret, frame = cap.read()

if not ret:

break

  

# preprocess

frame_tensor = preprocess_frame(frame)

frame_buffer.append(frame_tensor)

  

if len(frame_buffer) == SEQ_LEN:

seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE) # (1, SEQ_LEN, C, H, W)

  

# clear previous hooks

gradients.clear()

activations.clear()

  

# forward

cnn_out = model.cnn(seq_tensor[:, -1]) # Grad-CAM on last frame only

model.zero_grad()

  

# backward for Suspicious class

score = cnn_out[0, 1]

score.backward()

  

# Grad-CAM computation

grad = gradients[-1].cpu().detach().numpy()[0]

act = activations[-1].cpu().detach().numpy()[0]

weights = np.mean(grad, axis=(1, 2))

cam = np.zeros(act.shape[1:], dtype=np.float32)

for i, w in enumerate(weights):

cam += w * act[i]

  

cam = np.maximum(cam, 0)

cam = cv2.resize(cam, (frame.shape[1], frame.shape[0]))

cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)

heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)

overlay = cv2.addWeighted(frame, 0.5, heatmap, 0.5, 0)

  

# Full sequence prediction

with torch.no_grad():

outputs = model(seq_tensor)

probs = torch.softmax(outputs, dim=1)

pred_class = torch.argmax(probs, dim=1).item()

label = classes[pred_class]

confidence = probs[0, pred_class].item()

  

# put text

cv2.putText(overlay, f"{label} ({confidence*100:.1f}%)", (10,30),

cv2.FONT_HERSHEY_SIMPLEX, 1, (255,255,255), 2)

  

# show

cv2.imshow("Live Grad-CAM", overlay)

else:

cv2.imshow("Live Grad-CAM", frame)

  

# quit

if cv2.waitKey(1) & 0xFF == ord('q'):

break

  

cap.release()

cv2.destroyAllWindows()
```


# Explain
Absolutely! Let’s go **line by line** and explain your **live Grad-CAM with CNN-LSTM webcam script**, detailing **what, why, and when**. This script predicts “Normal” or “Suspicious” events in real-time while showing **Grad-CAM visualization** on the last frame.

---

```python
import cv2
import torch
from PIL import Image
import torchvision.transforms as T
from collections import deque
import numpy as np
# from train_cnn_lstm import CNNLSTMModel  # your model class
```

- **What it does:** Imports libraries.
    
    - `cv2` → OpenCV for webcam and visualization.
        
    - `torch` → PyTorch for model & tensor operations.
        
    - `PIL.Image` → Convert OpenCV frame to PIL for transforms.
        
    - `torchvision.transforms` → Resize, normalize, convert to tensor.
        
    - `deque` → Buffer frames efficiently for sequence input.
        
    - `numpy` → For Grad-CAM computations.
        
- **Why it’s needed:** Essential for **live webcam input, preprocessing, Grad-CAM, and model prediction**.
    

---

```python
# -------------------------------
# Config
# -------------------------------
DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")
MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"
SEQ_LEN = 8
FRAME_SIZE = 224
classes = {0: "Normal", 1: "Suspicious"}
```

- **What it does:** Sets configuration parameters:
    
    - Device (GPU/CPU), model path, sequence length, frame size, and class labels.
        
- **Why it’s needed:** Makes code **flexible & easy to modify** for different setups.
    

---

```python
# -------------------------------
# Transform
eval_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406],
                std=[0.229, 0.224, 0.225]),
])
```

- **What it does:** Preprocessing pipeline for frames:
    
    - Resize → CNN input size.
        
    - ToTensor → convert to tensor.
        
    - Normalize → match pretrained CNN backbone.
        
- **Why it’s needed:** Neural networks require **normalized tensors of consistent size**.
    

---

```python
# -------------------------------
# Load model
model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)
checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)
model.load_state_dict(checkpoint["model_state"])
model = model.to(DEVICE)
model.eval()
```

- **What it does:**
    
    - Instantiates CNN-LSTM model.
        
    - Loads pretrained weights.
        
    - Moves to device and sets evaluation mode.
        
- **Why it’s needed:** Prepares model for **real-time inference**.
    

---

```python
# -------------------------------
# Preprocess single frame
def preprocess_frame(frame):
    img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
    img = eval_transforms(img)
    return img
```

- **What it does:** Converts OpenCV BGR frame to **preprocessed tensor** for model.
    
- **Why it’s needed:** LSTM expects **tensors (C, H, W) normalized**.
    

---

```python
# -------------------------------
# Grad-CAM hooks
gradients = []
activations = []

def save_gradient(module, grad_input, grad_output):
    gradients.append(grad_output[0])

def save_activation(module, input, output):
    activations.append(output)
```

- **What it does:** Defines **hook functions** for Grad-CAM:
    
    - `save_activation` → saves output of target CNN layer.
        
    - `save_gradient` → saves gradients w.r.t target layer during backward pass.
        
- **Why it’s needed:** Grad-CAM requires **feature maps + gradients** to compute heatmap.
    

---

```python
# Choose a CNN layer to inspect
target_layer = model.cnn.backbone[-1]  # last layer of ResNet18 backbone
target_layer.register_forward_hook(save_activation)
target_layer.register_backward_hook(save_gradient)
```

- **What it does:**
    
    - Registers hooks on **last convolutional layer** of CNN for Grad-CAM.
        
- **Why it’s needed:** Grad-CAM works best on **last conv layer** because it retains spatial info.
    

---

```python
# -------------------------------
# Webcam setup
cap = cv2.VideoCapture(0)
frame_buffer = deque(maxlen=SEQ_LEN)
```

- **What it does:**
    
    - Opens webcam.
        
    - Initializes **frame buffer** of length `SEQ_LEN`.
        
- **Why it’s needed:** CNN-LSTM requires **a sequence of frames** for prediction.
    

---

```python
while True:
    ret, frame = cap.read()
    if not ret:
        break
```

- **What it does:** Reads frames continuously.
    
- **Why it’s needed:** Handles **live video stream** and webcam failures.
    

---

```python
    # preprocess
    frame_tensor = preprocess_frame(frame)
    frame_buffer.append(frame_tensor)
```

- **What it does:** Preprocess frame and add to buffer.
    
- **Why it’s needed:** Buffer stores **last SEQ_LEN frames** for LSTM input.
    

---

```python
    if len(frame_buffer) == SEQ_LEN:
        seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE)  # (1, SEQ_LEN, C, H, W)
```

- **What it does:** Converts buffer into **batch tensor** for model input.
    
- **Why it’s needed:** CNN-LSTM expects **batch + sequence + channels + height + width**.
    

---

```python
        # clear previous hooks
        gradients.clear()
        activations.clear()
```

- **What it does:** Clears previous Grad-CAM activations/gradients.
    
- **Why it’s needed:** Avoid **mixing Grad-CAM info from previous frames**.
    

---

```python
        # forward
        cnn_out = model.cnn(seq_tensor[:, -1])  # Grad-CAM on last frame only
        model.zero_grad()
```

- **What it does:**
    
    - Forward pass **only through CNN** on last frame.
        
    - Zeroes gradients before backward.
        
- **Why it’s needed:** Grad-CAM uses CNN features of **single frame**.
    

---

```python
        # backward for Suspicious class
        score = cnn_out[0, 1]
        score.backward()
```

- **What it does:** Computes gradient w.r.t **target class** (“Suspicious”).
    
- **Why it’s needed:** Grad-CAM formula uses **class-specific gradients**.
    

---

```python
        # Grad-CAM computation
        grad = gradients[-1].cpu().detach().numpy()[0]
        act  = activations[-1].cpu().detach().numpy()[0]
        weights = np.mean(grad, axis=(1, 2))
        cam = np.zeros(act.shape[1:], dtype=np.float32)
        for i, w in enumerate(weights):
            cam += w * act[i]

        cam = np.maximum(cam, 0)
        cam = cv2.resize(cam, (frame.shape[1], frame.shape[0]))
        cam = (cam - cam.min()) / (cam.max() - cam.min() + 1e-9)
        heatmap = cv2.applyColorMap(np.uint8(255 * cam), cv2.COLORMAP_JET)
        overlay = cv2.addWeighted(frame, 0.5, heatmap, 0.5, 0)
```

- **What it does:**
    
    - Compute Grad-CAM heatmap from activations and gradients.
        
    - Apply **ReLU**, resize to frame size.
        
    - Normalize to 0–1.
        
    - Overlay heatmap on original frame.
        
- **Why it’s needed:** Visualizes **which regions CNN focuses on** for suspicious detection.
    

---

```python
        # Full sequence prediction
        with torch.no_grad():
            outputs = model(seq_tensor)
            probs = torch.softmax(outputs, dim=1)
            pred_class = torch.argmax(probs, dim=1).item()
            label = classes[pred_class]
            confidence = probs[0, pred_class].item()
```

- **What it does:** Predicts **full sequence label** using LSTM.
    
- **Why it’s needed:** Grad-CAM shows **last frame focus**, while LSTM gives **sequence prediction**.
    

---

```python
        # put text
        cv2.putText(overlay, f"{label} ({confidence*100:.1f}%)", (10,30),
                    cv2.FONT_HERSHEY_SIMPLEX, 1, (255,255,255), 2)
```

- **What it does:** Draws **predicted label & confidence** on frame.
    
- **Why it’s needed:** Shows **real-time prediction** to user.
    

---

```python
        # show
        cv2.imshow("Live Grad-CAM", overlay)
    else:
        cv2.imshow("Live Grad-CAM", frame)
```

- **What it does:** Displays either **overlayed Grad-CAM** or **raw frame** if buffer not full.
    
- **Why it’s needed:** Provides **visual feedback during prediction**.
    

---

```python
    # quit
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

- **What it does:** Exits loop on pressing `'q'`.
    
- **Why it’s needed:** Allows **safe termination** of live webcam feed.
    

---

```python
cap.release()
cv2.destroyAllWindows()
```

- **What it does:**
    
    - Releases webcam.
        
    - Closes OpenCV windows.
        
- **Why it’s needed:** Frees system resources and prevents **camera lock**.
    

---

✅ **Summary:**  
This script:

1. Captures webcam frames.
    
2. Buffers the last `SEQ_LEN` frames for **CNN-LSTM** prediction.
    
3. Computes **Grad-CAM on last frame** to visualize focus areas.
    
4. Makes **sequence prediction** using LSTM.
    
5. Displays **heatmap overlay + prediction confidence** in real-time.
    

---



```python
import cv2

import torch

from PIL import Image

import torchvision.transforms as T

from collections import deque

import numpy as np

# from train_cnn_lstm import CNNLSTMModel # your model class

  

# -------------------------------

# Config

# -------------------------------

DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")

MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"

SEQ_LEN = 8

FRAME_SIZE = 224

classes = {0: "Normal", 1: "Suspicious"}

  

# -------------------------------

# Transform

# -------------------------------

eval_transforms = T.Compose([

T.Resize((FRAME_SIZE, FRAME_SIZE)),

T.ToTensor(),

T.Normalize(mean=[0.485, 0.456, 0.406],

std=[0.229, 0.224, 0.225]),

])

  

# -------------------------------

# Load model

# -------------------------------

model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)

checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)

model.load_state_dict(checkpoint["model_state"])

model = model.to(DEVICE)

model.eval()

  

# -------------------------------

# Preprocess frame

# -------------------------------

def preprocess_frame(frame):

img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))

img = eval_transforms(img)

return img

  

# -------------------------------

# Video prediction

# -------------------------------

VIDEO_PATH = "/home/atiar/Downloads/video to frame/data/vandalism/Vandalism049_x264.mp4"

cap = cv2.VideoCapture(VIDEO_PATH)

  

frame_buffer = deque(maxlen=SEQ_LEN)

frame_idx = 0

  

# Optional: write annotated output video

fourcc = cv2.VideoWriter_fourcc(*'mp4v')

out = cv2.VideoWriter('annotated_output.mp4', fourcc, 20.0,

(int(cap.get(cv2.CAP_PROP_FRAME_WIDTH)),

int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))))

  

while True:

ret, frame = cap.read()

if not ret:

break

  

frame_idx += 1

frame_tensor = preprocess_frame(frame)

frame_buffer.append(frame_tensor)

  

label = "N/A"

confidence = 0.0

  

if len(frame_buffer) == SEQ_LEN:

seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE) # (1, SEQ_LEN, C, H, W)

with torch.no_grad():

outputs = model(seq_tensor)

probs = torch.softmax(outputs, dim=1)

pred_class = torch.argmax(probs, dim=1).item()

label = classes[pred_class]

confidence = probs[0, pred_class].item()

  

# Overlay prediction

cv2.putText(frame, f"{label} ({confidence*100:.1f}%)", (10,30),

cv2.FONT_HERSHEY_SIMPLEX, 1, (0,0,255), 2)

  

# Show frame

cv2.imshow("Video Prediction", frame)

out.write(frame)

  

# Quit on 'q'

if cv2.waitKey(1) & 0xFF == ord('q'):

break

  

cap.release()

out.release()

cv2.destroyAllWindows()

print("Video prediction completed. Saved as 'annotated_output.mp4'.")
```

# Explain

Absolutely! Let’s go **line by line** and explain your **video file prediction code** with CNN-LSTM, including **what, why, and when** each part is needed. This script predicts “Normal” or “Suspicious” on a video file and optionally saves an annotated video.

---

```python
import cv2
import torch
from PIL import Image
import torchvision.transforms as T
from collections import deque
import numpy as np
# from train_cnn_lstm import CNNLSTMModel  # your model class
```

- **What it does:** Imports necessary libraries.
    
    - `cv2` → Read video frames, display, and write output.
        
    - `torch` → PyTorch for model inference.
        
    - `PIL.Image` → Convert OpenCV frames to PIL format for transformations.
        
    - `torchvision.transforms` → Resize, normalize, convert to tensor.
        
    - `deque` → Efficiently store last `SEQ_LEN` frames.
        
    - `numpy` → For tensor to array conversions if needed.
        
- **Why it’s needed:** Essential for **video reading, preprocessing, buffering, and model prediction**.
    

---

```python
# -------------------------------
# Config
# -------------------------------
DEVICE = torch.device("cuda" if torch.cuda.is_available() else "cpu")
MODEL_PATH = "/home/atiar/Downloads/video to frame/best_cnn_lstm.pth"
SEQ_LEN = 8
FRAME_SIZE = 224
classes = {0: "Normal", 1: "Suspicious"}
```

- **What it does:** Sets configuration parameters.
    
    - `DEVICE` → Use GPU if available.
        
    - `MODEL_PATH` → Path to pretrained CNN-LSTM model.
        
    - `SEQ_LEN` → Number of frames LSTM expects as input.
        
    - `FRAME_SIZE` → Resize frames to this size.
        
    - `classes` → Map numeric output to human-readable label.
        
- **Why it’s needed:** Makes the code **flexible and easy to configure**.
    

---

```python
# -------------------------------
# Transform
eval_transforms = T.Compose([
    T.Resize((FRAME_SIZE, FRAME_SIZE)),
    T.ToTensor(),
    T.Normalize(mean=[0.485, 0.456, 0.406],
                std=[0.229, 0.224, 0.225]),
])
```

- **What it does:** Defines preprocessing for video frames:
    
    - Resize → CNN input size.
        
    - Convert to tensor → for PyTorch input.
        
    - Normalize → match pretrained backbone stats (like ResNet).
        
- **Why it’s needed:** CNN-LSTM requires **normalized tensors** of consistent size for prediction.
    

---

```python
# -------------------------------
# Load model
model = CNNLSTMModel(feat_dim=512, lstm_hidden=256, lstm_layers=1, num_classes=2, bidirectional=False)
checkpoint = torch.load(MODEL_PATH, map_location=DEVICE)
model.load_state_dict(checkpoint["model_state"])
model = model.to(DEVICE)
model.eval()
```

- **What it does:**
    
    - Instantiates the CNN-LSTM model.
        
    - Loads pretrained weights from checkpoint.
        
    - Moves model to GPU/CPU.
        
    - Sets model to evaluation mode (`eval()`) → disables dropout/batchnorm updates.
        
- **Why it’s needed:** Prepares model for **inference on video frames**.
    

---

```python
# -------------------------------
# Preprocess frame
def preprocess_frame(frame):
    img = Image.fromarray(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
    img = eval_transforms(img)
    return img
```

- **What it does:** Converts OpenCV BGR frame to **RGB PIL image**, then applies transforms (resize, tensor, normalize).
    
- **Why it’s needed:** CNN-LSTM expects **tensor of shape (C, H, W)** with normalization.
    

---

```python
# -------------------------------
# Video prediction
VIDEO_PATH = "/home/atiar/Downloads/video to frame/data/vandalism/Vandalism049_x264.mp4"
cap = cv2.VideoCapture(VIDEO_PATH)
```

- **What it does:** Opens the video file for reading frames.
    
- **Why it’s needed:** Enables **frame-by-frame processing** for prediction.
    

---

```python
frame_buffer = deque(maxlen=SEQ_LEN)
frame_idx = 0
```

- **What it does:**
    
    - `frame_buffer` → stores last `SEQ_LEN` frames for LSTM input.
        
    - `frame_idx` → keeps track of frame number.
        
- **Why it’s needed:** LSTM requires a **sequence of frames**.
    

---

```python
# Optional: write annotated output video
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
out = cv2.VideoWriter('annotated_output.mp4', fourcc, 20.0,
                      (int(cap.get(cv2.CAP_PROP_FRAME_WIDTH)),
                       int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))))
```

- **What it does:** Sets up a **video writer** to save annotated frames.
    
    - `fourcc` → codec (mp4v).
        
    - Frame rate → 20 FPS.
        
    - Frame size → same as original video.
        
- **Why it’s needed:** Saves **output video with predictions overlayed**.
    

---

```python
while True:
    ret, frame = cap.read()
    if not ret:
        break
```

- **What it does:** Reads frames in a loop.
    
- **Why it’s needed:** Stops loop when video ends (`ret=False`).
    

---

```python
    frame_idx += 1
    frame_tensor = preprocess_frame(frame)
    frame_buffer.append(frame_tensor)

    label = "N/A"
    confidence = 0.0
```

- **What it does:**
    
    - Preprocess frame and add to buffer.
        
    - Initialize label/confidence in case **sequence not full yet**.
        
- **Why it’s needed:** LSTM predicts only after **buffer has SEQ_LEN frames**.
    

---

```python
    if len(frame_buffer) == SEQ_LEN:
        seq_tensor = torch.stack(list(frame_buffer), dim=0).unsqueeze(0).to(DEVICE)  # (1, SEQ_LEN, C, H, W)
        with torch.no_grad():
            outputs = model(seq_tensor)
            probs = torch.softmax(outputs, dim=1)
            pred_class = torch.argmax(probs, dim=1).item()
            label = classes[pred_class]
            confidence = probs[0, pred_class].item()
```

- **What it does:**
    
    - Converts buffer into **sequence tensor**.
        
    - Adds batch dimension `(1, SEQ_LEN, C, H, W)`.
        
    - Forward pass through CNN-LSTM.
        
    - `softmax` → probabilities.
        
    - Get **predicted class and confidence**.
        
- **Why it’s needed:** Generates **realistic predictions using the sequence** of frames.
    

---

```python
        # Overlay prediction
        cv2.putText(frame, f"{label} ({confidence*100:.1f}%)", (10,30),
                    cv2.FONT_HERSHEY_SIMPLEX, 1, (0,0,255), 2)
```

- **What it does:** Draws **prediction and confidence** on frame.
    
- **Why it’s needed:** Makes video **interpretable for humans**.
    

---

```python
    # Show frame
    cv2.imshow("Video Prediction", frame)
    out.write(frame)
```

- **What it does:**
    
    - Displays **current frame in a window**.
        
    - Writes frame to **output video**.
        
- **Why it’s needed:** Allows **live preview** and saving annotated video.
    

---

```python
    # Quit on 'q'
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

- **What it does:** Stops loop if `'q'` key is pressed.
    
- **Why it’s needed:** Allows **safe manual termination**.
    

---

```python
cap.release()
out.release()
cv2.destroyAllWindows()
print("Video prediction completed. Saved as 'annotated_output.mp4'.")
```

- **What it does:**
    
    - Releases video capture and writer.
        
    - Closes OpenCV windows.
        
    - Prints completion message.
        
- **Why it’s needed:** **Frees resources**, ensures **video file is saved correctly**.
    

---

✅ **Summary:**

1. Reads video file frame by frame.
    
2. Buffers last `SEQ_LEN` frames for CNN-LSTM.
    
3. Predicts **Normal/Suspicious** per sequence.
    
4. Overlay predictions on video.
    
5. Saves **annotated output** as MP4.
    

---

