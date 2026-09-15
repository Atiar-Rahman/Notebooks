
হ্যাঁ, এখানেই অনেক beginner confuse হয়। `os` লিখে PyPI-তে search করলে **অনেক package আসা স্বাভাবিক**। কিন্তু তোমার **`os` শেখার জন্য PyPI-তে package খোঁজার দরকার নেই।**

### প্রথমে একটা গুরুত্বপূর্ণ বিষয়

Python-এর `os` হলো **standard library module**।

অর্থাৎ:

```python
import os
```

করলেই Python-এর সাথে থাকা `os` ব্যবহার করতে পারবে। আলাদা করে:

```bash
pip install os
```

করতে হবে না।

### তাহলে কীভাবে `os` শিখবে?

**Step 1 — Official Python documentation**

Search করো:

> Python os module official documentation

তারপর Python-এর official documentation-এর `os` module page পড়বে।

**Step 2 — শুধু গুরুত্বপূর্ণ অংশগুলো শেখো**

`os`-এর সব function মুখস্থ করার দরকার নেই। প্রথমে এগুলো:

|Topic|Example|
|---|---|
|Current directory|`os.getcwd()`|
|Change directory|`os.chdir()`|
|List files|`os.listdir()`|
|Environment variables|`os.environ`|
|Create directory|`os.mkdir()`|
|Create nested directories|`os.makedirs()`|
|Rename|`os.rename()`|
|Delete file|`os.remove()`|
|Delete directory|`os.rmdir()`|
|Check path|`os.path.exists()`|
|Check file|`os.path.isfile()`|
|Check directory|`os.path.isdir()`|
|Join paths|`os.path.join()`|
|File extension/path info|`os.path.splitext()`|

### Step 3 — তারপর `os.path`

`os` শেখার সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি হলো:

```python
import os

path = os.path.join("data", "images", "photo.png")

print(path)
print(os.path.exists(path))
print(os.path.isfile(path))
print(os.path.dirname(path))
print(os.path.basename(path))
```

### Step 4 — Mini project

শুধু function শেখার বদলে একটা ছোট project বানাও:

**File Organizer**

যেমন:

```text
Downloads/
    photo.jpg
    song.mp3
    document.pdf
    video.mp4
```

Python দিয়ে automatically:

```text
Downloads/
    Images/
    Music/
    Documents/
    Videos/
```

এবং files তাদের category অনুযায়ী move করবে।

এতে `os.listdir()`, `os.path`, `os.mkdir()`, `os.rename()` ইত্যাদি বাস্তবে শিখে যাবে।

---

### ⭐ আর PyPI কীভাবে ব্যবহার করবে?

এটা মনে রাখো:

> **Standard Library → Python Docs**  
> **Third-party package → PyPI + Official Documentation**

যেমন:

```text
os              → Python Docs
json            → Python Docs
pathlib         → Python Docs

requests        → PyPI + Requests documentation
pandas          → PyPI + Pandas documentation
numpy            → PyPI + NumPy documentation
django           → PyPI + Django documentation
```

আর একটা গুরুত্বপূর্ণ বিষয়: **`os`-এর নতুন code-এ অনেক file/path কাজের জন্য `pathlib`-ও শেখা উচিত।** `os` বোঝার পর `pathlib` শেখালে Python file handling অনেক পরিষ্কার হবে।

চাইলে আমরা এখন **`os` package/module একদম course-এর মতো Step 1 থেকে practical করে** শুরু করতে পারি।

---

হ্যাঁ, **এটাই Python-এর official documentation**। ✅

[Python `os` module official documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

URL-টা দেখলেই বোঝা যায়:

```text
https://docs.python.org/3/
                 ↑
          Python official docs
```

আর:

```text
/library/os.html
```

মানে Python Standard Library-এর `os` module-এর documentation।

### তুমি কীভাবে এই page থেকে শিখবে?

পুরো page শুরু থেকে শেষ পর্যন্ত পড়ার দরকার নেই। এই order-এ যাও:

**1. `os.getcwd()`** → current directory  
**2. `os.chdir()`** → directory change  
**3. `os.listdir()`** → files/folders দেখা  
**4. `os.mkdir()` / `os.makedirs()`** → folder তৈরি  
**5. `os.remove()`** → file delete  
**6. `os.rename()`** → rename/move  
**7. `os.environ`** → environment variables  
**8. `os.path`** → path handling

তারপর **প্রতিটা function নিজে code করে practice করবে।**

চাইলে আমি তোমাকে এই official documentation ধরেই **`os` Module — Day 1 থেকে Day 3 complete course** শুরু করাতে পারি।


---

অবশ্যই। আমরা **Python official documentation**-কে মূল reference ধরে `os` module শিখব। [Python `os` module official documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

# 🐍 OS Module — Day 1 → Day 3

### Course Goal

৩ দিনে তুমি শিখবে:

| Day       | Focus                             |
| --------- | --------------------------------- |
| **Day 1** | Directory + Files basics          |
| **Day 2** | `os.path` + Environment Variables |
| **Day 3** | File Management + Mini Project    |

---

# 🟢 DAY 1 — OS Fundamentals

## 1. `import os`

Python-এর built-in `os` module ব্যবহার করতে:

```python
import os
```

কোনো `pip install` দরকার নেই।

---

## 2. `os.getcwd()`

`getcwd()` = **Get Current Working Directory**

```python
import os

current_directory = os.getcwd()

print(current_directory)
```

যদি তোমার terminal এই directory-তে থাকে:

```text
/home/atiar/python
```

তাহলে output হবে:

```text
/home/atiar/python
```

### Practice

```python
import os

print(os.getcwd())
```

**নিজে run করে দেখো।**

---

# 3. `os.chdir()`

`chdir()` = **Change Directory**

ধরো:

```text
/home/atiar
```

থেকে:

```text
/home/atiar/Documents
```

যেতে চাও।

```python
import os

os.chdir("/home/atiar/Documents")

print(os.getcwd())
```

Output:

```text
/home/atiar/Documents
```

### ⚠️ Important

তোমার নিজের computer-এর actual path ব্যবহার করবে।

---

# 4. `os.listdir()`

এটা খুব গুরুত্বপূর্ণ।

একটি directory-এর ভিতরের files/folders দেখতে:

```python
import os

items = os.listdir()

print(items)
```

উদাহরণ:

```text
['main.py', 'data', 'image.jpg', 'notes.txt']
```

নির্দিষ্ট directory:

```python
items = os.listdir("/home/atiar/Documents")

print(items)
```

---

# 5. File নাকি Folder?

এখানে `os.path` ব্যবহার করব।

```python
import os

items = os.listdir()

for item in items:
    if os.path.isfile(item):
        print("File:", item)

    elif os.path.isdir(item):
        print("Folder:", item)
```

Output হতে পারে:

```text
File: main.py
File: notes.txt
Folder: data
Folder: projects
```

এটা খুব গুরুত্বপূর্ণ concept।

---

# 6. `os.mkdir()`

নতুন একটি directory তৈরি:

```python
import os

os.mkdir("test")
```

তাহলে:

```text
current_folder/
    test/
```

তৈরি হবে।

### Better practice

```python
import os

if not os.path.exists("test"):
    os.mkdir("test")
```

এতে `test` আগে থেকে থাকলে error হবে না।

---

# 7. `os.makedirs()`

Nested directories তৈরি করতে:

```python
import os

os.makedirs("project/data/images")
```

এতে:

```text
project/
└── data/
    └── images/
```

তৈরি হবে।

---

# 📝 Day 1 Practice

এই program নিজে বানানোর চেষ্টা করো:

```text
Current Directory
        ↓
List all items
        ↓
Separate Files and Folders
        ↓
Create "practice" folder
        ↓
Create "practice/images" folder
```

Expected structure:

```text
practice/
└── images/
```

---

# 🟡 DAY 2 — `os.path` + Environment

এখন আসবে `os` module-এর সবচেয়ে useful অংশগুলোর একটি।

## 1. `os.path.exists()`

কোনো path আছে কিনা:

```python
import os

print(os.path.exists("test"))
```

Output:

```text
True
```

অথবা:

```text
False
```

---

# 2. `os.path.isfile()`

কোনো path file কিনা:

```python
import os

print(os.path.isfile("main.py"))
```

---

# 3. `os.path.isdir()`

কোনো path directory কিনা:

```python
import os

print(os.path.isdir("data"))
```

---

# 4. `os.path.join()`

এটা **অত্যন্ত গুরুত্বপূর্ণ**।

ধরো:

```python
folder = "data"
filename = "image.jpg"

path = os.path.join(folder, filename)

print(path)
```

Output Linux-এ:

```text
data/image.jpg
```

Windows-এ appropriate separator ব্যবহার করবে।

তাই manually:

```python
path = "data/" + filename
```

করার চেয়ে:

```python
path = os.path.join("data", filename)
```

ব্যবহার করা ভালো।

---

# 5. `basename()`

```python
import os

path = "/home/atiar/data/image.jpg"

print(os.path.basename(path))
```

Output:

```text
image.jpg
```

---

# 6. `dirname()`

```python
path = "/home/atiar/data/image.jpg"

print(os.path.dirname(path))
```

Output:

```text
/home/atiar/data
```

---

# 7. `splitext()`

File name এবং extension আলাদা করতে:

```python
import os

filename = "photo.jpg"

name, extension = os.path.splitext(filename)

print(name)
print(extension)
```

Output:

```text
photo
.jpg
```

এটা file organizer-এর মতো project-এ অনেক কাজে লাগে।

---

# 8. Environment Variables

Python program থেকে environment variable access করতে:

```python
import os

print(os.environ)
```

একটি নির্দিষ্ট variable:

```python
print(os.environ.get("HOME"))
```

Linux-এ output হতে পারে:

```text
/home/atiar
```

### কেন গুরুত্বপূর্ণ?

Backend development-এ environment variables ব্যবহার করে:

```text
DATABASE_URL
SECRET_KEY
API_KEY
DEBUG
```

এরকম configuration রাখা হয়।

---

# 🟠 DAY 3 — File Management

এখন আমরা `os` দিয়ে actual file management করব।

## 1. `os.rename()`

File rename:

```python
import os

os.rename("old.txt", "new.txt")
```

Folder rename-ও করা যায়।

---

# 2. `os.remove()`

File delete:

```python
import os

os.remove("new.txt")
```

⚠️ এটা practice folder-এর মধ্যে ব্যবহার করবে।

---

# 3. `os.rmdir()`

Empty directory delete:

```python
import os

os.rmdir("test")
```

Directory-এর ভিতরে file থাকলে সাধারণত আগে contents সরাতে হবে।

---

# 4. File List + Extension

এখন একটি practical example:

```python
import os

files = os.listdir()

for file in files:

    if os.path.isfile(file):

        name, extension = os.path.splitext(file)

        print(
            "Name:",
            name,
            "Extension:",
            extension
        )
```

Possible output:

```text
Name: main Extension: .py
Name: photo Extension: .jpg
Name: notes Extension: .txt
```

---

# 🚀 Day 3 Mini Project — File Organizer

এখন সবচেয়ে গুরুত্বপূর্ণ project।

ধরো:

```text
Downloads/
├── photo.jpg
├── image.png
├── song.mp3
├── movie.mp4
├── notes.txt
└── report.pdf
```

আমরা চাই:

```text
Downloads/
├── Images/
│   ├── photo.jpg
│   └── image.png
│
├── Music/
│   └── song.mp3
│
├── Videos/
│   └── movie.mp4
│
└── Documents/
    ├── notes.txt
    └── report.pdf
```

এখানে তোমাকে একসাথে ব্যবহার করতে হবে:

```text
os.listdir()
os.path.join()
os.path.isfile()
os.path.splitext()
os.path.exists()
os.mkdir()
os.rename()
```

**Bonus:** পরে `shutil.move()` শিখলে file সরানোর কাজ আরও পরিষ্কারভাবে করতে পারবে।

---

# 📚 3-Day Revision Sheet

|Function|কাজ|
|---|---|
|`os.getcwd()`|Current directory|
|`os.chdir()`|Directory change|
|`os.listdir()`|Directory contents|
|`os.mkdir()`|Directory তৈরি|
|`os.makedirs()`|Nested directories তৈরি|
|`os.remove()`|File delete|
|`os.rmdir()`|Empty directory delete|
|`os.rename()`|Rename|
|`os.path.exists()`|Path exists?|
|`os.path.isfile()`|File?|
|`os.path.isdir()`|Directory?|
|`os.path.join()`|Path তৈরি|
|`os.path.basename()`|Filename বের করা|
|`os.path.dirname()`|Parent directory|
|`os.path.splitext()`|Extension আলাদা করা|
|`os.environ`|Environment variables|

## 🎯 শেখার নিয়ম

প্রতিটি function-এর জন্য এই pattern follow করবে:

**Documentation → Example → নিজের code → ছোট problem → project**

Official docs-এ কোনো function দেখলে শুধু syntax মুখস্থ করবে না। **"কেন ব্যবহার করব?" + "কখন ব্যবহার করব?"**—এই দুটো বুঝবে।

পরবর্তী ধাপে আমরা **Day 1-এর `os.getcwd()`, `os.chdir()`, `os.listdir()` একদম হাতে-কলমে exercises দিয়ে শুরু** করতে পারি।


# 🐍 Python `os` Module — Day 1

আজ আমরা শুধু **৩টা জিনিস** খুব ভালোভাবে শিখব:

1. `os.getcwd()`
    
2. `os.chdir()`
    
3. `os.listdir()`
    

Official reference: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

---

## 1️⃣ `import os`

প্রথমে:

```python
import os
```

`os` Python-এর **standard library module**, তাই `pip install os` করতে হয় না।

---

# 2️⃣ `os.getcwd()`

### `getcwd` = Get Current Working Directory

তোমার Python program **কোন directory থেকে কাজ করছে**, সেটা জানতে:

```python
import os

print(os.getcwd())
```

তোমার Ubuntu-তে এমন output আসতে পারে:

```text
/home/atiar/python
```

### বুঝে রাখো

```text
os
 ↓
getcwd()
 ↓
বর্তমান working directory
```

---

## 🧪 Exercise 1

এই code run করো:

```python
import os

current_path = os.getcwd()

print("Current Directory:", current_path)
```

### Expected

```text
Current Directory: /home/atiar/...
```

**Task:** তোমার computer-এ যে exact path দেখাবে সেটা লক্ষ্য করো।

---

# 3️⃣ `os.chdir()`

### `chdir` = Change Directory

Current directory পরিবর্তন করতে ব্যবহার হয়।

ধরো তোমার current directory:

```text
/home/atiar
```

এবং সেখানে `Documents` folder আছে।

```python
import os

os.chdir("/home/atiar/Documents")

print(os.getcwd())
```

Output:

```text
/home/atiar/Documents
```

অর্থাৎ:

```text
আগে:
 /home/atiar

       ↓ os.chdir()

পরে:
 /home/atiar/Documents
```

---

## 🧪 Exercise 2

প্রথমে তোমার current directory দেখো:

```python
import os

print(os.getcwd())
```

তারপর এমন একটি existing folder-এ যাও:

```python
os.chdir("Documents")
```

তারপর:

```python
print(os.getcwd())
```

### ⚠️ গুরুত্বপূর্ণ

যদি `Documents` current directory-এর ভিতরে না থাকে, তাহলে error আসবে।

তাই আগে:

```python
print(os.listdir())
```

দিয়ে দেখো কোন folder আছে।

---

# 4️⃣ `os.listdir()`

এটা Day 1-এর সবচেয়ে গুরুত্বপূর্ণ function।

একটি directory-এর ভিতরে কী কী আছে সেটা দেখতে:

```python
import os

print(os.listdir())
```

ধরো output:

```text
['main.py', 'data', 'image.jpg', 'notes.txt']
```

এখানে:

```text
main.py     → file
data        → folder
image.jpg   → file
notes.txt   → file
```

---

## নির্দিষ্ট directory-এর contents

```python
import os

print(os.listdir("/home/atiar/Documents"))
```

এতে `Documents` folder-এর ভিতরের সব item দেখাবে।

---

# 5️⃣ `listdir()` + Loop

এখন আমরা একটু useful code লিখি:

```python
import os

items = os.listdir()

for item in items:
    print(item)
```

Output:

```text
main.py
data
image.jpg
notes.txt
```

### এখানে কী হচ্ছে?

```text
os.listdir()
      ↓
সব item-এর list
      ↓
for loop
      ↓
একটা একটা item
      ↓
print()
```

---

# 🧠 খুব গুরুত্বপূর্ণ Concept

`os.getcwd()` আর `os.listdir()` এক জিনিস নয়।

|Function|কাজ|
|---|---|
|`os.getcwd()`|আমি **কোথায় আছি?**|
|`os.chdir()`|আমি **অন্য জায়গায় যাব**|
|`os.listdir()`|এই জায়গায় **কী কী আছে?**|

একটা সহজ analogy:

```text
getcwd()   → আমি কোন ঘরে আছি?
chdir()    → অন্য ঘরে যাই
listdir()  → এই ঘরে কী কী আছে দেখি
```

---

# 🔥 Exercise 3 — তিনটাকে একসাথে

নিজে আগে চেষ্টা করো:

```python
import os

print("Current Directory:")
print(os.getcwd())

print("\nItems:")
print(os.listdir())
```

---

# 🧩 Exercise 4 — একটু কঠিন

এমন output তৈরি করো:

```text
Current Directory: /home/atiar/...

Items:
- main.py
- data
- image.jpg
- notes.txt
```

Hint:

```python
print("Current Directory:", os.getcwd())

print("\nItems:")

for item in os.listdir():
    print("-", item)
```

---

# 🎯 Day 1 Challenge

এখন **নিজে code না দেখে** এই program বানানোর চেষ্টা করো:

### Requirements

Program:

1. Current directory দেখাবে
    
2. Current directory-এর সব item দেখাবে
    
3. মোট কতগুলো item আছে সেটা দেখাবে
    

Expected:

```text
Current Directory: /home/atiar/python

Items:
- main.py
- data
- image.jpg
- notes.txt

Total Items: 4
```

### শেষের অংশের জন্য hint:

```python
items = os.listdir()

print("Total Items:", len(items))
```

---

## ✅ Day 1-এর আজকের Target

আজ শুধু এগুলো mastery করো:

```python
import os

os.getcwd()
os.chdir()
os.listdir()
```

**পরবর্তী ধাপে `os.path`-এ যাওয়ার আগে এই ৩টা দিয়ে ৫–১০টা ছোট exercise করো।**


# 🐍 Python `os` Module — Day 2

আজ আমরা `os.path` শিখব। Day 1-এ শিখেছিলে:

```python
os.getcwd()
os.chdir()
os.listdir()
```

আজকের মূল বিষয়:

```text
os.path.exists()
os.path.isfile()
os.path.isdir()
os.path.join()
os.path.basename()
os.path.dirname()
os.path.splitext()
```

Official documentation: [Python `os.path` documentation](https://docs.python.org/3/library/os.path.html?utm_source=chatgpt.com)

---

# 1️⃣ `os.path.exists()`

কোনো file বা folder **আছে কিনা** check করে।

```python
import os

print(os.path.exists("data"))
```

যদি `data` থাকে:

```text
True
```

না থাকলে:

```text
False
```

### কেন গুরুত্বপূর্ণ?

ধরো তুমি folder তৈরি করতে চাও:

```python
if not os.path.exists("data"):
    os.mkdir("data")
```

এতে আগে check করবে folder already আছে কিনা।

---

# 2️⃣ `os.path.isfile()`

কোনো path **file কিনা** check করে।

```python
import os

print(os.path.isfile("main.py"))
```

Output:

```text
True
```

যদি `main.py` file হয়।

---

# 3️⃣ `os.path.isdir()`

কোনো path **directory/folder কিনা** check করে।

```python
import os

print(os.path.isdir("data"))
```

Output:

```text
True
```

---

## 🧠 তিনটাকে একসাথে বুঝো

ধরো:

```text
project/
├── main.py
└── data/
```

তাহলে:

```python
os.path.exists("main.py")
```

→ `True`

```python
os.path.isfile("main.py")
```

→ `True`

```python
os.path.isdir("main.py")
```

→ `False`

আর:

```python
os.path.exists("data")
```

→ `True`

```python
os.path.isfile("data")
```

→ `False`

```python
os.path.isdir("data")
```

→ `True`

---

# 4️⃣ `os.path.join()`

এটা **খুব গুরুত্বপূর্ণ**।

ধরো:

```python
folder = "data"
filename = "photo.jpg"
```

তুমি path বানাতে চাও:

```text
data/photo.jpg
```

তাহলে:

```python
import os

path = os.path.join("data", "photo.jpg")

print(path)
```

Output Linux-এ:

```text
data/photo.jpg
```

### কেন `/` manually ব্যবহার না করে `join()`?

এটা:

```python
path = "data/" + "photo.jpg"
```

এর চেয়ে:

```python
path = os.path.join("data", "photo.jpg")
```

বেশি portable এবং path handling-এর জন্য ভালো।

---

# 5️⃣ Nested Path

```python
import os

path = os.path.join(
    "project",
    "data",
    "images",
    "photo.jpg"
)

print(path)
```

Output:

```text
project/data/images/photo.jpg
```

---

# 6️⃣ `os.path.basename()`

একটি complete path থেকে **শেষের অংশ** বের করে।

```python
import os

path = "/home/atiar/project/data/photo.jpg"

print(os.path.basename(path))
```

Output:

```text
photo.jpg
```

সহজভাবে:

```text
/home/atiar/project/data/photo.jpg
                                  ↑
                              basename
```

---

# 7️⃣ `os.path.dirname()`

Path-এর **parent directory** বের করে।

```python
import os

path = "/home/atiar/project/data/photo.jpg"

print(os.path.dirname(path))
```

Output:

```text
/home/atiar/project/data
```

সহজভাবে:

```text
/home/atiar/project/data/photo.jpg
                         ↑
                       dirname
```

---

# 8️⃣ `basename()` + `dirname()`

একসাথে:

```python
import os

path = "/home/atiar/project/data/photo.jpg"

print("File:", os.path.basename(path))
print("Folder:", os.path.dirname(path))
```

Output:

```text
File: photo.jpg
Folder: /home/atiar/project/data
```

---

# 9️⃣ `os.path.splitext()`

File name এবং extension আলাদা করে।

```python
import os

name, extension = os.path.splitext("photo.jpg")

print(name)
print(extension)
```

Output:

```text
photo
.jpg
```

আর:

```python
name, extension = os.path.splitext("report.pdf")

print(name)
print(extension)
```

Output:

```text
report
.pdf
```

---

# 🔥 Practical Example

ধরো directory:

```text
files/
├── photo.jpg
├── report.pdf
├── song.mp3
└── data.csv
```

আমরা প্রতিটি file-এর নাম এবং extension বের করব।

```python
import os

files = os.listdir("files")

for file in files:

    if os.path.isfile(os.path.join("files", file)):

        name, extension = os.path.splitext(file)

        print("Name:", name)
        print("Extension:", extension)
        print()
```

Output:

```text
Name: photo
Extension: .jpg

Name: report
Extension: .pdf

Name: song
Extension: .mp3

Name: data
Extension: .csv
```

এখানে **একটা গুরুত্বপূর্ণ বিষয়** লক্ষ্য করো:

```python
os.path.join("files", file)
```

কেন ব্যবহার করেছি?

কারণ `os.path.isfile()`-কে শুধু:

```python
file
```

দিলে Python current directory-তে file খুঁজবে।

কিন্তু আমাদের file আছে:

```text
files/photo.jpg
```

তাই complete path তৈরি করেছি।

---

# 🧪 Day 2 Exercises

### Exercise 1 — Check existence

নিজে লিখো:

```python
import os

path = "data"

# data exists কিনা check করো
```

---

### Exercise 2 — File নাকি folder?

একটি loop লিখে current directory-এর প্রতিটি item:

```text
File: ...
Folder: ...
```

এভাবে print করো।

Hint:

```python
for item in os.listdir():
    if os.path.isfile(item):
        ...
    elif os.path.isdir(item):
        ...
```

---

### Exercise 3 — File extension

নিজে এমন program বানাও:

```text
photo.jpg → .jpg
document.pdf → .pdf
song.mp3 → .mp3
program.py → .py
```

---

### Exercise 4 — Path builder

এই structure-এর path তৈরি করো:

```text
project/
    data/
        images/
            photo.jpg
```

শুধু `os.path.join()` ব্যবহার করে।

---

# 🎯 Day 2 Challenge

এই program **নিজে** বানানোর চেষ্টা করো:

```text
Current Directory: /home/...

Files:
- main.py       (.py)
- photo.jpg     (.jpg)
- notes.txt     (.txt)

Folders:
- data
- projects

Total Files: 3
Total Folders: 2
```

তোমার প্রধান weapons হবে:

```python
os.getcwd()
os.listdir()
os.path.join()
os.path.isfile()
os.path.isdir()
os.path.splitext()
```

**Day 2-এর মূল concept এক লাইনে:**

> `os` দিয়ে directory-এর কাজ করি, আর `os.path` দিয়ে file/path সম্পর্কে information বের করি।


---
# 🐍 Python `os` Module — Day 3

আজ আমরা `os` দিয়ে **file & folder management** শিখব।

Day 1:

```python
os.getcwd()
os.chdir()
os.listdir()
```

Day 2:

```python
os.path.exists()
os.path.isfile()
os.path.isdir()
os.path.join()
os.path.basename()
os.path.dirname()
os.path.splitext()
```

আজ:

```python
os.mkdir()
os.makedirs()
os.rename()
os.remove()
os.rmdir()
```

Official documentation: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

---

# 1️⃣ `os.mkdir()` — Folder তৈরি

```python
import os

os.mkdir("data")
```

তাহলে:

```text
project/
├── main.py
└── data/
```

হবে।

### ⚠️ যদি folder আগে থেকেই থাকে

```python
os.mkdir("data")
```

চালালে error আসতে পারে।

তাই নিরাপদভাবে:

```python
import os

if not os.path.exists("data"):
    os.mkdir("data")
```

---

# 2️⃣ `os.makedirs()` — Nested Folder

একাধিক level-এর folder একসাথে তৈরি করতে:

```python
import os

os.makedirs("project/data/images")
```

তৈরি হবে:

```text
project/
└── data/
    └── images/
```

আরও নিরাপদভাবে:

```python
os.makedirs("project/data/images", exist_ok=True)
```

`exist_ok=True` দিলে folder আগে থেকেই থাকলেও error হবে না।

---

# 3️⃣ `os.rename()` — Rename

ধরো:

```text
old.txt
```

কে:

```text
new.txt
```

করতে চাও।

```python
import os

os.rename("old.txt", "new.txt")
```

---

## Folder rename

```python
os.rename("old_folder", "new_folder")
```

এটাও করা যায়।

---

# 4️⃣ `os.remove()` — File Delete

```python
import os

os.remove("new.txt")
```

এতে `new.txt` delete হবে।

### ⚠️ সাবধান

`os.remove()` ব্যবহার করার আগে নিশ্চিত হও যে file-টি সত্যিই delete করতে চাও।

Practice করার সময় আলাদা একটা folder ব্যবহার করো।

---

# 5️⃣ `os.rmdir()` — Empty Folder Delete

```python
import os

os.rmdir("data")
```

এটি একটি **empty directory** remove করে।

যদি folder-এর ভিতরে file থাকে, আগে contents handle করতে হবে।

---

# 6️⃣ `rename()` দিয়ে Move করা

`os.rename()` শুধু rename নয়, একই filesystem-এর মধ্যে path বদলে file সরাতেও ব্যবহার করা যেতে পারে।

ধরো:

```text
files/
    photo.jpg
```

এটাকে:

```text
images/
    photo.jpg
```

করতে:

```python
import os

os.rename(
    "files/photo.jpg",
    "images/photo.jpg"
)
```

তবে বাস্তব file-moving-এর জন্য পরে `shutil.move()` শেখা আরও ভালো হবে।

---

# 7️⃣ সবগুলো একসাথে

একটি safe practice:

```python
import os

# Create folder
if not os.path.exists("practice"):
    os.mkdir("practice")

# Create nested folders
os.makedirs("practice/images", exist_ok=True)

print(os.listdir("practice"))
```

Output:

```text
['images']
```

---

# 🔥 8️⃣ File Organizer Project

এখন Day 3-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

ধরো:

```text
downloads/
├── photo.jpg
├── image.png
├── song.mp3
├── movie.mp4
├── notes.txt
└── report.pdf
```

আমরা চাই:

```text
downloads/
├── Images/
│   ├── photo.jpg
│   └── image.png
│
├── Music/
│   └── song.mp3
│
├── Videos/
│   └── movie.mp4
│
└── Documents/
    ├── notes.txt
    └── report.pdf
```

এই project-এ Day 1 + Day 2 + Day 3-এর concepts একসাথে লাগবে।

---

## Step 1 — Extensions চিনে নেওয়া

```python
import os

files = os.listdir("downloads")

for file in files:
    name, extension = os.path.splitext(file)

    print(file, "->", extension)
```

Output:

```text
photo.jpg -> .jpg
image.png -> .png
song.mp3 -> .mp3
movie.mp4 -> .mp4
notes.txt -> .txt
report.pdf -> .pdf
```

---

# Step 2 — Category তৈরি

```python
import os

base = "downloads"

folders = [
    "Images",
    "Music",
    "Videos",
    "Documents"
]

for folder in folders:
    path = os.path.join(base, folder)
    os.makedirs(path, exist_ok=True)
```

এখন:

```text
downloads/
├── Images/
├── Music/
├── Videos/
└── Documents/
```

তৈরি হবে।

---

# Step 3 — File অনুযায়ী category নির্বাচন

এখন extension দেখে category:

```python
import os

image_extensions = [".jpg", ".jpeg", ".png"]
music_extensions = [".mp3", ".wav"]
video_extensions = [".mp4", ".mkv"]
document_extensions = [".txt", ".pdf"]

for file in os.listdir("downloads"):

    name, extension = os.path.splitext(file)

    if extension in image_extensions:
        print(file, "-> Images")

    elif extension in music_extensions:
        print(file, "-> Music")

    elif extension in video_extensions:
        print(file, "-> Videos")

    elif extension in document_extensions:
        print(file, "-> Documents")
```

এখানে তুমি গুরুত্বপূর্ণ একটা Python concept শিখছ:

```python
extension in image_extensions
```

মানে extension ওই list-এর মধ্যে আছে কিনা।

---

# 🧠 Day 3-এর Core Concept

আজকের functionগুলো মনে রাখার সহজ উপায়:

|Function|কাজ|
|---|---|
|`os.mkdir()`|একটি folder তৈরি|
|`os.makedirs()`|nested folders তৈরি|
|`os.rename()`|rename / path change|
|`os.remove()`|file delete|
|`os.rmdir()`|empty folder delete|

---

# 🎯 Day 3 Exercises

### Exercise 1

`practice` নামে folder তৈরি করো।

তার ভিতরে:

```text
practice/
└── python/
    └── os/
```

তৈরি করো।

---

### Exercise 2

তৈরি করো:

```text
old.txt
```

তারপর rename করে:

```text
new.txt
```

করো।

---

### Exercise 3

একটি folder তৈরি করো:

```text
temporary/
```

তারপর সেটা delete করো।

---

### Exercise 4 — Challenge ⭐

নিজে এমন program বানাও:

```text
downloads/
    photo.jpg
    song.mp3
    report.pdf
```

Program automatically তৈরি করবে:

```text
downloads/
├── Images/
├── Music/
└── Documents/
```

তারপর extension অনুযায়ী files organize করবে।

**Hint:** আজকের সবকিছু একসাথে লাগবে:

```python
os.listdir()
os.path.join()
os.path.isfile()
os.path.splitext()
os.makedirs()
os.rename()
```

---

# 🏁 Day 1–3 Complete

এখন তুমি `os` module-এর basic file-system workflow বুঝে গেছ:

```text
Current location
      ↓
os.getcwd()

Directory change
      ↓
os.chdir()

See contents
      ↓
os.listdir()

Check path
      ↓
os.path.exists()

File / Folder
      ↓
isfile() / isdir()

Build path
      ↓
os.path.join()

Create
      ↓
mkdir() / makedirs()

Rename / Move
      ↓
rename()

Delete
      ↓
remove() / rmdir()
```

### পরের logical step

**Day 4 → `os.environ`, environment variables, `os.system()`, `os.name`, `os.walk()` এবং তারপর `os` দিয়ে একটি real-world project।**

---
# 🐍 Python `os` Module — Day 4

আজ আমরা `os` module-এর একটু **advanced এবং practical** অংশ শিখব:

1. `os.environ`
    
2. `os.getenv()`
    
3. `os.name`
    
4. `os.system()`
    
5. `os.walk()`
    

Official documentation: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

---

# 1️⃣ `os.environ`

`os.environ` হলো environment variables-এর একটি mapping।

```python
import os

print(os.environ)
```

অনেকগুলো variable দেখতে পাবে।

যেমন Linux-এ থাকতে পারে:

```text
HOME
PATH
USER
SHELL
LANG
```

---

## নির্দিষ্ট variable

```python
import os

print(os.environ["HOME"])
```

Linux-এ এমন output হতে পারে:

```text
/home/atiar
```

### ⚠️ কিন্তু variable না থাকলে?

```python
print(os.environ["MY_VARIABLE"])
```

এতে `KeyError` হতে পারে।

তাই সাধারণত:

```python
print(os.environ.get("MY_VARIABLE"))
```

ব্যবহার করা নিরাপদ।

Output:

```text
None
```

---

# 2️⃣ `os.getenv()`

Environment variable পাওয়ার আরেকটি সহজ উপায়:

```python
import os

home = os.getenv("HOME")

print(home)
```

এটা প্রায় এরকম:

```python
os.environ.get("HOME")
```

---

## Default value

এটা খুব useful:

```python
import os

debug = os.getenv("DEBUG", "False")

print(debug)
```

যদি `DEBUG` না থাকে:

```text
False
```

পাবে।

---

# 🔥 Backend-এ কেন গুরুত্বপূর্ণ?

তুমি Django/FastAPI backend করলে secret configuration code-এর মধ্যে hard-code না করে environment variable ব্যবহার করতে পারো।

যেমন:

```text
SECRET_KEY
DATABASE_URL
API_KEY
DEBUG
```

তারপর Python:

```python
import os

secret_key = os.getenv("SECRET_KEY")
```

এটা production development-এর খুব গুরুত্বপূর্ণ concept।

---

# 3️⃣ `os.name`

Operating system-এর basic indication পেতে:

```python
import os

print(os.name)
```

Linux/Unix-এ সাধারণত:

```text
posix
```

Windows-এ:

```text
nt
```

তবে মনে রাখবে, `os.name` তোমাকে exact distro/version বলে না।

---

# 4️⃣ `os.system()`

Operating system-এর shell command চালাতে পারে:

```python
import os

os.system("echo Hello")
```

Output:

```text
Hello
```

Linux-এ:

```python
os.system("pwd")
```

এটা current directory দেখাতে পারে।

```python
os.system("ls")
```

directory contents দেখাতে পারে।

### ⚠️ Important

`os.system()` শেখা useful, কিন্তু নতুন Python code-এ external commands চালানোর জন্য পরে **`subprocess` module** শেখা বেশি ভালো।

---

# 5️⃣ `os.walk()` ⭐

এটা Day 4-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

`os.walk()` directory tree-এর মধ্যে **recursively** ঘুরে files/folders খুঁজে দেয়।

ধরো:

```text
project/
├── main.py
├── data/
│   ├── train.csv
│   └── test.csv
└── images/
    ├── cat.jpg
    └── dog.jpg
```

তাহলে:

```python
import os

for root, dirs, files in os.walk("project"):
    print("ROOT:", root)
    print("DIRS:", dirs)
    print("FILES:", files)
```

এটা পুরো directory tree ঘুরে দেখবে।

---

# 6️⃣ শুধু সব files বের করা

এটা খুব practical:

```python
import os

for root, dirs, files in os.walk("project"):

    for file in files:
        print(os.path.join(root, file))
```

Output:

```text
project/main.py
project/data/train.csv
project/data/test.csv
project/images/cat.jpg
project/images/dog.jpg
```

এখানে:

```python
os.path.join(root, file)
```

ব্যবহার করে complete path তৈরি করেছি।

---

# 🧠 `listdir()` বনাম `walk()`

এটা খুব ভালোভাবে বুঝে রাখো।

|Function|কাজ|
|---|---|
|`os.listdir()`|একটি directory-এর immediate contents|
|`os.walk()`|directory + তার ভিতরের সব subdirectory recursively|

উদাহরণ:

```text
project/
├── main.py
└── data/
    └── train/
        └── image.jpg
```

`os.listdir("project")`:

```text
main.py
data
```

কিন্তু `os.walk("project")` শেষ পর্যন্ত:

```text
main.py
train/
image.jpg
```

সব খুঁজে পেতে পারে।

---

# 🧪 Day 4 Exercise 1

তোমার নিজের computer-এর একটি test folder নাও:

```text
practice/
├── a.txt
├── data/
│   ├── b.txt
│   └── c.txt
└── images/
    └── photo.jpg
```

তারপর `os.walk()` দিয়ে শুধু files print করো।

Expected:

```text
practice/a.txt
practice/data/b.txt
practice/data/c.txt
practice/images/photo.jpg
```

---

# 🧪 Exercise 2

শুধু `.py` files খুঁজে বের করো।

Hint:

```python
for root, dirs, files in os.walk("."):

    for file in files:

        if file.endswith(".py"):
            print(os.path.join(root, file))
```

এটা তোমার Python project-এর মধ্যে Python files খুঁজতে পারবে।

---

# 🧪 Exercise 3

Environment variable:

```python
import os

print("HOME:", os.getenv("HOME"))
print("USER:", os.getenv("USER"))
print("SHELL:", os.getenv("SHELL"))
```

নিজের Ubuntu-তে run করে output দেখো।

---

# ⭐ Day 4 Challenge

একটা program বানাও যেটা:

1. একটি folder নেবে
    
2. `os.walk()` দিয়ে সব files খুঁজবে
    
3. মোট কতটি file আছে দেখাবে
    
4. `.py` কতটি
    
5. `.jpg/.png` কতটি
    
6. `.pdf` কতটি
    

Expected:

```text
Folder: project

Total files: 25
Python files: 8
Images: 10
PDF files: 3
Other files: 4
```

এখানে তোমার আগের শেখা:

```text
os.walk()
os.path.join()
os.path.splitext()
os.path.isfile()
```

সব একসাথে কাজে লাগবে।

---

## 🎯 Day 4 Mastery

আজকের শেষে এগুলো বুঝতে হবে:

```python
os.environ
os.getenv()
os.name
os.system()
os.walk()
```

বিশেষ করে **`os.walk()` + `os.path`** ভালোভাবে আয়ত্ত করো। এগুলো দিয়ে real-world file scanning, dataset processing, project file analysis ইত্যাদি করা যায়।

**Day 5-এ আমরা `os`-এর আরও useful parts + `shutil` দিয়ে real file-management automation project করব।**

----
# 🐍 Python `os` Module — Day 5

আজ `os`-এর basic শেখা শেষ করে **real-world file automation** করব।

আজকের focus:

1. `os.walk()` revision
    
2. `os.scandir()`
    
3. `os.stat()`
    
4. `shutil` কেন দরকার
    
5. **Real File Organizer Project**
    
6. Practice challenge
    

Official references: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com) এবং [Python `shutil` documentation](https://docs.python.org/3/library/shutil.html?utm_source=chatgpt.com)

---

# 1️⃣ `os.walk()` Revision

ধরো:

```text
project/
├── main.py
├── data/
│   ├── train.csv
│   └── test.csv
└── images/
    ├── cat.jpg
    └── dog.jpg
```

সব file খুঁজতে:

```python
import os

for root, dirs, files in os.walk("project"):
    for file in files:
        path = os.path.join(root, file)
        print(path)
```

Output:

```text
project/main.py
project/data/train.csv
project/data/test.csv
project/images/cat.jpg
project/images/dog.jpg
```

### মনে রাখো

```text
root  → বর্তমানে কোন directory-তে আছি
dirs  → ওই directory-এর folders
files → ওই directory-এর files
```

---

# 2️⃣ `os.scandir()` ⭐

`os.listdir()` শুধু নাম দেয়।

```python
import os

for item in os.listdir("."):
    print(item)
```

কিন্তু `os.scandir()` প্রতিটি item সম্পর্কে আরও information দিতে পারে।

```python
import os

for entry in os.scandir("."):
    print(entry.name)
```

এখানে `entry` object-এর মাধ্যমে জানতে পারো:

```python
entry.is_file()
entry.is_dir()
```

Example:

```python
import os

for entry in os.scandir("."):

    if entry.is_file():
        print("File:", entry.name)

    elif entry.is_dir():
        print("Folder:", entry.name)
```

এটা অনেক ক্ষেত্রে `listdir()` + আলাদা path checking-এর চেয়ে convenient।

---

# 3️⃣ `os.stat()`

কোনো file/directory-এর metadata দেখতে:

```python
import os

info = os.stat("main.py")

print(info)
```

এতে file-এর বিভিন্ন metadata পাওয়া যায়।

যেমন:

```python
print(info.st_size)
```

এটা file-এর **size in bytes** দেয়।

---

## File size বের করা

```python
import os

size = os.path.getsize("main.py")

print("Size:", size, "bytes")
```

আরও readable করতে:

```python
size = os.path.getsize("main.py")

print(f"Size: {size / 1024:.2f} KB")
```

---

# 4️⃣ এবার `shutil` কেন?

`os` দিয়ে basic filesystem operations করা যায়।

কিন্তু file/folder **copy, move, complete directory removal** ইত্যাদির জন্য Python-এর `shutil` module খুব useful।

Import:

```python
import shutil
```

---

# 5️⃣ `shutil.copy()`

একটি file copy:

```python
import shutil

shutil.copy("photo.jpg", "backup/photo.jpg")
```

অথবা:

```python
shutil.copy("photo.jpg", "backup")
```

---

# 6️⃣ `shutil.move()`

File move:

```python
import shutil

shutil.move("photo.jpg", "images/photo.jpg")
```

এটা file organizer project-এ খুব useful।

---

# 7️⃣ `shutil.copytree()`

পুরো directory copy করতে:

```python
import shutil

shutil.copytree("project", "project_backup")
```

তাহলে:

```text
project/
     ↓
project_backup/
```

তৈরি হবে।

---

# 8️⃣ `shutil.rmtree()`

পুরো directory tree delete করতে পারে:

```python
import shutil

shutil.rmtree("temporary")
```

### ⚠️ খুব সাবধান

এটা folder এবং তার ভিতরের contents delete করতে পারে।

Practice করার সময় শুধু নিজের test folder ব্যবহার করবে।

---

# 🚀 Day 5 Project — Smart File Organizer

এবার আমরা বাস্তব project বানাব।

Input:

```text
downloads/
├── photo.jpg
├── image.png
├── song.mp3
├── movie.mp4
├── notes.txt
└── report.pdf
```

Output:

```text
downloads/
├── Images/
│   ├── photo.jpg
│   └── image.png
├── Music/
│   └── song.mp3
├── Videos/
│   └── movie.mp4
└── Documents/
    ├── notes.txt
    └── report.pdf
```

---

## Step 1 — Categories

```python
import os
import shutil

base = "downloads"

categories = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Music": [".mp3", ".wav"],
    "Videos": [".mp4", ".mkv"],
    "Documents": [".pdf", ".txt", ".docx"]
}
```

এখানে dictionary ব্যবহার করছি।

---

## Step 2 — Folder তৈরি

```python
for folder in categories:

    path = os.path.join(base, folder)

    os.makedirs(path, exist_ok=True)
```

তাহলে:

```text
downloads/
├── Images/
├── Music/
├── Videos/
└── Documents/
```

তৈরি হবে।

---

# Step 3 — Files scan

```python
for file in os.listdir(base):

    full_path = os.path.join(base, file)

    if not os.path.isfile(full_path):
        continue

    print(file)
```

এখানে folderগুলো বাদ দিয়ে শুধু files নেওয়া হচ্ছে।

---

# Step 4 — Extension বের করা

```python
name, extension = os.path.splitext(file)

extension = extension.lower()
```

`.JPG` এবং `.jpg` যেন একইভাবে কাজ করে, তাই:

```python
extension.lower()
```

ব্যবহার করছি।

---

# Step 5 — Category খুঁজে বের করা

```python
for category, extensions in categories.items():

    if extension in extensions:

        print(file, "->", category)
```

---

# Step 6 — File Move

সবকিছু একসাথে:

```python
import os
import shutil

base = "downloads"

categories = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Music": [".mp3", ".wav"],
    "Videos": [".mp4", ".mkv"],
    "Documents": [".pdf", ".txt", ".docx"]
}

# Create folders
for category in categories:
    folder_path = os.path.join(base, category)
    os.makedirs(folder_path, exist_ok=True)


# Organize files
for file in os.listdir(base):

    full_path = os.path.join(base, file)

    if not os.path.isfile(full_path):
        continue

    name, extension = os.path.splitext(file)
    extension = extension.lower()

    for category, extensions in categories.items():

        if extension in extensions:

            destination = os.path.join(
                base,
                category,
                file
            )

            shutil.move(full_path, destination)

            print(f"Moved: {file} -> {category}")

            break
```

🎉 এটাই তোমার প্রথম **real-world `os` + `shutil` automation project**।

---

# 🧠 Day 5-এ কী শিখলে?

|Tool|কাজ|
|---|---|
|`os.walk()`|Recursive file scanning|
|`os.scandir()`|Directory entries efficiently inspect করা|
|`os.stat()`|File metadata|
|`os.path.getsize()`|File size|
|`shutil.copy()`|File copy|
|`shutil.move()`|File move|
|`shutil.copytree()`|Directory copy|
|`shutil.rmtree()`|Directory tree delete|

---

# 🎯 Day 5 Challenge ⭐

নিজে এমন program বানানোর চেষ্টা করো:

```text
Downloads/
├── Images/
├── Videos/
├── Music/
├── Documents/
└── Others/
```

যদি extension কোনো category-তে না থাকে:

```text
something.zip
program.exe
data.json
```

তাহলে:

```text
Others/
```

এ যাবে।

### তোমার program-এর workflow হবে:

```text
Downloads
    ↓
os.listdir()
    ↓
isfile()
    ↓
splitext()
    ↓
extension check
    ↓
category নির্বাচন
    ↓
shutil.move()
    ↓
Organized Downloads
```

---

## 🏁 Day 1 → Day 5 Progress

```text
DAY 1
cwd()
chdir()
listdir()

        ↓

DAY 2
os.path.*

        ↓

DAY 3
mkdir()
makedirs()
rename()
remove()
rmdir()

        ↓

DAY 4
environ
getenv()
system()
walk()

        ↓

DAY 5
scandir()
stat()
shutil
File Organizer
```

**এখন `os`-এর function মুখস্থ করার চেয়ে Day 5-এর File Organizer project নিজে ২–৩ বার বানানো বেশি valuable।** এরপর আমরা `os`-এর remaining important functions দিয়ে **Day 6 → Advanced OS + automation** করতে পারি।


# 🐍 Python `os` Module — Day 6

আজ আমরা `os`-এর **advanced practical features** শিখব। Day 5 পর্যন্ত file/folder management করেছি। আজ focus হবে:

1. `os.path.abspath()`
    
2. `os.path.realpath()`
    
3. `os.path.relpath()`
    
4. `os.path.normpath()`
    
5. `os.walk()` দিয়ে advanced scanning
    
6. File extension filtering
    
7. একটি **Duplicate/Report Scanner** project
    

Official documentation: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

---

# 1️⃣ `os.path.abspath()`

কোনো relative path-কে **absolute path** বানায়।

```python
import os

path = "data/image.jpg"

print(os.path.abspath(path))
```

যদি current directory হয়:

```text
/home/atiar/project
```

তাহলে output হতে পারে:

```text
/home/atiar/project/data/image.jpg
```

### Relative vs Absolute

```text
data/image.jpg
     ↓
relative path
```

আর:

```text
/home/atiar/project/data/image.jpg
```

হলো absolute path।

---

# 2️⃣ `os.path.realpath()`

এটা path-এর actual/real location বের করতে useful, বিশেষ করে symbolic link থাকলে।

```python
import os

print(os.path.realpath("data"))
```

সাধারণ path-এর ক্ষেত্রে `abspath()` এবং `realpath()` অনেক সময় একই ধরনের result দিতে পারে।

---

# 3️⃣ `os.path.relpath()`

একটি path-কে অন্য directory-এর relative path হিসেবে দেখাতে:

```python
import os

path = "/home/atiar/project/data/image.jpg"

print(os.path.relpath(path))
```

Current directory অনুযায়ী relative path পাবে।

আর নির্দিষ্ট starting point:

```python
print(
    os.path.relpath(
        "/home/atiar/project/data/image.jpg",
        "/home/atiar/project"
    )
)
```

Output:

```text
data/image.jpg
```

---

# 4️⃣ `os.path.normpath()`

Path-এর unnecessary `.` এবং `..` clean করে।

```python
import os

path = "project/data/../images/./photo.jpg"

print(os.path.normpath(path))
```

Output:

```text
project/images/photo.jpg
```

### কেন দরকার?

অনেক সময় programmatically path তৈরি করলে এমন path হতে পারে:

```text
project/data/../images/./photo.jpg
```

`normpath()` সেটাকে clean করে।

---

# 5️⃣ Path Functions একসাথে

এই চারটি ভালোভাবে আলাদা করো:

|Function|কাজ|
|---|---|
|`abspath()`|Absolute path তৈরি|
|`realpath()`|Real/actual path|
|`relpath()`|Relative path|
|`normpath()`|Path normalize/clean|

---

# 6️⃣ `os.walk()` Advanced

Day 4-এ আমরা basic `os.walk()` দেখেছিলাম।

আজ extension অনুযায়ী files খুঁজব।

ধরো:

```text
project/
├── main.py
├── app.py
├── data/
│   ├── train.csv
│   └── test.csv
└── images/
    ├── cat.jpg
    └── dog.jpg
```

শুধু Python files:

```python
import os

for root, dirs, files in os.walk("project"):

    for file in files:

        if file.endswith(".py"):
            print(os.path.join(root, file))
```

Output:

```text
project/main.py
project/app.py
```

---

# 7️⃣ Multiple Extensions

শুধু `.jpg`, `.png`, `.jpeg`:

```python
import os

extensions = (".jpg", ".jpeg", ".png")

for root, dirs, files in os.walk("project"):

    for file in files:

        if file.lower().endswith(extensions):
            print(os.path.join(root, file))
```

এখানে:

```python
(".jpg", ".jpeg", ".png")
```

একটি tuple।

`endswith()` একাধিক suffix গ্রহণ করতে পারে।

---

# 8️⃣ File Size Scanner ⭐

এখন `os.path.getsize()` ব্যবহার করি।

```python
import os

for root, dirs, files in os.walk("project"):

    for file in files:

        path = os.path.join(root, file)

        size = os.path.getsize(path)

        print(file, size, "bytes")
```

---

## KB-তে দেখানো

```python
size = os.path.getsize(path)

size_kb = size / 1024

print(f"{file}: {size_kb:.2f} KB")
```

---

# 9️⃣ Large File Finder

এবার ধরো তুমি এমন files খুঁজতে চাও যেগুলো **1 MB-এর বেশি**।

```python
import os

folder = "project"

limit = 1 * 1024 * 1024

for root, dirs, files in os.walk(folder):

    for file in files:

        path = os.path.join(root, file)

        size = os.path.getsize(path)

        if size > limit:
            print(
                file,
                "->",
                round(size / (1024 * 1024), 2),
                "MB"
            )
```

এটা real-world file analysis-এর একটা basic example।

---

# 🚀 Day 6 Project — File Report Generator

এখন আমরা এমন program বানাব যেটা একটি folder scan করে report তৈরি করবে।

Expected:

```text
Folder: project

Total Files: 20
Python Files: 5
Images: 8
PDF Files: 3

Largest Files:
video.mp4 → 25.4 MB
dataset.csv → 12.8 MB
```

---

## Step 1 — Counter তৈরি

```python
import os

folder = "project"

total = 0
python_files = 0
images = 0
pdfs = 0
```

---

## Step 2 — Scan

```python
for root, dirs, files in os.walk(folder):

    for file in files:

        total += 1

        extension = os.path.splitext(file)[1].lower()

        if extension == ".py":
            python_files += 1

        elif extension in (".jpg", ".jpeg", ".png"):
            images += 1

        elif extension == ".pdf":
            pdfs += 1
```

---

## Step 3 — Report

```python
print("Folder:", folder)
print()

print("Total Files:", total)
print("Python Files:", python_files)
print("Images:", images)
print("PDF Files:", pdfs)
```

---

# ⭐ Day 6 Challenge

এবার নিজের হাতে একটা **File Analyzer** বানাও।

Program-এর input:

```text
Folder path
```

Program output করবে:

```text
========================
     FILE REPORT
========================

Folder: project

Total Files: 35

Python: 8
Images: 12
PDF: 5
CSV: 4
Other: 6

Largest File:
dataset.csv → 25.4 MB
```

### ব্যবহার করবে:

```python
os.walk()
os.path.join()
os.path.splitext()
os.path.getsize()
os.path.abspath()
```

---

# 🧠 Day 6-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা

এখন `os`-কে শুধু **কিছু function-এর collection** হিসেবে দেখবে না।

তুমি এটাকে একটা workflow হিসেবে ভাববে:

```text
Path
 ↓
os.path.abspath()
 ↓
Directory
 ↓
os.walk()
 ↓
Files
 ↓
os.path.splitext()
 ↓
File information
 ↓
os.path.getsize()
 ↓
Analysis / Automation
```

### এখন পর্যন্ত তোমার `os` journey

```text
Day 1 → Directory basics
Day 2 → Path handling
Day 3 → Create / Rename / Delete
Day 4 → Environment + os.walk
Day 5 → File automation + shutil
Day 6 → Advanced paths + File analysis
```

**Day 7-এ `os` module-এর গুরুত্বপূর্ণ অংশগুলো দিয়ে একটি final project + complete revision + interview questions করলে `os` module-এর foundation বেশ শক্ত হয়ে যাবে।**


---
# 🐍 Python `os` Module — Day 7

আজ হবে **Final Revision + Final Project + Interview Practice**।  
আজকের পর `os`-এর জন্য আর function মুখস্থ করার দরকার নেই—বরং documentation দেখে প্রয়োজনীয় function খুঁজে ব্যবহার করার skill তৈরি করবে।

Official docs: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

---

# 1. পুরো `os` Module Revision

### Directory

|Function|কাজ|
|---|---|
|`os.getcwd()`|Current directory|
|`os.chdir()`|Directory change|
|`os.listdir()`|Contents দেখা|
|`os.mkdir()`|Folder তৈরি|
|`os.makedirs()`|Nested folder তৈরি|
|`os.remove()`|File delete|
|`os.rmdir()`|Empty folder delete|
|`os.rename()`|Rename|

### Path

|Function|কাজ|
|---|---|
|`os.path.exists()`|Path আছে কিনা|
|`os.path.isfile()`|File কিনা|
|`os.path.isdir()`|Folder কিনা|
|`os.path.join()`|Path তৈরি|
|`os.path.basename()`|Filename|
|`os.path.dirname()`|Parent directory|
|`os.path.splitext()`|Name + extension|
|`os.path.abspath()`|Absolute path|
|`os.path.realpath()`|Real path|
|`os.path.relpath()`|Relative path|
|`os.path.normpath()`|Path clean|
|`os.path.getsize()`|File size|

### Advanced

```python
os.environ
os.getenv()
os.name
os.system()
os.walk()
os.scandir()
os.stat()
```

---

# 2. সবচেয়ে গুরুত্বপূর্ণ 10টি

সবগুলো সমানভাবে গুরুত্বপূর্ণ নয়।

আমি তোমাকে এই 10টি আগে mastery করতে বলব:

```python
os.getcwd()
os.listdir()
os.path.exists()
os.path.isfile()
os.path.isdir()
os.path.join()
os.path.splitext()
os.makedirs()
os.walk()
os.getenv()
```

---

# 3. Final Project — File Analyzer

আজ আমরা এমন একটা program বানাব যেটা একটি directory scan করে report তৈরি করবে।

### Example

```text
project/
├── app.py
├── main.py
├── data/
│   ├── train.csv
│   └── test.csv
├── images/
│   ├── cat.jpg
│   └── dog.png
└── docs/
    └── report.pdf
```

Program output:

```text
================================
        FILE ANALYZER
================================

Directory:
 /home/atiar/project

Total Files: 7
Total Folders: 3

Python: 2
Images: 2
CSV: 2
PDF: 1

================================
```

---

# 4. Step 1 — Directory Input

```python
import os

folder = input("Enter folder path: ")

folder = os.path.abspath(folder)

print("Scanning:", folder)
```

এখানে:

```python
os.path.abspath()
```

ব্যবহার করেছি যাতে user relative path দিলেও absolute path পাওয়া যায়।

---

# 5. Step 2 — Check Directory

```python
if not os.path.isdir(folder):
    print("Invalid directory")
    exit()
```

এখন ভুল folder দিলে program বন্ধ হয়ে যাবে।

---

# 6. Step 3 — Counters

```python
total_files = 0
total_folders = 0

python_files = 0
image_files = 0
csv_files = 0
pdf_files = 0
```

---

# 7. Step 4 — `os.walk()`

```python
for root, dirs, files in os.walk(folder):

    total_folders += len(dirs)

    for file in files:

        total_files += 1

        extension = os.path.splitext(file)[1].lower()
```

এখন প্রতিটি file-এর extension আমাদের কাছে আছে।

---

# 8. Step 5 — Category Count

```python
        if extension == ".py":
            python_files += 1

        elif extension in (".jpg", ".jpeg", ".png", ".gif"):
            image_files += 1

        elif extension == ".csv":
            csv_files += 1

        elif extension == ".pdf":
            pdf_files += 1
```

---

# 9. Step 6 — Report

```python
print()
print("=" * 32)
print("        FILE ANALYZER")
print("=" * 32)

print()
print("Directory:", folder)

print()
print("Total Files:", total_files)
print("Total Folders:", total_folders)

print()
print("Python:", python_files)
print("Images:", image_files)
print("CSV:", csv_files)
print("PDF:", pdf_files)

print()
print("=" * 32)
```

---

# 🚀 Complete Project

এখন সব একসাথে:

```python
import os

folder = input("Enter folder path: ")

folder = os.path.abspath(folder)

if not os.path.isdir(folder):
    print("Invalid directory")
    exit()

total_files = 0
total_folders = 0

python_files = 0
image_files = 0
csv_files = 0
pdf_files = 0

for root, dirs, files in os.walk(folder):

    total_folders += len(dirs)

    for file in files:

        total_files += 1

        extension = os.path.splitext(file)[1].lower()

        if extension == ".py":
            python_files += 1

        elif extension in (".jpg", ".jpeg", ".png", ".gif"):
            image_files += 1

        elif extension == ".csv":
            csv_files += 1

        elif extension == ".pdf":
            pdf_files += 1


print()
print("=" * 32)
print("        FILE ANALYZER")
print("=" * 32)

print()
print("Directory:", folder)

print()
print("Total Files:", total_files)
print("Total Folders:", total_folders)

print()
print("Python:", python_files)
print("Images:", image_files)
print("CSV:", csv_files)
print("PDF:", pdf_files)

print()
print("=" * 32)
```

---

# 🧠 এখন Codeটা নিজে Explain করো

তোমার নিজের ভাষায় বলতে পারা উচিত:

```text
os.path.abspath()
        ↓
User-এর path → absolute path

os.path.isdir()
        ↓
Path valid directory কিনা

os.walk()
        ↓
পুরো directory tree scan

os.path.splitext()
        ↓
File extension বের করা

if/elif
        ↓
File category করা

counter
        ↓
Statistics তৈরি
```

এটাই আসল learning।

---

# ⭐ Day 7 Challenge

এখন **উপরের code copy না করে** নতুন করে বানাও।

আর ৩টা feature যোগ করো:

### Feature 1 — Largest File

Output:

```text
Largest File:
dataset.csv → 25.4 MB
```

ব্যবহার করবে:

```python
os.path.getsize()
```

---

### Feature 2 — Other Files

যেগুলো `.py`, image, `.csv`, `.pdf` নয়:

```text
Other: 6
```

---

### Feature 3 — File List

প্রতিটি file-এর complete path দেখাবে:

```text
Files:

/home/atiar/project/main.py
/home/atiar/project/data/train.csv
/home/atiar/project/images/cat.jpg
```

ব্যবহার করবে:

```python
os.path.join(root, file)
```

---

# 🎯 Final `os` Skill Map

```text
                    os
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
   Directory       Path       Environment
        │            │            │
    getcwd()       join()       environ
    chdir()        exists()     getenv()
    listdir()      isfile()
    mkdir()        isdir()
    makedirs()     splitext()
    rename()       abspath()
    remove()       getsize()
    rmdir()        walk()
```

### এখন তোমার next step

`os`-এর **৭ দিনের foundation complete**। এখন আর random `os` function শেখার দরকার নেই। কোনো নতুন function দরকার হলে **official documentation থেকে search করে শেখার অভ্যাস** করো।

এরপর সবচেয়ে logical package হলো **`pathlib`**—কারণ modern Python-এ file/path handling-এর জন্য এটা খুব গুরুত্বপূর্ণ। তারপর `shutil` + `subprocess` শিখলে Python automation-এর foundation অনেক শক্ত হবে।

---

হ্যাঁ। সহজভাবে বললে, Python-এর **`os` module ব্যবহার করা হয় Python program থেকে Operating System-এর সাথে কাজ করার জন্য।**

Official docs: [Python `os` documentation](https://docs.python.org/3/library/os.html?utm_source=chatgpt.com)

### `os` দিয়ে কী কী করা যায়?

|কাজ|Example|
|---|---|
|📁 Current folder জানা|`os.getcwd()`|
|📂 Folder change|`os.chdir()`|
|📋 Folder-এর files দেখা|`os.listdir()`|
|📁 Folder তৈরি|`os.mkdir()`|
|📁 Nested folder তৈরি|`os.makedirs()`|
|🗑️ File delete|`os.remove()`|
|🗑️ Empty folder delete|`os.rmdir()`|
|✏️ File/folder rename|`os.rename()`|
|🔍 File আছে কিনা|`os.path.exists()`|
|📄 File কিনা|`os.path.isfile()`|
|📂 Folder কিনা|`os.path.isdir()`|
|🔗 Path তৈরি|`os.path.join()`|
|📎 File extension বের করা|`os.path.splitext()`|
|🌳 পুরো folder tree scan|`os.walk()`|
|🔐 Environment variable|`os.getenv()`|
|💻 OS information|`os.name`|

### একটা বাস্তব উদাহরণ

ধরো তোমার computer-এ:

```text
Downloads/
├── photo.jpg
├── song.mp3
├── report.pdf
└── video.mp4
```

Python দিয়ে তুমি automatically:

```text
Downloads/
├── Images/
│   └── photo.jpg
├── Music/
│   └── song.mp3
├── Documents/
│   └── report.pdf
└── Videos/
    └── video.mp4
```

বানাতে পারো।

এখানে `os` দিয়ে তুমি **folder তৈরি, files খোঁজা, extension চেনা এবং path তৈরি** করতে পারবে; file move করার জন্য `shutil` ব্যবহার করা সুবিধাজনক।

### তোমার ক্ষেত্রে `os` কোথায় কাজে লাগবে?

তুমি যেহেতু **Python, Backend, AI/ML এবং Cybersecurity** শিখছ, `os` অনেক জায়গায় কাজে লাগবে:

```text
Python Automation
       ↓
os + pathlib + shutil

Backend
       ↓
Environment Variables
SECRET_KEY / DATABASE_URL

AI/ML
       ↓
Dataset folders
Images / Models / Checkpoints

Cybersecurity
       ↓
File & directory operations
Environment inspection
Process/system interaction
```

**এক লাইনে:**

> `os` = Python থেকে computer-এর **file system, directories, environment এবং কিছু OS-level functionality** নিয়ে কাজ করার interface।

আর একটা গুরুত্বপূর্ণ distinction: **`os` কোনো একটাই “package” নয়; এটা Python Standard Library-এর একটি module।** তাই `pip install os` করার দরকার নেই।


