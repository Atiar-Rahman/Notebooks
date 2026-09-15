# M16 — Complete End-to-End Educational Video Generator 🚀

M1–M15 পর্যন্ত আমরা আলাদা আলাদা engine তৈরি করেছি।
**M16-এর মূল লক্ষ্য হলো এগুলোকে একসাথে connect করে একটি working Educational Video AI pipeline বানানো।**

এখন থেকে আমরা আর শুধু “একটা feature কীভাবে কাজ করে” শিখব না—বরং **পুরো product architecture** তৈরি করব।

---

# 1. M16-এ আমরা কী বানাব?

User শুধু লিখবে:

```text
Explain binary search to a beginner in 30 seconds.
```

System নিজে করবে:

```text
User Prompt
    ↓
Prompt Parser
    ↓
Educational Planner
    ↓
Script Generator
    ↓
Scene Planner
    ↓
Visual Planner
    ↓
Animation Generator
    ↓
TTS
    ↓
Subtitle Generator
    ↓
Timeline Sync
    ↓
FFmpeg
    ↓
final_video.mp4
```

অর্থাৎ user-এর কাছে পুরো complexity invisible থাকবে।

---

# 2. Final Product-এর Vision

আমাদের AI-এর interface হতে পারে:

```text
┌────────────────────────────────────────────┐
│        🎓 Educational Video AI             │
├────────────────────────────────────────────┤
│                                            │
│ Topic                                      │
│ ┌────────────────────────────────────────┐ │
│ │ Explain Binary Search                  │ │
│ └────────────────────────────────────────┘ │
│                                            │
│ Audience: Beginner                         │
│ Duration: 30 seconds                       │
│ Language: English                          │
│ Style: Clean 2D Animation                  │
│                                            │
│              [ Generate Video ]            │
│                                            │
└────────────────────────────────────────────┘
```

Click:

```text
Generate Video
```

তারপর:

```text
Generating...
✓ Script
✓ Scene Plan
✓ Visual Plan
✓ Animation
✓ Voice
✓ Subtitle
✓ Composition

100%
```

শেষে:

```text
🎬 video.mp4
```

---

# 3. M16 Architecture

এটাই এখন আমাদের **master architecture**:

```text
                    USER
                     │
                     ▼
              ┌─────────────┐
              │ Prompt API  │
              └──────┬──────┘
                     │
                     ▼
             ┌──────────────┐
             │ LLM Planner  │
             └──────┬───────┘
                    │
              VideoPlan JSON
                    │
        ┌───────────┼────────────┐
        ▼           ▼            ▼
      Script      Visual       Timing
        │           │            │
        ▼           ▼            │
       TTS         Manim         │
        │           │            │
        ▼           ▼            │
      Audio      Scene MP4       │
        │                        │
        ▼                        │
     Whisper                     │
        │                        │
        ▼                        │
    Subtitle                    │
        │                        │
        └───────────┬────────────┘
                    ▼
             Timeline Engine
                    │
                    ▼
               FFmpeg
                    │
                    ▼
              FINAL VIDEO
```

---

# 4. সবচেয়ে গুরুত্বপূর্ণ Architecture Principle

এখানে একটা principle মনে রাখবে:

> **LLM decides what should happen. Deterministic code decides how it happens.**

অর্থাৎ LLM বলবে:

```json
{
  "object": "array",
  "action": "highlight",
  "target": "middle"
}
```

কিন্তু LLM সরাসরি:

```python
self.play(...)
```

লিখবে না।

Renderer করবে:

```text
JSON
 ↓
Interpreter
 ↓
Manim
```

এতে system অনেক stable হবে।

---

# 5. M16 Project Structure

এখন project structure upgrade করব:

```text
educational_video_ai/
│
├── app/
│   ├── __init__.py
│   ├── config.py
│   ├── pipeline.py
│   └── schemas.py
│
├── planner/
│   ├── educational_planner.py
│   ├── script_generator.py
│   └── scene_planner.py
│
├── visual/
│   ├── visual_planner.py
│   └── visual_schema.py
│
├── renderer/
│   ├── factory.py
│   ├── interpreter.py
│   ├── render.py
│   │
│   ├── objects/
│   │   ├── shapes.py
│   │   ├── text.py
│   │   ├── arrays.py
│   │   ├── stack.py
│   │   ├── queue.py
│   │   ├── tree.py
│   │   └── graph.py
│   │
│   └── animations/
│       ├── basic.py
│       ├── movement.py
│       └── highlight.py
│
├── tts/
│   ├── engine.py
│   ├── cleaner.py
│   └── duration.py
│
├── subtitle/
│   ├── transcribe.py
│   ├── srt.py
│   ├── ass.py
│   └── formatter.py
│
├── timeline/
│   ├── scene_manager.py
│   ├── scheduler.py
│   └── sync.py
│
├── composer/
│   ├── ffmpeg.py
│   └── video.py
│
├── projects/
│
├── audio/
├── videos/
├── output/
│
├── scripts/
│   └── generate_video.py
│
├── requirements.txt
└── README.md
```

---

# 6. কেন এতগুলো folder?

কারণ আমরা একটা **AI product** বানাচ্ছি, শুধু একটা Python script না।

Bad architecture:

```text
main.py
2000 lines
```

Better:

```text
planner/
tts/
renderer/
subtitle/
timeline/
composer/
```

প্রতিটি component-এর আলাদা responsibility।

এটা হলো **Separation of Concerns**।

---

# 7. Central Pipeline

সব module connect করবে:

```text
app/pipeline.py
```

Concept:

```python
class EducationalVideoPipeline:

    def generate(self, prompt):
        pass
```

এটাই আমাদের main controller।

---

# 8. Pipeline-এর ধাপ

```text
generate(prompt)
       │
       ├── 1. Create Project
       ├── 2. Generate Plan
       ├── 3. Generate Script
       ├── 4. Generate Visual Plan
       ├── 5. Render Scenes
       ├── 6. Generate Voice
       ├── 7. Generate Subtitle
       ├── 8. Synchronize
       ├── 9. Compose
       └── 10. Return Video
```

---

# 9. Project ID

প্রতিটি video generation-এর জন্য unique project দরকার।

```python
import uuid


def create_project_id():

    return str(uuid.uuid4())
```

Example:

```text
d7e2c8c1-...
```

Project:

```text
projects/
└── d7e2c8c1/
```

---

# 10. Project Folder

একটি generated video:

```text
projects/
└── project_001/
    │
    ├── input.json
    ├── plan.json
    ├── script.json
    │
    ├── scenes/
    │   ├── scene_001.json
    │   ├── scene_001.mp4
    │   ├── scene_001.wav
    │   ├── scene_001.srt
    │   └── scene_001.ass
    │
    ├── audio/
    │
    ├── subtitles/
    │
    └── final.mp4
```

এটা production-এর জন্য অনেক ভালো।

---

# 11. Project State

Pipeline মাঝপথে fail করতে পারে।

যেমন:

```text
✓ Planner
✓ Script
✓ Visual
✗ TTS
```

যদি আবার শুরু করি, সবকিছু পুনরায় generate করা wasteful।

তাই state রাখব:

```json
{
    "project_id": "project_001",
    "status": "tts_failed",

    "steps": {
        "planning": "completed",
        "script": "completed",
        "visual": "completed",
        "render": "completed",
        "tts": "failed",
        "subtitle": "pending",
        "compose": "pending"
    }
}
```

এটা production system-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 12. Pipeline State Machine

```text
CREATED
   ↓
PLANNING
   ↓
SCRIPT_READY
   ↓
VISUAL_READY
   ↓
RENDERING
   ↓
AUDIO_READY
   ↓
SUBTITLE_READY
   ↓
COMPOSING
   ↓
COMPLETED
```

Error হলে:

```text
ANY STEP
   ↓
FAILED
```

---

# 13. Main Pipeline Skeleton

```python
class EducationalVideoPipeline:

    def __init__(
        self,
        planner,
        renderer,
        tts,
        subtitle,
        composer
    ):

        self.planner = planner
        self.renderer = renderer
        self.tts = tts
        self.subtitle = subtitle
        self.composer = composer

    def generate(self, prompt):

        project = self.create_project()

        plan = self.planner.create_plan(
            prompt
        )

        scenes = self.renderer.render(
            plan
        )

        audio = self.tts.generate(
            scenes
        )

        subtitles = self.subtitle.generate(
            audio
        )

        video = self.composer.compose(
            scenes,
            audio,
            subtitles
        )

        return video
```

এখন এটা শুধু skeleton।

পরবর্তী steps-এ আমরা প্রতিটি method বাস্তবে connect করব।

---

# 14. Dependency Injection

এই architecture-এর একটা বড় সুবিধা:

```text
Pipeline
   │
   ├── Planner
   ├── Renderer
   ├── TTS
   ├── Subtitle
   └── Composer
```

Pipeline নিজে জানে না:

```text
কোন LLM?
কোন TTS?
কোন renderer?
```

যেমন:

```python
pipeline = EducationalVideoPipeline(
    planner=OpenAIPlanner(),
    renderer=ManimRenderer(),
    tts=LocalTTS(),
    subtitle=WhisperSubtitle(),
    composer=FFmpegComposer()
)
```

পরে:

```python
pipeline = EducationalVideoPipeline(
    planner=LocalLLMPlanner(),
    renderer=ManimRenderer(),
    tts=AdvancedTTS(),
    subtitle=WhisperSubtitle(),
    composer=FFmpegComposer()
)
```

Pipeline পরিবর্তন করতে হচ্ছে না।

---

# 15. Schema হলো Backbone

M16-এ আমরা structured schema-কে আরও শক্তিশালী করব।

একটি complete `VideoPlan`:

```json
{
    "project_id": "project_001",
    "topic": "Binary Search",
    "subject": "Computer Science",
    "audience": "beginner",
    "difficulty": "beginner",
    "language": "en",
    "duration": 30,
    "style": "clean_2d",

    "learning_objectives": [
        "Understand binary search",
        "Identify the middle element",
        "Understand elimination of half"
    ],

    "scenes": []
}
```

---

# 16. Scene Schema

```json
{
    "scene_id": 1,

    "start": 0,
    "end": 5,

    "narration": {
        "text": "Binary search is a fast way to find an item.",
        "audio": null,
        "duration": null
    },

    "visual": {
        "style": "clean_2d",
        "objects": [],
        "animations": []
    },

    "subtitle": {
        "srt": null,
        "ass": null
    },

    "transition": {
        "type": "fade",
        "duration": 0.5
    }
}
```

এটাই আমাদের **Intermediate Representation (IR)**।

---

# 17. IR কী?

IR = Intermediate Representation.

সহজভাবে:

```text
Human Prompt
     ↓
LLM
     ↓
Structured JSON
     ↓
Renderer
```

এই JSON হলো bridge।

```text
AI
 ↓
JSON
 ↓
Software
```

এটা তোমার entire project-এর অন্যতম গুরুত্বপূর্ণ design decision।

---

# 18. কেন Direct Code Generation করব না?

Bad:

```text
User
 ↓
LLM
 ↓
Manim Python Code
 ↓
Execute
```

Problems:

* invalid code
* security issues
* unpredictable output
* difficult validation
* debugging কঠিন
* style consistency কম

Better:

```text
User
 ↓
LLM
 ↓
Scene JSON
 ↓
Validate
 ↓
Renderer
 ↓
Manim
```

---

# 19. Validation Layer

LLM output বিশ্বাস করা যাবে না।

তাই:

```text
LLM
 ↓
JSON
 ↓
Pydantic
 ↓
Validation
 ↓
Renderer
```

Example:

```python
from pydantic import BaseModel
from typing import List


class Scene(BaseModel):

    scene_id: int
    start: float
    end: float
    narration: str


class VideoPlan(BaseModel):

    topic: str
    duration: float
    scenes: List[Scene]
```

---

# 20. Timing Validation

```python
def validate_timing(scenes):

    previous_end = 0

    for scene in scenes:

        if scene.start < previous_end:
            raise ValueError(
                "Scene overlap detected."
            )

        if scene.end <= scene.start:
            raise ValueError(
                "Invalid scene duration."
            )

        previous_end = scene.end
```

---

# 21. Content Validation

শুধু timing validation যথেষ্ট নয়।

Check:

```text
topic exists?
duration valid?
scene exists?
narration exists?
visual exists?
```

Example:

```python
def validate_plan(plan):

    if not plan.topic:
        raise ValueError(
            "Topic is required."
        )

    if plan.duration <= 0:
        raise ValueError(
            "Duration must be positive."
        )

    if not plan.scenes:
        raise ValueError(
            "At least one scene required."
        )
```

---

# 22. Educational Validation

আরও advanced validation:

```text
Learning objectives
        ↓
Script
        ↓
Scene
```

প্রতিটি objective অন্তত কোনো scene-এ explain হয়েছে কিনা check করতে পারি।

Example:

```text
Objectives:

1. Define binary search
2. Explain middle element
3. Explain half elimination
```

Scene mapping:

```text
Scene 1 → Objective 1
Scene 2 → Objective 2
Scene 3 → Objective 3
```

এতে video শুধু সুন্দর animation না হয়ে **educationally coherent** হবে।

---

# 23. Quality Control Layer

M16 থেকে এটা add করব:

```text
Generated Video
       ↓
Quality Checker
       ↓
┌──────┼─────────┐
▼      ▼         ▼
Audio  Timing   Content
```

Check:

### Audio

```text
audio exists?
duration valid?
```

### Video

```text
video exists?
duration valid?
resolution valid?
```

### Subtitle

```text
subtitle exists?
timestamp valid?
```

### Content

```text
scene count?
object references?
```

---

# 24. Automated Video QA

Function:

```python
def validate_output(video_path):

    checks = {
        "file_exists": False,
        "duration_valid": False,
        "resolution_valid": False
    }

    # perform checks...

    return checks
```

Output:

```json
{
    "file_exists": true,
    "duration_valid": true,
    "resolution_valid": true
}
```

---

# 25. End-to-End CLI

এখন user command line থেকে করতে পারবে:

```bash
python scripts/generate_video.py \
"Explain binary search to a beginner in 30 seconds"
```

Output:

```text
Creating project...

[1/8] Planning...
✓

[2/8] Script generation...
✓

[3/8] Visual planning...
✓

[4/8] Rendering...
✓

[5/8] TTS...
✓

[6/8] Subtitle...
✓

[7/8] Composition...
✓

[8/8] Quality check...
✓

Video generated successfully.

output/project_001/final.mp4
```

---

# 26. CLI Code

```python
import argparse


def main():

    parser = argparse.ArgumentParser()

    parser.add_argument(
        "prompt",
        type=str
    )

    args = parser.parse_args()

    print(
        f"Generating video for: "
        f"{args.prompt}"
    )


if __name__ == "__main__":
    main()
```

Run:

```bash
python scripts/generate_video.py \
"Explain photosynthesis to a beginner in 30 seconds"
```

---

# 27. M16-এর প্রথম Working Version

আমরা প্রথমে সব AI model একসাথে লাগাব না।

**Vertical slice approach** ব্যবহার করব।

প্রথম working system:

```text
Prompt
 ↓
Hardcoded/Mock Plan
 ↓
Manim
 ↓
TTS
 ↓
SRT
 ↓
FFmpeg
 ↓
MP4
```

এটা সফল হলে:

```text
Mock Plan
```

replace করে:

```text
LLM Planner
```

করব।

এটাই professional development approach।

---

# 28. কেন প্রথমে Mock Plan?

ধরো LLM সমস্যা করছে।

তখন যদি পুরো pipeline:

```text
LLM
TTS
Whisper
Manim
FFmpeg
```

একসাথে debug করো, কোন জায়গায় সমস্যা বুঝতে কঠিন হবে।

তাই:

```text
Mock JSON
 ↓
Renderer
 ↓
TTS
 ↓
Subtitle
 ↓
FFmpeg
```

প্রথমে verify করব।

তারপর LLM যোগ করব।

---

# 29. Mock Plan

`projects/test_plan.json`

```json
{
    "project_id": "test_001",
    "topic": "Binary Search",
    "duration": 10,

    "scenes": [
        {
            "scene_id": 1,
            "start": 0,
            "end": 5,

            "narration": {
                "text":
                "Binary search works on sorted data."
            },

            "visual": {
                "objects": [
                    {
                        "name": "array",
                        "object_type": "array",
                        "values": [
                            10, 20, 30, 40, 50
                        ]
                    }
                ]
            }
        },

        {
            "scene_id": 2,
            "start": 5,
            "end": 10,

            "narration": {
                "text":
                "We check the middle element first."
            },

            "visual": {
                "objects": [
                    {
                        "name": "array",
                        "object_type": "array",
                        "values": [
                            10, 20, 30, 40, 50
                        ]
                    }
                ]
            }
        }
    ]
}
```

---

# 30. M16 MVP Pipeline

প্রথম MVP:

```text
test_plan.json
      ↓
Scene Parser
      ↓
Manim Renderer
      ↓
scene_001.mp4
scene_002.mp4
      ↓
TTS
      ↓
voice files
      ↓
Subtitle
      ↓
SRT
      ↓
FFmpeg
      ↓
final.mp4
```

এটা হলো আমাদের **first complete system**।

---

# 31. API Layer

পরবর্তী stage-এ CLI-এর বদলে API দেব।

Architecture:

```text
React Frontend
      ↓
Django / FastAPI
      ↓
Video Generation API
      ↓
Pipeline
      ↓
GPU Worker
      ↓
Final Video
```

তুমি যেহেতু Django/DRF already জানো, backend হিসেবে Django + DRF ব্যবহার করতে পারো।

---

# 32. API Endpoint

Concept:

```http
POST /api/videos/generate/
```

Request:

```json
{
    "prompt":
    "Explain binary search to a beginner",

    "duration": 30,
    "language": "en",
    "style": "clean_2d"
}
```

Response:

```json
{
    "project_id": "project_001",
    "status": "queued"
}
```

---

# 33. কেন `queued`?

Video generation computationally expensive।

HTTP request-এর মধ্যে:

```text
LLM
+
Manim
+
TTS
+
Whisper
+
FFmpeg
```

সব চালালে request অনেকক্ষণ ধরে open থাকবে।

Better:

```text
API
 ↓
Queue
 ↓
Worker
 ↓
GPU
```

---

# 34. Production Architecture

```text
                 React
                   │
                   ▼
              Django API
                   │
                   ▼
              PostgreSQL
                   │
                   ▼
             Redis Queue
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
    CPU Worker            GPU Worker
        │                     │
        │              AI Models
        │                     │
        └──────────┬──────────┘
                   ▼
              Video Storage
                   │
                   ▼
                 CDN
                   │
                   ▼
                User
```

তোমার existing Django/DRF knowledge এখানে কাজে লাগবে।

---

# 35. CPU vs GPU কাজ

সব কাজ GPU-তে করা দরকার নেই।

### CPU

```text
JSON validation
FFmpeg
file management
database
API
```

### GPU

```text
LLM
VLM
TTS
Image generation
Video generation
Whisper large models
```

এতে GPU resource efficient হবে।

---

# 36. Async Job System

Production:

```text
POST /generate
       ↓
job_id
       ↓
Redis
       ↓
Worker
       ↓
Generate
       ↓
Update status
```

Frontend:

```text
GET /jobs/{id}
```

Response:

```json
{
    "status": "rendering",
    "progress": 62
}
```

শেষে:

```json
{
    "status": "completed",
    "progress": 100,
    "video": "..."
}
```

---

# 37. Progress Tracking

আমাদের pipeline:

```text
planning       10%
script         20%
visual         35%
rendering      55%
tts            70%
subtitle       80%
composition    95%
complete       100%
```

এটা UI-তে দেখানো যাবে।

---

# 38. M16 End-to-End Demo

User:

```text
Explain photosynthesis to a beginner in 30 seconds.
```

System:

```text
Project Created
       ↓
Topic:
Photosynthesis

Subject:
Biology

Level:
Beginner

Duration:
30 sec
```

Planner:

```text
Learning objectives:

1. Define photosynthesis
2. Identify sunlight as energy
3. Identify CO₂ and water
4. Understand glucose + oxygen
```

---

# 39. Scene Plan

```text
Scene 1
0–5
What is photosynthesis?

Scene 2
5–12
Sunlight reaches the plant.

Scene 3
12–20
Water + CO₂ enter the process.

Scene 4
20–26
Plant produces glucose and oxygen.

Scene 5
26–30
Quick summary.
```

---

# 40. Visual Plan

```text
Scene 1:
plant + title

Scene 2:
sun → plant

Scene 3:
water + CO₂ → leaf

Scene 4:
glucose + oxygen

Scene 5:
complete process diagram
```

---

# 41. TTS

```text
Scene 1 → voice_001.wav
Scene 2 → voice_002.wav
Scene 3 → voice_003.wav
Scene 4 → voice_004.wav
Scene 5 → voice_005.wav
```

---

# 42. Subtitle

```text
Scene 1 → scene_001.ass
Scene 2 → scene_002.ass
Scene 3 → scene_003.ass
Scene 4 → scene_004.ass
Scene 5 → scene_005.ass
```

---

# 43. Final Composition

```text
Scene 1
+
Scene 2
+
Scene 3
+
Scene 4
+
Scene 5

       ↓

Timeline Engine

       ↓

FFmpeg

       ↓

photosynthesis.mp4
```

---

# 44. M16-এর সবচেয়ে গুরুত্বপূর্ণ lesson

এখন তুমি বুঝবে:

**AI Video Generator = একটি single AI model নয়।**

বরং:

```text
                    AI VIDEO GENERATOR
                           │
      ┌────────────────────┼────────────────────┐
      │                    │                    │
      ▼                    ▼                    ▼
   Language              Vision              Audio
      │                    │                    │
      ▼                    ▼                    ▼
    LLM/VLM             Visual AI            TTS
      │                    │                    │
      └────────────────────┼────────────────────┘
                           ▼
                     Orchestration
                           │
                           ▼
                      Renderer
                           │
                           ▼
                        FFmpeg
```

এটাই তোমার project-এর core idea।

---

# 45. M16 Development Strategy

আমি তোমাকে recommend করব এই order:

### Phase A — Local MVP

```text
Mock JSON
 ↓
Manim
 ↓
Local TTS
 ↓
Whisper
 ↓
SRT
 ↓
FFmpeg
 ↓
MP4
```

### Phase B — AI Planner

```text
User Prompt
 ↓
LLM
 ↓
Scene JSON
 ↓
Existing pipeline
```

### Phase C — Better Visuals

```text
Manim
+
Image Generator
+
Diagram Generator
```

### Phase D — AI Video

```text
Pretrained Video Model
```

### Phase E — Fine-tuning

```text
Educational Dataset
        ↓
LoRA / PEFT
        ↓
Domain Adaptation
```

---

# 46. এখন থেকে আমরা Model Training-এর দিকে যাব

M1–M16 ছিল মূলত:

> **AI Video Generation System Engineering**

এরপর বড় অংশ হবে:

> **AI Model + Dataset + Fine-tuning**

আমাদের পরবর্তী roadmap:

```text
M17 → Educational Dataset & Data Pipeline
M18 → Advanced LLM Integration
M19 → Prompt Engineering + Structured Generation
M20 → VLM-based Visual Understanding
M21 → Image Generation Integration
M22 → Video Generation Models
M23 → LoRA / PEFT Fine-tuning
M24 → Educational Style Fine-tuning
M25 → Evaluation System
M26 → RAG + Trusted Knowledge
M27 → GPU Optimization
M28 → Celery/Redis Distributed Pipeline
M29 → Django + React Production App
M30 → Complete AI Educational Video Generator
```

---

# 47. M16 Mini Project 🎯

এবার তোমার সবচেয়ে গুরুত্বপূর্ণ practical task।

## Project: `EducationalVideoPipeline`

Input:

```text
Explain binary search to a beginner in 20 seconds.
```

Pipeline:

```text
Prompt
 ↓
Mock VideoPlan
 ↓
Validate JSON
 ↓
Render 2–4 scenes
 ↓
Generate TTS
 ↓
Get audio duration
 ↓
Generate subtitles
 ↓
Synchronize timeline
 ↓
Combine scenes
 ↓
Final MP4
```

Expected folder:

```text
projects/
└── binary_search_001/
    │
    ├── plan.json
    │
    ├── scenes/
    │   ├── scene_001.mp4
    │   ├── scene_001.wav
    │   ├── scene_001.srt
    │   │
    │   ├── scene_002.mp4
    │   ├── scene_002.wav
    │   └── scene_002.srt
    │
    └── final.mp4
```

---

# 48. M16 Completion Test

নিজে এই প্রশ্নগুলোর উত্তর দিতে পারলে M16 complete:

### Architecture

* [ ] End-to-end pipeline explain করতে পারি
* [ ] Modular architecture বুঝি
* [ ] Separation of Concerns বুঝি
* [ ] Dependency Injection বুঝি
* [ ] IR/Scene JSON কেন দরকার বুঝি

### Engineering

* [ ] Project ID তৈরি করতে পারি
* [ ] Pipeline state রাখতে পারি
* [ ] Validation করতে পারি
* [ ] Error handling করতে পারি
* [ ] Progress tracking বুঝি

### AI

* [ ] LLM-এর role বুঝি
* [ ] VLM-এর role বুঝি
* [ ] TTS-এর role বুঝি
* [ ] Whisper-এর role বুঝি
* [ ] Animation engine-এর role বুঝি

### Media

* [ ] Video render
* [ ] Audio generation
* [ ] Subtitle generation
* [ ] Timeline synchronization
* [ ] FFmpeg composition

### Production

* [ ] API architecture বুঝি
* [ ] Queue কেন দরকার বুঝি
* [ ] CPU/GPU workload আলাদা করতে পারি
* [ ] Worker architecture বুঝি

---

# 🧠 M1 → M16: আমরা কোথায় পৌঁছেছি?

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
Speech Understanding
        ↓
M5
Computer Vision
        ↓
M6
Vision Models
        ↓
M7
Multimodal Understanding
        ↓
M8
Educational Planning
        ↓
M9
Script Generation
        ↓
M10
Visual Planning
        ↓
M11
Animation Engine
        ↓
M12
Generic Diagram Engine
        ↓
M13
Timeline Engine
        ↓
M14
TTS Engine
        ↓
M15
Subtitle + Sync
        ↓
M16
🔥 COMPLETE PIPELINE
```

এখন সবচেয়ে গুরুত্বপূর্ণ পরিবর্তন হলো:

```text
আগে:
আমরা component বানাচ্ছিলাম।

এখন:
আমরা components দিয়ে PRODUCT বানাচ্ছি।
```

**M17 থেকে আমরা Educational AI-এর জন্য high-quality dataset pipeline তৈরি করব**—কোন data collect করবে, video থেকে কীভাবে script/scene/visual information বের করবে, JSONL dataset বানাবে, train/validation/test split করবে, dataset quality score করবে এবং ভবিষ্যতের **LoRA/fine-tuning-এর জন্য training-ready dataset** তৈরি করবে।
