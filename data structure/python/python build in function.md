
Python-এর **built-in functions** মানে হলো—যেগুলো ব্যবহার করতে আলাদা করে কোনো লাইব্রেরি import করতে হয় না। এগুলো সরাসরি Python-এ পাওয়া যায়।

---

## 🔹 1. Input / Output

```python
print("Hello")
x = input("Enter number: ")
```

- `print()` → output দেখায়
    
- `input()` → user input নেয় (string হিসেবে)
    

---

## 🔹 2. Type Conversion

```python
int("10")
float("3.5")
str(25)
bool(0)
list("abc")
tuple([1,2])
set([1,2,2])
```

- `int()`, `float()`, `str()`
    
- `bool()`
    
- `list()`, `tuple()`, `set()`
    

---

## 🔹 3. Numeric Functions

```python
abs(-5)        # 5
pow(2, 3)      # 8
round(3.6)     # 4
min(1,2,3)
max(4,6,1)
sum([1,2,3])
```

- `abs()`
    
- `pow()`
    
- `round()`
    
- `min()`, `max()`
    
- `sum()`
    

---

## 🔹 4. Sequence & Collection

```python
len([1,2,3])
sorted([3,1,2])
reversed([1,2,3])
enumerate(["a","b"])
zip([1,2],[3,4])
```

- `len()`
    
- `sorted()`
    
- `reversed()`
    
- `enumerate()`
    
- `zip()`
    

---

## 🔹 5. Type Checking

```python
type(10)
isinstance(10, int)
```

- `type()`
    
- `isinstance()`
    

---

## 🔹 6. Logical / Boolean

```python
all([True, True])
any([False, True])
```

- `all()` → সব True হলে True
    
- `any()` → একটি True হলেই True
    

---

## 🔹 7. Character / ASCII

```python
ord('A')   # 65
chr(65)    # 'A'
```

- `ord()` → char → ASCII
    
- `chr()` → ASCII → char
    

---

## 🔹 8. Math / Iteration

```python
range(5)
```

- `range()` → sequence তৈরি করে
    

---

## 🔹 9. Object / Memory

```python
id(x)
help(print)
```

- `id()` → memory address
    
- `help()` → documentation
    

---

## 🔹 10. Execution / Dynamic

```python
eval("2+3")
```

- `eval()` → string কে expression হিসেবে execute করে (⚠️ careful)
    

---

## 🔹 11. File / Advanced

```python
open("file.txt")
```

- `open()` → file handle
    

---

## 🔹 Most Used Built-ins (Interview Favorite ⭐)

- `print()`
    
- `len()`
    
- `type()`
    
- `range()`
    
- `sum()`
    
- `min() / max()`
    
- `sorted()`
    
- `enumerate()`
    
- `zip()`
    
- `isinstance()`
    

---

Python-এর **built-in modules** মানে হলো—যেগুলো Python install করলেই পাওয়া যায়, আলাদা করে pip install করতে হয় না।

নিচে **সবচেয়ে important built-in modules** category অনুযায়ী দেওয়া হলো 👇

---

## 🔹 1. System & OS Related

### `sys`

```python
import sys
print(sys.argv)
print(sys.path)
sys.exit()
```

👉 command-line args, Python environment control

### `os`

```python
import os
os.getcwd()
os.listdir()
os.mkdir("test")
os.remove("file.txt")
```

👉 file, directory, environment variable

---

## 🔹 2. Math & Numbers

### `math`

```python
import math
math.sqrt(16)
math.ceil(4.2)
math.floor(4.9)
math.pi
```

### `random`

```python
import random
random.randint(1, 10)
random.choice([1,2,3])
random.shuffle(list)
```

---

## 🔹 3. Date & Time

### `datetime`

```python
from datetime import datetime
now = datetime.now()
print(now.year)
```

### `time`

```python
import time
time.sleep(2)
```

---

## 🔹 4. Data Structures

### `collections`

```python
from collections import Counter, defaultdict
Counter("banana")
```

### `heapq`

```python
import heapq
heapq.heappush(h, 5)
```

---

## 🔹 5. Iteration & Functional

### `itertools`

```python
import itertools
itertools.permutations([1,2,3])
```

### `functools`

```python
from functools import reduce
reduce(lambda x,y: x+y, [1,2,3])
```

---

## 🔹 6. File & Data Handling

### `json`

```python
import json
json.dumps({"a":1})
json.loads('{"a":1}')
```

### `pickle`

```python
import pickle
pickle.dump(obj, file)
```

### `csv`

```python
import csv
```

---

## 🔹 7. Text & Pattern

### `re`

```python
import re
re.search("ab", "abc")
```

### `string`

```python
import string
string.ascii_letters
```

---

## 🔹 8. Security & Encoding

### `hashlib`

```python
import hashlib
hashlib.md5(b"text").hexdigest()
```

### `base64`

```python
import base64
```

---

## 🔹 9. Debugging & Testing

### `logging`

```python
import logging
logging.warning("Warning!")
```

### `unittest`

```python
import unittest
```

---

## 🔹 10. Networking & Internet

### `socket`

```python
import socket
```

### `http`

```python
import http.client
```

---

## 🔹 11. Concurrency

### `threading`

```python
import threading
```

### `multiprocessing`

```python
import multiprocessing
```

---

## 🔹 12. Import Utilities

### `importlib`

```python
import importlib
```

---

## ⭐ Most Important Built-in Modules (Interview)

* `os`
* `sys`
* `math`
* `random`
* `datetime`
* `collections`
* `itertools`
* `json`
* `re`
* `logging`

---

## 🔹 Check All Built-in Modules

```python
help("modules")
```

---

`datetime` module Python-এর **সবচেয়ে important built-in module**গুলোর একটি।
এখানে আমি **interview + real project-এ সবচেয়ে বেশি ব্যবহৃত method গুলো** সুন্দরভাবে explain করছি 👇

---

# 📦 `datetime` Module (Important Methods)

```python
import datetime
from datetime import date, time, datetime, timedelta
```

---

## 🔹 1️⃣ `date` Class (Only Date)

### ✔️ `date.today()`

আজকের তারিখ

```python
from datetime import date
print(date.today())
```

### ✔️ `date(year, month, day)`

নিজে date বানানো

```python
d = date(2026, 1, 20)
print(d)
```

### ✔️ `date.year`, `month`, `day`

```python
print(d.year, d.month, d.day)
```

---

## 🔹 2️⃣ `time` Class (Only Time)

### ✔️ `time(hour, minute, second)`

```python
from datetime import time
t = time(10, 30, 45)
print(t)
```

### ✔️ `hour`, `minute`, `second`

```python
print(t.hour)
```

---

## 🔹 3️⃣ `datetime` Class (Date + Time) ⭐ MOST IMPORTANT

### ✔️ `datetime.now()`

বর্তমান date + time

```python
from datetime import datetime
now = datetime.now()
print(now)
```

### ✔️ `datetime.today()`

`now()` এর মতোই কাজ করে

```python
datetime.today()
```

### ✔️ `datetime(year, month, day, hour, min, sec)`

```python
dt = datetime(2026,1,20,10,30,0)
```

---

### ✔️ Access Parts

```python
now.year
now.month
now.day
now.hour
now.minute
now.second
```

---

## 🔹 4️⃣ Format & Parse (🔥 VERY IMPORTANT)

### ✔️ `strftime()` → date → string

```python
now.strftime("%Y-%m-%d %H:%M:%S")
```

| Code | Meaning    |
| ---- | ---------- |
| %Y   | Year       |
| %m   | Month      |
| %d   | Day        |
| %H   | Hour (24)  |
| %M   | Minute     |
| %S   | Second     |
| %A   | Day name   |
| %B   | Month name |

---

### ✔️ `strptime()` → string → datetime

```python
dt = datetime.strptime("2026-01-20", "%Y-%m-%d")
```

📌 **Interview Question:**
➡️ *Difference between `strftime` & `strptime`*

* `strftime` → format
* `strptime` → parse

---

## 🔹 5️⃣ `timedelta` (Date Difference) ⭐⭐

### ✔️ Add / Subtract Date

```python
from datetime import timedelta

future = now + timedelta(days=5)
past = now - timedelta(days=2)
```

### ✔️ Difference Between Two Dates

```python
d1 = datetime(2026,1,1)
d2 = datetime(2026,1,20)
diff = d2 - d1
print(diff.days)
```

---

## 🔹 6️⃣ Comparison

```python
if d1 < d2:
    print("Earlier")
```

---

## 🔹 7️⃣ Convert Between Types

### ✔️ datetime → date / time

```python
now.date()
now.time()
```

---

## 🔹 8️⃣ ISO Format (API / Django)

```python
now.isoformat()
```

---

## 🔹 9️⃣ Timestamp (Unix Time)

```python
now.timestamp()
```

---

## 🔹 10️⃣ Weekday / Calendar

```python
now.weekday()      # 0 = Monday
now.isoweekday()   # 1 = Monday
```

---

## ⭐ Interview Most Important Summary

| Topic            | Why              |
| ---------------- | ---------------- |
| `datetime.now()` | current time     |
| `strftime()`     | formatting       |
| `strptime()`     | parsing          |
| `timedelta`      | date calculation |
| `timestamp()`    | unix time        |
| comparison       | validation       |

---

## 🔥 Django / Real-World Usage

```python
from django.utils import timezone
timezone.now()
```

---

# ⭐ Python `datetime` – Important Interview Questions

---

## 1️⃣ `datetime.now()` vs `datetime.today()`

**Q:** পার্থক্য কী?

**A:**
➡️ বাস্তবে কোনো পার্থক্য নেই
➡️ দুটোই current date + time দেয়

```python
datetime.now()
datetime.today()
```

---

## 2️⃣ `date` vs `datetime`

**Q:** `date` আর `datetime` এর পার্থক্য?

**A:**

* `date` → শুধু date (year, month, day)
* `datetime` → date + time

---

## 3️⃣ `strftime()` vs `strptime()` ⭐⭐

**Q:** Difference?

**A:**

* `strftime()` → datetime ➝ string (format)
* `strptime()` → string ➝ datetime (parse)

---

## 4️⃣ `timedelta` কী কাজে লাগে?

**A:**
➡️ Date/time add–subtract করতে

```python
now + timedelta(days=5)
```

---

## 5️⃣ দুইটা date এর difference কীভাবে বের করো?

```python
d2 - d1   # returns timedelta
```

---

## 6️⃣ Unix Timestamp কী?

**A:**
➡️ 1970-01-01 থেকে seconds count

```python
datetime.now().timestamp()
```

---

## 7️⃣ `weekday()` vs `isoweekday()`

**A:**

* `weekday()` → Monday = 0
* `isoweekday()` → Monday = 1

---

## 8️⃣ String থেকে date convert করো কীভাবে?

```python
datetime.strptime("2026-01-20", "%Y-%m-%d")
```

---

## 9️⃣ Date format change কীভাবে করো?

```python
now.strftime("%d-%m-%Y")
```

---

## 🔟 `datetime` object immutable কেন?

**A:**
➡️ Safety & consistency বজায় রাখার জন্য
➡️ পরিবর্তন করলে নতুন object তৈরি হয়

---

## 11️⃣ `datetime` comparison করা যায়?

**A:**
➡️ হ্যাঁ

```python
if d1 < d2:
    pass
```

---

## 12️⃣ Timezone-aware vs naive datetime ⭐⭐⭐

**Q:** Difference?

**A:**

* **Naive** → timezone info নাই
* **Aware** → timezone info আছে

```python
datetime.now()          # naive
timezone.now()          # aware (Django)
```

---

## 13️⃣ Django-তে কোনটা use করবে?

**A:**
➡️ `django.utils.timezone.now()`

---

## 14️⃣ ISO format কী?

**A:**
➡️ Standard date-time format (API)

```python
now.isoformat()
```

---

## 15️⃣ `datetime` vs `time` module

**A:**

* `datetime` → date + time manipulation
* `time` → sleep, timestamp, low-level time

---

## ⭐ Top 5 MUST REMEMBER (Interview)

1. `strftime()` vs `strptime()`
2. `timedelta`
3. Unix timestamp
4. Timezone-aware datetime
5. Date comparison

---

## 🔥 Bonus Trick (Interview Impression)

```python
from datetime import datetime, timezone
datetime.now(timezone.utc)
```

---
