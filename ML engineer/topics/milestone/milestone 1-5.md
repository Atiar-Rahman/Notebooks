Great. তাহলে আজ থেকে **Milestone 1 — AI Video Pipeline Foundation** শুরু করি।

তোমার Python knowledge আছে, তাই basic syntax না পড়ে আমরা সরাসরি **যে Python concepts এই AI project-এ বাস্তবে লাগবে** সেগুলো শিখব।

# 🟢 M1 — AI Video Pipeline Foundation

### M1-এর লক্ষ্য

এই milestone শেষে তুমি এমন একটা Python pipeline বানাতে পারবে:

```text
Input Video
    ↓
Python Pipeline
    ↓
Read File
    ↓
Extract Metadata
    ↓
Create Output Folders
    ↓
Save JSON Metadata
    ↓
Log Everything
```

---

# M1 Topics

আমরা 10টা topic cover করব:

```text
M1.1  Project Environment
M1.2  pathlib & File Management
M1.3  JSON
M1.4  JSONL
M1.5  Functions & Modular Code
M1.6  Exception Handling
M1.7  Logging
M1.8  argparse
M1.9  Environment Variables
M1.10 Complete Pipeline
```

---

# M1.1 — Project Environment

প্রথমে project তৈরি করো।

Ubuntu terminal:

```bash
mkdir educational_video_ai
cd educational_video_ai
```

Virtual environment:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

Check:

```bash
python --version
```

তারপর:

```bash
mkdir -p videos
mkdir -p frames
mkdir -p transcripts
mkdir -p dataset
mkdir -p logs
mkdir -p scripts
```

Final structure:

```text
educational_video_ai/
│
├── .venv/
│
├── videos/
├── frames/
├── transcripts/
├── dataset/
├── logs/
├── scripts/
│
├── requirements.txt
└── README.md
```

---

# M1.2 — pathlib

AI pipeline-এ আমরা অনেক file নিয়ে কাজ করব।

যেমন:

```text
video.mp4
frame_001.jpg
frame_002.jpg
transcript.json
scene.json
final_video.mp4
```

তাই `pathlib` খুব গুরুত্বপূর্ণ।

Example:

```python
from pathlib import Path

video_dir = Path("videos")

print(video_dir.exists())
```

Folder তৈরি:

```python
frames_dir = Path("frames")

frames_dir.mkdir(exist_ok=True)
```

File check:

```python
video = Path("videos/video.mp4")

if video.exists():
    print("Video exists")
else:
    print("Video not found")
```

Files দেখা:

```python
for file in video_dir.iterdir():
    print(file)
```

---

# M1.3 — JSON

আমাদের project-এর সবচেয়ে গুরুত্বপূর্ণ data format হবে **JSON**।

Example:

```python
import json

data = {
    "video_id": "video_001",
    "topic": "Photosynthesis",
    "subject": "Biology",
    "duration": 60
}

with open("dataset/metadata.json", "w") as file:
    json.dump(data, file, indent=4)
```

Result:

```json
{
    "video_id": "video_001",
    "topic": "Photosynthesis",
    "subject": "Biology",
    "duration": 60
}
```

Read:

```python
with open("dataset/metadata.json", "r") as file:
    data = json.load(file)

print(data["topic"])
```

Output:

```text
Photosynthesis
```

---

# M1.4 — JSONL

এটা তোমার future training dataset-এর জন্য খুব গুরুত্বপূর্ণ।

JSON:

```text
metadata.json
```

একটা object রাখতে পারে।

JSONL:

```text
train.jsonl
```

প্রতিটি line একটি training example।

Example:

```json
{"topic":"Photosynthesis","subject":"Biology"}
{"topic":"Binary Search","subject":"Computer Science"}
{"topic":"Newton's Law","subject":"Physics"}
```

Python:

```python
import json

data = [
    {
        "topic": "Photosynthesis",
        "subject": "Biology"
    },
    {
        "topic": "Binary Search",
        "subject": "Computer Science"
    }
]

with open("dataset/train.jsonl", "w") as file:
    for item in data:
        file.write(json.dumps(item) + "\n")
```

Read:

```python
with open("dataset/train.jsonl", "r") as file:

    for line in file:
        item = json.loads(line)
        print(item)
```

---

# M1.5 — Modular Functions

আমরা কখনো একটা বড় Python file-এ সব code লিখব না।

Instead:

```text
scripts/
├── video.py
├── dataset.py
├── utils.py
└── main.py
```

Function example:

```python
def create_directory(path):
    path.mkdir(parents=True, exist_ok=True)
```

তারপর:

```python
from pathlib import Path

create_directory(Path("frames"))
```

এতে pipeline maintain করা সহজ হবে।

---

# M1.6 — Exception Handling

AI pipeline-এ error আসবেই।

Example:

```python
from pathlib import Path

video = Path("videos/video.mp4")

try:
    if not video.exists():
        raise FileNotFoundError("Video file not found")

    print("Video found")

except FileNotFoundError as error:
    print(f"Error: {error}")
```

Future pipeline:

```text
Video
 ↓
Whisper
 ↓
Vision
 ↓
LLM
 ↓
TTS
 ↓
FFmpeg
```

যেকোনো জায়গায় error হতে পারে।

তাই error handling খুব important।

---

# M1.7 — Logging

শুধু `print()` ব্যবহার না করে আমরা logging ব্যবহার করব।

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.info("Pipeline started")
logging.warning("Video duration is short")
logging.error("Video not found")
```

Output:

```text
2026-09-06 07:10:20 - INFO - Pipeline started
```

এগুলো পরে:

```text
logs/pipeline.log
```

এ save করতে পারবে।

---

# M1.8 — argparse

এটা দিয়ে terminal থেকে input দেওয়া যাবে।

Example:

```bash
python main.py --video videos/video.mp4
```

Python:

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--video",
    required=True
)

args = parser.parse_args()

print(args.video)
```

Run:

```bash
python main.py --video videos/video.mp4
```

Output:

```text
videos/video.mp4
```

এটা আমাদের final AI pipeline-এ খুব useful হবে।

---

# M1.9 — Environment Variables

API key কখনো code-এর মধ্যে লিখবে না।

❌ Bad:

```python
API_KEY = "my-secret-key"
```

Better:

```text
.env
```

```text
OPENAI_API_KEY=xxxx
```

Python:

```python
import os

api_key = os.getenv("OPENAI_API_KEY")
```

পরে `python-dotenv` ব্যবহার করব।

---

# M1.10 — Complete Mini Project

এখন সব concepts একসাথে ব্যবহার করো।

Create:

```text
scripts/main.py
```

Code:

```python
import argparse
import json
import logging
from pathlib import Path


# -------------------------
# Logging
# -------------------------

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)


# -------------------------
# Create directories
# -------------------------

def create_directories():

    directories = [
        "videos",
        "frames",
        "transcripts",
        "dataset",
        "logs"
    ]

    for directory in directories:

        path = Path(directory)

        path.mkdir(
            parents=True,
            exist_ok=True
        )

        logging.info(
            f"Directory ready: {path}"
        )


# -------------------------
# Video validation
# -------------------------

def validate_video(video_path):

    video = Path(video_path)

    if not video.exists():

        raise FileNotFoundError(
            f"Video not found: {video}"
        )

    if video.suffix.lower() not in [
        ".mp4",
        ".avi",
        ".mov",
        ".mkv"
    ]:

        raise ValueError(
            "Unsupported video format"
        )

    logging.info(
        f"Video validated: {video}"
    )

    return video


# -------------------------
# Save metadata
# -------------------------

def save_metadata(video_path):

    video = Path(video_path)

    metadata = {

        "video_id": video.stem,

        "filename": video.name,

        "extension": video.suffix,

        "path": str(video)

    }

    output = Path(
        "dataset/video_metadata.json"
    )

    with open(output, "w") as file:

        json.dump(
            metadata,
            file,
            indent=4
        )

    logging.info(
        f"Metadata saved: {output}"
    )


# -------------------------
# Main
# -------------------------

def main():

    parser = argparse.ArgumentParser(
        description="Educational Video AI Pipeline"
    )

    parser.add_argument(
        "--video",
        required=True,
        help="Path to input video"
    )

    args = parser.parse_args()

    try:

        logging.info(
            "Pipeline started"
        )

        create_directories()

        video = validate_video(
            args.video
        )

        save_metadata(video)

        logging.info(
            "Pipeline completed successfully"
        )

    except Exception as error:

        logging.error(
            f"Pipeline failed: {error}"
        )


if __name__ == "__main__":
    main()
```

---

# Run করার আগে

একটা test video রাখো:

```text
videos/video.mp4
```

তারপর:

```bash
python scripts/main.py --video videos/video.mp4
```

Expected:

```text
Pipeline started
Directory ready: videos
Directory ready: frames
Directory ready: transcripts
Directory ready: dataset
Directory ready: logs
Video validated: videos/video.mp4
Metadata saved: dataset/video_metadata.json
Pipeline completed successfully
```

তারপর:

```text
dataset/video_metadata.json
```

এর মধ্যে থাকবে:

```json
{
    "video_id": "video",
    "filename": "video.mp4",
    "extension": ".mp4",
    "path": "videos/video.mp4"
}
```

---

# 🧠 M1-এর সবচেয়ে গুরুত্বপূর্ণ Concept

এই architecture-টা মনে রাখো:

```text
              main.py
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
  Validation  Metadata  Logging
       │         │
       └─────────┼─────────┘
                 ↓
          Dataset Folder
```

পরবর্তীতে এটিই বড় হবে:

```text
                    main.py
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
     Whisper        Vision           LLM
        ↓              ↓              ↓
   Transcript     Visual Info     Scene Plan
        └──────────────┼──────────────┘
                       ↓
                  Video Generator
```

---

# ✅ M1 Completion Checklist

M1 complete বলার আগে এগুলো নিজে করতে পারো কিনা check করো:

* [ ] Virtual environment তৈরি করতে পারি
* [ ] `pathlib` দিয়ে folder/file handle করতে পারি
* [ ] JSON write করতে পারি
* [ ] JSON read করতে পারি
* [ ] JSONL তৈরি/read করতে পারি
* [ ] Function দিয়ে code modular করতে পারি
* [ ] `try/except` ব্যবহার করতে পারি
* [ ] Python logging ব্যবহার করতে পারি
* [ ] `argparse` দিয়ে terminal argument নিতে পারি
* [ ] Environment variable কী বুঝি
* [ ] Complete pipeline run করতে পারি

### 🎯 M1 Practice Task

নিজে একটি program বানাও:

```text
video.mp4
   ↓
Python
   ↓
metadata.json
```

যেখানে metadata-তে অন্তত এগুলো থাকবে:

```json
{
    "video_id": "...",
    "filename": "...",
    "extension": "...",
    "path": "...",
    "status": "ready"
}
```

**এটা নিজে করে ফেললে M1 শেষ।**

এরপর আমরা **M2 — Video Processing & FFmpeg/OpenCV** শুরু করব, যেখানে প্রথমবার তোমার actual educational video-এর **FPS, resolution, duration, audio এবং frames** নিয়ে কাজ করব।


# 🟢 M2 — Video Processing & FFmpeg/OpenCV

M1-এ আমরা Python pipeline foundation তৈরি করেছি। এখন **M2-তে actual video নিয়ে কাজ করব**।

M2-এর শেষে তুমি একটি video থেকে automatically বের করতে পারবে:

```text
video.mp4
   │
   ├── Duration
   ├── FPS
   ├── Width
   ├── Height
   ├── Frame Count
   ├── Audio Information
   │
   └── Frames
          ├── frame_00001.jpg
          ├── frame_00002.jpg
          └── ...
```

এটাই পরে **Whisper + Vision Model + Scene Planner**-এর input হবে।

---

# M2 Roadmap

```text
M2.1  Video Fundamentals
M2.2  FFmpeg Installation
M2.3  FFmpeg Basic Commands
M2.4  Video Metadata
M2.5  Audio Extraction
M2.6  OpenCV Basics
M2.7  Frame Extraction
M2.8  Timestamp-based Sampling
M2.9  Keyframe / Scene Sampling
M2.10 Complete Video Processing Pipeline
```

---

# M2.1 — Video কীভাবে কাজ করে?

একটি video আসলে অনেকগুলো image/frame-এর sequence।

ধরো:

```text
Frame 1
   ↓
Frame 2
   ↓
Frame 3
   ↓
Frame 4
   ↓
...
```

যদি video:

```text
FPS = 30
```

তাহলে প্রতি second-এ প্রায় 30টি frame থাকে।

10 second video:

```text
30 × 10 = 300 frames
```

---

## Important Terms

### 1. FPS

**Frames Per Second**

```text
30 FPS
```

মানে প্রতি second-এ 30 frame।

---

### 2. Resolution

যেমন:

```text
1920 × 1080
```

এখানে:

```text
Width  = 1920
Height = 1080
```

---

### 3. Duration

Video কত second।

```text
60 seconds
```

---

### 4. Frame Count

Total frame:

```text
1800 frames
```

---

### 5. Codec

Video compress/decode করার technology।

Common:

```text
H.264
H.265 / HEVC
AV1
VP9
```

---

### 6. Container

Video file-এর wrapper।

যেমন:

```text
.mp4
.mkv
.mov
.avi
```

একটা `.mp4` file-এর ভিতরে থাকতে পারে:

```text
Video
Audio
Subtitle
Metadata
```

---

# M2.2 — FFmpeg Install

Ubuntu:

```bash
sudo apt update
sudo apt install ffmpeg
```

Check:

```bash
ffmpeg -version
```

আর:

```bash
ffprobe -version
```

`ffmpeg` দিয়ে video manipulate করব।

`ffprobe` দিয়ে video সম্পর্কে information বের করব।

---

# M2.3 — FFmpeg Basic Commands

ধরো:

```text
videos/video.mp4
```

## Video information

```bash
ffprobe videos/video.mp4
```

আর cleaner output:

```bash
ffprobe -v error \
-show_entries format=duration \
-of default=noprint_wrappers=1 \
videos/video.mp4
```

Output:

```text
duration=60.123456
```

---

# Video থেকে audio বের করা

```bash
ffmpeg -i videos/video.mp4 audio.wav
```

আর Whisper-এর জন্য ভালো format:

```bash
ffmpeg -i videos/video.mp4 \
-ac 1 \
-ar 16000 \
audio.wav
```

এখানে:

```text
-ac 1
```

মানে mono audio।

```text
-ar 16000
```

মানে sample rate 16 kHz।

---

# Video থেকে প্রথম 10 seconds

```bash
ffmpeg -i videos/video.mp4 \
-t 10 \
videos/short.mp4
```

---

# Video resize

```bash
ffmpeg -i videos/video.mp4 \
-vf scale=1280:720 \
videos/resized.mp4
```

---

# M2.4 — Python দিয়ে Video Metadata

এখন Python ব্যবহার করব।

Install:

```bash
pip install opencv-python
```

Create:

```text
scripts/video_info.py
```

Code:

```python
import cv2
from pathlib import Path


VIDEO_PATH = Path("videos/video.mp4")


def get_video_info(video_path):

    if not video_path.exists():
        raise FileNotFoundError(
            f"Video not found: {video_path}"
        )

    cap = cv2.VideoCapture(str(video_path))

    if not cap.isOpened():
        raise RuntimeError(
            "Could not open video"
        )

    fps = cap.get(cv2.CAP_PROP_FPS)

    frame_count = int(
        cap.get(cv2.CAP_PROP_FRAME_COUNT)
    )

    width = int(
        cap.get(cv2.CAP_PROP_FRAME_WIDTH)
    )

    height = int(
        cap.get(cv2.CAP_PROP_FRAME_HEIGHT)
    )

    duration = frame_count / fps

    cap.release()

    return {
        "fps": fps,
        "frame_count": frame_count,
        "width": width,
        "height": height,
        "duration": duration
    }


if __name__ == "__main__":

    info = get_video_info(VIDEO_PATH)

    print(f"FPS: {info['fps']}")
    print(f"Frames: {info['frame_count']}")
    print(f"Resolution: {info['width']}x{info['height']}")
    print(f"Duration: {info['duration']:.2f} seconds")
```

Run:

```bash
python scripts/video_info.py
```

Example output:

```text
FPS: 30.0
Frames: 1800
Resolution: 1920x1080
Duration: 60.00 seconds
```

---

# 🧠 Important Formula

আমরা এখানে ব্যবহার করেছি:

```text
Duration = Frame Count / FPS
```

যেমন:

```text
Frame Count = 1800
FPS = 30

Duration = 1800 / 30
         = 60 seconds
```

---

# M2.5 — Audio Extraction

আমাদের next milestone হবে Whisper।

Whisper video-এর visual দেখে না।

Whisper মূলত:

```text
Audio
 ↓
Speech
 ↓
Text
```

তাই video থেকে audio আলাদা করতে হবে।

Python থেকে FFmpeg চালানো যায়:

```python
import subprocess

command = [
    "ffmpeg",
    "-i",
    "videos/video.mp4",
    "-ac",
    "1",
    "-ar",
    "16000",
    "audio.wav"
]

subprocess.run(command, check=True)
```

এতে:

```text
video.mp4
   ↓
FFmpeg
   ↓
audio.wav
```

---

# M2.6 — OpenCV Basics

OpenCV দিয়ে video read করা:

```python
import cv2

cap = cv2.VideoCapture(
    "videos/video.mp4"
)
```

Frame read:

```python
success, frame = cap.read()
```

যদি:

```text
success = True
```

তাহলে frame পাওয়া গেছে।

---

# একটি frame save করা

```python
import cv2

cap = cv2.VideoCapture(
    "videos/video.mp4"
)

success, frame = cap.read()

if success:

    cv2.imwrite(
        "frames/test.jpg",
        frame
    )

cap.release()
```

Result:

```text
frames/
└── test.jpg
```

---

# M2.7 — সব Frames Extract করা

এটা technically possible:

```python
while True:

    success, frame = cap.read()

    if not success:
        break

    cv2.imwrite(...)
```

কিন্তু educational AI-এর জন্য **সব frame save করা সাধারণত দরকার নেই**।

ধরো:

```text
Video = 10 minutes
FPS = 30
```

Total:

```text
10 × 60 × 30
= 18,000 frames
```

18,000 image store করা unnecessarily expensive হতে পারে।

তাই আমরা **sampling** করব।

---

# M2.8 — প্রতি 2 Second-এ একটি Frame

আমাদের project-এর জন্য খুব useful।

```text
Video:

0 sec  → Frame
2 sec  → Frame
4 sec  → Frame
6 sec  → Frame
8 sec  → Frame
...
```

Code:

```python
import cv2
from pathlib import Path


VIDEO_PATH = "videos/video.mp4"
OUTPUT_DIR = Path("frames/video")
INTERVAL = 2.0


def extract_frames(
    video_path,
    output_dir,
    interval
):

    output_dir.mkdir(
        parents=True,
        exist_ok=True
    )

    cap = cv2.VideoCapture(video_path)

    if not cap.isOpened():
        raise RuntimeError(
            "Could not open video"
        )

    fps = cap.get(
        cv2.CAP_PROP_FPS
    )

    frame_count = int(
        cap.get(
            cv2.CAP_PROP_FRAME_COUNT
        )
    )

    duration = frame_count / fps

    current_time = 0.0
    frame_id = 1

    while current_time < duration:

        cap.set(
            cv2.CAP_PROP_POS_MSEC,
            current_time * 1000
        )

        success, frame = cap.read()

        if not success:
            break

        output_file = (
            output_dir /
            f"frame_{frame_id:05d}.jpg"
        )

        cv2.imwrite(
            str(output_file),
            frame
        )

        print(
            f"Saved {output_file} "
            f"at {current_time:.2f}s"
        )

        frame_id += 1
        current_time += interval

    cap.release()


if __name__ == "__main__":

    extract_frames(
        VIDEO_PATH,
        OUTPUT_DIR,
        INTERVAL
    )
```

Run:

```bash
python scripts/extract_frames.py
```

Result:

```text
frames/
└── video/
    ├── frame_00001.jpg
    ├── frame_00002.jpg
    ├── frame_00003.jpg
    ├── frame_00004.jpg
    └── ...
```

---

# M2.9 — Timestamp কেন এত Important?

এটা তোমার entire project-এর একটা core concept।

ধরো:

```text
Video
0 ─────────────────────────────── 60 sec
```

Whisper বলল:

```text
0–5 sec:
"Plants need sunlight."

5–10 sec:
"Water is absorbed through roots."
```

Frame extraction:

```text
0 sec → frame_001
2 sec → frame_002
4 sec → frame_003

6 sec → frame_004
8 sec → frame_005
```

তাহলে mapping:

```text
Scene 1
0–5 sec
   ↓
frame_001
frame_002
frame_003

Scene 2
5–10 sec
   ↓
frame_004
frame_005
```

এটাই পরে:

```text
Whisper
   +
Vision
   +
LLM
```

combine করতে সাহায্য করবে।

---

# M2.10 — Complete M2 Pipeline

এখন আমরা সব combine করব।

```text
                    video.mp4
                        │
           ┌────────────┴────────────┐
           ↓                         ↓
       FFmpeg                    OpenCV
           ↓                         ↓
       Audio.wav                  Frames
           │                         │
           ↓                         ↓
       Whisper                  Vision Model
           │                         │
           └────────────┬────────────┘
                        ↓
                  Scene Planner
```

M2-এর actual output:

```text
educational_video_ai/
│
├── videos/
│   └── video.mp4
│
├── frames/
│   └── video/
│       ├── frame_00001.jpg
│       ├── frame_00002.jpg
│       └── ...
│
├── transcripts/
│
├── dataset/
│
└── scripts/
    ├── main.py
    ├── video_info.py
    └── extract_frames.py
```

---

# 🧪 M2 Practice Project

এখন তুমি নিজে একটি **Video Analyzer** বানাবে।

Input:

```bash
python scripts/analyze_video.py \
    --video videos/video.mp4
```

Program output করবে:

```text
================================
VIDEO INFORMATION
================================

File: video.mp4
Format: MP4
FPS: 30
Resolution: 1920x1080
Frames: 1800
Duration: 60 seconds

Audio: Available

================================
FRAME EXTRACTION
================================

Sampling interval: 2 seconds

Frames extracted: 30

================================
STATUS
================================

Video analysis completed!
```

এবং:

```text
frames/video/
```

এর মধ্যে 30টি frame থাকবে।

---

# 🎯 M2 Completion Checklist

M2 complete বলার আগে এগুলো করতে পারো কিনা দেখো:

* [ ] FPS বুঝি
* [ ] Resolution বুঝি
* [ ] Frame count বুঝি
* [ ] Duration calculate করতে পারি
* [ ] Codec ও container-এর difference বুঝি
* [ ] FFmpeg install করতে পারি
* [ ] FFprobe দিয়ে metadata দেখতে পারি
* [ ] Video থেকে audio extract করতে পারি
* [ ] OpenCV দিয়ে video read করতে পারি
* [ ] Frame save করতে পারি
* [ ] প্রতি N second-এ frame extract করতে পারি
* [ ] Frame-এর timestamp track করতে পারি
* [ ] Video → Audio + Frames pipeline বুঝি

## ⭐ M2-এর সবচেয়ে গুরুত্বপূর্ণ output

শেষে তোমার কাছে থাকবে:

```text
video.mp4
   │
   ├──────────────→ audio.wav
   │
   └──────────────→ timestamped frames
```

**এটাই M3-এর foundation।**

### পরের Milestone: **M3 — JSON/JSONL Dataset Engineering**

সেখানে আমরা এই raw data-গুলোকে proper AI training dataset-এ convert করব:

```text
Video
 ↓
Metadata
 ↓
Frames
 ↓
Transcript
 ↓
Scene
 ↓
Educational Dataset
```

এবং তখন থেকে project-এর **actual dataset তৈরির কাজ** শুরু হবে।


---
# 🟢 M3 — JSON/JSONL Dataset Engineering

M1-এ আমরা Python pipeline foundation করেছি।
M2-তে video → metadata + audio + frames করেছি।

এখন M3-এর মূল কাজ:

> **Raw video data-কে AI training-এর জন্য clean, structured, validated dataset-এ convert করা।**

---

# 🎯 M3 শেষে আমরা কী পাব?

```text
video.mp4
   │
   ├── metadata
   ├── frames
   └── transcript
          ↓
     Scene Dataset
          ↓
   train.jsonl
   validation.jsonl
   test.jsonl
```

Final structure:

```text
dataset/
├── metadata/
│   └── video_001.json
│
├── scenes/
│   └── video_001_scenes.json
│
├── train.jsonl
├── validation.jsonl
└── test.jsonl
```

---

# M3 Roadmap

```text
M3.1  Dataset Architecture
M3.2  JSON Schema Design
M3.3  Metadata Creation
M3.4  Transcript Dataset
M3.5  Scene Dataset
M3.6  JSONL Dataset
M3.7  Dataset Validation
M3.8  Train/Validation/Test Split
M3.9  Dataset Statistics
M3.10 Complete Dataset Pipeline
```

---

# M3.1 — Dataset Architecture

আমাদের AI future-এ দুই ধরনের কাজ করবে:

### Task A — Existing video বুঝবে

```text
Video
 ↓
Whisper
 ↓
Vision
 ↓
Scene Dataset
```

### Task B — নতুন educational video তৈরি করবে

```text
Topic
 ↓
LLM
 ↓
Scene Dataset
 ↓
Visual Generation
```

তাই dataset-এর structure ভালোভাবে design করা খুব গুরুত্বপূর্ণ।

---

# M3.2 — Dataset Schema

একটা educational video-এর complete record এমন হতে পারে:

```json
{
    "video_id": "video_001",
    "topic": "Photosynthesis",
    "subject": "Biology",
    "difficulty": "beginner",
    "language": "en",
    "duration": 60,
    "learning_objectives": [
        "Understand photosynthesis",
        "Identify required inputs",
        "Understand the outputs"
    ],
    "scenes": []
}
```

এখানে:

```text
video_id
```

unique identifier।

```text
topic
```

ভিডিওটি কী নিয়ে।

```text
subject
```

Biology / Physics / Mathematics / Computer Science ইত্যাদি।

```text
difficulty
```

যেমন:

```text
beginner
intermediate
advanced
```

---

# M3.3 — Video Metadata

M2-তে আমরা video information বের করেছি।

এখন সেটা JSON-এ save করব।

Create:

```text
scripts/create_metadata.py
```

```python
import cv2
import json
from pathlib import Path


def get_video_metadata(video_path):

    video_path = Path(video_path)

    if not video_path.exists():
        raise FileNotFoundError(
            f"Video not found: {video_path}"
        )

    cap = cv2.VideoCapture(str(video_path))

    if not cap.isOpened():
        raise RuntimeError(
            "Could not open video"
        )

    fps = cap.get(cv2.CAP_PROP_FPS)

    frame_count = int(
        cap.get(cv2.CAP_PROP_FRAME_COUNT)
    )

    width = int(
        cap.get(cv2.CAP_PROP_FRAME_WIDTH)
    )

    height = int(
        cap.get(cv2.CAP_PROP_FRAME_HEIGHT)
    )

    duration = frame_count / fps

    cap.release()

    return {
        "video_id": video_path.stem,
        "filename": video_path.name,
        "format": video_path.suffix.lower(),
        "fps": fps,
        "frame_count": frame_count,
        "width": width,
        "height": height,
        "duration": duration
    }


def save_metadata(metadata):

    output_dir = Path("dataset/metadata")

    output_dir.mkdir(
        parents=True,
        exist_ok=True
    )

    output_file = (
        output_dir /
        f"{metadata['video_id']}.json"
    )

    with open(output_file, "w") as file:

        json.dump(
            metadata,
            file,
            indent=4
        )

    print(
        f"Saved: {output_file}"
    )


if __name__ == "__main__":

    video = "videos/video.mp4"

    metadata = get_video_metadata(video)

    save_metadata(metadata)
```

Run:

```bash
python scripts/create_metadata.py
```

Result:

```text
dataset/
└── metadata/
    └── video.json
```

---

# M3.4 — Transcript Dataset

M2-তে আমরা audio extraction করেছি।

পরের stage-এ Whisper output হবে:

```json
{
    "video_id": "video_001",
    "language": "en",
    "segments": [
        {
            "start": 0.0,
            "end": 4.5,
            "text": "Plants use sunlight to make food."
        },
        {
            "start": 4.5,
            "end": 9.0,
            "text": "This process is called photosynthesis."
        }
    ]
}
```

এখানে সবচেয়ে গুরুত্বপূর্ণ হচ্ছে:

```text
start
end
text
```

কারণ পরে frame-এর সাথে এগুলো match করব।

---

# M3.5 — Scene Dataset

এখন transcript segment থেকে scene তৈরি করব।

ধরো:

```text
0–5 sec
Plants use sunlight to make food.

5–10 sec
This process is called photosynthesis.
```

তাহলে:

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Plants use sunlight to make food."
}
```

এখন এটাতে পরে Vision output যোগ হবে:

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Plants use sunlight to make food.",
    "frames": [
        {
            "timestamp": 0,
            "path": "frames/video/frame_00001.jpg"
        },
        {
            "timestamp": 2,
            "path": "frames/video/frame_00002.jpg"
        },
        {
            "timestamp": 4,
            "path": "frames/video/frame_00003.jpg"
        }
    ],
    "visual_description": null
}
```

`visual_description` এখন `null`।

M4-এ Vision Model এটা fill করবে।

---

# M3.6 — JSONL

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

Training-এর জন্য আমরা সাধারণত এমন format ব্যবহার করব:

```text
train.jsonl
```

প্রতিটি line:

```json
{"video_id":"video_001","scene_id":1,...}
{"video_id":"video_001","scene_id":2,...}
{"video_id":"video_002","scene_id":1,...}
```

অর্থাৎ:

> **একটি line = একটি training example**

---

# কেন JSONL?

ধরো 100,000 scene আছে।

একটা বিশাল JSON file:

```text
dataset.json
```

ব্যবহার করা inconvenient হতে পারে।

JSONL:

```text
train.jsonl
```

এ সহজে line-by-line process করা যায়।

```python
with open("dataset/train.jsonl") as file:

    for line in file:

        item = json.loads(line)

        print(item)
```

---

# M3.7 — Dataset Validation

AI dataset-এ invalid data থাকলে training নষ্ট হতে পারে।

ধরো:

```json
{
    "scene_id": 1,
    "start": 10,
    "end": 5
}
```

এটা invalid।

কারণ:

```text
start > end
```

---

## আমরা validation rules বানাব

### Rule 1

`scene_id` থাকতে হবে।

### Rule 2

`start` থাকতে হবে।

### Rule 3

`end` থাকতে হবে।

### Rule 4

```text
end > start
```

### Rule 5

`narration` empty হওয়া যাবে না।

### Rule 6

duration positive হতে হবে।

---

# Basic Validator

```python
def validate_scene(scene):

    required_fields = [
        "scene_id",
        "start",
        "end",
        "narration"
    ]

    for field in required_fields:

        if field not in scene:
            return False, f"Missing: {field}"

    if scene["end"] <= scene["start"]:
        return False, "Invalid timestamps"

    if not scene["narration"].strip():
        return False, "Empty narration"

    return True, "Valid"
```

Test:

```python
scene = {
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Plants use sunlight."
}

valid, message = validate_scene(scene)

print(valid)
print(message)
```

Output:

```text
True
Valid
```

---

# M3.8 — Pydantic Validation

Project বড় হলে manual validation-এর বদলে **Pydantic** ব্যবহার করব।

Install:

```bash
pip install pydantic
```

Model:

```python
from pydantic import BaseModel, Field


class Scene(BaseModel):

    scene_id: int

    start: float = Field(
        ge=0
    )

    end: float

    narration: str

    visual_description: str | None = None
```

এখন:

```python
scene = Scene(
    scene_id=1,
    start=0,
    end=5,
    narration="Plants use sunlight."
)
```

Pydantic automatically structure validate করবে।

---

# M3.9 — Train / Validation / Test

Machine learning dataset সাধারণত তিন ভাগে ভাগ করব।

```text
Total Dataset
      │
      ├── Train
      ├── Validation
      └── Test
```

Typical split:

```text
Train       80%
Validation  10%
Test        10%
```

Example:

```text
1000 scenes

800 → train
100 → validation
100 → test
```

---

# খুব গুরুত্বপূর্ণ বিষয়

Randomly scene split করলে একটা problem হতে পারে।

ধরো:

```text
video_001

scene 1
scene 2
scene 3
scene 4
```

যদি:

```text
scene 1 → train
scene 2 → test
```

হয়, তাহলে একই video-এর information train ও test দু জায়গায় চলে যাবে।

এটা **data leakage** তৈরি করতে পারে।

### Better approach:

**Video-level split**

```text
video_001 → train
video_002 → train
video_003 → validation
video_004 → test
```

তার scenes একই split-এ থাকবে।

এটা তোমার project-এর জন্য খুব গুরুত্বপূর্ণ।

---

# M3.10 — Dataset Statistics

Dataset তৈরি হওয়ার পর statistics বের করব।

যেমন:

```text
================================
DATASET STATISTICS
================================

Total Videos:       100
Total Scenes:       4,500

Subjects:
Biology:            1,200
Physics:            900
Mathematics:        1,100
Computer Science:   1,300

Difficulty:
Beginner:           2,000
Intermediate:       1,700
Advanced:           800

Average Scene:
Duration:           6.2 sec
```

এগুলো dataset quality বুঝতে সাহায্য করবে।

---

# 🧠 Final Dataset Schema

M3 শেষে আমরা যে structure target করব:

```json
{
    "video_id": "video_001",

    "topic": "Photosynthesis",

    "subject": "Biology",

    "difficulty": "beginner",

    "language": "en",

    "duration": 60,

    "learning_objectives": [
        "Understand photosynthesis",
        "Identify inputs",
        "Identify outputs"
    ],

    "scenes": [

        {
            "scene_id": 1,

            "start": 0.0,

            "end": 5.0,

            "narration":
                "Plants use sunlight to make food.",

            "frames": [

                {
                    "timestamp": 0.0,
                    "path":
                        "frames/video_001/frame_00001.jpg"
                },

                {
                    "timestamp": 2.0,
                    "path":
                        "frames/video_001/frame_00002.jpg"
                }
            ],

            "visual_description": null,

            "on_screen_text": null,

            "animation_instruction": null,

            "scene_type": null
        }
    ]
}
```

এখন খেয়াল করো:

```text
visual_description = null
animation_instruction = null
scene_type = null
```

কারণ এগুলো আমরা **M4 + M5-এ AI দিয়ে generate করব।**

---

# 🔥 M3 Complete Pipeline

সবকিছু একসাথে:

```text
                    VIDEO
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
      Metadata      Audio       Frames
          │           ↓           │
          │        Whisper        │
          │           ↓           │
          │      Transcript       │
          │           │           │
          └───────────┼───────────┘
                      ↓
                 Scene Builder
                      ↓
               Scene Validation
                      ↓
                JSON Dataset
                      ↓
                  JSONL
                 /  |  \
                /   |   \
             Train Val  Test
```

---

# 📁 M3 Final Folder Structure

```text
educational_video_ai/
│
├── videos/
│   └── video_001.mp4
│
├── frames/
│   └── video_001/
│       ├── frame_00001.jpg
│       ├── frame_00002.jpg
│       └── ...
│
├── transcripts/
│   └── video_001_transcript.json
│
├── dataset/
│   │
│   ├── metadata/
│   │   └── video_001.json
│   │
│   ├── scenes/
│   │   └── video_001_scenes.json
│   │
│   ├── train.jsonl
│   ├── validation.jsonl
│   └── test.jsonl
│
└── scripts/
    ├── main.py
    ├── video_info.py
    ├── extract_frames.py
    ├── create_metadata.py
    ├── create_scenes.py
    ├── validate_dataset.py
    └── split_dataset.py
```

---

# 🧪 M3 Practice Project

এখন তোমার actual assignment:

### Input

```text
videos/video_001.mp4
```

### Pipeline

```text
Video
 ↓
Metadata
 ↓
Transcript
 ↓
Scene JSON
 ↓
Validation
 ↓
train/val/test JSONL
```

### Expected output

```text
dataset/
├── metadata/
├── scenes/
├── train.jsonl
├── validation.jsonl
└── test.jsonl
```

---

# ✅ M3 Completion Checklist

নিজে করতে পারলে M3 complete:

* [ ] JSON structure design করতে পারি
* [ ] JSON read/write করতে পারি
* [ ] JSONL বুঝি
* [ ] JSONL তৈরি করতে পারি
* [ ] Video metadata dataset-এ save করতে পারি
* [ ] Transcript structure বুঝি
* [ ] Transcript থেকে scene তৈরি করতে পারি
* [ ] Timestamp maintain করতে পারি
* [ ] Dataset validation করতে পারি
* [ ] Pydantic দিয়ে validation করতে পারি
* [ ] Train/validation/test বুঝি
* [ ] Video-level split কেন দরকার বুঝি
* [ ] Dataset statistics বের করতে পারি

---

## ⭐ M3-এর সবচেয়ে গুরুত্বপূর্ণ শিক্ষা

এখন পর্যন্ত:

```text
M1
Python Pipeline
       ↓
M2
Video Processing
       ↓
M3
Structured Dataset
```

এরপর সবচেয়ে exciting অংশ শুরু হবে:

# 🔵 M4 — Whisper + Speech Understanding

সেখানে আমরা **actual video → speech → timestamped transcript** pipeline তৈরি করব এবং Whisper/faster-whisper দিয়ে educational content-এর narration automatically extract করব।

তারপর:

```text
Video
 ↓
Whisper
 ↓
Timestamped Transcript
 ↓
Scene Alignment
```

এটাই পরের ধাপে **Vision Model-এর সাথে combine** হবে।


---
# 🟣 M4 — Whisper + Speech Understanding

এখন আমরা project-এর **actual AI understanding pipeline** শুরু করছি।

M1 → Python foundation
M2 → Video processing
M3 → Dataset engineering

এখন:

```text
🎬 Video
   ↓
🎵 Audio
   ↓
🧠 Whisper
   ↓
📝 Transcript
   ↓
⏱️ Timestamp
   ↓
🎞️ Scene-aligned transcript
```

M4 শেষ হলে তোমার system একটি educational video থেকে **কে কী বলছে, কখন বলছে, কতক্ষণ বলছে**—এসব automatically বের করতে পারবে।

---

# 🎯 M4 Learning Roadmap

```text id="m4road"
M4.1  Speech-to-Text Fundamentals
M4.2  Whisper Architecture
M4.3  faster-whisper Installation
M4.4  Video → Speech Transcription
M4.5  Language Detection
M4.6  Segment Timestamps
M4.7  Word Timestamps
M4.8  Transcript Cleaning
M4.9  Transcript → Scene Segmentation
M4.10 Transcript Validation
M4.11 Complete Whisper Pipeline
```

---

# M4.1 — Speech-to-Text কী?

Speech-to-Text বা **STT** হচ্ছে:

```text
Human Speech
     ↓
AI Speech Recognition
     ↓
Text
```

উদাহরণ:

```text
Audio:
"Binary search works on a sorted array."

             ↓

Transcript:
"Binary search works on a sorted array."
```

আমাদের project-এ এটা দরকার কারণ user যখন existing educational video upload করবে, আমরা narration বুঝতে চাই।

---

# M4.2 — Whisper কী?

**Whisper** হলো speech recognition model।

Conceptually:

```text
Video
 ↓
Audio
 ↓
Whisper
 ↓
Language Detection
 ↓
Speech Recognition
 ↓
Timestamped Transcript
```

Whisper শুধু text দেয় না; আমরা timestamps-ও নিতে পারি।

যেমন:

```json id="s8cvzi"
{
    "start": 0.0,
    "end": 4.2,
    "text": "Binary search works on sorted arrays."
}
```

এটা অত্যন্ত গুরুত্বপূর্ণ।

কারণ পরে আমরা জানতে চাই:

> এই narration-এর সময় screen-এ কী দেখানো হচ্ছিল?

---

# M4.3 — faster-whisper

Original Whisper-এর তুলনায় project pipeline-এর জন্য **faster-whisper** ব্যবহার করা practical।

Install:

```bash id="q8j5j1"
pip install faster-whisper
```

FFmpeg নিশ্চিত করো:

```bash id="5ov2cf"
ffmpeg -version
```

---

# Model Size

Whisper-এর বিভিন্ন model size আছে:

```text id="4q6qvh"
tiny
base
small
medium
large
```

General idea:

| Model  | Speed     | Accuracy  | Resource  |
| ------ | --------- | --------- | --------- |
| tiny   | Very fast | Lower     | Very low  |
| base   | Fast      | Good      | Low       |
| small  | Medium    | Better    | Medium    |
| medium | Slow      | High      | High      |
| large  | Very slow | Very high | Very high |

শুরুতে:

```text id="t6c2zv"
base
```

দিয়ে কাজ করো।

কারণ এখন আমাদের লক্ষ্য **pipeline শেখা**, maximum accuracy না।

---

# M4.4 — Video → Transcript

একটা গুরুত্বপূর্ণ বিষয়:

তোমাকে manually audio extract করে Whisper-কে দিতে হবে না।

faster-whisper video file directly handle করতে পারে।

ধরো:

```text id="b8p5zi"
videos/video_001.mp4
```

Create:

```text id="xk0h2f"
scripts/transcribe.py
```

Code:

```python
from faster_whisper import WhisperModel
from pathlib import Path
import json


VIDEO_PATH = "videos/video_001.mp4"
OUTPUT_DIR = Path("transcripts")

MODEL_SIZE = "base"


def transcribe_video(video_path):

    print("Loading Whisper model...")

    model = WhisperModel(
        MODEL_SIZE,
        device="cpu",
        compute_type="int8"
    )

    print("Transcribing video...")

    segments, info = model.transcribe(
        video_path,
        beam_size=5,
        word_timestamps=True
    )

    transcript_segments = []

    for segment in segments:

        words = []

        if segment.words:

            for word in segment.words:

                words.append({
                    "start": word.start,
                    "end": word.end,
                    "word": word.word
                })

        transcript_segments.append({

            "segment_id": len(
                transcript_segments
            ),

            "start": segment.start,

            "end": segment.end,

            "duration":
                segment.end - segment.start,

            "text": segment.text.strip(),

            "words": words
        })

    return {
        "language": info.language,

        "language_probability":
            info.language_probability,

        "segments":
            transcript_segments
    }


def save_transcript(video_path, data):

    OUTPUT_DIR.mkdir(
        parents=True,
        exist_ok=True
    )

    video_name = Path(
        video_path
    ).stem

    output_file = (
        OUTPUT_DIR /
        f"{video_name}_transcript.json"
    )

    with open(
        output_file,
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            data,
            file,
            indent=4,
            ensure_ascii=False
        )

    print(
        f"Transcript saved: {output_file}"
    )


def main():

    result = transcribe_video(
        VIDEO_PATH
    )

    save_transcript(
        VIDEO_PATH,
        result
    )


if __name__ == "__main__":
    main()
```

Run:

```bash id="f6kt5j"
python scripts/transcribe.py
```

---

# M4.5 — Language Detection

Whisper automatically language detect করতে পারে।

Output:

```json id="7z8q6v"
{
    "language": "en",
    "language_probability": 0.98
}
```

যদি Bangla video হয়:

```json id="k86vhr"
{
    "language": "bn",
    "language_probability": 0.97
}
```

আমাদের future application হতে পারে multilingual:

```text id="k2wq9b"
English
Bangla
Hindi
Arabic
...
```

তাই language metadata রাখা গুরুত্বপূর্ণ।

---

# M4.6 — Segment Timestamps

এটাই M4-এর সবচেয়ে গুরুত্বপূর্ণ concept।

ধরো video:

```text id="i7x0b0"
0 ───────────────────────────── 60 sec
```

Whisper output:

```text id="ddt2o9"
0.0 ── 4.5
"Plants use sunlight to make food."

4.5 ── 8.7
"This process is called photosynthesis."

8.7 ── 14.2
"Water enters the plant through the roots."
```

আমরা JSON-এ রাখব:

```json id="7y3a3e"
{
    "segment_id": 0,
    "start": 0.0,
    "end": 4.5,
    "duration": 4.5,
    "text": "Plants use sunlight to make food."
}
```

---

# কেন timestamp এত গুরুত্বপূর্ণ?

কারণ আমাদের final dataset হবে:

```text id="3ezb2e"
Narration
+
Visual
+
Time
```

যেমন:

```json id="3ol0x8"
{
    "start": 0,
    "end": 5,
    "narration": "Plants use sunlight to make food.",
    "visual_description": "A green plant receives sunlight."
}
```

এখানে narration এবং visual একই সময়ের।

---

# M4.7 — Word Timestamps

Segment timestamp:

```text id="d3y6mo"
0.0 ───────── 4.5 sec
"Binary search uses a sorted array."
```

Word timestamps আরও precise:

```json id="w7lh7k"
[
    {
        "word": "Binary",
        "start": 0.0,
        "end": 0.5
    },
    {
        "word": "search",
        "start": 0.5,
        "end": 1.1
    },
    {
        "word": "uses",
        "start": 1.1,
        "end": 1.5
    }
]
```

এগুলো পরে subtitle synchronization-এর জন্যও useful হবে।

---

# M4.8 — Transcript Cleaning

Whisper output সবসময় perfect হবে না।

ধরো:

```text
"  Binary   search works... "
```

আমরা clean করব:

```text
"Binary search works..."
```

Basic function:

```python id="f0um1c"
def clean_text(text):

    text = text.strip()

    text = " ".join(
        text.split()
    )

    return text
```

Use:

```python id="9psj7g"
text = clean_text(
    segment.text
)
```

---

# Empty Transcript Handling

কখনো Whisper empty segment দিতে পারে।

```python id="ylu3gj"
if not text:
    continue
```

---

# M4.9 — Transcript → Scene Segmentation

এখন একটা গুরুত্বপূর্ণ distinction বুঝো।

**Whisper segment = scene নয়।**

ধরো Whisper:

```text id="n49i4y"
0–2 sec: "Photosynthesis"
2–4 sec: "is the process"
4–7 sec: "by which plants make food."
```

এগুলো তিনটি speech segment।

কিন্তু visual scene হতে পারে:

```text id="f7l72p"
0–7 sec
One complete scene about photosynthesis.
```

অর্থাৎ:

```text id="v7lyoc"
Whisper Segment
       ≠
Visual Scene
```

আমরা এখন transcript থেকে **candidate scenes** তৈরি করব।

---

# Simple Scene Builder

Create:

```text id="w0f1cm"
scripts/build_scenes.py
```

```python
import json
from pathlib import Path


INPUT_FILE = (
    "transcripts/"
    "video_001_transcript.json"
)

OUTPUT_DIR = Path(
    "dataset/scenes"
)


MAX_SCENE_DURATION = 8.0


def load_transcript():

    with open(
        INPUT_FILE,
        "r",
        encoding="utf-8"
    ) as file:

        return json.load(file)


def build_scenes(data):

    segments = data["segments"]

    scenes = []

    current_scene = None

    for segment in segments:

        start = segment["start"]
        end = segment["end"]
        text = segment["text"].strip()

        if not text:
            continue

        if current_scene is None:

            current_scene = {
                "scene_id": len(scenes),
                "start": start,
                "end": end,
                "narration": text
            }

            continue

        current_duration = (
            end - current_scene["start"]
        )

        if current_duration <= MAX_SCENE_DURATION:

            current_scene["end"] = end

            current_scene["narration"] += (
                " " + text
            )

        else:

            scenes.append(
                current_scene
            )

            current_scene = {
                "scene_id": len(scenes),
                "start": start,
                "end": end,
                "narration": text
            }

    if current_scene:

        scenes.append(
            current_scene
        )

    return scenes


def save_scenes(scenes):

    OUTPUT_DIR.mkdir(
        parents=True,
        exist_ok=True
    )

    output_file = (
        OUTPUT_DIR /
        "video_001_scenes.json"
    )

    with open(
        output_file,
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            scenes,
            file,
            indent=4,
            ensure_ascii=False
        )

    print(
        f"Saved: {output_file}"
    )


def main():

    data = load_transcript()

    scenes = build_scenes(data)

    save_scenes(scenes)

    print(
        f"Scenes created: {len(scenes)}"
    )


if __name__ == "__main__":
    main()
```

---

# Output

```json id="6x7guk"
[
    {
        "scene_id": 0,
        "start": 0.0,
        "end": 7.0,
        "narration":
            "Photosynthesis is the process by which plants make food."
    },

    {
        "scene_id": 1,
        "start": 7.0,
        "end": 14.0,
        "narration":
            "Plants need sunlight, water, and carbon dioxide."
    }
]
```

---

# ⚠️ কিন্তু এটা Final Scene Detection নয়

এটা খুব important।

এই stage-এ:

```text id="7b5n8v"
Transcript
 ↓
Time-based candidate scenes
```

করছি।

পরে M5/M6-এ আমরা ব্যবহার করব:

```text id="80c1qz"
Transcript
+
Frames
+
Vision
+
LLM
 ↓
True Educational Scene
```

তখন scene boundary আরও intelligent হবে।

---

# M4.10 — Transcript Validation

আমরা transcript validate করব।

Rules:

### Rule 1

```text
start >= 0
```

### Rule 2

```text
end > start
```

### Rule 3

Text empty নয়।

### Rule 4

Segments ideally chronological:

```text
segment 1 start
<
segment 2 start
<
segment 3 start
```

---

## Validator

```python id="g4c15p"
def validate_segment(segment):

    if segment["start"] < 0:
        return False

    if segment["end"] <= segment["start"]:
        return False

    if not segment["text"].strip():
        return False

    return True
```

---

# M4.11 — Complete M4 Pipeline

এখন পুরো flow:

```text id="j0t6m4"
                    video.mp4
                        │
                        ▼
                   Audio Stream
                        │
                        ▼
                  faster-whisper
                        │
            ┌───────────┼───────────┐
            ↓           ↓           ↓
        Language     Segments      Words
            │           │           │
            └───────────┼───────────┘
                        ↓
                Transcript JSON
                        ↓
                 Text Cleaning
                        ↓
                Candidate Scenes
                        ↓
                 Scene Validation
```

---

# 📁 M4 Folder Structure

M4 শেষে project:

```text id="h9r9hv"
educational_video_ai/
│
├── videos/
│   └── video_001.mp4
│
├── frames/
│   └── video_001/
│       ├── frame_00001.jpg
│       ├── frame_00002.jpg
│       └── ...
│
├── transcripts/
│   └── video_001_transcript.json
│
├── dataset/
│   ├── metadata/
│   │   └── video_001.json
│   │
│   └── scenes/
│       └── video_001_scenes.json
│
└── scripts/
    ├── main.py
    ├── video_info.py
    ├── extract_frames.py
    ├── create_metadata.py
    ├── transcribe.py
    └── build_scenes.py
```

---

# 🧠 M4-এ যে Architecture বুঝতে হবে

এখন পর্যন্ত:

```text id="x7hjh6"
             VIDEO
                │
       ┌────────┴────────┐
       ↓                 ↓
    OpenCV            Whisper
       ↓                 ↓
     Frames          Transcript
       │                 │
       └────────┬────────┘
                ↓
          Scene Dataset
```

**এই দুই branch-ই আমাদের future AI-এর চোখ ও কান হবে।**

```text
Whisper = 👂 Ear
Vision  = 👁️ Eyes
LLM     = 🧠 Brain
Generator = 🎨 Hands
```

খুব সহজভাবে মনে রাখতে পারো:

```text id="4k7z7a"
👂 Whisper
   ↓
"What is being said?"

👁️ Vision
   ↓
"What is being shown?"

🧠 LLM
   ↓
"How should this be taught?"

🎨 Generator
   ↓
"Create the educational video."
```

---

# 🧪 M4 Practice Project

তোমার assignment:

### Input

```text
videos/video_001.mp4
```

### Run

```bash id="l4w8in"
python scripts/transcribe.py
```

তারপর:

```bash id="r8gqkn"
python scripts/build_scenes.py
```

### Expected:

```text
transcripts/
└── video_001_transcript.json
```

এবং:

```text
dataset/
└── scenes/
    └── video_001_scenes.json
```

---

# ⭐ M4 Completion Checklist

* [ ] Speech-to-Text বুঝি
* [ ] Whisper কী বুঝি
* [ ] faster-whisper install করতে পারি
* [ ] Video directly transcribe করতে পারি
* [ ] Language detect করতে পারি
* [ ] Segment timestamps বুঝি
* [ ] Word timestamps বুঝি
* [ ] Transcript JSON তৈরি করতে পারি
* [ ] Transcript clean করতে পারি
* [ ] Transcript থেকে candidate scenes তৈরি করতে পারি
* [ ] Timestamp validation করতে পারি
* [ ] Video → Whisper → Scene pipeline run করতে পারি

---

# 🎯 এখন Project কোথায়?

```text id="qpn5y0"
M1 ✅
Python Pipeline Foundation

M2 ✅
Video Processing

M3 ✅
Dataset Engineering

M4 ✅
Speech Understanding

        ↓

NEXT

M5 🔵
Computer Vision + Vision-Language Model
```

## 🔥 M5 হবে খুব গুরুত্বপূর্ণ

M4-তে AI **শুনতে** শিখেছে।

M5-তে AI **দেখতে** শিখবে:

```text id="y4mxv8"
video.mp4
   ↓
OpenCV
   ↓
Frames
   ↓
Vision Model
   ↓
"What is happening in this frame?"
   ↓
Visual Description
```

তারপর M4 + M5:

```text id="d5j8cj"
👂 Whisper
     +
👁️ Vision
     ↓
Scene Understanding
```

এবং সেখান থেকেই তোমার Educational Video AI-এর **real multimodal dataset** তৈরি হতে শুরু করবে।


----
# M5 — Computer Vision + Vision-Language Model (VLM)

M4-এ আমরা শিখেছি:

```text
Video
 ↓
Audio
 ↓
Whisper
 ↓
Transcript + Timestamp
```

এখন M5-এ আমরা **ভিডিওতে কী দেখা যাচ্ছে সেটা AI দিয়ে বুঝব**।

```text
Video
 ↓
Frames
 ↓
Computer Vision
 ↓
Vision Model
 ↓
"What is happening in this frame?"
 ↓
Visual Description
```

এটা তোমার Educational Video AI-এর জন্য খুব গুরুত্বপূর্ণ, কারণ পরে আমাদের system-কে বুঝতে হবে:

> **Narration কী বলছে + Screen-এ কী দেখাচ্ছে = Scene-এর আসল meaning**

---

# M5 Roadmap

আজ আমরা 8টি অংশে শিখব:

1. Computer Vision কী
2. Image কীভাবে computer বুঝে
3. Frame analysis
4. Object detection বনাম image classification
5. Vision-Language Model কী
6. Image → Text analysis
7. Video → Frame → VLM pipeline
8. আমাদের project-এর জন্য Visual Dataset তৈরি

---

# 1. Computer Vision কী?

Computer Vision হলো computer-কে image/video বুঝতে শেখানো।

মানুষ:

```text
👁️ Image দেখে
   ↓
🧠 Brain বুঝে
   ↓
"একজন teacher board-এ binary search বুঝাচ্ছে"
```

Computer:

```text
Image
 ↓
Pixels
 ↓
Vision Model
 ↓
Features
 ↓
Understanding
```

একটি image আসলে অনেকগুলো pixel-এর collection।

উদাহরণ:

```text
Image
640 × 480

↓
307,200 pixels
```

RGB image হলে প্রতিটি pixel:

```text
[R, G, B]
```

যেমন:

```text
[255, 0, 0] → Red
[0, 255, 0] → Green
[0, 0, 255] → Blue
```

---

# 2. OpenCV দিয়ে Image দেখা

Install:

```bash
pip install opencv-python
```

Test:

```python
import cv2

image = cv2.imread("frames/video_001/frame_00001.jpg")

print(image.shape)
```

Output হতে পারে:

```text
(720, 1280, 3)
```

মানে:

```text
Height = 720
Width  = 1280
Channels = 3
```

---

# 3. Frame হচ্ছে Image

আমাদের video:

```text
video.mp4
```

আসলে:

```text
Frame 1
Frame 2
Frame 3
Frame 4
...
Frame 1000
```

প্রতিটি frame একটি image।

তাই:

```text
Video
 ↓
Frames
 ↓
Images
 ↓
Vision Model
```

এটাই আমাদের M5-এর foundation।

---

# 4. Computer Vision-এর গুরুত্বপূর্ণ কাজ

Computer Vision-এ অনেক ধরনের task আছে।

### Image Classification

প্রশ্ন:

> ছবিতে কী আছে?

```text
Image
 ↓
Model
 ↓
"Cat"
```

---

### Object Detection

প্রশ্ন:

> কোথায় কী আছে?

```text
Image
 ↓
Model
 ↓
Person
Car
Book
Laptop
```

এবং bounding box পাওয়া যায়।

```text
┌─────────────────────┐
│                     │
│   ┌──────────┐      │
│   │  Person  │      │
│   └──────────┘      │
│                     │
└─────────────────────┘
```

---

### Image Segmentation

প্রশ্ন:

> কোন কোন pixel কোন object-এর?

উদাহরণ:

```text
Person → pixels
Car    → pixels
Road   → pixels
```

---

### Image Captioning

প্রশ্ন:

> ছবিটাকে sentence দিয়ে describe করো।

Output:

```text
"A teacher is explaining a diagram on a whiteboard."
```

---

### Visual Question Answering

Image:

```text
Teacher + Whiteboard
```

Question:

```text
"What is the teacher explaining?"
```

Answer:

```text
"The teacher is explaining photosynthesis."
```

---

# 5. আমাদের জন্য সবচেয়ে গুরুত্বপূর্ণ: Vision-Language Model

Educational Video AI-এর জন্য শুধু traditional Computer Vision যথেষ্ট নয়।

আমাদের দরকার:

# Vision-Language Model — VLM

VLM image + language একসাথে বুঝতে পারে।

Architecture:

```text
Image
  ↓
Vision Encoder
  ↓
Visual Features
  ↓
Language Model
  ↓
Text Understanding
```

তখন আমরা প্রশ্ন করতে পারি:

```text
Image:
[Teacher explaining binary search]

Question:
"What is happening in this image?"
```

Output:

```text
"A teacher is explaining binary search
using a diagram on a board."
```

---

# 6. কেন VLM আমাদের project-এ দরকার?

ধরো Whisper বললো:

```text
"Binary search repeatedly divides the search space in half."
```

কিন্তু frame-এ দেখা যাচ্ছে:

```text
Array:

[10] [20] [30] [40] [50] [60] [70]

                ↑
              MID
```

Whisper শুধু জানে:

```text
কি বলা হচ্ছে
```

VLM জানে:

```text
কি দেখা যাচ্ছে
```

দুটো combine করলে:

```text
Whisper
   +
VLM
   ↓
Complete Scene Understanding
```

---

# 7. Our Educational AI Architecture

M5-এর পরে architecture হবে:

```text
                    VIDEO
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
       AUDIO                    FRAMES
          ↓                       ↓
      Whisper                    VLM
          ↓                       ↓
     Transcript            Visual Description
          │                       │
          └───────────┬───────────┘
                      ↓
               Scene Understanding
                      ↓
                 Scene JSON
```

এটা আমাদের project-এর core architecture-এর একটি অংশ।

---

# 8. Frame Sampling

ধরো video:

```text
60 seconds
```

FPS:

```text
30
```

Total frames:

```text
60 × 30 = 1800 frames
```

প্রতিটি frame VLM-এ পাঠানো inefficient।

আমরা sampling করতে পারি:

```text
0 sec
2 sec
4 sec
6 sec
...
58 sec
```

অর্থাৎ:

```text
30 frames
```

instead of:

```text
1800 frames
```

এতে:

* processing কম
* GPU cost কম
* inference দ্রুত
* dataset ছোট

---

# 9. Frame Sampling Code

`extract_visual_frames.py`

```python
import cv2
from pathlib import Path


def extract_frames(video_path, output_dir, interval=2):

    output_dir = Path(output_dir)
    output_dir.mkdir(parents=True, exist_ok=True)

    cap = cv2.VideoCapture(str(video_path))

    if not cap.isOpened():
        raise RuntimeError("Cannot open video")

    fps = cap.get(cv2.CAP_PROP_FPS)
    total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))

    duration = total_frames / fps

    print(f"FPS: {fps}")
    print(f"Frames: {total_frames}")
    print(f"Duration: {duration:.2f} seconds")

    current_time = 0
    frame_id = 0

    while current_time < duration:

        cap.set(cv2.CAP_PROP_POS_MSEC, current_time * 1000)

        success, frame = cap.read()

        if not success:
            break

        filename = output_dir / f"frame_{frame_id:05d}.jpg"

        cv2.imwrite(str(filename), frame)

        print(f"Saved: {filename}")

        frame_id += 1
        current_time += interval

    cap.release()


if __name__ == "__main__":

    extract_frames(
        "videos/video_001.mp4",
        "frames/video_001",
        interval=2
    )
```

Run:

```bash
python scripts/extract_visual_frames.py
```

---

# 10. এখন VLM দিয়ে Frame Analyze

এখানে আমরা conceptually এমন pipeline চাই:

```python
image
   ↓
VLM
   ↓
description
```

Input:

```text
frame_00001.jpg
```

Prompt:

```text
Describe this educational scene.

Identify:
1. Main subject
2. Objects
3. Actions
4. Diagrams
5. On-screen text
6. Educational meaning
```

Expected output:

```json
{
    "main_subject": "teacher",
    "objects": [
        "whiteboard",
        "marker"
    ],
    "action": "explaining",
    "diagram": "binary search tree",
    "on_screen_text": "Binary Search",
    "educational_meaning": "The teacher is explaining binary search."
}
```

---

# 11. Generic VLM Pipeline

Production system-এ আমরা বিভিন্ন pretrained VLM ব্যবহার করতে পারি।

Concept:

```text
Image
 ↓
Processor
 ↓
Vision Encoder
 ↓
Language Model
 ↓
Generated Description
```

একটি model-এর ক্ষেত্রে code structure সাধারণত এরকম:

```python
from PIL import Image

image = Image.open("frame.jpg")

prompt = """
Describe this educational scene.
Explain what is being shown,
what objects are visible,
and what concept is being taught.
"""

result = model(
    image=image,
    prompt=prompt
)

print(result)
```

**Important:** এখনই specific VLM model-এর উপর depend না করাই ভালো। আমরা M5-এ architecture বুঝছি; M7-এ actual pretrained Vision Model integration আরও গভীরভাবে করব।

---

# 12. Visual Description Dataset

এখন আমাদের dataset আরও powerful হবে।

M4-এর পরে ছিল:

```json
{
  "start": 0,
  "end": 8,
  "narration": "Binary search divides the array in half."
}
```

M5-এর পরে:

```json
{
  "start": 0,
  "end": 8,

  "narration":
    "Binary search divides the array in half.",

  "visual_description":
    "An array is displayed with the middle element highlighted.",

  "objects": [
    "array",
    "numbers",
    "highlighted middle element"
  ],

  "on_screen_text":
    "Binary Search",

  "scene_type":
    "diagram"
}
```

এটাই future scene planner-এর input হবে।

---

# 13. Narration + Vision

এখন সবচেয়ে গুরুত্বপূর্ণ concept।

ধরো:

### Whisper

```text
"The heart pumps blood throughout the body."
```

### VLM

```text
"An animated human heart is shown,
with arrows indicating blood flow."
```

এখন LLM পাবে:

```text
Narration:
The heart pumps blood throughout the body.

Visual:
An animated heart is shown with arrows
indicating blood flow.
```

LLM বুঝতে পারবে:

```text
Scene Type = Educational Diagram
```

এবং পরে নতুন video generate করতে পারবে:

```text
Scene
 ↓
Animated heart
 ↓
Blood flow arrows
 ↓
Narration
```

---

# 14. Scene Types

আমাদের project-এ scene classification খুব useful।

আমরা শুরুতে এই types রাখতে পারি:

```text
talking_head
diagram
chart
code
equation
animation
real_world
screen_recording
text
transition
comparison
timeline
```

Example:

```json
{
    "scene_type": "diagram"
}
```

অথবা:

```json
{
    "scene_type": "code"
}
```

এটা পরে visual generator নির্বাচন করতে সাহায্য করবে।

---

# 15. Complete M5 Pipeline

এখন পুরো M5:

```text
                  VIDEO
                    │
          ┌─────────┴─────────┐
          │                   │
          ↓                   ↓
       AUDIO                FRAMES
          │                   │
          ↓                   ↓
       Whisper                VLM
          │                   │
          ↓                   ↓
     Transcript        Visual Description
          │                   │
          └─────────┬─────────┘
                    ↓
              Scene Analysis
                    ↓
              Scene JSON
```

---

# 16. Final Dataset Structure

M5-এর শেষে আমরা চাই:

```text
educational_video_ai/
│
├── videos/
│   └── video_001.mp4
│
├── frames/
│   └── video_001/
│       ├── frame_00001.jpg
│       ├── frame_00002.jpg
│       └── ...
│
├── transcripts/
│   └── video_001_transcript.json
│
├── vision/
│   └── video_001_vision.json
│
├── dataset/
│   └── scenes/
│       └── video_001_scenes.json
│
└── scripts/
    ├── transcribe.py
    ├── extract_frames.py
    ├── extract_visual_frames.py
    ├── vision_analysis.py
    └── build_scenes.py
```

---

# 17. M5 Mini Project

এখন তোমার practical task:

একটি educational video নাও।

উদাহরণ:

```text
videos/video_001.mp4
```

তারপর:

### Step 1

Video থেকে frame extract:

```bash
python scripts/extract_visual_frames.py
```

### Step 2

Whisper transcript তৈরি করো:

```bash
python scripts/transcribe.py
```

### Step 3

প্রতিটি 2-second sampled frame analyze করো।

### Step 4

Output তৈরি করো:

```text
vision/video_001_vision.json
```

Expected:

```json
[
  {
    "timestamp": 0,
    "description": "A teacher is standing beside a whiteboard.",
    "objects": ["teacher", "whiteboard"],
    "on_screen_text": "Introduction"
  },
  {
    "timestamp": 2,
    "description": "A binary search diagram is displayed.",
    "objects": ["array", "numbers"],
    "on_screen_text": "Binary Search"
  }
]
```

---

# 18. M5-এর সবচেয়ে গুরুত্বপূর্ণ শিক্ষা

এখন তোমার AI-এর তিনটি component হচ্ছে:

```text
👂 Whisper
"What is being said?"

👁️ Vision Model
"What is being shown?"

🧠 LLM
"What does it mean educationally?"
```

তারপর:

```text
🎨 Generator
"How should we recreate it?"
```

শেষে:

```text
🎬 Educational Video
```

---

# M5 Completion Checklist

M5 শেষ করার আগে তোমার এগুলো বুঝতে হবে:

* [ ] Computer Vision কী
* [ ] Pixel / RGB কী
* [ ] Frame কী
* [ ] Image Classification
* [ ] Object Detection
* [ ] Segmentation
* [ ] Image Captioning
* [ ] Vision-Language Model
* [ ] Frame Sampling
* [ ] Visual Description
* [ ] Scene Type
* [ ] Whisper + Vision combination
* [ ] Visual Dataset JSON
* [ ] Video → Frames → VLM pipeline

### M5-এর পর Architecture

```text
              EDUCATIONAL VIDEO
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
        AUDIO                   FRAMES
          ↓                       ↓
      WHISPER                    VLM
          ↓                       ↓
   TRANSCRIPT JSON        VISION JSON
          │                       │
          └───────────┬───────────┘
                      ↓
               SCENE UNDERSTANDING
                      ↓
                 SCENE JSON
```

**পরবর্তী M6:** আমরা **Computer Vision-এর practical Vision Model integration** করব—একটি pretrained VLM দিয়ে actual image analysis, prompt design, batch frame processing, structured JSON output, এবং আমাদের dataset-এর সঙ্গে integration।
