অবশ্যই। আমরা **M01-এ কোনো গুরুত্বপূর্ণ topic skip করব না**। তুমি যেহেতু এই roadmap follow করে শেষ পর্যন্ত AI Writing Platform build করতে চাও, তাই M01-কে শুধু basic Python না ধরে **AI/ML-এর জন্য complete Python foundation** হিসেবে করব।

# 🟢 M01 — Python for AI: Complete Foundation

## 🎯 M01-এর লক্ষ্য

M01 শেষ হলে তুমি যেন:

* Python confidently লিখতে পারো
* problem solve করতে পারো
* clean code লিখতে পারো
* files/data handle করতে পারো
* OOP বুঝতে পারো
* API/JSON নিয়ে কাজ করতে পারো
* reusable code লিখতে পারো
* error/debugging করতে পারো
* AI/ML code বুঝতে পারো
* পরের milestone-এর NumPy, Pandas, PyTorch code পড়তে পারো

---

# M01 Topic Map

আমরা M01-কে **15টি section**-এ ভাগ করব।

```text
M01
│
├── 01 Python Environment
├── 02 Syntax & Variables
├── 03 Data Types
├── 04 Operators
├── 05 Conditional Statements
├── 06 Loops
├── 07 Strings
├── 08 Collections
├── 09 Functions
├── 10 Modules & Packages
├── 11 Exception Handling
├── 12 File Handling
├── 13 OOP
├── 14 Advanced Python
└── 15 AI-oriented Python Project
```

---

# 01 — Python Environment

প্রথমে environment সম্পর্কে পরিষ্কার ধারণা।

### Topics

* Python কী?
* Interpreter কী?
* Compiler vs Interpreter
* Python implementation
* CPython
* Python version
* Python executable
* `python`
* `python3`
* `pip`
* Package
* Module
* Library
* Framework
* Virtual environment
* `venv`
* `requirements.txt`

### Commands

```bash
python3 --version
pip --version
```

Virtual environment:

```bash
python3 -m venv venv
```

Activate:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

Deactivate:

```bash
deactivate
```

---

# 02 — Python Syntax & Variables

### Topics

* Python syntax
* Indentation
* Comments
* Statements
* Expressions
* Variables
* Assignment
* Multiple assignment
* Constants convention
* Naming convention
* Dynamic typing
* Type checking
* `id()`
* `type()`

Example:

```python
name = "Atiar"
age = 25
height = 5.8

print(name)
print(type(name))
print(type(age))
```

Multiple assignment:

```python
x, y, z = 10, 20, 30
```

Swap:

```python
x, y = y, x
```

---

# 03 — Complete Python Data Types

এখানে কোনো data type skip করব না।

## Numeric

```text
int
float
complex
```

Example:

```python
x = 10
y = 3.14
z = 2 + 3j
```

## Boolean

```python
True
False
```

## String

```python
name = "Atiar"
```

## None

```python
value = None
```

## Collections

```text
list
tuple
set
dict
```

---

# 04 — Operators

Complete operator system:

### Arithmetic

```text
+
-
*
/
//
%
**
```

### Comparison

```text
==
!=
>
<
>=
<=
```

### Logical

```text
and
or
not
```

### Assignment

```text
=
+=
-=
*=
/=
%=
//=
**=
```

### Membership

```text
in
not in
```

### Identity

```text
is
is not
```

### Bitwise

```text
&
|
^
~
<<
>>
```

### Operator precedence

এটাও শিখবে।

---

# 05 — Conditional Statements

### Topics

* `if`
* `else`
* `elif`
* nested condition
* multiple conditions
* logical conditions
* ternary operator
* conditional expression
* `match-case`

Example:

```python
age = 20

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

Ternary:

```python
result = "Pass" if marks >= 40 else "Fail"
```

---

# 06 — Loops

Complete loop system:

### `for`

```python
for i in range(5):
    print(i)
```

### `while`

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

### Loop control

```text
break
continue
pass
```

### Nested loops

### `range()`

### Iteration

### `enumerate()`

### `zip()`

Example:

```python
names = ["A", "B", "C"]

for index, name in enumerate(names):
    print(index, name)
```

---

# 07 — Strings

এটা AI/NLP-এর জন্য খুব গুরুত্বপূর্ণ।

### Topics

* String creation
* Indexing
* Slicing
* Negative indexing
* Concatenation
* Repetition
* Membership
* String immutability

### Methods

```text
lower()
upper()
capitalize()
title()
strip()
lstrip()
rstrip()
replace()
split()
rsplit()
join()
find()
rfind()
index()
count()
startswith()
endswith()
isdigit()
isalpha()
isalnum()
isspace()
```

### Formatting

```text
f-string
format()
%
```

Example:

```python
name = "Atiar"
age = 25

text = f"My name is {name} and I am {age} years old."
```

### Escape characters

```text
\n
\t
\\
\"
\'
```

### Raw strings

```python
path = r"C:\Users\Atiar"
```

---

# 08 — Collections

এটা খুব deeply শিখবে।

## List

```text
create
index
slice
append
extend
insert
remove
pop
clear
index
count
sort
reverse
copy
```

Example:

```python
numbers = [5, 2, 8, 1]

numbers.append(10)
numbers.sort()

print(numbers)
```

---

## Tuple

```text
creation
indexing
slicing
unpacking
immutability
count
index
```

---

## Set

```text
add
remove
discard
pop
union
intersection
difference
symmetric_difference
subset
superset
```

---

## Dictionary

খুব গুরুত্বপূর্ণ।

```text
keys
values
items
get
update
pop
popitem
setdefault
clear
copy
```

Example:

```python
user = {
    "name": "Atiar",
    "age": 25
}

print(user["name"])
print(user.get("email"))
```

---

# 09 — Functions

Python-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

### Topics

* Function definition
* Calling
* Parameters
* Arguments
* Return
* Multiple return
* Default arguments
* Keyword arguments
* Positional arguments
* `*args`
* `**kwargs`
* Scope
* Local variable
* Global variable
* `global`
* `nonlocal`
* Nested functions
* First-class functions
* Higher-order functions
* Lambda
* Recursion
* Docstrings
* Type hints

Example:

```python
def add(a: int, b: int) -> int:
    return a + b
```

Multiple return:

```python
def calculate(a, b):
    return a + b, a - b
```

Unpacking:

```python
sum_value, difference = calculate(10, 5)
```

---

# 10 — Modules & Packages

### Topics

* Module
* Import
* `from ... import`
* Alias
* Package
* `__init__.py`
* `__name__`
* `__main__`

Example:

```python
import math

print(math.sqrt(25))
```

Own module:

```text
project/
│
├── main.py
└── calculator.py
```

`calculator.py`

```python
def add(a, b):
    return a + b
```

`main.py`

```python
from calculator import add

print(add(10, 20))
```

---

# 11 — Exception Handling

AI applications-এ error handling খুব গুরুত্বপূর্ণ।

### Topics

```text
try
except
else
finally
raise
```

Example:

```python
try:
    number = int(input("Enter number: "))
except ValueError:
    print("Invalid number")
```

Multiple exceptions:

```python
try:
    ...
except ValueError:
    ...
except ZeroDivisionError:
    ...
```

Custom exception:

```python
class InvalidAgeError(Exception):
    pass
```

---

# 12 — File Handling

AI project-এ text files নিয়ে অনেক কাজ হবে।

### Topics

* Open
* Read
* Write
* Append
* File modes
* `with`
* Text files
* CSV
* JSON
* Encoding
* `pathlib`

Example:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    text = file.read()

print(text)
```

Write:

```python
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("Hello AI")
```

---

# JSON

AI API-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

```python
import json

data = {
    "name": "Atiar",
    "skills": ["Python", "Django", "PyTorch"]
}

json_data = json.dumps(data, indent=4)

print(json_data)
```

Load:

```python
data = json.loads(json_data)
```

File:

```python
with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```

---

# CSV

```python
import csv

with open("data.csv", newline="") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

---

# 13 — Object-Oriented Programming

এটা পুরোপুরি শিখব।

## Class & Object

```python
class User:
    pass
```

Object:

```python
user = User()
```

---

## Constructor

```python
class User:

    def __init__(self, name):
        self.name = name
```

---

## Instance attributes

## Class attributes

## Instance methods

## Class methods

```python
@classmethod
```

## Static methods

```python
@staticmethod
```

---

# OOP-এর 4 Pillars

### 1. Encapsulation

### 2. Inheritance

### 3. Polymorphism

### 4. Abstraction

---

## Inheritance

```python
class Animal:

    def speak(self):
        print("Animal sound")


class Dog(Animal):

    def speak(self):
        print("Bark")
```

---

## Multiple inheritance

## Method overriding

## `super()`

## Abstract class

```python
from abc import ABC, abstractmethod
```

---

# 14 — Advanced Python

এখানে M01-এর advanced portion।

### Comprehensions

```text
List comprehension
Set comprehension
Dictionary comprehension
```

Example:

```python
squares = [x * x for x in range(10)]
```

---

### Iterators

```text
iter()
next()
```

---

### Generators

```python
def numbers():
    for i in range(5):
        yield i
```

---

### Decorators

```python
def decorator(func):

    def wrapper():
        print("Before")
        func()
        print("After")

    return wrapper
```

---

### Closures

### `map()`

### `filter()`

### `reduce()`

### `sorted()`

### `any()`

### `all()`

---

# Context Managers

```python
with open(...) as file:
    ...
```

এটার ভিতরের concept-ও বুঝবে।

---

# Dataclasses

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

---

# Type Hints

```python
def process_text(text: str) -> str:
    return text.lower()
```

Advanced:

```text
List
Dict
Tuple
Optional
Union
Any
Callable
```

---

# Regular Expressions

AI/NLP-এর আগে Regex জানা useful।

শিখবে:

```text
.
*
+
?
^
$
[]
()
{}
|
\
\d
\w
\s
```

Python:

```python
import re

text = "My email is test@example.com"

result = re.findall(
    r'[\w\.-]+@[\w\.-]+',
    text
)

print(result)
```

---

# 15 — AI-Oriented Python

এখন M01-এর সবচেয়ে important practical অংশ।

আমরা একটা ছোট **Text Processing Engine** বানাব।

Input:

```text
Artificial intelligence is changing the world.
Python is widely used in AI.
```

System:

```text
             TEXT
              ↓
       ┌──────────────┐
       │ Text Engine  │
       └──────┬───────┘
              │
      ┌───────┼────────┐
      ▼       ▼        ▼
   Words   Sentences  Chars
      │       │        │
      └───────┼────────┘
              ▼
          Statistics
```

Features:

```text
Total characters
Total words
Total sentences
Unique words
Average word length
Word frequency
Most common words
Longest word
Shortest word
```

Example output:

```text
Total Words: 12
Total Sentences: 2
Unique Words: 11
Average Word Length: 6.1

Most Common Words:
AI        2
Python    1
world     1
```

---

# 🧪 M01 Practice System

M01 শুধু পড়লে হবে না।

তুমি minimum:

### Level 1

**30 basic problems**

### Level 2

**30 intermediate problems**

### Level 3

**20 advanced problems**

### Total

```text
80 Python Problems
```

---

# 🧩 M01 Mini Projects

## Project 1 — Calculator

Features:

```text
+
-
*
/
%
**
```

---

## Project 2 — Student Management

```text
Add student
Remove student
Update student
Search student
Calculate result
```

---

## Project 3 — Contact Book

```text
Add contact
Search
Update
Delete
List
```

---

## Project 4 — Text Analyzer

```text
Word count
Sentence count
Character count
Frequency
Longest word
Shortest word
```

---

# 🚀 M01 Main Project

শেষে বানাবে:

## AI Text Processing CLI

Architecture:

```text
ai_text_tool/
│
├── main.py
├── text_processor.py
├── analyzer.py
├── tokenizer.py
├── utils.py
├── models.py
├── exceptions.py
├── data/
│   └── sample.txt
│
├── tests/
│   ├── test_processor.py
│   └── test_analyzer.py
│
├── requirements.txt
└── README.md
```

Features:

```text
1. Load text
2. Clean text
3. Count words
4. Count sentences
5. Count characters
6. Find unique words
7. Word frequency
8. Search words
9. Replace words
10. Text statistics
11. Export JSON
12. Export TXT
```

এটা পরে M05-এর NLP pipeline-এর foundation হিসেবে ব্যবহার করব।

---

# 🧠 M01 শেষে তোমার Knowledge Map

```text
Python
│
├── Syntax
├── Variables
├── Data Types
├── Operators
├── Conditions
├── Loops
├── Strings
├── Lists
├── Tuples
├── Sets
├── Dictionaries
│
├── Functions
│   ├── Arguments
│   ├── *args
│   ├── **kwargs
│   ├── Lambda
│   ├── Scope
│   └── Recursion
│
├── Modules
├── Packages
├── Exceptions
├── Files
│   ├── TXT
│   ├── CSV
│   └── JSON
│
├── OOP
│   ├── Class
│   ├── Object
│   ├── Inheritance
│   ├── Polymorphism
│   ├── Encapsulation
│   └── Abstraction
│
├── Advanced
│   ├── Comprehension
│   ├── Iterator
│   ├── Generator
│   ├── Decorator
│   ├── Closure
│   ├── Dataclass
│   └── Context Manager
│
└── AI-oriented Python
    └── Text Processing Engine
```

## ✅ M01 Completion Criteria

M01 complete বলব তখনই যখন তুমি independently পারবে:

* Python project setup করতে
* virtual environment তৈরি করতে
* functions লিখতে
* complex data structure manipulate করতে
* text process করতে
* JSON/CSV handle করতে
* class design করতে
* exceptions handle করতে
* modules বানাতে
* regular expression ব্যবহার করতে
* generators/decorators-এর concept explain করতে
* এবং **AI Text Processing CLI নিজে build করতে**।

**M01-এর কোনো topic শুধু নাম শুনে skip করব না।** আমরা যখন প্রতিটি section পড়ব, তখন **concept → কেন দরকার → syntax → অনেক example → common mistakes → practice → mini project → main project integration** এই sequence-এ যাব।

পরের ধাপে M01-এর **01 — Python Environment & Python execution model** থেকে একদম বিস্তারিত lesson শুরু করা যাবে।


---
# 🟢 M01.01 — Python Environment & Python Execution Model

আজ থেকে **M01 systematically শুরু করছি**। এই lesson-এর লক্ষ্য শুধু Python install করা নয়—Python code **কোথায় থাকে, কীভাবে execute হয়, interpreter কী করে, `python`/`python3`/`pip` কী, virtual environment কেন দরকার**—সব পরিষ্কার করা।

---

# 1. Python কী?

**Python হলো a high-level, general-purpose programming language।**

এটি ব্যবহার করা হয়:

```text
Web Development
     ↓
Django / FastAPI

Data Analysis
     ↓
NumPy / Pandas

Machine Learning
     ↓
Scikit-learn

Deep Learning
     ↓
PyTorch / TensorFlow

NLP
     ↓
Transformers / spaCy
```

আমাদের final AI Writing Platform-এর ক্ষেত্রে:

```text
Python
 ├── NLP
 ├── Machine Learning
 ├── PyTorch
 ├── Transformers
 ├── FastAPI
 └── Django
```

তাই Python-এর foundation strong হওয়া অত্যন্ত গুরুত্বপূর্ণ।

---

# 2. Programming Language আর Python-এর মধ্যে সম্পর্ক

ধরো তুমি লিখলে:

```python
print("Hello World")
```

Computer সরাসরি এই English-like code বুঝতে পারে না।

Computer ultimately machine instructions execute করে।

Conceptually:

```text
তুমি
 │
 │ Python code
 ▼
Python implementation
 │
 ▼
Machine-level execution
 │
 ▼
CPU
```

তাই Python code execute করার জন্য Python-এর runtime/implementation প্রয়োজন।

---

# 3. Python Interpreter কী?

সহজভাবে:

> **Interpreter হলো এমন software যা Python program execute করতে সাহায্য করে।**

তুমি লিখলে:

```python
x = 10
y = 20

print(x + y)
```

Python runtime এই program-এর instructions process করে এবং output দেয়:

```text
30
```

---

# 4. Python কি পুরোপুরি Interpreter-based?

এখানে একটা common misconception আছে।

অনেকে বলে:

> Python is an interpreted language.

শিক্ষার শুরুতে এটা বলা যায়, কিন্তু technically Python execution একটু বেশি interesting।

বিশেষ করে **CPython**-এ:

```text
Python Source Code
        │
        ▼
      Parser
        │
        ▼
     Bytecode
        │
        ▼
Python Virtual Machine
        │
        ▼
      Execution
```

অর্থাৎ `.py` source code সাধারণত সরাসরি CPU machine code হয়ে যায় না।

---

# 5. CPython কী?

**CPython হলো Python language-এর সবচেয়ে widely used implementation।**

তুমি যখন সাধারণভাবে Python install করো, বেশিরভাগ ক্ষেত্রে তুমি CPython ব্যবহার করছ।

Example:

```bash
python3 --version
```

যদি দেখো:

```text
Python 3.x.x
```

তাহলে সাধারণত তুমি CPython implementation ব্যবহার করছ।

---

# 6. Python Execution Model

এটা M01.01-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

ধরো তোমার file:

```text
hello.py
```

এর ভিতরে:

```python
name = "Atiar"

print(name)
```

তুমি চালালে:

```bash
python3 hello.py
```

High-level flow:

```text
hello.py
   │
   ▼
Source Code
   │
   ▼
Lexing / Parsing
   │
   ▼
AST
   │
   ▼
Bytecode
   │
   ▼
Python Virtual Machine
   │
   ▼
Output
```

এখন একে একে বুঝি।

---

# 7. Source Code

তুমি যে code লেখো:

```python
x = 10
print(x)
```

এটাই **source code**।

File:

```text
program.py
```

---

# 8. Parsing

Python প্রথমে code-এর syntax বুঝতে চেষ্টা করে।

যেমন:

```python
x = 10
print(x)
```

valid Python।

কিন্তু:

```python
x =
```

এটা invalid syntax।

Python তখন error দেখাবে:

```text
SyntaxError
```

অর্থাৎ parser-এর কাজের একটি অংশ হলো:

> Code-এর structure/syntax valid কিনা সেটা বুঝতে সাহায্য করা।

---

# 9. AST — Abstract Syntax Tree

Python source code-এর structure internally represent করার জন্য **AST (Abstract Syntax Tree)** ব্যবহার করে।

Example:

```python
x = 10
```

Conceptually:

```text
Assignment
├── Target
│   └── x
└── Value
    └── 10
```

তুমি এখন AST-এর implementation মুখস্থ করবে না।

শুধু concept:

```text
Source Code
     ↓
AST
     ↓
Program Structure
```

---

# 10. Bytecode

CPython source code থেকে **bytecode** তৈরি করে।

Bytecode হলো Python Virtual Machine-এর জন্য intermediate instructions।

Conceptually:

```text
Python Code
     ↓
Bytecode
     ↓
Python VM
```

তাই Python-এর `.pyc` files-এর নাম শুনে থাকতে পারো।

---

# 11. `.pyc` কী?

Python কিছু ক্ষেত্রে compiled bytecode cache করতে পারে।

সাধারণত দেখা যায়:

```text
__pycache__/
```

এর মধ্যে:

```text
something.cpython-3xx.pyc
```

জাতীয় file থাকতে পারে।

Example:

```text
project/
│
├── main.py
└── __pycache__/
    └── main.cpython-3xx.pyc
```

এখানে `.pyc` হলো Python bytecode cache।

### গুরুত্বপূর্ণ

`.pyc` হলো:

> **Machine code নয়।**

এটা Python-এর bytecode।

---

# 12. Python Virtual Machine

Bytecode execute করার জন্য CPython-এর execution machinery কাজ করে।

Conceptually:

```text
Bytecode
   ↓
Python Virtual Machine
   ↓
Execution
```

এখন পুরো pipeline:

```text
              Python Program
                    │
                    ▼
              Source Code
                    │
                    ▼
                 Parser
                    │
                    ▼
                   AST
                    │
                    ▼
                Bytecode
                    │
                    ▼
        Python Virtual Machine
                    │
                    ▼
                 Output
```

এই flow তোমাকে **বোঝা উচিত**, মুখস্থ করা নয়।

---

# 13. তাহলে Python কি Slow?

Python-এর performance নিয়ে পরে আমরা বিস্তারিত আলোচনা করব।

এখন শুধু বুঝো:

Python সাধারণত C/C++-এর মতো native compiled languages-এর তুলনায় অনেক ক্ষেত্রে slower।

কিন্তু Python-এর advantage:

```text
Easy syntax
+
Huge ecosystem
+
Rapid development
+
AI/ML libraries
+
Web frameworks
```

আর AI/ML-এর ক্ষেত্রে heavy numerical computation অনেক সময় চলে:

```text
Python
   ↓
PyTorch / NumPy
   ↓
C/C++ / CUDA
   ↓
CPU/GPU
```

এটা পরে M02/M15-এ আরও পরিষ্কার হবে।

---

# 14. Python Version কী?

Python-এর major versions:

```text
Python 2
Python 3
```

আজকের modern development-এর জন্য:

```text
Python 3.x
```

ব্যবহার করবে।

তোমার AI project-এর জন্য আমরা **একটি নির্দিষ্ট supported Python 3 version** ব্যবহার করব এবং project অনুযায়ী dependencies pin করব।

---

# 15. Python Version Check

Terminal খুলে:

```bash
python3 --version
```

অথবা:

```bash
python --version
```

Possible:

```text
Python 3.11.x
```

অথবা:

```text
Python 3.12.x
```

---

# 16. `python` বনাম `python3`

Linux/Ubuntu-তে অনেক সময়:

```bash
python
```

command configured থাকে না।

কিন্তু:

```bash
python3
```

কাজ করে।

তাই Ubuntu-তে সাধারণত:

```bash
python3 --version
```

ব্যবহার করা নিরাপদ।

---

# 17. Python Executable কোথায়?

Linux:

```bash
which python3
```

Example:

```text
/usr/bin/python3
```

Virtual environment activate করলে:

```bash
which python
```

তখন path পরিবর্তিত হবে।

এটা পরে virtual environment বুঝতে খুব গুরুত্বপূর্ণ হবে।

---

# 18. `pip` কী?

`pip` হলো Python package installer।

ধরো তুমি NumPy install করতে চাও:

```bash
pip install numpy
```

অথবা Linux-এ:

```bash
python3 -m pip install numpy
```

আমি সাধারণত recommend করব:

```bash
python3 -m pip install package_name
```

কারণ এতে তুমি কোন Python interpreter-এর সঙ্গে pip চলছে সেটা পরিষ্কারভাবে specify করছ।

---

# 19. Package কী?

ধরো Python নিজে তোমাকে অনেক functionality দেয়।

কিন্তু AI development-এর জন্য তোমার লাগবে:

```text
NumPy
Pandas
PyTorch
Transformers
spaCy
```

এগুলো external packages/libraries।

Example:

```bash
pip install numpy
```

তারপর:

```python
import numpy
```

---

# 20. Library vs Framework

এখন basic distinction:

### Library

তুমি library-কে call করো।

```text
Your Code
   ↓
Library
```

Example:

```python
import numpy as np
```

### Framework

Framework সাধারণত application structure/control flow-এর বড় অংশ নির্ধারণ করে।

```text
Framework
   ↓
Your Code
```

Examples:

```text
Django
FastAPI
```

এই distinction পরে Django এবং AI service architecture-এ কাজে লাগবে।

---

# 21. Virtual Environment কেন দরকার?

এটা **অত্যন্ত গুরুত্বপূর্ণ**।

ধরো:

### Project A

```text
Django 5.x
```

### Project B

```text
Django অন্য version
```

একই global Python environment-এ install করলে conflict হতে পারে।

তাই:

```text
Computer
│
├── Project A
│   └── Virtual Environment A
│
├── Project B
│   └── Virtual Environment B
│
└── Project C
    └── Virtual Environment C
```

প্রতিটি project-এর dependency আলাদা রাখা যায়।

---

# 22. Virtual Environment তৈরি

Ubuntu/Linux:

```bash
python3 -m venv venv
```

Project:

```text
my_project/
└── venv/
```

Activate:

```bash
source venv/bin/activate
```

Terminal-এ সাধারণত:

```text
(venv)
```

দেখাবে।

---

# 23. Virtual Environment-এর ভিতরে Python

Activate করার পর:

```bash
which python
```

আগের global path-এর পরিবর্তে environment-এর path দেখাবে।

এটাই খুব important concept:

```text
Global Python
      │
      X

Project Python
      │
      ▼
   venv Python
```

---

# 24. Package Install

Environment activate করে:

```bash
python -m pip install numpy
```

তারপর:

```bash
python -m pip show numpy
```

Packages:

```bash
python -m pip list
```

---

# 25. requirements.txt

Project-এর dependencies record করার জন্য:

```text
requirements.txt
```

Example:

```text
numpy
pandas
```

Install:

```bash
python -m pip install -r requirements.txt
```

বর্তমান installed versions capture করতে:

```bash
python -m pip freeze > requirements.txt
```

তবে production project-এ blindly `pip freeze` করার বদলে dependency management এবং version pinning বুঝে ব্যবহার করা ভালো।

---

# 26. কেন requirements.txt গুরুত্বপূর্ণ?

ধরো তুমি project GitHub-এ upload করলে।

অন্য developer:

```text
Clone project
     ↓
Create venv
     ↓
pip install -r requirements.txt
     ↓
Run project
```

এতে environment reproduce করা সহজ হয়।

---

# 27. `__pycache__` নিয়ে ধারণা

তুমি project চালানোর পর দেখতে পারো:

```text
project/
│
├── main.py
└── __pycache__/
```

ভয় পাওয়ার কিছু নেই।

এটি Python bytecode cache-এর জন্য তৈরি হতে পারে।

---

# 28. Interactive Python Shell

Terminal-এ:

```bash
python3
```

তাহলে:

```text
>>>
```

দেখবে।

এটা Python REPL।

REPL:

```text
Read
Evaluate
Print
Loop
```

Example:

```python
>>> 10 + 20
30
```

```python
>>> name = "Atiar"
>>> print(name)
Atiar
```

Exit:

```python
exit()
```

অথবা Linux:

```text
Ctrl + D
```

---

# 29. Script বনাম REPL

### REPL

Quick experiment:

```python
>>> 2 + 3
5
```

### Script

File:

```text
main.py
```

Code:

```python
print(2 + 3)
```

Run:

```bash
python3 main.py
```

Output:

```text
5
```

AI development-এ দুইটাই useful।

---

# 30. First Proper Python Program

একটি directory তৈরি করো:

```bash
mkdir python_ai
cd python_ai
```

Virtual environment:

```bash
python3 -m venv venv
```

Activate:

```bash
source venv/bin/activate
```

Create:

```bash
touch main.py
```

`main.py`:

```python
print("Hello, AI World!")
```

Run:

```bash
python main.py
```

Output:

```text
Hello, AI World!
```

---

# 31. Python Program Execution Observe করা

এবার:

```python
print("Step 1")

x = 10

print("Step 2")

y = 20

print("Result:", x + y)

print("Step 3")
```

Output:

```text
Step 1
Step 2
Result: 30
Step 3
```

Python সাধারণভাবে program-এর execution flow অনুসরণ করে।

পরের lessons-এ আমরা দেখব কীভাবে:

```text
condition
loop
function
exception
```

এই flow পরিবর্তন করে।

---

# 32. Python-এর Memory Concept — Basic Introduction

এখন খুব গভীরে যাব না।

ধরো:

```python
x = 10
```

Conceptually:

```text
x ───────► 10
```

আর:

```python
y = x
```

Conceptually:

```text
x ───────► 10
y ───────► 10
```

Python variable সম্পর্কে গুরুত্বপূর্ণ ধারণা:

> Variable সাধারণত value-এর container হিসেবে ভাবা সহজ হলেও Python-এর object model-এ variable একটি object-এর reference/name হিসেবে কাজ করে।

এটা আমরা **M01.02 Data Types + Memory Model**-এ deeply দেখব।

---

# 33. Python Dynamically Typed

Python-এ আগে থেকে variable type declare করতে হয় না:

```python
x = 10
```

তারপর:

```python
x = "Hello"
```

এটা valid।

কারণ Python dynamically typed।

তবে type hints ব্যবহার করতে পারো:

```python
x: int = 10
```

এটা Python-কে C++/Java-এর মতো statically typed করে না; type hint মূলত developer/tooling-এর জন্য।

---

# 34. Python-এর Strong Typing

Python dynamically typed হলেও **strongly typed**।

Example:

```python
x = "10"
y = 20

print(x + y)
```

এখানে error হবে, কারণ string আর integer সরাসরি যোগ করা যায় না।

তবে:

```python
x = "10"
y = 20

print(int(x) + y)
```

Output:

```text
30
```

এই distinction:

```text
Dynamic typing
        ≠
Weak typing
```

এটা interview-এও useful।

---

# 35. Python Documentation দেখা

Terminal:

```bash
python
```

তারপর:

```python
help()
```

অথবা:

```python
help(str)
```

Specific:

```python
help(print)
```

আর:

```python
dir(str)
```

এগুলো পরে debugging/learning-এ অনেক useful হবে।

---

# 36. `pip` সম্পর্কে Important Commands

Virtual environment active করে:

```bash
python -m pip --version
```

Package install:

```bash
python -m pip install numpy
```

Package uninstall:

```bash
python -m pip uninstall numpy
```

List:

```bash
python -m pip list
```

Show:

```bash
python -m pip show numpy
```

Update pip:

```bash
python -m pip install --upgrade pip
```

---

# 37. M01.01-এর Mental Model

এখন পুরো বিষয়টা এভাবে মনে রাখো:

```text
                 YOU
                  │
                  ▼
             Python Code
                  │
                  ▼
              .py File
                  │
                  ▼
               CPython
                  │
                  ▼
               Parsing
                  │
                  ▼
                 AST
                  │
                  ▼
              Bytecode
                  │
                  ▼
        Python Execution System
                  │
                  ▼
                CPU
```

আর package side:

```text
Python
 │
 ├── pip
 │
 ├── Virtual Environment
 │
 └── Packages
       ├── NumPy
       ├── Pandas
       ├── PyTorch
       ├── Transformers
       └── spaCy
```

---

# 🧪 M01.01 Practice

এখন theory শেষ। এই exercises **নিজে terminal-এ করবে**।

### Task 1

Check:

```bash
python3 --version
```

### Task 2

Check:

```bash
which python3
```

### Task 3

Create:

```text
python_ai/
```

### Task 4

Create virtual environment:

```bash
python3 -m venv venv
```

### Task 5

Activate it:

```bash
source venv/bin/activate
```

### Task 6

Check:

```bash
which python
```

### Task 7

Create:

```text
main.py
```

and write:

```python
print("My Python AI Journey Started")
```

### Task 8

Run:

```bash
python main.py
```

### Task 9

Enter REPL:

```bash
python
```

তারপর:

```python
10 + 20
```

এবং:

```python
name = "Atiar"
print(name)
```

### Task 10

Check:

```bash
python -m pip list
```

---

# 🧠 Concept Questions

Code না লিখেও answer করার চেষ্টা করো:

1. Python কী?
2. CPython কী?
3. Interpreter বলতে কী বোঝ?
4. Source code কী?
5. Bytecode কী?
6. `.pyc` কী?
7. `__pycache__` কী?
8. Python Virtual Machine বলতে কী বোঝ?
9. `python` এবং `python3`-এর পার্থক্য কী?
10. `pip` কী?
11. Package কী?
12. Library এবং Framework-এর পার্থক্য কী?
13. Virtual environment কেন ব্যবহার করি?
14. `requirements.txt` কেন দরকার?
15. Python dynamically typed বলতে কী বোঝ?
16. Dynamic typing আর weak typing কি একই?
17. REPL কী?
18. `.py` file এবং REPL-এর মধ্যে পার্থক্য কী?
19. Python source code থেকে execution পর্যন্ত basic flow কী?
20. AI development-এ Python কেন এত গুরুত্বপূর্ণ?

---

# 🎯 M01.01 Completion Test

নিজেকে এই প্রশ্নটা করো:

> **"আমি যদি `python main.py` লিখি, তাহলে আমার Python code execution হওয়ার আগে/সময় মোটামুটি কী কী ধাপের মধ্য দিয়ে যায়?"**

তোমার answer ideally এমন হওয়া উচিত:

```text
main.py
   ↓
Python/CPython
   ↓
Parsing
   ↓
AST
   ↓
Bytecode
   ↓
Python execution machinery
   ↓
CPU
```

এটা যদি বুঝে থাকো, **M01.01 complete**।

---

## পরবর্তী Lesson

**M01.02 — Python Syntax, Variables & Object Model**

এখানে আমরা আরও গভীরে যাব:

```text
Syntax
Statements
Expressions
Variables
Objects
References
Memory
id()
type()
Assignment
Multiple Assignment
Unpacking
Mutable vs Immutable
Dynamic Typing
Naming Rules
PEP 8
```

বিশেষ করে **`x = 10` আসলে Python-এর ভিতরে কী ঘটায়**—এটা visual mental model দিয়ে বুঝব।

---
# 🟢 M01.02 — Python Syntax, Variables & Object Model

এখন আমরা Python-এর **core mental model** শিখব। এই lesson ভালোভাবে বুঝলে পরের Data Types, Functions, OOP, NumPy, PyTorch—সব অনেক সহজ হবে।

আজকের lesson:

```text
M01.02
│
├── 01 Syntax
├── 02 Statements
├── 03 Expressions
├── 04 Indentation
├── 05 Comments
├── 06 Variables
├── 07 Objects
├── 08 References
├── 09 Assignment
├── 10 type()
├── 11 id()
├── 12 Dynamic Typing
├── 13 Mutable vs Immutable
├── 14 Naming Rules
├── 15 Multiple Assignment
├── 16 Unpacking
├── 17 Constants
├── 18 PEP 8
└── 19 Practice + Test
```

---

# 1. Python Syntax কী?

**Syntax হলো Python code লেখার নিয়ম।**

যেমন:

```python
print("Hello")
```

এটি valid syntax।

কিন্তু:

```python
print("Hello"
```

এখানে closing `)` নেই।

তাই Python syntax error দেবে।

```text
SyntaxError
```

সহজভাবে:

> Syntax = Programming language-এর grammar rules.

যেমন English-এ:

```text
I am learning Python.
```

grammar-এর নিয়ম আছে।

Python-এরও:

```python
print("I am learning Python.")
```

লেখার নির্দিষ্ট নিয়ম আছে।

---

# 2. Python Statement কী?

**Statement হলো এমন একটি instruction যা Python execute করে।**

Example:

```python
x = 10
```

এটি একটি assignment statement।

আর:

```python
print(x)
```

এটি একটি function call statement হিসেবে কাজ করছে।

একটি program:

```python
x = 10
y = 20
print(x + y)
```

এখানে একাধিক statement আছে।

Execution:

```text
x = 10
   ↓
y = 20
   ↓
print(x + y)
```

---

# 3. Expression কী?

**Expression এমন code যা একটি value produce করে।**

Example:

```python
10 + 20
```

এর result:

```text
30
```

আর:

```python
x + y
```

এটাও expression।

আর:

```python
10
```

এটাও একটি expression/value expression।

---

# 4. Statement বনাম Expression

এটা খুব গুরুত্বপূর্ণ।

### Expression

```python
10 + 20
```

Result:

```text
30
```

### Statement

```python
x = 10 + 20
```

এখানে পুরোটা assignment statement।

ভেতরে:

```python
10 + 20
```

একটি expression।

Mental model:

```text
Statement
│
└── Expression
```

সব statement expression নয়, কিন্তু অনেক statement-এর মধ্যে expression থাকে।

---

# 5. Python Indentation

Python-এর সবচেয়ে গুরুত্বপূর্ণ syntax ruleগুলোর একটি হলো **indentation**।

C/C++/Java-তে সাধারণত:

```cpp
if (x > 10) {
    cout << x;
}
```

Python:

```python
if x > 10:
    print(x)
```

এখানে indentation structure বোঝায়।

---

# 6. Indentation কেন গুরুত্বপূর্ণ?

দেখো:

```python
if True:
    print("Hello")
```

Valid।

কিন্তু:

```python
if True:
print("Hello")
```

Invalid।

কারণ `if` block-এর ভিতরের code properly indented হয়নি।

---

# 7. সাধারণত কত spaces?

Python community convention:

```text
4 spaces
```

Example:

```python
if age >= 18:
    print("Adult")
```

Nested:

```python
if age >= 18:
    if age >= 60:
        print("Senior")
```

এখানে:

```text
if age >= 18:
    4 spaces

if age >= 60:
        8 spaces

print:
            12 spaces
```

---

# 8. Tab বনাম Spaces

একই project-এ indentation-এর জন্য সাধারণত **4 spaces** ব্যবহার করো।

VS Code সাধারণত automatically handle করতে পারে।

Best practice:

```text
Use spaces
Prefer 4 spaces
Don't randomly mix tabs and spaces
```

---

# 9. Colon `:` কেন ব্যবহার হয়?

Python block শুরু হওয়ার আগে সাধারণত `:` থাকে।

Examples:

```python
if age >= 18:
    ...
```

```python
for i in range(5):
    ...
```

```python
while x < 10:
    ...
```

```python
def add(a, b):
    ...
```

```python
class User:
    ...
```

Mental model:

```text
Block header
     ↓
     :
     ↓
Indented block
```

---

# 10. Comments

Comment হলো programmer-এর জন্য লেখা explanation, যা সাধারণ code execution-এর অংশ হিসেবে execute হয় না।

Single-line:

```python
# This is a comment

name = "Atiar"
```

Inline:

```python
age = 25  # User age
```

---

# 11. Multi-line Documentation

Python-এ documentation-এর জন্য **docstring** ব্যবহার করা হয়।

Example:

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

এটা সাধারণ comment-এর চেয়ে আলাদা concept।

পরে Functions lesson-এ আরও গভীরভাবে দেখব।

---

# 12. Variables কী?

এখন আসি সবচেয়ে গুরুত্বপূর্ণ অংশে।

ধরো:

```python
x = 10
```

Beginner explanation:

> `x` একটি variable এবং তার value 10।

এটা শেখার জন্য ঠিক আছে।

কিন্তু Python-এর actual object model বুঝতে গেলে আরও precise explanation:

> `x` হলো একটি **name/reference**, যা একটি Python object-এর দিকে refer করে।

এটা খুব গুরুত্বপূর্ণ।

---

# 13. Python Object কী?

Python-এর প্রায় সব data-ই object।

যেমন:

```python
10
```

একটি integer object।

```python
"Hello"
```

একটি string object।

```python
[1, 2, 3]
```

একটি list object।

```python
{"name": "Atiar"}
```

একটি dictionary object।

এমনকি function-ও object।

---

# 14. Object-এর মধ্যে কী থাকে?

Conceptually একটি Python object-এর মধ্যে থাকে:

```text
Object
│
├── Type
├── Value
└── Identity
```

### Type

Object কোন ধরনের?

```python
10
```

এর type:

```text
int
```

### Value

Value:

```text
10
```

### Identity

Object-এর unique identity/runtime identity থাকে।

Python-এ `id()` দিয়ে identity-এর একটি representation দেখা যায়।

---

# 15. `type()` Function

```python
x = 10

print(type(x))
```

Output:

```text
<class 'int'>
```

String:

```python
name = "Atiar"

print(type(name))
```

Output:

```text
<class 'str'>
```

List:

```python
numbers = [1, 2, 3]

print(type(numbers))
```

Output:

```text
<class 'list'>
```

---

# 16. `id()` Function

```python
x = 10

print(id(x))
```

এটা একটি integer-like identity value দেখাবে।

Example:

```text
140123456789
```

**Exact number তোমার system অনুযায়ী পরিবর্তিত হবে।**

`id()` সম্পর্কে এখন basic idea:

> একটি object-এর identity identify করতে সাহায্য করে।

---

# 17. `x = 10` আসলে কী করে?

এটা M01-এর সবচেয়ে গুরুত্বপূর্ণ concept।

তুমি লিখলে:

```python
x = 10
```

Beginner mental model:

```text
x → 10
```

আর Python object model:

```text
        ┌─────────────┐
x ─────►│ int object  │
        │ value = 10  │
        └─────────────┘
```

অর্থাৎ:

```text
x
│
└──── reference/name ────► object 10
```

---

# 18. `y = x`

ধরো:

```python
x = 10
y = x
```

Conceptually:

```text
        ┌─────────────┐
x ─────►│             │
        │ int = 10    │
y ─────►│             │
        └─────────────┘
```

দুটো name একই object-এর দিকে refer করতে পারে।

Check:

```python
x = 10
y = x

print(id(x))
print(id(y))
```

অনেক ক্ষেত্রে একই identity দেখতে পারো।

---

# 19. `is` Operator

Object identity compare করতে:

```python
is
```

Example:

```python
x = 10
y = x

print(x is y)
```

Result:

```text
True
```

`is` এবং `==` এক জিনিস নয়।

---

# 20. `==` বনাম `is`

### `==`

Value equality check করে।

```python
x == y
```

অর্থ:

> দুই object-এর value equal কি?

### `is`

Identity check করে।

```python
x is y
```

অর্থ:

> একই object কি?

---

# 21. Important Example

```python
a = [1, 2, 3]
b = [1, 2, 3]
```

এখন:

```python
print(a == b)
```

Output:

```text
True
```

কারণ values same।

কিন্তু:

```python
print(a is b)
```

সাধারণত:

```text
False
```

কারণ দুইটি আলাদা list object।

Mental model:

```text
a ───► [1,2,3]

b ───► [1,2,3]
```

দেখতে same হলেও object আলাদা।

---

# 22. Assignment কী?

```python
x = 10
```

এখানে `=` equality check করে না।

এটা assignment/reference binding operation।

ভুল:

```python
x = 10
```

মানে:

> x কি 10-এর সমান?

না।

বরং:

> name `x`-কে object `10`-এর সাথে bind করো।

---

# 23. `==` Equality

```python
x == 10
```

মানে:

> x-এর value 10-এর equal কি?

Example:

```python
x = 10

print(x == 10)
```

Output:

```text
True
```

---

# 24. Variable Reassignment

```python
x = 10
```

তারপর:

```python
x = 20
```

এখন:

```text
Before:

x ───► 10


After:

x ───► 20
```

`x` এখন নতুন object-এর দিকে refer করছে।

---

# 25. তাহলে পুরোনো object-এর কী হয়?

যদি অন্য কোনো reference না থাকে, Python-এর memory management system সেই object-কে পরে reclaim করতে পারে।

এখানে **garbage collection/reference counting** concepts আছে।

এগুলো এখন deeply নয়; M01-এর advanced section-এ memory management নিয়ে আলোচনা করব।

---

# 26. Dynamic Typing

Python dynamically typed।

Example:

```python
x = 10
```

এখন:

```python
print(type(x))
```

```text
<class 'int'>
```

তারপর:

```python
x = "Hello"
```

এখন:

```python
print(type(x))
```

```text
<class 'str'>
```

একই name অন্য ধরনের object-এর দিকে refer করতে পারে।

---

# 27. Dynamic Typing-এর Mental Model

```text
x ───► int object
```

তারপর:

```text
x ───► string object
```

তারপর:

```text
x ───► list object
```

Python-এর variable-এর fixed C-style type declaration প্রয়োজন হয় না।

---

# 28. Python Strongly Typed

Dynamic typing মানেই weak typing নয়।

Example:

```python
x = "10"
y = 20

print(x + y)
```

এখানে error হবে।

কারণ Python string `"10"` এবং integer `20`-কে automatically arbitrary way-তে concatenate করে না।

Correct:

```python
x = "10"
y = 20

print(int(x) + y)
```

Output:

```text
30
```

---

# 29. Type Conversion

Common conversions:

```python
int()
float()
str()
bool()
list()
tuple()
set()
dict()
```

Example:

```python
x = "100"

number = int(x)

print(number)
print(type(number))
```

Output:

```text
100
<class 'int'>
```

---

# 30. Mutable বনাম Immutable

এটা Python-এর অত্যন্ত গুরুত্বপূর্ণ concept।

## Immutable

Object তৈরি হওয়ার পর object-এর value পরিবর্তন করা যায় না।

Examples:

```text
int
float
bool
str
tuple
frozenset
```

## Mutable

Object-এর content পরিবর্তন করা যায়।

Examples:

```text
list
dict
set
```

---

# 31. String Immutable

```python
name = "Atiar"
```

তুমি করতে পারবে না:

```python
name[0] = "X"
```

এতে error হবে।

কারণ string immutable।

তবে:

```python
name = "Xtiar"
```

এখানে নতুন string object তৈরি/bind হতে পারে।

---

# 32. List Mutable

```python
numbers = [1, 2, 3]
```

এখন:

```python
numbers[0] = 100
```

valid।

Result:

```text
[100, 2, 3]
```

কারণ list mutable।

---

# 33. Mutable Object Reference Problem

এটা খুব ভালোভাবে বুঝো:

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

কেন?

কারণ:

```text
a ─────────┐
           ▼
        [1,2,3]
           ▲
           │
b ─────────┘
```

`a` এবং `b` একই list object-এর দিকে refer করছে।

`b.append(4)` করলে সেই একই object পরিবর্তিত হয়েছে।

---

# 34. Copy

আলাদা list চাইলে:

```python
a = [1, 2, 3]
b = a.copy()

b.append(4)

print(a)
print(b)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

Mental model:

```text
a ───► [1,2,3]

b ───► [1,2,3]
```

দুইটি আলাদা object।

Deep vs shallow copy আমরা Collections lesson-এ বিস্তারিত করব।

---

# 35. Variable Naming Rules

Valid:

```python
name = "Atiar"
age = 25
user_name = "Atiar"
_private = 10
name2 = "Test"
```

Invalid:

```python
2name = "Atiar"
```

কারণ variable name number দিয়ে শুরু করা যায় না।

Invalid:

```python
user-name = "Atiar"
```

কারণ `-` valid identifier character নয়।

---

# 36. Python Case Sensitive

```python
name = "Atiar"
Name = "Rahman"
NAME = "Python"
```

এগুলো তিনটি আলাদা name।

```python
print(name)
print(Name)
print(NAME)
```

---

# 37. Keywords

Python-এর কিছু reserved keywords আছে।

যেমন:

```text
if
else
elif
for
while
def
class
return
import
from
try
except
True
False
None
and
or
not
```

তুমি:

```python
class = 10
```

লিখতে পারবে না।

---

# 38. Keyword Check

Python থেকে:

```python
import keyword

print(keyword.kwlist)
```

এতে Python-এর keyword list দেখতে পারো।

---

# 39. Naming Convention

Python-এ সাধারণ convention:

### Variable

```python
user_name = "Atiar"
```

snake_case।

### Function

```python
def calculate_total():
    ...
```

### Class

```python
class UserProfile:
    ...
```

PascalCase/CapWords convention।

### Constant

```python
MAX_RETRIES = 3
```

UPPER_CASE।

---

# 40. Multiple Assignment

Python-এর সুন্দর feature।

```python
x = 10
y = 20
z = 30
```

এর পরিবর্তে:

```python
x, y, z = 10, 20, 30
```

---

# 41. Same Value

```python
x = y = z = 0
```

Conceptually:

```text
x ─┐
y ─┼──► 0
z ─┘
```

Immutable object হওয়ায় এখানে সমস্যা নেই।

---

# 42. Swapping Variables

অন্যান্য language-এ temporary variable লাগতে পারে:

```text
temp = x
x = y
y = temp
```

Python:

```python
x, y = y, x
```

Example:

```python
x = 10
y = 20

x, y = y, x

print(x)
print(y)
```

Output:

```text
20
10
```

---

# 43. Unpacking

ধরো:

```python
numbers = [10, 20, 30]
```

তুমি:

```python
a, b, c = numbers
```

এখন:

```text
a = 10
b = 20
c = 30
```

এটাই unpacking।

---

# 44. Extended Unpacking

```python
numbers = [1, 2, 3, 4, 5]

first, *middle, last = numbers
```

তাহলে:

```text
first = 1
middle = [2,3,4]
last = 5
```

এটা পরে functions এবং data processing-এ কাজে লাগবে।

---

# 45. `_` Variable

Python-এ `_` বিভিন্ন context-এ ব্যবহৃত হয়।

যেমন:

```python
for _ in range(5):
    print("Hello")
```

এখানে `_` দিয়ে বোঝানো হচ্ছে loop variable-এর value আমাদের দরকার নেই।

আর interactive Python shell-এ `_` previous result-এর জন্যও ব্যবহৃত হতে পারে।

Context অনুযায়ী meaning বদলায়।

---

# 46. Constants

Python-এ C++/Java-এর মতো strict constant keyword নেই।

Convention:

```python
PI = 3.14159
MAX_USERS = 100
API_VERSION = "v1"
```

Capital letters ব্যবহার করে বোঝানো হয়:

> এই value পরিবর্তন করা উচিত নয়।

কিন্তু technically:

```python
MAX_USERS = 200
```

করতে Python বাধা দেবে না।

---

# 47. Type Hints

Modern Python-এ:

```python
age: int = 25
```

আর:

```python
name: str = "Atiar"
```

Function:

```python
def add(a: int, b: int) -> int:
    return a + b
```

এগুলো code readability, IDE, static analysis-এর জন্য useful।

Python runtime সাধারণ assignment-এর মতোই কাজ করে; annotation নিজে automatic runtime type enforcement দেয় না।

---

# 48. `type()` বনাম Type Hint

```python
age: int = 25
```

এটা annotation।

Runtime type দেখতে:

```python
type(age)
```

দুটো আলাদা concept।

---

# 49. `id()` + `type()` Experiment

এই code নিজে run করো:

```python
x = 100

print("Value:", x)
print("Type:", type(x))
print("ID:", id(x))
```

তারপর:

```python
x = "Hello"

print("Value:", x)
print("Type:", type(x))
print("ID:", id(x))
```

খেয়াল করো:

```text
name একই
type পরিবর্তন
object reference পরিবর্তিত
```

---

# 50. Important Experiment — Mutable

এইটা অবশ্যই run করবে:

```python
a = [1, 2, 3]
b = a

print(a)
print(b)

print(a is b)

b.append(4)

print(a)
print(b)
```

Expected:

```text
[1, 2, 3]
[1, 2, 3]
True
[1, 2, 3, 4]
[1, 2, 3, 4]
```

এটা Python object model বোঝার জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 51. Another Experiment — Separate Objects

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

Expected:

```text
True
False
```

এখানে তুমি:

```text
Equality
vs
Identity
```

নিজে observe করবে।

---

# 52. `None`

Python-এ special object:

```python
None
```

ব্যবহার হয় "no value"/absence of a value বোঝাতে।

Example:

```python
result = None
```

Check:

```python
print(result is None)
```

Best practice:

```python
if result is None:
    ...
```

এখানে `is None` ব্যবহার করাই standard।

---

# 53. Boolean Object

```python
is_logged_in = True
```

অথবা:

```python
is_admin = False
```

Boolean হলো Python-এর built-in type:

```python
type(True)
```

Result:

```text
<class 'bool'>
```

---

# 54. Python Object Model — Final Mental Model

এখন সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                 Python Program
                       │
                       ▼
                Names / References
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
          x            y            z
          │            │            │
          ▼            ▼            ▼
      ┌────────┐   ┌────────┐   ┌────────┐
      │ Object │   │ Object │   │ Object │
      │ int    │   │ str    │   │ list   │
      │ 10     │   │ Hello  │   │ [...]  │
      └────────┘   └────────┘   └────────┘
          │            │            │
          ▼            ▼            ▼
        Type         Type         Type
```

আর:

```text
Name
 ↓
Reference
 ↓
Object
 ↓
Type + Value + Identity
```

এটাই আজকের সবচেয়ে important mental model।

---

# 55. কেন এই Concept AI-এর জন্য গুরুত্বপূর্ণ?

তুমি পরে লিখবে:

```python
model = MyModel()
```

এখানে:

```text
model
  ↓
reference
  ↓
Model object
```

তারপর:

```python
model.to("cuda")
```

বা:

```python
model.train()
```

তখন object/reference concept বুঝতে পারলে code অনেক সহজে বুঝবে।

আর:

```python
tokens = tokenizer(text)
```

এখানেও:

```text
tokens
 ↓
object
```

একই Python object model কাজ করছে।

---

# 🧪 M01.02 Practice Set

এখন **নিজে code লিখবে**।

## Level 1 — Basic

### 1

তিনটি variable তৈরি করো:

```text
name
age
country
```

এবং তাদের value print করো।

### 2

একটি variable-এর `type()` print করো।

### 3

একটি variable-এর `id()` print করো।

### 4

একটি integer → string → float-এ reassign করো।

### 5

দুইটি variable swap করো।

---

# Level 2 — Object Model

### 6

```python
a = 10
b = a
```

Check:

```text
a == b
a is b
id(a)
id(b)
```

### 7

```python
a = [1,2,3]
b = a
```

`b` পরিবর্তন করে দেখো `a` কী হয়।

### 8

```python
a = [1,2,3]
b = [1,2,3]
```

Check:

```text
a == b
a is b
```

### 9

String-এর character পরিবর্তন করার চেষ্টা করো।

### 10

List-এর element পরিবর্তন করো।

---

# Level 3 — Unpacking

### 11

```python
numbers = [10, 20, 30]
```

এগুলোকে:

```text
a
b
c
```

তে unpack করো।

### 12

```python
numbers = [1,2,3,4,5,6]
```

এভাবে unpack করো:

```text
first
middle
last
```

যাতে:

```text
first = 1
middle = [2,3,4,5]
last = 6
```

---

# Level 4 — Debugging

এই code-এ কী সমস্যা আছে বের করো:

```python
2name = "Atiar"
```

আর:

```python
class = 10
```

আর:

```python
if True
    print("Hello")
```

প্রতিটির error-এর কারণ explain করো।

---

# 🧠 M01.02 Theory Test

নিজে answer করার চেষ্টা করো:

1. Syntax কী?
2. Statement কী?
3. Expression কী?
4. Statement এবং expression-এর পার্থক্য কী?
5. Python indentation কেন গুরুত্বপূর্ণ?
6. `:` কোথায় ব্যবহার হয়?
7. Variable কী?
8. Python-এ variable-কে reference/name বলা হয় কেন?
9. Object কী?
10. Object-এর type কী?
11. Object identity কী?
12. `type()` কী করে?
13. `id()` কী করে?
14. `=` এবং `==`-এর পার্থক্য কী?
15. `==` এবং `is`-এর পার্থক্য কী?
16. Dynamic typing কী?
17. Dynamic typing এবং weak typing কি একই?
18. Mutable object কী?
19. Immutable object কী?
20. List mutable কেন?
21. String immutable বলতে কী বোঝ?
22. `a = b` করলে কী হয়?
23. `a = [1,2]` এবং `b = [1,2]` হলে `a is b` কেন false?
24. Unpacking কী?
25. Multiple assignment কী?
26. Python-এ constant কীভাবে convention করা হয়?
27. Type hint কী?
28. `None` কী?
29. Python case-sensitive বলতে কী বোঝ?
30. Python object model-এর basic flow কী?

---

# 🔥 M01.02 Challenge

এই program নিজে লেখো:

```text
Student Information System
```

Requirements:

```text
Name
Age
Department
CGPA
Skills
```

তারপর program যেন print করে:

```text
Student Information
-------------------
Name: Atiar
Age: 25
Department: CSE
CGPA: 3.30
Skills: Python, Django, PyTorch
```

তারপর:

```text
1. প্রতিটি variable-এর type দেখাবে
2. প্রতিটি variable-এর id দেখাবে
3. Skills-এর একটি নতুন list তৈরি করবে
4. Original list পরিবর্তন করলে copy পরিবর্তিত হয় কি না পরীক্ষা করবে
5. Name variable অন্য type-এ reassign করবে
```

---

# ✅ M01.02 Completion Checklist

M01.02 complete করার আগে নিশ্চিত হও:

```text
☐ Python syntax
☐ Statement
☐ Expression
☐ Indentation
☐ Comments
☐ Variables
☐ Objects
☐ References
☐ Assignment
☐ type()
☐ id()
☐ ==
☐ is
☐ Dynamic typing
☐ Strong typing
☐ Mutable
☐ Immutable
☐ Variable naming
☐ Keywords
☐ Multiple assignment
☐ Swapping
☐ Unpacking
☐ Constants
☐ Type hints
☐ None
☐ Object model
```

**এগুলোর কোনোটি বাদ দিও না।**

পরের lesson হবে:

# 🟢 M01.03 — Python Data Types: Complete Deep Dive

সেখানে আমরা `int`, `float`, `complex`, `bool`, `None`, `str`, `list`, `tuple`, `set`, `frozenset`, `dict`, `bytes`, `bytearray`, `range`—এগুলোর **creation → memory/object behavior → indexing → operations → methods → conversion → mutable/immutable → practical use → exercises** একে একে করব।



# 🟢 M01.03 — Python Data Types: Complete Deep Dive

আজ আমরা Python-এর **Data Types** একদম foundation থেকে deep level পর্যন্ত শিখব।
এই lesson ভালোভাবে বুঝলে পরবর্তী **Functions, OOP, Data Structures, NLP এবং AI/LLM programming** অনেক সহজ হবে।

---

# 1. Data Type কী?

Data type বলে দেয় একটি object কী ধরনের data represent করছে এবং তার সাথে কী ধরনের operation করা যায়।

উদাহরণ:

```python
age = 25
name = "Atiar"
price = 99.50
is_active = True
```

এখানে:

```text
25       → int
"Atiar"  → str
99.50    → float
True     → bool
```

Type দেখার জন্য:

```python
print(type(age))
print(type(name))
print(type(price))
print(type(is_active))
```

Output:

```text
<class 'int'>
<class 'str'>
<class 'float'>
<class 'bool'>
```

---

# 2. Python-এর প্রধান Built-in Data Types

Python-এর গুরুত্বপূর্ণ built-in types:

```text
Python Data Types
│
├── Numeric
│   ├── int
│   ├── float
│   └── complex
│
├── Boolean
│   └── bool
│
├── Text
│   └── str
│
├── Sequence
│   ├── list
│   ├── tuple
│   ├── range
│   └── str
│
├── Set
│   ├── set
│   └── frozenset
│
├── Mapping
│   └── dict
│
├── Binary
│   ├── bytes
│   ├── bytearray
│   └── memoryview
│
└── Special
    └── NoneType
```

---

# 3. `int` — Integer

পূর্ণ সংখ্যা হলো `int`.

```python
age = 25
quantity = 100
negative = -50
zero = 0
```

Check:

```python
print(type(25))
```

Output:

```text
<class 'int'>
```

### Arithmetic

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

Output:

```text
13
7
30
3.3333333333333335
3
1
1000
```

### Important operators

| Operator | Meaning        |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `//`     | Floor division |
| `%`      | Modulus        |
| `**`     | Power          |

---

# 4. Python Integer-এর বিশেষ বৈশিষ্ট্য

অনেক language-এ integer-এর size সীমিত।

Python-এ সাধারণভাবে integer arbitrary precision support করে।

```python
x = 999999999999999999999999999999999999999999

print(x)
```

এটা valid।

তবে বাস্তবে memory সীমাবদ্ধতা থাকবে।

---

# 5. `float`

Decimal number হলো `float`.

```python
price = 99.99
temperature = 36.5
rating = 4.8
```

```python
print(type(price))
```

Output:

```text
<class 'float'>
```

---

## Float calculation-এর সমস্যা

এটা খুব গুরুত্বপূর্ণ।

```python
print(0.1 + 0.2)
```

Output হতে পারে:

```text
0.30000000000000004
```

কেন?

কারণ computer সাধারণত decimal fraction-কে binary floating-point representation-এ store করে।

তাই financial application-এ সরাসরি float ব্যবহার করা সবসময় ভালো নয়।

প্রয়োজনে:

```python
from decimal import Decimal

x = Decimal("0.1")
y = Decimal("0.2")

print(x + y)
```

Output:

```text
0.3
```

---

# 6. `complex`

Complex number:

```python
z = 3 + 4j

print(type(z))
```

Output:

```text
<class 'complex'>
```

এখানে:

```text
3 → real part
4j → imaginary part
```

Access:

```python
print(z.real)
print(z.imag)
```

Output:

```text
3.0
4.0
```

Complex number সাধারণ web development-এ খুব বেশি লাগবে না, কিন্তু mathematics, signal processing, scientific computing ইত্যাদিতে গুরুত্বপূর্ণ।

---

# 7. `bool` — Boolean

Boolean-এর দুইটি value:

```python
True
False
```

```python
is_logged_in = True
is_admin = False
```

```python
print(type(True))
```

Output:

```text
<class 'bool'>
```

---

## Boolean আসলে কী?

Python-এ:

```python
bool
```

হলো `int`-এর subclass।

```python
print(isinstance(True, int))
```

Output:

```text
True
```

কারণ:

```text
True  → 1
False → 0
```

উদাহরণ:

```python
print(True + True)
print(True + False)
```

Output:

```text
2
1
```

তবে সাধারণ programming-এ `True` এবং `False`-কে boolean হিসেবেই ব্যবহার করবে।

---

# 8. `None`

`None` মানে সাধারণত **কোনো value নেই**।

```python
result = None
```

Type:

```python
print(type(result))
```

Output:

```text
<class 'NoneType'>
```

---

## `None` বনাম `0`

এক জিনিস নয়।

```python
x = None
y = 0

print(x == y)
```

Output:

```text
False
```

---

## `None` check

সঠিক:

```python
if result is None:
    print("No result")
```

Avoid:

```python
if result == None:
    ...
```

Best practice:

```python
is None
is not None
```

---

# 9. `str` — String

Text data হলো `str`.

```python
name = "Atiar"
message = 'Hello World'
```

Triple quotes:

```python
text = """
This is
multiple lines
"""
```

---

# 10. String Indexing

```python
name = "Python"
```

Index:

```text
 P  y  t  h  o  n
 0  1  2  3  4  5
```

```python
print(name[0])
print(name[2])
print(name[5])
```

Output:

```text
P
t
n
```

Negative indexing:

```text
 P  y  t  h  o  n
-6 -5 -4 -3 -2 -1
```

```python
print(name[-1])
```

Output:

```text
n
```

---

# 11. String Slicing

```python
name = "Python"
```

```python
print(name[0:3])
```

Output:

```text
Pyt
```

General syntax:

```python
string[start:stop:step]
```

`stop` included হয় না।

---

### Examples

```python
text = "Python Programming"

print(text[:6])
print(text[7:])
print(text[::2])
print(text[::-1])
```

শেষেরটি string reverse করে।

---

# 12. String Immutable

এটা অত্যন্ত গুরুত্বপূর্ণ।

```python
name = "Python"

name[0] = "J"
```

Error হবে:

```text
TypeError
```

কারণ `str` immutable।

পরিবর্তে:

```python
name = "J" + name[1:]

print(name)
```

Output:

```text
Jython
```

এখানে পুরনো string modify হয়নি। নতুন string তৈরি হয়েছে।

---

# 13. গুরুত্বপূর্ণ String Methods

```python
text = "hello python"
```

### Upper

```python
print(text.upper())
```

```text
HELLO PYTHON
```

### Lower

```python
print(text.lower())
```

### Capitalize

```python
print(text.capitalize())
```

### Title

```python
print(text.title())
```

### Replace

```python
print(text.replace("python", "world"))
```

### Split

```python
text = "Python Django React"

words = text.split()

print(words)
```

Output:

```python
['Python', 'Django', 'React']
```

### Join

```python
words = ["Python", "Django", "React"]

result = " ".join(words)

print(result)
```

Output:

```text
Python Django React
```

---

# 14. `list`

List হলো ordered, mutable collection।

```python
numbers = [10, 20, 30, 40]
```

Type:

```python
print(type(numbers))
```

---

## List বিভিন্ন ধরনের data রাখতে পারে

```python
data = [
    10,
    "Python",
    3.14,
    True,
    None
]
```

এমনকি nested list:

```python
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]
```

---

# 15. List Indexing

```python
numbers = [10, 20, 30, 40]
```

```python
print(numbers[0])
print(numbers[-1])
```

Output:

```text
10
40
```

---

# 16. List Mutable

```python
numbers = [10, 20, 30]

numbers[0] = 100

print(numbers)
```

Output:

```python
[100, 20, 30]
```

অর্থাৎ list modify করা যায়।

---

# 17. List Methods

### append()

শেষে item যোগ করে।

```python
numbers = [1, 2, 3]

numbers.append(4)

print(numbers)
```

```text
[1, 2, 3, 4]
```

### insert()

```python
numbers.insert(1, 100)
```

### remove()

```python
numbers.remove(100)
```

### pop()

```python
last = numbers.pop()
```

### sort()

```python
numbers.sort()
```

### reverse()

```python
numbers.reverse()
```

### extend()

```python
numbers.extend([5, 6, 7])
```

---

# 18. List-এর গুরুত্বপূর্ণ বিষয়: Reference

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

কারণ:

```text
a ─────┐
       ↓
   [1,2,3]
       ↑
       │
b ─────┘
```

দুটো name একই object-কে reference করছে।

---

# 19. `tuple`

Tuple হলো ordered এবং immutable collection।

```python
coordinates = (10, 20)
```

```python
print(type(coordinates))
```

---

## Tuple indexing

```python
print(coordinates[0])
```

---

## Tuple immutable

```python
coordinates[0] = 100
```

Error:

```text
TypeError
```

---

# 20. Tuple কেন ব্যবহার করব?

যখন data change হওয়ার কথা নয়।

উদাহরণ:

```python
RGB = (255, 255, 255)
```

বা:

```python
location = (23.8103, 90.4125)
```

---

# 21. Tuple Packing

```python
data = 10, 20, 30
```

Python এটাকে tuple হিসেবে নেয়।

```python
print(type(data))
```

Output:

```text
<class 'tuple'>
```

---

# 22. Tuple Unpacking

```python
x, y, z = (10, 20, 30)

print(x)
print(y)
print(z)
```

---

# 23. Single-element Tuple

এখানে beginners প্রায়ই ভুল করে।

এটা tuple নয়:

```python
x = (10)
```

এটা:

```python
int
```

Tuple:

```python
x = (10,)
```

---

# 24. `set`

Set হলো unordered collection of unique elements।

```python
numbers = {1, 2, 3, 4}
```

Duplicate automatically remove হয়:

```python
numbers = {1, 2, 2, 3, 3, 3}

print(numbers)
```

Output:

```text
{1, 2, 3}
```

---

# 25. Set কেন ব্যবহার করব?

যখন unique values দরকার।

উদাহরণ:

```python
tags = ["python", "django", "python", "react"]

unique_tags = set(tags)

print(unique_tags)
```

---

# 26. Set-এর Index নেই

এটা করা যায় না:

```python
numbers = {1, 2, 3}

print(numbers[0])
```

কারণ set indexed collection নয়।

---

# 27. Set Operations

ধরি:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
```

### Union

```python
print(A | B)
```

Output:

```text
{1, 2, 3, 4, 5, 6}
```

### Intersection

```python
print(A & B)
```

```text
{3, 4}
```

### Difference

```python
print(A - B)
```

```text
{1, 2}
```

### Symmetric Difference

```python
print(A ^ B)
```

```text
{1, 2, 5, 6}
```

---

# 28. `frozenset`

`frozenset` হলো immutable set।

```python
numbers = frozenset([1, 2, 3])
```

তুমি এর element change করতে পারবে না।

```python
print(type(numbers))
```

Output:

```text
<class 'frozenset'>
```

---

# 29. `dict`

Dictionary হলো **key-value mapping**।

```python
student = {
    "name": "Atiar",
    "age": 25,
    "department": "CSE"
}
```

Concept:

```text
key          value
 │             │
 ↓             ↓
"name"     → "Atiar"
"age"      → 25
"department"→ "CSE"
```

---

# 30. Dictionary Access

```python
print(student["name"])
print(student["age"])
```

Output:

```text
Atiar
25
```

---

# 31. Dictionary Modify

```python
student["age"] = 26
```

New key:

```python
student["country"] = "Bangladesh"
```

---

# 32. `get()`

Direct access:

```python
student["email"]
```

key না থাকলে `KeyError` হতে পারে।

Better:

```python
print(student.get("email"))
```

Output:

```text
None
```

Default:

```python
print(student.get("email", "Not provided"))
```

Output:

```text
Not provided
```

---

# 33. Dictionary Methods

```python
student.keys()
student.values()
student.items()
```

Example:

```python
for key, value in student.items():
    print(key, value)
```

---

# 34. Dictionary Keys-এর নিয়ম

সব object key হিসেবে ব্যবহার করা যায় না।

Key সাধারণত hashable হতে হয়।

Valid:

```python
data = {
    "name": "Atiar",
    1: "one",
    (1, 2): "coordinate"
}
```

List key:

```python
{
    [1, 2]: "test"
}
```

এটা invalid।

কারণ list mutable এবং hashable নয়।

---

# 35. `range`

`range` sequence of numbers তৈরি করতে ব্যবহৃত হয়।

```python
r = range(5)

print(r)
```

Output:

```text
range(0, 5)
```

Values:

```python
print(list(range(5)))
```

Output:

```text
[0, 1, 2, 3, 4]
```

---

## `range(start, stop, step)`

```python
range(1, 10, 2)
```

মানে:

```text
1, 3, 5, 7, 9
```

---

# 36. `bytes`

Binary immutable data।

```python
data = b"Hello"
```

```python
print(type(data))
```

Output:

```text
<class 'bytes'>
```

এটা networking, file processing, APIs, images ইত্যাদিতে গুরুত্বপূর্ণ।

---

# 37. `bytearray`

`bytearray` হলো mutable binary data।

```python
data = bytearray(b"Hello")

data[0] = 72

print(data)
```

---

# 38. `bytes` বনাম `bytearray`

| Type        | Mutable |
| ----------- | ------- |
| `bytes`     | ❌       |
| `bytearray` | ✅       |

---

# 39. Encoding ও Decoding

Text:

```python
text = "Hello"
```

Encode:

```python
data = text.encode("utf-8")

print(data)
```

Output:

```text
b'Hello'
```

Decode:

```python
text2 = data.decode("utf-8")

print(text2)
```

Output:

```text
Hello
```

AI/NLP এবং web application-এ encoding বোঝা খুব গুরুত্বপূর্ণ।

---

# 40. Type Conversion

এক type থেকে অন্য type-এ convert করা যায়।

### String → Integer

```python
x = "100"

x = int(x)

print(x)
print(type(x))
```

---

### Integer → String

```python
x = 100

x = str(x)
```

---

### String → Float

```python
price = float("99.50")
```

---

### List → Tuple

```python
numbers = [1, 2, 3]

result = tuple(numbers)
```

---

### Tuple → List

```python
data = (1, 2, 3)

result = list(data)
```

---

### List → Set

```python
numbers = [1, 2, 2, 3]

unique = set(numbers)

print(unique)
```

---

# 41. `bool()` Conversion

Python truthiness বোঝার জন্য খুব গুরুত্বপূর্ণ।

```python
print(bool(1))
print(bool(0))
```

Output:

```text
True
False
```

String:

```python
print(bool("hello"))
print(bool(""))
```

Output:

```text
True
False
```

List:

```python
print(bool([1, 2]))
print(bool([]))
```

Output:

```text
True
False
```

---

# 42. Falsey Values

Python-এ গুরুত্বপূর্ণ falsey values:

```python
False
None
0
0.0
0j
""
[]
()
{}
set()
```

অন্যদিকে সাধারণত non-empty object truthy।

---

# 43. Mutable বনাম Immutable

এটা M01-এর সবচেয়ে গুরুত্বপূর্ণ concepts-এর একটি।

## Immutable

যেগুলো তৈরি হওয়ার পরে পরিবর্তন করা যায় না।

```text
int
float
complex
bool
str
tuple
frozenset
bytes
```

---

## Mutable

যেগুলো modify করা যায়।

```text
list
dict
set
bytearray
```

---

# 44. Example — Immutable

```python
x = 10

print(id(x))

x = 20

print(id(x))
```

`x` এখন অন্য integer object-এর দিকে reference করছে।

---

# 45. Example — Mutable

```python
numbers = [1, 2, 3]

old_id = id(numbers)

numbers.append(4)

new_id = id(numbers)

print(old_id)
print(new_id)
```

সাধারণভাবে একই list object modify হয়েছে, তাই identity একই থাকে।

---

# 46. Shallow Copy ধারণা

```python
a = [1, 2, 3]

b = a.copy()

b.append(4)

print(a)
print(b)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

এখানে দুটি আলাদা list।

---

# 47. Nested List এবং Shallow Copy

এখানে বিষয়টা একটু advanced।

```python
a = [[1, 2], [3, 4]]

b = a.copy()

b[0].append(100)

print(a)
print(b)
```

Output:

```text
[[1, 2, 100], [3, 4]]
[[1, 2, 100], [3, 4]]
```

কেন?

কারণ outer list copy হলেও inner lists একই objects।

---

# 48. Deep Copy

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.deepcopy(a)

b[0].append(100)

print(a)
print(b)
```

Output:

```text
[[1, 2], [3, 4]]
[[1, 2, 100], [3, 4]]
```

---

# 49. Data Structure নির্বাচন

কোন data type কখন ব্যবহার করবে?

| Requirement                | Best choice |
| -------------------------- | ----------- |
| Integer                    | `int`       |
| Decimal                    | `float`     |
| Accurate money calculation | `Decimal`   |
| Text                       | `str`       |
| Changeable ordered data    | `list`      |
| Fixed ordered data         | `tuple`     |
| Unique values              | `set`       |
| Immutable unique values    | `frozenset` |
| Key-value data             | `dict`      |
| Number sequence            | `range`     |
| Binary immutable           | `bytes`     |
| Binary mutable             | `bytearray` |
| No value                   | `None`      |

---

# 50. AI Project-এর সাথে Connection

তুমি যেহেতু পরে AI writing/humanization project বানাতে চাচ্ছ, data types তোমার প্রতিদিন ব্যবহার হবে।

উদাহরণ:

```python
text = "Artificial intelligence is changing the world."

tokens = ["Artificial", "intelligence", "is", "changing", "the", "world"]

scores = [0.91, 0.87, 0.75, 0.82, 0.95, 0.88]

result = {
    "text": text,
    "tokens": tokens,
    "scores": scores,
    "is_ai_generated": True
}
```

এখানে:

```text
text              → str
tokens            → list
scores            → list
result            → dict
is_ai_generated   → bool
```

আর sentence-level analysis:

```python
sentences = [
    {
        "text": "AI is changing the world.",
        "score": 0.91,
        "label": "AI"
    },
    {
        "text": "People use AI every day.",
        "score": 0.42,
        "label": "Human"
    }
]
```

এ ধরনের structure তোমার future AI backend-এ অনেক ব্যবহার হবে।

---

# 51. খুব গুরুত্বপূর্ণ Mental Model

এখন পর্যন্ত:

```text
Python Variable
       ↓
    Reference
       ↓
     Object
       ↓
 ┌───────────────┐
 │ Type          │
 │ Value         │
 │ Identity      │
 └───────────────┘
```

উদাহরণ:

```python
x = [1, 2, 3]
```

এখানে:

```text
x
│
│ reference
↓
[1, 2, 3]
│
├── type = list
├── value = [1, 2, 3]
└── identity = unique object identity
```

---

# 52. `type()` বনাম `isinstance()`

### type()

```python
x = 10

print(type(x))
```

### isinstance()

```python
print(isinstance(x, int))
```

Output:

```text
True
```

`isinstance()` inheritance সম্পর্কেও কাজ করে।

```python
print(isinstance(True, int))
```

```text
True
```

---

# 53. `type()` দিয়ে comparison

```python
x = True

print(type(x) == bool)
```

Output:

```text
True
```

কিন্তু সাধারণ type-checking-এর ক্ষেত্রে:

```python
isinstance(x, bool)
```

অনেক ক্ষেত্রে বেশি flexible।

---

# 54. Important Interview Question

### Q: List এবং Tuple-এর পার্থক্য কী?

**List:**

```python
[1, 2, 3]
```

* Mutable
* Generally used for changeable collections

**Tuple:**

```python
(1, 2, 3)
```

* Immutable
* Generally used for fixed collections
* Can be hashable when its elements are hashable

---

# 55. Important Interview Question

### Q: Set কেন duplicate রাখে না?

Set internally hash-based structure ব্যবহার করে এবং elements unique রাখে।

```python
x = {1, 1, 2, 2, 3}

print(x)
```

```text
{1, 2, 3}
```

---

# 56. Important Interview Question

### Q: Dictionary এবং Set-এর মধ্যে পার্থক্য?

Dictionary:

```python
{
    "name": "Atiar"
}
```

এখানে:

```text
key → value
```

Set:

```python
{"Python", "Django", "React"}
```

এখানে শুধু unique values থাকে।

---

# 57. Important Interview Question

### Q: `str` immutable কেন গুরুত্বপূর্ণ?

কারণ:

```python
text = "hello"
```

তুমি `text`-এর character সরাসরি পরিবর্তন করতে পারবে না।

এটা string operations-এর predictable behavior এবং নিরাপদ sharing-এর মতো বৈশিষ্ট্যে সাহায্য করে।

---

# 58. Practice — Level 1

নিজে solve করো।

### Q1

```python
x = 100
```

এর type কী?

---

### Q2

```python
x = "100"
```

এটাকে integer বানাও।

---

### Q3

এই list থেকে duplicate remove করো:

```python
numbers = [1, 2, 2, 3, 4, 4, 5]
```

---

### Q4

এই tuple থেকে values unpack করো:

```python
data = ("Atiar", 25, "CSE")
```

---

### Q5

Dictionary তৈরি করো:

```text
name
age
email
country
```

---

# 59. Practice — Level 2

### Q6

এই string reverse করো:

```python
text = "Artificial Intelligence"
```

---

### Q7

এই list থেকে সবচেয়ে বড় number বের করো:

```python
numbers = [10, 50, 20, 90, 30]
```

---

### Q8

দুটি set-এর common elements বের করো:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
```

---

### Q9

Dictionary থেকে safely email বের করো:

```python
user = {
    "name": "Atiar",
    "age": 25
}
```

---

### Q10

Check করো:

```python
value = None
```

value `None` কিনা।

---

# 60. Practice — Level 3

এই data structure তৈরি করো:

```python
students = [
    {
        "name": "Rahim",
        "age": 22,
        "skills": ["Python", "Django"]
    },
    {
        "name": "Karim",
        "age": 24,
        "skills": ["Python", "React"]
    }
]
```

তারপর:

1. প্রথম student's name print করো
2. দ্বিতীয় student's age print করো
3. প্রথম student's skills-এর প্রথম item print করো
4. দ্বিতীয় student's skills-এ `"Django"` add করো
5. পুরো structure print করো

---

# 61. 🔥 M01.03 Challenge

নিচের input:

```python
text = """
Python is powerful.
Python is easy to learn.
Python is widely used in AI.
Python is powerful.
"""
```

তোমার কাজ:

### Step 1

Text থেকে sentences বের করো।

### Step 2

Duplicate sentence remove করো।

### Step 3

প্রতিটি sentence-এর word list তৈরি করো।

Expected conceptual structure:

```python
[
    {
        "sentence": "...",
        "words": [...]
    },
    ...
]
```

### Step 4

প্রতিটি sentence-এর word count বের করো।

শেষে structure এমন ধরনের হবে:

```python
[
    {
        "sentence": "Python is powerful.",
        "words": ["Python", "is", "powerful"],
        "word_count": 3
    }
]
```

এই challenge-টি future **NLP text-processing pipeline**-এর foundation।

---

# 62. M01.03 Completion Checklist

এই lesson complete হয়েছে ধরে নেওয়ার আগে তুমি যেন explain করতে পারো:

### Numeric

* [ ] `int`
* [ ] `float`
* [ ] `complex`
* [ ] `Decimal` কেন দরকার

### Basic

* [ ] `bool`
* [ ] `None`
* [ ] `str`

### Collections

* [ ] `list`
* [ ] `tuple`
* [ ] `set`
* [ ] `frozenset`
* [ ] `dict`
* [ ] `range`

### Binary

* [ ] `bytes`
* [ ] `bytearray`
* [ ] encoding/decoding

### Concepts

* [ ] Mutable vs immutable
* [ ] Indexing
* [ ] Slicing
* [ ] Hashable ধারণা
* [ ] Type conversion
* [ ] Truthy/Falsy
* [ ] `type()`
* [ ] `isinstance()`
* [ ] Reference behavior
* [ ] Shallow copy
* [ ] Deep copy

### Practical

* [ ] List operations
* [ ] Dictionary operations
* [ ] Set operations
* [ ] String operations
* [ ] Nested data structures
* [ ] Text-processing structure তৈরি

---

## 🧠 M01.03-এর মূল কথা

সবকিছু একসাথে মনে রাখার জন্য এই map-টা মনে রাখো:

```text
                 PYTHON DATA
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
    SIMPLE        COLLECTION       BINARY
       │              │              │
 ┌─────┼─────┐    ┌───┼────┐      ┌──┴────┐
 int float bool   list tuple dict   bytes
 complex None    set  range          bytearray
       │
      str
```

এবং সবচেয়ে গুরুত্বপূর্ণ:

```text
Mutable:
list
dict
set
bytearray

Immutable:
int
float
complex
bool
str
tuple
frozenset
bytes
```

**M01.03 complete.**
পরবর্তী ধাপ হবে **🟢 M01.04 — Operators & Expressions**, যেখানে arithmetic, comparison, logical, bitwise, assignment, membership, identity, operator precedence এবং Python-এর expression evaluation গভীরভাবে শিখব।


---
# 🟢 M01.04 — Python Operators & Expressions

আজকের lesson-এ Python-এর **সব গুরুত্বপূর্ণ operators** এবং **expression evaluation** একদম foundation থেকে advanced level পর্যন্ত শিখব।

এটা খুব গুরুত্বপূর্ণ, কারণ পরের **if/else, loops, functions, data structures, algorithms, Django, NLP/AI code**—সব জায়গায় operators ব্যবহার করবে।

---

# 1. Operator কী?

Operator হলো এমন একটি symbol/keyword যা কোনো operation সম্পন্ন করে।

উদাহরণ:

```python
a = 10
b = 5

print(a + b)
```

এখানে:

```text
a → operand
+ → operator
b → operand
```

Result:

```text
15
```

---

# 2. Python Operators-এর সম্পূর্ণ Map

```text
Python Operators
│
├── 1. Arithmetic
│
├── 2. Comparison / Relational
│
├── 3. Logical
│
├── 4. Assignment
│
├── 5. Identity
│
├── 6. Membership
│
├── 7. Bitwise
│
└── 8. Conditional Expression
```

---

# 3. Arithmetic Operators

সংখ্যার mathematical operation-এর জন্য ব্যবহার হয়।

| Operator | কাজ            |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `//`     | Floor Division |
| `%`      | Modulus        |
| `**`     | Exponentiation |

---

## 3.1 Addition `+`

```python
a = 10
b = 5

print(a + b)
```

Output:

```text
15
```

String-এর ক্ষেত্রেও `+` কাজ করে।

```python
first = "Hello"
second = "World"

print(first + " " + second)
```

Output:

```text
Hello World
```

এটাকে **concatenation** বলে।

---

# 4. Subtraction `-`

```python
a = 10
b = 3

print(a - b)
```

Output:

```text
7
```

---

# 5. Multiplication `*`

```python
print(5 * 4)
```

Output:

```text
20
```

String-এর সাথেও:

```python
print("Hi " * 3)
```

Output:

```text
Hi Hi Hi
```

List-এর সাথেও:

```python
print([1, 2] * 3)
```

Output:

```text
[1, 2, 1, 2, 1, 2]
```

---

# 6. Division `/`

Python-এ `/` সাধারণত float result দেয়।

```python
print(10 / 2)
```

Output:

```text
5.0
```

এমনকি:

```python
print(5 / 2)
```

Output:

```text
2.5
```

---

# 7. Floor Division `//`

```python
print(10 // 3)
```

Output:

```text
3
```

এটা result-এর floor নেয়।

আর negative number-এর ক্ষেত্রে গুরুত্বপূর্ণ:

```python
print(-10 // 3)
```

Output:

```text
-4
```

কারণ floor মানে ছোট integer-এর দিকে যাওয়া:

```text
-3.333...
↓
-4
```

---

# 8. Modulus `%`

Remainder বের করতে ব্যবহার হয়।

```python
print(10 % 3)
```

Output:

```text
1
```

কারণ:

```text
10 = 3 × 3 + 1
```

---

## Practical Example

Even/odd:

```python
number = 10

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

# 9. Exponentiation `**`

Power calculation:

```python
print(2 ** 3)
```

Output:

```text
8
```

কারণ:

```text
2 × 2 × 2 = 8
```

---

# 10. Comparison Operators

Comparison operator দুইটি value compare করে এবং result দেয়:

```text
True
False
```

Operators:

| Operator | Meaning       |
| -------- | ------------- |
| `==`     | Equal         |
| `!=`     | Not equal     |
| `>`      | Greater than  |
| `<`      | Less than     |
| `>=`     | Greater/equal |
| `<=`     | Less/equal    |

---

## `==`

```python
a = 10
b = 10

print(a == b)
```

Output:

```text
True
```

---

## `!=`

```python
print(10 != 5)
```

Output:

```text
True
```

---

## `>`

```python
print(10 > 5)
```

```text
True
```

---

## `<`

```python
print(10 < 5)
```

```text
False
```

---

## `>=`

```python
print(10 >= 10)
```

```text
True
```

---

## `<=`

```python
print(5 <= 10)
```

```text
True
```

---

# 11. `==` বনাম `is`

এটা খুব গুরুত্বপূর্ণ।

### `==`

Value compare করে।

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
```

Output:

```text
True
```

কারণ value একই।

### `is`

Identity compare করে।

```python
print(a is b)
```

Output:

```text
False
```

কারণ object দুটি আলাদা।

---

# 12. Logical Operators

Python-এর logical operators:

```text
and
or
not
```

---

# 13. `and`

দুই condition True হলে result True।

```python
age = 25
has_id = True

print(age >= 18 and has_id)
```

Output:

```text
True
```

Truth table:

| A     | B     | A and B |
| ----- | ----- | ------- |
| True  | True  | True    |
| True  | False | False   |
| False | True  | False   |
| False | False | False   |

---

# 14. `or`

কমপক্ষে একটি True হলে result True।

```python
is_admin = False
is_staff = True

print(is_admin or is_staff)
```

Output:

```text
True
```

Truth table:

| A     | B     | A or B |
| ----- | ----- | ------ |
| True  | True  | True   |
| True  | False | True   |
| False | True  | True   |
| False | False | False  |

---

# 15. `not`

Boolean value উল্টে দেয়।

```python
is_logged_in = True

print(not is_logged_in)
```

Output:

```text
False
```

---

# 16. Logical Operators শুধু Boolean-এ কাজ করে না

এটা Python-এর খুব গুরুত্বপূর্ণ behavior।

```python
print(10 and 20)
```

Output:

```text
20
```

এখানে `and` সবসময় `True`/`False` return করে না।

আর:

```python
print(10 or 20)
```

Output:

```text
10
```

কারণ Python operands-এর actual value return করতে পারে।

---

# 17. Short-Circuit Evaluation

Python unnecessary expression evaluate করে না।

### `and`

```python
False and something
```

প্রথম operand False হলে দ্বিতীয়টি evaluate করার দরকার নেই।

উদাহরণ:

```python
x = False

result = x and print("Hello")
```

`Hello` print হবে না।

---

### `or`

```python
True or something
```

প্রথম operand True হলে দ্বিতীয়টি দরকার নেই।

```python
x = True

result = x or print("Hello")
```

এখানেও `Hello` print হবে না।

---

# 18. Practical Short-Circuit

```python
user = None

if user and user.is_active:
    print("Active")
```

প্রথম অংশ:

```python
user
```

Falsey হওয়ায় Python দ্বিতীয় অংশ evaluate করবে না।

এটা Django/backend programming-এ অনেক কাজে লাগে।

---

# 19. Assignment Operators

Basic assignment:

```python
x = 10
```

এছাড়া:

```text
+=
-=
*=
/=
//=
%=
**=
&=
|=
^=
>>=
<<=
```

---

# 20. `+=`

```python
x = 10

x += 5

print(x)
```

Output:

```text
15
```

Conceptually:

```python
x = x + 5
```

---

# 21. `-=`

```python
x = 10
x -= 3

print(x)
```

Result:

```text
7
```

---

# 22. `*=`

```python
x = 10
x *= 3
```

Result:

```text
30
```

---

# 23. `/=`

```python
x = 10
x /= 2

print(x)
```

Output:

```text
5.0
```

খেয়াল করো type `float` হয়ে গেছে।

---

# 24. `%=` এবং `//=`

```python
x = 10

x %= 3
print(x)
```

Result:

```text
1
```

আর:

```python
x = 10
x //= 3
```

Result:

```text
3
```

---

# 25. `**=`

```python
x = 2

x **= 3

print(x)
```

Output:

```text
8
```

---

# 26. Identity Operators

দুইটি identity operator:

```text
is
is not
```

---

## `is`

দুই reference একই object-এর দিকে point করছে কিনা check করে।

```python
a = [1, 2]
b = a

print(a is b)
```

Output:

```text
True
```

---

## `is not`

```python
a = [1, 2]
b = [1, 2]

print(a is not b)
```

Output:

```text
True
```

---

# 27. `None` Check

Best practice:

```python
result = None

if result is None:
    print("No result")
```

আর:

```python
if result is not None:
    print(result)
```

---

# 28. Membership Operators

দুইটি:

```text
in
not in
```

কোনো collection-এর মধ্যে value আছে কিনা check করে।

---

## String

```python
text = "Python Programming"

print("Python" in text)
```

Output:

```text
True
```

---

## List

```python
numbers = [1, 2, 3, 4]

print(3 in numbers)
```

Output:

```text
True
```

---

## Tuple

```python
data = ("Python", "Django")

print("Python" in data)
```

---

## Set

```python
skills = {"Python", "Django", "React"}

print("Python" in skills)
```

---

# 29. `not in`

```python
numbers = [1, 2, 3]

print(10 not in numbers)
```

Output:

```text
True
```

---

# 30. Dictionary-তে `in`

খুব গুরুত্বপূর্ণ:

```python
user = {
    "name": "Atiar",
    "age": 25
}

print("name" in user)
```

Output:

```text
True
```

Dictionary-তে `in` defaultভাবে **keys** check করে।

```python
print("Atiar" in user)
```

Output:

```text
False
```

---

# 31. Bitwise Operators

Bitwise operators সরাসরি binary bits-এর উপর কাজ করে।

Operators:

| Operator | Meaning     |    |
| -------- | ----------- | -- |
| `&`      | AND         |    |
| `        | `           | OR |
| `^`      | XOR         |    |
| `~`      | NOT         |    |
| `<<`     | Left shift  |    |
| `>>`     | Right shift |    |

---

# 32. Binary Representation

ধরি:

```text
5 = 101
3 = 011
```

---

# 33. Bitwise AND `&`

```python
print(5 & 3)
```

Binary:

```text
  101
& 011
-----
  001
```

Result:

```text
1
```

---

# 34. Bitwise OR `|`

```python
print(5 | 3)
```

```text
  101
| 011
-----
  111
```

Result:

```text
7
```

---

# 35. Bitwise XOR `^`

XOR:

```text
same → 0
different → 1
```

```python
print(5 ^ 3)
```

```text
  101
^ 011
-----
  110
```

Result:

```text
6
```

---

# 36. Bitwise NOT `~`

```python
print(~5)
```

Result:

```text
-6
```

Python signed integer representation-এর কারণে:

```text
~x == -(x + 1)
```

তাই:

```text
~5 = -6
```

---

# 37. Left Shift `<<`

```python
print(5 << 1)
```

Binary:

```text
101 → 1010
```

Result:

```text
10
```

প্রায়:

```text
5 × 2 = 10
```

---

# 38. Right Shift `>>`

```python
print(10 >> 1)
```

Binary:

```text
1010 → 0101
```

Result:

```text
5
```

প্রায়:

```text
10 // 2 = 5
```

---

# 39. Bitwise Operator কোথায় লাগে?

সাধারণ CRUD web application-এ খুব বেশি নয়।

কিন্তু:

* algorithms
* networking
* permissions
* flags
* low-level programming
* cryptography-related concepts
* embedded systems
* optimization

ইত্যাদিতে গুরুত্বপূর্ণ।

---

# 40. Conditional Expression

Python-এ এক লাইনে condition লেখা যায়:

```python
age = 20

status = "Adult" if age >= 18 else "Minor"

print(status)
```

Output:

```text
Adult
```

Syntax:

```python
value_if_true if condition else value_if_false
```

---

# 41. Nested Conditional Expression

Possible:

```python
score = 85

result = (
    "Excellent" if score >= 80
    else "Good" if score >= 60
    else "Fail"
)

print(result)
```

তবে অতিরিক্ত nested ternary readability কমাতে পারে।

সেক্ষেত্রে `if/elif/else` ভালো।

---

# 42. Operator Precedence

একাধিক operator থাকলে Python কোনটা আগে করবে?

উদাহরণ:

```python
result = 2 + 3 * 4
```

Output:

```text
14
```

কারণ:

```text
3 * 4 = 12
2 + 12 = 14
```

`*` আগে হয়েছে।

---

# 43. Precedence Order

সাধারণভাবে গুরুত্বপূর্ণ order:

```text
Highest
│
├── ()
├── **
├── +x, -x, ~x
├── *, /, //, %
├── +, -
├── <<, >>
├── &
├── ^
├── |
├── comparisons
├── not
├── and
└── or
Lowest
```

---

# 44. Parentheses ব্যবহার

এই:

```python
result = 10 + 5 * 2
```

Result:

```text
20
```

কিন্তু:

```python
result = (10 + 5) * 2
```

Result:

```text
30
```

তাই complex expression-এ parentheses ব্যবহার করলে code বেশি readable হয়।

---

# 45. Comparison Chaining

Python-এর সুন্দর একটি feature:

```python
age = 25

print(18 <= age <= 60)
```

Output:

```text
True
```

এটা conceptually:

```python
18 <= age and age <= 60
```

এর মতো।

---

# 46. আরও Example

```python
x = 10

print(1 < x < 20)
```

Output:

```text
True
```

এটি mathematical notation-এর মতো।

---

# 47. Comparison Chaining with Equality

```python
x = 10

print(10 == x == 10)
```

Output:

```text
True
```

---

# 48. Operator Overloading

Python-এ একই operator different object-এর জন্য different behavior করতে পারে।

উদাহরণ:

```python
10 + 20
```

Result:

```text
30
```

কিন্তু:

```python
"Hello " + "World"
```

Result:

```text
Hello World
```

আবার:

```python
[1, 2] + [3, 4]
```

Result:

```text
[1, 2, 3, 4]
```

একই `+`, কিন্তু behavior type অনুযায়ী পরিবর্তিত হয়েছে।

এটাকে **operator overloading** বলা হয়।

পরবর্তীতে OOP-তে আমরা আরও গভীরভাবে দেখব।

---

# 49. Expressions কী?

Expression হলো এমন code যা একটি value produce করে।

উদাহরণ:

```python
10 + 20
```

এটা expression।

```python
x * 5
```

এটাও expression।

```python
age >= 18
```

এটাও expression।

---

# 50. Statement বনাম Expression

### Expression

```python
10 + 20
```

Result produce করে:

```text
30
```

### Statement

```python
x = 10
```

এটা assignment statement।

আর:

```python
if x > 5:
    print(x)
```

এটা control-flow statement।

---

# 51. Function Call-ও Expression হতে পারে

```python
len("Python")
```

এটা একটি expression কারণ value produce করে:

```text
6
```

তাই:

```python
x = len("Python")
```

এখানে `len("Python")` expression হিসেবে কাজ করছে।

---

# 52. Boolean Expression

```python
age = 25

result = age >= 18
```

এখানে:

```python
age >= 18
```

একটি boolean expression।

Result:

```python
True
```

---

# 53. Arithmetic + Comparison + Logical

বাস্তব code:

```python
age = 25
salary = 50000
has_experience = True

eligible = (
    age >= 18
    and salary >= 30000
    and has_experience
)

print(eligible)
```

Output:

```text
True
```

এই ধরনের expression তোমার backend/API business logic-এ অনেক থাকবে।

---

# 54. Real-world Example — Login

```python
email = "user@example.com"
password_correct = True
account_active = True

can_login = (
    email != ""
    and password_correct
    and account_active
)

print(can_login)
```

---

# 55. Real-world Example — AI Text Processing

ধরি AI system একটি sentence-এর score দিয়েছে:

```python
score = 0.87

is_high_probability = score >= 0.80

print(is_high_probability)
```

Output:

```text
True
```

আর:

```python
score = 0.87

label = "High" if score >= 0.80 else "Low"

print(label)
```

---

# 56. Real-world Example — API Permission

```python
is_authenticated = True
is_admin = False
is_owner = True

can_edit = (
    is_authenticated
    and (is_admin or is_owner)
)

print(can_edit)
```

Output:

```text
True
```

এই ধরনের logic Django/DRF permission system-এ খুব common।

---

# 57. `and`/`or` এর Value-returning Behavior

এইটা ভালোভাবে বোঝো:

```python
print("" or "Python")
```

Output:

```text
Python
```

কারণ `""` falsey।

আর:

```python
print("Python" or "Django")
```

Output:

```text
Python
```

কারণ `"Python"` truthy।

---

# 58. Default Value Pattern

এটা Python-এ খুব common:

```python
name = user_input or "Anonymous"
```

যদি:

```python
user_input = ""
```

তাহলে:

```text
name = "Anonymous"
```

আর:

```python
user_input = "Atiar"
```

তাহলে:

```text
name = "Atiar"
```

---

# 59. `not` এর Precedence

```python
x = True
y = False

print(not x and y)
```

Python আগে:

```python
not x
```

করবে।

Result:

```text
False
```

তারপর:

```python
False and False
```

Result:

```text
False
```

---

# 60. Common Mistake: `=` বনাম `==`

ভুল:

```python
if age = 18:
```

এটা invalid syntax।

সঠিক:

```python
if age == 18:
```

মনে রাখো:

```text
=   → assignment
==  → comparison
```

---

# 61. Common Mistake: `is` দিয়ে value comparison

Avoid:

```python
if x is 10:
```

Value compare করার জন্য:

```python
if x == 10:
```

`is` identity-এর জন্য।

বিশেষভাবে:

```python
x is None
```

ব্যবহার করা হয়।

---

# 62. Common Mistake: `and` / `or` precedence

```python
result = True or False and False
```

Python আগে `and` করবে:

```python
False and False
→ False
```

তারপর:

```python
True or False
→ True
```

Result:

```text
True
```

স্পষ্ট করতে:

```python
result = True or (False and False)
```

---

# 63. Advanced: Assignment Expression `:=`

Python 3.8+ এ **walrus operator** আছে:

```python
:= 
```

এটি expression-এর মধ্যে assignment করতে পারে।

উদাহরণ:

```python
if (n := len("Python")) > 5:
    print(n)
```

Output:

```text
6
```

এখানে:

```python
n := len("Python")
```

একইসাথে value assign এবং expression হিসেবে ব্যবহার করছে।

---

# 64. কখন `:=` ব্যবহার করবে?

খুব বেশি ব্যবহার করা উচিত নয়।

Readable code:

```python
length = len(text)

if length > 100:
    print(length)
```

অনেক সময় এটি বেশি পরিষ্কার।

Walrus operator useful হতে পারে loop বা conditional-এর কিছু নির্দিষ্ট pattern-এ।

---

# 65. Full Operator Summary

```text
Arithmetic
+  -  *  /  //  %  **

Comparison
==  !=  >  <  >=  <=

Logical
and  or  not

Assignment
=  +=  -=  *=  /=  //=
%=  **=  &=  |=  ^=  >>=  <<=

Identity
is  is not

Membership
in  not in

Bitwise
&  |  ^  ~  <<  >>

Conditional
x if condition else y

Assignment Expression
:=
```

---

# 66. 🧠 Operator Mental Model

```text
             OPERATOR
                 │
     ┌───────────┼───────────┐
     ↓           ↓           ↓
  Calculate   Compare      Logic
     │           │           │
 + - * /       == !=       and/or/not
 % // **       > < >= <=
     
     ┌───────────┼───────────┐
     ↓           ↓           ↓
 Identity    Membership    Bits
     │           │           │
  is/is not   in/not in   & | ^ ~ << >>
```

---

# 67. Practice — Level 1

নিজে solve করো।

### Q1

```python
a = 15
b = 4
```

নিচের সবগুলো বের করো:

```text
+
-
*
/
//
%
**
```

---

### Q2

Check করো numberটি even কিনা:

```python
number = 27
```

---

### Q3

Check করো:

```python
age = 25
```

age কি `18` থেকে `60` এর মধ্যে?

---

### Q4

```python
x = 10
y = 10
```

`==` এবং `is` ব্যবহার করে দুইটি result বের করো।

তারপর explain করো কেন result একই/ভিন্ন হতে পারে।

---

# 68. Practice — Level 2

### Q5

একজন user login করতে পারবে যদি:

```text
authenticated = True
active = True
```

দুটো condition True হলে `can_login = True` হবে।

---

### Q6

```python
score = 75
```

নিচের logic তৈরি করো:

```text
80+ → Excellent
60–79 → Good
below 60 → Fail
```

---

### Q7

এই list-এ `"Python"` আছে কিনা check করো:

```python
skills = ["Python", "Django", "React"]
```

---

### Q8

এই dictionary-তে `"email"` key আছে কিনা check করো:

```python
user = {
    "name": "Atiar",
    "age": 25
}
```

---

# 69. Practice — Level 3

এই expression-এর output **code না চালিয়ে** আগে অনুমান করো:

### Q9

```python
result = 10 + 5 * 2
```

---

### Q10

```python
result = (10 + 5) * 2
```

---

### Q11

```python
result = True or False and False
```

---

### Q12

```python
result = 10 > 5 and 20 < 30
```

---

### Q13

```python
result = 10 == 10 or 5 > 10
```

---

# 70. 🔥 M01.04 Challenge

একটি eligibility system বানাও।

Input:

```python
age = 25
score = 82
has_certificate = True
experience = 2
```

Rules:

```text
age >= 18
AND
score >= 70
AND
certificate থাকতে হবে
AND
experience >= 1
```

Output:

```text
Eligible
```

অন্যথায়:

```text
Not Eligible
```

---

# 71. 🔥 AI Project Challenge

ধরি তোমার future AI writing system একটি text-এর:

```python
ai_score = 0.87
word_count = 350
has_grammar_issue = False
```

Rules:

```text
AI score >= 0.80
AND
word count >= 100
AND
grammar issue নেই
```

তাহলে:

```text
"Needs Analysis"
```

অন্যথায়:

```text
"Low Risk"
```

এটা operators ব্যবহার করে implement করো।

---

# 72. M01.04 Completion Checklist

এই lesson শেষ করার আগে তুমি যেন explain করতে পারো:

### Arithmetic

* [ ] `+`
* [ ] `-`
* [ ] `*`
* [ ] `/`
* [ ] `//`
* [ ] `%`
* [ ] `**`

### Comparison

* [ ] `==`
* [ ] `!=`
* [ ] `>`
* [ ] `<`
* [ ] `>=`
* [ ] `<=`

### Logical

* [ ] `and`
* [ ] `or`
* [ ] `not`
* [ ] Truth table
* [ ] Short-circuit evaluation
* [ ] Value-returning behavior

### Assignment

* [ ] `=`
* [ ] `+=`
* [ ] `-=`
* [ ] `*=`
* [ ] `/=`
* [ ] `//=`
* [ ] `%=`
* [ ] `**=`

### Other

* [ ] `is`
* [ ] `is not`
* [ ] `in`
* [ ] `not in`
* [ ] Bitwise operators
* [ ] Conditional expression
* [ ] Operator precedence
* [ ] Comparison chaining
* [ ] Operator overloading
* [ ] Expression vs statement
* [ ] `:=`

---

## 🎯 M01.04-এর সবচেয়ে গুরুত্বপূর্ণ 10টি জিনিস

```text
1. =   → assignment
2. ==  → value comparison
3. is  → identity comparison
4. is None → None check
5. and/or/not → logical operations
6. in → membership
7. % → remainder
8. // → floor division
9. () → precedence control
10. x if condition else y → conditional expression
```

**M01.04 complete.**

পরবর্তী lesson হবে:

### 🟢 M01.05 — Python Control Flow

যেখানে আমরা **`if`, `elif`, `else`, nested conditions, truthy/falsy, `match-case`, loops-এর foundation, `break`, `continue`, `pass`, এবং control-flow design** বিস্তারিতভাবে শিখব।


---
# 🟢 M01.05 — Python Control Flow: Complete Deep Dive

আজ আমরা Python-এর **Control Flow** শিখব।
এটা Python-এর সবচেয়ে গুরুত্বপূর্ণ foundation-এর একটি, কারণ program কীভাবে **decision নেবে, কোন code কখন চলবে, কতবার চলবে, কোথায় থামবে**—এসব Control Flow দিয়ে নির্ধারণ করা হয়।

আমরা একসাথে শিখব:

```text
if
elif
else
nested if
truthy/falsy
and / or / not
conditional expression
match-case
for
while
break
continue
pass
else with loops
nested loops
control-flow design
```

> `for` এবং `while` আমরা এখানে foundation হিসেবে দেখব; পরবর্তী M01 lesson-এ iteration/loops আরও গভীরভাবে করা হবে।

---

# 1. Control Flow কী?

সাধারণভাবে Python code উপরের দিক থেকে নিচের দিকে execute করে:

```python
print("A")
print("B")
print("C")
```

Output:

```text
A
B
C
```

কিন্তু বাস্তব program-এ সব code সবসময় execute হবে না।

যেমন:

```python
age = 20

if age >= 18:
    print("Adult")
```

এখানে condition অনুযায়ী সিদ্ধান্ত নেওয়া হচ্ছে।

এটাই **Control Flow**।

---

# 2. Control Flow-এর মূল ধারণা

```text
Program
   │
   ↓
Condition?
   │
 ┌─┴───────┐
 ↓         ↓
True     False
 │         │
 ↓         ↓
Code A    Code B
```

অর্থাৎ program-এর execution path condition-এর উপর নির্ভর করে।

---

# 3. `if`

সবচেয়ে basic decision structure:

```python
if condition:
    statement
```

Example:

```python
age = 25

if age >= 18:
    print("Adult")
```

Output:

```text
Adult
```

---

# 4. `if` কীভাবে কাজ করে?

```python
age = 25

if age >= 18:
    print("Adult")
```

Python:

```text
age >= 18
     ↓
   True
     ↓
execute block
     ↓
"Adult"
```

যদি:

```python
age = 15
```

হয়:

```text
15 >= 18
    ↓
  False
    ↓
block skipped
```

---

# 5. Indentation

Python-এ block বোঝাতে indentation ব্যবহার করা হয়।

সঠিক:

```python
if age >= 18:
    print("Adult")
```

ভুল:

```python
if age >= 18:
print("Adult")
```

সাধারণ convention:

```text
4 spaces
```

ব্যবহার করা।

---

# 6. Multiple Statements

একটি `if` block-এর মধ্যে একাধিক statement থাকতে পারে:

```python
age = 25

if age >= 18:
    print("Adult")
    print("Eligible to vote")
    print("Can apply")
```

সবগুলো statement condition True হলে execute হবে।

---

# 7. `if` Condition Expression

Condition অবশ্যই Boolean value-তে evaluate হতে পারে।

```python
x = 10

if x > 5:
    print("Greater")
```

এখানে:

```python
x > 5
```

একটি Boolean expression।

---

# 8. `if` with Boolean

```python
is_logged_in = True

if is_logged_in:
    print("Welcome")
```

---

# 9. `if` with `None`

```python
user = None

if user is None:
    print("No user found")
```

`None` check করার best practice:

```python
is None
```

---

# 10. `if-else`

যখন দুইটি possible path আছে:

```python
if condition:
    ...
else:
    ...
```

Example:

```python
age = 15

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

Output:

```text
Minor
```

---

# 11. Real-world Login Example

```python
password_correct = True

if password_correct:
    print("Login successful")
else:
    print("Invalid password")
```

---

# 12. `if-elif-else`

একাধিক condition থাকলে:

```python
if condition1:
    ...
elif condition2:
    ...
else:
    ...
```

Example:

```python
score = 75

if score >= 80:
    print("Excellent")
elif score >= 60:
    print("Good")
else:
    print("Fail")
```

Output:

```text
Good
```

---

# 13. Python `elif` কীভাবে কাজ করে?

ধরি:

```python
score = 85
```

Python:

```text
score >= 80?
     ↓
   True
     ↓
Excellent
```

এর পরের `elif` আর check করবে না।

---

# 14. গুরুত্বপূর্ণ: First Matching Condition

```python
score = 90

if score >= 80:
    print("A")
elif score >= 60:
    print("B")
elif score >= 40:
    print("C")
else:
    print("F")
```

Output:

```text
A
```

যদিও:

```text
90 >= 60
90 >= 40
```

সবই True, কিন্তু প্রথম matching condition-ই execute হবে।

---

# 15. Condition Order খুব গুরুত্বপূর্ণ

ভুল design:

```python
score = 90

if score >= 40:
    print("Pass")
elif score >= 80:
    print("Excellent")
```

Output:

```text
Pass
```

কারণ `score >= 40` আগে True হয়ে গেছে।

সঠিক:

```python
if score >= 80:
    print("Excellent")
elif score >= 40:
    print("Pass")
else:
    print("Fail")
```

---

# 16. Nested `if`

একটি `if`-এর মধ্যে আরেকটি `if` থাকতে পারে।

```python
age = 25
has_id = True

if age >= 18:
    if has_id:
        print("Allowed")
```

---

# 17. Nested Condition Diagram

```text
age >= 18?
   │
   ├── False → Stop
   │
   └── True
        │
        ↓
     has_id?
        │
     ┌──┴──┐
     ↓     ↓
   True   False
     ↓      ↓
 Allowed  Denied
```

---

# 18. Nested `if` আরও Practical

```python
username = "admin"
password_correct = True

if username == "admin":
    if password_correct:
        print("Login successful")
    else:
        print("Wrong password")
else:
    print("Unknown user")
```

---

# 19. Nested `if` সবসময় দরকার হয় না

উপরের logic এভাবে লেখা যায়:

```python
if username == "admin" and password_correct:
    print("Login successful")
else:
    print("Login failed")
```

অনেক ক্ষেত্রে এটা বেশি readable।

---

# 20. Truthy & Falsy

Python-এ condition-এর জায়গায় সরাসরি value দেওয়া যায়।

```python
name = "Atiar"

if name:
    print("Name exists")
```

String non-empty হওয়ায় এটি True হিসেবে behave করবে।

---

# 21. Falsey Values

গুরুত্বপূর্ণ falsey values:

```python
False
None
0
0.0
0j
""
[]
()
{}
set()
```

উদাহরণ:

```python
items = []

if items:
    print("Items available")
else:
    print("No items")
```

Output:

```text
No items
```

---

# 22. Truthy Example

```python
items = [1, 2, 3]

if items:
    print("Items available")
```

Output:

```text
Items available
```

---

# 23. `bool()` দিয়ে পরীক্ষা

```python
print(bool(""))
print(bool("Python"))

print(bool([]))
print(bool([1]))

print(bool(0))
print(bool(10))
```

Output:

```text
False
True
False
True
False
True
```

---

# 24. Truthy/Falsy কেন গুরুত্বপূর্ণ?

Backend programming-এ খুব common:

```python
if user:
    ...
```

```python
if data:
    ...
```

```python
if errors:
    ...
```

```python
if token:
    ...
```

---

# 25. Logical Operators-এর সাথে Control Flow

আমরা M01.04-এ `and`, `or`, `not` শিখেছি।

এখন decision-এর মধ্যে ব্যবহার করব।

```python
age = 25
has_id = True

if age >= 18 and has_id:
    print("Allowed")
```

---

# 26. Multiple Conditions

```python
age = 25
country = "Bangladesh"

if age >= 18 and country == "Bangladesh":
    print("Eligible")
```

---

# 27. `or`

```python
is_admin = False
is_staff = True

if is_admin or is_staff:
    print("Access granted")
```

---

# 28. `not`

```python
is_banned = False

if not is_banned:
    print("User can continue")
```

---

# 29. Complex Condition

```python
age = 25
is_verified = True
is_banned = False

if age >= 18 and is_verified and not is_banned:
    print("Access granted")
```

এ ধরনের logic real application-এ খুব common।

---

# 30. Conditional Expression

এক লাইনের decision:

```python
age = 20

status = "Adult" if age >= 18 else "Minor"
```

এটাকে **ternary/conditional expression** বলা হয়।

---

# 31. Conditional Expression বনাম `if`

Conditional expression:

```python
status = "Adult" if age >= 18 else "Minor"
```

Normal:

```python
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
```

Simple assignment-এর ক্ষেত্রে প্রথমটি convenient।

---

# 32. `match-case`

Python 3.10+ এ structural pattern matching আছে।

Basic example:

```python
day = 2

match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case 3:
        print("Wednesday")
    case _:
        print("Unknown")
```

Output:

```text
Tuesday
```

---

# 33. `case _`

```python
case _:
```

এটি সাধারণভাবে default/fallback pattern হিসেবে কাজ করে।

অনেকটা:

```python
else
```

এর মতো।

---

# 34. `match` কেন ব্যবহার করব?

অনেক alternative value compare করতে হলে `match-case` code readable করতে পারে।

যেমন:

```python
command = "start"

match command:
    case "start":
        print("Starting")
    case "stop":
        print("Stopping")
    case "restart":
        print("Restarting")
    case _:
        print("Unknown command")
```

---

# 35. `match` বনাম `if-elif`

এটা:

```python
if command == "start":
    ...
elif command == "stop":
    ...
elif command == "restart":
    ...
```

এর পরিবর্তে:

```python
match command:
    case "start":
        ...
    case "stop":
        ...
    case "restart":
        ...
```

কিছু ক্ষেত্রে বেশি readable।

---

# 36. `match` with Multiple Values

```python
status = "pending"

match status:
    case "pending" | "processing":
        print("In progress")
    case "completed":
        print("Done")
    case "failed":
        print("Failed")
    case _:
        print("Unknown")
```

---

# 37. `match` with Guard

Pattern-এর সাথে condition যোগ করা যায়:

```python
score = 85

match score:
    case score if score >= 80:
        print("Excellent")
    case score if score >= 60:
        print("Good")
    case _:
        print("Fail")
```

---

# 38. `for` Loop — Control Flow-এর Repetition

`for` ব্যবহার করে iterable-এর প্রতিটি item-এর উপর কাজ করা যায়।

```python
numbers = [1, 2, 3, 4]

for number in numbers:
    print(number)
```

Output:

```text
1
2
3
4
```

---

# 39. `for` কীভাবে কাজ করে?

```text
numbers
   │
   ↓
[1, 2, 3, 4]
   │
   ├── 1 → execute
   ├── 2 → execute
   ├── 3 → execute
   └── 4 → execute
```

---

# 40. `range()` with `for`

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

---

# 41. `while`

যতক্ষণ condition True থাকবে, loop চলবে।

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

Output:

```text
1
2
3
4
5
```

---

# 42. Infinite Loop

যদি condition কখনো False না হয়:

```python
while True:
    print("Running")
```

এটা infinite loop।

তাই `break` দরকার হতে পারে।

---

# 43. `break`

Loop সম্পূর্ণভাবে terminate করে।

```python
for number in range(10):
    if number == 5:
        break

    print(number)
```

Output:

```text
0
1
2
3
4
```

---

# 44. `continue`

Current iteration skip করে next iteration-এ যায়।

```python
for number in range(5):
    if number == 2:
        continue

    print(number)
```

Output:

```text
0
1
3
4
```

`2` skip হয়েছে।

---

# 45. `break` বনাম `continue`

```text
break
  ↓
সম্পূর্ণ loop শেষ

continue
  ↓
বর্তমান iteration skip
  ↓
পরবর্তী iteration
```

---

# 46. `pass`

`pass` কিছু করে না।

এটি placeholder হিসেবে ব্যবহৃত হয়।

```python
if age >= 18:
    pass
```

এখানে error হবে না।

---

# 47. `pass` কেন দরকার?

যখন পরে code লিখবে:

```python
def process_data():
    pass
```

Function structure তৈরি করা যায়।

Class-এর ক্ষেত্রেও:

```python
class User:
    pass
```

---

# 48. `break`, `continue`, `pass` একসাথে

```python
for number in range(10):

    if number == 2:
        continue

    if number == 5:
        break

    if number == 3:
        pass

    print(number)
```

Output:

```text
0
1
3
4
```

---

# 49. Loop-এর `else`

Python-এর interesting feature।

```python
for number in range(5):
    print(number)
else:
    print("Loop completed")
```

Output:

```text
0
1
2
3
4
Loop completed
```

---

# 50. `else` কখন execute হয়?

Loop যদি **normalভাবে শেষ হয়**, তাহলে `else` execute হয়।

কিন্তু `break` হলে `else` execute হয় না।

```python
for number in range(5):
    if number == 2:
        break

    print(number)
else:
    print("Completed")
```

Output:

```text
0
1
```

`Completed` print হয়নি।

---

# 51. Loop `else` কেন useful?

বিশেষ করে search operation-এ।

```python
numbers = [10, 20, 30, 40]
target = 50

for number in numbers:
    if number == target:
        print("Found")
        break
else:
    print("Not found")
```

Output:

```text
Not found
```

এখানে:

```text
found → break → else skip
not found → loop শেষ → else execute
```

---

# 52. Nested Loops

একটি loop-এর মধ্যে আরেকটি loop।

```python
for i in range(3):
    for j in range(3):
        print(i, j)
```

Output:

```text
0 0
0 1
0 2
1 0
1 1
1 2
2 0
2 1
2 2
```

---

# 53. Nested Loop Flow

```text
i = 0
 ├── j = 0
 ├── j = 1
 └── j = 2

i = 1
 ├── j = 0
 ├── j = 1
 └── j = 2

i = 2
 ├── j = 0
 ├── j = 1
 └── j = 2
```

---

# 54. Practical Example — Matrix

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for value in row:
        print(value)
```

---

# 55. `break` in Nested Loop

খুব গুরুত্বপূর্ণ:

```python
for i in range(3):
    for j in range(3):
        if j == 1:
            break

        print(i, j)
```

`break` শুধু **যে loop-এর ভিতরে আছে সেই nearest loop** থেকে বের হয়।

---

# 56. `continue` in Nested Loop

```python
for i in range(3):
    for j in range(3):
        if j == 1:
            continue

        print(i, j)
```

শুধু inner loop-এর current iteration skip হবে।

---

# 57. Control Flow with Collections

ধরি:

```python
users = [
    {"name": "Rahim", "active": True},
    {"name": "Karim", "active": False},
    {"name": "Hasan", "active": True},
]
```

Active users:

```python
for user in users:
    if user["active"]:
        print(user["name"])
```

Output:

```text
Rahim
Hasan
```

এটা backend development-এ অত্যন্ত common pattern।

---

# 58. AI/NLP Example

ধরি:

```python
sentences = [
    {"text": "Python is useful.", "score": 0.90},
    {"text": "I like coding.", "score": 0.30},
    {"text": "AI is powerful.", "score": 0.85},
]
```

High-score sentences:

```python
for sentence in sentences:
    if sentence["score"] >= 0.80:
        print(sentence["text"])
```

Output:

```text
Python is useful.
AI is powerful.
```

---

# 59. Multiple Decisions in AI Pipeline

```python
score = 0.87

if score >= 0.90:
    label = "Very High"
elif score >= 0.80:
    label = "High"
elif score >= 0.50:
    label = "Medium"
else:
    label = "Low"

print(label)
```

Output:

```text
High
```

---

# 60. Control Flow Design

একটি ভালো decision system সাধারণত:

```text
Input
 ↓
Validate
 ↓
Condition
 ↓
Decision
 ↓
Action
 ↓
Output
```

Example:

```python
age = 25

if age < 0:
    print("Invalid age")
elif age < 18:
    print("Minor")
else:
    print("Adult")
```

এখানে validation আগে হয়েছে।

---

# 61. Guard Clause

Code readable করার জন্য **guard clause** ব্যবহার করা হয়।

ধরি:

```python
def process_user(user):
    if user is not None:
        if user["active"]:
            print("Processing")
```

এটা অনেক সময় এভাবে লেখা যায়:

```python
def process_user(user):
    if user is None:
        return

    if not user["active"]:
        return

    print("Processing")
```

এতে nested code কমে যায়।

---

# 62. Guard Clause কেন গুরুত্বপূর্ণ?

Bad:

```text
if user:
    if active:
        if verified:
            if permission:
                process()
```

অনেক nested block।

Better:

```text
if not user:
    return

if not active:
    return

if not verified:
    return

if not permission:
    return

process()
```

Large backend application-এ readability অনেক বাড়ে।

---

# 63. Control Flow-এর Common Mistakes

### Mistake 1 — `=` ব্যবহার

ভুল:

```python
if age = 18:
```

সঠিক:

```python
if age == 18:
```

---

### Mistake 2 — Indentation

ভুল:

```python
if age >= 18:
print("Adult")
```

সঠিক:

```python
if age >= 18:
    print("Adult")
```

---

# 64. Common Mistake — Condition সবসময় `== True` করা

অপ্রয়োজনীয়:

```python
if is_active == True:
    print("Active")
```

Better:

```python
if is_active:
    print("Active")
```

আর False check:

```python
if not is_active:
    print("Inactive")
```

---

# 65. Common Mistake — Empty Collection

এটা:

```python
items = []

if items == []:
    print("Empty")
```

কাজ করে।

কিন্তু অনেক ক্ষেত্রে আরও Pythonic:

```python
if not items:
    print("Empty")
```

---

# 66. Common Mistake — অতিরিক্ত Nested Conditions

এমন code:

```python
if user:
    if user["active"]:
        if user["verified"]:
            if user["age"] >= 18:
                print("Allowed")
```

এর পরিবর্তে:

```python
if (
    user
    and user["active"]
    and user["verified"]
    and user["age"] >= 18
):
    print("Allowed")
```

অথবা guard clauses।

---

# 67. Control Flow এবং Exceptions

এটা পরবর্তী advanced topic, কিন্তু basic ধারণা রাখো।

```python
try:
    number = int(input("Enter number: "))
except ValueError:
    print("Invalid number")
```

এখানেও program-এর execution path change হচ্ছে।

পরবর্তী lesson-এ exception handling আলাদাভাবে deep dive করা হবে।

---

# 68. একটি Complete Example

```python
age = 25
is_verified = True
is_banned = False
score = 85

if age < 18:
    print("Not eligible")

elif is_banned:
    print("Account banned")

elif not is_verified:
    print("Account not verified")

elif score >= 80:
    print("Eligible - Excellent")

elif score >= 60:
    print("Eligible - Good")

else:
    print("Eligible - Low score")
```

Output:

```text
Eligible - Excellent
```

এখানে আমরা ব্যবহার করেছি:

* `if`
* `elif`
* `else`
* comparison
* `not`
* boolean
* ordered conditions

---

# 69. 🧠 Control Flow Mental Model

এটা মনে রাখো:

```text
                 CONTROL FLOW
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
    Decision       Repetition      Transfer
       │              │              │
   if/elif/else    for/while    break
   match-case                     continue
                                  pass
```

আর:

```text
Decision
   ↓
Condition
   ↓
True / False
   ↓
Different execution path
```

---

# 70. Practice — Level 1

নিজে solve করো।

### Q1

একটি number:

```python
number = 15
```

Check করো number positive, negative নাকি zero।

---

### Q2

```python
age = 20
```

Check:

```text
18+ → Adult
below 18 → Minor
```

---

### Q3

```python
score = 72
```

Rules:

```text
80+ → A
70–79 → B
60–69 → C
50–59 → D
below 50 → F
```

---

### Q4

Check করো একটি number even নাকি odd।

---

# 71. Practice — Level 2

### Q5

Login system:

```python
email = "user@example.com"
password_correct = True
is_active = True
```

Rules:

```text
email থাকতে হবে
AND
password correct হতে হবে
AND
account active হতে হবে
```

Output:

```text
Login successful
```

---

### Q6

একটি list:

```python
numbers = [10, 20, 30, 40, 50]
```

শুধু `30`-এর পরের numbers print করো না।

অর্থাৎ `30` এবং তার পরের iteration skip/stop করার জন্য `continue` বা `break` ব্যবহার করে দুইটি solution লিখো।

---

### Q7

এই list-এ target search করো:

```python
numbers = [10, 20, 30, 40, 50]
target = 30
```

পেলে:

```text
Found
```

না পেলে:

```text
Not Found
```

এখানে loop `else` ব্যবহার করো।

---

# 72. Practice — Level 3

এই data:

```python
users = [
    {
        "name": "Rahim",
        "age": 22,
        "active": True
    },
    {
        "name": "Karim",
        "age": 17,
        "active": True
    },
    {
        "name": "Hasan",
        "age": 30,
        "active": False
    },
    {
        "name": "Nabil",
        "age": 25,
        "active": True
    }
]
```

শুধু সেই users print করো যাদের:

```text
age >= 18
AND
active == True
```

Expected:

```text
Rahim
Nabil
```

---

# 73. 🔥 M01.05 Challenge — AI Text Analysis

ধরি:

```python
sentences = [
    {
        "text": "Artificial intelligence is changing technology.",
        "score": 0.92
    },
    {
        "text": "I enjoy learning Python.",
        "score": 0.31
    },
    {
        "text": "Machine learning is useful.",
        "score": 0.78
    },
    {
        "text": "Python is easy to learn.",
        "score": 0.15
    }
]
```

তোমার task:

### Step 1

প্রতিটি sentence-এর score check করো।

### Step 2

Rules:

```text
score >= 0.80 → High
score >= 0.50 → Medium
score < 0.50 → Low
```

### Step 3

Output:

```text
Artificial intelligence is changing technology. → High
I enjoy learning Python. → Low
Machine learning is useful. → Medium
Python is easy to learn. → Low
```

### Step 4

একটি নতুন list তৈরি করো:

```python
[
    {
        "text": "...",
        "score": 0.92,
        "label": "High"
    }
]
```

এই exercise তোমার future **sentence-level NLP analysis pipeline**-এর foundation তৈরি করবে।

---

# 74. 🧪 M01.05 Theory Test

নিজেকে এই প্রশ্নগুলো করো:

1. Control Flow কী?
2. `if` কী করে?
3. `elif` কখন ব্যবহার করি?
4. `else` কখন execute হয়?
5. `if` এবং `elif`-এর মধ্যে পার্থক্য কী?
6. Nested `if` কী?
7. Truthy/Falsy কী?
8. `if []:` কেন False?
9. `if "Python":` কেন True?
10. `match-case` কী?
11. `case _` কী?
12. `for` কী?
13. `while` কী?
14. `break` কী করে?
15. `continue` কী করে?
16. `pass` কী করে?
17. loop-এর `else` কখন execute হয়?
18. `break` করলে loop-এর `else` কেন চলে না?
19. Guard clause কী?
20. অতিরিক্ত nested condition কেন avoid করা উচিত?

---

# 75. M01.05 Completion Checklist

### Decision Making

* [ ] `if`
* [ ] `elif`
* [ ] `else`
* [ ] Nested `if`
* [ ] Multiple conditions
* [ ] Condition ordering
* [ ] Truthy/Falsy
* [ ] `and`
* [ ] `or`
* [ ] `not`

### Modern Python

* [ ] Conditional expression
* [ ] `match`
* [ ] `case`
* [ ] `case _`
* [ ] Multiple patterns
* [ ] Guard pattern

### Repetition Foundation

* [ ] `for`
* [ ] `while`
* [ ] `range`
* [ ] Nested loops

### Loop Control

* [ ] `break`
* [ ] `continue`
* [ ] `pass`
* [ ] Loop `else`

### Code Design

* [ ] Condition ordering
* [ ] Guard clauses
* [ ] Avoid unnecessary nesting
* [ ] Pythonic truthiness
* [ ] Backend business logic
* [ ] AI/NLP decision logic

---

# 🎯 M01.05-এর সবচেয়ে গুরুত্বপূর্ণ 12টি বিষয়

```text
1. if          → decision
2. elif        → alternative condition
3. else        → fallback
4. indentation → block structure
5. truthy      → True-like value
6. falsy       → False-like value
7. and/or/not  → combine conditions
8. match-case  → pattern-based decision
9. for         → iterable-based repetition
10. while      → condition-based repetition
11. break      → stop loop
12. continue   → skip current iteration
```

### পুরো Control Flow-এর mental model:

```text
                 INPUT
                   │
                   ↓
               CONDITION
                   │
          ┌────────┴────────┐
          ↓                 ↓
        TRUE              FALSE
          │                 │
          ↓                 ↓
       ACTION A          ACTION B
          │                 │
          └────────┬────────┘
                   ↓
                 LOOP?
              ┌────┴────┐
             YES        NO
              │
              ↓
        Next iteration
```

**🟢 M01.05 complete.**

পরবর্তী ধাপ হবে **🟢 M01.06 — Python Loops & Iteration Deep Dive** — যেখানে `for`, `while`, `range`, `enumerate()`, `zip()`, iterable বনাম iterator, `iter()`, `next()`, nested loops, loop patterns, searching, counting, accumulation, এবং algorithmic loop thinking একদম গভীরভাবে শেখা হবে।


---
# 🚀 M01.06 — Python Loops & Iteration Deep Dive

আজকের lesson-এ আমরা শুধু `for`/`while` syntax শিখব না। **Iterable → Iterator → `iter()` → `next()` → loop internally কীভাবে কাজ করে → `enumerate()` → `zip()` → searching → counting → accumulation → nested loops → algorithmic thinking**—সব cover করব।

---

# 1. Iteration কী?

**Iteration** হলো কোনো data collection-এর elements একে একে process করা।

```python
numbers = [10, 20, 30, 40]

for number in numbers:
    print(number)
```

Output:

```text
10
20
30
40
```

Flow:

```text
[10, 20, 30, 40]
       ↓
      10 → process
       ↓
      20 → process
       ↓
      30 → process
       ↓
      40 → process
```

---

# 2. Loop কী?

Loop হলো কোনো কাজ বারবার করার mechanism।

Python-এর প্রধান loop:

```text
for
while
```

### `for`

সাধারণত কোনো iterable-এর প্রতিটি item নিয়ে কাজ করতে:

```python
for item in collection:
    ...
```

### `while`

Condition `True` থাকা পর্যন্ত:

```python
while condition:
    ...
```

---

# 3. Iterable কী?

**Iterable** হলো এমন object যার elements একে একে পাওয়া যায়।

Common iterable:

```text
list
tuple
string
set
dict
range
```

Example:

```python
numbers = [10, 20, 30]

for x in numbers:
    print(x)
```

List হলো iterable।

String-ও iterable:

```python
text = "Python"

for char in text:
    print(char)
```

Output:

```text
P
y
t
h
o
n
```

---

# 4. Iterator কী?

**Iterator** হলো এমন object যেটা একবারে একটি value দেয় এবং নিজের current position মনে রাখে।

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

```text
10
20
30
```

Concept:

```text
List
 ↓
iter()
 ↓
Iterator
 ↓
next() → 10
 ↓
next() → 20
 ↓
next() → 30
```

---

# 5. `iter()` Deep Dive

```python
numbers = [10, 20, 30]

it = iter(numbers)
```

এখন `it` হলো iterator।

```python
print(it)
```

তারপর:

```python
print(next(it))
```

Output:

```text
10
```

আবার:

```python
print(next(it))
```

Output:

```text
20
```

আবার:

```python
print(next(it))
```

Output:

```text
30
```

---

# 6. `next()` কী করে?

`next()` iterator থেকে পরবর্তী element বের করে।

```python
numbers = [10, 20, 30]

it = iter(numbers)

print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
```

যখন আর কোনো element নেই:

```python
print(next(it))
```

তখন:

```text
StopIteration
```

exception পাওয়া যাবে।

---

# 7. `for` Loop Internally কীভাবে কাজ করে?

এই code:

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Conceptually Python এটাকে এরকমভাবে চালায়:

```python
iterator = iter(numbers)

while True:
    try:
        number = next(iterator)
        print(number)
    except StopIteration:
        break
```

অর্থাৎ:

```text
for
 ↓
iter()
 ↓
next()
 ↓
process
 ↓
next()
 ↓
process
 ↓
next()
 ↓
process
 ↓
StopIteration
 ↓
loop শেষ
```

এটি Python-এর সবচেয়ে গুরুত্বপূর্ণ loop concepts-এর একটি।

---

# 8. `for` + List

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers:
    print(number)
```

---

# 9. `for` + Tuple

```python
languages = ("Python", "JavaScript", "C++")

for language in languages:
    print(language)
```

---

# 10. `for` + String

```python
word = "Algorithm"

for character in word:
    print(character)
```

---

# 11. `for` + Set

```python
numbers = {10, 20, 30, 40}

for number in numbers:
    print(number)
```

মনে রাখবে:

> Set-এর iteration order-এর উপর নির্ভর করা উচিত নয়।

---

# 12. Dictionary Loop

```python
user = {
    "name": "Atiar",
    "age": 25,
    "country": "Bangladesh"
}
```

### শুধু keys

```python
for key in user:
    print(key)
```

অথবা:

```python
for key in user.keys():
    print(key)
```

---

### শুধু values

```python
for value in user.values():
    print(value)
```

---

### Key + Value

```python
for key, value in user.items():
    print(key, value)
```

Output:

```text
name Atiar
age 25
country Bangladesh
```

এখানে গুরুত্বপূর্ণ বিষয়:

```python
for key, value in user.items():
```

প্রতিটি `(key, value)` pair unpack হচ্ছে।

---

# 13. `range()` Deep Dive

Loop-এর সঙ্গে সবচেয়ে বেশি ব্যবহৃত function:

```python
range()
```

### Basic

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

খেয়াল করো:

```text
range(5)
start = 0
stop = 5
```

`5` included নয়।

---

# 14. `range(start, stop)`

```python
for i in range(2, 7):
    print(i)
```

Output:

```text
2
3
4
5
6
```

Formula:

```text
start included
stop excluded
```

---

# 15. `range(start, stop, step)`

```python
for i in range(0, 10, 2):
    print(i)
```

Output:

```text
0
2
4
6
8
```

---

# 16. Reverse `range()`

```python
for i in range(10, 0, -1):
    print(i)
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

---

# 17. `range()` নিয়ে Common Mistake

ভুল:

```python
range(1, 10)
```

এতে `10` আসবে না।

Output:

```text
1 2 3 4 5 6 7 8 9
```

যদি `10` দরকার হয়:

```python
range(1, 11)
```

---

# 18. `enumerate()`

ধরো:

```python
names = ["Rahim", "Karim", "Hasan"]
```

আমরা index এবং value দুটোই চাই।

পুরনো style:

```python
for i in range(len(names)):
    print(i, names[i])
```

Better:

```python
for index, name in enumerate(names):
    print(index, name)
```

Output:

```text
0 Rahim
1 Karim
2 Hasan
```

---

# 19. `enumerate()` Starting Index

Default:

```python
enumerate(names)
```

starts from `0`.

কিন্তু চাইলে:

```python
for index, name in enumerate(names, start=1):
    print(index, name)
```

Output:

```text
1 Rahim
2 Karim
3 Hasan
```

এটি অনেক Pythonic।

---

# 20. `zip()`

দুটি list একসাথে iterate করতে `zip()` খুব useful।

```python
names = ["Rahim", "Karim", "Hasan"]
scores = [80, 75, 90]

for name, score in zip(names, scores):
    print(name, score)
```

Output:

```text
Rahim 80
Karim 75
Hasan 90
```

Concept:

```text
names       scores
Rahim   →    80
Karim   →    75
Hasan   →    90
```

---

# 21. Multiple `zip()`

```python
names = ["Rahim", "Karim", "Hasan"]
scores = [80, 75, 90]
cities = ["Dhaka", "Chittagong", "Rajshahi"]

for name, score, city in zip(names, scores, cities):
    print(name, score, city)
```

---

# 22. `zip()`-এর গুরুত্বপূর্ণ বিষয়

যদি length আলাদা হয়:

```python
names = ["Rahim", "Karim", "Hasan"]
scores = [80, 75]
```

```python
for name, score in zip(names, scores):
    print(name, score)
```

শুধু matching পর্যন্ত যাবে:

```text
Rahim 80
Karim 75
```

`Hasan` বাদ যাবে।

---

# 23. `while` Loop

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

Output:

```text
1
2
3
4
5
```

Flow:

```text
count = 1
 ↓
1 <= 5 ? YES
 ↓
print
 ↓
count += 1
 ↓
2 <= 5 ?
 ↓
...
 ↓
6 <= 5 ? NO
 ↓
END
```

---

# 24. Infinite Loop

এটি dangerous:

```python
count = 1

while count <= 5:
    print(count)
```

কারণ `count` কখনো পরিবর্তন হচ্ছে না।

তাই condition সবসময়:

```text
True
```

হয়ে থাকবে।

সঠিক:

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

---

# 25. Counter Pattern

অনেক algorithm-এ count করতে হয়।

```python
numbers = [1, 2, 3, 4, 5]

count = 0

for number in numbers:
    count += 1

print(count)
```

Output:

```text
5
```

যদিও এখানে built-in:

```python
len(numbers)
```

ব্যবহার করা যায়, কিন্তু algorithm শেখার জন্য counter pattern জানা গুরুত্বপূর্ণ।

---

# 26. Counting Specific Values

ধরো:

```python
numbers = [1, 5, 3, 5, 7, 5, 2]
```

আমরা `5` কতবার আছে সেটা বের করব।

```python
count = 0

for number in numbers:
    if number == 5:
        count += 1

print(count)
```

Output:

```text
3
```

Algorithm:

```text
count = 0

প্রতিটি number:
    যদি target হয়:
        count বাড়াও
```

---

# 27. Accumulator Pattern

Accumulator হলো loop-এর মধ্যে result জমাতে থাকা।

```python
numbers = [10, 20, 30, 40]

total = 0

for number in numbers:
    total += number

print(total)
```

Output:

```text
100
```

Flow:

```text
total = 0

+10 → 10
+20 → 30
+30 → 60
+40 → 100
```

---

# 28. Average বের করা

```python
scores = [80, 70, 90, 60]

total = 0

for score in scores:
    total += score

average = total / len(scores)

print(average)
```

Output:

```text
75.0
```

---

# 29. Maximum খোঁজা

```python
numbers = [10, 45, 23, 89, 12]

maximum = numbers[0]

for number in numbers:
    if number > maximum:
        maximum = number

print(maximum)
```

Output:

```text
89
```

Algorithm:

```text
প্রথম element → current maximum

প্রতিটি পরের element:
    যদি বড় হয়:
        maximum update
```

---

# 30. Minimum খোঁজা

```python
numbers = [10, 45, 23, 89, 12]

minimum = numbers[0]

for number in numbers:
    if number < minimum:
        minimum = number

print(minimum)
```

Output:

```text
10
```

---

# 31. Searching

ধরো:

```python
numbers = [10, 20, 30, 40, 50]

target = 30
```

Search:

```python
found = False

for number in numbers:
    if number == target:
        found = True
        break

print(found)
```

Output:

```text
True
```

এটাকে basic **Linear Search** বলা হয়।

---

# 32. Linear Search

Algorithm:

```text
START
 ↓
প্রথম element
 ↓
target-এর সাথে compare
 ↓
match?
 ├── YES → found → STOP
 └── NO
      ↓
পরবর্তী element
      ↓
repeat
```

Python:

```python
numbers = [10, 20, 30, 40, 50]

target = 40

for number in numbers:
    if number == target:
        print("Found")
        break
else:
    print("Not Found")
```

---

# 33. `break`

`break` loop সম্পূর্ণ বন্ধ করে দেয়।

```python
for i in range(10):
    if i == 5:
        break

    print(i)
```

Output:

```text
0
1
2
3
4
```

---

# 34. `continue`

`continue` current iteration skip করে next iteration-এ যায়।

```python
for i in range(5):
    if i == 2:
        continue

    print(i)
```

Output:

```text
0
1
3
4
```

---

# 35. `break` বনাম `continue`

| Statement  | কাজ                         |
| ---------- | --------------------------- |
| `break`    | পুরো loop বন্ধ              |
| `continue` | শুধু current iteration skip |
| `pass`     | কিছু না করা                 |

---

# 36. Nested Loop

একটি loop-এর ভিতরে আরেকটি loop।

```python
for i in range(3):
    for j in range(3):
        print(i, j)
```

Output:

```text
0 0
0 1
0 2
1 0
1 1
1 2
2 0
2 1
2 2
```

Flow:

```text
i = 0
    j = 0
    j = 1
    j = 2

i = 1
    j = 0
    j = 1
    j = 2

i = 2
    j = 0
    j = 1
    j = 2
```

---

# 37. Nested Loop দিয়ে Pattern

```python
for i in range(5):
    for j in range(5):
        print("*", end=" ")

    print()
```

Output:

```text
* * * * *
* * * * *
* * * * *
* * * * *
* * * * *
```

---

# 38. Triangle Pattern

```python
for i in range(1, 6):
    for j in range(i):
        print("*", end=" ")

    print()
```

Output:

```text
*
* *
* * *
* * * *
* * * * *
```

এ ধরনের nested loop problem algorithm শেখার সময় খুব গুরুত্বপূর্ণ।

---

# 39. Nested List

AI/NLP data-তে nested list common।

```python
documents = [
    ["Python", "is", "easy"],
    ["AI", "is", "powerful"],
    ["Django", "is", "useful"]
]
```

সব word print:

```python
for document in documents:
    for word in document:
        print(word)
```

Output:

```text
Python
is
easy
AI
is
powerful
Django
is
useful
```

---

# 40. NLP Example — Word Counting

```python
text = "python is easy and python is powerful"

words = text.split()

count = 0

for word in words:
    if word == "python":
        count += 1

print(count)
```

Output:

```text
2
```

---

# 41. NLP Example — Long Words

```python
text = "Python makes artificial intelligence development easier"

words = text.split()

for word in words:
    if len(word) > 6:
        print(word)
```

Output:

```text
artificial
intelligence
development
```

এখানে loop + condition একসাথে ব্যবহার হচ্ছে।

---

# 42. AI Text Score Analysis

ধরো:

```python
sentences = [
    {"text": "AI is changing technology.", "score": 0.92},
    {"text": "I love Python.", "score": 0.21},
    {"text": "Machine learning is useful.", "score": 0.81}
]
```

High-score sentences:

```python
for sentence in sentences:
    if sentence["score"] >= 0.80:
        print(sentence["text"])
```

Output:

```text
AI is changing technology.
Machine learning is useful.
```

এ ধরনের loop পরবর্তীতে sentence-level text analysis system-এ খুব কাজে লাগবে।

---

# 43. Flag Pattern

কোনো condition পাওয়া গেছে কিনা track করতে flag ব্যবহার করা হয়।

```python
numbers = [10, 20, 30, 40]

found = False

for number in numbers:
    if number == 30:
        found = True
        break

print(found)
```

এখানে:

```text
found = False
```

মানে এখনো পাওয়া যায়নি।

পেলে:

```python
found = True
```

---

# 44. Loop `else`

Python-এর interesting feature:

```python
for number in range(5):
    print(number)
else:
    print("Loop completed")
```

Output:

```text
0
1
2
3
4
Loop completed
```

কিন্তু `break` হলে `else` execute হবে না:

```python
for number in range(5):
    if number == 2:
        break

    print(number)
else:
    print("Completed")
```

Output:

```text
0
1
```

কারণ loop `break` দিয়ে শেষ হয়েছে।

---

# 45. Search Algorithm + Loop `else`

এখানে loop `else` খুব সুন্দরভাবে ব্যবহার করা যায়:

```python
numbers = [10, 20, 30, 40]

target = 50

for number in numbers:
    if number == target:
        print("Found")
        break
else:
    print("Not Found")
```

Output:

```text
Not Found
```

---

# 46. `reversed()`

Sequence reverse order-এ iterate করতে:

```python
numbers = [1, 2, 3, 4, 5]

for number in reversed(numbers):
    print(number)
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

# 47. `sorted()` দিয়ে Loop

```python
numbers = [40, 10, 30, 20]

for number in sorted(numbers):
    print(number)
```

Output:

```text
10
20
30
40
```

মনে রাখবে:

```python
sorted(numbers)
```

নতুন sorted result দেয়।

---

# 48. `.sort()` বনাম `sorted()`

### `.sort()`

Original list পরিবর্তন করে:

```python
numbers = [40, 10, 30, 20]

numbers.sort()

print(numbers)
```

Output:

```text
[10, 20, 30, 40]
```

### `sorted()`

নতুন list দেয়:

```python
numbers = [40, 10, 30, 20]

new_numbers = sorted(numbers)

print(numbers)
print(new_numbers)
```

Output:

```text
[40, 10, 30, 20]
[10, 20, 30, 40]
```

---

# 49. Loop-এর সময় Collection Modify করা

এই ধরনের code avoid করো:

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers:
    if number % 2 == 0:
        numbers.remove(number)
```

কারণ iteration-এর সময় collection পরিবর্তন করলে unexpected behavior হতে পারে।

Better:

```python
numbers = [1, 2, 3, 4, 5]

odd_numbers = []

for number in numbers:
    if number % 2 != 0:
        odd_numbers.append(number)

print(odd_numbers)
```

Output:

```text
[1, 3, 5]
```

পরবর্তীতে **List Comprehension** দিয়ে আরও Pythonic way শিখব।

---

# 50. Off-by-One Error

Algorithm-এর সবচেয়ে common mistake।

```python
for i in range(1, 5):
    print(i)
```

Output:

```text
1
2
3
4
```

`5` আসবে না।

কারণ:

```text
range(start, stop)

start → included
stop  → excluded
```

---

# 51. Loop Algorithmic Thinking

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

একটি loop problem দেখলে নিজেকে ৫টি প্রশ্ন করো:

### Question 1

**আমি কী iterate করছি?**

```text
list?
string?
dictionary?
range?
nested data?
```

### Question 2

**প্রতিটি item-এর সঙ্গে কী করব?**

```text
compare?
count?
sum?
search?
modify?
```

### Question 3

**কোন variable result ধরে রাখবে?**

```text
count
total
maximum
minimum
found
result
```

### Question 4

**কখন loop বন্ধ হবে?**

```text
সব item শেষ?
target পাওয়া?
condition false?
```

### Question 5

**Time complexity কত?**

এটা আমরা পরবর্তী Algorithm milestones-এ বিস্তারিত করব।

---

# 52. একটি Algorithm চিন্তা করি

Problem:

> একটি list-এর মধ্যে কয়টি even number আছে?

Input:

```python
numbers = [10, 15, 22, 31, 40, 51]
```

প্রথমে English logic:

```text
count = 0

প্রতিটি number:
    যদি even হয়:
        count বাড়াও

return count
```

Python:

```python
numbers = [10, 15, 22, 31, 40, 51]

count = 0

for number in numbers:
    if number % 2 == 0:
        count += 1

print(count)
```

Output:

```text
3
```

এটাই basic algorithmic thinking।

---

# 53. আরেকটি Algorithm

Problem:

> একটি sentence-এর সবচেয়ে বড় word length বের করো।

```python
text = "Python is powerful programming language"

words = text.split()

maximum = 0

for word in words:
    if len(word) > maximum:
        maximum = len(word)

print(maximum)
```

Output:

```text
11
```

কারণ:

```text
programming → 11
```

---

# 54. Complete Example — AI Text Analyzer

```python
sentences = [
    {"text": "AI is changing the world.", "score": 0.91},
    {"text": "I enjoy programming.", "score": 0.25},
    {"text": "Machine learning is powerful.", "score": 0.84},
    {"text": "Python is fun.", "score": 0.18}
]

high_score_count = 0
low_score_count = 0

for sentence in sentences:

    score = sentence["score"]

    if score >= 0.80:
        high_score_count += 1

    else:
        low_score_count += 1

print("High:", high_score_count)
print("Low:", low_score_count)
```

Output:

```text
High: 2
Low: 2
```

এখানে আমরা ব্যবহার করেছি:

```text
list
dictionary
for loop
condition
counter
dictionary access
comparison
```

---

# 55. `enumerate()` + AI Example

Sentence-এর index দরকার হলে:

```python
sentences = [
    "AI is powerful.",
    "Python is useful.",
    "Django is popular."
]

for index, sentence in enumerate(sentences, start=1):
    print(f"{index}. {sentence}")
```

Output:

```text
1. AI is powerful.
2. Python is useful.
3. Django is popular.
```

---

# 56. `zip()` + AI Example

```python
sentences = [
    "AI is powerful.",
    "Python is useful.",
    "Django is popular."
]

scores = [0.91, 0.30, 0.75]

for sentence, score in zip(sentences, scores):
    print(sentence, "→", score)
```

Output:

```text
AI is powerful. → 0.91
Python is useful. → 0.3
Django is popular. → 0.75
```

---

# 57. Loop Performance — Basic Idea

ধরো:

```python
numbers = [1, 2, 3, ..., 1000]
```

একবার loop করলে:

```python
for number in numbers:
    ...
```

প্রায় 1000টি element process হবে।

এটা আমরা পরে বলব:

```text
O(n)
```

Nested loop:

```python
for i in numbers:
    for j in numbers:
        ...
```

প্রায়:

```text
n × n
```

operations হতে পারে।

এটা:

```text
O(n²)
```

এর দিকে যায়।

**Time Complexity** M02-এ আরও গভীরভাবে শেখা হবে।

---

# 58. Common Loop Mistakes

### Mistake 1 — Infinite loop

```python
x = 1

while x <= 10:
    print(x)
```

Problem:

```text
x পরিবর্তন হচ্ছে না
```

---

### Mistake 2 — Wrong range

```python
range(1, 10)
```

এখানে 10 নেই।

---

### Mistake 3 — ভুল indentation

```python
for i in range(5):
print(i)
```

Invalid।

সঠিক:

```python
for i in range(5):
    print(i)
```

---

### Mistake 4 — unnecessary index

Avoid:

```python
for i in range(len(numbers)):
    print(numbers[i])
```

যদি index প্রয়োজন না হয়।

Better:

```python
for number in numbers:
    print(number)
```

---

### Mistake 5 — collection modify করা

Loop চলাকালীন list modify করলে unexpected result হতে পারে।

---

# 59. কখন `for`, কখন `while`?

| Situation                    | Best choice     |
| ---------------------------- | --------------- |
| List-এর প্রতিটি item process | `for`           |
| String-এর character process  | `for`           |
| নির্দিষ্ট number of times    | `for + range()` |
| Condition-based repetition   | `while`         |
| User input validation        | `while`         |
| Search                       | `for`           |
| Infinite service loop        | `while`         |
| Iterator process             | `for`           |

---

# 60. Real-World Backend Example

ধরো API থেকে users এসেছে:

```python
users = [
    {"name": "Rahim", "active": True},
    {"name": "Karim", "active": False},
    {"name": "Hasan", "active": True}
]
```

Active users:

```python
for user in users:
    if user["active"]:
        print(user["name"])
```

Output:

```text
Rahim
Hasan
```

Backend development-এ এই ধরনের loop খুব common।

---

# 61. Real-World NLP Example

একটি paragraph:

```python
text = """
Artificial intelligence is growing rapidly.
Python is useful for AI development.
Machine learning requires data.
"""
```

Sentence process:

```python
sentences = text.strip().split(".")

for sentence in sentences:
    sentence = sentence.strip()

    if sentence:
        print(sentence)
```

Output:

```text
Artificial intelligence is growing rapidly
Python is useful for AI development
Machine learning requires data
```

এখানে future NLP pipeline-এর basic idea দেখা যাচ্ছে:

```text
Raw Text
   ↓
Split
   ↓
Individual Sentences
   ↓
Process Each Sentence
```

---

# 62. Mini Algorithm: Character Frequency

Problem:

> `"banana"`-তে `a` কয়বার আছে?

```python
text = "banana"

count = 0

for char in text:
    if char == "a":
        count += 1

print(count)
```

Output:

```text
3
```

---

# 63. Mini Algorithm: Vowel Count

```python
text = "programming"

vowels = "aeiou"

count = 0

for char in text:
    if char in vowels:
        count += 1

print(count)
```

Output:

```text
3
```

---

# 64. Mini Algorithm: Reverse String

Basic loop দিয়ে:

```python
text = "Python"

reverse = ""

for char in text:
    reverse = char + reverse

print(reverse)
```

Output:

```text
nohtyP
```

এখানে প্রতিটি iteration-এ নতুন result তৈরি হচ্ছে।

---

# 65. Mini Algorithm: Duplicate Detection

```python
numbers = [1, 2, 3, 2, 5]

seen = set()
duplicate = False

for number in numbers:

    if number in seen:
        duplicate = True
        break

    seen.add(number)

print(duplicate)
```

Output:

```text
True
```

এটি পরবর্তীতে **Hashing / Set-based algorithms** বোঝার জন্য useful হবে।

---

# 66. Practice Set — Level 1

নিজে code করবে।

### Problem 1

1 থেকে 100 পর্যন্ত print করো।

### Problem 2

1 থেকে 100 পর্যন্ত শুধু even numbers print করো।

### Problem 3

1 থেকে 100 পর্যন্ত odd numbers print করো।

### Problem 4

1 থেকে 100 পর্যন্ত sum বের করো।

### Problem 5

একটি number-এর multiplication table তৈরি করো।

Example:

```text
5 × 1 = 5
5 × 2 = 10
...
5 × 10 = 50
```

---

# 67. Practice Set — Level 2

### Problem 6

List-এর maximum বের করো।

```python
numbers = [23, 11, 56, 34, 78, 12]
```

### Problem 7

Minimum বের করো।

### Problem 8

Even number count করো।

### Problem 9

Odd number count করো।

### Problem 10

কোনো target list-এ আছে কিনা search করো।

---

# 68. Practice Set — Level 3

### Problem 11

একটি string-এর vowel count করো।

### Problem 12

String-এর consonant count করো।

### Problem 13

String reverse করো।

### Problem 14

একটি list-এ duplicate আছে কিনা detect করো।

### Problem 15

Sentence-এর longest word বের করো।

---

# 69. Practice Set — Level 4

এইগুলো algorithmic thinking develop করবে।

### Problem 16

```python
numbers = [10, 20, 10, 30, 20, 10]
```

প্রতিটি number কতবার এসেছে সেটা বের করো।

Expected concept:

```text
10 → 3
20 → 2
30 → 1
```

---

### Problem 17

একটি sentence-এ সবচেয়ে বেশি ব্যবহৃত word বের করো।

---

### Problem 18

একটি list sorted কিনা check করো।

Example:

```python
[1, 2, 3, 4, 5]
```

→ Sorted

```python
[1, 3, 2, 4]
```

→ Not Sorted

---

### Problem 19

দুটি list-এর common elements বের করো।

```python
a = [1, 2, 3, 4]
b = [3, 4, 5, 6]
```

Expected:

```text
3
4
```

---

### Problem 20

একটি list থেকে second largest number বের করো।

এখানে built-in `sort()` ব্যবহার না করে করার চেষ্টা করো।

---

# 70. Algorithm Challenge 🔥

একটি AI text analyzer তৈরি করো।

Input:

```python
sentences = [
    {"text": "Artificial intelligence is powerful.", "score": 0.92},
    {"text": "I like Python programming.", "score": 0.32},
    {"text": "Machine learning is transforming industries.", "score": 0.87},
    {"text": "Django is a web framework.", "score": 0.21}
]
```

তোমার program:

1. প্রতিটি sentence print করবে
2. score print করবে
3. score `>= 0.80` হলে `"High"`
4. score `< 0.80` হলে `"Low"`
5. total high score count করবে
6. total low score count করবে
7. highest score বের করবে
8. highest-score sentence বের করবে

Expected concept:

```text
Iteration
+
Condition
+
Counter
+
Accumulator
+
Maximum
+
Dictionary
```

এটা তোমার future AI writing platform-এর sentence-analysis logic-এর foundation হতে পারে।

---

# 71. Theory Questions

নিজে answer করার চেষ্টা করো।

### Q1

Iterable কী?

### Q2

Iterator কী?

### Q3

`iter()` কী করে?

### Q4

`next()` কী করে?

### Q5

`for` loop internally কীভাবে iterator ব্যবহার করে?

### Q6

`range(5)` কী values দেয়?

### Q7

`range(2, 10, 2)` কী values দেয়?

### Q8

`enumerate()` কেন ব্যবহার করা হয়?

### Q9

`zip()` কী করে?

### Q10

`break` এবং `continue`-এর পার্থক্য কী?

### Q11

`while` loop কখন ব্যবহার করবে?

### Q12

Infinite loop কী?

### Q13

Accumulator pattern কী?

### Q14

Flag variable কী?

### Q15

Linear Search কী?

### Q16

Nested loop কী?

### Q17

Loop `else` কখন execute হয়?

### Q18

Off-by-one error কী?

### Q19

Loop-এর মধ্যে list modify করা কেন problematic হতে পারে?

### Q20

একটি simple loop এবং nested loop-এর performance-এর মধ্যে পার্থক্য কী?

---

# 72. M01.06 Mental Model

এই পুরো lesson-এর core concept মনে রাখো:

```text
ITERATION
   │
   ├── Iterable
   │     ├── list
   │     ├── tuple
   │     ├── string
   │     ├── set
   │     ├── dict
   │     └── range
   │
   └── Iterator
          │
          ├── iter()
          │
          └── next()
```

তারপর:

```text
LOOP
 │
 ├── for
 │    ├── range()
 │    ├── enumerate()
 │    ├── zip()
 │    └── reversed()
 │
 └── while
```

আর algorithmic patterns:

```text
Loop
 │
 ├── Counter
 ├── Accumulator
 ├── Flag
 ├── Search
 ├── Min/Max
 ├── Frequency
 └── Nested Loop
```

---

# ✅ M01.06 Completion Checklist

এই lesson complete করার আগে নিশ্চিত হও তুমি পারো:

### Iteration Fundamentals

* [ ] Iteration explain করতে
* [ ] Iterable explain করতে
* [ ] Iterator explain করতে
* [ ] `iter()` ব্যবহার করতে
* [ ] `next()` ব্যবহার করতে
* [ ] `StopIteration` বুঝতে
* [ ] `for` loop-এর internal mechanism explain করতে

### Loops

* [ ] `for`
* [ ] `while`
* [ ] `range()`
* [ ] reverse range
* [ ] nested loops
* [ ] infinite loop identify করা
* [ ] off-by-one error identify করা

### Python Tools

* [ ] `enumerate()`
* [ ] `zip()`
* [ ] `reversed()`
* [ ] `sorted()`
* [ ] `.sort()`

### Algorithmic Patterns

* [ ] Counter
* [ ] Accumulator
* [ ] Flag
* [ ] Search
* [ ] Linear Search
* [ ] Min
* [ ] Max
* [ ] Frequency counting
* [ ] Nested-loop processing

### Control

* [ ] `break`
* [ ] `continue`
* [ ] `pass`
* [ ] loop `else`

### Practical

* [ ] List iteration
* [ ] Dictionary iteration
* [ ] String iteration
* [ ] Nested data iteration
* [ ] NLP text processing
* [ ] AI sentence-score processing

---

## 🎯 M01.06-এর মূল শিক্ষা

সবচেয়ে গুরুত্বপূর্ণ mental model:

```text
Collection
    ↓
Iterable
    ↓
Iterator
    ↓
next()
    ↓
One item
    ↓
Process
    ↓
Next item
    ↓
...
    ↓
StopIteration
```

আর algorithm-এর জন্য:

```text
Input
 ↓
Loop
 ↓
Condition / Processing
 ↓
Update Result
 ↓
Output
```

**M01.06 শেষ হলে তোমার Python loop foundation যথেষ্ট শক্ত হবে।** এরপর **M01.07 — Python Functions & Function Design Deep Dive**-এ যাব, যেখানে function definition, parameters, arguments, return, scope, default/keyword arguments, `*args`, `**kwargs`, recursion-এর foundation এবং reusable algorithm design বিস্তারিতভাবে শুরু হবে।


---
# 🚀 M01.07 — Python Functions & Function Design Deep Dive

আজ আমরা Python-এর **Functions** একদম foundation থেকে deep level পর্যন্ত শিখব।
এটা খুব গুরুত্বপূর্ণ, কারণ পরবর্তী সময়ে Algorithm, Django/DRF, AI/NLP—সব জায়গাতেই function ব্যবহার করবে।

আমাদের লক্ষ্য:

```text
Function
├── Definition
├── Calling
├── Parameters
├── Arguments
├── return
├── Default arguments
├── Keyword arguments
├── Positional arguments
├── *args
├── **kwargs
├── Scope
├── Local / Global
├── Nested functions
├── Recursion foundation
├── Function design
└── Algorithmic functions
```

---

# 1. Function কী?

**Function হলো reusable code block**, যেটা একটি নির্দিষ্ট কাজ করে।

ধরো বারবার:

```python
print("Hello")
```

লিখতে চাই না।

আমরা function তৈরি করতে পারি:

```python
def greet():
    print("Hello")
```

তারপর:

```python
greet()
```

Output:

```text
Hello
```

---

# 2. Function কেন ব্যবহার করব?

Function-এর প্রধান সুবিধা:

### 1. Reusability

একবার লিখে অনেকবার ব্যবহার করা যায়।

### 2. Organization

বড় program ছোট ছোট অংশে ভাগ করা যায়।

### 3. Maintainability

এক জায়গায় পরিবর্তন করলে সহজে maintain করা যায়।

### 4. Testing

একটি function আলাদাভাবে test করা যায়।

### 5. Abstraction

ভেতরের complexity hide করে শুধু প্রয়োজনীয় interface ব্যবহার করা যায়।

---

# 3. Function-এর Basic Structure

```python
def function_name():
    # code
```

Example:

```python
def greet():
    print("Hello")
```

এখানে:

```text
def
 ↓
function_name
 ↓
()
 ↓
:
 ↓
function body
```

---

# 4. Function Define করা বনাম Call করা

এটি খুব গুরুত্বপূর্ণ।

```python
def greet():
    print("Hello")
```

এখানে function **define** হয়েছে।

কিন্তু function execute হয়নি।

Execute করতে:

```python
greet()
```

এটাকে function **call/invoke** করা বলে।

---

# 5. Function Execution Flow

```python
def greet():
    print("Hello")

print("Start")

greet()

print("End")
```

Output:

```text
Start
Hello
End
```

Flow:

```text
Program start
     ↓
print Start
     ↓
greet()
     ↓
function body
     ↓
print Hello
     ↓
return
     ↓
print End
```

---

# 6. Function Parameters

Function-কে input দেওয়ার জন্য parameter ব্যবহার করা হয়।

```python
def greet(name):
    print("Hello", name)
```

এখানে:

```text
name = parameter
```

Call:

```python
greet("Atiar")
```

Output:

```text
Hello Atiar
```

---

# 7. Parameter বনাম Argument

এই distinction interview-এও আসে।

```python
def greet(name):
    print(name)
```

`name` হলো:

> Parameter

আর:

```python
greet("Atiar")
```

`"Atiar"` হলো:

> Argument

অর্থাৎ:

```text
Parameter → function definition-এর variable

Argument → function call-এর actual value
```

---

# 8. Multiple Parameters

```python
def add(a, b):
    print(a + b)
```

Call:

```python
add(10, 20)
```

Output:

```text
30
```

এখানে:

```text
a = 10
b = 20
```

---

# 9. `return`

Function থেকে result ফেরত পাঠাতে `return` ব্যবহার করা হয়।

```python
def add(a, b):
    return a + b
```

তারপর:

```python
result = add(10, 20)

print(result)
```

Output:

```text
30
```

---

# 10. `print()` বনাম `return`

এটা খুব গুরুত্বপূর্ণ।

### `print()`

শুধু output দেখায়:

```python
def add(a, b):
    print(a + b)
```

### `return`

Result caller-এর কাছে ফেরত দেয়:

```python
def add(a, b):
    return a + b
```

তাই:

```python
result = add(10, 20)
```

এরপর `result` ব্যবহার করা যাবে।

---

# 11. `return` Function-এর Execution বন্ধ করে

```python
def test():
    print("A")
    return
    print("B")
```

Call:

```python
test()
```

Output:

```text
A
```

`return`-এর পরের code execute হবে না।

---

# 12. Multiple Return Values

Python-এ:

```python
def calculate(a, b):
    total = a + b
    difference = a - b

    return total, difference
```

Call:

```python
result = calculate(10, 5)

print(result)
```

Output:

```text
(15, 5)
```

Python internally tuple return করছে।

Unpacking:

```python
total, difference = calculate(10, 5)

print(total)
print(difference)
```

---

# 13. Function Return না করলে কী হয়?

```python
def greet():
    print("Hello")
```

```python
result = greet()

print(result)
```

Output:

```text
Hello
None
```

অর্থাৎ function explicitly কিছু return না করলে Python:

```python
None
```

return করে।

---

# 14. Positional Arguments

```python
def introduce(name, age):
    print(name, age)
```

Call:

```python
introduce("Atiar", 25)
```

Mapping:

```text
name → Atiar
age  → 25
```

Position অনুযায়ী value assign হয়েছে।

---

# 15. Keyword Arguments

Name explicitly বলে দিতে পারি:

```python
introduce(name="Atiar", age=25)
```

এটি keyword argument।

আর order change করেও:

```python
introduce(age=25, name="Atiar")
```

কাজ করবে।

---

# 16. Positional + Keyword

```python
def user_info(name, age, city):
    print(name, age, city)
```

এভাবে:

```python
user_info("Atiar", age=25, city="Dhaka")
```

valid।

কিন্তু:

```python
user_info(name="Atiar", 25, city="Dhaka")
```

invalid।

কারণ positional argument keyword argument-এর পরে দেওয়া যায় না।

---

# 17. Default Parameter

কোনো parameter-এর default value দিতে পারি।

```python
def greet(name="Guest"):
    print("Hello", name)
```

এখন:

```python
greet()
```

Output:

```text
Hello Guest
```

আবার:

```python
greet("Atiar")
```

Output:

```text
Hello Atiar
```

---

# 18. Multiple Default Parameters

```python
def create_user(name, age=18, country="Bangladesh"):
    print(name, age, country)
```

```python
create_user("Atiar")
```

Output:

```text
Atiar 18 Bangladesh
```

---

# 19. Default Parameter-এর Rule

এটা ভুল:

```python
def test(a=10, b):
    pass
```

কারণ required parameter default parameter-এর পরে এসেছে।

সঠিক:

```python
def test(a, b=10):
    pass
```

Rule:

```text
Required parameters
        ↓
Default parameters
```

---

# 20. `*args`

যখন কতগুলো positional argument আসবে সেটা আগে থেকে জানা নেই, তখন `*args` ব্যবহার করতে পারি।

```python
def add(*numbers):
    total = 0

    for number in numbers:
        total += number

    return total
```

Call:

```python
print(add(10, 20))
print(add(10, 20, 30))
print(add(1, 2, 3, 4, 5))
```

Output:

```text
30
60
15
```

---

# 21. `args` আসলে কী?

```python
def test(*args):
    print(args)
```

```python
test(10, 20, 30)
```

Output:

```text
(10, 20, 30)
```

অর্থাৎ `args` একটি **tuple**।

```text
*args
  ↓
tuple
```

---

# 22. `**kwargs`

Variable number of keyword arguments গ্রহণ করতে:

```python
def user_info(**kwargs):
    print(kwargs)
```

Call:

```python
user_info(
    name="Atiar",
    age=25,
    city="Dhaka"
)
```

Output conceptually:

```python
{
    "name": "Atiar",
    "age": 25,
    "city": "Dhaka"
}
```

অর্থাৎ:

```text
**kwargs
   ↓
dictionary
```

---

# 23. `*args` + `**kwargs`

```python
def test(*args, **kwargs):
    print(args)
    print(kwargs)
```

Call:

```python
test(
    10,
    20,
    name="Atiar",
    age=25
)
```

Output:

```text
(10, 20)
{'name': 'Atiar', 'age': 25}
```

---

# 24. Parameter Order

Advanced function syntax-এ সাধারণভাবে:

```python
def function(
    positional,
    default=...,
    *args,
    keyword_only=...,
    **kwargs
):
    ...
```

উদাহরণ:

```python
def example(a, b=10, *args, c=20, **kwargs):
    print(a, b, args, c, kwargs)
```

---

# 25. Keyword-Only Parameter

`*` ব্যবহার করে keyword-only parameter তৈরি করা যায়।

```python
def create_user(name, *, age, city):
    print(name, age, city)
```

এখন:

```python
create_user(
    "Atiar",
    age=25,
    city="Dhaka"
)
```

valid।

কিন্তু:

```python
create_user("Atiar", 25, "Dhaka")
```

invalid।

কারণ `age` এবং `city` keyword হিসেবে দিতে হবে।

---

# 26. Positional-Only Parameter

Python-এ `/` ব্যবহার করে positional-only parameter define করা যায়।

```python
def add(a, b, /):
    return a + b
```

এখন:

```python
add(10, 20)
```

valid।

কিন্তু:

```python
add(a=10, b=20)
```

invalid।

কারণ `/`-এর আগের parameter positional-only।

---

# 27. Scope কী?

**Scope** হলো variable কোথা থেকে accessible।

Example:

```python
def test():
    x = 10
    print(x)

test()
```

এখানে `x` function-এর ভিতরে তৈরি হয়েছে।

Function-এর বাইরে:

```python
print(x)
```

করলে `NameError` হবে।

কারণ `x` local scope-এ আছে।

---

# 28. Local Variable

```python
def calculate():
    result = 100
    print(result)
```

`result` হলো local variable।

এটি function-এর বাইরে directly accessible নয়।

---

# 29. Global Variable

```python
x = 100

def test():
    print(x)

test()
```

Output:

```text
100
```

Function global variable read করতে পারে।

---

# 30. Local বনাম Global

```python
x = 100

def test():
    x = 50
    print(x)

test()

print(x)
```

Output:

```text
50
100
```

Function-এর local `x` global `x`-কে পরিবর্তন করেনি।

---

# 31. `global`

Global variable modify করতে:

```python
count = 0

def increase():
    global count
    count += 1

increase()

print(count)
```

Output:

```text
1
```

তবে সাধারণ application design-এ অপ্রয়োজনীয় global state avoid করা ভালো।

---

# 32. LEGB Rule

Python variable খোঁজার একটি গুরুত্বপূর্ণ rule:

```text
L → Local
E → Enclosing
G → Global
B → Built-in
```

অর্থাৎ:

```text
Local
 ↓
Enclosing
 ↓
Global
 ↓
Built-in
```

এটাই **LEGB**।

---

# 33. Built-in Scope

Python-এর built-in names:

```python
print()
len()
sum()
max()
min()
type()
range()
```

এগুলো built-in namespace-এর অংশ।

---

# 34. Nested Function

Function-এর ভিতরে function define করা যায়।

```python
def outer():

    def inner():
        print("Hello")

    inner()

outer()
```

Output:

```text
Hello
```

---

# 35. Function as Object

Python-এ function একটি object।

তাই:

```python
def greet():
    print("Hello")
```

আমরা:

```python
x = greet
```

করতে পারি।

তারপর:

```python
x()
```

Output:

```text
Hello
```

খেয়াল করো:

```python
x = greet
```

এখানে `()` নেই।

কারণ আমরা function call করছি না; function object-এর reference রাখছি।

---

# 36. Function Pass করা

একটি function অন্য function-এ argument হিসেবে দেওয়া যায়।

```python
def greet():
    print("Hello")

def execute(function):
    function()

execute(greet)
```

Output:

```text
Hello
```

এটাই Python-এর **first-class function** concept-এর foundation।

---

# 37. Lambda Function

ছোট anonymous function:

```python
square = lambda x: x * x
```

তারপর:

```python
print(square(5))
```

Output:

```text
25
```

Normal function:

```python
def square(x):
    return x * x
```

Lambda সাধারণত ছোট expression-এর জন্য বেশি useful।

---

# 38. Function Documentation — Docstring

Function কী করে সেটা document করতে:

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

তারপর:

```python
help(add)
```

ব্যবহার করা যায়।

---

# 39. Type Hints

Function-এর parameter ও return type document করা যায়:

```python
def add(a: int, b: int) -> int:
    return a + b
```

এটা Python-কে force করে না যে অবশ্যই `int` দিতে হবে।

এটা mainly:

```text
readability
IDE support
static analysis
documentation
```

এর জন্য useful।

---

# 40. AI/NLP Function Example

ধরো sentence-এর word count করতে চাই।

```python
def word_count(text):
    words = text.split()
    return len(words)
```

Call:

```python
text = "Artificial intelligence is powerful"

result = word_count(text)

print(result)
```

Output:

```text
5
```

---

# 41. Sentence Analyzer Function

```python
def analyze_sentence(text):
    words = text.split()

    return {
        "text": text,
        "word_count": len(words),
        "character_count": len(text)
    }
```

Call:

```python
result = analyze_sentence(
    "Python is useful for AI."
)

print(result)
```

Conceptually:

```text
{
    text: ...,
    word_count: ...,
    character_count: ...
}
```

এটাই ভবিষ্যতের AI writing platform-এর ছোট foundation।

---

# 42. Algorithm Function

Problem:

> একটি list-এর maximum number বের করো।

Function:

```python
def find_maximum(numbers):

    maximum = numbers[0]

    for number in numbers:
        if number > maximum:
            maximum = number

    return maximum
```

Call:

```python
numbers = [10, 50, 20, 90, 30]

result = find_maximum(numbers)

print(result)
```

Output:

```text
90
```

এখন algorithm reusable হয়েছে।

---

# 43. Search Function

```python
def linear_search(numbers, target):

    for number in numbers:
        if number == target:
            return True

    return False
```

Use:

```python
numbers = [10, 20, 30, 40]

print(linear_search(numbers, 30))
print(linear_search(numbers, 100))
```

Output:

```text
True
False
```

---

# 44. Function + Loop + Condition

একটি function-এর ভিতরে আমরা আগের lessons-এর concept combine করতে পারি:

```python
def count_even(numbers):

    count = 0

    for number in numbers:

        if number % 2 == 0:
            count += 1

    return count
```

Call:

```python
numbers = [1, 2, 3, 4, 5, 6]

print(count_even(numbers))
```

Output:

```text
3
```

এখন আমরা already তৈরি করেছি:

```text
Function
+
Parameter
+
Loop
+
Condition
+
Counter
+
Return
```

---

# 45. Pure Function

একটি গুরুত্বপূর্ণ software engineering concept:

**Pure function** সাধারণত:

1. একই input দিলে একই output দেয়
2. বাইরের state পরিবর্তন করে না

Example:

```python
def add(a, b):
    return a + b
```

Input:

```text
10, 20
```

Output সবসময়:

```text
30
```

---

# 46. Side Effect

Function যদি বাইরের state পরিবর্তন করে বা external কাজ করে, সেটা side effect হতে পারে।

```python
numbers = []

def add_number(number):
    numbers.append(number)
```

এখানে function বাইরের `numbers` পরিবর্তন করছে।

Backend development-এ side effects অবশ্যই থাকবে—যেমন:

```text
database write
file write
API request
email sending
```

কিন্তু এগুলো কোথায় হচ্ছে সেটা design-এর সময় পরিষ্কার রাখা গুরুত্বপূর্ণ।

---

# 47. Mutable Default Argument — Important Trap ⚠️

এই code:

```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

unexpected behavior করতে পারে।

কারণ default list function call-এর প্রতিবার নতুন করে তৈরি হয় না।

Better:

```python
def add_item(item, items=None):

    if items is None:
        items = []

    items.append(item)

    return items
```

এটা Python-এর খুব গুরুত্বপূর্ণ interview concept।

---

# 48. Function Design Principle

একটি function ideally একটি **clear responsibility** রাখবে।

খারাপ design:

```python
def process_everything():
    # database
    # validation
    # email
    # AI processing
    # payment
    # logging
```

Better:

```text
validate_user()
save_user()
generate_text()
send_email()
process_payment()
```

এটাকে সহজভাবে বলা যায়:

> One function → one clear responsibility.

---

# 49. Function Naming

Python convention:

```python
calculate_total()
find_maximum()
process_text()
analyze_sentence()
create_user()
```

সাধারণত:

```text
snake_case
```

ব্যবহার করা হয়।

Avoid:

```python
def x():
```

যদি function-এর purpose বোঝা না যায়।

---

# 50. Function-এর Ideal Structure

একটি ভালো function সাধারণত:

```python
def function_name(parameters):
    # validate
    # process
    # return result
```

Example:

```python
def calculate_average(scores):

    if not scores:
        return 0

    total = sum(scores)

    return total / len(scores)
```

এখানে empty input-এর জন্য guard রাখা হয়েছে।

---

# 51. Guard Clause

আগের lesson-এর concept function-এর সঙ্গে combine করা যায়।

```python
def process_user(user):

    if user is None:
        return

    if not user["active"]:
        return

    print("Processing user")
```

এতে unnecessary nesting কমে।

---

# 52. Recursion — Foundation

একটি function নিজেকেই call করলে তাকে **recursion** বলে।

Example:

```python
def countdown(n):

    if n == 0:
        return

    print(n)

    countdown(n - 1)
```

Call:

```python
countdown(5)
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

# 53. Recursion-এর দুইটি অংশ

প্রতিটি recursive function-এ সাধারণত:

```text
Base Case
+
Recursive Case
```

Example:

```python
def countdown(n):

    if n == 0:       # Base case
        return

    print(n)

    countdown(n - 1) # Recursive case
```

Base case না থাকলে infinite recursion হতে পারে।

---

# 54. Factorial Function

Mathematical definition:

```text
5! = 5 × 4 × 3 × 2 × 1
```

Recursive implementation:

```python
def factorial(n):

    if n == 0:
        return 1

    return n * factorial(n - 1)
```

```python
print(factorial(5))
```

Output:

```text
120
```

Recursion আমরা পরে **Algorithms**-এ আরও গভীরভাবে করব।

---

# 55. Function Composition

একটি function-এর output অন্য function-এর input হতে পারে।

```python
def clean_text(text):
    return text.strip().lower()

def word_count(text):
    return len(text.split())
```

তারপর:

```python
text = "  Python Is Powerful  "

cleaned = clean_text(text)
count = word_count(cleaned)

print(count)
```

Flow:

```text
Raw Text
   ↓
clean_text()
   ↓
Clean Text
   ↓
word_count()
   ↓
Result
```

এটাই NLP pipeline-এর basic idea।

---

# 56. AI Writing Platform-এর Perspective

তোমার future AI writing assistant-এ function architecture এমন হতে পারে:

```text
User Text
   ↓
validate_text()
   ↓
clean_text()
   ↓
split_sentences()
   ↓
analyze_text()
   ↓
generate_rewrites()
   ↓
rank_results()
   ↓
return_response()
```

প্রতিটি কাজ আলাদা function হলে system maintain করা সহজ হবে।

---

# 57. Practice — Beginner

### Problem 1

একটি function লেখো:

```python
greet()
```

যেটা:

```text
Hello, World!
```

print করবে।

---

### Problem 2

দুটি number যোগ করার function:

```python
add(a, b)
```

---

### Problem 3

একটি number even কিনা:

```python
is_even(n)
```

Expected:

```python
is_even(10)  # True
is_even(7)   # False
```

---

### Problem 4

একটি number-এর square:

```python
square(n)
```

---

### Problem 5

তিনটি number-এর maximum:

```python
maximum(a, b, c)
```

---

# 58. Practice — Intermediate

### Problem 6

List-এর sum বের করো:

```python
calculate_sum(numbers)
```

### Problem 7

List-এর even count:

```python
count_even(numbers)
```

### Problem 8

Linear search:

```python
search(numbers, target)
```

### Problem 9

String reverse:

```python
reverse_text(text)
```

### Problem 10

Word count:

```python
word_count(text)
```

---

# 59. Practice — Advanced

### Problem 11

একটি function লেখো যেটা sentence-এর:

```text
word count
character count
vowel count
```

return করবে।

---

### Problem 12

একটি function লেখো:

```python
find_second_largest(numbers)
```

`sort()` ব্যবহার করবে না।

---

### Problem 13

একটি function লেখো:

```python
is_palindrome(text)
```

Example:

```python
is_palindrome("madam")
```

→ `True`

---

### Problem 14

একটি function লেখো:

```python
frequency_count(numbers)
```

যেটা dictionary return করবে।

Example:

```python
[1, 2, 1, 3, 2, 1]
```

Result:

```python
{
    1: 3,
    2: 2,
    3: 1
}
```

---

# 60. M01.07 Challenge 🔥

একটি reusable **Text Analyzer** function তৈরি করো।

```python
def analyze_text(text):
    ...
```

Input:

```python
text = """
Artificial intelligence is changing the world.
Python is powerful for AI development.
Machine learning is useful.
"""
```

Function-এর output ideally:

```python
{
    "character_count": ...,
    "word_count": ...,
    "sentence_count": ...,
    "average_word_length": ...,
}
```

এখানে ব্যবহার করবে:

```text
Function
Parameters
Return
String
List
Loop
Condition
Counter
Accumulator
```

---

# 61. Theory Questions

নিজে answer করার চেষ্টা করো।

1. Function কী?
2. Function কেন ব্যবহার করা হয়?
3. Function define এবং call-এর পার্থক্য কী?
4. Parameter কী?
5. Argument কী?
6. Parameter ও argument-এর পার্থক্য কী?
7. `return` কী?
8. `print()` এবং `return`-এর পার্থক্য কী?
9. Function return না করলে কী হয়?
10. Positional argument কী?
11. Keyword argument কী?
12. Default parameter কী?
13. `*args` কী?
14. `**kwargs` কী?
15. `*args` কোন data type?
16. `**kwargs` কোন data type?
17. Local variable কী?
18. Global variable কী?
19. LEGB কী?
20. Nested function কী?
21. Function কি Python-এ object?
22. Lambda function কী?
23. Docstring কী?
24. Type hint কী?
25. Pure function কী?
26. Side effect কী?
27. Mutable default argument problem কী?
28. Guard clause কী?
29. Recursion কী?
30. Base case কী?
31. Recursive case কী?
32. Function composition কী?
33. একটি function-এ কেন অতিরিক্ত responsibility রাখা উচিত নয়?

---

# 62. M01.07 Final Mental Model

এখন Python program-এর structure এভাবে চিন্তা করো:

```text
                 PYTHON PROGRAM
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
     Data           Logic         Functions
        │              │              │
   list/dict/etc.   if/loop      reusable code
                       │              │
                       └──────┬───────┘
                              ↓
                           return
                              ↓
                           Result
```

আর function:

```text
Input
  ↓
Parameter
  ↓
Function
  ↓
Processing
  ↓
Return
  ↓
Output
```

Algorithm-এর perspective:

```text
Problem
  ↓
Break into functions
  ↓
Each function solves one task
  ↓
Combine functions
  ↓
Complete solution
```

---

# ✅ M01.07 Completion Checklist

### Function Basics

* [ ] Function কী
* [ ] Function define
* [ ] Function call
* [ ] Parameters
* [ ] Arguments
* [ ] `return`
* [ ] `print()` vs `return`
* [ ] Multiple return values

### Arguments

* [ ] Positional arguments
* [ ] Keyword arguments
* [ ] Default arguments
* [ ] `*args`
* [ ] `**kwargs`
* [ ] Keyword-only parameters
* [ ] Positional-only parameters

### Scope

* [ ] Local scope
* [ ] Global scope
* [ ] `global`
* [ ] LEGB
* [ ] Nested function

### Advanced Foundation

* [ ] Function as object
* [ ] Function as argument
* [ ] Lambda
* [ ] Docstring
* [ ] Type hints
* [ ] Pure function
* [ ] Side effects
* [ ] Mutable default argument problem
* [ ] Guard clause
* [ ] Function composition

### Algorithms

* [ ] Search function
* [ ] Maximum function
* [ ] Counter function
* [ ] Accumulator function
* [ ] Text analyzer
* [ ] Recursion foundation
* [ ] Base case
* [ ] Recursive case

---

## 🎯 M01.07-এর সবচেয়ে গুরুত্বপূর্ণ ৫টি বিষয়

এগুলো অবশ্যই ভালোভাবে বুঝবে:

```text
1. Parameter vs Argument
2. print() vs return
3. *args vs **kwargs
4. Local / Global / LEGB
5. Function → Input → Processing → Return
```

**M01.07 complete হলে Python-এর reusable-code foundation তৈরি হবে।** এরপর **M01.08 — Python Function Arguments, Scope, Lambda & Functional Programming Deep Dive**-এ আরও advanced function behavior, unpacking, closures, decorators-এর foundation, `map()`, `filter()`, `reduce()`, higher-order functions এবং functional programming concepts বিস্তারিতভাবে নেওয়া যাবে।


---
# 🚀 M01.08 — Python Advanced Functions & Functional Programming

আজকের lesson-এ আমরা **M01.07-এর function foundation** থেকে আরও advanced level-এ যাব।

এই lesson-এর মূল লক্ষ্য:

```text
Functions
├── Argument Unpacking
├── *args / **kwargs Deep Dive
├── Positional-only / Keyword-only
├── First-Class Functions
├── Higher-Order Functions
├── Lambda
├── map()
├── filter()
├── reduce()
├── sorted(key=...)
├── Closures
├── nonlocal
├── Decorators Foundation
├── Recursion Deep Dive
└── Functional Programming Concepts
```

এগুলো ভালোভাবে জানলে পরবর্তীতে **Django decorators, Python libraries, AI/NLP pipelines, callbacks এবং algorithm design** বুঝতে অনেক সহজ হবে।

---

# 1. Function আবার কেন গুরুত্বপূর্ণ?

ধরো তোমার AI writing system-এ:

```text
User Text
   ↓
clean_text()
   ↓
split_sentences()
   ↓
analyze_sentence()
   ↓
generate_rewrite()
   ↓
rank_results()
   ↓
return_result()
```

প্রতিটি কাজ আলাদা function হলে system manageable হয়।

তাই আমরা এখন function-কে শুধু "code block" হিসেবে না দেখে **first-class programming object** হিসেবে দেখব।

---

# 2. Argument Unpacking

আগের lesson-এ দেখেছি:

```python
def add(a, b):
    return a + b
```

এখন:

```python
numbers = [10, 20]

print(add(*numbers))
```

Output:

```text
30
```

এখানে:

```python
*numbers
```

list-এর elements unpack করেছে:

```text
[10, 20]
   ↓
10, 20
   ↓
add(10, 20)
```

---

# 3. List Unpacking

```python
numbers = [1, 2, 3]

a, b, c = numbers

print(a)
print(b)
print(c)
```

Output:

```text
1
2
3
```

---

# 4. Function Call-এ Unpacking

```python
def introduce(name, age, city):
    print(name, age, city)
```

Data:

```python
user = ["Atiar", 25, "Dhaka"]
```

Call:

```python
introduce(*user)
```

এটি equivalent:

```python
introduce("Atiar", 25, "Dhaka")
```

---

# 5. Dictionary Unpacking

ধরো:

```python
def create_user(name, age):
    print(name, age)
```

Data:

```python
user = {
    "name": "Atiar",
    "age": 25
}
```

Call:

```python
create_user(**user)
```

Equivalent:

```python
create_user(
    name="Atiar",
    age=25
)
```

---

# 6. `*args` Deep Dive

```python
def test(*args):
    print(args)
```

Call:

```python
test(10, 20, 30)
```

Output:

```text
(10, 20, 30)
```

অর্থাৎ:

```text
*args
  ↓
tuple
```

---

# 7. `**kwargs` Deep Dive

```python
def test(**kwargs):
    print(kwargs)
```

Call:

```python
test(
    name="Atiar",
    age=25,
    city="Dhaka"
)
```

Output:

```text
{
    "name": "Atiar",
    "age": 25,
    "city": "Dhaka"
}
```

অর্থাৎ:

```text
**kwargs
   ↓
dictionary
```

---

# 8. `*args` Iterate করা

```python
def calculate_sum(*numbers):

    total = 0

    for number in numbers:
        total += number

    return total
```

```python
print(calculate_sum(10, 20, 30, 40))
```

Output:

```text
100
```

---

# 9. `**kwargs` Iterate করা

```python
def print_user(**user):

    for key, value in user.items():
        print(key, "=", value)
```

Call:

```python
print_user(
    name="Atiar",
    age=25,
    city="Dhaka"
)
```

---

# 10. Mixed Arguments

```python
def example(name, *args, **kwargs):
    print(name)
    print(args)
    print(kwargs)
```

Call:

```python
example(
    "Atiar",
    10,
    20,
    age=25,
    city="Dhaka"
)
```

Output:

```text
Atiar
(10, 20)
{'age': 25, 'city': 'Dhaka'}
```

---

# 11. First-Class Function

Python-এ function একটি object।

তাই function:

* variable-এ রাখা যায়
* argument হিসেবে পাঠানো যায়
* return করা যায়
* collection-এ রাখা যায়

Example:

```python
def greet():
    return "Hello"
```

এখন:

```python
message = greet

print(message())
```

Output:

```text
Hello
```

---

# 12. Function List-এর মধ্যে রাখা

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


operations = [add, subtract]
```

এখন:

```python
print(operations[0](10, 5))
print(operations[1](10, 5))
```

Output:

```text
15
5
```

এটি powerful concept।

---

# 13. Higher-Order Function

যে function:

* অন্য function গ্রহণ করে অথবা
* function return করে

তাকে **Higher-Order Function** বলা হয়।

Example:

```python
def execute(function, value):
    return function(value)
```

তারপর:

```python
def square(x):
    return x * x
```

Call:

```python
result = execute(square, 5)

print(result)
```

Output:

```text
25
```

---

# 14. Function Return করা

একটি function অন্য function return করতে পারে।

```python
def create_multiplier(n):

    def multiplier(x):
        return x * n

    return multiplier
```

এখন:

```python
double = create_multiplier(2)

print(double(5))
```

Output:

```text
10
```

এখানে আমরা পৌঁছে গেলাম **closure** concept-এ।

---

# 15. Lambda Function

Lambda হলো ছোট anonymous function।

Normal:

```python
def square(x):
    return x * x
```

Lambda:

```python
square = lambda x: x * x
```

Call:

```python
print(square(5))
```

Output:

```text
25
```

---

# 16. Lambda Multiple Arguments

```python
add = lambda a, b: a + b

print(add(10, 20))
```

Output:

```text
30
```

---

# 17. Lambda কখন ব্যবহার করবে?

Lambda ভালো যখন:

```text
ছোট
+
simple
+
একবার/সীমিত জায়গায়
```

ব্যবহার করতে হবে।

খুব complex logic হলে normal `def` ব্যবহার করাই ভালো।

---

# 18. `map()`

`map()` একটি function-কে iterable-এর প্রতিটি element-এর উপর apply করে।

Example:

```python
numbers = [1, 2, 3, 4, 5]

result = map(lambda x: x * 2, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6, 8, 10]
```

Flow:

```text
1 → ×2 → 2
2 → ×2 → 4
3 → ×2 → 6
4 → ×2 → 8
5 → ×2 → 10
```

---

# 19. `map()` Normal Function দিয়ে

```python
def square(x):
    return x * x


numbers = [1, 2, 3, 4]

result = map(square, numbers)

print(list(result))
```

Output:

```text
[1, 4, 9, 16]
```

---

# 20. `map()` কী return করে?

Python 3-এ:

```python
map(...)
```

সরাসরি list return করে না।

এটি একটি **map iterator** return করে।

তাই:

```python
list(result)
```

ব্যবহার করে values দেখা হয়েছে।

---

# 21. `filter()`

`filter()` condition অনুযায়ী elements রাখে।

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(
    lambda x: x % 2 == 0,
    numbers
)

print(list(result))
```

Output:

```text
[2, 4, 6]
```

Flow:

```text
1 → False → বাদ
2 → True  → রাখ
3 → False → বাদ
4 → True  → রাখ
5 → False → বাদ
6 → True  → রাখ
```

---

# 22. `filter()` Normal Function দিয়ে

```python
def is_even(x):
    return x % 2 == 0


numbers = [1, 2, 3, 4, 5]

result = filter(is_even, numbers)

print(list(result))
```

---

# 23. `reduce()`

`reduce()` iterable-এর values একত্র করে একটি final result তৈরি করে।

এটি `functools` থেকে import করতে হয়।

```python
from functools import reduce
```

Example:

```python
numbers = [1, 2, 3, 4]

result = reduce(
    lambda a, b: a + b,
    numbers
)

print(result)
```

Output:

```text
10
```

Flow:

```text
1 + 2 = 3
3 + 3 = 6
6 + 4 = 10
```

---

# 24. `reduce()` দিয়ে Multiplication

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

result = reduce(
    lambda a, b: a * b,
    numbers
)

print(result)
```

Output:

```text
120
```

---

# 25. `map()` বনাম `filter()` বনাম `reduce()`

| Function   | কাজ                        |
| ---------- | -------------------------- |
| `map()`    | প্রতিটি item transform     |
| `filter()` | condition অনুযায়ী select   |
| `reduce()` | সব item combine করে result |

Mental model:

```text
map
Input → Transform → Output collection

filter
Input → Condition → Selected collection

reduce
Input → Combine → Single result
```

---

# 26. `sorted(key=...)`

এটি অত্যন্ত গুরুত্বপূর্ণ।

ধরো:

```python
users = [
    {"name": "Rahim", "age": 30},
    {"name": "Karim", "age": 20},
    {"name": "Hasan", "age": 25}
]
```

Age অনুযায়ী sort:

```python
users_sorted = sorted(
    users,
    key=lambda user: user["age"]
)
```

Result:

```text
Karim → 20
Hasan → 25
Rahim → 30
```

---

# 27. Reverse Sorting

```python
users_sorted = sorted(
    users,
    key=lambda user: user["age"],
    reverse=True
)
```

এখন:

```text
Rahim → 30
Hasan → 25
Karim → 20
```

---

# 28. AI/NLP Example — Sentence Ranking

```python
sentences = [
    {"text": "Python is useful.", "score": 0.40},
    {"text": "AI is powerful.", "score": 0.90},
    {"text": "Django is popular.", "score": 0.70}
]
```

Score অনুযায়ী:

```python
ranked = sorted(
    sentences,
    key=lambda item: item["score"],
    reverse=True
)
```

এখন highest score প্রথমে থাকবে।

AI system-এ candidate ranking-এর basic idea এখান থেকেই আসে।

---

# 29. Closure কী?

Closure হলো nested function-এর এমন behavior যেখানে inner function তার outer function-এর variable মনে রাখতে পারে।

Example:

```python
def multiplier(n):

    def multiply(x):
        return x * n

    return multiply
```

এখন:

```python
double = multiplier(2)
triple = multiplier(3)
```

তারপর:

```python
print(double(10))
print(triple(10))
```

Output:

```text
20
30
```

`double` মনে রাখছে:

```text
n = 2
```

আর `triple` মনে রাখছে:

```text
n = 3
```

---

# 30. Closure Mental Model

```text
multiplier(2)
     ↓
  n = 2
     ↓
multiply()
     ↓
closure
     ↓
double()
```

অর্থাৎ inner function outer scope-এর value ধরে রাখে।

---

# 31. `nonlocal`

Nested function-এর outer variable modify করতে `nonlocal` ব্যবহার করা হয়।

```python
def counter():

    count = 0

    def increase():
        nonlocal count
        count += 1
        return count

    return increase
```

Use:

```python
c = counter()

print(c())
print(c())
print(c())
```

Output:

```text
1
2
3
```

এখানে `count` outer function-এর variable।

---

# 32. Decorator কী?

Decorator হলো এমন function যা অন্য function-এর behavior modify বা extend করে।

Basic idea:

```text
Original Function
       ↓
   Decorator
       ↓
Enhanced Function
```

Example:

```python
def decorator(function):

    def wrapper():
        print("Before")
        function()
        print("After")

    return wrapper
```

তারপর:

```python
@decorator
def greet():
    print("Hello")
```

Call:

```python
greet()
```

Output:

```text
Before
Hello
After
```

---

# 33. `@decorator` কী করছে?

এই:

```python
@decorator
def greet():
    print("Hello")
```

conceptually:

```python
def greet():
    print("Hello")

greet = decorator(greet)
```

এটা খুব গুরুত্বপূর্ণ।

Django-তে decorators অনেক জায়গায় দেখতে পাবে।

---

# 34. Decorator with Arguments

Real functions arguments নিতে পারে।

```python
def decorator(function):

    def wrapper(*args, **kwargs):
        print("Before")

        result = function(*args, **kwargs)

        print("After")

        return result

    return wrapper
```

এখানে:

```python
*args
**kwargs
```

ব্যবহার করার কারণ হলো original function-এর বিভিন্ন ধরনের arguments support করা।

---

# 35. Practical Decorator — Logging

```python
def log_call(function):

    def wrapper(*args, **kwargs):
        print("Calling:", function.__name__)

        result = function(*args, **kwargs)

        print("Finished:", function.__name__)

        return result

    return wrapper
```

Use:

```python
@log_call
def add(a, b):
    return a + b
```

Call:

```python
print(add(10, 20))
```

Conceptually:

```text
Calling: add
Finished: add
30
```

---

# 36. `functools.wraps`

Decorator তৈরি করার সময় metadata preserve করার জন্য:

```python
from functools import wraps
```

তারপর:

```python
def log_call(function):

    @wraps(function)
    def wrapper(*args, **kwargs):
        print("Calling function")

        return function(*args, **kwargs)

    return wrapper
```

এটি professional Python code-এ useful।

---

# 37. Recursion Deep Dive

Recursion:

> একটি function নিজেকেই call করে।

Example:

```python
def countdown(n):

    if n == 0:
        return

    print(n)

    countdown(n - 1)
```

Call:

```python
countdown(3)
```

Flow:

```text
countdown(3)
   ↓
countdown(2)
   ↓
countdown(1)
   ↓
countdown(0)
   ↓
return
```

---

# 38. Recursion-এর Base Case

Base case না থাকলে:

```python
def test():
    test()
```

এটি infinite recursion তৈরি করবে।

Python eventually:

```text
RecursionError
```

দেবে।

---

# 39. Factorial Recursion

```python
def factorial(n):

    if n == 0:
        return 1

    return n * factorial(n - 1)
```

`factorial(4)`:

```text
4 × factorial(3)
    ↓
4 × 3 × factorial(2)
    ↓
4 × 3 × 2 × factorial(1)
    ↓
4 × 3 × 2 × 1
    ↓
24
```

---

# 40. Recursion vs Loop

একই কাজ loop দিয়ে:

```python
def factorial(n):

    result = 1

    for i in range(1, n + 1):
        result *= i

    return result
```

Recursion:

```python
def factorial(n):

    if n == 0:
        return 1

    return n * factorial(n - 1)
```

দুটোই valid।

Python-এ সাধারণ repetition-এর ক্ষেত্রে loop অনেক সময় বেশি practical, কারণ recursion-এর call-stack overhead এবং recursion-depth limitation আছে।

---

# 41. Functional Programming কী?

Functional programming একটি programming paradigm যেখানে computation-কে function composition এবং data transformation-এর মাধ্যমে ভাবা হয়।

Common concepts:

```text
Pure Functions
Immutability
First-Class Functions
Higher-Order Functions
Function Composition
map()
filter()
reduce()
```

Python পুরোপুরি functional language নয়; এটি multi-paradigm language।

---

# 42. Pure Function Example

```python
def square(x):
    return x * x
```

একই input:

```python
square(5)
```

সবসময়:

```text
25
```

দেবে।

---

# 43. Function Composition

ধরো:

```python
def clean(text):
    return text.strip().lower()


def word_count(text):
    return len(text.split())
```

তারপর:

```python
text = "  Python Is Powerful  "

cleaned = clean(text)

result = word_count(cleaned)

print(result)
```

Flow:

```text
Raw Text
   ↓
clean()
   ↓
Clean Text
   ↓
word_count()
   ↓
Result
```

---

# 44. AI/NLP Pipeline

এই concept future project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

```text
Raw Text
    ↓
clean_text()
    ↓
normalize_text()
    ↓
split_sentences()
    ↓
tokenize()
    ↓
analyze()
    ↓
generate()
    ↓
rank()
    ↓
final output
```

প্রতিটি stage আলাদা function হতে পারে।

---

# 45. `map()` + NLP

ধরো:

```python
sentences = [
    "  Python Is Powerful  ",
    " AI Is Useful ",
    "Django Is Great"
]
```

Clean করতে:

```python
cleaned = map(
    lambda text: text.strip().lower(),
    sentences
)

print(list(cleaned))
```

Output:

```text
[
    "python is powerful",
    "ai is useful",
    "django is great"
]
```

---

# 46. `filter()` + NLP

Long sentence select:

```python
sentences = [
    "Python is great",
    "Artificial intelligence is changing the world",
    "AI is useful"
]
```

```python
long_sentences = filter(
    lambda text: len(text.split()) > 4,
    sentences
)

print(list(long_sentences))
```

---

# 47. `map()` + `filter()` Together

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = filter(
    lambda x: x % 2 == 0,
    numbers
)

squared = map(
    lambda x: x * x,
    even_numbers
)

print(list(squared))
```

Output:

```text
[4, 16, 36]
```

Flow:

```text
[1,2,3,4,5,6]
      ↓
   filter
      ↓
 [2,4,6]
      ↓
    map
      ↓
 [4,16,36]
```

---

# 48. কখন List Comprehension Better?

আগের code:

```python
squared = map(
    lambda x: x * x,
    filter(lambda x: x % 2 == 0, numbers)
)
```

এটা তুলনামূলকভাবে difficult to read।

Python-এ অনেক ক্ষেত্রে:

```python
result = [
    x * x
    for x in numbers
    if x % 2 == 0
]
```

আরও readable।

List comprehension আমরা পরবর্তী lesson-এ deep dive করব।

---

# 49. Algorithm Design with Functions

একটি বড় problem:

> Text-এর longest word বের করো।

একটি function:

```python
def longest_word(text):

    words = text.split()

    longest = ""

    for word in words:
        if len(word) > len(longest):
            longest = word

    return longest
```

Test:

```python
text = "Python makes artificial intelligence powerful"

print(longest_word(text))
```

Output:

```text
intelligence
```

এখন algorithm একটি reusable function হয়ে গেছে।

---

# 50. Function Decomposition

বড় text analyzer এক function-এ না লিখে:

```python
def clean_text(text):
    ...


def split_sentences(text):
    ...


def count_words(text):
    ...


def analyze_sentence(sentence):
    ...


def generate_report(data):
    ...
```

তারপর:

```python
def analyze_text(text):

    text = clean_text(text)

    sentences = split_sentences(text)

    data = []

    for sentence in sentences:
        data.append(
            analyze_sentence(sentence)
        )

    return generate_report(data)
```

এটাই **function decomposition**।

---

# 51. Practice — Level 1

নিজে solve করবে।

### Problem 1

`*args` ব্যবহার করে সব number-এর sum বের করো।

```python
sum_all(10, 20, 30, 40)
```

Expected:

```text
100
```

---

### Problem 2

`**kwargs` ব্যবহার করে user information print করো।

---

### Problem 3

একটি function তৈরি করো যেটা অন্য function argument হিসেবে নেয়।

---

### Problem 4

Lambda দিয়ে:

```text
square
cube
addition
```

তৈরি করো।

---

# 52. Practice — Level 2

### Problem 5

`map()` ব্যবহার করে:

```python
[1, 2, 3, 4, 5]
```

কে square করো।

---

### Problem 6

`filter()` ব্যবহার করে শুধু odd numbers রাখো।

---

### Problem 7

`reduce()` দিয়ে list-এর product বের করো।

---

### Problem 8

`sorted(key=...)` ব্যবহার করে students-কে score অনুযায়ী descending order-এ সাজাও।

```python
students = [
    {"name": "A", "score": 70},
    {"name": "B", "score": 90},
    {"name": "C", "score": 80}
]
```

---

# 53. Practice — Level 3

### Problem 9 — Closure

একটি function তৈরি করো:

```python
create_power(n)
```

যেটা এমন function return করবে:

```python
square = create_power(2)
cube = create_power(3)
```

Expected:

```python
square(5)  # 25
cube(5)    # 125
```

---

### Problem 10 — Decorator

একটি decorator তৈরি করো যেটা function call-এর আগে:

```text
"Starting..."
```

এবং পরে:

```text
"Finished..."
```

print করবে।

---

# 54. Practice — Level 4

### Problem 11

একটি function:

```python
analyze_text(text)
```

তৈরি করো।

Return করবে:

```python
{
    "word_count": ...,
    "character_count": ...,
    "vowel_count": ...,
    "longest_word": ...
}
```

---

### Problem 12

Function composition ব্যবহার করে:

```text
clean
→ tokenize
→ analyze
```

pipeline তৈরি করো।

---

# 55. M01.08 Challenge 🔥

একটি mini **AI Text Analysis Pipeline** বানাও।

Input:

```python
text = """
Artificial intelligence is changing the world.
Python is useful for machine learning.
Django is powerful for backend development.
"""
```

তোমার functions হবে:

```python
clean_text()
split_sentences()
word_count()
average_word_length()
longest_word()
analyze_sentence()
```

শেষে:

```python
analyze_text(text)
```

একটি structured dictionary return করবে।

Architecture:

```text
                 analyze_text()
                       │
                       ↓
                  clean_text()
                       │
                       ↓
               split_sentences()
                       │
                       ↓
              ┌────────┴────────┐
              ↓                 ↓
      analyze_sentence()   analyze_sentence()
              │                 │
              └────────┬────────┘
                       ↓
                  final result
```

এখানে লক্ষ্য হলো **একটি বড় function না লিখে ছোট reusable functions দিয়ে system design করা।**

---

# 🧠 M01.08 Core Mental Model

এই lesson-এর সবচেয়ে গুরুত্বপূর্ণ structure:

```text
FUNCTION
   │
   ├── First-Class Object
   │
   ├── Can receive function
   │       ↓
   │   Higher-Order Function
   │
   ├── Can return function
   │       ↓
   │    Closure
   │
   ├── Can wrap function
   │       ↓
   │    Decorator
   │
   └── Can transform data
           │
           ├── map()
           ├── filter()
           └── reduce()
```

Argument flow:

```text
*args
  ↓
tuple

**kwargs
  ↓
dictionary

*list
  ↓
positional unpacking

**dict
  ↓
keyword unpacking
```

---

# ✅ M01.08 Completion Checklist

### Arguments

* [ ] `*args`
* [ ] `**kwargs`
* [ ] `*` unpacking
* [ ] `**` unpacking
* [ ] positional-only
* [ ] keyword-only

### Functional Concepts

* [ ] First-class function
* [ ] Higher-order function
* [ ] Lambda
* [ ] `map()`
* [ ] `filter()`
* [ ] `reduce()`
* [ ] `sorted(key=...)`

### Advanced Functions

* [ ] Nested functions
* [ ] Closure
* [ ] `nonlocal`
* [ ] Decorator
* [ ] `@decorator`
* [ ] `functools.wraps`

### Recursion

* [ ] Recursive function
* [ ] Base case
* [ ] Recursive case
* [ ] Factorial
* [ ] Recursion vs loop

### Software Design

* [ ] Pure function
* [ ] Side effects
* [ ] Function composition
* [ ] Function decomposition
* [ ] AI/NLP pipeline design

---

## 🎯 M01.08-এর 7টি অবশ্যই জানা Concept

```text
1. *args / **kwargs
2. Argument unpacking
3. First-class functions
4. Higher-order functions
5. map / filter / reduce
6. Closures + decorators
7. Function decomposition
```

এগুলো আয়ত্ত হলে Python-এর **function system** অনেক শক্ত হয়ে যাবে। এরপর **M01.09 — Python Data Structures & Comprehensions Deep Dive**-এ `list`, `dict`, `set` comprehension, nested comprehension, conditional comprehension, generator expression এবং practical data transformation শেখা হবে—যা AI/NLP data processing-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।


---
# M01.09 — Python Data Structures & Comprehensions Deep Dive

আজকের lesson-এ আমরা Python-এর **List, Tuple, Set, Dictionary এবং Comprehension** খুব গভীরভাবে শিখব। যেহেতু তোমার লক্ষ্য পরে **AI/NLP + AI writing platform** বানানো, তাই examples-গুলো সেদিকেও relate করব।

---

# 1. Data Structure কী?

Data structure হলো এমন একটি উপায় যার মাধ্যমে আমরা data **store, organize এবং process** করি।

Python-এর গুরুত্বপূর্ণ built-in data structures:

```text
List       → ordered + mutable
Tuple      → ordered + immutable
Set        → unique + unordered
Dictionary → key-value
```

উদাহরণ:

```python
numbers = [10, 20, 30]

point = (10, 20)

unique_numbers = {10, 20, 30}

user = {
    "name": "Atiar",
    "age": 25
}
```

---

# 2. কোন Data Structure কখন ব্যবহার করব?

| Requirement                 | Structure |
| --------------------------- | --------- |
| Ordered changing data       | `list`    |
| Fixed ordered data          | `tuple`   |
| Unique values               | `set`     |
| Key-value data              | `dict`    |
| Fast membership checking    | `set`     |
| Structured object-like data | `dict`    |

AI/NLP example:

```python
tokens = ["AI", "is", "changing", "the", "world"]
```

এখানে `list` ভালো।

Unique words:

```python
unique_words = {"AI", "is", "changing", "the", "world"}
```

এখানে `set` ভালো।

Word frequency:

```python
frequency = {
    "AI": 5,
    "Python": 10,
    "data": 7
}
```

এখানে `dict` ভালো।

---

# 3. List Deep Dive

List হলো:

* ordered
* mutable
* duplicate allowed
* indexed

```python
numbers = [10, 20, 30, 40]
```

## Indexing

```python
numbers[0]
```

Output:

```text
10
```

শেষ element:

```python
numbers[-1]
```

Output:

```text
40
```

---

# 4. List Slicing

```python
numbers = [10, 20, 30, 40, 50]
```

```python
print(numbers[1:4])
```

Output:

```text
[20, 30, 40]
```

Syntax:

```text
list[start:stop:step]
```

Example:

```python
print(numbers[::2])
```

Output:

```text
[10, 30, 50]
```

Reverse:

```python
print(numbers[::-1])
```

---

# 5. List Add Operations

## append()

শেষে একটি item:

```python
numbers = [1, 2, 3]

numbers.append(4)

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

## extend()

একাধিক item:

```python
numbers = [1, 2]

numbers.extend([3, 4, 5])

print(numbers)
```

Output:

```text
[1, 2, 3, 4, 5]
```

Difference:

```python
numbers = [1, 2]

numbers.append([3, 4])

print(numbers)
```

Output:

```text
[1, 2, [3, 4]]
```

কিন্তু:

```python
numbers = [1, 2]

numbers.extend([3, 4])

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

# 6. insert()

নির্দিষ্ট position-এ add:

```python
numbers = [1, 2, 4]

numbers.insert(2, 3)

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

# 7. List Remove Operations

### remove()

Value দিয়ে remove:

```python
numbers = [10, 20, 30]

numbers.remove(20)

print(numbers)
```

---

### pop()

Index দিয়ে remove এবং value return করে:

```python
numbers = [10, 20, 30]

x = numbers.pop()

print(x)
```

Output:

```text
30
```

Specific index:

```python
x = numbers.pop(0)
```

---

### del

```python
numbers = [10, 20, 30]

del numbers[1]
```

---

### clear()

```python
numbers.clear()
```

সব item remove করবে।

---

# 8. List Search

```python
numbers = [10, 20, 30, 40]
```

Membership:

```python
print(20 in numbers)
```

Output:

```text
True
```

Index:

```python
print(numbers.index(30))
```

Output:

```text
2
```

Count:

```python
numbers = [10, 20, 10, 30, 10]

print(numbers.count(10))
```

Output:

```text
3
```

---

# 9. Sorting

```python
numbers = [5, 2, 8, 1]

numbers.sort()

print(numbers)
```

Output:

```text
[1, 2, 5, 8]
```

Descending:

```python
numbers.sort(reverse=True)
```

---

## sorted()

`sorted()` নতুন list তৈরি করে।

```python
numbers = [5, 2, 8, 1]

result = sorted(numbers)

print(numbers)
print(result)
```

`numbers` unchanged থাকবে।

---

# 10. Tuple Deep Dive

Tuple হলো:

```text
ordered
immutable
duplicate allowed
indexed
```

```python
point = (10, 20)
```

Access:

```python
print(point[0])
```

---

## Tuple unpacking

```python
person = ("Atiar", 25)

name, age = person

print(name)
print(age)
```

---

## Extended unpacking

```python
numbers = (1, 2, 3, 4, 5)

first, *middle, last = numbers

print(first)
print(middle)
print(last)
```

Output:

```text
1
[2, 3, 4]
5
```

---

# 11. Tuple কেন ব্যবহার করব?

যখন data পরিবর্তন করা উচিত নয়।

উদাহরণ:

```python
coordinates = (23.8103, 90.4125)
```

অথবা:

```python
RGB = (255, 255, 255)
```

Fixed configuration data-এর জন্য tuple useful।

---

# 12. Set Deep Dive

Set-এর সবচেয়ে গুরুত্বপূর্ণ বৈশিষ্ট্য:

> Duplicate রাখে না।

```python
numbers = {1, 2, 3, 3, 3}

print(numbers)
```

Output:

```text
{1, 2, 3}
```

---

# 13. Set Add

```python
numbers = {1, 2, 3}

numbers.add(4)
```

---

Multiple:

```python
numbers.update([5, 6, 7])
```

---

# 14. Set Remove

```python
numbers.remove(2)
```

কিন্তু value না থাকলে error হবে।

```python
numbers.discard(2)
```

`discard()` value না থাকলেও error দেয় না।

---

# 15. Mathematical Set Operations

ধরি:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
```

## Union

```python
print(A | B)
```

Output:

```text
{1, 2, 3, 4, 5, 6}
```

অথবা:

```python
A.union(B)
```

---

## Intersection

Common elements:

```python
print(A & B)
```

Output:

```text
{3, 4}
```

---

## Difference

```python
print(A - B)
```

Output:

```text
{1, 2}
```

---

## Symmetric Difference

দুই set-এ আছে কিন্তু common নয়:

```python
print(A ^ B)
```

Output:

```text
{1, 2, 5, 6}
```

---

# 16. Set-এর AI/NLP Use Case

ধরি দুই document-এর words:

```python
doc1 = {"AI", "Python", "Machine", "Learning"}

doc2 = {"AI", "Python", "Data", "Science"}
```

Common words:

```python
common = doc1 & doc2

print(common)
```

Output:

```text
{'AI', 'Python'}
```

এটা document similarity-এর basic idea বুঝতে সাহায্য করবে।

---

# 17. Dictionary Deep Dive

Dictionary:

```python
user = {
    "name": "Atiar",
    "age": 25,
    "country": "Bangladesh"
}
```

Structure:

```text
key → value
```

---

# 18. Dictionary Access

```python
print(user["name"])
```

Output:

```text
Atiar
```

আরেকটি method:

```python
print(user.get("name"))
```

---

## Difference

```python
user["email"]
```

Key না থাকলে:

```text
KeyError
```

কিন্তু:

```python
user.get("email")
```

Output:

```text
None
```

Default:

```python
user.get("email", "Not Found")
```

---

# 19. Dictionary Add / Update

```python
user["email"] = "atiar@example.com"
```

Existing key update:

```python
user["age"] = 26
```

Multiple:

```python
user.update({
    "age": 26,
    "city": "Dhaka"
})
```

---

# 20. Dictionary Remove

```python
user.pop("age")
```

Last item:

```python
user.popitem()
```

Delete:

```python
del user["city"]
```

সব:

```python
user.clear()
```

---

# 21. Dictionary keys(), values(), items()

```python
user = {
    "name": "Atiar",
    "age": 25
}
```

Keys:

```python
print(user.keys())
```

Values:

```python
print(user.values())
```

Both:

```python
print(user.items())
```

Loop:

```python
for key, value in user.items():
    print(key, value)
```

---

# 22. Nested Data Structures

Real-world applications-এ nested structure খুব গুরুত্বপূর্ণ।

```python
users = [
    {
        "name": "Atiar",
        "age": 25
    },
    {
        "name": "Rahim",
        "age": 30
    }
]
```

Access:

```python
print(users[0]["name"])
```

Output:

```text
Atiar
```

---

# 23. AI/NLP Nested Data

```python
document = {
    "title": "AI Introduction",
    "sentences": [
        {
            "text": "AI is powerful.",
            "score": 0.91
        },
        {
            "text": "Python is useful.",
            "score": 0.32
        }
    ]
}
```

Access:

```python
print(document["sentences"][0]["text"])
```

Output:

```text
AI is powerful.
```

---

# 24. এবার আসি Comprehension-এ

Python comprehension হলো concise way-তে collection তৈরি করার technique।

Traditional loop:

```python
numbers = []

for i in range(1, 6):
    numbers.append(i * 2)

print(numbers)
```

Output:

```text
[2, 4, 6, 8, 10]
```

Comprehension:

```python
numbers = [i * 2 for i in range(1, 6)]
```

---

# 25. List Comprehension Syntax

General structure:

```python
[expression for item in iterable]
```

Example:

```python
squares = [x ** 2 for x in range(1, 6)]
```

Output:

```text
[1, 4, 9, 16, 25]
```

Mental model:

```text
[ expression   for   item   in   iterable ]
       ↓             ↓          ↓
      কী হবে       variable    কোথা থেকে
```

---

# 26. Conditional List Comprehension

Syntax:

```python
[expression for item in iterable if condition]
```

Example:

```python
even = [x for x in range(10) if x % 2 == 0]
```

Output:

```text
[0, 2, 4, 6, 8]
```

---

# 27. Mapping + Filtering

```python
numbers = [1, 2, 3, 4, 5]

result = [x * 2 for x in numbers if x % 2 == 0]

print(result)
```

Output:

```text
[4, 8]
```

এখানে:

```text
numbers
 ↓
filter even
 ↓
multiply by 2
 ↓
result
```

---

# 28. Conditional Expression inside Comprehension

এখানে একটি গুরুত্বপূর্ণ difference আছে।

```python
result = [
    "Even" if x % 2 == 0 else "Odd"
    for x in range(5)
]
```

Output:

```text
['Even', 'Odd', 'Even', 'Odd', 'Even']
```

এখানে `if/else` expression-এর অংশ।

---

# 29. Filter vs Conditional Expression

### শুধু filter:

```python
[x for x in numbers if x > 5]
```

শুধু matching values থাকবে।

### if/else:

```python
["High" if x > 5 else "Low" for x in numbers]
```

সব values থাকবে, কিন্তু label পরিবর্তিত হবে।

এটা খুব গুরুত্বপূর্ণ।

---

# 30. Nested List Comprehension

ধরি:

```python
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]
```

সব numbers বের করতে:

```python
result = [x for row in matrix for x in row]
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

এটা প্রথমে confusing হতে পারে।

Traditional equivalent:

```python
result = []

for row in matrix:
    for x in row:
        result.append(x)
```

---

# 31. Matrix তৈরি

```python
matrix = [
    [i * j for j in range(1, 4)]
    for i in range(1, 4)
]

print(matrix)
```

Output:

```text
[
    [1, 2, 3],
    [2, 4, 6],
    [3, 6, 9]
]
```

---

# 32. Dictionary Comprehension

Syntax:

```python
{key: value for item in iterable}
```

Example:

```python
squares = {
    x: x ** 2
    for x in range(1, 6)
}
```

Output:

```text
{
    1: 1,
    2: 4,
    3: 9,
    4: 16,
    5: 25
}
```

---

# 33. Dictionary Comprehension with Condition

```python
squares = {
    x: x ** 2
    for x in range(1, 11)
    if x % 2 == 0
}
```

Output:

```text
{
    2: 4,
    4: 16,
    6: 36,
    8: 64,
    10: 100
}
```

---

# 34. AI/NLP Word Score Dictionary

ধরি:

```python
words = ["AI", "Python", "Machine", "Learning"]

scores = [0.9, 0.8, 0.7, 0.95]
```

Dictionary বানাতে:

```python
result = {
    word: score
    for word, score in zip(words, scores)
}
```

Output:

```python
{
    "AI": 0.9,
    "Python": 0.8,
    "Machine": 0.7,
    "Learning": 0.95
}
```

---

# 35. Set Comprehension

Syntax:

```python
{expression for item in iterable}
```

Example:

```python
numbers = [1, 2, 2, 3, 3, 4]

unique_squares = {
    x ** 2
    for x in numbers
}

print(unique_squares)
```

Output:

```text
{1, 4, 9, 16}
```

Duplicate automatically বাদ।

---

# 36. String থেকে Unique Characters

```python
text = "programming"

chars = {char for char in text}

print(chars)
```

এখানে duplicate characters বাদ যাবে।

---

# 37. NLP Token Filtering

ধরি:

```python
text = "Python is a powerful programming language"

tokens = text.split()
```

আমরা ছোট শব্দ বাদ দিতে চাই:

```python
filtered = [
    word
    for word in tokens
    if len(word) > 3
]

print(filtered)
```

Output:

```text
['Python', 'powerful', 'programming', 'language']
```

এটাই NLP preprocessing-এর basic idea।

---

# 38. Token Normalization

```python
tokens = ["Python", "PYTHON", "python", "AI"]

normalized = [
    word.lower()
    for word in tokens
]
```

Output:

```text
['python', 'python', 'python', 'ai']
```

Unique:

```python
unique_words = {
    word.lower()
    for word in tokens
}
```

---

# 39. Sentence Filtering

```python
sentences = [
    {"text": "AI is powerful", "score": 0.91},
    {"text": "Python is useful", "score": 0.45},
    {"text": "Machine learning is growing", "score": 0.87}
]
```

High-score sentences:

```python
high_score = [
    sentence
    for sentence in sentences
    if sentence["score"] >= 0.80
]
```

---

# 40. Extract শুধু Text

```python
texts = [
    sentence["text"]
    for sentence in sentences
]
```

Output:

```text
[
    "AI is powerful",
    "Python is useful",
    "Machine learning is growing"
]
```

---

# 41. Generator Expression

List comprehension:

```python
numbers = [x * 2 for x in range(1000000)]
```

এটি পুরো list memory-তে তৈরি করবে।

Generator expression:

```python
numbers = (x * 2 for x in range(1000000))
```

এটি values প্রয়োজন অনুযায়ী generate করে।

```python
for number in numbers:
    print(number)
```

Memory-efficient processing-এর জন্য generator গুরুত্বপূর্ণ।

Generator আমরা পরের advanced lesson-এ আরও গভীরভাবে শিখব।

---

# 42. enumerate() + Comprehension

ধরি:

```python
words = ["AI", "Python", "Django"]
```

Index সহ:

```python
result = [
    (index, word)
    for index, word in enumerate(words)
]
```

Output:

```text
[
    (0, 'AI'),
    (1, 'Python'),
    (2, 'Django')
]
```

---

# 43. zip() + Comprehension

```python
words = ["AI", "Python", "Django"]
scores = [0.9, 0.8, 0.7]
```

Dictionary:

```python
result = {
    word: score
    for word, score in zip(words, scores)
}
```

---

# 44. Comprehension vs Loop

### Loop

```python
result = []

for x in numbers:
    if x > 10:
        result.append(x * 2)
```

### Comprehension

```python
result = [
    x * 2
    for x in numbers
    if x > 10
]
```

Comprehension shorter।

কিন্তু **shorter ≠ always better**।

---

# 45. কখন Comprehension ব্যবহার করব?

ভালো:

```python
squares = [x * x for x in numbers]
```

আরও readable:

```python
high_scores = [
    score
    for score in scores
    if score >= 0.8
]
```

কিন্তু খুব complicated হলে loop ব্যবহার করো।

Bad example:

```python
result = [
    complicated_function(x, y)
    if condition(x)
    else another_function(x, y)
    for x in data
    for y in other_data
    if another_condition(x, y)
]
```

এটা maintain করা কঠিন।

তখন normal loop ভালো।

---

# 46. Nested Comprehension-এর গুরুত্বপূর্ণ Rule

যদি comprehension পড়তে গিয়ে তোমার মনে হয়:

> "এটা বুঝতে অনেক সময় লাগছে"

তাহলে loop ব্যবহার করো।

Professional programming-এ:

```text
Readability > cleverness
```

---

# 47. Frequency Counting

ধরি:

```python
words = [
    "python",
    "ai",
    "python",
    "django",
    "ai",
    "python"
]
```

Manual dictionary:

```python
frequency = {}

for word in words:
    frequency[word] = frequency.get(word, 0) + 1
```

Output:

```text
{
    'python': 3,
    'ai': 2,
    'django': 1
}
```

এটা NLP-তে অত্যন্ত গুরুত্বপূর্ণ pattern।

---

# 48. Dictionary Comprehension দিয়ে Transformation

```python
scores = {
    "AI": 0.91,
    "Python": 0.75,
    "Django": 0.62
}
```

শুধু high score:

```python
high_scores = {
    word: score
    for word, score in scores.items()
    if score >= 0.80
}
```

Output:

```text
{
    "AI": 0.91
}
```

---

# 49. Nested Dictionary

```python
users = {
    1: {
        "name": "Atiar",
        "age": 25
    },
    2: {
        "name": "Rahim",
        "age": 30
    }
}
```

Access:

```python
print(users[1]["name"])
```

Output:

```text
Atiar
```

---

# 50. AI Pipeline Data Transformation

ধরি raw data:

```python
texts = [
    "AI is powerful.",
    "Python is easy.",
    "Machine learning is useful."
]
```

Lowercase:

```python
normalized = [
    text.lower()
    for text in texts
]
```

Words:

```python
tokens = [
    text.split()
    for text in normalized
]
```

এখন:

```text
Raw Text
   ↓
Normalize
   ↓
Tokenize
   ↓
Filter
   ↓
Analyze
```

এই ধরনের transformation pattern তোমার future AI writing project-এ বারবার আসবে।

---

# 51. Real AI Example

```python
sentences = [
    {
        "text": "AI is changing the world.",
        "score": 0.91
    },
    {
        "text": "Python is easy to learn.",
        "score": 0.32
    },
    {
        "text": "Machine learning is powerful.",
        "score": 0.87
    }
]
```

High-score:

```python
high_risk = [
    item
    for item in sentences
    if item["score"] >= 0.80
]
```

Only text:

```python
texts = [
    item["text"]
    for item in high_risk
]
```

Result:

```text
[
    "AI is changing the world.",
    "Machine learning is powerful."
]
```

---

# 52. Data Structure Selection — Practical Thinking

ধরি তোমার AI application-এ:

### All sentences

```python
sentences = []
```

### Unique words

```python
unique_words = set()
```

### Word frequency

```python
word_frequency = {}
```

### Fixed model configuration

```python
model_config = (
    "bert",
    512,
    0.001
)
```

### User data

```python
user = {
    "id": 1,
    "name": "Atiar",
    "email": "..."
}
```

এই selection skill খুব গুরুত্বপূর্ণ।

---

# 53. Common Mistake — Mutable Aliasing

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

কারণ:

```text
a ──┐
    ├──> same list object
b ──┘
```

Copy চাইলে:

```python
b = a.copy()
```

অথবা:

```python
b = list(a)
```

---

# 54. Common Mistake — Dictionary Key

Dictionary key সাধারণত hashable হতে হবে।

Valid:

```python
data = {
    "name": "Atiar",
    1: "one",
    (1, 2): "point"
}
```

Invalid:

```python
data = {
    [1, 2]: "test"
}
```

কারণ list mutable এবং unhashable।

---

# 55. Common Mistake — Set Indexing

এটা করা যাবে না:

```python
numbers = {10, 20, 30}

print(numbers[0])
```

Set indexed নয়।

যদি ordered/indexed data দরকার হয়:

```python
numbers = [10, 20, 30]
```

---

# 56. Comprehension-এর Mental Model

সবসময় এইভাবে চিন্তা করো:

```python
result = [
    transformation
    for item in data
    if condition
]
```

মানে:

```text
DATA
 ↓
প্রতিটি item
 ↓
condition?
 ↓
হ্যাঁ
 ↓
transformation
 ↓
RESULT
```

---

# 57. Algorithmic Thinking

এই lesson শুধু Python syntax নয়।

ধরি:

```python
numbers = [1, 2, 3, 4, 5, 6]
```

Problem:

> Even numbers-এর square বের করো।

প্রথমে algorithm:

```text
1. numbers traverse করো
2. even কিনা check করো
3. even হলে square করো
4. result store করো
```

Loop:

```python
result = []

for x in numbers:
    if x % 2 == 0:
        result.append(x ** 2)
```

Comprehension:

```python
result = [
    x ** 2
    for x in numbers
    if x % 2 == 0
]
```

এটাই algorithm → implementation।

---

# 58. Practice — Level 1

### Q1

এই list-এর প্রতিটি number-এর square তৈরি করো:

```python
numbers = [1, 2, 3, 4, 5]
```

Expected:

```text
[1, 4, 9, 16, 25]
```

---

### Q2

শুধু odd numbers বের করো।

---

### Q3

শুধু 10-এর বেশি numbers বের করো।

---

### Q4

সব string lowercase করো:

```python
words = ["PYTHON", "AI", "DJANGO"]
```

---

### Q5

Unique words বের করো:

```python
words = ["ai", "python", "ai", "django", "python"]
```

---

# 59. Practice — Level 2

### Q6

এই data থেকে শুধু names বের করো:

```python
users = [
    {"name": "Atiar", "age": 25},
    {"name": "Rahim", "age": 30},
    {"name": "Karim", "age": 22}
]
```

---

### Q7

শুধু age >= 25 users বের করো।

---

### Q8

এই list থেকে word length dictionary তৈরি করো:

```python
words = ["AI", "Python", "Django"]
```

Expected:

```python
{
    "AI": 2,
    "Python": 6,
    "Django": 6
}
```

---

### Q9

এই list-এর unique square বের করো:

```python
numbers = [1, 2, 2, 3, 3, 4]
```

---

# 60. Practice — Level 3

এই data:

```python
sentences = [
    {"text": "AI is powerful", "score": 0.91},
    {"text": "Python is easy", "score": 0.45},
    {"text": "Machine learning is useful", "score": 0.87},
    {"text": "Django is great", "score": 0.30}
]
```

### Task 1

Score >= 0.80 sentences বের করো।

### Task 2

শুধু তাদের text বের করো।

### Task 3

Dictionary তৈরি করো:

```python
{
    sentence_text: score
}
```

### Task 4

শুধু score >= 0.80 রাখো।

---

# 61. Challenge — NLP

এই text:

```python
text = """
Python is powerful and Python is easy.
AI is powerful and AI is useful.
"""
```

তোমার কাজ:

### Step 1

Lowercase করো।

### Step 2

Words বের করো।

### Step 3

Unique words বের করো।

### Step 4

প্রতিটি word-এর frequency বের করো।

Expected concept:

```python
{
    "python": 2,
    "is": 4,
    "powerful": 2,
    ...
}
```

এখানে তুমি **list + set + dictionary + loop** একসাথে ব্যবহার করবে।

---

# 62. Theory Questions

নিজে answer দেওয়ার চেষ্টা করো।

### 1.

List এবং tuple-এর মধ্যে difference কী?

### 2.

Set কেন duplicate রাখে না?

### 3.

Dictionary কীভাবে data store করে?

### 4.

`append()` এবং `extend()` এর difference কী?

### 5.

`remove()` এবং `pop()` এর difference কী?

### 6.

`sort()` এবং `sorted()` এর difference কী?

### 7.

List comprehension কী?

### 8.

List comprehension-এর basic syntax কী?

### 9.

Filtering এবং conditional expression-এর difference কী?

### 10.

Dictionary comprehension কী?

### 11.

Set comprehension কী?

### 12.

Nested comprehension কী?

### 13.

Comprehension কখন ব্যবহার না করাই ভালো?

### 14.

Set NLP-তে কীভাবে useful?

### 15.

Dictionary NLP-তে কেন গুরুত্বপূর্ণ?

---

# 63. M01.09 Final Mental Model

এখন তোমার মাথায় এই map থাকা উচিত:

```text
Python Data Structures
│
├── List
│   ├── indexing
│   ├── slicing
│   ├── append
│   ├── extend
│   ├── insert
│   ├── remove
│   ├── pop
│   ├── sort
│   └── search
│
├── Tuple
│   ├── indexing
│   ├── slicing
│   └── unpacking
│
├── Set
│   ├── unique values
│   ├── union
│   ├── intersection
│   ├── difference
│   └── symmetric difference
│
├── Dictionary
│   ├── key/value
│   ├── get
│   ├── update
│   ├── pop
│   ├── keys
│   ├── values
│   └── items
│
└── Comprehension
    ├── List
    ├── Dictionary
    ├── Set
    ├── Filtering
    ├── Mapping
    ├── Nested
    ├── enumerate
    └── zip
```

---

# ✅ M01.09 Completion Checklist

নিজেকে check করো:

* [ ] List বুঝেছি
* [ ] List indexing/slicing পারি
* [ ] append/extend/insert পারি
* [ ] remove/pop/del/clear পারি
* [ ] sort/sorted বুঝেছি
* [ ] Tuple বুঝেছি
* [ ] Tuple unpacking পারি
* [ ] Set বুঝেছি
* [ ] Union/intersection/difference পারি
* [ ] Dictionary বুঝেছি
* [ ] get/update/pop/items পারি
* [ ] Nested data structures বুঝেছি
* [ ] List comprehension পারি
* [ ] Conditional comprehension পারি
* [ ] Nested comprehension বুঝেছি
* [ ] Dictionary comprehension পারি
* [ ] Set comprehension পারি
* [ ] Generator expression-এর basic idea বুঝেছি
* [ ] enumerate + comprehension পারি
* [ ] zip + comprehension পারি
* [ ] AI/NLP data transformation বুঝেছি
* [ ] Frequency counting বুঝেছি
* [ ] কোন data structure কখন ব্যবহার করতে হয় বুঝেছি

### 🎯 M01.09-এর সবচেয়ে গুরুত্বপূর্ণ takeaway

তুমি এখন শুধু Python syntax শিখছ না। তুমি **data নিয়ে algorithmically চিন্তা করা** শুরু করছ।

পরবর্তী ধাপে আমরা আরও ভিতরে যাব:

**M01.10 — Python Iterators, Generators & Lazy Evaluation**

এখানে `iter()`, `next()`, iterator protocol, `yield`, generator function, generator expression, lazy evaluation, memory efficiency এবং বড় AI/NLP dataset কীভাবে efficiently process করতে হয়—এসব বিস্তারিত শিখব।


---
# M01.10 — Python Iterators, Generators & Lazy Evaluation

আজকের lesson খুব গুরুত্বপূর্ণ। কারণ তুমি যখন **AI/NLP, large dataset, document processing, model inference pipeline** নিয়ে কাজ করবে, তখন লাখ লাখ data একসাথে memory-তে load না করে **একটা একটা করে process** করতে হবে।

এই lesson শেষে তুমি বুঝবে:

```text
Iterable
   ↓
Iterator
   ↓
next()
   ↓
Generator
   ↓
yield
   ↓
Lazy Evaluation
   ↓
Memory Efficient Processing
```

---

# 1. Iterable কী?

যে object-এর উপর আমরা `for` loop চালাতে পারি তাকে সাধারণভাবে **iterable** বলা হয়।

Examples:

```python
numbers = [1, 2, 3, 4]

for number in numbers:
    print(number)
```

এখানে `numbers` একটি iterable।

আরও examples:

```python
list
tuple
string
set
dictionary
range
file
```

Example:

```python
for char in "Python":
    print(char)
```

---

# 2. Iterable বনাম Iterator

এটা খুব ভালোভাবে বুঝতে হবে।

### Iterable

যে object থেকে iterator তৈরি করা যায়।

```python
numbers = [1, 2, 3]
```

### Iterator

যে object একবারে **পরবর্তী value** দিতে পারে।

```python
iterator = iter(numbers)
```

তারপর:

```python
print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

```text
1
2
3
```

---

# 3. `iter()` কী করে?

```python
numbers = [10, 20, 30]

iterator = iter(numbers)
```

এখন:

```text
numbers
   ↓
iter()
   ↓
iterator
```

তারপর:

```python
print(next(iterator))
```

Output:

```text
10
```

আবার:

```python
print(next(iterator))
```

Output:

```text
20
```

---

# 4. `next()` কী করে?

`next()` iterator থেকে পরবর্তী value বের করে।

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

```text
10
20
30
```

আরেকবার:

```python
print(next(iterator))
```

তাহলে:

```text
StopIteration
```

কারণ iterator-এর আর কোনো value নেই।

---

# 5. `StopIteration`

Iterator শেষ হয়ে গেলে Python internally `StopIteration` exception ব্যবহার করে।

```python
numbers = [1, 2]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

শেষ `next()`-এ:

```text
StopIteration
```

---

# 6. তাহলে `for` Loop কীভাবে কাজ করে?

এটা খুব গুরুত্বপূর্ণ।

আমরা লিখি:

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Python conceptually অনেকটা এরকম কাজ করে:

```python
iterator = iter(numbers)

while True:
    try:
        number = next(iterator)
        print(number)
    except StopIteration:
        break
```

অর্থাৎ:

```text
for loop
   ↓
iter()
   ↓
next()
   ↓
next()
   ↓
next()
   ↓
StopIteration
   ↓
loop শেষ
```

---

# 7. Iterator-এর মূল ধারণা

একটি iterator-এর মূল কাজ:

> "আমাকে next value দাও।"

Example:

```python
numbers = [10, 20, 30]

it = iter(numbers)

print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
```

Iterator-এর state থাকে।

```text
Start
 ↓
10
 ↓
20
 ↓
30
 ↓
End
```

---

# 8. Iterator Stateful

একই iterator আবার শুরু থেকে শুরু হয় না।

```python
numbers = [10, 20, 30]

it = iter(numbers)

print(next(it))
```

Output:

```text
10
```

তারপর:

```python
print(next(it))
```

Output:

```text
20
```

এখন আবার:

```python
for x in it:
    print(x)
```

Output:

```text
30
```

কারণ iterator ইতোমধ্যে 10 এবং 20 consume করেছে।

---

# 9. Iterable আবার ব্যবহার করা যায়

```python
numbers = [10, 20, 30]

for x in numbers:
    print(x)

for x in numbers:
    print(x)
```

দুইবারই data পাওয়া যাবে।

কারণ `list` iterable; iterator নয়।

---

# 10. `range()` কেন efficient?

```python
numbers = range(1000000000)
```

এখানে এক billion সংখ্যার বিশাল list তৈরি হচ্ছে না।

`range` একটি compact iterable object।

```python
for number in range(10):
    print(number)
```

প্রয়োজন অনুযায়ী values পাওয়া যায়।

এটাই lazy-style processing-এর একটি basic example।

---

# 11. Memory Comparison

ধরি:

```python
numbers = [x for x in range(1000000)]
```

এখানে প্রায় 1 million values-এর list তৈরি হচ্ছে।

অন্যদিকে:

```python
numbers = (x for x in range(1000000))
```

এটি generator expression।

এখানে পুরো result list তৈরি হচ্ছে না।

---

# 12. Generator কী?

Generator হলো Python-এর এমন একটি বিশেষ ধরনের iterator যা values **একবারে একটি করে** তৈরি করে।

Generator সাধারণত `yield` ব্যবহার করে তৈরি করা হয়।

```python
def numbers():
    yield 1
    yield 2
    yield 3
```

এখন:

```python
result = numbers()

print(next(result))
print(next(result))
print(next(result))
```

Output:

```text
1
2
3
```

---

# 13. `yield` কী?

`return` এবং `yield` এক জিনিস নয়।

### return

```python
def test():
    return 10
```

Function execution শেষ হয়ে যায়।

### yield

```python
def test():
    yield 10
    yield 20
```

Function execution pause হয় এবং পরে আবার resume করতে পারে।

---

# 14. Generator Function

```python
def generate_numbers():
    yield 1
    yield 2
    yield 3
```

এটি call করলে:

```python
result = generate_numbers()
```

সাথে সাথে 1, 2, 3 তৈরি হয় না।

Generator object তৈরি হয়।

```text
generate_numbers()
       ↓
generator object
```

---

# 15. Generator Lazy

এটাই সবচেয়ে গুরুত্বপূর্ণ concept।

```python
def generate_numbers():
    print("Generating 1")
    yield 1

    print("Generating 2")
    yield 2

    print("Generating 3")
    yield 3
```

```python
g = generate_numbers()

print("Start")

print(next(g))
print(next(g))
```

Output-এর flow হবে:

```text
Start

Generating 1
1

Generating 2
2
```

তৃতীয় value এখনো generate হয়নি।

---

# 16. Generator একবারে একটি Value তৈরি করে

```python
def count():
    for i in range(5):
        yield i
```

```python
for number in count():
    print(number)
```

Output:

```text
0
1
2
3
4
```

কিন্তু সব values একসাথে memory-তে রাখা হয়নি।

---

# 17. Generator vs List

### List

```python
def get_numbers():
    return [1, 2, 3, 4, 5]
```

পুরো list তৈরি।

### Generator

```python
def get_numbers():
    for i in range(1, 6):
        yield i
```

একবারে একটি value।

---

# 18. কখন Generator ব্যবহার করব?

বিশেষ করে:

```text
Large datasets
Large files
Streaming data
AI/NLP documents
Database records
Logs
Model inference
Data pipelines
```

যখন data অনেক বড় এবং পুরোটা memory-তে রাখা প্রয়োজন নেই।

---

# 19. Generator Expression

List comprehension:

```python
numbers = [x * 2 for x in range(10)]
```

Generator expression:

```python
numbers = (x * 2 for x in range(10))
```

Difference:

```text
[] → list তৈরি
() → generator expression
```

---

# 20. Generator Expression ব্যবহার

```python
numbers = (x * 2 for x in range(5))

for number in numbers:
    print(number)
```

Output:

```text
0
2
4
6
8
```

---

# 21. Generator-এর `next()`

```python
numbers = (x * 2 for x in range(5))

print(next(numbers))
print(next(numbers))
print(next(numbers))
```

Output:

```text
0
2
4
```

---

# 22. Generator Exhausted

```python
numbers = (x for x in range(3))

print(next(numbers))
print(next(numbers))
print(next(numbers))
```

এখন:

```python
print(next(numbers))
```

→ `StopIteration`

Generator শেষ হয়ে গেছে।

---

# 23. Generator Restart করা যায়?

না।

```python
g = (x for x in range(3))

for x in g:
    print(x)

for x in g:
    print(x)
```

দ্বিতীয় loop-এ কিছু পাওয়া যাবে না।

কারণ generator exhausted।

আবার generator তৈরি করতে হবে।

---

# 24. `yield` vs `return`

খুব গুরুত্বপূর্ণ:

| `return`         | `yield`            |
| ---------------- | ------------------ |
| value return করে | value produce করে  |
| function শেষ     | function pause     |
| সাধারণ function  | generator function |
| একবার result     | multiple values    |
| eager-style      | lazy               |

Example:

```python
def normal():
    return [1, 2, 3]
```

vs:

```python
def generator():
    yield 1
    yield 2
    yield 3
```

---

# 25. Generator State

Generator pause অবস্থায় তার execution state মনে রাখে।

```python
def test():
    print("A")
    yield 1

    print("B")
    yield 2

    print("C")
    yield 3
```

```python
g = test()

print(next(g))
print(next(g))
```

Flow:

```text
Call generator
      ↓
Print A
      ↓
yield 1
      ↓
pause
      ↓
next()
      ↓
Print B
      ↓
yield 2
      ↓
pause
```

---

# 26. Infinite Generator

Generator দিয়ে infinite sequence তৈরি করা যায়।

```python
def infinite_numbers():
    number = 0

    while True:
        yield number
        number += 1
```

এখন:

```python
g = infinite_numbers()

print(next(g))
print(next(g))
print(next(g))
```

Output:

```text
0
1
2
```

Generator lazy হওয়ায় পুরো infinite sequence memory-তে তৈরি হয় না।

---

# 27. Infinite Generator-এর সাথে সাবধানতা

এটা বিপজ্জনক:

```python
for number in infinite_numbers():
    print(number)
```

এটি theoretically শেষ হবে না।

তাই limit ব্যবহার করো:

```python
g = infinite_numbers()

for _ in range(5):
    print(next(g))
```

Output:

```text
0
1
2
3
4
```

---

# 28. Generator Pipeline

এটি তোমার AI project-এর জন্য খুব গুরুত্বপূর্ণ।

ধরি:

```text
Raw Documents
      ↓
Clean
      ↓
Tokenize
      ↓
Filter
      ↓
Analyze
```

প্রতিটি step generator হতে পারে।

```python
def clean_texts(texts):
    for text in texts:
        yield text.strip().lower()
```

তারপর:

```python
def filter_texts(texts):
    for text in texts:
        if len(text) > 10:
            yield text
```

এখন:

```python
texts = [
    "Hello World",
    "Artificial Intelligence is powerful",
    "Python is useful"
]

cleaned = clean_texts(texts)
filtered = filter_texts(cleaned)

for text in filtered:
    print(text)
```

এখানে পুরো intermediate data list তৈরি করতে হচ্ছে না।

---

# 29. AI/NLP Large Dataset Example

ধরি তোমার কাছে:

```text
10 million documents
```

এভাবে করলে:

```python
documents = load_all_documents()
```

সমস্যা হতে পারে:

```text
Huge RAM usage
Slow startup
MemoryError
```

Better architecture:

```python
def load_documents():
    for document in source:
        yield document
```

তারপর:

```python
for document in load_documents():
    process(document)
```

Concept:

```text
10 Million Documents
        ↓
    Generator
        ↓
Document 1
Document 2
Document 3
...
```

একবারে পুরো 10 million memory-তে নয়।

---

# 30. File Processing

বড় file-এর ক্ষেত্রে generator খুব useful।

ধরি file:

```text
5 GB
```

এভাবে পুরো file load না করাই ভালো:

```python
with open("large.txt") as file:
    data = file.read()
```

বরং:

```python
with open("large.txt") as file:
    for line in file:
        process(line)
```

File object নিজেই iterable এবং line-by-line processing করা যায়।

---

# 31. Custom Generator

```python
def read_numbers(numbers):
    for number in numbers:
        yield number
```

ব্যবহার:

```python
numbers = [10, 20, 30]

for number in read_numbers(numbers):
    print(number)
```

---

# 32. Generator দিয়ে Transformation

```python
def square_numbers(numbers):
    for number in numbers:
        yield number ** 2
```

ব্যবহার:

```python
numbers = [1, 2, 3, 4, 5]

squares = square_numbers(numbers)

for value in squares:
    print(value)
```

Output:

```text
1
4
9
16
25
```

---

# 33. Generator Chaining

```python
def numbers():
    for i in range(10):
        yield i
```

Filter:

```python
def even_numbers(numbers):
    for number in numbers:
        if number % 2 == 0:
            yield number
```

Square:

```python
def square_numbers(numbers):
    for number in numbers:
        yield number ** 2
```

Pipeline:

```python
data = numbers()
data = even_numbers(data)
data = square_numbers(data)

for value in data:
    print(value)
```

Output:

```text
0
4
16
36
64
```

Architecture:

```text
numbers()
    ↓
even_numbers()
    ↓
square_numbers()
    ↓
output
```

---

# 34. This is Functional Pipeline Thinking

তোমার আগের M01.08-এর concept-এর সাথে এটি connect করো।

আগে:

```text
clean()
 ↓
normalize()
 ↓
analyze()
 ↓
generate()
```

এখন:

```text
generator
 ↓
generator
 ↓
generator
 ↓
final output
```

অর্থাৎ data flow করে।

---

# 35. Lazy Evaluation কী?

Lazy evaluation মানে:

> প্রয়োজন হওয়ার আগে computation না করা।

Example:

```python
numbers = (x * 2 for x in range(1000000))
```

এখানে 1 million multiplication একসাথে করা হচ্ছে না।

যখন:

```python
next(numbers)
```

তখন প্রয়োজনীয় value তৈরি হচ্ছে।

---

# 36. Eager vs Lazy

### Eager

```python
numbers = [x * 2 for x in range(1000000)]
```

সব values আগে তৈরি।

### Lazy

```python
numbers = (x * 2 for x in range(1000000))
```

প্রয়োজন অনুযায়ী তৈরি।

```text
Eager:
Input → Process Everything → Store → Use

Lazy:
Input → Process One → Use
             ↓
          Next → Process
```

---

# 37. Memory Efficiency

Generator-এর সবচেয়ে বড় advantage:

> Memory-efficient processing.

Example:

```python
def read_data(data):
    for item in data:
        yield item
```

এখানে intermediate list না বানিয়ে stream করা যায়।

তবে মনে রাখবে:

**Generator সবসময় faster নয়।**

এটি মূলত memory efficiency এবং streaming-এর জন্য valuable।

---

# 38. Generator vs List — Important

| Feature            | List        | Generator            |
| ------------------ | ----------- | -------------------- |
| Memory             | বেশি        | কম                   |
| Reusable           | হ্যাঁ       | না, exhausted        |
| Indexing           | হ্যাঁ       | সাধারণত না           |
| Lazy               | না          | হ্যাঁ                |
| `next()`           | না          | হ্যাঁ                |
| Large data         | কম suitable | খুব suitable         |
| Multiple iteration | হ্যাঁ       | নতুন generator দরকার |

---

# 39. Generator এবং `list()`

Generator থেকে list বানানো যায়:

```python
g = (x * 2 for x in range(5))

result = list(g)

print(result)
```

Output:

```text
[0, 2, 4, 6, 8]
```

কিন্তু তখন generator-এর lazy advantage-এর একটি বড় অংশ চলে গেল, কারণ পুরো result memory-তে চলে এসেছে।

---

# 40. `yield from`

এক generator থেকে অন্য iterable-এর values yield করতে:

```python
def numbers():
    yield from [1, 2, 3, 4]
```

এটি roughly:

```python
def numbers():
    for number in [1, 2, 3, 4]:
        yield number
```

এর মতো।

---

# 41. Generator Composition

```python
def first():
    yield 1
    yield 2

def second():
    yield from first()
    yield 3
    yield 4
```

```python
for x in second():
    print(x)
```

Output:

```text
1
2
3
4
```

---

# 42. Iterator Protocol

Python-এর iterator concept-এর পিছনে protocol আছে।

একটি iterator সাধারণত implement করে:

```python
__iter__()
__next__()
```

Example:

```python
iterator = iter([1, 2, 3])

print(iterator.__iter__())
print(iterator.__next__())
```

সাধারণত direct dunder method call না করে:

```python
iter()
next()
```

ব্যবহার করাই ভালো।

---

# 43. Custom Iterator

এখন আমরা নিজে iterator বানাই:

```python
class Counter:

    def __init__(self, max_value):
        self.current = 0
        self.max_value = max_value

    def __iter__(self):
        return self

    def __next__(self):

        if self.current >= self.max_value:
            raise StopIteration

        value = self.current
        self.current += 1

        return value
```

ব্যবহার:

```python
counter = Counter(5)

for number in counter:
    print(number)
```

Output:

```text
0
1
2
3
4
```

---

# 44. Custom Iterator-এর Flow

```text
for
 ↓
iter(counter)
 ↓
__iter__()
 ↓
next()
 ↓
__next__()
 ↓
value
 ↓
next()
 ↓
...
 ↓
StopIteration
```

এখন তুমি বুঝতে পারবে Python `for` loop internally কীভাবে কাজ করে।

---

# 45. Generator বনাম Custom Iterator

Custom iterator:

```python
class Counter:
    ...
```

এখানে manually লিখতে হয়েছে:

```python
__iter__()
__next__()
StopIteration
```

Generator:

```python
def counter():
    for i in range(5):
        yield i
```

Python internally iterator protocol handle করে।

তাই সাধারণ ক্ষেত্রে generator অনেক সহজ।

---

# 46. Real AI Text Pipeline

ধরি:

```python
documents = [
    "AI IS powerful.",
    "Python IS useful.",
    "Machine Learning is growing."
]
```

### Step 1 — Normalize

```python
def normalize(documents):

    for document in documents:
        yield document.lower()
```

### Step 2 — Tokenize

```python
def tokenize(documents):

    for document in documents:
        yield document.split()
```

### Step 3 — Filter

```python
def filter_tokens(documents):

    for tokens in documents:
        yield [
            token
            for token in tokens
            if len(token) > 2
        ]
```

Pipeline:

```python
data = normalize(documents)
data = tokenize(data)
data = filter_tokens(data)

for item in data:
    print(item)
```

এটা একটি ছোট **streaming NLP pipeline**।

---

# 47. Large Document Processing Architecture

Future AI writing platform-এর ক্ষেত্রে conceptually:

```text
Uploaded Document
       ↓
Document Reader
       ↓
Generator
       ↓
Text Cleaner
       ↓
Sentence Splitter
       ↓
Tokenization
       ↓
Analysis
       ↓
Rewrite
       ↓
Output
```

প্রতিটি stage পুরো data copy না করে stream করতে পারে।

---

# 48. গুরুত্বপূর্ণ সতর্কতা

Generator ব্যবহার করলেই সবসময় application better হবে না।

যদি data:

```text
small
reused many times
randomly indexed
```

তাহলে list ভালো হতে পারে।

Example:

```python
users = [...]
```

যদি বারবার:

```python
users[10]
users[50]
users[100]
```

করতে হয়, list সুবিধাজনক।

Generator sequential processing-এর জন্য বেশি উপযোগী।

---

# 49. কখন List?

```text
Small/medium data
Need indexing
Need repeated iteration
Need random access
Need length frequently
```

Example:

```python
tokens = text.split()
```

---

# 50. কখন Generator?

```text
Huge data
Streaming
One-pass processing
Large files
Database rows
AI dataset pipelines
Log processing
Infinite sequences
Memory-sensitive operations
```

---

# 51. Practical Example — Batch Processing

ধরি:

```python
documents = [
    "Document 1",
    "Document 2",
    "Document 3",
    "Document 4",
    "Document 5"
]
```

Batch generator:

```python
def batch_documents(documents, batch_size):

    for i in range(0, len(documents), batch_size):
        yield documents[i:i + batch_size]
```

ব্যবহার:

```python
for batch in batch_documents(documents, 2):
    print(batch)
```

Output:

```text
['Document 1', 'Document 2']
['Document 3', 'Document 4']
['Document 5']
```

এটা ML inference/training pipeline-এর basic concept।

---

# 52. Generator + Model Inference Concept

Future-এ conceptually:

```python
def generate_batches(dataset, batch_size):

    for i in range(0, len(dataset), batch_size):
        yield dataset[i:i + batch_size]
```

তারপর:

```python
for batch in generate_batches(dataset, 32):
    predictions = model.predict(batch)
```

এভাবে dataset processing structured করা যায়।

---

# 53. Important Performance Thinking

তোমার মাথায় এখন এই ৩টি concept আলাদা থাকতে হবে:

```text
Algorithm
   ↓
How to solve

Data Structure
   ↓
How to store

Iterator/Generator
   ↓
How to consume/process
```

এগুলো একসাথে future AI system-এ খুব গুরুত্বপূর্ণ।

---

# 54. Practice — Level 1

### Q1

`iter()` এবং `next()` ব্যবহার করে:

```python
numbers = [10, 20, 30]
```

তিনটি value বের করো।

---

### Q2

নিজে generator বানাও:

```python
1
2
3
4
5
```

---

### Q3

Generator বানাও যেটা শুধু even numbers yield করবে।

Expected:

```text
0
2
4
6
8
```

---

### Q4

Generator দিয়ে 1 থেকে 100 পর্যন্ত square তৈরি করো।

---

# 55. Practice — Level 2

### Q5

এই function তৈরি করো:

```python
def even_numbers(numbers):
    ...
```

যেটি list return না করে generator return করবে।

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]
```

Expected:

```text
2
4
6
```

---

### Q6

একটি generator তৈরি করো যা string-এর প্রতিটি word yield করবে।

```python
text = "Python is powerful"
```

Expected:

```text
Python
is
powerful
```

---

### Q7

একটি generator তৈরি করো যা শুধু 5 characters-এর বেশি word yield করবে।

---

# 56. Practice — Level 3

এই pipeline বানাও:

```text
Raw Text
   ↓
Lowercase
   ↓
Split
   ↓
Filter length > 3
   ↓
Output
```

Input:

```python
text = """
Python is a powerful programming language
and Python is useful for AI development
"""
```

প্রতিটি stage generator হিসেবে তৈরি করার চেষ্টা করো।

---

# 57. Challenge — Streaming NLP Pipeline

একটি generator pipeline তৈরি করো:

```text
Documents
    ↓
Normalize
    ↓
Sentence
    ↓
Filter
    ↓
Output
```

Input:

```python
documents = [
    "AI is changing the world.",
    "Python is useful.",
    "Machine learning is powerful.",
    "AI is useful for automation."
]
```

Requirements:

1. lowercase
2. sentence split
3. empty sentence বাদ
4. sentence length > 15 হলে yield
5. final output একবারে একটি sentence

---

# 58. Theory Questions

নিজে উত্তর দেওয়ার চেষ্টা করো।

### 1.

Iterable কী?

### 2.

Iterator কী?

### 3.

Iterable এবং iterator-এর difference কী?

### 4.

`iter()` কী করে?

### 5.

`next()` কী করে?

### 6.

`StopIteration` কী?

### 7.

`for` loop internally কীভাবে iterator ব্যবহার করে?

### 8.

Generator কী?

### 9.

`yield` কী?

### 10.

`return` এবং `yield`-এর difference কী?

### 11.

Lazy evaluation কী?

### 12.

Generator memory efficient কেন?

### 13.

Generator কেন reusable নয়?

### 14.

Generator expression কী?

### 15.

`yield from` কী?

### 16.

Custom iterator কী?

### 17.

`__iter__()` কী?

### 18.

`__next__()` কী?

### 19.

List এবং generator কখন ব্যবহার করবে?

### 20.

AI/NLP pipeline-এ generator কেন useful?

---

# 59. M01.10 Final Mental Model

পুরো lesson-টা এই diagram দিয়ে মনে রাখো:

```text
ITERABLE
   │
   │ iter()
   ↓
ITERATOR
   │
   │ next()
   ↓
VALUE
   │
   │ next()
   ↓
VALUE
   │
   │ next()
   ↓
VALUE
   │
   ↓
StopIteration
```

Generator:

```text
Generator Function
       │
       │ yield
       ↓
Generator Object
       │
       │ next()
       ↓
Value
       │
       ↓
Pause
       │
       │ next()
       ↓
Next Value
```

Lazy pipeline:

```text
Large Dataset
      ↓
Generator
      ↓
Transform
      ↓
Generator
      ↓
Filter
      ↓
Generator
      ↓
Model
      ↓
Output
```

---

# ✅ M01.10 Completion Checklist

### Iterable & Iterator

* [ ] Iterable বুঝেছি
* [ ] Iterator বুঝেছি
* [ ] `iter()` বুঝেছি
* [ ] `next()` বুঝেছি
* [ ] `StopIteration` বুঝেছি
* [ ] `for` loop internally কীভাবে কাজ করে বুঝেছি
* [ ] Iterator state বুঝেছি
* [ ] Iterator protocol বুঝেছি

### Generator

* [ ] Generator কী বুঝেছি
* [ ] `yield` বুঝেছি
* [ ] `return` vs `yield` বুঝেছি
* [ ] Generator function পারি
* [ ] Generator expression পারি
* [ ] Generator exhausted বুঝেছি
* [ ] Generator restart করা যায় না বুঝেছি
* [ ] `yield from` বুঝেছি
* [ ] Infinite generator বুঝেছি

### Lazy Evaluation

* [ ] Lazy evaluation বুঝেছি
* [ ] Eager vs lazy বুঝেছি
* [ ] Memory efficiency বুঝেছি
* [ ] Large file processing বুঝেছি
* [ ] Streaming data বুঝেছি
* [ ] Generator pipeline বুঝেছি

### Advanced

* [ ] Custom iterator বুঝেছি
* [ ] `__iter__()` বুঝেছি
* [ ] `__next__()` বুঝেছি
* [ ] Generator vs custom iterator বুঝেছি
* [ ] AI/NLP streaming pipeline বুঝেছি
* [ ] Batch processing concept বুঝেছি

---

## 🎯 M01.10-এর মূল শিক্ষা

এখন তোমার Python mental model অনেক বেশি শক্ত হয়েছে:

```text
M01.07
Functions
   ↓
M01.08
Advanced Functions
   ↓
M01.09
Data Structures
   ↓
M01.10
Iterators + Generators
   ↓
Efficient Data Processing
```

বিশেষ করে তোমার ভবিষ্যৎ **AI/NLP application**-এর জন্য এই conceptটি মনে রাখবে:

> **ছোট data হলে list সহজ; বড় data হলে stream/generator চিন্তা করো।**

পরবর্তী lesson হবে **M01.11 — Python Exception Handling, Error Handling & Debugging Deep Dive** — যেখানে `try`, `except`, `else`, `finally`, `raise`, custom exception, exception hierarchy, traceback, debugging strategy এবং production-level error handling বিস্তারিত শেখা হবে।


---
# M01.11 — Python Exception Handling, Error Handling & Debugging Deep Dive

আজকের lesson-এ আমরা Python-এর **Error, Exception, Exception Handling এবং Debugging** সম্পূর্ণভাবে শিখব।

এটা খুব গুরুত্বপূর্ণ কারণ তুমি পরে যখন **Django/DRF backend + AI/NLP model + API + database + ML inference** একসাথে ব্যবহার করবে, তখন error handling production application-এর অন্যতম গুরুত্বপূর্ণ অংশ হবে।

আজকের flow:

```text
Error
 ↓
Exception
 ↓
try
 ↓
except
 ↓
else
 ↓
finally
 ↓
raise
 ↓
Custom Exception
 ↓
Traceback
 ↓
Debugging
 ↓
Production Error Handling
```

---

# 1. Error কী?

Program-এর execution-এর সময় কোনো সমস্যা হলে তাকে সাধারণভাবে error বলা হয়।

Example:

```python
print(10 / 0)
```

Output:

```text
ZeroDivisionError
```

আরেকটি:

```python
print(name)
```

যদি `name` define না করা থাকে:

```text
NameError
```

---

# 2. Syntax Error

Code-এর syntax ভুল হলে Python program execute করার আগেই error দেয়।

```python
if True
    print("Hello")
```

এখানে `:` missing।

Python বলবে:

```text
SyntaxError
```

আরেকটি:

```python
print("Hello"
```

এখানে closing `)` নেই।

---

# 3. Syntax Error বনাম Runtime Exception

### Syntax Error

Program run হওয়ার আগেই ধরা পড়ে।

```python
if True
```

### Runtime Exception

Program চলার সময় ঘটে।

```python
x = 10 / 0
```

তাই:

```text
Syntax Error
→ Code structure problem

Runtime Exception
→ Execution-time problem
```

---

# 4. Exception কী?

Exception হলো এমন একটি event যা program-এর normal execution interrupt করে।

Example:

```python
number = int("hello")
```

Output:

```text
ValueError
```

কারণ `"hello"` integer-এ convert করা যায় না।

---

# 5. Common Python Exceptions

তোমাকে অন্তত এগুলো ভালোভাবে জানতে হবে:

```text
Exception
├── ValueError
├── TypeError
├── NameError
├── IndexError
├── KeyError
├── AttributeError
├── ZeroDivisionError
├── FileNotFoundError
├── ImportError
├── ModuleNotFoundError
├── PermissionError
├── RuntimeError
├── RecursionError
└── StopIteration
```

---

# 6. `ValueError`

Value-এর type acceptable হলেও value invalid হলে `ValueError` হতে পারে।

```python
age = int("abc")
```

এখানে Python integer আশা করছে কিন্তু `"abc"` valid integer value নয়।

---

# 7. `TypeError`

Wrong type-এর operation করলে:

```python
print("10" + 5)
```

Output:

```text
TypeError
```

কারণ string এবং integer এভাবে যোগ করা যায় না।

আরেকটি:

```python
len(100)
```

Integer-এর length নেই।

---

# 8. `IndexError`

List-এর বাইরে index access করলে:

```python
numbers = [10, 20, 30]

print(numbers[10])
```

→ `IndexError`

Valid index:

```text
0
1
2
```

---

# 9. `KeyError`

Dictionary-তে নেই এমন key access করলে:

```python
user = {
    "name": "Atiar"
}

print(user["email"])
```

→ `KeyError`

Better:

```python
print(user.get("email"))
```

---

# 10. `NameError`

Undefined variable:

```python
print(username)
```

যদি আগে:

```python
username = ...
```

না থাকে।

→ `NameError`

---

# 11. `AttributeError`

Object-এর মধ্যে নেই এমন attribute/method access করলে:

```python
text = "Python"

text.append("!")
```

String-এর `append()` method নেই।

→ `AttributeError`

---

# 12. `ZeroDivisionError`

```python
x = 10
y = 0

print(x / y)
```

→ `ZeroDivisionError`

---

# 13. `FileNotFoundError`

```python
with open("unknown.txt") as file:
    data = file.read()
```

File না থাকলে:

```text
FileNotFoundError
```

---

# 14. কেন Exception Handling দরকার?

ধরি তোমার application-এ:

```text
User
 ↓
API
 ↓
AI Model
 ↓
Database
 ↓
Response
```

AI model error করলে যদি exception handle না করো:

```text
Application crash
```

কিন্তু handle করলে:

```text
AI Model Error
     ↓
Catch
     ↓
Log
     ↓
Safe Response
```

Application পুরোপুরি crash না-ও করতে পারে।

---

# 15. `try`

যে code-এ exception হওয়ার possibility আছে সেটা `try` block-এ রাখা হয়।

```python
try:
    result = 10 / 0
```

কিন্তু শুধু `try` দিলে incomplete।

---

# 16. `except`

Exception catch করতে:

```python
try:
    result = 10 / 0

except:
    print("Something went wrong")
```

Output:

```text
Something went wrong
```

---

# 17. Specific Exception Catch করা

Bare `except` avoid করা ভালো যখন specific exception জানা আছে।

Better:

```python
try:
    result = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")
```

এতে code-এর intent পরিষ্কার হয়।

---

# 18. Multiple Exceptions

```python
try:
    number = int(input("Enter number: "))
    result = 100 / number

except ValueError:
    print("Invalid number")

except ZeroDivisionError:
    print("Cannot divide by zero")
```

এখন দুই ধরনের problem আলাদাভাবে handle হচ্ছে।

---

# 19. Exception Object

Exception-এর message দেখতে:

```python
try:
    number = int("abc")

except ValueError as error:
    print(error)
```

Output-এর মতো:

```text
invalid literal for int() with base 10: 'abc'
```

এখানে:

```python
as error
```

exception object ধরে রাখে।

---

# 20. Multiple Exceptions একসাথে

একই handling হলে:

```python
try:
    ...
except (ValueError, TypeError) as error:
    print(error)
```

এতে দুই ধরনের exception একই block-এ handle হবে।

---

# 21. `else`

`try` সফলভাবে execute হলে `else` execute হয়।

```python
try:
    number = int("10")

except ValueError:
    print("Invalid number")

else:
    print("Conversion successful")
```

Flow:

```text
try
 ↓
Success?
 ├── No → except
 └── Yes → else
```

---

# 22. `finally`

`finally` সাধারণত শেষ পর্যন্ত execute হয়।

```python
try:
    print("Try")

except Exception:
    print("Except")

finally:
    print("Finally")
```

Output:

```text
Try
Finally
```

Exception হলেও:

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("Error")

finally:
    print("Always runs")
```

Output:

```text
Error
Always runs
```

---

# 23. `finally` কেন দরকার?

Resource cleanup-এর জন্য খুব useful।

যেমন:

```text
File
Database connection
Network connection
Lock
Temporary resource
```

Example:

```python
file = None

try:
    file = open("data.txt")
    data = file.read()

finally:
    if file:
        file.close()
```

তবে modern Python-এ file-এর জন্য `with` আরও ভালো।

---

# 24. `with` এবং Exception Safety

```python
with open("data.txt") as file:
    data = file.read()
```

এখানে Python context manager resource management handle করে।

তাই manual:

```python
file.close()
```

করার প্রয়োজন হয় না।

---

# 25. `raise`

নিজে exception তৈরি করতে `raise` ব্যবহার করা যায়।

```python
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")
```

Output:

```text
ValueError: Age cannot be negative
```

---

# 26. কেন `raise` ব্যবহার করব?

Business rule enforce করার জন্য।

Example:

```python
def withdraw(balance, amount):

    if amount <= 0:
        raise ValueError("Amount must be positive")

    if amount > balance:
        raise ValueError("Insufficient balance")

    return balance - amount
```

এখানে invalid input হলে function নিজেই problem জানাচ্ছে।

---

# 27. `raise` + `except`

```python
try:
    age = -5

    if age < 0:
        raise ValueError("Invalid age")

except ValueError as error:
    print(error)
```

Flow:

```text
Condition
 ↓
raise
 ↓
Exception
 ↓
except
 ↓
Handle
```

---

# 28. Re-raising Exception

কখনও exception catch করার পর আবার throw করতে হতে পারে।

```python
try:
    process_data()

except ValueError:
    print("Logging error")
    raise
```

`raise` without argument বর্তমান exception আবার raise করে।

Production systems-এ এটা useful হতে পারে যখন logging করার পর upper layer-কে exception জানাতে হবে।

---

# 29. Exception Hierarchy

Python-এর exception structure hierarchy-based।

Conceptually:

```text
BaseException
│
├── KeyboardInterrupt
├── SystemExit
└── Exception
     │
     ├── ValueError
     ├── TypeError
     ├── LookupError
     │    ├── IndexError
     │    └── KeyError
     ├── OSError
     │    ├── FileNotFoundError
     │    └── PermissionError
     └── RuntimeError
```

সব exception `Exception` থেকে সরাসরি আসে না, তাই hierarchy বোঝা useful।

---

# 30. Parent Exception Catch করা

```python
try:
    number = int("abc")

except Exception as error:
    print(error)
```

এটি অনেক সাধারণ exception catch করতে পারে।

কিন্তু:

```python
except Exception:
```

সবকিছুর জন্য blindly ব্যবহার করা উচিত নয়।

---

# 31. Exception Order Matters

এটা ভুল pattern:

```python
try:
    ...
except Exception:
    ...
except ValueError:
    ...
```

কারণ `ValueError` আগে থেকেই `Exception` দ্বারা catch হয়ে যাবে।

Better:

```python
try:
    ...
except ValueError:
    ...
except Exception:
    ...
```

অর্থাৎ:

```text
Specific
  ↓
General
```

---

# 32. Custom Exception

তুমি নিজের exception class তৈরি করতে পারো।

```python
class InvalidAgeError(Exception):
    pass
```

তারপর:

```python
age = -10

if age < 0:
    raise InvalidAgeError("Age cannot be negative")
```

---

# 33. Custom Exception কেন?

Large application-এ domain-specific errors useful।

যেমন AI platform:

```text
InvalidDocumentError
ModelNotAvailableError
TokenLimitExceededError
QuotaExceededError
UnsupportedFileError
ProcessingTimeoutError
```

এগুলো generic `ValueError` থেকে বেশি meaningful।

---

# 34. Custom Exception Example

```python
class InsufficientCreditsError(Exception):
    pass
```

Function:

```python
def process_document(credits):

    if credits <= 0:
        raise InsufficientCreditsError(
            "Not enough credits"
        )

    return "Processing..."
```

Handle:

```python
try:
    process_document(0)

except InsufficientCreditsError as error:
    print(error)
```

---

# 35. Exception Chaining

এক exception-এর কারণে আরেক exception হলে:

```python
try:
    number = int("abc")

except ValueError as error:
    raise RuntimeError("Data processing failed") from error
```

এখানে original exception-এর context preserve থাকে।

Concept:

```text
Original Error
      ↓
ValueError
      ↓
Application Error
      ↓
RuntimeError
```

Large systems-এ debugging-এর জন্য এটি useful।

---

# 36. `assert`

`assert` development-time assumptions check করার জন্য ব্যবহার করা যায়।

```python
age = 25

assert age >= 0
```

Condition false হলে:

```python
assert age >= 0, "Age cannot be negative"
```

---

# 37. `assert` বনাম `raise`

`assert`:

```python
assert user is not None
```

Internal assumption check-এর জন্য বেশি উপযোগী।

`raise`:

```python
if user is None:
    raise ValueError("User is required")
```

Application validation/business logic-এর জন্য বেশি explicit।

Production validation-এর ক্ষেত্রে সাধারণত `raise`/explicit validation ব্যবহার করা উচিত।

---

# 38. Traceback কী?

Exception হলে Python যে detailed error report দেয় তাকে traceback বলা হয়।

Example:

```python
def divide(a, b):
    return a / b

def calculate():
    return divide(10, 0)

calculate()
```

Output-এর মধ্যে থাকবে:

```text
Traceback
   ↓
calculate()
   ↓
divide()
   ↓
ZeroDivisionError
```

Traceback হলো debugging-এর সবচেয়ে গুরুত্বপূর্ণ information-এর একটি।

---

# 39. Traceback কীভাবে পড়বে?

সাধারণভাবে নিচ থেকে শুরু করে error type/message দেখো:

```text
Traceback ...
File ...
File ...
ZeroDivisionError: division by zero
```

শেষ line:

```text
ZeroDivisionError
```

সাধারণত মূল exception type এবং message দেয়।

তার আগের lines বলে:

> কোথা থেকে এই error পর্যন্ত execution এসেছে।

---

# 40. Debugging কী?

Debugging হলো:

> Program-এর ভুলের কারণ খুঁজে বের করে ঠিক করার process।

Flow:

```text
Bug
 ↓
Reproduce
 ↓
Understand
 ↓
Locate
 ↓
Fix
 ↓
Test
```

---

# 41. Debugging-এর First Rule

Error দেখেই code change করা শুরু করবে না।

প্রথমে:

```text
1. Error কী?
2. কোন line?
3. Input কী ছিল?
4. Expected কী ছিল?
5. Actual কী হয়েছে?
6. কেন হয়েছে?
```

---

# 42. Print Debugging

সবচেয়ে simple debugging:

```python
def calculate(a, b):

    print("a =", a)
    print("b =", b)

    result = a / b

    print("result =", result)

    return result
```

Development-এর সময় useful।

কিন্তু production application-এ structured logging বেশি ভালো।

---

# 43. Python Debugger — `breakpoint()`

Python-এ built-in debugger আছে।

```python
def calculate(a, b):

    result = a + b

    breakpoint()

    return result
```

Program ওই জায়গায় pause করবে।

তখন variables inspect করতে পারো।

---

# 44. Debugger-এ কী দেখতে পারো?

Break point-এর সময়:

```text
variables
values
execution flow
function stack
expressions
```

IDE যেমন VS Code-এ graphical debugger ব্যবহার করা যায়।

---

# 45. Logging

Production application-এ `print()`-এর পরিবর্তে logging ব্যবহার করা ভালো।

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Application started")
```

Error:

```python
logging.error("Something went wrong")
```

---

# 46. Log Levels

Common levels:

```text
DEBUG
INFO
WARNING
ERROR
CRITICAL
```

General meaning:

```text
DEBUG
↓
Detailed developer information

INFO
↓
Normal application events

WARNING
↓
Potential problem

ERROR
↓
Operation failed

CRITICAL
↓
Serious application/system problem
```

---

# 47. Exception Logging

```python
import logging

try:
    result = 10 / 0

except ZeroDivisionError:
    logging.exception("Division failed")
```

`logging.exception()` exception context/traceback সহ useful logging দেয় যখন exception handler-এর ভিতরে ব্যবহার করা হয়।

---

# 48. `except Exception` কেন dangerous হতে পারে?

ধরি:

```python
try:
    process_document()

except Exception:
    print("Failed")
```

Problem:

```text
কোন error?
কেন?
কোন document?
কোন stage?
```

কিছুই জানা যাচ্ছে না।

Better:

```python
try:
    process_document()

except Exception as error:
    logging.exception(
        "Document processing failed"
    )
```

এতে diagnosis সহজ হয়।

---

# 49. API Error Handling Concept

ধরি AI API:

```text
POST /api/humanize/
```

Possible errors:

```text
Invalid input
Unauthorized
File too large
Model unavailable
Quota exceeded
Timeout
Server error
```

Backend-এর দায়িত্ব:

```text
Internal Exception
       ↓
Catch
       ↓
Log technical details
       ↓
Return safe client response
```

Client-কে raw traceback দেওয়া উচিত নয়।

---

# 50. User Error vs System Error

এটা খুব গুরুত্বপূর্ণ।

### User input error

```text
Invalid text
Empty document
Unsupported file
```

Client-কে meaningful message দেওয়া যায়।

### System error

```text
Database failure
Model crash
Internal service failure
```

Client-কে generic message:

```text
"Something went wrong. Please try again."
```

আর technical details server-side log করা উচিত।

---

# 51. AI Model Error Handling

ধরি:

```python
def predict(model, text):
    return model(text)
```

Model failure হতে পারে।

Better concept:

```python
def predict(model, text):

    if not text:
        raise ValueError("Text is required")

    try:
        return model(text)

    except Exception as error:
        logging.exception("Model inference failed")
        raise
```

এখানে:

```text
Validation
 ↓
Inference
 ↓
Error logging
 ↓
Re-raise
```

---

# 52. Exception Handling-এর Golden Rule

এই pattern মনে রাখো:

```python
try:
    risky_operation()

except SpecificError as error:
    handle_error(error)

else:
    success_logic()

finally:
    cleanup()
```

এটাই basic professional structure।

---

# 53. কিন্তু সব Code `try`-এর ভিতরে রাখবে না

Bad:

```python
try:
    user = get_user()
    text = clean_text()
    result = model.predict(text)
    save_result(result)
    send_email()

except Exception:
    print("Error")
```

এখানে কোন operation fail করেছে বোঝা কঠিন।

Better:

```python
user = get_user()

text = clean_text(user)

try:
    result = model.predict(text)

except ModelError:
    ...

save_result(result)
```

যে operation risky, সেটার কাছাকাছি exception handling রাখো।

---

# 54. Fail Fast

Invalid input হলে শুরুতেই reject করো।

```python
def process(text):

    if not text:
        raise ValueError("Text is required")

    if len(text) > 10000:
        raise ValueError("Text too long")

    ...
```

এতে unnecessary processing হবে না।

---

# 55. Defensive Programming

মানে সম্ভাব্য problem আগে চিন্তা করে code লেখা।

Example:

```python
def get_email(user):

    if user is None:
        return None

    return user.get("email")
```

কিন্তু defensive programming অতিরিক্ত করাও ঠিক নয়। Valid assumptions এবং explicit contracts রাখা ভালো।

---

# 56. Exception Handling Anti-Pattern

### 1. Empty except

```python
try:
    ...
except:
    pass
```

এটা dangerous।

Error silently disappear হয়ে যায়।

---

# 57. Silent Failure

```python
try:
    process_data()

except Exception:
    pass
```

Problem:

```text
Error হয়েছে
কিন্তু তুমি জানো না
```

Production debugging nightmare হতে পারে।

---

# 58. আরেকটি ভুল — সবকিছুকে Exception

```python
try:
    x = 10
except Exception:
    ...
```

Risk না থাকলে unnecessary `try/except` লিখো না।

Exception handling purposeful হওয়া উচিত।

---

# 59. আরেকটি ভুল — Error Message হারিয়ে ফেলা

Bad:

```python
except Exception:
    print("Error")
```

Better:

```python
except Exception as error:
    print(error)
```

Production:

```python
except Exception:
    logging.exception("Processing failed")
```

---

# 60. আরেকটি গুরুত্বপূর্ণ বিষয় — Cleanup

যদি resource manually manage করো:

```python
resource = acquire()

try:
    process(resource)

finally:
    release(resource)
```

এখানে error হলেও resource release হবে।

---

# 61. Exception Handling Architecture

Production application-এ conceptually:

```text
                 Application
                     │
         ┌───────────┴───────────┐
         ↓                       ↓
     Validation              Processing
         │                       │
         ↓                       ↓
   User Errors              System Errors
         │                       │
         ↓                       ↓
 Client Response             Logging
                                 │
                                 ↓
                           Monitoring
```

---

# 62. AI Writing Platform Example

তোমার future platform:

```text
User submits text
       ↓
Validate input
       ↓
Token limit check
       ↓
AI model
       ↓
Generate candidates
       ↓
Rank results
       ↓
Save result
       ↓
Return response
```

Potential exceptions:

```text
InvalidTextError
TokenLimitExceededError
ModelUnavailableError
InferenceTimeoutError
DatabaseError
```

এই errors আলাদা করে design করা যায়।

---

# 63. Mini Project — Safe Calculator

একটি calculator তৈরি করো:

```python
def divide(a, b):
    ...
```

Requirements:

1. `b == 0` হলে error handle করবে
2. invalid input হলে handle করবে
3. successful result return করবে
4. meaningful error message দেবে

Expected behavior:

```text
10 / 2
→ 5
```

এবং:

```text
10 / 0
→ Cannot divide by zero
```

---

# 64. Mini Project — AI Text Validator

Function:

```python
def validate_text(text):
    ...
```

Requirements:

```text
Empty text
↓
ValueError

Text too long
↓
ValueError

Valid text
↓
return True
```

Example:

```python
validate_text("")
```

→ error

---

# 65. Challenge — Custom Exceptions

এই exception classes তৈরি করো:

```python
class InvalidDocumentError(Exception):
    pass

class TokenLimitExceededError(Exception):
    pass

class ModelUnavailableError(Exception):
    pass
```

তারপর:

```python
def process_document(text):
    ...
```

Rules:

```text
empty
→ InvalidDocumentError

too long
→ TokenLimitExceededError

model unavailable
→ ModelUnavailableError
```

---

# 66. Challenge — Full Error Pipeline

এই architecture implement করার চেষ্টা করো:

```text
Input
 ↓
validate()
 ↓
clean()
 ↓
analyze()
 ↓
generate()
 ↓
save()
```

প্রতিটি function-এর নিজস্ব error হতে পারে।

Example:

```python
class ValidationError(Exception):
    pass

class AnalysisError(Exception):
    pass

class GenerationError(Exception):
    pass

class StorageError(Exception):
    pass
```

এখন centralized handling design করো।

---

# 67. Debugging Practice

এই code-এ error খুঁজে বের করো:

```python
def calculate(numbers):

    total = 0

    for i in range(len(numbers) + 1):
        total += numbers[i]

    return total


numbers = [10, 20, 30]

print(calculate(numbers))
```

Hint:

`range()` এবং valid index নিয়ে চিন্তা করো।

---

# 68. Debugging Practice 2

```python
def get_score(data):

    return data["score"]


result = {
    "name": "AI"
}

print(get_score(result))
```

কোন exception হবে?

কীভাবে safe করবে?

---

# 69. Debugging Practice 3

```python
def process(text):

    words = text.split()

    return words[10]


print(process("Python is easy"))
```

কোন error?

কীভাবে fix করবে?

---

# 70. M01.11 Final Mental Model

পুরো exception system:

```text id="9n8e6u"
                 Python Program
                       │
                       ↓
                  Error occurs
                       │
                       ↓
                   Exception
                       │
                       ↓
                     try
                       │
              ┌────────┴────────┐
              ↓                 ↓
           Success            Error
              ↓                 ↓
            else             except
              │                 │
              └────────┬────────┘
                       ↓
                    finally
                       │
                       ↓
                    Continue
```

আর custom error:

```text id="1w9q6n"
Business Rule
      ↓
   raise
      ↓
Custom Exception
      ↓
Exception Handler
      ↓
Log
      ↓
Safe Response
```

---

# ✅ M01.11 Completion Checklist

### Error Fundamentals

* [ ] Error কী বুঝেছি
* [ ] SyntaxError বুঝেছি
* [ ] Runtime exception বুঝেছি
* [ ] Exception কী বুঝেছি
* [ ] Common exception চিনতে পারি
* [ ] Traceback পড়তে পারি

### Exception Handling

* [ ] `try`
* [ ] `except`
* [ ] specific exception
* [ ] multiple exceptions
* [ ] exception object
* [ ] `else`
* [ ] `finally`
* [ ] `raise`
* [ ] re-raise
* [ ] exception chaining

### Exception Design

* [ ] Exception hierarchy
* [ ] custom exception
* [ ] domain-specific exception
* [ ] `assert`
* [ ] `assert` vs `raise`
* [ ] specific → general exception order

### Debugging

* [ ] traceback বুঝি
* [ ] print debugging
* [ ] `breakpoint()`
* [ ] debugger concept
* [ ] logging
* [ ] log levels
* [ ] `logging.exception()`
* [ ] reproduce → locate → fix → test workflow

### Production Thinking

* [ ] user error vs system error
* [ ] safe API error response
* [ ] model error handling
* [ ] resource cleanup
* [ ] fail fast
* [ ] defensive programming
* [ ] silent failure avoid করা
* [ ] unnecessary `try/except` avoid করা
* [ ] AI pipeline error handling

---

## 🎯 M01.11-এর সবচেয়ে গুরুত্বপূর্ণ ৫টি বিষয়

```text
1. Specific exception ধরো
2. Error silently ignore করো না
3. Risky operation-এর কাছাকাছি handling করো
4. Technical details log করো, user-কে safe message দাও
5. Business-specific problem-এর জন্য custom exception ব্যবহার করো
```

তোমার ভবিষ্যৎ AI application-এর জন্য এই patternটি বিশেষভাবে মনে রাখবে:

```text id="s2yqrf"
User Input
    ↓
Validation
    ↓
try
    ↓
AI Processing
    ↓
Success → Result
    ↓
Exception
    ↓
Log Technical Error
    ↓
Safe API Response
```

**M01.11 complete হলে Python-এর basic error handling foundation সম্পূর্ণ হলো।**

পরবর্তী ধাপ: **M01.12 — Python Modules, Packages, Imports & Project Structure Deep Dive** — যেখানে `import`, `from ... import`, `__name__`, `__main__`, modules, packages, `__init__.py`, absolute/relative imports, circular imports, `pip` packages এবং professional Python project structure বিস্তারিত শেখা হবে।


----
# 🚀 M01.12 — Python Modules, Packages, Imports & Project Structure Deep Dive

আজ আমরা Python-এর এমন একটি বিষয় শিখব যেটা **বড় project**, **Django/DRF**, **AI/NLP project**, এবং শেষ পর্যন্ত তোমার **AI Writing Platform** বানানোর জন্য খুব গুরুত্বপূর্ণ।

আগের lessons-এ আমরা function, data structure, generator, exception handling পর্যন্ত শিখেছি। এখন এগুলোকে কীভাবে **একাধিক file/module/package-এর মধ্যে organize** করতে হয় সেটা শিখব।

---

# 🎯 আজকের Learning Goals

M01.12 শেষে তুমি বুঝবে:

* Module কী?
* Package কী?
* Library কী?
* `import` কীভাবে কাজ করে?
* `from ... import ...`
* `as` alias
* Absolute import
* Relative import
* `__name__`
* `__main__`
* `if __name__ == "__main__"`
* Python module search path
* `sys.path`
* `PYTHONPATH`
* `__init__.py`
* Package structure
* Sub-package
* Circular import
* Import error debugging
* Standard library import
* Third-party package import
* নিজের module তৈরি করা
* বড় project structure
* AI/NLP project structure
* Django-style modular architecture
* Clean import practices

---

# 1. Module কী?

সহজভাবে:

> **একটি Python `.py` file = একটি Module**

ধরো:

```text
calculator.py
```

এর ভিতরে:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b
```

এখন `calculator.py` একটি module।

অন্য file থেকে আমরা এটি ব্যবহার করতে পারি।

```python
import calculator

print(calculator.add(10, 5))
```

Output:

```text
15
```

---

# 2. কেন Module দরকার?

ধরো তুমি সব code একটি file-এ লিখলে:

```text
main.py
```

এখানে থাকবে:

```text
User authentication
Database
AI model
Text processing
API
File processing
Payment
Email
Logging
```

কিছুদিন পর file হয়তো:

```text
main.py
```

২০,০০০+ lines হয়ে যাবে। 😵

এটা maintain করা কঠিন।

তাই আমরা ভাগ করি:

```text
auth.py
database.py
ai_model.py
text_processor.py
payment.py
email_service.py
```

এটাই modular programming।

---

# 3. Module Example

Project:

```text
project/
│
├── main.py
└── calculator.py
```

### calculator.py

```python
def add(a, b):
    return a + b


def multiply(a, b):
    return a * b
```

### main.py

```python
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

# 4. `import module`

Syntax:

```python
import module_name
```

Example:

```python
import math
```

তারপর:

```python
print(math.sqrt(25))
```

Output:

```text
5.0
```

---

# 5. `from module import function`

পুরো module import না করে নির্দিষ্ট function import করতে পারো।

```python
from math import sqrt

print(sqrt(25))
```

আর:

```python
from math import pi

print(pi)
```

---

# 6. Multiple Import

```python
from math import sqrt, pi

print(sqrt(16))
print(pi)
```

---

# 7. Alias — `as`

কোনো module-এর ছোট নাম দিতে পারো।

```python
import math as m

print(m.sqrt(25))
```

আরেকটি common example:

```python
import numpy as np
```

```python
import pandas as pd
```

এগুলো Python ecosystem-এ খুব common।

---

# 8. `from module import *`

এটা technically করা যায়:

```python
from math import *
```

তারপর:

```python
print(sqrt(25))
```

কিন্তু সাধারণত **avoid করা ভালো**।

কারণ:

```python
sqrt()
```

কোথা থেকে এসেছে সেটা বোঝা কঠিন।

Better:

```python
import math

math.sqrt(25)
```

অথবা:

```python
from math import sqrt
```

---

# 9. Module থেকে variable import

Module শুধু function রাখবে এমন না।

### config.py

```python
APP_NAME = "AI Writer"
VERSION = "1.0"
```

### main.py

```python
import config

print(config.APP_NAME)
print(config.VERSION)
```

Output:

```text
AI Writer
1.0
```

---

# 10. Module-এর ভিতরে Class

### user.py

```python
class User:

    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hello {self.name}"
```

### main.py

```python
from user import User

user = User("Atiar")

print(user.greet())
```

Output:

```text
Hello Atiar
```

---

# 11. Standard Library Modules

Python-এর সাথে অনেক module built-in থাকে।

উদাহরণ:

```python
import os
import sys
import math
import json
import random
import datetime
import pathlib
import re
import logging
```

এগুলোকে **Python Standard Library** বলা হয়।

---

# 12. `os`

```python
import os

print(os.getcwd())
```

বর্তমান working directory দেখাবে।

আর:

```python
print(os.listdir())
```

বর্তমান directory-এর file দেখাবে।

---

# 13. `sys`

```python
import sys

print(sys.version)
```

Python version দেখতে পারো।

আর:

```python
print(sys.path)
```

এটা অত্যন্ত গুরুত্বপূর্ণ।

---

# 14. `sys.path`

Python যখন:

```python
import calculator
```

দেখে, তখন Python কোথায় `calculator.py` খুঁজবে?

Python বিভিন্ন path search করে।

দেখতে:

```python
import sys

for path in sys.path:
    print(path)
```

Conceptually:

```text
import calculator
        ↓
Python search path
        ↓
calculator.py খোঁজে
        ↓
পেলে import
        ↓
না পেলে ModuleNotFoundError
```

---

# 15. `ModuleNotFoundError`

যদি লিখো:

```python
import something
```

কিন্তু module না থাকে:

```text
ModuleNotFoundError: No module named 'something'
```

এটা খুব common error।

---

# 16. Package কী?

Module:

```text
calculator.py
```

Package হলো multiple module-এর collection।

উদাহরণ:

```text
utils/
│
├── __init__.py
├── calculator.py
├── string_utils.py
└── date_utils.py
```

এখানে:

```text
utils
```

একটি package।

---

# 17. Package কেন দরকার?

বড় project:

```text
project/
│
├── users/
├── products/
├── orders/
├── payments/
├── ai/
└── utils/
```

প্রতিটি folder-এর ভিতরে অনেক module থাকতে পারে।

এভাবে project organized থাকে।

---

# 18. `__init__.py`

Traditional Python package structure:

```text
utils/
│
├── __init__.py
├── calculator.py
└── text.py
```

`__init__.py` package initialization-এর জন্য ব্যবহৃত হয়।

এটি empty-ও হতে পারে:

```python
# __init__.py
```

Modern Python-এ কিছু ক্ষেত্রে `__init__.py` ছাড়াও namespace package সম্ভব, কিন্তু সাধারণ application/project structure-এ এটি রাখা এখনও খুব common এবং পরিষ্কার।

---

# 19. Package Import

Structure:

```text
project/
│
├── main.py
│
└── utils/
    ├── __init__.py
    └── calculator.py
```

### calculator.py

```python
def add(a, b):
    return a + b
```

### main.py

```python
from utils.calculator import add

print(add(10, 20))
```

---

# 20. Package থেকে Module Import

```python
from utils import calculator

print(calculator.add(10, 20))
```

---

# 21. Nested Package

বড় project-এ package-এর ভিতর package থাকতে পারে।

```text
project/
│
├── main.py
│
└── ai/
    │
    ├── __init__.py
    │
    ├── preprocessing/
    │   ├── __init__.py
    │   ├── cleaning.py
    │   └── tokenizer.py
    │
    └── models/
        ├── __init__.py
        ├── classifier.py
        └── generator.py
```

Import:

```python
from ai.preprocessing.cleaning import clean_text
```

---

# 22. Absolute Import

Project structure:

```text
project/
│
├── main.py
└── utils/
    ├── __init__.py
    └── text.py
```

Absolute import:

```python
from utils.text import clean_text
```

এখানে পুরো package path ব্যবহার করা হয়েছে।

---

# 23. Relative Import

ধরো:

```text
project/
│
└── app/
    ├── __init__.py
    ├── service.py
    └── utils/
        ├── __init__.py
        └── text.py
```

`service.py` থেকে:

```python
from .utils.text import clean_text
```

`.` মানে:

> current package

---

# 24. দুই Dot `..`

```python
from ..utils import helper
```

`..` মানে parent package-এর দিকে যাওয়া।

Concept:

```text
.
current package

..
parent package
```

---

# 25. Absolute vs Relative Import

### Absolute

```python
from app.utils.text import clean_text
```

### Relative

```python
from .utils.text import clean_text
```

বড় application-এ দুই ধরনের import-ই দেখা যায়।

---

# 26. `__name__`

Python module-এর একটি special variable:

```python
__name__
```

নিজের file সরাসরি execute করলে:

```python
print(__name__)
```

Output:

```text
__main__
```

কিন্তু অন্য module থেকে import করলে:

```python
print(__name__)
```

Output হতে পারে:

```text
calculator
```

---

# 27. `__main__`

ধরো:

### calculator.py

```python
def add(a, b):
    return a + b


print("Calculator loaded")
```

### main.py

```python
import calculator
```

তাহলে import করলেই:

```text
Calculator loaded
```

print হবে।

কারণ module-এর top-level code execute হয়।

---

# 28. `if __name__ == "__main__"`

এটা খুব গুরুত্বপূর্ণ।

### calculator.py

```python
def add(a, b):
    return a + b


if __name__ == "__main__":
    print(add(10, 20))
```

এখন:

```bash
python calculator.py
```

Output:

```text
30
```

কিন্তু অন্য file থেকে:

```python
import calculator
```

করলে `30` print হবে না।

কারণ:

```python
__name__ == "calculator"
```

not:

```python
"__main__"
```

---

# 29. কেন এটা গুরুত্বপূর্ণ?

একটি Python file একই সাথে:

1. Module হিসেবে ব্যবহার হতে পারে
2. Standalone program হিসেবে run হতে পারে

Example:

```python
def clean_text(text):
    return text.strip().lower()


if __name__ == "__main__":
    text = "  HELLO WORLD  "
    print(clean_text(text))
```

এটা production project-এ খুব useful pattern।

---

# 30. Module Loading Concept

যখন:

```python
import calculator
```

Python broadly:

```text
import
 ↓
module search
 ↓
find module
 ↓
load module
 ↓
execute module code
 ↓
create module object
 ↓
bind name
```

---

# 31. Import একাধিকবার করলে কী হয়?

ধরো:

```python
import calculator
import calculator
import calculator
```

Python সাধারণত module বারবার নতুন করে execute করে না।

Loaded module `sys.modules`-এ রাখা হয়।

দেখতে পারো:

```python
import sys

print("math" in sys.modules)
```

---

# 32. `sys.modules`

```python
import sys

print(sys.modules)
```

এখানে বর্তমানে loaded module-এর references পাওয়া যাবে।

Concept:

```text
import module
     ↓
sys.modules check
     ↓
already loaded?
   /       \
 yes       no
 ↓          ↓
reuse     load
```

এটি Python import system বোঝার জন্য গুরুত্বপূর্ণ।

---

# 33. Circular Import

এটি বড় project-এর common problem।

ধরো:

```text
a.py
b.py
```

`a.py`:

```python
from b import something
```

`b.py`:

```python
from a import something
```

এখন:

```text
a → b → a → b → ...
```

এ ধরনের dependency সমস্যা তৈরি হতে পারে।

---

# 34. Circular Import কেন খারাপ?

Error হতে পারে:

```text
ImportError
```

অথবা:

```text
cannot import name ...
```

কারণ module পুরোপুরি initialize হওয়ার আগেই অন্য module তাকে import করতে চাচ্ছে।

---

# 35. Circular Import Avoid করার উপায়

### Method 1 — Architecture improve

Bad:

```text
users → orders
orders → users
```

Better:

```text
users
orders
shared
```

Shared logic আলাদা module-এ রাখো।

---

### Method 2 — Common functionality আলাদা করো

```text
utils/
    validators.py
    helpers.py
```

তারপর:

```text
users → validators
orders → validators
```

এতে circular dependency কমে।

---

# 36. Third-Party Package

Python-এর বাইরে install করা package:

```bash
pip install requests
```

তারপর:

```python
import requests
```

এগুলো standard library নয়।

---

# 37. Standard vs Third-party vs Local

তিন ধরনের import:

```text
1. Standard Library
2. Third-party package
3. Your own project modules
```

Example:

```python
import os
import json

import requests
import numpy as np

from app.utils.text import clean_text
```

---

# 38. Import Organization

সাধারণত imports এভাবে organize করা ভালো:

```python
# Standard library
import os
import json

# Third-party
import numpy as np
import pandas as pd

# Local
from app.utils.text import clean_text
```

এতে code readable হয়।

---

# 39. নিজের Utility Package

ধরো AI project:

```text
ai_writer/
│
├── main.py
│
└── utils/
    ├── __init__.py
    ├── text.py
    ├── validation.py
    └── formatting.py
```

### text.py

```python
def clean_text(text):
    return text.strip()
```

### validation.py

```python
def validate_text(text):
    return bool(text.strip())
```

### main.py

```python
from utils.text import clean_text
from utils.validation import validate_text

text = "  Hello AI  "

if validate_text(text):
    text = clean_text(text)

print(text)
```

---

# 40. AI Writing Project Structure

তোমার future project-এর জন্য modular structure এমন হতে পারে:

```text
ai_writer/
│
├── app/
│   │
│   ├── __init__.py
│   │
│   ├── api/
│   │   ├── __init__.py
│   │   ├── routes.py
│   │   └── schemas.py
│   │
│   ├── services/
│   │   ├── __init__.py
│   │   ├── rewriting.py
│   │   ├── detection.py
│   │   └── analysis.py
│   │
│   ├── models/
│   │   ├── __init__.py
│   │   ├── generator.py
│   │   └── classifier.py
│   │
│   ├── preprocessing/
│   │   ├── __init__.py
│   │   ├── cleaning.py
│   │   └── tokenizer.py
│   │
│   └── utils/
│       ├── __init__.py
│       ├── logging.py
│       └── helpers.py
│
├── tests/
│
├── requirements.txt
├── .env
└── main.py
```

এখন:

```text
API
 ↓
Service
 ↓
Preprocessing
 ↓
Model
 ↓
Post-processing
 ↓
Response
```

এই architecture পরবর্তী AI lessons-এ খুব গুরুত্বপূর্ণ হবে।

---

# 41. Module Design Principle

একটি module-এর ideally একটি clear responsibility থাকা উচিত।

Bad:

```text
everything.py
```

এর ভিতরে:

```text
database
AI
email
payment
authentication
text processing
```

Better:

```text
database.py
ai.py
email.py
payment.py
auth.py
text_processing.py
```

এটাকে বলা যায় **separation of concerns**।

---

# 42. Module Dependency

ধরো:

```text
main.py
   ↓
service.py
   ↓
model.py
   ↓
preprocessing.py
```

এখানে dependency flow clear।

কিন্তু:

```text
main → service
service → model
model → main
```

এটা avoid করা উচিত।

---

# 43. `__all__`

Package/module থেকে কোন names publicভাবে expose করবে তা control করতে `__all__` ব্যবহার করা যায়।

```python
__all__ = ["add", "subtract"]
```

Example:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def secret_function():
    pass
```

```python
__all__ = ["add", "subtract"]
```

এটি বিশেষ করে wildcard imports-এর behavior control করতে ব্যবহৃত হয়।

তবে সাধারণ application code-এ `from module import *` avoid করাই ভালো।

---

# 44. Import Error Debugging

যদি দেখো:

```text
ModuleNotFoundError
```

তাহলে check করো:

### Step 1

File আছে?

```text
calculator.py
```

### Step 2

Current directory ঠিক?

```bash
pwd
```

### Step 3

Python কোথায় খুঁজছে?

```python
import sys

print(sys.path)
```

### Step 4

Package structure ঠিক?

```text
utils/
    __init__.py
    calculator.py
```

### Step 5

Virtual environment ঠিক?

```bash
which python
```

---

# 45. `pip` Package vs Python Module

এখানে একটা গুরুত্বপূর্ণ distinction আছে।

তুমি install করতে পারো:

```bash
pip install requests
```

তারপর import:

```python
import requests
```

অর্থাৎ:

```text
pip package name
        ≠
necessarily import name
```

সবসময় package name এবং import name একই হবে এমন নয়।

---

# 46. Module vs Package vs Library vs Framework

এগুলো মনে রাখো:

| Concept   | Meaning                              |
| --------- | ------------------------------------ |
| Module    | সাধারণত একটি `.py` file              |
| Package   | Modules-এর organized collection      |
| Library   | Reusable functionality-এর collection |
| Framework | Application structure/control দেয়    |

উদাহরণ:

```text
calculator.py
     ↓
Module

utils/
     ↓
Package

NumPy
     ↓
Library

Django
     ↓
Framework
```

---

# 47. Python Project-এর Recommended Structure

ছোট project:

```text
project/
│
├── main.py
├── utils.py
└── config.py
```

Medium:

```text
project/
│
├── app/
│   ├── services/
│   ├── models/
│   └── utils/
│
├── tests/
├── main.py
└── requirements.txt
```

Large:

```text
project/
│
├── src/
│   └── application/
│       ├── api/
│       ├── domain/
│       ├── services/
│       ├── models/
│       ├── infrastructure/
│       └── utils/
│
├── tests/
├── scripts/
├── configs/
├── requirements.txt
└── pyproject.toml
```

পরবর্তীতে আমরা `pyproject.toml`-ও বিস্তারিত শিখব।

---

# 48. AI/NLP Example — Text Processing Modules

ধরো:

```text
ai_text/
│
├── main.py
│
└── text/
    ├── __init__.py
    ├── cleaning.py
    ├── sentence.py
    └── statistics.py
```

### cleaning.py

```python
def clean_text(text):
    return " ".join(text.strip().split())
```

### sentence.py

```python
def split_sentences(text):
    return text.split(".")
```

### statistics.py

```python
def word_count(text):
    return len(text.split())
```

### main.py

```python
from text.cleaning import clean_text
from text.sentence import split_sentences
from text.statistics import word_count


text = "   AI   is changing the world.   "

text = clean_text(text)

print(split_sentences(text))
print(word_count(text))
```

এটাই modular AI pipeline-এর foundation।

---

# 49. Module + Function + Generator

আমরা আগের lessons-এর knowledge combine করতে পারি।

### loader.py

```python
def load_texts(texts):
    for text in texts:
        yield text
```

### cleaning.py

```python
def clean_text(text):
    return text.strip().lower()
```

### main.py

```python
from loader import load_texts
from cleaning import clean_text

texts = [
    " Hello World ",
    " Python Is Great ",
    " AI Is Powerful "
]

for text in load_texts(texts):
    print(clean_text(text))
```

Output:

```text
hello world
python is great
ai is powerful
```

এখানে তুমি already শিখে ফেলেছ:

```text
Module
+
Function
+
Generator
+
Import
+
Pipeline
```

---

# 50. Module Architecture Mental Model

এটা খুব ভালোভাবে মনে রাখবে:

```text
                Application
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
        API       Services     Utils
                     │
               ┌─────┴─────┐
               ↓           ↓
          Preprocessing   Models
               │           │
               └─────┬─────┘
                     ↓
                  Result
```

---

# 51. M01.12 Practical Project

এখন একটি mini project বানাও:

## **Text Analyzer**

Structure:

```text
text_analyzer/
│
├── main.py
│
├── text_utils/
│   ├── __init__.py
│   ├── cleaning.py
│   ├── statistics.py
│   └── analysis.py
│
└── tests/
```

---

## `cleaning.py`

তৈরি করো:

```python
def clean_text(text):
    return " ".join(text.strip().split())
```

---

## `statistics.py`

Functions:

```python
def word_count(text):
    return len(text.split())


def character_count(text):
    return len(text)
```

---

## `analysis.py`

```python
def is_long_text(text):
    return len(text.split()) > 20
```

---

## `main.py`

```python
from text_utils.cleaning import clean_text
from text_utils.statistics import word_count, character_count
from text_utils.analysis import is_long_text


text = """
Artificial intelligence is changing
the way people work and learn.
"""

text = clean_text(text)

print("Text:", text)
print("Words:", word_count(text))
print("Characters:", character_count(text))
print("Long text:", is_long_text(text))
```

---

# 🧠 M01.12 Important Concepts

আজকের সবচেয়ে গুরুত্বপূর্ণ concepts:

```text
Python File
    ↓
Module
    ↓
Package
    ↓
Project Architecture
```

আর:

```text
import
from ... import ...
as
__name__
__main__
__init__.py
sys.path
sys.modules
absolute import
relative import
circular import
```

---

# 🔥 M01.12 Practice

## Level 1

একটি module বানাও:

```text
calculator.py
```

Functions:

```text
add()
subtract()
multiply()
divide()
```

তারপর `main.py` থেকে import করো।

---

## Level 2

Package বানাও:

```text
math_utils/
├── __init__.py
├── basic.py
└── advanced.py
```

`basic.py`:

```text
add
subtract
multiply
```

`advanced.py`:

```text
square
cube
```

তারপর `main.py` থেকে import করো।

---

## Level 3

এই structure বানাও:

```text
ai_project/
│
├── main.py
│
├── preprocessing/
│   ├── __init__.py
│   ├── cleaning.py
│   └── tokenizer.py
│
├── analysis/
│   ├── __init__.py
│   └── statistics.py
│
└── utils/
    ├── __init__.py
    └── helpers.py
```

Pipeline:

```text
Raw Text
   ↓
Cleaning
   ↓
Tokenization
   ↓
Statistics
   ↓
Result
```

---

# 🧪 Theory Questions

নিজে answer করার চেষ্টা করো:

1. Module কী?
2. Package কী?
3. Module এবং package-এর পার্থক্য কী?
4. `import` কী করে?
5. `from x import y` কী?
6. `as` কেন ব্যবহার করা হয়?
7. `__init__.py` কী?
8. `__name__` কী?
9. `__main__` কী?
10. `if __name__ == "__main__"` কেন ব্যবহার করা হয়?
11. `sys.path` কী?
12. `sys.modules` কী?
13. Absolute import কী?
14. Relative import কী?
15. Circular import কী?
16. `ModuleNotFoundError` কেন হয়?
17. Standard library কী?
18. Third-party package কী?
19. Module এবং library-এর পার্থক্য কী?
20. বড় project-এ modular architecture কেন দরকার?

---

# 🎯 M01.12 Completion Checklist

নিজেকে পরীক্ষা করো:

```text
[ ] Module বুঝি
[ ] Package বুঝি
[ ] __init__.py বুঝি
[ ] import বুঝি
[ ] from import বুঝি
[ ] alias বুঝি
[ ] absolute import বুঝি
[ ] relative import বুঝি
[ ] __name__ বুঝি
[ ] __main__ বুঝি
[ ] if __name__ == "__main__" বুঝি
[ ] sys.path বুঝি
[ ] sys.modules বুঝি
[ ] ModuleNotFoundError debug করতে পারি
[ ] Circular import বুঝি
[ ] নিজের package বানাতে পারি
[ ] AI/NLP project modularize করতে পারি
[ ] Separation of concerns বুঝি
[ ] ছোট modular project বানাতে পারি
```

### 🧩 আজকের Core Mental Model

```text
                    Python Project
                          │
             ┌────────────┼────────────┐
             ↓            ↓            ↓
          Package      Package      Module
             │
       ┌─────┼─────┐
       ↓     ↓     ↓
    Module Module Module
       │
   ┌───┴────┐
   ↓        ↓
Functions  Classes
   │
   ↓
Reusable Logic
```

**M01.12 complete হলে Python code আর শুধু আলাদা আলাদা `.py` file হিসেবে দেখবে না—তুমি এখন project-কে modules/packages হিসেবে design করা শুরু করবে।**

➡️ **Next: M01.13 — Python File Handling, Paths, JSON, CSV & Data Serialization Deep Dive**


---
# 🚀 M01.13 — Python File Handling, Paths, JSON, CSV & Data Serialization Deep Dive

আজকের lesson খুব গুরুত্বপূর্ণ। কারণ বাস্তব **AI/NLP project**, backend application, dataset processing, model configuration—সব জায়গাতেই file এবং data serialization ব্যবহার হবে।

আজ আমরা শিখব:

```text
File
 ↓
Read
 ↓
Process
 ↓
Write
 ↓
Serialize
 ↓
Store / Transfer
```

---

# 🎯 M01.13 Learning Goals

এই lesson শেষে তুমি পারবে:

* File কীভাবে open করতে হয়
* `open()` ব্যবহার
* `read()`
* `readline()`
* `readlines()`
* `write()`
* `writelines()`
* `with open()`
* File modes
* Text file handling
* Encoding
* UTF-8
* Binary files
* `pathlib`
* File path
* Directory তৈরি
* File exists check
* File rename/delete
* JSON
* JSON encode/decode
* `json.dumps()`
* `json.loads()`
* `json.dump()`
* `json.load()`
* CSV
* `csv.reader`
* `csv.writer`
* `csv.DictReader`
* `csv.DictWriter`
* Serialization
* Deserialization
* Pickle concept
* JSON vs CSV vs Pickle
* AI/NLP dataset handling
* Error handling with files
* Large file processing
* File-based mini project

---

# 1. File কী?

File হলো disk-এ data সংরক্ষণের একটি মাধ্যম।

উদাহরণ:

```text
users.txt
data.json
students.csv
config.json
model.pkl
image.jpg
video.mp4
```

Python দিয়ে এগুলো read/write করা যায়।

---

# 2. File কেন দরকার?

ধরো তোমার AI application:

```text
User
 ↓
Text
 ↓
AI Processing
 ↓
Result
```

Application বন্ধ করলে যদি result হারিয়ে যায়?

তাই result save করতে হবে:

```text
Result
 ↓
JSON
 ↓
Disk
```

Dataset:

```text
CSV
 ↓
Python
 ↓
Pandas
 ↓
Model
```

Configuration:

```text
config.json
 ↓
Python
 ↓
Application
```

---

# 3. `open()`

Python-এ file open করার basic function:

```python
open()
```

Example:

```python
file = open("data.txt", "r")
```

এখানে:

```text
data.txt → file name
r        → read mode
```

---

# 4. File Read

```python
file = open("data.txt", "r")

content = file.read()

print(content)

file.close()
```

---

# 5. `close()`

File ব্যবহার শেষে:

```python
file.close()
```

করা উচিত।

কারণ file resource system-এর সাথে connected থাকে।

---

# 6. `with open()` — Recommended

Better approach:

```python
with open("data.txt", "r") as file:
    content = file.read()

print(content)
```

এখানে Python automatically file close করবে।

এটাই সাধারণত recommended pattern।

---

# 7. Why `with`?

ধরো:

```python
file = open("data.txt")
```

তারপর মাঝখানে exception হলো:

```python
something()
```

তাহলে `close()` হয়তো execute নাও হতে পারে।

কিন্তু:

```python
with open("data.txt") as file:
    ...
```

resource cleanup automatically handle করে।

---

# 8. File Modes

সবচেয়ে গুরুত্বপূর্ণ modes:

| Mode | Meaning      |
| ---- | ------------ |
| `r`  | Read         |
| `w`  | Write        |
| `a`  | Append       |
| `x`  | Create new   |
| `b`  | Binary       |
| `t`  | Text         |
| `+`  | Read + Write |

---

# 9. Read Mode — `r`

```python
with open("data.txt", "r") as file:
    data = file.read()
```

File না থাকলে:

```text
FileNotFoundError
```

---

# 10. Write Mode — `w`

```python
with open("data.txt", "w") as file:
    file.write("Hello Python")
```

⚠️ গুরুত্বপূর্ণ:

`w` existing content overwrite করে।

আগে যদি থাকে:

```text
Hello
World
```

তারপর:

```python
with open("data.txt", "w") as file:
    file.write("New Data")
```

আগের content replace হবে।

---

# 11. Append Mode — `a`

Existing content-এর শেষে data যোগ করতে:

```python
with open("data.txt", "a") as file:
    file.write("\nNew Line")
```

Existing content থাকবে।

---

# 12. Create Mode — `x`

নতুন file create করতে:

```python
with open("new.txt", "x") as file:
    file.write("Hello")
```

File already exist করলে exception হবে:

```text
FileExistsError
```

---

# 13. `read()`

পুরো file:

```python
with open("data.txt") as file:
    data = file.read()

print(data)
```

---

# 14. `read(size)`

নির্দিষ্ট number of characters:

```python
with open("data.txt") as file:
    data = file.read(10)

print(data)
```

---

# 15. `readline()`

এক line করে পড়তে:

```python
with open("data.txt") as file:
    line = file.readline()

print(line)
```

---

# 16. Multiple `readline()`

```python
with open("data.txt") as file:

    line1 = file.readline()
    line2 = file.readline()
    line3 = file.readline()

    print(line1)
    print(line2)
    print(line3)
```

---

# 17. `readlines()`

সব line list হিসেবে:

```python
with open("data.txt") as file:
    lines = file.readlines()

print(lines)
```

Example:

```text
Hello
Python
AI
```

Result:

```python
[
    "Hello\n",
    "Python\n",
    "AI\n"
]
```

---

# 18. File Iterate করা

বড় file-এর জন্য এটি খুব useful:

```python
with open("data.txt") as file:
    for line in file:
        print(line.strip())
```

এখানে পুরো file একসাথে memory-তে load করার প্রয়োজন নেই।

এটি আমরা M01.10-এর generator/lazy evaluation-এর সাথে relate করতে পারি।

---

# 19. `write()`

```python
with open("output.txt", "w") as file:
    file.write("Python")
```

`write()` সাধারণত string নেয়।

```python
file.write("Hello")
```

কিন্তু:

```python
file.write(100)
```

সরাসরি কাজ করবে না।

Better:

```python
file.write(str(100))
```

---

# 20. `writelines()`

একাধিক string লিখতে:

```python
lines = [
    "Python\n",
    "Django\n",
    "AI\n"
]

with open("data.txt", "w") as file:
    file.writelines(lines)
```

---

# 21. New Line

```python
with open("data.txt", "w") as file:
    file.write("Hello\n")
    file.write("Python\n")
    file.write("AI\n")
```

`\n` নতুন line তৈরি করে।

---

# 22. Encoding

Text file-এর ক্ষেত্রে encoding গুরুত্বপূর্ণ।

Recommended:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

Write:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("বাংলা ভাষা")
```

UTF-8 ব্যবহার করলে বাংলা, English এবং অনেক Unicode character handle করা যায়।

---

# 23. Encoding Error

ভুল encoding ব্যবহার করলে error হতে পারে:

```text
UnicodeDecodeError
```

তাই modern application-এ সাধারণত:

```python
encoding="utf-8"
```

explicitly দেওয়া ভালো।

---

# 24. Text vs Binary

দুই ধরনের file:

```text
Text
Binary
```

Text:

```text
.txt
.csv
.json
.py
.html
```

Binary:

```text
.jpg
.png
.mp4
.pdf
.zip
```

---

# 25. Binary Mode

Binary read:

```python
with open("image.jpg", "rb") as file:
    data = file.read()
```

Binary write:

```python
with open("copy.jpg", "wb") as file:
    file.write(data)
```

Modes:

```text
rb → read binary
wb → write binary
ab → append binary
```

---

# 26. File Copy Example

```python
with open("image.jpg", "rb") as source:
    data = source.read()

with open("copy.jpg", "wb") as destination:
    destination.write(data)
```

---

# 27. File Pointer

Python file object-এর একটি current position থাকে।

```python
with open("data.txt", "r") as file:

    print(file.tell())

    data = file.read(5)

    print(data)
    print(file.tell())
```

`tell()` current position দেখায়।

---

# 28. `seek()`

File pointer move করতে:

```python
with open("data.txt", "r") as file:

    print(file.read(5))

    file.seek(0)

    print(file.read(5))
```

`seek(0)` file-এর beginning-এ ফিরে যায়।

---

# 29. File Existence — `os`

```python
import os

if os.path.exists("data.txt"):
    print("File exists")
```

---

# 30. `os.path.isfile()`

```python
import os

if os.path.isfile("data.txt"):
    print("It is a file")
```

---

# 31. `os.path.isdir()`

```python
if os.path.isdir("data"):
    print("It is a directory")
```

---

# 32. `pathlib` — Modern Approach

Python-এ path handling-এর জন্য `pathlib` খুব useful।

```python
from pathlib import Path

path = Path("data.txt")
```

---

# 33. Check File Exists

```python
from pathlib import Path

path = Path("data.txt")

if path.exists():
    print("Exists")
```

---

# 34. Check File

```python
if path.is_file():
    print("File")
```

Directory:

```python
if path.is_dir():
    print("Directory")
```

---

# 35. Create Directory

```python
from pathlib import Path

folder = Path("data")

folder.mkdir()
```

Parent directory না থাকলে:

```python
folder.mkdir(parents=True, exist_ok=True)
```

এটা practical project-এ খুব useful।

---

# 36. `Path` দিয়ে File Write

```python
from pathlib import Path

path = Path("data.txt")

path.write_text(
    "Hello Python",
    encoding="utf-8"
)
```

---

# 37. `Path` দিয়ে File Read

```python
content = path.read_text(
    encoding="utf-8"
)

print(content)
```

---

# 38. Path Joining

Traditional:

```python
import os

path = os.path.join("data", "users", "users.json")
```

`pathlib`:

```python
from pathlib import Path

path = Path("data") / "users" / "users.json"
```

এটা অনেক cleaner।

---

# 39. Parent / Name / Suffix

```python
from pathlib import Path

path = Path("data/users.json")

print(path.name)
print(path.stem)
print(path.suffix)
print(path.parent)
```

Result conceptually:

```text
name   → users.json
stem   → users
suffix → .json
parent → data
```

---

# 40. List Files

```python
from pathlib import Path

folder = Path("data")

for file in folder.iterdir():
    print(file)
```

---

# 41. Find Specific Files

```python
for file in Path(".").glob("*.txt"):
    print(file)
```

Recursive:

```python
for file in Path(".").rglob("*.txt"):
    print(file)
```

---

# 42. Rename

```python
from pathlib import Path

old = Path("old.txt")
new = Path("new.txt")

old.rename(new)
```

---

# 43. Delete

```python
path.unlink()
```

Directory delete করতে আলাদা handling প্রয়োজন।

---

# 44. File Handling + Exception Handling

আগের M01.11-এর knowledge এখানে apply হবে।

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()

except FileNotFoundError:
    print("File not found")

except PermissionError:
    print("Permission denied")
```

---

# 🟢 JSON

এখন আসি খুব গুরুত্বপূর্ণ topic-এ।

# 45. JSON কী?

JSON:

> **JavaScript Object Notation**

এটি structured data store এবং transfer করার একটি জনপ্রিয় text format।

Example:

```json
{
    "name": "Atiar",
    "age": 25,
    "skills": [
        "Python",
        "Django",
        "AI"
    ]
}
```

JSON API, configuration, frontend-backend communication ইত্যাদিতে খুব common।

---

# 46. Python Dictionary → JSON

Python:

```python
user = {
    "name": "Atiar",
    "age": 25,
    "skills": ["Python", "Django", "AI"]
}
```

JSON string বানাতে:

```python
import json

json_data = json.dumps(user)

print(json_data)
```

---

# 47. `json.dumps()`

`dumps`:

```text
Python object
     ↓
JSON string
```

Example:

```python
data = {
    "name": "Atiar",
    "active": True
}

result = json.dumps(data)

print(result)
```

---

# 48. Pretty JSON

Readable format:

```python
result = json.dumps(
    data,
    indent=4
)

print(result)
```

Output:

```json
{
    "name": "Atiar",
    "active": true
}
```

খেয়াল করো Python:

```python
True
```

JSON:

```json
true
```

---

# 49. JSON File Write

```python
import json

user = {
    "name": "Atiar",
    "age": 25,
    "skills": ["Python", "AI"]
}

with open("user.json", "w", encoding="utf-8") as file:
    json.dump(user, file, indent=4)
```

এখানে:

```text
json.dump()
```

সরাসরি file-এ JSON লিখে।

---

# 50. JSON File Read

```python
import json

with open("user.json", "r", encoding="utf-8") as file:
    user = json.load(file)

print(user)
```

এখানে JSON → Python object।

---

# 51. `loads()` vs `load()`

এটা অবশ্যই মনে রাখবে।

### `loads`

String থেকে:

```python
json.loads()
```

### `load`

File থেকে:

```python
json.load()
```

---

# 52. `dumps()` vs `dump()`

### `dumps`

Python object → JSON string

```python
json.dumps(data)
```

### `dump`

Python object → JSON file

```python
json.dump(data, file)
```

---

# 53. JSON Data Types

JSON support করে:

```text
string
number
boolean
null
array
object
```

Python mapping:

| Python  | JSON   |
| ------- | ------ |
| `dict`  | object |
| `list`  | array  |
| `str`   | string |
| `int`   | number |
| `float` | number |
| `True`  | true   |
| `False` | false  |
| `None`  | null   |

---

# 54. AI Project JSON Example

ধরো AI text analysis result:

```python
result = {
    "text": "Artificial intelligence is powerful.",
    "score": 0.91,
    "label": "AI-like",
    "sentences": [
        {
            "text": "Artificial intelligence is powerful.",
            "score": 0.91
        }
    ]
}
```

Save:

```python
import json

with open("analysis.json", "w", encoding="utf-8") as file:
    json.dump(result, file, indent=4)
```

এ ধরনের structure API response এবং saved analysis result-এ useful।

---

# 🟢 CSV

# 55. CSV কী?

CSV:

> **Comma-Separated Values**

Example:

```csv
name,age,score
Atiar,25,90
Rahim,24,85
Karim,26,88
```

Dataset-এর জন্য CSV খুব common।

---

# 56. CSV Read

```python
import csv

with open("students.csv", "r", encoding="utf-8") as file:

    reader = csv.reader(file)

    for row in reader:
        print(row)
```

Output:

```text
['name', 'age', 'score']
['Atiar', '25', '90']
['Rahim', '24', '85']
```

খেয়াল করো CSV থেকে values সাধারণত string হিসেবে আসে।

---

# 57. CSV Write

```python
import csv

rows = [
    ["name", "age"],
    ["Atiar", 25],
    ["Rahim", 24]
]

with open(
    "students.csv",
    "w",
    newline="",
    encoding="utf-8"
) as file:

    writer = csv.writer(file)

    writer.writerows(rows)
```

---

# 58. `writerow()`

একটি row:

```python
writer.writerow(["Atiar", 25])
```

Multiple:

```python
writer.writerows(rows)
```

---

# 59. `DictReader`

CSV data dictionary হিসেবে পড়তে:

```python
import csv

with open("students.csv", encoding="utf-8") as file:

    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

Result:

```python
{
    "name": "Atiar",
    "age": "25"
}
```

এটা structured processing-এর জন্য খুব useful।

---

# 60. `DictWriter`

```python
import csv

fieldnames = ["name", "age", "score"]

with open(
    "students.csv",
    "w",
    newline="",
    encoding="utf-8"
) as file:

    writer = csv.DictWriter(
        file,
        fieldnames=fieldnames
    )

    writer.writeheader()

    writer.writerow({
        "name": "Atiar",
        "age": 25,
        "score": 90
    })
```

---

# 61. CSV Dataset Example

AI/NLP dataset:

```csv
text,label
"AI is powerful",ai
"Python is useful",human
"Machine learning is growing",ai
```

Python:

```python
import csv

with open("dataset.csv", encoding="utf-8") as file:

    reader = csv.DictReader(file)

    for row in reader:
        text = row["text"]
        label = row["label"]

        print(text, label)
```

---

# 🟣 Serialization

# 62. Serialization কী?

Serialization:

> Python object → এমন format যা save বা transfer করা যায়।

Concept:

```text
Python Object
      ↓
Serialization
      ↓
JSON / Pickle / etc.
      ↓
Storage / Network
```

---

# 63. Deserialization

উল্টো process:

```text
Stored Data
     ↓
Deserialization
     ↓
Python Object
```

---

# 64. JSON Serialization

```python
data = {
    "name": "Atiar",
    "score": 95
}
```

Serialize:

```python
json_string = json.dumps(data)
```

Deserialize:

```python
data = json.loads(json_string)
```

---

# 65. Pickle

Python object serialize করার জন্য:

```python
import pickle
```

Example:

```python
data = {
    "name": "Atiar",
    "score": 95
}

with open("data.pkl", "wb") as file:
    pickle.dump(data, file)
```

Read:

```python
with open("data.pkl", "rb") as file:
    data = pickle.load(file)
```

---

# ⚠️ 66. Pickle Security Warning

খুব গুরুত্বপূর্ণ:

> **Untrusted pickle file কখনো load করবে না।**

কারণ malicious pickle data loading-এর সময় arbitrary code execution-এর ঝুঁকি তৈরি করতে পারে।

তাই user-uploaded/untrusted data-এর ক্ষেত্রে JSON বা safer structured formats prefer করা উচিত।

---

# 67. JSON vs Pickle

| Feature                      | JSON            | Pickle                           |
| ---------------------------- | --------------- | -------------------------------- |
| Human-readable               | ✅               | ❌                                |
| Python-specific              | ❌               | ✅                                |
| Web/API friendly             | ✅               | ❌                                |
| Security with untrusted data | তুলনামূলক safer | ⚠️ unsafe to load untrusted data |
| Cross-language               | ✅               | ❌/limited                        |
| Complex Python objects       | Limited         | ✅                                |

---

# 68. JSON vs CSV

| Feature                | JSON        | CSV         |
| ---------------------- | ----------- | ----------- |
| Nested data            | ✅           | ❌           |
| Tabular data           | ভালো        | ⭐ Excellent |
| API                    | ⭐ Excellent | কম          |
| Human readable         | ✅           | ✅           |
| Dataset                | ভালো        | ⭐ Excellent |
| Hierarchical structure | ✅           | ❌           |

---

# 69. কোনটা কখন ব্যবহার করবে?

### CSV

যখন data:

```text
Rows + Columns
```

যেমন:

```text
ML dataset
student data
sales data
```

### JSON

যখন:

```text
Nested / structured data
```

যেমন:

```text
API response
configuration
AI analysis result
user settings
```

### Pickle

Python-specific object serialization-এর ক্ষেত্রে ব্যবহার হতে পারে, কিন্তু untrusted input-এর জন্য নয়।

---

# 70. AI Project Data Flow

একটি AI application:

```text
CSV Dataset
     ↓
Python
     ↓
Preprocessing
     ↓
Model
     ↓
Prediction
     ↓
JSON
     ↓
API
```

---

# 71. Configuration JSON

ধরো:

```text
config.json
```

```json
{
    "model": "text-model",
    "threshold": 0.85,
    "max_tokens": 512
}
```

Python:

```python
import json

with open("config.json", encoding="utf-8") as file:
    config = json.load(file)

print(config["model"])
print(config["threshold"])
```

---

# 72. JSON + Exception Handling

```python
import json

try:
    with open("config.json", encoding="utf-8") as file:
        config = json.load(file)

except FileNotFoundError:
    print("Config file missing")

except json.JSONDecodeError:
    print("Invalid JSON")
```

এখানে M01.11-এর exception handling সরাসরি ব্যবহার হচ্ছে।

---

# 73. Large File Processing

Bad:

```python
with open("large.txt") as file:
    data = file.read()
```

যদি file খুব বড় হয়, memory pressure হতে পারে।

Better:

```python
with open("large.txt") as file:
    for line in file:
        process(line)
```

এটা M01.10-এর lazy iteration-এর সাথে directly related।

---

# 74. Large JSON?

যদি JSON অত্যন্ত বড় হয়:

```python
json.load(file)
```

পুরো JSON memory-তে load করতে পারে।

Large-scale systems-এ তখন ব্যবহার করা যায়:

* JSON Lines / NDJSON
* streaming parsers
* database
* object storage
* chunked processing

JSON Lines example:

```text
{"text": "Hello", "label": "human"}
{"text": "AI is powerful", "label": "ai"}
{"text": "Python is useful", "label": "human"}
```

প্রতিটি line একটি JSON object।

---

# 75. JSON Lines Processing

```python
import json

with open("data.jsonl", encoding="utf-8") as file:

    for line in file:
        record = json.loads(line)

        print(record)
```

এটি বড় NLP/ML dataset processing-এ খুব useful।

---

# 76. File + Generator

আগের generator lesson-এর সাথে combine করি:

```python
import json

def read_jsonl(path):

    with open(path, encoding="utf-8") as file:

        for line in file:
            yield json.loads(line)
```

তারপর:

```python
for record in read_jsonl("dataset.jsonl"):
    print(record)
```

এখানে:

```text
File
 ↓
Generator
 ↓
One record
 ↓
Process
 ↓
Next record
```

এটা scalable data processing-এর foundation।

---

# 77. AI Dataset Pipeline

একটি বাস্তব NLP dataset pipeline:

```text
dataset.jsonl
      ↓
read_jsonl()
      ↓
clean_text()
      ↓
tokenize()
      ↓
validate()
      ↓
model
      ↓
prediction
```

তুমি M01.06, M01.07, M01.10, M01.11 এবং আজকের M01.13-এর concepts একসাথে ব্যবহার করতে পারছো।

---

# 78. File Handling Best Practices

### 1. `with` ব্যবহার করো

```python
with open(...) as file:
    ...
```

### 2. Encoding explicitly দাও

```python
encoding="utf-8"
```

### 3. Large file পুরোটা read করো না

```python
for line in file:
```

### 4. Error handle করো

```python
try:
    ...
except FileNotFoundError:
    ...
```

### 5. Path-এর জন্য `pathlib` prefer করো

```python
Path("data") / "file.json"
```

### 6. User input blindly file path হিসেবে ব্যবহার করো না

Security-এর জন্য path validation দরকার হতে পারে।

---

# 79. File Path Security

ধরো application user-এর কাছ থেকে filename নেয়:

```python
filename = input("Filename: ")
```

তারপর:

```python
open(filename)
```

এটা production application-এ dangerous হতে পারে।

কারণ malicious user unexpected path access করার চেষ্টা করতে পারে।

তাই production system-এ:

```text
User Input
   ↓
Validate
   ↓
Allowed Directory
   ↓
Safe Path
   ↓
File Access
```

---

# 80. Mini Project — AI Text Dataset Manager

এখন একটি project বানাও।

Structure:

```text
text_dataset/
│
├── main.py
│
├── data/
│   ├── input.json
│   └── output.json
│
└── utils/
    ├── __init__.py
    ├── file_utils.py
    └── text_utils.py
```

---

## `text_utils.py`

```python
def clean_text(text):
    return " ".join(text.strip().split())


def word_count(text):
    return len(text.split())
```

---

## `file_utils.py`

```python
import json


def load_json(path):

    with open(path, encoding="utf-8") as file:
        return json.load(file)


def save_json(data, path):

    with open(path, "w", encoding="utf-8") as file:
        json.dump(data, file, indent=4)
```

---

## `main.py`

```python
from utils.file_utils import load_json, save_json
from utils.text_utils import clean_text, word_count


data = load_json("data/input.json")

results = []

for item in data:

    text = clean_text(item["text"])

    result = {
        "original": item["text"],
        "cleaned": text,
        "word_count": word_count(text)
    }

    results.append(result)


save_json(results, "data/output.json")
```

---

# 81. Input JSON

`input.json`:

```json
[
    {
        "text": "   Artificial intelligence is powerful.   "
    },
    {
        "text": "   Python is useful for AI.   "
    }
]
```

Output:

```json
[
    {
        "original": "   Artificial intelligence is powerful.   ",
        "cleaned": "Artificial intelligence is powerful.",
        "word_count": 5
    },
    {
        "original": "   Python is useful for AI.   ",
        "cleaned": "Python is useful for AI.",
        "word_count": 5
    }
]
```

---

# 🧠 পুরো M01.13 Mental Model

এটা মনে রাখবে:

```text
                    FILE SYSTEM
                        │
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
        Text          JSON           CSV
          │             │             │
       read/write    load/dump    reader/writer
          │             │             │
          └─────────────┼─────────────┘
                        ↓
                 Python Objects
                        ↓
                  Processing
                        ↓
                 Serialization
                        ↓
                  Save / Transfer
```

আর বড় dataset-এর ক্ষেত্রে:

```text
Large File
    ↓
Iterator
    ↓
Generator
    ↓
One Record
    ↓
Process
    ↓
Next Record
```

---

# 🧪 M01.13 Practice

## Level 1 — Text File

একটি program বানাও:

```text
notes.txt
```

Program:

1. file create করবে
2. 5টি line লিখবে
3. file read করবে
4. line count করবে
5. word count করবে

---

## Level 2 — JSON

`users.json` তৈরি করো:

```json
[
    {
        "name": "Atiar",
        "age": 25
    },
    {
        "name": "Rahim",
        "age": 24
    }
]
```

Python দিয়ে:

* load করো
* average age বের করো
* নতুন user add করো
* আবার save করো

---

## Level 3 — CSV

`students.csv`:

```csv
name,score
Atiar,90
Rahim,85
Karim,88
```

Program:

```text
CSV read
 ↓
scores extract
 ↓
average calculate
 ↓
highest score
 ↓
result.json
```

---

# 🔥 Level 4 — AI/NLP Challenge

একটি `dataset.jsonl` তৈরি করো:

```text
{"text": "AI is changing the world.", "label": "ai"}
{"text": "Python is easy to learn.", "label": "human"}
{"text": "Machine learning is powerful.", "label": "ai"}
```

Program:

```text
JSONL
 ↓
Generator
 ↓
Read one record
 ↓
Clean text
 ↓
Word count
 ↓
Save result
```

Output:

```json
{
    "text": "AI is changing the world.",
    "label": "ai",
    "word_count": 5
}
```

---

# 📝 Theory Questions

নিজে answer করার চেষ্টা করো:

1. File কী?
2. `open()` কী করে?
3. `r`, `w`, `a`, `x` এর difference কী?
4. `with open()` কেন ব্যবহার করা হয়?
5. `read()` কী করে?
6. `readline()` কী করে?
7. `readlines()` কী করে?
8. `write()` এবং `writelines()` এর difference কী?
9. Encoding কী?
10. UTF-8 কেন গুরুত্বপূর্ণ?
11. Text এবং binary file-এর difference কী?
12. `rb` এবং `wb` কী?
13. `tell()` কী?
14. `seek()` কী?
15. `pathlib` কী?
16. `Path` কেন useful?
17. JSON কী?
18. `dump()` এবং `dumps()` এর difference কী?
19. `load()` এবং `loads()` এর difference কী?
20. JSON এবং CSV-এর difference কী?
21. CSV dataset-এর জন্য কেন useful?
22. Serialization কী?
23. Deserialization কী?
24. Pickle কী?
25. Untrusted pickle load করা কেন unsafe?
26. Large file কীভাবে memory-efficientভাবে process করবে?
27. JSONL কী?
28. JSONL + generator কেন AI/NLP dataset-এর জন্য useful?
29. File handling-এ `FileNotFoundError` কীভাবে handle করবে?
30. Production application-এ user-provided file path কেন validate করতে হবে?

---

# ✅ M01.13 Completion Checklist

```text
[ ] open()
[ ] close()
[ ] with open()
[ ] r
[ ] w
[ ] a
[ ] x
[ ] rb
[ ] wb
[ ] read()
[ ] readline()
[ ] readlines()
[ ] write()
[ ] writelines()
[ ] encoding
[ ] UTF-8
[ ] tell()
[ ] seek()
[ ] pathlib
[ ] Path
[ ] mkdir()
[ ] exists()
[ ] is_file()
[ ] is_dir()
[ ] glob()
[ ] rename()
[ ] unlink()
[ ] JSON
[ ] json.load()
[ ] json.loads()
[ ] json.dump()
[ ] json.dumps()
[ ] CSV
[ ] csv.reader
[ ] csv.writer
[ ] DictReader
[ ] DictWriter
[ ] Serialization
[ ] Deserialization
[ ] Pickle concept
[ ] Pickle security
[ ] JSONL
[ ] Large file processing
[ ] Generator + file processing
[ ] File exception handling
[ ] AI/NLP dataset processing
```

## 🔗 Previous Lessons-এর সাথে Connection

এখন পর্যন্ত তোমার Python foundation:

```text
M01.01
Python Environment
       ↓
M01.02
Variables + Object Model
       ↓
M01.03
Data Types
       ↓
M01.04
Operators
       ↓
M01.05
Control Flow
       ↓
M01.06
Loops + Iteration
       ↓
M01.07
Functions
       ↓
M01.08
Advanced Functions
       ↓
M01.09
Data Structures
       ↓
M01.10
Iterators + Generators
       ↓
M01.11
Exception Handling
       ↓
M01.12
Modules + Packages
       ↓
👉 M01.13
Files + JSON + CSV + Serialization
```

এখন Python-এর **core foundation অনেক শক্ত হচ্ছে**। পরবর্তী ধাপে আমরা আরও গুরুত্বপূর্ণ Python concepts-এর দিকে যাব, যেগুলো পরে backend এবং AI/NLP code-এ সরাসরি ব্যবহার হবে।

➡️ **Next: M01.14 — Python Object-Oriented Programming (OOP) Deep Dive: Class, Object, Constructor, Inheritance, Polymorphism, Encapsulation & Abstraction**


----
# 🚀 M01.14 — Python Object-Oriented Programming (OOP) Deep Dive

আজকের lesson **খুবই গুরুত্বপূর্ণ**। কারণ Django, Django REST Framework, PyTorch, TensorFlow, Hugging Face—সব জায়গাতেই OOP-এর ব্যবহার দেখতে পাবে।

আমরা শুধু `class` এবং `object` শিখব না; বরং **OOP কীভাবে চিন্তা করতে হয়**, inheritance, polymorphism, encapsulation, abstraction এবং বাস্তব AI project-এ এগুলো কোথায় ব্যবহার হবে—সব দেখব।

---

# 🎯 M01.14 Learning Goals

এই lesson শেষে তুমি বুঝবে:

* OOP কী?
* কেন OOP দরকার?
* Class
* Object
* Attribute
* Method
* Constructor
* `self`
* `__init__`
* Instance attribute
* Class attribute
* Instance method
* Class method
* Static method
* Encapsulation
* Public / Protected / Private convention
* Getter / Setter
* Property
* Inheritance
* Method overriding
* `super()`
* Multiple inheritance
* MRO
* Polymorphism
* Duck typing
* Abstraction
* Abstract class
* `ABC`
* `@abstractmethod`
* Composition
* Aggregation
* Association
* Magic/Dunder methods
* `__str__`
* `__repr__`
* `__len__`
* `__eq__`
* `__add__`
* Dataclass
* OOP design principles
* AI/NLP project architecture
* Common OOP mistakes

---

# 1. OOP কী?

OOP = **Object-Oriented Programming**

Programming-এর একটি paradigm যেখানে application-কে **objects** এবং তাদের behavior-এর মাধ্যমে design করা হয়।

সহজভাবে:

```text
Object
 ├── Data
 └── Behavior
```

উদাহরণ:

```text
User
 ├── name
 ├── email
 └── login()
```

এখানে:

```text
name/email → Data
login()    → Behavior
```

---

# 2. Real-world Example

একজন Student:

```text
Student
│
├── name
├── id
├── department
│
├── study()
├── attend_exam()
└── get_result()
```

Python:

```python
class Student:

    def study(self):
        print("Student is studying")

    def attend_exam(self):
        print("Student is attending exam")
```

---

# 3. Class কী?

Class হলো একটি **blueprint/template**।

উদাহরণ:

```python
class Car:
    pass
```

এখানে `Car` হলো class।

এখন class থেকে object তৈরি করা যায়।

---

# 4. Object কী?

Class-এর instance হলো object।

```python
class Car:
    pass


car1 = Car()
car2 = Car()
```

এখানে:

```text
Car → Class

car1 → Object
car2 → Object
```

Mental model:

```text
Class
  │
  ├── Object 1
  ├── Object 2
  └── Object 3
```

---

# 5. Attribute কী?

Object-এর data হলো attribute।

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Object:

```python
student = Student("Atiar", 25)
```

Attributes:

```python
student.name
student.age
```

---

# 6. Method কী?

Class-এর ভিতরের function হলো method।

```python
class Student:

    def study(self):
        print("Studying")
```

এখানে:

```text
study()
```

হলো method।

Call:

```python
student.study()
```

---

# 7. `__init__()`

`__init__()` হলো initializer method।

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

যখন:

```python
student = Student("Atiar", 25)
```

তখন initialization logic execute হয়।

---

# 8. `self` কী?

`self` বর্তমান object-কে reference করে।

```python
class Student:

    def __init__(self, name):
        self.name = name
```

যখন:

```python
student1 = Student("Atiar")
student2 = Student("Rahim")
```

তখন conceptually:

```text
student1
 └── name = Atiar

student2
 └── name = Rahim
```

`self` দিয়ে current object-এর attributes access করা হয়।

---

# 9. `self` আসলে কী?

এই:

```python
student.study()
```

Python-এর method call-এর conceptually কাছাকাছি:

```python
Student.study(student)
```

অর্থাৎ object নিজেকে method-এর প্রথম argument হিসেবে দেয়।

---

# 10. Complete Class Example

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print(f"My name is {self.name}")
        print(f"I am {self.age} years old")


student = Student("Atiar", 25)

student.introduce()
```

Output:

```text
My name is Atiar
I am 25 years old
```

---

# 11. Multiple Objects

```python
student1 = Student("Atiar", 25)
student2 = Student("Rahim", 24)
student3 = Student("Karim", 26)
```

প্রতিটি object-এর নিজস্ব data থাকে।

```text
student1 → Atiar
student2 → Rahim
student3 → Karim
```

---

# 12. Instance Attribute

যে attribute প্রতিটি object-এর আলাদা:

```python
class User:

    def __init__(self, name):
        self.name = name
```

এখানে:

```python
self.name
```

instance attribute।

---

# 13. Class Attribute

Class-এর shared attribute:

```python
class User:

    platform = "AI Writer"

    def __init__(self, name):
        self.name = name
```

এখন:

```python
user1 = User("Atiar")
user2 = User("Rahim")

print(user1.platform)
print(user2.platform)
```

দুজনই:

```text
AI Writer
```

ব্যবহার করবে।

---

# 14. Instance vs Class Attribute

```python
class User:

    platform = "AI Writer"

    def __init__(self, name):
        self.name = name
```

এখানে:

```text
platform → Class attribute
name     → Instance attribute
```

Mental model:

```text
Class
 │
 ├── platform = AI Writer
 │
 ├── user1
 │    └── name = Atiar
 │
 └── user2
      └── name = Rahim
```

---

# 15. Instance Method

সবচেয়ে common method:

```python
class User:

    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hello {self.name}"
```

এখানে `greet()` instance method।

---

# 16. Class Method

Class-level behavior-এর জন্য:

```python
class User:

    platform = "AI Writer"

    @classmethod
    def get_platform(cls):
        return cls.platform
```

Call:

```python
print(User.get_platform())
```

এখানে `cls` current class-কে reference করে।

---

# 17. `self` vs `cls`

```text
self → object/instance
cls  → class
```

Instance method:

```python
def method(self):
    ...
```

Class method:

```python
@classmethod
def method(cls):
    ...
```

---

# 18. Static Method

যে method class বা instance-এর data directly ব্যবহার করে না:

```python
class MathUtils:

    @staticmethod
    def add(a, b):
        return a + b
```

Call:

```python
print(MathUtils.add(10, 20))
```

এখানে `self` বা `cls` লাগে না।

---

# 19. Three Method Types

| Method   | First parameter | Use           |
| -------- | --------------- | ------------- |
| Instance | `self`          | Object data   |
| Class    | `cls`           | Class data    |
| Static   | none            | Utility logic |

---

# 20. Encapsulation

Encapsulation মানে data এবং behavior এক unit-এর মধ্যে organize করা এবং internal implementation-এর access control/design করা।

Example:

```python
class BankAccount:

    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
```

Data:

```text
balance
```

Behavior:

```text
deposit()
```

একসাথে class-এর মধ্যে।

---

# 21. Public Attribute

```python
class User:

    def __init__(self):
        self.name = "Atiar"
```

এটি public convention।

Access:

```python
user.name
```

---

# 22. Protected Convention

Python-এ `_name` সাধারণত convention হিসেবে "internal/protected" বোঝায়।

```python
class User:

    def __init__(self):
        self._email = "example@email.com"
```

এটি language-level strict protection নয়।

---

# 23. Private Name

Double underscore:

```python
class User:

    def __init__(self):
        self.__password = "secret"
```

তারপর:

```python
user.__password
```

সাধারণভাবে কাজ করবে না।

Python name mangling ব্যবহার করে।

---

# 24. Name Mangling

```python
class User:

    def __init__(self):
        self.__password = "secret"
```

Internally এটি conceptually এমন name-এ transform হয়:

```text
_User__password
```

তবে এটাকে real security boundary ভাববে না।

---

# 25. Getter / Setter

ধরো:

```python
class User:

    def __init__(self, age):
        self._age = age

    def get_age(self):
        return self._age

    def set_age(self, age):

        if age < 0:
            raise ValueError("Age cannot be negative")

        self._age = age
```

---

# 26. `@property`

Python-এ cleaner approach:

```python
class User:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):

        if value < 0:
            raise ValueError("Age cannot be negative")

        self._age = value
```

ব্যবহার:

```python
user.age = 25

print(user.age)
```

এখানে method-এর মতো define হলেও attribute-এর মতো ব্যবহার হচ্ছে।

---

# 27. Inheritance

Inheritance মানে একটি class অন্য class-এর behavior/data inherit করতে পারে।

```python
class Animal:

    def eat(self):
        print("Eating")


class Dog(Animal):
    pass
```

এখন:

```python
dog = Dog()

dog.eat()
```

Output:

```text
Eating
```

---

# 28. Parent এবং Child Class

```text
Animal
   ↑
   │
  Dog
```

এখানে:

```text
Animal → Parent/Base/Superclass
Dog    → Child/Derived/Subclass
```

---

# 29. Method Overriding

Child class parent-এর method redefine করতে পারে।

```python
class Animal:

    def speak(self):
        print("Animal sound")


class Dog(Animal):

    def speak(self):
        print("Woof")
```

```python
dog = Dog()
dog.speak()
```

Output:

```text
Woof
```

---

# 30. `super()`

Parent class-এর implementation call করতে:

```python
class Animal:

    def __init__(self, name):
        self.name = name


class Dog(Animal):

    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

এখন:

```python
dog = Dog("Max", "Labrador")
```

Dog-এর constructor parent-এর constructor-ও ব্যবহার করছে।

---

# 31. Inheritance Example

```python
class User:

    def __init__(self, name, email):
        self.name = name
        self.email = email

    def login(self):
        print("User logged in")


class Admin(User):

    def delete_user(self):
        print("User deleted")
```

Admin পাবে:

```text
name
email
login()
delete_user()
```

---

# 32. Multi-Level Inheritance

```text
Animal
   ↓
Mammal
   ↓
Dog
```

Python:

```python
class Animal:
    pass


class Mammal(Animal):
    pass


class Dog(Mammal):
    pass
```

---

# 33. Multiple Inheritance

একটি class একাধিক parent inherit করতে পারে।

```python
class A:
    def feature_a(self):
        print("A")


class B:
    def feature_b(self):
        print("B")


class C(A, B):
    pass
```

এখন:

```python
obj = C()

obj.feature_a()
obj.feature_b()
```

---

# 34. Multiple Inheritance সতর্কতা

এটি powerful হলেও architecture জটিল করতে পারে।

বিশেষ করে যদি:

```text
A
↙ ↘
B  C
↘ ↙
 D
```

এরকম diamond structure হয়।

এখানে **MRO** গুরুত্বপূর্ণ।

---

# 35. MRO — Method Resolution Order

Python কোন class-এ method খুঁজবে তার order:

```python
print(C.mro())
```

অথবা:

```python
print(C.__mro__)
```

Concept:

```text
C
↓
A
↓
B
↓
object
```

Actual order inheritance graph অনুযায়ী Python-এর MRO algorithm দ্বারা নির্ধারিত হয়।

---

# 36. `object`

Python-এর class hierarchy-তে শেষ পর্যন্ত built-in:

```python
object
```

থাকে।

```python
class User:
    pass
```

Conceptually:

```text
User
 ↓
object
```

---

# 37. Polymorphism

Polymorphism:

> একই interface, different behavior।

Example:

```python
class Dog:

    def speak(self):
        return "Woof"


class Cat:

    def speak(self):
        return "Meow"
```

একই method:

```text
speak()
```

কিন্তু behavior আলাদা।

---

# 38. Polymorphism Example

```python
def make_sound(animal):
    print(animal.speak())
```

তারপর:

```python
make_sound(Dog())
make_sound(Cat())
```

Output:

```text
Woof
Meow
```

Function-কে জানতে হচ্ছে না object আসলে Dog না Cat।

---

# 39. Duck Typing

Python-এর famous concept:

> "If it behaves like what I need, I can use it."

```python
class Dog:

    def speak(self):
        return "Woof"


class Robot:

    def speak(self):
        return "Beep"
```

```python
def communicate(obj):
    print(obj.speak())
```

দুটোই কাজ করবে।

```python
communicate(Dog())
communicate(Robot())
```

Python সাধারণত strict inheritance relationship-এর বদলে behavior-এর ওপর অনেক ক্ষেত্রে নির্ভর করতে পারে।

---

# 40. Abstraction

Abstraction মানে unnecessary implementation details hide করে essential interface define করা।

ধরো:

```text
AI Model
   ↓
generate()
```

User শুধু জানবে:

```python
model.generate(text)
```

ভিতরে:

```text
Tokenization
↓
Embedding
↓
Transformer
↓
Inference
↓
Decoding
```

কিন্তু সব detail caller-এর জানা প্রয়োজন নেই।

---

# 41. Abstract Base Class

Python-এ:

```python
from abc import ABC, abstractmethod
```

তারপর:

```python
class Model(ABC):

    @abstractmethod
    def generate(self, text):
        pass
```

এটি একটি abstract interface-এর মতো কাজ করে।

---

# 42. Abstract Class Example

```python
from abc import ABC, abstractmethod


class Model(ABC):

    @abstractmethod
    def generate(self, text):
        pass


class AIModel(Model):

    def generate(self, text):
        return f"Generated: {text}"
```

এখন:

```python
model = AIModel()

print(model.generate("Hello"))
```

---

# 43. Abstract Class Directly Instantiate?

```python
model = Model()
```

করলে error হবে, কারণ abstract method implement করা হয়নি।

Concept:

```text
Model
 ↓
Interface
 ↓
AIModel
 ↓
Implementation
```

---

# 44. Composition

Composition হলো একটি object-এর ভিতরে অন্য object রাখা।

উদাহরণ:

```python
class Engine:

    def start(self):
        print("Engine started")


class Car:

    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
```

এখানে:

```text
Car
 └── Engine
```

---

# 45. Composition vs Inheritance

Inheritance:

```text
Dog IS-A Animal
```

Composition:

```text
Car HAS-A Engine
```

এটা খুব গুরুত্বপূর্ণ।

```text
IS-A → Inheritance
HAS-A → Composition
```

---

# 46. কেন Composition গুরুত্বপূর্ণ?

ধরো AI application:

```text
AIWriter
 ├── TextProcessor
 ├── Model
 ├── Validator
 └── Formatter
```

এখানে inheritance দিয়ে সবকিছু করার দরকার নেই।

Composition:

```python
class AIWriter:

    def __init__(self, model, processor):
        self.model = model
        self.processor = processor
```

এটি flexible architecture দেয়।

---

# 47. Composition Example — AI

```python
class TextProcessor:

    def clean(self, text):
        return text.strip()


class Model:

    def generate(self, text):
        return text.upper()


class AIWriter:

    def __init__(self, processor, model):
        self.processor = processor
        self.model = model

    def rewrite(self, text):
        clean = self.processor.clean(text)
        return self.model.generate(clean)
```

ব্যবহার:

```python
processor = TextProcessor()
model = Model()

writer = AIWriter(processor, model)

print(writer.rewrite(" hello ai "))
```

Output:

```text
HELLO AI
```

---

# 48. Dependency Injection

উপরের example-এ:

```python
writer = AIWriter(processor, model)
```

`AIWriter` নিজে `Model()` তৈরি করছে না।

বাইরে থেকে dependency দেওয়া হচ্ছে।

এটি:

> **Dependency Injection**

এর একটি simple example।

এটা future backend/AI architecture-এ খুব গুরুত্বপূর্ণ হবে।

---

# 49. Association

দুটি object relationship-এ থাকতে পারে কিন্তু একে অপরের owner নয়।

Example:

```python
class Teacher:
    pass


class Student:
    pass
```

Teacher এবং Student একে অপরের সাথে associated হতে পারে।

---

# 50. Aggregation

একটি object অন্য object-কে contain করে, কিন্তু contained object independently exist করতে পারে।

Concept:

```text
Department
 ├── Teacher
 ├── Teacher
 └── Teacher
```

Teacher department ছাড়াও conceptualভাবে exist করতে পারে।

---

# 51. Composition vs Aggregation

সহজভাবে:

```text
Composition:
Strong ownership

Aggregation:
Weak ownership
```

উদাহরণ:

```text
House → Room
```

Composition-এর মতো ভাবা যায়।

```text
University → Student
```

Aggregation-এর মতো ভাবা যায়।

---

# 52. Dunder / Magic Methods

Python-এর special methods:

```text
__init__
__str__
__repr__
__len__
__eq__
__add__
__lt__
...
```

এগুলোকে dunder methods বলা হয়।

Dunder = double underscore।

---

# 53. `__str__`

Object print করলে human-readable representation দিতে:

```python
class User:

    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name
```

```python
user = User("Atiar")

print(user)
```

Output:

```text
Atiar
```

---

# 54. `__repr__`

Developer/debugging representation:

```python
class User:

    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"User(name={self.name!r})"
```

```python
user = User("Atiar")

print(repr(user))
```

Output:

```text
User(name='Atiar')
```

---

# 55. `__len__`

```python
class Team:

    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)
```

তারপর:

```python
team = Team(["A", "B", "C"])

print(len(team))
```

Output:

```text
3
```

---

# 56. `__eq__`

Object equality define করতে:

```python
class User:

    def __init__(self, email):
        self.email = email

    def __eq__(self, other):
        return self.email == other.email
```

তারপর:

```python
u1 = User("a@example.com")
u2 = User("a@example.com")

print(u1 == u2)
```

Output:

```text
True
```

---

# 57. `__add__`

Operator overloading:

```python
class Score:

    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Score(self.value + other.value)
```

তারপর:

```python
a = Score(10)
b = Score(20)

c = a + b

print(c.value)
```

Output:

```text
30
```

Python-এর:

```python
a + b
```

internally special method mechanism ব্যবহার করতে পারে।

---

# 58. Dataclass

যখন class মূলত data hold করে, তখন `dataclass` খুব useful।

```python
from dataclasses import dataclass


@dataclass
class User:
    name: str
    age: int
```

এখন:

```python
user = User("Atiar", 25)

print(user)
```

Automatically useful methods পাওয়া যায়, যেমন readable representation এবং equality behavior।

---

# 59. Dataclass Example

```python
from dataclasses import dataclass


@dataclass
class TextResult:

    text: str
    score: float
    label: str
```

ব্যবহার:

```python
result = TextResult(
    text="AI is powerful",
    score=0.91,
    label="AI"
)

print(result.text)
print(result.score)
```

AI/NLP result modeling-এর জন্য এটি খুব useful।

---

# 60. OOP + AI Model Architecture

তোমার future AI application-এ এমন design হতে পারে:

```text
AIWriter
    │
    ├── TextProcessor
    │
    ├── Model
    │
    ├── Detector
    │
    └── Formatter
```

Python:

```python
class AIWriter:

    def __init__(
        self,
        processor,
        model,
        detector,
        formatter
    ):
        self.processor = processor
        self.model = model
        self.detector = detector
        self.formatter = formatter
```

এটা composition-based architecture।

---

# 61. AI Model Interface

Abstract class:

```python
from abc import ABC, abstractmethod


class TextModel(ABC):

    @abstractmethod
    def generate(self, text):
        pass
```

একটি implementation:

```python
class LocalModel(TextModel):

    def generate(self, text):
        return f"Local result: {text}"
```

অন্য implementation:

```python
class APIModel(TextModel):

    def generate(self, text):
        return f"API result: {text}"
```

এখন `AIWriter` model implementation-এর details না জেনেও interface-এর মাধ্যমে কাজ করতে পারে।

---

# 62. Polymorphism + AI

```python
def process(model, text):
    return model.generate(text)
```

তারপর:

```python
local = LocalModel()
api = APIModel()

print(process(local, "Hello"))
print(process(api, "Hello"))
```

একই:

```python
generate()
```

কিন্তু implementation আলাদা।

এটাই practical polymorphism।

---

# 63. OOP Project Structure

আজকের concepts ব্যবহার করে:

```text
ai_writer/
│
├── app/
│   │
│   ├── models/
│   │   ├── base.py
│   │   ├── local.py
│   │   └── api.py
│   │
│   ├── services/
│   │   ├── writer.py
│   │   ├── detector.py
│   │   └── analyzer.py
│   │
│   ├── preprocessing/
│   │   ├── cleaner.py
│   │   └── tokenizer.py
│   │
│   └── schemas/
│       └── result.py
│
└── main.py
```

---

# 64. OOP Design Example

### `base.py`

```python
from abc import ABC, abstractmethod


class TextModel(ABC):

    @abstractmethod
    def generate(self, text):
        pass
```

### `local.py`

```python
from .base import TextModel


class LocalModel(TextModel):

    def generate(self, text):
        return text.upper()
```

### `writer.py`

```python
class AIWriter:

    def __init__(self, model):
        self.model = model

    def rewrite(self, text):
        return self.model.generate(text)
```

### `main.py`

```python
from app.models.local import LocalModel
from app.services.writer import AIWriter


model = LocalModel()

writer = AIWriter(model)

result = writer.rewrite("hello world")

print(result)
```

Output:

```text
HELLO WORLD
```

---

# 65. Why This Architecture Is Powerful

পরে তুমি model পরিবর্তন করতে পারবে:

```text
LocalModel
     ↓
AIWriter
```

থেকে:

```text
APIModel
     ↓
AIWriter
```

`AIWriter`-এর core logic পরিবর্তন করতে হবে না।

এটাই good software design-এর একটি গুরুত্বপূর্ণ idea।

---

# 66. OOP Common Mistake #1

সবকিছুর জন্য class বানানো।

খারাপ:

```python
class Add:
    ...
```

যখন simple function যথেষ্ট:

```python
def add(a, b):
    return a + b
```

OOP ব্যবহার করবে যখন object/state/behavior/design relationship থেকে বাস্তব benefit পাওয়া যায়।

---

# 67. Common Mistake #2

অতিরিক্ত inheritance।

যেমন:

```text
A
 ↓
B
 ↓
C
 ↓
D
 ↓
E
 ↓
F
```

খুব deep hierarchy maintenance কঠিন করতে পারে।

অনেক ক্ষেত্রে composition better।

---

# 68. Common Mistake #3

God Class

একটি class-এর ভিতরে সবকিছু:

```text
AIWriter
 ├── Database
 ├── Authentication
 ├── Payment
 ├── Email
 ├── Model
 ├── File
 ├── Logging
 ├── API
 └── Everything
```

এটা avoid করা উচিত।

---

# 69. Common Mistake #4

এক class-এর অতিরিক্ত responsibility।

Better:

```text
TextProcessor
ModelService
DetectionService
FileService
UserService
```

প্রতিটির clear responsibility থাকা ভালো।

---

# 70. Single Responsibility Principle

একটি class-এর ideally একটি primary responsibility থাকা উচিত।

```text
TextCleaner
    ↓
Text cleaning

ModelService
    ↓
Model inference

FileService
    ↓
File operations
```

এটি SOLID principles-এর প্রথম principle:

> **S — Single Responsibility Principle**

SOLID-এর বাকি principles আমরা পরবর্তী advanced lesson-এ আরও গভীরভাবে দেখব।

---

# 71. OOP + Previous Lessons

এখন দেখো M01-এর concepts কীভাবে connect হচ্ছে:

```text
Variables
   ↓
Data Types
   ↓
Functions
   ↓
Modules
   ↓
Files
   ↓
Classes
   ↓
Objects
   ↓
Reusable Components
```

আর:

```text
Function
   ↓
Method
   ↓
Class
   ↓
Object
   ↓
System
```

---

# 72. Mini Project — AI Text Analyzer

এখন একটি ছোট OOP project বানাও।

Structure:

```text
ai_analyzer/
│
├── main.py
│
├── models.py
├── processor.py
└── analyzer.py
```

---

## `models.py`

```python
class TextDocument:

    def __init__(self, text):
        self.text = text

    def word_count(self):
        return len(self.text.split())
```

---

## `processor.py`

```python
class TextProcessor:

    def clean(self, text):
        return " ".join(text.strip().split())

    def lowercase(self, text):
        return text.lower()
```

---

## `analyzer.py`

```python
class TextAnalyzer:

    def analyze(self, text):
        return {
            "word_count": len(text.split()),
            "character_count": len(text)
        }
```

---

## `main.py`

```python
from models import TextDocument
from processor import TextProcessor
from analyzer import TextAnalyzer


text = "   Artificial intelligence is powerful.   "

processor = TextProcessor()

text = processor.clean(text)
text = processor.lowercase(text)

document = TextDocument(text)

analyzer = TextAnalyzer()

result = analyzer.analyze(document.text)

print(result)
```

Output:

```text
{
    'word_count': 5,
    'character_count': 40
}
```

---

# 🔥 Level 2 Challenge

এখন inheritance ব্যবহার করো:

```text
TextAnalyzer
      ↑
 ┌────┴────┐
AIAnalyzer HumanAnalyzer
```

Base class:

```python
class TextAnalyzer:

    def analyze(self, text):
        raise NotImplementedError
```

Child classes:

```python
class AIAnalyzer(TextAnalyzer):

    def analyze(self, text):
        ...
```

```python
class HumanAnalyzer(TextAnalyzer):

    def analyze(self, text):
        ...
```

তারপর polymorphism ব্যবহার করো।

---

# 🔥 Level 3 Challenge — Model Interface

এবার:

```text
TextModel
   ↑
   ├── LocalModel
   └── MockAPIModel

AIWriter
   ↓
Model
```

Requirements:

```text
[ ] Abstract class
[ ] abstractmethod
[ ] inheritance
[ ] method overriding
[ ] polymorphism
[ ] composition
[ ] dependency injection
```

---

# 🧪 Theory Questions

নিজে answer করার চেষ্টা করো:

1. OOP কী?
2. Class কী?
3. Object কী?
4. Class এবং Object-এর পার্থক্য কী?
5. Attribute কী?
6. Method কী?
7. `self` কী?
8. `__init__()` কী?
9. Instance attribute কী?
10. Class attribute কী?
11. Instance method কী?
12. Class method কী?
13. Static method কী?
14. `self` এবং `cls`-এর difference কী?
15. Encapsulation কী?
16. Public/protected/private convention কী?
17. Name mangling কী?
18. `@property` কী?
19. Inheritance কী?
20. Method overriding কী?
21. `super()` কী?
22. Multiple inheritance কী?
23. MRO কী?
24. Polymorphism কী?
25. Duck typing কী?
26. Abstraction কী?
27. Abstract class কী?
28. `ABC` কী?
29. `@abstractmethod` কী?
30. Composition কী?
31. Aggregation কী?
32. Association কী?
33. IS-A এবং HAS-A relationship কী?
34. Dunder method কী?
35. `__str__()` এবং `__repr__()`-এর difference কী?
36. `__eq__()` কী?
37. Operator overloading কী?
38. Dataclass কী?
39. Dependency Injection কী?
40. কখন inheritance-এর বদলে composition ব্যবহার করবে?

---

# 🎯 M01.14 Completion Checklist

```text
[ ] OOP concept
[ ] Class
[ ] Object
[ ] Attribute
[ ] Method
[ ] __init__
[ ] self
[ ] Instance attribute
[ ] Class attribute
[ ] Instance method
[ ] Class method
[ ] Static method
[ ] Encapsulation
[ ] Public convention
[ ] Protected convention
[ ] Private/name mangling
[ ] Getter
[ ] Setter
[ ] @property
[ ] Inheritance
[ ] Parent class
[ ] Child class
[ ] Method overriding
[ ] super()
[ ] Multiple inheritance
[ ] MRO
[ ] Polymorphism
[ ] Duck typing
[ ] Abstraction
[ ] ABC
[ ] abstractmethod
[ ] Composition
[ ] Aggregation
[ ] Association
[ ] IS-A
[ ] HAS-A
[ ] Dunder methods
[ ] __str__
[ ] __repr__
[ ] __len__
[ ] __eq__
[ ] __add__
[ ] Dataclass
[ ] Dependency Injection
[ ] OOP architecture
[ ] AI/NLP OOP design
```

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণভাবে এভাবে ভাববে:

```text
                    CLASS
                      │
              ┌───────┴───────┐
              ↓               ↓
           DATA            BEHAVIOR
        Attributes         Methods
              │               │
              └───────┬───────┘
                      ↓
                   OBJECT
```

তারপর বড় architecture:

```text
                    APPLICATION
                         │
              ┌──────────┼──────────┐
              ↓          ↓          ↓
          Services     Models      Utils
              │          │
              │       Abstract
              │          ↓
              │     Implementations
              │          │
              └────┬─────┘
                   ↓
              Composition
                   ↓
              Polymorphism
                   ↓
               AI System
```

### 🔗 M01 Progress

```text
M01.01 → Python Environment
M01.02 → Variables & Object Model
M01.03 → Data Types
M01.04 → Operators
M01.05 → Control Flow
M01.06 → Loops & Iteration
M01.07 → Functions
M01.08 → Advanced Functions
M01.09 → Data Structures
M01.10 → Iterators & Generators
M01.11 → Exception Handling
M01.12 → Modules & Packages
M01.13 → Files, JSON, CSV & Serialization
👉 M01.14 → OOP
```

**M01.14-এর সবচেয়ে গুরুত্বপূর্ণ takeaway:**
`class` মুখস্থ করার চেয়ে **কখন function, কখন class, কখন inheritance এবং কখন composition ব্যবহার করবে**—এই design thinking শেখাটাই বেশি গুরুত্বপূর্ণ। এটা পরবর্তী Django, FastAPI, PyTorch এবং AI/NLP architecture-এ সরাসরি কাজে লাগবে।
