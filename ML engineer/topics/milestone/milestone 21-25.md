# M21 — Image Generation Integration 🎨🤖

M20 পর্যন্ত তোমার AI-এর:

* 👂 **Ears** → Whisper
* 👁️ **Eyes** → VLM
* 🧠 **Brain** → LLM
* ✋ **Hands** → Manim/Renderer

ছিল।

এখন M21-এ আমরা AI-কে **Creative Visual Generator** দেব।

> **M21-এর লক্ষ্য:** Educational Scene JSON → AI Image Prompt → Image Generation Model → Educational Visual Asset

---

# 1. M21-এ আমরা কী বানাব?

User লিখবে:

```text
Explain photosynthesis to a beginner in 30 seconds.
```

LLM তৈরি করবে:

```text
Scene 1:
Show a green plant receiving sunlight.

Scene 2:
Show water entering through roots.

Scene 3:
Show CO₂ entering leaves.

Scene 4:
Show glucose and oxygen being produced.
```

M21:

```text
Scene JSON
    ↓
Visual Prompt Generator
    ↓
Image Generation Model
    ↓
Generated Image
    ↓
Visual Asset
```

তারপর:

```text
Generated Image
       ↓
Animation
       ↓
TTS
       ↓
Subtitle
       ↓
FFmpeg
       ↓
Educational Video
```

---

# 2. কেন Image Generation দরকার?

M12-এর Manim renderer দিয়ে আমরা তৈরি করতে পারি:

```text
Circle
Square
Arrow
Array
Tree
Graph
Equation
Flowchart
```

কিন্তু ধরো:

> "Show a realistic human heart pumping blood."

Manim দিয়ে এটা করা unnecessary difficult।

Image generation model ব্যবহার করলে:

```text
Prompt
 ↓
AI Image
 ↓
Heart illustration
```

তৈরি করা সম্ভব।

---

# 3. Manim বনাম Image Generation

| Task                       | Manim | Image Generation |
| -------------------------- | ----- | ---------------- |
| Binary Search              | ⭐⭐⭐⭐⭐ | ⭐⭐               |
| Equation                   | ⭐⭐⭐⭐⭐ | ⭐                |
| Flowchart                  | ⭐⭐⭐⭐⭐ | ⭐⭐               |
| Array                      | ⭐⭐⭐⭐⭐ | ⭐                |
| Human anatomy illustration | ⭐⭐    | ⭐⭐⭐⭐⭐            |
| Historical scene           | ⭐     | ⭐⭐⭐⭐⭐            |
| Biology illustration       | ⭐⭐⭐   | ⭐⭐⭐⭐⭐            |
| Realistic environment      | ⭐     | ⭐⭐⭐⭐⭐            |
| Exact labels/text          | ⭐⭐⭐⭐⭐ | ⭐⭐               |

তাই আমরা কোনো একটাকে replace করব না।

বরং:

```text
Manim + Image Generation
```

একসাথে ব্যবহার করব।

---

# 4. M21 Architecture

```text
                         USER
                          │
                          ▼
                    Educational LLM
                          │
                          ▼
                     VideoPlan
                          │
                          ▼
                    Scene Planner
                          │
                          ▼
                    Visual Plan
                          │
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
       Deterministic               Generative
         Visuals                     Visuals
             │                         │
             ▼                         ▼
          Manim                 Image Generator
             │                         │
             └────────────┬────────────┘
                          ▼
                    Scene Composer
                          │
                          ▼
                         MP4
```

---

# 5. সবচেয়ে গুরুত্বপূর্ণ Concept

M21-এ আমরা **LLM-কে সরাসরি image generation prompt লিখতে দেব**, কিন্তু controlled structure-এর মাধ্যমে।

অর্থাৎ:

```text
LLM
 ↓
Visual Specification
 ↓
Prompt Builder
 ↓
Image Model
```

Direct:

```text
LLM → random image prompt
```

এর চেয়ে structured approach ভালো।

---

# 6. Visual Asset Schema

নতুন schema বানাই।

`image/schema.py`

```python
from typing import List, Optional
from pydantic import BaseModel


class ImageRequest(BaseModel):

    scene_id: int

    prompt: str

    negative_prompt: Optional[str] = None

    width: int = 1280
    height: int = 720

    style: str = "educational"

    objects: List[str] = []

    background: str = "simple"
```

এখন image generation request structured হবে।

---

# 7. কেন Schema দরকার?

LLM যদি বলে:

```json
{
  "prompt": "A plant",
  "style": "scientific"
}
```

আমাদের application জানবে:

```text
prompt
style
width
height
objects
background
```

এরপর image generator শুধু structured request গ্রহণ করবে।

---

# 8. Image Generator Abstraction

M18-এর LLM client-এর মতো:

`image/client.py`

```python
from abc import ABC, abstractmethod


class ImageGenerator(ABC):

    @abstractmethod
    def generate(self, request):
        pass
```

এতে পরে আমরা বিভিন্ন provider/model ব্যবহার করতে পারব।

---

# 9. Mock Image Generator

Development-এর জন্য প্রথমে mock তৈরি করো।

```python
class MockImageGenerator(ImageGenerator):

    def generate(self, request):

        print("Generating image...")
        print("Prompt:", request.prompt)

        return {
            "path": f"output/scene_{request.scene_id}.png"
        }
```

এতে actual model ছাড়াই pipeline test করা যাবে।

---

# 10. Image Prompt Generator

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

`image/prompts.py`

```python
def build_image_prompt(
    topic,
    visual_description,
    objects,
    style,
    background
):

    object_text = ", ".join(objects)

    return f"""
Create a high-quality educational illustration.

Topic:
{topic}

Visual description:
{visual_description}

Important objects:
{object_text}

Style:
{style}

Background:
{background}

Requirements:

- Clear educational composition
- Easy to understand
- Focus on the main concept
- Avoid unnecessary objects
- Keep important objects visually distinct
- Suitable for educational video
"""
```

---

# 11. Example

Input:

```python
prompt = build_image_prompt(
    topic="Photosynthesis",
    visual_description=(
        "A green plant receiving sunlight "
        "while water enters through its roots."
    ),
    objects=[
        "sun",
        "green plant",
        "water",
        "roots"
    ],
    style="clean educational illustration",
    background="simple"
)
```

Generated prompt conceptually:

```text
Create a high-quality educational illustration.

Topic:
Photosynthesis

Visual description:
A green plant receiving sunlight while
water enters through its roots.

Important objects:
sun, green plant, water, roots

Style:
clean educational illustration

Background:
simple
```

---

# 12. Prompt Engineering for Image Models

Text LLM prompt এবং Image prompt এক না।

LLM-এর জন্য:

```text
Explain binary search.
```

Image model-এর জন্য visual information বেশি গুরুত্বপূর্ণ:

```text
A clean educational illustration of a sorted
array with five numbered boxes, the middle
element highlighted, simple white background,
clear 2D vector style.
```

Image prompt-এ specify করতে পারো:

```text
subject
composition
objects
camera/view
style
lighting
background
aspect ratio
```

---

# 13. Image Prompt Structure

আমাদের standard:

```text
SUBJECT
+
COMPOSITION
+
OBJECTS
+
ACTION
+
STYLE
+
BACKGROUND
+
CAMERA
+
EDUCATIONAL CONSTRAINTS
```

Example:

```text
A green plant receiving sunlight,
roots absorbing water,
leaves visible,
clean educational scientific illustration,
simple background,
side view,
clear composition,
minimal distractions.
```

---

# 14. Educational Style

আমাদের system-এ style configuration থাকবে:

```python
IMAGE_STYLES = {

    "clean_2d": """
    clean 2D educational illustration,
    flat design, simple shapes
    """,

    "scientific": """
    scientifically accurate educational
    illustration with clear structures
    """,

    "whiteboard": """
    whiteboard educational drawing style
    """,

    "cartoon": """
    friendly educational cartoon illustration
    """,

    "realistic": """
    realistic educational visualization
    """
}
```

---

# 15. Subject-Specific Image Instructions

যেমন Biology:

```python
SUBJECT_VISUAL_RULES = {

    "biology": """
    Show biological structures clearly.
    Prefer labeled educational composition.
    Maintain scientifically appropriate anatomy.
    """,

    "physics": """
    Show physical objects, forces,
    motion and cause-effect relationships clearly.
    """,

    "computer_science": """
    Prefer diagrams, data structures,
    code visualizations and clean technical graphics.
    """,

    "mathematics": """
    Prefer equations, graphs,
    geometric figures and clear spatial relationships.
    """
}
```

---

# 16. Image Generation Pipeline

এখন:

```python
def create_image_request(scene):

    prompt = build_image_prompt(
        topic=scene["topic"],
        visual_description=scene["visual_description"],
        objects=scene["objects"],
        style=scene["style"],
        background=scene["background"]
    )

    return ImageRequest(
        scene_id=scene["scene_id"],
        prompt=prompt,
        style=scene["style"]
    )
```

---

# 17. Image Generation Manager

`image/manager.py`

```python
class ImageManager:

    def __init__(self, generator):
        self.generator = generator

    def generate_scene_image(
        self,
        request
    ):

        result = self.generator.generate(
            request
        )

        return result
```

ব্যবহার:

```python
generator = MockImageGenerator()

manager = ImageManager(
    generator
)

result = manager.generate_scene_image(
    request
)

print(result)
```

---

# 18. এখন Real Model কোথায় বসবে?

Architecture:

```text
ImageManager
      ↓
ImageGenerator Interface
      ↓
┌───────────────┐
│               │
▼               ▼
Cloud Model   Local Model
```

যেমন:

```text
Cloud image generation API
```

অথবা:

```text
Stable Diffusion-family
Flux-family
অন্যান্য open image-generation model
```

তুমি যে model ব্যবহার করবে, সেটা শুধু:

```python
class SomeImageGenerator(ImageGenerator):
    ...
```

implement করবে।

মূল application পরিবর্তন করতে হবে না।

---

# 19. Local Image Generation

Advanced architecture:

```text
Python
  ↓
Diffusion Pipeline
  ↓
GPU
  ↓
PNG
```

Conceptually:

```python
image = pipeline(
    prompt
).images[0]

image.save(
    "output/scene_01.png"
)
```

এখানে actual model, memory requirement এবং inference configuration model অনুযায়ী আলাদা হবে।

---

# 20. কেন Pretrained Model?

আমরা image generation model:

```text
❌ from scratch train
```

করব না।

বরং:

```text
Pretrained Model
      ↓
Prompt
      ↓
Image
```

তারপর ভবিষ্যতে:

```text
Pretrained Model
      ↓
LoRA
      ↓
Educational Style
```

করব।

---

# 21. M23-এর সাথে Connection

আমাদের roadmap:

```text
M21 → Image Generation
M22 → Video Generation
M23 → LoRA / PEFT
M24 → Educational Style Fine-tuning
```

অর্থাৎ এখন আমরা model **use** করব।

পরে model **adapt** করব।

---

# 22. Generated Image Quality Problem

Image model output সবসময় perfect হবে না।

সমস্যা হতে পারে:

```text
Wrong object
Wrong composition
Bad anatomy
Wrong diagram
Unreadable text
Extra objects
Wrong visual concept
```

বিশেষ করে:

> **Exact mathematical/technical text image model-এর উপর blindly rely করা উচিত নয়।**

যেমন image model দিয়ে:

```text
O(log n)
```

সঠিকভাবে render করার guarantee নেই।

তাই:

```text
AI Image
+
Manim/Text Overlay
```

ব্যবহার করব।

---

# 23. Hybrid Rendering ⭐

এটাই তোমার project-এর জন্য খুব গুরুত্বপূর্ণ architecture।

ধরো scene:

```text
"Binary search checks the middle element."
```

Background:

```text
AI-generated educational illustration
```

এর উপর:

```text
Manim
 ↓
Array
 ↓
Exact numbers
 ↓
Highlight
 ↓
Arrow
 ↓
Text
```

Final:

```text
AI Image
   +
Deterministic Graphics
   ↓
High-quality educational scene
```

---

# 24. Hybrid Architecture

```text
              Scene JSON
                  │
          ┌───────┴───────┐
          ▼               ▼
     Image Prompt      Exact Elements
          │               │
          ▼               ▼
    Image Generator      Manim
          │               │
          ▼               ▼
     Background        Labels/Shapes
          │               │
          └───────┬───────┘
                  ▼
             Composition
                  │
                  ▼
                Scene
```

এটা তোমার final system-এর জন্য খুব powerful।

---

# 25. Example — Biology

Scene:

```text
Plants use sunlight to make food.
```

Image Generator:

```text
Plant
Sun
Leaves
Natural environment
```

Manim overlay:

```text
Sunlight
   ↓
Plant
   ↓
Glucose
```

TTS:

```text
"Plants use sunlight to make food."
```

Final scene:

```text
┌──────────────────────────────┐
│          ☀️                  │
│           ↓                  │
│         🌱                   │
│           ↓                  │
│       Food + O₂              │
│                              │
│ Plants use sunlight...       │
└──────────────────────────────┘
```

---

# 26. Image Asset Manager

Generated assets organize করতে হবে।

Structure:

```text
projects/
└── project_001/
    ├── plan.json
    ├── scenes/
    │   ├── scene_001/
    │   │   ├── prompt.txt
    │   │   ├── image.png
    │   │   └── metadata.json
    │   │
    │   └── scene_002/
    │       ├── prompt.txt
    │       ├── image.png
    │       └── metadata.json
```

---

# 27. Image Metadata

প্রতিটি generated image-এর সাথে metadata রাখবে:

```json
{
  "scene_id": 1,
  "prompt": "A green plant receiving sunlight...",
  "model": "image-model",
  "style": "scientific",
  "width": 1280,
  "height": 720
}
```

এটা ভবিষ্যতে debugging/evaluation-এর জন্য খুব দরকারি।

---

# 28. Seed এবং Reproducibility

অনেক image generation system-এ seed ব্যবহার করা যায়।

```text
Prompt
+
Seed
 ↓
Image
```

যদি একই configuration support করে, একই বা কাছাকাছি output পুনরায় পাওয়া সহজ হয়।

Metadata:

```json
{
  "seed": 12345
}
```

Production system-এ generation parameters save করা ভালো।

---

# 29. Multiple Candidates

একটা image generate করে সঙ্গে সঙ্গে ব্যবহার না করে:

```text
Prompt
 ↓
Image 1
Image 2
Image 3
 ↓
Quality Selection
 ↓
Best Image
```

করতে পারো।

---

# 30. Automatic Image Evaluation

Future architecture:

```text
Generated Image
       ↓
VLM
       ↓
Evaluate
       ↓
Does it match the scene?
       │
    ┌──┴──┐
    ▼     ▼
   Yes    No
    │     │
    ▼     ▼
 Accept  Regenerate
```

এটা M20-এর VLM-এর সাথে integrate হবে।

---

# 31. Self-Correction Image Pipeline

ধরো scene চেয়েছিল:

```text
A plant receiving sunlight.
```

Generated image:

```text
Plant + Moon 🌙
```

VLM detect করবে:

```text
Expected: Sun
Found: Moon
```

তারপর:

```text
Regenerate
```

Better prompt:

```text
A green plant receiving bright sunlight
from a clearly visible sun.
```

---

# 32. Image Quality Checker Schema

```python
class ImageEvaluation(BaseModel):

    matches_scene: bool

    visual_quality: float

    educational_relevance: float

    composition_quality: float

    issues: list[str]
```

Example:

```json
{
  "matches_scene": true,
  "visual_quality": 0.91,
  "educational_relevance": 0.94,
  "composition_quality": 0.88,
  "issues": []
}
```

---

# 33. Quality Threshold

```python
def is_acceptable(
    evaluation
):

    return (
        evaluation.matches_scene
        and evaluation.visual_quality >= 0.8
        and evaluation.educational_relevance >= 0.8
    )
```

যদি false:

```text
Regenerate
```

---

# 34. Complete M21 Pipeline

এখন পুরো flow:

```text
User Prompt
     ↓
M19 LLM
     ↓
VideoPlan
     ↓
M10 Visual Planner
     ↓
Scene Visual Specification
     ↓
Image Prompt Builder
     ↓
Image Generation
     ↓
Generated Image
     ↓
M20 VLM Quality Check
     │
     ├── Good → Continue
     │
     └── Bad → Regenerate
     ↓
Hybrid Composition
     ↓
Manim + Image
     ↓
Scene MP4
```

---

# 35. Image Generation + M12 Renderer

M12 renderer ছিল:

```text
Visual JSON
 ↓
Primitive Factory
 ↓
Animation
 ↓
Manim
```

এখন:

```text
Visual JSON
 ↓
Visual Decision
 ├── primitive → Manim
 ├── diagram → Manim
 ├── illustration → Image Generator
 └── hybrid → Image + Manim
```

এটা অনেক বেশি scalable।

---

# 36. Visual Decision Engine

```python
def choose_renderer(scene):

    scene_type = scene["scene_type"]

    if scene_type in [
        "algorithm",
        "equation",
        "code",
        "flowchart"
    ]:
        return "manim"

    if scene_type in [
        "real_world",
        "historical",
        "scientific_illustration"
    ]:
        return "image"

    return "hybrid"
```

এটা পরে আরও intelligent করা যাবে।

---

# 37. Example

### Binary Search

```text
scene_type = algorithm
```

→

```text
Manim
```

### Photosynthesis

```text
scene_type = scientific_illustration
```

→

```text
Image Generation
```

### Physics

```text
scene_type = explanation
```

→

```text
Hybrid
```

---

# 38. M21 Mini Project

এখন একটা simple project তৈরি করো:

```text
Input:
Explain photosynthesis to a beginner.
```

LLM থেকে একটি scene নাও:

```json
{
  "scene_id": 1,
  "visual_description":
    "A green plant receives sunlight.",
  "objects": [
    "sun",
    "plant",
    "sunlight"
  ],
  "style": "clean_2d"
}
```

তারপর:

```text
Scene JSON
    ↓
Image Prompt
    ↓
Image Generator
    ↓
image.png
```

---

# 39. Mini Project — Better Version

আরও ভালো test:

### Scene 1

```text
A green plant receiving sunlight.
```

### Scene 2

```text
Water entering through the roots.
```

### Scene 3

```text
Carbon dioxide entering the leaves.
```

### Scene 4

```text
The plant producing glucose and oxygen.
```

প্রতিটির জন্য image generate করো।

তারপর:

```text
scene_001.png
scene_002.png
scene_003.png
scene_004.png
```

---

# 40. তারপর Manim Overlay

ধরো `scene_001.png`:

```text
Plant + Sun
```

Manim overlay:

```text
Sunlight
    ↓
Plant
```

তাহলে final scene হবে:

```text
Generated Illustration
+
Exact Educational Graphics
```

---

# 41. M21 Common Errors

### ❌ Error 1 — Image model-কে exact diagram-এর দায়িত্ব দেওয়া

যেমন:

```text
Generate exact binary search array:
10 20 30 40 50
```

Image model ভুল করতে পারে।

Better:

```text
Image Model → background
Manim → exact array
```

---

### ❌ Error 2 — Image model দিয়ে text generate করা

Important educational text:

```text
O(log n)
TCP
UDP
F = ma
```

এগুলো deterministic renderer দিয়ে overlay করা ভালো।

---

### ❌ Error 3 — VLM validation না করা

Generated image blindly accept করো না।

```text
Image
 ↓
VLM
 ↓
Quality Check
```

---

### ❌ Error 4 — Every scene AI-generated

সব scene image generation দরকার নেই।

```text
Algorithm → Manim
Equation → Manim
Realistic biology → Image
Mixed → Hybrid
```

---

### ❌ Error 5 — Generated asset save না করা

Prompt + model + settings + output path save করবে।

---

# 42. M21 Production Architecture

```text
                      VIDEO PLAN
                          │
                          ▼
                   VISUAL PLANNER
                          │
                          ▼
                  RENDERING DECISION
                          │
              ┌───────────┼───────────┐
              ▼           ▼           ▼
            MANIM       IMAGE       HYBRID
              │           │           │
              │           ▼           │
              │      IMAGE MODEL      │
              │           │           │
              │           ▼           │
              │      GENERATED IMAGE  │
              │           │           │
              └───────────┼───────────┘
                          ▼
                   VLM QUALITY CHECK
                          │
                    ┌─────┴─────┐
                    ▼           ▼
                  PASS         FAIL
                    │           │
                    ▼           ▼
                COMPOSE      REGENERATE
                    │
                    ▼
                   MP4
```

---

# 43. M21-এ সবচেয়ে গুরুত্বপূর্ণ Design Principle

তোমার AI-এর জন্য:

> **Not every visual should be generated by AI.**

বরং:

```text
Exact visual
    ↓
Deterministic renderer

Creative visual
    ↓
Generative model

Mixed visual
    ↓
Hybrid renderer
```

এটাই তোমার educational video system-এর জন্য সবচেয়ে practical architecture।

---

# 44. M21 Completion Checklist

### Image Generation

* [ ] Image generation কী বুঝতে হবে
* [ ] Image prompt কী
* [ ] Image model vs LLM
* [ ] Pretrained image models
* [ ] Local vs cloud generation
* [ ] Image generation abstraction

### Prompt

* [ ] Subject
* [ ] Composition
* [ ] Objects
* [ ] Action
* [ ] Style
* [ ] Background
* [ ] Camera/view
* [ ] Educational constraints

### Engineering

* [ ] ImageRequest schema
* [ ] ImageGenerator interface
* [ ] Mock generator
* [ ] ImageManager
* [ ] Asset storage
* [ ] Metadata
* [ ] Seed/reproducibility

### Quality

* [ ] VLM evaluation
* [ ] Image quality score
* [ ] Educational relevance
* [ ] Regeneration
* [ ] Self-correction

### Architecture

* [ ] Manim renderer
* [ ] Image renderer
* [ ] Hybrid renderer
* [ ] Renderer decision engine

---

# 🔥 M21-এর Final Picture

এখন তোমার Educational Video AI-এর architecture:

```text
                         USER
                          │
                          ▼
                         LLM
                          │
                          ▼
                    VideoPlan JSON
                          │
                          ▼
                    Visual Planner
                          │
             ┌────────────┼────────────┐
             ▼            ▼            ▼
           Manim        Image        Hybrid
             │            │            │
             │            ▼            │
             │       Image Model       │
             │            │            │
             │            ▼            │
             │       Generated Image   │
             │            │            │
             └────────────┼────────────┘
                          ▼
                         VLM
                          │
                    Quality Check
                          │
                   ┌──────┴──────┐
                   ▼             ▼
                 PASS          FAIL
                   │             │
                   ▼             ▼
               Compose       Regenerate
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
             EDUCATIONAL MP4
```

## 🧠 M21-এর Golden Rule

```text
LLM
 = What should be shown?

Image Model
 = Generate creative visual

Manim
 = Generate exact visual

VLM
 = Check whether the visual is correct

FFmpeg
 = Assemble everything
```

এখন তোমার system শুধু **script + animation** বানাতে পারবে না; প্রয়োজনে **AI-generated visual assets + deterministic educational graphics** মিলিয়ে অনেক richer educational video তৈরি করতে পারবে।

### পরবর্তী: M22 — Video Generation Models 🎬

M21-এ:

```text
Scene → Image
```

M22-এ আমরা যাব:

```text
Scene
  ↓
Text/Image Prompt
  ↓
Video Generation Model
  ↓
Short AI Video Clip
  ↓
VLM Quality Check
  ↓
Scene Composition
  ↓
Final Educational Video
```

এখান থেকেই তোমার project **text-to-image থেকে actual AI video generation**-এর দিকে যাবে।

----
# M22 — Video Generation Models 🎬🤖

M21-এ আমরা শিখেছি:

```text
Scene
 ↓
Image Prompt
 ↓
Image Generation
 ↓
Educational Image
```

এখন M22-এ আমরা এটাকে এক ধাপ এগিয়ে নিয়ে যাব:

```text
Scene
 ↓
Text / Image Prompt
 ↓
Video Generation Model
 ↓
AI Video Clip
 ↓
VLM Quality Check
 ↓
Scene Composition
 ↓
Final Educational Video
```

এটাই তোমার project-এর **actual AI video generation layer**।

---

# 1. M22-এর মূল লক্ষ্য

ধরো user লিখল:

> **"Explain how blood flows through the human heart in 20 seconds."**

M18/M19 তৈরি করবে:

```json
{
  "topic": "Blood Flow Through the Heart",
  "duration": 20,
  "scenes": [
    {
      "scene_id": 1,
      "start": 0,
      "end": 5,
      "narration": "Blood enters the right side of the heart.",
      "visual_description": "Blood flowing into the right atrium.",
      "scene_type": "process"
    },
    {
      "scene_id": 2,
      "start": 5,
      "end": 10,
      "narration": "It moves into the right ventricle.",
      "visual_description": "Blood moving from atrium to ventricle.",
      "scene_type": "process"
    }
  ]
}
```

M22-এর কাজ:

```text
Visual Description
       ↓
Video Prompt
       ↓
Video Generation Model
       ↓
5-second AI Video
```

---

# 2. Image Generation বনাম Video Generation

M21:

```text
Text
 ↓
Image
```

M22:

```text
Text/Image
 ↓
Video
```

কিন্তু সবচেয়ে গুরুত্বপূর্ণ পার্থক্য:

### Image

একটি frame:

```text
🌱 Plant
☀️ Sun
```

### Video

সময় অনুযায়ী পরিবর্তন:

```text
0 sec → Sun appears
1 sec → Sunlight moves
2 sec → Plant reacts
3 sec → Leaves move
4 sec → Camera moves
```

অর্থাৎ:

> **Video = Visual + Time + Motion**

---

# 3. Video Generation Model কী করে?

Conceptually:

```text
Text Prompt
     +
Optional Image
     +
Motion Instruction
        ↓
Video Generation Model
        ↓
Frames
        ↓
Video
```

একটি video model-এর কাজ:

```text
"Create a plant growing from a seed"
```

থেকে temporal sequence তৈরি করা।

---

# 4. Text-to-Video

সবচেয়ে basic:

```text
Text
 ↓
Video Model
 ↓
Video
```

Example:

```text
A seed grows into a small green plant
in a clean educational animation style.
```

Output:

```text
seed
 ↓
sprout
 ↓
plant
```

---

# 5. Image-to-Video

এটা তোমার project-এর জন্য আরও গুরুত্বপূর্ণ।

M21-এর generated image:

```text
Plant + Sun
```

তারপর:

```text
Image
 +
Motion Prompt
 ↓
Video Model
 ↓
Animated Plant
```

Motion prompt:

```text
The sunlight gently moves toward
the plant while the leaves move slightly.
```

Architecture:

```text
M21
Image Generation
      ↓
Initial Image
      ↓
M22
Image-to-Video
      ↓
Motion
      ↓
Video
```

---

# 6. কেন Image-to-Video গুরুত্বপূর্ণ?

Text-to-video-তে model পুরো scene নিজে তৈরি করে।

ফলে:

```text
❌ Object পরিবর্তন
❌ Composition পরিবর্তন
❌ Character পরিবর্তন
❌ Wrong visual
```

হতে পারে।

Image-to-video-তে:

```text
Initial Image
      ↓
Video Model
      ↓
Motion
```

তাই visual consistency তুলনামূলকভাবে বেশি control করা যায়।

---

# 7. তোমার Educational AI-এর জন্য Best Strategy

আমি recommend করব:

```text
           Scene JSON
               │
               ▼
         Visual Planner
               │
       ┌───────┴────────┐
       ▼                ▼
    Static             Motion
    Scene               Scene
       │                │
       ▼                ▼
 Image Generation   Video Generation
       │                │
       └───────┬────────┘
               ▼
            Compose
```

অর্থাৎ প্রতিটি scene-এ video model ব্যবহার করার দরকার নেই।

---

# 8. Scene-এর জন্য Renderer Decision

M21-এ আমরা করেছিলাম:

```python
def choose_renderer(scene):

    scene_type = scene["scene_type"]

    if scene_type in [
        "algorithm",
        "equation",
        "code",
        "flowchart"
    ]:
        return "manim"

    if scene_type in [
        "real_world",
        "historical",
        "scientific_illustration"
    ]:
        return "image"

    return "hybrid"
```

M22-এ এটাকে expand করব:

```python
def choose_renderer(scene):

    scene_type = scene["scene_type"]

    if scene_type in [
        "algorithm",
        "equation",
        "code",
        "flowchart"
    ]:
        return "manim"

    if scene_type in [
        "real_world",
        "historical"
    ]:
        return "video"

    if scene_type in [
        "scientific_illustration",
        "process"
    ]:
        return "hybrid"

    return "image"
```

---

# 9. Static বনাম Motion

ধরো:

> "Binary search is a search algorithm."

Static image যথেষ্ট।

```text
Binary Search
[10][20][30][40][50]
```

কিন্তু:

> "The algorithm checks the middle element and eliminates half of the array."

এখানে motion দরকার।

```text
[10][20][30][40][50]
          ↑
        middle
          ↓
[10][20]     [40][50]
```

এখানে Manim actually video generation model-এর চেয়েও ভালো।

---

# 10. কখন Video Model ব্যবহার করবে?

Use Video Model যখন:

### 1. Real-world motion

```text
A person running
```

### 2. Natural movement

```text
Water flowing
```

### 3. Biological movement

```text
Heart beating
```

### 4. Physics

```text
Ball falling
```

### 5. Historical/environmental scene

```text
Ancient city marketplace
```

### 6. Cinematic illustration

```text
Solar system moving through space
```

---

# 11. কখন Video Model ব্যবহার করবে না?

Exact educational information-এর জন্য:

```text
❌ Equation
❌ Code
❌ Array
❌ Graph labels
❌ Mathematical diagram
❌ Exact flowchart
```

এসবের জন্য:

```text
Manim
SVG
HTML/CSS
Canvas
```

better।

---

# 12. M22 Video Request Schema

`video/schema.py`

```python
from typing import Optional
from pydantic import BaseModel


class VideoRequest(BaseModel):

    scene_id: int

    prompt: str

    negative_prompt: Optional[str] = None

    duration: float = 5

    width: int = 1280
    height: int = 720

    fps: int = 24

    style: str = "educational"

    motion_strength: float = 0.5

    input_image: Optional[str] = None
```

এখানে:

```text
prompt
duration
resolution
fps
style
motion_strength
input_image
```

থাকছে।

---

# 13. Video Generator Interface

M21-এর মতো abstraction:

```python
from abc import ABC, abstractmethod


class VideoGenerator(ABC):

    @abstractmethod
    def generate(self, request):
        pass
```

এতে provider/model change করলেও পুরো application বদলাতে হবে না।

---

# 14. Mock Video Generator

Development-এর সময়:

```python
class MockVideoGenerator(VideoGenerator):

    def generate(self, request):

        print("Generating video...")
        print("Prompt:", request.prompt)

        return {
            "path": f"output/scene_{request.scene_id}.mp4"
        }
```

এটা প্রথমে ব্যবহার করো।

---

# 15. Video Prompt Generator

`video/prompts.py`

```python
def build_video_prompt(
    topic,
    visual_description,
    motion_instruction,
    style
):

    return f"""
Create a short educational video.

Topic:
{topic}

Visual description:
{visual_description}

Motion:
{motion_instruction}

Style:
{style}

Requirements:

- Keep the main subject consistent.
- Use clear educational composition.
- Keep motion natural and relevant.
- Avoid unnecessary objects.
- Do not introduce unrelated concepts.
"""
```

---

# 16. Example

Input:

```python
prompt = build_video_prompt(
    topic="Photosynthesis",

    visual_description=(
        "A green plant standing under sunlight."
    ),

    motion_instruction=(
        "Sunlight rays move gently toward "
        "the leaves while the leaves move slightly."
    ),

    style="clean educational animation"
)
```

Result conceptually:

```text
Create a short educational video.

A green plant standing under sunlight.

Sunlight rays move gently toward the leaves
while the leaves move slightly.

Clean educational animation.
```

---

# 17. Motion Prompt ⭐

M22-এর সবচেয়ে গুরুত্বপূর্ণ নতুন concept হলো:

> **Motion Prompt**

Image prompt:

```text
A green plant under sunlight.
```

Video prompt:

```text
A green plant under sunlight.
Sunlight rays gently move toward the leaves.
Leaves move slightly in the breeze.
Camera remains stable.
```

Motion আলাদা করে define করলে output control করা সহজ হয়।

---

# 18. Motion Schema

```python
class MotionPlan(BaseModel):

    primary_motion: str

    secondary_motion: list[str] = []

    camera_motion: str = "static"

    motion_strength: float = 0.5
```

Example:

```json
{
  "primary_motion": "sunlight moves toward the plant",
  "secondary_motion": [
    "leaves move gently"
  ],
  "camera_motion": "static",
  "motion_strength": 0.4
}
```

---

# 19. Camera Motion

Video generation-এ camera movement important:

```text
static
zoom_in
zoom_out
pan_left
pan_right
tilt_up
tilt_down
tracking
orbit
```

Example:

```text
Solar System
```

Camera:

```text
zoom_out
```

কারণ পুরো solar system reveal করা হবে।

---

# 20. Motion Types

তোমার system-এ standard vocabulary রাখো:

```python
MOTION_TYPES = [
    "appear",
    "move",
    "grow",
    "rotate",
    "flow",
    "expand",
    "contract",
    "transform",
    "highlight",
    "camera_zoom",
    "camera_pan",
    "camera_static"
]
```

এতে LLM random motion instruction কম দেবে।

---

# 21. Video Model Abstraction

Architecture:

```text
VideoManager
      ↓
VideoGenerator
      ↓
┌───────────────┐
│               │
▼               ▼
Cloud API     Local Model
```

একই application:

```python
generator = SomeVideoGenerator()
```

ব্যবহার করবে।

---

# 22. Local vs Cloud

### Cloud

Advantages:

```text
✅ সহজ setup
✅ GPU দরকার নেই
✅ powerful models
```

Disadvantages:

```text
❌ API cost
❌ internet dependency
❌ rate limits
```

### Local

Advantages:

```text
✅ Full control
✅ No per-generation API cost
✅ Fine-tuning possibility
```

Disadvantages:

```text
❌ High VRAM requirement
❌ Slower
❌ Model setup difficult
```

তোমার বর্তমান PC setup দিয়ে বড় video diffusion model local-এ চালানো সবসময় practical নাও হতে পারে। তাই development-এর সময় API-based model বা ছোট open-source model দিয়ে শুরু করা ভালো।

---

# 23. Video Generation Cost Problem

একটি educational video:

```text
60 seconds
```

যদি model শুধু:

```text
5 sec
```

clip generate করে, তাহলে:

```text
60 / 5 = 12 clips
```

প্রয়োজন।

প্রতিটি scene regenerate করলে cost দ্রুত বাড়বে।

তাই:

> **Video generation model পুরো video generate করবে না।**

আমরা short clips generate করব।

---

# 24. Short Clip Strategy ⭐⭐⭐

আমাদের system:

```text
60 sec Video

Scene 1 → 5 sec
Scene 2 → 5 sec
Scene 3 → 6 sec
Scene 4 → 5 sec
Scene 5 → 7 sec
...
```

প্রতিটি scene independently generate:

```text
Scene 1 → clip_001.mp4
Scene 2 → clip_002.mp4
Scene 3 → clip_003.mp4
```

তারপর FFmpeg:

```text
clip 1
 +
clip 2
 +
clip 3
 ↓
Full Video
```

---

# 25. Video Continuity Problem

এক scene শেষ:

```text
Plant on left
```

পরের scene:

```text
Plant on right
```

দেখতে inconsistent লাগবে।

Solution:

```text
Scene 1
   ↓
Last Frame
   ↓
Scene 2 Initial Image
   ↓
Video Generation
```

Architecture:

```text
Scene 1 Video
      ↓
Last Frame Extraction
      ↓
Scene 2 Image
      ↓
Image-to-Video
```

এভাবে temporal continuity improve করা যায়।

---

# 26. Keyframe Architecture

Advanced system:

```text
Scene
 ↓
Start Keyframe
 ↓
Video Model
 ↓
End Frame
```

তারপর:

```text
End Frame
 ↓
Next Scene Start
```

এটা long educational video-এর consistency-এর জন্য গুরুত্বপূর্ণ।

---

# 27. M22 Scene Schema

আমাদের Scene JSON এখন আরও powerful:

```json
{
  "scene_id": 1,
  "start": 0,
  "end": 5,

  "narration":
    "Plants use sunlight to make food.",

  "visual": {
    "type": "video",
    "description":
      "A green plant under sunlight."
  },

  "motion": {
    "primary":
      "sunlight rays move toward leaves",
    "secondary": [
      "leaves move gently"
    ],
    "camera": "static"
  },

  "style": "clean_2d",

  "continuity": {
    "use_previous_frame": false
  }
}
```

---

# 28. Video Quality Checker

M20 VLM এখন M22-এ অত্যন্ত গুরুত্বপূর্ণ।

```text
Generated Video
       ↓
Frame Sampling
       ↓
VLM
       ↓
Quality Evaluation
```

---

# 29. Video Evaluation

Check:

```text
1. Subject consistency
2. Motion correctness
3. Scene relevance
4. Visual quality
5. Educational relevance
6. Temporal consistency
```

Schema:

```python
class VideoEvaluation(BaseModel):

    scene_match: float

    visual_quality: float

    motion_quality: float

    educational_relevance: float

    temporal_consistency: float

    issues: list[str]
```

---

# 30. Overall Score

```python
def video_quality_score(evaluation):

    return (
        evaluation.scene_match * 0.25
        + evaluation.visual_quality * 0.20
        + evaluation.motion_quality * 0.20
        + evaluation.educational_relevance * 0.20
        + evaluation.temporal_consistency * 0.15
    )
```

Threshold:

```python
if score >= 0.80:
    accept()
else:
    regenerate()
```

---

# 31. Regeneration Loop

```text
Video Prompt
     ↓
Generate
     ↓
VLM Evaluation
     ↓
Score
     │
 ┌───┴────┐
 ▼        ▼
PASS     FAIL
 │        │
 ▼        ▼
Accept   Improve Prompt
            │
            ▼
         Generate
```

এটা self-correcting system-এর শুরু।

---

# 32. Prompt Correction

যদি VLM বলে:

```text
Issue:
Plant disappears halfway through video.
```

Correction prompt:

```text
Maintain the same green plant throughout
the entire clip. Do not change the plant,
camera framing, or background.
```

তারপর regenerate।

---

# 33. VLM + Video

M20 ছিল:

```text
Image → VLM
```

এখন:

```text
Video
 ↓
Frames
 ↓
VLM
 ↓
Temporal Visual Analysis
```

Example:

```text
Frame 1 → Plant
Frame 2 → Plant
Frame 3 → Plant
Frame 4 → Plant
```

Good.

কিন্তু:

```text
Frame 1 → Plant
Frame 2 → Plant
Frame 3 → Tree
Frame 4 → Car
```

VLM detect করতে পারবে:

```text
Temporal inconsistency
```

---

# 34. Video Generation-এর বড় সমস্যা

বর্তমান generative video systems-এ সাধারণ সমস্যা:

```text
❌ Temporal inconsistency
❌ Object identity drift
❌ Physics errors
❌ Text errors
❌ Anatomy errors
❌ Exact diagram errors
❌ Long-video consistency
```

তাই educational AI-এর ক্ষেত্রে model output blindly ব্যবহার করা যাবে না।

---

# 35. সবচেয়ে গুরুত্বপূর্ণ Architecture

তোমার system হবে:

```text
              EDUCATIONAL SCENE
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Exact       Static      Motion
       Visual      Visual      Visual
          │          │          │
          ▼          ▼          ▼
        Manim       Image      Video
          │          │          │
          └──────────┼──────────┘
                     ▼
                  VLM Check
                     │
                     ▼
                  Compose
```

এটাই **hybrid educational video generation system**।

---

# 36. Example — Binary Search

User:

```text
Explain binary search in 15 seconds.
```

Scene 1:

```text
Definition
```

→ Manim

Scene 2:

```text
Sorted array
```

→ Manim

Scene 3:

```text
Middle element highlighted
```

→ Manim

Scene 4:

```text
Fast transition / conceptual visualization
```

→ Image/Video model optional

অর্থাৎ:

```text
Binary Search
     ↓
Mostly Manim
```

---

# 37. Example — Photosynthesis

User:

```text
Explain photosynthesis in 20 seconds.
```

Scene 1:

```text
Plant under sunlight
```

→ Image/Video

Scene 2:

```text
Water entering roots
```

→ Video

Scene 3:

```text
CO₂ entering leaf
```

→ Hybrid

Scene 4:

```text
Chemical equation
```

→ Manim

Final:

```text
Video
+
Video
+
Hybrid
+
Manim
```

---

# 38. Example — Physics

Prompt:

> Explain gravity to a beginner.

Scene 1:

```text
Apple falling from tree
```

→ Video Generation

Scene 2:

```text
Earth attracting object
```

→ Image + animation

Scene 3:

```text
F = ma
```

→ Manim

Scene 4:

```text
Summary
```

→ Manim/Text

এটাই smart renderer architecture।

---

# 39. Video Asset Structure

```text
projects/
└── project_001/
    ├── plan.json
    │
    ├── scenes/
    │   ├── scene_001/
    │   │   ├── prompt.txt
    │   │   ├── request.json
    │   │   ├── video.mp4
    │   │   ├── first_frame.jpg
    │   │   ├── last_frame.jpg
    │   │   └── evaluation.json
    │   │
    │   └── scene_002/
    │       ├── prompt.txt
    │       ├── request.json
    │       ├── video.mp4
    │       └── evaluation.json
    │
    └── output/
        └── final.mp4
```

---

# 40. Video Metadata

```json
{
  "scene_id": 1,
  "model": "video-model",
  "prompt": "A green plant...",
  "duration": 5,
  "width": 1280,
  "height": 720,
  "fps": 24,
  "generation_type": "image_to_video"
}
```

Future debugging-এর জন্য এগুলো খুব important।

---

# 41. Video Generator Manager

```python
class VideoManager:

    def __init__(self, generator):
        self.generator = generator

    def generate_scene(self, request):

        result = self.generator.generate(
            request
        )

        return result
```

Usage:

```python
generator = MockVideoGenerator()

manager = VideoManager(
    generator
)

result = manager.generate_scene(
    request
)

print(result)
```

---

# 42. Complete M22 Flow

এখন পুরো M22:

```text
User Prompt
     ↓
M19 LLM
     ↓
VideoPlan
     ↓
M10 Visual Planner
     ↓
Scene JSON
     ↓
Renderer Decision
     │
     ├─────────────┬──────────────┐
     ▼             ▼              ▼
   Manim         Image          Video
     │             │              │
     │             │         Video Model
     │             │              │
     │             ▼              ▼
     │          Image Model    Video Clip
     │             │              │
     └─────────────┼──────────────┘
                   ▼
              VLM Quality Check
                   │
              ┌────┴────┐
              ▼         ▼
            PASS       FAIL
              │         │
              │      Regenerate
              │
              ▼
          Scene Composer
              ↓
             TTS
              ↓
          Subtitles
              ↓
            FFmpeg
              ↓
       Educational Video
```

---

# 43. M22 Folder Structure

তোমার existing project-এ যোগ করো:

```text
educational_video_ai/
│
├── video_generation/
│   ├── __init__.py
│   ├── schema.py
│   ├── client.py
│   ├── prompts.py
│   ├── manager.py
│   ├── evaluator.py
│   ├── continuity.py
│   └── mock.py
│
├── image/
│   ├── schema.py
│   ├── client.py
│   ├── prompts.py
│   └── manager.py
│
├── vlm/
│   ├── client.py
│   ├── analyzer.py
│   └── evaluator.py
│
├── renderer/
├── planner/
├── tts/
├── subtitle/
├── timeline/
├── composer/
└── projects/
```

---

# 44. M22 Mini Project

এখন আমরা খুব ছোট একটি project বানাব।

## Input

```text
Explain how a seed grows into a plant.
```

## Scene Plan

```text
Scene 1 — Seed
Scene 2 — Sprout
Scene 3 — Young plant
Scene 4 — Mature plant
```

---

## Scene 1

```json
{
  "scene_id": 1,
  "visual_description":
    "A seed placed in soil.",
  "motion": {
    "primary":
      "camera slowly moves toward the seed"
  }
}
```

→ Image-to-video

---

## Scene 2

```json
{
  "scene_id": 2,
  "visual_description":
    "A small green sprout emerges from soil.",
  "motion": {
    "primary":
      "the sprout slowly grows upward"
  }
}
```

→ Video generation

---

## Scene 3

```json
{
  "scene_id": 3,
  "visual_description":
    "A young plant develops several leaves.",
  "motion": {
    "primary":
      "leaves slowly unfold"
  }
}
```

→ Video generation

---

## Scene 4

```json
{
  "scene_id": 4,
  "visual_description":
    "A healthy mature plant.",
  "motion": {
    "primary":
      "plant gently moves in the breeze"
  }
}
```

→ Image-to-video

---

# 45. তারপর TTS

Narration:

```text
A seed begins its journey underground.
With water and suitable conditions,
a small sprout emerges.
The plant develops leaves and continues growing.
```

M14:

```text
Text
 ↓
TTS
 ↓
voice.wav
```

---

# 46. Subtitle

M15:

```text
voice.wav
 ↓
Whisper
 ↓
timestamps
 ↓
SRT
```

---

# 47. Final Composition

M13/M16:

```text
Scene 1
+
Scene 2
+
Scene 3
+
Scene 4
+
Voice
+
Subtitle
```

→

```text
plant_growth.mp4
```

---

# 48. M22-এর সবচেয়ে গুরুত্বপূর্ণ নতুন Concept

আগের architecture:

```text
LLM
 ↓
Scene
 ↓
Image
```

এখন:

```text
LLM
 ↓
Scene
 ↓
Renderer Decision
 ↓
┌───────────────┐
│ Manim         │
│ Image         │
│ Video         │
│ Hybrid        │
└───────────────┘
```

এটাই তোমার system-কে **general-purpose educational video generator** বানাবে।

---

# 49. Foundation Model Train করা লাগবে?

না।

এখন:

```text
❌ Train video model from scratch
```

করবে না।

বরং:

```text
Pretrained Video Model
        ↓
Prompt
        ↓
Video
```

ব্যবহার করবে।

পরবর্তীতে:

```text
Pretrained Model
        ↓
Educational Dataset
        ↓
LoRA / PEFT
        ↓
Educational Video Style
```

এটা M23/M24-এ আসবে।

---

# 50. M22 → M23 Connection

এখন পর্যন্ত:

```text
M18 → LLM
M19 → Prompt
M20 → VLM
M21 → Image Generation
M22 → Video Generation
```

পরবর্তী:

```text
M23 → LoRA / PEFT Fine-tuning
```

M23-এ আমরা শিখব:

```text
Pretrained Model
      ↓
Educational Dataset
      ↓
LoRA
      ↓
Fine-tuned Model
```

---

# 51. M22 Completion Checklist

### Video Generation

* [ ] Text-to-video
* [ ] Image-to-video
* [ ] Short clip generation
* [ ] Motion prompt
* [ ] Camera motion
* [ ] Video request schema
* [ ] Video generator abstraction
* [ ] Video manager

### Architecture

* [ ] Manim renderer
* [ ] Image renderer
* [ ] Video renderer
* [ ] Hybrid renderer
* [ ] Renderer decision engine

### Quality

* [ ] VLM video evaluation
* [ ] Temporal consistency
* [ ] Scene matching
* [ ] Motion quality
* [ ] Regeneration
* [ ] Prompt correction

### Production

* [ ] Scene-level video generation
* [ ] Keyframes
* [ ] Previous-frame continuity
* [ ] Video metadata
* [ ] Asset management
* [ ] FFmpeg composition

---

# 🧠 M22-এর Golden Rule

```text
Manim
= Exact educational graphics

Image Model
= Creative static visuals

Video Model
= Creative motion

VLM
= Visual quality control

LLM
= Educational intelligence

FFmpeg
= Final assembly
```

আর সবচেয়ে গুরুত্বপূর্ণ:

> **Video generation model তোমার পুরো educational video বানাবে না। এটি scene-level visual generator হিসেবে কাজ করবে।**

তাহলে system হবে:

```text
             EDUCATIONAL AI
                   │
                   ▼
                  LLM
                   │
                   ▼
              Scene Planner
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
      Manim      Image      Video
        │          │          │
        └──────────┼──────────┘
                   ▼
                  VLM
                   │
                   ▼
             Quality Check
                   │
                   ▼
              Scene Compose
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
       🎬 EDUCATIONAL VIDEO
```

**M22 শেষ হলে তোমার project-এর generative layer দাঁড়িয়ে গেল।**

**পরবর্তী M23 → LoRA / PEFT Fine-tuning:** pretrained image/video/LLM/VLM model-কে তোমার **educational visual style ও structured generation requirements** অনুযায়ী কীভাবে fine-tune করবে—সেটা শুরু হবে।


---
# M23 — LoRA / PEFT Fine-tuning 🤖🧠

M22 পর্যন্ত আমরা **pretrained models ব্যবহার** করেছি।

এখন M23-এ আমরা শিখব কীভাবে pretrained model-কে **তোমার নিজের educational video system-এর জন্য adapt** করা যায়।

সবচেয়ে গুরুত্বপূর্ণ কথা:

> **M23-এ আমরা model from scratch train করব না। Pretrained model-এর ওপর ছোট, efficient fine-tuning করব।**

---

# 1. M23-এর মূল লক্ষ্য

আমাদের বর্তমান system:

```text id="c1a7d4"
User Prompt
     ↓
LLM
     ↓
Scene JSON
     ↓
Image / Video Model
     ↓
Educational Video
```

কিন্তু pretrained model generic।

আমরা চাই:

```text id="q8m2v1"
Pretrained Model
       +
Educational Dataset
       ↓
LoRA / PEFT
       ↓
Educationally Adapted Model
```

যাতে model তোমার desired style/format/behavior আরও ভালোভাবে follow করে।

---

# 2. Fine-tuning কী?

ধরো pretrained model ইতিমধ্যে অনেক data থেকে শিখেছে:

```text id="j2x9k3"
Images
Videos
Text
Concepts
Styles
```

এখন আমরা তাকে নতুন করে সব শেখাব না।

বরং বলব:

> "আমার educational application-এ এই ধরনের output চাই।"

উদাহরণ:

```text id="m7v4p8"
Generic Image Model
        ↓
Educational Dataset
        ↓
Fine-tuning
        ↓
Educational Visual Model
```

---

# 3. From Scratch বনাম Fine-tuning

### From Scratch

```text id="s4n8q2"
Random Model
    ↓
Huge Dataset
    ↓
Huge GPU
    ↓
Long Training
    ↓
New Model
```

খরচ এবং computational requirement অনেক বেশি।

### Fine-tuning

```text id="u3k6w9"
Pretrained Model
      ↓
Small/medium dataset
      ↓
LoRA
      ↓
Adapter
      ↓
Specialized Model
```

এটাই practical।

---

# 4. PEFT কী?

**PEFT = Parameter-Efficient Fine-Tuning**

এর উদ্দেশ্য:

> পুরো model-এর সব parameter train না করে অল্প কিছু parameter train করা।

ধরো model:

```text id="n5r2x8"
1 Billion Parameters
```

Traditional fine-tuning:

```text id="d7p4m1"
1B parameters
     ↓
Train almost everything
```

PEFT:

```text id="h9q3v6"
1B parameter model
       │
       ├── Frozen
       │
       └── Small trainable adapter
                    ↓
                  Train
```

---

# 5. LoRA কী?

**LoRA = Low-Rank Adaptation**

এটা PEFT-এর একটি জনপ্রিয় technique।

মূল idea:

```text id="a8k5z2"
Pretrained Weight
      ↓
Frozen
```

এর সাথে ছোট trainable matrices যোগ করা হয়।

Conceptually:

```text id="r4m7c1"
Original Weight W
       +
LoRA Update ΔW
       ↓
Adapted Weight
```

Mathematically:

```text id="b6n2x9"
W' = W + ΔW
```

LoRA-তে:

```text id="v3p8q5"
ΔW = B × A
```

যেখানে `A` এবং `B` ছোট matrices।

---

# 6. Rank কী?

LoRA-তে একটি গুরুত্বপূর্ণ parameter:

```text id="k7s2m4"
rank = r
```

যেমন:

```text
r = 4
r = 8
r = 16
r = 32
```

ছোট rank:

```text id="w9d3f6"
কম trainable parameters
কম memory
কম capacity
```

বড় rank:

```text id="t2q8h5"
বেশি capacity
বেশি memory
বেশি training
```

শুরুতে:

```text
r = 8 অথবা 16
```

ভালো starting point হতে পারে।

---

# 7. LoRA Conceptual Architecture

```text id="e5m8r2"
                 PRETRAINED MODEL
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
          Frozen W          LoRA A + B
              │                 │
              │                 ▼
              │              ΔW
              │                 │
              └────────┬────────┘
                       ▼
                    W + ΔW
                       │
                       ▼
                Adapted Output
```

---

# 8. কেন LoRA তোমার Project-এর জন্য Useful?

তোমার educational AI-তে বিভিন্ন model থাকবে:

```text id="f7k3n1"
LLM
VLM
Image Model
Video Model
```

প্রতিটা model-কে পুরোপুরি retrain করার দরকার নেই।

LoRA দিয়ে:

```text id="x6m4p9"
Base Model
   ↓
Educational Adaptation
```

করতে পারবে।

---

# 9. কিন্তু একটা গুরুত্বপূর্ণ বিষয় ⚠️

**সব model-এ LoRA একইভাবে ব্যবহার করা হয় না।**

উদাহরণ:

```text id="j8q2w5"
LLM
→ LoRA খুব common

VLM
→ LoRA/PEFT possible

Diffusion Image Model
→ LoRA খুব common

Video Diffusion Model
→ LoRA possible but much more expensive/complex
```

তাই M23-এ আমরা প্রথমে **LLM LoRA** দিয়ে concept বুঝব।

তারপর image/video model-এর দিকে যাব।

---

# 10. M23 Learning Architecture

```text id="r5v9k2"
Educational Dataset
        ↓
Data Cleaning
        ↓
Instruction Dataset
        ↓
Tokenizer
        ↓
Pretrained LLM
        ↓
LoRA Adapter
        ↓
Training
        ↓
Validation
        ↓
Evaluation
        ↓
Saved Adapter
```

---

# 11. Dataset for LLM LoRA

আমাদের M17 dataset থেকে আমরা এমন data তৈরি করতে পারি:

```json id="h2x7m4"
{
  "instruction": "Explain binary search to a beginner.",
  "input": {
    "duration": 30,
    "style": "clean_2d"
  },
  "output": {
    "topic": "Binary Search",
    "learning_objectives": [
      "Understand binary search",
      "Understand the middle element"
    ],
    "scenes": [
      {
        "scene_id": 1,
        "narration": "Binary search works on sorted data.",
        "scene_type": "definition"
      }
    ]
  }
}
```

এখানে:

```text id="p9c3v6"
Input
 ↓
Expected Output
```

থাকছে।

---

# 12. Instruction Fine-tuning

আমাদের model-কে শেখানো হবে:

```text id="q4m8s1"
User:
Explain photosynthesis to a beginner.

Model:
[structured educational plan]
```

আরেকটা:

```text id="y6n2k7"
User:
Explain gravity to a 10-year-old.

Model:
[structured educational plan]
```

এভাবে অনেক example।

---

# 13. Training Dataset Format

Simple format:

```json id="w8r3p5"
{
  "instruction": "Explain photosynthesis.",
  "input": "Beginner, 30 seconds.",
  "output": "..."
}
```

Chat format:

```json id="m4q7z2"
{
  "messages": [
    {
      "role": "user",
      "content": "Explain binary search."
    },
    {
      "role": "assistant",
      "content": "{...structured JSON...}"
    }
  ]
}
```

কোন format ব্যবহার করবে সেটা training framework/model-এর উপর নির্ভর করবে।

---

# 14. Fine-tuning-এর আগে Dataset Quality

এখানে একটি golden rule:

> **Bad dataset + fine-tuning = bad specialized model.**

তাই:

```text id="n7x4c2"
Raw Dataset
 ↓
Cleaning
 ↓
Validation
 ↓
Human Review
 ↓
Training Dataset
```

---

# 15. Dataset Quality Checklist

প্রতিটি sample-এর:

```text id="v3k8m1"
✓ Accurate
✓ Clear
✓ No contradictions
✓ Correct JSON
✓ Correct timing
✓ Correct educational level
✓ Correct subject
✓ No unnecessary text
```

থাকা উচিত।

---

# 16. Training / Validation / Test

M17-এর মতো:

```text id="j5p2q9"
Dataset
   │
   ├── Train 80%
   ├── Validation 10%
   └── Test 10%
```

কিন্তু গুরুত্বপূর্ণ:

> একই topic-এর প্রায় identical samples তিন জায়গায় ছড়িয়ে দিও না।

নাহলে model memorization-এর কারণে test score artificially high হতে পারে।

---

# 17. Installation

LLM LoRA শেখার জন্য common stack:

```bash id="x8m4r2"
pip install torch
pip install transformers
pip install datasets
pip install peft
pip install accelerate
pip install bitsandbytes
```

এখানে:

```text
torch        → training
transformers → model
datasets     → dataset
peft         → LoRA
accelerate   → training/device management
bitsandbytes → quantization
```

Model compatibility অনুযায়ী package versions adjust করতে হতে পারে।

---

# 18. PEFT Import

```python id="q5v8n2"
from peft import LoraConfig, get_peft_model
```

LoRA configuration:

```python id="r7m3k9"
lora_config = LoraConfig(
    r=8,
    lora_alpha=16,
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM"
)
```

---

# 19. Configuration বুঝি

### `r`

```text id="f3x9m5"
Rank
```

যেমন:

```python id="0v7k2q"
r=8
```

### `lora_alpha`

Scaling factor।

```python id="n4c8p1"
lora_alpha=16
```

### `lora_dropout`

Overfitting কমাতে সাহায্য করতে পারে।

```python id="m6q2z8"
lora_dropout=0.05
```

### `bias`

সাধারণভাবে:

```python id="w5r8x3"
bias="none"
```

### `task_type`

Causal language model-এর জন্য:

```python id="k9p4v7"
task_type="CAUSAL_LM"
```

---

# 20. Model Load

Conceptually:

```python id="t2m8q5"
from transformers import AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained(
    MODEL_NAME
)
```

তারপর:

```python id="y7x3n9"
model = get_peft_model(
    model,
    lora_config
)
```

এখন model LoRA adapter ব্যবহার করবে।

---

# 21. Trainable Parameters

সবচেয়ে interesting অংশ:

```python id="c8m5r2"
model.print_trainable_parameters()
```

তুমি দেখতে পারবে:

```text
trainable params:
...
all params:
...
trainable%:
...
```

Expected idea:

```text id="v4q9k1"
Trainable
↓
small percentage

Frozen
↓
large percentage
```

এটাই PEFT-এর advantage।

---

# 22. Quantization + LoRA

আরও advanced technique:

```text id="z6n3p8"
QLoRA
```

Conceptually:

```text id="h4r7m2"
Large Model
   ↓
4-bit Quantization
   ↓
LoRA
   ↓
Fine-tuning
```

এতে memory requirement অনেক কমানো যায়।

---

# 23. QLoRA

QLoRA-এর মূল idea:

```text id="k3p9x6"
Quantized Base Model
        +
LoRA Adapter
        ↓
Training
```

তোমার মতো limited GPU environment-এর জন্য এটা খুব useful concept।

তবে exact VRAM requirement model size, sequence length, batch size, quantization implementation ইত্যাদির ওপর নির্ভর করে।

---

# 24. LoRA বনাম QLoRA

| Feature                | LoRA          | QLoRA                 |
| ---------------------- | ------------- | --------------------- |
| Base model             | Normal/frozen | Quantized/frozen      |
| Adapter                | Yes           | Yes                   |
| Memory                 | Lower         | Usually even lower    |
| Training               | Efficient     | More memory efficient |
| Complexity             | Moderate      | Higher                |
| Large model adaptation | Good          | Very useful           |

---

# 25. Educational AI-তে কী Fine-tune করব?

এখানে খুব গুরুত্বপূর্ণ decision।

তোমার project-এ:

### LLM

Fine-tune করা যেতে পারে:

```text id="r8m3v5"
Educational explanation style
Scene planning
Structured JSON
Difficulty adaptation
Teaching strategy
```

### VLM

Fine-tune করা যেতে পারে:

```text id="x2q7n4"
Educational scene understanding
Diagram understanding
Visual teaching point extraction
```

### Image Model

Fine-tune করা যেতে পারে:

```text id="m9k5p1"
Educational illustration style
Scientific diagram style
Consistent visual style
```

### Video Model

পরে:

```text id="z4v8c6"
Educational motion style
Specific visual style
Domain-specific generation
```

---

# 26. কী Fine-tune করা উচিত নয়?

প্রথম থেকেই:

```text id="p6x2n9"
❌ Everything
❌ Huge video model
❌ All subjects
❌ All styles
❌ All languages
```

একসাথে করতে যেও না।

---

# 27. Best First Fine-tuning Project

আমি তোমার project-এর জন্য প্রথম fine-tuning target রাখব:

> **Educational Scene Planner LLM**

Input:

```text id="q3m7k8"
Explain binary search to a beginner
in 30 seconds.
```

Output:

```json id="h8v2c5"
{
  "topic": "Binary Search",
  "difficulty": "beginner",
  "learning_objectives": [...],
  "scenes": [...]
}
```

এটা তোমার existing M18/M19 pipeline-এর সাথে সরাসরি connect করবে।

---

# 28. Base Model → Educational Planner

Architecture:

```text id="j4p8x2"
Pretrained LLM
      ↓
LoRA
      ↓
Educational Planner
      ↓
Scene JSON
```

এতে M19-এর prompt engineering এবং M23-এর fine-tuning দুটো একসাথে ব্যবহার হবে।

---

# 29. Prompt Engineering vs Fine-tuning

খুব গুরুত্বপূর্ণ পার্থক্য।

### Prompt Engineering

```text id="m2x7k9"
Model
 +
Prompt
 ↓
Desired Output
```

Model-এর parameters change হয় না।

### Fine-tuning

```text id="c5r8v1"
Model
 +
Training Dataset
 ↓
Updated Adapter
 ↓
Specialized Behavior
```

Model behavior adapt হয়।

---

# 30. কখন Prompt ব্যবহার করবে?

যদি শুধু:

```text id="y9q3m6"
"Explain this at beginner level"
```

বললেই model ভালো output দেয়:

→ Prompt যথেষ্ট।

---

# 31. কখন Fine-tuning করবে?

যদি repeatedly চাই:

```text id="k7v4p2"
Always output this exact schema.

Always use educational scene structure.

Always follow our teaching strategy.

Always produce this style of visual instruction.
```

এবং prompting দিয়েও consistent result না পাওয়া যায়:

→ Fine-tuning useful হতে পারে।

---

# 32. Fine-tuning Pipeline

```text id="b8m5x1"
Educational Dataset
       ↓
Clean
       ↓
Validate
       ↓
Format
       ↓
Tokenizer
       ↓
Base Model
       ↓
LoRA
       ↓
Training
       ↓
Validation
       ↓
Evaluation
       ↓
Adapter
```

---

# 33. Training Configuration

Typical training concepts:

```python id="v6q2m9"
TrainingArguments(
    output_dir="outputs/educational_lora",

    num_train_epochs=3,

    per_device_train_batch_size=1,

    gradient_accumulation_steps=8,

    learning_rate=2e-4,

    logging_steps=10,

    save_steps=100,

    evaluation_strategy="steps"
)
```

**Note:** Transformer/TRL version অনুযায়ী কিছু argument-এর নাম বা API পরিবর্তিত হতে পারে। Code copy করার আগে installed version-এর documentation/API verify করা উচিত।

---

# 34. Batch Size কম হলে?

GPU memory কম হলে:

```text id="q2n7k4"
batch_size = 1
```

করা যায়।

কিন্তু effective batch size বাড়ানোর জন্য:

```python id="r5x8m3"
gradient_accumulation_steps=8
```

ব্যবহার করা যায়।

Conceptually:

```text id="t9v4p1"
1 sample
1 sample
1 sample
...
        ↓
accumulate gradients
        ↓
update model
```

---

# 35. Learning Rate

LoRA fine-tuning-এ full-model training-এর তুলনায় learning rate আলাদা হতে পারে।

Example:

```text id="z3m6q8"
2e-4
1e-4
5e-5
```

কিন্তু exact value dataset/model-এর ওপর experiment করতে হবে।

একটি fixed value blindly ব্যবহার করা উচিত নয়।

---

# 36. Epoch কী?

একবার পুরো training dataset model-এর মাধ্যমে pass করা:

```text id="f8r2k5"
1 Epoch
```

যেমন:

```text
1000 samples
 ↓
model sees all 1000
 ↓
1 epoch
```

৩ epoch:

```text id="p7x4m9"
Dataset
 ↓
Epoch 1
 ↓
Epoch 2
 ↓
Epoch 3
```

---

# 37. Overfitting

ধরো training dataset:

```text id="n4v8c2"
1000 examples
```

Model training data খুব ভালোভাবে memorize করল।

Training loss:

```text
↓ ↓ ↓
```

কিন্তু validation:

```text
↑
```

তাহলে:

> Overfitting হতে পারে।

---

# 38. Overfitting Control

ব্যবহার করতে পারো:

```text id="q6m2x9"
✓ Validation set
✓ LoRA dropout
✓ Early stopping
✓ Lower epochs
✓ Better dataset
✓ More diverse examples
```

---

# 39. Dataset Diversity ⭐

Educational AI-এর dataset-এ শুধু:

```text
Binary Search
Binary Search
Binary Search
```

দেওয়া উচিত না।

বরং:

```text id="w8p3r6"
Computer Science
 ├── Binary Search
 ├── Sorting
 ├── Stack
 ├── Queue
 └── Graph

Biology
 ├── Photosynthesis
 ├── Cell
 ├── DNA
 └── Respiration

Physics
 ├── Gravity
 ├── Force
 ├── Energy
 └── Motion

Mathematics
 ├── Algebra
 ├── Geometry
 ├── Probability
 └── Calculus
```

---

# 40. Difficulty Diversity

প্রতিটি topic:

```text id="y5n9k2"
Beginner
Intermediate
Advanced
```

version-এ থাকা উচিত।

Example:

```text
Binary Search
```

Beginner:

```text
Simple explanation
```

Intermediate:

```text
Algorithm + complexity
```

Advanced:

```text
Proof + edge cases + implementation
```

---

# 41. Language Diversity

যদি তোমার product future-এ multilingual হয়:

```text id="r3x7m8"
English
Bangla
Hindi
Arabic
...
```

তাহলে dataset-এ language metadata রাখো।

তবে প্রথম model-এর scope ছোট রাখাই ভালো।

---

# 42. LoRA Adapter Save

Training শেষে:

```text id="c9q2v6"
Base Model
+
educational_adapter
```

দুটি আলাদা থাকবে।

Structure:

```text id="h7m4p1"
models/
├── base/
│
└── adapters/
    └── educational_planner/
        ├── adapter_config.json
        └── adapter_model.safetensors
```

Adapter সাধারণত base model-এর তুলনায় অনেক ছোট।

---

# 43. Inference

Training-এর পরে:

```text id="x5r8n3"
User Prompt
 ↓
Base Model
 +
Educational LoRA
 ↓
Educational Output
```

অর্থাৎ deployment-এর সময় adapter load করা হবে।

---

# 44. Multiple Adapters

একই base model-এর জন্য:

```text id="m8q3v5"
Base Model
   │
   ├── Educational Adapter
   ├── Coding Adapter
   ├── Medical Adapter
   └── Story Adapter
```

এটা powerful architecture।

তোমার system-এ:

```text id="p2x7k4"
Base LLM
   ↓
Educational Adapter
```

ব্যবহার করা যেতে পারে।

---

# 45. Subject-specific Adapter

Advanced:

```text id="q6v9m2"
Base Model
    │
    ├── CS Adapter
    ├── Biology Adapter
    ├── Math Adapter
    └── Physics Adapter
```

কিন্তু এটা পরে।

প্রথমে:

```text
one base model
+
one educational adapter
```

করো।

---

# 46. LoRA for Image Generation

M21-এর image model-এর ক্ষেত্রে LoRA আরও interesting।

ধরো তুমি চাই:

```text id="v8n3q5"
Every image should look like
a clean educational scientific illustration.
```

Dataset:

```text id="f4m7x2"
Image 1 → educational style
Image 2 → educational style
Image 3 → educational style
...
```

তারপর:

```text id="k9p5r1"
Base Image Model
      ↓
Educational LoRA
      ↓
Educational Image Model
```

---

# 47. Image LoRA

Conceptually:

```text id="y3x8m6"
Base Diffusion Model
        ↓
LoRA Adapter
        ↓
Style Adaptation
```

Prompt:

```text
Photosynthesis
```

Output:

```text
Educational scientific illustration
```

এটাই M24-এর বড় লক্ষ্য হবে।

---

# 48. Video LoRA

M22-এর video model-এর ক্ষেত্রেও:

```text id="p4m8q2"
Base Video Model
       ↓
Educational Motion LoRA
       ↓
Educational Video
```

Possible target:

```text id="z7x3n5"
clean motion
consistent objects
scientific visualization
educational composition
```

কিন্তু video LoRA significantly more computationally demanding হতে পারে।

---

# 49. খুব গুরুত্বপূর্ণ — Dataset বনাম Fine-tuning

তোমার project-এর সবচেয়ে বড় asset হবে:

> **Educational Dataset**

Model নয়।

কারণ future-এ model change হতে পারে:

```text id="r2v7k4"
Model A
 ↓
Model B
 ↓
Model C
```

কিন্তু তোমার dataset:

```text id="m5x8q3"
Educational Dataset
```

থেকে যাবে।

তাই:

```text id="q8n3p6"
DATASET > MODEL
```

এই principle মনে রাখো।

---

# 50. M23 Mini Project

এখন একটা ছোট project:

### Goal

একটি tiny educational instruction dataset তৈরি করো।

```text id="k4p9x2"
dataset/
├── train.jsonl
├── validation.jsonl
└── test.jsonl
```

Train sample:

```json id="w7m3q8"
{
  "instruction": "Explain binary search to a beginner.",
  "input": {
    "duration": 30
  },
  "output": {
    "topic": "Binary Search",
    "difficulty": "beginner",
    "learning_objectives": [
      "Understand sorted data",
      "Understand the middle element"
    ]
  }
}
```

আরেকটি:

```json id="z2n6v5"
{
  "instruction": "Explain photosynthesis to a beginner.",
  "input": {
    "duration": 30
  },
  "output": {
    "topic": "Photosynthesis",
    "difficulty": "beginner",
    "learning_objectives": [
      "Understand sunlight",
      "Understand plant food production"
    ]
  }
}
```

---

# 51. Mini Project Architecture

```text id="p8r4m2"
JSONL Dataset
      ↓
Hugging Face Dataset
      ↓
Tokenizer
      ↓
Pretrained LLM
      ↓
LoRA
      ↓
Trainer
      ↓
Adapter
      ↓
Inference
      ↓
Scene JSON
```

---

# 52. M23-এর Production Architecture

শেষ পর্যন্ত তোমার AI system:

```text id="c7m2x9"
                       USER
                        │
                        ▼
                    Django API
                        │
                        ▼
                 Educational LLM
                        │
               ┌────────┴────────┐
               │                 │
               ▼                 ▼
          Base Model       LoRA Adapter
               │                 │
               └────────┬────────┘
                        ▼
                  Scene JSON
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
        Manim         Image         Video
                        │             │
                   Image LoRA     Video LoRA
                        │             │
                        └──────┬──────┘
                               ▼
                              VLM
                               │
                               ▼
                            Quality
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
                      EDUCATIONAL VIDEO
```

---

# 53. M23-এ এখনই কী train করবে?

আমি তোমাকে এই order-এ যেতে বলব:

### Stage 1 — Tiny experiment

```text
100–500 samples
```

Goal:

> বুঝতে হবে LoRA training আসলে কীভাবে কাজ করে।

### Stage 2 — Educational Planner

```text
1k–10k high-quality samples
```

Goal:

> LLM → reliable educational scene JSON

### Stage 3 — Image Style

```text
Educational images
+
captions/prompts
```

Goal:

> consistent educational visual style

### Stage 4 — Video Style

আরও বড় dataset + বেশি GPU:

```text
Educational video clips
+
motion descriptions
```

Goal:

> educational motion generation

---

# 54. এখনই বড় model train করা উচিত?

**না।**

প্রথমে:

```text id="f5q8n3"
Tiny Model
+
Tiny Dataset
+
LoRA
+
Successful Training
```

এই loop বুঝে নাও।

তারপর scale করো।

---

# 55. M23-এর সবচেয়ে গুরুত্বপূর্ণ Formula

```text id="r9x4m7"
Pretrained Knowledge
        +
Your Educational Data
        +
LoRA
        ↓
Specialized Behavior
```

আর পুরো project-এর ক্ষেত্রে:

```text id="m3q8v2"
LLM
 = Educational Brain

VLM
 = Visual Evaluator

Image LoRA
 = Educational Visual Style

Video LoRA
 = Educational Motion Style

Manim
 = Exact Graphics

TTS
 = Voice

FFmpeg
 = Assembly
```

---

# 56. M23 Completion Checklist

### PEFT

* [ ] PEFT কী
* [ ] কেন PEFT
* [ ] LoRA কী
* [ ] Low-rank adaptation
* [ ] Rank
* [ ] Alpha
* [ ] Dropout
* [ ] Frozen parameters
* [ ] Trainable parameters

### Training

* [ ] Instruction dataset
* [ ] Chat dataset
* [ ] Tokenization
* [ ] Training
* [ ] Validation
* [ ] Test
* [ ] Learning rate
* [ ] Epoch
* [ ] Batch size
* [ ] Gradient accumulation
* [ ] Overfitting

### Efficient Training

* [ ] Quantization
* [ ] QLoRA
* [ ] Memory optimization
* [ ] GPU utilization

### Educational AI

* [ ] Educational LLM adapter
* [ ] Educational VLM adapter
* [ ] Image LoRA
* [ ] Video LoRA
* [ ] Subject diversity
* [ ] Difficulty diversity
* [ ] Dataset quality

---

# 🧠 M23-এর Golden Rule

> **Don't teach a pretrained model everything again. Teach it your specific behavior.**

তোমার ক্ষেত্রে:

```text
Generic LLM
     ↓
"Explain things"
```

এর পরিবর্তে:

```text
Educational LoRA
     ↓
"Understand learner
 → create objectives
 → create script
 → create scenes
 → create visual instructions
 → return valid Scene JSON"
```

এই adaptation-টাই M23-এর মূল উদ্দেশ্য।

---

## M21 → M22 → M23

এখন পুরো generative evolution:

```text id="q4n8m2"
M21
Text/Scene
   ↓
Image Generation
   ↓
Educational Image


M22
Text/Image/Scene
   ↓
Video Generation
   ↓
Educational Video Clip


M23
Educational Dataset
   ↓
LoRA / PEFT
   ↓
Adapted Model
   ↓
Better Educational Generation
```

### পরবর্তী M24 — Educational Style Fine-tuning 🎨

M23-এ আমরা **LoRA কী এবং কীভাবে fine-tuning architecture কাজ করে** শিখলাম।

M24-এ practicalভাবে focus হবে:

```text
Educational Image Dataset
        ↓
Caption / Prompt Dataset
        ↓
Base Diffusion Model
        ↓
Image LoRA Training
        ↓
Educational Style Adapter
        ↓
"Photosynthesis"
        ↓
Consistent Educational Illustration
```

এবং এরপর একই concept **video-generation model-এর educational style adaptation**-এর দিকে নেওয়া হবে।


----
# M24 — Educational Style Fine-tuning 🎨

এখন আমরা **M23-এর LoRA/PEFT knowledge-কে practical image-generation fine-tuning-এ apply করব**।

আমাদের লক্ষ্য:

```text
Educational Image Dataset
        ↓
Image + Caption/Prompt Dataset
        ↓
Pretrained Diffusion Model
        ↓
LoRA Training
        ↓
Educational Style LoRA
        ↓
Text Prompt
        ↓
Consistent Educational Illustration
```

উদাহরণ:

**Input**

> Explain photosynthesis with a clean educational illustration.

**Output concept**

```text
        ☀️
        ↓ sunlight
     🌱 Plant
        ↓
   O₂ + Glucose
```

অর্থাৎ model শুধু "pretty image" বানাবে না—আমরা তাকে **একটি নির্দিষ্ট educational visual style** শেখাতে চাই।

---

# 1. M24-এ আমরা কী শিখব?

এই milestone-এ 10টি গুরুত্বপূর্ণ বিষয়:

1. Image Diffusion Model কী
2. Image LoRA কীভাবে কাজ করে
3. Educational image dataset তৈরি
4. Caption / prompt dataset
5. Image preprocessing
6. LoRA training architecture
7. Training configuration
8. Dataset → LoRA pipeline
9. Trained adapter ব্যবহার
10. Educational Video Generator-এর সাথে integration

---

# 2. কেন Image LoRA দরকার?

ধরো তুমি একটি pretrained image model ব্যবহার করছ।

প্রতিবার prompt দিলে style পরিবর্তন হতে পারে:

```text
Prompt
 ↓
Model
 ↓
Image A → realistic
Image B → cartoon
Image C → 3D
Image D → watercolor
```

আমরা চাই:

```text
Prompt
 ↓
Base Model
 +
Educational LoRA
 ↓
Consistent Educational Style
```

যেমন:

```text
Photosynthesis
Binary Search
Newton's Law
Human Heart
Solar System
DNA
```

সব image-এর visual language একই থাকবে।

---

# 3. Base Model বনাম LoRA

এটা M23-এর সবচেয়ে গুরুত্বপূর্ণ concept।

ধরো:

```text
Base Diffusion Model
        |
        | frozen
        ↓
   Original Model
```

আমরা পুরো model retrain করব না।

বরং:

```text
Base Model
    +
Small LoRA Adapter
    ↓
Educational Model
```

Base model:

```text
W
```

LoRA:

```text
ΔW = B × A
```

Final:

```text
W' = W + ΔW
```

এখানে মূল model-এর বেশিরভাগ parameter unchanged থাকে।

---

# 4. Educational Style বলতে কী বুঝি?

শুধু cartoon style নয়।

আমাদের style হতে পারে:

```text
Clean
Simple
Educational
Clear
Minimal
Labeled
Scientifically appropriate
Consistent
```

উদাহরণ:

### Biology

```text
Human Heart
 ↓
clean diagram
 ↓
labels
 ↓
simple background
 ↓
clear structures
```

### Computer Science

```text
Binary Search
 ↓
array
 ↓
highlighted middle
 ↓
arrows
 ↓
minimal background
```

### Mathematics

```text
Pythagorean theorem
 ↓
triangle
 ↓
a² + b² = c²
 ↓
clear labels
```

---

# 5. Dataset সবচেয়ে গুরুত্বপূর্ণ

M24-এর success অনেকটাই dataset-এর উপর নির্ভর করবে।

আমরা চাই:

```text
Image
+
Caption
+
Topic
+
Subject
+
Style
```

উদাহরণ:

```text
images/
├── biology_001.png
├── biology_002.png
├── biology_003.png
├── math_001.png
└── cs_001.png
```

তার সাথে:

```text
metadata.jsonl
```

---

# 6. Dataset Format

একটি sample:

```json
{
  "image": "biology_001.png",
  "caption": "clean educational illustration of photosynthesis showing a green plant receiving sunlight and absorbing carbon dioxide"
}
```

আরেকটি:

```json
{
  "image": "cs_001.png",
  "caption": "clean educational diagram showing binary search on a sorted array with the middle element highlighted"
}
```

আরেকটি:

```json
{
  "image": "math_001.png",
  "caption": "clean educational illustration of a right triangle with clearly labeled sides and the equation a squared plus b squared equals c squared"
}
```

---

# 7. Dataset Structure

আমি recommend করব:

```text
educational_style_dataset/
│
├── images/
│   ├── biology/
│   │   ├── image_001.png
│   │   ├── image_002.png
│   │   └── image_003.png
│   │
│   ├── mathematics/
│   │   ├── image_001.png
│   │   └── image_002.png
│   │
│   └── computer_science/
│       ├── image_001.png
│       └── image_002.png
│
├── metadata.jsonl
│
├── train.jsonl
├── validation.jsonl
└── test.jsonl
```

---

# 8. কতগুলো Image দরকার?

প্রথম experiment-এর জন্য huge dataset দরকার নেই।

### Experiment 1

```text
100–300 images
```

শুধু pipeline test করার জন্য।

### Experiment 2

```text
500–1,000 images
```

ভালো initial style adaptation।

### Experiment 3

```text
2,000–10,000+
```

আরও robust educational style-এর জন্য।

কিন্তু:

> **1,000 high-quality images > 10,000 poor-quality images**

---

# 9. Dataset Diversity

একই ধরনের image দিয়ে dataset বানানো যাবে না।

ধরো সব image:

```text
plant
plant
plant
plant
plant
```

তাহলে model-এর শেখা style খুব narrow হবে।

বরং:

```text
Biology
 ├── plants
 ├── cells
 ├── human body
 └── ecosystem

Physics
 ├── force
 ├── motion
 ├── electricity
 └── waves

Math
 ├── geometry
 ├── algebra
 ├── graph
 └── probability

Computer Science
 ├── arrays
 ├── trees
 ├── graphs
 └── algorithms
```

---

# 10. Dataset Quality Rules

Training image-এর ক্ষেত্রে:

### Good

```text
✓ clear
✓ high resolution
✓ educational
✓ simple composition
✓ understandable
✓ consistent style
✓ correct concept
```

### Bad

```text
✗ blurry
✗ random objects
✗ incorrect anatomy
✗ incorrect equations
✗ unreadable text
✗ watermark
✗ duplicate images
✗ irrelevant images
```

বিশেষ করে educational AI-এর জন্য:

**Factual correctness > visual beauty**

---

# 11. Copyright খুব গুরুত্বপূর্ণ

Dataset তৈরির সময় arbitrary internet image বা YouTube screenshot নিয়ে training করা উচিত নয়।

Prefer:

```text
Original images
+
Public-domain images
+
Compatible open-license datasets
+
Properly licensed content
```

এবং dataset-এর সাথে provenance রাখবে:

```json
{
  "source_type": "original",
  "license": "original"
}
```

অথবা:

```json
{
  "source_type": "public_domain",
  "license": "CC BY",
  "attribution_required": true
}
```

---

# 12. Caption কেন এত গুরুত্বপূর্ণ?

LoRA শুধু image দেখে style শেখে না—caption/prompt relationship-ও গুরুত্বপূর্ণ।

ধরো image:

```text
Binary Search
```

Caption:

```text
educational diagram of binary search
```

তাহলে model শিখবে:

```text
"binary search"
        ↓
এই ধরনের visual
```

আর যদি caption হয়:

```text
beautiful image
```

তাহলে educational relationship দুর্বল হবে।

---

# 13. Caption Template

আমরা একটি consistent template ব্যবহার করতে পারি:

```text
[style] + [subject] + [concept] + [objects] + [composition]
```

উদাহরণ:

```text
clean educational illustration of photosynthesis,
showing a green plant, sunlight and carbon dioxide,
with a simple labeled composition
```

Binary search:

```text
clean educational diagram of binary search,
showing a sorted array with the middle element highlighted,
simple technical composition
```

---

# 14. Dataset তৈরির Python Code

প্রথমে directory তৈরি:

```python
from pathlib import Path

BASE_DIR = Path("educational_style_dataset")

(BASE_DIR / "images").mkdir(parents=True, exist_ok=True)

print("Dataset directory created.")
```

---

# 15. JSONL তৈরি

```python
import json

records = [
    {
        "image": "images/biology_001.png",
        "caption": (
            "clean educational illustration of photosynthesis "
            "showing a green plant receiving sunlight"
        )
    },
    {
        "image": "images/cs_001.png",
        "caption": (
            "clean educational diagram of binary search "
            "showing a sorted array with the middle element highlighted"
        )
    }
]

with open(
    "educational_style_dataset/metadata.jsonl",
    "w",
    encoding="utf-8"
) as f:

    for record in records:
        f.write(
            json.dumps(
                record,
                ensure_ascii=False
            ) + "\n"
        )
```

---

# 16. Dataset Load করা

Hugging Face `datasets` ব্যবহার করতে পারো।

```bash
pip install datasets pillow
```

তারপর:

```python
from datasets import load_dataset

dataset = load_dataset(
    "json",
    data_files="educational_style_dataset/metadata.jsonl"
)

print(dataset)
```

Expected:

```text
DatasetDict({
    train: Dataset(...)
})
```

---

# 17. Dataset Split

```python
dataset = dataset["train"]

split = dataset.train_test_split(
    test_size=0.1,
    seed=42
)

train_dataset = split["train"]
test_dataset = split["test"]
```

এখন:

```text
90% → training
10% → testing
```

Large dataset হলে আলাদা validation set-ও রাখবে।

---

# 18. Image Preprocessing

Training-এর আগে:

```text
Image
 ↓
Resize
 ↓
Normalize
 ↓
Tensor
 ↓
Model
```

Conceptually:

```python
from PIL import Image

image = Image.open(
    "educational_style_dataset/images/biology_001.png"
)

print(image.size)
```

---

# 19. Diffusion Model কীভাবে কাজ করে?

খুব simplified version:

```text
Text Prompt
     ↓
Text Encoder
     ↓
Conditioning
     ↓
Diffusion Model
     ↓
Noise → Image
```

Training-এর সময়:

```text
Real Image
   ↓
Add Noise
   ↓
Noisy Image
   ↓
Model predicts noise
   ↓
Learn
```

Inference:

```text
Random Noise
     ↓
Denoising
     ↓
Image
```

---

# 20. Image LoRA Training Architecture

পুরো architecture:

```text
              Text Prompt
                   ↓
              Text Encoder
                   ↓
            Conditioning
                   ↓
              U-Net / Model
              ↙          ↘
        Base Weights     LoRA
             │             │
             └──────┬──────┘
                    ↓
               Prediction
                    ↓
                  Loss
                    ↓
             Update LoRA only
```

Base weights:

```text
FROZEN
```

LoRA:

```text
TRAINABLE
```

---

# 21. Training Pipeline

আমাদের final pipeline:

```text
Educational Images
       ↓
Captions
       ↓
Dataset Cleaning
       ↓
Train / Validation / Test
       ↓
Pretrained Diffusion Model
       ↓
Add LoRA
       ↓
Training
       ↓
Save Adapter
       ↓
Generate Test Images
       ↓
Evaluate
```

---

# 22. গুরুত্বপূর্ণ বিষয় — Model Choice

Image LoRA-এর জন্য বিভিন্ন diffusion architecture আছে।

Conceptually:

```text
Stable Diffusion family
SDXL family
Flux-family models
Other diffusion architectures
```

কিন্তু **সব model-এর LoRA training code একই নয়**।

এখানে আমাদের architecture শেখা সবচেয়ে গুরুত্বপূর্ণ:

```text
Dataset
 ↓
Base model
 ↓
LoRA adapter
 ↓
Training
 ↓
Adapter
```

তারপর hardware অনুযায়ী specific implementation নির্বাচন করব।

---

# 23. তোমার PC-এর জন্য গুরুত্বপূর্ণ

তোমার বর্তমান machine-এ যদি NVIDIA CUDA GPU না থাকে, তাহলে image LoRA training practicalভাবে খুব slow বা difficult হতে পারে।

CPU দিয়ে:

```text
Training
   ↓
Possible
```

কিন্তু:

```text
Speed
 ↓
Very slow
```

তাই serious diffusion LoRA training-এর জন্য NVIDIA CUDA GPU বা cloud GPU বেশি practical।

---

# 24. GPU Memory কেন গুরুত্বপূর্ণ?

ধরো:

```text
Base Model
+
Optimizer
+
Gradients
+
Activations
+
LoRA
```

সব GPU memory ব্যবহার করে।

তাই:

```text
VRAM ↑
    ↓
larger model / batch / resolution
```

কিন্তু LoRA-এর সুবিধা:

```text
Full Fine-tuning
→ huge trainable parameters

LoRA
→ small trainable parameters
```

---

# 25. Batch Size

ধরো:

```python
batch_size = 1
```

একবারে একটি image।

যদি GPU memory allow করে:

```python
batch_size = 2
```

বা:

```python
batch_size = 4
```

কিন্তু diffusion training-এ VRAM requirement দ্রুত বাড়তে পারে।

---

# 26. Learning Rate

LoRA training-এ learning rate গুরুত্বপূর্ণ।

Conceptually:

```text
Too high
 ↓
unstable / overfit

Too low
 ↓
training too slow

Balanced
 ↓
good adaptation
```

একটি starting point হিসেবে LoRA training-এ প্রায়:

```text
1e-4
```

জাতীয় learning rate দেখা যায়, কিন্তু architecture এবং training framework অনুযায়ী এটা tune করতে হবে।

---

# 27. Epoch

ধরো dataset:

```text
1000 images
```

এক epoch:

```text
1000 images → model sees once
```

3 epochs:

```text
1000
1000
1000
 ↓
3000 image exposures
```

খুব বেশি epoch দিলে:

```text
Overfitting
```

হতে পারে।

---

# 28. Overfitting

ধরো তুমি শুধু:

```text
100 identical plant images
```

দিয়ে train করেছ।

তারপর:

```text
Prompt: Photosynthesis
```

model খুব similar plant image বানাচ্ছে।

এটা হতে পারে:

```text
memorization / overfitting
```

আমরা চাই:

```text
Style learned
```

not:

```text
Specific image memorized
```

---

# 29. Style Token

একটি powerful technique হলো unique trigger/style token ব্যবহার করা।

যেমন:

```text
edu_style
```

Caption:

```text
edu_style, clean educational illustration of photosynthesis...
```

আর inference:

```text
edu_style, explain photosynthesis
```

তাহলে modelকে বলা হচ্ছে:

```text
Use the learned educational style.
```

---

# 30. Dataset Caption Example

```text
edu_style, clean educational illustration of photosynthesis,
green plant receiving sunlight,
simple labeled scientific composition
```

আর:

```text
edu_style, clean educational diagram of binary search,
sorted array, middle element highlighted,
minimal technical composition
```

আর:

```text
edu_style, educational physics diagram,
ball moving under gravity,
simple arrows showing motion
```

---

# 31. কেন Trigger Token useful?

Architecture:

```text
Prompt
   ↓
edu_style
   ↓
LoRA
   ↓
Educational visual style
```

এতে base model-এর normal capability retain করার সুযোগ থাকে।

Without trigger:

```text
photosynthesis
 ↓
generic image
```

With trigger:

```text
edu_style + photosynthesis
 ↓
educational illustration
```

---

# 32. Training Data Generator

একটি helper:

```python
def build_caption(
    subject,
    concept,
    objects
):
    object_text = ", ".join(objects)

    return (
        f"edu_style, clean educational illustration "
        f"of {subject}, explaining {concept}, "
        f"showing {object_text}, "
        f"simple clear composition"
    )
```

Example:

```python
caption = build_caption(
    subject="biology",
    concept="photosynthesis",
    objects=["plant", "sunlight", "carbon dioxide"]
)

print(caption)
```

Output:

```text
edu_style, clean educational illustration of biology,
explaining photosynthesis,
showing plant, sunlight, carbon dioxide,
simple clear composition
```

---

# 33. Educational Style LoRA বনাম Content LoRA

এটা খুব important distinction।

### Style LoRA

শেখাবে:

```text
clean
educational
minimal
diagram-like
consistent
```

### Subject LoRA

শেখাতে পারে:

```text
specific anatomy
specific scientific visual style
specific domain
```

### Character LoRA

শেখাতে পারে:

```text
same character
```

আমাদের M24-এর primary goal:

```text
Educational Style LoRA
```

---

# 34. কিন্তু একটা বড় সমস্যা আছে

Image generation model সাধারণত **exact text ভালোভাবে generate করতে পারে না**।

উদাহরণ:

Prompt:

```text
Binary Search
Array: 10 20 30 40 50
```

Generated image:

```text
10 20 3O 40 5O
```

এখানে:

```text
30 → 3O
```

হতে পারে।

Educational video-তে এটা unacceptable হতে পারে।

তাই আমরা আগের architecture রাখব:

```text
AI Image
+
Manim exact labels
```

---

# 35. Hybrid Educational Visual

আমাদের final architecture হবে:

```text
Scene JSON
      ↓
   Router
  ↙      ↘
Manim   Image LoRA
  ↓         ↓
Exact     Creative
Diagram   Background
  ↘       ↙
    Composite
       ↓
     Video
```

উদাহরণ:

```text
AI-generated background
        +
exact array
        +
exact labels
        +
exact arrows
        ↓
Educational scene
```

---

# 36. M24-এর জন্য Image Router

```python
def choose_image_engine(scene_type):
    exact_types = [
        "algorithm",
        "equation",
        "code",
        "flowchart"
    ]

    generative_types = [
        "real_world",
        "scientific_illustration",
        "historical"
    ]

    if scene_type in exact_types:
        return "manim"

    if scene_type in generative_types:
        return "image_lora"

    return "hybrid"
```

---

# 37. Final Educational Generator Architecture

M24 শেষ হলে:

```text
User Prompt
     ↓
LLM
     ↓
VideoPlan
     ↓
Scene Planner
     ↓
Scene JSON
     ↓
Visual Router
   ↙   ↓    ↘
Manim Image Video
      LoRA Model
        ↓
       VLM
        ↓
Quality Check
        ↓
TTS
        ↓
Subtitle
        ↓
FFmpeg
        ↓
FINAL MP4
```

---

# 38. VLM Quality Control

Generated image তৈরি হওয়ার পর আমরা আবার VLM ব্যবহার করব।

```text
Image
 ↓
VLM
 ↓
Evaluation
```

Evaluation:

```json
{
  "scene_match": 0.94,
  "educational_relevance": 0.91,
  "visual_quality": 0.89,
  "composition_quality": 0.87,
  "issues": []
}
```

---

# 39. Automatic Regeneration

যদি:

```text
score >= 0.80
```

তাহলে:

```text
ACCEPT
```

না হলে:

```text
FAIL
 ↓
Improve Prompt
 ↓
Generate Again
```

Architecture:

```text
Prompt
 ↓
Image LoRA
 ↓
Image
 ↓
VLM
 ↓
Score
 ├── PASS → Accept
 └── FAIL → Regenerate
```

---

# 40. M24 Folder Structure

তোমার project এখন এমন হতে পারে:

```text
educational_video_ai/
│
├── dataset/
│   ├── images/
│   ├── metadata.jsonl
│   ├── train.jsonl
│   ├── validation.jsonl
│   └── test.jsonl
│
├── image/
│   ├── schema.py
│   ├── client.py
│   ├── prompts.py
│   ├── manager.py
│   └── evaluator.py
│
├── image_training/
│   ├── dataset.py
│   ├── preprocess.py
│   ├── train.py
│   ├── config.py
│   └── inference.py
│
├── models/
│   ├── base/
│   └── adapters/
│       └── educational_style/
│
├── renderer/
│
├── planner/
│
├── tts/
│
├── subtitle/
│
├── timeline/
│
└── composer/
```

---

# 41. `config.py`

একটি conceptual training configuration:

```python
MODEL_NAME = "YOUR_BASE_DIFFUSION_MODEL"

OUTPUT_DIR = "models/adapters/educational_style"

IMAGE_SIZE = 512

BATCH_SIZE = 1

NUM_EPOCHS = 3

LEARNING_RATE = 1e-4

LORA_RANK = 16

LORA_ALPHA = 16

LORA_DROPOUT = 0.05

TRIGGER_TOKEN = "edu_style"
```

এগুলো **starting configuration**, universal best values নয়।

---

# 42. Training Pseudocode

আমাদের training logic:

```python
def train():

    dataset = load_training_dataset()

    model = load_pretrained_diffusion_model()

    lora = create_lora_adapter(
        rank=16,
        alpha=16
    )

    model.add_adapter(lora)

    freeze_base_model(model)

    for epoch in range(NUM_EPOCHS):

        for batch in dataset:

            images = batch["images"]
            captions = batch["captions"]

            noise = sample_noise()

            noisy_images = add_noise(
                images,
                noise
            )

            prediction = model(
                noisy_images,
                captions
            )

            loss = calculate_loss(
                prediction,
                noise
            )

            loss.backward()

            optimizer.step()

            optimizer.zero_grad()

    save_lora_adapter(
        model,
        OUTPUT_DIR
    )
```

এটা conceptual code; actual implementation architecture-specific training framework ব্যবহার করবে।

---

# 43. Inference

Training শেষে আমাদের কাছে:

```text
models/
└── adapters/
    └── educational_style/
        ├── adapter_config.json
        └── adapter_model.safetensors
```

Inference:

```text
Base Model
    +
Educational LoRA
    ↓
Prompt
    ↓
Image
```

Prompt:

```text
edu_style,
clean educational illustration of photosynthesis,
showing a green plant receiving sunlight,
simple scientific composition
```

---

# 44. M24-এর সবচেয়ে গুরুত্বপূর্ণ Engineering Principle

আমরা **একটা giant AI model** বানাচ্ছি না।

আমরা বানাচ্ছি:

```text
SYSTEM
```

যার ভিতরে:

```text
LLM
+
VLM
+
Image Model
+
Image LoRA
+
Video Model
+
Video LoRA
+
Manim
+
TTS
+
Whisper
+
FFmpeg
```

প্রত্যেকের আলাদা কাজ।

---

# 45. M24 বনাম M23

| M23                      | M24                       |
| ------------------------ | ------------------------- |
| LoRA concept             | Image LoRA                |
| PEFT                     | Diffusion adaptation      |
| LLM fine-tuning          | Image model fine-tuning   |
| Scene JSON behavior      | Visual style              |
| Text → structured output | Text → educational visual |
| Adapter training         | Image adapter training    |

---

# 46. M24 Mini Project 🎯

এখন তোমার practical project:

## **Educational Style LoRA**

Target:

```text
Input:
"Photosynthesis"

Output:
Consistent educational illustration
```

Dataset:

```text
100–300 images
```

Subjects:

```text
Biology
Mathematics
Physics
Computer Science
```

Training:

```text
Base Diffusion Model
+
LoRA
```

Output:

```text
educational_style/
└── adapter_model.safetensors
```

তারপর:

```text
Prompt
 ↓
Base Model + LoRA
 ↓
Educational Image
```

---

# 47. M24 Practice Tasks

### Task 1

Create:

```text
educational_style_dataset/
```

### Task 2

Collect/create:

```text
100 educational images
```

### Task 3

Create:

```text
metadata.jsonl
```

### Task 4

প্রতিটি image-এর caption তৈরি করো।

### Task 5

Dataset split:

```text
80% train
10% validation
10% test
```

### Task 6

একটি trigger token ব্যবহার করো:

```text
edu_style
```

### Task 7

Base diffusion model load করো।

### Task 8

LoRA adapter configure করো।

### Task 9

Small training run করো।

### Task 10

Test prompts:

```text
edu_style, photosynthesis

edu_style, binary search

edu_style, Newton's second law

edu_style, human heart

edu_style, solar system
```

তারপর compare করো:

```text
Before LoRA
vs
After LoRA
```

---

# 48. M24 Completion Test

M24 complete হয়েছে কিনা check করবে:

* [ ] Diffusion model বুঝি
* [ ] Image generation pipeline বুঝি
* [ ] LoRA বুঝি
* [ ] Dataset format বুঝি
* [ ] Captioning বুঝি
* [ ] Trigger token বুঝি
* [ ] Train/validation/test বুঝি
* [ ] Image preprocessing বুঝি
* [ ] LoRA configuration বুঝি
* [ ] Overfitting বুঝি
* [ ] Image LoRA inference বুঝি
* [ ] VLM evaluation বুঝি
* [ ] Manim + Image LoRA hybrid বুঝি
* [ ] Educational Video Generator-এর সাথে integration বুঝি

---

# 49. এখন আমাদের পুরো project কোথায়?

তুমি এখন এখানে:

```text
M1  ─ Foundation                 ✅
M2  ─ Video Processing           ✅
M3  ─ Dataset Engineering       ✅
M4  ─ Whisper                    ✅
M5  ─ Computer Vision            ✅
M6  ─ Pretrained Vision          ✅
M7  ─ Multimodal Understanding   ✅
M8  ─ Scene Planner              ✅
M9  ─ Script Engine              ✅
M10 ─ Visual Planner             ✅
M11 ─ Animation Engine           ✅
M12 ─ Generic Renderer           ✅
M13 ─ Timeline                   ✅
M14 ─ TTS                        ✅
M15 ─ Subtitle                   ✅
M16 ─ End-to-End Pipeline        ✅
M17 ─ Dataset Pipeline           ✅
M18 ─ LLM Integration            ✅
M19 ─ Prompt Engineering         ✅
M20 ─ VLM                        ✅
M21 ─ Image Generation           ✅
M22 ─ Video Generation           ✅
M23 ─ LoRA / PEFT                ✅
M24 ─ Educational Style LoRA     ← YOU ARE HERE
```

এর পর:

```text
M25 → Evaluation System
M26 → RAG + Trusted Knowledge
M27 → GPU Optimization
M28 → Celery + Redis Distributed Pipeline
M29 → Django + React Production App
M30 → Complete AI Educational Video Generator
```

### সবচেয়ে গুরুত্বপূর্ণ কথা

**M24-এ তোমার লক্ষ্য পুরো diffusion model train করা নয়।**

তোমার লক্ষ্য:

```text
Pretrained Image Model
        +
Educational Style LoRA
        ↓
Consistent Educational Visual Generator
```

আর exact educational information যেমন **equation, code, array, graph, labels** হলে:

```text
Image LoRA → creative visual
Manim      → exact visual
VLM        → verification
```

এই hybrid architecture-টাই তোমার project-কে শুধু একটা image generator না বানিয়ে **একটা practical Educational Video Generation AI system** বানাবে।


----
# M25 — Evaluation System 🎯

M24-এ আমরা **Educational Style LoRA** পর্যন্ত এসেছি। এখন সবচেয়ে গুরুত্বপূর্ণ production concept:

> **AI video তৈরি করেছে — কিন্তু ভিডিওটা সত্যিই ভালো হয়েছে কিনা সেটা কীভাবে automatically বুঝব?**

এটাই M25।

আমাদের লক্ষ্য:

```text
Generated Educational Video
          ↓
      Evaluation
          ↓
 ┌────────┼─────────┐
 ↓        ↓         ↓
Content  Visual    Audio
 ↓        ↓         ↓
Accuracy Quality   Sync
 └────────┼─────────┘
          ↓
      Quality Score
          ↓
    PASS / FAIL
          ↓
   Regenerate if needed
```

---

# 1. M25-এ কী শিখবে?

এই milestone-এ আমরা শিখব:

1. AI Evaluation কী
2. Rule-based evaluation
3. LLM-based evaluation
4. VLM-based evaluation
5. Audio evaluation
6. Subtitle evaluation
7. Scene-level evaluation
8. Full-video evaluation
9. Quality scoring
10. Automatic regeneration
11. Evaluation dataset
12. Human evaluation
13. Evaluation dashboard
14. Production quality-control pipeline

---

# 2. কেন Evaluation System দরকার?

ধরো user দিল:

> Explain binary search to a beginner in 30 seconds.

AI video বানালো।

কিন্তু সমস্যা হতে পারে:

```text
❌ Wrong explanation
❌ Wrong array
❌ Wrong highlighted element
❌ Narration too fast
❌ Subtitle mismatch
❌ Scene timing wrong
❌ Visual unrelated to narration
❌ Text unreadable
❌ Audio missing
❌ Video corrupted
```

শুধু `video.mp4 exists` মানেই successful generation না।

আমাদের দরকার:

```text
Video Generated
      ↓
Is it correct?
      ↓
Is it educational?
      ↓
Is visual correct?
      ↓
Is audio synchronized?
      ↓
Is subtitle synchronized?
      ↓
PASS / FAIL
```

---

# 3. Evaluation-এর 3 স্তর

আমরা তিন ধরনের evaluation ব্যবহার করব।

## Level 1 — Deterministic

Code দিয়ে check করা যায়।

```text
duration
resolution
FPS
audio exists
subtitle exists
scene timing
file exists
```

## Level 2 — AI Evaluation

LLM/VLM দিয়ে:

```text
accuracy
clarity
visual relevance
educational quality
```

## Level 3 — Human Evaluation

মানুষ দেখে:

```text
Is this actually useful?
```

Production system-এ তিনটিই দরকার।

---

# 4. Complete Evaluation Architecture

```text
                 Generated Video
                       ↓
                ┌──────────────┐
                │ Video Loader │
                └──────┬───────┘
                       ↓
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   Video Check     Audio Check    Subtitle Check
        ↓              ↓              ↓
        └──────────────┼──────────────┘
                       ↓
                  Scene Analysis
                       ↓
                ┌──────┴──────┐
                ↓             ↓
              VLM            LLM
                ↓             ↓
          Visual Quality   Content Quality
                └──────┬──────┘
                       ↓
                 Score Engine
                       ↓
                 PASS / FAIL
                       ↓
              Regeneration Loop
```

---

# 5. Evaluation Categories

আমাদের main categories:

```text
1. Content Accuracy
2. Educational Quality
3. Visual Quality
4. Audio Quality
5. Subtitle Quality
6. Timing / Synchronization
7. Technical Quality
8. Consistency
```

---

# 6. Content Accuracy

প্রথম প্রশ্ন:

> AI যা বলেছে সেটা সত্যি?

Example:

```text
Narration:
"Binary search works on sorted data."
```

সঠিক।

কিন্তু:

```text
"Binary search works on any unsorted array."
```

ভুল।

তাই:

```text
Content Accuracy
       ↓
LLM / trusted knowledge
       ↓
Score
```

---

# 7. Educational Quality

শুধু correct হলেই যথেষ্ট নয়।

Example:

```text
Correct explanation
+
Very complicated language
```

Beginner-এর জন্য ভালো educational content হবে না।

তাই evaluate করব:

```text
Clarity
Completeness
Audience fit
Learning objective coverage
Teaching strategy
```

---

# 8. Visual Quality

VLM ব্যবহার করে check করব:

```text
Does image match narration?
```

Example:

Narration:

> "The middle element is highlighted."

Visual:

```text
10 20 [30] 40 50
```

Good.

কিন্তু যদি:

```text
[10] 20 30 40 50
```

তাহলে mismatch।

---

# 9. Audio Quality

Check করতে হবে:

```text
Audio exists
Volume reasonable
No corruption
Speech understandable
Duration correct
```

Advanced:

```text
Speech rate
Silence
Noise
Pronunciation
```

---

# 10. Subtitle Quality

Check:

```text
Subtitle exists
Correct text
Correct timing
No overlap
No subtitle outside video duration
```

Example:

```text
0.0 ───── 3.2
Binary search is fast.

3.2 ───── 6.0
It works on sorted data.
```

---

# 11. Technical Quality

Basic technical validator:

```python id="i0a7ru"
from pathlib import Path

def validate_video_file(path):
    path = Path(path)

    if not path.exists():
        return False, "Video file does not exist."

    if path.stat().st_size == 0:
        return False, "Video file is empty."

    if path.suffix.lower() != ".mp4":
        return False, "Video must be MP4."

    return True, "Video file is valid."
```

---

# 12. FFprobe দিয়ে Video Check

আমরা M2-এ FFmpeg শিখেছি। এবার সেটা evaluation-এ ব্যবহার করব।

```python id="54a7w7"
import subprocess
import json

def get_video_info(path):

    command = [
        "ffprobe",
        "-v", "quiet",
        "-print_format", "json",
        "-show_format",
        "-show_streams",
        path
    ]

    result = subprocess.run(
        command,
        capture_output=True,
        text=True
    )

    if result.returncode != 0:
        raise RuntimeError(
            result.stderr
        )

    return json.loads(result.stdout)
```

---

# 13. Duration Check

```python id="rj5l4f"
def validate_duration(
    actual_duration,
    expected_duration,
    tolerance=1.0
):
    difference = abs(
        actual_duration - expected_duration
    )

    return difference <= tolerance
```

যদি:

```text
Expected = 30 sec
Actual = 30.4 sec
```

তাহলে acceptable হতে পারে।

কিন্তু:

```text
Expected = 30 sec
Actual = 42 sec
```

তাহলে:

```text
FAIL
```

---

# 14. Scene Timing Evaluation

আমাদের আগের validator ব্যবহার করব:

```python id="i4u9e8"
def validate_scene_timing(scenes):

    previous_end = 0

    for scene in scenes:

        start = scene["start"]
        end = scene["end"]

        if start < previous_end:
            return False

        if end <= start:
            return False

        previous_end = end

    return True
```

---

# 15. Evaluation Schema

এখন একটি central schema তৈরি করি।

```python id="2fghp7"
from pydantic import BaseModel
from typing import List


class EvaluationResult(BaseModel):

    content_accuracy: float
    educational_quality: float
    visual_quality: float
    audio_quality: float
    subtitle_quality: float
    synchronization: float
    technical_quality: float
    consistency: float

    issues: List[str] = []
```

প্রতিটি score:

```text
0.0 → 1.0
```

---

# 16. Overall Quality Score

আমরা weighted score ব্যবহার করব।

```python id="6m1e9x"
def calculate_quality_score(
    content_accuracy,
    educational_quality,
    visual_quality,
    audio_quality,
    subtitle_quality,
    synchronization,
    technical_quality,
    consistency
):

    return (
        content_accuracy * 0.20
        + educational_quality * 0.20
        + visual_quality * 0.15
        + audio_quality * 0.10
        + subtitle_quality * 0.10
        + synchronization * 0.10
        + technical_quality * 0.10
        + consistency * 0.05
    )
```

উদাহরণ:

```text
Content             0.95
Educational         0.90
Visual              0.88
Audio               0.92
Subtitle            0.94
Sync                0.91
Technical           1.00
Consistency         0.87
```

Final:

```text
≈ 0.925
```

অর্থাৎ:

```text
92.5%
```

---

# 17. Pass / Fail Threshold

```python id="03a8hp"
def quality_status(score):

    if score >= 0.85:
        return "PASS"

    if score >= 0.70:
        return "REVIEW"

    return "FAIL"
```

তাহলে:

```text
0.85–1.00 → PASS
0.70–0.84 → HUMAN REVIEW
< 0.70    → FAIL
```

এটা একটি initial policy; পরে real evaluation data দিয়ে thresholds tune করবে।

---

# 18. Scene-Level Evaluation

পুরো video একসাথে evaluate না করে scene-level করা ভালো।

```text id="5h5x2v"
Video
 ↓
Scene 1
 ↓
Evaluate
 ↓
Scene 2
 ↓
Evaluate
 ↓
Scene 3
 ↓
Evaluate
```

কারণ:

```text
Scene 1 → Good
Scene 2 → Good
Scene 3 → Wrong
Scene 4 → Good
```

তাহলে শুধু Scene 3 regenerate করা যাবে।

এতে cost কমবে।

---

# 19. Scene Evaluation Schema

```python id="e9n8lh"
class SceneEvaluation(BaseModel):

    scene_id: int

    narration_visual_match: float

    educational_relevance: float

    visual_quality: float

    readability: float

    timing_quality: float

    issues: list[str] = []
```

---

# 20. VLM Evaluation

M20-এ আমরা VLM শিখেছি।

এখন VLM-এর কাজ:

```text
Scene Image
+
Narration
+
Visual Plan
       ↓
      VLM
       ↓
Evaluation JSON
```

Prompt:

```python id="d9jz87"
def build_vlm_evaluation_prompt(
    narration,
    visual_description
):

    return f"""
Evaluate this educational scene.

Narration:
{narration}

Expected visual:
{visual_description}

Check:

1. Does the visual match the narration?
2. Does it represent the intended concept?
3. Is the composition clear?
4. Is the educational meaning obvious?
5. Is important text readable?

Return JSON:

{{
    "narration_visual_match": 0.0,
    "educational_relevance": 0.0,
    "visual_quality": 0.0,
    "readability": 0.0,
    "issues": []
}}

Return JSON only.
"""
```

---

# 21. Example VLM Result

```json id="9x08pp"
{
  "narration_visual_match": 0.96,
  "educational_relevance": 0.94,
  "visual_quality": 0.91,
  "readability": 0.88,
  "issues": []
}
```

Good scene।

---

# 22. Bad Scene Example

```json id="6f3xxr"
{
  "narration_visual_match": 0.42,
  "educational_relevance": 0.55,
  "visual_quality": 0.78,
  "readability": 0.83,
  "issues": [
    "The highlighted element does not appear to be the middle element.",
    "The visual does not clearly communicate binary search."
  ]
}
```

এখন scene regenerate করতে হবে।

---

# 23. LLM Content Evaluation

VLM visual দেখে।

LLM content evaluate করতে পারে।

Architecture:

```text
Script
+
Learning Objectives
+
Scene Plan
       ↓
      LLM
       ↓
Content Evaluation
```

Prompt:

```python id="4wz8oe"
def build_content_evaluation_prompt(
    topic,
    learning_objectives,
    script
):

    return f"""
Evaluate this educational script.

Topic:
{topic}

Learning objectives:
{learning_objectives}

Script:
{script}

Evaluate:

- factual accuracy
- clarity
- audience suitability
- learning objective coverage
- logical structure
- unnecessary information

Return JSON only.
"""
```

---

# 24. Evaluation JSON

```json id="8a7g31"
{
  "factual_accuracy": 0.96,
  "clarity": 0.91,
  "audience_fit": 0.94,
  "objective_coverage": 0.89,
  "logical_structure": 0.93,
  "issues": []
}
```

---

# 25. Audio Evaluation

আমাদের audio evaluator:

```python id="f6kqg2"
class AudioEvaluation(BaseModel):

    exists: bool
    duration: float
    speech_quality: float
    volume_quality: float
    clarity: float
    issues: list[str] = []
```

Basic validation:

```python id="u0s1cj"
def validate_audio(
    audio_path,
    expected_duration
):

    actual_duration = get_audio_duration(
        audio_path
    )

    duration_ok = (
        abs(actual_duration - expected_duration)
        <= 1.0
    )

    return {
        "exists": True,
        "duration": actual_duration,
        "duration_ok": duration_ok
    }
```

---

# 26. Subtitle Evaluation

```python id="4r9e0c"
def validate_subtitles(
    subtitles,
    video_duration
):

    previous_end = 0

    for subtitle in subtitles:

        start = subtitle["start"]
        end = subtitle["end"]

        if start < previous_end:
            return False, "Subtitle overlap"

        if end <= start:
            return False, "Invalid subtitle timing"

        if end > video_duration:
            return False, "Subtitle exceeds video"

        previous_end = end

    return True, "Subtitles valid"
```

---

# 27. Narration বনাম Subtitle Check

Whisper দিয়ে generated audio আবার transcribe করা যায়।

```text id="p8cq7f"
Generated TTS
     ↓
Whisper
     ↓
Actual transcript
     ↓
Compare
     ↓
Original script
```

Example:

Original:

```text
Binary search checks the middle element.
```

Actual:

```text
Binary search checks the middle element.
```

Good।

যদি:

```text
Binary search checks the middle number.
```

তাহলে semantic difference detect করা যায়।

---

# 28. Text Similarity

একটি simple baseline:

```python id="6z0k7k"
from difflib import SequenceMatcher

def text_similarity(a, b):

    return SequenceMatcher(
        None,
        a.lower(),
        b.lower()
    ).ratio()
```

Example:

```python id="y9d9zv"
score = text_similarity(
    "Binary search checks the middle element.",
    "Binary search checks the middle element."
)

print(score)
```

Result:

```text
1.0
```

---

# 29. কিন্তু Exact Text Similarity সবসময় যথেষ্ট নয়

Example:

```text
A:
Binary search checks the middle element.

B:
We first examine the center item.
```

String similarity কম।

কিন্তু meaning একই।

তাই advanced system:

```text
Exact similarity
+
Embedding similarity
+
LLM semantic evaluation
```

ব্যবহার করবে।

---

# 30. Synchronization Evaluation

এটা আমাদের project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

আমাদের check করতে হবে:

```text
Narration
      ↕
Animation
      ↕
Subtitle
```

Example:

Narration:

> "The middle element is highlighted."

Animation:

```text
highlight middle
```

Subtitle:

```text
The middle element is highlighted.
```

সব synchronized হলে:

```text
SYNC = GOOD
```

---

# 31. Sync Schema

```python id="d9b8w8"
class SyncEvaluation(BaseModel):

    narration_animation: float
    narration_subtitle: float
    visual_timing: float
    overall_sync: float
    issues: list[str] = []
```

---

# 32. Automatic Regeneration Loop

এখন M25-এর সবচেয়ে powerful feature:

```text id="1yq6gs"
Generate
   ↓
Evaluate
   ↓
Score
   ↓
 ┌───────────────┐
 │               │
 PASS           FAIL
 │               │
 ↓               ↓
Accept      Improve Prompt
                 ↓
              Generate
                 ↓
              Evaluate
```

---

# 33. Regeneration Manager

```python id="f1m42h"
class RegenerationManager:

    def __init__(
        self,
        generator,
        evaluator,
        max_attempts=3
    ):
        self.generator = generator
        self.evaluator = evaluator
        self.max_attempts = max_attempts

    def generate(self, request):

        for attempt in range(
            self.max_attempts
        ):

            result = self.generator.generate(
                request
            )

            evaluation = self.evaluator.evaluate(
                result
            )

            if evaluation["score"] >= 0.85:
                return result

            request = self.improve_request(
                request,
                evaluation
            )

        raise RuntimeError(
            "Generation failed quality check."
        )
```

---

# 34. Prompt Improvement

যদি evaluator বলে:

```text
The middle element is not clearly highlighted.
```

তাহলে next prompt:

```text
Make the middle element visually dominant.
Use a clear highlight around the center cell.
Do not highlight other array elements.
```

অর্থাৎ:

```text
Evaluation
 ↓
Issue
 ↓
Prompt Improvement
 ↓
Regeneration
```

---

# 35. Evaluation Report

প্রতিটি project-এর জন্য save করব:

```text id="4f3yhl"
projects/
└── project_001/
    ├── plan.json
    ├── evaluation.json
    ├── scenes/
    ├── audio/
    ├── subtitles/
    └── output/
        └── final.mp4
```

`evaluation.json`:

```json id="ldgr6v"
{
  "overall_score": 0.91,
  "status": "PASS",
  "content_accuracy": 0.95,
  "educational_quality": 0.91,
  "visual_quality": 0.89,
  "audio_quality": 0.93,
  "subtitle_quality": 0.95,
  "synchronization": 0.90,
  "technical_quality": 1.0,
  "consistency": 0.88,
  "issues": []
}
```

---

# 36. Evaluation History

Production system-এ শুধু latest score রাখবে না।

```text id="0whqxh"
Attempt 1
Score = 0.61
FAIL

Attempt 2
Score = 0.74
REVIEW

Attempt 3
Score = 0.91
PASS
```

এতে বুঝতে পারবে:

```text
How many regenerations?
Which errors?
Which model?
Which prompt?
Which scene?
```

---

# 37. Evaluation Database Model

Django ব্যবহার করলে:

```python id="qskh5h"
class VideoEvaluation(models.Model):

    project_id = models.CharField(
        max_length=100
    )

    overall_score = models.FloatField()

    content_accuracy = models.FloatField()

    educational_quality = models.FloatField()

    visual_quality = models.FloatField()

    audio_quality = models.FloatField()

    subtitle_quality = models.FloatField()

    synchronization = models.FloatField()

    technical_quality = models.FloatField()

    consistency = models.FloatField()

    status = models.CharField(
        max_length=20
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

# 38. Scene Evaluation Database

```python id="0td5s4"
class SceneEvaluation(models.Model):

    video_evaluation = models.ForeignKey(
        VideoEvaluation,
        on_delete=models.CASCADE
    )

    scene_id = models.IntegerField()

    visual_match = models.FloatField()

    educational_relevance = models.FloatField()

    readability = models.FloatField()

    timing_quality = models.FloatField()

    score = models.FloatField()

    issues = models.JSONField(
        default=list
    )
```

এতে scene-level analytics পাওয়া যাবে।

---

# 39. Human Evaluation

AI evaluator perfect হবে না।

তাই human review দরকার।

UI:

```text id="tqj9xb"
┌───────────────────────────────┐
│        Video Preview          │
│                               │
│          ▶ PLAY               │
│                               │
└───────────────────────────────┘

Content Accuracy:     ⭐⭐⭐⭐⭐
Educational Value:    ⭐⭐⭐⭐⭐
Visual Quality:       ⭐⭐⭐⭐⭐
Audio Quality:        ⭐⭐⭐⭐⭐
Overall:              ⭐⭐⭐⭐⭐

[ Approve ] [ Reject ] [ Edit ]
```

---

# 40. Human Evaluation Dataset

Reviewer data save করবে:

```json id="c0z8j7"
{
  "video_id": "video_001",
  "human_score": 4.5,
  "content_accuracy": 5,
  "educational_value": 4,
  "visual_quality": 5,
  "audio_quality": 4,
  "approved": true
}
```

এগুলো ভবিষ্যতে:

```text
Evaluation Dataset
```

হিসেবে ব্যবহার করা যাবে।

---

# 41. AI Score বনাম Human Score

এটা খুব valuable।

ধরো:

```text
AI Score = 0.92
Human Score = 0.60
```

মানে:

```text
AI evaluator ভুলভাবে high score দিয়েছে।
```

অথবা:

```text
AI Score = 0.70
Human Score = 0.90
```

তাহলে evaluator overly strict হতে পারে।

আমরা পরে:

```text
AI Evaluation
       +
Human Evaluation
       ↓
Better Evaluation Model
```

বানাতে পারি।

---

# 42. M25 Evaluation Dashboard

Production UI:

```text id="8m8x8h"
Educational Video Evaluation
────────────────────────────────

Overall Score       91%

Content Accuracy    95%
Educational Quality 91%
Visual Quality      89%
Audio Quality       93%
Subtitle Quality    95%
Synchronization     90%
Technical Quality  100%
Consistency         88%

Status: PASS
```

Scene breakdown:

```text id="9l44kh"
Scene 1   94%   PASS
Scene 2   92%   PASS
Scene 3   68%   FAIL
Scene 4   91%   PASS
Scene 5   95%   PASS
```

System automatically:

```text
Regenerate Scene 3
```

---

# 43. M25-এর Production Architecture

সব milestone combine করলে:

```text id="8qf4vz"
                    USER
                      ↓
                  Django API
                      ↓
                Educational LLM
                      ↓
                  VideoPlan
                      ↓
                Scene Planner
                      ↓
             ┌────────┼────────┐
             ↓        ↓        ↓
           Manim    Image     Video
                     LoRA     Model
             └────────┼────────┘
                      ↓
                     VLM
                      ↓
                Scene Evaluation
                      ↓
             ┌────────┴────────┐
             ↓                 ↓
          PASS               FAIL
             ↓                 ↓
           TTS            Regenerate
             ↓                 ↑
        Subtitle             │
             ↓                │
          FFmpeg ─────────────┘
             ↓
        Final Video
             ↓
       Full Evaluation
             ↓
       PASS / REVIEW / FAIL
             ↓
          Storage
```

---

# 44. Evaluation Rules Engine

সব evaluation AI দিয়ে করা উচিত নয়।

আমি recommend করব:

```text id="jjx2mx"
Deterministic
     +
AI
     +
Human
```

### Deterministic

```text
File exists
Duration
FPS
Resolution
Audio
Subtitle
Timing
```

### VLM

```text
Visual correctness
Visual relevance
Composition
Readability
```

### LLM

```text
Factual accuracy
Clarity
Learning objectives
Audience fit
```

### Human

```text
Actual usefulness
Engagement
Overall quality
```

---

# 45. Quality Gate

Production-এ final gate:

```python id="mbgq5h"
def quality_gate(result):

    if result["technical_quality"] < 0.95:
        return "FAIL"

    if result["content_accuracy"] < 0.85:
        return "FAIL"

    if result["educational_quality"] < 0.80:
        return "REVIEW"

    if result["overall_score"] >= 0.85:
        return "PASS"

    return "REVIEW"
```

Technical quality-এর ক্ষেত্রে আমরা content score-এর চেয়ে stricter হতে পারি।

---

# 46. Evaluation is NOT Just a Score

একটা বড় ভুল:

```text
Score = 0.91
```

বলেই শেষ করা।

আমাদের দরকার:

```text
Score
+
Reason
+
Detected Issues
+
Affected Scene
+
Suggested Fix
```

Example:

```json id="m1q1fh"
{
  "score": 0.76,
  "status": "REVIEW",
  "issues": [
    {
      "scene_id": 3,
      "type": "visual_mismatch",
      "description": "Middle element is not highlighted.",
      "severity": "high",
      "suggestion": "Highlight the center array element."
    }
  ]
}
```

এটাই production-grade evaluation।

---

# 47. M25 Mini Project 🎯

এখন তোমার practical project:

## **Educational Video Quality Controller**

Input:

```text
final.mp4
+
plan.json
```

System:

```text id="8v1gkv"
Video
 ↓
Technical Check
 ↓
Audio Check
 ↓
Subtitle Check
 ↓
Extract Scenes
 ↓
VLM
 ↓
LLM
 ↓
Score Engine
 ↓
Evaluation Report
```

Output:

```json id="r5j1mv"
{
  "overall_score": 0.89,
  "status": "PASS",
  "issues": [],
  "scene_scores": [
    0.92,
    0.88,
    0.86,
    0.91
  ]
}
```

---

# 48. M25 Project Structure

```text id="o0o5nm"
educational_video_ai/
│
├── evaluation/
│   ├── __init__.py
│   │
│   ├── schema.py
│   ├── technical.py
│   ├── audio.py
│   ├── subtitle.py
│   ├── timing.py
│   │
│   ├── content.py
│   ├── visual.py
│   ├── synchronization.py
│   │
│   ├── scoring.py
│   ├── quality_gate.py
│   ├── evaluator.py
│   └── report.py
│
├── regeneration/
│   ├── manager.py
│   └── prompt_improver.py
│
├── projects/
│
└── ...
```

---

# 49. Central Evaluator

সবশেষে:

```python id="4z8o0x"
class EducationalVideoEvaluator:

    def __init__(
        self,
        technical_checker,
        audio_checker,
        subtitle_checker,
        content_checker,
        visual_checker,
        sync_checker
    ):

        self.technical_checker = technical_checker
        self.audio_checker = audio_checker
        self.subtitle_checker = subtitle_checker
        self.content_checker = content_checker
        self.visual_checker = visual_checker
        self.sync_checker = sync_checker

    def evaluate(
        self,
        video,
        plan
    ):

        technical = (
            self.technical_checker
            .evaluate(video)
        )

        audio = (
            self.audio_checker
            .evaluate(video)
        )

        subtitles = (
            self.subtitle_checker
            .evaluate(video)
        )

        content = (
            self.content_checker
            .evaluate(plan)
        )

        visual = (
            self.visual_checker
            .evaluate(video, plan)
        )

        sync = (
            self.sync_checker
            .evaluate(video, plan)
        )

        return self.build_report(
            technical,
            audio,
            subtitles,
            content,
            visual,
            sync
        )
```

এটাই M25-এর **central evaluation brain**।

---

# 50. M25 Completion Checklist

তুমি M25 complete করলে এগুলো পারবে:

* [ ] Technical video validation
* [ ] FFprobe evaluation
* [ ] Audio validation
* [ ] Subtitle validation
* [ ] Scene timing validation
* [ ] LLM content evaluation
* [ ] VLM visual evaluation
* [ ] Narration-visual matching
* [ ] Audio-subtitle synchronization
* [ ] Quality scoring
* [ ] PASS/REVIEW/FAIL
* [ ] Scene-level evaluation
* [ ] Automatic regeneration
* [ ] Prompt improvement
* [ ] Evaluation history
* [ ] Human evaluation
* [ ] Evaluation database
* [ ] Evaluation dashboard
* [ ] Quality gate

---

# 🔥 M25-এর Core Architecture

সবচেয়ে গুরুত্বপূর্ণভাবে এটা মনে রাখবে:

```text
              GENERATE
                 ↓
              EVALUATE
                 ↓
             QUALITY?
            ↙         ↘
          YES          NO
           ↓            ↓
        ACCEPT      IMPROVE
                        ↓
                    REGENERATE
                        ↓
                     EVALUATE
```

আর তোমার পুরো AI system এখন:

```text
LLM
 ↓
Educational Planning
 ↓
Scene JSON
 ↓
 ┌─────────┬──────────┬─────────┐
 ↓         ↓          ↓
Manim   Image LoRA  Video Model
 ↓         ↓          ↓
 └─────────┴──────────┘
             ↓
            VLM
             ↓
         Evaluation
             ↓
            TTS
             ↓
         Subtitle
             ↓
          FFmpeg
             ↓
        Final Video
             ↓
      Final Evaluation
             ↓
      PASS / REVIEW / FAIL
```

**M25-এর মূল শিক্ষা:**

> **Generate করা AI-এর প্রথম কাজ; নিজের output যাচাই করে ভুল হলে নিজে improve করা—এটাই production-grade AI system-এর গুরুত্বপূর্ণ বৈশিষ্ট্য।**

এর পরের **M26 = RAG + Trusted Knowledge** — সেখানে আমরা AI-এর factual hallucination কমিয়ে **trusted sources/knowledge base থেকে verified educational content** তৈরি করার architecture বানাব।
