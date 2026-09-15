# M6 — Pretrained Vision Model Integration

M5-এ আমরা শিখেছি:

```text
Video
 ↓
Frames
 ↓
Vision Model
 ↓
Visual Description
```

M6-এ আমরা এটাকে **actual AI pipeline**-এ নিয়ে যাব।

আজকের লক্ষ্য:

```text
Image
 ↓
Pretrained Vision Model
 ↓
Prompt
 ↓
AI Understanding
 ↓
Structured JSON
 ↓
vision/video_001_vision.json
```

---

# 1. M6-এ কী শিখব?

আজ আমরা 10টি milestone cover করব:

1. Pretrained model কী
2. Vision Encoder কী
3. Vision-Language Model কীভাবে কাজ করে
4. Hugging Face ecosystem
5. Image processor
6. Image → model
7. Prompt → model
8. Batch frame analysis
9. Structured visual JSON
10. Whisper + Vision integration

---

# 2. Pretrained Model কেন?

আমরা যদি শুরু থেকে একটি Vision Model train করি:

```text
Millions of images
+
Huge GPU
+
Weeks/months training
```

এটা আমাদের project-এর জন্য unnecessary।

Instead:

```text
Pretrained VLM
       ↓
Already learned visual patterns
       ↓
Our educational dataset
       ↓
Later LoRA fine-tuning
```

এটাই practical approach।

---

# 3. Hugging Face

আমাদের project-এ Hugging Face ecosystem খুব গুরুত্বপূর্ণ।

এখানে পাওয়া যায়:

* Vision Models
* Language Models
* Vision-Language Models
* Transformers
* Tokenizers
* Processors
* Datasets
* PEFT/LoRA

Install:

```bash
pip install transformers
pip install torch
pip install pillow
```

Check:

```bash
python -c "import torch; print(torch.__version__)"
```

---

# 4. VLM কীভাবে কাজ করে?

একটি VLM সাধারণত:

```text
              IMAGE
                ↓
         Vision Encoder
                ↓
        Visual Features
                ↓
              LLM
                ↑
             Prompt
                ↓
             Answer
```

ধরো image:

```text
Teacher + Whiteboard
```

Prompt:

```text
What is happening in this image?
```

Model:

```text
A teacher is explaining a topic
using a whiteboard.
```

---

# 5. Image + Text দুটোই Input

Traditional CNN:

```text
Image
 ↓
CNN
 ↓
Class
```

VLM:

```text
Image + Text
      ↓
     VLM
      ↓
Natural Language Answer
```

যেমন:

```text
Image:
[Binary Search Diagram]

Prompt:
"What concept is being explained?"
```

Output:

```text
"The image explains binary search."
```

---

# 6. Processor কী?

VLM সরাসরি JPG বুঝতে পারে না।

আমাদের:

```text
JPG
 ↓
Processor
 ↓
Tensor
 ↓
Model
```

Processor সাধারণত handle করে:

* image resizing
* normalization
* tokenization
* image tensor
* text tokens

তাই code-এ প্রায়ই দেখবে:

```python
processor(...)
```

---

# 7. প্রথম VLM Test

Learning purpose-এর জন্য একটি ছোট pretrained image-to-text model দিয়ে শুরু করা যায়।

Install:

```bash
pip install transformers torch pillow
```

Example:

```python
from transformers import pipeline

pipe = pipeline(
    "image-to-text",
    model="Salesforce/blip-image-captioning-base"
)

result = pipe("frames/video_001/frame_00001.jpg")

print(result)
```

Output-এর ধরন:

```text
[
    {
        "generated_text":
        "a man standing in front of a white board"
    }
]
```

এটা আমাদের প্রথম **Visual Description**।

---

# 8. BLIP এখানে কী করছে?

BLIP একটি vision-language architecture।

Input:

```text
Image
```

Output:

```text
Text
```

অর্থাৎ:

```text
Frame
 ↓
BLIP
 ↓
Caption
```

এটা M6-এর basic foundation।

---

# 9. কিন্তু আমাদের Educational AI-এর জন্য Caption যথেষ্ট নয়

ধরো model বললো:

```text
"A person standing next to a diagram."
```

এটা খুব generic।

আমাদের দরকার:

```text
Main subject
Objects
Action
Educational concept
Diagram
Text
Scene type
```

তাই prompt-based VLM দরকার।

---

# 10. Structured Visual Analysis

আমরা চাই:

```json
{
    "main_subject": "teacher",
    "objects": [
        "whiteboard",
        "marker",
        "diagram"
    ],
    "action": "explaining",
    "concept": "binary search",
    "on_screen_text": "Binary Search",
    "scene_type": "diagram"
}
```

এটা future LLM Scene Planner-এর জন্য অনেক বেশি useful।

---

# 11. Prompt Engineering

VLM-কে শুধু:

```text
Describe this image.
```

দিলে সাধারণ answer আসতে পারে।

Better:

```text
Analyze this image as an educational video scene.

Identify:

1. Main subject
2. Visible objects
3. Main action
4. Educational concept
5. Diagram or chart
6. On-screen text
7. Scene type

Return concise information.
```

এই ধরনের prompt আমাদের system-এ ব্যবহার করা যাবে।

---

# 12. Scene Type Classification

আমাদের predefined categories:

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
comparison
timeline
```

Example:

```text
Whiteboard + teacher
        ↓
talking_head
```

যদি diagram:

```text
Array + arrows
        ↓
diagram
```

যদি programming code:

```text
Python code
        ↓
code
```

---

# 13. Batch Frame Processing

একটি video-তে থাকতে পারে:

```text
30 frames
```

আমরা manually:

```python
pipe(frame1)
pipe(frame2)
pipe(frame3)
...
```

করব না।

Function বানাব:

```python
from pathlib import Path
from transformers import pipeline


def analyze_frames(frame_dir):

    pipe = pipeline(
        "image-to-text",
        model="Salesforce/blip-image-captioning-base"
    )

    frame_dir = Path(frame_dir)

    results = []

    for frame_path in sorted(frame_dir.glob("*.jpg")):

        output = pipe(str(frame_path))

        description = output[0]["generated_text"]

        results.append({
            "frame": frame_path.name,
            "description": description
        })

    return results
```

---

# 14. Save JSON

```python
import json


def save_results(results, output_path):

    with open(output_path, "w", encoding="utf-8") as f:

        json.dump(
            results,
            f,
            indent=2,
            ensure_ascii=False
        )
```

Complete:

```python
from pathlib import Path
import json

from transformers import pipeline


def analyze_frames(frame_dir):

    model = pipeline(
        "image-to-text",
        model="Salesforce/blip-image-captioning-base"
    )

    frame_dir = Path(frame_dir)

    results = []

    for frame_path in sorted(frame_dir.glob("*.jpg")):

        try:

            output = model(str(frame_path))

            description = output[0]["generated_text"]

            results.append({
                "frame": frame_path.name,
                "description": description
            })

            print(frame_path.name)
            print(description)

        except Exception as e:

            print(
                f"Error processing {frame_path}: {e}"
            )

    return results


def save_results(results, output_path):

    with open(
        output_path,
        "w",
        encoding="utf-8"
    ) as f:

        json.dump(
            results,
            f,
            indent=2,
            ensure_ascii=False
        )


if __name__ == "__main__":

    frames = "frames/video_001"

    output = "vision/video_001_vision.json"

    Path("vision").mkdir(exist_ok=True)

    results = analyze_frames(frames)

    save_results(results, output)

    print("Vision analysis completed.")
```

Run:

```bash
python scripts/vision_analysis.py
```

---

# 15. Output

তুমি পাবে:

```text
vision/
└── video_001_vision.json
```

Example:

```json
[
  {
    "frame": "frame_00000.jpg",
    "description":
      "a teacher standing in front of a whiteboard"
  },
  {
    "frame": "frame_00001.jpg",
    "description":
      "a diagram displayed on a whiteboard"
  },
  {
    "frame": "frame_00002.jpg",
    "description":
      "numbers arranged in a row"
  }
]
```

---

# 16. Timestamp যোগ করা

শুধু frame name যথেষ্ট নয়।

আমাদের দরকার:

```text
frame
+
timestamp
```

যদি প্রতি 2 seconds-এ frame নেওয়া হয়:

```python
timestamp = frame_id * 2
```

তাহলে:

```json
{
    "frame": "frame_00003.jpg",
    "timestamp": 6.0,
    "description": "numbers arranged in a row"
}
```

এটা খুব গুরুত্বপূর্ণ।

কারণ পরে:

```text
Whisper timestamp
        +
Vision timestamp
        ↓
Scene alignment
```

করব।

---

# 17. Better Vision JSON

Final structure:

```json
{
  "video_id": "video_001",

  "frames": [
    {
      "frame_id": 0,
      "timestamp": 0.0,
      "path": "frames/video_001/frame_00000.jpg",

      "description":
        "A teacher is standing beside a whiteboard.",

      "objects": [
        "teacher",
        "whiteboard"
      ],

      "action": "explaining",

      "concept": "binary search",

      "on_screen_text": "Binary Search",

      "scene_type": "diagram"
    }
  ]
}
```

এটাই আমাদের **Vision Dataset**।

---

# 18. Whisper + VLM

এখন সবচেয়ে গুরুত্বপূর্ণ integration।

আমাদের কাছে:

### Transcript

```json
{
  "start": 0,
  "end": 5,
  "text":
    "Binary search divides the array into two parts."
}
```

### Vision

```json
{
  "timestamp": 2,
  "description":
    "An array is displayed with the middle element highlighted."
}
```

দুটো combine:

```text
              Video
                │
       ┌────────┴────────┐
       ↓                 ↓
     Audio             Frames
       ↓                 ↓
   Whisper              VLM
       ↓                 ↓
 Transcript         Visual Analysis
       │                 │
       └────────┬────────┘
                ↓
           Scene Context
```

---

# 19. Scene Context

আমরা তখন একটা scene তৈরি করতে পারি:

```json
{
  "scene_id": 1,

  "start": 0,
  "end": 5,

  "narration":
    "Binary search divides the array into two parts.",

  "visual_description":
    "An array is displayed with the middle element highlighted.",

  "objects": [
    "array",
    "numbers",
    "highlight"
  ],

  "concept":
    "binary search",

  "scene_type":
    "diagram"
}
```

এটা M7/M8-এ আরও intelligent হবে।

---

# 20. Important Problem: Frame-by-Frame Analysis

ধরো:

```text
Frame 1:
Teacher

Frame 2:
Teacher

Frame 3:
Teacher

Frame 4:
Teacher
```

প্রতিটি frame আলাদাভাবে VLM-এ পাঠালে:

```text
4 × inference
```

কিন্তু আসলে এটা একই scene।

তাই future pipeline-এ আমরা করব:

```text
Frames
 ↓
Similarity
 ↓
Scene grouping
 ↓
Representative frames
 ↓
VLM
```

Example:

```text
0–8 sec
 ↓
8 frames
 ↓
similarity
 ↓
1 scene
 ↓
2 representative frames
 ↓
VLM
```

এতে computational cost অনেক কমবে।

---

# 21. Scene Change Detection

একটি basic technique:

```text
Frame 1
   ↓
Frame 2
   ↓
Difference
   ↓
High difference?
   ↓
New Scene
```

Example:

```text
0–10 sec
Teacher

10–20 sec
Diagram

20–30 sec
Code
```

আমরা detect করতে পারি:

```text
Teacher → Diagram
```

এটা scene boundary-এর candidate।

---

# 22. M6-এর Real Architecture

এখন তোমার system:

```text
                  VIDEO
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
        AUDIO                FRAMES
          ↓                   ↓
      Whisper                VLM
          ↓                   ↓
    Transcript          Visual Analysis
          │                   │
          └─────────┬─────────┘
                    ↓
              Scene Context
                    ↓
                JSON Dataset
```

---

# 23. আমাদের AI-এর Brain এখন কীভাবে তৈরি হচ্ছে?

এখন পর্যন্ত:

```text
M1
↓
Python Pipeline

M2
↓
Video Processing

M3
↓
Dataset Engineering

M4
↓
Speech Understanding

M5
↓
Vision Understanding

M6
↓
Pretrained VLM Integration
```

অর্থাৎ এখন AI:

```text
👂 শুনতে পারে
👁️ দেখতে পারে
📦 structured data তৈরি করতে পারে
```

পরবর্তী পর্যায়ে:

```text
🧠 বুঝতে শিখবে
```

---

# 24. M6 Practice Project

একটি 30–60 second educational video নাও।

Example:

```text
Binary Search
```

Run:

```text
Video
 ↓
Frame extraction
 ↓
VLM
```

Output:

```text
vision/video_001_vision.json
```

তারপর manually check করো:

### Question 1

VLM কি teacher detect করেছে?

### Question 2

Diagram detect করেছে?

### Question 3

On-screen text detect করেছে?

### Question 4

Concept বুঝেছে?

### Question 5

Scene type সঠিক হয়েছে?

---

# 25. M6 Mini Project

একটা script বানাও:

```text
scripts/
└── vision_analysis.py
```

Input:

```bash
python scripts/vision_analysis.py \
    --frames frames/video_001 \
    --output vision/video_001_vision.json
```

Output:

```json
{
  "video_id": "video_001",
  "frames": [...]
}
```

এখানে argparse ব্যবহার করবে।

---

# 26. M6 Completion Test

নিজেকে এই প্রশ্নগুলো করো:

### Basic

* [ ] Pretrained model কী?
* [ ] VLM কী?
* [ ] Vision Encoder কী?
* [ ] Processor কী?
* [ ] Image → Tensor কীভাবে হয়?

### Practical

* [ ] Hugging Face install করতে পারি?
* [ ] pretrained vision model load করতে পারি?
* [ ] image analyze করতে পারি?
* [ ] batch frame process করতে পারি?
* [ ] JSON save করতে পারি?

### Project

* [ ] Frame timestamp রাখতে পারি?
* [ ] Visual description তৈরি করতে পারি?
* [ ] Scene type তৈরি করতে পারি?
* [ ] Whisper + VLM combine করতে পারি?

---

# 🔥 M6-এর মূল ধারণা

এখন তোমার Educational Video AI-এর perception layer:

```text
             EDUCATIONAL VIDEO
                     │
        ┌────────────┴────────────┐
        ↓                         ↓
      AUDIO                     VIDEO
        ↓                         ↓
    ┌───────┐                 FRAMES
    │Whisper│                    ↓
    └───┬───┘                   VLM
        ↓                        ↓
   WHAT IS SAID?            WHAT IS SHOWN?
        │                        │
        └──────────┬─────────────┘
                   ↓
             SCENE CONTEXT
                   ↓
                JSON
```

### পরবর্তী M7 — **Scene Understanding + Multimodal AI**

M7-এ আমরা সবচেয়ে গুরুত্বপূর্ণ অংশে যাব:

```text
Whisper Transcript
        +
VLM Visual Description
        +
Frame Timestamp
        ↓
Multimodal LLM
        ↓
Educational Scene Understanding
        ↓
Scene JSON
```

অর্থাৎ AI শুধু **"কি বলা হয়েছে"** এবং **"কি দেখা যাচ্ছে"** জানবে না—এগুলো মিলিয়ে **"এই scene-এ শিক্ষার্থীকে আসলে কী শেখানো হচ্ছে এবং কীভাবে visual বানানো উচিত"** সেটাও বের করবে।


----
# M7 — Multimodal Scene Understanding 🧠

এখন আমরা তোমার Educational Video AI-এর **সবচেয়ে গুরুত্বপূর্ণ intelligence layer**-এ ঢুকব।

M6 পর্যন্ত আমাদের AI আলাদাভাবে বুঝতে পারে:

```text
👂 Whisper
"What is being said?"

👁️ VLM
"What is being shown?"
```

M7-এ আমরা দুটোকে একসাথে করব:

```text
             VIDEO
               │
       ┌───────┴────────┐
       ↓                ↓
     AUDIO            FRAMES
       ↓                ↓
   Whisper             VLM
       ↓                ↓
 Transcript      Visual Analysis
       │                │
       └───────┬────────┘
               ↓
       Multimodal LLM
               ↓
       Scene Understanding
               ↓
          Scene JSON
```

---

# M7-এর লক্ষ্য

একটি educational video দেখে AI যেন বলতে পারে:

> **কী বলা হচ্ছে?**
> **কী দেখানো হচ্ছে?**
> **কোন concept শেখানো হচ্ছে?**
> **কোন visual গুরুত্বপূর্ণ?**
> **কোন scene type?**
> **পরবর্তীতে নতুন video বানাতে কী visual দরকার?**

---

# 1. Multimodal AI কী?

Multimodal মানে একাধিক ধরনের information একসাথে process করা।

আমাদের ক্ষেত্রে:

```text
Text
+
Image
+
Timestamp
+
Audio transcript
```

সব একসাথে।

Traditional AI:

```text
Text → Text
```

Vision AI:

```text
Image → Text
```

Multimodal AI:

```text
Image + Text → Understanding
```

---

# 2. কেন M7 দরকার?

ধরো video-তে narrator বলছে:

```text
"Binary search checks the middle element first."
```

Whisper বুঝবে:

```text
Narration:
Binary search checks the middle element first.
```

কিন্তু frame-এ:

```text
[10] [20] [30] [40] [50] [60] [70]
                 ↑
                MID
```

VLM বুঝবে:

```text
Visual:
An array is shown with the middle element highlighted.
```

কিন্তু আমাদের final AI-এর দরকার:

```text
Concept:
Binary search

Teaching action:
Explain checking the middle element

Visual:
Array with middle element highlighted

Scene type:
Algorithm diagram
```

এই transformation-টাই M7।

---

# 3. Multimodal Scene Understanding

আমাদের input:

```json
{
  "timestamp": 4.0,

  "narration":
    "Binary search checks the middle element first.",

  "visual_description":
    "An array is displayed with the middle element highlighted."
}
```

AI output:

```json
{
  "concept": "Binary Search",

  "teaching_point":
    "The algorithm checks the middle element first.",

  "visual_elements": [
    "array",
    "numbers",
    "middle element",
    "highlight"
  ],

  "scene_type": "algorithm_diagram"
}
```

---

# 4. Scene Understanding বনাম Scene Detection

দুটো এক জিনিস নয়।

### Scene Detection

প্রশ্ন:

> Scene কোথায় শুরু এবং শেষ?

```text
0 sec ───────── 8 sec
        Scene 1
```

### Scene Understanding

প্রশ্ন:

> Scene-এ কী শেখানো হচ্ছে?

```text
Scene 1
 ↓
Binary Search
 ↓
Middle element
 ↓
Array
```

আমরা M7-এ দ্বিতীয় অংশে বেশি focus করব।

---

# 5. Input Data Design

M4 থেকে:

```text
transcripts/
└── video_001_transcript.json
```

M6 থেকে:

```text
vision/
└── video_001_vision.json
```

এখন দুটো combine করব।

---

# 6. Transcript Data

Example:

```json
{
  "segments": [
    {
      "start": 0.0,
      "end": 5.0,
      "text":
        "Binary search checks the middle element first."
    },
    {
      "start": 5.0,
      "end": 10.0,
      "text":
        "If the target is smaller, we search the left half."
    }
  ]
}
```

---

# 7. Vision Data

```json
{
  "frames": [
    {
      "timestamp": 2.0,
      "description":
        "An array is shown with the middle element highlighted."
    },
    {
      "timestamp": 6.0,
      "description":
        "The left half of the array is highlighted."
    }
  ]
}
```

---

# 8. Timestamp Alignment

এটাই খুব গুরুত্বপূর্ণ।

Transcript:

```text
0 ───── 5
Binary search checks middle
```

Vision:

```text
2 sec
Array + middle highlighted
```

তাই:

```text
0 ───────────── 5
│              │
└── Scene 1 ───┘
      ↑
    Frame
```

Frame `2 sec` scene `0–5 sec`-এর মধ্যে।

---

# 9. Python দিয়ে Alignment

আমরা function তৈরি করতে পারি:

```python
def find_frames_for_scene(
    scene_start,
    scene_end,
    vision_frames
):
    matched = []

    for frame in vision_frames:

        timestamp = frame["timestamp"]

        if scene_start <= timestamp <= scene_end:
            matched.append(frame)

    return matched
```

Example:

```python
frames = find_frames_for_scene(
    0,
    5,
    vision_frames
)
```

Output:

```text
frame at 2 sec
```

---

# 10. Transcript + Vision Combine

```python
def build_scene_context(
    transcript_segment,
    vision_frames
):

    start = transcript_segment["start"]
    end = transcript_segment["end"]

    matched_frames = find_frames_for_scene(
        start,
        end,
        vision_frames
    )

    return {
        "start": start,
        "end": end,
        "narration": transcript_segment["text"],
        "visuals": matched_frames
    }
```

Output:

```json
{
  "start": 0,
  "end": 5,

  "narration":
    "Binary search checks the middle element first.",

  "visuals": [
    {
      "timestamp": 2,
      "description":
        "An array is shown with the middle element highlighted."
    }
  ]
}
```

---

# 11. এখন AI Reasoning Layer

এখন আমাদের multimodal reasoning input:

```text
NARRATION:
Binary search checks the middle element first.

VISUAL:
An array is shown with the middle element highlighted.

TASK:
Determine what concept is being taught
and what visual elements are important.
```

LLM output:

```json
{
  "concept": "Binary Search",

  "learning_point":
    "Binary search begins by checking the middle element.",

  "important_visuals": [
    "array",
    "middle element",
    "highlight"
  ],

  "scene_type": "algorithm_diagram"
}
```

---

# 12. Prompt Engineering

আমাদের prompt খুব গুরুত্বপূর্ণ।

একটি ভালো system prompt:

```text
You are an educational video analysis assistant.

Your task is to analyze a video scene using:
1. Narration
2. Visual description
3. Timestamp information

Determine:

- educational concept
- key teaching point
- important visual elements
- scene type
- on-screen text
- animation opportunity
- learner difficulty

Return valid JSON only.
```

তারপর scene data:

```text
Narration:
"Binary search checks the middle element first."

Visual:
"An array is shown with the middle element highlighted."

Timestamp:
0–5 seconds
```

---

# 13. Expected Output

```json
{
  "concept": "Binary Search",

  "teaching_point":
    "The algorithm starts by checking the middle element.",

  "important_visuals": [
    "array",
    "middle element",
    "highlight"
  ],

  "scene_type": "algorithm_diagram",

  "on_screen_text": [
    "Binary Search",
    "MID"
  ],

  "animation_opportunity":
    "Highlight the middle element and then split the array.",

  "difficulty": "beginner"
}
```

এখন এই JSON ভবিষ্যতের **video generator-এর জন্য instruction** হিসেবে কাজ করবে।

---

# 14. Educational Meaning

এখানে একটি গুরুত্বপূর্ণ concept আছে।

একটি সাধারণ VLM বলবে:

> "An array with numbers is shown."

কিন্তু educational AI বলবে:

> "The visual demonstrates that binary search examines the middle element before eliminating half of the search space."

দুটোর পার্থক্য:

```text
VLM
 ↓
Visual Description

Multimodal Educational AI
 ↓
Educational Meaning
```

এটাই আমাদের project-এর uniqueness।

---

# 15. Learning Objective Extraction

M7-এ আমরা scene-level learning objective-ও বের করতে পারি।

Input:

```text
Binary search repeatedly divides
the search space in half.
```

Output:

```json
{
  "learning_objective":
    "Understand that binary search eliminates half
     of the search space at each step."
}
```

একটি video-র জন্য:

```json
{
  "learning_objectives": [
    "Define binary search",
    "Understand the middle element",
    "Understand search-space reduction",
    "Understand O(log n) complexity"
  ]
}
```

---

# 16. Difficulty Detection

AI scene দেখে difficulty estimate করতে পারে:

```text
beginner
intermediate
advanced
```

Example:

```json
{
  "concept": "Binary Search",
  "difficulty": "beginner"
}
```

আর যদি scene-এ থাকে:

```text
T(n) = T(n/2) + O(1)
```

তাহলে:

```json
{
  "difficulty": "intermediate"
}
```

---

# 17. Scene Type আরও intelligent করা

M6-এ আমরা basic scene type দিয়েছিলাম।

M7-এ semantic scene type:

```text
concept_explanation
definition
example
comparison
step_by_step
diagram
equation
code_walkthrough
experiment
summary
quiz
```

Example:

```text
"Photosynthesis converts light energy
into chemical energy."

↓
definition
```

অথবা:

```text
"First choose the middle element.
Then compare it with the target."

↓
step_by_step
```

---

# 18. Full Scene JSON

এখন আমরা এমন structure চাই:

```json
{
  "scene_id": 1,

  "start": 0.0,
  "end": 5.0,

  "narration":
    "Binary search checks the middle element first.",

  "visual_description":
    "An array is shown with the middle element highlighted.",

  "concept":
    "Binary Search",

  "learning_point":
    "The algorithm starts by checking the middle element.",

  "learning_objective":
    "Understand the role of the middle element.",

  "important_visuals": [
    "array",
    "middle element",
    "highlight"
  ],

  "on_screen_text": [
    "Binary Search",
    "MID"
  ],

  "scene_type":
    "step_by_step",

  "difficulty":
    "beginner",

  "animation_opportunity":
    "Highlight the middle element and split the array."
}
```

এটা অনেকটা আমাদের **master scene specification**।

---

# 19. কেন Scene JSON এত গুরুত্বপূর্ণ?

কারণ পরবর্তী system সরাসরি JSON পড়তে পারবে।

```text
Scene JSON
    │
    ├── narration
    │       ↓
    │      TTS
    │
    ├── scene_type
    │       ↓
    │    Generator
    │
    ├── visual_elements
    │       ↓
    │    Animation
    │
    ├── on_screen_text
    │       ↓
    │    Text Renderer
    │
    └── duration
            ↓
         FFmpeg
```

অর্থাৎ JSON হচ্ছে:

# 🎯 AI Video Generator-এর Intermediate Representation

---

# 20. IR কী?

Software engineering-এ intermediate representation বা IR হলো দুই system-এর মাঝের structured format।

আমাদের:

```text
Human Prompt
      ↓
LLM
      ↓
Scene JSON    ← IR
      ↓
Video Generator
```

এটা খুব powerful architecture।

---

# 21. Complete M7 Pipeline

```text
                     VIDEO
                       │
          ┌────────────┴────────────┐
          ↓                         ↓
        AUDIO                     FRAMES
          ↓                         ↓
      Whisper                      VLM
          ↓                         ↓
    Transcript               Visual Description
          │                         │
          └────────────┬────────────┘
                       ↓
              Timestamp Alignment
                       ↓
               Scene Context
                       ↓
                Multimodal LLM
                       ↓
             Educational Reasoning
                       ↓
                  Scene JSON
                       ↓
             ┌─────────┴─────────┐
             ↓                   ↓
       Learning Info        Visual Plan
```

---

# 22. Complete Python Architecture

Project structure:

```text
educational_video_ai/
│
├── videos/
│
├── frames/
│
├── transcripts/
│
├── vision/
│
├── scenes/
│
├── scripts/
│   ├── transcribe.py
│   ├── vision_analysis.py
│   ├── align_scene.py
│   ├── multimodal_analysis.py
│   └── validate_scene.py
│
└── dataset/
```

---

# 23. `align_scene.py`

```python
import json


def load_json(path):

    with open(path, "r", encoding="utf-8") as f:
        return json.load(f)


def find_visuals(
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


def build_context(
    transcript,
    vision
):

    scenes = []

    frames = vision["frames"]

    for segment in transcript["segments"]:

        start = segment["start"]
        end = segment["end"]

        visuals = find_visuals(
            start,
            end,
            frames
        )

        scenes.append({

            "start": start,
            "end": end,

            "narration":
                segment["text"],

            "visuals":
                visuals

        })

    return scenes


if __name__ == "__main__":

    transcript = load_json(
        "transcripts/video_001_transcript.json"
    )

    vision = load_json(
        "vision/video_001_vision.json"
    )

    scenes = build_context(
        transcript,
        vision
    )

    with open(
        "scenes/video_001_context.json",
        "w",
        encoding="utf-8"
    ) as f:

        json.dump(
            scenes,
            f,
            indent=2,
            ensure_ascii=False
        )

    print("Scene context created.")
```

---

# 24. M7-এর পরে Dataset Transformation

আগে:

```text
Video
 ↓
Transcript
```

তারপর:

```text
Video
 ↓
Frames
 ↓
Visual Description
```

এখন:

```text
Video
 ↓
Transcript + Vision
 ↓
Scene Understanding
 ↓
Educational Scene Dataset
```

---

# 25. একটি Real Example

Input video:

> "Photosynthesis is the process by which plants use sunlight to make food."

Frame:

```text
☀️
 ↓
🌱
 ↓
🍃
```

Whisper:

```text
"Plants use sunlight to make food."
```

VLM:

```text
"A green plant is shown receiving sunlight."
```

Multimodal LLM:

```json
{
  "concept": "Photosynthesis",

  "teaching_point":
    "Plants use light energy to produce food.",

  "visual_elements": [
    "sunlight",
    "plant",
    "leaves"
  ],

  "scene_type":
    "concept_explanation",

  "animation_opportunity":
    "Animate sunlight moving toward the leaves."
}
```

🔥 এখন দেখো কী হলো:

AI শুধু video **understand** করছে না।

AI ভবিষ্যতের নতুন video-এর জন্য **production instruction** তৈরি করছে।

---

# 26. M7-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা

আমাদের পুরো project এখন চারটি intelligence layer পাচ্ছে:

```text
👂 Whisper
Speech Understanding

👁️ VLM
Visual Understanding

🧠 Multimodal LLM
Educational Understanding

🎨 Generator
Visual Creation
```

এগুলো:

```text
Input Video
     ↓
Understanding
     ↓
Structured Scene
     ↓
Generation
```

---

# 27. M7 Mini Project

একটি 30–60 second educational video নিয়ে:

### Step 1

Whisper চালাও:

```text
video
 ↓
transcript.json
```

### Step 2

Frame analysis:

```text
frames
 ↓
vision.json
```

### Step 3

Timestamp alignment:

```text
transcript + vision
 ↓
scene_context.json
```

### Step 4

প্রতিটি scene-এর জন্য বের করো:

```text
concept
learning_point
visual_elements
scene_type
difficulty
animation_opportunity
```

### Step 5

সবকিছু save করো:

```text
scenes/
└── video_001_scene_analysis.json
```

---

# 28. M7 Completion Checklist

### Understanding

* [ ] Multimodal AI কী?
* [ ] VLM এবং LLM-এর পার্থক্য
* [ ] Scene Detection বনাম Scene Understanding
* [ ] Timestamp alignment
* [ ] Educational reasoning
* [ ] Intermediate Representation

### Coding

* [ ] Transcript load
* [ ] Vision JSON load
* [ ] Timestamp matching
* [ ] Scene context তৈরি
* [ ] Structured JSON save

### AI

* [ ] Multimodal prompt design
* [ ] Concept extraction
* [ ] Learning objective extraction
* [ ] Scene type classification
* [ ] Visual element extraction
* [ ] Animation instruction generation

---

# 🚀 এখন তোমার Project কোথায় এসেছে?

```text
M1  Python Pipeline
 ↓
M2  Video Processing
 ↓
M3  Dataset Engineering
 ↓
M4  Whisper
 ↓
M5  Computer Vision
 ↓
M6  Pretrained VLM
 ↓
M7  Multimodal Scene Understanding
 ↓
       🎯 SCENE JSON
```

এখন থেকে project-এর সবচেয়ে গুরুত্বপূর্ণ transition শুরু হবে:

```text
                UNDERSTANDING
                      ↓
                  SCENE JSON
                      ↓
              ┌───────┴────────┐
              ↓                ↓
        Narration Plan    Visual Plan
              ↓                ↓
             TTS        Animation/Images
              │                │
              └───────┬────────┘
                      ↓
                 FINAL VIDEO
```

**পরবর্তী M8 — Educational Scene Planner:** আমরা user-এর সাধারণ prompt যেমন **“Explain photosynthesis to a beginner in 60 seconds”** সরাসরি নিয়ে **learning objectives → script → scenes → timing → narration → visual instructions → scene JSON** তৈরি করব। এটাই তোমার AI-এর **generation brain**-এর প্রথম বড় ধাপ।



---
# M8 — Educational Scene Planner 🧠🎬

এখন আমরা তোমার project-এর **generation brain** তৈরি করা শুরু করব।

M7 পর্যন্ত আমরা existing educational video **understand** করতে শিখেছি।

```text
Existing Video
     ↓
Whisper
     ↓
Transcript
     +
VLM
     ↓
Visual Understanding
     ↓
Multimodal LLM
     ↓
Scene Understanding
```

M8-এ direction উল্টো হবে:

```text
User Topic
    ↓
Educational Planner
    ↓
Learning Objectives
    ↓
Script
    ↓
Scenes
    ↓
Visual Instructions
    ↓
Scene JSON
```

অর্থাৎ user শুধু বলবে:

> **"Explain photosynthesis to a beginner in 60 seconds."**

আমাদের AI পুরো video-এর blueprint তৈরি করবে।

---

# 1. M8-এর Main Goal

আমাদের input:

```text
Explain binary search to a beginner in 30 seconds.
```

AI-এর output:

```text
Learning Objectives
        ↓
Script
        ↓
Scene Plan
        ↓
Narration
        ↓
Visual Description
        ↓
Animation Instruction
        ↓
Timing
```

শেষে:

```json
{
  "topic": "Binary Search",
  "duration": 30,
  "difficulty": "beginner",
  "scenes": [...]
}
```

এই JSON-টাই পরবর্তী Video Generator ব্যবহার করবে।

---

# 2. Educational Scene Planner কী?

Scene Planner হলো এমন একটি AI component যা একটি topic-কে ছোট ছোট **teach-able visual scenes**-এ ভেঙে দেয়।

উদাহরণ:

```text
User:
"Explain photosynthesis in 60 seconds."
```

Planner:

```text
Scene 1 → What is photosynthesis?
Scene 2 → Sunlight
Scene 3 → Water + CO₂
Scene 4 → Glucose production
Scene 5 → Oxygen
Scene 6 → Summary
```

---

# 3. কেন Scene Planner দরকার?

LLM যদি সরাসরি বলে:

> "Generate a video about photosynthesis."

তাহলে output uncontrolled হতে পারে।

কিন্তু আমরা যদি pipeline বানাই:

```text
Prompt
 ↓
Learning Objectives
 ↓
Script
 ↓
Scene Planning
 ↓
Visual Planning
 ↓
Generation
```

তাহলে প্রতিটি stage independently validate করা যায়।

এটাই production-grade architecture।

---

# 4. M8 Architecture

```text
                    USER PROMPT
                         │
                         ↓
                ┌─────────────────┐
                │ Topic Extraction│
                └────────┬────────┘
                         ↓
                Learning Objectives
                         ↓
                  Difficulty Level
                         ↓
                    Script Plan
                         ↓
                  Scene Breakdown
                         ↓
              Visual Instructions
                         ↓
                 Animation Plan
                         ↓
                  Scene JSON
```

---

# 5. User Prompt Analysis

User বিভিন্নভাবে prompt দিতে পারে:

```text
Explain binary search.
```

অথবা:

```text
Explain binary search to a beginner.
```

অথবা:

```text
Explain binary search to a beginner in 30 seconds.
```

অথবা:

```text
Create a visual explanation of photosynthesis
for high school students in 60 seconds.
```

Planner-এর কাজ:

```text
Topic
Audience
Difficulty
Duration
Language
Style
Subject
```

বের করা।

---

# 6. Prompt Schema

আমরা প্রথমে একটা structured request তৈরি করব।

```json
{
  "topic": "Binary Search",
  "audience": "beginner",
  "difficulty": "beginner",
  "duration": 30,
  "language": "en",
  "style": "educational"
}
```

আরেকটি example:

```json
{
  "topic": "Photosynthesis",
  "audience": "high school",
  "difficulty": "intermediate",
  "duration": 60,
  "language": "en",
  "style": "animated"
}
```

---

# 7. Duration কেন গুরুত্বপূর্ণ?

ধরো:

```text
30 seconds
```

তাহলে script অনেক বড় হতে পারবে না।

সাধারণ speaking rate প্রায়:

```text
130–160 words/minute
```

তাই 30 sec-এর জন্য আনুমানিক:

```text
65–80 words
```

60 sec:

```text
130–160 words
```

আমরা exact fixed number না রেখে একটা target range ব্যবহার করব।

```python
target_words = duration * 2.3
```

30 sec:

```text
30 × 2.3 = 69 words
```

60 sec:

```text
60 × 2.3 = 138 words
```

---

# 8. Learning Objectives

Educational AI-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

শুধু script generate করলে সেটা educational নাও হতে পারে।

তাই প্রথমে:

```text
Topic
 ↓
Learning Objectives
```

Example:

### Topic

```text
Binary Search
```

### Objectives

```text
1. Define binary search.
2. Understand the middle element.
3. Understand why half of the search space is removed.
4. Understand the basic idea of O(log n).
```

Beginner হলে objectives কম ও সহজ হবে।

---

# 9. Learning Objective-এর Rule

একটি ভালো objective:

```text
Understand binary search.
```

এর চেয়ে ভালো:

```text
Explain how binary search repeatedly eliminates
half of a sorted search space.
```

আরও ভালো measurable objective:

```text
Given a sorted array, identify which half
binary search should search next.
```

আমাদের planner-কে এই ধরনের objective তৈরি করতে হবে।

---

# 10. Script Planning

Objectives:

```text
1. Define binary search.
2. Explain middle element.
3. Explain elimination.
```

Script:

```text
"Binary search is a fast way to find an item
in a sorted list.

Instead of checking every item, we start with
the middle element.

If our target is smaller, we ignore the right half.
If it is larger, we ignore the left half.

By repeatedly removing half of the search space,
binary search becomes extremely efficient."
```

---

# 11. Script থেকে Scene

এখন script-কে scene-এ ভাগ করব।

```text
Scene 1
Definition

Scene 2
Middle element

Scene 3
Comparison

Scene 4
Eliminate half

Scene 5
Repeat

Scene 6
Summary
```

এটাই Scene Planning।

---

# 12. Scene-এর Basic Structure

প্রতিটি scene-এ থাকবে:

```text
scene_id
start
end
duration
narration
visual_description
on_screen_text
scene_type
animation_instruction
```

Example:

```json
{
  "scene_id": 1,
  "start": 0,
  "end": 5,
  "duration": 5,
  "narration":
    "Binary search is a fast way to find an item in a sorted list.",

  "visual_description":
    "A sorted array appears on screen.",

  "on_screen_text":
    "Binary Search",

  "scene_type":
    "concept_explanation",

  "animation_instruction":
    "Reveal the array from left to right."
}
```

---

# 13. Scene Types

আমাদের planner-এর জন্য standard vocabulary তৈরি করা ভালো:

```text
definition
concept_explanation
example
comparison
step_by_step
diagram
equation
code
code_walkthrough
experiment
timeline
summary
quiz
```

এগুলো পরে generator-এর decision-making-এ কাজে লাগবে।

---

# 14. Scene Type → Generator

এটা খুব powerful architecture।

```text
scene_type
     │
     ├── diagram
     │      ↓
     │    Manim
     │
     ├── equation
     │      ↓
     │    Math Renderer
     │
     ├── code
     │      ↓
     │    Code Animation
     │
     ├── real_world
     │      ↓
     │    Image/Video Model
     │
     └── talking_head
            ↓
        Avatar/Video
```

অর্থাৎ Scene Planner decide করবে **কোন scene-এর জন্য কোন generation engine ব্যবহার করতে হবে।**

---

# 15. Visual Instruction

Narration:

```text
"Binary search checks the middle element first."
```

Bad visual instruction:

```text
Show binary search.
```

Good:

```text
Display a sorted array of numbers.
Highlight the middle element.
Add a label "MID".
Animate a pointer moving toward the middle.
```

Better structured version:

```json
{
  "visual_elements": [
    "sorted_array",
    "middle_pointer",
    "MID_label"
  ],
  "animation": [
    "show_array",
    "highlight_middle",
    "display_pointer"
  ]
}
```

এটা generator-এর জন্য অনেক বেশি useful।

---

# 16. Educational Style

Planner user-এর style preference-ও রাখতে পারে:

```text
style:
    clean
    colorful
    minimal
    realistic
    2d_animation
    whiteboard
    cinematic
```

Example:

```json
{
  "style": "clean_2d_animation"
}
```

---

# 17. Complete Planning JSON

এখন আমরা একটি **master format** তৈরি করব।

```json
{
  "project_id": "video_001",

  "topic": "Binary Search",

  "subject": "Computer Science",

  "audience": "beginner",

  "difficulty": "beginner",

  "language": "en",

  "duration": 30,

  "style": "clean_2d_animation",

  "learning_objectives": [
    "Define binary search",
    "Understand the middle element",
    "Understand elimination of half the search space"
  ],

  "scenes": [
    {
      "scene_id": 1,
      "start": 0,
      "end": 5,

      "narration":
        "Binary search is a fast way to find an item in a sorted list.",

      "visual_description":
        "A sorted array appears on screen.",

      "visual_elements": [
        "sorted_array"
      ],

      "on_screen_text": [
        "Binary Search"
      ],

      "scene_type":
        "definition",

      "animation_instruction":
        "Reveal the sorted array."
    },

    {
      "scene_id": 2,
      "start": 5,
      "end": 10,

      "narration":
        "We begin by checking the middle element.",

      "visual_description":
        "The middle element becomes highlighted.",

      "visual_elements": [
        "array",
        "middle_element",
        "highlight"
      ],

      "on_screen_text": [
        "MID"
      ],

      "scene_type":
        "step_by_step",

      "animation_instruction":
        "Highlight the middle element."
    }
  ]
}
```

---

# 18. এবার LLM ব্যবহার

M8-এর actual AI অংশ।

আমরা LLM-কে বলব:

```text
You are an expert educational video planner.

Create a structured educational video plan.

Requirements:

- Match the requested duration.
- Adapt to the target audience.
- Create measurable learning objectives.
- Divide the explanation into logical scenes.
- Every scene must have narration.
- Every scene must have visual instructions.
- Avoid unnecessary information.
- Return valid JSON only.
```

User prompt:

```text
Explain binary search to a beginner in 30 seconds.
```

---

# 19. Structured Output কেন?

যদি LLM output দেয়:

```text
First explain binary search...
Then show an array...
Then...
```

তাহলে machine-এর জন্য parse করা কঠিন।

কিন্তু:

```json
{
  "topic": "...",
  "duration": 30,
  "scenes": [...]
}
```

হলে:

```text
JSON
 ↓
Python
 ↓
Generator
```

সহজ।

---

# 20. JSON Validation

LLM ভুল JSON দিতে পারে।

তাই validation দরকার।

Python-এ আমরা `pydantic` ব্যবহার করতে পারি।

Install:

```bash
pip install pydantic
```

Model:

```python
from pydantic import BaseModel
from typing import List


class Scene(BaseModel):

    scene_id: int
    start: float
    end: float
    narration: str
    visual_description: str
    scene_type: str
    animation_instruction: str


class VideoPlan(BaseModel):

    topic: str
    duration: float
    difficulty: str
    learning_objectives: List[str]
    scenes: List[Scene]
```

---

# 21. Validation Example

```python
plan = VideoPlan(
    topic="Binary Search",
    duration=30,
    difficulty="beginner",
    learning_objectives=[
        "Define binary search"
    ],
    scenes=[]
)

print(plan)
```

যদি required field missing হয়:

```text
ValidationError
```

এটা production system-এ খুব গুরুত্বপূর্ণ।

---

# 22. Scene Timing Validation

ধরো:

```text
Scene 1 → 0–5
Scene 2 → 5–10
Scene 3 → 10–15
```

ঠিক।

কিন্তু:

```text
Scene 1 → 0–5
Scene 2 → 4–10
```

Overlap হয়েছে।

আমরা validation function বানাতে পারি।

```python
def validate_timing(scenes):

    previous_end = 0

    for scene in scenes:

        start = scene["start"]
        end = scene["end"]

        if start < previous_end:
            raise ValueError(
                "Scene timing overlap detected"
            )

        if end <= start:
            raise ValueError(
                "Invalid scene duration"
            )

        previous_end = end
```

---

# 23. Duration Validation

শেষ scene:

```text
end = 31
```

কিন্তু requested:

```text
30 seconds
```

তাহলে problem।

```python
if abs(last_end - duration) > 1:
    print("Warning: duration mismatch")
```

একটু tolerance রাখা ভালো।

---

# 24. Word Count Validation

যদি 30 sec video:

```text
target ≈ 69 words
```

কিন্তু LLM লিখলো:

```text
250 words
```

তাহলে সেটা 30 sec-এ বলা সম্ভব হবে না।

Function:

```python
def estimate_speaking_time(text):

    words = len(text.split())

    words_per_minute = 140

    return (words / words_per_minute) * 60
```

Example:

```python
text = "Binary search is a fast algorithm..."

seconds = estimate_speaking_time(text)

print(seconds)
```

---

# 25. Complete Planner Pipeline

এখন architecture:

```text
User Prompt
    ↓
Prompt Parser
    ↓
Topic
Audience
Duration
Difficulty
Style
    ↓
Learning Objective Generator
    ↓
Script Generator
    ↓
Scene Planner
    ↓
Visual Planner
    ↓
JSON Validator
    ↓
Timing Validator
    ↓
Word Count Validator
    ↓
FINAL SCENE JSON
```

---

# 26. Project Folder Update

M7 পর্যন্ত:

```text
educational_video_ai/
│
├── videos/
├── frames/
├── transcripts/
├── vision/
├── scenes/
│
├── scripts/
│   ├── transcribe.py
│   ├── vision_analysis.py
│   ├── align_scene.py
│   └── multimodal_analysis.py
│
└── dataset/
```

M8:

```text
educational_video_ai/
│
├── videos/
├── frames/
├── transcripts/
├── vision/
│
├── scenes/
│   ├── source_scenes/
│   └── generated_scenes/
│
├── planner/
│   ├── prompt_parser.py
│   ├── objective_generator.py
│   ├── script_generator.py
│   ├── scene_planner.py
│   └── validator.py
│
├── scripts/
│
└── dataset/
```

---

# 27. M8 Mini Project

এখন তোমার প্রথম **AI Video Planner** বানাবে।

Input:

```text
"Explain photosynthesis to a beginner in 60 seconds."
```

Output:

```text
planner/
    ↓
video_plan.json
```

যেখানে থাকবে:

```text
topic
subject
audience
difficulty
duration
learning_objectives
scenes
```

প্রতিটি scene:

```text
start
end
narration
visual_description
visual_elements
scene_type
animation_instruction
on_screen_text
```

---

# 28. Example: Photosynthesis

Input:

```text
Explain photosynthesis to a beginner in 60 seconds.
```

Expected high-level output:

```text
Scene 1 — Introduction
0–8 sec

Scene 2 — Sunlight
8–18 sec

Scene 3 — Water + CO₂
18–30 sec

Scene 4 — Glucose
30–42 sec

Scene 5 — Oxygen
42–52 sec

Scene 6 — Summary
52–60 sec
```

Visual:

```text
☀️
 ↓
🌱
 ↓
CO₂ + H₂O
 ↓
🍬 Glucose
+
O₂
```

---

# 29. একটি গুরুত্বপূর্ণ Design Decision

আমরা LLM-কে সরাসরি code generate করতে দেব না।

❌ Bad:

```text
User
 ↓
LLM
 ↓
Python/Manim code
 ↓
Video
```

কারণ code ভুল হলে পুরো pipeline ভেঙে যেতে পারে।

Better:

```text
User
 ↓
LLM
 ↓
Structured Scene JSON
 ↓
Renderer
 ↓
Video
```

অর্থাৎ:

# LLM plans, deterministic code executes.

এটা তোমার project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ architecture principle।

---

# 30. Scene JSON → Generator Mapping

পরবর্তী generation phase-এ:

```text
scene_type
       │
       ├── equation
       │      ↓
       │    Manim
       │
       ├── algorithm_diagram
       │      ↓
       │    Manim
       │
       ├── code_walkthrough
       │      ↓
       │    Code Renderer
       │
       ├── real_world
       │      ↓
       │    Image/Video Model
       │
       └── concept_explanation
              ↓
         Animation Engine
```

এখানেই M8-এর output future system-এর input হয়ে যাবে।

---

# 31. M8-এর সবচেয়ে গুরুত্বপূর্ণ Concept

তোমার AI-এর workflow এখন:

```text
                 USER
                  │
                  ↓
            "Explain X"
                  │
                  ↓
           🧠 PLANNER
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
    Objectives  Script    Scenes
        │         │         │
        └─────────┼─────────┘
                  ↓
             Scene JSON
                  │
                  ↓
          🎨 GENERATION
```

এখানে **Scene JSON হচ্ছে contract**।

Planner বলবে:

> কী বানাতে হবে।

Generator বলবে:

> কীভাবে বানাতে হবে।

---

# 32. M8 Completion Checklist

### Educational Intelligence

* [ ] User prompt parse
* [ ] Topic extraction
* [ ] Audience extraction
* [ ] Difficulty
* [ ] Duration
* [ ] Learning objectives
* [ ] Script planning
* [ ] Scene breakdown
* [ ] Visual planning

### Structured Generation

* [ ] Scene JSON
* [ ] Pydantic validation
* [ ] Scene timing validation
* [ ] Word count validation
* [ ] Duration validation
* [ ] Scene type classification

### Architecture

* [ ] LLM = planner
* [ ] JSON = intermediate representation
* [ ] Renderer = executor
* [ ] Deterministic validation

---

# 🚀 এখন তোমার Project-এর অবস্থান

```text
M1  Python Pipeline
 ↓
M2  Video Processing
 ↓
M3  Dataset Engineering
 ↓
M4  Whisper / Speech
 ↓
M5  Computer Vision
 ↓
M6  VLM
 ↓
M7  Multimodal Scene Understanding
 ↓
M8  Educational Scene Planner
 ↓
🎯 SCENE JSON
```

এখন আমরা **understanding side থেকে generation side-এ ঢুকছি**।

পরের ধাপ **M9 — Script Generation & Educational Content Engine**-এ আমরা planner-কে আরও গভীর করব: **topic → learning objectives → teaching strategy → script → narration timing → scene-by-scene script**, এবং beginner/intermediate/advanced অনুযায়ী একই topic-এর আলাদা educational explanation তৈরি করব।


---
# M9 — Script Generation & Educational Content Engine 🧠📝

M8-এ আমরা তৈরি করেছি:

```text
User Prompt
     ↓
Topic
     ↓
Learning Objectives
     ↓
Scene Plan
     ↓
Scene JSON
```

এখন M9-এ আমরা **প্রতিটি scene-এর জন্য high-quality educational script** তৈরি করব।

আমাদের লক্ষ্য:

```text
User:
"Explain photosynthesis to a beginner in 60 seconds."

              ↓

        Educational Engine
              ↓
       Learning Objectives
              ↓
       Teaching Strategy
              ↓
        Complete Script
              ↓
       Scene Narration
              ↓
      Timing Validation
              ↓
        Final Scene JSON
```

---

# 1. M9-এর মূল লক্ষ্য

একটি ভালো educational video শুধু তথ্য দেয় না।

এটি:

```text
Explain
   ↓
Example
   ↓
Visualize
   ↓
Connect
   ↓
Reinforce
   ↓
Summarize
```

করবে।

তাই M9-এ আমরা AI-কে শেখাব:

> **কীভাবে একটি topic-কে সহজে শেখানোর মতো script বানাতে হয়।**

---

# 2. কেন আলাদা Script Engine দরকার?

M8-এর Scene Planner বলতে পারে:

```json
{
  "scene_type": "definition",
  "visual_description": "Show a green plant and sunlight."
}
```

কিন্তু narration কী হবে?

```text
"Photosynthesis is the process by which..."
```

এটা M9-এর কাজ।

Architecture:

```text
M8
Scene Planning
     ↓
M9
Script Generation
     ↓
M10+
Visual / Animation Generation
```

---

# 3. Educational Script বনাম সাধারণ AI Text

সাধারণ LLM:

> Photosynthesis is the process by which green plants convert light energy into chemical energy.

Beginner educational script:

> Plants need food to grow. But unlike us, plants can make their own food. They use sunlight, water, and carbon dioxide to do it. This process is called photosynthesis.

দ্বিতীয়টি বেশি:

* সহজ
* conversational
* visualizable
* teachable

---

# 4. Educational Script-এর Structure

আমরা একটি সাধারণ teaching pattern ব্যবহার করব:

```text
HOOK
 ↓
CONTEXT
 ↓
CORE CONCEPT
 ↓
EXAMPLE
 ↓
VISUAL EXPLANATION
 ↓
SUMMARY
```

Short video হলে সব অংশ লাগবে না।

---

# 5. Hook কী?

প্রথম কয়েক সেকেন্ডে attention তৈরি করা।

Example:

```text
"How can a plant make its own food?"
```

তারপর:

```text
"The answer is photosynthesis."
```

Algorithm:

```text
Question
 ↓
Curiosity
 ↓
Answer
```

---

# 6. Context

User-কে বলবে:

> কেন concept-টি গুরুত্বপূর্ণ?

Example:

```text
"Plants cannot walk to a kitchen and get food.
Instead, they make their own food."
```

এটা concept-এর context তৈরি করে।

---

# 7. Core Concept

তারপর মূল definition:

```text
"Photosynthesis is the process plants use
to make food using sunlight."
```

---

# 8. Example

Abstract concept-এর পরে concrete example:

```text
"Think of a leaf as a tiny food factory."
```

Visual:

```text
☀️
 ↓
🌿
 ↓
🍬
```

---

# 9. Summary

শেষে:

```text
"So remember:

Sunlight + Water + Carbon Dioxide
→ Food + Oxygen"
```

এটা learner-এর memory reinforce করে।

---

# 10. Teaching Strategy

একই topic সবাইকে একইভাবে শেখানো উচিত নয়।

আমাদের AI-এর কাছে থাকবে:

```text
Audience
Difficulty
Prior Knowledge
Duration
```

Example:

### Beginner

```text
Binary Search

"Instead of checking every number,
we repeatedly cut the search area in half."
```

### Intermediate

```text
Binary Search

"Because the array is sorted, comparing the target
with the middle element lets us eliminate half
of the remaining search space."
```

### Advanced

```text
Binary Search

"For a sorted sequence, each comparison reduces
the search interval by approximately half,
giving O(log n) search complexity."
```

একই concept।

কিন্তু explanation আলাদা।

---

# 11. Difficulty Adapter

আমরা একটি rule তৈরি করব:

```text
difficulty
     │
     ├── beginner
     │      ↓
     │   simple words
     │   examples
     │   fewer concepts
     │
     ├── intermediate
     │      ↓
     │   technical terms
     │   deeper explanation
     │
     └── advanced
            ↓
         precise terminology
         equations
         edge cases
```

---

# 12. Technical Vocabulary Control

Beginner:

```text
"half of the list"
```

Intermediate:

```text
"half of the search space"
```

Advanced:

```text
"logarithmic reduction of the search interval"
```

আমাদের AI audience অনুযায়ী vocabulary পরিবর্তন করবে।

---

# 13. Script Length

এটা খুব গুরুত্বপূর্ণ।

আমরা আগের মতো:

```python
WORDS_PER_MINUTE = 140
```

ধরতে পারি।

Approximation:

```python
def target_words(duration):
    return int(duration * 140 / 60)
```

30 seconds:

```text
≈ 70 words
```

60 seconds:

```text
≈ 140 words
```

---

# 14. Better: Word Range

Exact number না রেখে range ব্যবহার করা ভালো।

```python
def word_range(duration):

    min_words = int(duration * 120 / 60)
    max_words = int(duration * 160 / 60)

    return min_words, max_words
```

60 sec:

```text
120–160 words
```

30 sec:

```text
60–80 words
```

এতে natural narration সম্ভব।

---

# 15. Scene-level Narration

ধরো total duration:

```text
60 seconds
```

Scenes:

```text
0–8
8–18
18–30
30–42
42–52
52–60
```

প্রতিটি scene-এর narration আলাদা হবে।

```json
{
  "scene_id": 1,
  "start": 0,
  "end": 8,
  "narration": "Have you ever wondered how plants make food?"
}
```

---

# 16. Scene Narration কেন গুরুত্বপূর্ণ?

কারণ পরে:

```text
Scene 1
 ↓
TTS
 ↓
Audio 1
```

তারপর:

```text
Scene 2
 ↓
TTS
 ↓
Audio 2
```

এবং:

```text
Scene 1 Visual
+
Scene 1 Audio
 ↓
Scene 1 Video
```

তারপর সব scene combine হবে।

---

# 17. M9 Prompt Architecture

LLM-কে একটি বড় prompt দেওয়ার পরিবর্তে আমরা structured instructions দেব।

```text
SYSTEM:
You are an expert educational content designer.

USER:

Topic:
Binary Search

Audience:
Beginner

Duration:
30 seconds

Language:
English

Style:
Simple and visual

Learning Objectives:
1. Define binary search.
2. Explain the middle element.
3. Explain why half the search space is removed.

Create a concise educational script.
```

---

# 18. Script Generation Rules

LLM-এর জন্য rules:

```text
1. Start with a clear explanation.
2. Use simple language.
3. Avoid unnecessary details.
4. Introduce one idea at a time.
5. Use concrete examples.
6. Match the requested difficulty.
7. Match the duration.
8. Make every scene visually representable.
9. Avoid unsupported claims.
10. Return structured JSON.
```

---

# 19. Structured Script Output

আমরা চাই:

```json
{
  "topic": "Binary Search",

  "duration": 30,

  "script": {
    "hook": "...",
    "body": "...",
    "summary": "..."
  },

  "scenes": [
    {
      "scene_id": 1,
      "narration": "...",
      "estimated_duration": 5
    }
  ]
}
```

---

# 20. Scene JSON এখন আরও Powerful হবে

M8:

```json
{
  "scene_id": 1,
  "visual_description": "...",
  "scene_type": "definition"
}
```

M9:

```json
{
  "scene_id": 1,

  "start": 0,
  "end": 5,

  "narration":
    "Binary search is a fast way to find an item
     in a sorted list.",

  "estimated_words": 16,

  "visual_description":
    "A sorted array appears on screen.",

  "scene_type":
    "definition",

  "on_screen_text":
    "Binary Search"
}
```

---

# 21. Narration Timing

প্রতিটি scene-এর narration-এর speaking time estimate করব।

```python
def estimate_duration(text, wpm=140):

    words = len(text.split())

    return words / wpm * 60
```

Example:

```python
text = """
Binary search is a fast way to find
an item in a sorted list.
"""

print(estimate_duration(text))
```

যদি output:

```text
4.7 seconds
```

তাহলে scene duration যদি 3 sec হয়:

```text
❌ Too long
```

Planner-কে revise করতে হবে।

---

# 22. Automatic Script Validation

আমরা validation layer বানাব:

```text
Script
 ↓
Word Count
 ↓
Timing
 ↓
Objective Coverage
 ↓
Scene Coverage
 ↓
Validation
```

---

# 23. Objective Coverage

ধরো objectives:

```text
1. Define binary search
2. Explain middle element
3. Explain elimination
```

Generated script:

```text
"Binary search finds items quickly."
```

এখানে:

```text
Objective 1 → partial
Objective 2 → missing
Objective 3 → missing
```

তাই script incomplete।

আমাদের planner check করবে।

---

# 24. Objective-to-Scene Mapping

এটা খুব useful।

```json
{
  "scene_id": 1,
  "learning_objectives": [1]
}
```

Scene 2:

```json
{
  "scene_id": 2,
  "learning_objectives": [2]
}
```

Scene 3:

```json
{
  "scene_id": 3,
  "learning_objectives": [3]
}
```

তাহলে পুরো lesson traceable হয়।

---

# 25. Complete Educational Plan

M9 শেষে ideal output:

```json
{
  "topic": "Binary Search",

  "subject": "Computer Science",

  "audience": "beginner",

  "difficulty": "beginner",

  "duration": 30,

  "learning_objectives": [
    "Define binary search",
    "Understand the middle element",
    "Understand elimination of half the search space"
  ],

  "scenes": [
    {
      "scene_id": 1,
      "start": 0,
      "end": 6,

      "learning_objectives": [1],

      "narration":
        "Binary search is a fast way to find
         an item in a sorted list.",

      "visual_description":
        "Show a sorted array.",

      "scene_type":
        "definition"
    },

    {
      "scene_id": 2,
      "start": 6,
      "end": 14,

      "learning_objectives": [2],

      "narration":
        "We start by checking the middle element.",

      "visual_description":
        "Highlight the middle element.",

      "scene_type":
        "step_by_step"
    },

    {
      "scene_id": 3,
      "start": 14,
      "end": 24,

      "learning_objectives": [3],

      "narration":
        "If the target is smaller, we ignore the
         right half. If it is larger, we ignore
         the left half.",

      "visual_description":
        "Fade out the eliminated half.",

      "scene_type":
        "diagram"
    },

    {
      "scene_id": 4,
      "start": 24,
      "end": 30,

      "learning_objectives": [1, 2, 3],

      "narration":
        "By repeatedly removing half the search space,
         binary search finds items very efficiently.",

      "visual_description":
        "Show the search space shrinking.",

      "scene_type":
        "summary"
    }
  ]
}
```

---

# 26. Teaching Strategy Layer

M9-এ আরেকটি গুরুত্বপূর্ণ feature যোগ করা যায়:

```text
teaching_strategy
```

Possible values:

```text
direct_explanation
example_first
analogy
problem_solution
step_by_step
question_answer
comparison
story_based
```

---

# 27. Example: Analogy

Topic:

```text
Binary Search
```

Strategy:

```text
analogy
```

Script:

> Imagine looking for a word in a dictionary. You don't start from the first page. You open near the middle, decide which half contains the word, and repeat.

Visual:

```text
Dictionary
     ↓
Middle Page
     ↓
Left / Right
     ↓
Repeat
```

এটা beginner-এর জন্য খুব effective হতে পারে।

---

# 28. Strategy নির্বাচন

Planner:

```text
Audience = beginner
        +
Concept = abstract
        ↓
Use analogy
```

যদি:

```text
Audience = advanced
Concept = algorithm complexity
```

তাহলে:

```text
Use direct technical explanation
```

---

# 29. Script Quality Score

আমরা ভবিষ্যতে একটি quality score রাখতে পারি:

```text
clarity
accuracy
coverage
visualizability
timing
engagement
```

Example:

```json
{
  "quality": {
    "clarity": 0.92,
    "accuracy": 0.96,
    "coverage": 0.90,
    "visualizability": 0.94,
    "timing": 0.98
  }
}
```

প্রথম MVP-তে এই score LLM দিয়ে approximate করা যায়; পরে evaluator model দিয়ে উন্নত করা যাবে।

---

# 30. Hallucination Control

Educational AI-তে hallucination dangerous।

তাই prompt-এ:

```text
Do not invent facts.

If information is uncertain,
state the uncertainty.

Use only well-established information
unless sources are explicitly provided.
```

আর আরও ভালো architecture:

```text
User Topic
 ↓
Knowledge Retrieval
 ↓
Trusted Sources
 ↓
Script Generation
```

এটা পরে **RAG** phase-এ করা যাবে।

---

# 31. Script → TTS-এর জন্য প্রস্তুতি

M9-এর output পরে যাবে:

```text
Narration
 ↓
TTS
 ↓
Audio
```

তাই script-এ TTS-friendly writing দরকার।

Bad:

```text
"Photosynthesis—an oxygenic phototrophic process—..."
```

Beginner TTS-এর জন্য better:

```text
"Plants use sunlight to make food.
This process is called photosynthesis."
```

---

# 32. Pauses যোগ করা

TTS natural করতে আমরা metadata রাখতে পারি:

```json
{
  "narration":
    "Binary search is fast.",

  "pause_after":
    0.5
}
```

অথবা:

```json
{
  "sentence": "First, find the middle element.",
  "pause": 0.3
}
```

পরে audio generation-এ এগুলো ব্যবহার করা যাবে।

---

# 33. On-Screen Text আলাদা

Narration:

```text
"Binary search starts with the middle element."
```

On-screen text:

```text
"CHECK THE MIDDLE"
```

পুরো narration screen-এ দেখানো উচিত নয়।

এটা important educational video principle।

```text
Narration
≠
On-screen text
```

---

# 34. Visual + Narration Alignment

Scene:

```json
{
  "narration":
    "We check the middle element.",

  "visual_action":
    "Highlight middle element",

  "on_screen_text":
    "MID"
}
```

সব তিনটি একই teaching point support করছে।

```text
Narration
     +
Visual
     +
Text
     ↓
One Teaching Point
```

এটা M9-এর core principle।

---

# 35. M9 Full Architecture

```text
                     USER PROMPT
                          │
                          ↓
                    M8 PLANNER
                          │
                          ↓
                  Topic + Audience
                          │
                          ↓
                 Learning Objectives
                          │
                          ↓
                  Teaching Strategy
                          │
                          ↓
                   Script Generator
                          │
                          ↓
                    Scene Narration
                          │
              ┌───────────┼───────────┐
              ↓           ↓           ↓
           Timing     Objectives   Visualizability
              │           │           │
              └───────────┼───────────┘
                          ↓
                    VALIDATION
                          ↓
                   FINAL SCENE JSON
```

---

# 36. Project Folder Update

M9-এর পরে:

```text
educational_video_ai/
│
├── videos/
├── frames/
├── transcripts/
├── vision/
│
├── planner/
│   ├── prompt_parser.py
│   ├── objective_generator.py
│   ├── script_generator.py
│   ├── scene_planner.py
│   ├── teaching_strategy.py
│   └── validator.py
│
├── scenes/
│   ├── source_scenes/
│   └── generated_scenes/
│
├── scripts/
│
├── dataset/
│
└── logs/
```

---

# 37. M9 Mini Project

এখন তোমার project-এ একটি input নাও:

```text
"Explain recursion to a beginner in 45 seconds."
```

AI-এর output হওয়া উচিত:

```text
Topic:
Recursion

Audience:
Beginner

Duration:
45 sec

Learning Objectives:
1. Understand what recursion means.
2. Understand the base case.
3. Understand recursive calls.
```

তারপর:

```text
Scene 1
Hook

Scene 2
Definition

Scene 3
Simple example

Scene 4
Base case

Scene 5
Recursive call

Scene 6
Summary
```

প্রতিটি scene-এ:

```text
start
end
narration
visual_description
visual_elements
on_screen_text
scene_type
animation_instruction
learning_objectives
```

---

# 38. M9-এর Coding Task

তোমার `planner/` directory-তে:

```text
planner/
├── script_generator.py
├── timing.py
├── strategy.py
└── validator.py
```

### `timing.py`

```python
def estimate_duration(text, wpm=140):

    words = len(text.split())

    return (words / wpm) * 60


def word_range(duration):

    minimum = int(duration * 120 / 60)
    maximum = int(duration * 160 / 60)

    return minimum, maximum
```

### `validator.py`

```python
def validate_script(text, duration):

    words = len(text.split())

    minimum, maximum = word_range(duration)

    if words < minimum:
        return False, "Script is too short."

    if words > maximum:
        return False, "Script is too long."

    return True, "Script length is valid."
```

---

# 39. M9 Completion Test

নিজেকে এই questions করো:

### Educational

* [ ] Hook কী?
* [ ] Learning objective কী?
* [ ] Teaching strategy কী?
* [ ] Beginner বনাম advanced explanation কীভাবে পরিবর্তন হয়?
* [ ] Example কেন দরকার?
* [ ] Summary কেন দরকার?

### AI

* [ ] LLM দিয়ে script generate করতে পারি?
* [ ] Structured JSON generate করতে পারি?
* [ ] Word count validate করতে পারি?
* [ ] Speaking duration estimate করতে পারি?
* [ ] Learning objectives-এর coverage check করতে পারি?

### Video

* [ ] Narration scene-এর সাথে align করতে পারি?
* [ ] On-screen text আলাদা করতে পারি?
* [ ] Visual instruction তৈরি করতে পারি?
* [ ] Scene type নির্বাচন করতে পারি?

---

# 🔥 M1 → M9 পর্যন্ত আমাদের AI

এখন পর্যন্ত আমরা তৈরি করেছি:

```text
M1
Python AI Pipeline
       ↓
M2
Video Processing
       ↓
M3
Dataset Engineering
       ↓
M4
Whisper / Speech
       ↓
M5
Computer Vision
       ↓
M6
Pretrained VLM
       ↓
M7
Multimodal Understanding
       ↓
M8
Educational Scene Planner
       ↓
M9
Script Generation
       ↓
🎯 EDUCATIONAL SCENE JSON
```

এখন আমাদের কাছে এমন একটি JSON থাকবে যা **video renderer বুঝতে পারবে**।

---

# 🚀 M10 — Educational Visual Planning

পরবর্তী ধাপে আমরা narration-কে visual-এর সাথে আরও গভীরভাবে map করব:

```text
Scene Narration
      ↓
Visual Elements
      ↓
Objects
      ↓
Camera Movement
      ↓
Animation Actions
      ↓
Text
      ↓
Diagram
      ↓
Color/Style
      ↓
Generator Instructions
```

উদাহরণ:

```text
Narration:
"Plants use sunlight to make food."

↓
Visual Plan:

☀️ Sun
↓
Light Rays
↓
🌱 Plant
↓
🍬 Glucose

Animation:
1. Show plant
2. Bring sunlight
3. Animate light entering leaf
4. Show glucose
5. Show oxygen
```

**M10-এর পরেই আমরা প্রথমবার সত্যিকারের `Scene JSON → Animation` pipeline তৈরি করার দিকে যাব।**


----
# M10 — Educational Visual Planning

M9-এ আমরা শিখেছি **কীভাবে educational script + scene JSON তৈরি করতে হয়**।

এখন M10-এর কাজ হলো:

> **Narration → কী দেখানো হবে → কীভাবে দেখানো হবে → কখন animation হবে**

অর্থাৎ M10 থেকে আমাদের AI শুধু “কী বলতে হবে” জানবে না, বরং **ভিডিওতে কী দেখাতে হবে তার সম্পূর্ণ visual plan তৈরি করবে।**

---

# 1. M10-এর মূল লক্ষ্য

ধরো user বললো:

> **“Explain photosynthesis to a beginner in 30 seconds.”**

M9 তৈরি করবে:

```text
Narration:
"Plants use sunlight to make food."

Narration:
"Water and carbon dioxide are used in this process."

Narration:
"Plants produce glucose and oxygen."
```

কিন্তু ভিডিও বানানোর জন্য এটা যথেষ্ট নয়।

আমাদের জানতে হবে:

```text
কী দেখাব?
↓
Sun
↓
Sunlight rays
↓
Plant
↓
Water
↓
CO₂
↓
Glucose
↓
Oxygen
```

এবং animation:

```text
1. Plant appears
2. Sun appears
3. Sunlight moves toward plant
4. Water enters
5. CO₂ enters
6. Glucose appears
7. Oxygen appears
```

এটাই **Educational Visual Planning**।

---

# 2. M10 Architecture

আমাদের pipeline এখন হবে:

```text
USER PROMPT
     ↓
M8 Educational Planner
     ↓
M9 Script Generator
     ↓
Narration
     ↓
M10 Visual Planner
     ↓
Visual Plan
     ↓
M11 Animation Generator
     ↓
Manim / Image / Video Model
```

আরেকভাবে:

```text
              ┌──────────────┐
              │ User Prompt  │
              └──────┬───────┘
                     ↓
             ┌──────────────┐
             │ Script Plan  │
             └──────┬───────┘
                    ↓
             ┌──────────────┐
             │   Narration  │
             └──────┬───────┘
                    ↓
          ┌─────────────────────┐
          │  Visual Planner     │
          └──────────┬──────────┘
                     ↓
              ┌─────────────┐
              │ Visual Plan │
              └──────┬──────┘
                     ↓
          ┌─────────────────────┐
          │ Animation Generator │
          └─────────────────────┘
```

---

# 3. কেন M10 দরকার?

LLM যদি সরাসরি video code generate করে:

```text
User
 ↓
LLM
 ↓
Python code
 ↓
Video
```

তাহলে সমস্যা হবে।

যেমন:

* animation ভুল হতে পারে
* timing mismatch হতে পারে
* narration-এর সাথে visual মিলবে না
* একই object-এর design বারবার পরিবর্তন হতে পারে
* generated code unstable হতে পারে

তাই আমরা **Intermediate Representation (IR)** ব্যবহার করব।

```text
Narration
   ↓
Visual Plan
   ↓
Animation Code
```

এটা অনেক বেশি reliable।

---

# 4. Visual Plan কী?

একটি scene-এর visual plan হতে পারে:

```json
{
  "scene_id": 1,
  "start": 0,
  "end": 5,

  "narration": "Plants use sunlight to make food.",

  "visual": {
    "background": "light",
    "objects": [
      "sun",
      "plant",
      "sunlight"
    ],
    "layout": "center"
  },

  "animation": [
    {
      "action": "show",
      "object": "plant",
      "duration": 1
    },
    {
      "action": "show",
      "object": "sun",
      "duration": 1
    },
    {
      "action": "move",
      "object": "sunlight",
      "target": "plant",
      "duration": 2
    }
  ],

  "on_screen_text": [
    "Sunlight → Plant"
  ]
}
```

এখন এই JSON দেখে আমাদের animation engine কাজ করতে পারবে।

---

# 5. Visual Planning-এর প্রধান components

প্রতিটি scene-এর জন্য আমরা অন্তত এই information রাখব:

```text
1. Visual objects
2. Object properties
3. Layout
4. Camera
5. Animation
6. Timing
7. On-screen text
8. Diagram
9. Transition
10. Visual style
```

---

# 6. Visual Objects

প্রথমে জানতে হবে scene-এ কী কী object আছে।

Example:

```text
Topic: Binary Search
```

Objects:

```json
[
  "array",
  "numbers",
  "middle_element",
  "left_pointer",
  "right_pointer"
]
```

Photosynthesis:

```json
[
  "sun",
  "plant",
  "water",
  "carbon_dioxide",
  "glucose",
  "oxygen"
]
```

Networking:

```json
[
  "computer",
  "router",
  "server",
  "data_packet"
]
```

---

# 7. Object Properties

শুধু object-এর নাম যথেষ্ট নয়।

আমাদের বলতে হবে object কীভাবে দেখতে হবে।

Example:

```json
{
  "object": "sun",
  "type": "circle",
  "position": "top_right",
  "size": "large",
  "label": "Sun"
}
```

Plant:

```json
{
  "object": "plant",
  "type": "illustration",
  "position": "center",
  "size": "medium",
  "label": "Plant"
}
```

---

# 8. Layout Planning

Visual elements কোথায় থাকবে?

Example:

```text
        ☀️ Sun

          ↓
       sunlight

          ↓

        🌱 Plant

   H₂O →       ← CO₂
```

JSON:

```json
{
  "layout": {
    "sun": "top_right",
    "plant": "center",
    "water": "left",
    "carbon_dioxide": "right"
  }
}
```

---

# 9. Animation Planning

এটা M10-এর সবচেয়ে important অংশ।

আমরা animation-কে actions হিসেবে define করব।

যেমন:

```text
show
hide
move
fade_in
fade_out
scale
highlight
transform
draw
write
rotate
```

Example:

```json
{
  "action": "fade_in",
  "object": "plant",
  "duration": 1
}
```

তারপর:

```json
{
  "action": "move",
  "object": "sunlight",
  "from": "sun",
  "to": "plant",
  "duration": 2
}
```

---

# 10. Animation Timeline

ধরো scene duration 8 seconds।

তাহলে:

```text
0s ─────────────── 8s

0–1s   Plant appears
1–2s   Sun appears
2–4s   Sunlight moves
4–6s   Water enters
6–8s   Glucose appears
```

JSON:

```json
{
  "animations": [
    {
      "start": 0,
      "duration": 1,
      "action": "show",
      "object": "plant"
    },
    {
      "start": 1,
      "duration": 1,
      "action": "show",
      "object": "sun"
    },
    {
      "start": 2,
      "duration": 2,
      "action": "move",
      "object": "sunlight"
    },
    {
      "start": 4,
      "duration": 2,
      "action": "move",
      "object": "water"
    },
    {
      "start": 6,
      "duration": 2,
      "action": "show",
      "object": "glucose"
    }
  ]
}
```

---

# 11. Narration → Visual Mapping

এটা খুব গুরুত্বপূর্ণ।

আমরা চাই:

```text
Narration
    ↓
Visual
```

Example:

### Narration

> "Binary search checks the middle element first."

Visual:

```text
[10] [20] [30] [40] [50] [60] [70]
                ↑
              middle
```

Animation:

```text
1. Show array
2. Highlight middle
3. Show pointer
4. Display "Middle element"
```

JSON:

```json
{
  "narration": "Binary search checks the middle element first.",

  "visual_elements": [
    "sorted_array",
    "middle_element",
    "pointer"
  ],

  "animation": [
    {
      "action": "show",
      "object": "sorted_array"
    },
    {
      "action": "highlight",
      "object": "middle_element"
    },
    {
      "action": "show",
      "object": "pointer"
    }
  ]
}
```

---

# 12. Scene Types

আমাদের system-এ scene type রাখা খুব useful।

আমি এই types recommend করব:

```text
definition
explanation
diagram
process
comparison
example
step_by_step
timeline
equation
code
algorithm
chart
real_world
summary
question
```

Example:

```json
{
  "scene_type": "algorithm"
}
```

Binary search-এর জন্য।

Photosynthesis:

```json
{
  "scene_type": "process"
}
```

Mathematics:

```json
{
  "scene_type": "equation"
}
```

---

# 13. Educational Visual Patterns

সব educational topic একইভাবে visualize করা উচিত নয়।

### Definition

```text
Term
 ↓
Meaning
 ↓
Simple example
```

### Process

```text
Input
 ↓
Step 1
 ↓
Step 2
 ↓
Output
```

### Comparison

```text
A              B

Fast           Slow
Simple         Complex
```

### Algorithm

```text
Input
 ↓
Step 1
 ↓
Step 2
 ↓
Result
```

### Cause → Effect

```text
Cause
  ↓
Process
  ↓
Effect
```

এই patterns আমাদের Visual Planner-কে আরও intelligent করবে।

---

# 14. Visual Style

User চাইতে পারে:

```text
"Make it like a clean 2D educational animation."
```

অথবা:

```text
"Make it realistic."
```

অথবা:

```text
"Make it whiteboard style."
```

তাই style parameter রাখতে হবে।

Example:

```json
{
  "visual_style": {
    "style": "clean_2d",
    "background": "minimal",
    "text_style": "large",
    "animation": "smooth"
  }
}
```

Possible styles:

```text
clean_2d
whiteboard
realistic
3d
minimal
cartoon
scientific
technical
cinematic
```

---

# 15. Camera Planning

Educational video-তে camera movement-ও দরকার হতে পারে।

Actions:

```text
zoom_in
zoom_out
pan_left
pan_right
pan_up
pan_down
follow
static
```

Example:

```json
{
  "camera": {
    "type": "zoom_in",
    "target": "middle_element",
    "duration": 2
  }
}
```

Binary search:

```text
Full Array
     ↓
    Zoom
     ↓
Middle Element
```

---

# 16. On-screen Text

Narration আর on-screen text একই জিনিস নয়।

Narration:

> "Binary search checks the middle element first."

Screen:

```text
CHECK THE MIDDLE
```

এতে learner দ্রুত concept ধরতে পারে।

আমরা JSON-এ রাখব:

```json
{
  "on_screen_text": [
    {
      "text": "Check the middle",
      "position": "top",
      "duration": 3
    }
  ]
}
```

---

# 17. Diagram Planning

Educational AI-এর জন্য diagram খুব গুরুত্বপূর্ণ।

Example:

```text
Client
  |
  ↓
Router
  |
  ↓
Server
```

JSON:

```json
{
  "diagram": {
    "type": "flowchart",
    "nodes": [
      "Client",
      "Router",
      "Server"
    ],
    "connections": [
      ["Client", "Router"],
      ["Router", "Server"]
    ]
  }
}
```

এরপর Manim বা অন্য renderer diagram তৈরি করবে।

---

# 18. Visual Plan Schema

এখন আমরা একটা proper Pydantic model বানাব।

Install:

```bash
pip install pydantic
```

Create:

```text
planner/
└── visual_schema.py
```

Code:

```python
from pydantic import BaseModel
from typing import List, Optional


class VisualObject(BaseModel):
    name: str
    object_type: str
    position: str
    size: str = "medium"
    label: Optional[str] = None


class AnimationAction(BaseModel):
    action: str
    object: str
    start: float
    duration: float
    target: Optional[str] = None


class CameraPlan(BaseModel):
    action: str = "static"
    target: Optional[str] = None
    duration: float = 0


class VisualPlan(BaseModel):
    scene_id: int
    visual_style: str
    objects: List[VisualObject]
    animations: List[AnimationAction]
    camera: CameraPlan
    on_screen_text: List[str]
```

---

# 19. Example Visual Plan

```python
visual_plan = VisualPlan(
    scene_id=1,

    visual_style="clean_2d",

    objects=[
        VisualObject(
            name="plant",
            object_type="plant",
            position="center",
            size="large",
            label="Plant"
        ),

        VisualObject(
            name="sun",
            object_type="sun",
            position="top_right",
            size="large",
            label="Sun"
        ),

        VisualObject(
            name="sunlight",
            object_type="light_rays",
            position="between",
            size="medium"
        )
    ],

    animations=[
        AnimationAction(
            action="fade_in",
            object="plant",
            start=0,
            duration=1
        ),

        AnimationAction(
            action="fade_in",
            object="sun",
            start=1,
            duration=1
        ),

        AnimationAction(
            action="move",
            object="sunlight",
            start=2,
            duration=2,
            target="plant"
        )
    ],

    camera=CameraPlan(
        action="static"
    ),

    on_screen_text=[
        "Sunlight → Plant"
    ]
)
```

---

# 20. Validation

Visual planning-এ validation খুব গুরুত্বপূর্ণ।

আমরা check করব:

```text
Scene duration
Animation timing
Unknown objects
Negative duration
Overlapping actions
Missing narration
Missing visual
```

Example:

```python
def validate_animation_timing(animations, scene_duration):

    for animation in animations:

        if animation.start < 0:
            raise ValueError(
                "Animation cannot start before 0."
            )

        if animation.duration <= 0:
            raise ValueError(
                "Animation duration must be positive."
            )

        end_time = animation.start + animation.duration

        if end_time > scene_duration:
            raise ValueError(
                "Animation exceeds scene duration."
            )

    return True
```

---

# 21. Object Validation

Animation-এ এমন object ব্যবহার করা যাবে না যেটা scene-এ নেই।

```python
def validate_animation_objects(objects, animations):

    object_names = {
        obj.name
        for obj in objects
    }

    for animation in animations:

        if animation.object not in object_names:

            raise ValueError(
                f"Unknown object: {animation.object}"
            )

    return True
```

এটা খুব useful।

---

# 22. LLM-এর জন্য Visual Planning Prompt

এখন আসল AI অংশ।

LLM-কে আমরা বলব:

```text
You are an educational visual planning engine.

Your task is to convert educational narration
into a structured visual plan.

For each scene determine:

1. Visual objects
2. Object type
3. Position
4. Size
5. Animation actions
6. Animation timing
7. Camera movement
8. On-screen text
9. Visual style

Important rules:

- Visuals must directly support narration.
- Do not introduce unnecessary objects.
- Keep educational accuracy.
- Use simple visual structures for beginners.
- Do not create animation code.
- Return JSON only.
```

Notice:

**LLM code লিখবে না।**

LLM শুধু plan তৈরি করবে।

---

# 23. Full Pipeline এখন

আমাদের project এখন:

```text
User
 ↓
"Explain Binary Search"
 ↓
M8
Educational Planner
 ↓
Learning Objectives
 ↓
M9
Script Generator
 ↓
Narration
 ↓
M10
Visual Planner
 ↓
Visual Objects
 ↓
Animation Plan
 ↓
Camera Plan
 ↓
Text Plan
 ↓
M11
Animation Renderer
```

এখানে M10 হলো **bridge**:

```text
LANGUAGE
   ↓
M9
   ↓
VISUAL INSTRUCTION
   ↓
M10
   ↓
ANIMATION
   ↓
M11
```

---

# 24. সবচেয়ে গুরুত্বপূর্ণ Design Principle

আমাদের project-এর একটা rule মনে রাখবে:

> **LLM decides WHAT should happen. Deterministic code decides HOW it happens.**

Example:

LLM:

```json
{
  "action": "highlight",
  "object": "middle_element"
}
```

Python/Manim:

```python
highlight(middle_element)
```

অর্থাৎ:

```text
LLM
 ↓
JSON
 ↓
Renderer
 ↓
Video
```

এতে system অনেক বেশি controllable হবে।

---

# 25. M10 Mini Project

এখন তোমার task:

### Input

```text
Explain Binary Search to a beginner in 20 seconds.
```

তোমার system-এর output ideally:

```text
Scene 1
0–4 sec
↓
Show sorted array

Scene 2
4–8 sec
↓
Highlight middle element

Scene 3
8–13 sec
↓
Compare target with middle

Scene 4
13–17 sec
↓
Remove half of array

Scene 5
17–20 sec
↓
Show result
```

এবং প্রতিটি scene-এ:

```text
✓ narration
✓ objects
✓ positions
✓ animation
✓ timing
✓ camera
✓ on-screen text
```

---

# 26. M10 Complete Folder Structure

M9-এর folder structure এখন update করি:

```text
educational_video_ai/
│
├── videos/
│
├── frames/
│
├── transcripts/
│
├── vision/
│
├── scenes/
│   ├── source_scenes/
│   ├── generated_scenes/
│   └── visual_plans/
│
├── planner/
│   ├── prompt_parser.py
│   ├── objective_generator.py
│   ├── script_generator.py
│   ├── strategy.py
│   ├── timing.py
│   ├── validator.py
│   │
│   ├── visual_schema.py
│   ├── visual_planner.py
│   └── visual_validator.py
│
├── renderer/
│
├── scripts/
│
├── dataset/
│
└── logs/
```

---

# 27. M10-এর Learning Checklist

M10 শেষ করার আগে এগুলো বুঝতে হবে:

### Concepts

* [x] Educational Visual Planning
* [x] Narration → Visual Mapping
* [x] Visual Objects
* [x] Object Properties
* [x] Layout Planning
* [x] Animation Actions
* [x] Animation Timeline
* [x] Scene Types
* [x] Visual Styles
* [x] Camera Planning
* [x] On-screen Text
* [x] Diagram Planning
* [x] Pydantic Visual Schema
* [x] Visual Validation
* [x] LLM → Visual Plan
* [x] LLM vs Renderer separation

---

# 28. M1 → M10 আমরা কোথায় এসেছি?

এখন পর্যন্ত আমাদের AI pipeline:

```text
M1
Python Pipeline
 ↓
M2
Video Processing
 ↓
M3
Dataset Engineering
 ↓
M4
Whisper
 ↓
M5
Computer Vision
 ↓
M6
Pretrained Vision Model
 ↓
M7
Multimodal Scene Understanding
 ↓
M8
Educational Scene Planner
 ↓
M9
Script Generator
 ↓
M10
Visual Planner
```

এখন আমরা সত্যিই **video generation-এর কাছাকাছি চলে এসেছি।**

---

# 🚀 Next: M11 — Animation Generation Engine

M11 হবে অত্যন্ত গুরুত্বপূর্ণ।

আমরা তখন করব:

```text
Visual Plan JSON
       ↓
Animation Renderer
       ↓
        Manim
       ↓
      MP4
```

যেমন AI output করবে:

```json
{
  "object": "array",
  "action": "show"
}
```

তারপর আমাদের Python engine সেটা বুঝে **নিজে Manim animation তৈরি করবে**।

অর্থাৎ প্রথমবারের মতো:

> **User topic → AI plan → Automatically generated educational animation**

এটাই হবে আমাদের project's প্রথম সত্যিকারের **video generation engine**।



---
