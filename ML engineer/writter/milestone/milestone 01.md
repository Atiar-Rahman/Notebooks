# 🚀 MILESTONE 02 — JSON & Dataset Design

### Complete coverage — কোনো Topic Skip করা হবে না

তুমি **M01-এর Python foundation + OOP** complete করেছো। এখন আমরা **M02: JSON & Dataset Design** শুরু করছি।

এই milestone খুব গুরুত্বপূর্ণ, কারণ পরবর্তীতে AI/NLP/ML project-এ তোমাকে বারবার কাজ করতে হবে:

```text
Python
  ↓
JSON
  ↓
Dataset
  ↓
Preprocessing
  ↓
Training / Validation / Testing
  ↓
AI Model
```

বিশেষ করে AI writing / text-processing platform বানাতে গেলে structured data কীভাবে design করতে হয় সেটা ভালোভাবে জানতে হবে।

---

# 📚 M02 Curriculum

এই milestone-এ আমরা নিচের সব topic cover করব:

```text
M02.01 JSON Fundamentals
M02.02 JSON Data Types
M02.03 JSON Objects & Arrays
M02.04 Nested JSON
M02.05 JSON ↔ Python Conversion
M02.06 JSON File Handling
M02.07 JSONL / NDJSON
M02.08 Dataset Schema & Metadata
M02.09 Dataset Validation
M02.10 Train / Validation / Test Split
M02.11 Dataset Design for AI/NLP
M02.12 Dataset Cleaning & Quality
M02.13 Annotation / Labeling
M02.14 Dataset Versioning
M02.15 Dataset Statistics
M02.16 Dataset Pipeline
M02.17 Practical AI Dataset Project
M02.18 M02 Final Challenge
```

---

# M02.01 — JSON কী?

**JSON = JavaScript Object Notation**

JSON একটি lightweight data format।

যেমন:

```json
{
    "name": "Atiar",
    "age": 25,
    "language": "Python"
}
```

এখানে:

```text
name     → Atiar
age      → 25
language → Python
```

JSON সাধারণত ব্যবহৃত হয়:

* API
* Web application
* Configuration
* Database export
* Dataset
* Machine Learning
* NLP
* AI systems

---

# JSON কেন এত গুরুত্বপূর্ণ?

ধরো AI model-কে text দিতে হবে:

```text
Input:
Artificial intelligence is changing the world.
```

এটা structured করলে:

```json
{
    "text": "Artificial intelligence is changing the world."
}
```

আর যদি result রাখতে চাও:

```json
{
    "text": "Artificial intelligence is changing the world.",
    "score": 0.92,
    "label": "AI"
}
```

এটাই structured data।

---

# M02.02 — JSON Data Types

JSON-এর মূল data types:

```text
String
Number
Boolean
Null
Object
Array
```

---

## 1. String

```json
{
    "name": "Atiar"
}
```

String অবশ্যই double quote:

```json
"Python"
```

এটা valid:

```json
"name": "Atiar"
```

এটা JSON হিসেবে invalid:

```json
"name": 'Atiar'
```

---

# 2. Number

```json
{
    "age": 25,
    "score": 95.5
}
```

JSON-এ আলাদা করে Python-এর মতো:

```text
int
float
```

লিখতে হয় না।

---

# 3. Boolean

JSON-এ:

```json
true
false
```

উদাহরণ:

```json
{
    "is_active": true
}
```

⚠️ JSON-এ:

```python
True
False
```

লিখবে না।

JSON:

```json
true
false
```

Python:

```python
True
False
```

---

# 4. Null

JSON:

```json
{
    "email": null
}
```

Python-এর equivalent:

```python
None
```

---

# 5. Object

Object হলো key-value structure:

```json
{
    "name": "Atiar",
    "age": 25
}
```

Python dictionary-এর মতো।

---

# 6. Array

JSON array:

```json
{
    "skills": [
        "Python",
        "Django",
        "SQL"
    ]
}
```

Python:

```python
skills = [
    "Python",
    "Django",
    "SQL"
]
```

---

# M02.03 — JSON Object & Array

## Object

```json
{
    "id": 1,
    "name": "John",
    "age": 25
}
```

Structure:

```text
Object
 ├── id
 ├── name
 └── age
```

---

## Array

```json
[
    "Python",
    "JavaScript",
    "SQL"
]
```

একাধিক data রাখে।

---

## Object-এর ভিতরে Array

```json
{
    "name": "Atiar",
    "skills": [
        "Python",
        "Django",
        "SQL"
    ]
}
```

---

## Array-এর ভিতরে Object

```json
[
    {
        "id": 1,
        "name": "Atiar"
    },
    {
        "id": 2,
        "name": "Rahim"
    }
]
```

এটা dataset-এর জন্য খুব common structure।

---

# M02.04 — Nested JSON

Nested JSON মানে:

> একটি JSON object-এর ভিতরে আরেকটি object/array/object আছে।

উদাহরণ:

```json
{
    "user": {
        "id": 1,
        "name": "Atiar",
        "profile": {
            "country": "Bangladesh",
            "language": "English"
        }
    }
}
```

Access concept:

```text
user
 ↓
profile
 ↓
country
```

Python:

```python
data["user"]["profile"]["country"]
```

Output:

```text
Bangladesh
```

---

# Nested Array

```json
{
    "courses": [
        {
            "name": "Python",
            "topics": [
                "Variables",
                "Functions",
                "OOP"
            ]
        },
        {
            "name": "SQL",
            "topics": [
                "SELECT",
                "JOIN",
                "GROUP BY"
            ]
        }
    ]
}
```

Python:

```python
print(data["courses"][0]["topics"])
```

Output:

```text
['Variables', 'Functions', 'OOP']
```

---

# AI Dataset-এর Nested JSON

```json
{
    "id": 1001,
    "source": {
        "type": "user",
        "language": "en"
    },
    "input": {
        "text": "AI is changing the world."
    },
    "output": {
        "text": "Artificial intelligence is transforming the world."
    }
}
```

এ ধরনের structure ভবিষ্যতে খুব কাজে লাগবে।

---

# M02.05 — JSON ↔ Python

Python-এর `json` module ব্যবহার করব।

```python
import json
```

---

# Python → JSON String

```python
import json

data = {
    "name": "Atiar",
    "age": 25,
    "skills": ["Python", "Django"]
}

json_data = json.dumps(data)

print(json_data)
```

Output:

```json
{"name": "Atiar", "age": 25, "skills": ["Python", "Django"]}
```

---

# `dumps()`

```python
json.dumps()
```

মানে:

```text
Python object
      ↓
JSON string
```

---

# JSON String → Python

```python
json_string = '''
{
    "name": "Atiar",
    "age": 25
}
'''

data = json.loads(json_string)

print(data)
```

`loads()`:

```text
JSON string
     ↓
Python object
```

---

# `dump()` vs `dumps()`

খুব গুরুত্বপূর্ণ।

### `dumps()`

String তৈরি করে:

```python
json.dumps(data)
```

### `dump()`

File-এ লেখে:

```python
json.dump(data, file)
```

---

# `loads()` vs `load()`

### `loads()`

String থেকে:

```python
json.loads(json_string)
```

### `load()`

File থেকে:

```python
json.load(file)
```

মনে রাখো:

```text
s = string

dump   → file
dumps  → string

load   → file
loads  → string
```

---

# Pretty JSON

```python
json.dumps(data, indent=4)
```

Output:

```json
{
    "name": "Atiar",
    "age": 25,
    "skills": [
        "Python",
        "Django"
    ]
}
```

---

# ensure_ascii

বাংলা text থাকলে:

```python
data = {
    "text": "আমি Python শিখছি"
}

print(json.dumps(data, ensure_ascii=False))
```

এতে বাংলা readable থাকবে।

---

# M02.06 — JSON File Handling

একটি file:

```text
data.json
```

তৈরি করো।

```python
import json

data = {
    "name": "Atiar",
    "age": 25,
    "skills": [
        "Python",
        "Django",
        "SQL"
    ]
}

with open("data.json", "w", encoding="utf-8") as file:
    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False
    )
```

---

# JSON File Read

```python
import json

with open("data.json", "r", encoding="utf-8") as file:
    data = json.load(file)

print(data)
```

---

# JSON Dataset Read

ধরো:

```json
[
    {
        "id": 1,
        "text": "Python is easy."
    },
    {
        "id": 2,
        "text": "Machine learning is powerful."
    }
]
```

Python:

```python
with open("dataset.json", encoding="utf-8") as file:
    dataset = json.load(file)

for item in dataset:
    print(item["text"])
```

---

# M02.07 — JSONL / NDJSON

AI/ML dataset-এর জন্য এটা অত্যন্ত গুরুত্বপূর্ণ।

**JSONL = JSON Lines**

প্রতিটি line-এ একটি JSON object।

Example:

```json
{"id": 1, "text": "Python is easy."}
{"id": 2, "text": "AI is powerful."}
{"id": 3, "text": "Machine learning is useful."}
```

এখানে পুরো file একটি বড় JSON array নয়।

প্রতিটি line আলাদা record।

---

# JSON vs JSONL

### JSON

```json
[
    {
        "id": 1,
        "text": "Hello"
    },
    {
        "id": 2,
        "text": "World"
    }
]
```

### JSONL

```json
{"id": 1, "text": "Hello"}
{"id": 2, "text": "World"}
```

---

# JSONL কেন AI dataset-এ useful?

ধরো 10 GB dataset।

সব JSON একসাথে load করলে:

```python
data = json.load(file)
```

অনেক RAM লাগতে পারে।

JSONL line-by-line process করা যায়।

```python
import json

with open("dataset.jsonl", encoding="utf-8") as file:
    for line in file:
        item = json.loads(line)
        print(item)
```

---

# Generator দিয়ে JSONL

আরও efficient:

```python
import json

def read_jsonl(path):
    with open(path, encoding="utf-8") as file:
        for line in file:
            yield json.loads(line)
```

ব্যবহার:

```python
for item in read_jsonl("dataset.jsonl"):
    print(item)
```

Memory:

```text
Huge Dataset
     ↓
one line
     ↓
process
     ↓
next line
```

এটা M01-এর generator knowledge-এর practical application।

---

# M02.08 — Dataset Schema

এখন আসি AI dataset-এর সবচেয়ে গুরুত্বপূর্ণ অংশে।

**Schema** মানে dataset-এর structure/rules।

ধরো আমাদের AI writing dataset:

```json
{
    "id": 1,
    "input": "AI is changing the world.",
    "output": "Artificial intelligence is transforming the world.",
    "language": "en",
    "category": "rewriting"
}
```

Schema:

```text
id          → integer
input       → string
output      → string
language    → string
category    → string
```

---

# ভালো Schema কেন দরকার?

যদি dataset-এর এক record:

```json
{
    "input": "...",
    "output": "..."
}
```

আর অন্য record:

```json
{
    "source": "...",
    "target": "..."
}
```

তাহলে model pipeline-এ সমস্যা হবে।

তাই শুরু থেকেই structure consistent রাখতে হবে।

---

# Recommended AI Text Dataset Schema

```json
{
    "id": "sample_000001",
    "input": "AI is changing the world.",
    "output": "Artificial intelligence is transforming the world.",
    "language": "en",
    "task": "paraphrase",
    "source": "synthetic",
    "quality_score": 0.95
}
```

---

# Metadata

Metadata হলো data সম্পর্কে information।

উদাহরণ:

```json
{
    "id": "sample_001",
    "language": "en",
    "domain": "education",
    "source": "human",
    "created_at": "2026-09-06",
    "quality_score": 0.94
}
```

এগুলো মূল text নয়।

Text-এর সম্পর্কে information।

---

# M02.09 — Dataset Validation

Dataset তৈরি করলেই হবে না।

Check করতে হবে:

```text
সব record valid?
সব field আছে?
Data type ঠিক?
Text empty?
Duplicate আছে?
Label valid?
```

---

# Simple Validation

```python
def validate_record(record):

    required_fields = [
        "id",
        "input",
        "output"
    ]

    for field in required_fields:
        if field not in record:
            return False

    return True
```

---

# Type Validation

```python
def validate_record(record):

    if not isinstance(record.get("id"), str):
        return False

    if not isinstance(record.get("input"), str):
        return False

    if not isinstance(record.get("output"), str):
        return False

    return True
```

---

# Empty Text Validation

```python
def validate_record(record):

    input_text = record.get("input", "")
    output_text = record.get("output", "")

    if not input_text.strip():
        return False

    if not output_text.strip():
        return False

    return True
```

---

# Label Validation

ধরো:

```text
human
ai
unknown
```

allowed labels:

```python
VALID_LABELS = {
    "human",
    "ai",
    "unknown"
}
```

Check:

```python
if record["label"] not in VALID_LABELS:
    return False
```

---

# Schema Validation Concept

Production project-এ schema validation-এর জন্য পরে আমরা tools শিখব:

```text
JSON Schema
Pydantic
FastAPI validation
Marshmallow
```

এখন concept বুঝে রাখো।

---

# M02.10 — Train / Validation / Test Split

Machine Learning-এর fundamental concept।

Dataset সাধারণত:

```text
Dataset
   │
   ├── Training
   ├── Validation
   └── Testing
```

---

## Training Set

Model শেখে এখান থেকে।

সাধারণত:

```text
70–80%
```

---

## Validation Set

Training-এর সময় model evaluate/tune করতে ব্যবহৃত হয়।

সাধারণত:

```text
10–15%
```

---

## Test Set

শেষে final performance measure করা হয়।

সাধারণত:

```text
10–20%
```

---

# Example

10000 samples:

```text
Train      = 8000
Validation = 1000
Test       = 1000
```

অর্থাৎ:

```text
80% / 10% / 10%
```

---

# Python Split

```python
from sklearn.model_selection import train_test_split

train, temp = train_test_split(
    dataset,
    test_size=0.2,
    random_state=42
)

validation, test = train_test_split(
    temp,
    test_size=0.5,
    random_state=42
)
```

Result:

```text
80% train
10% validation
10% test
```

---

# Data Leakage

খুব গুরুত্বপূর্ণ।

যদি test data training-এ চলে যায়:

```text
Training
   ↓
Test data accidentally included
```

তাহলে evaluation ভুল হবে।

এটাকে বলে:

**Data Leakage**

---

# Duplicate Leakage

ধরো:

```text
Train:
"AI is changing the world."

Test:
"AI is changing the world."
```

এখানে duplicate।

Model আসলে নতুন data-এর উপর test হচ্ছে না।

তাই dataset split-এর আগে duplicate handling গুরুত্বপূর্ণ।

---

# M02.11 — Dataset Design for AI/NLP

এখন আমাদের actual AI project-এর দিকে আসি।

ধরো আমরা text rewriting system বানাব।

Input:

```text
The weather is very good today.
```

Output:

```text
Today's weather is really nice.
```

Dataset:

```json
{
    "id": 1,
    "input": "The weather is very good today.",
    "output": "Today's weather is really nice.",
    "task": "rewrite",
    "language": "en"
}
```

---

# Instruction Dataset

LLM fine-tuning-এর ক্ষেত্রে structure হতে পারে:

```json
{
    "instruction": "Rewrite the sentence in a natural style.",
    "input": "The weather is very good today.",
    "output": "Today's weather is really nice."
}
```

আরও structured:

```json
{
    "id": "001",
    "instruction": "Rewrite the text naturally.",
    "input": "The weather is very good today.",
    "output": "Today's weather is really nice.",
    "metadata": {
        "language": "en",
        "domain": "general",
        "quality": 0.95
    }
}
```

---

# Classification Dataset

যদি AI-generated text classification করতে চাও:

```json
{
    "text": "Artificial intelligence is transforming modern society.",
    "label": "ai"
}
```

আর:

```json
{
    "text": "I went to the market yesterday and bought some vegetables.",
    "label": "human"
}
```

---

# Sentence-level Dataset

পরে যদি sentence-level analysis করো:

```json
{
    "document_id": "doc_001",
    "sentences": [
        {
            "id": 1,
            "text": "AI is powerful.",
            "score": 0.91,
            "label": "ai"
        },
        {
            "id": 2,
            "text": "I use it every day.",
            "score": 0.35,
            "label": "human"
        }
    ]
}
```

এখান থেকেই পরে UI-তে sentence highlighting করা সম্ভব হবে।

---

# M02.12 — Dataset Cleaning & Quality

Raw dataset সাধারণত clean থাকে না।

Example:

```text
"  AI is powerful.   "
```

Clean:

```text
"AI is powerful."
```

---

# Duplicate

```text
AI is useful.
AI is useful.
AI is useful.
```

Duplicate remove করতে হবে।

---

# Empty

```text
""
"   "
```

Remove বা investigate করতে হবে।

---

# Invalid Characters

কখনও dataset-এ আসতে পারে:

```text
\u0000
```

বা corrupted text।

---

# Normalize

Basic normalization:

```python
def clean_text(text):
    text = text.strip()
    text = " ".join(text.split())
    return text
```

Example:

```python
text = "   AI     is     powerful.   "

print(clean_text(text))
```

Output:

```text
AI is powerful.
```

---

# Quality Score

Dataset record-এর quality measure রাখা যায়:

```json
{
    "text": "AI is powerful.",
    "quality_score": 0.95
}
```

যদি:

```text
quality_score < 0.5
```

তাহলে manual review করা যেতে পারে।

---

# M02.13 — Annotation / Labeling

Machine Learning dataset-এর জন্য label অত্যন্ত গুরুত্বপূর্ণ।

উদাহরণ:

```text
Text
 ↓
Human annotation
 ↓
Label
```

Classification:

```text
Text → AI
Text → Human
```

Sentiment:

```text
Positive
Negative
Neutral
```

---

# Example

```json
{
    "text": "I really enjoyed this movie.",
    "label": "positive"
}
```

আর:

```json
{
    "text": "The movie was boring.",
    "label": "negative"
}
```

---

# Multi-class

```text
positive
negative
neutral
```

---

# Multi-label

একটি text-এর multiple label থাকতে পারে:

```json
{
    "text": "Python is useful and easy to learn.",
    "labels": [
        "technology",
        "education"
    ]
}
```

---

# Annotation Quality

সব annotator একই rule follow করছে কি না সেটা গুরুত্বপূর্ণ।

তাই আগে annotation guideline তৈরি করতে হয়।

```text
Label = AI
→ text generated by an AI system

Label = Human
→ text written independently by a human
```

এতে inconsistency কমে।

---

# M02.14 — Dataset Versioning

Dataset পরিবর্তন হবে।

তাই version রাখতে হবে:

```text
dataset_v1
dataset_v2
dataset_v3
```

উদাহরণ:

```text
v1.0
v1.1
v2.0
```

---

# কেন version দরকার?

ধরো:

```text
Model A → Dataset v1
Model B → Dataset v2
```

পরে জানতে হবে কোন dataset ব্যবহার করা হয়েছিল।

---

# Dataset Folder Structure

```text
dataset/
│
├── raw/
│   └── original.jsonl
│
├── cleaned/
│   └── cleaned.jsonl
│
├── processed/
│   └── processed.jsonl
│
├── train/
│   └── train.jsonl
│
├── validation/
│   └── validation.jsonl
│
├── test/
│   └── test.jsonl
│
└── metadata.json
```

---

# Raw Data কখনো overwrite করবে না

Best practice:

```text
raw
 ↓
clean
 ↓
process
 ↓
split
```

না:

```text
raw
 ↓
overwrite
```

কারণ original data হারিয়ে যেতে পারে।

---

# M02.15 — Dataset Statistics

Dataset সম্পর্কে statistics জানা দরকার।

যেমন:

```text
Total samples: 100,000

Human: 50,000
AI:    50,000
```

---

# Class Distribution

যদি:

```text
AI     = 90,000
Human  = 10,000
```

তাহলে dataset imbalanced।

```text
90% AI
10% Human
```

এতে model biased হতে পারে।

---

# Text Length

প্রতিটি text-এর length measure করতে পারো:

```python
length = len(text.split())
```

Example:

```python
text = "Python is a powerful programming language."

print(len(text.split()))
```

---

# Statistics Example

```python
lengths = []

for item in dataset:
    length = len(item["text"].split())
    lengths.append(length)

print("Minimum:", min(lengths))
print("Maximum:", max(lengths))
print("Average:", sum(lengths) / len(lengths))
```

---

# Useful Dataset Statistics

```text
Total samples
Number of classes
Class distribution
Minimum length
Maximum length
Average length
Median length
Duplicate count
Missing values
Language distribution
Domain distribution
```

---

# M02.16 — Complete Dataset Pipeline

এখন সব concept একসাথে।

```text
Raw Data
   ↓
Collection
   ↓
JSON/JSONL
   ↓
Schema Validation
   ↓
Cleaning
   ↓
Duplicate Removal
   ↓
Annotation
   ↓
Quality Check
   ↓
Statistics
   ↓
Train/Validation/Test Split
   ↓
Processed Dataset
   ↓
Model Training
```

---

# AI Writing Dataset Pipeline

```text
Raw Text
   ↓
Collect
   ↓
JSONL
   ↓
Validate
   ↓
Clean
   ↓
Remove Duplicates
   ↓
Annotate
   ↓
Quality Filter
   ↓
Split
   ↓
Train Dataset
   ↓
Model
```

---

# M02.17 — Practical Project

এখন একটি ছোট কিন্তু complete project বানাবে।

## Project: AI Text Dataset Manager

Folder:

```text
ai_dataset_project/
│
├── data/
│   ├── raw/
│   │   └── dataset.jsonl
│   │
│   ├── cleaned/
│   │   └── dataset.jsonl
│   │
│   └── split/
│       ├── train.jsonl
│       ├── validation.jsonl
│       └── test.jsonl
│
├── scripts/
│   ├── create_dataset.py
│   ├── validate.py
│   ├── clean.py
│   ├── statistics.py
│   └── split.py
│
└── README.md
```

---

# Step 1 — Raw Dataset

`dataset.jsonl`

```json
{"id": "001", "input": "AI is changing the world.", "output": "Artificial intelligence is transforming the world.", "label": "rewrite"}
{"id": "002", "input": "Python is easy to learn.", "output": "Python is relatively easy to learn.", "label": "rewrite"}
{"id": "003", "input": "Machine learning is useful.", "output": "Machine learning has many practical applications.", "label": "rewrite"}
```

---

# Step 2 — Read Dataset

```python
import json

def read_jsonl(path):
    with open(path, encoding="utf-8") as file:
        for line in file:
            yield json.loads(line)


for item in read_jsonl("data/raw/dataset.jsonl"):
    print(item)
```

---

# Step 3 — Validate

```python
def validate(item):

    required_fields = [
        "id",
        "input",
        "output",
        "label"
    ]

    for field in required_fields:
        if field not in item:
            return False

    if not item["input"].strip():
        return False

    if not item["output"].strip():
        return False

    return True
```

---

# Step 4 — Clean

```python
def clean_text(text):
    return " ".join(text.strip().split())
```

Apply:

```python
item["input"] = clean_text(item["input"])
item["output"] = clean_text(item["output"])
```

---

# Step 5 — Save Clean Dataset

```python
import json

with open(
    "data/cleaned/dataset.jsonl",
    "w",
    encoding="utf-8"
) as file:

    for item in dataset:

        file.write(
            json.dumps(
                item,
                ensure_ascii=False
            ) + "\n"
        )
```

---

# Step 6 — Split

```python
from sklearn.model_selection import train_test_split

train, temp = train_test_split(
    dataset,
    test_size=0.2,
    random_state=42
)

validation, test = train_test_split(
    temp,
    test_size=0.5,
    random_state=42
)
```

---

# Step 7 — Save Splits

Function বানানো ভালো:

```python
import json

def save_jsonl(data, path):

    with open(path, "w", encoding="utf-8") as file:

        for item in data:

            file.write(
                json.dumps(
                    item,
                    ensure_ascii=False
                ) + "\n"
            )
```

তারপর:

```python
save_jsonl(train, "data/split/train.jsonl")
save_jsonl(validation, "data/split/validation.jsonl")
save_jsonl(test, "data/split/test.jsonl")
```

---

# Step 8 — Statistics

```python
def dataset_statistics(dataset):

    total = len(dataset)

    input_lengths = [
        len(item["input"].split())
        for item in dataset
    ]

    print("Total:", total)
    print("Min:", min(input_lengths))
    print("Max:", max(input_lengths))
    print("Average:", sum(input_lengths) / total)
```

---

# Final Architecture

তোমার M02 project:

```text
                DATASET MANAGER
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
      Read           Clean          Validate
        │              │              │
        └──────────────┼──────────────┘
                       ↓
                  Statistics
                       ↓
                    Split
                       ↓
          ┌────────────┼────────────┐
          ↓            ↓            ↓
        Train       Validation      Test
```

---

# 🧠 M02-এর সবচেয়ে গুরুত্বপূর্ণ Concepts

এগুলো অবশ্যই বুঝতে হবে:

### JSON

```text
Structured data format
```

### JSON Object

```text
{
    "key": "value"
}
```

### JSON Array

```text
[
    {...},
    {...}
]
```

### Nested JSON

```text
object
 ↓
object
 ↓
array
 ↓
object
```

### Python ↔ JSON

```text
dumps → Python → JSON string
loads → JSON string → Python

dump  → Python → JSON file
load  → JSON file → Python
```

### JSONL

```text
one line = one record
```

### Schema

```text
Dataset structure + rules
```

### Validation

```text
Data valid কিনা check
```

### Cleaning

```text
raw → clean
```

### Annotation

```text
data → label
```

### Split

```text
Dataset
├── Train
├── Validation
└── Test
```

### Versioning

```text
v1 → v2 → v3
```

---

# 🎯 M02 Practice Set

## Beginner

### Task 1

এই JSON তৈরি করো:

```text
name
age
country
skills
```

---

### Task 2

Python dictionary থেকে JSON string তৈরি করো।

---

### Task 3

JSON string থেকে Python dictionary তৈরি করো।

---

### Task 4

একটি JSON file তৈরি করে read করো।

---

## Intermediate

### Task 5

এই structure তৈরি করো:

```text
User
 ├── profile
 │    ├── name
 │    ├── age
 │    └── country
 │
 └── skills
```

---

### Task 6

১০টি record-এর JSONL dataset তৈরি করো।

---

### Task 7

JSONL generator দিয়ে dataset read করো।

---

### Task 8

Empty text detect করো।

---

### Task 9

Duplicate record detect করো।

---

### Task 10

Dataset-এর:

```text
min length
max length
average length
```

calculate করো।

---

# 🔥 Advanced Challenge

একটি dataset তৈরি করো:

```json
{
    "id": "001",
    "instruction": "Rewrite the text naturally.",
    "input": "The weather is very good today.",
    "output": "Today's weather is really nice.",
    "metadata": {
        "language": "en",
        "domain": "general",
        "quality_score": 0.95
    }
}
```

তারপর Python program দিয়ে:

1. JSONL read করবে
2. schema validate করবে
3. empty data remove করবে
4. duplicate remove করবে
5. text clean করবে
6. statistics বের করবে
7. 80/10/10 split করবে
8. train/validation/test JSONL save করবে

---

# 📝 M02 Theory Questions

নিজে উত্তর দেওয়ার চেষ্টা করবে:

1. JSON কী?
2. JSON কেন ব্যবহার করা হয়?
3. JSON-এর data types কী কী?
4. JSON object কী?
5. JSON array কী?
6. Nested JSON কী?
7. JSON এবং Python dictionary-এর পার্থক্য কী?
8. `json.dumps()` কী করে?
9. `json.loads()` কী করে?
10. `json.dump()` কী করে?
11. `json.load()` কী করে?
12. JSON এবং JSONL-এর পার্থক্য কী?
13. JSONL AI dataset-এর জন্য কেন useful?
14. Schema কী?
15. Metadata কী?
16. Dataset validation কেন দরকার?
17. Dataset cleaning কী?
18. Annotation কী?
19. Train dataset কী?
20. Validation dataset কী?
21. Test dataset কী?
22. Data leakage কী?
23. Dataset versioning কেন দরকার?
24. Class imbalance কী?
25. Duplicate data কেন সমস্যা?
26. Raw dataset overwrite করা উচিত নয় কেন?
27. AI/NLP dataset-এর একটি ভালো schema কেমন হতে পারে?
28. JSONL generator কেন memory-efficient?
29. Dataset statistics কেন দরকার?
30. AI model training-এর আগে dataset pipeline কেন দরকার?

---

# ✅ M02 Completion Checklist

সবগুলো **✓** করতে পারলে M02 complete:

```text
[ ] JSON কী বুঝি
[ ] JSON syntax বুঝি
[ ] String বুঝি
[ ] Number বুঝি
[ ] Boolean বুঝি
[ ] Null বুঝি
[ ] Object বুঝি
[ ] Array বুঝি
[ ] Nested JSON বুঝি
[ ] Python → JSON করতে পারি
[ ] JSON → Python করতে পারি
[ ] dumps() বুঝি
[ ] loads() বুঝি
[ ] dump() বুঝি
[ ] load() বুঝি
[ ] JSON file read করতে পারি
[ ] JSON file write করতে পারি
[ ] JSONL বুঝি
[ ] JSONL read করতে পারি
[ ] Generator দিয়ে JSONL process করতে পারি
[ ] Dataset schema design করতে পারি
[ ] Metadata বুঝি
[ ] Dataset validation করতে পারি
[ ] Dataset cleaning করতে পারি
[ ] Duplicate detect করতে পারি
[ ] Annotation বুঝি
[ ] Label design করতে পারি
[ ] Dataset statistics বের করতে পারি
[ ] Train/Validation/Test বুঝি
[ ] Data leakage বুঝি
[ ] Dataset versioning বুঝি
[ ] Raw/Cleaned/Processed structure বুঝি
[ ] AI/NLP dataset design করতে পারি
[ ] Complete dataset pipeline বানাতে পারি
[ ] Practical project complete করতে পারি
```

---

# 🏁 M02-এর Final Mental Model

সবচেয়ে গুরুত্বপূর্ণভাবে এটা মাথায় রাখো:

```text
                 RAW DATA
                    ↓
              JSON / JSONL
                    ↓
                 SCHEMA
                    ↓
               VALIDATION
                    ↓
                 CLEANING
                    ↓
             DUPLICATE CHECK
                    ↓
                ANNOTATION
                    ↓
              QUALITY CHECK
                    ↓
               STATISTICS
                    ↓
                  SPLIT
          ┌─────────┼─────────┐
          ↓         ↓         ↓
        TRAIN      VAL       TEST
          │         │         │
          └─────────┼─────────┘
                    ↓
                AI MODEL
                    ↓
              EVALUATION
```

### M01 + M02 এখন পর্যন্ত:

```text
M01 — Python Foundation + OOP
              ↓
M02 — JSON & Dataset Design
              ↓
M03 — Data Processing / next foundation
              ↓
M04 — ...
              ↓
NLP
              ↓
Transformers
              ↓
LLM
              ↓
Fine-tuning
              ↓
AI Writing System
              ↓
Production Platform
```

**M02-এর লক্ষ্য শুধু JSON syntax শেখা নয়**—শেষে তোমাকে এমন অবস্থায় যেতে হবে যেখানে একটি **real AI dataset কীভাবে design, validate, clean, analyze এবং train/validation/test-এ prepare করতে হয়**, সেটা নিজে করতে পারো।


---
# 🚀 MILESTONE 03 — Python Data Processing & Standard Library

M02-এ আমরা **JSON, JSONL, Dataset Schema, Validation, Cleaning, Statistics, Train/Validation/Test split** শিখেছি।

এখন M03-এর লক্ষ্য হলো:

> **Python দিয়ে real-world data efficiently process, transform, search, sort, aggregate এবং automate করা।**

AI/NLP project-এর জন্য এই milestone খুব গুরুত্বপূর্ণ।

```text
M01
Python Foundation + OOP
        ↓
M02
JSON + Dataset Design
        ↓
M03
Data Processing + Standard Library
        ↓
M04
Git + Linux + Software Engineering
        ↓
M05+
Backend / NLP / ML / LLM
```

---

# 📚 M03 Complete Curriculum

কোনো topic skip না করার জন্য M03-কে এভাবে ভাগ করছি:

```text
M03.01  Data Processing Fundamentals
M03.02  String Processing Deep Dive
M03.03  Regular Expressions (Regex)
M03.04  Advanced Text Cleaning
M03.05  Sorting & Searching
M03.06  Aggregation & Counting
M03.07  Collections Module
M03.08  itertools
M03.09  functools
M03.10  datetime
M03.11  os & Environment Variables
M03.12  pathlib Advanced
M03.13  shutil
M03.14  glob & File Discovery
M03.15  CSV/JSON/JSONL Processing
M03.16  Data Validation Pipeline
M03.17  Memory-Efficient Processing
M03.18  Performance Basics
M03.19  Data Pipeline Architecture
M03.20  Complete AI/NLP Data Processing Project
M03.21  Final Challenge
```

---

# M03.01 — Data Processing Fundamentals

Data processing মানে:

```text
Raw Data
   ↓
Read
   ↓
Validate
   ↓
Clean
   ↓
Transform
   ↓
Analyze
   ↓
Save
```

উদাহরণ:

```python
data = [
    "  Python is great  ",
    "AI is powerful",
    "   Machine Learning   "
]
```

Clean:

```python
cleaned = []

for text in data:
    text = text.strip()
    cleaned.append(text)
```

Result:

```python
[
    "Python is great",
    "AI is powerful",
    "Machine Learning"
]
```

---

# Processing-এর 4টি প্রধান কাজ

## 1. Extract

Data বের করা।

```python
names = [user["name"] for user in users]
```

## 2. Transform

Data পরিবর্তন করা।

```python
text = text.lower()
```

## 3. Filter

প্রয়োজনীয় data রাখা।

```python
long_texts = [
    text for text in texts
    if len(text) > 100
]
```

## 4. Aggregate

অনেক data থেকে summary তৈরি করা।

```python
total = sum(scores)
```

---

# M03.02 — String Processing Deep Dive

AI/NLP-এর জন্য string processing অত্যন্ত গুরুত্বপূর্ণ।

---

## `lower()`

```python
text = "Python Is Powerful"

print(text.lower())
```

Output:

```text
python is powerful
```

---

## `upper()`

```python
text.upper()
```

---

## `capitalize()`

```python
text = "python is easy"

print(text.capitalize())
```

Output:

```text
Python is easy
```

---

## `title()`

```python
text = "python programming language"

print(text.title())
```

Output:

```text
Python Programming Language
```

---

# `strip()`

```python
text = "   Hello World   "

print(text.strip())
```

Left:

```python
text.lstrip()
```

Right:

```python
text.rstrip()
```

---

# `replace()`

```python
text = "I like Java"

text = text.replace("Java", "Python")

print(text)
```

Output:

```text
I like Python
```

---

# `split()`

```python
text = "Python is powerful"

words = text.split()

print(words)
```

Output:

```python
['Python', 'is', 'powerful']
```

---

# Split by delimiter

```python
text = "Python,Django,SQL"

skills = text.split(",")

print(skills)
```

---

# `join()`

```python
words = ["Python", "is", "powerful"]

text = " ".join(words)

print(text)
```

Output:

```text
Python is powerful
```

---

# `startswith()`

```python
text = "Python programming"

print(text.startswith("Python"))
```

---

# `endswith()`

```python
print(text.endswith("programming"))
```

---

# `find()`

```python
text = "Python is powerful"

print(text.find("powerful"))
```

না পেলে:

```text
-1
```

---

# `index()`

```python
text.index("powerful")
```

না পেলে exception হবে।

তাই সাধারণ search-এর জন্য `find()` নিরাপদ।

---

# `count()`

```python
text = "Python Python Python"

print(text.count("Python"))
```

---

# String slicing

```python
text = "Python"

print(text[0])
print(text[:3])
print(text[-1])
print(text[::-1])
```

---

# Important: String immutable

```python
text = "Python"
```

এভাবে করা যাবে না:

```python
text[0] = "J"
```

কারণ string immutable।

নতুন string তৈরি করতে হবে:

```python
text = "J" + text[1:]
```

---

# M03.03 — Regular Expressions (Regex)

Regex = **Regular Expression**

Text-এর মধ্যে pattern খুঁজতে ব্যবহার হয়।

Python:

```python
import re
```

---

# Basic Search

```python
text = "Python is powerful"

result = re.search("Python", text)

print(result)
```

---

# `re.findall()`

```python
text = "Python is great. Python is easy."

matches = re.findall("Python", text)

print(matches)
```

Output:

```python
['Python', 'Python']
```

---

# Digit Pattern

```python
text = "My age is 25"

numbers = re.findall(r"\d+", text)

print(numbers)
```

Output:

```python
['25']
```

`\d` = digit

---

# Word Pattern

```python
text = "Python AI ML"

words = re.findall(r"\w+", text)

print(words)
```

---

# Common Regex Symbols

```text
\d    digit
\D    non-digit

\w    word character
\W    non-word

\s    whitespace
\S    non-whitespace

.     any character
^     beginning
$     ending

*     zero or more
+     one or more
?     zero or one

[]    character set
()    group
|     OR
```

---

# Example: Extract numbers

```python
text = """
Python 3.11
Django 5
PostgreSQL 16
"""

numbers = re.findall(r"\d+(?:\.\d+)?", text)

print(numbers)
```

---

# Email Pattern

Basic example:

```python
text = "Contact me at test@example.com"

emails = re.findall(
    r"[\w.-]+@[\w.-]+\.\w+",
    text
)

print(emails)
```

Production email validation can be more complicated; regex should not be treated as a complete email specification.

---

# Regex substitution

```python
text = "Python    is     powerful"

cleaned = re.sub(r"\s+", " ", text)

print(cleaned)
```

Output:

```text
Python is powerful
```

---

# Regex split

```python
text = "Python,AI;ML,Django"

parts = re.split(r"[,;]", text)

print(parts)
```

---

# Compile Regex

যদি একই pattern বারবার ব্যবহার করো:

```python
pattern = re.compile(r"\d+")

print(pattern.findall("Age 25"))
print(pattern.findall("Age 30"))
```

---

# M03.04 — Advanced Text Cleaning

AI/NLP project-এ raw text সাধারণত:

```text
"   AI   is    powerful!!!   "
```

Clean করার দরকার হয়।

---

# Basic Cleaning Function

```python
import re

def clean_text(text):

    text = text.strip()

    text = re.sub(
        r"\s+",
        " ",
        text
    )

    return text
```

---

# Lowercase

```python
def clean_text(text):

    text = text.strip()
    text = text.lower()
    text = re.sub(r"\s+", " ", text)

    return text
```

---

# Remove HTML

```python
html = "<p>Hello <b>World</b></p>"
```

Basic:

```python
cleaned = re.sub(r"<[^>]+>", "", html)

print(cleaned)
```

Output:

```text
Hello World
```

For real HTML parsing, later use a dedicated HTML parser rather than relying solely on regex.

---

# Remove URLs

```python
text = "Visit https://example.com now"

text = re.sub(
    r"https?://\S+",
    "",
    text
)
```

---

# Remove punctuation

```python
import string

text = "Hello, world!"

cleaned = text.translate(
    str.maketrans("", "", string.punctuation)
)

print(cleaned)
```

---

# Tokenization-এর Basic Concept

```python
text = "AI is changing the world."

tokens = text.split()

print(tokens)
```

Output:

```python
['AI', 'is', 'changing', 'the', 'world.']
```

এটা basic whitespace tokenization।

Proper NLP tokenization আমরা পরে NLP milestone-এ বিস্তারিত করব।

---

# M03.05 — Sorting & Searching

---

# `sorted()`

```python
numbers = [5, 2, 9, 1]

result = sorted(numbers)

print(result)
```

---

# Reverse

```python
sorted(numbers, reverse=True)
```

---

# `.sort()`

```python
numbers.sort()
```

Difference:

```text
sorted()
→ নতুন list দেয়

list.sort()
→ original list পরিবর্তন করে
```

---

# Sort by Key

```python
users = [
    {"name": "A", "age": 30},
    {"name": "B", "age": 20},
    {"name": "C", "age": 25}
]

users = sorted(
    users,
    key=lambda user: user["age"]
)
```

---

# Sort AI Scores

```python
results = [
    {"text": "A", "score": 0.50},
    {"text": "B", "score": 0.95},
    {"text": "C", "score": 0.80}
]

results = sorted(
    results,
    key=lambda item: item["score"],
    reverse=True
)
```

---

# Searching

Simple:

```python
if "Python" in skills:
    print("Found")
```

---

# `any()`

```python
scores = [0.2, 0.4, 0.9]

if any(score > 0.8 for score in scores):
    print("High score found")
```

---

# `all()`

```python
scores = [0.9, 0.8, 0.95]

if all(score >= 0.8 for score in scores):
    print("All are high")
```

---

# `min()` / `max()`

```python
scores = [0.4, 0.9, 0.7]

print(min(scores))
print(max(scores))
```

With objects:

```python
best = max(
    results,
    key=lambda x: x["score"]
)
```

---

# M03.06 — Aggregation & Counting

---

# `sum()`

```python
numbers = [10, 20, 30]

print(sum(numbers))
```

---

# Average

```python
average = sum(numbers) / len(numbers)
```

---

# Frequency Counting

Manual:

```python
words = [
    "python",
    "ai",
    "python",
    "ml"
]

frequency = {}

for word in words:
    frequency[word] = frequency.get(word, 0) + 1

print(frequency)
```

---

# `Counter`

এখন standard library-এর powerful tool।

```python
from collections import Counter

words = [
    "python",
    "ai",
    "python",
    "ml",
    "python"
]

counter = Counter(words)

print(counter)
```

Output:

```python
Counter({
    'python': 3,
    'ai': 1,
    'ml': 1
})
```

---

# Most Common

```python
counter.most_common(2)
```

---

# M03.07 — `collections` Module

Python-এর `collections` module খুব গুরুত্বপূর্ণ।

প্রধানগুলো:

```text
Counter
defaultdict
deque
namedtuple
ChainMap
```

---

# Counter

আগেই দেখেছি:

```python
from collections import Counter
```

---

# defaultdict

সাধারণ dictionary:

```python
data = {}

data["python"] = data.get("python", 0) + 1
```

`defaultdict`:

```python
from collections import defaultdict

data = defaultdict(int)

data["python"] += 1
data["python"] += 1

print(data)
```

---

# defaultdict(list)

```python
groups = defaultdict(list)

groups["ai"].append("Python")
groups["ai"].append("PyTorch")
groups["web"].append("Django")
```

Result:

```python
{
    "ai": ["Python", "PyTorch"],
    "web": ["Django"]
}
```

---

# deque

Double-ended queue:

```python
from collections import deque

queue = deque()

queue.append("A")
queue.append("B")

print(queue.popleft())
```

Useful for:

* queues
* sliding windows
* BFS
* streaming buffers

---

# `deque` maxlen

```python
history = deque(maxlen=3)

history.append("A")
history.append("B")
history.append("C")
history.append("D")

print(history)
```

Output:

```text
B C D
```

পুরনো item automatically বের হয়ে গেছে।

AI chat history-এর মতো use case-এ useful।

---

# M03.08 — `itertools`

`itertools` efficient iterator tools দেয়।

```python
import itertools
```

---

# `count()`

```python
counter = itertools.count(1)

print(next(counter))
print(next(counter))
print(next(counter))
```

Output:

```text
1
2
3
```

Infinite iterator।

---

# `cycle()`

```python
colors = itertools.cycle(["A", "B", "C"])
```

Repeated:

```text
A B C A B C A B C...
```

---

# `repeat()`

```python
itertools.repeat("AI", 3)
```

---

# `chain()`

Multiple iterable combine:

```python
a = [1, 2]
b = [3, 4]

result = itertools.chain(a, b)

print(list(result))
```

---

# `islice()`

Iterator-এর slice:

```python
numbers = itertools.count()

result = itertools.islice(
    numbers,
    5
)

print(list(result))
```

---

# `product()`

Cartesian product:

```python
colors = ["red", "blue"]
sizes = ["S", "M"]

result = itertools.product(
    colors,
    sizes
)

print(list(result))
```

---

# `combinations()`

```python
items = ["A", "B", "C"]

print(
    list(
        itertools.combinations(items, 2)
    )
)
```

---

# `permutations()`

```python
print(
    list(
        itertools.permutations(["A", "B", "C"], 2)
    )
)
```

---

# M03.09 — `functools`

---

# `reduce()`

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(
    lambda a, b: a + b,
    numbers
)

print(result)
```

---

# `partial()`

Function-এর কিছু argument আগে থেকে set করা।

```python
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(
    power,
    exponent=2
)

print(square(5))
```

Output:

```text
25
```

---

# `lru_cache`

Repeated expensive function calls cache করা যায়।

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):

    if n <= 1:
        return n

    return fibonacci(n - 1) + fibonacci(n - 2)
```

এতে repeated calculation কমে।

---

# `wraps`

M01-এ decorator-এ দেখেছি:

```python
from functools import wraps
```

Original function-এর metadata preserve করতে ব্যবহৃত হয়।

---

# M03.10 — Date & Time

Python:

```python
from datetime import datetime
```

---

# Current Time

```python
now = datetime.now()

print(now)
```

---

# Date

```python
from datetime import date

today = date.today()

print(today)
```

---

# Specific Date

```python
from datetime import date

d = date(2026, 9, 6)

print(d)
```

---

# Formatting

```python
now.strftime("%Y-%m-%d")
```

Result:

```text
2026-09-06
```

Common:

```text
%Y → year
%m → month
%d → day
%H → hour
%M → minute
%S → second
```

---

# String → datetime

```python
from datetime import datetime

date_string = "2026-09-06"

date_object = datetime.strptime(
    date_string,
    "%Y-%m-%d"
)
```

---

# Time Difference

```python
from datetime import datetime

start = datetime.now()

# processing

end = datetime.now()

duration = end - start

print(duration)
```

---

# Timezone Concept

Production applications-এ timezone গুরুত্বপূর্ণ।

তাই পরে আমরা শিখব:

```text
UTC
Timezone-aware datetime
Naive datetime
```

---

# M03.11 — `os` & Environment Variables

Python:

```python
import os
```

---

# Current Directory

```python
print(os.getcwd())
```

---

# List Directory

```python
print(os.listdir())
```

---

# Environment Variable

```python
api_key = os.getenv("API_KEY")
```

---

# `.env`

Production project-এ secret code কখনো সরাসরি:

```python
API_KEY = "secret-key"
```

লিখবে না।

Instead:

```text
.env
```

এবং environment variable ব্যবহার করবে।

Example:

```text
API_KEY=your-secret-key
DATABASE_URL=...
```

পরে আমরা `python-dotenv` এবং production secret management বিস্তারিত শিখব।

---

# M03.12 — `pathlib` Advanced

M01/M02-এ basic `Path` দেখেছি।

এখন advanced ব্যবহার।

```python
from pathlib import Path

base = Path("data")
```

---

# Create directory

```python
base.mkdir(
    parents=True,
    exist_ok=True
)
```

---

# Check

```python
base.exists()
base.is_dir()
base.is_file()
```

---

# Iterate

```python
for item in base.iterdir():
    print(item)
```

---

# Glob

```python
files = base.glob("*.json")

for file in files:
    print(file)
```

---

# Recursive

```python
files = base.rglob("*.json")
```

সব subdirectory search করবে।

---

# File properties

```python
file.name
file.stem
file.suffix
file.parent
```

---

# Rename

```python
old = Path("old.txt")
new = Path("new.txt")

old.rename(new)
```

---

# Delete

```python
file.unlink()
```

সতর্কতার সাথে ব্যবহার করবে।

---

# M03.13 — `shutil`

File/folder operations-এর জন্য:

```python
import shutil
```

---

# Copy File

```python
shutil.copy(
    "source.txt",
    "backup.txt"
)
```

---

# Copy Directory

```python
shutil.copytree(
    "data",
    "backup"
)
```

---

# Move

```python
shutil.move(
    "file.txt",
    "archive/file.txt"
)
```

---

# Delete Directory

```python
shutil.rmtree("backup")
```

⚠️ এটা recursive delete করে। Production-এ খুব সাবধানে ব্যবহার করবে।

---

# M03.14 — `glob` & File Discovery

Python-এর `glob` module:

```python
import glob
```

---

# Find JSON

```python
files = glob.glob("data/*.json")

print(files)
```

---

# Recursive

```python
files = glob.glob(
    "data/**/*.json",
    recursive=True
)
```

---

# `pathlib` বনাম `glob`

Modern Python project-এ সাধারণত:

```python
Path.rglob()
```

খুব clean।

---

# M03.15 — CSV / JSON / JSONL Processing

M02-এ basic JSON/JSONL শিখেছি।

এখন processing pipeline।

---

# CSV Read

```python
import csv

with open(
    "students.csv",
    encoding="utf-8"
) as file:

    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

---

# CSV Write

```python
import csv

rows = [
    {
        "name": "Atiar",
        "score": 90
    },
    {
        "name": "Rahim",
        "score": 85
    }
]

with open(
    "students.csv",
    "w",
    newline="",
    encoding="utf-8"
) as file:

    writer = csv.DictWriter(
        file,
        fieldnames=["name", "score"]
    )

    writer.writeheader()
    writer.writerows(rows)
```

---

# JSONL Processor

```python
import json

def process_jsonl(input_path, output_path):

    with open(input_path, encoding="utf-8") as infile, \
         open(output_path, "w", encoding="utf-8") as outfile:

        for line in infile:

            item = json.loads(line)

            item["processed"] = True

            outfile.write(
                json.dumps(
                    item,
                    ensure_ascii=False
                ) + "\n"
            )
```

---

# M03.16 — Complete Data Validation Pipeline

এখন real pipeline।

```text
Input
 ↓
Parse
 ↓
Validate Schema
 ↓
Clean
 ↓
Transform
 ↓
Filter
 ↓
Deduplicate
 ↓
Statistics
 ↓
Save
```

---

# Validation Function

```python
def validate_record(record):

    required = [
        "id",
        "text"
    ]

    for field in required:

        if field not in record:
            return False

    if not isinstance(
        record["text"],
        str
    ):
        return False

    if not record["text"].strip():
        return False

    return True
```

---

# Cleaning Function

```python
import re

def clean_text(text):

    text = text.strip()

    text = re.sub(
        r"\s+",
        " ",
        text
    )

    return text
```

---

# Transformation

```python
def process_record(record):

    record["text"] = clean_text(
        record["text"]
    )

    record["word_count"] = len(
        record["text"].split()
    )

    return record
```

---

# M03.17 — Memory-Efficient Processing

ধরো:

```text
dataset = 50 GB
```

এটা করা dangerous:

```python
data = json.load(file)
```

RAM কম হতে পারে।

Instead:

```python
def read_jsonl(path):

    with open(path, encoding="utf-8") as file:

        for line in file:

            yield json.loads(line)
```

তারপর:

```python
for item in read_jsonl("huge.jsonl"):

    process(item)
```

---

# Batch Processing

AI systems-এ batch খুব common।

```python
def batches(iterable, batch_size):

    batch = []

    for item in iterable:

        batch.append(item)

        if len(batch) == batch_size:

            yield batch
            batch = []

    if batch:
        yield batch
```

ব্যবহার:

```python
for batch in batches(data, 32):

    process_batch(batch)
```

---

# Memory Model

```text
Bad:

50 GB Dataset
     ↓
RAM
     ↓
Crash ❌


Good:

50 GB Dataset
     ↓
Small Batch
     ↓
Process
     ↓
Next Batch
     ↓
Process
     ↓
...
```

AI inference/training pipeline-এ এই concept খুব গুরুত্বপূর্ণ।

---

# M03.18 — Performance Basics

Performance measure:

```python
import time

start = time.perf_counter()

# operation

end = time.perf_counter()

print(end - start)
```

---

# Avoid unnecessary work

Bad:

```python
for item in data:

    clean_text(item)

    if condition:
        clean_text(item)
```

একই কাজ দুইবার হতে পারে।

Better:

```python
for item in data:

    cleaned = clean_text(item)

    if condition:
        ...
```

---

# List vs Generator

List:

```python
numbers = [
    x * 2
    for x in range(1000000)
]
```

সব memory-তে।

Generator:

```python
numbers = (
    x * 2
    for x in range(1000000)
)
```

Lazy।

---

# Set for Membership

Bad:

```python
if word in huge_list:
    ...
```

অনেক ক্ষেত্রে membership-এর জন্য set দ্রুততর:

```python
valid_words = set(words)

if word in valid_words:
    ...
```

এটা algorithmic efficiency-এর foundation।

---

# M03.19 — Data Pipeline Architecture

এখন সবকিছুকে architecture হিসেবে দেখো।

```text
             RAW DATA
                 ↓
          Data Loader
                 ↓
          Parser / Reader
                 ↓
           Validator
                 ↓
            Cleaner
                 ↓
          Transformer
                 ↓
            Filter
                 ↓
         Deduplicator
                 ↓
           Statistics
                 ↓
             Split
                 ↓
       Processed Dataset
```

Code architecture:

```text
project/
│
├── data/
│
├── processors/
│   ├── loader.py
│   ├── validator.py
│   ├── cleaner.py
│   ├── transformer.py
│   └── statistics.py
│
├── scripts/
│   └── process_dataset.py
│
└── tests/
```

এটা পরে বড় AI project-এর foundation হবে।

---

# M03.20 — Complete AI/NLP Data Processing Project

এখন একটি real project বানাবে।

## Project Name

**AI Text Dataset Processor**

---

# Folder Structure

```text
ai_text_processor/
│
├── data/
│   ├── raw/
│   │   └── dataset.jsonl
│   │
│   ├── cleaned/
│   │   └── cleaned.jsonl
│   │
│   └── reports/
│       └── statistics.json
│
├── src/
│   ├── loader.py
│   ├── cleaner.py
│   ├── validator.py
│   ├── statistics.py
│   └── pipeline.py
│
├── tests/
│
├── requirements.txt
└── main.py
```

---

# Raw Dataset

```json
{"id": "001", "text": "   AI   is   changing the world.   ", "label": "ai"}
{"id": "002", "text": "Python is a powerful language.", "label": "human"}
{"id": "003", "text": "   Machine learning is useful. ", "label": "ai"}
```

---

# `loader.py`

```python
import json


def read_jsonl(path):

    with open(
        path,
        encoding="utf-8"
    ) as file:

        for line in file:

            line = line.strip()

            if not line:
                continue

            yield json.loads(line)
```

---

# `cleaner.py`

```python
import re


def clean_text(text):

    text = text.strip()

    text = re.sub(
        r"\s+",
        " ",
        text
    )

    return text
```

---

# `validator.py`

```python
def validate_record(record):

    required_fields = [
        "id",
        "text",
        "label"
    ]

    for field in required_fields:

        if field not in record:
            return False

    if not isinstance(
        record["text"],
        str
    ):
        return False

    if not record["text"].strip():
        return False

    return True
```

---

# `statistics.py`

```python
from collections import Counter


def calculate_statistics(records):

    labels = Counter()
    lengths = []

    for record in records:

        labels[record["label"]] += 1

        lengths.append(
            len(record["text"].split())
        )

    return {
        "total": len(records),
        "labels": dict(labels),
        "min_length": min(lengths)
            if lengths else 0,
        "max_length": max(lengths)
            if lengths else 0,
        "average_length": (
            sum(lengths) / len(lengths)
            if lengths
            else 0
        )
    }
```

---

# `pipeline.py`

```python
from .loader import read_jsonl
from .cleaner import clean_text
from .validator import validate_record


def process_dataset(input_path):

    records = []

    for record in read_jsonl(input_path):

        if not validate_record(record):
            continue

        record["text"] = clean_text(
            record["text"]
        )

        record["word_count"] = len(
            record["text"].split()
        )

        records.append(record)

    return records
```

---

# `main.py`

```python
from src.pipeline import process_dataset
from src.statistics import calculate_statistics


dataset = process_dataset(
    "data/raw/dataset.jsonl"
)

stats = calculate_statistics(
    dataset
)

print(stats)
```

---

# Final Pipeline

```text
dataset.jsonl
      ↓
    Loader
      ↓
   Validator
      ↓
    Cleaner
      ↓
 Word Counter
      ↓
  Statistics
      ↓
   Clean Data
```

---

# 🔥 M03 Advanced Challenge

এখন তুমি নিজে এমন program বানাবে যেখানে:

### Input

একটি বড় `dataset.jsonl`

প্রতিটি record:

```json
{
    "id": "001",
    "text": "   AI is powerful.   ",
    "label": "ai"
}
```

### Program করবে:

```text
1. Read JSONL
2. Ignore empty lines
3. Parse JSON
4. Validate schema
5. Remove invalid records
6. Clean whitespace
7. Normalize text
8. Detect duplicate text
9. Calculate word count
10. Calculate character count
11. Count labels
12. Calculate min length
13. Calculate max length
14. Calculate average length
15. Save cleaned JSONL
16. Save statistics.json
17. Handle exceptions
18. Process line-by-line
19. Never load huge dataset entirely into RAM
```

---

# 🧠 M03-এ যেসব Python Tools Master করতে হবে

```text
String
├── strip
├── split
├── join
├── replace
├── find
├── count
├── startswith
└── endswith

Regex
├── search
├── match
├── findall
├── sub
├── split
└── compile

Collections
├── Counter
├── defaultdict
└── deque

Itertools
├── chain
├── count
├── cycle
├── repeat
├── islice
├── product
├── combinations
└── permutations

Functools
├── reduce
├── partial
├── lru_cache
└── wraps

Datetime
├── datetime
├── date
├── timedelta
├── strftime
└── strptime

OS
├── getcwd
├── listdir
└── getenv

Pathlib
├── Path
├── exists
├── mkdir
├── glob
├── rglob
├── rename
└── unlink

Shutil
├── copy
├── copytree
├── move
└── rmtree
```

---

# 📝 M03 Theory Questions

নিজে answer করার চেষ্টা করবে:

1. Data processing কী?
2. Extract, Transform, Filter, Aggregate কী?
3. String immutable কেন?
4. `split()` এবং `join()` কীভাবে কাজ করে?
5. `strip()` কী করে?
6. `replace()` কী করে?
7. `find()` এবং `index()`-এর difference কী?
8. Regex কী?
9. `\d`, `\w`, `\s` কী?
10. `*`, `+`, `?` Regex-এ কী করে?
11. `re.findall()` কী করে?
12. `re.sub()` কী করে?
13. `re.compile()` কখন useful?
14. `sorted()` এবং `.sort()`-এর পার্থক্য কী?
15. `key=` parameter কী?
16. `any()` এবং `all()` কী?
17. `Counter` কী?
18. `defaultdict` কেন useful?
19. `deque` কী?
20. `itertools` কেন ব্যবহার করা হয়?
21. `chain()` কী?
22. `islice()` কী?
23. `combinations()` এবং `permutations()` difference কী?
24. `reduce()` কী?
25. `partial()` কী?
26. `lru_cache()` কী?
27. `datetime` কেন দরকার?
28. Naive এবং timezone-aware datetime কী?
29. Environment variable কী?
30. `.env` কেন ব্যবহার করা হয়?
31. `pathlib` কেন useful?
32. `glob()` এবং `rglob()` কী?
33. `shutil` কী কাজে লাগে?
34. Generator বড় dataset-এর জন্য কেন useful?
35. Batch processing কী?
36. Data leakage কী?
37. Duplicate data কেন remove করা দরকার?
38. Dataset statistics কেন দরকার?
39. Memory-efficient processing কী?
40. AI/NLP data pipeline কী?

---

# 🎯 M03 Practice Levels

## Level 1 — Basic

```text
[ ] 10টি string clean করা
[ ] lowercase করা
[ ] whitespace normalize করা
[ ] split/join ব্যবহার
[ ] word count করা
[ ] character count করা
```

## Level 2 — Intermediate

```text
[ ] Regex দিয়ে number extract
[ ] Regex দিয়ে URL remove
[ ] Counter দিয়ে frequency
[ ] defaultdict দিয়ে grouping
[ ] sorted দিয়ে score ranking
[ ] pathlib দিয়ে files search
```

## Level 3 — Advanced

```text
[ ] JSONL generator
[ ] batch processor
[ ] duplicate detection
[ ] validation pipeline
[ ] statistics generator
[ ] large dataset processing
```

## Level 4 — AI Project

```text
[ ] Raw dataset
[ ] Validation
[ ] Cleaning
[ ] Transformation
[ ] Filtering
[ ] Deduplication
[ ] Statistics
[ ] JSONL output
[ ] Statistics report
```

---

# ✅ M03 Completion Checklist

```text
[ ] Data Processing fundamentals
[ ] String processing
[ ] String methods
[ ] String slicing
[ ] String immutability
[ ] Regex fundamentals
[ ] Regex patterns
[ ] Regex search
[ ] Regex findall
[ ] Regex substitution
[ ] Regex split
[ ] Regex compilation
[ ] Text cleaning
[ ] Sorting
[ ] Searching
[ ] any()
[ ] all()
[ ] min()
[ ] max()
[ ] sum()
[ ] Counter
[ ] defaultdict
[ ] deque
[ ] itertools
[ ] chain
[ ] count
[ ] cycle
[ ] repeat
[ ] islice
[ ] product
[ ] combinations
[ ] permutations
[ ] functools
[ ] reduce
[ ] partial
[ ] lru_cache
[ ] wraps
[ ] datetime
[ ] date
[ ] timedelta
[ ] strftime
[ ] strptime
[ ] timezone concept
[ ] os
[ ] environment variables
[ ] .env concept
[ ] pathlib
[ ] glob
[ ] rglob
[ ] shutil
[ ] CSV processing
[ ] JSON processing
[ ] JSONL processing
[ ] schema validation
[ ] data cleaning
[ ] duplicate detection
[ ] dataset statistics
[ ] batch processing
[ ] generator-based processing
[ ] memory-efficient processing
[ ] performance measurement
[ ] data pipeline architecture
[ ] AI/NLP dataset processor project
[ ] final challenge
```

---

# 🏆 M03 শেষে তোমার Skill Level

M03 শেষ করার পর তোমার mental model হবে:

```text
                 RAW DATA
                     ↓
              File / API / DB
                     ↓
                 LOAD DATA
                     ↓
                  PARSE
                     ↓
                VALIDATE
                     ↓
                  CLEAN
                     ↓
                TRANSFORM
                     ↓
                 FILTER
                     ↓
              DEDUPLICATE
                     ↓
                AGGREGATE
                     ↓
                STATISTICS
                     ↓
               SAVE JSONL
                     ↓
              AI / ML MODEL
```

এবং Python side:

```text
Python
 │
 ├── Data Structures
 ├── Functions
 ├── OOP
 ├── Generators
 ├── Exceptions
 ├── Modules
 ├── File Handling
 │
 └── Data Processing
       ├── Regex
       ├── Collections
       ├── itertools
       ├── functools
       ├── datetime
       ├── os
       ├── pathlib
       └── shutil
```

**M01 + M02 + M03 = Python-এর foundation থেকে real-world data-processing foundation পর্যন্ত।**

পরের ধাপে আমরা software-development environment ও engineering side-এ যাব—যেখানে **Git/GitHub, Linux/CLI, virtual environment, dependency management, project configuration, testing এবং code quality** ধাপে ধাপে আসবে।
