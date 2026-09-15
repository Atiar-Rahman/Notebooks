অবশ্যই। এবার আমরা **Python `json` module-এর Complete Course** করব—আগের `pathlib` course-এর মতো **Day 1 → Day 10**, এবং প্রতিদিন theory + code + practice + mini project থাকবে।

Official documentation: [Python `json` official documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)

# 🐍 Python `json` Module — Complete Course

## 🎯 Course Goal

Course শেষে তুমি পারবে:

```text
Python Object
     ↓
   JSON
     ↓
Save / Send / API
     ↓
   JSON
     ↓
Python Object
```

বিশেষ করে:

- JSON কী এবং কেন ব্যবহার হয়
    
- `json.dumps()`
    
- `json.loads()`
    
- `json.dump()`
    
- `json.load()`
    
- JSON file read/write
    
- nested JSON
    
- list/dictionary conversion
    
- API response handle করা
    
- JSON validation
    
- pretty printing
    
- sorting
    
- encoding
    
- error handling
    
- JSON + pathlib
    
- JSON + REST API
    
- configuration files
    
- real-world project
    

---

# 📚 10-Day Roadmap

|Day|Topic|
|---|---|
|**Day 1**|JSON Fundamentals + `dumps()`|
|**Day 2**|`loads()` + JSON → Python|
|**Day 3**|`dump()` + JSON File Writing|
|**Day 4**|`load()` + JSON File Reading|
|**Day 5**|Nested JSON + Complex Data|
|**Day 6**|Formatting, Sorting & Encoding|
|**Day 7**|Error Handling & Validation|
|**Day 8**|JSON + `pathlib` + Configuration|
|**Day 9**|JSON + API + Real-world Data|
|**Day 10**|🔥 Final JSON Database Project|

---

# 🔥 JSON-এর সবচেয়ে গুরুত্বপূর্ণ চারটি Function

প্রথম থেকেই এই ৪টা পরিষ্কার রাখবে:

```python
json.dumps()
json.loads()

json.dump()
json.load()
```

Mental model:

```text
              Python
                 │
       ┌─────────┴─────────┐
       ↓                   ↓
    dumps()              dump()
       │                   │
       ↓                   ↓
   JSON string          JSON file


              JSON
                 │
       ┌─────────┴─────────┐
       ↓                   ↓
    loads()              load()
       │                   │
       ↓                   ↓
    Python              Python
```

### মনে রাখার সহজ উপায়

```text
s = string

dumps → Python → JSON string
loads → JSON string → Python

dump → Python → JSON file
load → JSON file → Python
```

---

# 🧩 JSON কোথায় ব্যবহার হয়?

তুমি যেহেতু **React + Django REST API** নিয়ে কাজ করো, JSON তোমার জন্য খুব important।

উদাহরণ:

```text
React
  │
  │ JSON
  ↓
Django REST API
  │
  │ JSON
  ↓
React
```

Example response:

```json
{
    "id": 1,
    "name": "Ati",
    "email": "user@example.com"
}
```

Python:

```python
data = {
    "id": 1,
    "name": "Ati",
    "email": "user@example.com"
}
```

---

# ⚠️ JSON এবং Python Dictionary এক জিনিস নয়

দেখতে কাছাকাছি হলেও:

```python
{
    "name": "Rahim"
}
```

এটা **Python dictionary**।

আর:

```json
{
    "name": "Rahim"
}
```

এটা **JSON data**।

Conversion করতে `json` module ব্যবহার করি।

---

# 🗺️ Course Flow

আমরা এভাবে এগোব:

```text
Day 1
  ↓
JSON basics
  ↓
Day 2
  ↓
JSON → Python
  ↓
Day 3
  ↓
Python → JSON File
  ↓
Day 4
  ↓
JSON File → Python
  ↓
Day 5
  ↓
Nested JSON
  ↓
Day 6
  ↓
Formatting
  ↓
Day 7
  ↓
Validation + Errors
  ↓
Day 8
  ↓
Config System
  ↓
Day 9
  ↓
API Data
  ↓
Day 10
  ↓
🔥 JSON Database Project
```

## 🏆 Final Project

শেষে আমরা বানাব:

### `JSON Student Management System`

Features:

```text
1. Add student
2. View students
3. Search student
4. Update student
5. Delete student
6. Save to JSON
7. Load from JSON
8. Statistics
9. Backup
10. Exit
```

এখানে একসাথে ব্যবহার হবে:

```python
json
pathlib
functions
list
dict
exception handling
file handling
```

**Day 1 থেকেই শুরু করব `json.dumps()` দিয়ে এবং Python data → JSON conversion খুব ভালোভাবে বুঝব।**




# 🐍 Python JSON Module — Day 1

## JSON Fundamentals + `json.dumps()`

আজকের লক্ষ্য হলো **JSON কী, Python dictionary আর JSON-এর পার্থক্য কী, এবং `json.dumps()` কীভাবে কাজ করে**—এগুলো একদম পরিষ্কার করা।

Official documentation: [Python `json` official documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)

---

# 1️⃣ JSON কী?

**JSON = JavaScript Object Notation**

এটি একটি lightweight **data interchange format**।

সহজভাবে:

> এক program থেকে অন্য program-এ structured data পাঠানো/সংরক্ষণ করার জন্য JSON খুব বেশি ব্যবহৃত হয়।

যেমন Django API থেকে React-এ:

```text
Django
   ↓
   JSON
   ↓
React
```

---

# 2️⃣ একটি JSON Example

```json
{
    "name": "Rahim",
    "age": 25,
    "city": "Dhaka"
}
```

এখানে:

```text
"name" → key
"Rahim" → value

"age" → key
25 → value
```

---

# 3️⃣ Python Dictionary বনাম JSON

Python:

```python
student = {
    "name": "Rahim",
    "age": 25
}
```

এটা হলো **Python dictionary**।

JSON:

```json
{
    "name": "Rahim",
    "age": 25
}
```

দেখতে প্রায় একই।

কিন্তু Python program-এর ভিতরে প্রথমটি Python object, আর দ্বিতীয়টি JSON format-এর data।

---

# 4️⃣ JSON Module Import

Python-এর built-in `json` module আছে।

তাই installation দরকার নেই।

```python
import json
```

তারপর:

```python
print(json)
```

---

# 5️⃣ `json.dumps()` ⭐⭐⭐

আজকের সবচেয়ে গুরুত্বপূর্ণ function:

```python
json.dumps()
```

এর কাজ:

```text
Python object
     ↓
json.dumps()
     ↓
JSON string
```

Example:

```python
import json

student = {
    "name": "Rahim",
    "age": 25
}

result = json.dumps(student)

print(result)
```

Output:

```text
{"name": "Rahim", "age": 25}
```

---

# 6️⃣ `dumps` নামটা কেন?

এখানে:

```text
dump + s
```

`s` = **string**

তাই মনে রাখো:

```text
dumps
  ↓
Python → JSON string
```

আর পরে আমরা শিখব:

```text
dump
  ↓
Python → JSON file
```

---

# 7️⃣ `type()` দিয়ে দেখি

```python
import json

student = {
    "name": "Rahim",
    "age": 25
}

result = json.dumps(student)

print(type(student))
print(type(result))
```

Output:

```text
<class 'dict'>
<class 'str'>
```

খুব গুরুত্বপূর্ণ:

```text
Python dict
     ↓
  dumps()
     ↓
Python str
```

অর্থাৎ JSON string Python-এ সাধারণত `str` হিসেবে থাকে।

---

# 8️⃣ String-এর ভিতরে JSON

```python
result = json.dumps(student)

print(repr(result))
```

তুমি দেখতে পারো JSON একটি Python string হিসেবে stored হয়েছে।

---

# 9️⃣ Python Data Types → JSON

`json` module অনেক common Python type convert করতে পারে।

|Python|JSON|
|---|---|
|`dict`|object|
|`list`|array|
|`tuple`|array|
|`str`|string|
|`int`|number|
|`float`|number|
|`True`|`true`|
|`False`|`false`|
|`None`|`null`|

---

# 🔟 Dictionary

```python
import json

data = {
    "name": "Ati",
    "age": 22
}

print(json.dumps(data))
```

Output:

```json
{"name": "Ati", "age": 22}
```

---

# 1️⃣1️⃣ List

```python
import json

numbers = [10, 20, 30, 40]

result = json.dumps(numbers)

print(result)
```

Output:

```json
[10, 20, 30, 40]
```

---

# 1️⃣2️⃣ String

```python
import json

name = "Rahim"

print(json.dumps(name))
```

Output:

```text
"Rahim"
```

খেয়াল করো JSON string-এর ভিতরে quotation marks আছে।

---

# 1️⃣3️⃣ Boolean

Python:

```python
data = {
    "active": True
}
```

JSON:

```json
{
    "active": true
}
```

⚠️ Python:

```python
True
False
None
```

JSON:

```text
true
false
null
```

---

# 1️⃣4️⃣ `None`

```python
import json

data = {
    "name": "Rahim",
    "phone": None
}

print(json.dumps(data))
```

Output:

```json
{"name": "Rahim", "phone": null}
```

---

# 1️⃣5️⃣ Nested Dictionary ⭐⭐⭐

Real API data সাধারণত nested হয়।

```python
import json

student = {
    "name": "Rahim",
    "age": 22,
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}

result = json.dumps(student)

print(result)
```

Output:

```json
{
    "name": "Rahim",
    "age": 22,
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
```

---

# 1️⃣6️⃣ Dictionary + List

আরও realistic:

```python
import json

student = {
    "name": "Rahim",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}

print(json.dumps(student))
```

এটাই API response-এর common structure।

---

# 1️⃣7️⃣ Pretty JSON ⭐⭐⭐

Normal:

```python
print(json.dumps(student))
```

সব এক line-এ আসতে পারে।

Readable করতে:

```python
print(
    json.dumps(
        student,
        indent=4
    )
)
```

Output:

```json
{
    "name": "Rahim",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

`indent=4` JSON-কে সুন্দরভাবে format করে।

---

# 1️⃣8️⃣ `indent=2`

কম spacing:

```python
print(
    json.dumps(
        student,
        indent=2
    )
)
```

অনেক project-এ:

```python
indent=2
```

ব্যবহার করা হয়।

---

# 1️⃣9️⃣ `sort_keys=True`

JSON-এর keys alphabetically sort করতে:

```python
import json

data = {
    "z": 10,
    "a": 20,
    "m": 30
}

print(
    json.dumps(
        data,
        sort_keys=True
    )
)
```

Output:

```json
{"a": 20, "m": 30, "z": 10}
```

Pretty version:

```python
print(
    json.dumps(
        data,
        indent=4,
        sort_keys=True
    )
)
```

---

# 2️⃣0️⃣ Unicode / বাংলা Text ⭐⭐⭐

JSON-এ বাংলা text থাকতে পারে।

```python
import json

data = {
    "name": "আতিয়ার",
    "city": "ঢাকা"
}

print(
    json.dumps(
        data,
        ensure_ascii=False,
        indent=4
    )
)
```

Output:

```json
{
    "name": "আতিয়ার",
    "city": "ঢাকা"
}
```

### `ensure_ascii=False` কেন?

Default behavior-এ non-ASCII characters escaped form-এ দেখাতে পারে।

বাংলা/Unicode readable রাখতে:

```python
ensure_ascii=False
```

খুব useful।

---

# 2️⃣1️⃣ একটি API-এর মতো Data

ধরো Django API থেকে এমন data আসবে:

```python
user = {
    "id": 101,
    "username": "atiar",
    "email": "user@example.com",
    "is_active": True,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

JSON বানাতে:

```python
import json

json_data = json.dumps(
    user,
    indent=4,
    ensure_ascii=False
)

print(json_data)
```

এটাই JSON-এর practical use।

---

# 🔥 2️⃣2️⃣ JSON String তৈরি করে Variable-এ রাখা

```python
import json

data = {
    "name": "Rahim",
    "age": 25
}

json_string = json.dumps(data)

print(json_string)
```

এখন:

```python
json_string
```

একটি string।

```python
print(type(json_string))
```

Output:

```text
<class 'str'>
```

---

# 2️⃣3️⃣ JSON String-এর সাথে সাধারণ String-এর পার্থক্য

```python
text = '{"name": "Rahim"}'
```

এটি একটি Python string।

কিন্তু এর ভিতরের content JSON format follow করছে।

```python
print(type(text))
```

Output:

```text
<class 'str'>
```

JSON format হওয়া আর Python-এর `dict` হওয়া এক জিনিস নয়।

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Concept

এটা মুখস্থ করো:

```text
Python Dictionary
        │
        │ json.dumps()
        ↓
   JSON String
```

Example:

```python
data = {
    "name": "Rahim",
    "age": 25
}

json_data = json.dumps(data)
```

Before:

```python
type(data)
```

→ `dict`

After:

```python
type(json_data)
```

→ `str`

---

# 🧪 Day 1 Practice

## Exercise 1

এই dictionary তৈরি করো:

```python
student = {
    "name": "Your Name",
    "age": 22,
    "department": "CSE"
}
```

তারপর:

```python
json.dumps()
```

ব্যবহার করে JSON string বানাও।

---

## Exercise 2

এই data JSON-এ convert করো:

```python
skills = [
    "Python",
    "Django",
    "React",
    "SQL"
]
```

---

## Exercise 3 ⭐

এই nested data convert করো:

```python
student = {
    "name": "Rahim",
    "age": 22,
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    },
    "skills": [
        "Python",
        "Django"
    ]
}
```

এবং:

```python
indent=4
```

দিয়ে সুন্দরভাবে print করো।

---

## Exercise 4 ⭐⭐

এই data:

```python
data = {
    "name": "আতিয়ার",
    "city": "ঢাকা",
    "country": "বাংলাদেশ"
}
```

এমনভাবে JSON বানাও যেন বাংলা text readable থাকে।

Hint:

```python
ensure_ascii=False
```

---

# 🏆 Day 1 Mini Challenge

একটি **User Profile JSON Generator** বানাও।

Input:

```text
Name:
Age:
City:
Email:
Skills:
```

তারপর Python dictionary বানিয়ে:

```python
json.dumps(
    data,
    indent=4,
    ensure_ascii=False
)
```

দিয়ে JSON output দেখাবে।

Expected:

```json
{
    "name": "Ati",
    "age": 22,
    "city": "Dhaka",
    "email": "user@example.com",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

---

# 📌 Day 1 Cheat Sheet

```python
import json
```

### Python → JSON string

```python
json.dumps(data)
```

### Pretty JSON

```python
json.dumps(data, indent=4)
```

### Sort keys

```python
json.dumps(data, sort_keys=True)
```

### Unicode

```python
json.dumps(
    data,
    ensure_ascii=False
)
```

### সব একসাথে

```python
json.dumps(
    data,
    indent=4,
    sort_keys=True,
    ensure_ascii=False
)
```

---

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ⏭️
Day 3  → dump() + JSON File Writing
Day 4  → load() + JSON File Reading
Day 5  → Nested JSON + Complex Data
Day 6  → Formatting + Sorting + Encoding
Day 7  → Error Handling + Validation
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 1-এর মূল কথা:** `dumps()` = **Python object → JSON string**। এটা ভালোভাবে বুঝে ফেললে Day 2-এর `loads()` অনেক সহজ হবে।

# 🐍 Python `json` Module — Day 2

## `json.loads()` — JSON → Python

গতকাল আমরা শিখেছি:

```text
Python object
     ↓
json.dumps()
     ↓
JSON string
```

আজ শিখব এর উল্টোটা:

```text
JSON string
     ↓
json.loads()
     ↓
Python object
```

Official documentation: [Python `json` documentation — `loads()`](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com#json.loads)

---

# 1️⃣ `json.loads()` কী?

`loads()` এর কাজ হলো **JSON string-কে Python object-এ convert করা**।

```python
import json

json_data = '{"name": "Rahim", "age": 25}'

data = json.loads(json_data)

print(data)
print(type(data))
```

Output:

```text
{'name': 'Rahim', 'age': 25}
<class 'dict'>
```

অর্থাৎ:

```text
JSON string
     ↓
   loads()
     ↓
Python dict
```

---

# 2️⃣ `loads` নামটা কেন?

মনে রাখো:

```text
loads
  ↑
load + s
```

এখানে `s` = **string**

তাই:

```python
json.loads()
```

মানে:

> JSON string থেকে Python object load করা।

---

# 3️⃣ `dumps()` বনাম `loads()` ⭐⭐⭐

এগুলো অবশ্যই clear থাকতে হবে।

|Function|কাজ|
|---|---|
|`dumps()`|Python → JSON string|
|`loads()`|JSON string → Python|

### Example

```python
import json

data = {
    "name": "Rahim",
    "age": 25
}

json_string = json.dumps(data)

python_data = json.loads(json_string)
```

Flow:

```text
Python dict
    │
    │ dumps()
    ↓
JSON string
    │
    │ loads()
    ↓
Python dict
```

---

# 4️⃣ JSON Object → Python Dictionary

JSON:

```python
json_data = '''
{
    "name": "Rahim",
    "age": 25,
    "city": "Dhaka"
}
'''
```

Convert:

```python
import json

data = json.loads(json_data)

print(data["name"])
print(data["age"])
print(data["city"])
```

Output:

```text
Rahim
25
Dhaka
```

---

# 5️⃣ JSON Array → Python List

JSON:

```python
json_data = '''
[
    "Python",
    "Django",
    "React"
]
'''
```

Python:

```python
import json

skills = json.loads(json_data)

print(skills)
print(type(skills))
```

Output:

```text
['Python', 'Django', 'React']
<class 'list'>
```

So:

```text
JSON array
    ↓
Python list
```

---

# 6️⃣ JSON String → Python String

```python
import json

data = '"Python"'

result = json.loads(data)

print(result)
print(type(result))
```

Output:

```text
Python
<class 'str'>
```

খেয়াল করো JSON input:

```text
"Python"
```

কিন্তু Python result:

```text
Python
```

---

# 7️⃣ JSON Number → Python Number

### Integer

```python
import json

data = "100"

result = json.loads(data)

print(result)
print(type(result))
```

Output:

```text
100
<class 'int'>
```

### Float

```python
data = "3.14"

result = json.loads(data)

print(result)
print(type(result))
```

Output:

```text
3.14
<class 'float'>
```

---

# 8️⃣ JSON Boolean → Python Boolean ⭐⭐⭐

JSON:

```text
true
```

Python:

```python
True
```

Example:

```python
import json

data = '{"active": true}'

result = json.loads(data)

print(result)
print(type(result["active"]))
```

Output:

```text
{'active': True}
<class 'bool'>
```

---

# 9️⃣ `false`

JSON:

```python
data = '{"active": false}'
```

Python:

```python
result = json.loads(data)

print(result)
```

Output:

```python
{'active': False}
```

---

# 🔟 JSON `null` → Python `None`

JSON:

```python
data = '{"phone": null}'
```

Convert:

```python
import json

result = json.loads(data)

print(result)
print(result["phone"])
```

Output:

```text
{'phone': None}
None
```

Mapping:

```text
JSON       Python
──────────────────
true   →   True
false  →   False
null   →   None
```

---

# 1️⃣1️⃣ Nested JSON ⭐⭐⭐

Real API data অনেক সময় nested হয়।

```python
import json

json_data = '''
{
    "name": "Rahim",
    "age": 25,
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
'''

data = json.loads(json_data)

print(data["name"])
print(data["address"]["city"])
print(data["address"]["country"])
```

Output:

```text
Rahim
Dhaka
Bangladesh
```

Mental model:

```text
data
 │
 ├── name
 ├── age
 │
 └── address
       ├── city
       └── country
```

---

# 1️⃣2️⃣ JSON List + Dictionary

আরও realistic API:

```python
import json

json_data = '''
{
    "name": "Rahim",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
'''

data = json.loads(json_data)

print(data["name"])

for skill in data["skills"]:
    print(skill)
```

Output:

```text
Rahim
Python
Django
React
```

---

# 1️⃣3️⃣ List-এর ভিতরে Dictionary

এটা API-তে খুব common।

```python
import json

json_data = '''
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
'''

users = json.loads(json_data)

for user in users:
    print(
        user["id"],
        user["name"]
    )
```

Output:

```text
1 Rahim
2 Karim
3 Hasan
```

এ ধরনের structure Django REST API response-এ প্রায়ই দেখা যায়।

---

# 1️⃣4️⃣ `loads()` + API Response

ধরো কোনো API থেকে JSON string এসেছে:

```python
response_data = '''
{
    "id": 101,
    "username": "atiar",
    "email": "user@example.com"
}
'''
```

Python:

```python
import json

user = json.loads(response_data)

print(user["username"])
```

Output:

```text
atiar
```

বাস্তবে `requests` library ব্যবহার করলে response handling আরও সহজ হয়, কিন্তু JSON parsing-এর মূল concept হলো `loads()`।

---

# 1️⃣5️⃣ Invalid JSON ⭐⭐⭐

সব string JSON নয়।

এটা valid JSON:

```python
'{"name": "Rahim"}'
```

কিন্তু:

```python
"{'name': 'Rahim'}"
```

এটি Python dictionary-এর representation, **valid JSON নয়**।

কারণ JSON object-এ keys-এর জন্য double quotes ব্যবহার করতে হয়।

---

# 1️⃣6️⃣ `JSONDecodeError`

Invalid JSON দিলে error হবে:

```python
import json

data = "{'name': 'Rahim'}"

result = json.loads(data)
```

Error:

```text
json.decoder.JSONDecodeError
```

তাই user/API input parse করার সময় error handling গুরুত্বপূর্ণ।

---

# 1️⃣7️⃣ Error Handling

```python
import json

data = "{'name': 'Rahim'}"

try:

    result = json.loads(data)

    print(result)

except json.JSONDecodeError:

    print("Invalid JSON!")
```

Output:

```text
Invalid JSON!
```

---

# 1️⃣8️⃣ Real-world JSON Parser

একটি reusable function:

```python
import json


def parse_json(json_string):

    try:

        return json.loads(json_string)

    except json.JSONDecodeError:

        print("Invalid JSON!")
        return None
```

Use:

```python
data = '{"name": "Rahim"}'

result = parse_json(data)

print(result)
```

---

# 1️⃣9️⃣ `loads()` এর Input অবশ্যই String হতে হবে

এটা:

```python
import json

data = {
    "name": "Rahim"
}

json.loads(data)
```

সঠিক ব্যবহার নয়, কারণ `data` ইতোমধ্যেই Python dictionary।

এক্ষেত্রে:

```python
json.dumps(data)
```

দরকার।

মনে রাখো:

```text
dict → dumps()

JSON string → loads()
```

---

# 🔥 2️⃣0️⃣ Round Trip

এটা খুব গুরুত্বপূর্ণ concept।

```python
import json

original = {
    "name": "Rahim",
    "age": 25,
    "skills": [
        "Python",
        "Django"
    ]
}

json_data = json.dumps(original)

restored = json.loads(json_data)

print(restored)
```

Flow:

```text
Original Python object
        ↓
     dumps()
        ↓
    JSON string
        ↓
     loads()
        ↓
Restored Python object
```

Check:

```python
print(original == restored)
```

Output:

```text
True
```

---

# 2️⃣1️⃣ Important Type Mapping

এটা আজ ভালোভাবে মুখস্থ করো:

|JSON|Python|
|---|---|
|object|`dict`|
|array|`list`|
|string|`str`|
|number (integer)|`int`|
|number (decimal)|`float`|
|`true`|`True`|
|`false`|`False`|
|`null`|`None`|

---

# 🧠 `dumps()` + `loads()` Mental Model

```text
                Python
                  │
             ┌────┴────┐
             │         │
          dumps()   loads()
             │         ↑
             ↓         │
          JSON String
```

আরও সহজ:

```text
dumps = বাইরে পাঠানোর জন্য JSON বানাও
loads = JSON থেকে Python data বানাও
```

---

# 🧪 Day 2 Practice

## Exercise 1

এই JSON string parse করো:

```python
json_data = '''
{
    "name": "Karim",
    "age": 30,
    "city": "Rajshahi"
}
'''
```

তারপর print করো:

```text
name
age
city
```

---

## Exercise 2

এই JSON array parse করো:

```python
json_data = '''
[
    "Python",
    "JavaScript",
    "Django",
    "React"
]
'''
```

তারপর loop করে প্রতিটি item print করো।

---

## Exercise 3 ⭐

এই JSON parse করো:

```python
json_data = '''
{
    "name": "Rahim",
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    },
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
'''
```

Output:

```text
Name: Rahim
City: Dhaka
Country: Bangladesh

Skills:
Python
Django
React
```

---

# 🏆 Day 2 Mini Project

## JSON User Parser

একটি JSON string:

```python
json_data = '''
{
    "id": 101,
    "name": "Ati",
    "email": "user@example.com",
    "active": true,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
'''
```

`json.loads()` দিয়ে parse করে সুন্দরভাবে output দাও:

```text
========================
       USER INFO
========================

ID      : 101
Name    : Ati
Email   : user@example.com
Active  : True

Skills:
- Python
- Django
- React
```

এরপর invalid JSON দিলে যেন program crash না করে:

```text
Invalid JSON!
```

দেখায়—`try/except` ব্যবহার করবে।

---

# 📌 Day 2 Cheat Sheet

```python
import json
```

### JSON → Python

```python
data = json.loads(json_string)
```

### Dictionary

```text
JSON object → dict
```

### Array

```text
JSON array → list
```

### Boolean

```text
true  → True
false → False
```

### Null

```text
null → None
```

### Error handling

```python
try:
    data = json.loads(text)

except json.JSONDecodeError:
    print("Invalid JSON")
```

### সবচেয়ে গুরুত্বপূর্ণ:

```text
Python dict
    ↓
dumps()
    ↓
JSON string
    ↓
loads()
    ↓
Python dict
```

---

# 📚 Course Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python            ✅
Day 3  → dump() + JSON File Writing        ⏭️
Day 4  → load() + JSON File Reading
Day 5  → Nested JSON + Complex Data
Day 6  → Formatting + Sorting + Encoding
Day 7  → Error Handling + Validation
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 3-এ আমরা `json.dump()` শিখব—অর্থাৎ Python data সরাসরি `.json` file-এ save করা।**

# 🐍 Python `json` Module — Day 3

## 💾 `json.dump()` — JSON File Writing

গত দুই দিনে আমরা শিখেছি:

```text
Day 1:
Python → JSON string
        ↓
     dumps()

Day 2:
JSON string → Python
        ↓
     loads()
```

আজ শিখব:

```text
Python object
      ↓
   json.dump()
      ↓
   .json file
```

Official documentation: [Python `json.dump()` documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com#json.dump)

---

# 1️⃣ `dump()` কী?

`json.dump()` Python data সরাসরি একটি **file-এর মধ্যে JSON format-এ লিখে দেয়**।

```python
import json

data = {
    "name": "Rahim",
    "age": 25
}

with open("student.json", "w") as file:
    json.dump(data, file)
```

এখন একই directory-তে:

```text
student.json
```

তৈরি হবে।

File-এর ভিতরে:

```json
{"name": "Rahim", "age": 25}
```

---

# 2️⃣ `dump()` বনাম `dumps()` ⭐⭐⭐

এটা খুব ভালোভাবে বুঝবে।

|Function|কাজ|
|---|---|
|`dumps()`|Python → JSON **string**|
|`dump()`|Python → JSON **file**|
|`loads()`|JSON **string** → Python|
|`load()`|JSON **file** → Python|

Mental model:

```text
                 Python
                   │
           ┌───────┴───────┐
           ↓               ↓
       dumps()           dump()
           ↓               ↓
      JSON string       JSON file
```

---

# 3️⃣ Basic `dump()` Example

```python
import json

student = {
    "name": "Rahim",
    "age": 25,
    "department": "CSE"
}

with open("student.json", "w") as file:
    json.dump(student, file)
```

---

# 4️⃣ কেন `with open()`?

```python
with open("student.json", "w") as file:
```

এখানে:

```text
student.json → file name
"w"          → write mode
file         → file object
```

`with` block শেষ হলে Python automatically file close করে।

এটা manually:

```python
file.close()
```

করার চেয়ে safer এবং cleaner।

---

# 5️⃣ Pretty JSON File ⭐⭐⭐

আগের মতো readable JSON চাইলে:

```python
import json

student = {
    "name": "Rahim",
    "age": 25,
    "department": "CSE",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}

with open("student.json", "w") as file:

    json.dump(
        student,
        file,
        indent=4
    )
```

File:

```json
{
    "name": "Rahim",
    "age": 25,
    "department": "CSE",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

---

# 6️⃣ বাংলা Text Save করা ⭐⭐⭐

বাংলা data নিয়ে কাজ করলে:

```python
import json

data = {
    "name": "আতিয়ার",
    "city": "ঢাকা",
    "country": "বাংলাদেশ"
}

with open(
    "data.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False
    )
```

এখন `data.json` খুললে বাংলা readable থাকবে।

### গুরুত্বপূর্ণ:

```python
encoding="utf-8"
```

এবং:

```python
ensure_ascii=False
```

একসাথে ব্যবহার করা ভালো।

---

# 7️⃣ `sort_keys=True`

JSON file-এর keys alphabetically সাজাতে:

```python
import json

data = {
    "name": "Rahim",
    "age": 25,
    "city": "Dhaka"
}

with open("data.json", "w") as file:

    json.dump(
        data,
        file,
        indent=4,
        sort_keys=True
    )
```

---

# 8️⃣ Complete Pretty JSON

Real project-এ এমন লিখতে পারো:

```python
import json

data = {
    "name": "আতিয়ার",
    "age": 22,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}

with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False,
        sort_keys=True
    )
```

---

# 9️⃣ List Save করা

শুধু dictionary নয়, list-ও save করা যায়।

```python
import json

skills = [
    "Python",
    "Django",
    "React",
    "SQL"
]

with open(
    "skills.json",
    "w"
) as file:

    json.dump(
        skills,
        file,
        indent=4
    )
```

File:

```json
[
    "Python",
    "Django",
    "React",
    "SQL"
]
```

---

# 🔟 List of Dictionaries ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

```python
students = [
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
```

Save:

```python
import json

with open(
    "students.json",
    "w"
) as file:

    json.dump(
        students,
        file,
        indent=4
    )
```

Result:

```json
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
```

এই structure-টাই আমাদের final **JSON Student Management System**-এ কাজে লাগবে।

---

# 1️⃣1️⃣ `pathlib` + `json` ⭐⭐⭐

তুমি যেহেতু `pathlib` course শেষ করেছ, এখন দুইটা একসাথে ব্যবহার করা শিখবে।

```python
from pathlib import Path
import json

file_path = Path("data/student.json")

file_path.parent.mkdir(
    parents=True,
    exist_ok=True
)

data = {
    "name": "Rahim",
    "age": 25
}

with file_path.open(
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4
    )
```

এখন automatically:

```text
data/
└── student.json
```

তৈরি হবে।

---

# 1️⃣2️⃣ Existing File Overwrite

ধরো:

```text
student.json
```

আগে থেকেই আছে।

তুমি:

```python
open("student.json", "w")
```

করলে existing content overwrite হবে।

Example:

আগে:

```json
{
    "name": "Rahim",
    "age": 25
}
```

তারপর:

```python
data = {
    "name": "Karim"
}
```

save করলে file হবে:

```json
{
    "name": "Karim"
}
```

আগের `age` চলে যাবে।

⚠️ তাই update operation করার সময় সাধারণত আগে `load()` → modify → `dump()` করতে হয়। এটা Day 4-এ করব।

---

# 1️⃣3️⃣ JSON File-এর শেষে Data Append?

এখানে beginners একটা common mistake করে।

ভাবতে পারো:

```python
open("data.json", "a")
```

দিয়ে নতুন dictionary append করব।

কিন্তু JSON সাধারণত এমনভাবে append করা যায় না:

```json
{"name": "Rahim"}
{"name": "Karim"}
```

এটা valid single JSON document নয়।

বরং:

```json
[
    {
        "name": "Rahim"
    },
    {
        "name": "Karim"
    }
]
```

এই structure রাখতে হলে পুরো list read → modify → rewrite করতে হয়।

এটাই Day 4-এর গুরুত্বপূর্ণ অংশ হবে।

---

# 1️⃣4️⃣ `dump()` কী Return করে?

```python
result = json.dump(
    data,
    file
)

print(result)
```

সাধারণত:

```text
None
```

দেবে।

কারণ `dump()` মূলত file-এ লিখে দেয়।

অন্যদিকে:

```python
result = json.dumps(data)
```

একটি JSON string return করে।

তাই:

```text
dumps() → returns JSON string
dump()  → writes to file
```

---

# 1️⃣5️⃣ Real-world Example — Configuration File

ধরো তোমার application-এর settings:

```python
config = {
    "app_name": "My App",
    "debug": True,
    "language": "en",
    "max_users": 100
}
```

Save:

```python
import json

with open(
    "config.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        config,
        file,
        indent=4
    )
```

`config.json`:

```json
{
    "app_name": "My App",
    "debug": true,
    "language": "en",
    "max_users": 100
}
```

এ ধরনের configuration file বাস্তব Python project-এ দেখা যায়।

---

# 1️⃣6️⃣ JSON + User Data

```python
import json

users = [
    {
        "id": 1,
        "username": "ati",
        "active": True
    },
    {
        "id": 2,
        "username": "rahim",
        "active": False
    }
]

with open(
    "users.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        users,
        file,
        indent=4
    )
```

JSON:

```json
[
    {
        "id": 1,
        "username": "ati",
        "active": true
    },
    {
        "id": 2,
        "username": "rahim",
        "active": false
    }
]
```

খেয়াল করো:

Python:

```python
True
False
```

JSON:

```text
true
false
```

`json` module automatically conversion করে।

---

# 🔥 1️⃣7️⃣ Complete Flow

এখন পর্যন্ত ৩ দিনের knowledge একসাথে:

### Step 1

Python:

```python
data = {
    "name": "Rahim",
    "age": 25
}
```

### Step 2 — JSON string

```python
json_string = json.dumps(data)
```

### Step 3 — JSON file

```python
with open("data.json", "w") as file:
    json.dump(data, file)
```

Flow:

```text
Python Dictionary
       │
       ├── dumps() ──→ JSON String
       │
       └── dump() ───→ JSON File
```

---

# 🧪 Day 3 Practice

## Exercise 1

এই data `student.json`-এ save করো:

```python
student = {
    "name": "Rahim",
    "age": 22,
    "department": "CSE",
    "cgpa": 3.50
}
```

JSON file সুন্দরভাবে format করবে।

---

## Exercise 2

একটি `students.json` বানাও:

```python
students = [
    {
        "id": 1,
        "name": "Rahim",
        "age": 22
    },
    {
        "id": 2,
        "name": "Karim",
        "age": 23
    },
    {
        "id": 3,
        "name": "Hasan",
        "age": 21
    }
]
```

---

## Exercise 3 ⭐

বাংলা data save করো:

```python
student = {
    "name": "আতিয়ার",
    "department": "কম্পিউটার সায়েন্স",
    "city": "ঢাকা"
}
```

এই দুইটি ব্যবহার করবে:

```python
encoding="utf-8"
ensure_ascii=False
```

---

## Exercise 4 ⭐⭐

`pathlib` ব্যবহার করে:

```text
data/
└── users.json
```

automatically তৈরি করো।

Hint:

```python
from pathlib import Path

path = Path("data/users.json")

path.parent.mkdir(
    parents=True,
    exist_ok=True
)
```

তারপর `json.dump()` দিয়ে data save করো।

---

# 🏆 Day 3 Mini Project

## Student JSON Saver

একটি program বানাও:

```text
=========================
   STUDENT JSON SAVER
=========================

Name:
Age:
Department:
CGPA:
```

Input নিয়ে dictionary বানাবে:

```python
student = {
    "name": name,
    "age": age,
    "department": department,
    "cgpa": cgpa
}
```

তারপর:

```text
data/
└── student.json
```

এর মধ্যে save করবে।

JSON দেখতে এমন হবে:

```json
{
    "name": "Ati",
    "age": 22,
    "department": "CSE",
    "cgpa": 3.5
}
```

---

# 📌 Day 3 Cheat Sheet

### Python → JSON string

```python
json.dumps(data)
```

### Python → JSON file

```python
with open("data.json", "w") as file:
    json.dump(data, file)
```

### Pretty JSON

```python
json.dump(
    data,
    file,
    indent=4
)
```

### বাংলা support

```python
json.dump(
    data,
    file,
    indent=4,
    ensure_ascii=False
)
```

### UTF-8

```python
open(
    "data.json",
    "w",
    encoding="utf-8"
)
```

---

# 🧠 আজকের ৪টি Function আবার মনে রাখো

```text
Python
  │
  ├── dumps() ──→ JSON string
  │
  └── dump() ───→ JSON file


JSON
  │
  ├── loads() ──→ Python object
  │
  └── load() ───→ Python object
```

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ⏭️
Day 5  → Nested JSON + Complex Data
Day 6  → Formatting + Sorting + Encoding
Day 7  → Error Handling + Validation
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 4-এ সবচেয়ে গুরুত্বপূর্ণ বিষয় হবে `json.load()`—JSON file থেকে data পড়া, তারপর সেই data modify করে আবার save করা।**


# 🐍 Python `json` Module — Day 4

## 📖 `json.load()` — JSON File Reading

গত ৩ দিনে:

```text
Day 1 → dumps()
Day 2 → loads()
Day 3 → dump()
```

আজকের মূল বিষয়:

```text
JSON File
    ↓
json.load()
    ↓
Python Object
```

Official documentation: [Python `json.load()` documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com#json.load)

---

# 1️⃣ `json.load()` কী?

`json.load()` একটি **JSON file থেকে data পড়ে Python object-এ convert করে**।

ধরো `student.json`:

```json
{
    "name": "Rahim",
    "age": 25,
    "department": "CSE"
}
```

Python:

```python
import json

with open("student.json", "r") as file:
    data = json.load(file)

print(data)
```

Output:

```text
{'name': 'Rahim', 'age': 25, 'department': 'CSE'}
```

এখন:

```python
print(type(data))
```

Output:

```text
<class 'dict'>
```

---

# 2️⃣ `load()` বনাম `loads()` ⭐⭐⭐

এখানে সবচেয়ে বেশি confusion হয়।

|Function|Input|Output|
|---|---|---|
|`loads()`|JSON **string**|Python object|
|`load()`|JSON **file**|Python object|
|`dumps()`|Python object|JSON **string**|
|`dump()`|Python object|JSON **file**|

সহজভাবে:

```text
JSON STRING
    ↓
loads()

JSON FILE
    ↓
load()
```

---

# 3️⃣ Basic Example

`student.json`:

```json
{
    "name": "Rahim",
    "age": 22,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

Python:

```python
import json

with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    student = json.load(file)

print(student)
```

---

# 4️⃣ Data Access করা

`load()` করার পর তুমি normal Python dictionary-এর মতো কাজ করতে পারবে।

```python
print(student["name"])
print(student["age"])
```

Output:

```text
Rahim
22
```

Skills:

```python
for skill in student["skills"]:
    print(skill)
```

Output:

```text
Python
Django
React
```

---

# 5️⃣ JSON File → Python Dictionary

এই flow-টা খুব ভালোভাবে বুঝো:

```text
student.json
     │
     │ json.load()
     ↓
Python dict
     │
     ├── student["name"]
     ├── student["age"]
     └── student["skills"]
```

`load()` করার পর JSON নিয়ে আর আলাদা syntax লাগে না—Python object হিসেবে কাজ করবে।

---

# 6️⃣ List JSON File

ধরো `students.json`:

```json
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
```

Read:

```python
import json

with open(
    "students.json",
    "r",
    encoding="utf-8"
) as file:

    students = json.load(file)

print(type(students))
```

Output:

```text
<class 'list'>
```

তারপর:

```python
for student in students:

    print(
        student["id"],
        student["name"]
    )
```

Output:

```text
1 Rahim
2 Karim
3 Hasan
```

---

# 7️⃣ `pathlib` + `json.load()` ⭐⭐⭐

তুমি যেহেতু `pathlib` শিখেছ, এখন দুটো একসাথে ব্যবহার করা উচিত।

```python
from pathlib import Path
import json

file_path = Path("data/student.json")

with file_path.open(
    "r",
    encoding="utf-8"
) as file:

    data = json.load(file)

print(data)
```

এটা clean modern Python style।

---

# 8️⃣ File না থাকলে কী হবে?

```python
import json

with open("unknown.json", "r") as file:
    data = json.load(file)
```

যদি file না থাকে:

```text
FileNotFoundError
```

তাই real application-এ error handling দরকার।

---

# 9️⃣ `FileNotFoundError` Handle করা

```python
import json

try:

    with open(
        "student.json",
        "r",
        encoding="utf-8"
    ) as file:

        data = json.load(file)

    print(data)

except FileNotFoundError:

    print("JSON file not found!")
```

---

# 🔟 Invalid JSON Handle করা ⭐⭐⭐

ধরো file-এর ভিতরে:

```text
{'name': 'Rahim'}
```

এটা valid JSON নয়।

তখন:

```python
json.load(file)
```

করলে:

```text
json.JSONDecodeError
```

হতে পারে।

তাই:

```python
import json

try:

    with open(
        "student.json",
        "r",
        encoding="utf-8"
    ) as file:

        data = json.load(file)

except FileNotFoundError:

    print("File not found!")

except json.JSONDecodeError:

    print("Invalid JSON!")

else:

    print("Data loaded successfully!")
    print(data)
```

এটাই real-world pattern-এর কাছাকাছি।

---

# 1️⃣1️⃣ JSON Load করে Data Modify করা ⭐⭐⭐

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ practical concept।

ধরো:

```json
{
    "name": "Rahim",
    "age": 25
}
```

Read:

```python
import json

with open("student.json", "r") as file:
    student = json.load(file)
```

এখন modify:

```python
student["age"] = 26
student["city"] = "Dhaka"
```

এখন Python object:

```python
{
    "name": "Rahim",
    "age": 26,
    "city": "Dhaka"
}
```

কিন্তু **file এখনো update হয়নি**।

আবার `dump()` করতে হবে।

```python
with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        student,
        file,
        indent=4
    )
```

Flow:

```text
JSON File
   ↓
load()
   ↓
Python dict
   ↓
Modify
   ↓
dump()
   ↓
Updated JSON File
```

⭐⭐⭐ এই pattern খুব গুরুত্বপূর্ণ।

---

# 1️⃣2️⃣ Complete Update Example

```python
import json

# Read
with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    student = json.load(file)


# Modify
student["age"] = 26
student["city"] = "Dhaka"


# Save
with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        student,
        file,
        indent=4,
        ensure_ascii=False
    )

print("Student updated!")
```

---

# 1️⃣3️⃣ List-এর মধ্যে নতুন Student Add

`students.json`:

```json
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    }
]
```

Read:

```python
import json

with open(
    "students.json",
    "r",
    encoding="utf-8"
) as file:

    students = json.load(file)
```

Add:

```python
students.append({
    "id": 3,
    "name": "Hasan"
})
```

Save:

```python
with open(
    "students.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        students,
        file,
        indent=4
    )
```

Result:

```json
[
    {
        "id": 1,
        "name": "Rahim"
    },
    {
        "id": 2,
        "name": "Karim"
    },
    {
        "id": 3,
        "name": "Hasan"
    }
]
```

---

# 1️⃣4️⃣ Student Search

এখন JSON file থেকে student load করে search করতে পারো।

```python
import json

with open(
    "students.json",
    "r",
    encoding="utf-8"
) as file:

    students = json.load(file)


search_name = input(
    "Enter student name: "
)

for student in students:

    if student["name"].lower() == search_name.lower():

        print("Student found!")
        print(student)

        break

else:

    print("Student not found!")
```

এটা আমাদের final project-এর একটি feature হবে।

---

# 1️⃣5️⃣ Student Delete

```python
import json

with open(
    "students.json",
    "r",
    encoding="utf-8"
) as file:

    students = json.load(file)


student_id = int(
    input("Enter student ID: ")
)

students = [
    student
    for student in students
    if student["id"] != student_id
]


with open(
    "students.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        students,
        file,
        indent=4
    )
```

এখানে আমরা:

```text
load
 ↓
filter
 ↓
dump
```

করেছি।

---

# 1️⃣6️⃣ JSON Database-এর Basic Idea

Database না ব্যবহার করে ছোট application-এ JSON file-কে simple data storage হিসেবে ব্যবহার করা যায়।

```text
students.json
      │
      ↓
   json.load()
      │
      ↓
 Python List
      │
 ┌────┼────┐
 ↓    ↓    ↓
Add Search Delete
 │    │    │
 └────┼────┘
      ↓
   json.dump()
      ↓
students.json
```

তবে production application-এর জন্য বড় data বা multi-user concurrent operations হলে proper database ব্যবহার করা উচিত।

---

# 1️⃣7️⃣ `load()` + `pathlib`

আরও clean version:

```python
from pathlib import Path
import json

path = Path("data/students.json")

try:

    with path.open(
        "r",
        encoding="utf-8"
    ) as file:

        students = json.load(file)

except FileNotFoundError:

    students = []

except json.JSONDecodeError:

    print("Invalid JSON file!")
    students = []
```

এখানে file না থাকলে:

```python
students = []
```

দিয়ে নতুন data শুরু করা হচ্ছে।

---

# 🔥 1️⃣8️⃣ Reusable JSON Functions

Real projects-এ একই code বারবার না লিখে function বানানো ভালো।

### Load function

```python
import json
from pathlib import Path


def load_json(path):

    path = Path(path)

    with path.open(
        "r",
        encoding="utf-8"
    ) as file:

        return json.load(file)
```

Use:

```python
students = load_json(
    "students.json"
)
```

---

### Save function

```python
def save_json(path, data):

    path = Path(path)

    path.parent.mkdir(
        parents=True,
        exist_ok=True
    )

    with path.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            data,
            file,
            indent=4,
            ensure_ascii=False
        )
```

Use:

```python
save_json(
    "data/students.json",
    students
)
```

এটা খুব useful abstraction।

---

# 🏆 Day 4 Mini Project

## Student JSON CRUD — Part 1

আজ এমন program বানাও:

```text
========================
 STUDENT MANAGER
========================

1. View students
2. Add student
3. Update student
4. Delete student
5. Exit
```

আজ শুধু এই flow practice করো:

```text
students.json
      ↓
    load()
      ↓
Python list
      ↓
Add / Update / Delete
      ↓
    dump()
      ↓
students.json
```

### Initial `students.json`

```json
[]
```

### Add করলে:

```json
[
    {
        "id": 1,
        "name": "Ati",
        "age": 22,
        "department": "CSE"
    }
]
```

তারপর দ্বিতীয় student add করলে list-এর মধ্যে আরেকটি dictionary যোগ হবে।

---

# 🧪 Day 4 Exercises

### Exercise 1

একটি JSON file থেকে dictionary load করো।

### Exercise 2

একটি JSON file থেকে list load করে সব student print করো।

### Exercise 3 ⭐

JSON file-এর একটি student's `age` update করো।

### Exercise 4 ⭐

নতুন student add করো।

### Exercise 5 ⭐⭐

ID দিয়ে student delete করো।

### Exercise 6 ⭐⭐

`load_json()` এবং `save_json()` reusable function তৈরি করো।

---

# 📌 আজকের Cheat Sheet

```python
# JSON file → Python
with open("data.json", "r") as file:
    data = json.load(file)
```

```python
# Python → JSON file
with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```

### সবচেয়ে গুরুত্বপূর্ণ pattern:

```text
READ
 ↓
load()

MODIFY
 ↓
Python object

WRITE
 ↓
dump()
```

### চারটি function একসাথে:

```text
dumps() → Python → JSON string
loads() → JSON string → Python

dump()  → Python → JSON file
load()  → JSON file → Python
```

---

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ⏭️
Day 6  → Formatting + Sorting + Encoding
Day 7  → Error Handling + Validation
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 5-এ আমরা Nested JSON, deeply nested dictionary/list, real API-style JSON এবং nested data safely access করার techniques শিখব।**


---
# 🐍 Python `json` Module — Day 5

## Nested JSON + Complex Data

আজকের লক্ষ্য হলো **nested JSON** ভালোভাবে বোঝা। Real-world API, Django REST Framework, configuration file—সব জায়গাতেই nested JSON দেখতে পাবে।

Official documentation: [Python `json` official documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)

---

# 1️⃣ Nested JSON কী?

একটি JSON object-এর ভিতরে আরেকটি object বা array থাকলে তাকে **nested JSON** বলতে পারো।

Simple:

```json
{
    "name": "Rahim",
    "age": 25
}
```

Nested:

```json
{
    "name": "Rahim",
    "age": 25,
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
```

এখানে:

```text
student
 ├── name
 ├── age
 └── address
       ├── city
       └── country
```

---

# 2️⃣ Nested Dictionary Access

Python-এ:

```python
student = {
    "name": "Rahim",
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
```

City:

```python
print(student["address"]["city"])
```

Output:

```text
Dhaka
```

Country:

```python
print(student["address"]["country"])
```

---

# 3️⃣ Nested JSON → Python

ধরো API থেকে:

```python
json_data = '''
{
    "name": "Rahim",
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
'''
```

Parse:

```python
import json

student = json.loads(json_data)

print(student["name"])
print(student["address"]["city"])
```

Output:

```text
Rahim
Dhaka
```

---

# 4️⃣ Dictionary → List → Dictionary ⭐⭐⭐

এটা খুব common structure:

```json
{
    "name": "Rahim",
    "skills": [
        {
            "name": "Python",
            "level": "Advanced"
        },
        {
            "name": "Django",
            "level": "Intermediate"
        }
    ]
}
```

Structure:

```text
student
 ├── name
 └── skills
      ├── [0]
      │    ├── name
      │    └── level
      │
      └── [1]
           ├── name
           └── level
```

Python:

```python
data = {
    "name": "Rahim",
    "skills": [
        {
            "name": "Python",
            "level": "Advanced"
        },
        {
            "name": "Django",
            "level": "Intermediate"
        }
    ]
}
```

Python:

```python
print(data["skills"][0]["name"])
```

Output:

```text
Python
```

আর:

```python
print(data["skills"][1]["level"])
```

Output:

```text
Intermediate
```

---

# 5️⃣ Loop দিয়ে Nested Data Read করা

Hard-coded index ব্যবহার না করে:

```python
for skill in data["skills"]:
    print(skill["name"])
```

Output:

```text
Python
Django
```

আর:

```python
for skill in data["skills"]:
    print(
        skill["name"],
        "→",
        skill["level"]
    )
```

Output:

```text
Python → Advanced
Django → Intermediate
```

---

# 6️⃣ List → Dictionary → List

আরেকটি common structure:

```json
[
    {
        "name": "Rahim",
        "skills": [
            "Python",
            "Django"
        ]
    },
    {
        "name": "Karim",
        "skills": [
            "JavaScript",
            "React"
        ]
    }
]
```

Python:

```python
students = [
    {
        "name": "Rahim",
        "skills": [
            "Python",
            "Django"
        ]
    },
    {
        "name": "Karim",
        "skills": [
            "JavaScript",
            "React"
        ]
    }
]
```

Access:

```python
print(students[0]["name"])
```

Output:

```text
Rahim
```

প্রথম student's প্রথম skill:

```python
print(students[0]["skills"][0])
```

Output:

```text
Python
```

---

# 7️⃣ Nested Loop ⭐⭐⭐

সব student-এর সব skill print করতে:

```python
for student in students:

    print(student["name"])

    for skill in student["skills"]:
        print(" -", skill)
```

Output:

```text
Rahim
 - Python
 - Django

Karim
 - JavaScript
 - React
```

এটা খুব গুরুত্বপূর্ণ pattern।

---

# 8️⃣ Deeply Nested JSON

কখনো JSON অনেক level deep হতে পারে:

```json
{
    "user": {
        "profile": {
            "contact": {
                "address": {
                    "city": "Dhaka"
                }
            }
        }
    }
}
```

Access:

```python
city = data["user"]["profile"]["contact"]["address"]["city"]

print(city)
```

Output:

```text
Dhaka
```

এটা কাজ করে, কিন্তু অনেক nested হলে code কঠিন হয়ে যায়।

---

# 9️⃣ `.get()` ব্যবহার করা ⭐⭐⭐

Direct access:

```python
city = data["address"]["city"]
```

যদি `"address"` না থাকে → `KeyError` হতে পারে।

`.get()` ব্যবহার করলে safer হতে পারে:

```python
address = data.get("address", {})
city = address.get("city")

print(city)
```

যদি city না থাকে:

```text
None
```

---

# 🔟 `.get()` এর Default Value

```python
city = data.get("city", "Unknown")

print(city)
```

যদি `"city"` না থাকে:

```text
Unknown
```

এটা API response handle করার সময় খুব useful।

---

# 1️⃣1️⃣ Nested `.get()`

ধরো:

```python
data = {
    "user": {
        "profile": {
            "name": "Rahim"
        }
    }
}
```

Safe access:

```python
user = data.get("user", {})
profile = user.get("profile", {})

name = profile.get("name", "Unknown")

print(name)
```

Output:

```text
Rahim
```

---

# 1️⃣2️⃣ API-Style JSON ⭐⭐⭐

Django REST API-এর মতো:

```json
{
    "success": true,
    "data": {
        "user": {
            "id": 101,
            "username": "atiar",
            "email": "user@example.com"
        },
        "permissions": [
            "read",
            "write"
        ]
    }
}
```

Parse:

```python
import json

result = json.loads(json_data)
```

Success:

```python
print(result["success"])
```

User:

```python
user = result["data"]["user"]

print(user["username"])
print(user["email"])
```

Permissions:

```python
for permission in result["data"]["permissions"]:
    print(permission)
```

---

# 1️⃣3️⃣ Real API Response বুঝার Technique

কোনো API থেকে complex JSON পেলে প্রথমে পুরো structure বুঝবে।

ধরো:

```json
{
    "data": {
        "users": [
            {
                "id": 1,
                "name": "Rahim"
            },
            {
                "id": 2,
                "name": "Karim"
            }
        ]
    }
}
```

Structure:

```text
root
 └── data
      └── users
           ├── [0]
           │    ├── id
           │    └── name
           │
           └── [1]
                ├── id
                └── name
```

তারপর:

```python
users = data["data"]["users"]

for user in users:
    print(user["name"])
```

---

# 1️⃣4️⃣ Nested JSON Save করা

`json.dump()` nested structure-ও save করতে পারে।

```python
import json

data = {
    "student": {
        "name": "Rahim",
        "address": {
            "city": "Dhaka",
            "country": "Bangladesh"
        },
        "skills": [
            "Python",
            "Django"
        ]
    }
}

with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False
    )
```

---

# 1️⃣5️⃣ Nested JSON Load করা

তারপর একই file read:

```python
import json

with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    data = json.load(file)

print(data["student"]["name"])
```

Output:

```text
Rahim
```

---

# 1️⃣6️⃣ Nested Data Modify ⭐⭐⭐

ধরো:

```python
data = {
    "student": {
        "name": "Rahim",
        "address": {
            "city": "Dhaka"
        }
    }
}
```

City পরিবর্তন:

```python
data["student"]["address"]["city"] = "Rajshahi"
```

নতুন field:

```python
data["student"]["address"]["country"] = "Bangladesh"
```

Result:

```python
{
    "student": {
        "name": "Rahim",
        "address": {
            "city": "Rajshahi",
            "country": "Bangladesh"
        }
    }
}
```

---

# 1️⃣7️⃣ Nested List-এর Data Modify

```python
data = {
    "students": [
        {
            "id": 1,
            "name": "Rahim"
        },
        {
            "id": 2,
            "name": "Karim"
        }
    ]
}
```

ID 2-এর name:

```python
for student in data["students"]:

    if student["id"] == 2:
        student["name"] = "Abir"
```

Result:

```python
{
    "students": [
        {
            "id": 1,
            "name": "Rahim"
        },
        {
            "id": 2,
            "name": "Abir"
        }
    ]
}
```

---

# 1️⃣8️⃣ Nested JSON Search

```python
search_id = 2

for student in data["students"]:

    if student["id"] == search_id:
        print("Found:", student)
        break
```

এটাই JSON-based CRUD application-এ কাজে লাগবে।

---

# 1️⃣9️⃣ Nested JSON থেকে নতুন List তৈরি

ধরো:

```python
students = [
    {"id": 1, "name": "Rahim"},
    {"id": 2, "name": "Karim"},
    {"id": 3, "name": "Hasan"}
]
```

শুধু names:

```python
names = [
    student["name"]
    for student in students
]

print(names)
```

Output:

```text
['Rahim', 'Karim', 'Hasan']
```

---

# 2️⃣0️⃣ Important Concept — JSON Structure চিনবে কীভাবে?

JSON দেখেই প্রথমে determine করো:

### `{ }`

মানে:

```text
Object → Python dict
```

### `[ ]`

মানে:

```text
Array → Python list
```

Example:

```json
{
    "users": [
        {
            "name": "Rahim"
        }
    ]
}
```

এখানে:

```text
{ } → dict
  ↓
"users" → list
  ↓
[0] → dict
  ↓
"name" → string
```

এটা বুঝতে পারলে complex JSON অনেক সহজ হয়ে যায়।

---

# 🧠 Master Pattern

এই JSON:

```json
{
    "users": [
        {
            "name": "Rahim",
            "address": {
                "city": "Dhaka"
            },
            "skills": [
                "Python",
                "Django"
            ]
        }
    ]
}
```

Python-এ:

```python
data["users"][0]["name"]
```

→ `"Rahim"`

```python
data["users"][0]["address"]["city"]
```

→ `"Dhaka"`

```python
data["users"][0]["skills"][0]
```

→ `"Python"`

এখানে তিনটি rule:

```text
{} → key
[] → index
{} → key
```

---

# 🧪 Day 5 Practice

## Exercise 1

এই JSON parse করো:

```python
json_data = '''
{
    "name": "Ati",
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
'''
```

Print:

```text
Name
City
Country
```

---

## Exercise 2

এই data থেকে সব student's name print করো:

```python
students = [
    {
        "id": 1,
        "name": "Rahim",
        "skills": ["Python", "Django"]
    },
    {
        "id": 2,
        "name": "Karim",
        "skills": ["React", "JavaScript"]
    }
]
```

---

## Exercise 3 ⭐

সব student's সব skills print করো:

```text
Rahim:
- Python
- Django

Karim:
- React
- JavaScript
```

---

## Exercise 4 ⭐⭐

ID দিয়ে student search করো।

```text
Enter ID: 2

Student Found:
Name: Karim
Skills:
- React
- JavaScript
```

---

## Exercise 5 ⭐⭐

এই nested data থেকে শুধু city বের করো:

```python
data = {
    "company": {
        "office": {
            "location": {
                "city": "Dhaka",
                "country": "Bangladesh"
            }
        }
    }
}
```

Expected:

```text
Dhaka
```

---

# 🏆 Day 5 Mini Project

## Nested JSON Student Manager

আজকের project:

```text
students.json

{
    "school": {
        "name": "ABC School",
        "location": {
            "city": "Dhaka"
        },
        "students": [
            {
                "id": 1,
                "name": "Rahim",
                "skills": [
                    "Python",
                    "Django"
                ]
            },
            {
                "id": 2,
                "name": "Karim",
                "skills": [
                    "React",
                    "JavaScript"
                ]
            }
        ]
    }
}
```

Program-এর features:

```text
1. School information
2. View all students
3. Search student by ID
4. Show student's skills
5. Add skill
6. Update student
7. Save JSON
```

এখানে একসাথে practice হবে:

```text
json.load()
json.dump()
dict
list
nested dict
nested list
loop
.get()
```

---

# 📌 Day 5 Cheat Sheet

### Nested dictionary

```python
data["user"]["profile"]["name"]
```

### List-এর ভিতরের dictionary

```python
data["users"][0]["name"]
```

### Loop

```python
for user in data["users"]:
    print(user["name"])
```

### Nested list

```python
for user in data["users"]:
    for skill in user["skills"]:
        print(skill)
```

### Safe access

```python
data.get("name", "Unknown")
```

### Nested safe access

```python
user = data.get("user", {})
profile = user.get("profile", {})
name = profile.get("name", "Unknown")
```

---

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ✅
Day 6  → Formatting + Sorting + Encoding   ⏭️
Day 7  → Error Handling + Validation
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 6-এ আমরা `indent`, `sort_keys`, `ensure_ascii`, `separators`, `allow_nan` ইত্যাদি দিয়ে JSON formatting, serialization options এবং Unicode handling গভীরভাবে শিখব।**


# 🐍 Python `json` Module — Day 6

## Formatting, Sorting & Encoding

আজ আমরা JSON-কে **সুন্দর, readable এবং controlled format-এ তৈরি করা** শিখব।

গত দিন পর্যন্ত:

```text
Day 1 → dumps()
Day 2 → loads()
Day 3 → dump()
Day 4 → load()
Day 5 → Nested JSON
```

আজ:

```text
indent
sort_keys
ensure_ascii
separators
allow_nan
```

Official documentation: [Python `json` official documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)

---

# 1️⃣ `indent` — JSON সুন্দরভাবে Format করা ⭐⭐⭐

Normal:

```python
import json

data = {
    "name": "Rahim",
    "age": 25,
    "skills": ["Python", "Django", "React"]
}

print(json.dumps(data))
```

Output:

```json
{"name": "Rahim", "age": 25, "skills": ["Python", "Django", "React"]}
```

Readable করতে:

```python
print(json.dumps(data, indent=4))
```

Output:

```json
{
    "name": "Rahim",
    "age": 25,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}
```

### `indent=2`

```python
json.dumps(data, indent=2)
```

কম spacing হবে।

### `indent=4`

```python
json.dumps(data, indent=4)
```

আরও বেশি indentation হবে।

---

# 2️⃣ `indent` শুধু `dumps()`-এ নয়

`dump()`-এর সাথেও:

```python
with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```

অর্থাৎ:

```text
dumps(data, indent=4)
```

এবং:

```text
dump(data, file, indent=4)
```

দুটোতেই কাজ করে।

---

# 3️⃣ `sort_keys=True` ⭐⭐⭐

Dictionary-এর key alphabetically sort করতে:

```python
data = {
    "name": "Rahim",
    "age": 25,
    "city": "Dhaka"
}

print(
    json.dumps(
        data,
        sort_keys=True
    )
)
```

Output:

```json
{"age": 25, "city": "Dhaka", "name": "Rahim"}
```

---

# 4️⃣ `sort_keys` + `indent`

দুটো একসাথে:

```python
print(
    json.dumps(
        data,
        indent=4,
        sort_keys=True
    )
)
```

Output:

```json
{
    "age": 25,
    "city": "Dhaka",
    "name": "Rahim"
}
```

### কখন useful?

Configuration files, debugging এবং predictable JSON output-এর ক্ষেত্রে।

---

# 5️⃣ `ensure_ascii` ⭐⭐⭐

এটা বিশেষভাবে বাংলা/Unicode text-এর জন্য গুরুত্বপূর্ণ।

```python
data = {
    "name": "আতিয়ার",
    "city": "ঢাকা"
}

print(json.dumps(data))
```

Default behavior-এ non-ASCII characters escaped form-এ দেখা যেতে পারে।

Readable রাখতে:

```python
print(
    json.dumps(
        data,
        ensure_ascii=False
    )
)
```

Output:

```json
{"name": "আতিয়ার", "city": "ঢাকা"}
```

---

# 6️⃣ `ensure_ascii=False` + `indent`

সবচেয়ে useful combination:

```python
print(
    json.dumps(
        data,
        indent=4,
        ensure_ascii=False
    )
)
```

Output:

```json
{
    "name": "আতিয়ার",
    "city": "ঢাকা"
}
```

বাংলা, Arabic, Japanese ইত্যাদি Unicode text-এর ক্ষেত্রে এটি useful।

---

# 7️⃣ `encoding="utf-8"` এবং `ensure_ascii=False` এক জিনিস নয়

এখানে beginners অনেক সময় confuse হয়।

### `encoding`

File কীভাবে text encode/decode করবে:

```python
with open(
    "data.json",
    "w",
    encoding="utf-8"
) as file:
    ...
```

### `ensure_ascii`

JSON output-এ non-ASCII characters কীভাবে represent হবে:

```python
json.dump(
    data,
    file,
    ensure_ascii=False
)
```

দুটো আলাদা বিষয়।

বাংলা JSON file-এর জন্য সাধারণত:

```python
with open(
    "data.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False
    )
```

---

# 8️⃣ `separators` ⭐⭐

Default JSON:

```python
data = {
    "name": "Rahim",
    "age": 25
}

print(json.dumps(data))
```

Output:

```json
{"name": "Rahim", "age": 25}
```

Custom separators:

```python
print(
    json.dumps(
        data,
        separators=(",", ":")
    )
)
```

Output:

```json
{"name":"Rahim","age":25}
```

এখানে unnecessary spaces বাদ দেওয়া হয়েছে।

---

# 9️⃣ `separators` কেন ব্যবহার করব?

Compact JSON দরকার হলে:

```python
separators=(",", ":")
```

ব্যবহার করতে পারো।

যেমন:

```python
json.dumps(
    data,
    separators=(",", ":")
)
```

এতে JSON একটু ছোট হবে।

তবে readable JSON-এর জন্য সাধারণত:

```python
indent=4
```

বেশি useful।

---

# 🔟 Pretty বনাম Compact JSON

### Pretty

```python
json.dumps(
    data,
    indent=4
)
```

```json
{
    "name": "Rahim",
    "age": 25
}
```

### Compact

```python
json.dumps(
    data,
    separators=(",", ":")
)
```

```json
{"name":"Rahim","age":25}
```

---

# 1️⃣1️⃣ `allow_nan`

Python floating-point special values:

```python
float("nan")
float("inf")
float("-inf")
```

Example:

```python
data = {
    "value": float("nan")
}

print(json.dumps(data))
```

Python-এর JSON encoder defaultভাবে এগুলোকে:

```text
NaN
Infinity
-Infinity
```

এর মতো output করতে পারে।

কিন্তু strict JSON-এর দৃষ্টিতে এগুলো standard JSON number নয়।

Strict behavior চাইলে:

```python
json.dumps(
    data,
    allow_nan=False
)
```

এতে `ValueError` হবে।

### Important

API বা standard-compliant JSON তৈরি করতে special floating-point values থাকলে এই option সম্পর্কে জানা দরকার।

---

# 1️⃣2️⃣ `allow_nan` Example

```python
import json

data = {
    "score": float("nan")
}

try:

    result = json.dumps(
        data,
        allow_nan=False
    )

    print(result)

except ValueError:

    print("Invalid JSON number!")
```

Output:

```text
Invalid JSON number!
```

---

# 1️⃣3️⃣ `dump()`-এর Formatting

File-এ:

```python
import json

data = {
    "name": "আতিয়ার",
    "age": 22,
    "city": "ঢাকা"
}

with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        sort_keys=True,
        ensure_ascii=False
    )
```

Result:

```json
{
    "age": 22,
    "city": "ঢাকা",
    "name": "আতিয়ার"
}
```

---

# 1️⃣4️⃣ JSON Formatting-এর Complete Combination ⭐⭐⭐

```python
import json

data = {
    "name": "আতিয়ার",
    "age": 22,
    "city": "ঢাকা",
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}

result = json.dumps(
    data,
    indent=4,
    sort_keys=True,
    ensure_ascii=False
)

print(result)
```

এই combination বেশিরভাগ learning/project situation-এর জন্য যথেষ্ট।

---

# 1️⃣5️⃣ `json.dumps()` দিয়ে Custom Formatting

তুমি চাইলে `indent` string-ও দিতে পারো।

```python
result = json.dumps(
    data,
    indent="    "
)
```

অর্থাৎ ৪টি space-এর বদলে নির্দিষ্ট indentation string ব্যবহার করা যায়।

---

# 1️⃣6️⃣ `sort_keys` Nested Data-তেও কাজ করে

```python
data = {
    "user": {
        "name": "Rahim",
        "age": 25,
        "city": "Dhaka"
    }
}
```

```python
print(
    json.dumps(
        data,
        indent=4,
        sort_keys=True
    )
)
```

Nested object-এর keys-ও sort হবে।

---

# 1️⃣7️⃣ JSON Formatting-এর Practical Rule

তোমার project-এ সাধারণত:

### Development / Debugging

```python
json.dumps(
    data,
    indent=4,
    ensure_ascii=False
)
```

### Predictable output

```python
json.dumps(
    data,
    indent=4,
    sort_keys=True,
    ensure_ascii=False
)
```

### Compact output

```python
json.dumps(
    data,
    separators=(",", ":")
)
```

---

# 1️⃣8️⃣ `dump()` + `load()` + Formatting

একটি complete example:

```python
import json

data = {
    "name": "আতিয়ার",
    "age": 22,
    "skills": [
        "Python",
        "Django",
        "React"
    ]
}

# Write
with open(
    "student.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        data,
        file,
        indent=4,
        ensure_ascii=False,
        sort_keys=True
    )


# Read
with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    loaded_data = json.load(file)


print(loaded_data)
```

Flow:

```text
Python dict
    ↓
json.dump()
    ↓
Formatted JSON file
    ↓
json.load()
    ↓
Python dict
```

---

# 1️⃣9️⃣ JSON বনাম Python `repr()`

এটা একটা গুরুত্বপূর্ণ concept।

Python:

```python
data = {
    "name": "Rahim"
}

print(data)
```

Output:

```text
{'name': 'Rahim'}
```

এটা Python dictionary representation।

JSON:

```python
print(json.dumps(data))
```

Output:

```json
{"name": "Rahim"}
```

JSON-এ standard JSON syntax ব্যবহার হয়।

---

# 🧠 2️⃣0️⃣ আজকের সবচেয়ে গুরুত্বপূর্ণ Parameters

|Parameter|কাজ|
|---|---|
|`indent`|Pretty formatting|
|`sort_keys`|Keys sort|
|`ensure_ascii`|Unicode representation|
|`separators`|JSON spacing/control|
|`allow_nan`|Non-standard float handling|

---

# 🧪 Day 6 Practice

## Exercise 1

এই data:

```python
data = {
    "z": 10,
    "a": 20,
    "m": 30
}
```

`sort_keys=True` দিয়ে JSON বানাও।

Expected:

```json
{
    "a": 20,
    "m": 30,
    "z": 10
}
```

---

## Exercise 2

বাংলা data:

```python
data = {
    "name": "আতিয়ার",
    "country": "বাংলাদেশ",
    "city": "ঢাকা"
}
```

`ensure_ascii=False` এবং `indent=4` ব্যবহার করো।

---

## Exercise 3 ⭐

একটি compact JSON তৈরি করো:

```python
separators=(",", ":")
```

---

## Exercise 4 ⭐⭐

একই data দিয়ে দুই ধরনের JSON তৈরি করো:

### Pretty

```text
indent=4
```

### Compact

```text
separators=(",", ":")
```

দুটোর output compare করো।

---

## Exercise 5 ⭐⭐

`allow_nan=False` দিয়ে:

```python
data = {
    "score": float("nan")
}
```

serialize করার চেষ্টা করো এবং কী error হচ্ছে দেখো।

---

# 🏆 Day 6 Mini Project

## JSON Formatter Tool

একটি program বানাও:

```text
========================
    JSON FORMATTER
========================

1. Pretty JSON
2. Compact JSON
3. Sorted JSON
4. Unicode JSON
5. Exit
```

একটি Python dictionary থাকবে।

User option অনুযায়ী:

```text
1 → indent=4
2 → separators=(",", ":")
3 → sort_keys=True
4 → ensure_ascii=False
```

ব্যবহার করে output দেখাবে।

---

# 📌 Day 6 Cheat Sheet

```python
# Pretty
json.dumps(data, indent=4)

# Sorted
json.dumps(data, sort_keys=True)

# Unicode
json.dumps(data, ensure_ascii=False)

# Compact
json.dumps(data, separators=(",", ":"))

# Strict special-float handling
json.dumps(data, allow_nan=False)
```

### সবচেয়ে useful combination:

```python
json.dumps(
    data,
    indent=4,
    sort_keys=True,
    ensure_ascii=False
)
```

---

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ✅
Day 6  → Formatting + Sorting + Encoding   ✅
Day 7  → Error Handling + Validation       ⏭️
Day 8  → JSON + pathlib + Configuration
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 7-এ আমরা JSON error handling, `JSONDecodeError`, invalid JSON, validation এবং robust JSON loader তৈরি করা শিখব।**

# 🐍 Python `json` Module — Day 7

## Error Handling, Validation & Robust JSON Handling

আজ আমরা শিখব কীভাবে JSON program-কে **ভেঙে যাওয়া থেকে রক্ষা করতে হয়**।

আজকের মূল বিষয়:

```text
JSON Error
   ↓
try / except
   ↓
JSONDecodeError
   ↓
FileNotFoundError
   ↓
Validation
   ↓
Safe JSON Loader
```

Official documentation: [Python `json` documentation — Exceptions & decoding](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com#exceptions)

---

# 1️⃣ JSON Error কেন হয়?

ধরো `student.json`:

```json
{
    "name": "Rahim",
    "age": 25
}
```

এটা valid JSON।

কিন্তু যদি ভুল করে লিখো:

```text
{
    "name": "Rahim",
    "age": 25
```

শেষের:

```text
}
```

নেই।

তাহলে:

```python
json.load(file)
```

করলে JSON parsing error হবে।

---

# 2️⃣ `JSONDecodeError` ⭐⭐⭐

Invalid JSON handle করার জন্য:

```python
import json

try:

    with open(
        "student.json",
        "r",
        encoding="utf-8"
    ) as file:

        data = json.load(file)

except json.JSONDecodeError:

    print("Invalid JSON!")
```

এখন program crash না করে message দেখাবে।

---

# 3️⃣ `FileNotFoundError`

File-ই যদি না থাকে:

```python
import json

try:

    with open(
        "student.json",
        "r",
        encoding="utf-8"
    ) as file:

        data = json.load(file)

except FileNotFoundError:

    print("File does not exist!")

except json.JSONDecodeError:

    print("JSON file is invalid!")
```

এখন দুই ধরনের problem আলাদা করে handle হচ্ছে।

---

# 4️⃣ দুই Error-এর Difference

|Error|কারণ|
|---|---|
|`FileNotFoundError`|File পাওয়া যায়নি|
|`JSONDecodeError`|File আছে কিন্তু JSON invalid|

Mental model:

```text
Open file
   │
   ├── File নেই
   │      ↓
   │ FileNotFoundError
   │
   └── File আছে
          ↓
       json.load()
          │
          ├── Invalid JSON
          │      ↓
          │ JSONDecodeError
          │
          └── Valid JSON
                 ↓
             Python object
```

---

# 5️⃣ `try / except / else / finally`

Python exception handling-এর complete structure:

```python
try:
    # risky code

except:
    # error

else:
    # no error

finally:
    # always runs
```

JSON example:

```python
import json

try:

    with open(
        "student.json",
        "r",
        encoding="utf-8"
    ) as file:

        data = json.load(file)

except FileNotFoundError:

    print("File not found!")

except json.JSONDecodeError:

    print("Invalid JSON!")

else:

    print("JSON loaded successfully!")
    print(data)

finally:

    print("Operation finished.")
```

---

# 6️⃣ `except Exception` কখন ব্যবহার করবে?

তুমি চাইলে:

```python
except Exception as e:
    print(e)
```

কিন্তু beginners-এর জন্য সব error এভাবে ধরার অভ্যাস ভালো নয়।

Better:

```python
except FileNotFoundError:
    ...

except json.JSONDecodeError:
    ...
```

কারণ তুমি জানো **কোন error কেন হচ্ছে**।

---

# 7️⃣ Error Message দেখা

```python
except json.JSONDecodeError as e:

    print("Invalid JSON")
    print("Error:", e)
```

এতে Python error-এর বিস্তারিত information দেখাবে।

---

# 8️⃣ `JSONDecodeError` থেকে Location জানা ⭐⭐

`JSONDecodeError`-এর কিছু useful attributes আছে।

```python
except json.JSONDecodeError as e:

    print("Message:", e.msg)
    print("Line:", e.lineno)
    print("Column:", e.colno)
```

যেমন invalid JSON হলে:

```text
Message: Expecting property name enclosed in double quotes
Line: 3
Column: 5
```

Debugging-এর জন্য এটা খুব useful।

---

# 9️⃣ Invalid JSON Example

ভুল:

```json
{
    "name": "Rahim",
    "age": 25,
}
```

শেষের comma-এর কারণে standard JSON invalid।

Python:

```python
import json

try:

    json.loads("""
    {
        "name": "Rahim",
        "age": 25,
    }
    """)

except json.JSONDecodeError as e:

    print("Invalid JSON!")
    print("Line:", e.lineno)
    print("Column:", e.colno)
```

---

# 🔟 JSON-এর গুরুত্বপূর্ণ Rule ⭐⭐⭐

Python dictionary:

```python
{
    "name": "Rahim"
}
```

JSON:

```json
{
    "name": "Rahim"
}
```

JSON-এর key অবশ্যই **double quotes**-এ হতে হবে।

❌ ভুল:

```json
{
    'name': 'Rahim'
}
```

✅ সঠিক:

```json
{
    "name": "Rahim"
}
```

---

# 1️⃣1️⃣ Python `True` বনাম JSON `true`

Python:

```python
data = {
    "active": True
}
```

JSON:

```json
{
    "active": true
}
```

Python:

```text
True
False
None
```

JSON:

```text
true
false
null
```

`json` module conversion automatically করে।

---

# 1️⃣2️⃣ Validation কী?

JSON valid হলেই data **সঠিক** হবে—এমন না।

ধরো:

```json
{
    "name": "Rahim",
    "age": "twenty"
}
```

এটা valid JSON।

কিন্তু আমাদের application যদি `age` integer আশা করে, তাহলে data invalid **for our application**।

তাই দুই ধরনের checking:

```text
JSON Syntax Validation
        +
Application Data Validation
```

---

# 1️⃣3️⃣ Basic Validation

ধরো আমরা চাই:

```text
name → string
age → integer
```

Code:

```python
import json

with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    student = json.load(file)


if not isinstance(student, dict):

    print("Student data must be an object!")

elif not isinstance(student.get("name"), str):

    print("Name must be a string!")

elif not isinstance(student.get("age"), int):

    print("Age must be an integer!")

else:

    print("Valid student data!")
```

---

# 1️⃣4️⃣ Required Fields ⭐⭐⭐

ধরো `name` এবং `age` অবশ্যই থাকতে হবে।

```python
required_fields = [
    "name",
    "age"
]

for field in required_fields:

    if field not in student:

        print(
            f"Missing field: {field}"
        )
```

---

# 1️⃣5️⃣ Required Field + Type Validation

আরও clean:

```python
import json

with open(
    "student.json",
    "r",
    encoding="utf-8"
) as file:

    student = json.load(file)


if "name" not in student:
    print("Name is required!")

elif "age" not in student:
    print("Age is required!")

elif not isinstance(student["name"], str):
    print("Name must be a string!")

elif not isinstance(student["age"], int):
    print("Age must be an integer!")

else:
    print("Student data is valid!")
```

---

# 1️⃣6️⃣ Function দিয়ে Validation ⭐⭐⭐

একই validation বারবার লিখতে চাই না।

```python
def validate_student(student):

    if not isinstance(student, dict):
        return False

    if "name" not in student:
        return False

    if "age" not in student:
        return False

    if not isinstance(student["name"], str):
        return False

    if not isinstance(student["age"], int):
        return False

    return True
```

Use:

```python
if validate_student(student):
    print("Valid student")
else:
    print("Invalid student")
```

---

# 1️⃣7️⃣ Better Validation Function

কেন invalid সেটা জানালে বেশি useful:

```python
def validate_student(student):

    if not isinstance(student, dict):
        return "Student must be an object"

    if "name" not in student:
        return "Name is required"

    if "age" not in student:
        return "Age is required"

    if not isinstance(student["name"], str):
        return "Name must be a string"

    if not isinstance(student["age"], int):
        return "Age must be an integer"

    return None
```

Use:

```python
error = validate_student(student)

if error:
    print("Validation error:", error)
else:
    print("Valid student!")
```

---

# 1️⃣8️⃣ Safe JSON Loader ⭐⭐⭐

এখন আমরা একটা reusable function বানাবো।

```python
import json


def load_json(path):

    try:

        with open(
            path,
            "r",
            encoding="utf-8"
        ) as file:

            return json.load(file)

    except FileNotFoundError:

        print("File not found!")
        return None

    except json.JSONDecodeError:

        print("Invalid JSON!")
        return None
```

Use:

```python
data = load_json(
    "students.json"
)

if data is not None:
    print(data)
```

এটা real project-এ useful pattern।

---

# 1️⃣9️⃣ Safe JSON Saver

একইভাবে:

```python
import json


def save_json(path, data):

    try:

        with open(
            path,
            "w",
            encoding="utf-8"
        ) as file:

            json.dump(
                data,
                file,
                indent=4,
                ensure_ascii=False
            )

        return True

    except OSError as e:

        print("Could not save file:", e)
        return False
```

Use:

```python
success = save_json(
    "students.json",
    students
)

if success:
    print("Saved successfully!")
```

---

# 2️⃣0️⃣ `OSError` কেন?

File-related অনেক operating-system error `OSError` hierarchy-এর মধ্যে আসে।

যেমন:

```text
Permission problem
File system problem
Invalid path
```

তাই save operation-এর জন্য:

```python
except OSError:
```

useful হতে পারে।

---

# 2️⃣1️⃣ Safe JSON Database Pattern 🔥

এখন Day 4 + Day 7 combine করি।

```python
import json


def load_json(path):

    try:

        with open(
            path,
            "r",
            encoding="utf-8"
        ) as file:

            return json.load(file)

    except FileNotFoundError:

        return []

    except json.JSONDecodeError:

        print("Invalid JSON!")
        return []


def save_json(path, data):

    with open(
        path,
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            data,
            file,
            indent=4,
            ensure_ascii=False
        )
```

তারপর:

```python
students = load_json(
    "students.json"
)

students.append({
    "id": 1,
    "name": "Rahim"
})

save_json(
    "students.json",
    students
)
```

Flow:

```text
students.json
     ↓
 load_json()
     ↓
Python list
     ↓
Modify
     ↓
save_json()
     ↓
students.json
```

---

# 2️⃣2️⃣ Empty JSON File

ধরো `students.json` একদম empty:

```text
<empty>
```

তাহলে:

```python
json.load(file)
```

করলে `JSONDecodeError` হবে।

তাই:

```python
except json.JSONDecodeError:
    return []
```

ব্যবহার করে empty database হিসেবে শুরু করা যায়।

---

# 2️⃣3️⃣ `null` Handle করা

JSON:

```json
{
    "name": "Rahim",
    "phone": null
}
```

Python:

```python
data["phone"]
```

হবে:

```python
None
```

Check:

```python
if data["phone"] is None:
    print("Phone number not provided")
```

---

# 2️⃣4️⃣ Validation Example — Complete

ধরো:

```json
{
    "name": "Rahim",
    "age": 25,
    "email": "rahim@example.com"
}
```

Validator:

```python
def validate_student(student):

    required = [
        "name",
        "age",
        "email"
    ]

    for field in required:

        if field not in student:
            return f"{field} is required"

    if not isinstance(student["name"], str):
        return "Name must be string"

    if not isinstance(student["age"], int):
        return "Age must be integer"

    if not isinstance(student["email"], str):
        return "Email must be string"

    return None
```

Use:

```python
error = validate_student(student)

if error:
    print("Invalid:", error)
else:
    print("Student is valid!")
```

---

# 2️⃣5️⃣ Important: Valid JSON ≠ Valid Application Data ⭐⭐⭐

এইটা মনে রাখবে।

```json
{
    "name": 123,
    "age": "hello"
}
```

এটা **valid JSON**।

কিন্তু student application-এর জন্য হয়তো invalid।

তাই:

```text
JSON Parser
     ↓
Syntax valid?
     ↓
Application Validator
     ↓
Data valid?
```

---

# 🧪 Day 7 Practice

### Exercise 1

একটি invalid JSON file তৈরি করো এবং `JSONDecodeError` handle করো।

---

### Exercise 2

File না থাকলে:

```text
File not found!
```

দেখাবে।

---

### Exercise 3

একটি JSON file থেকে:

```text
name
age
email
```

required field হিসেবে validate করো।

---

### Exercise 4 ⭐

Check করো:

```text
name → string
age → integer
skills → list
```

---

### Exercise 5 ⭐⭐

`load_json()` function বানাও:

```python
data = load_json("students.json")
```

File না থাকলে:

```python
[]
```

return করবে।

Invalid JSON হলে error message দেখাবে।

---

### Exercise 6 ⭐⭐

`save_json()` function বানাও:

```python
save_json(
    "students.json",
    students
)
```

এবং:

```text
indent=4
ensure_ascii=False
```

ব্যবহার করো।

---

# 🏆 Day 7 Mini Project

## Robust Student JSON Manager

আজকের project:

```text
=========================
 STUDENT MANAGER
=========================

1. View students
2. Add student
3. Update student
4. Delete student
5. Search student
6. Exit
```

Requirements:

```text
✔ JSON file missing → automatically handle
✔ Invalid JSON → handle
✔ Required fields → validate
✔ Data types → validate
✔ load_json() function
✔ save_json() function
✔ Nested/list data support
```

এই project শেষ করলে তুমি `json` module-এর basic থেকে intermediate usage অনেকটাই practically cover করে ফেলবে।

---

# 📌 Day 7 Cheat Sheet

### JSON error

```python
except json.JSONDecodeError:
```

### File error

```python
except FileNotFoundError:
```

### General file-system error

```python
except OSError:
```

### Error details

```python
except json.JSONDecodeError as e:
    print(e.msg)
    print(e.lineno)
    print(e.colno)
```

### Validation

```python
isinstance(data, dict)
isinstance(data, list)
isinstance(data, str)
isinstance(data, int)
```

### Safe loading

```python
def load_json(path):
    try:
        with open(path, "r", encoding="utf-8") as file:
            return json.load(file)
    except FileNotFoundError:
        return []
    except json.JSONDecodeError:
        return []
```

---

# 📚 Course Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ✅
Day 6  → Formatting + Sorting + Encoding   ✅
Day 7  → Error Handling + Validation       ✅
Day 8  → JSON + pathlib + Configuration    ⏭️
Day 9  → JSON + API
Day 10 → 🔥 JSON Database Project
```

**Day 8-এ `json` + `pathlib` দিয়ে proper configuration system, file paths, default config, config update এবং project structure তৈরি করব।**

# 🐍 Python `json` Module — Day 8

## `json` + `pathlib` + Configuration System

আজ আমরা `json`-কে শুধু data file হিসেবে নয়, **real project configuration system** হিসেবে ব্যবহার করব।

আজকের লক্ষ্য:

```text
pathlib
   +
json
   ↓
config.json
   ↓
Load
   ↓
Validate
   ↓
Modify
   ↓
Save
```

Official documentation: [Python `json` documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)  
Official `pathlib` documentation: [Python `pathlib` documentation](https://docs.python.org/3/library/pathlib.html?utm_source=chatgpt.com)

---

# 1️⃣ Configuration কী?

Application-এর কিছু settings code-এর ভিতরে hard-code না করে আলাদা file-এ রাখাকে configuration approach বলতে পারো।

যেমন:

```json
{
    "app_name": "Student Manager",
    "debug": true,
    "language": "en",
    "max_students": 100
}
```

File:

```text
config.json
```

তাহলে Python code থেকে:

```python
config["debug"]
```

দিয়ে setting ব্যবহার করা যায়।

---

# 2️⃣ কেন Configuration File ব্যবহার করব?

ধরো code-এর মধ্যে:

```python
MAX_STUDENTS = 100
DEBUG = True
LANGUAGE = "en"
```

এগুলো পরিবর্তন করতে code edit করতে হবে।

কিন্তু config file ব্যবহার করলে:

```json
{
    "max_students": 100,
    "debug": true,
    "language": "en"
}
```

শুধু JSON পরিবর্তন করলেই হবে।

---

# 3️⃣ Project Structure ⭐⭐⭐

আজ থেকে এই structure follow করো:

```text
student_manager/
│
├── main.py
│
├── config/
│   └── config.json
│
└── data/
    └── students.json
```

এখানে:

```text
config/ → application settings
data/   → application data
```

এটা খুব useful separation।

---

# 4️⃣ `pathlib` দিয়ে Path তৈরি

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent

CONFIG_DIR = BASE_DIR / "config"

CONFIG_FILE = CONFIG_DIR / "config.json"
```

এখন:

```text
CONFIG_FILE
```

হবে:

```text
student_manager/config/config.json
```

---

# 5️⃣ Directory Automatically Create

```python
CONFIG_DIR.mkdir(
    parents=True,
    exist_ok=True
)
```

এখানে:

```text
parents=True
```

প্রয়োজন হলে parent directory তৈরি করবে।

আর:

```text
exist_ok=True
```

মানে directory আগে থেকেই থাকলে error করবে না।

---

# 6️⃣ Default Configuration ⭐⭐⭐

ধরো প্রথমবার application চালালে config file নেই।

তখন default config তৈরি করব।

```python
DEFAULT_CONFIG = {
    "app_name": "Student Manager",
    "debug": True,
    "language": "en",
    "max_students": 100
}
```

---

# 7️⃣ Default Config Save করা

```python
import json
from pathlib import Path


BASE_DIR = Path(__file__).resolve().parent

CONFIG_DIR = BASE_DIR / "config"
CONFIG_FILE = CONFIG_DIR / "config.json"

CONFIG_DIR.mkdir(
    parents=True,
    exist_ok=True
)


DEFAULT_CONFIG = {
    "app_name": "Student Manager",
    "debug": True,
    "language": "en",
    "max_students": 100
}


if not CONFIG_FILE.exists():

    with CONFIG_FILE.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            DEFAULT_CONFIG,
            file,
            indent=4
        )
```

প্রথমবার run করলে:

```text
config/
└── config.json
```

তৈরি হবে।

---

# 8️⃣ Config Load করা

```python
with CONFIG_FILE.open(
    "r",
    encoding="utf-8"
) as file:

    config = json.load(file)
```

তারপর:

```python
print(config)
```

---

# 9️⃣ Configuration Access

```python
print(config["app_name"])
```

Output:

```text
Student Manager
```

আর:

```python
print(config["max_students"])
```

Output:

```text
100
```

---

# 🔟 `.get()` ব্যবহার

যদি কোনো setting না থাকে:

```python
language = config.get(
    "language",
    "en"
)
```

মানে:

```text
language থাকলে → সেটি
না থাকলে → "en"
```

---

# 1️⃣1️⃣ Config Update ⭐⭐⭐

ধরো user চাইছে:

```text
max_students = 200
```

Python:

```python
config["max_students"] = 200
```

কিন্তু শুধু memory-তে পরিবর্তন হয়েছে।

File update করতে:

```python
with CONFIG_FILE.open(
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        config,
        file,
        indent=4
    )
```

Flow:

```text
config.json
    ↓
json.load()
    ↓
Python dict
    ↓
Modify
    ↓
json.dump()
    ↓
config.json
```

---

# 1️⃣2️⃣ Configuration-এর Nested Structure ⭐⭐⭐

Real project-এ config nested হতে পারে।

```json
{
    "app": {
        "name": "Student Manager",
        "version": "1.0"
    },
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "students"
    },
    "logging": {
        "enabled": true,
        "level": "INFO"
    }
}
```

Python:

```python
config["app"]["name"]
```

Output:

```text
Student Manager
```

Database port:

```python
config["database"]["port"]
```

Output:

```text
5432
```

---

# 1️⃣3️⃣ Better Configuration File

তুমি project-এ এমন config রাখতে পারো:

```json
{
    "app": {
        "name": "Student Manager",
        "version": "1.0.0",
        "debug": true
    },
    "student": {
        "max_students": 100,
        "default_department": "CSE"
    },
    "storage": {
        "data_file": "data/students.json"
    }
}
```

তারপর:

```python
config["student"]["max_students"]
```

---

# 1️⃣4️⃣ Config Validation

শুধু JSON valid হলেই হবে না।

ধরো:

```json
{
    "app": {
        "name": "Student Manager"
    }
}
```

কিন্তু আমাদের application চায়:

```text
app
student
storage
```

তাই validation দরকার।

```python
def validate_config(config):

    required_sections = [
        "app",
        "student",
        "storage"
    ]

    for section in required_sections:

        if section not in config:

            return False

    return True
```

Use:

```python
if validate_config(config):

    print("Configuration valid!")

else:

    print("Invalid configuration!")
```

---

# 1️⃣5️⃣ Type Validation

আরও ভালো validation:

```python
def validate_config(config):

    if not isinstance(config, dict):
        return False

    if "app" not in config:
        return False

    if "student" not in config:
        return False

    if not isinstance(
        config["student"],
        dict
    ):
        return False

    if "max_students" not in config["student"]:
        return False

    if not isinstance(
        config["student"]["max_students"],
        int
    ):
        return False

    return True
```

---

# 1️⃣6️⃣ `load_config()` Function ⭐⭐⭐

এখন সবকিছু function-এর মধ্যে রাখি।

```python
import json
from pathlib import Path


def load_config(path):

    try:

        with path.open(
            "r",
            encoding="utf-8"
        ) as file:

            return json.load(file)

    except FileNotFoundError:

        return None

    except json.JSONDecodeError:

        print("Invalid configuration file!")

        return None
```

Use:

```python
config = load_config(
    CONFIG_FILE
)
```

---

# 1️⃣7️⃣ `save_config()` Function

```python
def save_config(path, config):

    path.parent.mkdir(
        parents=True,
        exist_ok=True
    )

    with path.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            config,
            file,
            indent=4,
            ensure_ascii=False
        )
```

Use:

```python
save_config(
    CONFIG_FILE,
    config
)
```

---

# 1️⃣8️⃣ Complete Configuration Manager 🔥

এখন সব একসাথে:

```python
import json
from pathlib import Path


BASE_DIR = Path(__file__).resolve().parent

CONFIG_DIR = BASE_DIR / "config"

CONFIG_FILE = CONFIG_DIR / "config.json"


DEFAULT_CONFIG = {
    "app": {
        "name": "Student Manager",
        "version": "1.0.0",
        "debug": True
    },
    "student": {
        "max_students": 100,
        "default_department": "CSE"
    },
    "storage": {
        "data_file": "data/students.json"
    }
}


def save_config(path, config):

    path.parent.mkdir(
        parents=True,
        exist_ok=True
    )

    with path.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            config,
            file,
            indent=4,
            ensure_ascii=False
        )


def load_config(path):

    try:

        with path.open(
            "r",
            encoding="utf-8"
        ) as file:

            return json.load(file)

    except FileNotFoundError:

        save_config(
            path,
            DEFAULT_CONFIG
        )

        return DEFAULT_CONFIG

    except json.JSONDecodeError:

        print("Invalid config!")

        return DEFAULT_CONFIG


config = load_config(
    CONFIG_FILE
)

print(
    config["app"]["name"]
)

print(
    config["student"]["max_students"]
)
```

---

# 1️⃣9️⃣ Data File Path Config থেকে নেওয়া

Config:

```json
{
    "storage": {
        "data_file": "data/students.json"
    }
}
```

Python:

```python
data_file = (
    BASE_DIR /
    config["storage"]["data_file"]
)
```

এখন:

```text
student_manager/
│
├── config/
│   └── config.json
│
└── data/
    └── students.json
```

---

# 2️⃣0️⃣ Config + Student Data

এখন architecture:

```text
student_manager/
│
├── main.py
│
├── config/
│   └── config.json
│
└── data/
    └── students.json
```

Flow:

```text
main.py
   │
   ├── config.json
   │       ↓
   │    settings
   │
   └── students.json
           ↓
       application data
```

এটা আগের Day 7 project-কে অনেক বেশি organized করে।

---

# 2️⃣1️⃣ Configuration Change

ধরো:

```python
config["student"]["max_students"] = 500
```

তারপর:

```python
save_config(
    CONFIG_FILE,
    config
)
```

File automatically update হবে।

---

# 2️⃣2️⃣ Important Concept: Config vs Data

এটা খুব ভালোভাবে মনে রাখবে।

### Configuration

```text
config.json
```

contains:

```text
app settings
database settings
limits
features
paths
```

### Data

```text
students.json
```

contains:

```text
students
users
products
orders
```

অর্থাৎ:

```text
Configuration ≠ Application Data
```

---

# 2️⃣3️⃣ আজকের Practical Architecture

```text
                 Application
                      │
              ┌───────┴───────┐
              ↓               ↓
         config.json     students.json
              │               │
              ↓               ↓
         Settings           Data
              │               │
              └───────┬───────┘
                      ↓
                    main.py
```

---

# 🧪 Day 8 Practice

### Exercise 1

এই structure তৈরি করো:

```text
my_project/
├── main.py
├── config/
│   └── config.json
└── data/
    └── students.json
```

`pathlib` দিয়ে directories তৈরি করবে।

---

### Exercise 2

Default config বানাও:

```json
{
    "app": {
        "name": "My App",
        "version": "1.0"
    },
    "student": {
        "max_students": 100
    }
}
```

---

### Exercise 3 ⭐

`load_config()` function তৈরি করো।

File না থাকলে default config তৈরি করবে।

---

### Exercise 4 ⭐⭐

Config validation করো:

```text
app → dict
student → dict
max_students → int
```

---

### Exercise 5 ⭐⭐

User input নিয়ে:

```text
Enter maximum students:
```

config update করো এবং আবার `config.json`-এ save করো।

---

# 🏆 Day 8 Mini Project

## ⚙️ Configuration Manager

Program:

```text
==========================
   CONFIG MANAGER
==========================

1. Show configuration
2. Change app name
3. Change max students
4. Toggle debug
5. Reset configuration
6. Exit
```

সব পরিবর্তন:

```text
load
 ↓
modify
 ↓
validate
 ↓
save
```

করবে।

---

# 📌 Day 8 Cheat Sheet

### Path

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent
```

### Config path

```python
CONFIG_FILE = BASE_DIR / "config" / "config.json"
```

### Directory

```python
CONFIG_FILE.parent.mkdir(
    parents=True,
    exist_ok=True
)
```

### Load

```python
with CONFIG_FILE.open(
    "r",
    encoding="utf-8"
) as file:

    config = json.load(file)
```

### Save

```python
with CONFIG_FILE.open(
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        config,
        file,
        indent=4,
        ensure_ascii=False
    )
```

---

# 📚 Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ✅
Day 6  → Formatting + Sorting + Encoding   ✅
Day 7  → Error Handling + Validation       ✅
Day 8  → json + pathlib + Configuration    ✅
Day 9  → JSON + API                        ⏭️
Day 10 → 🔥 JSON Database Project
```

**Day 9-এ আমরা JSON-কে HTTP/API-এর সাথে ব্যবহার করব—API response থেকে JSON পড়া, JSON request body তৈরি করা, `requests` দিয়ে API call করা এবং real-world API response parse করা।**


# 🐍 Python `json` Module — Day 9

## JSON + API + `requests`

আজ আমরা শিখব **real-world API থেকে JSON নেওয়া এবং API-তে JSON পাঠানো**।

আজকের flow:

```text
Python
  ↓
HTTP Request
  ↓
API
  ↓
JSON Response
  ↓
Python dict/list
```

এটা তোমার **Django REST API / React frontend / Python backend** কাজের জন্য খুবই গুরুত্বপূর্ণ।

Official docs: [Python `json` documentation](https://docs.python.org/3/library/json.html?utm_source=chatgpt.com)  
`requests` documentation: [Requests documentation](https://requests.readthedocs.io/en/latest/?utm_source=chatgpt.com)

---

# 1️⃣ API কী?

API হলো এমন একটি interface যার মাধ্যমে একটি application অন্য application-এর সাথে data exchange করে।

উদাহরণ:

```text
Python Application
       ↓
    HTTP GET
       ↓
     Server
       ↓
   JSON Response
```

Response:

```json
{
    "id": 1,
    "name": "Rahim",
    "age": 25
}
```

Python-এ এই JSON response সাধারণত dictionary/list হিসেবে ব্যবহার করবে।

---

# 2️⃣ `requests` Install

`requests` Python-এর built-in module নয়।

Install:

```bash
pip install requests
```

তারপর:

```python
import requests
```

---

# 3️⃣ প্রথম GET Request ⭐⭐⭐

একটি public test API ব্যবহার করি:

```python
import requests

response = requests.get(
    "https://jsonplaceholder.typicode.com/users/1"
)

print(response.status_code)
```

সাধারণত successful request-এর status:

```text
200
```

---

# 4️⃣ `response.text`

Server থেকে আসা raw response:

```python
print(response.text)
```

তুমি JSON text-এর মতো কিছু দেখতে পারো:

```json
{
    "id": 1,
    "name": "Leanne Graham"
}
```

`response.text` হলো **string**।

---

# 5️⃣ `response.json()` ⭐⭐⭐

সবচেয়ে গুরুত্বপূর্ণ।

```python
data = response.json()

print(data)
```

এখন JSON response Python object-এ convert হয়েছে।

যেমন:

```python
print(data["name"])
```

Output-এর মতো হবে:

```text
Leanne Graham
```

---

# 6️⃣ `response.json()` বনাম `json.loads()`

এখানে important difference:

### Raw JSON string

```python
json.loads(response.text)
```

### Requests-এর convenient method

```python
response.json()
```

অর্থাৎ:

```python
data = response.json()
```

সাধারণ API code-এ বেশি convenient।

---

# 7️⃣ GET Request-এর Complete Example

```python
import requests

url = "https://jsonplaceholder.typicode.com/users/1"

response = requests.get(url)

print("Status:", response.status_code)

data = response.json()

print("ID:", data["id"])
print("Name:", data["name"])
print("Email:", data["email"])
```

---

# 8️⃣ Status Code Check ⭐⭐⭐

শুধু response পাওয়া গেলেই হবে না।

```python
response = requests.get(url)

if response.status_code == 200:

    data = response.json()

    print(data)

else:

    print(
        "Request failed:",
        response.status_code
    )
```

Common status codes:

|Status|Meaning|
|--:|---|
|`200`|OK|
|`201`|Created|
|`400`|Bad Request|
|`401`|Unauthorized|
|`403`|Forbidden|
|`404`|Not Found|
|`500`|Server Error|

---

# 9️⃣ `raise_for_status()` ⭐⭐⭐

আরও clean approach:

```python
response = requests.get(url)

response.raise_for_status()

data = response.json()

print(data)
```

যদি HTTP error থাকে, exception raise করবে।

---

# 🔟 API Error Handling

Real-world code:

```python
import requests

url = "https://jsonplaceholder.typicode.com/users/1"

try:

    response = requests.get(
        url,
        timeout=10
    )

    response.raise_for_status()

    data = response.json()

    print(data)

except requests.RequestException as e:

    print("Request error:", e)

except ValueError:

    print("Response is not valid JSON!")
```

এখানে:

```text
Network/HTTP problem
        ↓
RequestException

JSON parsing problem
        ↓
ValueError
```

---

# 1️⃣1️⃣ `timeout` ⭐⭐⭐

API request কখনো কখনো indefinitely wait করতে পারে।

তাই:

```python
requests.get(
    url,
    timeout=10
)
```

মানে request-এর জন্য maximum waiting time নির্ধারণ করা।

**Production code-এ timeout দেওয়া ভালো practice।**

---

# 1️⃣2️⃣ API থেকে Multiple Users

Endpoint:

```text
/users
```

Code:

```python
import requests

url = "https://jsonplaceholder.typicode.com/users"

response = requests.get(
    url,
    timeout=10
)

response.raise_for_status()

users = response.json()

print(type(users))
```

Output:

```text
<class 'list'>
```

কারণ API response:

```json
[
    {
        "id": 1,
        "name": "Leanne Graham"
    },
    {
        "id": 2,
        "name": "Ervin Howell"
    }
]
```

---

# 1️⃣3️⃣ Loop দিয়ে API Data

```python
for user in users:

    print(
        user["id"],
        user["name"]
    )
```

Output-এর মতো:

```text
1 Leanne Graham
2 Ervin Howell
3 Clementine Bauch
...
```

---

# 1️⃣4️⃣ Nested API JSON ⭐⭐⭐

API response হতে পারে:

```json
{
    "id": 1,
    "name": "Rahim",
    "address": {
        "city": "Dhaka",
        "country": "Bangladesh"
    }
}
```

Access:

```python
data["address"]["city"]
```

Output:

```text
Dhaka
```

এটা Day 5-এর nested JSON concept-এর direct application।

---

# 1️⃣5️⃣ Query Parameters

API-তে parameters পাঠাতে পারো:

```python
params = {
    "userId": 1
}

response = requests.get(
    "https://jsonplaceholder.typicode.com/posts",
    params=params,
    timeout=10
)
```

Requests নিজে URL তৈরি করবে।

Conceptually:

```text
/posts?userId=1
```

---

# 1️⃣6️⃣ Query Parameters কেন দরকার?

ধরো API:

```text
/products?category=phone
```

তাহলে Python:

```python
params = {
    "category": "phone"
}

response = requests.get(
    url,
    params=params
)
```

এটা API filtering/search-এর জন্য খুব common।

---

# 1️⃣7️⃣ POST + JSON ⭐⭐⭐

এবার server-এ JSON পাঠানো।

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

data = {
    "title": "Python",
    "body": "Learning JSON",
    "userId": 1
}

response = requests.post(
    url,
    json=data,
    timeout=10
)

print(response.status_code)
print(response.json())
```

এখানে:

```python
json=data
```

খুব important।

Requests dictionary-কে JSON request body হিসেবে পাঠানোর কাজটি handle করে।

---

# 1️⃣8️⃣ `json=` বনাম `data=`

### JSON পাঠাতে:

```python
requests.post(
    url,
    json=data
)
```

### Form-style data:

```python
requests.post(
    url,
    data=data
)
```

API JSON body চাইলে সাধারণত:

```python
json=data
```

ব্যবহার করবে।

---

# 1️⃣9️⃣ Manually `json.dumps()` করা কি দরকার?

সাধারণভাবে `requests` ব্যবহার করলে:

```python
requests.post(
    url,
    json=data
)
```

এটাই যথেষ্ট।

তোমাকে সাধারণত manually:

```python
json.dumps(data)
```

করতে হবে না।

কারণ `requests` JSON encoding handle করে।

---

# 2️⃣0️⃣ POST Response

```python
response = requests.post(
    url,
    json=data,
    timeout=10
)

response.raise_for_status()

result = response.json()

print(result)
```

Concept:

```text
Python dict
    ↓
requests
    ↓
JSON request
    ↓
API
    ↓
JSON response
    ↓
Python dict
```

---

# 2️⃣1️⃣ PUT Request

Existing resource update করার জন্য:

```python
data = {
    "id": 1,
    "title": "Updated title",
    "body": "Updated body",
    "userId": 1
}

response = requests.put(
    "https://jsonplaceholder.typicode.com/posts/1",
    json=data,
    timeout=10
)

response.raise_for_status()

print(response.json())
```

---

# 2️⃣2️⃣ PATCH Request

Partial update:

```python
data = {
    "title": "New title"
}

response = requests.patch(
    "https://jsonplaceholder.typicode.com/posts/1",
    json=data,
    timeout=10
)

response.raise_for_status()

print(response.json())
```

---

# 2️⃣3️⃣ DELETE Request

```python
response = requests.delete(
    "https://jsonplaceholder.typicode.com/posts/1",
    timeout=10
)

print(response.status_code)
```

---

# 2️⃣4️⃣ HTTP Methods মনে রাখো

```text
GET     → Read
POST    → Create
PUT     → Replace/Update
PATCH   → Partial Update
DELETE  → Delete
```

এগুলো তোমার Django REST API শেখার সময় খুব কাজে লাগবে।

---

# 2️⃣5️⃣ JSON Headers ⭐⭐⭐

কখনো API-তে explicitly header পাঠাতে হয়:

```python
headers = {
    "Content-Type": "application/json"
}
```

তারপর:

```python
response = requests.post(
    url,
    json=data,
    headers=headers,
    timeout=10
)
```

তবে `json=` ব্যবহার করলে Requests সাধারণত appropriate JSON content type header সেট করে।

---

# 2️⃣6️⃣ Authorization Header

Authentication API-তে:

```python
headers = {
    "Authorization": "Bearer YOUR_TOKEN"
}
```

তারপর:

```python
response = requests.get(
    url,
    headers=headers,
    timeout=10
)
```

⚠️ বাস্তব token/password source code-এ hard-code করা উচিত নয়।

---

# 2️⃣7️⃣ JSON + API + Save to File 🔥

এবার Day 3/4 + Day 9 combine করি।

```python
import json
import requests

url = "https://jsonplaceholder.typicode.com/users"

response = requests.get(
    url,
    timeout=10
)

response.raise_for_status()

users = response.json()

with open(
    "users.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        users,
        file,
        indent=4,
        ensure_ascii=False
    )
```

Flow:

```text
API
 ↓
GET
 ↓
JSON response
 ↓
response.json()
 ↓
Python list
 ↓
json.dump()
 ↓
users.json
```

🔥 এটা খুব important real-world pattern।

---

# 2️⃣8️⃣ API JSON → Filter → Save

ধরো আমরা শুধু users-এর name এবং email রাখতে চাই:

```python
simplified_users = []

for user in users:

    simplified_users.append({
        "name": user["name"],
        "email": user["email"]
    })
```

তারপর:

```python
with open(
    "users_simple.json",
    "w",
    encoding="utf-8"
) as file:

    json.dump(
        simplified_users,
        file,
        indent=4
    )
```

Flow:

```text
API JSON
   ↓
Parse
   ↓
Filter
   ↓
Transform
   ↓
Save JSON
```

---

# 2️⃣9️⃣ API Data থেকে Search

```python
search_name = "Leanne Graham"

for user in users:

    if user["name"] == search_name:

        print(
            "Found:",
            user
        )
```

---

# 3️⃣0️⃣ Realistic API Client Function ⭐⭐⭐

একটি reusable function:

```python
import requests


def get_users():

    url = (
        "https://jsonplaceholder.typicode.com"
        "/users"
    )

    try:

        response = requests.get(
            url,
            timeout=10
        )

        response.raise_for_status()

        return response.json()

    except requests.RequestException as e:

        print("API error:", e)
        return []

    except ValueError:

        print("Invalid JSON response!")
        return []
```

Use:

```python
users = get_users()

for user in users:

    print(user["name"])
```

---

# 🧠 Day 9-এর সবচেয়ে গুরুত্বপূর্ণ Concept

```text
json.loads()
```

ব্যবহার করো যখন তোমার কাছে **JSON string** আছে।

```text
response.json()
```

ব্যবহার করো যখন `requests` response থেকে JSON নিতে চাও।

```text
json.load(file)
```

ব্যবহার করো যখন **JSON file** পড়ছো।

```text
json.dumps(data)
```

ব্যবহার করো যখন Python object → **JSON string** করতে চাও।

```text
json.dump(data, file)
```

ব্যবহার করো যখন Python object → **JSON file** করতে চাও।

---

# 📌 4টা Method একসাথে

|Method|কাজ|
|---|---|
|`json.loads()`|JSON string → Python|
|`json.load()`|JSON file → Python|
|`json.dumps()`|Python → JSON string|
|`json.dump()`|Python → JSON file|

আর API-এর জন্য:

```python
response.json()
```

→ API response → Python object

---

# 🧪 Day 9 Practice

### Exercise 1

এই API থেকে users আনো:

```text
https://jsonplaceholder.typicode.com/users
```

সব user's:

```text
ID
Name
Email
```

print করো।

---

### Exercise 2

শুধু যেসব user-এর `address.city` আছে, তাদের city print করো।

---

### Exercise 3 ⭐

API থেকে users নিয়ে:

```text
users.json
```

file-এ save করো।

Formatting:

```python
indent=4
ensure_ascii=False
```

---

### Exercise 4 ⭐⭐

শুধু:

```text
name
email
city
```

নিয়ে নতুন JSON file তৈরি করো:

```text
users_simple.json
```

---

### Exercise 5 ⭐⭐

POST request দিয়ে:

```python
{
    "title": "Python JSON",
    "body": "Learning API",
    "userId": 1
}
```

পাঠাও এবং response print করো।

---

# 🏆 Day 9 Mini Project

## 🌐 API → JSON Data Manager

Program:

```text
=============================
       API DATA MANAGER
=============================

1. Fetch users from API
2. Show users
3. Search user
4. Save users to JSON
5. Create simplified JSON
6. Refresh API data
7. Exit
```

Architecture:

```text
             API
              ↓
         requests.get()
              ↓
       response.json()
              ↓
        Python objects
          ↙       ↘
       Search     Filter
          ↓         ↓
       Output    JSON file
```

এখানে তুমি একসাথে ব্যবহার করবে:

```text
requests
json
dict
list
nested JSON
exception handling
file handling
pathlib
```

---

# 📚 Course Progress

```text
Day 1  → JSON Fundamentals + dumps()       ✅
Day 2  → loads() + JSON → Python           ✅
Day 3  → dump() + JSON File Writing        ✅
Day 4  → load() + JSON File Reading        ✅
Day 5  → Nested JSON + Complex Data        ✅
Day 6  → Formatting + Sorting + Encoding   ✅
Day 7  → Error Handling + Validation       ✅
Day 8  → json + pathlib + Configuration    ✅
Day 9  → JSON + API + requests             ✅
Day 10 → 🔥 Final JSON Database Project    ⏭️
```

**Day 10 হবে final project day — `json` দিয়ে একটি complete mini database/CRUD system বানাবো, যেখানে Create, Read, Update, Delete, Search, Validation, Error Handling, `pathlib` এবং JSON persistence সব একসাথে থাকবে।**

# 🐍 Python `json` Module — Day 10

## 🔥 Final Project: JSON Database / CRUD System

আজ আমাদের `json` module course-এর **final project**।  
আজ পর্যন্ত শেখা সবকিছু একসাথে ব্যবহার করব।

```text
Day 1  → dumps()
Day 2  → loads()
Day 3  → dump()
Day 4  → load()
Day 5  → Nested JSON
Day 6  → Formatting
Day 7  → Error Handling + Validation
Day 8  → pathlib + Configuration
Day 9  → API + requests
Day 10 → 🔥 Complete JSON Database
```

---

# 🎯 আজকের Project

আমরা একটি **Student Management System** বানাবো।

Features:

```text
=============================
     STUDENT MANAGER
=============================

1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Add Skill
7. Delete Skill
8. Save Data
9. Exit
```

Data থাকবে:

```text
data/students.json
```

Configuration থাকবে:

```text
config/config.json
```

---

# 1️⃣ Project Structure

প্রথমে:

```text
student_manager/
│
├── main.py
│
├── config/
│   └── config.json
│
└── data/
    └── students.json
```

`pathlib` দিয়ে directories automatically তৈরি করব।

---

# 2️⃣ JSON Database Structure

`students.json`:

```json
{
    "students": [
        {
            "id": 1,
            "name": "Rahim",
            "age": 22,
            "email": "rahim@example.com",
            "department": "CSE",
            "skills": [
                "Python",
                "Django"
            ]
        }
    ]
}
```

Structure:

```text
database
└── students
    ├── id
    ├── name
    ├── age
    ├── email
    ├── department
    └── skills[]
```

---

# 3️⃣ Imports

```python
import json
from pathlib import Path
```

---

# 4️⃣ Project Paths

```python
BASE_DIR = Path(__file__).resolve().parent

CONFIG_DIR = BASE_DIR / "config"
DATA_DIR = BASE_DIR / "data"

CONFIG_FILE = CONFIG_DIR / "config.json"
STUDENTS_FILE = DATA_DIR / "students.json"
```

Directories:

```python
CONFIG_DIR.mkdir(
    parents=True,
    exist_ok=True
)

DATA_DIR.mkdir(
    parents=True,
    exist_ok=True
)
```

---

# 5️⃣ Default Configuration

```python
DEFAULT_CONFIG = {
    "app": {
        "name": "Student Manager",
        "version": "1.0.0"
    },
    "student": {
        "max_students": 100
    }
}
```

---

# 6️⃣ Default Database

```python
DEFAULT_DATA = {
    "students": []
}
```

---

# 7️⃣ JSON Load Function ⭐⭐⭐

```python
def load_json(path, default):

    try:

        with path.open(
            "r",
            encoding="utf-8"
        ) as file:

            return json.load(file)

    except FileNotFoundError:

        save_json(path, default)

        return default

    except json.JSONDecodeError:

        print(
            f"Invalid JSON: {path}"
        )

        return default
```

এখানে আমাদের Day 7-এর error handling ব্যবহার হয়েছে।

---

# 8️⃣ JSON Save Function

```python
def save_json(path, data):

    with path.open(
        "w",
        encoding="utf-8"
    ) as file:

        json.dump(
            data,
            file,
            indent=4,
            ensure_ascii=False
        )
```

---

# 9️⃣ Load Configuration

```python
config = load_json(
    CONFIG_FILE,
    DEFAULT_CONFIG
)
```

---

# 🔟 Load Students

```python
database = load_json(
    STUDENTS_FILE,
    DEFAULT_DATA
)

students = database["students"]
```

এখন:

```text
students
```

এর মধ্যে সব student থাকবে।

---

# 1️⃣1️⃣ Generate Student ID

আমাদের ID unique হতে হবে।

```python
def generate_id(students):

    if not students:
        return 1

    return max(
        student["id"]
        for student in students
    ) + 1
```

যদি:

```text
1
2
3
```

থাকে, next ID:

```text
4
```

---

# 1️⃣2️⃣ Add Student ⭐⭐⭐

```python
def add_student(students):

    name = input(
        "Enter name: "
    ).strip()

    age = input(
        "Enter age: "
    ).strip()

    email = input(
        "Enter email: "
    ).strip()

    department = input(
        "Enter department: "
    ).strip()

    if not name:
        print("Name is required!")
        return

    if not age.isdigit():
        print("Age must be a number!")
        return

    student = {
        "id": generate_id(students),
        "name": name,
        "age": int(age),
        "email": email,
        "department": department,
        "skills": []
    }

    students.append(student)

    print("Student added successfully!")
```

---

# 1️⃣3️⃣ View Students

```python
def view_students(students):

    if not students:

        print("No students found.")
        return

    for student in students:

        print("\n------------------")

        print(
            "ID:",
            student["id"]
        )

        print(
            "Name:",
            student["name"]
        )

        print(
            "Age:",
            student["age"]
        )

        print(
            "Email:",
            student["email"]
        )

        print(
            "Department:",
            student["department"]
        )

        print(
            "Skills:",
            ", ".join(student["skills"])
        )
```

---

# 1️⃣4️⃣ Search Student ⭐⭐⭐

ID দিয়ে:

```python
def find_student(students, student_id):

    for student in students:

        if student["id"] == student_id:
            return student

    return None
```

তারপর:

```python
def search_student(students):

    value = input(
        "Enter student ID: "
    ).strip()

    if not value.isdigit():

        print("Invalid ID!")
        return

    student = find_student(
        students,
        int(value)
    )

    if student:

        print(
            "Name:",
            student["name"]
        )

        print(
            "Email:",
            student["email"]
        )

        print(
            "Skills:",
            ", ".join(student["skills"])
        )

    else:

        print("Student not found!")
```

---

# 1️⃣5️⃣ Update Student

```python
def update_student(students):

    value = input(
        "Enter student ID: "
    ).strip()

    if not value.isdigit():
        print("Invalid ID!")
        return

    student = find_student(
        students,
        int(value)
    )

    if not student:

        print("Student not found!")
        return

    name = input(
        f"Name [{student['name']}]: "
    ).strip()

    email = input(
        f"Email [{student['email']}]: "
    ).strip()

    if name:
        student["name"] = name

    if email:
        student["email"] = email

    print("Student updated!")
```

---

# 1️⃣6️⃣ Delete Student

```python
def delete_student(students):

    value = input(
        "Enter student ID: "
    ).strip()

    if not value.isdigit():

        print("Invalid ID!")
        return

    student_id = int(value)

    student = find_student(
        students,
        student_id
    )

    if not student:

        print("Student not found!")
        return

    students.remove(student)

    print("Student deleted!")
```

---

# 1️⃣7️⃣ Add Skill ⭐⭐⭐

```python
def add_skill(students):

    value = input(
        "Enter student ID: "
    ).strip()

    if not value.isdigit():

        print("Invalid ID!")
        return

    student = find_student(
        students,
        int(value)
    )

    if not student:

        print("Student not found!")
        return

    skill = input(
        "Enter skill: "
    ).strip()

    if not skill:

        print("Skill cannot be empty!")
        return

    if skill in student["skills"]:

        print("Skill already exists!")
        return

    student["skills"].append(skill)

    print("Skill added!")
```

---

# 1️⃣8️⃣ Delete Skill

```python
def delete_skill(students):

    value = input(
        "Enter student ID: "
    ).strip()

    if not value.isdigit():
        print("Invalid ID!")
        return

    student = find_student(
        students,
        int(value)
    )

    if not student:

        print("Student not found!")
        return

    if not student["skills"]:

        print("No skills found!")
        return

    print(
        "Skills:",
        ", ".join(student["skills"])
    )

    skill = input(
        "Enter skill to delete: "
    ).strip()

    if skill in student["skills"]:

        student["skills"].remove(skill)

        print("Skill deleted!")

    else:

        print("Skill not found!")
```

---

# 1️⃣9️⃣ Save Students

```python
def save_students(students):

    data = {
        "students": students
    }

    save_json(
        STUDENTS_FILE,
        data
    )

    print("Data saved successfully!")
```

---

# 2️⃣0️⃣ Menu

```python
def show_menu():

    print("""
=============================
      STUDENT MANAGER
=============================

1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Add Skill
7. Delete Skill
8. Save Data
9. Exit

=============================
""")
```

---

# 2️⃣1️⃣ Main Loop 🔥

সব function এখন connect করব।

```python
while True:

    show_menu()

    choice = input(
        "Enter choice: "
    ).strip()

    if choice == "1":

        add_student(students)

    elif choice == "2":

        view_students(students)

    elif choice == "3":

        search_student(students)

    elif choice == "4":

        update_student(students)

    elif choice == "5":

        delete_student(students)

    elif choice == "6":

        add_skill(students)

    elif choice == "7":

        delete_skill(students)

    elif choice == "8":

        save_students(students)

    elif choice == "0":

        save_students(students)

        print(
            "Goodbye!"
        )

        break

    else:

        print(
            "Invalid choice!"
        )
```

---

# 2️⃣2️⃣ Complete Architecture

আমাদের program এখন:

```text
                    main.py
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   Configuration    Students       Functions
        │              │              │
        ↓              ↓              ↓
   config.json    students.json     CRUD
                                      │
                         ┌────────────┼────────────┐
                         ↓            ↓            ↓
                       Create       Update       Delete
                         ↓            ↓            ↓
                       Search       Skills       Save
```

---

# 2️⃣3️⃣ এখানে `json` কোথায় কোথায় ব্যবহার হয়েছে?

```text
json.load()
     ↓
JSON file → Python

json.dump()
     ↓
Python → JSON file
```

আর:

```text
json.JSONDecodeError
     ↓
Invalid JSON handling
```

---

# 2️⃣4️⃣ `pathlib` কোথায় ব্যবহার হয়েছে?

```python
BASE_DIR = Path(__file__).resolve().parent
```

```python
CONFIG_DIR = BASE_DIR / "config"
```

```python
DATA_DIR = BASE_DIR / "data"
```

```python
CONFIG_FILE.open(...)
```

এতে hard-coded OS-specific paths লেখার প্রয়োজন কমে।

---

# 2️⃣5️⃣ আমাদের CRUD কী?

|Operation|Function|
|---|---|
|Create|`add_student()`|
|Read|`view_students()`|
|Search|`search_student()`|
|Update|`update_student()`|
|Delete|`delete_student()`|

এটাই **CRUD**:

```text
C → Create
R → Read
U → Update
D → Delete
```

---

# 2️⃣6️⃣ Example Run

```text
=============================
      STUDENT MANAGER
=============================

1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Add Skill
7. Delete Skill
8. Save Data
9. Exit

Enter choice: 1

Enter name: Atiar
Enter age: 22
Enter email: atiar@example.com
Enter department: CSE

Student added successfully!
```

তারপর:

```text
Enter choice: 6

Enter student ID: 1
Enter skill: Python

Skill added!
```

`students.json`:

```json
{
    "students": [
        {
            "id": 1,
            "name": "Atiар",
            "age": 22,
            "email": "atiar@example.com",
            "department": "CSE",
            "skills": [
                "Python"
            ]
        }
    ]
}
```

---

# 2️⃣7️⃣ আজকের সবচেয়ে গুরুত্বপূর্ণ Learning

এই project শেষ করার পর তুমি শুধু `json` syntax জানবে না—তুমি বুঝবে:

```text
JSON
 ↓
File Storage
 ↓
Python Data Structures
 ↓
Validation
 ↓
CRUD
 ↓
Persistence
 ↓
Configuration
```

এটাই `json` module-এর practical foundation।

---

# 🧠 Final `json` Cheat Sheet

```python
import json
```

### Python → JSON string

```python
json.dumps(data)
```

### JSON string → Python

```python
json.loads(text)
```

### Python → JSON file

```python
json.dump(data, file)
```

### JSON file → Python

```python
json.load(file)
```

### Pretty JSON

```python
json.dumps(data, indent=4)
```

### Unicode

```python
json.dumps(
    data,
    ensure_ascii=False
)
```

### Sorted

```python
json.dumps(
    data,
    sort_keys=True
)
```

### Error

```python
except json.JSONDecodeError:
```

---

# 🏆 JSON Course Complete

```text
             Python json
                  │
     ┌────────────┼────────────┐
     ↓            ↓            ↓
 Serialization  Files         APIs
     │            │            │
 dumps/dump    load/save    requests
     │            │            │
     └────────────┼────────────┘
                  ↓
               CRUD
                  ↓
           Real Application
```

### এখন তোমার `json` module শেখার পরের ধাপ

তোমার জন্য সবচেয়ে logical sequence হবে:

```text
json                 ✅
   ↓
requests              ← API
   ↓
os                    ✅
   ↓
pathlib               ✅
   ↓
datetime
   ↓
re (Regular Expression)
   ↓
csv
   ↓
logging
   ↓
sqlite3
   ↓
argparse
```

বিশেষ করে **`json + pathlib + os + requests`** ভালোভাবে জানা তোমার Python automation/backend কাজের জন্য খুব useful foundation।


