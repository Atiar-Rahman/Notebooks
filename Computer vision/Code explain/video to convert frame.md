# 🚀 Complete YouTube → Action Dataset Pipeline (CNN + LSTM)

---

# 🧠 STEP 1 — Download YouTube Video

## Install:

```bash
pip install yt-dlp
```

## Download:

```bash
yt-dlp "YOUTUBE_URL"
```

---

# 🧠 STEP 2 — Trim useful clip (FFmpeg)

## Keep only useful action part

```bash
ffmpeg -i input.mp4 -ss 00:00:10 -to 00:00:30 -c copy output.mp4
```

👉 keeps:

```id="a1"
10s → 30s
```

---

# 🧠 STEP 3 — Best FPS for CNN+LSTM

## Recommended:

|Task|FPS|
|---|---|
|Slow action|3–5 FPS|
|Normal action|5–10 FPS|
|Fast action|10–15 FPS|

---

## BEST DEFAULT:

```id="fps1"
5 FPS
```

👉 avoids duplicate frames + reduces computation

---

# 🧠 STEP 4 — Automatic Frame Extractor

```python
import cv2
import os

video_path = "video.mp4"
output_folder = "frames"

os.makedirs(output_folder, exist_ok=True)

cap = cv2.VideoCapture(video_path)

fps = cap.get(cv2.CAP_PROP_FPS)
frame_interval = int(fps / 5)  # extract 5 FPS

count = 0
saved = 0

while True:
    ret, frame = cap.read()

    if not ret:
        break

    if count % frame_interval == 0:
        cv2.imwrite(f"{output_folder}/frame_{saved}.jpg", frame)
        saved += 1

    count += 1

cap.release()

print("Done!")
```

---

# 🧠 STEP 5 — Automatic Blur Remover

```python
import cv2
import os

input_folder = "frames"
output_folder = "clean_frames"

os.makedirs(output_folder, exist_ok=True)

THRESHOLD = 100

for file in os.listdir(input_folder):

    path = os.path.join(input_folder, file)

    image = cv2.imread(path)

    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    score = cv2.Laplacian(gray, cv2.CV_64F).var()

    if score > THRESHOLD:
        cv2.imwrite(os.path.join(output_folder, file), image)

print("Blur filtering done!")
```

---

# 🧠 STEP 6 — Duplicate Frame Remover

## Simple frame difference method

```python
import cv2
import os
import numpy as np

input_folder = "clean_frames"
output_folder = "unique_frames"

os.makedirs(output_folder, exist_ok=True)

prev = None

THRESHOLD = 5

for file in sorted(os.listdir(input_folder)):

    path = os.path.join(input_folder, file)

    img = cv2.imread(path)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    if prev is None:
        cv2.imwrite(os.path.join(output_folder, file), img)
        prev = gray
        continue

    diff = np.mean(cv2.absdiff(prev, gray))

    if diff > THRESHOLD:
        cv2.imwrite(os.path.join(output_folder, file), img)

    prev = gray

print("Duplicate removal done!")
```

---

# 🧠 STEP 7 — Resize Frames

```python
img = cv2.resize(img, (224,224))
```

---

# 🧠 STEP 8 — Sequence Creation for CNN+LSTM

Example:

```id="seq1"
16 frames = 1 sample
```

Best common settings:

|Type|Sequence Length|
|---|---|
|Light model|8|
|Standard|16|
|Heavy action|32|

---

# 🚀 BEST DEFAULT

```id="best1"
16 frames
5 FPS
224x224
```

---

# 🧠 STEP 9 — FFmpeg Useful Commands

---

## Extract frames directly

```bash
ffmpeg -i video.mp4 -vf fps=5 frames/frame_%04d.jpg
```

---

## Resize video

```bash
ffmpeg -i input.mp4 -vf scale=224:224 output.mp4
```

---

## Remove audio

```bash
ffmpeg -i input.mp4 -an output.mp4
```

---

## Convert FPS

```bash
ffmpeg -i input.mp4 -filter:v fps=5 output.mp4
```

---

# 🧠 STEP 10 — Dataset Structure

```id="ds1"
dataset/
    walking/
    running/
    fighting/
```

---

# 🔥 VERY IMPORTANT FOR CNN+LSTM

## Keep temporal order

❌ DON'T:

```id="bad1"
shuffle frames randomly
```

✅ DO:

```id="good1"
frame1 → frame2 → frame3
```

---

# 🚀 GOLDEN PIPELINE

```id="pipe1"
YouTube
↓
Trim
↓
Extract frames
↓
Blur remove
↓
Duplicate remove
↓
Resize
↓
Sequence create
↓
Train CNN+LSTM
```

---

# ⚡ BEST PRACTICAL SETTINGS

|Parameter|Recommended|
|---|---|
|FPS|5|
|Image size|224x224|
|Sequence length|16|
|Blur threshold|100|
|Batch size|8–16|

---

# 🧠 FINAL PRO TIP

👉 More data ≠ better always

Best results come from:

```id="tip1"
clean + diverse + correctly labeled sequences
```


YouTube video download করতে সবচেয়ে সহজ ও reliable উপায় হলো `yt-dlp` ব্যবহার করা।

---

# 🚀 STEP 1 — Install yt-dlp

## Linux / Mac

```bash id="a1"
pip install yt-dlp
```

## Windows

```bash id="a2"
pip install yt-dlp
```

---

# 🚀 STEP 2 — Download video

```bash id="a3"
yt-dlp "YOUTUBE_VIDEO_URL"
```

Example:

```bash id="a4"
yt-dlp "https://www.youtube.com/watch?v=VIDEO_ID"
```

---

# 🚀 STEP 3 — Download specific quality

## 720p

```bash id="a5"
yt-dlp -f "bestvideo[height<=720]+bestaudio/best" URL
```

---

# 🚀 STEP 4 — Save in custom folder

```bash id="a6"
yt-dlp -o "videos/%(title)s.%(ext)s" URL
```

---

# 🚀 STEP 5 — Download multiple videos

Create:

```id="a7"
urls.txt
```

Inside:

```id="a8"
url1
url2
url3
```

Then:

```bash id="a9"
yt-dlp -a urls.txt
```

---

# 🚀 STEP 6 — Download only useful clips (recommended)

You can trim later using FFmpeg:

```bash id="a10"
ffmpeg -i input.mp4 -ss 00:00:10 -to 00:00:30 -c copy output.mp4
```

---

# 🧠 BEST PRACTICE FOR DATASET

## Download:

✅ clear videos
✅ stable camera
✅ visible action
✅ minimal text/watermark

Avoid:
❌ meme edits
❌ heavy transitions
❌ blurry clips
❌ compilation videos

---

# 🚀 VERY IMPORTANT (Dataset legality)

For research/personal ML experimentation সাধারণত okay, কিন্তু:

* copyrighted content redistribute কোরো না
* public dataset release করলে source/license check করো

---

# ⚡ PRO TIP

For action recognition:

```id="tip1"
Short clean clips > long noisy videos
```

---

# 🧠 Full workflow

```id="wf1"
YouTube
↓
Download
↓
Trim
↓
Extract frames
↓
Clean noisy frames
↓
Create sequences
↓
Train model
```
তুমি Python script-এ `yt-dlp` ব্যবহার করে URL add করতে পারো।

---

# 🚀 Simple Example

## Install first

```bash id="i1"
pip install yt-dlp
```

---

# 🧠 Python Script

```python id="p1"
import yt_dlp

url = "https://www.youtube.com/watch?v=VIDEO_ID"

ydl_opts = {
    'outtmpl': 'videos/%(title)s.%(ext)s'
}

with yt_dlp.YoutubeDL(ydl_opts) as ydl:
    ydl.download([url])

print("Download completed!")
```

---

# 🚀 Multiple URLs

```python id="p2"
import yt_dlp

urls = [
    "https://www.youtube.com/watch?v=VIDEO1",
    "https://www.youtube.com/watch?v=VIDEO2"
]

ydl_opts = {
    'outtmpl': 'videos/%(title)s.%(ext)s'
}

with yt_dlp.YoutubeDL(ydl_opts) as ydl:
    ydl.download(urls)
```

---

# 🚀 Download 720p

```python id="p3"
ydl_opts = {
    'format': 'bestvideo[height<=720]+bestaudio/best',
    'outtmpl': 'videos/%(title)s.%(ext)s'
}
```

---

# 🚀 Full Recommended Script

```python id="p4"
import yt_dlp
import os

os.makedirs("videos", exist_ok=True)

url = "https://www.youtube.com/watch?v=VIDEO_ID"

ydl_opts = {
    'format': 'bestvideo[height<=720]+bestaudio/best',
    'outtmpl': 'videos/%(title)s.%(ext)s'
}

with yt_dlp.YoutubeDL(ydl_opts) as ydl:
    ydl.download([url])

print("Done!")
```

---

# 🧠 Run Script

Save:

```id="r1"
download.py
```

Run:

```bash id="r2"
python download.py
```

---

# ⚡ PRO TIP

Dataset collection এর জন্য:

```id="tip1"
1 action class = 1 folder
```

Example:

```id="tip2"
dataset/
   walking/
   running/
   fighting/
```

YouTube videos download করে class অনুযায়ী রাখো।
