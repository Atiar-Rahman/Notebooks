# M17 — Educational Dataset Engineering & Training Data Pipeline 📚🧠

M16-এ আমরা **Prompt → Script → Visual → TTS → Subtitle → Video** পুরো pipeline connect করেছি।

এখন আমরা project-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটিতে ঢুকছি:

> **AI-কে ভালোভাবে শেখানোর জন্য কীভাবে high-quality educational dataset তৈরি করবে।**

কারণ তুমি যদি ভবিষ্যতে নিজের **Educational Video AI model fine-tune** করতে চাও, তাহলে শুধু অনেক video থাকলেই হবে না। Dataset-কে machine-learning-এর উপযোগী structured format-এ তৈরি করতে হবে।

---

# 1. M17-এর মূল লক্ষ্য

আমরা এমন একটি dataset pipeline বানাব:

```text
Educational Videos
       ↓
Video Metadata
       ↓
Audio Extraction
       ↓
Whisper
       ↓
Transcript
       ↓
Frame Extraction
       ↓
Vision Analysis
       ↓
Scene Detection
       ↓
Educational Annotation
       ↓
Quality Validation
       ↓
JSONL Dataset
       ↓
Train / Validation / Test
       ↓
Training-ready Dataset
```

শেষে:

```text
dataset/
├── train.jsonl
├── validation.jsonl
├── test.jsonl
├── metadata.json
└── statistics.json
```

---

# 2. কেন Dataset এত গুরুত্বপূর্ণ?

ধরো তুমি model-কে শেখাতে চাও:

> "How should an educational video explain binary search?"

Model-এর কাছে শুধু:

```text
video.mp4
```

থাকলে model জানে না:

* Topic কী?
* কোন অংশে কী শেখানো হচ্ছে?
* narration কী?
* visual কী?
* learning objective কী?
* animation কেন হয়েছে?
* কোন difficulty level?
* কোন scene কোন concept explain করছে?

তাই আমাদের দরকার:

```text
Video
+
Transcript
+
Scene
+
Visual
+
Educational Meaning
```

---

# 3. Dataset-এর মূল ধারণা

একটি educational sample:

```text
Input
 ↓
Topic + Audience + Difficulty
 ↓
Expected Educational Explanation
 ↓
Expected Visual Plan
```

অর্থাৎ training data হতে পারে:

```json id="v9kn21"
{
    "input": {
        "topic": "Binary Search",
        "audience": "beginner",
        "duration": 30
    },

    "output": {
        "script": "...",
        "visual_plan": "...",
        "scene_plan": "..."
    }
}
```

---

# 4. আমাদের Dataset-এর বিভিন্ন স্তর

M17-তে dataset একটাই হবে না।

আমরা কয়েকটি dataset তৈরি করব।

### Dataset 1 — Video Metadata

```text
video_id
topic
subject
duration
language
resolution
fps
```

### Dataset 2 — Transcript

```text
start
end
text
```

### Dataset 3 — Scene Dataset

```text
scene_id
start
end
narration
visual
```

### Dataset 4 — Educational Dataset

```text
topic
learning_objectives
difficulty
teaching_strategy
script
visual_plan
```

### Dataset 5 — Training Dataset

সবকিছু structured format-এ।

---

# 5. Dataset Architecture

```text id="9j3m4k"
                  RAW DATA
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
       Videos                Metadata
          │
          ▼
      FFmpeg/OpenCV
          │
     ┌────┴─────┐
     ▼          ▼
   Audio      Frames
     │          │
     ▼          ▼
  Whisper      VLM
     │          │
     └────┬─────┘
          ▼
   Scene Understanding
          │
          ▼
 Educational Annotation
          │
          ▼
       Validation
          │
          ▼
        JSONL
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
 Train   Val   Test
```

---

# 6. Raw Dataset

ধরো আমাদের কাছে:

```text
raw_videos/
├── binary_search.mp4
├── sorting.mp4
├── photosynthesis.mp4
├── gravity.mp4
└── tcp_ip.mp4
```

কিন্তু এগুলো training-ready না।

---

# 7. Metadata তৈরি

প্রতিটি video-এর metadata:

```json id="3c9k4a"
{
    "video_id": "video_001",
    "filename": "binary_search.mp4",
    "topic": "Binary Search",
    "subject": "Computer Science",
    "language": "en",
    "duration": 60,
    "fps": 30,
    "width": 1280,
    "height": 720
}
```

---

# 8. Metadata কেন দরকার?

ধরো পরে তুমি search করতে চাও:

```text
Find all beginner-level computer science videos.
```

Metadata না থাকলে কঠিন।

Metadata থাকলে:

```text
subject = Computer Science
difficulty = beginner
```

দিয়ে filter করতে পারবে।

---

# 9. Video Metadata Extractor

আমরা M2-তে যে FFprobe/OpenCV শিখেছি সেটা ব্যবহার করব।

```python id="3s6e0f"
import cv2


def get_video_metadata(video_path):

    cap = cv2.VideoCapture(video_path)

    if not cap.isOpened():
        raise ValueError(
            f"Cannot open video: {video_path}"
        )

    fps = cap.get(
        cv2.CAP_PROP_FPS
    )

    frame_count = int(
        cap.get(
            cv2.CAP_PROP_FRAME_COUNT
        )
    )

    width = int(
        cap.get(
            cv2.CAP_PROP_FRAME_WIDTH
        )
    )

    height = int(
        cap.get(
            cv2.CAP_PROP_FRAME_HEIGHT
        )
    )

    cap.release()

    duration = frame_count / fps

    return {
        "fps": fps,
        "frame_count": frame_count,
        "width": width,
        "height": height,
        "duration": duration
    }
```

---

# 10. Important validation

এখানে একটা সমস্যা:

```python
duration = frame_count / fps
```

যদি:

```text
fps = 0
```

হয়?

Error হবে।

তাই:

```python id="6s9k2q"
if fps <= 0:
    raise ValueError(
        "Invalid FPS."
    )
```

এই ধরনের validation dataset pipeline-এ খুব গুরুত্বপূর্ণ।

---

# 11. Audio Dataset

প্রতিটি video থেকে:

```text
video.mp4
    ↓
audio.wav
```

Command:

```bash id="shm8aj"
ffmpeg \
-i video.mp4 \
-ac 1 \
-ar 16000 \
audio.wav
```

আমরা standard রাখব:

```text
Channels = 1
Sample Rate = 16000 Hz
```

---

# 12. Transcript Dataset

Whisper output:

```json id="k6g9vf"
{
    "video_id": "video_001",
    "segments": [
        {
            "start": 0.0,
            "end": 4.2,
            "text": "Binary search is a fast algorithm."
        },
        {
            "start": 4.2,
            "end": 8.0,
            "text": "It works on sorted data."
        }
    ]
}
```

---

# 13. Word-level Dataset

আরও detailed:

```json id="1f9nzs"
{
    "word": "Binary",
    "start": 0.0,
    "end": 0.5
}
```

তারপর:

```text
Binary
search
is
a
fast
algorithm
```

প্রতিটির timestamp থাকবে।

---

# 14. Frame Dataset

আমরা প্রতি frame save করব না।

ধরো:

```text
Video = 10 minutes
FPS = 30
```

Total frames:

```text
10 × 60 × 30
= 18,000 frames
```

এতগুলো frame unnecessary।

তাই:

```text
Every 2 seconds
```

sample করা যায়।

---

# 15. Frame Sampling

```python id="3w8f6q"
import cv2
from pathlib import Path


def extract_frames(
    video_path,
    output_dir,
    interval=2
):

    output_dir = Path(output_dir)
    output_dir.mkdir(
        parents=True,
        exist_ok=True
    )

    cap = cv2.VideoCapture(video_path)

    fps = cap.get(
        cv2.CAP_PROP_FPS
    )

    frame_interval = int(
        fps * interval
    )

    frame_index = 0
    saved_index = 0

    while True:

        ret, frame = cap.read()

        if not ret:
            break

        if frame_index % frame_interval == 0:

            output_path = (
                output_dir
                / f"frame_{saved_index:05d}.jpg"
            )

            cv2.imwrite(
                str(output_path),
                frame
            )

            saved_index += 1

        frame_index += 1

    cap.release()
```

---

# 16. Dataset-এর সবচেয়ে important অংশ: Scene

Video:

```text
0 → 60 sec
```

এটাকে আমরা ভাগ করব:

```text
Scene 1: 0–8
Scene 2: 8–16
Scene 3: 16–25
Scene 4: 25–35
Scene 5: 35–45
Scene 6: 45–60
```

প্রতিটি scene একটি educational unit।

---

# 17. Scene কী?

Scene মানে শুধু camera shot নয়।

Educational context-এ:

> একটি নির্দিষ্ট teaching point যেখানে narration + visual একই concept explain করে।

উদাহরণ:

```text
Narration:
"We check the middle element first."

Visual:
Array-এর middle element highlight করা।

Concept:
Middle element selection.
```

এটাই একটি ভালো educational scene।

---

# 18. Scene Dataset Schema

```json id="2b5zqq"
{
    "video_id": "video_001",

    "scene_id": 1,

    "start": 0.0,
    "end": 5.0,

    "narration":
        "Binary search is a fast search algorithm.",

    "visual_description":
        "A sorted array appears on screen.",

    "concept":
        "Definition of binary search",

    "scene_type":
        "definition",

    "on_screen_text":
        ["Binary Search"],

    "animation_instruction":
        "Reveal the sorted array."
}
```

---

# 19. Educational Annotation

এখানেই dataset powerful হবে।

প্রতিটি scene-এর সাথে:

```text
Concept
Learning Point
Learning Objective
Difficulty
Teaching Strategy
Visual Type
```

যোগ করব।

Example:

```json id="bq8m6x"
{
    "concept": "Binary Search",

    "learning_point":
        "The algorithm checks the middle element first.",

    "learning_objective":
        "Understand the first step of binary search.",

    "difficulty":
        "beginner",

    "teaching_strategy":
        "step_by_step",

    "visual_type":
        "algorithm_diagram"
}
```

---

# 20. কেন এই annotations দরকার?

ভবিষ্যতে তুমি model-কে জিজ্ঞেস করতে পারবে:

```text
Generate a beginner explanation
of binary search.
```

Model training data থেকে pattern শিখবে:

```text
Topic
+
Audience
+
Difficulty
+
Objective
+
Visual
```

→

```text
Script
+
Scene
+
Animation
```

---

# 21. Dataset-এর Final Schema

আমি তোমার project-এর জন্য এই schema recommend করছি:

```json id="frx2my"
{
    "video_id": "video_001",

    "topic": "Binary Search",

    "subject": "Computer Science",

    "difficulty": "beginner",

    "audience": "beginner",

    "language": "en",

    "duration": 30,

    "learning_objectives": [
        "Define binary search",
        "Understand the middle element",
        "Understand half elimination"
    ],

    "teaching_strategy":
        "step_by_step",

    "scenes": [

        {
            "scene_id": 1,

            "start": 0,

            "end": 5,

            "narration":
                "Binary search is a fast search algorithm.",

            "visual_description":
                "A sorted array appears.",

            "concept":
                "Binary search definition",

            "learning_point":
                "Binary search works on sorted data.",

            "scene_type":
                "definition",

            "on_screen_text":
                ["Binary Search"]
        }
    ]
}
```

---

# 22. JSON বনাম JSONL

এটা খুব গুরুত্বপূর্ণ।

### JSON

একটি file:

```json id="3b2y4n"
[
    {...},
    {...},
    {...}
]
```

### JSONL

প্রতিটি line একটি sample:

```text id="0as9l1"
{"video_id":"001", ...}
{"video_id":"002", ...}
{"video_id":"003", ...}
```

Training dataset-এর জন্য JSONL খুব convenient।

---

# 23. কেন JSONL?

ধরো:

```text
1 million samples
```

একটা huge JSON file load করা inefficient হতে পারে।

JSONL:

```text
line 1 → sample 1
line 2 → sample 2
line 3 → sample 3
```

streaming করা সহজ।

---

# 24. JSONL Writer

```python id="v1cyn2"
import json


def write_jsonl(
    records,
    output_path
):

    with open(
        output_path,
        "w",
        encoding="utf-8"
    ) as file:

        for record in records:

            file.write(
                json.dumps(
                    record,
                    ensure_ascii=False
                )
                + "\n"
            )
```

---

# 25. JSONL Reader

```python id="r4c2d8"
import json


def read_jsonl(path):

    records = []

    with open(
        path,
        "r",
        encoding="utf-8"
    ) as file:

        for line in file:

            line = line.strip()

            if not line:
                continue

            records.append(
                json.loads(line)
            )

    return records
```

---

# 26. Dataset Validation

Dataset তৈরি করলেই হবে না।

একটি record:

```json id="5qg7tp"
{
    "video_id": "",
    "topic": "",
    "duration": -10
}
```

স্পষ্টতই invalid।

তাই validation দরকার।

---

# 27. Required Fields

```python id="42g2mt"
REQUIRED_FIELDS = [
    "video_id",
    "topic",
    "subject",
    "difficulty",
    "language",
    "duration",
    "learning_objectives",
    "scenes"
]
```

---

# 28. Validator

```python id="b9q7lq"
def validate_record(record):

    for field in REQUIRED_FIELDS:

        if field not in record:

            raise ValueError(
                f"Missing field: {field}"
            )

    if record["duration"] <= 0:

        raise ValueError(
            "Duration must be positive."
        )

    if not record["scenes"]:

        raise ValueError(
            "Scenes cannot be empty."
        )

    return True
```

---

# 29. Scene Validation

```python id="o0m2sx"
def validate_scenes(scenes):

    previous_end = 0

    for scene in scenes:

        start = scene["start"]
        end = scene["end"]

        if start < previous_end:

            raise ValueError(
                "Scene overlap detected."
            )

        if end <= start:

            raise ValueError(
                "Invalid scene timing."
            )

        previous_end = end

    return True
```

---

# 30. Dataset Quality Score

এখন আমরা আরও advanced হব।

প্রতিটি sample-এর quality score দিতে পারি।

Example:

```text id="l4f16s"
Transcript Quality      0.95
Visual Quality          0.90
Scene Quality           0.88
Educational Quality     0.92
Metadata Quality        1.00
```

Overall:

```text id="m7o4m9"
Quality Score = 0.93
```

---

# 31. কেন Quality Score?

সব collected data সমান ভালো হবে না।

কিছু video:

```text
Good explanation
Clear audio
Good visual
```

কিছু:

```text
Poor audio
Confusing explanation
No useful visual
```

Model training-এ high-quality samples বেশি valuable।

---

# 32. Simple Quality Function

```python id="z89qsp"
def quality_score(
    transcript_score,
    visual_score,
    educational_score,
    metadata_score
):

    return (
        transcript_score * 0.25
        + visual_score * 0.25
        + educational_score * 0.35
        + metadata_score * 0.15
    )
```

Educational quality-কে বেশি weight দিলাম।

কারণ আমাদের লক্ষ্য educational AI।

---

# 33. Dataset Filtering

ধরো:

```text
Quality >= 0.80
```

শুধু এগুলো training-এ:

```text id="zfrqfj"
0.92 → KEEP
0.87 → KEEP
0.81 → KEEP
0.64 → REMOVE
0.55 → REMOVE
```

---

# 34. Duplicate Detection

Dataset-এর আরেকটি বড় problem:

```text
Video A
Video B
```

দুটো একই content হতে পারে।

এটা duplicate।

Duplicate থাকলে training distribution skew হতে পারে।

আমরা future-এ ব্যবহার করতে পারি:

```text
Perceptual Hash
Embedding similarity
Transcript similarity
```

---

# 35. Transcript Similarity

ধরো:

```text
Video A:
"Binary search is a fast search algorithm."

Video B:
"Binary search is a very fast searching algorithm."
```

Text আলাদা হলেও meaning প্রায় same।

Embedding দিয়ে similarity বের করা যায়।

Concept:

```text
Text
 ↓
Embedding
 ↓
Cosine Similarity
 ↓
Similarity > threshold
 ↓
Possible duplicate
```

এটা M17-এর advanced topic।

---

# 36. Data Leakage — খুব গুরুত্বপূর্ণ

ধরো:

```text
Video A
 ├── Scene 1
 ├── Scene 2
 └── Scene 3
```

তুমি যদি:

```text
Train:
Scene 1

Test:
Scene 3
```

করো, তাহলে leakage হতে পারে।

কারণ একই video-এর content train এবং test উভয় জায়গায়।

---

# 37. Correct Split

**Video-level split** করতে হবে।

```text
Video A ────────── TRAIN

Video B ────────── TRAIN

Video C ────────── VALIDATION

Video D ────────── TEST
```

একই video-এর scene বিভিন্ন split-এ যাবে না।

---

# 38. Train / Validation / Test

Recommended:

```text
Train       80%
Validation  10%
Test        10%
```

অথবা:

```text
Train       70%
Validation  15%
Test        15%
```

Dataset size অনুযায়ী পরিবর্তন করতে পারো।

---

# 39. Split করার Python

```python id="d7c5d0"
import random


def split_dataset(
    records,
    train_ratio=0.8,
    val_ratio=0.1,
    seed=42
):

    random.seed(seed)

    records = records.copy()

    random.shuffle(records)

    total = len(records)

    train_end = int(
        total * train_ratio
    )

    val_end = int(
        total * (
            train_ratio + val_ratio
        )
    )

    train = records[:train_end]

    validation = records[
        train_end:val_end
    ]

    test = records[val_end:]

    return train, validation, test
```

---

# 40. কিন্তু real project-এ random split যথেষ্ট নয়

আমাদের dataset-এ class/topic imbalance হতে পারে।

ধরো:

```text
Computer Science = 80%
Biology = 10%
Physics = 5%
Math = 5%
```

Model Computer Science-এর দিকে biased হতে পারে।

তাই statistics দেখতে হবে।

---

# 41. Dataset Statistics

আমরা calculate করব:

```text
Total videos
Total scenes
Total hours
Subjects
Languages
Difficulty distribution
Scene types
Average duration
Average words
```

Example:

```json id="v0gd9v"
{
    "total_videos": 1000,
    "total_scenes": 8500,

    "subjects": {
        "computer_science": 300,
        "biology": 200,
        "physics": 150,
        "mathematics": 250,
        "other": 100
    },

    "difficulty": {
        "beginner": 500,
        "intermediate": 350,
        "advanced": 150
    }
}
```

---

# 42. Dataset Statistics Function

```python id="5fsk9a"
from collections import Counter


def dataset_statistics(records):

    subjects = Counter(
        record["subject"]
        for record in records
    )

    difficulty = Counter(
        record["difficulty"]
        for record in records
    )

    total_scenes = sum(
        len(record["scenes"])
        for record in records
    )

    return {
        "total_videos": len(records),
        "total_scenes": total_scenes,
        "subjects": dict(subjects),
        "difficulty": dict(difficulty)
    }
```

---

# 43. Dataset Versioning

M17-এ আরেকটি professional concept:

```text
Dataset v1
Dataset v2
Dataset v3
```

Example:

```text
dataset_v1/
dataset_v2/
dataset_v3/
```

অথবা:

```json id="n7kr8x"
{
    "dataset_version": "1.0.0",
    "created_at": "2026-09-06",
    "total_samples": 10000
}
```

---

# 44. কেন Versioning?

ধরো তুমি:

```text
v1 → 10,000 samples
```

দিয়ে model train করলে।

পরে:

```text
v2 → 30,000 samples
```

দিলে performance change হলো।

তুমি জানতে চাইবে:

> কোন dataset version ব্যবহার করা হয়েছিল?

তাই versioning দরকার।

---

# 45. Dataset Provenance

প্রতিটি sample-এর source information রাখা উচিত।

```json id="pr1y2r"
{
    "video_id": "video_001",

    "source": {
        "type": "public_domain",
        "license": "CC BY",
        "attribution_required": true
    }
}
```

অথবা:

```json id="h2ndy0"
{
    "source": {
        "type": "original"
    }
}
```

---

# 46. Copyright বিষয়টি খুব গুরুত্বপূর্ণ

তুমি যেহেতু AI video generation system বানাচ্ছ, dataset collection-এর সময়:

**যেকোনো internet video download করে training-এ ব্যবহার করা safe ধরে নেবে না।**

Use:

```text
নিজের তৈরি content
+
Public domain
+
Explicitly licensed content
+
যে license ML/training use অনুমোদন করে
```

License/provenance metadata রাখবে।

---

# 47. Dataset Pipeline-এর বাস্তব Workflow

ধরো তোমার কাছে 100 video আছে।

```text
100 Videos
    ↓
Metadata extraction
    ↓
Audio extraction
    ↓
Whisper
    ↓
Frame sampling
    ↓
VLM analysis
    ↓
Scene segmentation
    ↓
LLM educational annotation
    ↓
Validation
    ↓
Quality filtering
    ↓
Deduplication
    ↓
Train/Val/Test
    ↓
JSONL
```

এটাই M17-এর মূল pipeline।

---

# 48. Automated Dataset Builder

আমরা একটা central class করতে পারি:

```python id="l1ek9j"
class DatasetBuilder:

    def __init__(
        self,
        whisper,
        vision,
        annotator
    ):

        self.whisper = whisper
        self.vision = vision
        self.annotator = annotator

    def process_video(
        self,
        video_path
    ):

        metadata = self.extract_metadata(
            video_path
        )

        transcript = self.transcribe(
            video_path
        )

        frames = self.extract_frames(
            video_path
        )

        visual_data = self.analyze_frames(
            frames
        )

        scenes = self.create_scenes(
            transcript,
            visual_data
        )

        annotation = self.annotate(
            scenes
        )

        return annotation
```

---

# 49. End-to-End Dataset Builder

Final architecture:

```text id="l8nq1a"
                 VIDEO
                   │
                   ▼
              Metadata
                   │
                   ▼
               Audio
                   │
                   ▼
               Whisper
                   │
                   ▼
             Transcript
                   │
                   │
Frames ────────────┤
  │                │
  ▼                ▼
 Vision          Timing
  │                │
  └───────┬────────┘
          ▼
    Scene Alignment
          │
          ▼
 Educational Annotation
          │
          ▼
     Quality Filter
          │
          ▼
      Deduplication
          │
          ▼
       JSONL
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
 Train   Val   Test
```

---

# 50. Training Dataset-এর জন্য দুটি গুরুত্বপূর্ণ Format

পরবর্তীতে তুমি দুই ধরনের training data ব্যবহার করবে।

### Format A — Instruction Dataset

```json id="qg0q4k"
{
    "instruction":
        "Explain binary search to a beginner.",

    "input": {
        "duration": 30,
        "style": "clean_2d"
    },

    "output": {
        "script": "...",
        "scene_plan": [...]
    }
}
```

এটা LLM/Planner fine-tuning-এর জন্য useful।

---

### Format B — Multimodal Dataset

```json id="l0r5qn"
{
    "topic": "Binary Search",

    "frames": [
        "frame_001.jpg",
        "frame_002.jpg"
    ],

    "transcript":
        "We check the middle element.",

    "scene_type":
        "algorithm_diagram",

    "visual_description":
        "Middle element is highlighted."
}
```

এটা VLM/vision-related training-এর জন্য useful।

---

# 51. Model অনুযায়ী Dataset আলাদা হবে

এটা খুব গুরুত্বপূর্ণ।

তুমি **একটা dataset দিয়ে সব model train করবে না।**

### LLM

```text
Prompt
→
Script / Scene JSON
```

### VLM

```text
Image + Text
→
Visual Understanding
```

### TTS

```text
Text
→
Speech
```

### Video Model

```text
Text / Image
→
Video
```

প্রতিটি model-এর data requirement আলাদা।

---

# 52. তোমার Educational AI-এর জন্য Dataset Strategy

আমি recommend করব:

```text
                 MASTER DATASET
                       │
       ┌───────────────┼────────────────┐
       ▼               ▼                ▼
  LLM Dataset      VLM Dataset      Video Dataset
       │               │                │
       ▼               ▼                ▼
Script/JSON       Image+Text        Text→Video
```

পাশাপাশি:

```text
TTS Dataset
```

এবং:

```text
Evaluation Dataset
```

---

# 53. Evaluation Dataset

Training data-এর বাইরে একটা **gold test set** রাখবে।

যেমন:

```text
100 carefully reviewed prompts
```

Examples:

```text
Explain binary search.
Explain photosynthesis.
Explain Newton's second law.
Explain TCP handshake.
Explain recursion.
```

প্রতিটির জন্য human-approved expected output থাকবে।

তারপর model generate করলে compare করবে।

---

# 54. Human Annotation

সব annotation AI দিয়ে করালে ভুল থাকতে পারে।

Best workflow:

```text
Video
 ↓
AI generates annotation
 ↓
Human reviews
 ↓
Correct
 ↓
Approved Dataset
```

অর্থাৎ:

> **AI-assisted annotation, human-verified dataset.**

এটা খুব powerful approach।

---

# 55. Annotation UI — Future

তোমার Django + React knowledge এখানে ব্যবহার করা যাবে।

UI:

```text id="b8h1ck"
┌─────────────────────────────────────────┐
│ Video Preview                           │
│                                         │
│       🎬                               │
│                                         │
├─────────────────────────────────────────┤
│ Scene 01                                │
│ Start: 00:00                            │
│ End:   00:05                            │
│                                         │
│ Narration:                              │
│ [ Binary search checks the middle... ]  │
│                                         │
│ Concept: [ Binary Search ]              │
│                                         │
│ Scene Type: [ Algorithm ]               │
│                                         │
│ Difficulty: [ Beginner ]                │
│                                         │
│ [Approve] [Edit] [Reject]               │
└─────────────────────────────────────────┘
```

এভাবে dataset annotation করা যাবে।

---

# 56. M17 Mini Project 🎯

এখন তোমার practical project:

## `EducationalDatasetBuilder`

একটি video নেবে:

```text
videos/binary_search.mp4
```

এবং তৈরি করবে:

```text
dataset/
└── video_001/
    │
    ├── metadata.json
    ├── audio.wav
    ├── transcript.json
    ├── frames/
    │   ├── frame_00001.jpg
    │   ├── frame_00002.jpg
    │   └── ...
    │
    └── scenes.json
```

---

# 57. তারপর Final JSONL

সব video process করে:

```text
dataset/
├── train.jsonl
├── validation.jsonl
├── test.jsonl
└── statistics.json
```

---

# 58. Example `train.jsonl`

```text id="g8j1z9"
{"video_id":"001","topic":"Binary Search","subject":"Computer Science",...}
{"video_id":"002","topic":"Photosynthesis","subject":"Biology",...}
{"video_id":"003","topic":"Newton's Laws","subject":"Physics",...}
```

---

# 59. M17-এর Advanced Goal

শেষে তোমার dataset pipeline এমন হবে:

```text
             RAW VIDEO
                 ↓
          Automatic Processing
                 ↓
        ┌────────┴────────┐
        ▼                 ▼
      Audio              Frames
        ↓                 ↓
     Whisper             VLM
        ↓                 ↓
        └───────┬─────────┘
                ▼
        Multimodal Analysis
                ↓
       Educational Annotation
                ↓
        Human Verification
                ↓
          Quality Filter
                ↓
           Deduplicate
                ↓
         Dataset Versioning
                ↓
        Train / Val / Test
                ↓
             JSONL
                ↓
       ┌────────┼─────────┐
       ▼        ▼         ▼
      LLM      VLM       Video
    Dataset   Dataset    Dataset
```

---

# 60. M17 Completion Checklist

### Video Data

* [ ] Video metadata extract করতে পারি
* [ ] FPS বুঝি
* [ ] Duration বুঝি
* [ ] Resolution বুঝি
* [ ] Frame sampling করতে পারি

### Audio

* [ ] Audio extract করতে পারি
* [ ] Whisper transcript তৈরি করতে পারি
* [ ] Segment timestamp বুঝি
* [ ] Word timestamp বুঝি

### Scene

* [ ] Scene কী বুঝি
* [ ] Scene boundary তৈরি করতে পারি
* [ ] Narration + visual align করতে পারি
* [ ] Scene annotation করতে পারি

### Educational Data

* [ ] Topic
* [ ] Subject
* [ ] Audience
* [ ] Difficulty
* [ ] Learning objective
* [ ] Teaching strategy
* [ ] Learning point
* [ ] Scene type

সব বুঝতে হবে।

### Dataset Engineering

* [ ] JSON
* [ ] JSONL
* [ ] Validation
* [ ] Quality scoring
* [ ] Duplicate detection concept
* [ ] Train/Val/Test
* [ ] Video-level split
* [ ] Dataset statistics
* [ ] Dataset versioning
* [ ] Data provenance

---

# 🔥 M1 → M17 এখন কী দাঁড়িয়েছে?

```text id="q4xj4h"
M1  Python Pipeline
 ↓
M2  Video Processing
 ↓
M3  Dataset Engineering
 ↓
M4  Speech Understanding
 ↓
M5  Computer Vision
 ↓
M6  Pretrained Vision Models
 ↓
M7  Multimodal Understanding
 ↓
M8  Educational Planner
 ↓
M9  Script Generator
 ↓
M10 Visual Planner
 ↓
M11 Animation Engine
 ↓
M12 Generic Diagram Engine
 ↓
M13 Timeline Engine
 ↓
M14 TTS
 ↓
M15 Subtitle + Sync
 ↓
M16 End-to-End Pipeline
 ↓
🔥 M17 Training Dataset Pipeline
```

এখন project-এর সবচেয়ে গুরুত্বপূর্ণ transformation শুরু হয়েছে:

```text
আগে:
"আমরা video generate করতে পারি।"

এখন:
"আমরা AI-কে শেখানোর মতো structured educational data তৈরি করতে পারি।"
```

## পরবর্তী: M18 — Advanced LLM Integration 🧠

M18-এ আমরা **LLM-কে তোমার Educational Video AI-এর actual brain** হিসেবে integrate করব:

```text
User Prompt
     ↓
LLM
     ↓
Topic Understanding
     ↓
Audience Understanding
     ↓
Learning Objectives
     ↓
Teaching Strategy
     ↓
Script
     ↓
Scene JSON
     ↓
Visual JSON
```

এবং সবচেয়ে গুরুত্বপূর্ণভাবে **structured JSON output, prompt design, validation, retries, hallucination control, model/API abstraction এবং local-vs-cloud LLM architecture** তৈরি করব।

----
# M18 — Advanced LLM Integration 🧠

আজ আমরা তোমার Educational Video AI-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি তৈরি করব:

> **LLM হবে system-এর “Brain” — কিন্তু LLM সরাসরি video বানাবে না।**

M17-তে আমরা training-ready educational dataset pipeline তৈরি করেছি।  
M18-তে আমরা সেই dataset/architecture ব্যবহার করে **real LLM → structured VideoPlan JSON** pipeline তৈরি করব।

---

# 1. M18-এ আমরা কী বানাব?

User লিখবে:

```text
Explain binary search to a beginner in 30 seconds.
```

System:

```text
User Prompt
     ↓
LLM
     ↓
Understand Topic
     ↓
Understand Audience
     ↓
Create Learning Objectives
     ↓
Choose Teaching Strategy
     ↓
Generate Script
     ↓
Generate Scene Plan
     ↓
Generate Visual Instructions
     ↓
Validate JSON
     ↓
VideoPlan
```

শেষে আমরা এমন JSON পাব:

```json
{
  "topic": "Binary Search",
  "subject": "Computer Science",
  "audience": "beginner",
  "difficulty": "beginner",
  "duration": 30,
  "learning_objectives": [
    "Understand what binary search is",
    "Understand the middle element",
    "Understand how half the search space is removed"
  ],
  "teaching_strategy": "step_by_step",
  "scenes": [
    {
      "scene_id": 1,
      "start": 0,
      "end": 5,
      "narration": "Binary search is a fast way to find an item in a sorted list.",
      "visual_description": "Show a sorted array.",
      "scene_type": "definition"
    }
  ]
}
```

এই JSON যাবে:

```text
M18 LLM
   ↓
M10 Visual Planner
   ↓
M11/M12 Renderer
   ↓
M14 TTS
   ↓
M15 Subtitle
   ↓
M16 Composer
```

---

# 2. কেন Advanced LLM Integration দরকার?

আগে আমরা static/mock JSON ব্যবহার করছিলাম।

যেমন:

```python
plan = {
    "topic": "Binary Search",
    ...
}
```

এটা production AI না।

আমাদের দরকার:

```text
Any User Prompt
      ↓
LLM
      ↓
Structured Educational Plan
```

যেমন:

### Input 1

```text
Explain photosynthesis to a child in 60 seconds.
```

### Input 2

```text
Explain TCP vs UDP to a networking student in 45 seconds.
```

### Input 3

```text
Explain recursion with a simple example.
```

একই pipeline সবগুলো handle করবে।

---

# 3. সবচেয়ে গুরুত্বপূর্ণ Architecture

M18-এর architecture:

```text
                    USER
                     │
                     ▼
              User Prompt
                     │
                     ▼
             Prompt Processor
                     │
                     ▼
             ┌───────────────┐
             │      LLM      │
             │    "Brain"    │
             └───────┬───────┘
                     │
                     ▼
             Structured JSON
                     │
                     ▼
              Pydantic Validator
                     │
             ┌───────┴────────┐
             │                │
           Valid            Invalid
             │                │
             ▼                ▼
       Continue         Retry / Repair
             │
             ▼
        VideoPlan
             │
       ┌─────┼─────┐
       ▼     ▼     ▼
    Script Visual Timing
       │     │     │
       └─────┼─────┘
             ▼
        M10/M11/M12
```

এখানে সবচেয়ে গুরুত্বপূর্ণ design principle:

> **LLM সিদ্ধান্ত নেবে কী বানাতে হবে।  
> Deterministic code সিদ্ধান্ত নেবে কীভাবে বানাতে হবে।**

---

# 4. LLM কী করবে?

LLM-এর দায়িত্ব:

### 1. Topic understanding

```text
"Explain binary search"
```

→ Topic:

```text
Binary Search
```

### 2. Audience understanding

```text
to a beginner
```

→

```text
Audience = beginner
```

### 3. Difficulty

```text
Difficulty = beginner
```

### 4. Learning objectives

```text
1. Understand binary search
2. Understand sorted data
3. Understand middle element
4. Understand elimination
```

### 5. Teaching strategy

যেমন:

```text
step_by_step
```

### 6. Script

Natural language narration।

### 7. Scene planning

```text
Scene 1 → Introduction
Scene 2 → Array
Scene 3 → Middle element
Scene 4 → Remove half
Scene 5 → Summary
```

### 8. Visual planning

```text
Show array
Highlight middle
Remove left half
```

---

# 5. LLM কী করবে না?

এটা খুব গুরুত্বপূর্ণ।

LLM-কে সরাসরি এটা করতে দিও না:

```text
Generate complete Manim Python code
```

বরং:

```text
LLM
 ↓
JSON
 ↓
Renderer
 ↓
Python/Manim
```

কারণ LLM-generated code হতে পারে:

- invalid
    
- unsafe
    
- inconsistent
    
- difficult to validate
    
- difficult to maintain
    

আমাদের system হবে:

```text
LLM → Plan
Code → Execution
```

---

# 6. Project Structure

M18-এর জন্য structure:

```text
educational_video_ai/
│
├── app/
│   ├── config.py
│   ├── schemas.py
│   └── pipeline.py
│
├── llm/
│   ├── __init__.py
│   ├── client.py
│   ├── prompts.py
│   ├── planner.py
│   ├── parser.py
│   ├── validator.py
│   └── retry.py
│
├── planner/
│   ├── educational_planner.py
│   ├── script_generator.py
│   └── scene_planner.py
│
├── renderer/
│
├── tts/
│
├── subtitle/
│
├── timeline/
│
├── composer/
│
├── projects/
│
├── output/
│
├── .env
├── requirements.txt
└── scripts/
    └── generate_video.py
```

আজকের focus:

```text
llm/
├── client.py
├── prompts.py
├── planner.py
├── parser.py
├── validator.py
└── retry.py
```

---

# 7. Installation

আমরা API-independent architecture তৈরি করব।

প্রথমে:

```bash
pip install pydantic python-dotenv
```

তোমার নির্দিষ্ট LLM provider-এর SDK পরে `client.py`-তে plug করা যাবে।

উদাহরণ:

```text
OpenAI
Anthropic
Gemini
local Ollama
Hugging Face
vLLM
```

অর্থাৎ architecture provider-dependent হবে না।

---

# 8. Environment Variables

`.env`

```env
LLM_API_KEY=your_api_key
LLM_MODEL=your_model
```

কখনো Python code-এর মধ্যে API key লিখবে না:

```python
API_KEY = "abc123"
```

❌ ভুল।

বরং:

```python
from dotenv import load_dotenv
import os

load_dotenv()

api_key = os.getenv("LLM_API_KEY")
model = os.getenv("LLM_MODEL")
```

---

# 9. Configuration

`app/config.py`

```python
import os
from dotenv import load_dotenv

load_dotenv()


class Settings:
    LLM_API_KEY = os.getenv("LLM_API_KEY")
    LLM_MODEL = os.getenv("LLM_MODEL", "default-model")
    MAX_RETRIES = 3


settings = Settings()
```

### কেন class?

যাতে পুরো application-এ:

```python
from app.config import settings

print(settings.LLM_MODEL)
```

ব্যবহার করতে পারি।

---

# 10. VideoPlan Schema

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

`app/schemas.py`

```python
from typing import List
from pydantic import BaseModel, Field


class Scene(BaseModel):
    scene_id: int
    start: float
    end: float

    narration: str
    visual_description: str

    scene_type: str

    on_screen_text: List[str] = Field(default_factory=list)

    animation_instruction: str = ""


class VideoPlan(BaseModel):
    topic: str
    subject: str

    audience: str
    difficulty: str

    language: str

    duration: float

    learning_objectives: List[str]

    teaching_strategy: str

    scenes: List[Scene]
```

এখন LLM যা output দেবে সেটা এই schema-এর সাথে match করতে হবে।

---

# 11. কেন Pydantic?

ধরো LLM output দিল:

```json
{
  "topic": "Binary Search",
  "duration": "thirty seconds"
}
```

আমাদের দরকার:

```python
duration: float
```

Pydantic detect করতে পারবে:

```text
Expected float
Got invalid value
```

আর যদি:

```json
{
  "topic": "Binary Search"
}
```

তাহলে missing fields detect হবে।

অর্থাৎ:

```text
LLM
 ↓
Untrusted Output
 ↓
Pydantic
 ↓
Trusted Internal Data
```

এটা production AI system-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 12. Prompt Engineering

এখন আসল Brain instruction।

`llm/prompts.py`

```python
SYSTEM_PROMPT = """
You are an expert educational content planner.

Your job is to convert a user's educational request
into a structured video plan.

The video plan must be:

- educationally accurate
- easy to understand
- appropriate for the target audience
- logically structured
- visually explainable
- synchronized with the requested duration

You must return structured JSON.

Do not return markdown.
Do not return explanations outside the JSON.

The JSON must contain:

topic
subject
audience
difficulty
language
duration
learning_objectives
teaching_strategy
scenes

Each scene must contain:

scene_id
start
end
narration
visual_description
scene_type
on_screen_text
animation_instruction
"""
```

---

# 13. User Prompt

এখন user-এর prompt:

```python
def build_user_prompt(user_prompt: str) -> str:
    return f"""
Create an educational video plan for this request:

{user_prompt}

Requirements:

1. Identify the topic.
2. Identify the subject.
3. Identify the target audience.
4. Determine the difficulty.
5. Create clear learning objectives.
6. Choose an appropriate teaching strategy.
7. Create a narration script.
8. Divide the video into scenes.
9. Give visual descriptions for every scene.
10. Give animation instructions where useful.
11. Keep scene timing within the requested duration.
"""
```

---

# 14. Prompt Engineering-এর গুরুত্বপূর্ণ Rule

LLM-কে শুধু বলবে না:

```text
Explain binary search.
```

বরং context দাও:

```text
You are an expert educational content planner.

Create a 30-second explanation of binary search
for a beginner.

Use simple language.

Create 3 learning objectives.

Return structured JSON.
```

এতে output quality অনেক ভালো হবে।

---

# 15. Prompt-এর পাঁচটি Layer

আমাদের Educational AI-তে prompt structure হবে:

```text
1. ROLE
2. TASK
3. CONTEXT
4. CONSTRAINTS
5. OUTPUT FORMAT
```

### ROLE

```text
You are an expert educational content planner.
```

### TASK

```text
Create a video plan.
```

### CONTEXT

```text
Audience = beginner
Subject = computer science
```

### CONSTRAINTS

```text
Duration = 30 seconds
Simple language
Maximum 5 scenes
```

### OUTPUT FORMAT

```text
Return structured JSON.
```

---

# 16. LLM Client Abstraction

এখন provider-independent interface বানাব।

`llm/client.py`

```python
from abc import ABC, abstractmethod


class LLMClient(ABC):

    @abstractmethod
    def generate(self, system_prompt: str, user_prompt: str) -> str:
        pass
```

এটা একটি interface।

এর ফলে আমরা পরে:

```text
OpenAIClient
GeminiClient
OllamaClient
HuggingFaceClient
```

বানাতে পারব।

---

# 17. Mock LLM Client

Development-এর জন্য খুব useful।

```python
class MockLLMClient(LLMClient):

    def generate(self, system_prompt: str, user_prompt: str) -> str:

        return """
        {
            "topic": "Binary Search",
            "subject": "Computer Science",
            "audience": "beginner",
            "difficulty": "beginner",
            "language": "en",
            "duration": 30,
            "learning_objectives": [
                "Understand binary search",
                "Understand the middle element",
                "Understand how half the search space is removed"
            ],
            "teaching_strategy": "step_by_step",
            "scenes": [
                {
                    "scene_id": 1,
                    "start": 0,
                    "end": 5,
                    "narration": "Binary search is a fast way to search sorted data.",
                    "visual_description": "Show a sorted array.",
                    "scene_type": "definition",
                    "on_screen_text": ["Binary Search"],
                    "animation_instruction": "Reveal the array."
                }
            ]
        }
        """
```

এতে API call ছাড়াই পুরো pipeline test করা যাবে।

এটা খুব ভালো software engineering practice।

---

# 18. JSON Parser

`llm/parser.py`

```python
import json


def parse_json(text: str) -> dict:

    try:
        return json.loads(text)

    except json.JSONDecodeError as error:
        raise ValueError(
            f"Invalid JSON returned by LLM: {error}"
        )
```

এখন:

```python
raw_output = client.generate(
    system_prompt,
    user_prompt
)

data = parse_json(raw_output)
```

---

# 19. Pydantic Validation

`llm/validator.py`

```python
from app.schemas import VideoPlan


def validate_video_plan(data: dict) -> VideoPlan:

    try:
        return VideoPlan.model_validate(data)

    except Exception as error:
        raise ValueError(
            f"Video plan validation failed: {error}"
        )
```

Flow:

```text
LLM String
   ↓
JSON Parse
   ↓
dict
   ↓
Pydantic
   ↓
VideoPlan
```

---

# 20. Timing Validation

Pydantic শুধু type validation করবে।

Educational logic validation আমাদের করতে হবে।

`llm/validator.py`

```python
def validate_scene_timing(plan: VideoPlan):

    previous_end = 0

    for scene in plan.scenes:

        if scene.start < previous_end:
            raise ValueError(
                f"Scene {scene.scene_id} overlaps."
            )

        if scene.end <= scene.start:
            raise ValueError(
                f"Scene {scene.scene_id} has invalid timing."
            )

        if scene.end > plan.duration:
            raise ValueError(
                f"Scene {scene.scene_id} exceeds video duration."
            )

        previous_end = scene.end

    return True
```

---

# 21. Learning Objective Validation

এটাও important।

ধরো user বলেছে:

```text
Explain binary search.
```

কিন্তু LLM output:

```text
learning_objectives = []
```

এটা acceptable না।

```python
def validate_learning_objectives(plan):

    if not plan.learning_objectives:
        raise ValueError(
            "At least one learning objective is required."
        )

    return True
```

---

# 22. Scene Validation

```python
def validate_scenes(plan):

    if not plan.scenes:
        raise ValueError(
            "Video must contain at least one scene."
        )

    return True
```

---

# 23. Complete Validation

```python
def validate_plan(plan):

    validate_scene_timing(plan)
    validate_learning_objectives(plan)
    validate_scenes(plan)

    return True
```

এখন:

```text
LLM
 ↓
JSON
 ↓
Pydantic
 ↓
Timing Validation
 ↓
Educational Validation
 ↓
Approved Plan
```

---

# 24. Advanced Retry System

LLM সবসময় perfect output দেবে না।

সমস্যা হতে পারে:

```text
Invalid JSON
Missing field
Invalid timing
Too many scenes
Empty narration
```

তাই:

```text
LLM
 ↓
Validate
 ↓
FAIL
 ↓
Retry
 ↓
LLM
 ↓
Validate
 ↓
SUCCESS
```

---

# 25. Retry Code

`llm/retry.py`

```python
def generate_valid_plan(
    client,
    system_prompt,
    user_prompt,
    max_retries=3
):

    last_error = None

    for attempt in range(max_retries):

        try:

            raw_output = client.generate(
                system_prompt,
                user_prompt
            )

            data = parse_json(raw_output)

            plan = validate_video_plan(data)

            validate_plan(plan)

            return plan

        except Exception as error:

            last_error = error

            print(
                f"Attempt {attempt + 1} failed: {error}"
            )

    raise RuntimeError(
        f"Failed after {max_retries} attempts: {last_error}"
    )
```

এখানে architecture:

```text
Attempt 1
   ↓
Invalid
   ↓
Attempt 2
   ↓
Invalid
   ↓
Attempt 3
   ↓
Valid
```

---

# 26. Complete Educational Planner

`llm/planner.py`

```python
from llm.prompts import (
    SYSTEM_PROMPT,
    build_user_prompt
)

from llm.parser import parse_json
from llm.validator import (
    validate_video_plan,
    validate_plan
)


class EducationalLLMPlanner:

    def __init__(self, client):
        self.client = client

    def create_plan(self, user_prompt):

        system_prompt = SYSTEM_PROMPT

        prompt = build_user_prompt(
            user_prompt
        )

        raw_output = self.client.generate(
            system_prompt,
            prompt
        )

        data = parse_json(raw_output)

        plan = validate_video_plan(data)

        validate_plan(plan)

        return plan
```

এটাই আমাদের M18-এর main brain interface।

---

# 27. Run করার Script

`scripts/test_llm.py`

```python
from llm.client import MockLLMClient
from llm.planner import EducationalLLMPlanner


def main():

    client = MockLLMClient()

    planner = EducationalLLMPlanner(
        client
    )

    prompt = (
        "Explain binary search "
        "to a beginner in 30 seconds."
    )

    plan = planner.create_plan(prompt)

    print(plan.model_dump_json(indent=2))


if __name__ == "__main__":
    main()
```

Run:

```bash
python scripts/test_llm.py
```

Output হবে structured VideoPlan।

---

# 28. Complete Flow এখন

তোমার M16 pipeline ছিল:

```text
Prompt
 ↓
Planner
 ↓
Renderer
 ↓
TTS
 ↓
Subtitle
 ↓
FFmpeg
```

এখন M18-এর পরে:

```text
User Prompt
     ↓
Educational LLM
     ↓
JSON
     ↓
JSON Parser
     ↓
Pydantic
     ↓
Educational Validator
     ↓
VideoPlan
     ↓
Visual Planner
     ↓
Renderer
     ↓
TTS
     ↓
Subtitle
     ↓
Timeline
     ↓
FFmpeg
     ↓
MP4
```

---

# 29. M18-এর সবচেয়ে গুরুত্বপূর্ণ Concept — Structured Generation

Traditional LLM:

```text
Prompt
 ↓
Text
```

আমাদের system:

```text
Prompt
 ↓
Structured Data
```

অর্থাৎ:

```text
LLM
 ↓
JSON
 ↓
Pydantic
 ↓
Application
```

এটা AI application development-এর খুব গুরুত্বপূর্ণ pattern।

---

# 30. JSON হলো Intermediate Representation

আমরা এটাকে **IR — Intermediate Representation** হিসেবে ধরতে পারি।

```text
Natural Language
       ↓
      LLM
       ↓
   VideoPlan IR
       ↓
 ┌─────┼─────┐
 ↓     ↓     ↓
TTS  Visual Timeline
       ↓
    Renderer
       ↓
      MP4
```

এই architecture-এর সবচেয়ে বড় সুবিধা হলো:

LLM বদলাতে পারবে।

আজ:

```text
OpenAI
```

কাল:

```text
Gemini
```

পরশু:

```text
Local Llama
```

কিন্তু:

```text
VideoPlan
```

একই থাকবে।

---

# 31. Local LLM Support

Future-এ তুমি local model চালাতে পারো:

```text
Ollama
   ↓
Local LLM
   ↓
VideoPlan
```

অথবা:

```text
Hugging Face
   ↓
Transformers
   ↓
Local GPU
```

Architecture change হবে না।

শুধু:

```python
client = OpenAIClient()
```

এর জায়গায়:

```python
client = OllamaClient()
```

---

# 32. Hallucination Control

Educational AI-এর ক্ষেত্রে এটা অত্যন্ত গুরুত্বপূর্ণ।

LLM ভুল তথ্য দিতে পারে।

যেমন:

```text
User: Explain Newton's laws.
```

LLM ভুল statement তৈরি করলে educational video-ও ভুল হবে।

তাই আমাদের architecture হবে:

```text
User
 ↓
LLM
 ↓
Content Validation
 ↓
Trusted Knowledge / RAG
 ↓
Final Plan
```

M18-এ আমরা basic validation করছি।

পরবর্তীতে:

```text
M26 → RAG + Trusted Knowledge
```

এটা আরও শক্তিশালী করবে।

---

# 33. Advanced Prompt — Accuracy

System prompt-এ আমরা add করতে পারি:

```text
Do not invent scientific or technical facts.

If a claim is uncertain, do not fabricate it.

Prefer well-established educational explanations.

Keep the explanation appropriate for the requested level.
```

এতে hallucination কমানোর চেষ্টা করা যায়, যদিও **prompt alone accuracy guarantee করে না**।

---

# 34. Duration Control

User:

```text
Explain recursion in 20 seconds.
```

LLM যেন 3 মিনিটের script না দেয়।

আমরা target word count ব্যবহার করতে পারি।

আগের M9 rule:

```text
120–160 WPM
```

20 sec:

```text
20 / 60 × 120 = 40 words
20 / 60 × 160 ≈ 53 words
```

অর্থাৎ:

```text
40–53 words
```

Planner prompt-এ:

```text
Target narration length:
40–53 words.
```

এতে timing control ভালো হবে।

---

# 35. Scene Duration

ধরো:

```text
Video = 30 sec
```

LLM output:

```text
Scene 1 = 0–8
Scene 2 = 8–15
Scene 3 = 15–24
Scene 4 = 24–30
```

Excellent।

কিন্তু যদি:

```text
Scene 1 = 0–10
Scene 2 = 8–15
```

তাহলে:

```text
OVERLAP ❌
```

আমাদের validator detect করবে।

---

# 36. LLM Quality Architecture

Production-এ শুধু একটা LLM call যথেষ্ট না।

Better:

```text
                  User Prompt
                       ↓
                Planning LLM
                       ↓
                  VideoPlan
                       ↓
                Validation
                       ↓
               Quality Check
                       ↓
          ┌────────────┴────────────┐
          │                         │
        Good                     Bad
          │                         │
          ▼                         ▼
       Continue                   Retry
```

আর advanced version:

```text
Planner LLM
     ↓
Content Reviewer LLM
     ↓
Final Validator
```

একটি model content বানাবে।

অন্যটি review করবে।

---

# 37. Educational Quality Checker

Future implementation:

```python
def educational_quality_score(plan):

    score = 0

    if plan.learning_objectives:
        score += 25

    if plan.scenes:
        score += 25

    if all(scene.narration for scene in plan.scenes):
        score += 25

    if all(scene.visual_description for scene in plan.scenes):
        score += 25

    return score
```

যদি:

```text
score >= 80
```

তাহলে:

```text
APPROVED
```

---

# 38. M18 Mini Project

এখন তোমার task:

### Input

```text
Explain photosynthesis to a beginner in 30 seconds.
```

System-এর output:

```text
VideoPlan
```

এর মধ্যে থাকতে হবে:

```text
topic
subject
audience
difficulty
duration
learning_objectives
teaching_strategy
scenes
```

কমপক্ষে 4 scenes:

```text
Scene 1 → What is photosynthesis?
Scene 2 → Sunlight
Scene 3 → Water + CO₂
Scene 4 → Glucose + Oxygen
```

---

# 39. আরও ভালো Mini Project

একই program-এ তিনটি prompt test করো:

### Test 1

```text
Explain binary search to a beginner in 30 seconds.
```

### Test 2

```text
Explain photosynthesis to a child in 30 seconds.
```

### Test 3

```text
Explain TCP vs UDP to a networking student in 45 seconds.
```

তারপর দেখবে:

```text
Topic
Audience
Difficulty
Learning Objectives
Teaching Strategy
Scenes
```

কীভাবে পরিবর্তিত হচ্ছে।

এটাই আসল **general-purpose educational AI**।

---

# 40. M18 Completion Checklist

M18 শেষ করার আগে এগুলো পারতে হবে:

### LLM

-  LLM architecture বুঝতে হবে
    
-  System prompt বুঝতে হবে
    
-  User prompt বুঝতে হবে
    
-  Role/Task/Context/Constraint বুঝতে হবে
    
-  Structured output বুঝতে হবে
    

### Engineering

-  `.env`
    
-  Environment variables
    
-  LLM client abstraction
    
-  Mock client
    
-  JSON parsing
    
-  Pydantic validation
    
-  Timing validation
    
-  Scene validation
    
-  Retry system
    

### Educational AI

-  Topic extraction
    
-  Audience detection
    
-  Difficulty adaptation
    
-  Learning objectives
    
-  Teaching strategy
    
-  Script generation
    
-  Scene planning
    
-  Visual instructions
    

### Architecture

সবচেয়ে গুরুত্বপূর্ণ:

```text
Prompt
 ↓
LLM
 ↓
Structured VideoPlan
 ↓
Validation
 ↓
Renderer
```

---

# 41. M18-এর Final Architecture

এখন তোমার পুরো system অনেক বেশি পরিষ্কার:

```text
                         USER
                          │
                          ▼
                   Natural Language
                          │
                          ▼
                ┌──────────────────┐
                │   LLM PLANNER    │
                │                  │
                │ Topic            │
                │ Audience         │
                │ Difficulty       │
                │ Objectives       │
                │ Strategy         │
                │ Script           │
                │ Scenes           │
                └────────┬─────────┘
                         │
                         ▼
                  STRUCTURED JSON
                         │
                         ▼
                  JSON VALIDATOR
                         │
                         ▼
                  PYDANTIC MODEL
                         │
                         ▼
                    VIDEO PLAN
                         │
             ┌───────────┼───────────┐
             ▼           ▼           ▼
          SCRIPT       VISUAL      TIMING
             │           │           │
             ▼           ▼           ▼
            TTS       MANIM/VLM    Timeline
             │           │           │
             └───────────┼───────────┘
                         ▼
                      FFmpeg
                         │
                         ▼
                  EDUCATIONAL MP4
```

## 🔥 M18-এর মূল শিক্ষা

তোমার Educational Video AI-এর **brain এখন conceptualভাবে তৈরি**:

> **User-এর natural-language request → LLM → structured educational plan → deterministic video-generation pipeline.**

আর একটা বিষয় খুব মনে রাখবে:

```text
❌ LLM → Generate entire video code

✅ LLM → Generate structured plan
                    ↓
             Deterministic Engine
                    ↓
                  Video
```

এটাই তোমার project-কে একটা সাধারণ “AI script generator” থেকে **real AI video-generation pipeline**-এ পরিণত করবে।

**Next: M19 — Prompt Engineering + Structured Generation**  
এখানে আমরা M18-এর basic prompt থেকে আরও advanced **few-shot prompting, dynamic prompts, JSON schema enforcement, self-correction, prompt templates, difficulty adaptation, scene-count control এবং reliable structured generation** তৈরি করব।


---
# M19 — Prompt Engineering + Structured Generation 🧠

M18-এ আমরা শিখেছি:

```text
User Prompt
    ↓
LLM
    ↓
JSON
    ↓
Pydantic Validation
    ↓
VideoPlan
```

M19-এ আমরা এটাকে **আরও reliable, controllable এবং production-ready** করব।

আজকের মূল লক্ষ্য:

> **একই LLM-কে ভালোভাবে নির্দেশ দিয়ে consistent educational video plan তৈরি করানো।**

---

# 1. M19-এ কী শিখব?

আজ আমরা শিখব:

1. Prompt Engineering fundamentals
2. Prompt Template
3. System Prompt vs User Prompt
4. Few-shot prompting
5. Zero-shot prompting
6. Chain-of-thought না দেখিয়ে structured reasoning approach
7. Dynamic prompt generation
8. Difficulty control
9. Duration control
10. Scene count control
11. Subject-specific prompting
12. JSON schema enforcement
13. Self-correction
14. Validation + retry
15. Prompt versioning
16. Complete M19 planner
17. Mini project

Architecture:

```text id="m19arch"
User Prompt
     ↓
Prompt Parser
     ↓
Prompt Template
     ↓
Context Injection
     ↓
LLM
     ↓
Structured JSON
     ↓
Schema Validation
     ↓
Quality Validation
     ↓
Self Correction / Retry
     ↓
Final VideoPlan
```

---

# 2. Prompt Engineering কী?

সহজভাবে:

> **LLM-কে কীভাবে instruction দিলে desired output পাওয়া যায়—সেটাই Prompt Engineering।**

উদাহরণ:

### Weak prompt

```text
Explain binary search.
```

LLM অনেক ধরনের উত্তর দিতে পারে।

### Better prompt

```text
Explain binary search to a beginner.
Use simple language.
Give one example.
Keep the explanation under 100 words.
```

### আরও ভালো

```text
You are an expert educational content planner.

Create a 30-second educational video
about binary search for a beginner.

Learning objectives:
- Define binary search
- Explain the middle element
- Explain why half of the search space is removed

Use simple language.

Return only structured JSON.
```

এখানে output অনেক বেশি predictable হবে।

---

# 3. Prompt-এর Anatomy

আমাদের Educational AI prompt হবে:

```text id="promptlayers"
ROLE
  +
TASK
  +
CONTEXT
  +
CONSTRAINTS
  +
PROCESS
  +
OUTPUT FORMAT
```

---

## ROLE

```text
You are an expert educational content planner.
```

LLM-কে তার কাজের context দেয়।

---

## TASK

```text
Create an educational video plan.
```

---

## CONTEXT

```text
Topic: Binary Search
Audience: Beginner
Subject: Computer Science
```

---

## CONSTRAINTS

```text
Duration: 30 seconds
Maximum scenes: 5
Simple language
```

---

## PROCESS

```text
First identify the learning objectives.
Then create a teaching strategy.
Then create the narration.
Then divide the narration into scenes.
Then create visual instructions.
```

---

## OUTPUT FORMAT

```text
Return only JSON.
```

---

# 4. Zero-shot Prompting

কোনো example না দিয়ে instruction দেওয়া।

```text id="zero"
Explain binary search to a beginner.

Return a structured educational video plan.
```

এটাই zero-shot।

Flow:

```text
Instruction
   ↓
LLM
   ↓
Output
```

Simple কিন্তু output variability বেশি হতে পারে।

---

# 5. Few-shot Prompting

LLM-কে example দেখিয়ে desired pattern শেখানো।

উদাহরণ:

```text id="fewshot"
Example:

Input:
Explain photosynthesis to a beginner.

Output:
{
  "topic": "Photosynthesis",
  "difficulty": "beginner",
  "teaching_strategy": "step_by_step"
}

Now create a plan for:

Explain binary search to a beginner.
```

এতে LLM বুঝতে পারে আমরা কী ধরনের output চাই।

---

# 6. Few-shot কেন গুরুত্বপূর্ণ?

ধরো আমরা চাই:

```text
scene_type
```

সবসময় এই values-এর মধ্যে হবে:

```text
definition
explanation
example
process
comparison
summary
```

LLM-কে example দিলে consistency বাড়ে।

```text
Example:

scene_type = "definition"

Example:

scene_type = "process"

Example:

scene_type = "comparison"
```

তারপর নতুন content generate করানো যায়।

---

# 7. কিন্তু একটা সমস্যা আছে

Prompt-এর মধ্যে অনেক example দিলে:

```text
Prompt
+
Examples
+
Instructions
+
Context
```

prompt বড় হয়ে যায়।

ফলে:

* token usage বাড়ে
* latency বাড়ে
* cost বাড়তে পারে

তাই production-এ carefully selected few-shot examples ব্যবহার করতে হবে।

---

# 8. Dynamic Prompt

আমাদের system-এ prompt hard-code করা যাবে না।

কারণ user যেকোনো topic দিতে পারে।

আমরা template ব্যবহার করব।

`llm/prompts.py`

```python
SYSTEM_PROMPT = """
You are an expert educational video planner.

Your task is to create accurate,
clear and visually explainable educational videos.

Always follow the requested:
- topic
- audience
- difficulty
- duration
- language
- style

Return structured JSON only.
"""
```

তারপর:

```python
def build_prompt(
    topic,
    audience,
    difficulty,
    duration,
    language,
    style
):
    return f"""
Create an educational video about:

Topic: {topic}
Audience: {audience}
Difficulty: {difficulty}
Duration: {duration} seconds
Language: {language}
Visual Style: {style}

Create:
1. Learning objectives
2. Teaching strategy
3. Narration
4. Scene breakdown
5. Visual descriptions
6. Animation instructions

Return valid structured JSON.
"""
```

এটাই dynamic prompt।

---

# 9. Prompt Template Architecture

আমাদের project-এ:

```text id="templatearch"
Prompt Template
      ↓
User Parameters
      ↓
Dynamic Prompt
      ↓
LLM
```

Example:

```python
prompt = build_prompt(
    topic="Binary Search",
    audience="beginner",
    difficulty="beginner",
    duration=30,
    language="en",
    style="clean_2d"
)
```

---

# 10. Difficulty Adaptation

এটা Educational AI-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

User বলল:

```text
Explain recursion to a child.
```

Output হওয়া উচিত:

```text
Simple analogy
Simple vocabulary
Few technical terms
```

কিন্তু:

```text
Explain recursion to a computer science student.
```

Output:

```text
Technical terminology
Base case
Recursive case
Call stack
Complexity
```

---

# 11. Difficulty Prompt

```python
DIFFICULTY_INSTRUCTIONS = {

    "beginner": """
    Use simple language.
    Avoid unnecessary technical terminology.
    Use intuitive examples and analogies.
    Explain one concept at a time.
    """,

    "intermediate": """
    Use moderate technical terminology.
    Include practical examples.
    Explain the underlying mechanism.
    """,

    "advanced": """
    Use precise technical terminology.
    Include equations, edge cases,
    complexity and implementation details
    when relevant.
    """
}
```

তারপর:

```python
difficulty_instruction = DIFFICULTY_INSTRUCTIONS[
    difficulty
]
```

---

# 12. Dynamic Difficulty Prompt

```python
def build_prompt(
    topic,
    audience,
    difficulty,
    duration,
    language,
    style
):

    difficulty_instruction = (
        DIFFICULTY_INSTRUCTIONS[difficulty]
    )

    return f"""
Topic: {topic}

Audience: {audience}

Difficulty: {difficulty}

Duration: {duration} seconds

Language: {language}

Visual Style: {style}

Difficulty Instructions:
{difficulty_instruction}

Create an educational video plan.

Return structured JSON only.
"""
```

এখন একই model বিভিন্ন learner-এর জন্য content তৈরি করতে পারবে।

---

# 13. Duration Control

এটা আমাদের project-এর খুব গুরুত্বপূর্ণ অংশ।

User:

```text
Explain binary search in 10 seconds.
```

অন্য user:

```text
Explain binary search in 5 minutes.
```

দুটোর script একই হওয়া উচিত না।

---

## Word budget

আমরা ধরছি:

```text
120–160 words/minute
```

Function:

```python
def calculate_word_budget(duration):
    minimum = int(duration * 120 / 60)
    maximum = int(duration * 160 / 60)

    return minimum, maximum
```

10 seconds:

```text
20–26 words
```

30 seconds:

```text
60–80 words
```

60 seconds:

```text
120–160 words
```

---

# 14. Prompt-এ Word Budget

```python
minimum, maximum = calculate_word_budget(duration)

prompt = f"""
The narration should contain approximately
{minimum} to {maximum} words.

Do not exceed the requested duration.
"""
```

এতে LLM-এর script duration-এর সাথে align হওয়ার সম্ভাবনা বাড়ে।

তবে মনে রাখবে:

> Word count দিয়ে exact duration guarantee করা যায় না।
> শেষ পর্যন্ত TTS audio duration দিয়ে timing verify করতে হবে।

---

# 15. Scene Count Control

ধরো:

```text
10 sec
```

তাহলে:

```text
10 scenes
```

দরকার নেই।

আমরা একটা rule করতে পারি:

```python
def calculate_scene_count(duration):

    if duration <= 15:
        return 2

    if duration <= 30:
        return 4

    if duration <= 60:
        return 6

    return 8
```

এখন:

```text
10 sec → 2 scenes
30 sec → 4 scenes
60 sec → 6 scenes
```

এটা অবশ্য fixed rule না; পরে content complexity অনুযায়ী dynamic করতে পারবে।

---

# 16. Prompt-এ Scene Limit

```python
scene_count = calculate_scene_count(duration)

prompt = f"""
Create exactly {scene_count} scenes.

Each scene must have:
- narration
- visual_description
- scene_type
- animation_instruction
"""
```

এতে scene explosion কমে।

---

# 17. Scene Types Restrict করা

LLM যেকোনো string লিখলে সমস্যা হতে পারে:

```text
scene_type = "cool_explanation"
```

আমাদের renderer বুঝবে না।

তাই allowed values:

```python
SCENE_TYPES = [
    "definition",
    "explanation",
    "example",
    "process",
    "comparison",
    "step_by_step",
    "diagram",
    "equation",
    "code",
    "algorithm",
    "chart",
    "summary"
]
```

Prompt:

```text
scene_type must be one of:

definition
explanation
example
process
comparison
step_by_step
diagram
equation
code
algorithm
chart
summary
```

---

# 18. Pydantic Enum

আরও ভালো validation করতে পারি।

```python
from enum import Enum


class SceneType(str, Enum):

    DEFINITION = "definition"
    EXPLANATION = "explanation"
    EXAMPLE = "example"
    PROCESS = "process"
    COMPARISON = "comparison"
    STEP_BY_STEP = "step_by_step"
    DIAGRAM = "diagram"
    EQUATION = "equation"
    CODE = "code"
    ALGORITHM = "algorithm"
    CHART = "chart"
    SUMMARY = "summary"
```

তারপর:

```python
class Scene(BaseModel):

    scene_id: int
    start: float
    end: float
    narration: str
    visual_description: str
    scene_type: SceneType

    on_screen_text: List[str] = Field(
        default_factory=list
    )

    animation_instruction: str = ""
```

এখন:

```text
scene_type = "random"
```

হলে validation fail করবে।

---

# 19. Structured Output-এর আসল উদ্দেশ্য

আমাদের লক্ষ্য:

```text
❌ Free-form text
```

না।

আমাদের লক্ষ্য:

```text
✅ Machine-readable structured data
```

যেমন:

```json
{
  "topic": "Recursion",
  "duration": 30,
  "scenes": []
}
```

এই JSON সরাসরি আমাদের application ব্যবহার করতে পারবে।

---

# 20. Self-Correction

LLM প্রথমবার ভুল করলে আবার নিজেকেই correction instruction দেওয়া যায়।

Flow:

```text id="selfcorrect"
Prompt
 ↓
LLM
 ↓
Invalid JSON
 ↓
Validation Error
 ↓
Correction Prompt
 ↓
LLM
 ↓
Correct JSON
```

Correction prompt:

```python
def build_correction_prompt(
    original_prompt,
    error_message
):

    return f"""
Your previous response was invalid.

Original request:
{original_prompt}

Validation error:
{error_message}

Fix the problem.

Return only valid structured JSON.
Do not include markdown.
"""
```

---

# 21. Retry System

M18-এ আমরা basic retry দেখেছি।

M19-এ এটাকে আরও ভালো করি।

```python
def generate_with_retry(
    client,
    system_prompt,
    user_prompt,
    max_retries=3
):

    current_prompt = user_prompt

    for attempt in range(max_retries):

        try:

            raw = client.generate(
                system_prompt,
                current_prompt
            )

            data = parse_json(raw)

            plan = validate_video_plan(data)

            validate_plan(plan)

            return plan

        except Exception as error:

            current_prompt = build_correction_prompt(
                user_prompt,
                str(error)
            )

    raise RuntimeError(
        "Unable to generate valid plan."
    )
```

---

# 22. Retry-এর একটা সমস্যা

প্রতিবার একই prompt পাঠালে:

```text
Attempt 1
Attempt 2
Attempt 3
```

একই ভুল আসতে পারে।

তাই error feedback দিতে হবে।

Example:

```text
Validation error:

Scene 3 end time exceeds
the total video duration.

Fix the timing.
```

LLM বুঝতে পারবে কী ঠিক করতে হবে।

---

# 23. Better Self-Correction

আরও structured correction:

```python
def build_correction_prompt(
    original_prompt,
    data,
    errors
):

    return f"""
You generated an invalid educational video plan.

Original request:
{original_prompt}

Generated plan:
{data}

Validation errors:
{errors}

Correct ONLY the invalid parts.

Requirements:
- Preserve valid information.
- Fix timing errors.
- Fix missing fields.
- Follow the schema.
- Return JSON only.
"""
```

এটা পুরো plan আবার নতুন করে generate করার চেয়ে ভালো হতে পারে।

---

# 24. Quality Rubric

শুধু JSON valid হলেই content ভালো নয়।

আমাদের quality dimensions:

```text
Accuracy
Clarity
Educational Value
Visualizability
Timing
Audience Fit
```

একটা score system:

```python
def quality_score(
    accuracy,
    clarity,
    educational_value,
    visualizability,
    timing,
    audience_fit
):

    return (
        accuracy * 0.25 +
        clarity * 0.15 +
        educational_value * 0.25 +
        visualizability * 0.15 +
        timing * 0.10 +
        audience_fit * 0.10
    )
```

---

# 25. Prompt Versioning

Production project-এ prompt change করলে output change হতে পারে।

তাই:

```text
prompts/
├── planner_v1.txt
├── planner_v2.txt
├── planner_v3.txt
```

অথবা:

```python
PROMPT_VERSION = "1.0.0"
```

Dataset-এ save:

```json
{
  "prompt_version": "1.0.0",
  "model": "model-name"
}
```

এটা future evaluation-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 26. Prompt + Model Version

আমাদের generated project metadata:

```json
{
  "project_id": "project_001",
  "model": "llm-model",
  "prompt_version": "1.0.0",
  "topic": "Binary Search",
  "duration": 30
}
```

এতে পরে বুঝতে পারবে:

> কোন model + কোন prompt দিয়ে video তৈরি হয়েছিল?

---

# 27. Subject-Specific Prompting

Educational AI general-purpose হওয়ায় subject অনুযায়ী prompt change করা উচিত।

### Computer Science

```text
Prefer:
- algorithms
- code
- diagrams
- data structures
- complexity
```

### Biology

```text
Prefer:
- biological processes
- labeled diagrams
- cause/effect
- scientific terminology
```

### Mathematics

```text
Prefer:
- equations
- step-by-step derivation
- graphs
- numerical examples
```

### History

```text
Prefer:
- timeline
- chronology
- cause/effect
- maps
```

---

# 28. Subject Configuration

```python
SUBJECT_INSTRUCTIONS = {

    "computer_science": """
    Use algorithms, code examples,
    diagrams and data structures when useful.
    """,

    "biology": """
    Use biological processes,
    labeled diagrams and scientific explanations.
    """,

    "mathematics": """
    Use equations, numerical examples,
    graphs and step-by-step derivations.
    """,

    "history": """
    Use timelines, chronology,
    events and cause-effect relationships.
    """
}
```

তারপর:

```python
subject_instruction = SUBJECT_INSTRUCTIONS.get(
    subject,
    ""
)
```

---

# 29. Complete Dynamic Prompt Builder

এখন সব একসাথে:

```python
def build_educational_prompt(
    topic,
    subject,
    audience,
    difficulty,
    duration,
    language,
    style
):

    minimum_words, maximum_words = (
        calculate_word_budget(duration)
    )

    scene_count = calculate_scene_count(
        duration
    )

    difficulty_instruction = (
        DIFFICULTY_INSTRUCTIONS[difficulty]
    )

    subject_instruction = (
        SUBJECT_INSTRUCTIONS.get(
            subject,
            ""
        )
    )

    return f"""
Create an educational video plan.

TOPIC:
{topic}

SUBJECT:
{subject}

AUDIENCE:
{audience}

DIFFICULTY:
{difficulty}

LANGUAGE:
{language}

VISUAL STYLE:
{style}

DURATION:
{duration} seconds

TARGET WORD COUNT:
{minimum_words}-{maximum_words} words

NUMBER OF SCENES:
Exactly {scene_count}

DIFFICULTY INSTRUCTIONS:
{difficulty_instruction}

SUBJECT INSTRUCTIONS:
{subject_instruction}

TASK:

1. Identify the core concept.
2. Create learning objectives.
3. Choose a teaching strategy.
4. Write concise narration.
5. Divide the narration into scenes.
6. Create visual descriptions.
7. Create animation instructions.
8. Add useful on-screen text.

CONSTRAINTS:

- Keep the content educationally accurate.
- Use language appropriate for the audience.
- Do not invent facts.
- Do not exceed the requested duration.
- Every scene must have narration.
- Every scene must have a visual description.
- Scene timing must not overlap.
- Scene timing must stay within the video duration.

Return JSON only.
"""
```

এটা M19-এর সবচেয়ে গুরুত্বপূর্ণ code-এর একটি।

---

# 30. Example — Binary Search

Input:

```text
Explain binary search to a beginner
in 30 seconds.
```

Parameters:

```python
topic = "Binary Search"
subject = "Computer Science"
audience = "beginner"
difficulty = "beginner"
duration = 30
language = "en"
style = "clean_2d"
```

LLM-এর expected structure:

```json
{
  "topic": "Binary Search",
  "subject": "Computer Science",
  "audience": "beginner",
  "difficulty": "beginner",
  "language": "en",
  "duration": 30,
  "learning_objectives": [
    "Understand binary search",
    "Understand the middle element",
    "Understand elimination of half the search space"
  ],
  "teaching_strategy": "step_by_step",
  "scenes": []
}
```

---

# 31. Example — Biology

Input:

```text
Explain photosynthesis to a child
in 30 seconds.
```

LLM should adapt:

```text
Difficulty = beginner
Teaching strategy = analogy
Visual = plant + sun + water + CO2
```

Potential scenes:

```text
Scene 1 → Plant
Scene 2 → Sunlight
Scene 3 → Water + CO₂
Scene 4 → Food + Oxygen
```

---

# 32. Example — Mathematics

Input:

```text
Explain Pythagorean theorem
to a high school student in 45 seconds.
```

Planner should recognize:

```text
Subject = Mathematics
Visual = right triangle
Visual = equation
Visual = numerical example
```

Scene structure:

```text
Scene 1 → theorem
Scene 2 → triangle
Scene 3 → equation
Scene 4 → example
Scene 5 → summary
```

এখানে একই LLM, কিন্তু prompt context বদলে যাচ্ছে।

---

# 33. M19-এর Important Architecture

```text id="m19full"
                    USER
                     │
                     ▼
              Natural Prompt
                     │
                     ▼
              Prompt Parser
                     │
                     ▼
          ┌────────────────────┐
          │ Prompt Controller  │
          └─────────┬──────────┘
                    │
        ┌───────────┼────────────┐
        ▼           ▼            ▼
     Subject     Difficulty    Duration
        │           │            │
        └───────────┼────────────┘
                    ▼
             Dynamic Prompt
                    │
                    ▼
                   LLM
                    │
                    ▼
             Structured JSON
                    │
                    ▼
                Pydantic
                    │
                    ▼
             Quality Validator
                    │
            ┌───────┴───────┐
            │               │
          Valid           Invalid
            │               │
            ▼               ▼
       VideoPlan         Correction
                            │
                            ▼
                           LLM
```

---

# 34. M19 Complete Folder

```text
educational_video_ai/
│
├── app/
│   ├── config.py
│   ├── schemas.py
│   └── pipeline.py
│
├── llm/
│   ├── __init__.py
│   ├── client.py
│   ├── prompts.py
│   ├── planner.py
│   ├── parser.py
│   ├── validator.py
│   ├── retry.py
│   └── quality.py
│
├── planner/
│   ├── educational_planner.py
│   ├── script_generator.py
│   └── scene_planner.py
│
├── renderer/
├── tts/
├── subtitle/
├── timeline/
├── composer/
│
├── prompts/
│   ├── planner_v1.txt
│   └── planner_v2.txt
│
├── projects/
├── output/
│
└── scripts/
    └── test_planner.py
```

---

# 35. M19 Mini Project

এখন তোমার project task:

একটি **Universal Educational Prompt Engine** বানাও।

User শুধু লিখবে:

```text
Explain recursion to a beginner in 30 seconds.
```

System automatically বের করবে:

```text
topic
subject
audience
difficulty
duration
language
style
word budget
scene count
```

তারপর dynamic prompt বানাবে।

---

# 36. Mini Project Input

Test করো:

### Test 1

```text
Explain binary search to a beginner in 30 seconds.
```

### Test 2

```text
Explain photosynthesis to a child in 45 seconds.
```

### Test 3

```text
Explain TCP vs UDP to an intermediate networking student in 60 seconds.
```

### Test 4

```text
Explain the Pythagorean theorem to a high school student in 45 seconds.
```

---

# 37. তুমি কী observe করবে?

একই LLM:

```text
Binary Search
```

→ algorithm diagram

```text
Photosynthesis
```

→ biological process

```text
TCP vs UDP
```

→ comparison diagram

```text
Pythagorean theorem
```

→ equation + triangle

অর্থাৎ:

> **Prompt Engineering-এর মাধ্যমে একই AI engine বিভিন্ন educational domain-এর জন্য adaptive হয়ে যাচ্ছে।**

---

# 38. Common Mistakes

### ❌ Mistake 1

একটা giant prompt বানানো।

```text
5000 lines prompt
```

এটা maintain করা কঠিন।

Better:

```text
Base Prompt
+
Subject Prompt
+
Difficulty Prompt
+
Format Prompt
```

---

### ❌ Mistake 2

LLM output blindly trust করা।

```python
plan = llm.generate(...)
render(plan)
```

❌

Better:

```text
LLM
 ↓
Parse
 ↓
Validate
 ↓
Quality Check
 ↓
Render
```

---

### ❌ Mistake 3

LLM-generated timing blindly use করা।

সবসময় verify:

```python
validate_scene_timing()
```

---

### ❌ Mistake 4

Prompt-এর মাধ্যমে exact behavior guarantee করা।

Prompt helpful, কিন্তু guarantee না।

তাই:

```text
Prompt
+
Schema
+
Validation
+
Retry
+
Evaluation
```

সব একসাথে দরকার।

---

# 39. M19-এর Golden Architecture

এটা মনে রাখবে:

```text
        PROMPT
          ↓
       CONTEXT
          ↓
      CONSTRAINTS
          ↓
          LLM
          ↓
    STRUCTURED OUTPUT
          ↓
       SCHEMA
          ↓
      VALIDATION
          ↓
     QUALITY CHECK
          ↓
    SELF-CORRECTION
          ↓
      VIDEO PLAN
```

---

# 40. M19 Completion Test

নিজেকে এই প্রশ্নগুলোর উত্তর দিতে পারলে M19 complete:

### Prompt Engineering

* [ ] Prompt Engineering কী?
* [ ] Zero-shot কী?
* [ ] Few-shot কী?
* [ ] Dynamic prompt কী?
* [ ] System prompt কী?
* [ ] User prompt কী?
* [ ] Prompt template কী?

### Educational Control

* [ ] Difficulty control
* [ ] Audience control
* [ ] Duration control
* [ ] Word budget
* [ ] Scene count
* [ ] Subject-specific instructions
* [ ] Teaching strategy

### Structured Generation

* [ ] JSON output
* [ ] Pydantic
* [ ] Enum validation
* [ ] Timing validation
* [ ] Scene validation
* [ ] Quality validation
* [ ] Retry
* [ ] Self-correction

### Production

* [ ] Prompt versioning
* [ ] Model version tracking
* [ ] Validation before rendering
* [ ] LLM abstraction

---

# 🔥 M19-এর মূল শিক্ষা

M18-এ আমরা বানিয়েছিলাম:

```text
LLM → VideoPlan
```

M19-এ এটাকে বানালাম:

```text
User Prompt
     ↓
Prompt Controller
     ↓
Dynamic Context
     ↓
Subject Rules
     ↓
Difficulty Rules
     ↓
Duration Rules
     ↓
Scene Rules
     ↓
LLM
     ↓
Structured JSON
     ↓
Pydantic
     ↓
Quality Validation
     ↓
Self-Correction
     ↓
Reliable VideoPlan
```

এখন তোমার Educational Video AI আর শুধু **LLM দিয়ে text generate করা system নয়**।

এটা ধীরে ধীরে হচ্ছে:

> **A controllable AI content-generation system যেখানে LLM planning করে, structured data তৈরি করে, আর deterministic pipeline সেই plan execute করে।**

### পরবর্তী ধাপ — **M20: VLM-based Visual Understanding**

সেখানে আমরা system-কে “চোখ” দেব:

```text
Educational Video
       ↓
Frames
       ↓
VLM
       ↓
What is happening visually?
       ↓
Objects
Actions
Text
Diagram
Concept
Scene Type
       ↓
Visual Understanding JSON
       ↓
LLM
       ↓
Educational Scene Plan
```

অর্থাৎ M20 থেকে তোমার AI শুধু **কী বলা হচ্ছে** তা নয়, **স্ক্রিনে কী দেখানো হচ্ছে** সেটাও বুঝতে পারবে।

---
# M20 — VLM-Based Visual Understanding 👁️🧠

M19 পর্যন্ত আমরা তোমার AI-কে **Brain** দিয়েছি:

```text
User Prompt
     ↓
LLM
     ↓
Educational Plan
     ↓
Structured JSON
```

এখন M20-তে আমরা AI-কে **Eyes** দেব।

> **VLM = Vision-Language Model**
> অর্থাৎ এমন model যা image/video-এর visual information এবং language—দুটো একসাথে বুঝতে পারে।

---

# 1. M20-এ আমরা কী বানাব?

আমাদের লক্ষ্য:

```text
Educational Video
       ↓
Video Frames
       ↓
VLM
       ↓
Visual Understanding
       ↓
Structured JSON
```

যেমন ভিডিওতে দেখা যাচ্ছে:

```text
┌──────────────────────────────┐
│        Binary Search         │
│                              │
│  10  20  30  40  50          │
│           ↑                  │
│         middle               │
└──────────────────────────────┘
```

VLM বুঝবে:

```json
{
  "objects": [
    "array",
    "numbers",
    "highlight"
  ],
  "text": [
    "Binary Search"
  ],
  "action": "middle element is highlighted",
  "concept": "binary search",
  "scene_type": "algorithm_diagram"
}
```

---

# 2. কেন VLM দরকার?

শুধু Whisper ব্যবহার করলে:

```text
Whisper
 ↓
"What is being said?"
```

উদাহরণ:

```text
"The middle element is checked first."
```

কিন্তু screen-এ আসলে কী আছে সেটা Whisper জানে না।

অন্যদিকে VLM:

```text
VLM
 ↓
"What is being shown?"
```

দেখতে পারে:

```text
Array
Middle element
Highlight
Text
Diagram
```

তাই:

```text
Whisper = Ears 👂
VLM = Eyes 👁️
LLM = Brain 🧠
Renderer = Hands ✋
```

---

# 3. M20 Architecture

```text
                    VIDEO
                      │
                      ▼
               Frame Extraction
                      │
                      ▼
              Sampled Frames
                      │
             ┌────────┴────────┐
             │                 │
             ▼                 ▼
          Whisper             VLM
             │                 │
             ▼                 ▼
        Transcript       Visual Analysis
             │                 │
             └────────┬────────┘
                      ▼
              Multimodal LLM
                      │
                      ▼
            Educational Scene
                  Understanding
                      │
                      ▼
               Structured JSON
```

---

# 4. VLM বনাম Computer Vision

এগুলো এক জিনিস না।

### Traditional Computer Vision

```text
Image
 ↓
Object Detection
 ↓
"person"
"car"
"chair"
```

### VLM

```text
Image
+
Question
 ↓
Understanding
 ↓
"The teacher is explaining binary search
using a sorted array."
```

অর্থাৎ VLM visual information-এর সাথে language reasoning করতে পারে।

---

# 5. VLM কী কী করতে পারে?

আমাদের Educational Video AI-এর জন্য:

### Object Recognition

```text
array
tree
graph
person
whiteboard
```

### Text Recognition

```text
Binary Search
O(log n)
TCP
UDP
```

### Scene Understanding

```text
teacher explaining
diagram showing process
code displayed
equation displayed
```

### Visual Question Answering

```text
What is highlighted?

Which element is the teacher pointing at?

What does this diagram represent?
```

### Educational Understanding

```text
What concept is being illustrated?

What is the important visual teaching point?

Is this visual consistent with the narration?
```

---

# 6. আমাদের Input

ধরো video:

```text
videos/binary_search.mp4
```

প্রথমে frames:

```text
frames/
├── frame_00001.jpg
├── frame_00002.jpg
├── frame_00003.jpg
├── frame_00004.jpg
└── ...
```

কিন্তু প্রতি frame VLM-এ পাঠাব না।

---

# 7. Frame Sampling

ধরো video:

```text
60 seconds
30 FPS
```

Total frames:

```text
60 × 30 = 1800
```

সব 1800 frame VLM-এ পাঠানো inefficient।

বরং:

```text
Every 2 seconds
```

মানে প্রায়:

```text
30 frames
```

এটা অনেক practical।

---

# 8. Frame Extraction

M17-এর function ব্যবহার করতে পারো:

```python
import cv2
from pathlib import Path


def extract_frames(
    video_path,
    output_dir,
    interval=2
):

    output_dir = Path(output_dir)
    output_dir.mkdir(
        parents=True,
        exist_ok=True
    )

    cap = cv2.VideoCapture(video_path)

    fps = cap.get(
        cv2.CAP_PROP_FPS
    )

    if fps <= 0:
        raise ValueError(
            "Invalid FPS"
        )

    frame_interval = int(
        fps * interval
    )

    frame_index = 0
    saved_index = 0

    while True:

        ret, frame = cap.read()

        if not ret:
            break

        if frame_index % frame_interval == 0:

            path = (
                output_dir /
                f"frame_{saved_index:05d}.jpg"
            )

            cv2.imwrite(
                str(path),
                frame
            )

            saved_index += 1

        frame_index += 1

    cap.release()
```

---

# 9. VLM Input

একটি VLM-কে শুধু image দিলে:

```text
Image
 ↓
VLM
```

কিন্তু আমরা আরও ভালো ফল চাই:

```text
Image
+
Instruction
 ↓
VLM
```

যেমন:

```text
Analyze this educational frame.

Identify:
1. Important objects
2. Visible text
3. Main action
4. Educational concept
5. Scene type
6. Important visual teaching point
```

---

# 10. Generic VLM Prompt

`vlm/prompts.py`

```python
SYSTEM_PROMPT = """
You are an expert visual analyst
for an educational video generation system.

Analyze educational video frames carefully.

Identify:
- objects
- visible text
- actions
- diagrams
- concepts
- scene type
- visual teaching point

Do not invent information that is
not visually supported by the image.

Return structured JSON.
"""
```

---

# 11. User Prompt

```python
def build_visual_prompt():

    return """
Analyze this frame.

Return:

{
    "objects": [],
    "visible_text": [],
    "action": "",
    "concept": "",
    "scene_type": "",
    "visual_teaching_point": "",
    "description": ""
}

Return JSON only.
"""
```

---

# 12. VLM Schema

`vlm/schema.py`

```python
from typing import List
from pydantic import BaseModel


class VisualAnalysis(BaseModel):

    objects: List[str]

    visible_text: List[str]

    action: str

    concept: str

    scene_type: str

    visual_teaching_point: str

    description: str
```

এখন:

```text
VLM output
   ↓
JSON
   ↓
Pydantic
   ↓
VisualAnalysis
```

---

# 13. Example Output

Input image:

```text
Sorted array:
10 20 30 40 50

30 highlighted
```

VLM output:

```json
{
  "objects": [
    "array",
    "numbers",
    "highlight"
  ],
  "visible_text": [
    "10",
    "20",
    "30",
    "40",
    "50"
  ],
  "action": "middle element is highlighted",
  "concept": "binary search",
  "scene_type": "algorithm_diagram",
  "visual_teaching_point": "The middle element is checked first.",
  "description": "A sorted array is displayed with the middle element highlighted."
}
```

---

# 14. VLM-এর সবচেয়ে গুরুত্বপূর্ণ কাজ

আমাদের system-এ VLM শুধু:

```text
"What objects are visible?"
```

করবে না।

আমরা চাই:

```text
"What is the educational meaning of this visual?"
```

এটা খুব গুরুত্বপূর্ণ difference।

---

# 15. Visual Description বনাম Educational Meaning

ধরো image:

```text
Teacher
Whiteboard
Array
Arrow
```

Traditional caption:

```text
"A teacher is standing beside a whiteboard."
```

Educational VLM output:

```text
"The teacher is explaining binary search
using a sorted array and highlighting
the middle element."
```

দ্বিতীয়টা আমাদের system-এর জন্য বেশি useful।

---

# 16. Scene Type Classification

VLM scene type classify করবে।

Allowed types:

```python
SCENE_TYPES = [
    "talking_head",
    "diagram",
    "algorithm",
    "code",
    "equation",
    "chart",
    "process",
    "comparison",
    "timeline",
    "real_world",
    "text",
    "animation",
    "summary"
]
```

এটা পরে renderer-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 17. Scene Type → Renderer

আমাদের architecture:

```text
VLM
 ↓
scene_type
 ↓
Renderer
```

যেমন:

```text
algorithm
   ↓
Array Renderer
```

```text
equation
   ↓
MathTex Renderer
```

```text
flowchart
   ↓
Flowchart Renderer
```

```text
chart
   ↓
Chart Renderer
```

এখানে M12-এর generic renderer কাজে লাগবে।

---

# 18. VLM + Whisper

এখন আসল শক্তিশালী architecture।

Whisper:

```text
At 10 sec:

"We compare the target with
the middle element."
```

VLM:

```text
At 10 sec:

Array visible.
Middle element highlighted.
```

দুটো combine করলে:

```text
Narration:
"We compare the target with
the middle element."

Visual:
"Middle element is highlighted."
```

তারপর multimodal understanding:

```text
Teaching Point:
Binary search compares the target
with the middle element.
```

---

# 19. Timestamp Alignment

এটা M20-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

ধরো Whisper:

```json
{
  "start": 8.0,
  "end": 12.0,
  "text": "We compare the target with the middle element."
}
```

Frame:

```json
{
  "timestamp": 10.0,
  "description": "Middle element is highlighted."
}
```

তাহলে:

```text
8 sec ─────────── 12 sec
        ↑
      Frame
       10s
```

আমরা frame-টাকে narration segment-এর সাথে associate করতে পারি।

---

# 20. Timestamp Matching Function

```python
def find_visual_frames(
    start,
    end,
    frames
):

    matched = []

    for frame in frames:

        timestamp = frame["timestamp"]

        if start <= timestamp <= end:
            matched.append(frame)

    return matched
```

Example:

```python
frames = [
    {
        "timestamp": 4,
        "description": "Array"
    },
    {
        "timestamp": 10,
        "description": "Middle highlighted"
    },
    {
        "timestamp": 16,
        "description": "Left half removed"
    }
]
```

Narration:

```text
8 → 12
```

Result:

```python
[
    {
        "timestamp": 10,
        "description": "Middle highlighted"
    }
]
```

---

# 21. Multimodal Scene Object

এখন আমরা একটা combined structure বানাব।

```python
class MultimodalScene(BaseModel):

    scene_id: int

    start: float
    end: float

    narration: str

    visual_analysis: List[
        VisualAnalysis
    ]

    concept: str

    learning_point: str
```

এটা হবে:

```text
Whisper
+
VLM
 ↓
MultimodalScene
```

---

# 22. Full Multimodal Flow

```text
                    VIDEO
                      │
             ┌────────┴────────┐
             ▼                 ▼
          AUDIO              FRAMES
             │                 │
             ▼                 ▼
         Whisper              VLM
             │                 │
             ▼                 ▼
       Transcript        Visual Analysis
             │                 │
             └────────┬────────┘
                      ▼
               Timestamp Match
                      │
                      ▼
              Multimodal Scene
                      │
                      ▼
                     LLM
                      │
                      ▼
             Educational Meaning
```

---

# 23. VLM Client Abstraction

M18-এর LLM architecture-এর মতো VLM-এর জন্যও abstraction বানাব।

`vlm/client.py`

```python
from abc import ABC, abstractmethod


class VLMClient(ABC):

    @abstractmethod
    def analyze_image(
        self,
        image_path,
        prompt
    ):
        pass
```

---

# 24. Mock VLM

Development-এর জন্য:

```python
class MockVLMClient(VLMClient):

    def analyze_image(
        self,
        image_path,
        prompt
    ):

        return """
        {
            "objects": [
                "array",
                "numbers",
                "highlight"
            ],
            "visible_text": [
                "10",
                "20",
                "30",
                "40",
                "50"
            ],
            "action": "middle element is highlighted",
            "concept": "binary search",
            "scene_type": "algorithm",
            "visual_teaching_point":
                "The middle element is checked first.",
            "description":
                "A sorted array is displayed."
        }
        """
```

এতে real VLM ছাড়াই pipeline test করতে পারবে।

---

# 25. VLM Analyzer

`vlm/analyzer.py`

```python
from vlm.prompts import (
    SYSTEM_PROMPT,
    build_visual_prompt
)

from vlm.schema import VisualAnalysis
from llm.parser import parse_json


class VisualAnalyzer:

    def __init__(self, client):
        self.client = client

    def analyze(self, image_path):

        prompt = build_visual_prompt()

        raw = self.client.analyze_image(
            image_path,
            prompt
        )

        data = parse_json(raw)

        return VisualAnalysis.model_validate(
            data
        )
```

---

# 26. Multiple Frames

একটা scene-এর multiple frame থাকতে পারে।

```python
def analyze_frames(
    analyzer,
    frames
):

    results = []

    for frame in frames:

        analysis = analyzer.analyze(
            frame["path"]
        )

        results.append({
            "timestamp": frame["timestamp"],
            "analysis": analysis
        })

    return results
```

---

# 27. কেন Multiple Frames?

একটি frame misleading হতে পারে।

ধরো:

```text
Frame 1 → Array
Frame 2 → Middle highlighted
Frame 3 → Half removed
```

একসাথে দেখলে sequence বোঝা যায়।

```text
Frame 1
  ↓
Frame 2
  ↓
Frame 3
  ↓
Visual Evolution
```

---

# 28. Temporal Understanding

এখন আমরা একটা গুরুত্বপূর্ণ concept-এ আসি:

> **একটি image বুঝা এবং video-এর পরিবর্তন বুঝা এক জিনিস নয়।**

Frame:

```text
10s → Array
```

Frame:

```text
12s → Middle highlighted
```

Frame:

```text
14s → Half removed
```

Sequence:

```text
Array
 ↓
Middle selection
 ↓
Half elimination
```

এটাই temporal understanding।

---

# 29. Frame Difference

Basic computer vision দিয়ে পরিবর্তন detect করা যায়।

```python
import cv2


def frame_difference(
    frame1,
    frame2
):

    diff = cv2.absdiff(
        frame1,
        frame2
    )

    gray = cv2.cvtColor(
        diff,
        cv2.COLOR_BGR2GRAY
    )

    return gray.mean()
```

যদি difference অনেক বেশি হয়:

```text
Potential visual transition
```

এটা scene detection-এ সাহায্য করতে পারে।

---

# 30. VLM + Frame Difference

Advanced architecture:

```text
Video
 ↓
Frame Sampling
 ↓
Frame Difference
 ↓
Candidate Scene Boundaries
 ↓
VLM
 ↓
Visual Understanding
```

এতে প্রতিটি frame VLM-এ পাঠানোর প্রয়োজন কমে।

---

# 31. Important Optimization

ধরো:

```text
10-minute video
```

Every 2 seconds:

```text
300 frames
```

প্রতি frame VLM call করলে expensive হতে পারে।

Better:

```text
Video
 ↓
Cheap CV filtering
 ↓
Important frames
 ↓
VLM
```

এটা production-এ অনেক useful।

---

# 32. Smart Frame Sampling

Strategy:

```text
Every 2 sec
      ↓
Candidate frames
      ↓
Remove near-duplicates
      ↓
Scene change detection
      ↓
Important frames
      ↓
VLM
```

---

# 33. Duplicate Frame Detection

একই ধরনের frame বারবার পাঠানোর দরকার নেই।

Simple approach:

```python
def is_similar(
    score,
    threshold=5
):

    return score < threshold
```

Production-এ ব্যবহার করতে পারো:

* perceptual hash
* CLIP embeddings
* image embeddings
* cosine similarity

---

# 34. OCR + VLM

Educational videos-এ screen text খুব গুরুত্বপূর্ণ।

যেমন:

```text
O(log n)
Binary Search
TCP
UDP
F = ma
```

তাই future pipeline:

```text
Frame
 ↓
OCR
 ↓
Text
 +
VLM
 ↓
Visual Understanding
```

VLM নিজেও visible text বুঝতে পারে, কিন্তু dedicated OCR কিছু ক্ষেত্রে বেশি reliable হতে পারে।

---

# 35. Educational Visual Consistency

এখন সবচেয়ে powerful feature:

Whisper বলছে:

```text
"The middle element is selected."
```

VLM বলছে:

```text
"Left element is highlighted."
```

Mismatch!

```text
Narration ≠ Visual
```

System flag করবে:

```text
⚠ Visual inconsistency
```

এটা educational quality control-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 36. Consistency Checker

```python
def check_consistency(
    narration,
    visual_description
):

    # Future:
    # use LLM/VLM semantic comparison

    return {
        "consistent": True,
        "confidence": 0.91
    }
```

Future-এ এখানে multimodal LLM ব্যবহার করা যাবে।

---

# 37. Visual → Educational Scene JSON

শেষে M20-এর desired output:

```json
{
  "scene_id": 3,
  "start": 8,
  "end": 14,

  "narration": "We compare the target with the middle element.",

  "visual": {
    "objects": [
      "array",
      "middle_element",
      "highlight"
    ],

    "visible_text": [
      "10",
      "20",
      "30",
      "40",
      "50"
    ],

    "action": "middle element is highlighted",

    "scene_type": "algorithm",

    "description":
      "A sorted array is shown with the middle element highlighted."
  },

  "concept": "Binary Search",

  "learning_point":
    "Binary search checks the middle element first."
}
```

এই JSON আবার M19 LLM-এর কাছে যেতে পারে।

---

# 38. M20 + M19 Integration

এখন architecture অনেক powerful:

```text
                    USER
                     │
                     ▼
                  Prompt
                     │
                     ▼
                    LLM
                     │
                     ▼
                Video Plan
                     │
                     │
             Existing Video
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
       Whisper                  VLM
          │                     │
          ▼                     ▼
    Narration               Visual Data
          │                     │
          └──────────┬──────────┘
                     ▼
              Multimodal LLM
                     │
                     ▼
            Scene Understanding
                     │
                     ▼
             Visual Plan JSON
                     │
                     ▼
              M11/M12 Renderer
```

---

# 39. VLM-এর তিনটি Level

তোমার project-এ VLM development তিন ধাপে করো।

### Level 1 — Image Understanding

```text
Image
 ↓
VLM
 ↓
Description
```

### Level 2 — Educational Understanding

```text
Image
+
Educational Prompt
 ↓
VLM
 ↓
Concept
Learning Point
Scene Type
```

### Level 3 — Multimodal Understanding

```text
Image
+
Transcript
+
Timestamp
 ↓
VLM/MLLM
 ↓
Educational Scene
```

তৃতীয়টাই আমাদের final goal।

---

# 40. কোন Model ব্যবহার করবে?

M20-এর architecture **model-independent** রাখবে।

তুমি বিভিন্ন pretrained VLM ব্যবহার করতে পারো, যেমন:

```text
BLIP
LLaVA-family
Qwen-VL-family
InternVL-family
Gemma vision-capable models
```

Exact model selection তোমার GPU, VRAM, speed এবং license-এর উপর নির্ভর করবে।

তোমার architecture যেন model-এর উপর hard-code না হয়।

---

# 41. Local VLM Architecture

যদি local GPU থাকে:

```text
Video
 ↓
Frames
 ↓
Local VLM
 ↓
JSON
```

তাহলে API cost কমবে।

কিন্তু দরকার:

```text
GPU VRAM
Model storage
Inference optimization
```

---

# 42. Cloud VLM Architecture

```text
Video
 ↓
Frames
 ↓
Cloud VLM API
 ↓
JSON
```

Advantages:

* সহজ setup
* powerful model
* GPU নিজের লাগবে না

Disadvantages:

* API cost
* network latency
* data/privacy considerations
* rate limits

---

# 43. M20-এ এখনই Fine-tuning নয়

খুব গুরুত্বপূর্ণ।

এখন:

```text
❌ Train VLM from scratch
```

করবে না।

বরং:

```text
Pretrained VLM
      ↓
Prompt
      ↓
Structured Output
```

প্রথমে pipeline validate করো।

Fine-tuning পরে:

```text
M23 → LoRA / PEFT
M24 → Educational Style Fine-tuning
```

---

# 44. M20 Mini Project

এখন একটি ছোট project বানাও:

```text
binary_search.mp4
       ↓
Frame extraction
       ↓
5–10 frames
       ↓
VLM
       ↓
VisualAnalysis JSON
```

প্রতিটি frame-এর জন্য:

```json
{
  "timestamp": 10,
  "objects": [],
  "visible_text": [],
  "action": "",
  "concept": "",
  "scene_type": "",
  "visual_teaching_point": "",
  "description": ""
}
```

---

# 45. তারপর Whisper যোগ করো

Pipeline:

```text
binary_search.mp4
       │
       ├────→ Whisper
       │        ↓
       │     transcript
       │
       └────→ Frames
                ↓
               VLM
                ↓
          visual analysis
```

তারপর timestamp match:

```text
Transcript 8–12 sec
        +
Frame 10 sec
        ↓
Scene
```

---

# 46. Mini Project Output

শেষে এমন JSON তৈরি করবে:

```json
{
  "scene_id": 1,
  "start": 8,
  "end": 12,

  "narration":
    "We compare the target with the middle element.",

  "visual_description":
    "The middle element of a sorted array is highlighted.",

  "concept":
    "Binary Search",

  "learning_point":
    "The middle element is checked first.",

  "scene_type":
    "algorithm",

  "visual_elements": [
    "array",
    "middle_element",
    "highlight"
  ]
}
```

---

# 47. M20 Common Errors

## ❌ Error 1 — Every frame VLM-এ পাঠানো

```text
1000 frames
 ↓
1000 VLM calls
```

খুব inefficient।

Better:

```text
Sampling
+
Deduplication
+
Scene detection
```

---

## ❌ Error 2 — VLM output trust করা

VLM-ও ভুল করতে পারে।

তাই:

```text
VLM
 ↓
JSON
 ↓
Pydantic
 ↓
Validation
```

---

## ❌ Error 3 — শুধু image captioning

আমাদের দরকার:

```text
Visual description
+
Educational meaning
```

---

## ❌ Error 4 — Timestamp ignore করা

```text
Frame
+
Transcript
```

কিন্তু timestamp ছাড়া relationship দুর্বল।

Always:

```text
timestamp
```

রাখবে।

---

## ❌ Error 5 — Scene boundary ভুল

একটি scene:

```text
0–5 sec
```

পরেরটি:

```text
5–10 sec
```

overlap বা gap হলে timeline problem হতে পারে।

M13 validator ব্যবহার করবে।

---

# 48. M20 Final Architecture

তোমার Educational Video AI এখন:

```text
                         USER
                          │
                          ▼
                    User Prompt
                          │
                          ▼
                         LLM
                          │
                          ▼
                     Video Plan
                          │
                          │
                ┌─────────┴─────────┐
                │ Existing Video   │
                └─────────┬─────────┘
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
           AUDIO                    VIDEO
              │                       │
              ▼                       ▼
          Whisper                  Frames
              │                       │
              ▼                       ▼
        Transcript                   VLM
              │                       │
              │                       ▼
              │                Visual Analysis
              │                       │
              └───────────┬───────────┘
                          ▼
                  Timestamp Matching
                          │
                          ▼
                 Multimodal Understanding
                          │
                          ▼
                    Scene JSON
                          │
                          ▼
                  Educational Validation
                          │
                          ▼
                    Visual Planning
                          │
                          ▼
                    M11 / M12
                          │
                          ▼
                        TTS
                          │
                          ▼
                     Subtitle
                          │
                          ▼
                       FFmpeg
                          │
                          ▼
                   FINAL EDUCATIONAL
                        VIDEO
```

---

# 49. M20 Completion Checklist

### VLM Basics

* [ ] VLM কী বুঝতে হবে
* [ ] Vision + Language বুঝতে হবে
* [ ] Image understanding
* [ ] VQA
* [ ] Visual reasoning
* [ ] Scene understanding

### Video Understanding

* [ ] Frame sampling
* [ ] Timestamp
* [ ] Multiple frame analysis
* [ ] Temporal understanding
* [ ] Scene boundary
* [ ] Duplicate frame reduction

### Educational Understanding

* [ ] Objects
* [ ] Visible text
* [ ] Actions
* [ ] Concept
* [ ] Learning point
* [ ] Scene type
* [ ] Visual teaching point

### Multimodal

* [ ] Whisper + VLM
* [ ] Timestamp alignment
* [ ] Narration + visual combination
* [ ] Visual consistency checking

### Engineering

* [ ] VLM abstraction
* [ ] Mock VLM
* [ ] JSON parser
* [ ] Pydantic validation
* [ ] Retry
* [ ] Model-independent architecture

---

# 🔥 M20-এর মূল শিক্ষা

এখন তোমার AI-এর তিনটা core capability দাঁড়িয়েছে:

```text
        👂 EAR
       Whisper
          │
          ▼
    What is being said?


        👁️ EYES
        VLM
          │
          ▼
    What is being shown?


        🧠 BRAIN
        LLM
          │
          ▼
    How should it be taught?
```

তারপর:

```text
        ✋ HANDS
   Manim / Renderer
          │
          ▼
      Create Video
```

সব মিলিয়ে:

```text
Whisper
   +
VLM
   +
LLM
   +
Renderer
   +
TTS
   +
FFmpeg
      ↓
Educational Video AI
```

### পরবর্তী ধাপ — **M21: Image Generation Integration**

M20-এ AI শিখল **ভিডিওতে কী দেখা যাচ্ছে**।

M21-এ AI শিখবে **নিজে নতুন visual তৈরি করতে**:

```text
Educational Scene JSON
        ↓
Image Prompt
        ↓
Image Generation Model
        ↓
Educational Illustration
        ↓
Animation / Composition
        ↓
Video
```

অর্থাৎ M21 থেকে তোমার system শুধু Manim-এর predefined shapes ব্যবহার করবে না—প্রয়োজনে **AI-generated illustrations, diagrams, backgrounds এবং educational visual assets**-ও তৈরি করতে পারবে।

----
