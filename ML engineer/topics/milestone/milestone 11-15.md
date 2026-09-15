# M11 — Animation Generation Engine

M10-এ আমরা শিখেছি **Visual Plan তৈরি করা**।

এখন M11-এ আমরা সেই Visual Plan-কে **বাস্তব animation/video-তে convert করব**।

এটা আমাদের project-এর খুব গুরুত্বপূর্ণ milestone:

```text
User Topic
    ↓
M8 Educational Planner
    ↓
M9 Script Generator
    ↓
M10 Visual Planner
    ↓
M11 Animation Engine
    ↓
Manim
    ↓
MP4 Video
```

আজকের লক্ষ্য হবে প্রথমে **deterministic educational animation engine** বানানো।

---

# 1. M11-এর মূল লক্ষ্য

ধরো M10 আমাদের দিয়েছে:

```json
{
  "scene_id": 1,
  "objects": [
    {
      "name": "array",
      "type": "array",
      "position": "center"
    }
  ],
  "animations": [
    {
      "action": "show",
      "object": "array"
    }
  ]
}
```

M11-এর কাজ:

```text
JSON
 ↓
Read JSON
 ↓
Understand objects
 ↓
Create visual objects
 ↓
Execute animation actions
 ↓
Render
 ↓
MP4
```

অর্থাৎ:

> **M10 বলে কী করতে হবে, M11 সেটা করে।**

---

# 2. কেন Manim?

আমাদের educational AI-এর জন্য শুরুতে Manim খুব useful।

কারণ:

* mathematical animation করা যায়
* algorithm visualization করা যায়
* diagrams তৈরি করা যায়
* equations animate করা যায়
* text/highlight/pointer করা যায়
* Python দিয়ে control করা যায়
* একই design reproducibly তৈরি করা যায়

বিশেষ করে:

```text
Algorithm
Math
Physics
Computer Science
Programming
Data Structures
Flowcharts
Diagrams
```

এসবের জন্য Manim excellent।

তবে মনে রাখবে:

> Manim আমাদের পুরো final video generator নয়।

পরে আমরা আরও যোগ করব:

```text
Manim
+
Image Generation
+
Video Diffusion
+
TTS
+
Subtitles
+
FFmpeg
```

---

# 3. M11 Architecture

```text
                 Visual Plan JSON
                       ↓
              ┌─────────────────┐
              │ Plan Interpreter│
              └────────┬────────┘
                       ↓
              ┌─────────────────┐
              │ Object Factory  │
              └────────┬────────┘
                       ↓
              ┌─────────────────┐
              │ Animation Engine│
              └────────┬────────┘
                       ↓
                    Manim
                       ↓
                  Scene MP4
```

---

# 4. Installation

Ubuntu-তে:

```bash
sudo apt update
```

তারপর:

```bash
sudo apt install ffmpeg
```

Virtual environment activate করো:

```bash
source .venv/bin/activate
```

Manim:

```bash
pip install manim
```

Check:

```bash
manim --version
```

যদি কাজ করে, version দেখতে পাবে।

---

# 5. Project Structure

M11-এর জন্য structure:

```text
educational_video_ai/
│
├── planner/
│   ├── visual_schema.py
│   ├── visual_planner.py
│   └── visual_validator.py
│
├── scenes/
│   └── visual_plans/
│
├── renderer/
│   ├── __init__.py
│   ├── objects.py
│   ├── animations.py
│   ├── interpreter.py
│   └── render_scene.py
│
├── output/
│
└── scripts/
```

---

# 6. প্রথম Manim Animation

প্রথমে AI বাদ দিয়ে basic Manim বুঝি।

Create:

```text
renderer/hello_scene.py
```

Code:

```python
from manim import *


class HelloScene(Scene):

    def construct(self):

        text = Text("Educational AI")

        self.play(Write(text))

        self.wait(2)
```

Run:

```bash
manim -pql renderer/hello_scene.py HelloScene
```

এখানে:

```text
-p
```

মানে preview।

```text
-q
```

মানে quality।

```text
l
```

মানে low quality।

Output হবে একটি MP4।

---

# 7. Manim-এর Basic Concept

Manim-এ মূলত:

```text
Scene
 ↓
Mobject
 ↓
Animation
 ↓
Render
```

### Scene

ভিডিওর একটি scene।

```python
class MyScene(Scene):
    def construct(self):
        pass
```

### Mobject

Visual object।

যেমন:

```python
Circle()
Square()
Rectangle()
Text()
MathTex()
Arrow()
Line()
```

### Animation

Object-এর উপর action।

```python
Write()
Create()
FadeIn()
FadeOut()
Transform()
MoveToTarget()
```

---

# 8. আমাদের Object System

M10 থেকে object আসবে:

```json
{
  "name": "circle",
  "object_type": "circle",
  "position": "center"
}
```

M11-এ আমরা একটা **Object Factory** বানাব।

Create:

```text
renderer/objects.py
```

```python
from manim import *


def create_object(object_data):

    object_type = object_data["object_type"]

    if object_type == "circle":
        return Circle()

    elif object_type == "square":
        return Square()

    elif object_type == "rectangle":
        return Rectangle()

    elif object_type == "text":
        return Text(
            object_data.get("label", "")
        )

    elif object_type == "arrow":
        return Arrow(
            LEFT,
            RIGHT
        )

    else:
        raise ValueError(
            f"Unknown object type: {object_type}"
        )
```

এখন:

```text
JSON object
     ↓
create_object()
     ↓
Manim Mobject
```

---

# 9. Position System

M10-এ আমরা position দিয়েছিলাম:

```text
center
top
bottom
left
right
top_left
top_right
bottom_left
bottom_right
```

এগুলো Manim coordinate-এ convert করব।

Create:

```text
renderer/objects.py
```

এবার update:

```python
from manim import *


POSITIONS = {
    "center": ORIGIN,
    "top": UP * 2.5,
    "bottom": DOWN * 2.5,
    "left": LEFT * 4,
    "right": RIGHT * 4,
    "top_left": UP * 2.5 + LEFT * 4,
    "top_right": UP * 2.5 + RIGHT * 4,
    "bottom_left": DOWN * 2.5 + LEFT * 4,
    "bottom_right": DOWN * 2.5 + RIGHT * 4,
}


def get_position(position):

    return POSITIONS.get(
        position,
        ORIGIN
    )


def create_object(object_data):

    object_type = object_data["object_type"]

    if object_type == "circle":
        obj = Circle()

    elif object_type == "square":
        obj = Square()

    elif object_type == "rectangle":
        obj = Rectangle()

    elif object_type == "text":
        obj = Text(
            object_data.get("label", "")
        )

    elif object_type == "arrow":
        obj = Arrow(
            LEFT,
            RIGHT
        )

    else:
        raise ValueError(
            f"Unknown object type: {object_type}"
        )

    position = object_data.get(
        "position",
        "center"
    )

    obj.move_to(
        get_position(position)
    )

    return obj
```

এখন:

```json
{
  "object_type": "circle",
  "position": "top_right"
}
```

automatically top-right-এ যাবে।

---

# 10. Animation Factory

এখন action system তৈরি করব।

Create:

```text
renderer/animations.py
```

```python
from manim import *


def create_animation(
    action,
    obj,
    target=None
):

    if action == "show":
        return FadeIn(obj)

    elif action == "fade_in":
        return FadeIn(obj)

    elif action == "fade_out":
        return FadeOut(obj)

    elif action == "draw":
        return Create(obj)

    elif action == "write":
        return Write(obj)

    elif action == "highlight":
        return Indicate(obj)

    else:
        raise ValueError(
            f"Unknown animation: {action}"
        )
```

এখন:

```text
"show"
↓
FadeIn()

"draw"
↓
Create()

"write"
↓
Write()

"highlight"
↓
Indicate()
```

---

# 11. প্রথম AI-Generated Scene

এখন একটা JSON বানাই।

Create:

```text
scenes/visual_plans/scene_001.json
```

```json
{
  "scene_id": 1,

  "visual_style": "clean_2d",

  "objects": [
    {
      "name": "title",
      "object_type": "text",
      "position": "top",
      "label": "Binary Search"
    },

    {
      "name": "box",
      "object_type": "square",
      "position": "center"
    }
  ],

  "animations": [
    {
      "action": "write",
      "object": "title",
      "start": 0,
      "duration": 1
    },

    {
      "action": "show",
      "object": "box",
      "start": 1,
      "duration": 1
    },

    {
      "action": "highlight",
      "object": "box",
      "start": 2,
      "duration": 1
    }
  ],

  "camera": {
    "action": "static"
  },

  "on_screen_text": []
}
```

---

# 12. Plan Interpreter

এখন আমাদের সবচেয়ে গুরুত্বপূর্ণ component:

```text
renderer/interpreter.py
```

```python
from .objects import create_object
from .animations import create_animation


class PlanInterpreter:

    def __init__(self, plan):

        self.plan = plan

        self.objects = {}

    def build_objects(self):

        for obj_data in self.plan["objects"]:

            name = obj_data["name"]

            obj = create_object(
                obj_data
            )

            self.objects[name] = obj

    def get_object(self, name):

        if name not in self.objects:

            raise ValueError(
                f"Object not found: {name}"
            )

        return self.objects[name]
```

এখন interpreter JSON-এর object-গুলোকে Manim object-এ convert করতে পারে।

---

# 13. Scene Renderer

Create:

```text
renderer/render_scene.py
```

```python
import json

from manim import *

from .interpreter import PlanInterpreter
from .animations import create_animation


class GeneratedScene(Scene):

    def construct(self):

        with open(
            "scenes/visual_plans/scene_001.json",
            "r"
        ) as file:

            plan = json.load(file)

        interpreter = PlanInterpreter(plan)

        interpreter.build_objects()

        objects = interpreter.objects

        for obj in objects.values():
            self.add(obj)

        for animation_data in plan["animations"]:

            action = animation_data["action"]

            object_name = animation_data["object"]

            obj = interpreter.get_object(
                object_name
            )

            animation = create_animation(
                action,
                obj
            )

            self.play(
                animation,
                run_time=animation_data["duration"]
            )

        self.wait(1)
```

Run:

```bash
manim -pql renderer/render_scene.py GeneratedScene
```

এখন:

```text
JSON
 ↓
Python
 ↓
Manim
 ↓
MP4
```

---

# 14. একটা গুরুত্বপূর্ণ সমস্যা

উপরের code-এ:

```python
self.add(obj)
```

করলে object শুরু থেকেই scene-এ থাকবে।

কিন্তু আমরা চাই:

```text
0 sec → object invisible
1 sec → FadeIn
```

তাই object-কে initially scene-এ add না করে animation অনুযায়ী add করতে হবে।

এটা ঠিক করার জন্য আমরা interpreter-কে আরও intelligent করব।

---

# 15. Improved Animation Engine

```python
class PlanInterpreter:

    def __init__(self, plan, scene):

        self.plan = plan
        self.scene = scene
        self.objects = {}

    def build_objects(self):

        for obj_data in self.plan["objects"]:

            name = obj_data["name"]

            obj = create_object(
                obj_data
            )

            self.objects[name] = obj

    def get_object(self, name):

        if name not in self.objects:

            raise ValueError(
                f"Object not found: {name}"
            )

        return self.objects[name]

    def execute_animation(
        self,
        animation_data
    ):

        action = animation_data["action"]

        object_name = animation_data["object"]

        obj = self.get_object(
            object_name
        )

        animation = create_animation(
            action,
            obj
        )

        self.scene.play(
            animation,
            run_time=animation_data[
                "duration"
            ]
        )
```

---

# 16. Scene-এর ভিতরে

```python
class GeneratedScene(Scene):

    def construct(self):

        with open(
            "scenes/visual_plans/scene_001.json"
        ) as file:

            plan = json.load(file)

        interpreter = PlanInterpreter(
            plan,
            self
        )

        interpreter.build_objects()

        for animation_data in plan["animations"]:

            interpreter.execute_animation(
                animation_data
            )

        self.wait(1)
```

এখন animation engine clean হয়ে গেল।

---

# 17. Object Registry

এখানে আমরা একটা powerful concept ব্যবহার করছি:

```text
Object Registry
```

মানে:

```python
{
    "title": Text(...),
    "box": Square(...)
}
```

তাই JSON বলতে পারবে:

```json
{
  "object": "box"
}
```

Python খুঁজে বের করবে:

```python
objects["box"]
```

এটা ভবিষ্যতে অনেক কাজে লাগবে।

---

# 18. Move Animation

এখন `move` যোগ করি।

`animations.py`:

```python
from manim import *


def create_animation(
    action,
    obj,
    target=None
):

    if action == "show":
        return FadeIn(obj)

    elif action == "fade_in":
        return FadeIn(obj)

    elif action == "fade_out":
        return FadeOut(obj)

    elif action == "draw":
        return Create(obj)

    elif action == "write":
        return Write(obj)

    elif action == "highlight":
        return Indicate(obj)

    elif action == "move":

        if target is None:
            raise ValueError(
                "Move animation requires target."
            )

        return obj.animate.move_to(
            target
        )

    else:

        raise ValueError(
            f"Unknown animation: {action}"
        )
```

তবে এখানে `target` coordinate হতে পারে।

যেমন:

```python
target = RIGHT * 3
```

---

# 19. Highlight Animation

Educational video-তে highlight অত্যন্ত গুরুত্বপূর্ণ।

Example:

```text
[10] [20] [30] [40] [50]
              ↑
           HIGHLIGHT
```

Manim:

```python
self.play(
    Indicate(middle_element)
)
```

আমাদের JSON:

```json
{
  "action": "highlight",
  "object": "middle_element",
  "start": 5,
  "duration": 1
}
```

---

# 20. Binary Search Example

এখন আসল educational visualization বানানোর চেষ্টা করি।

Visual:

```text
10   20   30   40   50   60   70
                  ↑
                middle
```

Create:

```text
renderer/binary_search_scene.py
```

```python
from manim import *


class BinarySearchScene(Scene):

    def construct(self):

        numbers = [
            Text(str(n))
            for n in [10, 20, 30, 40, 50, 60, 70]
        ]

        group = VGroup(*numbers)

        group.arrange(
            RIGHT,
            buff=0.5
        )

        self.play(
            Write(group)
        )

        middle = numbers[3]

        self.play(
            Indicate(middle)
        )

        label = Text(
            "Check the middle element"
        )

        label.next_to(
            middle,
            DOWN
        )

        self.play(
            Write(label)
        )

        self.wait(2)
```

Run:

```bash
manim -pql renderer/binary_search_scene.py BinarySearchScene
```

এটাই আমাদের first educational animation।

---

# 21. কিন্তু আমাদের লক্ষ্য Hardcoded Animation নয়

উপরের:

```python
numbers = [...]
middle = numbers[3]
```

hardcoded।

আমাদের final system এমন হবে:

```text
User:
"Explain Binary Search"
```

LLM:

```json
{
  "objects": [...],
  "animations": [...]
}
```

Renderer:

```text
JSON
 ↓
Object Factory
 ↓
Animation Factory
 ↓
Manim
 ↓
MP4
```

অর্থাৎ Python code manually লিখতে হবে না।

---

# 22. M11-এর সবচেয়ে গুরুত্বপূর্ণ Architecture

শেষ architecture:

```text
                  USER
                    ↓
              Educational Topic
                    ↓
                  M8
                    ↓
             Educational Plan
                    ↓
                  M9
                    ↓
                 Script
                    ↓
                 M10
                    ↓
              Visual Plan JSON
                    ↓
          ┌─────────────────────┐
          │   M11 Renderer      │
          │                     │
          │ JSON Parser         │
          │ Object Factory      │
          │ Animation Factory   │
          │ Timeline Engine     │
          └──────────┬──────────┘
                     ↓
                   Manim
                     ↓
                  Scene MP4
```

---

# 23. Timeline Engine

এখন একটা গুরুত্বপূর্ণ সমস্যা আছে।

M10 আমাদের দিয়েছে:

```text
Animation 1 → start 0
Animation 2 → start 2
Animation 3 → start 5
```

কিন্তু আমাদের renderer এখন sequentially execute করছে।

Future-এ আমাদের **timeline engine** লাগবে।

Concept:

```python
animations = sorted(
    animations,
    key=lambda x: x["start"]
)
```

তারপর:

```text
Current Time = 0

Animation start = 0
→ execute

Animation start = 2
→ wait until 2

Animation start = 5
→ wait until 5
```

আর advanced version-এ একই সময়ে multiple animation:

```text
0–2 sec

Plant appears
+
Sun appears
+
Title appears
```

একসাথে execute করা যাবে:

```python
self.play(
    FadeIn(plant),
    FadeIn(sun),
    Write(title)
)
```

এটা M11-এর next refinement।

---

# 24. M11-এ আমরা এখন কী তৈরি করেছি?

তোমার system এখন conceptually পারে:

```text
✓ JSON read করতে
✓ Object তৈরি করতে
✓ Object position করতে
✓ Animation select করতে
✓ Animation execute করতে
✓ Manim render করতে
✓ MP4 তৈরি করতে
```

এটাই আমাদের **Animation Engine v1**।

---

# 25. M11 Mini Project

এখন তোমার practice project:

## Topic

```text
Explain Stack Data Structure
```

Visual:

```text
      ┌─────┐
      │ 30  │ ← TOP
      ├─────┤
      │ 20  │
      ├─────┤
      │ 10  │
      └─────┘
```

Animation:

```text
1. Show stack
2. Show PUSH
3. Add 40
4. Highlight TOP
5. Show POP
6. Remove 40
```

Expected:

```text
Narration
    ↓
Visual Plan
    ↓
JSON
    ↓
M11 Renderer
    ↓
Manim
    ↓
stack.mp4
```

---

# 26. M11 Completion Test

তুমি M11 complete করেছো যদি তুমি নিজে:

### Test 1

একটি JSON থেকে:

```text
Circle
Square
Text
```

generate করতে পারো।

### Test 2

JSON থেকে:

```text
FadeIn
FadeOut
Write
Create
Highlight
```

execute করতে পারো।

### Test 3

একটি educational diagram তৈরি করতে পারো।

### Test 4

JSON → Manim → MP4 pipeline চালাতে পারো।

### Test 5

Hardcoded Python animation-এর পরিবর্তে JSON-driven animation তৈরি করতে পারো।

---

# 27. M1 → M11 Progress

এখন আমাদের পুরো system:

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
M6  Vision Model
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
```

এখন পর্যন্ত সবচেয়ে গুরুত্বপূর্ণ transition:

```text
M9
"What should we say?"
        ↓
M10
"What should we show?"
        ↓
M11
"How do we animate it?"
```

---

# 🚀 M12 — Advanced Animation & Diagram Engine

M12-এ আমরা M11-কে আরও powerful করব।

শিখব:

```text
Arrays
↓
Linked Lists
↓
Trees
↓
Graphs
↓
Flowcharts
↓
Equations
↓
Charts
↓
Code Blocks
↓
Pointers
↓
Arrows
↓
Camera Movement
↓
Zoom
↓
Transform
```

এবং সবচেয়ে গুরুত্বপূর্ণ:

```text
Visual Plan JSON
       ↓
Generic Renderer
       ↓
Algorithm / Math / Science / Programming
       ↓
Automatically generated educational animation
```

অর্থাৎ M12 থেকে আমরা **একটা generic educational animation engine** বানাতে শুরু করব—শুধু Binary Search বা Stack-এর জন্য নয়।


----
# M12 — Advanced Animation & Generic Diagram Engine

M11-এ আমরা বানিয়েছি **JSON → Manim → MP4** basic animation engine।

এখন M12-এর লক্ষ্য হলো এটাকে এমনভাবে design করা যাতে **একটা নির্দিষ্ট algorithm-এর জন্য hardcode না করে**, একই engine দিয়ে:

* Algorithm
* Data Structure
* Mathematics
* Programming
* Physics
* Biology
* Networking
* Flowchart
* Process
* Diagram
* Charts

সব ধরনের educational visual তৈরি করা যায়।

---

# 1. M12-এর মূল লক্ষ্য

এখন আমাদের pipeline:

```text
User Topic
    ↓
M8 Planner
    ↓
M9 Script
    ↓
M10 Visual Plan
    ↓
M11 Animation Engine
    ↓
Manim
    ↓
MP4
```

M12-এ এটাকে আরও generic করব:

```text
                    Visual Plan JSON
                           ↓
                 ┌──────────────────┐
                 │ Generic Renderer │
                 └────────┬─────────┘
                          ↓
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
   Data Structure      Diagram          Equation
        ↓                 ↓                 ↓
     Manim              Manim             Manim
        └─────────────────┼─────────────────┘
                          ↓
                         MP4
```

---

# 2. কেন Generic Renderer দরকার?

ধরো তুমি Binary Search-এর জন্য লিখলে:

```python
middle = numbers[3]
```

এটা শুধু Binary Search-এর জন্য কাজ করবে।

কিন্তু আমাদের AI-এর কাছে user আসতে পারে:

```text
Explain Stack
Explain Queue
Explain Linked List
Explain Binary Tree
Explain BFS
Explain Newton's Law
Explain Photosynthesis
Explain HTTP
Explain SQL JOIN
```

প্রতিবার আলাদা Python code লিখলে project scalable হবে না।

তাই:

> **Topic-specific code নয় → reusable visual primitives তৈরি করব।**

---

# 3. Visual Primitive কী?

Visual primitive হলো ছোট ছোট reusable building block।

যেমন:

```text
Text
Circle
Rectangle
Line
Arrow
Dot
Number
Box
Node
Edge
Pointer
Array
Stack
Queue
Linked List
Tree
Graph
Chart
Equation
```

তারপর এগুলো combine করে complex animation বানাব।

---

# 4. আমাদের Renderer Architecture

```text
Visual Plan
     ↓
Plan Parser
     ↓
Primitive Factory
     ↓
Layout Engine
     ↓
Animation Engine
     ↓
Timeline Engine
     ↓
Manim
     ↓
MP4
```

আরও detailed:

```text
                    JSON
                     ↓
              ┌─────────────┐
              │   Parser    │
              └──────┬──────┘
                     ↓
              ┌─────────────┐
              │   Factory   │
              └──────┬──────┘
                     ↓
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
     Shapes        Diagrams      Structures
       ↓             ↓             ↓
     Circle        Flowchart      Array
     Square        Graph          Stack
     Text          Tree           Queue
       └─────────────┼─────────────┘
                     ↓
                Animation
                     ↓
                   Manim
```

---

# 5. M12 Folder Structure

M11-এর structure এখন update করি:

```text
educational_video_ai/
│
├── planner/
│   ├── prompt_parser.py
│   ├── objective_generator.py
│   ├── script_generator.py
│   ├── visual_planner.py
│   ├── visual_schema.py
│   └── validator.py
│
├── renderer/
│   ├── __init__.py
│   │
│   ├── objects/
│   │   ├── shapes.py
│   │   ├── text.py
│   │   ├── arrays.py
│   │   ├── stack.py
│   │   ├── queue.py
│   │   ├── linked_list.py
│   │   ├── tree.py
│   │   └── graph.py
│   │
│   ├── diagrams/
│   │   ├── flowchart.py
│   │   ├── process.py
│   │   └── comparison.py
│   │
│   ├── animations/
│   │   ├── basic.py
│   │   ├── movement.py
│   │   └── highlight.py
│   │
│   ├── layout/
│   │   ├── positions.py
│   │   └── arrange.py
│   │
│   ├── factory.py
│   ├── interpreter.py
│   └── render.py
│
├── scenes/
│   └── visual_plans/
│
├── output/
│
└── scripts/
```

এটা ভবিষ্যতে আমাদের project-এর core architecture হবে।

---

# 6. Basic Shapes

প্রথমে reusable shapes তৈরি করি।

`renderer/objects/shapes.py`

```python
from manim import *


def create_circle(radius=0.5):
    return Circle(radius=radius)


def create_square(size=1):
    return Square(side_length=size)


def create_rectangle(width=2, height=1):
    return Rectangle(
        width=width,
        height=height
    )


def create_line():
    return Line(
        LEFT,
        RIGHT
    )


def create_arrow():
    return Arrow(
        LEFT,
        RIGHT
    )
```

এখন অন্য file-এ আবার Circle-এর code লিখতে হবে না।

---

# 7. Text Primitive

`renderer/objects/text.py`

```python
from manim import *


def create_text(
    text,
    font_size=36
):

    return Text(
        text,
        font_size=font_size
    )
```

ব্যবহার:

```python
title = create_text(
    "Binary Search"
)
```

---

# 8. Position Engine

M11-এর position system আরও reusable করব।

`renderer/layout/positions.py`

```python
from manim import *


POSITIONS = {

    "center": ORIGIN,

    "top": UP * 2.5,

    "bottom": DOWN * 2.5,

    "left": LEFT * 4,

    "right": RIGHT * 4,

    "top_left": UP * 2.5 + LEFT * 4,

    "top_right": UP * 2.5 + RIGHT * 4,

    "bottom_left":
        DOWN * 2.5 + LEFT * 4,

    "bottom_right":
        DOWN * 2.5 + RIGHT * 4,
}


def get_position(name):

    return POSITIONS.get(
        name,
        ORIGIN
    )
```

---

# 9. Array Visualizer

এখন educational animation-এর জন্য একটা important primitive বানাব:

> **Array**

`renderer/objects/arrays.py`

```python
from manim import *


def create_array(
    values,
    box_size=1
):

    boxes = []

    for value in values:

        box = Square(
            side_length=box_size
        )

        label = Text(
            str(value),
            font_size=28
        )

        label.move_to(box)

        cell = VGroup(
            box,
            label
        )

        boxes.append(cell)

    array = VGroup(*boxes)

    array.arrange(
        RIGHT,
        buff=0
    )

    return array
```

এখন:

```python
array = create_array(
    [10, 20, 30, 40, 50]
)
```

Visual:

```text
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │
└────┴────┴────┴────┴────┘
```

---

# 10. Array Highlight

আমাদের array-এর specific cell highlight করতে হবে।

```python
def highlight_array_cell(
    array,
    index
):

    cell = array[index]

    return Indicate(cell)
```

ব্যবহার:

```python
self.play(
    highlight_array_cell(
        array,
        2
    )
)
```

এতে:

```text
10  20  [30]  40  50
          ↑
       highlight
```

---

# 11. Pointer

Algorithm visualization-এর জন্য pointer অত্যন্ত গুরুত্বপূর্ণ।

```python
from manim import *


def create_pointer(
    text="Pointer"
):

    arrow = Arrow(
        DOWN,
        ORIGIN
    )

    label = Text(
        text,
        font_size=24
    )

    label.next_to(
        arrow,
        DOWN
    )

    return VGroup(
        arrow,
        label
    )
```

আমরা ব্যবহার করতে পারি:

```text
       ↓
      mid
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │
└────┴────┴────┴────┘
```

---

# 12. Stack Visualizer

এখন Data Structure-এর reusable primitive।

`renderer/objects/stack.py`

```python
from manim import *


def create_stack(values):

    boxes = []

    for value in values:

        box = Rectangle(
            width=2,
            height=0.7
        )

        label = Text(
            str(value),
            font_size=28
        )

        label.move_to(box)

        cell = VGroup(
            box,
            label
        )

        boxes.append(cell)

    stack = VGroup(*boxes)

    stack.arrange(
        UP,
        buff=0
    )

    return stack
```

ব্যবহার:

```python
stack = create_stack(
    [10, 20, 30]
)
```

Visual:

```text
┌──────┐
│  30  │ ← TOP
├──────┤
│  20  │
├──────┤
│  10  │
└──────┘
```

---

# 13. Stack PUSH

ধরো:

```text
PUSH(40)
```

Visual:

```text
Before:

30
20
10


After:

40 ← new TOP
30
20
10
```

Manim-এর concept:

```python
new_item = create_stack([40])

self.play(
    FadeIn(new_item)
)
```

পরবর্তী version-এ আমরা generic action দেব:

```json
{
  "action": "push",
  "structure": "stack",
  "value": 40
}
```

Renderer নিজে বুঝবে কী করতে হবে।

---

# 14. Queue Visualizer

Queue:

```text
Front → [10] [20] [30] ← Rear
```

`renderer/objects/queue.py`

```python
from manim import *


def create_queue(values):

    boxes = []

    for value in values:

        box = Rectangle(
            width=1.5,
            height=0.8
        )

        label = Text(
            str(value),
            font_size=26
        )

        label.move_to(box)

        boxes.append(
            VGroup(box, label)
        )

    queue = VGroup(*boxes)

    queue.arrange(
        RIGHT,
        buff=0
    )

    return queue
```

---

# 15. Linked List

Linked List:

```text
┌────┐    ┌────┐    ┌────┐
│ 10 │ →  │ 20 │ →  │ 30 │
└────┘    └────┘    └────┘
```

Primitive:

```python
from manim import *


def create_linked_list(values):

    nodes = []

    for value in values:

        box = Square(
            side_length=1
        )

        label = Text(
            str(value),
            font_size=26
        )

        label.move_to(box)

        nodes.append(
            VGroup(box, label)
        )

    group = VGroup(*nodes)

    group.arrange(
        RIGHT,
        buff=1
    )

    arrows = []

    for i in range(
        len(nodes) - 1
    ):

        arrow = Arrow(
            nodes[i].get_right(),
            nodes[i + 1].get_left()
        )

        arrows.append(arrow)

    return VGroup(
        *nodes,
        *arrows
    )
```

---

# 16. Tree Visualizer

Binary Tree:

```text
             50
            /  \
          30    70
         / \    / \
       20  40  60  80
```

Tree rendering একটু বেশি complex।

প্রথম version-এ আমরা manually coordinates calculate করতে পারি।

Concept:

```python
class TreeNode:

    def __init__(
        self,
        value,
        left=None,
        right=None
    ):

        self.value = value
        self.left = left
        self.right = right
```

তারপর renderer:

```text
TreeNode
   ↓
Layout Engine
   ↓
Node + Edge
   ↓
Manim
```

এখানে M12-এর গুরুত্বপূর্ণ concept:

> **Data structure itself এবং তার visual representation আলাদা রাখা।**

---

# 17. Graph Visualizer

Graph:

```text
       A
      / \
     B   C
     |   |
     D---E
```

Graph-এর data:

```python
nodes = [
    "A",
    "B",
    "C",
    "D",
    "E"
]

edges = [
    ("A", "B"),
    ("A", "C"),
    ("B", "D"),
    ("C", "E"),
    ("D", "E")
]
```

তারপর:

```text
Graph Data
    ↓
Graph Layout
    ↓
Nodes + Edges
    ↓
Animation
```

---

# 18. Flowchart Engine

Educational videos-এ flowchart অনেক important।

Example:

```text
       START
         ↓
     Input Number
         ↓
     Number > 0 ?
       /     \
     YES      NO
      ↓        ↓
   Positive  Negative
       \      /
          ↓
         END
```

আমরা JSON-এ define করতে পারি:

```json
{
  "diagram_type": "flowchart",

  "nodes": [
    {
      "id": "start",
      "text": "START",
      "type": "start"
    },
    {
      "id": "input",
      "text": "Input Number",
      "type": "process"
    },
    {
      "id": "check",
      "text": "Number > 0?",
      "type": "decision"
    }
  ],

  "edges": [
    ["start", "input"],
    ["input", "check"]
  ]
}
```

Renderer automatically diagram তৈরি করবে।

---

# 19. Equation Renderer

Mathematics educational videos-এর জন্য:

```text
E = mc²
```

Manim:

```python
equation = MathTex(
    "E = mc^2"
)

self.play(
    Write(equation)
)
```

আরও complex:

```python
equation = MathTex(
    "a^2 + b^2 = c^2"
)
```

Visual planner বলবে:

```json
{
  "object_type": "equation",
  "content": "a^2 + b^2 = c^2"
}
```

Renderer করবে:

```python
MathTex(...)
```

---

# 20. Code Block Renderer

Programming educational videos-এর জন্য code দেখাতে হবে।

Example:

```text
for i in range(5):
    print(i)
```

Manim-এ আমরা code block render করতে পারি।

Concept:

```python
code = Code(
    code_string="""
for i in range(5):
    print(i)
""",
    language="Python"
)
```

এটা পরে আমাদের programming-video generator-এর জন্য খুব useful হবে।

---

# 21. Generic Factory

এখন সবচেয়ে important অংশ:

`renderer/factory.py`

```python
from .objects.shapes import (
    create_circle,
    create_square,
    create_rectangle
)

from .objects.text import create_text

from .objects.arrays import create_array

from .objects.stack import create_stack

from .objects.queue import create_queue


def create_visual(data):

    object_type = data["object_type"]

    if object_type == "circle":
        return create_circle()

    elif object_type == "square":
        return create_square()

    elif object_type == "rectangle":
        return create_rectangle()

    elif object_type == "text":
        return create_text(
            data["text"]
        )

    elif object_type == "array":
        return create_array(
            data["values"]
        )

    elif object_type == "stack":
        return create_stack(
            data["values"]
        )

    elif object_type == "queue":
        return create_queue(
            data["values"]
        )

    else:
        raise ValueError(
            f"Unknown object type: {object_type}"
        )
```

এটাই আমাদের **Generic Visual Factory**।

---

# 22. এখন JSON অনেক Powerful

আগে:

```json
{
  "object_type": "square"
}
```

এখন:

```json
{
  "object_type": "array",
  "values": [10, 20, 30, 40, 50]
}
```

অথবা:

```json
{
  "object_type": "stack",
  "values": [10, 20, 30]
}
```

অথবা:

```json
{
  "object_type": "queue",
  "values": [10, 20, 30]
}
```

LLM শুধু structured instruction তৈরি করবে।

---

# 23. Generic Animation Actions

আমাদের animation system-এ এখন আরও actions দরকার:

```text
show
hide
write
draw
fade_in
fade_out
move
highlight
scale
rotate
transform
replace
push
pop
enqueue
dequeue
connect
disconnect
```

এগুলো educational domain অনুযায়ী expand করা যাবে।

---

# 24. Animation Registry

একটা clean architecture:

```python
ANIMATION_REGISTRY = {
    "show": create_show_animation,
    "hide": create_hide_animation,
    "write": create_write_animation,
    "draw": create_draw_animation,
    "highlight": create_highlight_animation,
}
```

তখন আর বিশাল:

```python
if...
elif...
elif...
elif...
```

লিখতে হবে না।

Future architecture:

```python
handler = ANIMATION_REGISTRY[action]

handler(
    obj
)
```

এটা scalable design।

---

# 25. M12-এর Generic Scene JSON

এখন একটা realistic example:

```json
{
  "scene_id": 1,

  "duration": 8,

  "visual_style": "clean_2d",

  "objects": [

    {
      "name": "array",
      "object_type": "array",
      "values": [10, 20, 30, 40, 50, 60, 70],
      "position": "center"
    },

    {
      "name": "title",
      "object_type": "text",
      "text": "Binary Search",
      "position": "top"
    }
  ],

  "animations": [

    {
      "action": "show",
      "object": "title",
      "start": 0,
      "duration": 1
    },

    {
      "action": "show",
      "object": "array",
      "start": 1,
      "duration": 2
    },

    {
      "action": "highlight",
      "object": "array",
      "index": 3,
      "start": 4,
      "duration": 1
    }
  ]
}
```

এখন একই schema দিয়ে বিভিন্ন topic render করা যাবে।

---

# 26. Timeline Engine

এখন আমরা timeline-এর দিকে যাব।

ধরো:

```text
0s ───────────────────── 8s

Title       ███
Array          ██████
Highlight             ██
Pointer                  ███
```

প্রতিটি animation:

```json
{
  "start": 4,
  "duration": 2
}
```

মানে:

```text
start = 4
end = 6
```

আমরা validation করব:

```python
def validate_animation(
    animation,
    scene_duration
):

    start = animation["start"]

    duration = animation["duration"]

    end = start + duration

    if start < 0:
        raise ValueError(
            "Start cannot be negative"
        )

    if end > scene_duration:
        raise ValueError(
            "Animation exceeds scene duration"
        )
```

---

# 27. Parallel Animation

একই সময়ে:

```text
Sun appears
+
Plant appears
+
Title appears
```

তাই আমাদের renderer-কে grouping support করতে হবে।

JSON:

```json
{
  "start": 0,
  "parallel": true,
  "animations": [
    {
      "action": "show",
      "object": "sun"
    },
    {
      "action": "show",
      "object": "plant"
    },
    {
      "action": "write",
      "object": "title"
    }
  ]
}
```

Renderer:

```python
self.play(
    FadeIn(sun),
    FadeIn(plant),
    Write(title)
)
```

এটা future animation engine-এর জন্য খুব important।

---

# 28. M12-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা

আমাদের system এখন তিনটা layer-এ ভাগ হচ্ছে:

```text
LAYER 1 — DATA
    ↓
Array
Stack
Tree
Graph
Equation
Flowchart

LAYER 2 — VISUAL
    ↓
Circle
Box
Arrow
Text
Node
Edge

LAYER 3 — ANIMATION
    ↓
Show
Move
Highlight
Transform
Connect
Push
Pop
```

এতে architecture clean থাকবে।

---

# 29. Educational Example — Stack

User:

```text
Explain Stack Data Structure
```

M9:

```text
Stack is a linear data structure...
```

M10:

```text
Objects:
stack
top_pointer
value_40

Actions:
show
push
highlight
pop
```

M12 renderer:

```text
stack
 ↓
Stack Primitive
 ↓
Manim
```

Final:

```text
      40 ← TOP
      30
      20
      10
```

তারপর:

```text
POP
 ↓
40 disappears
 ↓
30 becomes TOP
```

---

# 30. Educational Example — Linked List

User:

```text
Explain Linked List
```

M10:

```text
Objects:
node_1
node_2
node_3
arrow_1
arrow_2
```

M12:

```text
LinkedList Primitive
       ↓
Node Factory
       ↓
Edge Factory
       ↓
Layout
       ↓
Animation
```

Final:

```text
10 → 20 → 30 → NULL
```

---

# 31. Educational Example — Physics

User:

```text
Explain Newton's Second Law
```

M9:

```text
F = ma
```

M10:

```text
Visual:
box
force arrow
acceleration arrow
equation
```

M12:

```text
Rectangle
+
Arrow
+
MathTex
```

Output:

```text
       Force →
    ┌─────────┐
    │  Object │
    └─────────┘

        F = ma
```

একই renderer!

---

# 32. Educational Example — Biology

User:

```text
Explain photosynthesis
```

M10:

```text
Objects:
sun
plant
water
CO2
glucose
oxygen

Actions:
show
move
transform
```

M12:

```text
Primitive objects
+
Arrows
+
Labels
+
Process diagram
```

Output:

```text
☀️
 ↓
🌱
↑   ↑
H₂O CO₂
 ↓
Glucose + O₂
```

পরবর্তীতে এগুলো Manim-এর বাইরে image/video models-এর সাথেও combine হবে।

---

# 33. M12-এর Mini Project

আজকের সবচেয়ে গুরুত্বপূর্ণ project:

## Build: Generic Educational Renderer

Input:

```json
{
  "scene_id": 1,
  "duration": 10,

  "objects": [

    {
      "name": "array",
      "object_type": "array",
      "values": [10, 20, 30, 40, 50],
      "position": "center"
    },

    {
      "name": "title",
      "object_type": "text",
      "text": "Find 30",
      "position": "top"
    }
  ],

  "animations": [

    {
      "action": "write",
      "object": "title",
      "start": 0,
      "duration": 1
    },

    {
      "action": "show",
      "object": "array",
      "start": 1,
      "duration": 2
    },

    {
      "action": "highlight",
      "object": "array",
      "index": 2,
      "start": 4,
      "duration": 1
    }
  ]
}
```

Output:

```text
        Find 30

┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │
└────┴────┴────┴────┴────┘
          ↑
       Highlight
```

এবং সবকিছু JSON থেকে generate হবে।

---

# 34. M12 Completion Test

M12 complete হয়েছে ধরে নেবে যখন তুমি নিজে:

### Test 1

```text
JSON → Circle
```

render করতে পারবে।

### Test 2

```text
JSON → Array
```

render করতে পারবে।

### Test 3

```text
JSON → Stack
```

render করতে পারবে।

### Test 4

```text
JSON → Linked List
```

render করতে পারবে।

### Test 5

```text
JSON → Flowchart
```

render করতে পারবে।

### Test 6

```text
JSON → Equation
```

render করতে পারবে।

### Test 7

একই renderer দিয়ে **Binary Search + Stack + Linked List** generate করতে পারবে।

---

# 35. M1 → M12 Progress

তোমার Educational Video AI এখন:

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
M6  Vision Model
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
M12 Generic Diagram & Animation Engine
```

এখন একটা গুরুত্বপূর্ণ milestone complete হলো:

```text
                EDUCATIONAL AI
                       │
                       ↓
                 Scene JSON
                       │
                       ↓
              Generic Renderer
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
    Algorithm        Science       Programming
       ↓               ↓               ↓
    Animation        Diagram        Code Visual
       └───────────────┼───────────────┘
                       ↓
                      MP4
```

## 🚀 Next: M13 — Advanced Timeline & Scene Composition

M13-এ আমরা এই renderer-কে আরও production-level করব:

```text
Scene 1
 ↓
Scene 2
 ↓
Scene 3
 ↓
Scene 4
 ↓
Full Video
```

এর সাথে:

* scene transition
* parallel animation
* sequential animation
* timing synchronization
* narration timing
* camera movement
* zoom/pan
* object tracking
* scene composition
* multi-scene rendering

তারপর আমরা **একটা 30–60 second educational video পুরোপুরি automatically generate** করার দিকে যাব।


---
# M13 — Advanced Timeline & Scene Composition

M12-এ আমরা **Generic Diagram & Animation Engine** বানিয়েছি।

এখন M13-এর লক্ষ্য হলো আলাদা আলাদা scene-কে **একটা complete educational video** হিসেবে compose করা।

এখন পর্যন্ত:

```text id="m13a01"
Topic
 ↓
M9 Script
 ↓
M10 Visual Plan
 ↓
M11 Animation Engine
 ↓
M12 Generic Renderer
 ↓
Individual Scene MP4
```

M13-এর পর:

```text id="m13a02"
Topic
 ↓
Script
 ↓
Visual Plan
 ↓
Scene 1 ──┐
Scene 2 ──┤
Scene 3 ──┤ → Timeline Engine → Full Video
Scene 4 ──┤
Scene 5 ──┘
```

অর্থাৎ **M13 হলো Scene → Full Video Composition Engine**।

---

# 1. M13-এ আমরা কী শিখব?

আজকের milestone-এ:

* Timeline system
* Scene duration
* Animation timing
* Sequential animation
* Parallel animation
* Scene transition
* Scene composition
* Narration synchronization
* Camera timing
* Object lifecycle
* Scene metadata
* Full-video timeline
* FFmpeg composition
* Automatic scene rendering

শিখব।

---

# 2. কেন Timeline Engine দরকার?

ধরো আমাদের video:

```text id="m13a03"
0–5 sec     Introduction
5–10 sec    Definition
10–18 sec   Example
18–25 sec   Animation
25–30 sec   Summary
```

এগুলো যদি আলাদা আলাদা থাকে:

```text id="m13a04"
scene_01.mp4
scene_02.mp4
scene_03.mp4
scene_04.mp4
scene_05.mp4
```

তাহলে final video বানাতে হবে:

```text id="m13a05"
scene_01
   +
scene_02
   +
scene_03
   +
scene_04
   +
scene_05
   ↓
final.mp4
```

এটাই M13-এর কাজ।

---

# 3. Timeline কী?

Timeline হলো পুরো video-র সময়ের map।

Example:

```text id="m13a06"
0s                                               30s
│────────────────────────────────────────────────│

│ Scene 1 │ Scene 2 │   Scene 3   │ Scene 4 │
0         5         10            20        30
```

আর scene-এর ভিতরেও timeline থাকবে।

```text id="m13a07"
Scene 3
10s ───────────────────────── 20s

10–12  Show array
12–15  Highlight middle
15–18  Move pointer
18–20  Show result
```

তাই আমাদের **দুই স্তরের timeline** থাকবে:

```text id="m13a08"
Full Video Timeline
        ↓
Scene Timeline
        ↓
Animation Timeline
```

---

# 4. Three-Level Timeline

এটা খুব গুরুত্বপূর্ণ architecture।

```text id="m13a09"
VIDEO
│
├── Scene 1
│    ├── Animation 1
│    ├── Animation 2
│    └── Animation 3
│
├── Scene 2
│    ├── Animation 1
│    └── Animation 2
│
└── Scene 3
     ├── Animation 1
     ├── Animation 2
     └── Animation 3
```

এটা আমাদের final system-এর core architecture-এর একটি অংশ হবে।

---

# 5. Scene Schema

আমরা আগে scene JSON ব্যবহার করেছি।

এখন এটাকে আরও powerful করি।

```json id="m13a10"
{
  "scene_id": 1,
  "start": 0,
  "end": 5,

  "transition": {
    "type": "fade",
    "duration": 0.5
  },

  "narration": {
    "text": "Binary search is a fast search algorithm.",
    "start": 0,
    "end": 5
  },

  "visuals": [],
  "animations": []
}
```

এখানে scene-এর:

```text
start
end
transition
narration
visuals
animations
```

সব আছে।

---

# 6. Scene Duration

Scene duration:

```python id="m13a11"
duration = end - start
```

Example:

```python id="m13a12"
start = 10
end = 18

duration = end - start

print(duration)
```

Output:

```text id="m13a13"
8
```

---

# 7. Timeline Validation

Timeline ভুল হলে video broken হতে পারে।

যেমন:

```text id="m13a14"
Scene 1
0–5

Scene 2
4–10
```

এখানে overlap:

```text id="m13a15"
Scene 1: 0──────5
Scene 2:     4────────10
             ↑
           overlap
```

আমরা এটা prevent করব।

```python id="m13a16"
def validate_scene_timing(scenes):

    previous_end = 0

    for scene in scenes:

        start = scene["start"]
        end = scene["end"]

        if start < previous_end:

            raise ValueError(
                f"Scene {scene['scene_id']} overlaps."
            )

        if end <= start:

            raise ValueError(
                f"Scene {scene['scene_id']} has invalid timing."
            )

        previous_end = end

    return True
```

---

# 8. Full Video Plan

এখন পুরো video-এর JSON:

```json id="m13a17"
{
  "video_id": "video_001",
  "title": "Binary Search",
  "duration": 30,

  "scenes": [

    {
      "scene_id": 1,
      "start": 0,
      "end": 5
    },

    {
      "scene_id": 2,
      "start": 5,
      "end": 10
    },

    {
      "scene_id": 3,
      "start": 10,
      "end": 20
    },

    {
      "scene_id": 4,
      "start": 20,
      "end": 26
    },

    {
      "scene_id": 5,
      "start": 26,
      "end": 30
    }

  ]
}
```

এটা আমাদের **Video Composition Plan**।

---

# 9. Sequential Animation

Sequential animation:

```text id="m13a18"
Animation A
     ↓
Animation B
     ↓
Animation C
```

Example:

```python id="m13a19"
self.play(
    FadeIn(circle)
)

self.play(
    Write(text)
)

self.play(
    Indicate(circle)
)
```

Timing:

```text id="m13a20"
0–1   FadeIn
1–2   Write
2–3   Highlight
```

---

# 10. Parallel Animation

Parallel মানে একই সময়ে multiple animation।

```text id="m13a21"
        ┌→ Sun appears
Start ──┼→ Plant appears
        └→ Title appears
```

Manim:

```python id="m13a22"
self.play(
    FadeIn(sun),
    FadeIn(plant),
    Write(title)
)
```

সবগুলো একই সময়ে শুরু হবে।

---

# 11. Parallel Animation JSON

```json id="m13a23"
{
  "start": 0,

  "parallel": true,

  "animations": [

    {
      "action": "fade_in",
      "object": "sun",
      "duration": 1
    },

    {
      "action": "fade_in",
      "object": "plant",
      "duration": 1
    },

    {
      "action": "write",
      "object": "title",
      "duration": 1
    }

  ]
}
```

এটা আমাদের timeline engine interpret করবে।

---

# 12. Animation Scheduler

এখন একটা scheduler তৈরি করি।

`renderer/animations/scheduler.py`

```python id="m13a24"
class AnimationScheduler:

    def __init__(self):

        self.events = []

    def add(
        self,
        start,
        duration,
        animation
    ):

        event = {
            "start": start,
            "end": start + duration,
            "animation": animation
        }

        self.events.append(event)

    def sort(self):

        self.events.sort(
            key=lambda event: event["start"]
        )

    def get_events(self):

        self.sort()

        return self.events
```

---

# 13. Scheduler Example

```python id="m13a25"
scheduler = AnimationScheduler()

scheduler.add(
    start=0,
    duration=2,
    animation="show_array"
)

scheduler.add(
    start=2,
    duration=1,
    animation="highlight_middle"
)

scheduler.add(
    start=3,
    duration=2,
    animation="move_pointer"
)
```

Timeline:

```text id="m13a26"
0────2────3────5

Show Array
      Highlight
           Move Pointer
```

---

# 14. Scene Composition

আমাদের এখন একটা Scene Composer দরকার।

`renderer/scene_composer.py`

```python id="m13a27"
class SceneComposer:

    def __init__(self):

        self.scenes = []

    def add_scene(
        self,
        scene
    ):

        self.scenes.append(scene)

    def sort_scenes(self):

        self.scenes.sort(
            key=lambda scene: scene["start"]
        )

    def get_duration(self):

        if not self.scenes:
            return 0

        self.sort_scenes()

        return max(
            scene["end"]
            for scene in self.scenes
        )
```

---

# 15. Scene Transition

Scene 1 শেষ হয়ে Scene 2 শুরু হলে transition দরকার হতে পারে।

Possible transitions:

```text id="m13a28"
cut
fade
fade_black
fade_white
slide_left
slide_right
zoom
```

### Cut

```text id="m13a29"
Scene 1
████████
        ↓
Scene 2
████████
```

কোনো transition নেই।

### Fade

```text id="m13a30"
Scene 1
███████
   ↓
 fade
   ↓
Scene 2
███████
```

---

# 16. Transition JSON

```json id="m13a31"
{
  "transition": {
    "type": "fade",
    "duration": 0.5
  }
}
```

M13-এর প্রথম version-এ সবচেয়ে সহজ:

```text
cut
fade
```

এই দুটো implement করাই যথেষ্ট।

---

# 17. Fade Transition

Manim scene-এর শেষে:

```python id="m13a32"
self.play(
    FadeOut(
        *self.mobjects
    )
)
```

অথবা scene composition level-এ FFmpeg ব্যবহার করা যায়।

এখানে গুরুত্বপূর্ণ distinction:

```text id="m13a33"
Manim
→ animation-level transition

FFmpeg
→ video-level transition
```

Final system-এ দুটোই লাগতে পারে।

---

# 18. Narration Synchronization

এখন একটা খুব important বিষয়।

ধরো narration:

```text id="m13a34"
"Binary search checks the middle element first."
```

Narration duration:

```text id="m13a35"
4.2 seconds
```

কিন্তু animation:

```text id="m13a36"
6 seconds
```

Mismatch।

```text id="m13a37"
Narration:
████████████ 4.2 sec

Animation:
██████████████████ 6 sec
```

এটা bad educational video।

তাই:

> **Narration timing এবং visual timing synchronize করতে হবে।**

---

# 19. Speech Duration Estimation

M9-এ আমরা word-based estimate শিখেছি।

```python id="m13a38"
def estimate_duration(
    text,
    wpm=140
):

    words = len(
        text.split()
    )

    return (
        words / wpm
    ) * 60
```

Example:

```python id="m13a39"
text = """
Binary search checks the middle
element first.
"""

print(
    estimate_duration(text)
)
```

এটা approximate duration দেবে।

কিন্তু final system-এ TTS তৈরি হওয়ার পরে **actual audio duration** ব্যবহার করা ভালো।

---

# 20. Actual Audio Duration

FFprobe:

```bash id="m13a40"
ffprobe \
-v error \
-show_entries format=duration \
-of default=noprint_wrappers=1 \
audio.wav
```

Python দিয়ে:

```python id="m13a41"
import subprocess


def get_audio_duration(path):

    result = subprocess.run(
        [
            "ffprobe",
            "-v",
            "error",
            "-show_entries",
            "format=duration",
            "-of",
            "default=noprint_wrappers=1:nokey=1",
            path
        ],
        capture_output=True,
        text=True
    )

    return float(
        result.stdout.strip()
    )
```

এটা পরে M20 TTS integration-এর সময় আরও important হবে।

---

# 21. Visual Timing Strategy

আমাদের rule:

```text id="m13a42"
Narration duration
       ↓
Scene duration
       ↓
Animation timing
```

Example:

```text id="m13a43"
Narration = 5.2 sec

Scene = 5.2 sec

Animation:
0–1   Show title
1–3   Show diagram
3–4   Highlight
4–5.2 Summary
```

এতে narration এবং visual synchronized থাকবে।

---

# 22. Scene Timing Automatically Generate

ধরো M9 দিয়েছে 5টি scene।

```python id="m13a44"
scenes = [
    {"duration": 4},
    {"duration": 6},
    {"duration": 7},
    {"duration": 5},
    {"duration": 3}
]
```

আমরা automatically start/end calculate করতে পারি:

```python id="m13a45"
def assign_timeline(scenes):

    current_time = 0

    for scene in scenes:

        duration = scene["duration"]

        scene["start"] = current_time

        scene["end"] = (
            current_time + duration
        )

        current_time += duration

    return scenes
```

Result:

```text id="m13a46"
Scene 1: 0–4
Scene 2: 4–10
Scene 3: 10–17
Scene 4: 17–22
Scene 5: 22–25
```

---

# 23. Full Video Duration

```python id="m13a47"
def calculate_video_duration(
    scenes
):

    if not scenes:
        return 0

    return max(
        scene["end"]
        for scene in scenes
    )
```

---

# 24. Video Composer

এখন আমরা final video composition-এর দিকে যাব।

ধরো render হয়েছে:

```text id="m13a48"
output/
├── scene_001.mp4
├── scene_002.mp4
├── scene_003.mp4
├── scene_004.mp4
└── scene_005.mp4
```

এগুলো combine করতে হবে।

---

# 25. FFmpeg Concatenation

একটি file বানাও:

```text id="m13a49"
scene_001.mp4
scene_002.mp4
scene_003.mp4
scene_004.mp4
scene_005.mp4
```

তারপর:

```bash id="m13a50"
ffmpeg \
-f concat \
-safe 0 \
-i scenes.txt \
-c copy \
output/final.mp4
```

তবে একটা condition আছে:

সব video-এর:

```text
resolution
codec
fps
audio format
```

compatible হতে হবে।

---

# 26. Better FFmpeg Composition

Production system-এ আমরা আগে সব scene normalize করব:

```bash id="m13a51"
ffmpeg \
-i scene.mp4 \
-vf "scale=1280:720,fps=30" \
-c:v libx264 \
-c:a aac \
normalized_scene.mp4
```

সব scene একই format-এ।

তারপর concatenate।

---

# 27. Video Standard

আমাদের educational video-এর একটা standard নির্ধারণ করা ভালো।

M13 থেকে:

```text id="m13a52"
Resolution: 1280 × 720
FPS: 30
Video: H.264
Audio: AAC
Container: MP4
```

Later user চাইলে:

```text
1920 × 1080
```

বা vertical:

```text
1080 × 1920
```

support করব।

---

# 28. Aspect Ratio

Educational videos বিভিন্ন platform-এর জন্য হতে পারে।

```text id="m13a53"
YouTube:
16:9

Shorts / Reels:
9:16

Instagram:
1:1
```

তাই plan-এ রাখতে পারি:

```json id="m13a54"
{
  "video_format": {
    "width": 1280,
    "height": 720,
    "fps": 30
  }
}
```

Future:

```json id="m13a55"
{
  "aspect_ratio": "9:16"
}
```

---

# 29. Scene Rendering Pipeline

এখন complete flow:

```text id="m13a56"
Scene JSON
    ↓
Plan Interpreter
    ↓
Object Factory
    ↓
Layout Engine
    ↓
Animation Scheduler
    ↓
Manim Scene
    ↓
scene_001.mp4
```

প্রতিটি scene-এর জন্য repeat হবে।

---

# 30. Full Video Pipeline

```text id="m13a57"
Video Plan
    ↓
Scene 1 JSON ──→ Render
Scene 2 JSON ──→ Render
Scene 3 JSON ──→ Render
Scene 4 JSON ──→ Render
Scene 5 JSON ──→ Render
    ↓
Normalize
    ↓
Concatenate
    ↓
Add Audio
    ↓
Add Subtitle
    ↓
Final MP4
```

এখন তুমি দেখতে পারছো M13 কেন গুরুত্বপূর্ণ।

---

# 31. Complete Video Plan Example

```json id="m13a58"
{
  "video_id": "binary_search_001",

  "title": "Binary Search",

  "duration": 30,

  "format": {
    "width": 1280,
    "height": 720,
    "fps": 30
  },

  "scenes": [

    {
      "scene_id": 1,
      "start": 0,
      "end": 5,
      "type": "definition"
    },

    {
      "scene_id": 2,
      "start": 5,
      "end": 10,
      "type": "example"
    },

    {
      "scene_id": 3,
      "start": 10,
      "end": 18,
      "type": "algorithm"
    },

    {
      "scene_id": 4,
      "start": 18,
      "end": 25,
      "type": "visual_explanation"
    },

    {
      "scene_id": 5,
      "start": 25,
      "end": 30,
      "type": "summary"
    }

  ]
}
```

---

# 32. M13-এর Core Classes

শেষ পর্যন্ত architecture এমন হতে পারে:

```text id="m13a59"
VideoComposer
      │
      ├── SceneComposer
      │
      ├── TimelineEngine
      │
      ├── AnimationScheduler
      │
      ├── TransitionManager
      │
      └── RenderManager
```

---

# 33. Timeline Engine

`renderer/timeline.py`

```python id="m13a60"
class Timeline:

    def __init__(self):

        self.events = []

    def add_event(
        self,
        start,
        duration,
        data
    ):

        self.events.append({
            "start": start,
            "end": start + duration,
            "data": data
        })

    def sort(self):

        self.events.sort(
            key=lambda x: x["start"]
        )

    def validate(self):

        self.sort()

        previous_end = 0

        for event in self.events:

            if event["start"] < previous_end:

                raise ValueError(
                    "Timeline overlap detected."
                )

            previous_end = event["end"]

        return True
```

এটা M13-এর core component।

---

# 34. Scene Manager

```python id="m13a61"
class SceneManager:

    def __init__(self):

        self.scenes = []

    def add(self, scene):

        self.scenes.append(scene)

    def sort(self):

        self.scenes.sort(
            key=lambda x: x["start"]
        )

    def validate(self):

        self.sort()

        previous_end = 0

        for scene in self.scenes:

            if scene["start"] < previous_end:

                raise ValueError(
                    "Scene overlap detected."
                )

            previous_end = scene["end"]

        return True
```

---

# 35. Full Architecture After M13

এখন আমাদের system:

```text id="m13a62"
                    USER
                      ↓
                 User Prompt
                      ↓
                     M8
              Educational Planner
                      ↓
                     M9
               Script Generator
                      ↓
                    M10
               Visual Planner
                      ↓
                    M11
             Animation Engine
                      ↓
                    M12
          Generic Visual Renderer
                      ↓
                    M13
       Timeline & Scene Composition
                      ↓
              ┌───────────────┐
              │ Scene 1       │
              │ Scene 2       │
              │ Scene 3       │
              │ Scene 4       │
              │ Scene 5       │
              └───────┬───────┘
                      ↓
               Full Video MP4
```

---

# 36. M13 Mini Project

এখন একটা complete mini project করো।

## Topic

```text
Explain Binary Search to a beginner in 30 seconds.
```

### Scene 1 — Introduction

```text
0–5 sec
```

Visual:

```text
Binary Search
```

Animation:

```text
Title appears
```

---

### Scene 2 — Sorted Array

```text
5–10 sec
```

Visual:

```text
10 20 30 40 50 60 70
```

Animation:

```text
Array appears
```

---

### Scene 3 — Middle Element

```text
10–16 sec
```

Visual:

```text
10 20 30 [40] 50 60 70
           ↑
         middle
```

Animation:

```text
Highlight 40
```

---

### Scene 4 — Remove Half

```text
16–24 sec
```

Visual:

```text
10 20 30 40 | 50 60 70
             ✕ ✕ ✕
```

Animation:

```text
Right half disappears
```

---

### Scene 5 — Summary

```text
24–30 sec
```

Visual:

```text
Binary Search
= Search half at a time
```

---

# 37. Expected Pipeline

```text id="m13a63"
prompt.json
    ↓
planner
    ↓
video_plan.json
    ↓
scene_001.json
scene_002.json
scene_003.json
scene_004.json
scene_005.json
    ↓
M11/M12 Renderer
    ↓
scene_001.mp4
scene_002.mp4
scene_003.mp4
scene_004.mp4
scene_005.mp4
    ↓
M13 Composer
    ↓
binary_search.mp4
```

---

# 38. M13 Completion Test

M13 complete হয়েছে যদি তুমি:

* [ ] Scene timing তৈরি করতে পারো
* [ ] Animation timeline তৈরি করতে পারো
* [ ] Sequential animation বুঝতে পারো
* [ ] Parallel animation বুঝতে পারো
* [ ] Scene overlap detect করতে পারো
* [ ] Scene duration calculate করতে পারো
* [ ] Narration duration estimate করতে পারো
* [ ] Scene transition concept বুঝতে পারো
* [ ] Multiple MP4 combine করতে পারো
* [ ] Standard resolution/FPS define করতে পারো
* [ ] Full video timeline তৈরি করতে পারো
* [ ] Scene 1 → Scene 2 → Scene 3 করে একটি complete MP4 বানাতে পারো

---

# 39. M1 → M13

এখন পর্যন্ত আমাদের journey:

```text id="m13a64"
M1   Python Pipeline
 ↓
M2   Video Processing
 ↓
M3   Dataset Engineering
 ↓
M4   Whisper
 ↓
M5   Computer Vision
 ↓
M6   Vision Model
 ↓
M7   Multimodal Understanding
 ↓
M8   Educational Planner
 ↓
M9   Script Generator
 ↓
M10  Visual Planner
 ↓
M11  Animation Engine
 ↓
M12  Generic Renderer
 ↓
M13  Timeline + Scene Composition
```

সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো, **M13 শেষ হলে আমাদের কাছে একটি working deterministic educational-video renderer থাকবে।**

অর্থাৎ:

```text id="m13a65"
Topic
 ↓
Scene Plan
 ↓
Visual Plan
 ↓
Animation
 ↓
Multiple Scenes
 ↓
Timeline
 ↓
FULL EDUCATIONAL VIDEO
```

## 🚀 Next: M14 — TTS + Voice/Narration Engine

M14-এ আমরা **AI-generated script-কে actual voice-এ convert** করব:

```text id="m13a66"
M9 Script
   ↓
Text Cleaning
   ↓
TTS Model
   ↓
voice.wav
   ↓
Scene Timing
   ↓
Animation Sync
```

এরপর pipeline হবে:

```text
Script
+
Visual
+
Animation
+
Voice
      ↓
Educational Video
```

এটাই আমাদের project-কে **silent animation generator থেকে actual educational video generator** বানানোর পরবর্তী বড় ধাপ।


---
# M14 — TTS + Voice / Narration Engine 🎙️

আজ আমরা তোমার **Educational Video Generation AI-এর Voice Engine** বানাবো।

M13 পর্যন্ত আমাদের pipeline ছিল:

```text
User Prompt
   ↓
Educational Planner
   ↓
Script Generator
   ↓
Visual Planner
   ↓
Animation Engine
   ↓
Scene MP4
```

এখন M14-তে যোগ হবে:

```text
Script
   ↓
Text Cleaning
   ↓
TTS Engine
   ↓
Voice WAV/MP3
   ↓
Audio Duration
   ↓
Scene Timing Sync
   ↓
Animation + Voice
```

শেষে:

```text
Script
+
Visual
+
Animation
+
Voice
      ↓
Educational Video
```

---

# 1. TTS কী?

**TTS = Text-to-Speech**

অর্থাৎ:

```text
Text
 ↓
AI Voice Model
 ↓
Human-like Speech
```

উদাহরণ:

```text
Input:
"Binary search is a fast searching algorithm."

Output:
voice.wav
```

তারপর এই `voice.wav` animation-এর সাথে যুক্ত হবে।

---

# 2. কেন TTS দরকার?

শুধু animation তৈরি করলে:

```text
🎬 Animation
```

কিন্তু educational video-তে দরকার:

```text
🎬 Animation
🎙️ Narration
📝 Subtitle
```

যেমন:

```text
0–5 sec

🎙️ "Binary search is a fast searching algorithm."

🎬 Sorted array appears.
```

এটাই আমাদের target।

---

# 3. M14 Architecture

আমাদের architecture:

```text
                 USER PROMPT
                     │
                     ▼
              Educational Planner
                     │
                     ▼
                Script JSON
                     │
                     ▼
              ┌──────────────┐
              │ Text Cleaner │
              └──────┬───────┘
                     │
                     ▼
                  TTS Model
                     │
                     ▼
                 voice.wav
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
     Audio Duration        Scene Timing
          │                     │
          └──────────┬──────────┘
                     ▼
              Timeline Engine
                     │
                     ▼
              Animation + Voice
                     │
                     ▼
              Educational Video
```

---

# 4. আমাদের TTS Engine-এর কাজ

M14 engine-এর দায়িত্ব হবে:

### Input

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Binary search is a fast search algorithm."
}
```

### Output

```text
audio/
└── scene_001.wav
```

এবং metadata:

```json
{
    "scene_id": 1,
    "audio": "audio/scene_001.wav",
    "duration": 4.2
}
```

---

# 5. TTS Model-এর ধরন

তোমার project-এর জন্য TTS broadly তিনভাবে করা যায়।

### Option 1 — Cloud TTS

```text
Your Server
   ↓
TTS API
   ↓
Audio
```

সহজ, কিন্তু API cost/Internet dependency আছে।

---

### Option 2 — Local pretrained TTS

```text
Your Computer/GPU
       ↓
Pretrained TTS
       ↓
voice.wav
```

আমাদের শেখার জন্য এটা গুরুত্বপূর্ণ।

---

### Option 3 — নিজের Voice Model Fine-tune

Advanced stage:

```text
Pretrained TTS
      +
Voice Dataset
      ↓
Fine-tuning / LoRA
      ↓
Educational Voice
```

এটা পরে করব।

**M14-তে আমরা pretrained/local TTS concept ও pipeline তৈরি করব।**

---

# 6. Project Structure

M13-এর project-এর সাথে এগুলো যোগ করো:

```text
educational_video_ai/
│
├── audio/
│   ├── raw/
│   ├── cleaned/
│   └── scenes/
│
├── tts/
│   ├── __init__.py
│   ├── engine.py
│   ├── cleaner.py
│   └── duration.py
│
├── timeline/
│   ├── scene_manager.py
│   └── sync.py
│
├── scripts/
│   └── generate_voice.py
│
├── renderer/
│
├── dataset/
│
├── videos/
│
└── requirements.txt
```

---

# 7. Text Cleaning

LLM-generated script সরাসরি TTS-তে দেওয়া ঠিক না।

কারণ script হতে পারে:

```text
**Binary Search**

Binary search is a fast algorithm...

[Pause]

Step 1:
Check the middle element.
```

TTS এগুলো ভুলভাবে পড়তে পারে।

তাই:

```text
Raw Script
    ↓
Text Cleaner
    ↓
Clean Text
    ↓
TTS
```

---

# 8. `tts/cleaner.py`

```python
import re


def clean_text(text):
    # Remove markdown bold
    text = re.sub(r"\*\*(.*?)\*\*", r"\1", text)

    # Remove markdown headings
    text = re.sub(r"#+\s*", "", text)

    # Remove brackets
    text = re.sub(r"\[(.*?)\]", r"\1", text)

    # Replace multiple spaces
    text = re.sub(r"\s+", " ", text)

    return text.strip()
```

---

# 9. এটা কী করছে?

ধরো:

```text
"**Binary Search** is a fast algorithm."
```

clean করার পরে:

```text
"Binary Search is a fast algorithm."
```

---

# 10. Test করি

```python
from tts.cleaner import clean_text


text = """
**Binary Search**

Binary search is a fast algorithm.
[Important]
"""

cleaned = clean_text(text)

print(cleaned)
```

Output:

```text
Binary Search Binary search is a fast algorithm. Important
```

---

# 11. TTS Engine

এখন আমাদের main engine:

```text
tts/engine.py
```

Concept:

```python
class TTSEngine:

    def generate(self, text, output_path):
        pass
```

আমরা implementation বদলাতে পারব কিন্তু পুরো pipeline পরিবর্তন করতে হবে না।

এটাই ভালো software architecture।

---

# 12. TTS abstraction

```python
class TTSEngine:

    def generate(self, text, output_path):
        raise NotImplementedError
```

এখন বিভিন্ন TTS model implement করা যাবে:

```text
TTSEngine
   │
   ├── LocalTTS
   ├── CloudTTS
   ├── CoquiTTS
   └── CustomTTS
```

এটা future-proof architecture।

---

# 13. Local TTS Example

একটি সহজ local TTS implementation দিয়ে শুরু করতে পারো।

```bash
pip install pyttsx3
```

তারপর:

```python
import pyttsx3


class LocalTTSEngine:

    def __init__(self):
        self.engine = pyttsx3.init()

    def generate(self, text, output_path):

        self.engine.save_to_file(
            text,
            output_path
        )

        self.engine.runAndWait()

        return output_path
```

---

# 14. ব্যবহার

```python
from tts.engine import LocalTTSEngine

tts = LocalTTSEngine()

tts.generate(
    "Binary search is a fast searching algorithm.",
    "audio/scenes/scene_001.wav"
)
```

Result:

```text
audio/
└── scenes/
    └── scene_001.wav
```

---

# 15. কিন্তু এখানে একটা সমস্যা আছে

Educational AI-এর জন্য শুধু voice generate করলেই হবে না।

আমাদের জানতে হবে:

> Voice কত seconds?

কারণ:

```text
Scene duration = 5 sec
```

কিন্তু voice যদি হয়:

```text
7.2 sec
```

তাহলে সমস্যা।

```text
Scene
0 ───────── 5 sec

Voice
0 ───────────────── 7.2 sec
```

Voice scene-এর বাইরে চলে যাবে।

---

# 16. Audio Duration

FFprobe ব্যবহার করব।

```python
import subprocess


def get_audio_duration(path):

    result = subprocess.run(
        [
            "ffprobe",
            "-v",
            "error",
            "-show_entries",
            "format=duration",
            "-of",
            "default=noprint_wrappers=1:nokey=1",
            path
        ],
        capture_output=True,
        text=True
    )

    return float(result.stdout.strip())
```

---

# 17. Test

```python
duration = get_audio_duration(
    "audio/scenes/scene_001.wav"
)

print(duration)
```

Example:

```text
4.37
```

মানে:

```text
Voice duration = 4.37 sec
```

---

# 18. Narration Timing

এখন আমাদের scene JSON:

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Binary search is a fast searching algorithm."
}
```

TTS:

```text
audio duration = 4.2 sec
```

তাহলে:

```text
Scene duration = 5 sec
Voice duration = 4.2 sec
```

Perfect।

---

# 19. কিন্তু voice বেশি হলে?

ধরো:

```text
Scene = 5 sec
Voice = 7 sec
```

আমাদের তিনটি strategy থাকতে পারে।

### Strategy 1

Scene duration বাড়ানো:

```text
5 sec → 7 sec
```

এটা educational content-এর জন্য সবচেয়ে safe।

---

### Strategy 2

Voice speed বাড়ানো:

```text
Normal
 ↓
1.1x
 ↓
1.2x
```

কিন্তু বেশি speed করলে naturalness কমে।

---

### Strategy 3

Script ছোট করা।

```text
Long narration
      ↓
LLM
      ↓
Short narration
```

আমাদের AI system-এ **Strategy 1 + Strategy 3** সবচেয়ে useful।

---

# 20. Automatic Timing System

আমরা function বানাব:

```python
def sync_scene_audio(scene, audio_duration):

    scene_duration = scene["end"] - scene["start"]

    if audio_duration > scene_duration:

        scene["end"] = (
            scene["start"] +
            audio_duration
        )

    return scene
```

---

# 21. Example

```python
scene = {
    "scene_id": 1,
    "start": 0,
    "end": 5
}

scene = sync_scene_audio(
    scene,
    7.2
)

print(scene)
```

Output:

```python
{
    "scene_id": 1,
    "start": 0,
    "end": 7.2
}
```

---

# 22. Scene Timing আরও ভালোভাবে

আমাদের Scene JSON এখন এমন হওয়া উচিত:

```json
{
    "scene_id": 1,

    "start": 0,
    "end": 5,

    "narration": {
        "text": "Binary search is a fast searching algorithm.",
        "audio": "audio/scenes/scene_001.wav",
        "duration": 4.2
    },

    "visuals": [],
    "animations": []
}
```

এখন scene-এর সব information এক জায়গায়।

---

# 23. M14-এর গুরুত্বপূর্ণ concept: Audio-driven timing

আগে:

```text
LLM decides:
Scene = 5 sec
```

তারপর:

```text
TTS = 6.4 sec
```

তাহলে mismatch।

Better architecture:

```text
LLM
 ↓
Narration
 ↓
TTS
 ↓
Actual Audio Duration
 ↓
Timeline
 ↓
Animation Timing
```

অর্থাৎ **actual audio duration becomes an important timing signal**।

---

# 24. Word Count → Estimated Duration

TTS generate করার আগেও আমরা estimate করতে পারি।

আগে M9-এ আমরা ব্যবহার করেছি:

```python
def estimate_duration(text, wpm=140):

    words = len(text.split())

    return (words / wpm) * 60
```

Example:

```text
70 words
```

At 140 WPM:

```text
70 / 140 × 60
= 30 sec
```

---

# 25. Scene Planning-এ এটা ব্যবহার করব

```text
Scene narration
       ↓
Word Count
       ↓
Estimated Duration
       ↓
Scene Duration
       ↓
TTS
       ↓
Actual Duration
       ↓
Correction
```

এটা অনেক বেশি robust।

---

# 26. Voice Selection

Future system-এ user দিতে পারবে:

```json
{
    "voice": "male",
    "language": "en",
    "speed": 1.0,
    "pitch": 1.0
}
```

অথবা:

```json
{
    "voice": "female",
    "language": "en",
    "speed": 0.95,
    "style": "teacher"
}
```

---

# 27. Educational Voice Styles

তোমার AI-তে voice style গুরুত্বপূর্ণ।

আমরা রাখতে পারি:

```text
teacher
friendly_teacher
professional
storyteller
energetic
calm
scientific
```

Example:

```text
Topic: Photosynthesis

Style: Friendly Teacher
```

Narration:

> "Think of a plant as a tiny solar-powered factory."

অন্যদিকে:

```text
Style: Scientific
```

হলে narration বেশি technical হবে।

---

# 28. Voice + Visual Synchronization

এটাই M14-এর সবচেয়ে important অংশ।

ধরো narration:

```text
"First, we find the middle element."
```

Timeline:

```text
0 sec
 │
 │ "First"
 │
 ▼
1 sec → array appears

2 sec → middle highlighted

3 sec → explanation

5 sec → next scene
```

অর্থাৎ narration-এর শব্দ/phrase-এর সাথে animation event synchronize করা যায়।

---

# 29. Advanced Narration Timeline

আমরা পরে এমন JSON তৈরি করতে পারি:

```json
{
    "narration": {
        "text": "First, we find the middle element.",
        "duration": 4.5
    },

    "animation_events": [
        {
            "time": 0.0,
            "action": "show",
            "object": "array"
        },
        {
            "time": 1.2,
            "action": "highlight",
            "object": "middle"
        }
    ]
}
```

তখন:

```text
Voice starts
     ↓
0.0s array
     ↓
1.2s middle highlight
     ↓
4.5s narration ends
```

এটাই আমাদের future **Audio-Visual Alignment Engine**।

---

# 30. Complete M14 Pipeline

এখন পুরো flow:

```text
User Prompt
     ↓
M8 Planner
     ↓
M9 Script
     ↓
M10 Visual Plan
     ↓
M11/M12 Animation
     ↓
M14 TTS
     ↓
Audio Duration
     ↓
Timeline Sync
     ↓
Scene Composition
     ↓
FFmpeg
     ↓
Educational MP4
```

---

# 31. Complete Example

Input:

```text
Explain binary search to a beginner in 20 seconds.
```

LLM output:

```json
{
    "topic": "Binary Search",
    "duration": 20,
    "scenes": [
        {
            "scene_id": 1,
            "narration": "Binary search is a fast way to find an item in a sorted list."
        },
        {
            "scene_id": 2,
            "narration": "We check the middle element first."
        },
        {
            "scene_id": 3,
            "narration": "If the target is smaller, we ignore the right half."
        },
        {
            "scene_id": 4,
            "narration": "This lets us search much faster than checking every item."
        }
    ]
}
```

TTS:

```text
scene_001.wav
scene_002.wav
scene_003.wav
scene_004.wav
```

Then:

```text
Scene 1
Animation + scene_001.wav

Scene 2
Animation + scene_002.wav

Scene 3
Animation + scene_003.wav

Scene 4
Animation + scene_004.wav
```

Finally:

```text
scene 1
   ↓
scene 2
   ↓
scene 3
   ↓
scene 4
   ↓
FINAL.mp4
```

---

# 32. M14 Folder Architecture

শেষে তোমার project-এর relevant অংশ:

```text
educational_video_ai/
│
├── audio/
│   ├── raw/
│   ├── cleaned/
│   └── scenes/
│
├── tts/
│   ├── __init__.py
│   ├── engine.py
│   ├── cleaner.py
│   └── duration.py
│
├── timeline/
│   ├── scene_manager.py
│   ├── scheduler.py
│   └── sync.py
│
├── renderer/
│   ├── objects/
│   ├── animations/
│   ├── layout/
│   └── render.py
│
├── scripts/
│   ├── generate_script.py
│   ├── generate_voice.py
│   └── render_video.py
│
├── dataset/
│
├── videos/
│
└── requirements.txt
```

---

# 33. M14 Mini Project 🎯

আজকের mini project:

## **Text → Voice → Duration**

একটা program বানাও:

```text
input:
"Binary search is a fast searching algorithm."
```

Program করবে:

```text
1. Clean text
2. Generate voice
3. Save WAV
4. Calculate duration
5. Print duration
```

Expected:

```text
Original text:
Binary search is a fast searching algorithm.

Clean text:
Binary search is a fast searching algorithm.

Audio:
audio/scenes/scene_001.wav

Duration:
3.8 seconds
```

---

# 34. তারপর Scene JSON-এর সাথে যুক্ত করো

Input:

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,
    "narration": "Binary search is a fast searching algorithm."
}
```

Output:

```json
{
    "scene_id": 1,
    "start": 0,
    "end": 5,

    "narration": {
        "text": "Binary search is a fast searching algorithm.",
        "audio": "audio/scenes/scene_001.wav",
        "duration": 3.8
    }
}
```

এটা করতে পারলে **M14-এর core concept complete**।

---

# 35. Common Errors

### Error 1 — `ffprobe not found`

```bash
sudo apt install ffmpeg
```

---

### Error 2 — TTS audio তৈরি হচ্ছে না

Check:

```bash
ls audio/scenes/
```

এবং:

```bash
ffprobe audio/scenes/scene_001.wav
```

---

### Error 3 — Voice scene-এর চেয়ে বড়

সমাধান:

```text
Actual audio duration
        ↓
Update scene duration
```

---

### Error 4 — Narration খুব দ্রুত

WPM কমাও:

```python
estimate_duration(text, wpm=130)
```

---

### Error 5 — Narration খুব ধীর

WPM বাড়াতে পারো:

```python
estimate_duration(text, wpm=150)
```

তবে final timing অবশ্যই **actual generated audio duration** দিয়ে যাচাই করবে।

---

# 36. M14 Completion Checklist

নিজেকে পরীক্ষা করো:

* [ ] TTS কী বুঝি
* [ ] Text cleaning করতে পারি
* [ ] TTS abstraction বুঝি
* [ ] Text থেকে audio generate করতে পারি
* [ ] WAV/MP3 output বুঝি
* [ ] FFprobe দিয়ে audio duration বের করতে পারি
* [ ] WPM থেকে duration estimate করতে পারি
* [ ] Scene-এর সাথে audio যুক্ত করতে পারি
* [ ] Audio বেশি হলে scene timing adjust করতে পারি
* [ ] Voice style concept বুঝি
* [ ] Audio-visual synchronization বুঝি
* [ ] Scene JSON-এ audio metadata রাখতে পারি

---

# 🚀 M14-এর পরে আমাদের অবস্থান

এখন system অনেক শক্তিশালী:

```text
                EDUCATIONAL AI
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
        SCRIPT                VISUAL
          │                     │
          ▼                     ▼
         TTS                 MANIM
          │                     │
          ▼                     ▼
       VOICE.wav             Scene.mp4
          │                     │
          └──────────┬──────────┘
                     ▼
                TIMELINE
                     │
                     ▼
                  FFmpeg
                     │
                     ▼
              🎬 FINAL VIDEO
```

**পরবর্তী milestone হবে M15 — Subtitle / Caption + Audio-Visual Synchronization Engine.**

সেখানে আমরা করব:

```text
Voice
 ↓
Word/Segment Timestamp
 ↓
Subtitle Generation
 ↓
SRT / ASS
 ↓
Animated Captions
 ↓
Voice + Animation + Subtitle
 ↓
Final Educational Video
```

এবং এরপর ধীরে ধীরে তোমার system-কে **real AI-generated educational video generator**-এর দিকে নিয়ে যাব।



----
# M15 — Subtitle / Caption + Audio-Visual Synchronization Engine 🎬📝🎙️

M14-তে আমরা **Text → TTS → Voice** তৈরি করেছি।
এখন M15-তে সেই voice-এর সাথে **subtitle এবং animation synchronize** করব।

এটা তোমার Educational Video AI-এর জন্য খুব গুরুত্বপূর্ণ milestone।

---

# 1. M15-এ আমরা কী বানাব?

ধরো user prompt:

```text
Explain binary search to a beginner in 20 seconds.
```

আমাদের system তৈরি করেছে:

```text
Script
   ↓
TTS
   ↓
voice.wav
```

এখন M15:

```text
voice.wav
   ↓
Speech Recognition / Timestamp
   ↓
Word / Segment timestamps
   ↓
Subtitle
   ↓
SRT / ASS
   ↓
Animated Caption
```

Final:

```text
Animation
    +
Voice
    +
Subtitle
    ↓
Educational Video
```

---

# 2. কেন Subtitle দরকার?

Educational video-তে subtitle অনেক useful।

একজন learner:

* শুনতে পারে
* পড়তে পারে
* গুরুত্বপূর্ণ শব্দ দেখতে পারে
* technical term বুঝতে পারে

যেমন:

```text
🎙️ Voice:

"Binary search checks the middle element first."

📝 Screen:

Binary Search

"checks the middle element first"
```

---

# 3. M15 Architecture

পুরো architecture:

```text
                  Script
                    │
                    ▼
                  TTS
                    │
                    ▼
                voice.wav
                    │
                    ▼
             Speech Recognition
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
     Segment Time          Word Time
          │                   │
          └─────────┬─────────┘
                    ▼
             Subtitle Engine
                    │
             ┌──────┴──────┐
             ▼             ▼
            SRT           ASS
             │             │
             └──────┬──────┘
                    ▼
             Caption Renderer
                    │
                    ▼
          Animation + Voice + Text
                    │
                    ▼
                FINAL.mp4
```

---

# 4. Subtitle-এর দুই ধরনের timing

এখানে একটা important concept আছে।

### Segment-level timestamp

```text
0.0 → 3.5
"Binary search is fast."
```

### Word-level timestamp

```text
0.0 → 0.5   Binary
0.5 → 0.9   search
0.9 → 1.1   is
1.1 → 1.5   fast
```

Word-level timing ব্যবহার করলে আমরা **karaoke-style captions** বা word-highlight animation করতে পারব।

---

# 5. M4-তে আমরা Word Timestamp already দেখেছি

Whisper:

```python
segments, info = model.transcribe(
    video_path,
    beam_size=5,
    word_timestamps=True
)
```

এখন M15-এ একই concept ব্যবহার করব।

Pipeline:

```text
voice.wav
   ↓
Whisper
   ↓
words + timestamps
```

---

# 6. কেন TTS audio আবার Whisper-এ পাঠাব?

খুব ভালো প্রশ্ন।

আমাদের কাছে original script আছে:

```text
"Binary search checks the middle element first."
```

কিন্তু আমরা চাই actual audio timing:

```text
Binary       0.00 → 0.42
search       0.42 → 0.86
checks       0.86 → 1.24
the          1.24 → 1.35
middle       1.35 → 1.82
element      1.82 → 2.30
first        2.30 → 2.72
```

TTS-এর actual speaking speed থেকে timestamp পাওয়া যায়।

তাই:

```text
TTS
 ↓
voice.wav
 ↓
Whisper
 ↓
actual timestamps
```

এটা practical এবং robust approach।

---

# 7. Installation

আমাদের M4-এর মতো:

```bash
source .venv/bin/activate
```

যদি আগে install না করে থাকো:

```bash
pip install faster-whisper
```

FFmpeg:

```bash
sudo apt update
sudo apt install ffmpeg
```

Check:

```bash
ffmpeg -version
```

---

# 8. Audio থেকে Word Timestamp

File:

```text
subtitle/transcribe.py
```

Code:

```python
from faster_whisper import WhisperModel


class AudioTranscriber:

    def __init__(
        self,
        model_size="base",
        device="cpu",
        compute_type="int8"
    ):

        self.model = WhisperModel(
            model_size,
            device=device,
            compute_type=compute_type
        )

    def transcribe(self, audio_path):

        segments, info = self.model.transcribe(
            audio_path,
            beam_size=5,
            word_timestamps=True
        )

        results = []

        for segment in segments:

            words = []

            if segment.words:

                for word in segment.words:

                    words.append({
                        "word": word.word.strip(),
                        "start": word.start,
                        "end": word.end
                    })

            results.append({
                "start": segment.start,
                "end": segment.end,
                "text": segment.text.strip(),
                "words": words
            })

        return results
```

---

# 9. Code বুঝি

এই অংশ:

```python
WhisperModel(
    model_size,
    device=device,
    compute_type=compute_type
)
```

Whisper model load করে।

আমাদের CPU machine হলে:

```python
device="cpu"
compute_type="int8"
```

GPU থাকলে পরে:

```python
device="cuda"
compute_type="float16"
```

ব্যবহার করতে পারি।

---

# 10. `word_timestamps=True`

এই line খুব important:

```python
word_timestamps=True
```

এটা না দিলে:

```text
Segment:
0 → 3 sec
"Binary search is fast."
```

পাব।

কিন্তু দিলে:

```text
Binary → 0.0–0.5
search → 0.5–0.9
is     → 0.9–1.0
fast   → 1.0–1.5
```

এরকম information পাওয়া যায়।

---

# 11. Example Output

ধরো audio:

```text
scene_001.wav
```

Output:

```json
{
    "start": 0.0,
    "end": 3.2,
    "text": "Binary search is fast.",
    "words": [
        {
            "word": "Binary",
            "start": 0.0,
            "end": 0.55
        },
        {
            "word": "search",
            "start": 0.55,
            "end": 1.05
        },
        {
            "word": "is",
            "start": 1.05,
            "end": 1.25
        },
        {
            "word": "fast",
            "start": 1.25,
            "end": 1.75
        }
    ]
}
```

এটাই আমাদের subtitle-এর raw data।

---

# 12. Subtitle Data Model

আমি recommend করব:

```text
subtitle/
├── transcribe.py
├── models.py
├── srt.py
├── ass.py
├── formatter.py
└── renderer.py
```

---

# 13. Subtitle Model

`subtitle/models.py`

```python
from dataclasses import dataclass
from typing import List


@dataclass
class WordTimestamp:

    word: str
    start: float
    end: float


@dataclass
class SubtitleSegment:

    start: float
    end: float
    text: str
    words: List[WordTimestamp]
```

---

# 14. কেন Dataclass?

কারণ raw dictionary:

```python
{
    "word": "Binary",
    "start": 0.0,
    "end": 0.5
}
```

এর বদলে:

```python
WordTimestamp(
    word="Binary",
    start=0.0,
    end=0.5
)
```

structured data পাওয়া যায়।

Large project-এ এটা maintain করা সহজ।

---

# 15. SRT কী?

SRT হলো standard subtitle format।

Example:

```text
1
00:00:00,000 --> 00:00:02,500
Binary search is a fast algorithm.

2
00:00:02,500 --> 00:00:05,000
It works on sorted data.
```

File:

```text
scene_001.srt
```

---

# 16. Seconds → SRT Time

আমাদের timestamp:

```text
3.52 seconds
```

SRT format:

```text
00:00:03,520
```

Function:

```python
def format_srt_time(seconds):

    hours = int(seconds // 3600)

    minutes = int(
        (seconds % 3600) // 60
    )

    secs = int(seconds % 60)

    milliseconds = int(
        (seconds - int(seconds)) * 1000
    )

    return (
        f"{hours:02d}:"
        f"{minutes:02d}:"
        f"{secs:02d},"
        f"{milliseconds:03d}"
    )
```

---

# 17. SRT Generator

`subtitle/srt.py`

```python
def format_srt_time(seconds):

    hours = int(seconds // 3600)

    minutes = int(
        (seconds % 3600) // 60
    )

    secs = int(seconds % 60)

    milliseconds = int(
        (seconds - int(seconds)) * 1000
    )

    return (
        f"{hours:02d}:"
        f"{minutes:02d}:"
        f"{secs:02d},"
        f"{milliseconds:03d}"
    )


def generate_srt(segments, output_path):

    lines = []

    for index, segment in enumerate(
        segments,
        start=1
    ):

        start = format_srt_time(
            segment["start"]
        )

        end = format_srt_time(
            segment["end"]
        )

        text = segment["text"]

        lines.append(
            str(index)
        )

        lines.append(
            f"{start} --> {end}"
        )

        lines.append(text)

        lines.append("")

    with open(
        output_path,
        "w",
        encoding="utf-8"
    ) as file:

        file.write(
            "\n".join(lines)
        )
```

---

# 18. Generate SRT

```python
from subtitle.transcribe import AudioTranscriber
from subtitle.srt import generate_srt


transcriber = AudioTranscriber()

segments = transcriber.transcribe(
    "audio/scenes/scene_001.wav"
)

generate_srt(
    segments,
    "audio/scenes/scene_001.srt"
)
```

Result:

```text
audio/
└── scenes/
    ├── scene_001.wav
    └── scene_001.srt
```

---

# 19. SRT File দেখতে এমন হবে

```text
1
00:00:00,000 --> 00:00:03,200
Binary search is a fast searching algorithm.

2
00:00:03,200 --> 00:00:05,100
It works on sorted data.
```

এখন subtitle ready।

---

# 20. Scene Subtitle বনাম Full Video Subtitle

এখানে একটা important architecture decision।

আমাদের কাছে:

```text
Scene 1
0 → 5

Scene 2
5 → 10

Scene 3
10 → 15
```

প্রতিটি scene-এর subtitle timestamp শুরু হবে:

```text
Scene 1:
0 → 5

Scene 2:
0 → 5

Scene 3:
0 → 5
```

কিন্তু final video-তে দরকার:

```text
Scene 1:
0 → 5

Scene 2:
5 → 10

Scene 3:
10 → 15
```

তাই **global timestamp offset** দরকার।

---

# 21. Offset কী?

ধরো Scene 2 শুরু হয়েছে:

```text
global_start = 5
```

তার local subtitle:

```text
0.0 → 2.0
```

Global subtitle হবে:

```text
5.0 → 7.0
```

Formula:

```text
global_time =
scene_start + local_time
```

---

# 22. Python Implementation

```python
def apply_scene_offset(
    segments,
    scene_start
):

    updated = []

    for segment in segments:

        new_segment = {
            **segment,
            "start": (
                segment["start"]
                + scene_start
            ),
            "end": (
                segment["end"]
                + scene_start
            )
        }

        updated.append(new_segment)

    return updated
```

---

# 23. Example

Input:

```python
segments = [
    {
        "start": 0,
        "end": 2,
        "text": "Check the middle element."
    }
]
```

Scene starts:

```python
scene_start = 5
```

Output:

```text
5 → 7
```

এটা final timeline-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 24. Word-level Captions

এখন আমরা আরও advanced level-এ যাব।

Segment:

```text
"Check the middle element."
```

Words:

```text
Check
the
middle
element
```

আমরা প্রতি word highlight করতে পারি।

Timeline:

```text
0.0       Check
0.5       the
0.7       middle
1.3       element
```

Visual:

```text
Check the middle element
^^^^^
```

তারপর:

```text
Check the middle element
      ^^^
```

তারপর:

```text
Check the middle element
          ^^^^^^
```

এটা **Karaoke Caption**।

---

# 25. কেন Educational AI-তে এটা powerful?

Algorithm video:

```text
"First, check the middle element."
```

Caption:

```text
First, check the middle element.
       ^^^^^
```

সাথে animation:

```text
Array:
[10] [20] [30] [40] [50]
             ↑
          middle
```

তিনটি signal একসাথে:

```text
🎙️ Voice
📝 Word Highlight
🎬 Animation
```

Learner-এর understanding অনেক বেশি clear হয়।

---

# 26. Caption Chunking

প্রতি word আলাদা subtitle দিলে screen clutter হতে পারে।

Bad:

```text
Binary
search
is
a
fast
algorithm
```

Better:

```text
Binary search
is a fast algorithm.
```

তাই আমরা **caption chunking** করব।

---

# 27. Chunking Strategy

ধরো:

```text
Binary search is a fast way to find an item.
```

আমরা বানাতে পারি:

```text
Chunk 1:
Binary search

Chunk 2:
is a fast way

Chunk 3:
to find an item
```

Rules:

```text
MAX_WORDS = 5
MAX_DURATION = 3 sec
```

---

# 28. Chunk Function

```python
def create_caption_chunks(
    words,
    max_words=5,
    max_duration=3.0
):

    chunks = []

    current = []

    for word in words:

        current.append(word)

        start = current[0]["start"]
        end = current[-1]["end"]

        duration = end - start

        if (
            len(current) >= max_words
            or duration >= max_duration
        ):

            chunks.append({
                "start": start,
                "end": end,
                "text": " ".join(
                    w["word"]
                    for w in current
                )
            })

            current = []

    if current:

        chunks.append({
            "start": current[0]["start"],
            "end": current[-1]["end"],
            "text": " ".join(
                w["word"]
                for w in current
            )
        })

    return chunks
```

---

# 29. Important Problem: Bad Whisper Words

Whisper কখনো punctuation বা spacing imperfect করতে পারে।

যেমন:

```text
"middle element."
```

কখনো output হতে পারে:

```text
" middle"
```

তাই:

```python
word.word.strip()
```

ব্যবহার করা ভালো।

---

# 30. Subtitle Style

Educational video-তে subtitle শুধু plain white text না।

আমরা style system রাখতে পারি:

```json
{
    "caption_style": {
        "font": "DejaVu Sans",
        "size": 36,
        "position": "bottom",
        "max_lines": 2,
        "highlight_word": true
    }
}
```

Future:

```text
font
size
position
background
stroke
highlight
animation
```

সব user/config controlled হতে পারে।

---

# 31. ASS Subtitle

SRT simple।

কিন্তু advanced styling-এর জন্য **ASS** বেশি powerful।

ASS support করে:

* font
* size
* position
* color
* outline
* shadow
* animation
* karaoke timing

তাই আমাদের architecture:

```text
Basic:
SRT

Advanced:
ASS
```

---

# 32. SRT vs ASS

| Feature              | SRT     | ASS       |
| -------------------- | ------- | --------- |
| Basic subtitle       | ✅       | ✅         |
| Font control         | Limited | ✅         |
| Position             | Limited | ✅         |
| Outline              | ❌       | ✅         |
| Karaoke              | ❌       | ✅         |
| Advanced animation   | ❌       | ✅         |
| Educational captions | Good    | Excellent |

আমাদের final system-এ **ASS support রাখা উচিত**।

---

# 33. FFmpeg দিয়ে Subtitle Burn

ধরো:

```text
video.mp4
subtitle.srt
```

Command:

```bash
ffmpeg \
-i video.mp4 \
-vf "subtitles=subtitle.srt" \
-c:a copy \
output/subtitled.mp4
```

এতে subtitle video-র ভিতরে permanently render হবে।

---

# 34. কিন্তু আমাদের project-এ ASS বেশি useful

```bash
ffmpeg \
-i video.mp4 \
-vf "ass=subtitle.ass" \
-c:a copy \
output/final.mp4
```

এখানে subtitle-এর style control করা যায়।

---

# 35. Audio + Video + Subtitle

এখন final composition:

```text
Scene Animation
       +
Voice
       +
Subtitle
       ↓
Scene Video
```

FFmpeg:

```bash
ffmpeg \
-i scene.mp4 \
-i voice.wav \
-map 0:v \
-map 1:a \
-c:v libx264 \
-c:a aac \
-shortest \
scene_final.mp4
```

---

# 36. `-shortest` কেন?

যদি:

```text
Video = 5 sec
Audio = 5.5 sec
```

তাহলে output যেন অস্বাভাবিকভাবে বাড়তে না থাকে।

```text
-shortest
```

shortest stream অনুযায়ী stop করতে সাহায্য করে।

তবে আমাদের timeline engine-এর দায়িত্ব হবে আগে থেকেই timing ঠিক করা।

---

# 37. Full Scene Pipeline

এখন Scene 1:

```text
Narration
    ↓
TTS
    ↓
scene_001.wav
    ↓
Whisper
    ↓
word timestamps
    ↓
caption chunks
    ↓
scene_001.srt / .ass
    ↓
Manim animation
    ↓
animation.mp4
    ↓
FFmpeg
    ↓
scene_001_final.mp4
```

---

# 38. Full Video Pipeline

সব scene:

```text
Scene 1
Animation + Voice + Caption
       ↓
Scene 1 MP4

Scene 2
Animation + Voice + Caption
       ↓
Scene 2 MP4

Scene 3
Animation + Voice + Caption
       ↓
Scene 3 MP4

       ↓

Timeline Composer

       ↓

FINAL EDUCATIONAL VIDEO
```

---

# 39. M15 Final JSON

এখন আমাদের Scene JSON আরও powerful হবে:

```json
{
    "scene_id": 2,

    "start": 5.0,
    "end": 10.0,

    "narration": {
        "text": "We check the middle element first.",
        "audio": "audio/scenes/scene_002.wav",
        "duration": 4.6
    },

    "subtitle": {
        "srt": "audio/scenes/scene_002.srt",
        "ass": "audio/scenes/scene_002.ass"
    },

    "visuals": [
        {
            "object": "array",
            "action": "show"
        }
    ],

    "animations": [
        {
            "start": 1.0,
            "action": "highlight",
            "object": "middle_element"
        }
    ]
}
```

এখন একটি scene-এর মধ্যে সব information আছে।

---

# 40. M15-এর সবচেয়ে গুরুত্বপূর্ণ Architecture

এখন আমাদের system:

```text
                 SCENE JSON
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
     Narration     Visual       Timing
        │            │            │
        ▼            ▼            │
       TTS         Manim         │
        │            │            │
        ▼            ▼            │
     voice.wav    scene.mp4       │
        │                         │
        ▼                         │
     Whisper                      │
        │                         │
        ▼                         │
   Word Timestamp                 │
        │                         │
        ▼                         │
    Subtitle                      │
        │                         │
        └──────────┬──────────────┘
                   ▼
             Sync Engine
                   │
                   ▼
             FFmpeg Composer
                   │
                   ▼
              FINAL VIDEO
```

---

# 41. Audio-Visual Synchronization Engine

এখন আমাদের আলাদা module করা উচিত:

```text
sync/
├── audio_sync.py
├── subtitle_sync.py
├── animation_sync.py
└── timeline_sync.py
```

---

# 42. Synchronization-এর তিন স্তর

### Level 1 — Scene Sync

```text
Scene
 ├── Audio
 ├── Visual
 └── Subtitle
```

সব একই duration-এর মধ্যে।

---

### Level 2 — Sentence Sync

```text
Sentence
 ↓
Animation Event
```

যেমন:

```text
"First, check the middle element."

0 sec → show array
1 sec → highlight middle
```

---

### Level 3 — Word Sync

```text
Word timestamp
       ↓
Highlight animation
```

যেমন:

```text
"middle"
   ↓
middle element highlight
```

এটাই advanced educational video generation-এর foundation।

---

# 43. M15 Mini Project 🎯

এখন তোমার project:

## **Voice → Word Timestamp → SRT → Subtitle Video**

Input:

```text
audio/scenes/scene_001.wav
```

Pipeline:

```text
voice.wav
 ↓
Whisper
 ↓
word timestamps
 ↓
SRT
 ↓
animation.mp4
 ↓
FFmpeg
 ↓
subtitle_video.mp4
```

---

# 44. Mini Project Step 1

Voice তৈরি করো:

```text
audio/scenes/scene_001.wav
```

Narration:

```text
Binary search is a fast way to find an item in a sorted list.
```

---

# 45. Step 2 — Transcribe

```python
from subtitle.transcribe import AudioTranscriber

transcriber = AudioTranscriber()

segments = transcriber.transcribe(
    "audio/scenes/scene_001.wav"
)

for segment in segments:

    print(segment["text"])

    for word in segment["words"]:
        print(
            word["word"],
            word["start"],
            word["end"]
        )
```

---

# 46. Step 3 — Generate SRT

```python
from subtitle.srt import generate_srt

generate_srt(
    segments,
    "audio/scenes/scene_001.srt"
)
```

---

# 47. Step 4 — Check Subtitle

Terminal:

```bash
cat audio/scenes/scene_001.srt
```

Expected:

```text
1
00:00:00,000 --> 00:00:04,000
Binary search is a fast way to find an item in a sorted list.
```

---

# 48. Step 5 — Add to Video

```bash
ffmpeg \
-i scene_001.mp4 \
-vf "subtitles=audio/scenes/scene_001.srt" \
-c:a copy \
output/scene_001_caption.mp4
```

---

# 49. Final Result

তুমি দেখতে পাবে:

```text
┌──────────────────────────────────┐
│                                  │
│       [10] [20] [30] [40] [50]   │
│                    ↑             │
│                 MIDDLE           │
│                                  │
│                                  │
│ Binary search is a fast way...   │
└──────────────────────────────────┘
              🎙️
```

এটাই M15-এর basic output।

---

# 50. Advanced Version

Basic subtitle-এর পরে:

```text
Voice
 ↓
Word timestamps
 ↓
Caption chunk
 ↓
Current word detection
 ↓
Highlight current word
 ↓
Animation event
```

Example:

```text
Voice:
"Check the middle element."

Caption:

Check the middle element.
^^^^^

then

Check the middle element.
          ^^^^^^

Animation:

[10] [20] [30] [40] [50]
          ↑
       highlight
```

এটা তোমার Educational AI-কে সাধারণ text-to-video system থেকে আলাদা করবে।

---

# 51. M15 Common Errors

### Error 1 — Whisper খুব slow

CPU-তে:

```python
model_size="tiny"
```

দিয়ে শুরু করতে পারো।

তারপর:

```text
tiny
 ↓
base
 ↓
small
```

Quality বনাম speed tradeoff বুঝবে।

---

### Error 2 — Word timestamp পাওয়া যাচ্ছে না

Check:

```python
word_timestamps=True
```

---

### Error 3 — Subtitle delay

সমাধান:

```text
Global time
=
Scene start
+
Local subtitle time
```

---

### Error 4 — Subtitle screen-এর বাইরে

Caption position/style ঠিক করতে হবে।

ASS ব্যবহার করলে অনেক বেশি control পাবে।

---

### Error 5 — Audio এবং animation mismatch

প্রথমে:

```text
actual audio duration
```

calculate করো।

তারপর timeline adjust করো।

---

# 52. M15 Completion Checklist

নিজেকে test করো:

* [ ] Subtitle কী বুঝি
* [ ] Segment timestamp বুঝি
* [ ] Word timestamp বুঝি
* [ ] Whisper দিয়ে audio transcribe করতে পারি
* [ ] SRT generate করতে পারি
* [ ] Seconds → SRT time conversion বুঝি
* [ ] Scene local timestamp বুঝি
* [ ] Global timestamp বুঝি
* [ ] Scene offset apply করতে পারি
* [ ] Caption chunking বুঝি
* [ ] SRT বনাম ASS বুঝি
* [ ] FFmpeg দিয়ে subtitle burn করতে পারি
* [ ] Voice + animation + subtitle combine করতে পারি
* [ ] Audio-visual synchronization বুঝি
* [ ] Word-level highlighting-এর concept বুঝি

---

# 🧠 এখন পর্যন্ত তোমার AI System

M1 → M15 পর্যন্ত আমরা আসলে একটা বড় foundation তৈরি করেছি:

```text
M1  → Python Pipeline
M2  → Video Processing
M3  → Dataset Engineering
M4  → Whisper / Speech
M5  → Computer Vision
M6  → Pretrained Vision Models
M7  → Multimodal Understanding
M8  → Educational Planner
M9  → Script Generator
M10 → Visual Planner
M11 → Animation Engine
M12 → Generic Diagram Engine
M13 → Timeline Engine
M14 → TTS / Voice Engine
M15 → Subtitle + Synchronization
```

এখন architecture দাঁড়াচ্ছে:

```text
                     USER
                      │
                      ▼
               EDUCATIONAL AI
                      │
                      ▼
              ┌───────────────┐
              │  LLM PLANNER  │
              └───────┬───────┘
                      │
              Script + Objectives
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
    VISUAL PLANNER            TTS ENGINE
          │                       │
          ▼                       ▼
     MANIM / AI                 Voice
          │                       │
          ▼                       ▼
      Animation                Whisper
          │                       │
          │                   Timestamps
          │                       │
          └──────────┬────────────┘
                     ▼
              SUBTITLE ENGINE
                     │
                     ▼
               SYNC ENGINE
                     │
                     ▼
               FFmpeg
                     │
                     ▼
              🎬 FINAL MP4
```

## পরবর্তী milestone: **M16 — Complete End-to-End Educational Video Generator**

M16-এ আমরা আর আলাদা আলাদা module শিখব না। বরং **M1–M15 সব একসাথে connect করে** একটি বাস্তব pipeline বানাব:

```text
"Explain Binary Search to a beginner in 30 seconds"
                    ↓
              AI Planner
                    ↓
              Script JSON
                    ↓
             Scene JSON
                    ↓
          Visual + Animation
                    ↓
               TTS Voice
                    ↓
              Subtitles
                    ↓
           Audio-Visual Sync
                    ↓
                 FFmpeg
                    ↓
          🎬 final_video.mp4
```

অর্থাৎ M16 থেকে আমরা **learning modules → actual working AI product**-এর দিকে যাব।
