
# 🧭 **Advanced Collections in Python**

---

## 🧱 1. `namedtuple()`

### ➤ What it is:

A lightweight, immutable object type like a tuple — but with **named fields** instead of numeric indexes.  
Think of it as a **tuple with labels**, similar to a simple class.

### ➤ Example:

```python
from collections import namedtuple

# Define a namedtuple type
Point = namedtuple("Point", ["x", "y"])

# Create instances
p1 = Point(10, 20)
p2 = Point(x=5, y=15)

print(p1.x, p1.y)      # Access by name
print(p2[0], p2[1])    # Still accessible by index
```

---

# 🧱 `namedtuple` — Explained in Simple Terms

---

## 🔹 What is a `namedtuple`?

`namedtuple` is a **factory function** from Python’s built-in **`collections`** module.  
It creates **tuple-like objects** that have **named fields** instead of just index positions.

Think of it as a **lightweight class** or a **tuple with labels**.

---

### 🧩 Basic Syntax

```python
from collections import namedtuple

# Create a new namedtuple type
Point = namedtuple('Point', ['x', 'y'])
```

Now, `Point` is a new **data type** (like a small class) that can hold data in two fields — `x` and `y`.

---

### 🧠 Example:

```python
# Create instances
p1 = Point(10, 20)
p2 = Point(x=5, y=15)

# Access values
print(p1.x, p1.y)      # Access by name → 10 20
print(p2[0], p2[1])    # Access by index → 5 15
```

✅ **Output:**

```
10 20
5 15
```

---

## 🧾 Why Use `namedtuple`?

|Feature|Benefit|
|---|---|
|**Named fields**|More readable code than plain tuples|
|**Immutable**|Like tuples (cannot modify values)|
|**Lightweight**|Less memory and faster than a class|
|**Supports indexing & unpacking**|Behaves like a tuple|
|**Documentation-friendly**|Self-describing field names|

---

## ⚙️ `namedtuple` vs Regular `tuple`

|Feature|`tuple`|`namedtuple`|
|---|---|---|
|Access|By index (`t[0]`)|By name (`t.x`) or index|
|Readability|Low|High|
|Memory|Low|Slightly higher|
|Mutability|Immutable|Immutable|
|Use case|Quick, simple grouping|Structured, readable data|

---

## 📦 Example: Using `namedtuple` in Real Scenarios

### 🧩 1. Representing Points or Coordinates

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(f"Point = ({p.x}, {p.y})")
```

### 🧩 2. Representing Student Records

```python
Student = namedtuple('Student', ['name', 'age', 'grade'])
s1 = Student('Alice', 20, 'A')
print(f"{s1.name} is {s1.age} years old and got {s1.grade}")
```

### 🧩 3. Unpacking Like a Tuple

```python
x, y = p
print(x, y)  # 3 4
```

---

## ⚡ Useful Features and Methods

### ✅ `_make()`: Create from iterable

```python
data = [5, 10]
p = Point._make(data)
print(p)  # Point(x=5, y=10)
```

---

### ✅ `_asdict()`: Convert to dictionary

```python
print(p._asdict())  # {'x': 5, 'y': 10}
```

---

### ✅ `_replace()`: Create new object with modified field

(Since namedtuples are **immutable**, you can’t change fields — but `_replace()` returns a **new one**.)

```python
p2 = p._replace(y=99)
print(p2)  # Point(x=5, y=99)
```

---

### ✅ `._fields`: List all field names

```python
print(Point._fields)  # ('x', 'y')
```

---

## 🧮 Example: More Complex Use Case

### Representing Employee Data

```python
Employee = namedtuple('Employee', ['id', 'name', 'department', 'salary'])

employees = [
    Employee(101, "Alice", "HR", 60000),
    Employee(102, "Bob", "IT", 75000),
    Employee(103, "Charlie", "Finance", 50000),
]

# Find high-salary employees
high_salary = [emp for emp in employees if emp.salary > 60000]
for e in high_salary:
    print(f"{e.name} works in {e.department} with salary {e.salary}")
```

✅ Output:

```
Bob works in IT with salary 75000
```

---

## 🧠 When to Use `namedtuple`

Use it when:

- You need **readable, immutable records**
    
- You don’t need **class methods or inheritance**
    
- You want **performance** and **clarity**
    

Don’t use it when:

- You need **mutable** objects
    
- You need **methods or behavior** (use a class instead)
    

---

## 🧾 Summary

|Feature|Description|
|---|---|
|Defined in|`collections` module|
|Syntax|`namedtuple('Name', ['field1', 'field2', ...])`|
|Access|By field name or index|
|Mutable?|❌ No (immutable)|
|Converts to dict?|✅ Yes, via `_asdict()`|
|Use case|Structured, readable, lightweight data container|

---

✅ **Why use it:**

- Lightweight alternative to classes
    
- Immutable (like tuples)
    
- Self-documenting field names
    

---

## 🧾 2. `deque` (Double-Ended Queue)

### ➤ What it is:

A **fast, flexible queue** that allows insertion and removal from **both ends** in **O(1)** time.

### ➤ Example:

```python
from collections import deque

dq = deque([10, 20, 30])

dq.append(40)       # Add right
dq.appendleft(0)    # Add left
dq.pop()            # Remove right
dq.popleft()        # Remove left

print(dq)  # deque([20, 30])
```

✅ **Why use it:**

- Much faster than `list` for queue operations
    
- Useful for **stacks**, **queues**, and **sliding windows**
    

---

## 🧩 3. `Counter`

### ➤ What it is:

A **dictionary subclass** that counts hashable objects (like frequencies).

### ➤ Example:

```python
from collections import Counter

data = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
count = Counter(data)

print(count)          # Counter({'apple': 3, 'banana': 2, 'orange': 1})
print(count.most_common(2))  # [('apple', 3), ('banana', 2)]
print(list(count.elements()))  # ['apple', 'apple', 'apple', 'banana', 'banana', 'orange']
```



It’s one of the **most useful advanced collection types**, especially for **counting, analytics, and frequency analysis**.

---

# 🧮 `collections.Counter` — Full Explanation

---

## 🔹 What is a `Counter`?

A **`Counter`** is a **subclass of `dict`** designed specifically for **counting hashable objects**.  
It automatically counts how many times each element appears in an iterable.

Think of it as a **frequency table** or a **histogram**.

---

### 🧩 Basic Example

```python
from collections import Counter

fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']

count = Counter(fruits)
print(count)
```

✅ **Output:**

```
Counter({'apple': 3, 'banana': 2, 'orange': 1})
```

So `Counter` counts how many times each item appears.

---

## 🧱 Key Features

|Feature|Description|
|---|---|
|✅ Counts elements automatically|No need for loops or manual counting|
|✅ Dictionary-like access|Use keys and values like normal dict|
|✅ Supports arithmetic operations|Add, subtract, or combine counters|
|✅ Provides useful methods|`most_common()`, `elements()`, etc.|

---

## ⚙️ Common Methods

Let’s explore the most useful built-in methods.

---

### 🧩 1️⃣ `Counter()` — Creating a Counter

You can create a `Counter` from:

- A **list**
    
- A **string**
    
- A **dictionary**
    
- A **keyword argument list**
    

```python
Counter(['a', 'b', 'a', 'c'])
Counter("hello")
Counter({'a': 2, 'b': 3})
Counter(a=2, b=3)
```

---

### 🧩 2️⃣ Access and Update Counts

```python
cnt = Counter("banana")

print(cnt['a'])  # 3
print(cnt['x'])  # 0 (nonexistent keys return 0, not KeyError)

# Add more counts
cnt.update("apple")
print(cnt)
```

✅ Output:

```
Counter({'a': 4, 'n': 2, 'b': 1, 'p': 2, 'l': 1, 'e': 1})
```

---

### 🧩 3️⃣ `most_common(n)`

Returns a list of the **n most frequent elements**.

```python
cnt = Counter("banana")
print(cnt.most_common(2))
```

✅ Output:

```
[('a', 3), ('n', 2)]
```

---

### 🧩 4️⃣ `elements()`

Returns **all elements**, repeating each as many times as its count (in arbitrary order).

```python
cnt = Counter({'apple': 3, 'banana': 2})
print(list(cnt.elements()))
```

✅ Output:

```
['apple', 'apple', 'apple', 'banana', 'banana']
```

---

### 🧩 5️⃣ Arithmetic Operations Between Counters

You can **add**, **subtract**, or **combine** two Counters easily.

```python
c1 = Counter(a=3, b=2)
c2 = Counter(a=1, b=4)

print(c1 + c2)   # Addition → Counter({'a': 4, 'b': 6})
print(c1 - c2)   # Subtraction → Counter({'a': 2})
print(c1 & c2)   # Intersection (min values) → Counter({'a': 1, 'b': 2})
print(c1 | c2)   # Union (max values) → Counter({'a': 3, 'b': 4})
```

---

### 🧩 6️⃣ Convert Back to Other Types

```python
cnt = Counter("apple")
print(dict(cnt))      # {'a': 1, 'p': 2, 'l': 1, 'e': 1}
print(list(cnt))      # ['a', 'p', 'l', 'e']
print(set(cnt))       # {'a', 'p', 'l', 'e'}
```

---

## 🧠 Example: Word Frequency Counter

```python
from collections import Counter

sentence = "the quick brown fox jumps over the lazy dog the quick fox"
words = sentence.split()

count = Counter(words)

print(count)
print(count.most_common(3))  # Top 3 frequent words
```

✅ Output:

```
Counter({'the': 3, 'quick': 2, 'fox': 2, 'brown': 1, 'jumps': 1, 'over': 1, 'lazy': 1, 'dog': 1})
[('the', 3), ('quick', 2), ('fox', 2)]
```

---

## 💡 Real-World Use Cases

|Use Case|Example|
|---|---|
|**Word frequency**|Counting occurrences of words in a text|
|**Character frequency**|Counting letters in a string|
|**Inventory management**|Tracking number of items|
|**Voting systems**|Counting votes for each candidate|
|**Data analysis**|Summarizing categorical data|

---

## ⚡ Example: Character Frequency in a String

```python
text = "abracadabra"
freq = Counter(text)

# Top 2 most common letters
print(freq.most_common(2))  # [('a', 5), ('b', 2)]
```

---

## ⚙️ Resetting and Clearing

```python
cnt = Counter(a=3, b=2)
cnt.clear()
print(cnt)  # Counter()
```

---

## 🔍 Summary Table

|Operation|Example|Description|
|---|---|---|
|Create|`Counter(iterable)`|Count elements|
|Access|`cnt['a']`|Get frequency (0 if missing)|
|Update|`cnt.update(iterable)`|Add counts|
|Most common|`cnt.most_common(n)`|Top n items|
|Elements|`list(cnt.elements())`|Expand counts|
|Arithmetic|`c1 + c2`, `c1 - c2`|Combine Counters|
|Clear|`cnt.clear()`|Remove all items|

---

## ⚖️ Comparison: `Counter` vs `dict`

|Feature|`dict`|`Counter`|
|---|---|---|
|Missing key|Raises `KeyError`|Returns `0`|
|Counting|Manual|Automatic|
|Built-in tools|Limited|`most_common()`, `elements()`|
|Use case|General mapping|Frequency counting|

---

✅ **In Short:**

> `Counter` = smart dictionary for counting things — words, items, events, etc.  
> It’s fast, convenient, and widely used in analytics, AI, and competitive programming.

---

Let’s go step by step — from **basic word frequency** to **advanced keyword and character analysis**.

---

# 🧠 Using `Counter` for Text Analytics

---

## ⚙️ Step 1: Import and Prepare Text

You can analyze any text — a paragraph, document, or file.

```python
from collections import Counter

text = """
Python is a powerful programming language.
Python is easy to learn and fun to use.
Python can be used for data science, AI, and web development.
"""
```

---

## 📊 Step 2: Count Word Frequency

### ✅ Basic Example

```python
words = text.lower().split()
word_count = Counter(words)

print(word_count)
```

🧾 **Output:**

```
Counter({'python': 3, 'is': 2, 'a': 1, 'powerful': 1, 'programming': 1, 'language.': 1, ...})
```

> It’s already useful — but let’s make it cleaner and smarter.

---

## 🧹 Step 3: Clean and Tokenize Text

Real text often has **punctuation, capitalization, and stopwords** (like _"the"_, _"and"_, _"is"_).  
Let’s clean those up for better analytics.

```python
import re
from collections import Counter

# 1️⃣ Clean text
clean_text = re.findall(r'\b\w+\b', text.lower())

# 2️⃣ Create a Counter
word_count = Counter(clean_text)

print(word_count.most_common(5))
```

✅ **Output:**

```
[('python', 3), ('is', 2), ('and', 2), ('a', 1), ('powerful', 1)]
```

---

## 🧩 Step 4: Remove Stopwords (for meaningful analysis)

You can remove common words like _"is"_, _"the"_, _"and"_ manually or use libraries like **NLTK**.

```python
stopwords = {'is', 'a', 'and', 'to', 'for', 'be', 'the'}

filtered_words = [w for w in clean_text if w not in stopwords]
filtered_count = Counter(filtered_words)

print(filtered_count.most_common(5))
```

✅ **Output:**

```
[('python', 3), ('powerful', 1), ('programming', 1), ('language', 1), ('easy', 1)]
```

---

## 🔍 Step 5: Get Insights

### ➤ Most common words:

```python
print(filtered_count.most_common(3))
# [('python', 3), ('powerful', 1), ('programming', 1)]
```

### ➤ Total unique words:

```python
print(len(filtered_count))
# e.g. 12
```

### ➤ Top N Keywords (for analytics or visualization):

```python
for word, freq in filtered_count.most_common(5):
    print(f"{word:<15} → {freq}")
```

---

## ✨ Step 6: Character-Level Analysis

Count **individual letters** instead of words.

```python
char_count = Counter(text.lower())
print(char_count.most_common(5))
```

✅ **Output:**

```
[(' ', 18), ('a', 9), ('n', 8), ('o', 8), ('t', 7)]
```

---

## 📈 Step 7: Real Example — Top Keywords in a Paragraph

```python
paragraph = """
Data science is an interdisciplinary field that uses scientific methods,
processes, algorithms, and systems to extract knowledge and insights from data.
Data science is related to machine learning and artificial intelligence.
"""

clean_text = re.findall(r'\b\w+\b', paragraph.lower())
stopwords = {'is', 'an', 'and', 'to', 'from', 'that', 'the', 'in', 'of'}
words = [w for w in clean_text if w not in stopwords]

word_count = Counter(words)
for word, freq in word_count.most_common(10):
    print(f"{word:<15} → {freq}")
```

✅ **Output:**

```
data            → 3
science         → 2
machine         → 1
learning        → 1
artificial      → 1
intelligence    → 1
interdisciplinary → 1
field           → 1
uses            → 1
scientific      → 1
```

---

## 🧮 Step 8: Use Counters Together — Combine or Compare Texts

```python
text1 = "Python is fun and powerful"
text2 = "Python is great for data science"

c1 = Counter(re.findall(r'\b\w+\b', text1.lower()))
c2 = Counter(re.findall(r'\b\w+\b', text2.lower()))

# Combine or compare
combined = c1 + c2
print(combined.most_common())
```

✅ Output:

```
[('python', 2), ('is', 2), ('fun', 1), ('and', 1), ('powerful', 1), ('great', 1), ('for', 1), ('data', 1), ('science', 1)]
```

---

## ⚡ Bonus: Visualizing Word Frequencies (Optional)

You can visualize the Counter results using **matplotlib**:

```python
import matplotlib.pyplot as plt

words, counts = zip(*filtered_count.most_common(5))
plt.bar(words, counts)
plt.title("Top 5 Words")
plt.show()
```

---

## 🧾 Summary Table

|Task|Code|Description|
|---|---|---|
|Count words|`Counter(text.split())`|Quick word frequency|
|Clean text|`re.findall(r'\b\w+\b', text.lower())`|Removes punctuation|
|Filter stopwords|List comprehension|Keeps meaningful words|
|Get top N|`.most_common(n)`|Returns top frequent words|
|Count chars|`Counter(text)`|Letter frequency|
|Combine texts|`c1 + c2`|Merge two Counters|
|Convert to dict|`dict(counter)`|Use as normal dictionary|

---

✅ **In short:**

> `Counter` is your go-to tool for **word frequency, keyword extraction, and text summaries** — a must-have for NLP, search, and data analytics.

---
### **mini keyword-extraction tool**
Awesome! ⚡  
Let’s build a **Mini Keyword-Extraction Tool** using only Python’s built-in libraries — no heavy NLP packages needed.

We’ll use:

- **`re`** → to clean and tokenize text
    
- **`Counter`** → to count word frequencies
    
- (optionally) a small **stopword list** → to remove common meaningless words like “the”, “and”, etc.
    

---

# 🧠 Mini Keyword Extraction Tool (Step by Step)

---

## ✅ Step 1: Import Tools

```python
import re
from collections import Counter
```

---

## ✅ Step 2: Define the Function

```python
def extract_keywords(text, top_n=10):
    # Step 1: Normalize (lowercase)
    text = text.lower()

    # Step 2: Tokenize words (keep only alphanumeric words)
    words = re.findall(r'\b[a-z]{2,}\b', text)  # words with ≥2 letters

    # Step 3: Define stopwords (you can expand this list)
    stopwords = {
        'the', 'and', 'is', 'in', 'to', 'of', 'for', 'a', 'an', 'on', 'by',
        'with', 'this', 'that', 'it', 'as', 'at', 'from', 'be', 'are', 'was',
        'or', 'its', 'can', 'will', 'which', 'has', 'have'
    }

    # Step 4: Filter out stopwords
    filtered_words = [w for w in words if w not in stopwords]

    # Step 5: Count frequencies
    counts = Counter(filtered_words)

    # Step 6: Return top N keywords
    return counts.most_common(top_n)
```

---

## ✅ Step 3: Try It Out

```python
text = """
Python is a popular programming language used for data analysis,
machine learning, web development, automation, and artificial intelligence.
Python's simplicity and large community make it a great choice for beginners
and professionals alike.
"""

keywords = extract_keywords(text, top_n=8)
for word, freq in keywords:
    print(f"{word:<15} → {freq}")
```

✅ **Output Example:**

```
python          → 2
programming     → 1
language        → 1
data            → 1
analysis        → 1
machine         → 1
learning        → 1
development     → 1
```

---

## ✅ Step 4: Make It More Useful (Optional Enhancements)

### ➤ 1️⃣ Accept File Input

You can easily read from a text file:

```python
with open("article.txt", "r", encoding="utf-8") as f:
    text = f.read()

keywords = extract_keywords(text, top_n=10)
print(keywords)
```

---

### ➤ 2️⃣ Ignore Rare Words (optional)

You can remove words that appear only once:

```python
keywords = [(w, f) for w, f in Counter(filtered_words).most_common() if f > 1]
```

---

### ➤ 3️⃣ Visualize (optional)

If you want a quick visualization:

```python
import matplotlib.pyplot as plt

words, counts = zip(*keywords)
plt.barh(words, counts)
plt.gca().invert_yaxis()  # most frequent on top
plt.title("Top Keywords")
plt.show()
```

---

## ✅ Step 5: Summary of What’s Happening

|Step|Task|Tool|
|---|---|---|
|1|Normalize and clean text|`str.lower()`, `re.findall()`|
|2|Remove stopwords|Python set|
|3|Count frequencies|`collections.Counter`|
|4|Extract top N words|`.most_common(n)`|
|5|(Optional) Visualize|`matplotlib`|

---

## ⚡ Example Output (for an article about AI):

```
data            → 5
science         → 4
machine         → 3
learning        → 3
artificial      → 2
intelligence    → 2
model           → 2
training        → 2
```

---

### ✅ In Short:

> Your mini keyword-extraction tool finds the **most frequent, meaningful words** in any paragraph or document — a lightweight way to summarize text, analyze documents, or preprocess data for NLP.

---

# ⚡ Mini Keyword Extraction Tool with Bigrams

---

## Step 1: Imports and Setup

```python
import re
from collections import Counter
from itertools import tee
```

---

## Step 2: Helper function to generate `bigrams`

```python
def generate_bigrams(words):
    """Generate bigrams (pairs of consecutive words) from a list."""
    # Create two iterators offset by one
    a, b = tee(words)
    next(b, None)
    return zip(a, b)
```

---

## Step 3: Main function with `bigrams`

```python
def extract_keywords_with_bigrams(text, top_n=10, include_bigrams=True):
    # Normalize text to lowercase
    text = text.lower()

    # Tokenize words (only alphabets, min length 2)
    words = re.findall(r'\b[a-z]{2,}\b', text)

    # Define stopwords (expand as needed)
    stopwords = {
        'the', 'and', 'is', 'in', 'to', 'of', 'for', 'a', 'an', 'on', 'by',
        'with', 'this', 'that', 'it', 'as', 'at', 'from', 'be', 'are', 'was',
        'or', 'its', 'can', 'will', 'which', 'has', 'have'
    }

    # Filter out stopwords
    filtered_words = [w for w in words if w not in stopwords]

    # Count single words
    word_counts = Counter(filtered_words)

    if include_bigrams:
        # Generate bigrams and filter out those containing stopwords
        bigrams = generate_bigrams(filtered_words)
        filtered_bigrams = [' '.join(bigram) for bigram in bigrams if all(word not in stopwords for word in bigram)]

        # Count bigrams
        bigram_counts = Counter(filtered_bigrams)

        # Combine counts: words + bigrams
        combined_counts = word_counts + bigram_counts

        # Return top N combined keywords and bigrams
        return combined_counts.most_common(top_n)
    else:
        # Return only top N single words
        return word_counts.most_common(top_n)
```

---

## Step 4: Try it out!

```python
text = """
Machine learning is a subset of artificial intelligence that focuses on building systems
that learn from data. Data science includes machine learning, statistics, and data analysis.
Many industries use machine learning for predictive analytics and automation.
"""

keywords = extract_keywords_with_bigrams(text, top_n=10, include_bigrams=True)
for kw, freq in keywords:
    print(f"{kw:<20} → {freq}")
```

---

## Expected output example:

```
machine learning      → 3
data                  → 3
learning              → 3
data science          → 1
artificial intelligence → 1
predictive analytics  → 1
automation            → 1
subset                → 1
focuses               → 1
building systems      → 1
```

---

# Recap:

- **Single words** and **bigrams** are both counted and combined.
    
- Stopwords are removed from both single words and bigrams.
    
- The output is a sorted list of the most frequent words and phrases.
    
- Easy to toggle bigrams on/off with the `include_bigrams` flag.
    

---

✅ **Why use it:**

- Quickly count occurrences
    
- Useful for statistics, `NLP`, and data analysis
    

---

## 🧮 4. `OrderedDict`

### ➤ What it is:

A **dictionary subclass** that remembers the **insertion order** of keys (like modern dicts, but with more control).

### ➤ Example:

```python
from collections import OrderedDict

od = OrderedDict()
od['a'] = 1
od['b'] = 2
od['c'] = 3

od.move_to_end('a')  # Move key to end
print(od)            # OrderedDict([('b', 2), ('c', 3), ('a', 1)])
```



---

# 📚 What is `OrderedDict`?

---

## 🔹 Overview

- `OrderedDict` is a **dictionary subclass** that **remembers the order** in which keys are inserted.
    
- Before Python 3.7, the built-in `dict` **did not guarantee order** — so if you wanted to keep insertion order, you had to use `OrderedDict`.
    
- Since Python 3.7+, the **built-in `dict` preserves insertion order by default**, but `OrderedDict` still has some unique features.
    

---

## 🔹 Why use `OrderedDict`?

|Feature|Built-in dict (Python ≥3.7)|`OrderedDict`|
|---|---|---|
|Maintains insertion order|Yes|Yes|
|Move existing key to end|No|Yes (`move_to_end()`)|
|Reversed iteration support|No (directly)|Yes (`reversed()`)|
|Equality considers order|No|Yes (two OrderedDicts are equal only if order & items same)|

---

# 🧰 How to Use `OrderedDict`

---

### ✅ Import and Create

```python
from collections import OrderedDict

od = OrderedDict()
od['apple'] = 3
od['banana'] = 2
od['orange'] = 1

print(od)
```

Output:

```
OrderedDict([('apple', 3), ('banana', 2), ('orange', 1)])
```

---

### ✅ Iteration preserves insertion order

```python
for key in od:
    print(key, od[key])
```

Output:

```
apple 3
banana 2
orange 1
```

---

### ✅ `move_to_end(key, last=True)`

- Move an existing key **to the end** (`last=True`, default) or **to the beginning** (`last=False`).
    

```python
od.move_to_end('banana')  # Move banana to the end
print(list(od.keys()))    # ['apple', 'orange', 'banana']

od.move_to_end('apple', last=False)  # Move apple to the beginning (already is)
print(list(od.keys()))    # ['apple', 'orange', 'banana']
```

---

### ✅ Equality with order matters

```python
od1 = OrderedDict([('a', 1), ('b', 2)])
od2 = OrderedDict([('b', 2), ('a', 1)])

print(od1 == od2)  # False (order differs)
```

---

### ✅ Reversed iteration

```python
for key in reversed(od):
    print(key)
```

Output:

```
banana
orange
apple
```

---

# 🧩 Use Cases

- When order of keys matters, for example:
    
    - Serialization (to JSON/YAML preserving order)
        
    - Configuration files reading/writing
        
    - LRU caches (move recently used to front or end)
        
    - Any algorithm needing consistent order and ability to reorder keys
        

---

# ⚙️ Quick Summary

|Feature|`OrderedDict`|
|---|---|
|Maintains insertion order|Yes|
|Can reorder keys|Yes — via `move_to_end()`|
|Equality check|Considers both keys, values _and_ order|
|Reversed iteration|Supported|
|Backwards compatibility|Needed in Python <3.7 for ordered dicts|

---



✅ **Why use it:**

- Useful when order **matters** (e.g., caching, serialization)
    
- Note: Regular `dict` in Python 3.7+ also preserves order, but `OrderedDict` gives **extra control** (like reordering).
    

---

## ⚙️ 5. `defaultdict`

### ➤ What it is:

A **dictionary** that provides a **default value** for missing keys automatically.

### ➤ Example:

```python
from collections import defaultdict

# Default value type: list
graph = defaultdict(list)

graph['A'].append('B')
graph['A'].append('C')
graph['B'].append('D')

print(graph)
# defaultdict(<class 'list'>, {'A': ['B', 'C'], 'B': ['D']})
```


# 📚 What is `defaultdict`?

---

## 🔹 Overview

- `defaultdict` is a subclass of the built-in Python `dict`.
    
- It **automatically assigns a default value** to any key that does **not exist yet** in the dictionary.
    
- This avoids **`KeyError` exceptions** when you try to access or modify keys that aren’t there.
    

---

## 🔹 Why use `defaultdict`?

Imagine you want to count items or group things in a dictionary. Normally, you’d write code like this:

```python
d = {}
if 'key' not in d:
    d['key'] = 0
d['key'] += 1
```

With `defaultdict`, you skip all that boilerplate — it creates a default value automatically.

---

# 🧰 How to Use `defaultdict`

---

### ✅ Import and create a `defaultdict`

```python
from collections import defaultdict

# Default value is int(), which is 0
d = defaultdict(int)
```

---

### ✅ Example 1: Counting word frequency

```python
words = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']

counts = defaultdict(int)
for word in words:
    counts[word] += 1

print(counts)
```

Output:

```
defaultdict(<class 'int'>, {'apple': 3, 'banana': 2, 'orange': 1})
```

---

### ✅ Example 2: Grouping items by a key

Suppose you want to group names by their first letter:

```python
names = ['Alice', 'Bob', 'Annie', 'Brian', 'Charlie']

groups = defaultdict(list)
for name in names:
    key = name[0]  # first letter
    groups[key].append(name)

print(groups)
```

Output:

```
defaultdict(<class 'list'>, {'A': ['Alice', 'Annie'], 'B': ['Bob', 'Brian'], 'C': ['Charlie']})
```

---

# ⚙️ How it Works

- When you access a **missing key**, `defaultdict` calls the _default factory_ function you gave it to create a default value.
    
- This default factory can be anything that takes no arguments and returns a value:
    
    - `int` → 0
        
    - `list` → []
        
    - `set` → set()
        
    - `lambda: 'unknown'` → custom default
        

Example with custom default:

```python
d = defaultdict(lambda: 'unknown')
print(d['missing_key'])  # Outputs: unknown
```

---

# 🧩 Use Cases

- Counting occurrences
    
- Grouping values (lists, sets)
    
- Auto-initializing complex data structures
    
- Avoiding manual key checks before assignment
    

---

# 🧾 Quick Summary

|Feature|Explanation|
|---|---|
|Subclass of `dict`|Behaves like a normal dictionary|
|Default value factory|A callable returning default values|
|Avoids KeyError|Missing keys get auto-created with default value|
|Common factories|`int`, `list`, `set`, or custom `lambda`|
|Useful for counters & grouping|Simplifies counting and grouping tasks|


---

# 🛠 Practical Examples Using `defaultdict`

---

## Example 1: Counting Word Frequency (Simpler than using dict)

```python
from collections import defaultdict

text = "apple banana apple orange banana apple"

words = text.split()
counts = defaultdict(int)  # default 0

for word in words:
    counts[word] += 1

print(dict(counts))
```

**Output:**

```python
{'apple': 3, 'banana': 2, 'orange': 1}
```

_Without `defaultdict`, you'd need to check if the key exists before incrementing._

---

## Example 2: Grouping Data — Names by First Letter

```python
from collections import defaultdict

names = ['Alice', 'Bob', 'Annie', 'Brian', 'Charlie']

groups = defaultdict(list)  # default empty list

for name in names:
    groups[name[0]].append(name)

print(dict(groups))
```

**Output:**

```python
{'A': ['Alice', 'Annie'], 'B': ['Bob', 'Brian'], 'C': ['Charlie']}
```

_Perfect for categorizing or clustering data._

---

## Example 3: Building an Inverted Index (Search Engine Concept)

Given documents, build a dictionary where each word maps to a list of document IDs that contain it.

```python
from collections import defaultdict

documents = {
    1: "the cat sat on the mat",
    2: "the dog chased the cat",
    3: "the dog and the cat are friends",
}

inverted_index = defaultdict(set)  # Use set to avoid duplicates

for doc_id, text in documents.items():
    for word in text.split():
        inverted_index[word].add(doc_id)

# Convert sets to lists for nicer display
inverted_index = {word: list(doc_ids) for word, doc_ids in inverted_index.items()}

print(inverted_index)
```

**Output:**

```python
{
 'the': [1, 2, 3],
 'cat': [1, 2, 3],
 'sat': [1],
 'on': [1],
 'mat': [1],
 'dog': [2, 3],
 'chased': [2],
 'and': [3],
 'are': [3],
 'friends': [3]
}
```

---

## Example 4: Counting Characters in a String

```python
from collections import defaultdict

text = "hello world"

char_count = defaultdict(int)

for char in text:
    char_count[char] += 1

print(dict(char_count))
```

**Output:**

```python
{'h': 1, 'e': 1, 'l': 3, 'o': 2, ' ': 1, 'w': 1, 'r': 1, 'd': 1}
```

---

# 🔑 Key takeaway:

> **`defaultdict` saves you from repetitive checks** — making your code cleaner, faster, and more Pythonic, especially for counting and grouping tasks.

---

Want me to show you how to combine `defaultdict` with other collections like `Counter` or `OrderedDict`?


✅ **Why use it:**

- Avoids `KeyError`
    
- Great for building grouped or graph-like structures
    

---

## 🔢 6. `ChainMap`

### ➤ What it is:

Combines multiple dictionaries into a **single view** (like layered scopes).

### ➤ Example:

```python
from collections import ChainMap

defaults = {"theme": "light", "language": "en"}
user = {"language": "fr"}

settings = ChainMap(user, defaults)

print(settings["language"])  # 'fr' (from user)
print(settings["theme"])     # 'light' (from defaults)
```

✅ **Why use it:**

- Useful for configuration or scoped variable lookups
    
- Allows layered or fallback data access
    

---

## 🧰 7. `UserDict`, `UserList`, `UserString`

### ➤ What they are:

Wrappers around built-in types (`dict`, `list`, `str`) that are **easier to subclass**.  
Used when you want to customize behavior safely.

### ➤ Example:

```python
from collections import UserDict

class MyDict(UserDict):
    def __setitem__(self, key, value):
        print(f"Setting {key} = {value}")
        super().__setitem__(key, value)

d = MyDict()
d["x"] = 10
```

✅ **Why use them:**

- Cleaner and safer subclassing of built-ins
    
- Great for building custom containers
    

---

# 🧾 Summary Table

|Collection|Type|Key Features|Common Use Case|
|---|---|---|---|
|**namedtuple**|tuple subclass|Named fields|Lightweight data objects|
|**deque**|list-like|Fast appends/pops on both ends|Queues, stacks|
|**Counter**|dict subclass|Counts items|Frequency counting|
|**OrderedDict**|dict subclass|Keeps insertion order|Ordered mappings|
|**defaultdict**|dict subclass|Default factory for missing keys|Grouping, graphs|
|**ChainMap**|view of multiple dicts|Combine scopes|Config layers|
|**UserDict/UserList/UserString**|wrapper classes|Custom container logic|Subclass safely|

---

## 💡 Pro Tip: Combining Advanced Collections

You can combine these for elegant solutions!

### Example: Group and Count

```python
from collections import defaultdict, Counter

# Group words by their first letter and count
words = ["apple", "apricot", "banana", "berry", "cherry", "coconut"]
groups = defaultdict(list)

for word in words:
    groups[word[0]].append(word)

# Count how many words in each group
count_by_letter = {k: Counter(v) for k, v in groups.items()}
print(groups)
print(count_by_letter)
```

---
Excellent question 👏 — these three are part of Python’s **`collections` module** and are designed for **safe subclassing** of built-in types.

Let’s break them down clearly 👇

---

# 📚 `UserDict`, `UserList`, `UserString` — Explained

---

## 🔹 Why They Exist

In Python, it’s possible to subclass built-in types like `dict`, `list`, or `str`.  
However, direct subclassing can sometimes behave unexpectedly (especially when overriding methods), because these types are **implemented in C** and **bypass normal Python method resolution** for performance.

👉 So, Python provides **wrapper classes** —  
✅ `UserDict`, ✅ `UserList`, ✅ `UserString` —  
which behave like their built-in counterparts but are written **in pure Python**.



---

# 🧱 1. `UserDict`

### ✅ Purpose:

A **wrapper around `dict`** — acts like a normal dictionary but allows **safe `subclassing` and customization**.

---

### 🧩 Example: Basic Use

```python
from collections import UserDict

class MyDict(UserDict):
    def __setitem__(self, key, value):
        print(f"Setting {key} = {value}")
        super().__setitem__(key, value)

d = MyDict()
d['a'] = 10
d['b'] = 20
print(d)
```

**Output:**

```
Setting a = 10
Setting b = 20
{'a': 10, 'b': 20}
```

---

### 🧠 Why use `UserDict`?

- You can safely override methods like `__setitem__`, `__delitem__`, `__getitem__`, etc.
    
- Prevents unexpected behavior seen in direct `dict` subclassing.
    

---

### ⚙️ Common Use Case:

For example, a **read-only dictionary**:

```python
class ReadOnlyDict(UserDict):
    def __setitem__(self, key, value):
        raise TypeError("This dictionary is read-only")

data = ReadOnlyDict({'x': 1, 'y': 2})
print(data['x'])
data['z'] = 3   # ❌ Raises TypeError
```

---

# 🧱 2. `UserList`

### ✅ Purpose:

A **wrapper around `list`** — used to create **custom list-like objects** that are easy to modify or extend.

---

### 🧩 Example: Logging additions to a list

```python
from collections import UserList

class LoggingList(UserList):
    def append(self, item):
        print(f"Adding: {item}")
        super().append(item)

lst = LoggingList([1, 2, 3])
lst.append(4)
print(lst)
```

**Output:**

```
Adding: 4
[1, 2, 3, 4]
```

---

### 🧠 Why use `UserList`?

- Safely customize list behaviors (e.g., validation, filtering, or logging).
    
- Unlike subclassing `list` directly, your overridden methods will **always** be used — even when internal operations (like slicing) create new lists.
    

---

### ⚙️ Example: A list that only accepts integers

```python
class IntList(UserList):
    def append(self, item):
        if not isinstance(item, int):
            raise TypeError("Only integers allowed!")
        super().append(item)

numbers = IntList([1, 2, 3])
numbers.append(4)
numbers.append("x")  # ❌ Raises TypeError
```

---

# 🧱 3. `UserString`

### ✅ Purpose:

A **wrapper around `str`** — behaves like a string but can be extended easily.

---

### 🧩 Example: A custom string class

```python
from collections import UserString

class UpperCaseString(UserString):
    def __init__(self, data):
        super().__init__(data.upper())

s = UpperCaseString("hello world")
print(s)        # HELLO WORLD
```

---

### ⚙️ Example: Custom string operations

```python
class SafeString(UserString):
    def append(self, text):
        self.data += text
    
    def remove(self, substring):
        self.data = self.data.replace(substring, "")

s = SafeString("DataScience")
s.append(" Rocks!")
s.remove("Data")
print(s)  # Science Rocks!
```

---

# 🧾 Summary Table

|Class|Base Type|Purpose|Example Use|
|---|---|---|---|
|**UserDict**|`dict`|Safe subclassing of dictionaries|Custom read-only or logging dictionaries|
|**UserList**|`list`|Safe subclassing of lists|Validation, filtering, logging|
|**UserString**|`str`|Safe subclassing of strings|String transformations or tracking|

---

# 💡 Key Benefits

✅ Behave exactly like their built-in counterparts  
✅ Written in pure Python — easy to extend safely  
✅ Overridden methods behave consistently  
✅ Ideal for creating **custom data containers**

---

# 🚀 Real-World Examples

### Example 1: Case-insensitive dictionary

```python
class CaseInsensitiveDict(UserDict):
    def __setitem__(self, key, value):
        key = key.lower()
        super().__setitem__(key, value)
    
    def __getitem__(self, key):
        return super().__getitem__(key.lower())

d = CaseInsensitiveDict()
d['Name'] = "Alice"
print(d['name'])  # Alice
```

---

### Example 2: Positive-only list

```python
class PositiveList(UserList):
    def append(self, item):
        if item < 0:
            raise ValueError("Only positive numbers allowed")
        super().append(item)

nums = PositiveList()
nums.append(10)
nums.append(-5)  # ❌ Raises ValueError
```

---

✅ **In short:**

> `UserDict`, `UserList`, and `UserString` are **`Pythonic` wrappers** around the basic types — perfect for **creating safe, customized data containers**.

---
Perfect 👏 — now we’re going to **combine** `UserDict`, `UserList`, and `UserString` to create a **custom, real-world data container** that uses all three together.

Let’s build something useful — say a **Contact Book** — where:

- Each **contact name** (a string) is stored as a `UserString`.
    
- Each **contact** has multiple **phone numbers** stored as a `UserList`.
    
- All contacts are managed in a **dictionary** subclassed from `UserDict`.
    

---

# 📒 Example: Custom Contact Book Using `UserDict`, `UserList`, `UserString`

---

### ✅ Step 1: Imports

```python
from collections import UserDict, UserList, UserString
```

---

### ✅ Step 2: Define the `UserString` subclass for contact names

```python
class ContactName(UserString):
    """A case-insensitive string wrapper for contact names."""
    def __eq__(self, other):
        return self.data.lower() == str(other).lower()

    def __hash__(self):
        # Allow using ContactName as a dict key
        return hash(self.data.lower())

    def __str__(self):
        return self.data.title()
```

🧩 **Purpose:**

- Makes names case-insensitive (`Alice` and `alice` are treated the same).
    
- Nicely formats names with `.title()`.
    

---

### ✅ Step 3: Define the `UserList` subclass for storing phone numbers

```python
class PhoneList(UserList):
    """List that stores only valid phone numbers (digits only)."""
    def append(self, number):
        if not number.isdigit():
            raise ValueError("Phone number must contain only digits!")
        super().append(number)
```

🧩 **Purpose:**

- Ensures only valid phone numbers are stored.
    
- Could be extended later for formatting or duplicates.
    

---

### ✅ Step 4: Define the `UserDict` subclass for the contact book

```python
class ContactBook(UserDict):
    """A dictionary where keys are ContactNames and values are PhoneLists."""
    
    def add_contact(self, name, phone):
        name = ContactName(name)
        if name not in self.data:
            self.data[name] = PhoneList()
        self.data[name].append(phone)
    
    def get_phones(self, name):
        name = ContactName(name)
        return self.data.get(name, [])
    
    def remove_contact(self, name):
        name = ContactName(name)
        if name in self.data:
            del self.data[name]
        else:
            print(f"No contact found for {name}")
    
    def __str__(self):
        lines = ["📞 Contact Book:"]
        for name, phones in self.data.items():
            lines.append(f"{name}: {', '.join(phones)}")
        return "\n".join(lines)
```

🧩 **Purpose:**

- Uses `ContactName` and `PhoneList` as types.
    
- Adds helper methods to add, remove, and view contacts.
    

---

### ✅ Step 5: Use it!

```python
book = ContactBook()
book.add_contact("Alice", "12345")
book.add_contact("Alice", "67890")
book.add_contact("bob", "55555")

print(book)
```

**Output:**

```
📞 Contact Book:
Alice: 12345, 67890
Bob: 55555
```

---

### ✅ Step 6: Demonstrate Case-Insensitivity

```python
print(book.get_phones("ALICE"))  # ['12345', '67890']
book.remove_contact("ALICE")
print(book)
```

**Output:**

```
['12345', '67890']
📞 Contact Book:
Bob: 55555
```

---

# 🧾 Summary

|Class|Used For|Behavior|
|---|---|---|
|**ContactName (UserString)**|Contact names|Case-insensitive & formatted|
|**PhoneList (UserList)**|Phone numbers|Validates digits only|
|**ContactBook (UserDict)**|Contacts storage|Combines both types with helper methods|

---

# 💡 Why This Combination Is Powerful

✅ Each class is **modular** and **reusable**  
✅ Clean, **object-oriented** design  
✅ Safer than `subclassing` built-ins directly  
✅ Easy to extend later (e.g., email fields, address lists, etc.)

---

## 🧩 What is a Heap?

A **heap** is a special type of binary tree that satisfies the _heap property_:

- **Min-heap** → Parent ≤ Children
    
- **Max-heap** → Parent ≥ Children
    

In Python, the `heapq` module implements **a min-heap** by default using a simple list.

---

## 🛠️ Basic `heapq` Operations

Let’s walk through the common operations.

```python
import heapq

# Create an empty heap
heap = []

# Add elements
heapq.heappush(heap, 5)
heapq.heappush(heap, 1)
heapq.heappush(heap, 3)

print("Heap:", heap)   # Heap: [1, 5, 3] (internally reordered)
```

### 🔍 Peek at the smallest element

```python
smallest = heap[0]
print("Smallest:", smallest)  # 1
```

### 🧹 Remove the smallest element

```python
min_value = heapq.heappop(heap)
print("Popped:", min_value)   # 1
print("New Heap:", heap)
```

---

## 🔄 Convert a List into a Heap

```python
nums = [5, 3, 8, 1]
heapq.heapify(nums)
print("Heapified list:", nums)
```

This rearranges the list **in place** to satisfy the heap property.

---

## ⚙️ Simulating a Max-Heap

`heapq` only provides a **min-heap**, but you can simulate a **max-heap** easily by inverting the values.

```python
nums = [5, 3, 8, 1]
max_heap = []

# Push negative values
for num in nums:
    heapq.heappush(max_heap, -num)

print("Simulated max-heap (negated):", max_heap)

# Pop the largest (by negating back)
largest = -heapq.heappop(max_heap)
print("Largest:", largest)
```

Or more compactly:

```python
largest = -heapq.heappop(max_heap)
```

---

## 🧮 Useful Functions

|Function|Description|
|---|---|
|`heapq.heappush(heap, item)`|Push item onto heap|
|`heapq.heappop(heap)`|Pop smallest item|
|`heapq.heappushpop(heap, item)`|Push new item, then pop smallest|
|`heapq.heapreplace(heap, item)`|Pop smallest, then push new item|
|`heapq.nlargest(n, iterable)`|Return n largest elements|
|`heapq.nsmallest(n, iterable)`|Return n smallest elements|

Example:

```python
nums = [5, 8, 3, 2, 7]
print(heapq.nlargest(2, nums))   # [8, 7]
print(heapq.nsmallest(3, nums))  # [2, 3, 5]
```

---

## 💡 Practice Ideas

1. **Find the k smallest/largest elements** from a list.
    
2. **Merge k sorted lists** efficiently using a heap.
    
3. **Implement a priority queue** (task scheduling, Dijkstra’s algorithm).
    
4. **Stream median** (maintain two heaps).
    
5. **Find the kth largest element** in a stream.
    

---
Excellent! 💪 Let’s dive into **heap practice problems** — perfect for sharpening your algorithmic and `heapq` skills.

I’ll give you **a short problem description**, what **type of heap** to use, and a **hint** (but not the full solution unless you ask).

---

## 🧩 Problem 1: Find the Kth Largest Element in a List

### 📜 Description

Given an unsorted list of numbers, find the **kth largest element**.

**Example:**

```python
nums = [3, 2, 1, 5, 6, 4]
k = 2
# Output: 5
```

### 💡 Hint

- You only need to keep track of the **k largest elements**.
    
- Use a **min-heap** of size `k` — push elements, and if the heap grows beyond `k`, pop the smallest.
    
- The top of the heap (`heap[0]`) will be your kth largest element.
    

---

## 🧩 Problem 2: Merge K Sorted Lists

### 📜 Description

You are given `k` sorted lists. Merge them into a single sorted list.

**Example:**

```python
lists = [
    [1, 4, 5],
    [1, 3, 4],
    [2, 6]
]
# Output: [1, 1, 2, 3, 4, 4, 5, 6]
```

### 💡 Hint

- Use a **min-heap** to always extract the smallest among the heads of all lists.
    
- Each heap entry can be a tuple `(value, list_index, element_index)` so you know where it came from.
    

---

## 🧩 Problem 3: Find the K Closest Points to the Origin

### 📜 Description

Given a list of points `(x, y)` on a 2D plane, return the `k` closest points to the origin `(0, 0)`.

**Example:**

```python
points = [(1, 3), (-2, 2)]
k = 1
# Output: [(-2, 2)]
```

### 💡 Hint

- Distance formula: `d^2 = x² + y²`.
    
- Use a **max-heap** of size `k` (store negative distances) to keep track of the `k` smallest distances.
    
- If heap size > `k`, pop the farthest point.
    

---

## 🧩 Problem 4: Top K Frequent Elements

### 📜 Description

Given a list of numbers, return the `k` most frequent elements.

**Example:**

```python
nums = [1,1,1,2,2,3]
k = 2
# Output: [1,2]
```

### 💡 Hint

- Use a dictionary to count frequencies.
    
- Use a **min-heap** of size `k` with pairs `(frequency, element)` to track the top `k`.
    
- If heap exceeds `k`, pop the smallest frequency.
    

---

## 🧩 Problem 5: Median from Data Stream

### 📜 Description

Design a structure that supports:

- `addNum(num)` → add a number
    
- `findMedian()` → return the median of all elements
    

**Example:**

```python
addNum(1)
addNum(2)
findMedian() → 1.5
addNum(3)
findMedian() → 2
```

### 💡 Hint

- Use **two heaps**:
    
    - A **max-heap** (left side) for the smaller half
        
    - A **min-heap** (right side) for the larger half
        
- Keep both heaps balanced (sizes differ by at most 1).
    
- Median = either the middle element or average of tops.
    

---

