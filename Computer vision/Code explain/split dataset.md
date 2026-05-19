```python
import os
import shutil
import random
from pathlib import Path

INPUT_DIR = "/media/atiar/volume A/archive/Violence Detection Dataset"
OUTPUT_DIR = "Violence"

TRAIN_SPLIT = 0.7
VAL_SPLIT = 0.15
TEST_SPLIT = 0.15

CLASSES = ["Normal", "Suspicious"]

random.seed(42)

# create folders
for split in ["train", "val", "test"]:
    for cls in CLASSES:
        os.makedirs(os.path.join(OUTPUT_DIR, split, cls), exist_ok=True)

for cls in CLASSES:
    class_path = Path(INPUT_DIR) / cls

    # collect video files
    videos = [v for v in class_path.iterdir() if v.is_file()]

    random.shuffle(videos)

    total = len(videos)

    train_end = int(total * TRAIN_SPLIT)
    val_end = train_end + int(total * VAL_SPLIT)

    train_videos = videos[:train_end]
    val_videos = videos[train_end:val_end]
    test_videos = videos[val_end:]

    def copy_files(vlist, split):
        for v in vlist:
            dst = Path(OUTPUT_DIR) / split / cls / v.name
            shutil.copy2(v, dst)

    copy_files(train_videos, "train")
    copy_files(val_videos, "val")
    copy_files(test_videos, "test")

    print(f"{cls}:")
    print(" Train:", len(train_videos))
    print(" Val:", len(val_videos))
    print(" Test:", len(test_videos))
    print("-" * 30)

print("✅ Dataset Split Complete")
```


```python
import os
import shutil
import random
from pathlib import Path
```

### Importing Libraries

- `os` → Used for working with folders and file paths.
    
- `shutil` → Used for copying files.
    
- `random` → Used to shuffle the dataset randomly.
    
- `Path` from `pathlib` → Makes file/folder path handling easier and cleaner.
    

---

```python
INPUT_DIR = "/media/atiar/volume A/archive/Violence Detection Dataset"
OUTPUT_DIR = "Violence"
```

### Dataset Paths

- `INPUT_DIR` → Location of the original dataset.
    
- `OUTPUT_DIR` → New folder where the split dataset will be stored.
    

Example final structure:

```text
Violence/
    train/
    val/
    test/
```

---

```python
TRAIN_SPLIT = 0.7
VAL_SPLIT = 0.15
TEST_SPLIT = 0.15
```

### Dataset Split Ratios

These define how the dataset is divided:

- 70% → training data
    
- 15% → validation data
    
- 15% → testing data
    

---

```python
CLASSES = ["Normal", "Suspicious"]
```

### Class Names

The dataset has two categories:

- `Normal`
    
- `Suspicious`
    

Your original dataset should contain:

```text
Violence Detection Dataset/
    Normal/
    Suspicious/
```

---

```python
random.seed(42)
```

### Fixed Randomness

This ensures the shuffle result is always the same every time the script runs.

Why useful?

- Reproducibility
    
- Same train/val/test split every run
    

---

# CREATE OUTPUT FOLDERS

```python
for split in ["train", "val", "test"]:
    for cls in CLASSES:
        os.makedirs(os.path.join(OUTPUT_DIR, split, cls), exist_ok=True)
```

### What Happens Here?

This loop creates folders like:

```text
Violence/
    train/
        Normal/
        Suspicious/
    val/
        Normal/
        Suspicious/
    test/
        Normal/
        Suspicious/
```

### Breakdown

- Outer loop → goes through `train`, `val`, `test`
    
- Inner loop → goes through each class
    

```python
os.makedirs(...)
```

Creates directories recursively.

```python
exist_ok=True
```

Prevents error if folder already exists.

---

# PROCESS EACH CLASS

```python
for cls in CLASSES:
```

### Loop Through Each Class

First:

```python
cls = "Normal"
```

Then:

```python
cls = "Suspicious"
```

---

```python
class_path = Path(INPUT_DIR) / cls
```

### Build Path to Class Folder

Example:

```python
/media/atiar/volume A/archive/Violence Detection Dataset/Normal
```

`Path()` makes path handling cleaner.

---

# COLLECT VIDEO FILES

```python
videos = [v for v in class_path.iterdir() if v.is_file()]
```

### What This Does

- Reads all items inside the class folder
    
- Keeps only files
    

Example:

```python
["video1.mp4", "video2.mp4", ...]
```

### Breakdown

- `class_path.iterdir()` → iterate through all items
    
- `v.is_file()` → keep only files
    

---

# SHUFFLE VIDEOS

```python
random.shuffle(videos)
```

### Why?

Randomizes the file order before splitting.

Without shuffling:

- Training may get only early files
    
- Testing may get only later files
    

Random shuffle prevents bias.

---

# TOTAL NUMBER OF VIDEOS

```python
total = len(videos)
```

Stores total number of video files.

Example:

```python
total = 100
```

---

# CALCULATE SPLIT INDICES

```python
train_end = int(total * TRAIN_SPLIT)
```

Example:

```python
100 * 0.7 = 70
```

So:

```python
train_end = 70
```

---

```python
val_end = train_end + int(total * VAL_SPLIT)
```

Example:

```python
70 + 15 = 85
```

So:

```python
val_end = 85
```

Remaining files go to test set.

---

# SPLIT DATA

```python
train_videos = videos[:train_end]
```

Takes first 70%.

Example:

```python
videos[0:70]
```

---

```python
val_videos = videos[train_end:val_end]
```

Takes next 15%.

Example:

```python
videos[70:85]
```

---

```python
test_videos = videos[val_end:]
```

Takes remaining files.

Example:

```python
videos[85:]
```

---

# FUNCTION TO COPY FILES

```python
def copy_files(vlist, split):
```

Defines a function:

- `vlist` → list of videos
    
- `split` → train/val/test
    

---

```python
for v in vlist:
```

Loop through each video file.

---

```python
dst = Path(OUTPUT_DIR) / split / cls / v.name
```

### Destination Path

Example:

```python
Violence/train/Normal/video1.mp4
```

### Components

- `OUTPUT_DIR`
    
- `split`
    
- `cls`
    
- original filename
    

---

```python
shutil.copy2(v, dst)
```

Copies the file from source to destination.

`copy2()` preserves metadata like:

- modification date
    
- permissions
    

---

# COPY FILES TO EACH SPLIT

```python
copy_files(train_videos, "train")
copy_files(val_videos, "val")
copy_files(test_videos, "test")
```

Calls the function three times:

- copies training files
    
- copies validation files
    
- copies testing files
    

---

# PRINT STATISTICS

```python
print(f"{cls}:")
```

Prints current class name.

Example:

```text
Normal:
```

---

```python
print(" Train:", len(train_videos))
print(" Val:", len(val_videos))
print(" Test:", len(test_videos))
```

Shows number of files in each split.

Example:

```text
Train: 70
Val: 15
Test: 15
```

---

```python
print("-" * 30)
```

Prints:

```text
------------------------------
```

Used for formatting output.

---

# FINAL MESSAGE

```python
print("✅ Dataset Split Complete")
```

Printed after all classes are processed.

Example:

```text
✅ Dataset Split Complete
```

---

# OVERALL FLOW OF THE PROGRAM

```text
1. Import libraries
2. Define dataset paths
3. Define split ratios
4. Create output folders
5. Read video files
6. Shuffle videos randomly
7. Split into train/val/test
8. Copy files into new folders
9. Print summary
```

---

# FINAL OUTPUT STRUCTURE

```text
Violence/
    train/
        Normal/
        Suspicious/

    val/
        Normal/
        Suspicious/

    test/
        Normal/
        Suspicious/
```

