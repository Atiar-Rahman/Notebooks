```python
import cv2
from pathlib import Path
from collections import deque

INPUT_DIR = "Violence"
OUTPUT_DIR = "/home/atiar/Downloads/Final_dataset_Gray"

SEQ_LEN = 8
IMG_SIZE = 96
STRIDE = 2
JPEG_QUALITY = 70

for split in ["train", "val", "test"]:
    for cls in ["Normal", "Suspicious"]:

        input_path = Path(INPUT_DIR) / split / cls
        output_path = Path(OUTPUT_DIR) / split / cls
        output_path.mkdir(parents=True, exist_ok=True)

        for video_file in input_path.glob("*"):

            cap = cv2.VideoCapture(str(video_file))

            frames = deque(maxlen=SEQ_LEN)
            seq_count = 0
            frame_idx = 0

            while True:
                ret, frame = cap.read()
                if not ret:
                    break

                frame_idx += 1

                # -------- stride control --------
                if frame_idx % STRIDE != 0:
                    continue

                # -------- GrayScale --------
                frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

                # -------- Resize --------
                frame = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))

                frames.append(frame)

                # -------- save sliding window --------
                if len(frames) == SEQ_LEN:
                    seq_folder = output_path / f"{video_file.stem}_seq{seq_count}"
                    seq_folder.mkdir(parents=True, exist_ok=True)

                    for i, f in enumerate(frames):
                        cv2.imwrite(
                            str(seq_folder / f"frame_{i}.jpg"),
                            f,
                            [cv2.IMWRITE_JPEG_QUALITY, JPEG_QUALITY]
                        )

                    seq_count += 1

            cap.release()
            print(f"{video_file.name} -> {seq_count} sequences created")

print("✅ Optimized GrayScale sequence generation complete")
```

```python
import cv2
```

- OpenCV library import করা হয়েছে।
    
- ভিডিও read, resize, grayscale conversion, image save করার জন্য লাগে।
    

---

```python
from pathlib import Path
```

- Modern path handling library।
    
- ফাইল/ফোল্ডার path সহজভাবে manage করতে সাহায্য করে।
    

---

```python
from collections import deque
```

- `deque` হলো fast queue structure।
    
- এখানে sliding window sequence বানানোর জন্য ব্যবহার করা হয়েছে।
    

---

# CONFIGURATION

```python
INPUT_DIR = "Violence"
```

- Original split dataset location।
    

Example:

```text
Violence/
 ├── train/
 ├── val/
 └── test/
```

---

```python
OUTPUT_DIR = "/home/atiar/Downloads/Final_dataset_Gray"
```

- Processed grayscale sequences এখানে save হবে।
    

---

```python
SEQ_LEN = 8
```

- প্রতিটি sequence এ 8 frame থাকবে।
    

Example:

```text
sequence:
frame1 frame2 frame3 ... frame8
```

---

```python
IMG_SIZE = 96
```

- সব frame resize হয়ে:
    

```text
96 × 96
```

হবে।

ছোট image ⇒

- faster training
    
- less storage
    
- less GPU memory
    

---

```python
STRIDE = 2
```

- প্রতি 2nd frame নেওয়া হবে।
    

Example:

```text
Original:
1 2 3 4 5 6 7 8

Used:
2 4 6 8
```

এতে:

- duplicate frames কমে
    
- dataset ছোট হয়
    
- motion information ভালো থাকে
    

---

```python
JPEG_QUALITY = 70
```

- JPG compression quality।
    
- 70 দিলে:
    
    - file size ছোট হয়
        
    - quality acceptable থাকে
        

---

# MAIN LOOP

```python
for split in ["train", "val", "test"]:
```

- তিন dataset split এর উপর loop।
    

---

```python
for cls in ["Normal", "Suspicious"]:
```

- দুই class এর উপর loop।
    

---

```python
input_path = Path(INPUT_DIR) / split / cls
```

Example:

```text
Violence/train/Normal
```

---

```python
output_path = Path(OUTPUT_DIR) / split / cls
```

Processed output path।

---

```python
output_path.mkdir(parents=True, exist_ok=True)
```

- Folder না থাকলে create করবে।
    

---

# VIDEO LOOP

```python
for video_file in input_path.glob("*"):
```

- সব video file iterate করবে।
    

---

```python
cap = cv2.VideoCapture(str(video_file))
```

- ভিডিও open করছে।
    

---

# SEQUENCE BUFFER

```python
frames = deque(maxlen=SEQ_LEN)
```

- সর্বশেষ 8 frame store করবে।
    
- নতুন frame এলে পুরনো frame automatic remove হবে।
    

Sliding window এর core logic এটা।

---

```python
seq_count = 0
```

- কয়টা sequence তৈরি হয়েছে count রাখে।
    

---

```python
frame_idx = 0
```

- frame number track করে।
    

---

# FRAME READING

```python
while True:
```

- পুরো ভিডিও frame by frame পড়বে।
    

---

```python
ret, frame = cap.read()
```

- এক frame read করছে।
    

---

```python
if not ret:
    break
```

- ভিডিও শেষ হলে loop stop।
    

---

```python
frame_idx += 1
```

- frame counter increase।
    

---

# STRIDE CONTROL

```python
if frame_idx % STRIDE != 0:
    continue
```

যদি STRIDE=2:

```text
1 skip
2 use
3 skip
4 use
```

---

# GRAYSCALE CONVERSION

```python
frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
```

RGB/BGR → grayscale।

Result:

```text
3 channel → 1 channel
```

Storage ও training faster হয়।

---

# RESIZE

```python
frame = cv2.resize(frame, (IMG_SIZE, IMG_SIZE))
```

সব frame:

```text
96 × 96
```

এ convert হয়।

---

# ADD TO SEQUENCE

```python
frames.append(frame)
```

বর্তমান frame queue তে add।

---

# SAVE SLIDING WINDOW

```python
if len(frames) == SEQ_LEN:
```

যখন queue তে 8 frame complete হবে:

```text
[f1 f2 f3 f4 f5 f6 f7 f8]
```

তখন save করবে।

---

```python
seq_folder = output_path / f"{video_file.stem}_seq{seq_count}"
```

Example:

```text
fight001_seq0
fight001_seq1
```

---

```python
seq_folder.mkdir(parents=True, exist_ok=True)
```

- sequence folder create।
    

---

# SAVE EACH FRAME

```python
for i, f in enumerate(frames):
```

- 8 frame save করবে।
    

---

```python
cv2.imwrite(
    str(seq_folder / f"frame_{i}.jpg"),
    f,
    [cv2.IMWRITE_JPEG_QUALITY, JPEG_QUALITY]
)
```

Example output:

```text
frame_0.jpg
frame_1.jpg
...
frame_7.jpg
```

---

```python
seq_count += 1
```

- next sequence number।
    

---

# CLEANUP

```python
cap.release()
```

- ভিডিও close।
    

---

```python
print(f"{video_file.name} -> {seq_count} sequences created")
```

- কত sequence তৈরি হলো দেখাবে।
    

---

# FINAL MESSAGE

```python
print("✅ Optimized GrayScale sequence generation complete")
```

সব process complete।

---

# MOST IMPORTANT CONCEPT → Sliding Window

ধরো frames:

```text
1 2 3 4 5 6 7 8 9 10
```

SEQ_LEN=8 হলে:

Sequence 1:

```text
1 2 3 4 5 6 7 8
```

Sequence 2:

```text
2 3 4 5 6 7 8 9
```

Sequence 3:

```text
3 4 5 6 7 8 9 10
```

এটা temporal learning এর জন্য খুব powerful।