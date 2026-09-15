অবশ্যই। এবার আমরা `os`-এর মতো **Python `sys` module-এর complete course** করব—official documentation ধরে, beginner → practical level পর্যন্ত।

Official reference: [Python `sys` module documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

# 🐍 Python `sys` Module — Complete Course

## 🎯 Course Goal

এই course শেষে তুমি বুঝবে:

- `sys` module কেন ব্যবহার করা হয়
    
- Command-line arguments কী
    
- Python interpreter সম্পর্কে information কীভাবে পাওয়া যায়
    
- `sys.path` কীভাবে কাজ করে
    
- `sys.argv`
    
- `sys.exit()`
    
- `sys.stdin`, `sys.stdout`, `sys.stderr`
    
- `sys.platform`
    
- `sys.version`
    
- `sys.modules`
    
- `sys.executable`
    
- `sys.getsizeof()`
    
- `sys.maxsize`
    
- Practical CLI project
    

---

# 📚 Course Structure

|Day|Topic|Difficulty|
|---|---|---|
|**Day 1**|`sys` introduction + interpreter information|🟢 Beginner|
|**Day 2**|`sys.argv` + Command-Line Arguments|🟢|
|**Day 3**|`sys.path` + Python module searching|🟡|
|**Day 4**|`sys.stdin`, `stdout`, `stderr`|🟡|
|**Day 5**|`sys.exit()` + Error/Program control|🟡|
|**Day 6**|`sys.modules`, `sys.executable`, `sys.platform`|🟡|
|**Day 7**|`sys.getsizeof()`, `maxsize` + practical analysis|🟠|
|**Day 8**|CLI File Analyzer Project|🟠|
|**Day 9**|Advanced `sys` concepts|🔴|
|**Day 10**|Final Project + Revision + Interview Questions|🔴|

---

# 🟢 Day 1 — `sys` Introduction

আজ আমরা এগুলো শিখব:

```python
import sys

sys.version
sys.version_info
sys.platform
sys.executable
sys.maxsize
```

---

## 1. `import sys`

```python
import sys

print(sys)
```

`sys` Python-এর **standard library module**।

তাই:

```bash
pip install sys
```

করতে হবে না।

---

# 2. `sys.version`

তোমার Python interpreter-এর version জানতে:

```python
import sys

print(sys.version)
```

Output-এর মতো হতে পারে:

```text
3.13.x ...
```

এখানে Python version এবং build information পাওয়া যায়।

---

# 3. `sys.version_info`

আরও structured information:

```python
import sys

print(sys.version_info)
```

এখানে Python-এর:

```text
major
minor
micro
releaselevel
serial
```

এরকম information পাওয়া যায়।

নির্দিষ্ট version:

```python
print(sys.version_info.major)
print(sys.version_info.minor)
```

---

# 4. Python version check

ধরো তোমার program-এর জন্য Python 3.10 বা তার বেশি প্রয়োজন।

```python
import sys

if sys.version_info < (3, 10):
    print("Python 3.10 or newer is required.")
else:
    print("Python version is supported.")
```

এটা practical use।

---

# 5. `sys.platform`

Operating system platform সম্পর্কে জানতে:

```python
import sys

print(sys.platform)
```

Linux-এ সাধারণত:

```text
linux
```

Windows-এ:

```text
win32
```

macOS-এ:

```text
darwin
```

তুমি cross-platform program তৈরি করলে এটা কাজে আসতে পারে।

---

# 6. `sys.executable` ⭐

Python interpreter-এর executable কোথায় আছে সেটা জানতে:

```python
import sys

print(sys.executable)
```

Ubuntu-তে এরকম হতে পারে:

```text
/usr/bin/python3
```

অথবা virtual environment ব্যবহার করলে:

```text
/home/atiar/project/.venv/bin/python
```

### কেন গুরুত্বপূর্ণ?

তুমি যখন একাধিক Python installation বা virtual environment নিয়ে কাজ করছ, তখন:

```python
sys.executable
```

দিয়ে বুঝতে পারবে **বর্তমানে কোন Python interpreter ব্যবহার হচ্ছে।**

---

# 7. `sys.maxsize`

```python
import sys

print(sys.maxsize)
```

সাধারণ 64-bit Python environment-এ এটি সাধারণত:

```text
9223372036854775807
```

এর মতো value হয়।

এটি Python-এর integer-এর সর্বোচ্চ সীমা বোঝায় না—Python integers arbitrary precision। `sys.maxsize` মূলত platform-এর সাধারণ maximum-sized integer-related সীমা বোঝাতে ব্যবহৃত হয়।

এই distinction-টা মনে রাখা গুরুত্বপূর্ণ।

---

# 🧪 Day 1 Practice

এই program নিজে লিখো:

```text
========================
   PYTHON SYSTEM INFO
========================

Python Version:
Platform:
Python Executable:
Max Size:
```

Hint:

```python
import sys

print("Python Version:", sys.version)
print("Platform:", sys.platform)
print("Python Executable:", sys.executable)
print("Max Size:", sys.maxsize)
```

---

# 🎯 Day 1 Challenge

নিজে এমন program বানাও:

```text
Python Information

Major Version: 3
Minor Version: 13
Platform: linux

Interpreter:
 /usr/bin/python3

Supported: Yes
```

এখানে ব্যবহার করবে:

```python
sys.version_info
sys.platform
sys.executable
```

---

# 🧠 আজকের Core Concepts

মনে রাখো:

```text
sys
 │
 ├── version
 │      → Python version
 │
 ├── version_info
 │      → structured version info
 │
 ├── platform
 │      → operating system platform
 │
 ├── executable
 │      → current Python interpreter
 │
 └── maxsize
        → platform-related maximum-sized integer value
```

### `os` বনাম `sys`

এটা খুব গুরুত্বপূর্ণ:

|`os`|`sys`|
|---|---|
|Operating System-এর সাথে কাজ|Python interpreter/runtime-এর সাথে কাজ|
|Files/folders|Python version|
|Paths|Command-line arguments|
|Environment variables|Module search path|
|OS commands|stdin/stdout/stderr|
|`os.walk()`|`sys.argv`|

**Day 2-এ আমরা `sys.argv` দিয়ে Command-Line Arguments শিখব।** এটা `sys` module-এর সবচেয়ে গুরুত্বপূর্ণ practical features-এর একটি।


# 🐍 Python `sys` Module — Day 2

আজ আমরা `sys.argv` শিখব।

এটা `sys` module-এর সবচেয়ে গুরুত্বপূর্ণ practical features-এর একটি।

Official documentation: [Python `sys.argv` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com#sys.argv)

---

# 1️⃣ `sys.argv` কী?

`sys.argv` হলো **command-line arguments-এর list**।

সহজভাবে:

```text
Terminal
   ↓
python program.py Atiar 20
   ↓
sys.argv
```

Python program command line থেকে যে values পায়, সেগুলো `sys.argv`-তে থাকে।

---

# 2️⃣ Basic Example

একটি file বানাও:

```text
app.py
```

এর মধ্যে:

```python
import sys

print(sys.argv)
```

তারপর terminal-এ:

```bash
python app.py
```

Output:

```text
['app.py']
```

এখন:

```bash
python app.py Atiar
```

Output:

```text
['app.py', 'Atiar']
```

আর:

```bash
python app.py Atiar 20
```

Output:

```text
['app.py', 'Atiar', '20']
```

---

# 3️⃣ `sys.argv` Index

এটা list-এর মতো কাজ করে।

```python
import sys

print(sys.argv[0])
print(sys.argv[1])
print(sys.argv[2])
```

যদি চালাও:

```bash
python app.py Atiar 20
```

তাহলে:

```text
sys.argv[0] → app.py
sys.argv[1] → Atiar
sys.argv[2] → 20
```

### খুব গুরুত্বপূর্ণ

`sys.argv[0]` সাধারণত **script/program name**।

Actual argument শুরু হয়:

```text
sys.argv[1]
```

থেকে।

---

# 4️⃣ সব Arguments Loop করা

```python
import sys

for argument in sys.argv:
    print(argument)
```

Terminal:

```bash
python app.py Atiar 20 Bangladesh
```

Output:

```text
app.py
Atiar
20
Bangladesh
```

---

# 5️⃣ Practical Example — Greeting

```python
import sys

name = sys.argv[1]

print("Hello", name)
```

Terminal:

```bash
python app.py Atiar
```

Output:

```text
Hello Atiar
```

---

# ⚠️ 6️⃣ একটা সমস্যা

যদি তুমি শুধু:

```bash
python app.py
```

চালাও, তাহলে:

```python
name = sys.argv[1]
```

এ error দিতে পারে:

```text
IndexError
```

কারণ `sys.argv[1]` নেই।

তাই আগে check করা ভালো:

```python
import sys

if len(sys.argv) < 2:
    print("Please provide your name.")
else:
    name = sys.argv[1]
    print("Hello", name)
```

---

# 7️⃣ `len(sys.argv)`

Arguments কয়টা আছে:

```python
import sys

print(len(sys.argv))
```

Command:

```bash
python app.py Atiar 20
```

Output:

```text
3
```

কারণ:

```text
0 → app.py
1 → Atiar
2 → 20
```

---

# 8️⃣ Numbers নিয়ে গুরুত্বপূর্ণ বিষয়

এটা খুব important:

```python
import sys

age = sys.argv[1]

print(type(age))
```

Terminal:

```bash
python app.py 25
```

Output:

```text
<class 'str'>
```

অর্থাৎ command-line argument **string হিসেবে আসে**।

যদি integer দরকার হয়:

```python
age = int(sys.argv[1])

print(age)
print(type(age))
```

Output:

```text
25
<class 'int'>
```

---

# 9️⃣ Practical Calculator

এবার আমরা command line থেকে দুইটা number নেব।

```python
import sys

if len(sys.argv) != 3:
    print("Usage: python calculator.py number1 number2")
else:
    a = float(sys.argv[1])
    b = float(sys.argv[2])

    print("Sum:", a + b)
```

Terminal:

```bash
python calculator.py 10 20
```

Output:

```text
Sum: 30.0
```

---

# 🔥 10️⃣ আরও Practical — Operation

Command:

```bash
python calculator.py 10 20 add
```

Code:

```python
import sys

if len(sys.argv) != 4:
    print("Usage: python calculator.py number1 number2 operation")
    sys.exit()

a = float(sys.argv[1])
b = float(sys.argv[2])
operation = sys.argv[3]

if operation == "add":
    print(a + b)

elif operation == "sub":
    print(a - b)

elif operation == "mul":
    print(a * b)

elif operation == "div":
    print(a / b)

else:
    print("Unknown operation")
```

Examples:

```bash
python calculator.py 10 20 add
```

```text
30
```

```bash
python calculator.py 10 20 mul
```

```text
200
```

এখানে তুমি `sys.argv` দিয়ে একটি ছোট **CLI application** বানিয়ে ফেলেছ।

---

# 🧠 `sys.argv` Mental Model

এটা মনে রাখো:

```text
python app.py Atiar 25
       │      │     │
       │      │     └── sys.argv[2]
       │      └──────── sys.argv[1]
       └─────────────── sys.argv[0]
```

অর্থাৎ:

```python
sys.argv
```

মূলত:

```python
[
    "app.py",
    "Atiar",
    "25"
]
```

---

# 🧪 Day 2 Exercises

### Exercise 1

এমন program বানাও:

```bash
python greet.py Atiar
```

Output:

```text
Hello, Atiar!
```

---

### Exercise 2

Command:

```bash
python info.py Atiar 25
```

Output:

```text
Name: Atiar
Age: 25
```

Hint:

```python
name = sys.argv[1]
age = int(sys.argv[2])
```

---

### Exercise 3 ⭐

Command:

```bash
python calculator.py 10 5 add
```

এগুলো support করো:

```text
add
sub
mul
div
```

---

# 🏆 Day 2 Challenge

একটা `file_info.py` বানাও।

Command:

```bash
python file_info.py example.txt
```

Program:

```text
File: example.txt
Exists: True
File: True
```

এখানে আজকের `sys` এবং আগের `os` একসাথে ব্যবহার করবে:

```python
import sys
import os
```

তারপর:

```python
filename = sys.argv[1]

print("File:", filename)
print("Exists:", os.path.exists(filename))
print("File:", os.path.isfile(filename))
```

এটাই আসল লক্ষ্য:

> **`sys` → user-এর কাছ থেকে command-line input নেওয়া**  
> **`os` → সেই input দিয়ে operating system-এর file/path নিয়ে কাজ করা**

পরের ধাপে **Day 3: `sys.path`**—এটা খুব গুরুত্বপূর্ণ, কারণ Python যখন `import` করে তখন **কোথায় module খুঁজে**, সেটা বুঝতে `sys.path` জানা দরকার।

# 🐍 Python `sys` Module — Day 3

আজকের সবচেয়ে গুরুত্বপূর্ণ topic:

> **`sys.path` — Python যখন `import` করে, তখন কোন কোন জায়গায় module/package খুঁজবে?**

Official documentation: [Python `sys.path` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com#sys.path)

---

# 1️⃣ `sys.path` কী?

প্রথমে:

```python
import sys

print(sys.path)
```

তুমি একটি list-এর মতো output পাবে:

```text
[
    '/home/atiar/project',
    '/usr/lib/python3...',
    ...
]
```

এই path-গুলোতে Python **modules/packages খোঁজে**।

সহজভাবে:

```text
import mymodule
       ↓
Python কোথায় খুঁজবে?
       ↓
sys.path
       ↓
একটার পর একটা location search
```

---

# 2️⃣ `sys.path` একটি List

```python
import sys

print(type(sys.path))
```

Output:

```text
<class 'list'>
```

তাই:

```python
for path in sys.path:
    print(path)
```

দিলে প্রতিটি search location আলাদা করে দেখতে পারবে।

---

# 3️⃣ কেন `sys.path` জানা গুরুত্বপূর্ণ?

ধরো তোমার project:

```text
project/
├── main.py
└── utils.py
```

`main.py`:

```python
import utils
```

Python `utils.py` খুঁজবে Python-এর module search path-এ।

যদি location search path-এর মধ্যে থাকে:

```text
utils.py
   ↓
FOUND
   ↓
import utils
```

না থাকলে:

```text
ModuleNotFoundError
```

---

# 4️⃣ নিজের Module Import

ধরো:

```text
project/
├── main.py
└── calculator.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`main.py`:

```python
import calculator

print(calculator.add(10, 20))
```

Output:

```text
30
```

এখানে Python `calculator.py` খুঁজে পেয়েছে।

---

# 5️⃣ `sys.path` দেখে বুঝবে কেন

`main.py`-তে:

```python
import sys

for path in sys.path:
    print(path)
```

তুমি দেখতে পারবে Python কোন কোন জায়গায় search করছে।

---

# 6️⃣ `sys.path.append()` ⭐

তুমি চাইলে runtime-এ একটি নতুন directory search path-এ যোগ করতে পারো।

ধরো:

```text
project/
├── main.py
└── modules/
    └── calculator.py
```

`calculator.py` সরাসরি current directory-তে নেই।

তখন:

```python
import sys

sys.path.append("./modules")

import calculator

print(calculator.add(10, 20))
```

এখন Python `modules` directory-তেও search করবে।

---

# ⚠️ কিন্তু একটা গুরুত্বপূর্ণ বিষয়

`sys.path.append()` দিয়ে import করানো **সবসময় best practice নয়**।

Real project-এ সাধারণত:

```text
packages
modules
virtual environments
proper project structure
```

ব্যবহার করা হয়।

`sys.path` modify করা বেশি useful:

- debugging
    
- experiments
    
- special runtime situations
    
- understanding Python imports
    

---

# 7️⃣ `sys.path.insert()`

`append()` path-কে শেষে যোগ করে।

```python
sys.path.append("./modules")
```

আর `insert()` নির্দিষ্ট position-এ যোগ করে:

```python
sys.path.insert(0, "./modules")
```

এখানে:

```text
0
↑
list-এর শুরু
```

---

# 8️⃣ `append()` vs `insert()`

|Code|কাজ|
|---|---|
|`sys.path.append(path)`|শেষে যোগ করে|
|`sys.path.insert(0, path)`|শুরুতে যোগ করে|

Example:

```python
import sys

print(sys.path)

sys.path.append("/home/atiar/modules")

print(sys.path)
```

---

# 9️⃣ `sys.path` Remove

যদি path remove করতে চাও:

```python
import sys

path = "./modules"

sys.path.append(path)

print(sys.path)

sys.path.remove(path)

print(sys.path)
```

---

# 🔥 10️⃣ Practical Project

এই structure তৈরি করো:

```text
myproject/
├── main.py
└── modules/
    └── calculator.py
```

### `calculator.py`

```python
def add(a, b):
    return a + b


def multiply(a, b):
    return a * b
```

### `main.py`

প্রথমে এটা try করো:

```python
import calculator
```

সম্ভবত Python `calculator` খুঁজে পাবে না, কারণ সেটা `modules/`-এর ভিতরে।

এখন:

```python
import sys

sys.path.append("./modules")

import calculator

print(calculator.add(10, 20))
print(calculator.multiply(5, 4))
```

Output:

```text
30
20
```

---

# 🧠 11️⃣ `sys.path` এবং `PYTHONPATH`

আরেকটি important concept আছে:

```text
PYTHONPATH
```

এটা একটি environment variable, যার মাধ্যমে Python-এর module search path-এ অতিরিক্ত directory যোগ করা যায়।

তাই conceptually:

```text
PYTHONPATH
     ↓
Python startup
     ↓
sys.path
     ↓
Module search
```

এটা `sys.path` বোঝার জন্য গুরুত্বপূর্ণ।

---

# 12️⃣ `sys.path` Debugging

কখনো এমন error পাবে:

```text
ModuleNotFoundError: No module named 'something'
```

তখন প্রথমে:

```python
import sys

print(sys.path)
```

দেখতে পারো।

তারপর প্রশ্ন করো:

> Python যে directory-তে module আছে সেখানে কি search করছে?

এটা backend এবং larger projects-এ debugging-এর জন্য useful।

---

# 🧪 Day 3 Exercise 1

এই code লিখো:

```python
import sys

for index, path in enumerate(sys.path):
    print(index, ":", path)
```

এখন প্রতিটি path-এর **index** দেখো।

---

# 🧪 Exercise 2

নিজের project-এ:

```text
project/
├── main.py
└── modules/
    └── hello.py
```

`hello.py`:

```python
def say_hello():
    print("Hello from module!")
```

`main.py` থেকে `hello.py` import করো।

Hint:

```python
sys.path.append("./modules")
```

---

# 🧪 Exercise 3 ⭐

এই তিনটা test করো:

```python
import sys

print("Number of paths:", len(sys.path))

for path in sys.path:
    print(path)
```

তারপর:

```python
sys.path.append("./test")
```

দিয়ে আবার `len(sys.path)` দেখো।

Difference বুঝতে চেষ্টা করো।

---

# 🏆 Day 3 Challenge

একটি project বানাও:

```text
calculator_project/
├── main.py
└── modules/
    └── calculator.py
```

`calculator.py`-তে:

```text
add()
subtract()
multiply()
divide()
```

functions তৈরি করবে।

`main.py`:

```text
1. Add
2. Subtract
3. Multiply
4. Divide
```

এর মতো একটি ছোট CLI program বানাবে এবং `sys.path` ব্যবহার করে `calculator` module import করবে।

---

# 🎯 আজকের Mental Model

সবচেয়ে গুরুত্বপূর্ণ flow:

```text
import calculator
       ↓
Python search করবে
       ↓
sys.path
       ↓
Path 1
       ↓
Path 2
       ↓
Path 3
       ↓
calculator পাওয়া গেল?
       ↓
YES → Import
NO  → ModuleNotFoundError
```

### আজকের ৫টি জিনিস মনে রাখো

```python
sys.path
sys.path.append()
sys.path.insert()
sys.path.remove()
PYTHONPATH
```

**Day 3-এর আসল লক্ষ্য `sys.path` মুখস্থ করা নয়—Python কীভাবে module খুঁজে `import` করে, সেই mechanism বুঝে ফেলা।**

পরের ধাপে **Day 4: `sys.stdin`, `sys.stdout`, `sys.stderr`** — Python-এর input/output stream কীভাবে কাজ করে, সেটা শিখব।

# 🐍 Python `sys` Module — Day 4

আজ আমরা শিখব Python-এর **Input/Output Streams**:

```python
sys.stdin
sys.stdout
sys.stderr
```

Official documentation: [Python `sys` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1️⃣ প্রথমে Concept বুঝি

সাধারণভাবে Python-এ:

```python
input()
print()
```

ব্যবহার করি।

কিন্তু internally Python-এর standard input/output streams আছে:

```text
Keyboard
   ↓
sys.stdin
   ↓
Python Program
   ↓
sys.stdout
   ↓
Terminal
```

আর error message-এর জন্য:

```text
Program
   ↓
sys.stderr
   ↓
Terminal / Error output
```

---

# 2️⃣ `sys.stdin`

`sys.stdin` হলো program-এর **standard input stream**।

সাধারণত keyboard থেকে input আসে।

```python
import sys

name = sys.stdin.readline()

print("Hello", name)
```

Terminal:

```text
Atiar
```

Output:

```text
Hello Atiar
```

---

# 3️⃣ `sys.stdin.readline()`

এটা একটি line input নেয়।

```python
import sys

name = sys.stdin.readline()

print(name)
```

যদি input দাও:

```text
Atiar
```

তাহলে newline character-ও input-এর অংশ হতে পারে।

তাই সাধারণত:

```python
name = sys.stdin.readline().strip()
```

ব্যবহার করা যায়।

---

# 4️⃣ `input()` বনাম `sys.stdin.readline()`

দুটোই input নেওয়ার জন্য।

### `input()`

```python
name = input("Name: ")
```

Beginner-friendly।

### `sys.stdin.readline()`

```python
import sys

name = sys.stdin.readline().strip()
```

এটা standard input stream-এর সরাসরি interface।

### সহজভাবে:

|`input()`|`sys.stdin`|
|---|---|
|সহজ|Low-level control বেশি|
|Interactive input|Stream-based input|
|Beginner-friendly|CLI/stream processing-এ useful|

---

# 5️⃣ `sys.stdout`

`sys.stdout` হলো standard output stream।

সাধারণত:

```python
print("Hello")
```

যেখানে output যায়, সেটাই `sys.stdout`।

তুমি সরাসরি লিখতে পারো:

```python
import sys

sys.stdout.write("Hello\n")
```

Output:

```text
Hello
```

---

# 6️⃣ `print()` এবং `sys.stdout`

এই দুটো প্রায় একই output stream ব্যবহার করে:

```python
print("Hello")
```

এবং:

```python
import sys

sys.stdout.write("Hello\n")
```

তবে `sys.stdout.write()`-এ newline নিজে দিতে হয়।

```python
sys.stdout.write("Hello")
sys.stdout.write("World")
```

Output:

```text
HelloWorld
```

আর:

```python
sys.stdout.write("Hello\n")
sys.stdout.write("World\n")
```

Output:

```text
Hello
World
```

---

# 7️⃣ `sys.stderr` ⭐

এটা **standard error stream**।

Error/warning ধরনের output আলাদা stream-এ পাঠাতে ব্যবহার করা যায়।

```python
import sys

sys.stderr.write("Something went wrong!\n")
```

Terminal-এ message দেখাবে:

```text
Something went wrong!
```

---

# 8️⃣ `stdout` বনাম `stderr`

খুব গুরুত্বপূর্ণ:

```text
sys.stdout
    ↓
Normal output

sys.stderr
    ↓
Error / diagnostic output
```

Example:

```python
import sys

print("Program started")

sys.stderr.write("Warning: something happened\n")

print("Program finished")
```

---

# 9️⃣ কেন আলাদা Stream দরকার?

ধরো একটি CLI program:

```text
Normal output → stdout
Error output  → stderr
```

তখন terminal-এ তুমি output আলাদাভাবে redirect করতে পারো।

Linux-এ:

```bash
python app.py > output.txt
```

এতে normal `stdout` output file-এ যাবে।

আর error `stderr` আলাদা থাকতে পারে।

এটা **Linux/DevOps/CLI tools**-এ খুব গুরুত্বপূর্ণ concept।

---

# 🔥 10️⃣ Practical Example

একটি program:

```python
import sys

name = sys.stdin.readline().strip()

if not name:
    sys.stderr.write("Error: Name is required\n")
else:
    sys.stdout.write(f"Hello, {name}\n")
```

Run:

```bash
python app.py
```

Input:

```text
Atiar
```

Output:

```text
Hello, Atiar
```

কিন্তু input না দিলে:

```text
Error: Name is required
```

---

# 11️⃣ `sys.stdin` দিয়ে Multiple Lines

এবার অনেকগুলো line পড়ি:

```python
import sys

for line in sys.stdin:
    print("Received:", line.strip())
```

Terminal-এ:

```text
Python
Django
React
```

প্রতিটি line program পড়তে পারবে।

`sys.stdin` শুধু keyboard নয়—input stream হিসেবে file বা pipe থেকেও data পেতে পারে।

---

# 12️⃣ Pipe Example ⭐

Linux terminal-এ:

```bash
echo "Hello Python" | python app.py
```

`app.py`:

```python
import sys

data = sys.stdin.read()

print("Received:", data)
```

Output:

```text
Received: Hello Python
```

এখানে:

```text
echo
 ↓
pipe |
 ↓
sys.stdin
 ↓
Python
```

এটাই command-line tools-এর powerful concept।

---

# 13️⃣ `sys.stdin.read()`

```python
import sys

data = sys.stdin.read()

print(data)
```

`read()` পুরো available input পড়তে পারে।

আর:

```python
sys.stdin.readline()
```

একটি line পড়ে।

### Difference

|Function|কাজ|
|---|---|
|`readline()`|একটি line|
|`read()`|পুরো input|
|`for line in sys.stdin`|একাধিক line process|

---

# 14️⃣ Practical Mini Project — Word Counter

`word_counter.py`:

```python
import sys

text = sys.stdin.read()

words = text.split()

print("Words:", len(words))
```

Run:

```bash
echo "Python is easy to learn" | python word_counter.py
```

Output:

```text
Words: 5
```

---

# 🧪 Day 4 Exercise 1

Program বানাও:

```python
import sys

text = sys.stdin.read()

print("Characters:", len(text))
```

তারপর:

```bash
echo "Hello Python" | python app.py
```

---

# 🧪 Exercise 2

Normal output `stdout` এবং error `stderr` আলাদা করে ব্যবহার করো:

```python
import sys

sys.stdout.write("Normal message\n")
sys.stderr.write("Error message\n")
```

---

# 🧪 Exercise 3 ⭐

একটি program বানাও যেটা stdin থেকে numbers নেবে:

```text
10
20
30
40
```

তারপর output:

```text
Total: 100
Average: 25
```

Hint:

```python
import sys

numbers = []

for line in sys.stdin:
    numbers.append(float(line.strip()))
```

---

# 🏆 Day 4 Challenge

একটি **CLI Text Analyzer** বানাও।

Input:

```bash
echo "Python is powerful and Python is easy" | python analyzer.py
```

Output:

```text
Characters: 41
Words: 7
Lines: 1
```

এখানে ব্যবহার করবে:

```python
sys.stdin
sys.stdout
```

---

# 🧠 আজকের Mental Model

```text
                 Python Program
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
      stdin        stdout       stderr
          ↑           ↓           ↓
       Input       Normal       Error
                    Output      Output
```

### সবচেয়ে গুরুত্বপূর্ণ:

```python
sys.stdin
```

➡️ Input stream

```python
sys.stdout
```

➡️ Normal output stream

```python
sys.stderr
```

➡️ Error/diagnostic output stream

---

## 🎯 Day 4 Mastery Checklist

আজ তোমার এগুলো বুঝতে হবে:

```python
sys.stdin
sys.stdin.readline()
sys.stdin.read()

sys.stdout
sys.stdout.write()

sys.stderr
sys.stderr.write()
```

এবং এই concept:

```text
input()
   ≈
sys.stdin

print()
   ≈
sys.stdout
```

তবে `stdin/stdout/stderr` **stream abstraction**, তাই CLI tools, Linux pipes, file redirection এবং automation-এ এগুলোর গুরুত্ব অনেক বেশি।


# 🐍 Python `sys` Module — Day 5

আজ আমরা শিখব:

- `sys.exit()`
    
- Exit status/code
    
- Program কখন এবং কেন বন্ধ করবে
    
- `SystemExit`
    
- `sys.exc_info()`
    
- Practical CLI validation project
    

Official documentation: [Python `sys` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1️⃣ `sys.exit()` কী?

`sys.exit()` ব্যবহার করে Python program **সঠিকভাবে বন্ধ** করা যায়।

```python
import sys

print("Program started")

sys.exit()

print("Program finished")
```

Output:

```text
Program started
```

`sys.exit()`-এর পরের code execute হবে না।

---

# 2️⃣ কেন `sys.exit()` দরকার?

ধরো user কোনো required input দেয়নি:

```python
import sys

name = ""

if not name:
    print("Name is required")
    sys.exit()

print("Hello", name)
```

Output:

```text
Name is required
```

এখানে invalid condition হলে program আর সামনে যায়নি।

---

# 3️⃣ `sys.exit()`-এ Message দেওয়া

তুমি চাইলে:

```python
import sys

sys.exit("Something went wrong")
```

Output:

```text
Something went wrong
```

এটা program terminate করার পাশাপাশি message দেখায়।

---

# 4️⃣ Exit Code ⭐

এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ concept।

```python
sys.exit(0)
```

সাধারণত:

```text
0 → success
```

আর non-zero value সাধারণত failure/error বোঝাতে ব্যবহৃত হয়।

```python
sys.exit(1)
```

মানে program unsuccessfulভাবে শেষ হয়েছে—কিন্তু **1-এর নির্দিষ্ট universal meaning নেই**; তোমার program-এর convention অনুযায়ী code ব্যবহার করা যায়।

---

# 5️⃣ Example

```python
import sys

age = int(input("Age: "))

if age < 0:
    print("Invalid age")
    sys.exit(1)

print("Valid age")
sys.exit(0)
```

এখানে:

```text
Valid → 0
Invalid → 1
```

---

# 6️⃣ Linux-এ Exit Code দেখা

তুমি Ubuntu ব্যবহার করছ, তাই এটা practice করা ভালো।

`app.py`:

```python
import sys

sys.exit(5)
```

Terminal:

```bash
python app.py
echo $?
```

Output:

```text
5
```

`$?` হলো আগের command-এর exit status।

আর:

```python
sys.exit(0)
```

দিলে:

```bash
echo $?
```

Output:

```text
0
```

---

# 7️⃣ কেন Exit Code গুরুত্বপূর্ণ?

CLI tools এবং automation-এ অন্য program বুঝতে পারে:

```text
Program
   ↓
Exit code
   ↓
Success / Failure
```

যেমন:

```text
0 → Success
1 → Failure
2 → Another failure
```

Shell scripts, CI/CD এবং automation-এ এই concept খুব গুরুত্বপূর্ণ।

---

# 8️⃣ `sys.exit()` আসলে কী করে?

একটু advanced concept:

```python
sys.exit()
```

internally `SystemExit` exception raise করে।

তাই:

```python
import sys

try:
    sys.exit(1)

except SystemExit:
    print("Program tried to exit")
```

Output:

```text
Program tried to exit
```

---

# 9️⃣ `SystemExit`

তুমি চাইলে সরাসরি exception-টাও দেখতে পারো:

```python
try:
    raise SystemExit(1)

except SystemExit:
    print("SystemExit caught")
```

Output:

```text
SystemExit caught
```

### কিন্তু সাধারণ program-এ

এভাবে না লিখে:

```python
sys.exit(1)
```

ব্যবহার করাই পরিষ্কার।

---

# 🔟 `sys.exit()` বনাম `return`

এটা খুব গুরুত্বপূর্ণ।

### Function-এর ভিতরে:

```python
def check():
    return
```

শুধু function থেকে বের হবে।

কিন্তু:

```python
import sys

sys.exit()
```

পুরো program terminate করতে পারে।

```text
return
  ↓
function শেষ

sys.exit()
  ↓
program exit
```

---

# 1️⃣1️⃣ `sys.exc_info()`

এটা একটু advanced।

Exception handling-এর সময় current exception-এর information পাওয়া যায়।

```python
import sys

try:
    x = 10 / 0

except:
    print(sys.exc_info())
```

এখানে exception-এর type, value এবং traceback-related information পাওয়া যাবে।

আরও পরিষ্কারভাবে:

```python
import sys

try:
    x = 10 / 0

except:
    exc_type, exc_value, exc_traceback = sys.exc_info()

    print("Type:", exc_type)
    print("Value:", exc_value)
```

Output-এর মতো:

```text
Type: <class 'ZeroDivisionError'>
Value: division by zero
```

### ⚠️ Modern Python code-এ

সাধারণ error handling-এর জন্য:

```python
except Exception as e:
    print(e)
```

অনেক সময় `sys.exc_info()`-এর চেয়ে সহজ।

---

# 🚀 Day 5 Project — CLI Validator

এবার `sys.argv` + `sys.exit()` একসাথে ব্যবহার করব।

Command:

```bash
python app.py Atiar 25
```

Expected:

```text
Name: Atiar
Age: 25
Status: Valid
```

কিন্তু:

```bash
python app.py
```

Output:

```text
Error: Name and age are required
```

এবং program non-zero exit করবে।

---

## Complete Code

```python
import sys

if len(sys.argv) != 3:
    print("Usage: python app.py <name> <age>")
    sys.exit(1)

name = sys.argv[1]

try:
    age = int(sys.argv[2])
except ValueError:
    print("Error: Age must be a number")
    sys.exit(2)

if age < 0:
    print("Error: Age cannot be negative")
    sys.exit(3)

print("Name:", name)
print("Age:", age)
print("Status: Valid")

sys.exit(0)
```

---

# 🧪 Test 1

```bash
python app.py Atiar 25
```

Output:

```text
Name: Atiar
Age: 25
Status: Valid
```

তারপর:

```bash
echo $?
```

Output:

```text
0
```

---

# 🧪 Test 2

```bash
python app.py
```

Output:

```text
Usage: python app.py <name> <age>
```

তারপর:

```bash
echo $?
```

Output:

```text
1
```

---

# 🧪 Test 3

```bash
python app.py Atiar abc
```

Output:

```text
Error: Age must be a number
```

Exit code:

```text
2
```

---

# 🧪 Test 4

```bash
python app.py Atiar -5
```

Output:

```text
Error: Age cannot be negative
```

Exit code:

```text
3
```

---

# 🧠 আজকের Mental Model

```text
CLI Arguments
     ↓
sys.argv
     ↓
Validation
     ↓
Valid?
 ┌───┴────┐
YES       NO
 ↓         ↓
Program   sys.exit(code)
runs
 ↓
sys.exit(0)
```

---

# 🎯 Day 5-এর Core Concepts

আজ এগুলো অবশ্যই বুঝবে:

```python
sys.exit()
sys.exit(0)
sys.exit(1)

SystemExit

sys.exc_info()
```

বিশেষ করে:

> **`sys.exit()` শুধু "program বন্ধ করার command" নয়; CLI/automation environment-এ exit status দিয়ে program সফল হয়েছে নাকি ব্যর্থ হয়েছে সেটাও communicate করা হয়।**

### `sys` Course Progress

```text
Day 1 → Python runtime information
Day 2 → sys.argv
Day 3 → sys.path
Day 4 → stdin / stdout / stderr
Day 5 → sys.exit() + exit codes
```

**Day 6-এ আমরা `sys.modules`, `sys.executable`, `sys.platform` এবং Python-এর import/runtime environment নিয়ে কাজ করব।**


# 🐍 Python `sys` Module — Day 6

আজ আমরা `sys`-এর **Python runtime ও import system**-এর গুরুত্বপূর্ণ অংশ শিখব:

```python
sys.modules
sys.executable
sys.platform
sys.implementation
```

Official documentation: [Python `sys` module documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1️⃣ `sys.modules` ⭐

`sys.modules` হলো Python process-এ **বর্তমানে imported modules-এর dictionary**।

```python
import sys

print(type(sys.modules))
```

Output:

```text
<class 'dict'>
```

এখন:

```python
import sys

print("os" in sys.modules)
```

যদি আগে `os` import করা হয়ে থাকে:

```text
True
```

---

# 2️⃣ `sys.modules` কীভাবে কাজ করে?

ধরো:

```python
import math
```

Python module-টি load করার পর সেটি `sys.modules`-এ রাখে।

```text
import math
     ↓
Python checks sys.modules
     ↓
math already loaded?
     ↓
YES → existing module ব্যবহার
NO  → module load করে
```

এটা Python-এর import system বোঝার জন্য খুব গুরুত্বপূর্ণ।

---

# 3️⃣ একটা Practical Example

```python
import sys

print("math" in sys.modules)

import math

print("math" in sys.modules)
```

Output:

```text
False
True
```

অর্থাৎ `import math` করার পর `math` module `sys.modules`-এ এসেছে।

---

# 4️⃣ `sys.modules`-এর ভিতরে কী আছে?

```python
import sys

for name in sys.modules:
    print(name)
```

অনেক module দেখতে পাবে।

যেমন:

```text
sys
builtins
os
math
...
```

তোমার Python environment এবং imported modules অনুযায়ী list আলাদা হবে।

---

# 5️⃣ `sys.modules` দিয়ে Module Check

```python
import sys

if "numpy" in sys.modules:
    print("NumPy is already imported")
else:
    print("NumPy is not imported yet")
```

⚠️ এখানে একটা important distinction:

```python
"numpy" in sys.modules
```

মানে **এই process-এ NumPy already imported হয়েছে কিনা**।

এর মানে NumPy computer-এ installed কিনা—তা নয়।

---

# 6️⃣ `sys.executable` ⭐

Day 1-এ দেখেছিলাম:

```python
import sys

print(sys.executable)
```

এটা current Python interpreter-এর executable path দেয়।

যেমন:

```text
/usr/bin/python3
```

Virtual environment হলে:

```text
/home/user/project/.venv/bin/python
```

---

# 7️⃣ কেন `sys.executable` এত গুরুত্বপূর্ণ?

ধরো তোমার computer-এ:

```text
Python 3.11
Python 3.13
```

দুটো আছে।

Terminal-এ:

```bash
python --version
```

আর কোনো project-এর মধ্যে:

```python
import sys

print(sys.executable)
```

দিয়ে তুমি জানতে পারবে **তোমার current program আসলে কোন Python interpreter দিয়ে চলছে।**

বিশেষ করে virtual environment debugging-এ এটা খুব useful।

---

# 8️⃣ `sys.platform`

Operating-system platform জানতে:

```python
import sys

print(sys.platform)
```

Common values:

|Platform|`sys.platform`|
|---|---|
|Linux|`linux`|
|Windows|`win32`|
|macOS|`darwin`|

Example:

```python
import sys

if sys.platform == "linux":
    print("Running on Linux")

elif sys.platform == "win32":
    print("Running on Windows")

elif sys.platform == "darwin":
    print("Running on macOS")
```

---

# 9️⃣ Cross-platform Program

ধরো তুমি platform অনুযায়ী message দেখাতে চাও:

```python
import sys

if sys.platform == "linux":
    print("Linux detected")

elif sys.platform == "win32":
    print("Windows detected")

else:
    print("Other platform")
```

এভাবে program-এর behavior platform অনুযায়ী পরিবর্তন করা যায়।

---

# 🔟 `sys.implementation`

Python implementation সম্পর্কে information:

```python
import sys

print(sys.implementation)
```

সাধারণ CPython installation-এ information-এর মধ্যে `name` থাকবে:

```python
print(sys.implementation.name)
```

Output:

```text
cpython
```

---

# 1️⃣1️⃣ CPython কী?

Python বলতে আমরা সাধারণত **CPython** ব্যবহার করি।

আরও Python implementations আছে, যেমন:

```text
CPython
PyPy
Jython
IronPython
```

তাই:

```python
sys.implementation.name
```

দিয়ে current implementation জানা যায়।

---

# 🔥 12️⃣ Practical Runtime Information Tool

এবার Day 1 + Day 6-এর concepts একসাথে ব্যবহার করি।

```python
import sys

print("=" * 40)
print("       PYTHON RUNTIME INFO")
print("=" * 40)

print("Python version:")
print(sys.version)

print()

print("Implementation:")
print(sys.implementation.name)

print()

print("Platform:")
print(sys.platform)

print()

print("Executable:")
print(sys.executable)

print()

print("Imported modules:")
print(len(sys.modules))
```

Output-এর মতো হতে পারে:

```text
========================================
       PYTHON RUNTIME INFO
========================================

Python version:
3.x.x ...

Implementation:
cpython

Platform:
linux

Executable:
/usr/bin/python3

Imported modules:
...
```

---

# 13️⃣ `sys.modules` দিয়ে Import Debugging

ধরো:

```python
import sys

print("Before:", "math" in sys.modules)

import math

print("After:", "math" in sys.modules)
```

এখানে import system-এর basic behavior দেখতে পারবে।

আর:

```python
print(sys.modules["math"])
```

দিয়ে loaded module object-এর reference দেখতে পারো।

---

# 14️⃣ `sys.modules` Modify করা উচিত?

Technically dictionary হওয়ায় manipulate করা যায়।

কিন্তু সাধারণ application code-এ:

```python
sys.modules.pop(...)
```

বা manually module entry পরিবর্তন করা **করার দরকার নেই**।

এগুলো advanced import behavior, testing, plugin systems বা specialized tooling-এর ক্ষেত্রে দেখা যায়।

তাই এখন লক্ষ্য হবে:

> `sys.modules` কী এবং Python import system-এ এর ভূমিকা কী—এটা বোঝা।

---

# 🧪 Day 6 Exercise 1

এই program লিখো:

```python
import sys

print("Python:", sys.version_info)
print("Platform:", sys.platform)
print("Executable:", sys.executable)
print("Implementation:", sys.implementation.name)
```

---

# 🧪 Exercise 2

```python
import sys

print("Before:", "json" in sys.modules)

import json

print("After:", "json" in sys.modules)
```

কেন `False → True` হলো সেটা নিজের ভাষায় explain করো।

---

# 🧪 Exercise 3 ⭐

একটি program বানাও যেটা check করবে:

```text
Python implementation: CPython
Platform: Linux
Python version: 3.x
```

Hint:

```python
sys.implementation.name
sys.platform
sys.version_info
```

---

# 🏆 Day 6 Challenge

একটি **Python Environment Checker** বানাও।

Expected output:

```text
================================
   PYTHON ENVIRONMENT CHECKER
================================

Python Version: 3.x
Implementation: cpython
Platform: linux

Python Executable:
/home/user/project/.venv/bin/python

Loaded Modules: 45

Status: Environment detected
================================
```

ব্যবহার করবে:

```python
sys.version_info
sys.implementation
sys.platform
sys.executable
sys.modules
```

---

# 🧠 আজকের Mental Model

`sys`-কে এখন এভাবে ভাবো:

```text
                    sys
                     │
        ┌────────────┼─────────────┐
        ↓            ↓             ↓
     Runtime       Import        Platform
        │            │             │
   version       modules       platform
   executable    sys.path
   implementation
```

### Day 6-এর Core

```python
sys.modules
```

➡️ বর্তমানে loaded/imported modules

```python
sys.executable
```

➡️ কোন Python interpreter চলছে

```python
sys.platform
```

➡️ কোন platform-এ চলছে

```python
sys.implementation
```

➡️ কোন Python implementation চলছে

---

## 📚 `sys` Course Progress

```text
Day 1 → Python runtime information
Day 2 → sys.argv
Day 3 → sys.path
Day 4 → stdin / stdout / stderr
Day 5 → sys.exit() + exit codes
Day 6 → modules + interpreter + platform
```

**Day 7-এ আমরা `sys.getsizeof()`, `sys.maxsize`, recursion-related `sys` features এবং memory/runtime analysis শিখব।**

---
# 🐍 Python `sys` Module — Day 7

আজ আমরা `sys`-এর **memory, recursion এবং runtime-limit related features** শিখব।

আজকের topics:

```text
1. sys.getsizeof()
2. sys.maxsize
3. sys.getrecursionlimit()
4. sys.setrecursionlimit()
5. sys.float_info
6. Practical Memory Analyzer
```

Official documentation: [Python `sys` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1️⃣ `sys.getsizeof()` ⭐

কোনো Python object কত bytes memory ব্যবহার করছে তার **shallow size** জানতে:

```python
import sys

x = 100

print(sys.getsizeof(x))
```

Output environment অনুযায়ী ভিন্ন হতে পারে।

---

## String

```python
import sys

name = "Python"

print(sys.getsizeof(name))
```

---

## List

```python
import sys

numbers = [1, 2, 3, 4, 5]

print(sys.getsizeof(numbers))
```

এখানে একটি গুরুত্বপূর্ণ বিষয়:

> `sys.getsizeof()` object-এর **shallow memory size** দেয়। Nested objects-এর পুরো memory automatically যোগ করে না।

যেমন:

```python
numbers = [1, 2, 3]
```

list object-এর নিজের memory এবং এর ভিতরের integer objects-এর memory আলাদা বিষয়।

---

# 2️⃣ `sys.getsizeof()` দিয়ে Comparison

```python
import sys

a = 10
b = "Hello"
c = [1, 2, 3, 4, 5]

print("Integer:", sys.getsizeof(a))
print("String:", sys.getsizeof(b))
print("List:", sys.getsizeof(c))
```

এখানে উদ্দেশ্য **exact number মুখস্থ করা নয়**।

বরং বুঝবে:

```text
Python object
     ↓
sys.getsizeof()
     ↓
approximate shallow size
```

---

# 3️⃣ `sys.maxsize`

আগে দেখেছিলাম:

```python
import sys

print(sys.maxsize)
```

64-bit environment-এ সাধারণত:

```text
9223372036854775807
```

এর মতো value দেখা যায়।

### ⚠️ Important

এটা Python integer-এর maximum value **নয়**।

Python integer বড় হতে পারে:

```python
x = 10 ** 100

print(x)
```

Python arbitrary-precision integers ব্যবহার করে।

তাই:

```text
sys.maxsize
≠
maximum Python integer
```

---

# 4️⃣ `sys.getrecursionlimit()` ⭐

Python recursion-এর maximum depth-এর default limit জানতে:

```python
import sys

print(sys.getrecursionlimit())
```

সাধারণ Python installation-এ এটি প্রায়:

```text
1000
```

এর কাছাকাছি হতে পারে, তবে exact value environment অনুযায়ী পরিবর্তিত হতে পারে।

---

# 5️⃣ Recursion কী?

একটি function নিজেকেই call করলে সেটাকে recursion বলে।

```python
def count(n):

    if n == 0:
        return

    print(n)

    count(n - 1)
```

Run:

```python
count(5)
```

Output:

```text
5
4
3
2
1
```

---

# 6️⃣ Recursion Limit কেন আছে?

ধরো ভুল করে:

```python
def test():
    test()

test()
```

এটা কখনো থামবে না।

Python unlimited recursion allow করে না।

শেষে সাধারণত:

```text
RecursionError
```

পাবে।

---

# 7️⃣ Recursion Limit দেখা

```python
import sys

limit = sys.getrecursionlimit()

print("Recursion limit:", limit)
```

---

# 8️⃣ `sys.setrecursionlimit()`

Limit পরিবর্তন করা যায়:

```python
import sys

sys.setrecursionlimit(2000)

print(sys.getrecursionlimit())
```

কিন্তু ⚠️ **এটা casually বাড়ানো উচিত নয়।**

খুব বেশি recursion limit দিলে Python process-এর জন্য সমস্যা হতে পারে।

তাই সাধারণ application-এ recursion limit বাড়ানোর আগে algorithm redesign করা ভালো।

---

# 9️⃣ Practical Recursion Example

```python
import sys

print("Limit:", sys.getrecursionlimit())

def countdown(n):

    if n == 0:
        return

    print(n)

    countdown(n - 1)

countdown(5)
```

এখানে recursion safe কারণ:

```text
5
 ↓
4
 ↓
3
 ↓
2
 ↓
1
 ↓
0
 ↓
return
```

---

# 🔟 `sys.float_info`

Python floating-point system-এর information:

```python
import sys

print(sys.float_info)
```

এতে floating-point representation সম্পর্কিত information পাওয়া যায়।

যেমন:

```python
print(sys.float_info.max)
print(sys.float_info.min)
print(sys.float_info.epsilon)
```

---

## `epsilon`

```python
print(sys.float_info.epsilon)
```

এটা floating-point precision সম্পর্কিত একটি গুরুত্বপূর্ণ value।

তবে এখন exact value মুখস্থ করার দরকার নেই।

---

# 1️⃣1️⃣ `sys.int_info`

Python integer representation সম্পর্কেও information পাওয়া যায়:

```python
import sys

print(sys.int_info)
```

আর:

```python
print(sys.int_info.bits_per_digit)
```

এটা Python integer-এর internal representation সম্পর্কে information দেয়।

এগুলো **advanced runtime information**—সাধারণ Python programming-এ প্রতিদিন ব্যবহার করবে না।

---

# 🚀 Day 7 Project — Python Memory Analyzer

এখন আমরা ছোট একটি practical tool বানাব।

User একটি value type select করবে এবং program object-এর shallow memory size দেখাবে।

```python
import sys

number = 100
text = "Python"
numbers = [1, 2, 3, 4, 5]

print("Integer:", sys.getsizeof(number), "bytes")
print("String:", sys.getsizeof(text), "bytes")
print("List:", sys.getsizeof(numbers), "bytes")
```

---

# 🔥 একটু Advanced Version

```python
import sys

objects = {
    "integer": 100,
    "string": "Python",
    "list": [1, 2, 3, 4, 5],
    "tuple": (1, 2, 3, 4, 5),
    "dictionary": {
        "name": "Atiar",
        "age": 20
    }
}

for name, obj in objects.items():

    size = sys.getsizeof(obj)

    print(f"{name}: {size} bytes")
```

এটা তোমার নিজের machine-এ run করো।

**Numbers মুখস্থ করবে না**, কারণ Python version/platform অনুযায়ী ফলাফল পরিবর্তিত হতে পারে।

---

# 🧪 Day 7 Exercise 1

এগুলো compare করো:

```python
import sys

a = []
b = [1]
c = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print(sys.getsizeof(a))
print(sys.getsizeof(b))
print(sys.getsizeof(c))
```

তারপর চিন্তা করো:

> List-এ elements বাড়লে object-এর size কীভাবে পরিবর্তন হচ্ছে?

---

# 🧪 Exercise 2

Recursion limit দেখাও:

```python
import sys

print(sys.getrecursionlimit())
```

তারপর একটা ছোট recursive function লিখে test করো।

---

# 🧪 Exercise 3

Runtime information:

```python
import sys

print("Integer Info:")
print(sys.int_info)

print()

print("Float Info:")
print(sys.float_info)
```

Output দেখে বুঝতে চেষ্টা করো Python-এর numeric runtime সম্পর্কে কী information পাওয়া যাচ্ছে।

---

# 🏆 Day 7 Challenge

একটি **Python Runtime Analyzer** বানাও।

Expected:

```text
========================================
       PYTHON RUNTIME ANALYZER
========================================

Python Version:
3.x.x

Implementation:
cpython

Platform:
linux

Executable:
/usr/bin/python3

Recursion Limit:
1000

Max Size:
9223372036854775807

Integer Info:
...

Float Info:
...

========================================
```

তুমি ব্যবহার করবে:

```python
sys.version
sys.implementation.name
sys.platform
sys.executable
sys.getrecursionlimit()
sys.maxsize
sys.int_info
sys.float_info
```

---

# 🧠 Day 7 Mental Model

এখন `sys` module-কে এভাবে organize করো:

```text
                    sys
                     │
     ┌───────────────┼────────────────┐
     ↓               ↓                ↓
   Input           Runtime           Import
     │               │                │
 sys.stdin      sys.version       sys.path
                sys.platform      sys.modules
                sys.executable
                sys.getsizeof()
                sys.maxsize
                recursion limit
```

---

# 📚 এখন পর্যন্ত `sys` Course

```text
Day 1
Python runtime information
        ↓
Day 2
sys.argv
        ↓
Day 3
sys.path
        ↓
Day 4
stdin / stdout / stderr
        ↓
Day 5
sys.exit() + exit codes
        ↓
Day 6
sys.modules + interpreter + platform
        ↓
Day 7
Memory + recursion + numeric runtime
```

## ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ ৫টি

```python
sys.getsizeof()
sys.maxsize
sys.getrecursionlimit()
sys.float_info
sys.int_info
```

**একটা গুরুত্বপূর্ণ কথা:** `sys`-এর সব attribute production programming-এ সমান গুরুত্বপূর্ণ নয়। `argv`, `path`, `stdin/stdout/stderr`, `exit`, `modules`, `executable`—এগুলো আগে ভালোভাবে আয়ত্ত করো। `float_info`, `int_info` ইত্যাদি মূলত Python runtime সম্পর্কে গভীরভাবে জানার জন্য।


# 🐍 Python `sys` Module — Day 8

আজ আমরা **Practical Project** করব।

আগের ৭ দিনে শেখা জিনিসগুলো একসাথে ব্যবহার করে একটি **Python CLI System Information Tool** বানাব।

Official documentation: [Python `sys` module documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 🎯 Day 8 Goal

আমরা এমন একটি program বানাব:

```text
python sysinfo.py
```

যেটা output দেবে:

```text
========================================
        PYTHON SYSTEM INFORMATION
========================================

Python Version : 3.x.x
Implementation  : cpython
Platform        : linux

Executable:
...

Recursion Limit : 1000
Max Size        : ...

Loaded Modules  : ...

========================================
```

এখানে আমরা ব্যবহার করব:

```python
sys.version
sys.version_info
sys.implementation
sys.platform
sys.executable
sys.getrecursionlimit()
sys.maxsize
sys.modules
```

---

# 1️⃣ Project Structure

একটা folder বানাও:

```text
sys_course/
│
└── sysinfo.py
```

---

# 2️⃣ Basic Version

`sysinfo.py`:

```python
import sys

print("=" * 40)
print("PYTHON SYSTEM INFORMATION")
print("=" * 40)

print("Python Version:", sys.version)
print("Implementation:", sys.implementation.name)
print("Platform:", sys.platform)
print("Executable:", sys.executable)
print("Recursion Limit:", sys.getrecursionlimit())
print("Max Size:", sys.maxsize)
print("Loaded Modules:", len(sys.modules))

print("=" * 40)
```

Run:

```bash
python sysinfo.py
```

---

# 3️⃣ Version সুন্দরভাবে দেখানো

`sys.version` অনেক information দেয়।

আমরা শুধু version number চাইলে:

```python
import sys

version = sys.version_info

print(
    f"{version.major}."
    f"{version.minor}."
    f"{version.micro}"
)
```

Output:

```text
3.13.5
```

---

# 4️⃣ Function ব্যবহার করি

Program বড় হলে সব code একসাথে না রেখে function বানানো ভালো।

```python
import sys


def show_python_version():
    version = sys.version_info

    print(
        f"{version.major}."
        f"{version.minor}."
        f"{version.micro}"
    )


show_python_version()
```

---

# 5️⃣ পুরো System Info Function

```python
import sys


def show_system_info():

    version = sys.version_info

    print("=" * 40)
    print("PYTHON SYSTEM INFORMATION")
    print("=" * 40)

    print(
        "Python Version:",
        f"{version.major}.{version.minor}.{version.micro}"
    )

    print("Implementation:", sys.implementation.name)

    print("Platform:", sys.platform)

    print("Executable:", sys.executable)

    print("Recursion Limit:", sys.getrecursionlimit())

    print("Max Size:", sys.maxsize)

    print("Loaded Modules:", len(sys.modules))

    print("=" * 40)


show_system_info()
```

---

# 6️⃣ `sys.argv` যোগ করি ⭐

এবার program-এ command-line option যোগ করব।

আমরা চাই:

```bash
python sysinfo.py
```

→ সব information

আর:

```bash
python sysinfo.py version
```

→ শুধু Python version

---

## Code

```python
import sys


def show_version():

    version = sys.version_info

    print(
        f"Python "
        f"{version.major}."
        f"{version.minor}."
        f"{version.micro}"
    )


if len(sys.argv) == 1:

    print("Python Version:")
    show_version()

elif sys.argv[1] == "version":

    show_version()

else:

    print("Unknown command")
    sys.exit(1)
```

---

# 7️⃣ Command Test

### Default

```bash
python sysinfo.py
```

### Version

```bash
python sysinfo.py version
```

### Wrong command

```bash
python sysinfo.py hello
```

Output:

```text
Unknown command
```

এবং exit code:

```bash
echo $?
```

```text
1
```

এখানে একসাথে ব্যবহার হলো:

```text
sys.argv
sys.exit()
```

---

# 8️⃣ Multiple Commands ⭐

এবার আরও ভালো CLI বানাই।

Supported commands:

```text
version
platform
python
modules
recursion
```

Code:

```python
import sys


def version():

    v = sys.version_info

    print(f"{v.major}.{v.minor}.{v.micro}")


def platform():

    print(sys.platform)


def python_path():

    print(sys.executable)


def modules():

    print("Loaded modules:", len(sys.modules))


def recursion():

    print("Recursion limit:", sys.getrecursionlimit())


if len(sys.argv) < 2:

    print("Usage:")
    print("python sysinfo.py version")
    print("python sysinfo.py platform")
    print("python sysinfo.py python")
    print("python sysinfo.py modules")
    print("python sysinfo.py recursion")

    sys.exit(1)


command = sys.argv[1]


if command == "version":

    version()

elif command == "platform":

    platform()

elif command == "python":

    python_path()

elif command == "modules":

    modules()

elif command == "recursion":

    recursion()

else:

    print("Unknown command:", command)

    sys.exit(1)
```

---

# 9️⃣ Test করো

### Python version

```bash
python sysinfo.py version
```

### Platform

```bash
python sysinfo.py platform
```

### Python executable

```bash
python sysinfo.py python
```

### Loaded modules

```bash
python sysinfo.py modules
```

### Recursion limit

```bash
python sysinfo.py recursion
```

---

# 🔥 10️⃣ `sys.path` Command যোগ করো

এবার Day 3-এর knowledge ব্যবহার করো।

Function:

```python
def show_paths():

    for path in sys.path:
        print(path)
```

তারপর:

```python
elif command == "path":

    show_paths()
```

এখন:

```bash
python sysinfo.py path
```

দিলে Python-এর module search paths দেখতে পাবে।

---

# 🔥 11️⃣ `modules` Command উন্নত করো

এখন শুধু count দেখাচ্ছি:

```python
print(len(sys.modules))
```

কিন্তু চাইলে module names-ও দেখাতে পারো:

```python
def show_modules():

    for name in sys.modules:
        print(name)
```

তারপর:

```python
elif command == "modules":

    show_modules()
```

---

# ⚠️ একটা গুরুত্বপূর্ণ বিষয়

`sys.modules`-এ অনেক module থাকবে।

তাই:

```python
for name in sys.modules:
    print(name)
```

অনেক output দিতে পারে।

এটা normal।

---

# 🧪 Day 8 Exercise 1

নতুন command যোগ করো:

```bash
python sysinfo.py implementation
```

Output:

```text
cpython
```

ব্যবহার করবে:

```python
sys.implementation.name
```

---

# 🧪 Exercise 2

এই command তৈরি করো:

```bash
python sysinfo.py maxsize
```

Output:

```text
Max size: ...
```

ব্যবহার:

```python
sys.maxsize
```

---

# 🧪 Exercise 3

এই command:

```bash
python sysinfo.py float
```

দিলে:

```text
Float max: ...
Float epsilon: ...
```

দেখাবে।

ব্যবহার করবে:

```python
sys.float_info.max
sys.float_info.epsilon
```

---

# 🏆 Day 8 Final Challenge

এবার complete CLI বানাও:

```text
python sysinfo.py version
python sysinfo.py platform
python sysinfo.py python
python sysinfo.py implementation
python sysinfo.py modules
python sysinfo.py path
python sysinfo.py recursion
python sysinfo.py maxsize
python sysinfo.py float
```

এবং:

```bash
python sysinfo.py help
```

দিলে:

```text
Available commands:

version
platform
python
implementation
modules
path
recursion
maxsize
float
help
```

দেখাবে।

---

# 🧠 Day 8-এ কী শিখলে?

আজ শুধু নতুন `sys` function শেখা নয়—**আগের concepts একসাথে ব্যবহার করা** হয়েছে।

```text
                 sys
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   sys.argv    Runtime     Import
       │          │          │
   CLI input   version    sys.path
               platform   sys.modules
               executable
                  │
                  ↓
              sys.exit()
```

### আজকের সবচেয়ে গুরুত্বপূর্ণ lesson:

> **একটা module শেখার আসল লক্ষ্য তার সব function মুখস্থ করা নয়; বরং কোন problem-এ কোন feature ব্যবহার করতে হয় সেটা বুঝতে শেখা।**

---

## 📚 `sys` Course Progress

```text
Day 1 → Runtime information
Day 2 → sys.argv
Day 3 → sys.path
Day 4 → stdin / stdout / stderr
Day 5 → sys.exit()
Day 6 → sys.modules / executable / platform
Day 7 → memory / recursion / numeric info
Day 8 → ⭐ Complete CLI Project
```

**Day 9-এ আমরা `sys`-এর advanced অংশ এবং `sys` বনাম `os` বনাম `subprocess`—কোন কাজের জন্য কোনটা ব্যবহার করবে—এটা শিখব।**

# 🐍 Python `sys` Module — Day 9

আজকের topic একটু **advanced + practical**:

> `sys` বনাম `os` বনাম `subprocess` — কোন কাজের জন্য কোন module ব্যবহার করবে?

Official documentation: [Python `sys` module documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1️⃣ `sys` আসলে কোথায় ব্যবহার হয়?

এখন পর্যন্ত আমরা দেখেছি:

```text
sys
│
├── sys.argv
├── sys.path
├── sys.modules
├── sys.stdin
├── sys.stdout
├── sys.stderr
├── sys.exit()
├── sys.executable
├── sys.platform
├── sys.version_info
└── sys.getsizeof()
```

এগুলোকে ৩টা category-তে ভাগ করতে পারো:

```text
        sys
         │
 ┌───────┼────────┐
 ↓       ↓        ↓
CLI    Runtime   Import
```

---

# 2️⃣ `sys` বনাম `os` ⭐

এই distinction খুব গুরুত্বপূর্ণ।

### `sys`

Python interpreter/program-এর সাথে কাজ:

```python
import sys

sys.argv
sys.path
sys.modules
sys.version
sys.executable
sys.exit()
```

### `os`

Operating system-এর সাথে কাজ:

```python
import os

os.getcwd()
os.listdir()
os.mkdir()
os.environ
os.path.exists()
```

সহজভাবে:

```text
sys → Python-এর ভিতরের environment
os  → Operating System
```

---

# 3️⃣ Example

Current Python interpreter:

```python
import sys

print(sys.executable)
```

Current directory:

```python
import os

print(os.getcwd())
```

দুটো completely different information।

---

# 4️⃣ `sys.argv` বনাম `os.environ`

Command-line argument:

```bash
python app.py Atiar
```

Python:

```python
import sys

print(sys.argv)
```

এখানে `Atiar` argument।

অন্যদিকে environment variable:

```bash
export USER_NAME=Atiar
```

Python:

```python
import os

print(os.getenv("USER_NAME"))
```

এখানে `USER_NAME` environment variable।

---

# 5️⃣ `sys` বনাম `subprocess` ⭐

এটাও খুব গুরুত্বপূর্ণ।

### `sys`

নিজের Python program-এর সাথে কাজ:

```python
import sys

print(sys.argv)
sys.exit()
```

### `subprocess`

Python থেকে **অন্য program/command চালাতে**:

```python
import subprocess

subprocess.run(["python", "--version"])
```

Concept:

```text
Python program
      │
      ├── sys
      │     ↓
      │   নিজের runtime
      │
      └── subprocess
            ↓
       অন্য program
```

---

# 6️⃣ Example — `sys.exit()`

```python
import sys

print("Starting...")

sys.exit(1)
```

এখানে Python program নিজেই exit করছে।

---

# 7️⃣ Example — `subprocess`

```python
import subprocess

subprocess.run(["python", "--version"])
```

এখানে Python একটি **external command** execute করছে।

---

# 8️⃣ `sys.modules` বনাম `sys.path`

এগুলোও আলাদা।

### `sys.path`

Python কোথায় module খুঁজবে:

```python
import sys

print(sys.path)
```

### `sys.modules`

এই process-এ কোন modules already loaded:

```python
print(sys.modules)
```

Mental model:

```text
import requests
       ↓
   sys.path
       ↓
module খুঁজে পাওয়া
       ↓
load
       ↓
sys.modules
```

এটা Python import system বোঝার জন্য খুব গুরুত্বপূর্ণ।

---

# 9️⃣ `sys.executable` + `subprocess`

এটা practical এবং useful pattern।

ধরো তুমি নিশ্চিত করতে চাও subprocess-এ **বর্তমান Python interpreter**-টাই ব্যবহার হবে।

```python
import sys
import subprocess

subprocess.run([
    sys.executable,
    "--version"
])
```

এখানে:

```text
sys.executable
      ↓
current Python interpreter
      ↓
subprocess
      ↓
Python --version
```

Virtual environment-এর ক্ষেত্রে এই pattern বিশেষভাবে useful।

---

# 🔟 `sys.stdin` + `sys.stdout`

CLI program-এর জন্য:

```python
import sys

name = sys.stdin.readline().strip()

sys.stdout.write(f"Hello {name}\n")
```

এখানে:

```text
stdin  → input
stdout → normal output
stderr → error output
```

---

# 1️⃣1️⃣ `sys.stderr` + CLI Error

```python
import sys

if len(sys.argv) < 2:

    sys.stderr.write(
        "Error: argument required\n"
    )

    sys.exit(1)
```

এটা ভালো CLI pattern:

```text
Invalid input
    ↓
stderr
    ↓
exit code 1
```

---

# 1️⃣2️⃣ `sys.platform` + `os`

দুটো একসাথে ব্যবহার করা যায়।

```python
import sys
import os

print("Platform:", sys.platform)
print("Current directory:", os.getcwd())
```

Output-এর মতো:

```text
Platform: linux
Current directory: /home/user/project
```

---

# 1️⃣3️⃣ Advanced: `sys.flags`

Python interpreter কীভাবে চালু হয়েছে তার কিছু configuration flags দেখতে পারো:

```python
import sys

print(sys.flags)
```

উদাহরণস্বরূপ:

```python
print(sys.flags.debug)
print(sys.flags.optimize)
print(sys.flags.verbose)
```

এগুলো interpreter startup options সম্পর্কে information দেয়।

---

# 1️⃣4️⃣ Advanced: `sys.prefix`

Current Python installation/environment-এর prefix জানতে:

```python
import sys

print(sys.prefix)
```

Virtual environment-এর context বোঝার সময় এটি useful হতে পারে।

আর:

```python
print(sys.base_prefix)
```

দিয়ে base Python installation-এর prefix দেখা যায়।

### Virtual environment concept

```text
System Python
      │
      ↓
Virtual Environment
      │
      ↓
sys.prefix
```

এই দুইটা compare করে virtual environment সম্পর্কিত debugging করা যায়।

---

# 1️⃣5️⃣ Virtual Environment Check

একটি practical function:

```python
import sys


def in_virtual_environment():

    return sys.prefix != sys.base_prefix


if in_virtual_environment():
    print("Virtual environment detected")

else:
    print("System Python")
```

এটা virtual environment detection-এর একটি common approach।

---

# 1️⃣6️⃣ `sys.gettrace()` এবং `sys.getprofile()`

আরও advanced features আছে:

```python
sys.gettrace()
sys.getprofile()
```

এগুলো Python debugging/profiling mechanisms-এর সাথে সম্পর্কিত।

এখন এগুলো implement করার দরকার নেই।

শুধু জানবে:

```text
gettrace()
    ↓
debugging / tracing

getprofile()
    ↓
profiling
```

---

# 1️⃣7️⃣ `sys._getframe()` ⚠️

Python-এর internal frame information access করার জন্য:

```python
import sys

frame = sys._getframe()

print(frame)
```

এখানে `_` দেখছ।

এ ধরনের underscore-prefixed API সাধারণ application code-এর জন্য **internal implementation detail** হিসেবে ধরা হয়।

তাই এখন:

> Understand it, but don't depend on it.

---

# 🧠 18️⃣ কোনটা কখন ব্যবহার করবে?

এই table-টা খুব ভালোভাবে বুঝে রাখো:

|Problem|Module|
|---|---|
|CLI arguments|`sys.argv`|
|Python version|`sys.version_info`|
|Current interpreter|`sys.executable`|
|Module search path|`sys.path`|
|Loaded modules|`sys.modules`|
|Standard input|`sys.stdin`|
|Standard output|`sys.stdout`|
|Error output|`sys.stderr`|
|Program exit|`sys.exit()`|
|Files/folders|`os`|
|Environment variables|`os.environ` / `os.getenv()`|
|OS command/external process|`subprocess`|

---

# 🔥 Day 9 Practical Project

এবার একটি **Environment Diagnostic Tool** বানাও।

`diagnostic.py`:

```python
import sys
import os
import subprocess


print("=" * 50)
print("       PYTHON ENVIRONMENT DIAGNOSTIC")
print("=" * 50)


# Python information
version = sys.version_info

print(
    "Python:",
    f"{version.major}.{version.minor}.{version.micro}"
)

print("Implementation:", sys.implementation.name)

# Platform
print("Platform:", sys.platform)

# Interpreter
print("Executable:", sys.executable)

# Working directory
print("Working Directory:", os.getcwd())

# Virtual environment
if sys.prefix != sys.base_prefix:
    print("Virtual Environment: Yes")
else:
    print("Virtual Environment: No")

# Recursion
print("Recursion Limit:", sys.getrecursionlimit())

# Loaded modules
print("Loaded Modules:", len(sys.modules))

# External Python version
result = subprocess.run(
    [sys.executable, "--version"],
    capture_output=True,
    text=True
)

print("Subprocess Python:", result.stdout.strip())

print("=" * 50)
```

Run:

```bash
python diagnostic.py
```

---

# 🧪 Day 9 Exercises

### Exercise 1

নিজের system-এর:

```text
Python executable
Python version
Platform
Current directory
```

একসাথে print করো।

---

### Exercise 2

Check করো তুমি virtual environment-এর মধ্যে আছো কিনা:

```python
import sys

print(sys.prefix)
print(sys.base_prefix)
```

তারপর compare করো।

---

### Exercise 3 ⭐

একটি program বানাও:

```bash
python checker.py
```

যদি Python version 3.10-এর নিচে হয়:

```text
Python 3.10+ required
```

এবং:

```python
sys.exit(1)
```

করবে।

---

# 🏆 Day 9 Challenge

একটি CLI command বানাও:

```bash
python diagnostic.py version
python diagnostic.py platform
python diagnostic.py python
python diagnostic.py cwd
python diagnostic.py venv
```

Example:

```bash
python diagnostic.py venv
```

Output:

```text
Virtual Environment: Yes
```

এখানে ব্যবহার করবে:

```python
sys.argv
sys.version_info
sys.platform
sys.executable
sys.prefix
sys.base_prefix
os.getcwd()
sys.exit()
```

---

# 🎯 Day 9-এর সবচেয়ে গুরুত্বপূর্ণ Lesson

তুমি এখন `sys`-কে শুধু function-এর list হিসেবে দেখবে না।

```text
                    Python Program
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
       CLI/Input         Runtime          Import
          │                │                │
      sys.argv        sys.version       sys.path
      sys.stdin       sys.platform      sys.modules
      sys.stdout      sys.executable
      sys.stderr      sys.prefix
          │
          ↓
      sys.exit()
```

### `sys` শেখার Priority

**Must know ⭐⭐⭐**

```text
sys.argv
sys.path
sys.modules
sys.executable
sys.stdin
sys.stdout
sys.stderr
sys.exit()
sys.version_info
```

**Useful ⭐⭐**

```text
sys.platform
sys.prefix
sys.base_prefix
sys.getsizeof()
sys.getrecursionlimit()
sys.flags
```

**Advanced ⭐**

```text
sys.implementation
sys.float_info
sys.int_info
sys.gettrace()
sys.getprofile()
```

**Internal/avoid depending on casually:**

```text
sys._getframe()
```

পরের **Day 10 হবে Final Project + `sys` module-এর complete revision + interview questions + practical tasks**।

# 🐍 Python `sys` Module — Day 10

## 🎓 Final Revision + Final Project + Interview Practice

আজ `sys` module-এর **complete course** শেষ করব। আজকের লক্ষ্য নতুন অনেক function শেখা নয়—বরং এতদিনের concepts একসাথে ব্যবহার করা।

Official documentation: [Python `sys` module documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

---

# 1. 🧠 Complete `sys` Revision

এখন পুরো module-টা category অনুযায়ী মনে রাখো।

### ⭐ CLI / User Input

```python
sys.argv
sys.stdin
```

### ⭐ Output

```python
sys.stdout
sys.stderr
```

### ⭐ Program Control

```python
sys.exit()
```

### ⭐ Python Runtime

```python
sys.version
sys.version_info
sys.executable
sys.implementation
sys.platform
```

### ⭐ Import System

```python
sys.path
sys.modules
```

### ⭐ Runtime / Limits

```python
sys.maxsize
sys.getsizeof()
sys.getrecursionlimit()
sys.setrecursionlimit()
```

### ⭐ Advanced

```python
sys.prefix
sys.base_prefix
sys.flags
sys.float_info
sys.int_info
```

---

# 2. 🔥 Final Project — `pyinfo`

আমরা একটি ছোট কিন্তু realistic **CLI Python Environment Analyzer** বানাব।

Run:

```bash
python pyinfo.py
```

অথবা:

```bash
python pyinfo.py version
python pyinfo.py platform
python pyinfo.py python
python pyinfo.py venv
python pyinfo.py modules
python pyinfo.py path
python pyinfo.py memory
python pyinfo.py help
```

---

# 3. Project Structure

```text
pyinfo/
│
└── pyinfo.py
```

---

# 4. Complete Project

```python
import sys


def show_version():
    v = sys.version_info

    print(
        f"Python: "
        f"{v.major}.{v.minor}.{v.micro}"
    )


def show_platform():
    print("Platform:", sys.platform)


def show_python():
    print("Python executable:")
    print(sys.executable)


def show_venv():
    if sys.prefix != sys.base_prefix:
        print("Virtual Environment: Yes")
        print("Environment:", sys.prefix)
    else:
        print("Virtual Environment: No")


def show_modules():
    print("Loaded modules:", len(sys.modules))


def show_path():
    print("Python module search paths:")

    for path in sys.path:
        print(" -", path)


def show_memory():
    objects = {
        "integer": 100,
        "string": "Python",
        "list": [1, 2, 3, 4, 5],
        "tuple": (1, 2, 3, 4, 5),
    }

    for name, obj in objects.items():
        print(
            f"{name}: "
            f"{sys.getsizeof(obj)} bytes"
        )


def show_help():
    print("""
Available commands:

version
platform
python
venv
modules
path
memory
help
""")


def show_all():
    print("=" * 50)
    print("           PYTHON ENVIRONMENT")
    print("=" * 50)

    show_version()

    print()

    show_platform()

    print()

    show_python()

    print()

    show_venv()

    print()

    show_modules()

    print("=" * 50)


# -------------------------
# Main Program
# -------------------------

if len(sys.argv) < 2:

    show_all()

    sys.exit(0)


command = sys.argv[1]


if command == "version":

    show_version()


elif command == "platform":

    show_platform()


elif command == "python":

    show_python()


elif command == "venv":

    show_venv()


elif command == "modules":

    show_modules()


elif command == "path":

    show_path()


elif command == "memory":

    show_memory()


elif command == "help":

    show_help()


else:

    print(
        f"Unknown command: {command}",
        file=sys.stderr
    )

    print(
        "Use: python pyinfo.py help",
        file=sys.stderr
    )

    sys.exit(1)
```

---

# 5. 🧪 Test the Project

### Python version

```bash
python pyinfo.py version
```

Expected:

```text
Python: 3.x.x
```

---

### Platform

```bash
python pyinfo.py platform
```

তোমার Ubuntu-তে সাধারণত:

```text
Platform: linux
```

---

### Python interpreter

```bash
python pyinfo.py python
```

Output:

```text
Python executable:
/home/.../.venv/bin/python
```

---

### Virtual environment

```bash
python pyinfo.py venv
```

Output:

```text
Virtual Environment: Yes
```

অথবা:

```text
Virtual Environment: No
```

---

### Loaded modules

```bash
python pyinfo.py modules
```

Output:

```text
Loaded modules: ...
```

---

### Module search path

```bash
python pyinfo.py path
```

এখানে Python কোন কোন directory-তে module খোঁজে দেখতে পাবে।

---

### Memory

```bash
python pyinfo.py memory
```

Output-এর মতো:

```text
integer: ... bytes
string: ... bytes
list: ... bytes
tuple: ... bytes
```

Numbers environment অনুযায়ী পরিবর্তিত হতে পারে।

---

# 6. ❌ Invalid Command

চালাও:

```bash
python pyinfo.py hello
```

তখন:

```text
Unknown command: hello
Use: python pyinfo.py help
```

এবং exit status হবে non-zero।

Ubuntu terminal-এ:

```bash
echo $?
```

---

# 7. 🔥 এখন বুঝো আমরা কী কী ব্যবহার করলাম

একটি project-এর মধ্যে:

```text
sys.argv
   ↓
CLI command গ্রহণ

sys.version_info
   ↓
Python version

sys.platform
   ↓
OS/platform

sys.executable
   ↓
Current Python interpreter

sys.prefix
sys.base_prefix
   ↓
Virtual environment

sys.modules
   ↓
Loaded modules

sys.path
   ↓
Import search path

sys.getsizeof()
   ↓
Object shallow size

sys.stderr
   ↓
Error message

sys.exit()
   ↓
Exit status
```

এটাই একটি module শেখার আসল উদ্দেশ্য।

---

# 8. 🎯 Interview Questions

এগুলো নিজে answer করার চেষ্টা করো।

### Q1. What is `sys`?

> Python-এর standard library module, যা Python interpreter/runtime এবং system-level interfaces-এর সাথে কাজ করার জন্য ব্যবহৃত হয়।

---

### Q2. What is `sys.argv`?

> Command-line arguments-এর list।

---

### Q3. `sys.argv[0]` কী?

সাধারণত current script/program-এর নাম বা path।

---

### Q4. `sys.path` কী?

Python module/package search করার locations-এর list।

---

### Q5. `sys.modules` কী?

বর্তমান Python process-এ imported/loaded modules-এর dictionary।

---

### Q6. `sys.executable` কী?

বর্তমানে যে Python interpreter দিয়ে program চলছে তার executable-এর path।

---

### Q7. `sys.exit()` কী করে?

Program termination initiate করে এবং optional exit status দেয়।

---

### Q8. Exit code `0` সাধারণত কী বোঝায়?

সাধারণত successful execution।

---

### Q9. `sys.stdin`, `stdout`, `stderr` কী?

```text
stdin  → standard input
stdout → standard output
stderr → standard error
```

---

### Q10. `sys.getsizeof()` কী?

একটি object-এর **shallow memory size** bytes-এ দেয়।

---

### Q11. `sys.maxsize` কি Python integer-এর maximum value?

**না।**

Python integers arbitrary precision হতে পারে।

---

### Q12. `sys.platform` কী?

Current platform/OS সম্পর্কে identifier দেয়।

---

# 9. 🧩 Final Practical Questions

এগুলো coding interview-এর মতো practice করো।

### Problem 1

Command:

```bash
python app.py Atiar 25
```

`sys.argv` ব্যবহার করে:

```text
Name: Atiar
Age: 25
```

print করো।

---

### Problem 2

Program-এর Python version check করো।

যদি Python 3.10-এর নিচে হয়:

```text
Python 3.10+ required
```

এবং non-zero exit করো।

---

### Problem 3

`sys.path` থেকে সব search location print করো।

---

### Problem 4

Check করো `json` module already loaded কিনা:

```python
"json" in sys.modules
```

তারপর:

```python
import json
```

এর পরে আবার check করো।

---

### Problem 5 ⭐

একটি program বানাও যেটা:

```text
Python Version
Platform
Executable
Virtual Environment
Loaded Modules
Recursion Limit
```

একসাথে দেখাবে।

---

# 10. 🏆 Final Challenge

এবার কোনো tutorial না দেখে নিজে **`pyinfo.py` আবার লিখবে**।

শুধু এই reference list ব্যবহার করবে:

```text
sys.argv
sys.version_info
sys.platform
sys.executable
sys.prefix
sys.base_prefix
sys.modules
sys.path
sys.getsizeof()
sys.getrecursionlimit()
sys.stdin
sys.stdout
sys.stderr
sys.exit()
```

যদি নিজে লিখতে পারো, তাহলে `sys` module-এর practical foundation ভালোভাবে তৈরি হয়েছে।

---

# 🧠 `sys` Module — Final Cheat Sheet

|Feature|ব্যবহার|
|---|---|
|`sys.argv`|CLI arguments|
|`sys.path`|Module search locations|
|`sys.modules`|Loaded modules|
|`sys.version`|Python version information|
|`sys.version_info`|Structured version|
|`sys.executable`|Current Python interpreter|
|`sys.platform`|Platform information|
|`sys.stdin`|Standard input|
|`sys.stdout`|Standard output|
|`sys.stderr`|Error output|
|`sys.exit()`|Program exit|
|`sys.getsizeof()`|Shallow object size|
|`sys.maxsize`|Platform-related max-sized integer|
|`sys.getrecursionlimit()`|Recursion limit|
|`sys.prefix`|Current environment prefix|
|`sys.base_prefix`|Base Python prefix|
|`sys.float_info`|Float information|
|`sys.int_info`|Integer representation info|
|`sys.flags`|Interpreter flags|

---

# 🎓 তোমার `sys` Course Complete

```text
Day 1  → Runtime Information       ✅
Day 2  → sys.argv                  ✅
Day 3  → sys.path                  ✅
Day 4  → stdin/stdout/stderr       ✅
Day 5  → sys.exit + Exit Codes     ✅
Day 6  → modules/interpreter       ✅
Day 7  → Memory/Recursion          ✅
Day 8  → CLI Project               ✅
Day 9  → sys vs os vs subprocess   ✅
Day 10 → Final Project + Revision  ✅
```

### এখন সবচেয়ে ভালো পরবর্তী ধাপ

`sys` শেষ করে সরাসরি আরেকটা বিশাল module মুখস্থ না করে **`os` + `sys` + `pathlib` + `shutil` + `subprocess`** একসাথে একটি **Python Automation/File Management Project**-এ ব্যবহার করলে তোমার শেখাটা অনেক বেশি solid হবে।


হ্যাঁ। খুব সহজভাবে বললে:

> **`sys` module ব্যবহার করা হয় Python program এবং Python interpreter-এর সাথে সরাসরি কাজ করার জন্য।**

Official docs: [Python `sys` documentation](https://docs.python.org/3/library/sys.html?utm_source=chatgpt.com)

## 🔥 `sys` কোথায় ব্যবহার হয়?

|Feature|কেন ব্যবহার হয়|Example|
|---|---|---|
|`sys.argv`|Command-line input নেওয়া|`python app.py hello`|
|`sys.exit()`|Program বন্ধ করা|Validation failure|
|`sys.path`|Python কোথায় module খুঁজবে|Custom module|
|`sys.modules`|কোন module loaded আছে দেখা|Import debugging|
|`sys.stdin`|Standard input নেওয়া|CLI/pipe|
|`sys.stdout`|Normal output|CLI tools|
|`sys.stderr`|Error output|CLI errors|
|`sys.executable`|কোন Python চলছে জানা|Virtual environment|
|`sys.version_info`|Python version check|Compatibility|
|`sys.platform`|OS/platform check|Linux/Windows behavior|
|`sys.getsizeof()`|Object-এর shallow size দেখা|Memory analysis|
|`sys.getrecursionlimit()`|Recursion limit দেখা|Debugging|

---

## 1. 🖥️ CLI Application

ধরো:

```bash
python calculator.py 10 20
```

Python:

```python
import sys

a = int(sys.argv[1])
b = int(sys.argv[2])

print(a + b)
```

এখানে `sys.argv` ব্যবহার হচ্ছে।

---

## 2. 🚪 Program Control

কোনো input ভুল হলে:

```python
import sys

if age < 0:
    print("Invalid age")
    sys.exit(1)
```

CLI tools এবং automation-এ এটা খুব common।

---

## 3. 📦 Python Import System

Python যখন করে:

```python
import mymodule
```

তখন module কোথায় খুঁজবে সেটা বোঝার জন্য:

```python
sys.path
```

এবং already loaded modules-এর জন্য:

```python
sys.modules
```

গুরুত্বপূর্ণ।

---

## 4. 🐍 কোন Python চলছে?

বিশেষ করে virtual environment-এর ক্ষেত্রে:

```python
import sys

print(sys.executable)
```

এটা দেখাবে current Python interpreter কোথায়।

---

## 5. 💻 OS অনুযায়ী Behavior

```python
import sys

if sys.platform == "linux":
    print("Linux")

elif sys.platform == "win32":
    print("Windows")
```

Cross-platform program-এ কাজে লাগে।

---

## 6. 🔄 Linux Pipe / CLI Automation

ধরো:

```bash
cat data.txt | python analyzer.py
```

Python:

```python
import sys

data = sys.stdin.read()

print(len(data))
```

এখানে:

```text
data.txt
   ↓
pipe |
   ↓
sys.stdin
   ↓
Python
```

এটা Linux এবং automation-এর জন্য গুরুত্বপূর্ণ।

---

# `sys` বনাম `os` — সবচেয়ে সহজ পার্থক্য

এটা মনে রাখো:

```text
              Python
                 │
        ┌────────┴────────┐
        ↓                 ↓
       sys               os
        ↓                 ↓
 Python Runtime       Operating System
```

### `sys`

```python
sys.argv
sys.path
sys.modules
sys.executable
sys.exit()
```

➡️ **Python-এর runtime/interpreter নিয়ে কাজ।**

### `os`

```python
os.getcwd()
os.listdir()
os.mkdir()
os.environ
```

➡️ **Operating System-এর files, folders, environment ইত্যাদি নিয়ে কাজ।**

---

# 🎯 তোমার জন্য Priority

তোমার Python শেখার ক্ষেত্রে `sys`-এর সবকিছু সমান গুরুত্বপূর্ণ নয়।

### ⭐⭐⭐ অবশ্যই শিখবে

```python
sys.argv
sys.path
sys.exit()
sys.stdin
sys.stdout
sys.stderr
sys.executable
sys.version_info
sys.modules
```

### ⭐⭐ পরে জানবে

```python
sys.platform
sys.prefix
sys.base_prefix
sys.getsizeof()
sys.getrecursionlimit()
```

### ⭐ Advanced

```python
sys.float_info
sys.int_info
sys.flags
sys.gettrace()
sys.getprofile()
```

**এক লাইনে:**  
`os` দিয়ে **computer/OS-এর সাথে** কাজ করো, আর `sys` দিয়ে **Python program/interpreter-এর সাথে** কাজ করো।