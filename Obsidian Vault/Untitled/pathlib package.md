অবশ্যই। এবার আমরা **Python `pathlib` module-এর complete course** করব—official documentation ভিত্তিক এবং practical project সহ।

[Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

`pathlib` শেখা তোমার জন্য খুব useful, কারণ **file/folder handling, automation, backend project, data science, ML dataset management**—সব জায়গায় path নিয়ে কাজ করতে হয়।

---

# 🐍 Python `pathlib` — Complete Course

## 📚 Course Roadmap

আমরা মোট **10 Days**-এ শেষ করব।

|Day|Topic|
|---|---|
|Day 1|`Path` কী + Basic path|
|Day 2|Current directory + Absolute/Relative path|
|Day 3|File/Folder check|
|Day 4|Create files & directories|
|Day 5|Read & Write files|
|Day 6|Directory traversal + `glob()`|
|Day 7|Rename, Move, Delete|
|Day 8|File metadata + Advanced path operations|
|Day 9|`pathlib` + `os` comparison + Automation|
|Day 10|Final File Manager Project + Revision|

---

# 🎯 `pathlib` কেন শিখবে?

আগে Python-এ path handling করতে অনেক সময়:

```python
import os

path = os.path.join("data", "images", "cat.jpg")
```

`pathlib`-এ:

```python
from pathlib import Path

path = Path("data") / "images" / "cat.jpg"
```

এটা অনেক বেশি readable।

---

# 🧠 `pathlib` কী?

`pathlib` হলো Python-এর standard library module যা **filesystem paths-এর সাথে object-orientedভাবে কাজ করার জন্য** তৈরি।

Basic:

```python
from pathlib import Path

path = Path("data")
```

এখানে `path` হলো একটি `Path` object।

---

# ⭐ Day 1 — `Path` Basics

## 1. Import

```python
from pathlib import Path
```

---

## 2. একটা Path তৈরি

```python
from pathlib import Path

path = Path("data")

print(path)
```

Output:

```text
data
```

---

## 3. File Path

```python
path = Path("data/images/cat.jpg")

print(path)
```

Output:

```text
data/images/cat.jpg
```

---

# 4. `/` Operator ⭐

`pathlib`-এর সবচেয়ে সুন্দর featureগুলোর একটি:

```python
from pathlib import Path

path = Path("data") / "images" / "cat.jpg"

print(path)
```

Output:

```text
data/images/cat.jpg
```

এটা:

```python
Path("data") / "images" / "cat.jpg"
```

নিজে থেকে proper path তৈরি করে।

---

# 5. Current Directory

```python
from pathlib import Path

path = Path.cwd()

print(path)
```

`cwd()` = **current working directory**

যেমন:

```text
/home/atiar/python-project
```

---

# 6. Home Directory

```python
from pathlib import Path

home = Path.home()

print(home)
```

Linux-এ এরকম হতে পারে:

```text
/home/atiar
```

---

# 7. Absolute Path

```python
from pathlib import Path

path = Path("/home/atiar/project/data.txt")

print(path.is_absolute())
```

Output:

```text
True
```

---

# 8. Relative Path

```python
from pathlib import Path

path = Path("data/data.txt")

print(path.is_absolute())
```

Output:

```text
False
```

---

# 🧠 Absolute vs Relative

```text
Absolute:

/home/atiar/project/data.txt
↑
Root থেকে পুরো location


Relative:

data/data.txt
↑
Current directory থেকে location
```

---

# 9. `resolve()`

Relative path-এর absolute version দেখতে:

```python
from pathlib import Path

path = Path("data/file.txt")

print(path.resolve())
```

যেমন:

```text
/home/atiar/project/data/file.txt
```

---

# 10. Path Parts ⭐

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print(path.parts)
```

Output-এর মতো:

```python
('data', 'images', 'cat.jpg')
```

Path-কে individual components হিসেবে পাওয়া যায়।

---

# 11. `name`

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print(path.name)
```

Output:

```text
cat.jpg
```

---

# 12. `stem`

Extension বাদ দিয়ে filename:

```python
print(path.stem)
```

Output:

```text
cat
```

---

# 13. `suffix`

File extension:

```python
print(path.suffix)
```

Output:

```text
.jpg
```

---

# 14. `parent`

Parent directory:

```python
print(path.parent)
```

Output:

```text
data/images
```

---

# 🔥 সবগুলো একসাথে

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print("Path:", path)
print("Name:", path.name)
print("Stem:", path.stem)
print("Suffix:", path.suffix)
print("Parent:", path.parent)
print("Parts:", path.parts)
print("Absolute:", path.is_absolute())
```

---

# 🧪 Day 1 Practice

এই path:

```python
Path("projects/python/data/train/images/cat.jpg")
```

এর:

1. `name`
    
2. `stem`
    
3. `suffix`
    
4. `parent`
    
5. `parts`
    

নিজে বের করো।

Expected:

```text
name   → cat.jpg
stem   → cat
suffix → .jpg
parent → projects/python/data/train/images
```

---

# 🏆 Day 1 Mini Project

একটি program বানাও:

```text
Path Analyzer
```

Input:

```python
path = Path("dataset/train/images/cat001.jpg")
```

Output:

```text
==============================
       PATH ANALYZER
==============================

Path: dataset/train/images/cat001.jpg

Name: cat001.jpg
Stem: cat001
Extension: .jpg

Parent:
dataset/train/images

Absolute: False

Parts:
dataset
train
images
cat001.jpg
```

তুমি ব্যবহার করবে:

```python
Path()
Path.cwd()
Path.home()
Path.resolve()
Path.parts
Path.name
Path.stem
Path.suffix
Path.parent
Path.is_absolute()
```

---

# 🎯 Day 1-এর Must Know

আজ শুধু এগুলো ভালোভাবে practice করো:

```python
from pathlib import Path

Path()

Path.cwd()
Path.home()

path / "file.txt"

path.resolve()

path.parts
path.name
path.stem
path.suffix
path.parent

path.is_absolute()
```

**পরের Day 2-এ আমরা `Path.exists()`, `is_file()`, `is_dir()`, `is_symlink()` এবং filesystem-এর মধ্যে কোনো path আসলে আছে কিনা সেটা check করা শিখব।**


# 🐍 Python `pathlib` — Day 2

আজ আমরা শিখব **কোনো file/folder সত্যিই আছে কিনা এবং সেটা file নাকি directory** সেটা check করা।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

## 🎯 আজকের Topics

```text
Path.exists()
Path.is_file()
Path.is_dir()
Path.is_symlink()
Path.is_absolute()
Path.resolve()
```

Day 1-এর path basics-এর উপর এগুলো ব্যবহার করব।

---

# 1️⃣ `Path.exists()` ⭐⭐⭐

কোনো path filesystem-এ আছে কিনা check করতে:

```python
from pathlib import Path

path = Path("data")

print(path.exists())
```

যদি `data` folder থাকে:

```text
True
```

না থাকলে:

```text
False
```

### Mental Model

```text
Path
 ↓
exists()?
 ↓
YES → True
NO  → False
```

---

# 2️⃣ File আছে কিনা

ধরো:

```text
project/
└── data.txt
```

Code:

```python
from pathlib import Path

path = Path("data.txt")

print(path.exists())
```

Output:

```text
True
```

---

# 3️⃣ `Path.is_file()` ⭐⭐⭐

Path-টি **regular file** কিনা check করতে:

```python
from pathlib import Path

path = Path("data.txt")

print(path.is_file())
```

Output:

```text
True
```

কিন্তু path যদি folder হয়:

```python
path = Path("data")
print(path.is_file())
```

Output:

```text
False
```

---

# 4️⃣ `Path.is_dir()` ⭐⭐⭐

Path-টি directory কিনা:

```python
from pathlib import Path

path = Path("data")

print(path.is_dir())
```

যদি `data` folder হয়:

```text
True
```

---

# 5️⃣ `exists()` বনাম `is_file()` বনাম `is_dir()`

এটা খুব ভালোভাবে বুঝো:

|Method|কী check করে|
|---|---|
|`exists()`|path আছে কিনা|
|`is_file()`|path file কিনা|
|`is_dir()`|path directory কিনা|

ধরো:

```text
project/
├── data/
└── data.txt
```

তাহলে:

```python
Path("data").exists()
```

→ `True`

```python
Path("data").is_dir()
```

→ `True`

```python
Path("data").is_file()
```

→ `False`

আর:

```python
Path("data.txt").exists()
```

→ `True`

```python
Path("data.txt").is_file()
```

→ `True`

```python
Path("data.txt").is_dir()
```

→ `False`

---

# 6️⃣ Practical Validation ⭐

ধরো user একটা path দিয়েছে:

```python
from pathlib import Path

path = Path("data.txt")

if not path.exists():
    print("Path does not exist")

elif path.is_file():
    print("This is a file")

elif path.is_dir():
    print("This is a directory")
```

এটা real-world application-এ অনেক useful।

---

# 7️⃣ `is_symlink()`

Linux-এ symbolic link থাকতে পারে।

Check করতে:

```python
from pathlib import Path

path = Path("my_link")

print(path.is_symlink())
```

Symbolic link হলে:

```text
True
```

না হলে:

```text
False
```

### Symbolic link কী?

সহজভাবে:

```text
real_file.txt
      ↑
      │
   symlink
      ↑
   my_link
```

`my_link` আসল file নয়; অন্য path-এর দিকে reference করে।

এটা Linux এবং system administration-এর ক্ষেত্রে বেশি দেখা যায়।

---

# 8️⃣ `is_absolute()`

Day 1-এ দেখেছিলাম:

```python
from pathlib import Path

path = Path("/home/user/file.txt")

print(path.is_absolute())
```

Output:

```text
True
```

Relative:

```python
path = Path("data/file.txt")

print(path.is_absolute())
```

Output:

```text
False
```

---

# 9️⃣ `resolve()`

Relative path-কে resolved absolute path হিসেবে দেখতে:

```python
from pathlib import Path

path = Path("data/file.txt")

print(path.resolve())
```

Output-এর মতো:

```text
/home/user/project/data/file.txt
```

---

# 🔥 10️⃣ `resolve()` + `exists()`

একসাথে:

```python
from pathlib import Path

path = Path("data/file.txt")

print("Original:", path)
print("Resolved:", path.resolve())
print("Exists:", path.exists())
```

Output:

```text
Original: data/file.txt
Resolved: /home/user/project/data/file.txt
Exists: True
```

---

# 1️⃣1️⃣ File Checker বানাই

এখন একটা reusable function:

```python
from pathlib import Path


def check_path(path):

    path = Path(path)

    if not path.exists():
        print("❌ Path does not exist")
        return

    if path.is_file():
        print("📄 This is a file")

    elif path.is_dir():
        print("📁 This is a directory")


check_path("data")
```

---

# 1️⃣2️⃣ User Input দিয়ে

```python
from pathlib import Path


path = input("Enter path: ")

path = Path(path)

if not path.exists():

    print("Path does not exist")

elif path.is_file():

    print("File found")

elif path.is_dir():

    print("Directory found")
```

এখন terminal-এ:

```bash
python app.py
```

তারপর:

```text
Enter path: data
```

Output:

```text
Directory found
```

---

# 1️⃣3️⃣ Extension Check

`pathlib` দিয়ে extension check-ও করা যায়।

```python
from pathlib import Path

path = Path("photo.jpg")

if path.suffix == ".jpg":
    print("JPEG image")
```

আর:

```python
if path.suffix in [".jpg", ".jpeg", ".png"]:
    print("Image file")
```

---

# 🔥 1️⃣4️⃣ Real-world File Validation

ধরো ML project-এ dataset image নেওয়া হচ্ছে।

```python
from pathlib import Path


def validate_image(path):

    path = Path(path)

    if not path.exists():
        print("File does not exist")
        return False

    if not path.is_file():
        print("This is not a file")
        return False

    if path.suffix.lower() not in [".jpg", ".jpeg", ".png"]:
        print("Unsupported image format")
        return False

    print("Valid image:", path)
    return True
```

Use:

```python
validate_image("cat.jpg")
```

এটা তোমার ML/data processing কাজেও useful হবে।

---

# 🧪 Day 2 Practice

তোমার project folder-এ এই structure বানাও:

```text
pathlib_practice/
│
├── data/
│
├── images/
│
└── test.txt
```

তারপর এই code চালাও:

```python
from pathlib import Path

paths = [
    Path("data"),
    Path("images"),
    Path("test.txt"),
    Path("unknown.txt")
]

for path in paths:

    print("\nPath:", path)
    print("Exists:", path.exists())
    print("File:", path.is_file())
    print("Directory:", path.is_dir())
```

Expected concept:

```text
data
Exists: True
File: False
Directory: True

test.txt
Exists: True
File: True
Directory: False

unknown.txt
Exists: False
File: False
Directory: False
```

---

# 🧪 Exercise 2

একটা function বানাও:

```python
check_file("test.txt")
```

যদি file থাকে:

```text
File exists
```

না থাকলে:

```text
File not found
```

---

# 🧪 Exercise 3 ⭐

একটা function বানাও:

```python
check_directory("data")
```

যদি directory হয়:

```text
Directory exists
```

না হলে:

```text
Directory not found
```

---

# 🏆 Day 2 Mini Project — Path Validator

একটি program বানাও:

```text
================================
       PATH VALIDATOR
================================

Enter path: dataset/train

Exists      : Yes
Type        : Directory
Absolute    : No
Resolved    : /home/user/project/dataset/train
```

যদি:

```text
Enter path: unknown.txt
```

তাহলে:

```text
Exists      : No
```

### ব্যবহার করবে:

```python
Path.exists()
Path.is_file()
Path.is_dir()
Path.is_absolute()
Path.resolve()
```

---

# 🧠 Day 2 Mental Model

```text
                 Path
                   │
             Does it exist?
              /          \
            NO            YES
            │              │
          False       File or Directory?
                         /       \
                       File      Dir
                        │         │
                    is_file()  is_dir()
```

---

# ⭐ আজকের Must Know

এই ৫টা অবশ্যই ভালোভাবে practice করো:

```python
path.exists()
path.is_file()
path.is_dir()
path.is_absolute()
path.resolve()
```

আর মনে রাখবে:

```text
exists()
    ↓
path আছে কিনা

is_file()
    ↓
regular file কিনা

is_dir()
    ↓
directory কিনা
```

### 📚 Progress

```text
Day 1 → Path basics                         ✅
Day 2 → Check file/directory/existence      ✅
Day 3 → Create files & directories          ⏭️
Day 4 → Read/write files
Day 5 → Directory traversal
Day 6 → glob/rglob
Day 7 → Rename/move/delete
Day 8 → Metadata & advanced operations
Day 9 → pathlib + os + automation
Day 10 → Final project
```


# 🐍 Python `pathlib` — Day 3

## 📁 Create Files & Directories

আজ আমরা শিখব `pathlib` দিয়ে **file এবং folder তৈরি করা**।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

## 🎯 আজকের Topics

```text
Path.mkdir()
Path.touch()
Path.parent
Path.mkdir(parents=True)
Path.mkdir(exist_ok=True)
```

---

# 1️⃣ `Path.mkdir()` — Folder তৈরি

```python
from pathlib import Path

path = Path("data")

path.mkdir()
```

এতে:

```text
project/
└── data/
```

folder তৈরি হবে।

---

# 2️⃣ Folder তৈরি করার আগে Check

যদি folder আগে থেকেই থাকে:

```python
from pathlib import Path

path = Path("data")

if not path.exists():
    path.mkdir()
```

এটা safe approach।

---

# 3️⃣ `exist_ok=True` ⭐⭐⭐

আরও সহজভাবে:

```python
from pathlib import Path

path = Path("data")

path.mkdir(exist_ok=True)
```

যদি `data` না থাকে → তৈরি করবে।

যদি আগে থেকেই থাকে → error করবে না।

```text
data নেই
   ↓
mkdir()
   ↓
data তৈরি

data আছে
   ↓
exist_ok=True
   ↓
কিছু হবে না
```

---

# 4️⃣ `parents=True` ⭐⭐⭐

ধরো তুমি তৈরি করতে চাও:

```text
project/
└── data/
    └── images/
        └── train/
```

একবারে:

```python
from pathlib import Path

path = Path("data/images/train")

path.mkdir(parents=True)
```

এতে প্রয়োজন হলে:

```text
data/
└── images/
    └── train/
```

সব directory তৈরি হবে।

---

# 5️⃣ `parents=True + exist_ok=True` ⭐⭐⭐

Real-world code-এ এই combination অনেক useful:

```python
from pathlib import Path

path = Path("data/images/train")

path.mkdir(
    parents=True,
    exist_ok=True
)
```

এর মানে:

> প্রয়োজনীয় parent directories তৈরি করো, আর directory আগে থেকেই থাকলে error দিও না।

---

# 6️⃣ `Path.touch()` — Empty File তৈরি

File তৈরি করতে:

```python
from pathlib import Path

path = Path("data.txt")

path.touch()
```

তাহলে:

```text
project/
└── data.txt
```

তৈরি হবে।

File-এর ভিতরে কিছু থাকবে না।

---

# 7️⃣ Folder-এর ভিতরে File

```python
from pathlib import Path

folder = Path("data")

folder.mkdir(exist_ok=True)

file = folder / "data.txt"

file.touch()
```

Result:

```text
project/
└── data/
    └── data.txt
```

এখানে `pathlib`-এর `/` operator খুব useful:

```python
folder / "data.txt"
```

---

# 8️⃣ Nested Folder + File ⭐

```python
from pathlib import Path

folder = Path("dataset/train/images")

folder.mkdir(
    parents=True,
    exist_ok=True
)

file = folder / "image001.txt"

file.touch()
```

Result:

```text
dataset/
└── train/
    └── images/
        └── image001.txt
```

এটা ML/data project-এ খুব useful pattern।

---

# 9️⃣ `touch()`-এ `exist_ok`

যদি file already থাকে:

```python
path.touch()
```

সাধারণভাবে existing file-এর ক্ষেত্রে error না দিয়ে কাজ করতে পারে; `touch()`-এর behavior options দিয়ে control করা যায়।

Explicitly:

```python
path.touch(exist_ok=True)
```

ব্যবহার করতে পারো।

---

# 🔟 File Create + Content

`touch()` দিয়ে empty file তৈরি করা যায়।

কিন্তু content লিখতে:

```python
from pathlib import Path

path = Path("data.txt")

path.write_text("Hello Python")
```

এতে file তৈরি হবে এবং:

```text
Hello Python
```

লিখে দেবে।

⚠️ `write_text()` যদি existing file-এ ব্যবহার করো, defaultভাবে পুরোনো content replace করে।

---

# 1️⃣1️⃣ `write_text()` Example

```python
from pathlib import Path

path = Path("message.txt")

path.write_text(
    "Hello!\n"
    "I am learning pathlib."
)
```

File:

```text
Hello!
I am learning pathlib.
```

---

# 1️⃣2️⃣ `read_text()`

যেহেতু আমরা file তৈরি করেছি, এখন read করতে পারি:

```python
from pathlib import Path

path = Path("message.txt")

print(path.read_text())
```

Output:

```text
Hello!
I am learning pathlib.
```

আজকের মূল topic create হলেও `read_text()`-এর basic idea এখন থেকেই বুঝে রাখো। পরে dedicated lesson-এ file I/O বিস্তারিত করব।

---

# 1️⃣3️⃣ `Path.parent` দিয়ে Parent Folder তৈরি

ধরো:

```python
from pathlib import Path

file = Path("data/images/train/cat.txt")
```

Parent:

```python
print(file.parent)
```

Output:

```text
data/images/train
```

এখন:

```python
file.parent.mkdir(
    parents=True,
    exist_ok=True
)

file.touch()
```

Result:

```text
data/
└── images/
    └── train/
        └── cat.txt
```

---

# 🔥 14️⃣ Practical Function — Create Folder

```python
from pathlib import Path


def create_directory(path):

    path = Path(path)

    path.mkdir(
        parents=True,
        exist_ok=True
    )

    print("Directory ready:", path)


create_directory("data/images/train")
```

---

# 🔥 15️⃣ Practical Function — Create File

```python
from pathlib import Path


def create_file(path):

    path = Path(path)

    path.parent.mkdir(
        parents=True,
        exist_ok=True
    )

    path.touch(
        exist_ok=True
    )

    print("File ready:", path)


create_file("data/images/train/info.txt")
```

এটা খুব useful pattern।

---

# 🧠 `mkdir()` বনাম `touch()`

এটা অবশ্যই মনে রাখবে:

```text
mkdir()
   ↓
Directory / Folder তৈরি

touch()
   ↓
File তৈরি
```

Example:

```python
Path("data").mkdir()
```

→ folder

```python
Path("data.txt").touch()
```

→ file

---

# 🧪 Day 3 Practice

এই structure তৈরি করো:

```text
pathlib_practice/
│
├── dataset/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   │
│   └── test/
│       ├── images/
│       └── labels/
│
└── logs/
```

একটি Python program দিয়ে সবগুলো তৈরি করবে।

Hint:

```python
from pathlib import Path

folders = [
    "dataset/train/images",
    "dataset/train/labels",
    "dataset/test/images",
    "dataset/test/labels",
    "logs"
]

for folder in folders:
    Path(folder).mkdir(
        parents=True,
        exist_ok=True
    )
```

---

# 🧪 Exercise 2

এই file structure তৈরি করো:

```text
project/
├── data/
│   └── raw/
│       └── dataset.csv
│
├── logs/
│   └── app.log
│
└── config/
    └── settings.txt
```

শুধু `pathlib` ব্যবহার করবে।

---

# 🏆 Day 3 Mini Project — Project Structure Generator

একটি program বানাও:

```python
from pathlib import Path
```

যেটা run করলে automatically:

```text
my_project/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── src/
│
├── tests/
│
├── logs/
│
└── README.md
```

তৈরি করবে।

একটি ভালো implementation:

```python
from pathlib import Path


root = Path("my_project")

folders = [
    "data/raw",
    "data/processed",
    "src",
    "tests",
    "logs"
]

for folder in folders:

    path = root / folder

    path.mkdir(
        parents=True,
        exist_ok=True
    )


readme = root / "README.md"

readme.touch(
    exist_ok=True
)

print("Project structure created!")
```

---

# ⭐ Day 3 Must Know

আজ এইগুলো ভালোভাবে practice করো:

```python
Path.mkdir()
Path.touch()

Path.mkdir(
    parents=True,
    exist_ok=True
)

path.parent
path / "file.txt"

path.write_text()
path.read_text()
```

সবচেয়ে গুরুত্বপূর্ণ mental model:

```text
                 pathlib
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       Directory             File
          │                   │
       mkdir()              touch()
          │                   │
          └───────┬───────────┘
                  ↓
             filesystem
```

### 📚 Course Progress

```text
Day 1 → Path Basics                    ✅
Day 2 → Check Path/File/Directory      ✅
Day 3 → Create File & Directory        ✅
Day 4 → Read & Write Files             ⏭️
Day 5 → Directory Traversal
Day 6 → glob() / rglob()
Day 7 → Rename / Move / Delete
Day 8 → Metadata & Advanced Operations
Day 9 → pathlib + os + Automation
Day 10 → Final File Manager Project
```


# 🐍 Python `pathlib` — Day 4

## 📖 Read & Write Files

আজ আমরা `pathlib` দিয়ে **file-এর ভিতরের data read, write, append এবং encoding** শিখব।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 আজকের Topics

```text
Path.read_text()
Path.write_text()
Path.open()
Path.read_bytes()
Path.write_bytes()
append mode
encoding
```

---

# 1️⃣ `write_text()` ⭐⭐⭐

একটি text file তৈরি করে content লেখার সবচেয়ে সহজ উপায়:

```python
from pathlib import Path

path = Path("hello.txt")

path.write_text("Hello Python!")
```

এতে:

```text
hello.txt
```

তৈরি হবে এবং ভিতরে থাকবে:

```text
Hello Python!
```

---

# 2️⃣ Existing File-এর Content Replace

ধরো:

```text
hello.txt

Hello Python!
```

এখন:

```python
path.write_text("Hello World!")
```

আগের content replace হয়ে যাবে:

```text
Hello World!
```

⚠️ তাই `write_text()` ব্যবহার করার সময় বুঝে ব্যবহার করবে।

---

# 3️⃣ `read_text()` ⭐⭐⭐

File-এর পুরো text পড়তে:

```python
from pathlib import Path

path = Path("hello.txt")

content = path.read_text()

print(content)
```

Output:

```text
Hello World!
```

---

# 4️⃣ Write → Read

একসাথে:

```python
from pathlib import Path

path = Path("message.txt")

path.write_text("I am learning pathlib.")

content = path.read_text()

print(content)
```

Output:

```text
I am learning pathlib.
```

---

# 5️⃣ Newline `\n`

Multiple lines লিখতে:

```python
from pathlib import Path

path = Path("notes.txt")

path.write_text(
    "Python\n"
    "Pathlib\n"
    "Automation"
)
```

File:

```text
Python
Pathlib
Automation
```

---

# 6️⃣ List থেকে Text তৈরি

```python
from pathlib import Path

lines = [
    "Python",
    "Django",
    "React",
    "Pathlib"
]

path = Path("skills.txt")

path.write_text("\n".join(lines))
```

File:

```text
Python
Django
React
Pathlib
```

---

# 7️⃣ File Read করে Lines পাওয়া

```python
from pathlib import Path

path = Path("skills.txt")

content = path.read_text()

lines = content.splitlines()

print(lines)
```

Output:

```python
['Python', 'Django', 'React', 'Pathlib']
```

তারপর:

```python
for line in lines:
    print(line)
```

Output:

```text
Python
Django
React
Pathlib
```

---

# 8️⃣ `encoding` ⭐⭐⭐

বাংলা বা অন্য Unicode text নিয়ে কাজ করলে encoding explicitly দেওয়া ভালো।

```python
from pathlib import Path

path = Path("bangla.txt")

path.write_text(
    "আমি Python শিখছি।",
    encoding="utf-8"
)
```

Read:

```python
content = path.read_text(
    encoding="utf-8"
)

print(content)
```

Output:

```text
আমি Python শিখছি।
```

### সাধারণ rule:

```python
encoding="utf-8"
```

text file-এর জন্য একটি ভালো default choice।

---

# 9️⃣ Append করা

`write_text()` পুরোনো content replace করে।

কিন্তু আমাদের যদি পুরোনো content রেখে নতুন content যোগ করতে হয়?

তাহলে `open()` ব্যবহার করব।

```python
from pathlib import Path

path = Path("log.txt")

with path.open("a", encoding="utf-8") as file:
    file.write("First log\n")
    file.write("Second log\n")
```

`"a"` = append mode।

---

# 🔟 `open()` Modes

সবচেয়ে গুরুত্বপূর্ণ modes:

|Mode|কাজ|
|---|---|
|`"r"`|Read|
|`"w"`|Write / replace|
|`"a"`|Append|
|`"x"`|নতুন file তৈরি; আগে থাকলে error|
|`"rb"`|Binary read|
|`"wb"`|Binary write|

---

# 1️⃣1️⃣ Read using `open()`

```python
from pathlib import Path

path = Path("hello.txt")

with path.open("r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

---

# 1️⃣2️⃣ `with` কেন ব্যবহার করি?

```python
with path.open(...) as file:
    ...
```

এভাবে file ব্যবহার করলে block শেষ হওয়ার পর file properly close করার ব্যবস্থা Python করে।

তাই সাধারণত:

```python
with path.open(...) as file:
```

pattern ব্যবহার করাই ভালো।

---

# 1️⃣3️⃣ `readline()`

একবারে একটি line:

```python
from pathlib import Path

path = Path("notes.txt")

with path.open("r", encoding="utf-8") as file:

    print(file.readline())
    print(file.readline())
```

যদি file:

```text
Python
Django
React
```

হয়, তাহলে প্রথম দুই line পাওয়া যাবে।

---

# 1️⃣4️⃣ `readlines()`

সব line list হিসেবে:

```python
from pathlib import Path

path = Path("notes.txt")

with path.open("r", encoding="utf-8") as file:

    lines = file.readlines()

print(lines)
```

Output:

```python
['Python\n', 'Django\n', 'React\n']
```

---

# 1️⃣5️⃣ বড় File হলে ⭐

ধরো 1GB file।

এভাবে:

```python
content = path.read_text()
```

পুরো file memory-তে load করার চেষ্টা করবে।

বড় file-এর ক্ষেত্রে line-by-line process করা ভালো:

```python
from pathlib import Path

path = Path("large.txt")

with path.open("r", encoding="utf-8") as file:

    for line in file:
        print(line.strip())
```

এটা large text files-এর জন্য বেশি memory-efficient approach।

---

# 1️⃣6️⃣ Binary File

সব file text নয়।

যেমন:

```text
image.jpg
video.mp4
model.pth
pdf
```

এগুলোর জন্য binary mode দরকার হতে পারে।

### Read bytes:

```python
from pathlib import Path

path = Path("image.jpg")

data = path.read_bytes()

print(len(data))
```

এখানে `data` হবে:

```python
bytes
```

---

# 1️⃣7️⃣ Write Bytes

```python
from pathlib import Path

path = Path("data.bin")

path.write_bytes(b"Hello")
```

এখানে:

```python
b"Hello"
```

হলো bytes literal।

---

# 1️⃣8️⃣ `read_text()` বনাম `read_bytes()`

```text
Text file
   ↓
read_text()
   ↓
str
```

আর:

```text
Binary file
   ↓
read_bytes()
   ↓
bytes
```

---

# 🔥 1️⃣9️⃣ Practical Project — Notes Manager

এখন একটি ছোট Notes Manager বানাই।

```python
from pathlib import Path

notes = Path("notes.txt")


def add_note(text):

    with notes.open("a", encoding="utf-8") as file:
        file.write(text + "\n")


def show_notes():

    if not notes.exists():
        print("No notes found.")
        return

    content = notes.read_text(
        encoding="utf-8"
    )

    print(content)


add_note("Learn pathlib")
add_note("Practice Python")
add_note("Build automation project")

show_notes()
```

Output:

```text
Learn pathlib
Practice Python
Build automation project
```

---

# 🔥 20️⃣ Better Notes Manager

User input নাও:

```python
from pathlib import Path

notes = Path("notes.txt")


def add_note():

    text = input("Enter note: ")

    with notes.open("a", encoding="utf-8") as file:
        file.write(text + "\n")

    print("Note added!")


def show_notes():

    if not notes.exists():
        print("No notes found.")
        return

    print("\nYour Notes:")

    with notes.open("r", encoding="utf-8") as file:

        for number, line in enumerate(file, start=1):

            print(
                f"{number}. {line.strip()}"
            )


while True:

    print("\n1. Add note")
    print("2. Show notes")
    print("3. Exit")

    choice = input("Choose: ")

    if choice == "1":
        add_note()

    elif choice == "2":
        show_notes()

    elif choice == "3":
        break

    else:
        print("Invalid choice")
```

এখানে আমরা ব্যবহার করলাম:

```text
Path.exists()
Path.open()
read
append
encoding
```

---

# 🧪 Day 4 Practice

## Exercise 1

এই file তৈরি করো:

```text
student.txt
```

Content:

```text
Name: Atiar
Department: CSE
Skill: Python
```

ব্যবহার করবে:

```python
Path.write_text()
```

---

## Exercise 2

`student.txt` read করে print করো:

```python
Path.read_text()
```

---

## Exercise 3

আরেকটি line append করো:

```text
Goal: Software Engineer
```

ব্যবহার করবে:

```python
path.open("a")
```

---

## Exercise 4 ⭐

একটি `students.txt` file বানাও:

```text
Rahim
Karim
Atiar
Hasan
```

Python দিয়ে read করে:

```text
1. Rahim
2. Karim
3. Atiar
4. Hasan
```

print করো।

Hint:

```python
for number, line in enumerate(lines, start=1):
    ...
```

---

# 🏆 Day 4 Mini Project — Simple File Editor

Program:

```text
================================
        FILE EDITOR
================================

1. Create/Write File
2. Read File
3. Append File
4. Exit
```

### Option 1

User filename এবং content দেবে:

```text
Filename: notes.txt
Content: Learning pathlib
```

### Option 2

File read করবে।

### Option 3

Existing file-এর শেষে content যোগ করবে।

### Option 4

Program বন্ধ করবে।

---

# 🧠 আজকের Mental Model

```text
                 pathlib
                    │
                  File
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
    Write          Read        Append
       │            │            │
write_text()   read_text()   open("a")
       │            │            │
       └────────────┴────────────┘
                    ↓
                File I/O
```

আর binary:

```text
Text
 ↓
read_text() / write_text()

Binary
 ↓
read_bytes() / write_bytes()
```

---

# ⭐ Day 4 Must Know

আজ এগুলো ভালোভাবে practice করো:

```python
path.read_text()

path.write_text(
    "Hello",
    encoding="utf-8"
)

path.read_bytes()

path.write_bytes(data)

path.open("r", encoding="utf-8")

path.open("a", encoding="utf-8")
```

### সবচেয়ে গুরুত্বপূর্ণ:

```text
write_text()
    ↓
পুরো text replace করে লিখে

read_text()
    ↓
পুরো text পড়ে

open("a")
    ↓
পুরোনো content রেখে নতুন content যোগ করে
```

---

## 📚 Course Progress

```text
Day 1 → Path Basics                    ✅
Day 2 → Check Path/File/Directory      ✅
Day 3 → Create File & Directory        ✅
Day 4 → Read & Write Files             ✅
Day 5 → Directory Traversal            ⏭️
Day 6 → glob() / rglob()
Day 7 → Rename / Move / Delete
Day 8 → Metadata & Advanced Operations
Day 9 → pathlib + os + Automation
Day 10 → Final File Manager Project
```

**Day 5-এ আমরা directory-এর ভিতরের files/folders বের করা—`iterdir()`, `glob()` এবং `rglob()`—শিখব।**


# 🐍 Python `pathlib` — Day 5

## 📂 Directory Traversal — `iterdir()`, `glob()`, `rglob()`

আজ আমরা শিখব একটি folder-এর ভিতরের **সব file ও folder খুঁজে বের করা**।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 আজকের Topics

```text
Path.iterdir()
Path.glob()
Path.rglob()
```

এগুলো `pathlib`-এর সবচেয়ে গুরুত্বপূর্ণ practical features-এর মধ্যে পড়ে।

---

# 1️⃣ `iterdir()` ⭐⭐⭐

একটি directory-এর immediate children দেখতে:

```python
from pathlib import Path

path = Path("data")

for item in path.iterdir():
    print(item)
```

ধরো:

```text
data/
├── train/
├── test/
├── data.csv
└── README.md
```

Output:

```text
data/train
data/test
data/data.csv
data/README.md
```

### গুরুত্বপূর্ণ

`iterdir()` শুধু **সরাসরি ভিতরের items** দেখায়।

এটা নিজে থেকে `train/`-এর ভিতরে ঢুকবে না।

---

# 2️⃣ File নাকি Folder?

`iterdir()`-এর সাথে Day 2-এর methods ব্যবহার করতে পারো:

```python
from pathlib import Path

path = Path("data")

for item in path.iterdir():

    if item.is_file():
        print("FILE:", item)

    elif item.is_dir():
        print("DIR :", item)
```

Output:

```text
DIR : data/train
DIR : data/test
FILE: data/data.csv
FILE: data/README.md
```

---

# 3️⃣ শুধু Files ⭐⭐⭐

```python
from pathlib import Path

path = Path("data")

for item in path.iterdir():

    if item.is_file():
        print(item)
```

এতে শুধু files আসবে।

---

# 4️⃣ শুধু Directories

```python
from pathlib import Path

path = Path("data")

for item in path.iterdir():

    if item.is_dir():
        print(item)
```

---

# 5️⃣ `glob()` ⭐⭐⭐

এখন আসি সবচেয়ে গুরুত্বপূর্ণ অংশে।

ধরো:

```text
data/
├── cat.jpg
├── dog.jpg
├── car.png
├── tree.png
└── data.txt
```

তুমি শুধু `.jpg` files চাও।

```python
from pathlib import Path

path = Path("data")

for file in path.glob("*.jpg"):
    print(file)
```

Output:

```text
data/cat.jpg
data/dog.jpg
```

---

# 6️⃣ `*.png`

```python
for file in path.glob("*.png"):
    print(file)
```

Output:

```text
data/car.png
data/tree.png
```

---

# 7️⃣ `*.txt`

```python
for file in path.glob("*.txt"):
    print(file)
```

Output:

```text
data/data.txt
```

---

# 8️⃣ সব files

```python
for item in path.glob("*"):
    print(item)
```

এতে directory-এর immediate children পাওয়া যাবে।

তবে `glob("*")` file এবং directory—দুটোই দিতে পারে।

শুধু files:

```python
for item in path.glob("*"):
    if item.is_file():
        print(item)
```

---

# 9️⃣ `glob()` Pattern বুঝো

```text
*.jpg
```

মানে:

> যেকোনো filename যার extension `.jpg`

Examples:

```text
cat.jpg       ✅
dog.jpg       ✅
photo.jpg     ✅
cat.png       ❌
```

---

# 🔟 `file_*.txt`

ধরো:

```text
data/
├── file_1.txt
├── file_2.txt
├── file_3.txt
├── test.txt
└── data.txt
```

Code:

```python
for file in path.glob("file_*.txt"):
    print(file)
```

Output:

```text
data/file_1.txt
data/file_2.txt
data/file_3.txt
```

---

# 1️⃣1️⃣ `rglob()` ⭐⭐⭐

এখন সবচেয়ে গুরুত্বপূর্ণ পার্থক্য।

`glob()` সাধারণভাবে একটি directory level-এর matching items খুঁজে।

কিন্তু `rglob()` **recursive search** করে—subdirectories-এর ভিতরেও যায়।

ধরো:

```text
dataset/
│
├── train/
│   ├── cat.jpg
│   └── dog.jpg
│
└── test/
    ├── cat.jpg
    └── car.jpg
```

Code:

```python
from pathlib import Path

dataset = Path("dataset")

for file in dataset.rglob("*.jpg"):
    print(file)
```

Output:

```text
dataset/train/cat.jpg
dataset/train/dog.jpg
dataset/test/cat.jpg
dataset/test/car.jpg
```

---

# 🔥 `glob()` vs `rglob()`

এটা খুব ভালোভাবে মনে রাখো:

```text
glob()
   ↓
বর্তমান directory-এর matching items

rglob()
   ↓
বর্তমান directory
      +
সব subdirectory
      +
তার subdirectory...
```

---

# 1️⃣2️⃣ ML Dataset Example ⭐⭐⭐

তোমার ML project-এর মতো dataset:

```text
dataset/
├── train/
│   ├── normal/
│   │   ├── 001.jpg
│   │   └── 002.jpg
│   │
│   └── robbery/
│       ├── 003.jpg
│       └── 004.jpg
│
└── test/
    ├── normal/
    │   └── 005.jpg
    │
    └── robbery/
        └── 006.jpg
```

সব image:

```python
from pathlib import Path

dataset = Path("dataset")

images = list(dataset.rglob("*.jpg"))

print("Total images:", len(images))
```

এটা ML preprocessing-এ খুব useful।

---

# 1️⃣3️⃣ Multiple Extensions

ধরো JPG এবং PNG দুটোই আছে।

```python
from pathlib import Path

path = Path("images")

images = []

for pattern in ["*.jpg", "*.png"]:

    images.extend(path.rglob(pattern))

print("Total images:", len(images))
```

---

# 1️⃣4️⃣ Case Sensitivity

কিছু filesystem/environment-এ:

```text
.jpg
.JPG
```

আলাদা হিসেবে ধরা হতে পারে।

তাই robust code-এর জন্য:

```python
from pathlib import Path

for file in Path("images").rglob("*"):

    if file.is_file() and file.suffix.lower() in {
        ".jpg",
        ".jpeg",
        ".png"
    }:
        print(file)
```

এখানে:

```python
file.suffix.lower()
```

ব্যবহার করে extension lowercase করা হয়েছে।

---

# 1️⃣5️⃣ `iterdir()` বনাম `glob()` বনাম `rglob()`

|Method|কাজ|
|---|---|
|`iterdir()`|Direct children সব দেখায়|
|`glob("*.jpg")`|Pattern matching করে|
|`rglob("*.jpg")`|Recursive pattern matching|

Mental model:

```text
iterdir()
   ↓
"ভিতরে কী আছে?"


glob("*.jpg")
   ↓
"এখানে কোন JPG আছে?"


rglob("*.jpg")
   ↓
"এই folder এবং তার সব subfolder-এ কোন JPG আছে?"
```

---

# 1️⃣6️⃣ `list()` কেন ব্যবহার করা হয়?

`glob()`, `rglob()`, `iterdir()` থেকে পাওয়া result-গুলোকে list-এ রাখতে পারো:

```python
from pathlib import Path

files = list(Path("data").rglob("*.jpg"))

print(files)
```

তারপর:

```python
print("Total:", len(files))
```

এটা dataset counting-এর জন্য useful।

---

# 1️⃣7️⃣ File Count

```python
from pathlib import Path

dataset = Path("dataset")

count = 0

for file in dataset.rglob("*"):

    if file.is_file():
        count += 1

print("Files:", count)
```

---

# 1️⃣8️⃣ Extension অনুযায়ী Count

```python
from pathlib import Path

dataset = Path("dataset")

jpg_count = 0
png_count = 0

for file in dataset.rglob("*"):

    if not file.is_file():
        continue

    if file.suffix.lower() == ".jpg":
        jpg_count += 1

    elif file.suffix.lower() == ".png":
        png_count += 1


print("JPG:", jpg_count)
print("PNG:", png_count)
```

---

# 🔥 1️⃣9️⃣ Practical Project — Image Finder

একটি reusable function:

```python
from pathlib import Path


def find_images(folder):

    folder = Path(folder)

    extensions = {
        ".jpg",
        ".jpeg",
        ".png",
        ".webp"
    }

    images = []

    for file in folder.rglob("*"):

        if file.is_file() and file.suffix.lower() in extensions:
            images.append(file)

    return images


images = find_images("dataset")

print("Total images:", len(images))

for image in images:
    print(image)
```

---

# 🧪 Day 5 Practice

## Exercise 1

এই structure বানাও:

```text
project/
├── data/
│   ├── train.txt
│   ├── test.txt
│   ├── image.jpg
│   └── image.png
│
└── logs/
    ├── app.log
    └── error.log
```

তারপর `iterdir()` দিয়ে সব items print করো।

---

## Exercise 2

শুধু `.txt` files বের করো:

```python
Path("project").glob("*.txt")
```

তারপর লক্ষ্য করো—`data/train.txt` কেন সরাসরি পাওয়া যাচ্ছে না।

---

## Exercise 3 ⭐

`rglob()` ব্যবহার করে project-এর সব `.txt` files বের করো:

```python
Path("project").rglob("*.txt")
```

---

## Exercise 4

সব image:

```text
.jpg
.jpeg
.png
```

খুঁজে বের করো।

---

# 🏆 Day 5 Mini Project — Dataset Analyzer

এই structure ধরে:

```text
dataset/
├── train/
│   ├── normal/
│   ├── robbery/
│   └── fight/
│
└── test/
    ├── normal/
    ├── robbery/
    └── fight/
```

Program লিখবে যেটা output দেবে:

```text
=============================
       DATASET ANALYZER
=============================

Total Images : 1200

JPG          : 800
PNG          : 400

Train Images : 1000
Test Images  : 200
```

### Hint

```python
train = Path("dataset/train")
test = Path("dataset/test")

train_images = list(train.rglob("*.jpg"))
test_images = list(test.rglob("*.jpg"))
```

তারপর `.png`-ও count করবে।

---

# 🧠 আজকের Core Concept

```text
                 Directory
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
      iterdir()    glob()     rglob()
          │          │           │
       সব item    pattern      recursive
                     │
                 "*.jpg"
                     │
                     ↓
                  JPG files
```

---

# ⭐ Day 5 Must Know

আজ অন্তত এগুলো নিজে হাতে 10–15 বার লিখবে:

```python
path.iterdir()

path.glob("*")

path.glob("*.jpg")

path.rglob("*")

path.rglob("*.jpg")
```

এবং অবশ্যই বুঝবে:

> **`iterdir()` = folder-এর direct contents দেখা**  
> **`glob()` = pattern দিয়ে search করা**  
> **`rglob()` = subfolder-সহ recursive search করা**

### 📚 Progress

```text
Day 1 → Path Basics                    ✅
Day 2 → Check Path/File/Directory      ✅
Day 3 → Create File & Directory        ✅
Day 4 → Read & Write Files             ✅
Day 5 → Directory Traversal            ✅
Day 6 → glob() / rglob() Advanced      ⏭️
Day 7 → Rename / Move / Delete
Day 8 → Metadata & Advanced Operations
Day 9 → pathlib + os + Automation
Day 10 → Final File Manager Project
```




# 🐍 Python `pathlib` — Day 6

## 🔎 `glob()` & `rglob()` Advanced

Day 5-এ আমরা `iterdir()`, `glob()` এবং `rglob()` এর basic শিখেছি। আজ এগুলো **ভালোভাবে ব্যবহার করে real-world file searching** করব।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 আজকের লক্ষ্য

আজ শেষে তুমি পারবে:

- নির্দিষ্ট extension-এর file খুঁজতে
    
- নির্দিষ্ট pattern-এর file খুঁজতে
    
- subdirectory সহ search করতে
    
- multiple extension search করতে
    
- hidden files নিয়ে কাজ করতে
    
- file count করতে
    
- dataset analyze করতে
    
- `glob()` বনাম `rglob()` সঠিকভাবে ব্যবহার করতে
    

---

# 1️⃣ `glob()` আবার বুঝি

ধরো:

```text
project/
├── data.txt
├── test.txt
├── image.jpg
└── image.png
```

```python
from pathlib import Path

path = Path("project")

for file in path.glob("*.txt"):
    print(file)
```

Output:

```text
project/data.txt
project/test.txt
```

---

# 2️⃣ `*` কী?

```python
*.txt
```

এখানে:

```text
*     → যেকোনো filename
.txt  → extension অবশ্যই .txt
```

তাই:

```text
hello.txt       ✅
data.txt        ✅
student.txt     ✅

hello.py        ❌
image.jpg       ❌
```

---

# 3️⃣ নির্দিষ্ট Filename Pattern

ধরো:

```text
data_1.csv
data_2.csv
data_3.csv
test.csv
```

```python
for file in Path("data").glob("data_*.csv"):
    print(file)
```

Output:

```text
data/data_1.csv
data/data_2.csv
data/data_3.csv
```

---

# 4️⃣ `?` Wildcard

`?` একটি single character match করতে পারে।

```python
from pathlib import Path

path = Path("data")

for file in path.glob("data_?.csv"):
    print(file)
```

এটি match করতে পারে:

```text
data_1.csv
data_2.csv
```

কিন্তু:

```text
data_10.csv
```

এর মতো filename-এর ক্ষেত্রে `?` শুধুমাত্র একটি character-এর জায়গা বোঝায়।

---

# 5️⃣ `rglob()` ⭐⭐⭐

ধরো:

```text
dataset/
├── train/
│   ├── cat.jpg
│   └── dog.jpg
│
└── test/
    ├── cat.jpg
    └── dog.jpg
```

```python
dataset = Path("dataset")

for file in dataset.rglob("*.jpg"):
    print(file)
```

Output:

```text
dataset/train/cat.jpg
dataset/train/dog.jpg
dataset/test/cat.jpg
dataset/test/dog.jpg
```

---

# 6️⃣ `glob()` এবং `rglob()` Difference

### `glob()`

```python
path.glob("*.jpg")
```

➡️ নির্দিষ্ট directory level-এর matching entries।

### `rglob()`

```python
path.rglob("*.jpg")
```

➡️ directory এবং তার nested subdirectories-এ recursively search করে।

মনে রাখো:

```text
glob  → এই directory-তে খোঁজো
rglob → এই directory + ভিতরের সব directory-তে খোঁজো
```

---

# 7️⃣ `glob("**/*.jpg")`

Recursive search করার আরেকটি pattern হলো:

```python
path.glob("**/*.jpg")
```

এটি nested directories-এর `.jpg` files খুঁজতে পারে।

তাই practicalভাবে:

```python
path.rglob("*.jpg")
```

লেখাটা সহজ এবং readable।

---

# 8️⃣ Multiple Extensions ⭐⭐⭐

ধরো তোমার image dataset-এ:

```text
.jpg
.jpeg
.png
.webp
```

আছে।

একটি pattern দিয়ে সব extension লেখা যায় না।

তাই:

```python
from pathlib import Path

path = Path("images")

extensions = [
    "*.jpg",
    "*.jpeg",
    "*.png",
    "*.webp"
]

for pattern in extensions:

    for file in path.rglob(pattern):
        print(file)
```

---

# 9️⃣ Better Approach

আরেকভাবে সব files নিয়ে extension check করতে পারো:

```python
from pathlib import Path

path = Path("images")

extensions = {
    ".jpg",
    ".jpeg",
    ".png",
    ".webp"
}

for file in path.rglob("*"):

    if file.is_file() and file.suffix.lower() in extensions:
        print(file)
```

এখানে:

```python
file.suffix
```

filename-এর extension দেয়।

---

# 🔟 কেন `.lower()`?

ধরো:

```text
cat.jpg
dog.JPG
bird.Png
```

এগুলোকে একইভাবে handle করতে:

```python
file.suffix.lower()
```

ফলে:

```text
.jpg
.jpg
.png
```

হয়ে যায়।

---

# 1️⃣1️⃣ File List তৈরি

Search result list হিসেবে রাখতে:

```python
from pathlib import Path

files = list(
    Path("dataset").rglob("*.jpg")
)

print(files)
```

তারপর:

```python
print("Total:", len(files))
```

---

# 1️⃣2️⃣ File Count ⭐⭐⭐

```python
from pathlib import Path

dataset = Path("dataset")

images = list(dataset.rglob("*.jpg"))

print("Total JPG:", len(images))
```

---

# 1️⃣3️⃣ Class-wise Dataset Count

ধরো:

```text
dataset/
├── normal/
├── robbery/
└── fight/
```

প্রতিটি class-এর image count করতে পারো:

```python
from pathlib import Path

dataset = Path("dataset")

for folder in dataset.iterdir():

    if not folder.is_dir():
        continue

    images = list(folder.rglob("*.jpg"))

    print(
        folder.name,
        ":",
        len(images)
    )
```

Output:

```text
normal : 500
robbery : 300
fight : 400
```

এটা ML dataset analysis-এর জন্য খুব useful।

---

# 1️⃣4️⃣ `iterdir()` + `rglob()` ⭐⭐⭐

এই combination খুব গুরুত্বপূর্ণ।

```python
for class_dir in dataset.iterdir():

    if class_dir.is_dir():

        images = list(
            class_dir.rglob("*.jpg")
        )

        print(
            class_dir.name,
            len(images)
        )
```

Mental model:

```text
dataset
   │
   ├── normal
   │     └── rglob("*.jpg")
   │
   ├── robbery
   │     └── rglob("*.jpg")
   │
   └── fight
         └── rglob("*.jpg")
```

---

# 1️⃣5️⃣ Recursive সব File

সব ধরনের file দেখতে:

```python
from pathlib import Path

for file in Path("project").rglob("*"):

    if file.is_file():
        print(file)
```

এতে nested directories-এর files-ও পাওয়া যাবে।

---

# 1️⃣6️⃣ শুধু Python Files

```python
for file in Path(".").rglob("*.py"):
    print(file)
```

এটা একটি project-এর সব Python source file খুঁজে দিতে পারে।

---

# 1️⃣7️⃣ শুধু JSON Files

```python
for file in Path(".").rglob("*.json"):
    print(file)
```

Useful for:

- API data
    
- configuration
    
- dataset metadata
    

---

# 1️⃣8️⃣ শুধু CSV Files

```python
for file in Path("data").rglob("*.csv"):
    print(file)
```

Data science project-এ খুব common।

---

# 1️⃣9️⃣ Hidden Files

Linux-এ hidden file সাধারণত `.` দিয়ে শুরু হয়:

```text
.env
.gitignore
.config
```

Simple pattern:

```python
for file in Path(".").glob(".*"):
    print(file)
```

তবে hidden files নিয়ে কাজ করার সময় বুঝে pattern ব্যবহার করবে—কারণ `.`-এর আচরণ shell glob-এর মতো ধরে নেওয়া ঠিক নয়।

---

# 2️⃣0️⃣ Search by Filename

ধরো:

```text
project/
├── user_model.py
├── user_service.py
├── auth_service.py
└── product_service.py
```

`service` থাকা files:

```python
from pathlib import Path

for file in Path("project").rglob("*service*.py"):
    print(file)
```

Output:

```text
project/user_service.py
project/auth_service.py
project/product_service.py
```

---

# 🔥 2️⃣1️⃣ Practical Function — File Finder

```python
from pathlib import Path


def find_files(folder, extension):

    folder = Path(folder)

    pattern = f"*.{extension}"

    return list(
        folder.rglob(pattern)
    )


files = find_files(
    "project",
    "py"
)

for file in files:
    print(file)
```

Call:

```python
find_files("dataset", "jpg")
```

---

# 🔥 2️⃣2️⃣ Better File Finder

Multiple extensions support করবে:

```python
from pathlib import Path


def find_files(folder, extensions):

    folder = Path(folder)

    extensions = {
        ext.lower()
        for ext in extensions
    }

    results = []

    for file in folder.rglob("*"):

        if not file.is_file():
            continue

        if file.suffix.lower() in extensions:
            results.append(file)

    return results


images = find_files(
    "dataset",
    [".jpg", ".png", ".jpeg"]
)

print("Total:", len(images))
```

---

# 🧪 Day 6 Practice

## Exercise 1

এই structure:

```text
project/
├── src/
│   ├── main.py
│   └── utils.py
│
├── tests/
│   └── test_main.py
│
├── data/
│   ├── train.csv
│   └── test.csv
│
└── README.md
```

### Task:

সব `.py` files বের করো।

Expected:

```text
src/main.py
src/utils.py
tests/test_main.py
```

---

## Exercise 2

সব `.csv` files বের করো।

Expected:

```text
data/train.csv
data/test.csv
```

---

## Exercise 3 ⭐

সব files-এর extension count করো।

Expected concept:

```text
.py   → 3
.csv  → 2
.md   → 1
```

Hint:

```python
from collections import Counter
```

তারপর:

```python
Counter(
    file.suffix.lower()
    for file in Path("project").rglob("*")
    if file.is_file()
)
```

---

# 🏆 Day 6 Mini Project — File Search Tool

একটি CLI tool বানাও:

```text
====================================
          FILE SEARCH TOOL
====================================

Enter directory: dataset
Enter extension: jpg

Searching...

Found:
----------------
dataset/train/a.jpg
dataset/train/b.jpg
dataset/test/c.jpg

Total: 3
```

Core code:

```python
from pathlib import Path

directory = Path(
    input("Enter directory: ")
)

extension = input(
    "Enter extension: "
).lower().lstrip(".")

pattern = f"*.{extension}"

files = list(
    directory.rglob(pattern)
)

print("\nFound:")

for file in files:
    print(file)

print("\nTotal:", len(files))
```

এখানে তুমি একসাথে ব্যবহার করলে:

```text
Path()
rglob()
is_file()
suffix
list()
len()
input()
```

---

# 🧠 Day 6 Final Concept

```text
                 Search
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
      glob                    rglob
        │                       │
  current level          recursive search
        │                       │
        ↓                       ↓
   "*.py"                  "*.py"
```

### ⭐ সবচেয়ে গুরুত্বপূর্ণ

```python
path.glob("*.py")
```

→ নির্দিষ্ট directory level-এর matching entries।

```python
path.rglob("*.py")
```

→ nested directories-সহ recursive search।

```python
path.rglob("*")
```

→ recursiveভাবে সব entries।

---

# 📚 Progress

```text
Day 1  → Path Basics                    ✅
Day 2  → Check Path/File/Directory      ✅
Day 3  → Create File & Directory        ✅
Day 4  → Read & Write Files             ✅
Day 5  → Directory Traversal            ✅
Day 6  → glob/rglob Advanced            ✅
Day 7  → Rename / Move / Delete         ⏭️
Day 8  → Metadata & Advanced Operations
Day 9  → pathlib + os + Automation
Day 10 → Final File Manager Project
```

**Day 7-এ আমরা filesystem-এর existing files/folders নিয়ে কাজ করব: `rename()`, `replace()`, `unlink()`, `rmdir()` এবং `shutil`-এর সাথে `pathlib` কীভাবে ব্যবহার হয়।**


# 🐍 Python `pathlib` — Day 7

## 🔄 Rename, Move & Delete Files/Folders

আজ আমরা শিখব existing **file/folder rename, move এবং delete** করা।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 আজকের Topics

```text
Path.rename()
Path.replace()
Path.unlink()
Path.rmdir()
Path.parent
Path.with_name()
Path.with_suffix()
```

এছাড়া শেষে `pathlib + shutil` দিয়ে **folder move/copy** দেখব।

---

# 1️⃣ `rename()` ⭐⭐⭐

ধরো:

```text
project/
└── old.txt
```

এখন rename করতে:

```python
from pathlib import Path

path = Path("old.txt")

path.rename("new.txt")
```

Result:

```text
project/
└── new.txt
```

অর্থাৎ:

```text
old.txt
   ↓
new.txt
```

---

# 2️⃣ অন্য Directory-তে Move

`rename()` শুধু নাম change নয়, অন্য path-এ move করতেও ব্যবহার করা যায়।

ধরো:

```text
project/
├── data.txt
└── archive/
```

```python
from pathlib import Path

source = Path("data.txt")
destination = Path("archive/data.txt")

source.rename(destination)
```

Result:

```text
project/
└── archive/
    └── data.txt
```

---

# 3️⃣ File Rename

আরও practical:

```python
from pathlib import Path

old = Path("report.txt")
new = old.with_name("final_report.txt")

old.rename(new)
```

এখানে:

```python
old.with_name("final_report.txt")
```

নতুন path তৈরি করছে।

---

# 4️⃣ `with_name()` ⭐⭐⭐

ধরো:

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

new_path = path.with_name("dog.jpg")

print(new_path)
```

Output:

```text
data/images/dog.jpg
```

শুধু filename পরিবর্তন হয়েছে।

---

# 5️⃣ `with_suffix()` ⭐⭐⭐

Extension পরিবর্তন করতে:

```python
from pathlib import Path

path = Path("image.jpg")

new_path = path.with_suffix(".png")

print(new_path)
```

Output:

```text
image.png
```

⚠️ এটা শুধু **নতুন Path object তৈরি করে**; filesystem-এর actual file rename করে না।

Actual rename:

```python
path.rename(path.with_suffix(".png"))
```

---

# 6️⃣ `replace()` ⭐⭐⭐

`replace()` দিয়ে destination existing থাকলে সেটাকে replace করার জন্য rename করা যায়।

```python
from pathlib import Path

source = Path("old.txt")
destination = Path("new.txt")

source.replace(destination)
```

`rename()` এবং `replace()`-এর behavior-এর মধ্যে গুরুত্বপূর্ণ পার্থক্য আছে, বিশেষ করে destination আগে থেকেই থাকলে। তাই overwrite semantics বুঝে ব্যবহার করবে।

---

# 7️⃣ `unlink()` — File Delete ⭐⭐⭐

File delete করতে:

```python
from pathlib import Path

path = Path("old.txt")

path.unlink()
```

File delete হয়ে যাবে।

```text
old.txt
   ↓
❌ deleted
```

---

# 8️⃣ Safe Delete

File আছে কিনা আগে check:

```python
from pathlib import Path

path = Path("old.txt")

if path.exists():
    path.unlink()
    print("File deleted")
else:
    print("File not found")
```

আরও নির্দিষ্টভাবে:

```python
if path.is_file():
    path.unlink()
```

---

# 9️⃣ `missing_ok=True`

File না থাকলেও error না চাইলে:

```python
from pathlib import Path

path = Path("old.txt")

path.unlink(missing_ok=True)
```

মানে:

```text
file আছে
    ↓
delete

file নেই
    ↓
কোনো error নয়
```

---

# 🔟 Directory Delete — `rmdir()`

**Empty directory** delete করতে:

```python
from pathlib import Path

path = Path("empty_folder")

path.rmdir()
```

⚠️ Folder-এর ভিতরে file/folder থাকলে `rmdir()` কাজ করবে না।

---

# 1️⃣1️⃣ `rmdir()` Example

```text
project/
└── empty/
```

```python
from pathlib import Path

Path("empty").rmdir()
```

Result:

```text
project/
```

---

# 1️⃣2️⃣ Non-empty Directory

ধরো:

```text
data/
└── file.txt
```

এখন:

```python
Path("data").rmdir()
```

করলে error হবে।

কারণ `data` empty নয়।

---

# 1️⃣3️⃣ Non-empty Folder Delete

এখানে `shutil` ব্যবহার করা হয়:

```python
import shutil
from pathlib import Path

path = Path("data")

shutil.rmtree(path)
```

এটি directory এবং তার contents recursively delete করতে পারে।

⚠️ **খুব সাবধানে ব্যবহার করবে।** `shutil.rmtree()` ভুল path দিলে অনেক data মুছে যেতে পারে।

---

# 1️⃣4️⃣ File Move

`pathlib` দিয়ে:

```python
from pathlib import Path

source = Path("data.txt")
destination = Path("backup/data.txt")

destination.parent.mkdir(
    parents=True,
    exist_ok=True
)

source.rename(destination)
```

এখানে প্রথমে:

```python
destination.parent
```

দিয়ে `backup/` বের করা হয়েছে।

তারপর folder তৈরি করা হয়েছে।

তারপর file move করা হয়েছে।

---

# 🔥 1️⃣5️⃣ Multiple Files Move

ধরো:

```text
project/
├── a.txt
├── b.txt
├── c.txt
└── backup/
```

সব `.txt` file backup-এ নিতে:

```python
from pathlib import Path

source_dir = Path("project")
backup_dir = source_dir / "backup"

backup_dir.mkdir(exist_ok=True)

for file in source_dir.glob("*.txt"):

    destination = backup_dir / file.name

    file.rename(destination)
```

Result:

```text
project/
└── backup/
    ├── a.txt
    ├── b.txt
    └── c.txt
```

---

# 1️⃣6️⃣ `file.name`

এটা খুব গুরুত্বপূর্ণ।

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print(path.name)
```

Output:

```text
cat.jpg
```

তাই:

```python
destination = backup_dir / file.name
```

মানে:

```text
backup/
└── একই filename
```

---

# 1️⃣7️⃣ Rename Multiple Files ⭐⭐⭐

ধরো:

```text
images/
├── image1.jpg
├── image2.jpg
└── image3.jpg
```

এগুলো rename করতে:

```python
from pathlib import Path

folder = Path("images")

for number, file in enumerate(
    folder.glob("*.jpg"),
    start=1
):

    new_name = f"photo_{number}.jpg"

    file.rename(
        folder / new_name
    )
```

Result:

```text
images/
├── photo_1.jpg
├── photo_2.jpg
└── photo_3.jpg
```

---

# 1️⃣8️⃣ Extension Change

ধরো:

```text
image.jpg
```

থেকে:

```text
image.png
```

করতে:

```python
from pathlib import Path

path = Path("image.jpg")

new_path = path.with_suffix(".png")

path.rename(new_path)
```

কিন্তু মনে রাখবে:

> `.jpg` file-কে শুধু `.png` rename করলে file-এর actual image format convert হয় না।

---

# 1️⃣9️⃣ `shutil.move()` কখন?

`pathlib` path manipulation-এর জন্য খুব ভালো।

কিন্তু complex file/folder operations-এর জন্য Python-এর `shutil` module useful।

```python
import shutil
from pathlib import Path

source = Path("data.txt")
destination = Path("backup/data.txt")

destination.parent.mkdir(
    parents=True,
    exist_ok=True
)

shutil.move(source, destination)
```

---

# 🧠 `rename()` vs `shutil.move()`

|Tool|সাধারণ ব্যবহার|
|---|---|
|`rename()`|rename / simple move|
|`replace()`|destination replace semantics সহ rename|
|`shutil.move()`|broader move operations|
|`unlink()`|file delete|
|`rmdir()`|empty directory delete|
|`shutil.rmtree()`|non-empty directory tree delete|

---

# 🔥 20️⃣ Practical File Organizer

এখন একটা ছোট automation example:

ধরো:

```text
downloads/
├── photo.jpg
├── image.png
├── notes.txt
├── report.pdf
└── data.csv
```

আমরা চাই:

```text
downloads/
├── images/
│   ├── photo.jpg
│   └── image.png
│
├── documents/
│   ├── notes.txt
│   └── report.pdf
│
└── data/
    └── data.csv
```

Code:

```python
from pathlib import Path

downloads = Path("downloads")

folders = {
    ".jpg": "images",
    ".png": "images",
    ".txt": "documents",
    ".pdf": "documents",
    ".csv": "data",
}

for file in downloads.iterdir():

    if not file.is_file():
        continue

    extension = file.suffix.lower()

    if extension not in folders:
        continue

    folder = downloads / folders[extension]

    folder.mkdir(
        exist_ok=True
    )

    destination = folder / file.name

    file.rename(destination)

print("Files organized!")
```

এটা **file automation-এর খুব practical example**।

---

# 🧪 Day 7 Practice

## Exercise 1 — Rename

তৈরি করো:

```text
old_name.txt
```

তারপর rename করো:

```text
new_name.txt
```

---

## Exercise 2 — Delete

তৈরি করো:

```text
temporary.txt
```

তারপর:

```python
Path("temporary.txt").unlink()
```

দিয়ে delete করো।

---

## Exercise 3 — Move

এই structure বানাও:

```text
project/
├── data.txt
└── backup/
```

তারপর:

```text
data.txt
```

move করো:

```text
backup/data.txt
```

---

## Exercise 4 ⭐ — Batch Rename

```text
images/
├── img1.jpg
├── img2.jpg
├── img3.jpg
├── img4.jpg
```

এগুলোকে:

```text
photo_1.jpg
photo_2.jpg
photo_3.jpg
photo_4.jpg
```

করো।

---

# 🏆 Day 7 Mini Project — File Organizer

একটি `downloads/` folder থাকবে:

```text
downloads/
├── photo.jpg
├── image.png
├── document.pdf
├── notes.txt
├── data.csv
└── report.pdf
```

Program automatically তৈরি করবে:

```text
downloads/
├── images/
├── documents/
└── data/
```

এবং files-এর extension অনুযায়ী move করবে।

### Bonus

Unknown extension হলে:

```text
others/
```

folder-এ move করবে।

---

# 🧠 আজকের Mental Model

```text
Existing Path
     │
     ├── Rename
     │     └── rename()
     │
     ├── Move
     │     ├── rename()
     │     └── shutil.move()
     │
     ├── Delete File
     │     └── unlink()
     │
     └── Delete Directory
           ├── rmdir()       → empty
           └── rmtree()      → non-empty
```

### ⭐ Must Know

```python
path.rename(...)
path.replace(...)

path.unlink()
path.unlink(missing_ok=True)

path.rmdir()

path.with_name(...)
path.with_suffix(...)

path.name
path.parent
```

আর সবচেয়ে গুরুত্বপূর্ণ safety rule:

> **`unlink()` এবং বিশেষ করে `shutil.rmtree()` ব্যবহার করার আগে path ঠিক আছে কিনা অবশ্যই verify করবে।**

---

# 📚 Course Progress

```text
Day 1  → Path Basics                    ✅
Day 2  → Check Path/File/Directory      ✅
Day 3  → Create File & Directory        ✅
Day 4  → Read & Write Files             ✅
Day 5  → Directory Traversal            ✅
Day 6  → glob/rglob Advanced            ✅
Day 7  → Rename / Move / Delete         ✅
Day 8  → Metadata & Advanced Operations ⏭️
Day 9  → pathlib + os + Automation
Day 10 → Final File Manager Project
```



# 🐍 Python `pathlib` — Day 8

## 📊 File & Directory Metadata

আজ আমরা `pathlib` দিয়ে কোনো file/folder সম্পর্কে **information বের করা** শিখব।

Official documentation: [Python `pathlib` official documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 আজকের Topics

```text
Path.stat()
Path.lstat()
Path.name
Path.stem
Path.suffix
Path.suffixes
Path.parent
Path.parts
Path.absolute()
Path.resolve()
Path.cwd()
Path.home()
```

এগুলো file manager, automation, backup system, dataset analyzer—সব জায়গায় কাজে লাগে।

---

# 1️⃣ `name` ⭐⭐⭐

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print(path.name)
```

Output:

```text
cat.jpg
```

মানে পুরো path থেকে **শেষের filename**।

---

# 2️⃣ `stem` ⭐⭐⭐

```python
print(path.stem)
```

Output:

```text
cat
```

`stem` = filename-এর extension বাদে অংশ।

```text
cat.jpg
 │   │
 │   └── suffix
 └────── stem
```

---

# 3️⃣ `suffix` ⭐⭐⭐

```python
print(path.suffix)
```

Output:

```text
.jpg
```

অর্থাৎ file-এর শেষ extension।

---

# 4️⃣ `suffixes`

একটি file-এ একাধিক suffix থাকতে পারে:

```python
from pathlib import Path

path = Path("backup.tar.gz")

print(path.name)
print(path.stem)
print(path.suffix)
print(path.suffixes)
```

Output concept:

```text
backup.tar.gz
backup.tar
.gz
['.tar', '.gz']
```

### Difference

```text
name
 ↓
backup.tar.gz

stem
 ↓
backup.tar

suffix
 ↓
.gz

suffixes
 ↓
['.tar', '.gz']
```

---

# 5️⃣ `parent` ⭐⭐⭐

```python
path = Path("data/images/cat.jpg")

print(path.parent)
```

Output:

```text
data/images
```

Parent directory বের করার জন্য খুব useful।

---

# 6️⃣ `parts`

Path-কে আলাদা অংশে দেখতে:

```python
path = Path("data/images/train/cat.jpg")

print(path.parts)
```

Output system অনুযায়ী এমন হতে পারে:

```python
('data', 'images', 'train', 'cat.jpg')
```

এটা path-এর individual components দেয়।

---

# 7️⃣ `stat()` ⭐⭐⭐

এখন আসি important অংশে।

```python
from pathlib import Path

path = Path("data.txt")

info = path.stat()

print(info)
```

`stat()` file-এর metadata দেয়।

যেমন:

```text
size
timestamps
permissions
inode
etc.
```

---

# 8️⃣ File Size

```python
from pathlib import Path

path = Path("data.txt")

size = path.stat().st_size

print(size)
```

`st_size` সাধারণত **bytes**-এ size দেয়।

যেমন:

```text
1024 bytes
```

মানে প্রায়:

```text
1 KB
```

---

# 9️⃣ File Size KB-তে

```python
size = path.stat().st_size

kb = size / 1024

print(kb, "KB")
```

আর MB:

```python
mb = size / (1024 * 1024)

print(mb, "MB")
```

---

# 🔟 File Size Function

Reusable function:

```python
from pathlib import Path


def get_size(path):

    path = Path(path)

    size = path.stat().st_size

    return size


print(
    get_size("data.txt"),
    "bytes"
)
```

---

# 1️⃣1️⃣ Modification Time

`stat()` থেকে modification timestamp পাওয়া যায়:

```python
from pathlib import Path

path = Path("data.txt")

info = path.stat()

print(info.st_mtime)
```

এটা Unix timestamp।

Readable datetime পেতে:

```python
from datetime import datetime

modified = datetime.fromtimestamp(
    info.st_mtime
)

print(modified)
```

---

# 1️⃣2️⃣ Access Time

```python
info = path.stat()

print(info.st_atime)
```

এটি last access time সম্পর্কিত timestamp।

---

# 1️⃣3️⃣ Creation Time নিয়ে সতর্কতা

```python
info.st_ctime
```

এটাকে সব operating system-এ "creation time" ধরে নেওয়া ঠিক নয়।

বিশেষ করে Unix-like systems-এ `ctime` সাধারণত **metadata/status change time** বোঝায়।

তাই OS অনুযায়ী timestamp-এর meaning বুঝে ব্যবহার করবে।

---

# 1️⃣4️⃣ `absolute()`

বর্তমান path থেকে absolute path তৈরি করতে:

```python
from pathlib import Path

path = Path("data/file.txt")

print(path.absolute())
```

উদাহরণ:

```text
/home/user/project/data/file.txt
```

---

# 1️⃣5️⃣ `resolve()` ⭐⭐⭐

```python
path = Path("data/file.txt")

print(path.resolve())
```

`resolve()` path-কে absolute করে এবং available হলে symbolic links resolve করে।

এটি path normalization-এর জন্য useful।

---

# 1️⃣6️⃣ `cwd()` ⭐⭐⭐

Current working directory:

```python
from pathlib import Path

print(Path.cwd())
```

উদাহরণ:

```text
/home/user/project
```

অর্থাৎ Python program বর্তমানে কোন directory থেকে run হচ্ছে।

---

# 1️⃣7️⃣ `home()`

Current user's home directory:

```python
from pathlib import Path

print(Path.home())
```

Linux-এ সাধারণত:

```text
/home/username
```

---

# 1️⃣8️⃣ `cwd()` বনাম `home()`

```text
Path.cwd()
   ↓
বর্তমানে যে directory-তে কাজ করছি

Path.home()
   ↓
বর্তমান user's home directory
```

উদাহরণ:

```python
print("Working:", Path.cwd())
print("Home:", Path.home())
```

---

# 1️⃣9️⃣ Complete Metadata Example ⭐⭐⭐

```python
from pathlib import Path
from datetime import datetime

path = Path("data.txt")

info = path.stat()

print("Name      :", path.name)
print("Stem      :", path.stem)
print("Suffix    :", path.suffix)
print("Parent    :", path.parent)
print("Size      :", info.st_size, "bytes")
print(
    "Modified  :",
    datetime.fromtimestamp(info.st_mtime)
)
print("Absolute  :", path.absolute())
```

---

# 🔥 2️⃣0️⃣ Practical — File Information Tool

```python
from pathlib import Path
from datetime import datetime


def file_info(file_path):

    path = Path(file_path)

    if not path.exists():
        print("File not found!")
        return

    if not path.is_file():
        print("This is not a file!")
        return

    info = path.stat()

    print("\n======================")
    print("     FILE INFO")
    print("======================")

    print("Name     :", path.name)
    print("Type     :", path.suffix)
    print("Size     :", info.st_size, "bytes")
    print(
        "Modified :",
        datetime.fromtimestamp(
            info.st_mtime
        )
    )
    print("Parent   :", path.parent)
    print("Absolute :", path.resolve())


file_info("data.txt")
```

---

# 2️⃣1️⃣ File Type Check

Metadata-এর সাথে এগুলোও combine করবে:

```python
path.is_file()
path.is_dir()
path.exists()
```

Example:

```python
from pathlib import Path

path = Path("data")

if not path.exists():
    print("Does not exist")

elif path.is_file():
    print("This is a file")

elif path.is_dir():
    print("This is a directory")
```

---

# 2️⃣2️⃣ Permission Check

`stat()` থেকে permission bits-ও পাওয়া যায়:

```python
import stat
from pathlib import Path

path = Path("data.txt")

mode = path.stat().st_mode

print(
    stat.filemode(mode)
)
```

Linux-এ output হতে পারে:

```text
-rw-r--r--
```

এটা filesystem permission information।

---

# 🔥 2️⃣3️⃣ Dataset Metadata Analyzer

ML project-এর জন্য practical example:

```python
from pathlib import Path


dataset = Path("dataset")

total_files = 0
total_size = 0

for file in dataset.rglob("*"):

    if not file.is_file():
        continue

    total_files += 1
    total_size += file.stat().st_size


print("Total files :", total_files)
print("Total bytes :", total_size)
print(
    "Total MB    :",
    total_size / (1024 * 1024)
)
```

এভাবে একটি dataset-এর মোট file count এবং total size বের করতে পারো।

---

# 🧪 Day 8 Practice

## Exercise 1

একটি file:

```text
student.txt
```

তৈরি করো।

তারপর print করো:

```text
Name
Stem
Suffix
Parent
Size
Absolute Path
```

---

## Exercise 2 ⭐

এই structure:

```text
dataset/
├── train/
│   ├── a.jpg
│   └── b.jpg
│
└── test/
    └── c.jpg
```

সব `.jpg` file-এর:

```text
filename
size
parent directory
```

print করো।

Hint:

```python
for file in Path("dataset").rglob("*.jpg"):
    ...
```

---

# 🏆 Day 8 Mini Project — Directory Analyzer

একটি folder দিলে program এমন output দেবে:

```text
================================
       DIRECTORY ANALYZER
================================

Directory: dataset

Files       : 120
Directories : 8
Total Size  : 45.7 MB

Extensions:
.jpg  → 80
.png  → 35
.txt  → 5
```

Core idea:

```python
from pathlib import Path
from collections import Counter

root = Path("dataset")

files = []
directories = []

for item in root.rglob("*"):

    if item.is_file():
        files.append(item)

    elif item.is_dir():
        directories.append(item)

extensions = Counter(
    file.suffix.lower()
    for file in files
)

total_size = sum(
    file.stat().st_size
    for file in files
)

print("Files       :", len(files))
print("Directories :", len(directories))
print(
    "Total Size  :",
    total_size / (1024 * 1024),
    "MB"
)

print("\nExtensions:")

for extension, count in extensions.items():
    print(extension, "→", count)
```

---

# 🧠 Day 8 Mental Model

```text
                 Path
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
     Name        Parent       Type
       │           │           │
     stem        parent      is_file()
     suffix                  is_dir()
                               │
                               ↓
                            Metadata
                               │
                             stat()
                               │
                    ┌──────────┼──────────┐
                    ↓          ↓          ↓
                   size      modified   permissions
```

---

# ⭐ Day 8 Must Know

```python
path.name
path.stem
path.suffix
path.suffixes
path.parent
path.parts

path.stat()
path.stat().st_size

path.absolute()
path.resolve()

Path.cwd()
Path.home()

path.exists()
path.is_file()
path.is_dir()
```

### সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
name       → cat.jpg
stem       → cat
suffix     → .jpg
suffixes   → ['.tar', '.gz']
parent     → data/images
stat()     → metadata
cwd()      → current working directory
home()     → user's home directory
```

---

# 📚 Course Progress

```text
Day 1  → Path Basics                    ✅
Day 2  → Check Path/File/Directory      ✅
Day 3  → Create File & Directory        ✅
Day 4  → Read & Write Files             ✅
Day 5  → Directory Traversal            ✅
Day 6  → glob/rglob Advanced            ✅
Day 7  → Rename / Move / Delete         ✅
Day 8  → Metadata & Advanced Operations ✅
Day 9  → pathlib + os + Automation      ⏭️
Day 10 → Final File Manager Project
```

**Day 9-এ সবচেয়ে important connection: `pathlib` + `os` একসাথে কীভাবে ব্যবহার করবে এবং real-world automation scripts কীভাবে বানাবে।**



# 🐍 Python `pathlib` — Day 9

## 🔗 `pathlib` + `os` + Automation

আজকের দিনটা খুব গুরুত্বপূর্ণ। কারণ এখন আমরা আলাদা আলাদা method না শিখে **real-world automation** বানানো শুরু করব।

Official docs:

- [Python `pathlib` documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)
    
- [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)
    

---

# 🎯 আজ কী শিখব?

```text
1. pathlib + os কখন ব্যবহার করব
2. Current directory
3. Environment variables
4. Directory automation
5. File organizer
6. Backup automation
7. Temporary files
8. Practical automation project
```

---

# 1️⃣ `pathlib` বনাম `os`

দুটোই filesystem-এর সাথে কাজ করতে পারে।

### `pathlib`

```python
from pathlib import Path

path = Path("data/images/cat.jpg")

print(path.name)
print(path.parent)
print(path.suffix)
```

এখানে path নিয়ে কাজ করা অনেক clean।

### `os`

```python
import os

print(os.getcwd())
print(os.listdir())
```

`os` শুধু filesystem নয়, operating-system level functionality-ও দেয়।

---

# 2️⃣ Current Working Directory

`pathlib`:

```python
from pathlib import Path

print(Path.cwd())
```

`os`:

```python
import os

print(os.getcwd())
```

দুটোই current working directory দেখায়।

---

# 3️⃣ Directory Change

`os` দিয়ে:

```python
import os

os.chdir("data")

print(os.getcwd())
```

কিন্তু নতুন code-এ সম্ভব হলে global working directory change না করে `Path` দিয়ে explicit paths ব্যবহার করা বেশি পরিষ্কার।

Example:

```python
from pathlib import Path

data = Path("data")

file = data / "test.txt"

print(file)
```

---

# 4️⃣ Environment Variables ⭐⭐⭐

এখানে `os` খুব গুরুত্বপূর্ণ।

```python
import os

username = os.getenv("USER")

print(username)
```

Environment variable না থাকলে:

```python
os.getenv("SOMETHING")
```

`None` দিতে পারে।

Default:

```python
username = os.getenv(
    "USER",
    "unknown"
)

print(username)
```

---

# 5️⃣ `.env` এবং Secret

যেমন:

```text
DATABASE_URL
API_KEY
SECRET_KEY
```

এসব code-এর ভিতরে hard-code না করাই ভালো।

Example:

```python
import os

api_key = os.getenv("API_KEY")

print(api_key)
```

⚠️ Real API key/password কখনো GitHub-এ commit করবে না।

---

# 6️⃣ `pathlib` + Environment Variable

ধরো environment variable:

```text
PROJECT_DIR=/home/user/project
```

Python:

```python
import os
from pathlib import Path

project_dir = Path(
    os.getenv("PROJECT_DIR", ".")
)

print(project_dir.resolve())
```

এখানে:

```text
os
 ↓
environment variable

pathlib
 ↓
path manipulation
```

---

# 7️⃣ Automation Example — Folder Structure

একটি project automatically তৈরি:

```python
from pathlib import Path

root = Path("my_project")

folders = [
    "src",
    "tests",
    "data/raw",
    "data/processed",
    "logs"
]

for folder in folders:
    (root / folder).mkdir(
        parents=True,
        exist_ok=True
    )

(root / "README.md").touch(
    exist_ok=True
)

print("Project created!")
```

Result:

```text
my_project/
├── src/
├── tests/
├── data/
│   ├── raw/
│   └── processed/
├── logs/
└── README.md
```

---

# 8️⃣ Automation — File Organizer ⭐⭐⭐

ধরো:

```text
downloads/
├── photo.jpg
├── image.png
├── report.pdf
├── notes.txt
└── data.csv
```

আমরা automatically organize করব।

```python
from pathlib import Path

downloads = Path("downloads")

categories = {
    "images": [".jpg", ".jpeg", ".png", ".webp"],
    "documents": [".pdf", ".txt", ".docx"],
    "data": [".csv", ".json"],
}

for folder in categories:
    (downloads / folder).mkdir(
        exist_ok=True
    )

for file in downloads.iterdir():

    if not file.is_file():
        continue

    extension = file.suffix.lower()

    for folder, extensions in categories.items():

        if extension in extensions:

            destination = (
                downloads /
                folder /
                file.name
            )

            file.rename(destination)

            break

print("Organization complete!")
```

---

# 9️⃣ কেন `break`?

এই অংশ:

```python
if extension in extensions:
    ...
    break
```

একটি file এক category-তে match করার পর loop বন্ধ করে।

যেমন:

```text
photo.jpg
```

match করবে:

```text
images
```

তারপর আর `documents`, `data` check করার প্রয়োজন নেই।

---

# 🔟 Unknown Files

ধরো:

```text
program.exe
video.mp4
archive.zip
```

এগুলো আমাদের categories-এ নেই।

তাহলে `others` বানানো যায়:

```python
from pathlib import Path

downloads = Path("downloads")

others = downloads / "others"

others.mkdir(exist_ok=True)

categories = {
    "images": {".jpg", ".jpeg", ".png"},
    "documents": {".pdf", ".txt"},
    "data": {".csv", ".json"},
}

for file in downloads.iterdir():

    if not file.is_file():
        continue

    extension = file.suffix.lower()

    destination_folder = others

    for folder, extensions in categories.items():

        if extension in extensions:
            destination_folder = downloads / folder
            break

    destination = (
        destination_folder / file.name
    )

    file.rename(destination)
```

---

# 1️⃣1️⃣ Backup Automation ⭐⭐⭐

ধরো:

```text
project/
└── data/
    ├── users.csv
    └── products.csv
```

Backup করতে `shutil` useful:

```python
from pathlib import Path
import shutil

source = Path("project/data")
backup = Path("backup/data")

backup.mkdir(
    parents=True,
    exist_ok=True
)

for file in source.iterdir():

    if file.is_file():

        shutil.copy2(
            file,
            backup / file.name
        )

print("Backup completed!")
```

---

# 1️⃣2️⃣ `copy()` বনাম `copy2()`

```python
shutil.copy()
```

file copy করে।

```python
shutil.copy2()
```

file copy করার পাশাপাশি metadata-ও preserve করার চেষ্টা করে।

Backup-এর জন্য `copy2()` useful।

---

# 1️⃣3️⃣ Recursive Backup

Nested folders থাকলে:

```text
project/
├── data/
│   ├── train/
│   └── test/
└── config/
```

`copytree()` ব্যবহার করা যায়:

```python
from pathlib import Path
import shutil

source = Path("project")
backup = Path("project_backup")

shutil.copytree(
    source,
    backup,
    dirs_exist_ok=True
)
```

---

# 1️⃣4️⃣ `pathlib` + `shutil`

এটা মনে রাখবে:

```text
pathlib
   ↓
Path তৈরি / manipulate / inspect

shutil
   ↓
Copy / Move / Directory operations

os
   ↓
Operating-system interaction
```

একসাথে ব্যবহার করা খুব common।

---

# 1️⃣5️⃣ File Extension Report

Automation-এর আরেকটি example:

```python
from pathlib import Path
from collections import Counter

root = Path("project")

extensions = Counter()

for file in root.rglob("*"):

    if file.is_file():

        extension = file.suffix.lower()

        if extension:
            extensions[extension] += 1

for extension, count in extensions.items():

    print(
        extension,
        "→",
        count
    )
```

Output:

```text
.py → 15
.json → 4
.csv → 8
.md → 3
```

---

# 🔥 1️⃣6️⃣ Automation — Delete Temporary Files

ধরো project-এ `.tmp` files আছে।

```python
from pathlib import Path

root = Path("project")

for file in root.rglob("*.tmp"):

    if file.is_file():
        file.unlink()

print("Temporary files removed!")
```

⚠️ Delete automation চালানোর আগে target pattern এবং directory ভালোভাবে verify করবে।

আর safer approach:

```python
for file in root.rglob("*.tmp"):
    print("Would delete:", file)
```

প্রথমে দেখে তারপর delete করা ভালো।

---

# 1️⃣7️⃣ Dry Run ⭐⭐⭐

Professional automation-এ **dry run** খুব useful।

```python
from pathlib import Path

root = Path("project")

for file in root.rglob("*.tmp"):

    print("Would delete:", file)
```

এতে actual delete হয় না।

তারপর নিশ্চিত হলে:

```python
file.unlink()
```

---

# 🔥 1️⃣8️⃣ Real-world Project — Project Cleaner

ধরো:

```text
my_project/
├── src/
├── tests/
├── __pycache__/
├── temp.tmp
├── debug.log
└── data/
    └── cache.tmp
```

আমরা `.tmp` এবং Python cache cleanup করব।

### Step 1 — Preview

```python
from pathlib import Path

root = Path("my_project")

for file in root.rglob("*.tmp"):
    print("TMP:", file)

for folder in root.rglob("__pycache__"):
    print("CACHE:", folder)
```

### Step 2 — Delete `.tmp`

```python
for file in root.rglob("*.tmp"):

    if file.is_file():
        file.unlink()
```

### Step 3 — Cache directory

```python
import shutil

for folder in root.rglob("__pycache__"):

    if folder.is_dir():
        shutil.rmtree(folder)
```

⚠️ `rmtree()` destructive—production/project cleanup script-এ whitelist বা dry-run ব্যবহার করা ভালো।

---

# 1️⃣9️⃣ `os` কখন বেশি দরকার?

এখন পর্যন্ত আমরা দেখেছি `pathlib` অনেক filesystem কাজ করতে পারে।

`os` তখন বেশি useful যখন OS-level functionality দরকার।

উদাহরণ:

```python
import os

print(os.environ)
print(os.getenv("HOME"))
print(os.cpu_count())
```

আর process-related কাজের ক্ষেত্রে `os`-এর কিছু functionality গুরুত্বপূর্ণ।

---

# 2️⃣0️⃣ একটি গুরুত্বপূর্ণ Rule

❌ সবকিছুর জন্য `os` ব্যবহার করতে হবে—এমন নয়।

Modern Python code-এ path manipulation-এর জন্য:

```python
from pathlib import Path
```

প্রথম পছন্দ রাখো।

তারপর প্রয়োজন অনুযায়ী:

```python
import os
import shutil
```

ব্যবহার করো।

---

# 🧠 আজকের Mental Model

```text
                 Python Automation
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
       pathlib           os           shutil
          │              │              │
       Path work      OS-level       Copy/Move
          │           features        operations
          │
    ┌─────┴─────┐
    ↓           ↓
 Files       Folders
```

---

# 🧪 Day 9 Practice

### Exercise 1

একটি script বানাও যেটা:

```text
project/
```

এর ভিতরে automatically:

```text
src/
tests/
data/
logs/
config/
```

তৈরি করবে।

---

### Exercise 2

একটি `downloads/` folder organize করো:

```text
.jpg/.png → images
.pdf/.txt → documents
.csv/.json → data
অন্য সব → others
```

---

### Exercise 3 ⭐

একটি project-এর extension report তৈরি করো:

```text
.py → 20
.json → 5
.md → 3
.csv → 8
```

---

### Exercise 4 ⭐⭐

একটি **safe project cleaner** বানাও:

```text
1. Scan
2. Show files
3. Confirm
4. Delete
```

প্রথমে অবশ্যই preview করবে।

---

# 🏆 Day 9 Mini Project

## 📁 Automatic Project Manager

একটি program বানাও যেখানে:

```text
1. Create project
2. Show files
3. Show statistics
4. Backup project
5. Find files by extension
6. Clean temporary files
7. Exit
```

এখানে ব্যবহার করবে:

```python
Path()
Path.mkdir()
Path.rglob()
Path.stat()
Path.unlink()
os.getenv()
Path.cwd()
shutil.copy2()
shutil.copytree()
```

এটা শেষ করতে পারলে `pathlib` শুধু syntax হিসেবে নয়, **real automation-এর জন্য** ব্যবহার করতে পারবে।

---

# 📚 Progress

```text
Day 1  → Path Basics                    ✅
Day 2  → Check Path/File/Directory      ✅
Day 3  → Create File & Directory        ✅
Day 4  → Read & Write Files             ✅
Day 5  → Directory Traversal            ✅
Day 6  → glob/rglob Advanced            ✅
Day 7  → Rename / Move / Delete         ✅
Day 8  → Metadata & Advanced Operations ✅
Day 9  → pathlib + os + Automation      ✅
Day 10 → Final File Manager Project     ⏭️
```

**Day 10 হবে final project: `Pathlib File Manager` — search, create, rename, move, delete, statistics এবং backup একসাথে।**




# 🐍 Python `pathlib` — Day 10

# 🗂️ Final Project: File Manager

আজ `pathlib` course-এর **final project**। আমরা এমন একটি ছোট **CLI File Manager** বানাব যেখানে তুমি একসাথে শিখবে:

```text
Create
List
Search
File information
Rename
Move
Delete
Directory statistics
Backup
```

Official docs: [Python pathlib documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 🎯 Final Project Architecture

আমাদের program:

```text
File Manager
│
├── 1. List files
├── 2. Search files
├── 3. File information
├── 4. Create folder
├── 5. Rename file
├── 6. Move file
├── 7. Delete file
├── 8. Statistics
├── 9. Backup
└── 0. Exit
```

---

# 1️⃣ Project Structure

প্রথমে:

```text
pathlib_file_manager/
└── file_manager.py
```

`file_manager.py`:

```python
from pathlib import Path
import shutil
```

---

# 2️⃣ Root Directory

আমরা কোন directory manage করব সেটা নির্ধারণ করি:

```python
ROOT = Path.cwd()
```

অর্থাৎ program যে directory থেকে চালানো হচ্ছে সেটাই root।

আর চাইলে:

```python
ROOT = Path("my_files")
ROOT.mkdir(exist_ok=True)
```

---

# 3️⃣ List Files

```python
def list_files():

    print("\n--- Files ---")

    for item in ROOT.iterdir():

        if item.is_file():
            print(item.name)
```

Call:

```python
list_files()
```

---

# 4️⃣ List Directories

```python
def list_directories():

    print("\n--- Directories ---")

    for item in ROOT.iterdir():

        if item.is_dir():
            print(item.name)
```

---

# 5️⃣ Search Files ⭐⭐⭐

User extension দেবে:

```python
def search_files():

    extension = input(
        "Enter extension: "
    ).strip().lower()

    if not extension.startswith("."):
        extension = "." + extension

    print("\nResults:")

    found = False

    for file in ROOT.rglob(f"*{extension}"):

        if file.is_file():

            print(file)
            found = True

    if not found:
        print("No files found.")
```

Example:

```text
Enter extension: py

Results:

project/main.py
project/utils.py
tests/test_main.py
```

---

# 6️⃣ File Information

```python
def file_information():

    name = input(
        "Enter file name: "
    ).strip()

    path = ROOT / name

    if not path.exists():
        print("File not found.")
        return

    if not path.is_file():
        print("Not a file.")
        return

    info = path.stat()

    print("\n--- File Information ---")

    print("Name   :", path.name)
    print("Stem   :", path.stem)
    print("Suffix :", path.suffix)
    print("Parent :", path.parent)
    print("Size   :", info.st_size, "bytes")
```

---

# 7️⃣ Create Directory

```python
def create_directory():

    name = input(
        "Enter directory name: "
    ).strip()

    path = ROOT / name

    path.mkdir(
        parents=True,
        exist_ok=True
    )

    print("Directory created.")
```

---

# 8️⃣ Rename File ⭐⭐⭐

```python
def rename_file():

    old_name = input(
        "Current file name: "
    ).strip()

    new_name = input(
        "New file name: "
    ).strip()

    old_path = ROOT / old_name
    new_path = ROOT / new_name

    if not old_path.exists():
        print("File not found.")
        return

    old_path.rename(new_path)

    print("File renamed.")
```

---

# 9️⃣ Move File

```python
def move_file():

    name = input(
        "File name: "
    ).strip()

    folder_name = input(
        "Destination folder: "
    ).strip()

    source = ROOT / name
    folder = ROOT / folder_name

    if not source.is_file():
        print("File not found.")
        return

    if not folder.is_dir():
        print("Destination folder doesn't exist.")
        return

    destination = folder / source.name

    source.rename(destination)

    print("File moved.")
```

---

# 🔟 Delete File

এখানে safety খুব important।

```python
def delete_file():

    name = input(
        "File name: "
    ).strip()

    path = ROOT / name

    if not path.is_file():
        print("File not found.")
        return

    print("You are about to delete:", path)

    confirm = input(
        "Type YES to confirm: "
    )

    if confirm == "YES":

        path.unlink()

        print("File deleted.")

    else:

        print("Cancelled.")
```

এখানে আমরা সরাসরি delete করছি না।

---

# 1️⃣1️⃣ Directory Statistics ⭐⭐⭐

```python
def statistics():

    files = []
    directories = []

    total_size = 0

    for item in ROOT.rglob("*"):

        if item.is_file():

            files.append(item)

            total_size += item.stat().st_size

        elif item.is_dir():

            directories.append(item)

    print("\n--- Statistics ---")

    print(
        "Files       :",
        len(files)
    )

    print(
        "Directories :",
        len(directories)
    )

    print(
        "Total size  :",
        round(
            total_size / (1024 * 1024),
            2
        ),
        "MB"
    )
```

---

# 1️⃣2️⃣ Backup ⭐⭐⭐

আমরা পুরো root directory backup করব।

```python
def backup():

    backup_dir = ROOT.parent / (
        ROOT.name + "_backup"
    )

    shutil.copytree(
        ROOT,
        backup_dir,
        dirs_exist_ok=True
    )

    print(
        "Backup created:",
        backup_dir
    )
```

ধরো:

```text
project/
```

তাহলে তৈরি হবে:

```text
project/
project_backup/
```

---

# 1️⃣3️⃣ Main Menu

এখন সব function একসাথে করি:

```python
def show_menu():

    print("\n")
    print("==============================")
    print("       PATHLIB FILE MANAGER")
    print("==============================")

    print("1. List files")
    print("2. List directories")
    print("3. Search files")
    print("4. File information")
    print("5. Create directory")
    print("6. Rename file")
    print("7. Move file")
    print("8. Delete file")
    print("9. Statistics")
    print("10. Backup")
    print("0. Exit")
```

---

# 1️⃣4️⃣ Main Loop

```python
def main():

    while True:

        show_menu()

        choice = input(
            "\nChoose option: "
        ).strip()

        if choice == "1":
            list_files()

        elif choice == "2":
            list_directories()

        elif choice == "3":
            search_files()

        elif choice == "4":
            file_information()

        elif choice == "5":
            create_directory()

        elif choice == "6":
            rename_file()

        elif choice == "7":
            move_file()

        elif choice == "8":
            delete_file()

        elif choice == "9":
            statistics()

        elif choice == "10":
            backup()

        elif choice == "0":
            print("Goodbye!")
            break

        else:
            print("Invalid option.")
```

শেষে:

```python
if __name__ == "__main__":
    main()
```

---

# 🏆 Complete Project

সব code এক file-এ:

```python
from pathlib import Path
import shutil


ROOT = Path.cwd()


def show_menu():

    print("\n")
    print("==============================")
    print("       PATHLIB FILE MANAGER")
    print("==============================")

    print("1. List files")
    print("2. List directories")
    print("3. Search files")
    print("4. File information")
    print("5. Create directory")
    print("6. Rename file")
    print("7. Move file")
    print("8. Delete file")
    print("9. Statistics")
    print("10. Backup")
    print("0. Exit")


def list_files():

    print("\n--- Files ---")

    for item in ROOT.iterdir():

        if item.is_file():
            print(item.name)


def list_directories():

    print("\n--- Directories ---")

    for item in ROOT.iterdir():

        if item.is_dir():
            print(item.name)


def search_files():

    extension = input(
        "Enter extension: "
    ).strip().lower()

    if not extension.startswith("."):
        extension = "." + extension

    found = False

    print("\nResults:")

    for file in ROOT.rglob(f"*{extension}"):

        if file.is_file():

            print(file)
            found = True

    if not found:
        print("No files found.")


def file_information():

    name = input(
        "Enter file name: "
    ).strip()

    path = ROOT / name

    if not path.is_file():

        print("File not found.")
        return

    info = path.stat()

    print("\n--- File Information ---")

    print("Name   :", path.name)
    print("Stem   :", path.stem)
    print("Suffix :", path.suffix)
    print("Parent :", path.parent)
    print("Size   :", info.st_size, "bytes")


def create_directory():

    name = input(
        "Enter directory name: "
    ).strip()

    path = ROOT / name

    path.mkdir(
        parents=True,
        exist_ok=True
    )

    print("Directory created.")


def rename_file():

    old_name = input(
        "Current file name: "
    ).strip()

    new_name = input(
        "New file name: "
    ).strip()

    old_path = ROOT / old_name
    new_path = ROOT / new_name

    if not old_path.is_file():

        print("File not found.")
        return

    old_path.rename(new_path)

    print("File renamed.")


def move_file():

    name = input(
        "File name: "
    ).strip()

    folder_name = input(
        "Destination folder: "
    ).strip()

    source = ROOT / name
    folder = ROOT / folder_name

    if not source.is_file():

        print("File not found.")
        return

    if not folder.is_dir():

        print("Destination folder doesn't exist.")
        return

    destination = folder / source.name

    source.rename(destination)

    print("File moved.")


def delete_file():

    name = input(
        "File name: "
    ).strip()

    path = ROOT / name

    if not path.is_file():

        print("File not found.")
        return

    print(
        "You are about to delete:",
        path
    )

    confirm = input(
        "Type YES to confirm: "
    )

    if confirm == "YES":

        path.unlink()

        print("File deleted.")

    else:

        print("Cancelled.")


def statistics():

    file_count = 0
    directory_count = 0
    total_size = 0

    for item in ROOT.rglob("*"):

        if item.is_file():

            file_count += 1
            total_size += item.stat().st_size

        elif item.is_dir():

            directory_count += 1

    print("\n--- Statistics ---")

    print("Files       :", file_count)
    print(
        "Directories :",
        directory_count
    )

    print(
        "Total size  :",
        round(
            total_size / (1024 * 1024),
            2
        ),
        "MB"
    )


def backup():

    backup_dir = ROOT.parent / (
        ROOT.name + "_backup"
    )

    shutil.copytree(
        ROOT,
        backup_dir,
        dirs_exist_ok=True
    )

    print(
        "Backup created:",
        backup_dir
    )


def main():

    while True:

        show_menu()

        choice = input(
            "\nChoose option: "
        ).strip()

        if choice == "1":
            list_files()

        elif choice == "2":
            list_directories()

        elif choice == "3":
            search_files()

        elif choice == "4":
            file_information()

        elif choice == "5":
            create_directory()

        elif choice == "6":
            rename_file()

        elif choice == "7":
            move_file()

        elif choice == "8":
            delete_file()

        elif choice == "9":
            statistics()

        elif choice == "10":
            backup()

        elif choice == "0":
            print("Goodbye!")
            break

        else:
            print("Invalid option.")


if __name__ == "__main__":
    main()
```

---

# 🧠 পুরো `pathlib` Course-এর Summary

তুমি এখন এইগুলো জানো:

|Area|Important methods|
|---|---|
|Path create|`Path()`|
|Current directory|`Path.cwd()`|
|Home|`Path.home()`|
|Join path|`/`|
|Existence|`exists()`|
|File check|`is_file()`|
|Folder check|`is_dir()`|
|Create folder|`mkdir()`|
|Create file|`touch()`|
|Read|`read_text()`|
|Write|`write_text()`|
|Iterate|`iterdir()`|
|Search|`glob()`|
|Recursive search|`rglob()`|
|Rename|`rename()`|
|Replace|`replace()`|
|Delete file|`unlink()`|
|Delete empty folder|`rmdir()`|
|Metadata|`stat()`|
|File size|`stat().st_size`|
|Filename|`name`|
|Extension|`suffix`|
|Multiple extensions|`suffixes`|
|Filename without final suffix|`stem`|
|Parent|`parent`|
|Components|`parts`|
|Absolute path|`absolute()`|
|Resolved path|`resolve()`|

---

# 🎓 এখন তোমার Level

```text
Day 1
  ↓
Path basics

Day 2–4
  ↓
File & Directory operations

Day 5–6
  ↓
Traversal + Search

Day 7–8
  ↓
Rename + Delete + Metadata

Day 9
  ↓
Automation

Day 10
  ↓
🔥 Complete File Manager
```

**এখন `pathlib`-এর basic-to-intermediate practical knowledge তোমার হয়ে গেছে।**

পরবর্তী ধাপে সবচেয়ে ভালো হবে **Python Standard Library-এর পরের important module** শেখা—যেমন `json`, `csv`, `datetime`, `shutil`, `subprocess`, `re`, `collections`, `logging` ইত্যাদি।



