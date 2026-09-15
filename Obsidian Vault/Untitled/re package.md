অবশ্যই। এবার আমরা Python-এর **`re` (Regular Expression) module** নিয়ে `datetime`-এর মতোই **complete course** করব—প্রথমে roadmap, তারপর তুমি `day1`, `day2` লিখলে সেই দিনের lesson দেব।

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

# 🐍 Python `re` Module — Complete Course

## 🎯 `re` module কী?

`re` = **Regular Expression**

এটা ব্যবহার করে text-এর মধ্যে নির্দিষ্ট **pattern খোঁজা, যাচাই করা, বের করা, পরিবর্তন করা এবং split করা** যায়।

উদাহরণ:

```python
import re

text = "My phone number is 01712345678"

result = re.search(r"\d+", text)

print(result.group())
```

Output:

```text
01712345678
```

---

# 📚 15-Day Complete Roadmap

|Day|Topic|কী শিখবে|
|---|---|---|
|Day 1|Regex Fundamentals|`re`, pattern, raw string|
|Day 2|Character Classes|`\d`, `\w`, `\s`, `[]`|
|Day 3|Quantifiers|`*`, `+`, `?`, `{}`|
|Day 4|Anchors|`^`, `$`, `\b`|
|Day 5|`re.search()`|Pattern search|
|Day 6|`re.match()`|String-এর শুরুতে matching|
|Day 7|`re.fullmatch()`|পুরো string validation|
|Day 8|`re.findall()`|সব matches বের করা|
|Day 9|`re.finditer()`|Match object নিয়ে কাজ|
|Day 10|`re.sub()`|Text replace|
|Day 11|`re.split()`|Pattern দিয়ে split|
|Day 12|Groups|`()`, capturing groups|
|Day 13|Advanced Regex|named groups, flags, lookaround|
|Day 14|Real-world Validation|Email, phone, URL, password, log parsing|
|Day 15|🔥 Final Project|Text Analyzer / Data Extractor|

---

# Day 1–5: Foundation

### Day 1 — Regex Fundamentals

শিখবে:

```python
import re
```

Raw string:

```python
r"\d+"
```

Pattern কী?

```text
text
 ↓
pattern
 ↓
regex engine
 ↓
match
```

---

### Day 2 — Character Classes

শিখবে:

```text
\d    digit
\D    non-digit

\w    word character
\W    non-word

\s    whitespace
\S    non-whitespace
```

এবং:

```python
[abc]
[a-z]
[A-Z]
[0-9]
[^0-9]
```

---

### Day 3 — Quantifiers

```text
*       0 or more
+       1 or more
?       0 or 1
{3}     exactly 3
{2,5}   2 to 5
{2,}    2 or more
```

Example:

```python
r"\d{11}"
```

১১ digit match করবে।

---

### Day 4 — Anchors

```text
^       beginning
$       end
\b      word boundary
\B      non-word boundary
```

Example:

```python
r"^Hello"
```

String অবশ্যই `Hello` দিয়ে শুরু হতে হবে।

---

### Day 5 — `re.search()`

```python
re.search(pattern, string)
```

Example:

```python
import re

text = "Python is powerful"

result = re.search(
    r"Python",
    text
)

if result:
    print("Found")
```

---

# Day 6–11: Core `re` Functions

## Day 6 — `re.match()`

```python
re.match(pattern, string)
```

এটা string-এর **শুরু থেকে** match করে।

---

## Day 7 — `re.fullmatch()`

পুরো string match করতে:

```python
re.fullmatch(
    r"\d{11}",
    "01712345678"
)
```

Validation-এর জন্য খুব useful।

---

## Day 8 — `re.findall()`

সব matching value:

```python
numbers = re.findall(
    r"\d+",
    "I have 10 apples and 20 oranges"
)

print(numbers)
```

Output:

```text
['10', '20']
```

---

## Day 9 — `re.finditer()`

প্রতিটি match-এর position এবং information:

```python
matches = re.finditer(
    r"\d+",
    text
)

for match in matches:
    print(match.group())
    print(match.start())
    print(match.end())
```

---

## Day 10 — `re.sub()`

Text replace:

```python
text = "I like Java"

result = re.sub(
    r"Java",
    "Python",
    text
)

print(result)
```

Output:

```text
I like Python
```

---

## Day 11 — `re.split()`

```python
text = "apple,banana;orange mango"

result = re.split(
    r"[,; ]",
    text
)

print(result)
```

এখানে comma, semicolon এবং space দিয়ে split হবে।

---

# Day 12–13: Advanced Regex

## Day 12 — Groups

```python
pattern = r"(\d{4})-(\d{2})-(\d{2})"
```

Text:

```text
2026-08-17
```

Groups:

```text
Group 1 → 2026
Group 2 → 08
Group 3 → 17
```

Python:

```python
match = re.search(
    pattern,
    "2026-08-17"
)

print(match.group(1))
print(match.group(2))
print(match.group(3))
```

---

## Day 13 — Advanced Features

শিখবে:

### Named groups

```python
r"(?P<year>\d{4})"
```

### Non-capturing group

```python
r"(?:abc)"
```

### Flags

```python
re.IGNORECASE
re.MULTILINE
re.DOTALL
```

### Lookahead

```python
(?=...)
```

### Negative lookahead

```python
(?!...)
```

### Lookbehind

```python
(?<=...)
```

### Negative lookbehind

```python
(?<!...)
```

---

# Day 14 — Real-world Applications

এখানে আমরা Regex দিয়ে বাস্তব কাজ করব।

### 📧 Email extraction

```python
pattern = r"[\w.-]+@[\w.-]+\.\w+"
```

---

### 📱 Phone extraction

বাংলাদেশি example:

```python
pattern = r"01\d{9}"
```

---

### 🌐 URL extraction

```python
pattern = r"https?://\S+"
```

---

### 🔢 Number extraction

```python
pattern = r"\d+"
```

---

### 📝 Hashtag extraction

```python
pattern = r"#\w+"
```

---

### 👤 Username

```python
pattern = r"@\w+"
```

---

### 📅 Date extraction

```python
pattern = r"\d{4}-\d{2}-\d{2}"
```

---

### 📋 Log parsing

Example:

```text
2026-08-17 10:30:15 ERROR Database connection failed
```

Regex দিয়ে বের করব:

```text
date
time
level
message
```

---

# Day 15 — 🔥 Final Project

আমরা বানাব:

# 📊 Text Analyzer & Data Extractor

Input:

```text
Hello, my email is user@example.com.
My phone is 01712345678.
Visit https://example.com
Date: 2026-08-17
#python #programming
```

Program automatically বের করবে:

```text
================================
       TEXT ANALYZER
================================

Emails:
user@example.com

Phone Numbers:
01712345678

URLs:
https://example.com

Dates:
2026-08-17

Hashtags:
#python
#programming

Numbers:
01712345678
2026
08
17
```

---

# 🧠 `re` Module-এর সবচেয়ে গুরুত্বপূর্ণ Functions

এগুলো অবশ্যই ভালোভাবে শিখবে:

```python
re.search()
re.match()
re.fullmatch()
re.findall()
re.finditer()
re.sub()
re.split()
re.compile()
```

---

# ⭐ Match Object

`re.search()` ইত্যাদি থেকে Match object পাওয়া যায়।

Important methods:

```python
match.group()
match.start()
match.end()
match.span()
match.groups()
```

Example:

```python
import re

text = "Python 123"

match = re.search(
    r"\d+",
    text
)

print(match.group())
print(match.start())
print(match.end())
print(match.span())
```

---

# 🔥 `re.compile()`

একই pattern বারবার ব্যবহার করলে:

```python
pattern = re.compile(
    r"\d+"
)

print(pattern.findall("10 20 30"))
print(pattern.findall("40 50"))
```

এটা reusable pattern তৈরি করে।

---

# 📌 Regex Learning Order

Regex শেখার সময় এই order maintain করো:

```text
Characters
   ↓
Character Classes
   ↓
Quantifiers
   ↓
Anchors
   ↓
search()
   ↓
match()
   ↓
fullmatch()
   ↓
findall()
   ↓
finditer()
   ↓
sub()
   ↓
split()
   ↓
Groups
   ↓
Flags
   ↓
Lookaround
   ↓
Real-world Regex
   ↓
Final Project
```

---

# ⚠️ একটি গুরুত্বপূর্ণ বিষয়

Regex দিয়ে **সব validation করার চেষ্টা করবে না**।

যেমন email-এর জন্য complex regex লিখে ফেললেও email validation-এর সব বাস্তব নিয়ম ধরা কঠিন। Regex সাধারণত **pattern matching/extraction**-এর জন্য সবচেয়ে useful।

তোমার Python backend শেখার ক্ষেত্রে `re` বিশেষভাবে কাজে লাগবে:

```text
Django/DRF
   ↓
Input validation
   ↓
re

Log processing
   ↓
re

Web scraping / text extraction
   ↓
re

Data cleaning
   ↓
re

Security-related input filtering
   ↓
re
```

**Course শুরু: Day 1 → Regex Fundamentals।**

# 🐍 Python `re` Module — Day 2

## 🎯 Character Classes

আজ আমরা Regex-এর সবচেয়ে গুরুত্বপূর্ণ foundation-এর একটি শিখব: **Character Classes**।

Official docs: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ Character Class কী?

Character class দিয়ে আমরা বলি:

> **কোন ধরনের character খুঁজতে চাই?**

যেমন:

```python
\d
```

মানে **digit** খুঁজবে।

```python
import re

text = "My age is 25"

result = re.findall(r"\d", text)

print(result)
```

Output:

```text
['2', '5']
```

---

# 2️⃣ `\d` — Digit

```python
\d
```

মানে digit।

Example:

```python
text = "Python 3.12"

print(re.findall(r"\d", text))
```

Output:

```text
['3', '1', '2']
```

### একসাথে পুরো number চাইলে

```python
print(re.findall(r"\d+", text))
```

Output:

```text
['3', '12']
```

এখানে:

```text
\d  → একটি digit
+   → এক বা একাধিক
```

---

# 3️⃣ `\D` — Non-Digit

`\d`-এর বিপরীত:

```python
\D
```

মানে digit ছাড়া অন্য character।

```python
text = "abc123"

print(re.findall(r"\D", text))
```

Output:

```text
['a', 'b', 'c']
```

---

# 4️⃣ `\w` — Word Character ⭐

```python
\w
```

সাধারণভাবে letters, digits এবং underscore-এর মতো word characters match করে।

```python
text = "Python_123"

print(re.findall(r"\w", text))
```

Output:

```text
['P', 'y', 't', 'h', 'o', 'n', '_', '1', '2', '3']
```

---

# 5️⃣ `\W` — Non-Word

`\w`-এর বিপরীত:

```python
\W
```

Example:

```python
text = "Hello, World!"

print(re.findall(r"\W", text))
```

Output concept:

```text
[',', ' ', '!']
```

---

# 6️⃣ `\s` — Whitespace

```python
\s
```

space, tab, newline-এর মতো whitespace match করে।

```python
text = "Hello World"

print(re.findall(r"\s", text))
```

Output:

```text
[' ']
```

---

# 7️⃣ `\S` — Non-Whitespace

```python
\S
```

মানে whitespace ছাড়া character।

```python
text = "Hi Bob"

print(re.findall(r"\S", text))
```

Output:

```text
['H', 'i', 'B', 'o', 'b']
```

---

# 8️⃣ Character Class `[]` ⭐⭐⭐

নিজের মতো character set তৈরি করতে পারো।

```python
[abc]
```

মানে:

> `a`, `b`, অথবা `c` — যেকোনো একটি।

Example:

```python
text = "apple banana cat"

print(re.findall(r"[abc]", text))
```

Output concept:

```text
['a', 'a', 'b', 'a', 'a', 'c']
```

---

# 9️⃣ `[a-z]`

একটি lowercase letter:

```python
[a-z]
```

Example:

```python
text = "Hello123"

print(re.findall(r"[a-z]", text))
```

Output:

```text
['e', 'l', 'l', 'o']
```

---

# 🔟 `[A-Z]`

Uppercase letter:

```python
text = "Hello PYTHON"

print(re.findall(r"[A-Z]", text))
```

Output:

```text
['H', 'P', 'Y', 'T', 'H', 'O', 'N']
```

---

# 1️⃣1️⃣ `[0-9]`

Digit-এর character-class version:

```python
[0-9]
```

Example:

```python
text = "abc123"

print(re.findall(r"[0-9]", text))
```

Output:

```text
['1', '2', '3']
```

তাই:

```text
\d
```

এবং:

```text
[0-9]
```

অনেক basic ক্ষেত্রে একই উদ্দেশ্যে ব্যবহার করা যায়।

---

# 1️⃣2️⃣ Multiple Character Range

একসাথে:

```python
[a-zA-Z]
```

মানে:

```text
a-z
+
A-Z
```

Example:

```python
text = "Hello PYTHON 123"

print(
    re.findall(r"[a-zA-Z]", text)
)
```

Output:

```text
['H', 'e', 'l', 'l', 'o',
 'P', 'Y', 'T', 'H', 'O', 'N']
```

---

# 1️⃣3️⃣ Letters + Numbers

```python
[a-zA-Z0-9]
```

মানে:

```text
lowercase
+
uppercase
+
digit
```

Example:

```python
text = "User123!"

print(
    re.findall(r"[a-zA-Z0-9]", text)
)
```

`!` match হবে না।

---

# 1️⃣4️⃣ Negated Character Class `[^...]`

এটা খুব গুরুত্বপূর্ণ।

```python
[^0-9]
```

মানে:

> digit ছাড়া যেকোনো character।

Example:

```python
text = "abc123"

print(
    re.findall(r"[^0-9]", text)
)
```

Output:

```text
['a', 'b', 'c']
```

---

# 1️⃣5️⃣ `[^a-z]`

Lowercase letter ছাড়া সব:

```python
text = "abcXYZ123"

print(
    re.findall(r"[^a-z]", text)
)
```

Output concept:

```text
['X', 'Y', 'Z', '1', '2', '3']
```

---

# 1️⃣6️⃣ Character Class-এর ভিতরে `-`

```python
[a-z]
```

এখানে `-` range বোঝায়।

```text
a-z
```

মানে:

```text
a b c d ... z
```

একইভাবে:

```python
[0-9]
```

মানে:

```text
0 1 2 3 ... 9
```

---

# 1️⃣7️⃣ Character Class-এর ভিতরে `^`

যদি শুরুতে থাকে:

```python
[^0-9]
```

তাহলে NOT বোঝায়।

কিন্তু:

```python
[0-9^]
```

এখানে `^` সাধারণ character হিসেবে নেওয়া হয়।

তাই position গুরুত্বপূর্ণ।

---

# 1️⃣8️⃣ Character Class-এর ভিতরে `.`

```python
[.]
```

এখানে `.` literal dot।

Example:

```python
text = "hello.world"

print(
    re.findall(r"[.]", text)
)
```

Output:

```text
['.']
```

---

# 1️⃣9️⃣ `.` বনাম `[.]`

Regex-এ:

```python
.
```

একটি special character।

সাধারণভাবে এটি newline ছাড়া যেকোনো single character match করে।

কিন্তু:

```python
[.]
```

শুধু actual dot match করে।

এটা খুব গুরুত্বপূর্ণ পার্থক্য।

---

# 2️⃣0️⃣ `\d` বনাম `[0-9]`

```text
\d
```

digit character class-এর shorthand।

আর:

```text
[0-9]
```

explicit range।

Basic English/ASCII-style numeric matching-এ দুটো প্রায়ই একই কাজের জন্য ব্যবহার হয়।

---

# 2️⃣1️⃣ `\w` বনাম `[a-zA-Z0-9_]`

এগুলো সব ক্ষেত্রে একদম identical ধরে নিও না।

Python-এর default Unicode behavior-এর কারণে `\w` আরও বিস্তৃত হতে পারে।

তাই:

```python
\w
```

কে শুধু:

```text
[a-zA-Z0-9_]
```

হিসেবে মুখস্থ না করাই ভালো।

---

# 2️⃣2️⃣ Practical Example — Username

ধরো username শুধু letters, numbers এবং underscore হতে পারবে:

```python
pattern = r"^[a-zA-Z0-9_]+$"
```

Example:

```python
username = "atiar_123"

if re.fullmatch(
    r"[a-zA-Z0-9_]+",
    username
):
    print("Valid")
else:
    print("Invalid")
```

---

# 2️⃣3️⃣ Practical Example — Only Numbers

```python
value = "123456"

if re.fullmatch(r"[0-9]+", value):
    print("Only numbers")
```

আরও সহজ:

```python
if re.fullmatch(r"\d+", value):
    print("Only numbers")
```

---

# 2️⃣4️⃣ Practical Example — Alphanumeric

```python
value = "Python123"

if re.fullmatch(
    r"[a-zA-Z0-9]+",
    value
):
    print("Valid")
```

---

# 2️⃣5️⃣ Practical Example — Remove Special Characters

```python
text = "Hello@World!123"

result = re.sub(
    r"[^a-zA-Z0-9 ]",
    "",
    text
)

print(result)
```

Output:

```text
HelloWorld123
```

এখানে:

```text
[^a-zA-Z0-9 ]
```

মানে:

> letters, numbers এবং space ছাড়া অন্য character।

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Cheat Sheet

|Pattern|Meaning|
|---|---|
|`\d`|digit|
|`\D`|non-digit|
|`\w`|word character|
|`\W`|non-word|
|`\s`|whitespace|
|`\S`|non-whitespace|
|`[abc]`|a/b/c-এর যেকোনো একটি|
|`[a-z]`|lowercase letters|
|`[A-Z]`|uppercase letters|
|`[0-9]`|digits|
|`[a-zA-Z]`|letters|
|`[a-zA-Z0-9]`|letters + digits|
|`[^0-9]`|non-digit|
|`[^a-z]`|non-lowercase|

---

# 🧪 Day 2 Practice

## Exercise 1

এই text থেকে সব digit বের করো:

```python
text = "I have 25 apples and 10 oranges."
```

Expected:

```text
['2', '5', '1', '0']
```

---

## Exercise 2

সব complete numbers বের করো:

```python
text = "I have 25 apples and 10 oranges."
```

Hint:

```python
r"\d+"
```

Expected:

```text
['25', '10']
```

---

## Exercise 3

শুধু uppercase letters বের করো:

```python
text = "Python Is AWESOME"
```

---

## Exercise 4

শুধু lowercase letters বের করো।

---

## Exercise 5

শুধু special characters বের করো:

```python
text = "Hello@Python#2026!"
```

---

## Exercise 6 ⭐

এই username valid কিনা check করো:

```text
atiar_123
```

Allowed:

```text
a-z
A-Z
0-9
_
```

---

## Exercise 7 ⭐⭐

এই text থেকে শুধু letters বের করো:

```python
text = "Python3.12 is Awesome!"
```

Expected concept:

```text
Python
is
Awesome
```

---

## Exercise 8 🔥

একটি string থেকে **letters + numbers রেখে**, সব special character remove করো।

Input:

```text
"Py@th#on!123"
```

Expected:

```text
"Python123"
```

Hint:

```python
re.sub()
```

এবং:

```python
[^a-zA-Z0-9]
```

---

# 🎯 আজকের মূল বিষয়

আজ তোমার ৬টি shorthand ভালোভাবে বুঝতে হবে:

```text
\d
\D
\w
\W
\s
\S
```

এবং character class:

```text
[...]
[^...]
[a-z]
[A-Z]
[0-9]
```

**Day 3-এ আমরা এগুলোর সঙ্গে `*`, `+`, `?`, `{n}`, `{n,m}` যোগ করব—এটাই Regex-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি: Quantifiers।**


# 🐍 Python `re` Module — Day 3

## 🎯 Quantifiers

আজ আমরা শিখব **Quantifier**। Regex-এ quantifier দিয়ে বলা হয়:

> **একটি pattern কতবার repeat হতে পারবে।**

আজকের সবচেয়ে গুরুত্বপূর্ণ symbols:

```text
*       0 বা তার বেশি
+       1 বা তার বেশি
?       0 বা 1
{n}     ঠিক n বার
{n,m}   n থেকে m বার
{n,}    কমপক্ষে n বার
```

---

# 1️⃣ `*` — Zero or More

```python
*
```

মানে:

> আগের character/pattern **0 বা তার বেশি বার** থাকতে পারে।

Example:

```python
import re

text = "ab aab aaab"

print(re.findall(r"a*", text))
```

এখানে `a` যতবার আছে, তার group match হতে পারে।

সহজভাবে:

```text
a* 
```

match করতে পারে:

```text
""
"a"
"aa"
"aaa"
"aaaa"
...
```

অর্থাৎ **zero or more**।

---

# 2️⃣ `+` — One or More ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

```python
+
```

মানে:

> আগের pattern **কমপক্ষে ১ বার** থাকতে হবে।

Example:

```python
text = "I have 25 apples and 10 oranges."

numbers = re.findall(
    r"\d+",
    text
)

print(numbers)
```

Output:

```text
['25', '10']
```

কারণ:

```text
\d
```

একটি digit।

আর:

```text
\d+
```

এক বা একাধিক digit।

তাই:

```text
2
25
123
2026
01712345678
```

সব match করতে পারে।

---

# 3️⃣ `\d` বনাম `\d+`

এটা খুব ভালোভাবে বুঝো।

### `\d`

```python
re.findall(r"\d", "12345")
```

Output:

```text
['1', '2', '3', '4', '5']
```

### `\d+`

```python
re.findall(r"\d+", "12345")
```

Output:

```text
['12345']
```

অর্থাৎ:

```text
\d
 ↓
একটি digit

\d+
 ↓
এক বা একাধিক digit-এর sequence
```

---

# 4️⃣ `?` — Zero or One

```python
?
```

মানে:

> আগের pattern **0 অথবা 1 বার** থাকতে পারে।

Example:

```python
text = "color colour"

print(
    re.findall(r"colou?r", text)
)
```

Output:

```text
['color', 'colour']
```

কারণ:

```text
colo
  u?
r
```

এখানে `u` optional।

তাই:

```text
color
colour
```

দুটোই match করে।

---

# 5️⃣ `{n}` — Exactly n Times

ধরো:

```python
\d{4}
```

মানে:

> ঠিক **৪টি digit**।

Example:

```python
text = "Year 2026 and 123"

print(
    re.findall(r"\d{4}", text)
)
```

Output:

```text
['2026']
```

কারণ:

```text
2026 → 4 digits
123  → 3 digits
```

---

# 6️⃣ `{n,m}` — n থেকে m Times

```python
\d{2,4}
```

মানে:

> minimum 2, maximum 4 digits।

Example:

```python
text = "1 12 123 1234 12345"

print(
    re.findall(r"\d{2,4}", text)
)
```

এখানে 2–4 digit-এর sequences match হবে।

---

# 7️⃣ `{n,}` — Minimum n Times

```python
\d{3,}
```

মানে:

> কমপক্ষে ৩টি digit।

তাই:

```text
12       ❌
123      ✅
1234     ✅
12345    ✅
123456   ✅
```

---

# 8️⃣ Quantifier Cheat Sheet

|Pattern|Meaning|
|---|---|
|`a*`|0 বা বেশি `a`|
|`a+`|1 বা বেশি `a`|
|`a?`|0 বা 1 `a`|
|`a{3}`|ঠিক 3টি `a`|
|`a{2,5}`|2–5টি `a`|
|`a{3,}`|কমপক্ষে 3টি `a`|

---

# 9️⃣ Real Example — Phone Number

বাংলাদেশি mobile number-এর basic pattern:

```python
r"01\d{9}"
```

ভেঙে দেখি:

```text
01
 ↓
শুরুতে 01

\d{9}
 ↓
আরও 9 digit
```

Total:

```text
01 + 9 digits = 11 digits
```

Example:

```python
import re

phone = "01712345678"

if re.fullmatch(r"01\d{9}", phone):
    print("Valid format")
else:
    print("Invalid format")
```

---

# 🔟 Real Example — PIN

৪ digit PIN:

```python
pattern = r"\d{4}"
```

Example:

```python
pin = "1234"

if re.fullmatch(r"\d{4}", pin):
    print("Valid PIN format")
```

---

# 1️⃣1️⃣ 6 Digit OTP

```python
otp = "483921"

if re.fullmatch(r"\d{6}", otp):
    print("Valid OTP format")
```

এখানে:

```text
\d{6}
```

মানে exactly 6 digits।

---

# 1️⃣2️⃣ Username Length

ধরো username 5 থেকে 12 characters:

```python
r"\w{5,12}"
```

Example:

```python
username = "atiar123"

if re.fullmatch(r"\w{5,12}", username):
    print("Valid")
```

⚠️ তবে `\w` ব্যবহার করলে Unicode word characters-এর behavior-ও বিবেচনা করতে হয়। শুধু ASCII username চাইলে explicit character class ব্যবহার করা ভালো:

```python
r"[A-Za-z0-9_]{5,12}"
```

---

# 1️⃣3️⃣ Password-এর Basic Pattern

ধরো password:

- minimum 8 characters
    
- maximum 20 characters
    

Basic length:

```python
r".{8,20}"
```

কিন্তু এটা **strong password validation নয়**।

কারণ এখানে শুধু length check হচ্ছে।

Advanced password validation আমরা পরে **lookahead** শেখার সময় করব।

---

# 1️⃣4️⃣ Quantifier Group-এর সাথে

Quantifier শুধু single character-এর জন্য না।

Group-এর সাথেও ব্যবহার করা যায়।

```python
(ab)+
```

মানে:

```text
ab
abab
ababab
abababab
```

Example:

```python
text = "ab abab ababab"

print(
    re.findall(r"(?:ab)+", text)
)
```

---

# 1️⃣5️⃣ Character Class + Quantifier ⭐⭐⭐

এগুলো একসাথে সবচেয়ে বেশি ব্যবহার করবে।

```python
[A-Z]+
```

মানে:

> এক বা একাধিক uppercase letter।

Example:

```python
text = "Hello PYTHON WORLD"

print(
    re.findall(r"[A-Z]+", text)
)
```

Output:

```text
['H', 'PYTHON', 'WORLD']
```

---

# 1️⃣6️⃣ Lowercase Words

```python
[a-z]+
```

Example:

```python
text = "hello world Python"

print(
    re.findall(r"[a-z]+", text)
)
```

---

# 1️⃣7️⃣ Alphanumeric Sequence

```python
[A-Za-z0-9]+
```

মানে:

> এক বা একাধিক letter অথবা digit।

Example:

```python
text = "Python123 @ hello456"

print(
    re.findall(
        r"[A-Za-z0-9]+",
        text
    )
)
```

Output concept:

```text
['Python123', 'hello456']
```

---

# 1️⃣8️⃣ Space সহ Text

```python
\s+
```

মানে:

> এক বা একাধিক whitespace।

Example:

```python
text = "Hello    World"

result = re.sub(
    r"\s+",
    " ",
    text
)

print(result)
```

Output:

```text
Hello World
```

🔥 এটা real-world text cleaning-এ খুব useful।

---

# 1️⃣9️⃣ `*` বনাম `+` ⭐⭐⭐

সবচেয়ে গুরুত্বপূর্ণ difference:

### `*`

```text
zero or more
```

### `+`

```text
one or more
```

Example:

```python
re.findall(r"a*", "bbb")
```

`a*` empty match-ও করতে পারে।

কিন্তু:

```python
re.findall(r"a+", "bbb")
```

কোনো `a` নেই, তাই meaningful `a+` match পাওয়া যাবে না।

**Rule:**

```text
* → optional repetition, zero allowed
+ → at least one required
```

---

# 2️⃣0️⃣ `?` বনাম `*`

```text
? → 0 or 1
* → 0 or many
```

Example:

```text
a?
```

match:

```text
""
"a"
```

কিন্তু:

```text
a*
```

match:

```text
""
"a"
"aa"
"aaa"
...
```

---

# 2️⃣1️⃣ `{2,4}` বনাম `{4}`

```text
{4}
```

শুধু:

```text
1234
```

কিন্তু:

```text
{2,4}
```

match করতে পারে:

```text
12
123
1234
```

---

# 🧠 একটি Pattern কীভাবে পড়বে?

এই pattern:

```python
r"01\d{9}"
```

এভাবে পড়বে:

```text
01
 ↓
literal 01

\d
 ↓
একটি digit

{9}
 ↓
এটা 9 বার

সুতরাং:

01 + 9 digits
```

আর:

```python
r"[A-Za-z]{3,10}"
```

পড়বে:

```text
[A-Za-z]
     ↓
letter

{3,10}
     ↓
3 থেকে 10 বার

অর্থাৎ:

3–10 letters
```

---

# 🔥 Day 3 Practical Examples

### Example 1 — 5 digit number

```python
re.fullmatch(r"\d{5}", "12345")
```

---

### Example 2 — 3–8 digit number

```python
re.fullmatch(r"\d{3,8}", "123456")
```

---

### Example 3 — Minimum 3 letters

```python
re.fullmatch(r"[A-Za-z]{3,}", "Python")
```

---

### Example 4 — 8–15 character username

```python
re.fullmatch(
    r"[A-Za-z0-9_]{8,15}",
    "atiar_123"
)
```

---

### Example 5 — Multiple spaces → single space

```python
text = "Python     is    powerful"

clean = re.sub(
    r"\s+",
    " ",
    text
)

print(clean)
```

Output:

```text
Python is powerful
```

---

# 🧪 Day 3 Practice

## Exercise 1

এই text থেকে সব numbers বের করো:

```python
text = "I bought 12 books, 3 pens and 25 notebooks."
```

Expected:

```text
['12', '3', '25']
```

---

## Exercise 2

শুধু 4-digit numbers বের করো:

```python
text = "2026 123 9999 45 2025"
```

Hint:

```python
r"\d{4}"
```

---

## Exercise 3

3–5 digit numbers বের করো:

```python
text = "12 123 1234 12345 123456"
```

---

## Exercise 4

এই phone number validate করো:

```text
01712345678
```

Pattern:

```text
01 + 9 digits
```

---

## Exercise 5

এক বা একাধিক whitespace-কে একটি space-এ convert করো:

```python
text = "Python    is   very     powerful"
```

Expected:

```text
Python is very powerful
```

---

## Exercise 6 ⭐

এই username:

```text
atiar_123
```

Rules:

```text
minimum 5
maximum 15
letters
numbers
underscore
```

Regex লিখো।

---

## Exercise 7 ⭐⭐

এই text থেকে সব uppercase word বের করো:

```python
text = "Python is VERY POWERFUL and FAST"
```

Expected concept:

```text
VERY
POWERFUL
FAST
```

---

## Exercise 8 🔥

এই pattern-এর অর্থ নিজের ভাষায় explain করো:

```python
r"[A-Za-z0-9_]{5,15}"
```

---

# 🎯 Day 3 শেষে তোমার জানা উচিত

```text
*       → 0+
+       → 1+
?       → 0 or 1
{n}     → exactly n
{n,m}   → n to m
{n,}    → minimum n
```

এবং এগুলো combine করতে পারা:

```text
\d+
\d{11}
[A-Za-z]+
[A-Za-z0-9_]{5,15}
\s+
(ab)+
```

### ⭐ সবচেয়ে গুরুত্বপূর্ণ formula

```text
Character Class
      +
Quantifier
      =
Powerful Pattern
```

উদাহরণ:

```python
[A-Za-z]+
```

→ এক বা একাধিক letter

```python
\d{11}
```

→ ঠিক 11 digit

```python
\s+
```

→ এক বা একাধিক whitespace

**Day 4-এ আমরা `^`, `$`, `\b`, `\B` শিখব—এগুলো দিয়ে pattern-এর অবস্থান বা boundary control করা যায়।**



# 🐍 Python `re` Module — Day 4

## 🎯 Anchors & Boundaries

আজকের topic:

```text
^
$
\b
\B
```

এগুলো দিয়ে Regex-কে বলা হয় **কোথা থেকে এবং কোথায় pattern match করতে হবে**।

Official docs: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `^` — Start of String

```python
^
```

মানে:

> Pattern অবশ্যই **string-এর শুরুতে** থাকতে হবে।

Example:

```python
import re

text = "Python is easy"

result = re.search(
    r"^Python",
    text
)

print(result)
```

Match হবে।

কারণ:

```text
Python is easy
^^^^^^
```

`Python` শুরুতেই আছে।

---

## ❌ Example

```python
text = "I love Python"

result = re.search(
    r"^Python",
    text
)

print(result)
```

এখানে match হবে না।

কারণ `Python` string-এর শুরুতে নেই।

```text
I love Python
^^^^^^^^^^^^
```

---

# 2️⃣ `$` — End of String

```python
$
```

মানে:

> Pattern অবশ্যই **string-এর শেষে** থাকতে হবে।

Example:

```python
text = "I love Python"

result = re.search(
    r"Python$",
    text
)

print(result)
```

Match হবে।

কারণ `Python` একদম শেষে।

```text
I love Python
       ^^^^^^
```

---

## ❌ Example

```python
text = "Python is easy"

result = re.search(
    r"Python$",
    text
)

print(result)
```

Match হবে না।

কারণ `Python` শেষে নেই।

---

# 3️⃣ `^` + `$` ⭐⭐⭐

এগুলো একসাথে ব্যবহার করলে:

```python
r"^Python$"
```

মানে:

> পুরো string অবশ্যই exactly `Python` হতে হবে।

Example:

```python
import re

print(
    re.fullmatch(
        r"Python",
        "Python"
    )
)
```

কিন্তু `search()` দিয়ে:

```python
re.search(
    r"^Python$",
    "Python"
)
```

match হবে।

---

## ❌

```text
Python is easy
```

match হবে না।

কারণ পুরো string `Python` নয়।

---

# 4️⃣ Practical Example — Exact Username

ধরো username-এর শুরু এবং শেষ control করতে চাই:

```python
pattern = r"^[A-Za-z0-9_]+$"
```

এটা বলছে:

```text
^
↓
শুরু

[A-Za-z0-9_]+
↓
letters/numbers/underscore

$
↓
শেষ
```

তাই:

```text
atiar123       ✅
atiar_123      ✅
atiar@test     ❌
atiar 123      ❌
```

---

# 5️⃣ `^` দিয়ে Starts With

ধরো সব Python-related sentence খুঁজতে চাই:

```python
text = "Python is powerful"

if re.search(r"^Python", text):
    print("Starts with Python")
```

Output:

```text
Starts with Python
```

---

# 6️⃣ `$` দিয়ে Ends With

```python
text = "I am learning Python"

if re.search(r"Python$", text):
    print("Ends with Python")
```

Output:

```text
Ends with Python
```

---

# 7️⃣ `\b` — Word Boundary ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

```python
\b
```

মানে:

> একটি **word character** এবং **non-word character**-এর boundary।

সহজভাবে:

> কোনো পুরো word আলাদা করে match করতে সাহায্য করে।

---

## Example

```python
text = "Python is powerful"

result = re.findall(
    r"\bPython\b",
    text
)

print(result)
```

Output:

```text
['Python']
```

---

# 8️⃣ কেন `\b` দরকার?

ধরো:

```python
text = "Python python Pythonic"
```

তুমি শুধু `Python` word খুঁজতে চাও।

যদি লিখো:

```python
re.findall(r"Python", text)
```

তাহলে:

```text
Python
Python
Python
```

এর মধ্যে `Pythonic`-এর অংশও match হবে।

কিন্তু:

```python
re.findall(
    r"\bPython\b",
    text
)
```

তাহলে শুধু standalone `Python` match হবে।

---

# 9️⃣ `\b` কোথায় থাকে?

ধরো:

```text
Hello World
```

`Hello`-এর:

```text
শুরু → word boundary
শেষ  → word boundary
```

তাই:

```python
r"\bHello\b"
```

মানে:

> পুরো `Hello` word।

---

# 🔟 Word Character কী?

Python regex-এর default Unicode behavior-এ `\w` সাধারণত word characters বোঝায়।

Conceptually:

```text
\w
↓
word character

\W
↓
non-word character
```

তাই:

```text
Hello!
     ↑
```

`o` এবং `!`-এর মাঝখানে boundary আছে।

---

# 1️⃣1️⃣ `\B` — Not a Word Boundary

`\b`-এর বিপরীত:

```python
\B
```

মানে:

> এখানে word boundary থাকা যাবে না।

Example:

```python
text = "Python Pythonic"

print(
    re.findall(
        r"Python\B",
        text
    )
)
```

এখানে `Pythonic`-এর `Python` অংশের পরে boundary নেই, কারণ তার পরেও word character (`i`) আছে।

তাই `Python`-এর অংশটি match হতে পারে `\B` condition অনুযায়ী।

---

# 1️⃣2️⃣ `\b` বনাম `\B`

|Pattern|Meaning|
|---|---|
|`\b`|Word boundary|
|`\B`|Not a word boundary|

সহজভাবে:

```text
\b
↓
boundary থাকতে হবে

\B
↓
boundary থাকতে পারবে না
```

---

# 1️⃣3️⃣ Practical Example — Word Search

Text:

```python
text = """
Python is popular.
Python programming is powerful.
Pythonic code can be clean.
"""
```

শুধু `Python` word:

```python
matches = re.findall(
    r"\bPython\b",
    text
)

print(matches)
```

এতে `Pythonic` থেকে `Python` নেওয়া হবে না।

---

# 1️⃣4️⃣ `^` + `$` + `\b` একসাথে

Example:

```python
pattern = r"^\bPython\b$"
```

এটা effectively বলছে:

> পুরো string-এ standalone `Python` থাকতে হবে এবং সেটাই পুরো content হতে হবে।

Valid:

```text
Python
```

Invalid:

```text
Python programming
```

Invalid:

```text
I love Python
```

---

# 1️⃣5️⃣ Real Example — Email-এর শুরু

ধরো text:

```python
text = "Email: user@example.com"
```

`Email` দিয়ে শুরু হচ্ছে কিনা:

```python
re.search(
    r"^Email:",
    text
)
```

---

# 1️⃣6️⃣ Real Example — File Extension

ধরো:

```python
filename = "report.pdf"
```

PDF দিয়ে শেষ হচ্ছে কিনা:

```python
if re.search(
    r"\.pdf$",
    filename
):
    print("PDF file")
```

### কেন `\.`?

Regex-এর `.` special character।

Actual dot match করতে:

```python
\.
```

ব্যবহার করা নিরাপদ।

---

# 1️⃣7️⃣ File Extension Validation

```python
pattern = r"\.(jpg|png|pdf)$"
```

এটা match করবে:

```text
photo.jpg
image.png
document.pdf
```

কিন্তু:

```text
photo.jpg.exe
```

match করবে না, কারণ `$` বলছে extension-টি একদম শেষে থাকতে হবে।

---

# 1️⃣8️⃣ `^` + Character Class

শুধু digit দিয়ে শুরু:

```python
r"^\d+"
```

Example:

```python
text = "123abc"

print(
    re.search(r"^\d+", text).group()
)
```

Output:

```text
123
```

---

# 1️⃣9️⃣ `$` + Character Class

শুধু digit দিয়ে শেষ:

```python
r"\d+$"
```

Example:

```python
text = "abc123"

match = re.search(
    r"\d+$",
    text
)

print(match.group())
```

Output:

```text
123
```

---

# 2️⃣0️⃣ Start + End Validation ⭐⭐⭐

একটি ১১-digit phone number:

```python
pattern = r"^01\d{9}$"
```

এখানে:

```text
^
↓
শুরু

01
↓
literal 01

\d{9}
↓
9 digits

$
↓
শেষ
```

তাই:

```text
01712345678   ✅
0171234567    ❌
abc01712345678 ❌
01712345678abc ❌
```

তবে বাস্তব Bangladesh phone validation-এর ক্ষেত্রে prefix/operator rules আরও নির্দিষ্ট হতে পারে; আজকের লক্ষ্য regex anchor বোঝা।

---

# 2️⃣1️⃣ `^` এবং `$` বনাম `fullmatch()`

এখানে একটি গুরুত্বপূর্ণ বিষয়।

তুমি লিখতে পারো:

```python
re.fullmatch(
    r"\d{11}",
    "01712345678"
)
```

অথবা:

```python
re.search(
    r"^\d{11}$",
    "01712345678"
)
```

দুটোই পুরো string validation-এর উদ্দেশ্যে ব্যবহার করা যায়।

তবে Python-এ **পুরো string match করতে `fullmatch()` সরাসরি এবং পরিষ্কার**।

---

# 2️⃣2️⃣ `^` এবং `$` সবসময় পুরো input বোঝায় না

এটা একটু advanced point।

`re.MULTILINE` flag ব্যবহার করলে:

```python
^
$
```

প্রতিটি line-এর শুরু/শেষের সাথেও কাজ করতে পারে।

Example:

```python
text = """Python
Java
Python
"""

print(
    re.findall(
        r"^Python$",
        text,
        re.MULTILINE
    )
)
```

এখানে প্রতিটি line আলাদাভাবে বিবেচিত হতে পারে।

এটা আমরা flags-এর সময় বিস্তারিত করব।

---

# 🧠 আজকের Cheat Sheet

|Symbol|Meaning|
|---|---|
|`^`|Start of string/line|
|`$`|End of string/line|
|`\b`|Word boundary|
|`\B`|Not a word boundary|

---

# 🔥 Pattern Reading Practice

### 1.

```python
r"^Hello"
```

মানে:

> `Hello` দিয়ে শুরু।

---

### 2.

```python
r"Python$"
```

মানে:

> `Python` দিয়ে শেষ।

---

### 3.

```python
r"^\d+$"
```

মানে:

> পুরো string-এ শুধু এক বা একাধিক digit।

Valid:

```text
12345
```

Invalid:

```text
123abc
```

---

### 4.

```python
r"\bcat\b"
```

মানে:

> standalone `cat` word।

Match:

```text
I have a cat.
```

কিন্তু `category`-এর ভিতরের `cat` match করবে না।

---

### 5.

```python
r"^[A-Za-z]+$"
```

মানে:

> পুরো string-এ শুধু English letters থাকতে হবে এবং কমপক্ষে একটি letter থাকতে হবে।

Valid:

```text
Python
Hello
ATIAR
```

Invalid:

```text
Python123
Hello World
Python!
```

---

# 🧪 Day 4 Practice

### Exercise 1

Check করো string `"Python"` দিয়ে শুরু কিনা।

```python
text = "Python is easy"
```

---

### Exercise 2

Check করো `"Python"` দিয়ে শেষ কিনা।

```python
text = "I am learning Python"
```

---

### Exercise 3 ⭐

একটি string-এ **শুধু digits** আছে কিনা check করো।

```text
123456
```

Hint:

```python
r"^\d+$"
```

---

### Exercise 4 ⭐

শুধু English letters আছে কিনা check করো:

```text
Python
```

Pattern নিজে লেখো।

---

### Exercise 5 ⭐

এই text থেকে standalone `cat` word বের করো:

```python
text = "cat category bobcat cat"
```

Expected:

```text
cat
cat
```

Hint:

```python
\b
```

---

### Exercise 6 🔥

PDF filename validate করো:

```text
report.pdf
```

কিন্তু এগুলো যেন valid না হয়:

```text
report.pdf.exe
report.txt
report.pdf.backup
```

---

### Exercise 7 🔥

এই pattern-এর অর্থ নিজের ভাষায় explain করো:

```python
r"^01\d{9}$"
```

---

### Exercise 8 🔥🔥

এই pattern-এর অর্থ explain করো:

```python
r"^[A-Za-z0-9_]{5,15}$"
```

এখানে আজকের **`^` + `$`** এবং গতকালের **character class + quantifier**—দুটো একসাথে ব্যবহার হয়েছে।

---

## 🎯 Day 4-এর মূল লক্ষ্য

আজ শেষে এই structure চিনতে পারা উচিত:

```text
^
↓
START

[character class]
↓
WHAT characters?

quantifier
↓
HOW MANY?

$
↓
END
```

যেমন:

```python
r"^[A-Za-z0-9_]{5,15}$"
```

এটাই Regex শেখার আসল skill—শুধু pattern মুখস্থ করা নয়, **pattern দেখে তার অর্থ পড়তে পারা**।


# 🐍 Python `re` Module — Day 5

## 🎯 `re.search()` — Pattern খোঁজা

আজ আমরা `re` module-এর সবচেয়ে গুরুত্বপূর্ণ functionগুলোর একটি শিখব:

```python
re.search()
```

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `re.search()` কী?

`re.search()` পুরো string-এর মধ্যে **প্রথম যে জায়গায় pattern match করে, সেটা খুঁজে বের করে**।

Syntax:

```python
re.search(pattern, string)
```

Example:

```python
import re

text = "I am learning Python"

result = re.search(r"Python", text)

print(result)
```

Match পাওয়া গেলে একটি **Match object** return করবে।

---

# 2️⃣ Match পাওয়া গেলে কী হয়?

```python
import re

text = "I am learning Python"

result = re.search(r"Python", text)

if result:
    print("Found")
else:
    print("Not found")
```

Output:

```text
Found
```

কারণ `Python` text-এর মধ্যে আছে।

---

# 3️⃣ Match না পাওয়া গেলে?

```python
result = re.search(
    r"Java",
    "I am learning Python"
)

print(result)
```

Output:

```text
None
```

তাই সাধারণত:

```python
if result:
    ...
```

ব্যবহার করা হয়।

---

# 4️⃣ `search()` কোথা থেকে খোঁজে?

খুব গুরুত্বপূর্ণ:

```python
re.search()
```

string-এর **যেকোনো জায়গা থেকে** pattern খুঁজে।

Example:

```python
text = "Hello Python World"

result = re.search(
    r"Python",
    text
)
```

এখানে `Python` মাঝখানে থাকলেও match হবে।

```text
Hello Python World
      ^^^^^^
```

---

# 5️⃣ `^` দিলে কী পরিবর্তন হয়?

আগের Day 4-এর concept ব্যবহার করি:

```python
re.search(r"^Python", text)
```

এখন `Python` অবশ্যই শুরুতে থাকতে হবে।

Example:

```python
text = "Python is easy"

print(
    re.search(r"^Python", text)
)
```

✅ Match।

কিন্তু:

```python
text = "I love Python"

print(
    re.search(r"^Python", text)
)
```

❌ Match হবে না।

---

# 6️⃣ `$` দিয়ে End Match

```python
text = "I love Python"

result = re.search(
    r"Python$",
    text
)

if result:
    print("Found at the end")
```

Output:

```text
Found at the end
```

---

# 7️⃣ `search()` + Character Class

Day 2-এর concept:

```python
text = "My age is 25"

result = re.search(
    r"\d+",
    text
)

print(result.group())
```

Output:

```text
25
```

এখানে:

```text
\d
↓
digit

+
↓
one or more
```

---

# 8️⃣ `search()` + Quantifier

Example:

```python
text = "Order number: 12345"

result = re.search(
    r"\d{5}",
    text
)

print(result.group())
```

Output:

```text
12345
```

---

# 9️⃣ `group()` ⭐⭐⭐

`search()` সাধারণত Match object দেয়।

Matched text বের করতে:

```python
result.group()
```

Example:

```python
import re

text = "My age is 25"

match = re.search(
    r"\d+",
    text
)

print(match.group())
```

Output:

```text
25
```

---

# 🔟 `start()`

Match কোথা থেকে শুরু হয়েছে:

```python
text = "My age is 25"

match = re.search(
    r"\d+",
    text
)

print(match.start())
```

Output:

```text
10
```

কারণ `25` index 10 থেকে শুরু।

---

# 1️⃣1️⃣ `end()`

```python
print(match.end())
```

Output:

```text
12
```

মনে রাখবে:

```text
start() → starting index
end()   → ending index-এর পরের index
```

---

# 1️⃣2️⃣ `span()`

দুটো একসাথে:

```python
print(match.span())
```

Output:

```text
(10, 12)
```

অর্থাৎ:

```text
start = 10
end   = 12
```

---

# 1️⃣3️⃣ Match Object

একটি Match object থেকে গুরুত্বপূর্ণ তথ্য:

```python
match.group()
match.start()
match.end()
match.span()
```

Example:

```python
import re

text = "Python 123"

match = re.search(
    r"\d+",
    text
)

print("Value:", match.group())
print("Start:", match.start())
print("End:", match.end())
print("Span:", match.span())
```

---

# 1️⃣4️⃣ `search()` শুধু প্রথম match দেয় ⭐

এটা খুব গুরুত্বপূর্ণ।

```python
text = "I have 10 apples and 20 oranges"

match = re.search(
    r"\d+",
    text
)

print(match.group())
```

Output:

```text
10
```

`20` আছে, কিন্তু `search()` শুধু **প্রথম match** return করে।

সবগুলো চাইলে পরে:

```python
re.findall()
```

শিখব।

---

# 1️⃣5️⃣ `search()` বনাম `findall()`

### `search()`

```python
re.search(
    r"\d+",
    "10 20 30"
)
```

প্রথম match:

```text
10
```

### `findall()`

```python
re.findall(
    r"\d+",
    "10 20 30"
)
```

সব match:

```text
['10', '20', '30']
```

সহজভাবে:

```text
search()
   ↓
প্রথম match

findall()
   ↓
সব match
```

---

# 1️⃣6️⃣ Real Example — Email আছে কিনা

```python
import re

text = "Contact me at user@example.com"

pattern = r"[\w.-]+@[\w.-]+\.\w+"

match = re.search(
    pattern,
    text
)

if match:
    print("Email found")
    print(match.group())
```

Output:

```text
Email found
user@example.com
```

---

# 1️⃣7️⃣ Real Example — Phone Number খোঁজা

```python
text = "Call me at 01712345678"

match = re.search(
    r"01\d{9}",
    text
)

if match:
    print(match.group())
```

Output:

```text
01712345678
```

এখানে `search()` text-এর যেকোনো জায়গায় phone number খুঁজছে।

---

# 1️⃣8️⃣ Real Example — URL

```python
text = "Visit https://example.com for more information."

match = re.search(
    r"https?://\S+",
    text
)

if match:
    print(match.group())
```

Output:

```text
https://example.com
```

---

# 1️⃣9️⃣ `search()` দিয়ে Validation?

এখানে সতর্ক হও।

ধরো:

```python
text = "123abc"

match = re.search(
    r"\d+",
    text
)
```

এটা match করবে:

```text
123
```

কিন্তু পুরো string শুধু number নয়।

যদি পুরো string validate করতে চাও, ভালো:

```python
re.fullmatch(r"\d+", text)
```

অথবা anchors:

```python
re.search(r"^\d+$", text)
```

তাই:

```text
search()
↓
খুঁজে বের করা

fullmatch()
↓
পুরো string validation
```

---

# 2️⃣0️⃣ `search()` + `^`

```python
text = "Python is great"

match = re.search(
    r"^Python",
    text
)
```

মানে:

> `Python` দিয়ে string শুরু হয়েছে কিনা।

---

# 2️⃣1️⃣ `search()` + `$`

```python
text = "I love Python"

match = re.search(
    r"Python$",
    text
)
```

মানে:

> `Python` দিয়ে string শেষ হয়েছে কিনা।

---

# 2️⃣2️⃣ `search()` + `\b`

Standalone word খুঁজতে:

```python
text = "Python is Pythonic"

match = re.search(
    r"\bPython\b",
    text
)

print(match.group())
```

এটা প্রথম standalone `Python` খুঁজবে।

`Pythonic`-এর ভিতরের `Python`কে standalone word হিসেবে match করবে না।

---

# 2️⃣3️⃣ Practical Project Example 🔥

ধরো একটি log:

```text
2026-08-17 ERROR Database connection failed
```

আমরা প্রথমে date খুঁজব:

```python
import re

log = "2026-08-17 ERROR Database connection failed"

date = re.search(
    r"\d{4}-\d{2}-\d{2}",
    log
)

if date:
    print("Date:", date.group())
```

Output:

```text
Date: 2026-08-17
```

তারপর error level:

```python
level = re.search(
    r"\bERROR\b",
    log
)

if level:
    print("Level:", level.group())
```

Output:

```text
Level: ERROR
```

এটাই Regex-এর real-world usage।

---

# 2️⃣4️⃣ একাধিক তথ্য আলাদা করে বের করা

```python
import re

text = """
Name: Atiar
Age: 25
Email: user@example.com
"""

name = re.search(
    r"Name:\s*(\w+)",
    text
)

age = re.search(
    r"Age:\s*(\d+)",
    text
)

email = re.search(
    r"Email:\s*([\w.-]+@[\w.-]+\.\w+)",
    text
)

print(name.group(1))
print(age.group(1))
print(email.group(1))
```

Output concept:

```text
Atiar
25
user@example.com
```

এখানে আমরা **group** ব্যবহার করেছি। Day 12-এ groups অনেক বিস্তারিত করব।

---

# 🧠 `re.search()` Mental Model

যখন তুমি লেখো:

```python
match = re.search(
    pattern,
    text
)
```

Python roughly এভাবে কাজ করে:

```text
TEXT
 ↓
character by character search
 ↓
pattern match?
 ↓
YES → Match object
NO  → None
```

---

# ⭐ Day 5 Cheat Sheet

|Code|কাজ|
|---|---|
|`re.search()`|প্রথম match খুঁজে|
|`match.group()`|matched text|
|`match.start()`|শুরু index|
|`match.end()`|শেষের পরের index|
|`match.span()`|`(start, end)`|
|`None`|match পাওয়া যায়নি|

---

# 🧪 Day 5 Practice

### Exercise 1

এই text থেকে প্রথম number বের করো:

```python
text = "I bought 25 books and 10 pens."
```

Expected:

```text
25
```

---

### Exercise 2

এই text-এর মধ্যে `Python` আছে কিনা check করো:

```python
text = "I am learning Python programming."
```

---

### Exercise 3

এই text থেকে প্রথম 11-digit phone number বের করো:

```python
text = "Contact: 01712345678"
```

---

### Exercise 4 ⭐

এই text থেকে প্রথম email বের করো:

```python
text = "Email me at user@example.com"
```

---

### Exercise 5 ⭐

এই text `Python` দিয়ে শুরু হয় কিনা check করো:

```python
text = "Python is powerful"
```

---

### Exercise 6 ⭐

এই text `Python` দিয়ে শেষ হয় কিনা check করো:

```python
text = "I am learning Python"
```

---

### Exercise 7 🔥

এই log থেকে **date** এবং **ERROR** বের করো:

```text
2026-08-17 ERROR Database connection failed
```

---

### Exercise 8 🔥🔥

এই text:

```python
text = """
Name: Atiar
Age: 25
Phone: 01712345678
"""
```

`re.search()` ব্যবহার করে প্রথমে:

```text
Name
Age
Phone
```

এর values বের করার চেষ্টা করো।

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়

`re.search()` = **text-এর মধ্যে প্রথম matching pattern খুঁজে বের করা।**

মনে রাখো:

```text
re.search()
    ↓
first match
    ↓
Match Object
    ↓
group()
start()
end()
span()
```

আর সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
search()   → কোথাও match আছে কিনা / প্রথম match
findall()  → সব match
fullmatch() → পুরো string match
```

**Day 6-এ আমরা `re.match()` শিখব এবং `search()` বনাম `match()` খুব পরিষ্কারভাবে compare করব।**
# 🐍 Python `re` Module — Day 6

## 🎯 `re.match()` — String-এর শুরু থেকে Matching

আজ আমরা শিখব:

```python
re.match()
```

এবং সবচেয়ে গুরুত্বপূর্ণভাবে:

```text
re.search()  vs  re.match()
```

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `re.match()` কী?

`re.match()` **শুধু string-এর শুরু থেকে** pattern match করার চেষ্টা করে।

Syntax:

```python
re.match(pattern, string)
```

Example:

```python
import re

text = "Python is easy"

result = re.match(r"Python", text)

print(result.group())
```

Output:

```text
Python
```

কারণ `Python` একদম শুরুতে আছে।

---

# 2️⃣ Pattern শুরুতে না থাকলে ❌

```python
import re

text = "I love Python"

result = re.match(r"Python", text)

print(result)
```

Output:

```text
None
```

কারণ:

```text
I love Python
^^^^^^^^^^^^
```

`Python` শুরুতে নেই।

---

# 3️⃣ `search()` বনাম `match()` ⭐⭐⭐

এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়।

### `re.search()`

পুরো string-এর মধ্যে খুঁজে:

```python
re.search(r"Python", "I love Python")
```

✅ Match হবে।

### `re.match()`

শুধু শুরু থেকে:

```python
re.match(r"Python", "I love Python")
```

❌ Match হবে না।

---

## সহজভাবে মনে রাখো

```text
search()
↓
পুরো text-এর মধ্যে খোঁজে

match()
↓
শুধু শুরু থেকে দেখে
```

---

# 4️⃣ একই Example দিয়ে Compare

```python
import re

text = "Hello Python"

search_result = re.search(
    r"Python",
    text
)

match_result = re.match(
    r"Python",
    text
)

print(search_result)
print(match_result)
```

Result:

```text
search() → Match object
match()  → None
```

কারণ `Python` মাঝখানে আছে।

---

# 5️⃣ `match()`-এ `^` দরকার হয়?

সাধারণত না।

এই দুটো একই উদ্দেশ্যে ব্যবহার করা যায়:

```python
re.match(r"Python", text)
```

এবং:

```python
re.search(r"^Python", text)
```

কারণ `match()` নিজেই শুরু থেকে match করে।

---

# 6️⃣ `match()` + `\d`

```python
text = "123abc"

result = re.match(
    r"\d+",
    text
)

print(result.group())
```

Output:

```text
123
```

কারণ string-এর শুরুতে digits আছে।

---

# 7️⃣ কিন্তু মাঝখানে number থাকলে?

```python
text = "abc123"

result = re.match(
    r"\d+",
    text
)

print(result)
```

Output:

```text
None
```

কারণ শুরু হচ্ছে:

```text
abc123
^^^
```

এখানে শুরুতে digit নেই।

কিন্তু:

```python
re.search(r"\d+", text)
```

দিলে `123` পাওয়া যাবে।

---

# 8️⃣ `match()` + Character Class

Day 2-এর concept:

```python
text = "Python123"

result = re.match(
    r"[A-Za-z]+",
    text
)

print(result.group())
```

Output:

```text
Python
```

কারণ শুরুতে letters আছে।

---

# 9️⃣ `match()` + Quantifier

Day 3:

```python
text = "12345abc"

result = re.match(
    r"\d{5}",
    text
)

print(result.group())
```

Output:

```text
12345
```

---

# 🔟 `match()` + `$`

একটি গুরুত্বপূর্ণ বিষয়:

```python
re.match(r"\d+", "123abc")
```

এটা `123` match করবে।

কিন্তু যদি তুমি **পুরো string** শুধু digit কিনা দেখতে চাও:

```python
re.fullmatch(r"\d+", "123abc")
```

দেওয়া ভালো।

অথবা:

```python
re.match(r"\d+$", "123abc")
```

এখানে `$` পুরো string-এর শেষ পর্যন্ত যেতে বাধ্য করবে, তাই match হবে না।

---

# 1️⃣1️⃣ `match()` Validation-এর জন্য?

`match()` দিয়ে শুরু থেকে format check করা যায়।

Example:

```python
phone = "01712345678"

result = re.match(
    r"01\d{9}",
    phone
)

if result:
    print("Starts with valid phone pattern")
```

কিন্তু এটি মনে রেখো:

```python
phone = "01712345678abc"
```

এখানেও `match()` pattern match করতে পারে, কারণ শুরুটা ঠিক আছে।

যদি **পুরো phone number validate** করতে চাও:

```python
if re.fullmatch(r"01\d{9}", phone):
    print("Valid")
```

এটাই বেশি পরিষ্কার।

---

# 1️⃣2️⃣ `match()` এবং `fullmatch()` ⭐⭐⭐

এটা খুব ভালোভাবে বোঝো।

### `match()`

শুরু থেকে match:

```python
re.match(r"\d+", "123abc")
```

Result:

```text
123
```

### `fullmatch()`

পুরো string match করতে হবে:

```python
re.fullmatch(r"\d+", "123abc")
```

Result:

```text
None
```

---

## Difference

```text
match()
↓
START → pattern → anything can remain

fullmatch()
↓
START → pattern → END
```

---

# 1️⃣3️⃣ Practical Example — Username

ধরো username-এর শুরুতে letter থাকতে হবে।

```python
username = "atiar123"

result = re.match(
    r"[A-Za-z]",
    username
)

if result:
    print("Starts with a letter")
```

---

# 1️⃣4️⃣ Practical Example — URL

ধরো URL `https://` দিয়ে শুরু কিনা:

```python
url = "https://example.com"

result = re.match(
    r"https?://",
    url
)

if result:
    print("Valid URL prefix")
```

এখানে:

```text
http
```

বা:

```text
https
```

match হতে পারে।

কারণ:

```text
s?
```

মানে `s` optional।

---

# 1️⃣5️⃣ Practical Example — Log

ধরো log line:

```text
ERROR Database connection failed
```

শুরুতে `ERROR` আছে কিনা:

```python
log = "ERROR Database connection failed"

result = re.match(
    r"ERROR",
    log
)

if result:
    print("Error log")
```

Output:

```text
Error log
```

কিন্তু:

```text
INFO ERROR Database connection failed
```

এখানে:

```python
re.match(r"ERROR", log)
```

❌ match করবে না।

কারণ `ERROR` শুরুতে নেই।

---

# 1️⃣6️⃣ `match()` + `group()`

`search()`-এর মতোই Match object পাওয়া যায়।

```python
text = "Age: 25"

match = re.match(
    r"Age:\s*(\d+)",
    text
)

if match:
    print(match.group())
```

Output:

```text
Age: 25
```

আর:

```python
print(match.group(1))
```

Output:

```text
25
```

Groups আমরা Day 12-এ বিস্তারিত শিখব।

---

# 1️⃣7️⃣ `match.start()`

```python
text = "Python is easy"

match = re.match(
    r"Python",
    text
)

print(match.start())
```

Output:

```text
0
```

কারণ `match()` সবসময় শুরু থেকে চেষ্টা করে।

---

# 1️⃣8️⃣ `match.end()`

```python
print(match.end())
```

Output:

```text
6
```

কারণ:

```text
Python
012345
```

শেষ index-এর পরের position = `6`।

---

# 1️⃣9️⃣ `match.span()`

```python
print(match.span())
```

Output:

```text
(0, 6)
```

---

# 2️⃣0️⃣ Important Comparison Table ⭐⭐⭐

|Function|কোথা থেকে খোঁজে|কতগুলো match|
|---|---|---|
|`re.search()`|যেকোনো জায়গা|প্রথমটি|
|`re.match()`|শুধু শুরু|প্রথমটি|
|`re.fullmatch()`|পুরো string|পুরোটা match হতে হবে|
|`re.findall()`|পুরো string|সবগুলো|

---

# 2️⃣1️⃣ একই Text দিয়ে চারটি Function

Text:

```python
text = "Python 123 Python 456"
```

### `search()`

```python
re.search(r"Python", text)
```

প্রথম `Python`।

### `match()`

```python
re.match(r"Python", text)
```

শুরুর `Python`।

### `fullmatch()`

```python
re.fullmatch(r"Python", text)
```

❌ None — পুরো string `Python` নয়।

### `findall()`

```python
re.findall(r"Python", text)
```

Output:

```text
['Python', 'Python']
```

---

# 2️⃣2️⃣ কখন কোনটা ব্যবহার করবে?

### 🔎 Text-এর মধ্যে কিছু খুঁজতে:

```python
re.search()
```

### 🟢 Text-এর শুরুতে pattern আছে কিনা:

```python
re.match()
```

### 🎯 পুরো input valid কিনা:

```python
re.fullmatch()
```

### 📋 সব matching value:

```python
re.findall()
```

---

# 🧠 মনে রাখার সহজ Trick

```text
search
   ↓
"কোথাও আছে?"

match
   ↓
"শুরুতে আছে?"

fullmatch
   ↓
"পুরোটা কি এটাই?"

findall
   ↓
"সবগুলো কোথায়?"
```

---

# 🧪 Day 6 Practice

### Exercise 1

এই text-এর শুরুতে `Python` আছে কিনা check করো:

```python
text = "Python is powerful"
```

---

### Exercise 2

এখানে `Python` শুরুতে নেই:

```python
text = "I love Python"
```

`re.match()` ব্যবহার করে দেখো।

---

### Exercise 3

এই text থেকে শুরুতে থাকা number বের করো:

```python
text = "12345 apples"
```

Hint:

```python
r"\d+"
```

---

### Exercise 4 ⭐

এই text-এ `123` আছে, কিন্তু শুরুতে নেই:

```python
text = "abc123"
```

`re.match()` এবং `re.search()` দুটো ব্যবহার করে difference দেখো।

---

### Exercise 5 ⭐

এই phone number পুরোপুরি valid কিনা check করো:

```python
phone = "01712345678"
```

কোনটা ব্যবহার করা better?

```text
match()
নাকি
fullmatch()
```

---

### Exercise 6 ⭐

URL `https://` অথবা `http://` দিয়ে শুরু কিনা check করো:

```python
url = "https://example.com"
```

---

### Exercise 7 🔥

এই log-এর শুরুতে `ERROR` আছে কিনা:

```python
log = "ERROR Database connection failed"
```

`re.match()` ব্যবহার করো।

---

### Exercise 8 🔥🔥

নিজে explain করো:

```python
re.search(r"\d+", "abc123")
```

এবং:

```python
re.match(r"\d+", "abc123")
```

কেন প্রথমটিতে match পাওয়া যায় কিন্তু দ্বিতীয়টিতে `None` পাওয়া যায়?

---

# 🎯 Day 6-এর Final Concept

আজকের সবচেয়ে গুরুত্বপূর্ণ relationship:

```text
              STRING
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
    search     match    fullmatch
       │         │         │
    anywhere    start    entire
       │         │         │
    first       first     whole
    match       match     string
```

**Day 7-এ আমরা `re.fullmatch()` পুরোপুরি শিখব—বিশেষ করে username, phone, PIN, ID, input validation ইত্যাদিতে কীভাবে ব্যবহার করতে হয়।**


# 🐍 Python `re` Module — Day 7

## 🎯 `re.fullmatch()` — Complete String Validation

আজ আমরা শিখব:

```python
re.fullmatch()
```

এটা `re` module-এর **validation-এর জন্য সবচেয়ে গুরুত্বপূর্ণ functionগুলোর একটি**।

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `re.fullmatch()` কী?

`re.fullmatch()` চেক করে:

> **পুরো string-টাই pattern-এর সাথে match করছে কিনা।**

Syntax:

```python
re.fullmatch(pattern, string)
```

Example:

```python
import re

text = "12345"

result = re.fullmatch(r"\d+", text)

print(result)
```

Match হবে।

কারণ পুরো string:

```text
12345
^^^^^
```

সবই digit।

---

# 2️⃣ Partial Match হলে ❌

```python
import re

text = "12345abc"

result = re.fullmatch(r"\d+", text)

print(result)
```

Output:

```text
None
```

কারণ:

```text
12345abc
^^^^^---
digits  letters
```

পুরো string digit নয়।

---

# 3️⃣ `fullmatch()` বনাম `match()` ⭐⭐⭐

এটা খুব ভালোভাবে বুঝতে হবে।

### `match()`

```python
re.match(r"\d+", "12345abc")
```

Result:

```text
12345
```

কারণ শুরুতে digit আছে।

### `fullmatch()`

```python
re.fullmatch(r"\d+", "12345abc")
```

Result:

```text
None
```

কারণ পুরো string digit হতে হবে।

---

# 4️⃣ `fullmatch()` বনাম `search()`

```python
text = "abc123"
```

### `search()`

```python
re.search(r"\d+", text)
```

✅ `123`

### `fullmatch()`

```python
re.fullmatch(r"\d+", text)
```

❌ `None`

কারণ পুরো string number নয়।

---

# 🧠 সহজভাবে

```text
search()
↓
কোথাও pattern আছে?

match()
↓
শুরুতে pattern আছে?

fullmatch()
↓
পুরো string pattern অনুযায়ী?
```

---

# 5️⃣ `fullmatch()` + `\d`

শুধু digits:

```python
import re

def is_number(text):
    return re.fullmatch(r"\d+", text) is not None
```

Test:

```python
print(is_number("12345"))
print(is_number("123abc"))
```

Output:

```text
True
False
```

---

# 6️⃣ 4 Digit PIN ⭐⭐⭐

ধরো PIN ঠিক 4 digit হতে হবে:

```python
pattern = r"\d{4}"
```

Example:

```python
pin = "1234"

if re.fullmatch(r"\d{4}", pin):
    print("Valid PIN")
else:
    print("Invalid PIN")
```

Output:

```text
Valid PIN
```

---

### Invalid:

```text
123     ❌
12345   ❌
12ab    ❌
```

কারণ:

```text
\d{4}
```

মানে exactly 4 digits।

---

# 7️⃣ 6 Digit OTP

```python
otp = "483921"

if re.fullmatch(r"\d{6}", otp):
    print("Valid OTP")
```

এখানে:

```text
\d{6}
↓
exactly 6 digits
```

---

# 8️⃣ Bangladesh Phone Format

Basic format:

```python
pattern = r"01\d{9}"
```

Validation:

```python
phone = "01712345678"

if re.fullmatch(r"01\d{9}", phone):
    print("Valid format")
else:
    print("Invalid format")
```

এখানে পুরো input match করতে হবে।

---

# 9️⃣ Username Validation ⭐⭐⭐

ধরো username-এর rules:

```text
5–15 characters
letters
numbers
underscore
```

Pattern:

```python
r"[A-Za-z0-9_]{5,15}"
```

Validation:

```python
username = "atiar_123"

if re.fullmatch(
    r"[A-Za-z0-9_]{5,15}",
    username
):
    print("Valid username")
else:
    print("Invalid username")
```

---

## কোনগুলো invalid?

```text
atiar          ✅
atiar123       ✅
atiar_123      ✅
abc            ❌  # too short
atiar@test     ❌  # @ not allowed
hello world    ❌  # space not allowed
```

---

# 🔟 শুধু English Letters

```python
name = "Atiar"

if re.fullmatch(
    r"[A-Za-z]+",
    name
):
    print("Valid")
```

এটা match করবে:

```text
Atiar
Python
HELLO
```

কিন্তু:

```text
Atiar123
Atiar Rahman
Atiar!
```

match করবে না।

---

# 1️⃣1️⃣ শুধু Lowercase Letters

```python
text = "python"

if re.fullmatch(
    r"[a-z]+",
    text
):
    print("Lowercase only")
```

---

# 1️⃣2️⃣ শুধু Uppercase Letters

```python
text = "PYTHON"

if re.fullmatch(
    r"[A-Z]+",
    text
):
    print("Uppercase only")
```

---

# 1️⃣3️⃣ Alphanumeric

শুধু letters + digits:

```python
pattern = r"[A-Za-z0-9]+"
```

Example:

```python
value = "Python123"

if re.fullmatch(
    r"[A-Za-z0-9]+",
    value
):
    print("Valid")
```

---

# 1️⃣4️⃣ `\w+` ব্যবহার করা যায়?

হ্যাঁ:

```python
r"\w+"
```

কিন্তু মনে রাখো:

```text
\w
```

শুধু `[A-Za-z0-9_]`-এর exact equivalent ধরে নেওয়া ঠিক নয়, কারণ Python-এর Unicode behavior আছে।

যদি তোমার requirement হয়:

> English letters + digits + underscore

তাহলে explicit:

```python
r"[A-Za-z0-9_]+"
```

আরও পরিষ্কার।

---

# 1️⃣5️⃣ Email-এর Basic Validation

একটি simple email pattern:

```python
pattern = r"[\w.-]+@[\w.-]+\.\w+"
```

Example:

```python
email = "user@example.com"

if re.fullmatch(
    pattern,
    email
):
    print("Valid email format")
```

⚠️ এটা **basic format check**, complete RFC-compliant email validation নয়।

---

# 1️⃣6️⃣ URL Scheme Validation

শুধু URL `http://` বা `https://` দিয়ে শুরু হওয়া নয়—পুরো input validate করতে চাইলে pattern design আরও বড় হবে।

Basic example:

```python
url = "https://example.com"

pattern = r"https?://.+"

if re.fullmatch(pattern, url):
    print("Valid basic URL format")
```

এখানে:

```text
http
https
```

দুটোই allowed।

কারণ:

```text
https?
   ↑
s optional
```

---

# 1️⃣7️⃣ Hex Color Basic Pattern

যেমন:

```text
#FFFFFF
```

Pattern:

```python
r"#[A-Fa-f0-9]{6}"
```

Validation:

```python
color = "#FF00AA"

if re.fullmatch(
    r"#[A-Fa-f0-9]{6}",
    color
):
    print("Valid hex color")
```

---

# 1️⃣8️⃣ Date Format Validation

ধরো format:

```text
2026-08-17
```

Basic format:

```python
pattern = r"\d{4}-\d{2}-\d{2}"
```

Example:

```python
date = "2026-08-17"

if re.fullmatch(
    r"\d{4}-\d{2}-\d{2}",
    date
):
    print("Correct format")
```

⚠️ এখানে শুধু **format** check হচ্ছে।

যেমন:

```text
9999-99-99
```

regex অনুযায়ী format ঠিক হতে পারে, কিন্তু real date নয়।

Actual date validation-এর জন্য `datetime` ব্যবহার করা ভালো।

---

# 1️⃣9️⃣ Time Format

Basic `HH:MM` format:

```python
time = "14:30"

if re.fullmatch(
    r"\d{2}:\d{2}",
    time
):
    print("Correct format")
```

কিন্তু:

```text
99:99
```

এটাও এই simple regex-এ match করবে।

তাই regex format check করছে, mathematical/time validity নয়।

---

# 2️⃣0️⃣ Password Length

Minimum 8 characters:

```python
password = "mypassword"

if re.fullmatch(
    r".{8,}",
    password
):
    print("Minimum length satisfied")
```

এখানে:

```text
.
↓
যেকোনো character

{8,}
↓
minimum 8
```

⚠️ Strong password validation পরে **lookahead** শেখার সময় করব।

---

# 2️⃣1️⃣ `.` এবং `fullmatch()`

ধরো:

```python
text = "Hello"

re.fullmatch(r".+", text)
```

Match করবে।

কারণ:

```text
.+ 
↓
এক বা একাধিক character
```

কিন্তু empty string:

```python
re.fullmatch(r".+", "")
```

❌ match করবে না।

---

# 2️⃣2️⃣ `*` বনাম `+`

```python
r".*"
```

মানে:

> zero or more

তাই empty string-ও match করতে পারে।

```python
re.fullmatch(r".*", "")
```

✅

কিন্তু:

```python
r".+"
```

মানে:

> one or more

তাই:

```python
re.fullmatch(r".+", "")
```

❌

---

# 2️⃣3️⃣ `fullmatch()` এবং `^ $`

তুমি চাইলে:

```python
re.fullmatch(
    r"\d{4}",
    "1234"
)
```

এটা পরিষ্কার।

আর `search()` দিয়ে:

```python
re.search(
    r"^\d{4}$",
    "1234"
)
```

এটাও কাজ করে।

কিন্তু পুরো string validation-এর জন্য:

```python
re.fullmatch()
```

অনেক সময় বেশি readable।

---

# 2️⃣4️⃣ Function বানিয়ে Validation

Production code-এ এমন function বানাতে পারো:

```python
import re

def is_valid_username(username):
    pattern = r"[A-Za-z0-9_]{5,15}"
    return re.fullmatch(pattern, username) is not None
```

Test:

```python
print(is_valid_username("atiar123"))
print(is_valid_username("ab"))
print(is_valid_username("atiar@test"))
```

Output:

```text
True
False
False
```

---

# 2️⃣5️⃣ Multiple Validators

একটি ছোট validation utility:

```python
import re


def is_valid_pin(pin):
    return re.fullmatch(
        r"\d{4}",
        pin
    ) is not None


def is_valid_username(username):
    return re.fullmatch(
        r"[A-Za-z0-9_]{5,15}",
        username
    ) is not None


def is_valid_phone(phone):
    return re.fullmatch(
        r"01\d{9}",
        phone
    ) is not None
```

Test:

```python
print(is_valid_pin("1234"))
print(is_valid_username("atiar123"))
print(is_valid_phone("01712345678"))
```

---

# 🧠 Day 7 Mental Model

যখন validation করতে হবে:

```text
INPUT
  ↓
fullmatch()
  ↓
পুরো input pattern-এর সাথে match?
  ↓
YES → valid format
NO  → invalid format
```

---

# ⭐ Day 7 Cheat Sheet

|Requirement|Regex|
|---|---|
|Only digits|`\d+`|
|Exactly 4 digits|`\d{4}`|
|Exactly 6 digits|`\d{6}`|
|5–15 username chars|`[A-Za-z0-9_]{5,15}`|
|Only English letters|`[A-Za-z]+`|
|Lowercase only|`[a-z]+`|
|Uppercase only|`[A-Z]+`|
|Letters + numbers|`[A-Za-z0-9]+`|
|Basic date format|`\d{4}-\d{2}-\d{2}`|
|Basic hex color|`#[A-Fa-f0-9]{6}`|

---

# 🧪 Day 7 Practice

### Exercise 1

4-digit PIN validate করো:

```python
pin = "1234"
```

---

### Exercise 2

এইগুলোর মধ্যে কোন username valid সেটা বের করো:

```text
atiar123
ab
atiar@test
atiar_123
```

Rules:

```text
5–15 chars
letters + numbers + underscore
```

---

### Exercise 3

এই phone number validate করো:

```text
01712345678
```

---

### Exercise 4 ⭐

শুধু lowercase English letters allowed:

```text
python
Python
python123
```

কোনগুলো valid?

---

### Exercise 5 ⭐

এই date-এর basic format validate করো:

```text
2026-08-17
```

Pattern:

```python
\d{4}-\d{2}-\d{2}
```

---

### Exercise 6 ⭐

এই hex colors validate করো:

```text
#FFFFFF
#12AB90
#XYZ123
#12345
```

---

### Exercise 7 🔥

এই function লিখো:

```python
def is_valid_username(username):
    ...
```

Rules:

```text
3–20 characters
English letters
numbers
underscore
```

---

### Exercise 8 🔥🔥

নিজের ভাষায় explain করো:

```python
re.match(r"\d+", "123abc")
```

কেন match হয়?

এবং:

```python
re.fullmatch(r"\d+", "123abc")
```

কেন match হয় না?

---

## 🎯 Day 7-এর Final Concept

```text
re.search()
    ↓
যেকোনো জায়গায় প্রথম match

re.match()
    ↓
শুরু থেকে প্রথম match

re.fullmatch()
    ↓
পুরো string match

re.findall()
    ↓
সব match
```

**আজ থেকে Regex-কে শুধু text search হিসেবে না দেখে input validation tool হিসেবেও ভাববে।**

**Day 8-এ আমরা `re.findall()` শিখব—একটি text থেকে সব matching data কীভাবে বের করতে হয়।**


# 🐍 Python `re` Module — Day 8

## 🎯 `re.findall()` — সব Match একসাথে বের করা

আজকের মূল বিষয়:

```python
re.findall()
```

এটা Regex-এর **data extraction**-এর জন্য খুব গুরুত্বপূর্ণ।

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `re.findall()` কী?

`re.findall()` একটি string-এর মধ্যে pattern-এর **সব non-overlapping match** খুঁজে একটি list হিসেবে return করে।

Syntax:

```python
re.findall(pattern, string)
```

Example:

```python
import re

text = "I have 10 apples and 20 oranges."

result = re.findall(r"\d+", text)

print(result)
```

Output:

```text
['10', '20']
```

---

# 2️⃣ `search()` বনাম `findall()` ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

```python
text = "10 apples, 20 oranges, 30 bananas"
```

### `search()`

```python
result = re.search(r"\d+", text)

print(result.group())
```

Output:

```text
10
```

শুধু **প্রথম match**।

### `findall()`

```python
result = re.findall(r"\d+", text)

print(result)
```

Output:

```text
['10', '20', '30']
```

অর্থাৎ:

```text
search()
   ↓
first match

findall()
   ↓
all matches
```

---

# 3️⃣ সব Words বের করা

```python
text = "Python is easy"

words = re.findall(
    r"\w+",
    text
)

print(words)
```

Output:

```text
['Python', 'is', 'easy']
```

---

# 4️⃣ শুধু Numbers

```python
text = "My marks are 80, 75 and 90."

numbers = re.findall(
    r"\d+",
    text
)

print(numbers)
```

Output:

```text
['80', '75', '90']
```

---

# 5️⃣ শুধু English Words

```python
text = "Python is very powerful"

words = re.findall(
    r"[A-Za-z]+",
    text
)

print(words)
```

Output:

```text
['Python', 'is', 'very', 'powerful']
```

---

# 6️⃣ Word Boundary ব্যবহার

ধরো:

```python
text = "Python Pythonic Python"
```

যদি:

```python
re.findall(r"Python", text)
```

দাও:

```text
['Python', 'Python', 'Python']
```

এখানে `Pythonic`-এর ভিতরের `Python`-ও match হয়েছে।

কিন্তু:

```python
re.findall(r"\bPython\b", text)
```

Output:

```text
['Python', 'Python']
```

কারণ `Pythonic` standalone `Python` নয়।

---

# 7️⃣ Email Extract করা ⭐⭐⭐

ধরো:

```python
text = """
Contact: user1@example.com
Support: help@example.org
Admin: admin@test.net
"""
```

Pattern:

```python
pattern = r"[\w.-]+@[\w.-]+\.\w+"
```

তারপর:

```python
emails = re.findall(
    pattern,
    text
)

print(emails)
```

Output:

```text
['user1@example.com', 'help@example.org', 'admin@test.net']
```

এটাই real-world data extraction-এর উদাহরণ।

---

# 8️⃣ Phone Number Extract

```python
text = """
Call 01712345678
or 01812345678
or 01912345678
"""
```

Pattern:

```python
pattern = r"01\d{9}"
```

তারপর:

```python
phones = re.findall(
    pattern,
    text
)

print(phones)
```

Output:

```text
['01712345678', '01812345678', '01912345678']
```

---

# 9️⃣ Date Extract

Text:

```python
text = """
Meeting: 2026-08-17
Deadline: 2026-08-25
Exam: 2026-09-01
"""
```

Regex:

```python
dates = re.findall(
    r"\d{4}-\d{2}-\d{2}",
    text
)

print(dates)
```

Output:

```text
['2026-08-17', '2026-08-25', '2026-09-01']
```

---

# 🔟 URL Extract

```python
text = """
Visit https://example.com
and https://python.org
"""
```

Basic pattern:

```python
urls = re.findall(
    r"https?://\S+",
    text
)

print(urls)
```

Output:

```text
['https://example.com', 'https://python.org']
```

---

# 1️⃣1️⃣ Hashtag Extract

```python
text = """
#Python #Programming #Django
"""
```

Pattern:

```python
hashtags = re.findall(
    r"#\w+",
    text
)

print(hashtags)
```

Output:

```text
['#Python', '#Programming', '#Django']
```

---

# 1️⃣2️⃣ Mentions Extract

```python
text = """
Hello @atiar
@python
@developer
"""
```

Pattern:

```python
mentions = re.findall(
    r"@\w+",
    text
)

print(mentions)
```

Output:

```text
['@atiar', '@python', '@developer']
```

---

# 1️⃣3️⃣ Decimal Numbers

ধরো:

```python
text = "Prices: 10.50, 25.75, 100.00"
```

Pattern:

```python
numbers = re.findall(
    r"\d+\.\d+",
    text
)

print(numbers)
```

Output:

```text
['10.50', '25.75', '100.00']
```

---

# 1️⃣4️⃣ Integer + Decimal দুটোই

```python
text = "Values: 10, 20.5, 30, 40.75"
```

Pattern:

```python
r"\d+(?:\.\d+)?"
```

এটা একটু advanced।

Output:

```text
['10', '20.5', '30', '40.75']
```

এখানে `(?:...)` হলো **non-capturing group**।

এটা আমরা পরে বিস্তারিত শিখব।

---

# 1️⃣5️⃣ `findall()` + Groups ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```python
text = "Age: 25, Age: 30"
```

Pattern:

```python
r"Age:\s*(\d+)"
```

তারপর:

```python
ages = re.findall(
    r"Age:\s*(\d+)",
    text
)

print(ages)
```

Output:

```text
['25', '30']
```

কারণ capturing group:

```python
(\d+)
```

match-এর ভিতরের number বের করছে।

---

# 1️⃣6️⃣ Multiple Groups

ধরো:

```python
text = """
Name: Atiar, Age: 25
Name: Rahim, Age: 30
"""
```

Pattern:

```python
pattern = r"Name:\s*(\w+),\s*Age:\s*(\d+)"
```

তারপর:

```python
result = re.findall(
    pattern,
    text
)

print(result)
```

Output:

```text
[
    ('Atiar', '25'),
    ('Rahim', '30')
]
```

অর্থাৎ multiple capturing groups থাকলে `findall()` tuple-এর list দিতে পারে।

---

# 1️⃣7️⃣ No Capturing Group

```python
re.findall(
    r"\d+",
    "10 20 30"
)
```

Output:

```text
['10', '20', '30']
```

---

# 1️⃣8️⃣ One Capturing Group

```python
re.findall(
    r"Age:\s*(\d+)",
    "Age: 25 Age: 30"
)
```

Output:

```text
['25', '30']
```

---

# 1️⃣9️⃣ Two Capturing Groups

```python
re.findall(
    r"(\w+)=(\d+)",
    "age=25 score=90"
)
```

Output:

```text
[
    ('age', '25'),
    ('score', '90')
]
```

এটা data extraction-এর জন্য অনেক useful।

---

# 2️⃣0️⃣ Dictionary-like Data Extract 🔥

Text:

```python
text = "name=Atiar age=25 city=Dhaka"
```

Pattern:

```python
pairs = re.findall(
    r"(\w+)=([A-Za-z0-9]+)",
    text
)

print(pairs)
```

Output:

```text
[
    ('name', 'Atiar'),
    ('age', '25'),
    ('city', 'Dhaka')
]
```

তারপর:

```python
data = dict(pairs)

print(data)
```

Output:

```python
{
    'name': 'Atiar',
    'age': '25',
    'city': 'Dhaka'
}
```

🔥 Regex দিয়ে semi-structured text parse করার একটা simple example।

---

# 2️⃣1️⃣ Log Parsing 🔥🔥

ধরো server log:

```python
text = """
2026-08-17 INFO Server started
2026-08-17 ERROR Database failed
2026-08-17 WARNING CPU high
"""
```

সব log levels:

```python
levels = re.findall(
    r"\b(INFO|ERROR|WARNING)\b",
    text
)

print(levels)
```

Output:

```text
['INFO', 'ERROR', 'WARNING']
```

---

# 2️⃣2️⃣ Log থেকে Dates

```python
dates = re.findall(
    r"\d{4}-\d{2}-\d{2}",
    text
)

print(dates)
```

Output:

```text
[
    '2026-08-17',
    '2026-08-17',
    '2026-08-17'
]
```

---

# 2️⃣3️⃣ Log থেকে Error Lines

যদি line-by-line pattern ব্যবহার করি:

```python
errors = re.findall(
    r".*ERROR.*",
    text
)

print(errors)
```

Output concept:

```text
['2026-08-17 ERROR Database failed']
```

`re.MULTILINE` ও `re.DOTALL` পরে বিস্তারিত করব।

---

# 2️⃣4️⃣ Case-insensitive Search

ধরো:

```python
text = "Python PYTHON python PyThOn"
```

Normal:

```python
re.findall(
    r"python",
    text
)
```

Output:

```text
['python']
```

`re.IGNORECASE` ব্যবহার করলে:

```python
re.findall(
    r"python",
    text,
    re.IGNORECASE
)
```

Output:

```text
['Python', 'PYTHON', 'python', 'PyThOn']
```

---

# 2️⃣5️⃣ `findall()` vs `finditer()` ⭐

আজ শুধু basic idea।

### `findall()`

```python
re.findall(r"\d+", "10 20 30")
```

দেয়:

```text
['10', '20', '30']
```

### `finditer()`

```python
re.finditer(r"\d+", "10 20 30")
```

Match objects-এর iterator দেয়।

যখন position, span, group ইত্যাদি দরকার হবে, `finditer()` বেশি useful।

এটা পরের lessons-এ বিস্তারিত করব।

---

# 2️⃣6️⃣ `findall()` সবসময় string list দেয় না

এটা গুরুত্বপূর্ণ।

### No group:

```python
re.findall(
    r"\d+",
    "10 20"
)
```

→

```text
['10', '20']
```

### One group:

```python
re.findall(
    r"Age:(\d+)",
    "Age:25 Age:30"
)
```

→

```text
['25', '30']
```

### Multiple groups:

```python
re.findall(
    r"(\w+)=(\d+)",
    "age=25 score=90"
)
```

→

```text
[('age', '25'), ('score', '90')]
```

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ Rule

```text
No capturing group
        ↓
list[str]

1 capturing group
        ↓
list[str]

2+ capturing groups
        ↓
list[tuple]
```

---

# ⭐ Day 8 Cheat Sheet

|কাজ|Pattern|
|---|---|
|সব numbers|`\d+`|
|সব words|`\w+`|
|সব emails|`[\w.-]+@[\w.-]+\.\w+`|
|সব phone|`01\d{9}`|
|সব dates|`\d{4}-\d{2}-\d{2}`|
|সব hashtags|`#\w+`|
|সব mentions|`@\w+`|
|সব URLs|`https?://\S+`|
|সব uppercase letters|`[A-Z]+`|
|সব lowercase letters|`[a-z]+`|

---

# 🧪 Day 8 Practice

### Exercise 1

এই text থেকে সব numbers বের করো:

```python
text = "I have 10 books, 20 pens and 30 pencils."
```

Expected:

```text
['10', '20', '30']
```

---

### Exercise 2

সব email বের করো:

```python
text = """
admin@example.com
support@test.org
user@gmail.com
"""
```

---

### Exercise 3

সব phone number বের করো:

```python
text = """
01712345678
01812345678
01912345678
"""
```

---

### Exercise 4 ⭐

এই text থেকে সব standalone `Python` বের করো:

```python
text = "Python Pythonic Python python"
```

শুধু exact `Python` চাই।

---

### Exercise 5 ⭐

এই text থেকে সব dates বের করো:

```python
text = """
2026-08-17
2026-08-20
2026-09-01
"""
```

---

### Exercise 6 ⭐

এই data থেকে key-value pairs বের করো:

```python
text = "name=Atiar age=25 city=Dhaka"
```

Expected:

```python
[
    ('name', 'Atiar'),
    ('age', '25'),
    ('city', 'Dhaka')
]
```

---

### Exercise 7 🔥

এই log থেকে সব log level বের করো:

```python
text = """
INFO Server started
ERROR Database failed
WARNING CPU high
INFO Server running
"""
```

Expected:

```text
['INFO', 'ERROR', 'WARNING', 'INFO']
```

---

### Exercise 8 🔥🔥

এই text থেকে **name + age** বের করো:

```python
text = """
Name: Atiar, Age: 25
Name: Rahim, Age: 30
Name: Karim, Age: 28
"""
```

Expected:

```python
[
    ('Atiar', '25'),
    ('Rahim', '30'),
    ('Karim', '28')
]
```

---

# 🎯 Day 8 Final Concept

আজকের মূল flow:

```text
TEXT
 ↓
re.findall()
 ↓
সব matching অংশ
 ↓
Python list
```

আর groups থাকলে:

```text
findall()
   ↓
1 group     → strings
2+ groups   → tuples
```

**Day 9-এ `re.finditer()` শিখব — একই সাথে সব match বের করে প্রতিটির `group()`, `start()`, `end()`, `span()` কীভাবে পাওয়া যায়।**



# 🐍 Python `re` Module — Day 9

## 🎯 `re.finditer()` — সব Match + Position বের করা

আজকের topic:

```python
re.finditer()
```

এটা `findall()`-এর মতো **সব match খুঁজে বের করে**, কিন্তু result হিসেবে **Match objects-এর iterator** দেয়।

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `finditer()` কী?

```python
import re

text = "I have 10 apples and 20 oranges."

matches = re.finditer(
    r"\d+",
    text
)

for match in matches:
    print(match.group())
```

Output:

```text
10
20
```

কিন্তু `findall()` থেকে গুরুত্বপূর্ণ পার্থক্য হলো—`finditer()` প্রতিটি match-এর **position**-ও দিতে পারে।

---

# 2️⃣ `findall()` বনাম `finditer()` ⭐⭐⭐

### `findall()`

```python
text = "10 apples, 20 oranges"

result = re.findall(
    r"\d+",
    text
)

print(result)
```

Output:

```text
['10', '20']
```

### `finditer()`

```python
matches = re.finditer(
    r"\d+",
    text
)

for match in matches:
    print(match.group())
    print(match.start())
    print(match.end())
```

এখানে প্রতিটি match-এর location-ও পাওয়া যাবে।

---

# 3️⃣ `group()`

```python
text = "Python 123 Django 456"

for match in re.finditer(
    r"\d+",
    text
):
    print(match.group())
```

Output:

```text
123
456
```

`group()` = matched text।

---

# 4️⃣ `start()`

Match কোথা থেকে শুরু হয়েছে:

```python
text = "Python 123 Django 456"

for match in re.finditer(
    r"\d+",
    text
):
    print(match.start())
```

Output:

```text
7
18
```

---

# 5️⃣ `end()`

```python
for match in re.finditer(
    r"\d+",
    text
):
    print(match.end())
```

Output:

```text
10
21
```

মনে রাখবে:

```text
start() → match-এর প্রথম index
end()   → match-এর শেষ index-এর পরের position
```

---

# 6️⃣ `span()` ⭐⭐⭐

`start()` এবং `end()` একসাথে:

```python
for match in re.finditer(
    r"\d+",
    text
):
    print(match.span())
```

Output:

```text
(7, 10)
(18, 21)
```

---

# 7️⃣ `group() + start() + end() + span()`

একসাথে:

```python
import re

text = "Python 123 Django 456"

for match in re.finditer(
    r"\d+",
    text
):
    print("Value:", match.group())
    print("Start:", match.start())
    print("End:", match.end())
    print("Span:", match.span())
    print()
```

Output:

```text
Value: 123
Start: 7
End: 10
Span: (7, 10)

Value: 456
Start: 18
End: 21
Span: (18, 21)
```

---

# 8️⃣ কেন `finditer()` দরকার?

ধরো text:

```text
I bought 10 apples and 20 oranges.
```

তুমি শুধু number চাও না।

তুমি জানতে চাও:

```text
10 কোথায়?
20 কোথায়?
```

তাহলে:

```python
for match in re.finditer(r"\d+", text):
    print(
        match.group(),
        match.span()
    )
```

Output:

```text
10 (9, 11)
20 (24, 26)
```

এটা text processing-এর জন্য খুব useful।

---

# 9️⃣ Real Example — Highlight Position

```python
text = "Python is easy and Python is powerful"

for match in re.finditer(
    r"\bPython\b",
    text
):
    print(
        "Found:",
        match.group(),
        "at:",
        match.span()
    )
```

Output concept:

```text
Found: Python at: (0, 6)
Found: Python at: (19, 25)
```

---

# 🔟 Email Extraction + Position 🔥

```python
text = """
Contact user@example.com
Support help@test.org
Admin admin@gmail.com
"""
```

Pattern:

```python
pattern = r"[\w.-]+@[\w.-]+\.\w+"
```

Code:

```python
for match in re.finditer(
    pattern,
    text
):
    print(
        match.group(),
        match.span()
    )
```

Output concept:

```text
user@example.com (9, 25)
help@test.org (...)
admin@gmail.com (...)
```

এখানে তুমি **email + location** দুটোই পাচ্ছ।

---

# 1️⃣1️⃣ Phone Number + Position

```python
text = """
Call 01712345678
or 01812345678
"""
```

```python
for match in re.finditer(
    r"01\d{9}",
    text
):
    print(
        "Phone:",
        match.group()
    )

    print(
        "Position:",
        match.span()
    )
```

এটা log processing, document processing ইত্যাদিতে কাজে লাগে।

---

# 1️⃣2️⃣ Groups সহ `finditer()` ⭐⭐⭐

Day 8-এ আমরা group দেখেছিলাম।

ধরো:

```python
text = """
Name: Atiar, Age: 25
Name: Rahim, Age: 30
"""
```

Pattern:

```python
pattern = r"Name:\s*(\w+),\s*Age:\s*(\d+)"
```

তারপর:

```python
for match in re.finditer(
    pattern,
    text
):
    print("Full:", match.group())
    print("Name:", match.group(1))
    print("Age:", match.group(2))
```

Output:

```text
Full: Name: Atiar, Age: 25
Name: Atiar
Age: 25

Full: Name: Rahim, Age: 30
Name: Rahim
Age: 30
```

---

# 1️⃣3️⃣ `group(0)`

`group(0)` সাধারণত পুরো match বোঝায়।

```python
text = "Age: 25"

match = re.search(
    r"Age:\s*(\d+)",
    text
)

print(match.group(0))
print(match.group(1))
```

Output:

```text
Age: 25
25
```

অর্থাৎ:

```text
group(0)
↓
পুরো match

group(1)
↓
প্রথম capturing group
```

---

# 1️⃣4️⃣ Multiple Groups

```python
text = """
Product: Laptop, Price: 50000
Product: Mouse, Price: 1000
"""
```

Pattern:

```python
pattern = r"Product:\s*(.*?),\s*Price:\s*(\d+)"
```

Code:

```python
for match in re.finditer(
    pattern,
    text
):
    print("Product:", match.group(1))
    print("Price:", match.group(2))
```

Output:

```text
Product: Laptop
Price: 50000

Product: Mouse
Price: 1000
```

---

# 1️⃣5️⃣ `finditer()` দিয়ে Dictionary বানানো 🔥

```python
text = "name=Atiar age=25 city=Dhaka"

pattern = r"(\w+)=([A-Za-z0-9]+)"

data = {}

for match in re.finditer(
    pattern,
    text
):
    key = match.group(1)
    value = match.group(2)

    data[key] = value

print(data)
```

Output:

```python
{
    'name': 'Atiar',
    'age': '25',
    'city': 'Dhaka'
}
```

---

# 1️⃣6️⃣ Log Parsing 🔥🔥

ধরো:

```python
logs = """
2026-08-17 INFO Server started
2026-08-17 ERROR Database failed
2026-08-17 WARNING CPU high
"""
```

Pattern:

```python
pattern = r"(\d{4}-\d{2}-\d{2})\s+(INFO|ERROR|WARNING)\s+(.*)"
```

তারপর:

```python
for match in re.finditer(
    pattern,
    logs
):
    date = match.group(1)
    level = match.group(2)
    message = match.group(3)

    print("Date:", date)
    print("Level:", level)
    print("Message:", message)
    print()
```

এটা একটি ছোট **log parser**-এর মতো কাজ করছে।

---

# 1️⃣7️⃣ `finditer()` vs `findall()` কখন?

|Requirement|Function|
|---|---|
|শুধু matched values|`findall()`|
|সব match + position|`finditer()`|
|groups + position|`finditer()`|
|প্রথম match|`search()`|
|শুরু থেকে match|`match()`|
|পুরো string validation|`fullmatch()`|

---

# 1️⃣8️⃣ Memory Efficiency

`findall()` সাধারণত সব result-এর list তৈরি করে:

```python
matches = re.findall(...)
```

`finditer()` iterator দেয়:

```python
matches = re.finditer(...)
```

তারপর একে একে process করতে পারো:

```python
for match in matches:
    ...
```

তাই **বড় text বা বড় dataset processing-এর ক্ষেত্রে `finditer()` অনেক সময় বেশি উপযোগী**।

তবে exact memory behavior/optimization context-এর ওপর নির্ভর করে—শুধু "finditer সবসময় faster" এমন নিয়ম নেই।

---

# 1️⃣9️⃣ `finditer()` Empty Matches

Regex এমন pattern-ও তৈরি করতে পারে যা empty string match করে:

```python
matches = re.finditer(
    r"\b",
    "Python"
)

for match in matches:
    print(match.span())
```

এখানে word boundaries-এর মতো zero-length matches পাওয়া যেতে পারে।

এটা advanced topic, তাই আপাতত শুধু মনে রাখো:

> Regex match সবসময় character consume করে এমন নয়।

---

# 2️⃣0️⃣ Compiled Pattern-এর সাথে

আগামী lessons-এ `re.compile()` বিস্তারিত করব।

Basic idea:

```python
pattern = re.compile(r"\d+")

for match in pattern.finditer(
    "10 20 30"
):
    print(match.group())
```

Output:

```text
10
20
30
```

Repeatedly একই regex ব্যবহার করলে compiled pattern useful হতে পারে।

---

# 🧠 আজকের Mental Model

```text
TEXT
 ↓
finditer()
 ↓
Match 1 → group/start/end/span
 ↓
Match 2 → group/start/end/span
 ↓
Match 3 → group/start/end/span
```

---

# ⭐ Day 9 Cheat Sheet

```python
match.group()
```

→ matched text

```python
match.group(1)
```

→ first captured group

```python
match.start()
```

→ starting position

```python
match.end()
```

→ ending position

```python
match.span()
```

→ `(start, end)`

---

# 🧪 Day 9 Practice

### Exercise 1

এই text থেকে সব numbers বের করো এবং তাদের position দেখাও:

```python
text = "I have 10 books and 20 pens."
```

Expected concept:

```text
10 → position
20 → position
```

---

### Exercise 2

সব email এবং তাদের position বের করো:

```python
text = """
admin@example.com
support@test.org
user@gmail.com
"""
```

---

### Exercise 3 ⭐

এই text থেকে সব standalone `Python` বের করো এবং `span()` দেখাও:

```python
text = "Python is easy. Python is powerful."
```

---

### Exercise 4 ⭐

এই data parse করো:

```python
text = "name=Atiar age=25 city=Dhaka"
```

প্রতিটি:

```text
key
value
position
```

print করো।

---

### Exercise 5 🔥

এই log parse করো:

```python
logs = """
2026-08-17 INFO Server started
2026-08-17 ERROR Database failed
2026-08-17 WARNING CPU high
"""
```

প্রতিটি line থেকে বের করো:

```text
Date
Level
Message
```

---

### Exercise 6 🔥🔥

এই pattern-এর প্রতিটি অংশ explain করো:

```python
r"Name:\s*(\w+),\s*Age:\s*(\d+)"
```

বিশেষ করে:

```text
\s*
(\w+)
(\d+)
```

---

# 🎯 Day 9-এর Final Concept

আজ তোমার মাথায় এই চারটি function-এর পার্থক্য পরিষ্কার থাকা উচিত:

```text
search()
   ↓
প্রথম match

match()
   ↓
শুরু থেকে প্রথম match

fullmatch()
   ↓
পুরো string

findall()
   ↓
সব match → list

finditer()
   ↓
সব match → Match objects
                 ↓
          group/start/end/span
```

**Day 10-এ আমরা `re.split()` এবং `re.sub()` শিখব—Regex দিয়ে text কীভাবে split এবং replace/clean করা যায়।**

# 🐍 Python `re` Module — Day 10

## 🎯 `re.split()` + `re.sub()` — Text Split & Replace

আজ আমরা `re` module-এর আরও দুইটি গুরুত্বপূর্ণ function শিখব:

```python
re.split()
re.sub()
```

এগুলো দিয়ে **text clean, transform, format এবং preprocess** করা যায়।

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# Part 1 — `re.split()`

## 1️⃣ `re.split()` কী?

Normal Python:

```python
text.split(",")
```

একটি নির্দিষ্ট separator দিয়ে split করে।

কিন্তু `re.split()` দিয়ে **regex pattern অনুযায়ী split** করা যায়।

Syntax:

```python
re.split(pattern, string)
```

---

## 2️⃣ Basic Example

```python
import re

text = "apple,banana,orange"

result = re.split(
    r",",
    text
)

print(result)
```

Output:

```text
['apple', 'banana', 'orange']
```

---

# 3️⃣ Multiple Separators ⭐⭐⭐

ধরো text:

```python
text = "apple,banana;orange|mango"
```

Separator তিনটি:

```text
,
;
|
```

একসাথে:

```python
result = re.split(
    r"[,;|]",
    text
)

print(result)
```

Output:

```text
['apple', 'banana', 'orange', 'mango']
```

এটাই `re.split()`-এর বড় সুবিধা।

---

# 4️⃣ Space দিয়ে Split

```python
text = "Python is very powerful"

result = re.split(
    r"\s+",
    text
)

print(result)
```

Output:

```text
['Python', 'is', 'very', 'powerful']
```

এখানে:

```text
\s+
```

মানে:

> এক বা একাধিক whitespace।

---

# 5️⃣ Multiple Spaces

```python
text = "Python    is   easy"
```

যদি:

```python
text.split(" ")
```

ব্যবহার করো, তাহলে অনেক empty item আসতে পারে।

Regex:

```python
result = re.split(
    r"\s+",
    text
)

print(result)
```

Output:

```text
['Python', 'is', 'easy']
```

---

# 6️⃣ Comma + Space

```python
text = "Python, Django, React, Next.js"
```

```python
result = re.split(
    r",\s*",
    text
)

print(result)
```

Output:

```text
['Python', 'Django', 'React', 'Next.js']
```

এখানে:

```text
,
```

comma এবং

```text
\s*
```

zero বা more spaces match করছে।

---

# 7️⃣ Newline দিয়ে Split

```python
text = """Python
Django
React
Next.js"""
```

```python
result = re.split(
    r"\n",
    text
)

print(result)
```

Output:

```text
['Python', 'Django', 'React', 'Next.js']
```

---

# 8️⃣ `\s+` দিয়ে Newline + Space দুটোই

```python
text = "Python\nDjango\tReact Next.js"
```

```python
result = re.split(
    r"\s+",
    text
)

print(result)
```

Output:

```text
['Python', 'Django', 'React', 'Next.js']
```

---

# 9️⃣ `maxsplit`

`re.split()`-এ কতবার split হবে সেটাও control করা যায়।

Syntax:

```python
re.split(pattern, string, maxsplit=...)
```

Example:

```python
text = "a-b-c-d-e"

result = re.split(
    r"-",
    text,
    maxsplit=2
)

print(result)
```

Output:

```text
['a', 'b', 'c-d-e']
```

অর্থাৎ প্রথম দুইবার split হয়েছে।

---

# 🔟 Capturing Group ব্যবহার করলে কী হয়?

এটা গুরুত্বপূর্ণ।

```python
text = "apple,banana;orange"
```

যদি:

```python
result = re.split(
    r"([,;])",
    text
)

print(result)
```

তাহলে separator-ও result-এর মধ্যে থাকবে:

```text
['apple', ',', 'banana', ';', 'orange']
```

কারণ:

```python
([,;])
```

এটা capturing group।

---

# 🧠 `re.split()` Mental Model

```text
TEXT
 ↓
pattern খুঁজে
 ↓
যেখানে pattern পাওয়া যায়
 ↓
সেখানে text কেটে দেয়
 ↓
LIST
```

---

# Part 2 — `re.sub()`

## 1️⃣1️⃣ `re.sub()` কী?

`re.sub()` দিয়ে regex অনুযায়ী text **replace** করা যায়।

Syntax:

```python
re.sub(pattern, replacement, string)
```

Example:

```python
import re

text = "I love Python"

result = re.sub(
    r"Python",
    "Django",
    text
)

print(result)
```

Output:

```text
I love Django
```

---

# 1️⃣2️⃣ সব Match Replace হয় ⭐⭐⭐

```python
text = "Python Python Python"

result = re.sub(
    r"Python",
    "Java",
    text
)

print(result)
```

Output:

```text
Java Java Java
```

`re.sub()` defaultভাবে **সব matching occurrence replace করে**।

---

# 1️⃣3️⃣ শুধু Number Replace

```python
text = "My age is 25"

result = re.sub(
    r"\d+",
    "XX",
    text
)

print(result)
```

Output:

```text
My age is XX
```

---

# 1️⃣4️⃣ সব Numbers Hide করা

```python
text = "My phone is 01712345678"

result = re.sub(
    r"\d",
    "*",
    text
)

print(result)
```

Output:

```text
My phone is ***********
```

এটা sensitive data masking-এর basic example।

---

# 1️⃣5️⃣ Multiple Spaces → One Space ⭐⭐⭐

Text cleaning-এ খুব common:

```python
text = "Python    is     very   easy"
```

```python
cleaned = re.sub(
    r"\s+",
    " ",
    text
)

print(cleaned)
```

Output:

```text
Python is very easy
```

🔥 NLP/data preprocessing-এ এই ধরনের operation খুব common।

---

# 1️⃣6️⃣ Extra Spaces Remove

ধরো:

```python
text = "   Python is easy   "
```

`re.sub()` দিয়ে internal whitespace normalize করা যায়:

```python
cleaned = re.sub(
    r"\s+",
    " ",
    text
).strip()

print(cleaned)
```

Output:

```text
Python is easy
```

---

# 1️⃣7️⃣ Punctuation Remove

```python
text = "Hello, Python! How are you?"

cleaned = re.sub(
    r"[^\w\s]",
    "",
    text
)

print(cleaned)
```

Output:

```text
Hello Python How are you
```

এখানে:

```text
[^\w\s]
```

মানে:

> word character অথবা whitespace নয়—এমন character।

অর্থাৎ punctuation remove হচ্ছে।

---

# 1️⃣8️⃣ শুধু Letters এবং Spaces রাখা

```python
text = "Hello123, Python!"

cleaned = re.sub(
    r"[^A-Za-z\s]",
    "",
    text
)

print(cleaned)
```

Output:

```text
Hello Python
```

---

# 1️⃣9️⃣ HTML Tag Remove 🔥

ধরো:

```python
text = "<p>Hello</p><b>Python</b>"
```

Basic example:

```python
cleaned = re.sub(
    r"<[^>]+>",
    "",
    text
)

print(cleaned)
```

Output:

```text
HelloPython
```

Space রাখতে চাইলে:

```python
cleaned = re.sub(
    r"<[^>]+>",
    " ",
    text
)

print(cleaned)
```

Output:

```text
 Hello Python 
```

তারপর:

```python
cleaned = re.sub(
    r"\s+",
    " ",
    cleaned
).strip()
```

Result:

```text
Hello Python
```

⚠️ Real HTML parsing-এর জন্য regex-এর বদলে HTML parser ব্যবহার করা বেশি নিরাপদ।

---

# 2️⃣0️⃣ Case Replacement

```python
text = "python PYTHON Python"

result = re.sub(
    r"python",
    "Django",
    text,
    flags=re.IGNORECASE
)

print(result)
```

Output:

```text
Django Django Django
```

---

# 2️⃣1️⃣ `count` / সীমিত Replacement ⭐⭐⭐

`re.sub()`-এর fourth positional argument হিসেবে count দেওয়া যায়।

```python
text = "Python Python Python"

result = re.sub(
    r"Python",
    "Django",
    text,
    count=1
)

print(result)
```

Output:

```text
Django Python Python
```

অর্থাৎ শুধু প্রথম match replace হয়েছে।

---

# 2️⃣2️⃣ `re.sub()` + Capturing Groups

ধরো:

```python
text = "John Smith"
```

আমরা order পরিবর্তন করতে চাই:

```text
John Smith
↓
Smith, John
```

Pattern:

```python
r"(\w+)\s+(\w+)"
```

Replacement:

```python
r"\2, \1"
```

Code:

```python
result = re.sub(
    r"(\w+)\s+(\w+)",
    r"\2, \1",
    text
)

print(result)
```

Output:

```text
Smith, John
```

এখানে:

```text
\1 → John
\2 → Smith
```

---

# 2️⃣3️⃣ `re.sub()` + Function 🔥🔥

Replacement হিসেবে function-ও ব্যবহার করা যায়।

Example:

```python
import re

text = "10 20 30"

def double(match):
    number = int(match.group())
    return str(number * 2)

result = re.sub(
    r"\d+",
    double,
    text
)

print(result)
```

Output:

```text
20 40 60
```

এটা অনেক powerful।

---

# 2️⃣4️⃣ Function কেন useful?

কারণ replacement সব জায়গায় একই হবে না।

Example:

```text
10 → 20
20 → 40
30 → 60
```

এখানে:

```text
replacement = fixed text
```

দিলে হবে না।

Function দিয়ে:

```text
matched value
      ↓
process
      ↓
new value
```

---

# 2️⃣5️⃣ Text Normalization 🔥

একটি realistic example:

```python
text = """
Hello,     Python!!!
Python is    very useful.
"""
```

প্রথমে punctuation:

```python
text = re.sub(
    r"[^\w\s]",
    "",
    text
)
```

তারপর multiple spaces:

```python
text = re.sub(
    r"\s+",
    " ",
    text
)
```

তারপর:

```python
text = text.strip()
```

Final:

```text
Hello Python Python is very useful
```

---

# 2️⃣6️⃣ `split()` + `sub()` একসাথে 🔥

ধরো:

```python
text = "Python,   Django; React | Next.js"
```

প্রথমে separators normalize:

```python
text = re.sub(
    r"\s*[,;|]\s*",
    ",",
    text
)
```

Result:

```text
Python,Django,React,Next.js
```

তারপর:

```python
items = re.split(
    r",",
    text
)

print(items)
```

Output:

```text
['Python', 'Django', 'React', 'Next.js']
```

---

# 2️⃣7️⃣ `re.sub()` vs `str.replace()`

### Simple fixed replacement:

```python
text.replace("Python", "Django")
```

এটাই সহজ।

### Regex দরকার হলে:

```python
re.sub(r"Python\d+", "Django", text)
```

যেমন:

```text
Python123
Python456
Python789
```

সব match করা যাবে।

---

# ⭐ Comparison Table

|Function|কাজ|
|---|---|
|`str.split()`|সাধারণ separator দিয়ে split|
|`re.split()`|Regex দিয়ে split|
|`str.replace()`|সাধারণ fixed replacement|
|`re.sub()`|Regex-based replacement|
|`re.findall()`|সব match → list|
|`re.finditer()`|সব match → Match objects|

---

# 🧠 আজকের Core Concept

### `re.split()`

```text
TEXT
 ↓
PATTERN খুঁজে
 ↓
সেখানে CUT
 ↓
LIST
```

### `re.sub()`

```text
TEXT
 ↓
PATTERN খুঁজে
 ↓
REPLACE
 ↓
NEW TEXT
```

---

# 🧪 Day 10 Practice

### Exercise 1

এই text comma, semicolon এবং pipe দিয়ে split করো:

```python
text = "Python,Django;React|Next.js"
```

Expected:

```python
['Python', 'Django', 'React', 'Next.js']
```

---

### Exercise 2

Multiple spaces একটিতে convert করো:

```python
text = "Python    is     very   easy"
```

Expected:

```text
Python is very easy
```

---

### Exercise 3

সব number `***` দিয়ে replace করো:

```python
text = "My PIN is 1234 and OTP is 567890"
```

Expected concept:

```text
My PIN is **** and OTP is ******
```

---

### Exercise 4 ⭐

সব punctuation remove করো:

```python
text = "Hello, Python! How are you?"
```

---

### Exercise 5 ⭐

এই text থেকে HTML tags remove করো:

```python
text = "<h1>Hello</h1><p>Python is easy</p>"
```

---

### Exercise 6 ⭐

শুধু প্রথম `Python` replace করো:

```python
text = "Python is easy. Python is powerful."
```

Expected:

```text
Django is easy. Python is powerful.
```

---

### Exercise 7 🔥

এই format:

```text
John Smith
Rahim Ahmed
Karim Hasan
```

প্রতিটি নামকে:

```text
Smith, John
Ahmed, Rahim
Hasan, Karim
```

এ convert করো `re.sub()` + capturing groups দিয়ে।

---

### Exercise 8 🔥🔥

এই function complete করো:

```python
def double_numbers(text):
    # every number × 2
    ...
```

Input:

```text
I have 10 apples and 20 oranges.
```

Expected:

```text
I have 20 apples and 40 oranges.
```

---

# 🎯 Day 10 Final Cheat Sheet

```python
re.split(r"\s+", text)
```

→ whitespace দিয়ে split

```python
re.split(r"[,;|]", text)
```

→ multiple separators দিয়ে split

```python
re.sub(r"\s+", " ", text)
```

→ multiple spaces → one space

```python
re.sub(r"\d+", "***", text)
```

→ numbers replace

```python
re.sub(r"[^\w\s]", "", text)
```

→ punctuation remove

```python
re.sub(pattern, replacement, text, count=1)
```

→ শুধু প্রথম match replace

```python
re.sub(pattern, function, text)
```

→ match অনুযায়ী dynamic replacement

---

## 🏆 এখন পর্যন্ত `re` Module

```text
Day 1 → Regex basics
Day 2 → Character classes
Day 3 → Quantifiers
Day 4 → Special characters
Day 5 → Groups / patterns
Day 6 → re.match()
Day 7 → re.fullmatch()
Day 8 → re.findall()
Day 9 → re.finditer()
Day 10 → re.split() + re.sub()
```

**Day 11-এ আমরা `re.compile()` এবং Regex Flags (`IGNORECASE`, `MULTILINE`, `DOTALL`, `VERBOSE`) শিখব।**


# 🐍 Python `re` Module — Day 11

## 🎯 `re.compile()` + Regex Flags

আজকের lesson-এ আমরা শিখব:

1. `re.compile()`
    
2. Compiled Pattern ব্যবহার
    
3. `re.IGNORECASE`
    
4. `re.MULTILINE`
    
5. `re.DOTALL`
    
6. `re.VERBOSE`
    
7. একাধিক flag একসাথে ব্যবহার
    

Official documentation: [Python `re` documentation](https://docs.python.org/3/library/re.html?utm_source=chatgpt.com)

---

# 1️⃣ `re.compile()` কী?

এখন পর্যন্ত আমরা সরাসরি লিখেছি:

```python
re.findall(r"\d+", text)
```

কিন্তু একই pattern বারবার ব্যবহার করতে হলে pattern-টাকে compile করে রাখা যায়:

```python
import re

pattern = re.compile(r"\d+")

result = pattern.findall("I have 10 books and 20 pens")

print(result)
```

Output:

```text
['10', '20']
```

এখানে:

```python
pattern = re.compile(r"\d+")
```

একটি **compiled regex pattern object** তৈরি করেছে।

---

# 2️⃣ Compile করার পর কী কী করা যায়?

Compiled pattern-এর নিজের method আছে:

```python
pattern.search()
pattern.match()
pattern.fullmatch()
pattern.findall()
pattern.finditer()
pattern.split()
pattern.sub()
```

Example:

```python
import re

pattern = re.compile(r"\d+")

print(pattern.search("Age: 25").group())
```

Output:

```text
25
```

---

# 3️⃣ `compile()` কেন ব্যবহার করব?

ধরো একই pattern 100 বার ব্যবহার করতে হবে:

```python
pattern = re.compile(r"\d+")

for text in texts:
    numbers = pattern.findall(text)
```

এতে code পরিষ্কার হয় এবং একই pattern object reuse করা যায়।

### গুরুত্বপূর্ণ:

`re.compile()` মানেই **সবসময় dramatic performance improvement** হবে—এমন নয়। Python internally কিছু recent patterns cache-ও করতে পারে। কিন্তু একই pattern বারবার ব্যবহার করলে compiled pattern **readability এবং reuse-এর জন্য খুব useful**।

---

# 4️⃣ Normal বনাম Compiled

### Normal:

```python
import re

re.findall(r"\d+", "Age 25")
re.findall(r"\d+", "Score 90")
re.findall(r"\d+", "Year 2026")
```

### Compiled:

```python
pattern = re.compile(r"\d+")

pattern.findall("Age 25")
pattern.findall("Score 90")
pattern.findall("Year 2026")
```

দুটোই valid।

---

# 5️⃣ Compiled Pattern + `search()`

```python
pattern = re.compile(r"Python")

text = "I love Python"

match = pattern.search(text)

if match:
    print("Found:", match.group())
```

Output:

```text
Found: Python
```

---

# 6️⃣ Compiled Pattern + `finditer()`

```python
pattern = re.compile(r"\d+")

text = "10 apples, 20 oranges, 30 bananas"

for match in pattern.finditer(text):
    print(match.group(), match.span())
```

Output:

```text
10 (0, 2)
20 (11, 13)
30 (23, 25)
```

---

# 7️⃣ Regex Flags কী?

Flags pattern-এর behavior পরিবর্তন করে।

Example:

```python
re.IGNORECASE
```

এটা regex-কে uppercase/lowercase ignore করতে বলে।

Common flags:

|Flag|কাজ|
|---|---|
|`re.IGNORECASE` / `re.I`|Case ignore|
|`re.MULTILINE` / `re.M`|`^` এবং `$` প্রতিটি line-এ কাজ করায়|
|`re.DOTALL` / `re.S`|`.`-কে newline match করতে দেয়|
|`re.VERBOSE` / `re.X`|Regex-এ whitespace/comment দিয়ে readable pattern|
|`re.ASCII` / `re.A`|কিছু character class-কে ASCII behavior-এ সীমাবদ্ধ করে|
|`re.DOTALL`|`.` newline-সহ match করে|

আজ সবচেয়ে গুরুত্বপূর্ণ চারটি:

```text
I
M
S
X
```

---

# 8️⃣ `re.IGNORECASE`

Case-sensitive:

```python
import re

text = "Python PYTHON python"

result = re.findall(
    r"python",
    text
)

print(result)
```

Output:

```text
['python']
```

কারণ default-এ case-sensitive।

---

## `IGNORECASE`

```python
result = re.findall(
    r"python",
    text,
    re.IGNORECASE
)

print(result)
```

Output:

```text
['Python', 'PYTHON', 'python']
```

---

# 9️⃣ Short Form: `re.I`

এই দুটো equivalent:

```python
re.IGNORECASE
```

এবং:

```python
re.I
```

Example:

```python
pattern = re.compile(
    r"python",
    re.I
)

print(pattern.findall(
    "Python PYTHON python"
))
```

---

# 🔟 Compile + Flag ⭐⭐⭐

এটাই practical style:

```python
pattern = re.compile(
    r"python",
    re.IGNORECASE
)

result = pattern.findall(
    "Python PYTHON python"
)

print(result)
```

---

# 1️⃣1️⃣ `re.MULTILINE`

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```python
text = """ERROR Server failed
INFO Server started
ERROR Database failed"""
```

Pattern:

```python
r"^ERROR"
```

`^` সাধারণত string-এর শুরু বোঝায়।

```python
re.findall(
    r"^ERROR",
    text
)
```

এখানে পুরো string-এর শুরুতেই শুধু একবার check হবে।

---

## `MULTILINE` ব্যবহার

```python
result = re.findall(
    r"^ERROR",
    text,
    re.MULTILINE
)

print(result)
```

Output:

```text
['ERROR', 'ERROR']
```

কারণ `MULTILINE` থাকলে:

```text
^
```

প্রতিটি line-এর beginning-এ কাজ করতে পারে।

---

# 1️⃣2️⃣ `^` + `MULTILINE`

ধরো:

```text
ERROR Server failed
INFO Server started
ERROR Database failed
```

Pattern:

```python
r"^ERROR"
```

`MULTILINE` ছাড়া:

```text
string-এর শুরু
      ↓
ERROR
```

`MULTILINE` সহ:

```text
line 1 → ERROR ✅
line 2 → INFO
line 3 → ERROR ✅
```

---

# 1️⃣3️⃣ `$` + `MULTILINE`

একইভাবে `$` line-এর ending-এ কাজ করতে পারে।

```python
text = """Python
Django
Python"""
```

```python
result = re.findall(
    r"Python$",
    text,
    re.MULTILINE
)

print(result)
```

Output:

```text
['Python', 'Python']
```

কারণ দুইটি `Python` line-এর শেষে আছে।

---

# 1️⃣4️⃣ `MULTILINE` সবচেয়ে বেশি কোথায় কাজে লাগে?

বিশেষ করে:

- Log files
    
- Configuration files
    
- Multi-line text
    
- Source code
    
- Documents
    

Example:

```python
log = """
INFO Server started
ERROR Database failed
INFO Server stopped
ERROR Connection failed
"""
```

সব ERROR line:

```python
errors = re.findall(
    r"^ERROR.*$",
    log,
    re.MULTILINE
)

print(errors)
```

---

# 1️⃣5️⃣ `re.DOTALL`

এটা বোঝার জন্য `.` মনে করো:

```text
. = প্রায় যেকোনো character
```

কিন্তু default-এ `.` newline match করে না।

Example:

```python
text = """Hello
Python"""
```

Pattern:

```python
r"Hello.*Python"
```

Default-এ:

```python
re.search(
    r"Hello.*Python",
    text
)
```

❌ match নাও করবে, কারণ `.` newline পার হচ্ছে না।

---

# 1️⃣6️⃣ `DOTALL` ব্যবহার

```python
result = re.search(
    r"Hello.*Python",
    text,
    re.DOTALL
)

print(result.group())
```

Output:

```text
Hello
Python
```

কারণ:

```python
re.DOTALL
```

`.`-কে newline match করতে দেয়।

---

# 1️⃣7️⃣ Short Form

```python
re.DOTALL
```

এর short form:

```python
re.S
```

তাই:

```python
re.search(
    r"Hello.*Python",
    text,
    re.S
)
```

---

# 1️⃣8️⃣ `MULTILINE` বনাম `DOTALL` ⭐⭐⭐

এগুলো গুলিয়ে ফেলবে না।

### `MULTILINE`

মূলত:

```text
^
$
```

এর behavior পরিবর্তন করে।

### `DOTALL`

মূলত:

```text
.
```

এর behavior পরিবর্তন করে।

মনে রাখো:

```text
M → Multiple lines → ^ $
S → Single dot crosses newline → .
```

---

# 1️⃣9️⃣ `re.VERBOSE`

Complex regex readable করার জন্য:

```python
re.VERBOSE
```

অথবা:

```python
re.X
```

Example:

```python
pattern = re.compile(
    r"""
    \d{4}      # year
    -
    \d{2}      # month
    -
    \d{2}      # day
    """,
    re.VERBOSE
)
```

এটা match করবে:

```text
2026-08-17
```

---

# 2️⃣0️⃣ কেন `VERBOSE` দরকার?

এক লাইনে:

```python
r"\d{4}-\d{2}-\d{2}"
```

Pattern ছোট, তাই সমস্যা নেই।

কিন্তু complex regex:

```python
r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})"
```

বড় হলে readable করা কঠিন হতে পারে।

`VERBOSE`:

```python
pattern = re.compile(
    r"""
    (?P<year>\d{4})    # Year
    -
    (?P<month>\d{2})   # Month
    -
    (?P<day>\d{2})     # Day
    """,
    re.VERBOSE
)
```

অনেক পরিষ্কার।

---

# 2️⃣1️⃣ `VERBOSE`-এর গুরুত্বপূর্ণ Rule

`re.VERBOSE` ব্যবহার করলে pattern-এর সাধারণ whitespace ignored হয়।

তাই:

```python
r"""
\d+ \s+ \d+
"""
```

এর whitespace formatting-এর অংশ হিসেবে ব্যবহৃত হচ্ছে না।

Literal space দরকার হলে carefully লিখতে হয়, যেমন:

```python
[ ]
```

অথবা escaped space।

---

# 2️⃣2️⃣ Multiple Flags ⭐⭐⭐

একসাথে একাধিক flag ব্যবহার করা যায়:

```python
re.IGNORECASE | re.MULTILINE
```

Example:

```python
text = """python is easy
PYTHON is powerful
Python is popular"""
```

```python
pattern = re.compile(
    r"^python",
    re.IGNORECASE | re.MULTILINE
)

for match in pattern.finditer(text):
    print(match.group())
```

Output:

```text
python
PYTHON
Python
```

---

# 2️⃣3️⃣ `IGNORECASE + MULTILINE + DOTALL`

প্রয়োজনে:

```python
flags = (
    re.IGNORECASE
    | re.MULTILINE
    | re.DOTALL
)
```

তারপর:

```python
pattern = re.compile(
    r"pattern",
    flags
)
```

---

# 2️⃣4️⃣ Flags compile-এর সময়

```python
pattern = re.compile(
    r"python",
    re.IGNORECASE
)
```

তারপর বারবার:

```python
pattern.findall(text1)
pattern.findall(text2)
pattern.findall(text3)
```

এতে প্রতিবার flag আলাদা করে দিতে হয় না।

---

# 2️⃣5️⃣ Practical Example — Log Parser 🔥

ধরো:

```python
logs = """
ERROR Database failed
INFO Server started
error Connection failed
WARNING CPU high
"""
```

Case ignore + multiline:

```python
pattern = re.compile(
    r"^error.*$",
    re.IGNORECASE | re.MULTILINE
)

for match in pattern.finditer(logs):
    print(match.group())
```

Output:

```text
ERROR Database failed
error Connection failed
```

এখানে:

```text
IGNORECASE
+
MULTILINE
```

দুটো একসাথে কাজ করছে।

---

# 2️⃣6️⃣ Practical Example — Multi-line Block 🔥

Text:

```python
text = """START
Python is a programming language.
It is easy to learn.
END"""
```

ধরো `START` থেকে `END` পর্যন্ত সব content extract করতে চাই।

```python
pattern = re.compile(
    r"START.*?END",
    re.DOTALL
)

match = pattern.search(text)

if match:
    print(match.group())
```

Output:

```text
START
Python is a programming language.
It is easy to learn.
END
```

---

# 2️⃣7️⃣ `DOTALL` + Non-Greedy `.*?`

এখানে:

```python
.*?
```

ব্যবহার করেছি।

কারণ `.*` greedy, আর `.*?` non-greedy।

এটা আমরা পরে আলাদা lesson-এ গভীরভাবে করব।

আজ শুধু মনে রাখো:

```text
.*   → যতটা সম্ভব বেশি নেয়
.*?  → যতটা সম্ভব কম নেয়
```

---

# 2️⃣8️⃣ Compiled Pattern-এর Useful Attributes

Compiled pattern:

```python
pattern = re.compile(
    r"\d+",
    re.IGNORECASE
)
```

তুমি দেখতে পারো:

```python
print(pattern.pattern)
```

Output:

```text
\d+
```

Flags:

```python
print(pattern.flags)
```

এগুলো advanced introspection-এর কাজে লাগতে পারে।

---

# 2️⃣9️⃣ `re.DEBUG`

আরেকটি advanced flag:

```python
re.DEBUG
```

Regex-এর internal compiled representation সম্পর্কে debugging information দেখাতে পারে।

Example:

```python
re.compile(
    r"\d+",
    re.DEBUG
)
```

এটা সাধারণ application code-এ খুব কম লাগে।

Regex complex হলে debugging-এর জন্য useful।

---

# 3️⃣0️⃣ কোন Flag কখন?

|Flag|কখন ব্যবহার করবে|
|---|---|
|`IGNORECASE`|uppercase/lowercase একইভাবে match করতে|
|`MULTILINE`|প্রতিটি line-এর শুরু/শেষে `^ $` ব্যবহার করতে|
|`DOTALL`|`.` দিয়ে newline-সহ text match করতে|
|`VERBOSE`|বড় regex readable করতে|
|`DEBUG`|regex debugging করতে|

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

```text
re.compile()
     ↓
Pattern object তৈরি
```

আর:

```text
re.IGNORECASE
     ↓
case ignore
```

```text
re.MULTILINE
     ↓
^ এবং $ → প্রতিটি line
```

```text
re.DOTALL
     ↓
. → newline-ও match
```

```text
re.VERBOSE
     ↓
complex regex → readable
```

---

# 🧪 Day 11 Practice

## Exercise 1

একটি compiled pattern বানাও:

```python
r"\d+"
```

তারপর এই text থেকে সব number বের করো:

```python
text = "10 apples, 20 oranges, 30 bananas"
```

---

## Exercise 2

Case-insensitive ভাবে `python` খুঁজে বের করো:

```python
text = "Python PYTHON python PyThOn"
```

`re.compile()` ব্যবহার করবে।

---

## Exercise 3 ⭐

এই multiline text:

```python
text = """ERROR Database failed
INFO Server started
ERROR Connection failed
INFO Server stopped"""
```

শুধু `ERROR` দিয়ে শুরু হওয়া lineগুলো বের করো।

Hint:

```python
^ERROR.*$
```

এবং:

```python
re.MULTILINE
```

---

## Exercise 4 ⭐

এই text:

```python
text = """Hello
Python
World"""
```

এই pattern:

```python
r"Hello.*World"
```

প্রথমে `DOTALL` ছাড়া test করো।

তারপর:

```python
re.DOTALL
```

দিয়ে test করো।

Difference explain করো।

---

## Exercise 5 🔥

এই text থেকে case-insensitive `python` দিয়ে শুরু হওয়া সব line বের করো:

```python
text = """Python is easy
Django is powerful
PYTHON is popular
React is useful
python is beginner friendly"""
```

দুটি flag ব্যবহার করো:

```python
re.IGNORECASE | re.MULTILINE
```

---

## Exercise 6 🔥

`VERBOSE` ব্যবহার করে এই date pattern লিখো:

```text
YYYY-MM-DD
```

Rules:

```text
Year  → 4 digits
Month → 2 digits
Day   → 2 digits
```

---

## Exercise 7 🔥🔥

এই text:

```python
text = """START
Python
Django
React
END"""
```

শুধু:

```text
START ... END
```

block-টি বের করো।

Hint:

```python
re.DOTALL
```

---

# 🎯 Day 11 Final Cheat Sheet

### Compile

```python
pattern = re.compile(r"\d+")
```

### Search

```python
pattern.search(text)
```

### Find all

```python
pattern.findall(text)
```

### Find iterator

```python
pattern.finditer(text)
```

### Case insensitive

```python
re.IGNORECASE
# or
re.I
```

### Multi-line

```python
re.MULTILINE
# or
re.M
```

### Dot matches newline

```python
re.DOTALL
# or
re.S
```

### Readable regex

```python
re.VERBOSE
# or
re.X
```

### Multiple flags

```python
re.IGNORECASE | re.MULTILINE
```

---

## 🏆 এখন পর্যন্ত `re` Course

```text
Day 1  → Regex Fundamentals
Day 2  → Character Classes
Day 3  → Quantifiers
Day 4  → Special Characters
Day 5  → Groups & Patterns
Day 6  → re.match()
Day 7  → re.fullmatch()
Day 8  → re.findall()
Day 9  → re.finditer()
Day 10 → re.split() + re.sub()
Day 11 → re.compile() + Flags
```

**Day 12-এ আমরা Capturing Groups, Non-Capturing Groups `(?:...)`, Named Groups `(?P<name>...)`, এবং `group()`/`groupdict()` বিস্তারিত শিখব।**


# 🐍 Python `re` Module — Day 12

## 🎯 Capturing Groups, Non-Capturing Groups & Named Groups

আজকের lesson খুব গুরুত্বপূর্ণ। আজ শিখবে:

1. Capturing Group `(...)`
    
2. `group()`
    
3. `group(1)`, `group(2)`
    
4. `groups()`
    
5. Non-Capturing Group `(?:...)`
    
6. Named Group `(?P<name>...)`
    
7. `groupdict()`
    
8. `Match.group()` দিয়ে practical data extraction
    

---

# 1️⃣ Capturing Group কী?

Regex-এ parentheses:

```python
(...)
```

ব্যবহার করলে matched অংশকে আলাদা করে **capture** করা যায়।

Example:

```python
import re

text = "My age is 25"

match = re.search(
    r"age is (\d+)",
    text
)

print(match.group())
print(match.group(1))
```

Output:

```text
age is 25
25
```

এখানে:

```text
group()
   ↓
age is 25

group(1)
   ↓
25
```

---

# 2️⃣ Group Number কীভাবে কাজ করে?

Pattern:

```python
r"(\w+) (\d+)"
```

এখানে দুইটি capturing group আছে:

```text
(\w+) → Group 1
(\d+) → Group 2
```

Example:

```python
text = "Python 123"

match = re.search(
    r"(\w+) (\d+)",
    text
)

print(match.group(0))
print(match.group(1))
print(match.group(2))
```

Output:

```text
Python 123
Python
123
```

মনে রাখো:

```text
group(0) → পুরো match
group(1) → প্রথম group
group(2) → দ্বিতীয় group
```

---

# 3️⃣ `groups()`

একসাথে সব captured group পেতে:

```python
text = "Python 123"

match = re.search(
    r"(\w+) (\d+)",
    text
)

print(match.groups())
```

Output:

```text
('Python', '123')
```

অর্থাৎ:

```python
match.groups()
```

→ সব capturing group-এর tuple দেয়।

---

# 4️⃣ Multiple Groups ⭐⭐⭐

ধরো:

```python
text = "Name: Atiar, Age: 25"
```

Pattern:

```python
pattern = r"Name:\s*(\w+),\s*Age:\s*(\d+)"
```

Code:

```python
match = re.search(
    pattern,
    text
)

print(match.group(1))
print(match.group(2))
```

Output:

```text
Atiar
25
```

---

# 5️⃣ `groups()` দিয়ে

```python
print(match.groups())
```

Output:

```text
('Atiar', '25')
```

---

# 6️⃣ Nested Groups ⭐

এটা খুব গুরুত্বপূর্ণ।

```python
pattern = r"((\w+)@(\w+)\.(\w+))"
```

ধরো:

```python
text = "user@example.com"
```

Groups:

```text
Group 1 → user@example.com
Group 2 → user
Group 3 → example
Group 4 → com
```

Code:

```python
match = re.search(
    pattern,
    text
)

print(match.group(0))
print(match.group(1))
print(match.group(2))
print(match.group(3))
print(match.group(4))
```

---

# 7️⃣ Group Number-এর Order

Group number নির্ধারিত হয় **opening parenthesis-এর order** অনুযায়ী।

Example:

```python
r"(A)(B)(C)"
```

তাহলে:

```text
(A) → Group 1
(B) → Group 2
(C) → Group 3
```

Nested হলেও একই নিয়ম।

---

# 8️⃣ Capturing Group কেন দরকার?

Regex দিয়ে শুধু match করা নয়, matched data-এর **parts আলাদা করে বের করতে**।

Example:

```text
2026-08-17
```

Pattern:

```python
r"(\d{4})-(\d{2})-(\d{2})"
```

এখন:

```text
Group 1 → 2026
Group 2 → 08
Group 3 → 17
```

Code:

```python
text = "2026-08-17"

match = re.search(
    r"(\d{4})-(\d{2})-(\d{2})",
    text
)

print("Year:", match.group(1))
print("Month:", match.group(2))
print("Day:", match.group(3))
```

Output:

```text
Year: 2026
Month: 08
Day: 17
```

---

# 9️⃣ Non-Capturing Group `(?:...)` ⭐⭐⭐

এখন আসি খুব গুরুত্বপূর্ণ concept-এ।

সাধারণ group:

```python
(...)
```

এটা capture করে।

কিন্তু:

```python
(?:...)
```

এটা **capture করে না**।

এটাকে বলা হয়:

> Non-Capturing Group

---

# 🔟 কেন Non-Capturing Group?

ধরো তুমি pattern-এর মধ্যে grouping করতে চাও, কিন্তু result হিসেবে group রাখতে চাও না।

Example:

```python
r"(?:Mr|Mrs|Dr)\. \w+"
```

এখানে:

```text
Mr
Mrs
Dr
```

এর মধ্যে যেকোনো একটি match করবে।

কিন্তু `Mr/Mrs/Dr` আলাদা capture হবে না।

---

# 1️⃣1️⃣ Capturing বনাম Non-Capturing

### Capturing:

```python
r"(Mr|Mrs|Dr)\. (\w+)"
```

এখানে:

```text
Group 1 → Mr/Mrs/Dr
Group 2 → Name
```

### Non-Capturing:

```python
r"(?:Mr|Mrs|Dr)\. (\w+)"
```

এখানে:

```text
Group 1 → Name
```

কারণ:

```python
(?:Mr|Mrs|Dr)
```

capture করছে না।

---

# 1️⃣2️⃣ Practical Example

```python
text = "Mr. Atiar"
```

Pattern:

```python
r"(Mr|Mrs|Dr)\. (\w+)"
```

```python
match = re.search(
    r"(Mr|Mrs|Dr)\. (\w+)",
    text
)

print(match.groups())
```

Output:

```text
('Mr', 'Atiar')
```

Non-capturing:

```python
match = re.search(
    r"(?:Mr|Mrs|Dr)\. (\w+)",
    text
)

print(match.groups())
```

Output:

```text
('Atiar',)
```

---

# 1️⃣3️⃣ কখন `(?:...)` ব্যবহার করবে?

যখন:

```text
Grouping দরকার
কিন্তু
Captured result দরকার নেই
```

Example:

```python
r"(?:https?|ftp)://"
```

এখানে protocol group করা হচ্ছে:

```text
http
https
ftp
```

কিন্তু আলাদা করে protocol capture করার প্রয়োজন নেই।

---

# 1️⃣4️⃣ Named Groups ⭐⭐⭐⭐⭐

Group number:

```python
group(1)
group(2)
group(3)
```

অনেক group হলে confusing হয়ে যেতে পারে।

তখন **Named Group** ব্যবহার করি।

Syntax:

```python
(?P<name>pattern)
```

---

# 1️⃣5️⃣ Named Group Example

```python
text = "2026-08-17"

pattern = (
    r"(?P<year>\d{4})-"
    r"(?P<month>\d{2})-"
    r"(?P<day>\d{2})"
)

match = re.search(
    pattern,
    text
)
```

এখন:

```python
print(match.group("year"))
print(match.group("month"))
print(match.group("day"))
```

Output:

```text
2026
08
17
```

এটা অনেক readable।

---

# 1️⃣6️⃣ Named Group + Number

Named group থাকলেও number দিয়েও access করা যায়।

```python
print(match.group(1))
print(match.group("year"))
```

দুটোই:

```text
2026
```

তবে named version বেশি readable:

```python
match.group("year")
```

---

# 1️⃣7️⃣ `groupdict()` ⭐⭐⭐⭐⭐

সব named group একসাথে dictionary হিসেবে পেতে:

```python
print(match.groupdict())
```

Output:

```python
{
    'year': '2026',
    'month': '08',
    'day': '17'
}
```

এটা খুব useful।

---

# 1️⃣8️⃣ Real-world Example — User Data 🔥

Text:

```python
text = "Name: Atiar, Age: 25, City: Dhaka"
```

Pattern:

```python
pattern = (
    r"Name:\s*(?P<name>\w+),\s*"
    r"Age:\s*(?P<age>\d+),\s*"
    r"City:\s*(?P<city>\w+)"
)
```

তারপর:

```python
match = re.search(
    pattern,
    text
)

print(match.groupdict())
```

Output:

```python
{
    'name': 'Atiar',
    'age': '25',
    'city': 'Dhaka'
}
```

🔥 Regex দিয়ে structured data extract করে ফেললাম।

---

# 1️⃣9️⃣ Named Groups + `finditer()` 🔥🔥

ধরো:

```python
text = """
Name: Atiar, Age: 25
Name: Rahim, Age: 30
Name: Karim, Age: 28
"""
```

Pattern:

```python
pattern = (
    r"Name:\s*(?P<name>\w+),\s*"
    r"Age:\s*(?P<age>\d+)"
)
```

Code:

```python
for match in re.finditer(
    pattern,
    text
):
    print(match.groupdict())
```

Output:

```python
{'name': 'Atiar', 'age': '25'}
{'name': 'Rahim', 'age': '30'}
{'name': 'Karim', 'age': '28'}
```

এটা বাস্তব data extraction-এর খুব useful pattern।

---

# 2️⃣0️⃣ Named Groups দিয়ে Date Parser

```python
text = "Today is 2026-08-17"

pattern = (
    r"(?P<year>\d{4})-"
    r"(?P<month>\d{2})-"
    r"(?P<day>\d{2})"
)

match = re.search(
    pattern,
    text
)

date = match.groupdict()

print(date)
```

Output:

```python
{
    'year': '2026',
    'month': '08',
    'day': '17'
}
```

---

# 2️⃣1️⃣ Email Parser 🔥

```python
text = "Contact: user@example.com"
```

Pattern:

```python
pattern = (
    r"(?P<username>[\w.-]+)"
    r"@"
    r"(?P<domain>[\w.-]+)"
    r"\."
    r"(?P<tld>\w+)"
)
```

Code:

```python
match = re.search(
    pattern,
    text
)

print(match.groupdict())
```

Output concept:

```python
{
    'username': 'user',
    'domain': 'example',
    'tld': 'com'
}
```

---

# 2️⃣2️⃣ Phone Number Parser

ধরো:

```text
01712345678
```

Pattern:

```python
pattern = (
    r"(?P<prefix>01\d)"
    r"(?P<number>\d{8})"
)
```

Code:

```python
match = re.search(
    pattern,
    "01712345678"
)

print(match.groupdict())
```

Output:

```python
{
    'prefix': '017',
    'number': '12345678'
}
```

---

# 2️⃣3️⃣ Named Group + `re.sub()` 🔥

Named groups replacement-এর সময়ও ব্যবহার করা যায়।

ধরো:

```python
text = "John Smith"
```

Pattern:

```python
pattern = (
    r"(?P<first>\w+)\s+"
    r"(?P<last>\w+)"
)
```

Replacement:

```python
replacement = r"\g<last>, \g<first>"
```

Code:

```python
result = re.sub(
    pattern,
    replacement,
    text
)

print(result)
```

Output:

```text
Smith, John
```

এখানে named replacement syntax:

```text
\g<last>
\g<first>
```

---

# 2️⃣4️⃣ `group()` vs `groups()` vs `groupdict()`

এগুলো খুব ভালোভাবে মনে রাখো।

|Method|Result|
|---|---|
|`group()`|পুরো match|
|`group(1)`|Group 1|
|`group(2)`|Group 2|
|`groups()`|সব numbered groups → tuple|
|`group("name")`|Named group|
|`groupdict()`|সব named groups → dictionary|

---

# 2️⃣5️⃣ একটা Full Example 🔥🔥

```python
import re

text = """
Name: Atiar, Email: atiar@example.com, Age: 25
Name: Rahim, Email: rahim@test.org, Age: 30
"""
```

Pattern:

```python
pattern = re.compile(
    r"Name:\s*(?P<name>\w+),\s*"
    r"Email:\s*(?P<email>[\w.-]+@[\w.-]+\.\w+),\s*"
    r"Age:\s*(?P<age>\d+)"
)
```

Extraction:

```python
for match in pattern.finditer(text):
    data = match.groupdict()
    print(data)
```

Output:

```python
{
    'name': 'Atiar',
    'email': 'atiar@example.com',
    'age': '25'
}

{
    'name': 'Rahim',
    'email': 'rahim@test.org',
    'age': '30'
}
```

🔥 এই pattern-টা একটা ছোট data parser-এর মতো কাজ করছে।

---

# 2️⃣6️⃣ সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

### Capturing

```python
(...)
```

```text
match করে
+
result capture করে
```

### Non-Capturing

```python
(?:...)
```

```text
match করে
+
result capture করে না
```

### Named Capturing

```python
(?P<name>...)
```

```text
match করে
+
নাম দিয়ে capture করে
```

---

# 🧠 Mental Model

```text
(...) 
   ↓
Group 1

(?:...)
   ↓
No group

(?P<name>...)
   ↓
Named group
```

তারপর:

```text
group(1)
   ↓
প্রথম group

groups()
   ↓
সব numbered group

group("name")
   ↓
নির্দিষ্ট named group

groupdict()
   ↓
সব named group → dict
```

---

# 🧪 Day 12 Practice

## Exercise 1

এই text থেকে Year, Month, Day আলাদা করো:

```python
text = "2026-08-17"
```

Pattern-এ capturing groups ব্যবহার করো।

Expected:

```text
Year: 2026
Month: 08
Day: 17
```

---

## Exercise 2

এই text:

```python
text = "Name: Atiar, Age: 25"
```

`groups()` ব্যবহার করে:

```text
Atiar
25
```

বের করো।

---

## Exercise 3 ⭐

এই pattern-এর output predict করো:

```python
pattern = r"(Mr|Mrs|Dr)\. (\w+)"
```

Input:

```text
Dr. Rahman
```

`group(0)`, `group(1)`, `group(2)` কী হবে?

---

## Exercise 4 ⭐

এটাকে non-capturing group-এ convert করো:

```python
r"(Mr|Mrs|Dr)\. (\w+)"
```

যাতে শুধু person's name capture হয়।

---

## Exercise 5 🔥

এই text parse করো:

```python
text = "Name: Atiar, Age: 25, City: Dhaka"
```

Named groups ব্যবহার করে:

```text
name
age
city
```

বের করো।

তারপর:

```python
match.groupdict()
```

এর output তৈরি করো।

---

## Exercise 6 🔥

এই তিনটি data parse করো:

```python
text = """
Name: Atiar, Age: 25
Name: Rahim, Age: 30
Name: Karim, Age: 28
"""
```

`finditer()` + named groups ব্যবহার করে output:

```python
{'name': 'Atiar', 'age': '25'}
{'name': 'Rahim', 'age': '30'}
{'name': 'Karim', 'age': '28'}
```

---

## Exercise 7 🔥🔥

Email:

```text
atiar@example.com
```

Named groups দিয়ে বের করো:

```text
username
domain
tld
```

Expected:

```python
{
    'username': 'atiar',
    'domain': 'example',
    'tld': 'com'
}
```

---

# 🏆 Day 12 Summary

```text
Day 12
│
├── (...) Capturing Group
│
├── group()
├── group(1)
├── group(2)
├── groups()
│
├── (?:...) Non-Capturing Group
│
├── (?P<name>...) Named Group
│
├── group("name")
└── groupdict()
```

### আজকের সবচেয়ে গুরুত্বপূর্ণ ৩টি syntax:

```python
(...)
```

**Capturing Group**

```python
(?:...)
```

**Non-Capturing Group**

```python
(?P<name>...)
```

**Named Capturing Group**

এর মধ্যে **`(?P<name>...)` + `groupdict()`** ভালোভাবে শিখে রাখো—real-world log parsing, text extraction, data cleaning এবং automation-এ এগুলো অনেক কাজে লাগবে।

# 🐍 Python `re` Module — Day 13

## 🎯 Backreferences, Lookahead & Lookbehind

আজকের lesson-এ আমরা Regex-এর **advanced matching** শিখব:

1. Backreference `\1`, `\2`
    
2. Named backreference `(?P=name)`
    
3. Lookahead `(?=...)`
    
4. Negative Lookahead `(?!...)`
    
5. Lookbehind `(?<=...)`
    
6. Negative Lookbehind `(?<!...)`
    
7. Real-world examples
    

---

# 1️⃣ Backreference কী?

ধরো text:

```python
text = "hello hello"
```

আমরা চাই একই word পরপর দুইবার আছে কিনা detect করতে।

Pattern:

```python
r"\b(\w+)\s+\1\b"
```

এখানে:

```text
(\w+)
   ↓
একটি word capture করল

\1
   ↓
ঠিক একই captured word আবার থাকতে হবে
```

Code:

```python
import re

text = "hello hello"

match = re.search(
    r"\b(\w+)\s+\1\b",
    text
)

if match:
    print(match.group())
```

Output:

```text
hello hello
```

---

# 2️⃣ `\1` কী?

আগের lesson-এ:

```python
(\w+)
```

ছিল **Group 1**।

তাই:

```python
\1
```

মানে:

> Group 1-এ যে text capture হয়েছে, ঠিক সেই text আবার match করতে হবে।

Example:

```text
hello hello
```

```text
(\w+) → hello
\1    → hello
```

Match ✅

কিন্তু:

```text
hello world
```

হবে না।

কারণ:

```text
Group 1 → hello
\1      → hello চাই
কিন্তু পাওয়া গেল → world
```

❌

---

# 3️⃣ Duplicate Word Detection ⭐⭐⭐

এটা খুব useful example:

```python
import re

text = "This is is a test"

pattern = r"\b(\w+)\s+\1\b"

match = re.search(
    pattern,
    text
)

if match:
    print("Duplicate:", match.group())
```

Output:

```text
Duplicate: is is
```

---

# 4️⃣ সব Duplicate Word বের করা

```python
text = "This is is a very very simple test"

pattern = r"\b(\w+)\s+\1\b"

matches = re.finditer(
    pattern,
    text,
    re.IGNORECASE
)

for match in matches:
    print(match.group())
```

Output:

```text
is is
very very
```

---

# 5️⃣ `\2` কী?

যদি দুইটি group থাকে:

```python
r"(\w+) (\w+)"
```

তাহলে:

```text
\1 → প্রথম group
\2 → দ্বিতীয় group
```

Example:

```python
text = "John Smith"

pattern = r"(\w+) (\w+)"

match = re.search(pattern, text)

print(match.group(1))
print(match.group(2))
```

Output:

```text
John
Smith
```

Backreference:

```python
r"(\w+) (\w+) \2"
```

মানে:

```text
word1 word2 word2
```

তাই:

```text
John Smith Smith
```

match করবে।

---

# 6️⃣ Named Backreference ⭐⭐⭐

Named group:

```python
(?P<word>\w+)
```

এর backreference:

```python
(?P=word)
```

Example:

```python
text = "hello hello"

pattern = r"\b(?P<word>\w+)\s+(?P=word)\b"

match = re.search(pattern, text)

if match:
    print(match.group())
```

Output:

```text
hello hello
```

এটা:

```python
\1
```

এর named version-এর মতো।

---

# 7️⃣ `\1` বনাম `(?P=name)`

|Syntax|অর্থ|
|---|---|
|`(\w+)`|Group তৈরি|
|`\1`|Group 1-এর text আবার match|
|`(?P<word>\w+)`|Named group|
|`(?P=word)`|Named group-এর text আবার match|

Complex regex হলে named version বেশি readable।

---

# 8️⃣ Lookahead কী?

এখন আসি খুব গুরুত্বপূর্ণ concept-এ।

**Lookahead কোনো text consume না করেই সামনে কী আছে তা check করে।**

Syntax:

```python
(?=...)
```

মানে:

> সামনে এই pattern থাকতে হবে।

---

# 9️⃣ Basic Lookahead

ধরো:

```python
text = "Python123"
```

আমরা শুধু `Python` match করতে চাই, কিন্তু condition হলো এর পরে অবশ্যই number থাকতে হবে।

```python
pattern = r"Python(?=\d+)"

match = re.search(
    pattern,
    text
)

print(match.group())
```

Output:

```text
Python
```

খেয়াল করো:

```text
Python123
^^^^^^
```

শুধু `Python` match হয়েছে।

`123` match-এর অংশ হয়নি।

---

# 🔟 Lookahead কীভাবে কাজ করছে?

Pattern:

```python
Python(?=\d+)
```

এখানে:

```text
Python
  ↓
match করো

(?=\d+)
  ↓
check করো সামনে number আছে কিনা
```

Input:

```text
Python123
```

তাই:

```text
Python → match ✅
123    → শুধু check করা হয়েছে
```

---

# 1️⃣1️⃣ Lookahead দিয়ে Number-এর আগে থাকা Text

```python
text = "Price: 500"

pattern = r"\w+(?=\s*:)"
```

এখানে আমরা `Price` match করতে পারি কারণ তার পরে `:` আছে।

আরও simple:

```python
pattern = r"\w+(?=:)"
```

---

# 1️⃣2️⃣ Positive Lookahead

```python
(?=...)
```

মানে:

> এই condition অবশ্যই true হতে হবে।

Example:

```python
text = "hello123"

pattern = r"hello(?=\d)"

print(
    re.search(pattern, text).group()
)
```

Output:

```text
hello
```

---

# 1️⃣3️⃣ Negative Lookahead ⭐⭐⭐

Syntax:

```python
(?!...)
```

মানে:

> সামনে এই pattern থাকা যাবে না।

Example:

```python
text = "Python Java"

pattern = r"Python(?!123)"
```

এখানে `Python`-এর পরে `123` থাকা যাবে না।

---

# 1️⃣4️⃣ Example

```python
text = "Python456"

pattern = r"Python(?!123)"

match = re.search(
    pattern,
    text
)

print(match.group())
```

Output:

```text
Python
```

কারণ:

```text
Python456
```

এর পরে `123` নেই।

---

কিন্তু:

```python
text = "Python123"

match = re.search(
    r"Python(?!123)",
    text
)

print(match)
```

Output:

```text
None
```

কারণ `Python`-এর পরে `123` আছে।

---

# 1️⃣5️⃣ Positive vs Negative Lookahead

|Syntax|অর্থ|
|---|---|
|`(?=X)`|সামনে X থাকতে হবে|
|`(?!X)`|সামনে X থাকা যাবে না|

Mental model:

```text
(?=X)
 ↓
X আছে? → YES → match

(?!X)
 ↓
X আছে? → YES → reject
```

---

# 1️⃣6️⃣ Practical Example — Password Rule

ধরো একটি password-এর মধ্যে:

- অন্তত একটি digit
    
- অন্তত একটি uppercase letter
    

থাকতে হবে।

Basic regex:

```python
pattern = r"^(?=.*[A-Z])(?=.*\d).+$"
```

এখানে:

```text
(?=.*[A-Z])
```

→ কোথাও uppercase আছে কিনা check

```text
(?=.*\d)
```

→ কোথাও digit আছে কিনা check

তারপর:

```text
.+
```

→ actual characters match করে।

Example:

```python
text = "Python123"

if re.fullmatch(pattern, text):
    print("Valid")
```

Output:

```text
Valid
```

⚠️ বাস্তব authentication/password validation-এর জন্য regex একা যথেষ্ট নয়; security rules এবং secure password handling আলাদাভাবে দরকার।

---

# 1️⃣7️⃣ Lookbehind কী?

Lookahead সামনে দেখে।

Lookbehind পিছনে দেখে।

Positive lookbehind:

```python
(?<=...)
```

মানে:

> এর আগে এই pattern থাকতে হবে।

---

# 1️⃣8️⃣ Basic Lookbehind

ধরো:

```python
text = "Price: 500"
```

আমরা শুধু `500` match করতে চাই, কিন্তু condition হলো তার আগে `Price:` থাকতে হবে।

```python
pattern = r"(?<=Price: )\d+"

match = re.search(
    pattern,
    text
)

print(match.group())
```

Output:

```text
500
```

এখানে:

```text
Price: 500
       ^^^
```

শুধু `500` match হয়েছে।

---

# 1️⃣9️⃣ Lookahead বনাম Lookbehind

### Lookahead

```python
X(?=Y)
```

মানে:

```text
X-এর পরে Y থাকতে হবে
```

### Lookbehind

```python
(?<=X)Y
```

মানে:

```text
Y-এর আগে X থাকতে হবে
```

Visual:

```text
LOOKAHEAD

X Y
^
match
condition → সামনে


LOOKBEHIND

X Y
  ^
  match
condition → পেছনে
```

---

# 2️⃣0️⃣ Negative Lookbehind

Syntax:

```python
(?<!...)
```

মানে:

> এর আগে এই pattern থাকা যাবে না।

Example:

```python
text = "USD 100"

pattern = r"(?<!USD )\d+"
```

এখানে `100`-এর আগে `USD` আছে।

তাই match হবে না।

---

# 2️⃣1️⃣ Example

```python
text = "Price 100"

pattern = r"(?<!USD )\d+"

match = re.search(
    pattern,
    text
)

print(match.group())
```

Output:

```text
100
```

কারণ এর আগে `USD` নেই।

---

# 2️⃣2️⃣ Four Lookaround Types ⭐⭐⭐⭐⭐

এগুলো খুব ভালোভাবে মনে রাখবে:

```text
Positive Lookahead
(?=X)

Negative Lookahead
(?!X)

Positive Lookbehind
(?<=X)

Negative Lookbehind
(?<!X)
```

Table:

|Regex|অর্থ|
|---|---|
|`(?=X)`|সামনে X থাকতে হবে|
|`(?!X)`|সামনে X থাকা যাবে না|
|`(?<=X)`|পেছনে X থাকতে হবে|
|`(?<!X)`|পেছনে X থাকা যাবে না|

---

# 2️⃣3️⃣ Important: Lookaround সাধারণত consume করে না

এটা খুব গুরুত্বপূর্ণ।

Pattern:

```python
r"Python(?=\d+)"
```

Input:

```text
Python123
```

Match:

```text
Python
```

না:

```text
Python123
```

কারণ:

```text
(?=\d+)
```

শুধু condition check করেছে।

---

# 2️⃣4️⃣ Practical Example — Find Number After `$`

Text:

```python
text = "Price $500 and $1000"
```

আমরা number match করতে চাই, `$` নয়।

```python
pattern = r"(?<=\$)\d+"

for match in re.finditer(pattern, text):
    print(match.group())
```

Output:

```text
500
1000
```

---

# 2️⃣5️⃣ Practical Example — Number NOT After `$`

```python
text = "Price $500, quantity 20"
```

Pattern:

```python
pattern = r"(?<!\$)\b\d+\b"
```

এতে `$`-এর immediately পরে থাকা number বাদ দেওয়ার চেষ্টা করা হচ্ছে।

তবে real-world parsing-এ exact spacing/format অনুযায়ী pattern adjust করতে হবে।

---

# 2️⃣6️⃣ Lookahead + Lookbehind একসাথে 🔥

ধরো:

```python
text = "Price: $500"
```

শুধু `500` match করতে চাই।

```python
pattern = r"(?<=\$)\d+(?=\b)"
```

এখানে:

```text
(?<=\$)
```

→ আগে `$` আছে

```text
\d+
```

→ number

```text
(?=\b)
```

→ সামনে word boundary

---

# 2️⃣7️⃣ Duplicate Word + Backreference 🔥

একটি useful duplicate detector:

```python
pattern = r"\b(?P<word>\w+)\s+(?P=word)\b"
```

Example:

```python
text = "This is is a very very good example"

for match in re.finditer(
    pattern,
    text,
    re.IGNORECASE
):
    print(match.group())
```

Output:

```text
is is
very very
```

---

# 2️⃣8️⃣ Backreference দিয়ে Replacement

Duplicate words remove করার একটি basic example:

```python
text = "This is is a test"

pattern = r"\b(\w+)\s+\1\b"

result = re.sub(
    pattern,
    r"\1",
    text
)

print(result)
```

Output:

```text
This is a test
```

🔥 এখানে:

```text
is is
```

→

```text
is
```

হয়ে গেছে।

---

# 2️⃣9️⃣ Real-world Example — Extract Number Before Unit

Text:

```python
text = "Weight: 50kg Height: 170cm"
```

Regex:

```python
pattern = r"\d+(?=kg|cm)"
```

এখানে:

```text
50kg
^^
```

→ `50`

এবং:

```text
170cm
^^^
```

→ `170`

Code:

```python
for match in re.finditer(
    pattern,
    text
):
    print(match.group())
```

Output:

```text
50
170
```

---

# 3️⃣0️⃣ Real-world Example — Extract Number Before Specific Unit

```python
text = "10kg 20kg 30m"

pattern = r"\d+(?=kg)"

print(
    re.findall(pattern, text)
)
```

Output:

```text
['10', '20']
```

`30m` match হয়নি।

কারণ:

```text
(?=kg)
```

condition পূরণ হয়নি।

---

# 🧠 Day 13 Mental Model

### Backreference

```text
(ABC)
  ↓
Group 1

\1
  ↓
ABC আবার চাই
```

### Lookahead

```text
X(?=Y)

X → match
Y → শুধু check
```

### Negative Lookahead

```text
X(?!Y)

X → match
Y → থাকা যাবে না
```

### Lookbehind

```text
(?<=X)Y

X → শুধু check
Y → match
```

### Negative Lookbehind

```text
(?<!X)Y

X → থাকা যাবে না
Y → match
```

---

# 🧪 Day 13 Practice

## Exercise 1

Duplicate word খুঁজে বের করো:

```python
text = "This is is a very very good book"
```

Expected:

```text
is is
very very
```

---

## Exercise 2

Backreference ব্যবহার করে:

```text
hello hello
Python Python
```

এর মতো duplicate words detect করো।

Hint:

```python
r"\b(\w+)\s+\1\b"
```

---

## Exercise 3 ⭐

এই text:

```python
text = "Python123 Django456 React"
```

শুধু সেই word match করো যার পরে number আছে।

Expected:

```text
Python
Django
```

Hint:

```python
(?=\d+)
```

---

## Exercise 4 ⭐

এই text:

```python
text = "Price: 500"
```

শুধু `500` match করো এবং নিশ্চিত করো যে এর আগে:

```text
Price: 
```

আছে।

Hint:

```python
(?<=Price: )\d+
```

---

## Exercise 5 ⭐

এই text:

```python
text = "10kg 20kg 30m 40kg"
```

শুধু `kg`-এর আগে থাকা numbers বের করো।

Expected:

```text
10
20
40
```

---

## Exercise 6 🔥

এই text:

```python
text = "USD 100, BDT 500, 200"
```

শুধু `USD`-এর পরে থাকা `100` বের করো।

Lookbehind ব্যবহার করো।

---

## Exercise 7 🔥

এই password:

```python
password = "Python123"
```

Regex দিয়ে check করো:

```text
কমপক্ষে ১টি uppercase
+
কমপক্ষে ১টি digit
```

Hint:

```python
(?=.*[A-Z])
(?=.*\d)
```

---

## Exercise 8 🔥🔥

এই text:

```python
text = "Price: $500, Discount: $100"
```

শুধু dollar-এর পরের numbers বের করো:

```text
500
100
```

Hint:

```python
(?<=\$)\d+
```

---

# 🏆 Day 13 Summary

আজকের সবচেয়ে গুরুত্বপূর্ণ syntax:

```python
(...)
```

→ Capturing Group

```python
\1
```

→ প্রথম captured group আবার match

```python
(?P<word>...)
```

→ Named Group

```python
(?P=word)
```

→ Named Backreference

```python
(?=...)
```

→ Positive Lookahead

```python
(?!...)
```

→ Negative Lookahead

```python
(?<=...)
```

→ Positive Lookbehind

```python
(?<!...)
```

→ Negative Lookbehind

---

## 📚 এখন পর্যন্ত `re` Course

```text
Day 1  → Regex Fundamentals
Day 2  → Character Classes
Day 3  → Quantifiers
Day 4  → Special Characters
Day 5  → Groups & Patterns
Day 6  → re.match()
Day 7  → re.fullmatch()
Day 8  → re.findall()
Day 9  → re.finditer()
Day 10 → re.split() + re.sub()
Day 11 → re.compile() + Flags
Day 12 → Capturing / Non-Capturing / Named Groups
Day 13 → Backreferences + Lookaround
```

**Day 13-এর core skill হলো: “কিছু match করার পাশাপাশি তার আগে/পরে কী আছে সেটা condition হিসেবে check করা।”**

অবশ্যই। এখন পর্যন্ত `re` module-এর Day 1–13 যা শিখেছ, সেগুলো ব্যবহার করে **একটা real-world project** করলে সবচেয়ে ভালো হবে।

# 🚀 Project: Log Analyzer & Error Detector

তুমি একটা Python program বানাবে যেটা একটি `.log` file পড়বে এবং Regex ব্যবহার করে:

- IP address বের করবে
    
- Date/Time বের করবে
    
- `INFO`, `WARNING`, `ERROR` detect করবে
    
- Error message বের করবে
    
- Email বের করবে
    
- HTTP status code বের করবে
    
- Duplicate words detect করবে
    
- নির্দিষ্ট IP কতবার এসেছে count করবে
    
- শেষে একটা summary report তৈরি করবে
    

---

## 📁 Project Structure

```text
log_analyzer/
│
├── main.py
├── analyzer.py
├── sample.log
└── report.txt
```

---

# 1️⃣ `sample.log`

এই sample data দিয়ে শুরু করো:

```text
2026-08-17 10:15:20 INFO User login from 192.168.1.10
2026-08-17 10:16:05 ERROR Database connection failed
2026-08-17 10:17:30 WARNING CPU usage high
2026-08-17 10:18:42 INFO User login from 192.168.1.20
2026-08-17 10:20:10 ERROR File not found
2026-08-17 10:21:15 INFO Contact admin@example.com
2026-08-17 10:22:00 ERROR ERROR server connection failed
```

---

# 2️⃣ `analyzer.py`

প্রথমে Regex patterns তৈরি করবে।

```python
import re


DATE_PATTERN = re.compile(
    r"(?P<date>\d{4}-\d{2}-\d{2})"
)

TIME_PATTERN = re.compile(
    r"(?P<time>\d{2}:\d{2}:\d{2})"
)

IP_PATTERN = re.compile(
    r"\b(?P<ip>\d{1,3}(?:\.\d{1,3}){3})\b"
)

EMAIL_PATTERN = re.compile(
    r"\b(?P<email>[\w.-]+@[\w.-]+\.\w+)\b"
)

LEVEL_PATTERN = re.compile(
    r"\b(?P<level>INFO|WARNING|ERROR)\b",
    re.IGNORECASE
)

STATUS_PATTERN = re.compile(
    r"\b(?P<status>[1-5]\d{2})\b"
)

DUPLICATE_PATTERN = re.compile(
    r"\b(?P<word>\w+)\s+(?P=word)\b",
    re.IGNORECASE
)
```

---

# 3️⃣ IP Address Extractor

```python
def extract_ips(text):
    return IP_PATTERN.findall(text)
```

Test:

```python
text = "User connected from 192.168.1.10"

print(extract_ips(text))
```

Output:

```text
['192.168.1.10']
```

---

# 4️⃣ Email Extractor

```python
def extract_emails(text):
    return EMAIL_PATTERN.findall(text)
```

Test:

```python
text = "Contact admin@example.com"

print(extract_emails(text))
```

Output:

```text
['admin@example.com']
```

---

# 5️⃣ Log Level Detector

```python
def extract_levels(text):
    return LEVEL_PATTERN.findall(text)
```

Example:

```python
text = "ERROR Database failed"

print(extract_levels(text))
```

Output:

```text
['ERROR']
```

---

# 6️⃣ Duplicate Word Detector

আমাদের sample-এ আছে:

```text
ERROR ERROR server
```

Function:

```python
def find_duplicates(text):
    return [
        match.group("word")
        for match in DUPLICATE_PATTERN.finditer(text)
    ]
```

Test:

```python
text = "ERROR ERROR server"

print(find_duplicates(text))
```

Output:

```text
['ERROR']
```

---

# 7️⃣ Date & Time Extractor

```python
def extract_datetime(text):
    date_match = DATE_PATTERN.search(text)
    time_match = TIME_PATTERN.search(text)

    if date_match and time_match:
        return {
            "date": date_match.group("date"),
            "time": time_match.group("time")
        }

    return None
```

---

# 8️⃣ সব Function একসাথে

`analyzer.py`:

```python
import re


DATE_PATTERN = re.compile(
    r"(?P<date>\d{4}-\d{2}-\d{2})"
)

TIME_PATTERN = re.compile(
    r"(?P<time>\d{2}:\d{2}:\d{2})"
)

IP_PATTERN = re.compile(
    r"\b(?P<ip>\d{1,3}(?:\.\d{1,3}){3})\b"
)

EMAIL_PATTERN = re.compile(
    r"\b(?P<email>[\w.-]+@[\w.-]+\.\w+)\b"
)

LEVEL_PATTERN = re.compile(
    r"\b(?P<level>INFO|WARNING|ERROR)\b",
    re.IGNORECASE
)

DUPLICATE_PATTERN = re.compile(
    r"\b(?P<word>\w+)\s+(?P=word)\b",
    re.IGNORECASE
)


def extract_ips(text):
    return IP_PATTERN.findall(text)


def extract_emails(text):
    return EMAIL_PATTERN.findall(text)


def extract_levels(text):
    return LEVEL_PATTERN.findall(text)


def find_duplicates(text):
    return [
        match.group("word")
        for match in DUPLICATE_PATTERN.finditer(text)
    ]


def extract_datetime(text):
    date_match = DATE_PATTERN.search(text)
    time_match = TIME_PATTERN.search(text)

    if date_match and time_match:
        return {
            "date": date_match.group("date"),
            "time": time_match.group("time")
        }

    return None
```

---

# 9️⃣ `main.py`

এখন log file পড়বে।

```python
from analyzer import (
    extract_ips,
    extract_emails,
    extract_levels,
    find_duplicates,
    extract_datetime
)


with open("sample.log", "r", encoding="utf-8") as file:
    text = file.read()


print("===== LOG ANALYZER =====")

print("\nIPs:")
print(extract_ips(text))

print("\nEmails:")
print(extract_emails(text))

print("\nLog Levels:")
print(extract_levels(text))

print("\nDuplicate Words:")
print(find_duplicates(text))

print("\nDate/Time:")
print(extract_datetime(text))
```

Run:

```bash
python main.py
```

---

# 🔥 এবার Project-টা Advanced করো

এখন শুধু extraction করলে হবে না।

## Feature 1 — Error Count

```text
ERROR → 3
WARNING → 1
INFO → 3
```

Hint:

```python
from collections import Counter
```

তারপর:

```python
levels = extract_levels(text)

counter = Counter(
    level.upper()
    for level in levels
)

print(counter)
```

---

# Feature 2 — IP Frequency

Input:

```text
192.168.1.10
192.168.1.20
192.168.1.10
```

Output:

```text
192.168.1.10 → 2
192.168.1.20 → 1
```

Hint:

```python
Counter(extract_ips(text))
```

---

# Feature 3 — Error Lines

এটা গুরুত্বপূর্ণ।

শুধু `ERROR` বের করবে না।

পুরো ERROR line বের করবে।

Regex:

```python
ERROR_LINE_PATTERN = re.compile(
    r"^.*\bERROR\b.*$",
    re.IGNORECASE | re.MULTILINE
)
```

তারপর:

```python
def extract_error_lines(text):
    return ERROR_LINE_PATTERN.findall(text)
```

---

# Feature 4 — Report তৈরি

শেষে:

```text
========================
       LOG REPORT
========================

Total Lines: 7

INFO: 3
WARNING: 1
ERROR: 3

IPs:
192.168.1.10 → 1
192.168.1.20 → 1

Emails:
admin@example.com

Duplicate Words:
ERROR ERROR

Error Messages:
Database connection failed
File not found
ERROR server connection failed
```

---

# ⭐ তোমার `re` Skills এখানে কোথায় ব্যবহার হচ্ছে?

|`re` Skill|Project-এ ব্যবহার|
|---|---|
|`re.search()`|Date/Time|
|`re.findall()`|IP/Email|
|`re.finditer()`|Duplicate words|
|`re.compile()`|সব regex|
|`re.IGNORECASE`|ERROR/INFO detection|
|`re.MULTILINE`|পুরো error line|
|Capturing Group|Date/IP|
|Named Group|`date`, `time`, `ip`|
|Non-Capturing Group|IP pattern|
|Backreference|Duplicate words|
|Lookahead|Advanced filtering|
|Lookbehind|Context-based extraction|
|`re.sub()`|Text cleaning|

---

# 🎯 তোমার Challenge

**আমি চাই তুমি প্রথমে পুরো project-এর code copy না করে নিজে লিখো।**

Implementation order:

```text
Step 1 → sample.log তৈরি
Step 2 → file read
Step 3 → IP extractor
Step 4 → Email extractor
Step 5 → Date/Time extractor
Step 6 → INFO/WARNING/ERROR detector
Step 7 → Error line extractor
Step 8 → Duplicate word detector
Step 9 → Counter দিয়ে statistics
Step 10 → report.txt তৈরি
```

এটা শেষ করতে পারলে তুমি শুধু `re` syntax মুখস্থ করবে না—**Regex দিয়ে real-world text/log processing করতে পারবে।**



