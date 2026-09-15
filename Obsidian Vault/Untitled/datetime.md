অবশ্যই। এবার আমরা **Python `datetime` module-এর complete course** করব—আগের `json`, `os`, `sys`, `pathlib` course-এর মতো **official Python documentation ভিত্তিক**, day-by-day এবং practical project সহ।

Official documentation: [Python `datetime` official documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

# 🐍 Python `datetime` Module — Complete Course

## 🎯 Course Goal

এই course শেষে তুমি পারবে:

```text
Current date/time
      ↓
Date
      ↓
Time
      ↓
Datetime
      ↓
Formatting
      ↓
Parsing
      ↓
Timedelta
      ↓
Timezone
      ↓
UTC
      ↓
Timestamp
      ↓
Date calculations
      ↓
Real-world projects
```

---

# 📚 15-Day Course Roadmap

|Day|Topic|Level|
|---|---|---|
|Day 1|`datetime` fundamentals|🟢|
|Day 2|`date` object|🟢|
|Day 3|`time` object|🟢|
|Day 4|`datetime` object|🟢|
|Day 5|`today()`, `now()`, `utcnow()` concepts|🟡|
|Day 6|`strftime()` — datetime → string|🟡|
|Day 7|`strptime()` — string → datetime|🟡|
|Day 8|`timedelta`|🟡|
|Day 9|Date/time calculations|🟡|
|Day 10|Timestamp + Unix time|🟡|
|Day 11|Timezone + aware/naive datetime|🔴|
|Day 12|UTC + `zoneinfo`|🔴|
|Day 13|Comparing dates + sorting|🟡|
|Day 14|Real-world datetime patterns|🔴|
|Day 15|🔥 Final Project|🔴|

---

# 🧠 প্রথমে ৪টি Core Object বুঝে নাও

`datetime` module-এর সবচেয়ে গুরুত্বপূর্ণ classes:

```python
from datetime import date
from datetime import time
from datetime import datetime
from datetime import timedelta
```

Concept:

```text
date
 ↓
শুধু তারিখ

time
 ↓
শুধু সময়

datetime
 ↓
তারিখ + সময়

timedelta
 ↓
সময়/তারিখের difference
```

---

# Day 1 — `datetime` Fundamentals

## 1️⃣ Module Import

```python
import datetime
```

অথবা:

```python
from datetime import datetime
```

দুটোই valid।

---

## 2️⃣ Current Date and Time

```python
from datetime import datetime

now = datetime.now()

print(now)
```

Output-এর মতো:

```text
2026-08-17 17:30:45.123456
```

Structure:

```text
2026-08-17
   ↓
date

17:30:45
   ↓
time
```

---

# 3️⃣ Current Date

```python
from datetime import date

today = date.today()

print(today)
```

Output:

```text
2026-08-17
```

---

# 4️⃣ Datetime-এর Components

```python
from datetime import datetime

now = datetime.now()

print(now.year)
print(now.month)
print(now.day)

print(now.hour)
print(now.minute)
print(now.second)
print(now.microsecond)
```

অর্থাৎ:

```text
datetime
├── year
├── month
├── day
├── hour
├── minute
├── second
└── microsecond
```

---

# 5️⃣ Date Components

```python
from datetime import date

today = date.today()

print(today.year)
print(today.month)
print(today.day)
```

---

# 6️⃣ Create Specific Date

```python
from datetime import date

birthday = date(
    2000,
    5,
    20
)

print(birthday)
```

Output:

```text
2000-05-20
```

---

# 7️⃣ Create Specific Datetime

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    15,
    30,
    45
)

print(dt)
```

Output:

```text
2026-08-17 15:30:45
```

---

# 8️⃣ Create Specific Time

```python
from datetime import time

t = time(
    14,
    30,
    15
)

print(t)
```

Output:

```text
14:30:15
```

---

# 9️⃣ Important Constructor Order

### `date`

```python
date(year, month, day)
```

### `time`

```python
time(hour, minute, second)
```

### `datetime`

```python
datetime(
    year,
    month,
    day,
    hour,
    minute,
    second
)
```

এগুলো ভালোভাবে মনে রাখবে।

---

# 🔟 `datetime` বনাম `date`

```python
date.today()
```

দেবে:

```text
2026-08-17
```

কিন্তু:

```python
datetime.now()
```

দেবে:

```text
2026-08-17 17:30:45
```

অর্থাৎ:

```text
date
→ Date only

datetime
→ Date + Time
```

---

# 1️⃣1️⃣ `datetime.combine()`

একটি `date` এবং একটি `time` combine করা যায়।

```python
from datetime import date, time, datetime

d = date(2026, 8, 17)

t = time(14, 30)

dt = datetime.combine(d, t)

print(dt)
```

Output:

```text
2026-08-17 14:30:00
```

---

# 1️⃣2️⃣ Date থেকে Datetime

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    15,
    30
)

print(dt.date())
print(dt.time())
```

Output:

```text
2026-08-17
15:30:00
```

এটা খুব important।

```text
datetime
   │
   ├── .date()
   │
   └── .time()
```

---

# 1️⃣3️⃣ Weekday

```python
from datetime import date

today = date.today()

print(today.weekday())
```

`weekday()`:

```text
Monday    → 0
Tuesday   → 1
Wednesday → 2
Thursday  → 3
Friday    → 4
Saturday  → 5
Sunday    → 6
```

---

# 1️⃣4️⃣ `isoweekday()`

```python
print(today.isoweekday())
```

এখানে:

```text
Monday    → 1
Tuesday   → 2
Wednesday → 3
Thursday  → 4
Friday    → 5
Saturday  → 6
Sunday    → 7
```

Difference:

|Method|Monday|Sunday|
|---|--:|--:|
|`weekday()`|0|6|
|`isoweekday()`|1|7|

---

# 1️⃣5️⃣ `replace()`

Datetime-এর নির্দিষ্ট অংশ পরিবর্তন করতে:

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    15,
    30
)

new_dt = dt.replace(
    year=2027
)

print(new_dt)
```

Output:

```text
2027-08-17 15:30:00
```

আর:

```python
new_dt = dt.replace(
    hour=10,
    minute=15
)
```

---

# 🧪 Day 1 Practice

### Exercise 1

Current:

```text
year
month
day
hour
minute
second
```

আলাদা করে print করো।

### Exercise 2

নিজের একটি birthday `date` object তৈরি করো।

### Exercise 3

একটি specific datetime তৈরি করো:

```text
2026-12-31 23:59:59
```

### Exercise 4

একটি datetime থেকে:

```text
date
time
weekday
```

print করো।

### Exercise 5 ⭐

`replace()` দিয়ে একটি datetime-এর:

```text
year
month
day
hour
minute
```

পরিবর্তন করে দেখো।

---

# 🏆 Day 1 Mini Project

## Digital Clock Information

Program এমন output দেবে:

```text
========================
     DATE & TIME
========================

Date       : 2026-08-17
Time       : 17:30:45
Year       : 2026
Month      : 8
Day        : 17
Weekday    : Monday
========================
```

এখানে ব্যবহার করবে:

```python
datetime.now()
.date()
.time()
.year
.month
.day
.weekday()
```

---

# 📌 Day 1 Cheat Sheet

```python
from datetime import date, time, datetime
```

### Current date

```python
date.today()
```

### Current datetime

```python
datetime.now()
```

### Specific date

```python
date(2026, 8, 17)
```

### Specific time

```python
time(15, 30)
```

### Specific datetime

```python
datetime(2026, 8, 17, 15, 30)
```

### Extract date

```python
dt.date()
```

### Extract time

```python
dt.time()
```

### Weekday

```python
dt.weekday()
```

### ISO weekday

```python
dt.isoweekday()
```

### Modify

```python
dt.replace(year=2027)
```

---

## 🚀 Course Progress

```text
Day 1  → Fundamentals                 ← START
Day 2  → date
Day 3  → time
Day 4  → datetime
Day 5  → Current date/time
Day 6  → strftime()
Day 7  → strptime()
Day 8  → timedelta
Day 9  → Date calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world patterns
Day 15 → 🔥 Final Project
```

**Day 2-এ আমরা `date` object পুরোপুরি শিখব—`fromordinal()`, `fromisoformat()`, `isoformat()`, `resolution`, date comparison এবং date manipulation সহ।**



# 🐍 Python `datetime` — Day 2

## `date` Object Complete Lesson

আজ আমরা শুধু **`date` class** নিয়ে কাজ করব।

Official documentation: [Python `datetime.date` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#date-objects)

আজকের flow:

```text
date
 │
 ├── Create
 ├── Access year/month/day
 ├── ISO format
 ├── Comparison
 ├── Weekday
 ├── Ordinal
 ├── Replace
 └── Date calculation
```

---

# 1️⃣ `date` কী?

`date` object শুধুমাত্র:

```text
Year + Month + Day
```

রাখে।

```python
from datetime import date

today = date.today()

print(today)
```

Output:

```text
2026-08-17
```

এখানে কোনো:

```text
hour
minute
second
```

নেই।

---

# 2️⃣ Specific Date তৈরি

Syntax:

```python
date(year, month, day)
```

Example:

```python
from datetime import date

birthday = date(2000, 5, 20)

print(birthday)
```

Output:

```text
2000-05-20
```

---

# 3️⃣ `year`, `month`, `day`

```python
d = date(2026, 8, 17)

print(d.year)
print(d.month)
print(d.day)
```

Output:

```text
2026
8
17
```

---

# 4️⃣ Today's Date

```python
today = date.today()

print(today)
```

এটি system-এর current local date ব্যবহার করে।

---

# 5️⃣ ISO Format ⭐⭐⭐

Python-এর standard date representation:

```text
YYYY-MM-DD
```

যেমন:

```text
2026-08-17
```

`isoformat()`:

```python
d = date(2026, 8, 17)

print(d.isoformat())
```

Output:

```text
2026-08-17
```

এটা API, database এবং JSON data-এর সাথে খুব বেশি ব্যবহার হয়।

---

# 6️⃣ ISO String থেকে Date ⭐⭐⭐

ধরো তোমার কাছে:

```python
date_string = "2026-08-17"
```

এটাকে `date` object করতে:

```python
d = date.fromisoformat(
    date_string
)

print(d)
```

এখন:

```python
print(type(d))
```

Output:

```text
<class 'datetime.date'>
```

অর্থাৎ:

```text
"2026-08-17"
       ↓
fromisoformat()
       ↓
date object
```

---

# 7️⃣ `date` Comparison ⭐⭐⭐

দুইটি date compare করা যায়।

```python
from datetime import date

d1 = date(2026, 8, 17)
d2 = date(2026, 12, 31)

print(d1 < d2)
```

Output:

```text
True
```

আর:

```python
print(d1 > d2)
```

Output:

```text
False
```

---

# 8️⃣ Equality

```python
d1 = date(2026, 8, 17)
d2 = date(2026, 8, 17)

print(d1 == d2)
```

Output:

```text
True
```

---

# 9️⃣ Practical Example — Birthday Check

```python
today = date.today()

birthday = date(
    2026,
    12,
    25
)

if today == birthday:

    print("Happy Birthday!")

else:

    print("Birthday is not today.")
```

---

# 🔟 `weekday()` ⭐⭐⭐

```python
d = date(2026, 8, 17)

print(d.weekday())
```

`weekday()` returns:

```text
Monday    → 0
Tuesday   → 1
Wednesday → 2
Thursday  → 3
Friday    → 4
Saturday  → 5
Sunday    → 6
```

---

# 1️⃣1️⃣ `isoweekday()`

```python
d = date(2026, 8, 17)

print(d.isoweekday())
```

Returns:

```text
Monday    → 1
Tuesday   → 2
Wednesday → 3
Thursday  → 4
Friday    → 5
Saturday  → 6
Sunday    → 7
```

---

# 1️⃣2️⃣ `strftime()` Preview

Day 6-এ বিস্তারিত শিখব।

আজ basic idea:

```python
d = date.today()

print(
    d.strftime("%d/%m/%Y")
)
```

Output-এর মতো:

```text
17/08/2026
```

Common codes:

|Code|Meaning|
|---|---|
|`%Y`|4-digit year|
|`%m`|month|
|`%d`|day|
|`%A`|weekday name|
|`%B`|month name|

Example:

```python
print(
    d.strftime("%A, %d %B %Y")
)
```

Output:

```text
Monday, 17 August 2026
```

---

# 1️⃣3️⃣ `replace()` ⭐⭐⭐

একটি date থেকে নতুন date তৈরি করতে:

```python
d = date(2026, 8, 17)

new_date = d.replace(
    year=2027
)

print(new_date)
```

Output:

```text
2027-08-17
```

Month:

```python
new_date = d.replace(
    month=12
)
```

Day:

```python
new_date = d.replace(
    day=25
)
```

⚠️ `date` object নিজে পরিবর্তিত হয় না; `replace()` নতুন object তৈরি করে।

---

# 1️⃣4️⃣ `toordinal()` ⭐⭐

প্রতিটি date-এর একটি ordinal number আছে।

```python
d = date(2026, 8, 17)

print(d.toordinal())
```

এটি নির্দিষ্ট Gregorian calendar reference থেকে সেই date-এর অবস্থানকে একটি integer হিসেবে দেয়।

তোমার সাধারণ application development-এ এটা খুব বেশি লাগবে না, তবে `date` API-এর অংশ হিসেবে জানা ভালো।

---

# 1️⃣5️⃣ `date.fromordinal()` ⭐⭐

Ordinal number থেকে আবার date:

```python
number = date(
    2026,
    8,
    17
).toordinal()

d = date.fromordinal(
    number
)

print(d)
```

Output:

```text
2026-08-17
```

Flow:

```text
date
 ↓
toordinal()
 ↓
integer
 ↓
fromordinal()
 ↓
date
```

---

# 1️⃣6️⃣ `min` এবং `max`

`date` class-এর supported range-এর boundary দেখতে পারো:

```python
print(date.min)
print(date.max)
```

এগুলো Python `date` object-এর সর্বনিম্ন এবং সর্বোচ্চ representable date।

---

# 1️⃣7️⃣ `date.resolution`

```python
print(date.resolution)
```

এটি দুইটি distinguishable `date` value-এর সবচেয়ে ছোট difference নির্দেশ করে।

Output:

```text
1 day, 0:00:00
```

অর্থাৎ `date`-এর resolution হলো **1 day**।

---

# 1️⃣8️⃣ Date Difference

দুইটি `date` subtract করলে `timedelta` পাওয়া যায়।

```python
from datetime import date

start = date(2026, 8, 1)
end = date(2026, 8, 17)

difference = end - start

print(difference)
```

Output:

```text
16 days, 0:00:00
```

এখানে:

```python
type(difference)
```

হবে:

```text
datetime.timedelta
```

`timedelta` আমরা **Day 8-এ বিস্তারিত** শিখব।

---

# 1️⃣9️⃣ কতদিন বাকি?

```python
from datetime import date

today = date.today()

exam_date = date(
    2026,
    12,
    1
)

remaining = exam_date - today

print(
    "Days remaining:",
    remaining.days
)
```

এটা real-world application-এ খুব useful।

---

# 2️⃣0️⃣ Past Date Check

```python
from datetime import date

today = date.today()

deadline = date(
    2026,
    8,
    10
)

if today > deadline:

    print("Deadline passed.")

else:

    print("Deadline is still active.")
```

---

# 2️⃣1️⃣ Future Date Check

```python
event_date = date(
    2026,
    12,
    25
)

if event_date > today:

    print("Event is in the future.")
```

---

# 2️⃣2️⃣ Date Sorting ⭐⭐⭐

একাধিক date:

```python
dates = [
    date(2026, 12, 1),
    date(2026, 8, 17),
    date(2026, 10, 5)
]
```

Sort:

```python
dates.sort()

print(dates)
```

Output:

```text
[
    2026-08-17,
    2026-10-05,
    2026-12-01
]
```

Reverse:

```python
dates.sort(
    reverse=True
)
```

---

# 2️⃣3️⃣ List থেকে Earliest Date

```python
earliest = min(dates)

print(earliest)
```

Latest:

```python
latest = max(dates)

print(latest)
```

এটা scheduling system-এ কাজে লাগে।

---

# 2️⃣4️⃣ JSON-এর সাথে `date` ⚠️

এখানে একটা গুরুত্বপূর্ণ বিষয়।

```python
import json
from datetime import date

data = {
    "created": date.today()
}
```

এখন:

```python
json.dumps(data)
```

সরাসরি কাজ করবে না, কারণ standard JSON `date` object বোঝে না।

তাই সাধারণভাবে date-কে string বানানো হয়:

```python
data = {
    "created": date.today().isoformat()
}
```

তারপর:

```python
json.dumps(data)
```

কাজ করবে।

JSON:

```json
{
    "created": "2026-08-17"
}
```

এটা তোমার আগের **JSON course-এর সাথে খুব important connection**।

---

# 2️⃣5️⃣ API-এর সাথে Date

API থেকে যদি আসে:

```json
{
    "name": "Exam",
    "date": "2026-12-01"
}
```

Python:

```python
from datetime import date

date_string = "2026-12-01"

exam_date = date.fromisoformat(
    date_string
)

print(exam_date)
```

এখন তুমি date compare করতে পারবে:

```python
if exam_date > date.today():
    print("Upcoming exam")
```

---

# 🧪 Day 2 Practice

## Exercise 1

তিনটি date তৈরি করো:

```text
2026-01-01
2026-06-15
2026-12-31
```

এবং তাদের:

```text
year
month
day
weekday
```

print করো।

---

## Exercise 2

এই string:

```python
"2026-10-25"
```

কে `date` object-এ convert করো।

---

## Exercise 3

আজকের date এবং তোমার একটি future exam date-এর difference বের করো।

---

## Exercise 4 ⭐

এই dates:

```python
dates = [
    date(2026, 12, 25),
    date(2026, 1, 10),
    date(2026, 6, 20),
    date(2026, 3, 15)
]
```

ascending order-এ sort করো।

---

## Exercise 5 ⭐⭐

একটি program বানাও:

```text
Enter deadline (YYYY-MM-DD):
```

তারপর বলবে:

```text
Deadline is in the future.
```

অথবা:

```text
Deadline has passed.
```

---

## Exercise 6 🔥

একটি event list:

```python
events = [
    {
        "name": "Python Exam",
        "date": "2026-09-10"
    },
    {
        "name": "Project Submission",
        "date": "2026-09-05"
    },
    {
        "name": "Presentation",
        "date": "2026-10-01"
    }
]
```

প্রতিটি date:

```python
date.fromisoformat()
```

দিয়ে convert করে **সবচেয়ে কাছের upcoming event** বের করার চেষ্টা করো।

---

# 🏆 Day 2 Mini Project

## 📅 Deadline Checker

Program:

```text
=============================
       DEADLINE CHECKER
=============================

Enter deadline:
2026-09-10

Today:
2026-08-17

Days remaining:
24

Status:
Upcoming
=============================
```

তুমি এখানে ব্যবহার করবে:

```python
date.today()
date.fromisoformat()
date - date
difference.days
```

---

# 📌 Day 2 Cheat Sheet

```python
from datetime import date
```

### Current date

```python
date.today()
```

### Create date

```python
date(2026, 8, 17)
```

### ISO → date

```python
date.fromisoformat(
    "2026-08-17"
)
```

### date → ISO

```python
d.isoformat()
```

### Components

```python
d.year
d.month
d.day
```

### Weekday

```python
d.weekday()
```

### ISO weekday

```python
d.isoweekday()
```

### Change date

```python
d.replace(
    year=2027
)
```

### Date difference

```python
date2 - date1
```

### Earliest

```python
min(dates)
```

### Latest

```python
max(dates)
```

### Ordinal

```python
d.toordinal()
```

### Ordinal → date

```python
date.fromordinal(n)
```

---

## 🚀 Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅ ← You are here
Day 3  → time Object                 ⏭️
Day 4  → datetime Object
Day 5  → Current Date/Time
Day 6  → strftime()
Day 7  → strptime()
Day 8  → timedelta
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 3-এ `time` object শিখব—hour, minute, second, microsecond, comparison, `isoformat()`, `fromisoformat()`, `replace()` এবং `datetime`-এর সাথে `time` combine করা।**



	# 🐍 Python `datetime` — Day 3

## `time` Object Complete Lesson

আজ আমরা `datetime` module-এর **`time` class** শিখব।

Official documentation: [Python `datetime.time` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#time-objects)

আজকের flow:

```text
time
 │
 ├── Create
 ├── hour / minute / second
 ├── microsecond
 ├── ISO format
 ├── String → time
 ├── Comparison
 ├── replace()
 ├── combine()
 └── Real-world usage
```

---

# 1️⃣ `time` কী?

`time` object শুধু **সময়** represent করে।

```text
Hour + Minute + Second + Microsecond
```

এতে date থাকে না।

```python
from datetime import time

t = time(14, 30, 15)

print(t)
```

Output:

```text
14:30:15
```

---

# 2️⃣ Import

```python
from datetime import time
```

অথবা:

```python
import datetime

t = datetime.time(14, 30)
```

দুটোই valid।

---

# 3️⃣ Basic `time()` Constructor

Syntax:

```python
time(
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)
```

Example:

```python
from datetime import time

t = time(
    14,
    30,
    45
)

print(t)
```

Output:

```text
14:30:45
```

---

# 4️⃣ Hour, Minute, Second

```python
from datetime import time

t = time(
    14,
    30,
    45
)

print(t.hour)
print(t.minute)
print(t.second)
```

Output:

```text
14
30
45
```

---

# 5️⃣ Microsecond ⭐

Python `datetime` maximum precision দেয় **microsecond** পর্যন্ত।

```python
t = time(
    14,
    30,
    45,
    123456
)

print(t)
```

Output:

```text
14:30:45.123456
```

Access:

```python
print(t.microsecond)
```

Output:

```text
123456
```

---

# 6️⃣ Valid Range

`hour`:

```text
0 → 23
```

`minute`:

```text
0 → 59
```

`second`:

```text
0 → 59
```

`microsecond`:

```text
0 → 999999
```

যেমন:

```python
time(23, 59, 59)
```

valid।

কিন্তু:

```python
time(25, 10, 10)
```

invalid, কারণ hour সর্বোচ্চ 23।

---

# 7️⃣ 12-Hour Clock vs Python

Python `time` object 24-hour representation ব্যবহার করে।

```python
time(14, 30)
```

মানে:

```text
2:30 PM
```

Python-এ:

```text
14:30
```

---

# 8️⃣ `isoformat()` ⭐⭐⭐

`time` object → string:

```python
t = time(
    14,
    30,
    45
)

print(t.isoformat())
```

Output:

```text
14:30:45
```

Microsecond থাকলে:

```python
t = time(
    14,
    30,
    45,
    123456
)

print(t.isoformat())
```

Output:

```text
14:30:45.123456
```

---

# 9️⃣ ISO String → `time` ⭐⭐⭐

ধরো API থেকে এসেছে:

```python
time_string = "14:30:45"
```

Convert:

```python
from datetime import time

t = time.fromisoformat(
    time_string
)

print(t)
```

Output:

```text
14:30:45
```

Flow:

```text
"14:30:45"
     ↓
fromisoformat()
     ↓
time object
```

এটা API/JSON processing-এ খুব useful।

---

# 🔟 `time` Comparison ⭐⭐⭐

দুইটি `time` compare করা যায়।

```python
from datetime import time

start = time(9, 0)
end = time(17, 0)

print(start < end)
```

Output:

```text
True
```

---

# 1️⃣1️⃣ Equality

```python
t1 = time(10, 30)
t2 = time(10, 30)

print(t1 == t2)
```

Output:

```text
True
```

---

# 1️⃣2️⃣ Office Hours Example

```python
from datetime import time

current = time(15, 30)

opening = time(9, 0)
closing = time(17, 0)

if opening <= current <= closing:
    print("Office is open.")
else:
    print("Office is closed.")
```

এটা real-world application-এর খুব common pattern।

---

# 1️⃣3️⃣ `replace()` ⭐⭐⭐

`time` object-এর অংশ পরিবর্তন করতে:

```python
from datetime import time

t = time(
    14,
    30,
    45
)

new_time = t.replace(
    hour=18
)

print(new_time)
```

Output:

```text
18:30:45
```

Minute পরিবর্তন:

```python
new_time = t.replace(
    minute=45
)
```

Second:

```python
new_time = t.replace(
    second=0
)
```

Microsecond:

```python
new_time = t.replace(
    microsecond=0
)
```

⚠️ `replace()` original object পরিবর্তন করে না; নতুন `time` object দেয়।

---

# 1️⃣4️⃣ `time` Immutable

এটা করা যাবে না:

```python
t.hour = 20
```

Error হবে।

এর পরিবর্তে:

```python
t = t.replace(
    hour=20
)
```

ব্যবহার করবে।

এটা খুব গুরুত্বপূর্ণ concept।

---

# 1️⃣5️⃣ `time.min`

সবচেয়ে ছোট representable `time`:

```python
from datetime import time

print(time.min)
```

Output-এর মতো:

```text
00:00:00
```

---

# 1️⃣6️⃣ `time.max`

```python
print(time.max)
```

Output:

```text
23:59:59.999999
```

---

# 1️⃣7️⃣ `time.resolution`

```python
print(time.resolution)
```

Output:

```text
0:00:00.000001
```

অর্থাৎ resolution:

```text
1 microsecond
```

---

# 1️⃣8️⃣ `tzinfo` — আজ শুধু ধারণা

`time` object timezone information ধারণ করতে পারে।

```python
t = time(
    14,
    30,
    tzinfo=some_timezone
)
```

কিন্তু timezone এখন বিস্তারিত শেখার দরকার নেই।

আমরা **Day 11–12**-তে:

```text
timezone
UTC
zoneinfo
aware datetime
naive datetime
```

বিস্তারিত করব।

---

# 1️⃣9️⃣ `time` + `date` = `datetime` ⭐⭐⭐

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ practical concept।

```python
from datetime import date, time, datetime

d = date(
    2026,
    8,
    17
)

t = time(
    14,
    30
)

dt = datetime.combine(
    d,
    t
)

print(dt)
```

Output:

```text
2026-08-17 14:30:00
```

Flow:

```text
date
2026-08-17
     +
time
14:30:00
     ↓
datetime
2026-08-17 14:30:00
```

---

# 2️⃣0️⃣ `datetime.time()`

উল্টো দিকেও যেতে পারো।

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    14,
    30
)

t = dt.time()

print(t)
```

Output:

```text
14:30:00
```

---

# 2️⃣1️⃣ `time` + JSON

আগের JSON course-এর সাথে connection।

এটা সরাসরি JSON serializable নয়:

```python
import json
from datetime import time

data = {
    "start_time": time(9, 30)
}

json.dumps(data)
```

তাই সাধারণভাবে:

```python
data = {
    "start_time": time(9, 30).isoformat()
}
```

তারপর:

```python
json.dumps(data)
```

Output:

```json
{
    "start_time": "09:30:00"
}
```

API/database-এর ক্ষেত্রে এই pattern খুব useful।

---

# 2️⃣2️⃣ API Response থেকে Time

ধরো API response:

```json
{
    "opening_time": "09:00:00",
    "closing_time": "17:00:00"
}
```

Python:

```python
from datetime import time

opening = time.fromisoformat(
    "09:00:00"
)

closing = time.fromisoformat(
    "17:00:00"
)

print(opening)
print(closing)
```

---

# 2️⃣3️⃣ Restaurant/Office Schedule

একটি practical example:

```python
from datetime import time

opening = time(9, 0)
closing = time(17, 0)

current = time(13, 45)

if opening <= current <= closing:
    status = "Open"
else:
    status = "Closed"

print(status)
```

Output:

```text
Open
```

---

# 2️⃣4️⃣ Multiple Time Slots

ধরো:

```python
from datetime import time

schedule = [
    time(9, 0),
    time(12, 30),
    time(15, 0),
    time(18, 30)
]
```

Loop:

```python
for t in schedule:
    print(t)
```

Output:

```text
09:00:00
12:30:00
15:00:00
18:30:00
```

---

# 2️⃣5️⃣ Sorting Times ⭐⭐⭐

```python
times = [
    time(18, 30),
    time(9, 0),
    time(12, 30),
    time(7, 45)
]

times.sort()

for t in times:
    print(t)
```

Output:

```text
07:45:00
09:00:00
12:30:00
18:30:00
```

---

# 2️⃣6️⃣ Earliest / Latest

```python
earliest = min(times)
latest = max(times)

print("Earliest:", earliest)
print("Latest:", latest)
```

---

# 2️⃣7️⃣ Time Formatting Preview

Day 6-এ `strftime()` বিস্তারিত করব।

আজ basic:

```python
from datetime import time

t = time(14, 30)

print(
    t.strftime("%H:%M")
)
```

Output:

```text
14:30
```

12-hour format:

```python
print(
    t.strftime("%I:%M %p")
)
```

Output:

```text
02:30 PM
```

---

# 2️⃣8️⃣ Important Format Codes

|Code|Meaning|Example|
|---|---|---|
|`%H`|24-hour|`14`|
|`%I`|12-hour|`02`|
|`%M`|Minute|`30`|
|`%S`|Second|`45`|
|`%f`|Microsecond|`123456`|
|`%p`|AM/PM|`PM`|

---

# 2️⃣9️⃣ Important Difference: `time` vs `timedelta`

এগুলো গুলিয়ে ফেলবে না।

### `time`

একটি দিনের নির্দিষ্ট সময়:

```text
14:30:00
```

### `timedelta`

সময়/তারিখের duration:

```text
2 hours
5 days
30 minutes
```

যেমন:

```python
from datetime import timedelta

duration = timedelta(
    hours=2
)
```

`timedelta` আমরা Day 8-এ বিস্তারিত করব।

---

# 🧪 Day 3 Practice

### Exercise 1

তৈরি করো:

```text
09:30:00
14:45:30
23:59:59
```

এবং তাদের:

```text
hour
minute
second
```

print করো।

---

### Exercise 2

এই string:

```python
"18:45:30"
```

কে `time` object-এ convert করো।

---

### Exercise 3

দুটি time:

```python
opening = time(9, 0)
closing = time(18, 0)
```

এবং user-এর input time office hours-এর মধ্যে কিনা check করো।

---

### Exercise 4 ⭐

এই times:

```python
times = [
    time(15, 30),
    time(8, 45),
    time(20, 15),
    time(12, 0)
]
```

ascending order-এ sort করো।

---

### Exercise 5 ⭐⭐

একটি program বানাও:

```text
Enter current time (HH:MM):
```

তারপর output:

```text
Office Status: OPEN
```

অথবা:

```text
Office Status: CLOSED
```

Office:

```text
09:00 → 17:00
```

---

### Exercise 6 🔥

একটি `date` এবং `time` নিয়ে complete `datetime` বানাও:

```text
Date: 2026-09-10
Time: 14:30
```

Expected:

```text
2026-09-10 14:30:00
```

Use:

```python
datetime.combine()
```

---

# 🏆 Day 3 Mini Project

## 🕐 Office Time Checker

Program:

```text
==============================
       OFFICE CHECKER
==============================

Office Opens : 09:00
Office Closes: 17:00

Enter current time (HH:MM):
14:30

Status: OPEN
==============================
```

তুমি ব্যবহার করবে:

```python
time()
time.fromisoformat()
time.hour
time.minute
strftime()
comparison
```

---

# 📌 Day 3 Cheat Sheet

```python
from datetime import time
```

### Create

```python
time(14, 30, 45)
```

### Components

```python
t.hour
t.minute
t.second
t.microsecond
```

### ISO

```python
t.isoformat()
```

### String → time

```python
time.fromisoformat(
    "14:30:45"
)
```

### Modify

```python
t.replace(
    hour=18
)
```

### Min

```python
time.min
```

### Max

```python
time.max
```

### Resolution

```python
time.resolution
```

### Date + Time

```python
datetime.combine(
    d,
    t
)
```

### Datetime → Time

```python
dt.time()
```

---

# 🚀 Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅ ← You are here
Day 4  → datetime Object             ⏭️
Day 5  → Current Date/Time
Day 6  → strftime()
Day 7  → strptime()
Day 8  → timedelta
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 4-এ আমরা `datetime` object-এর ওপর deep dive করব—`datetime()` constructor, `now()`, `combine()`, `.date()`, `.time()`, comparison, `replace()`, ISO conversion এবং date+time নিয়ে real-world examples।**

# 🐍 Python `datetime` — Day 4

## `datetime` Object Complete Lesson

আজ আমরা `datetime` class গভীরভাবে শিখব।

Official documentation: [Python `datetime` official documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#datetime-objects)

আজকের লক্ষ্য:

```text
datetime
   │
   ├── Create
   ├── now()
   ├── today()
   ├── Components
   ├── date()
   ├── time()
   ├── combine()
   ├── ISO format
   ├── Comparison
   ├── replace()
   ├── Timestamp
   └── Practical usage
```

---

# 1️⃣ `datetime` কী?

`datetime` object একই সাথে রাখে:

```text
Date + Time
```

অর্থাৎ:

```text
Year
Month
Day
Hour
Minute
Second
Microsecond
```

Example:

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    14,
    30,
    45
)

print(dt)
```

Output:

```text
2026-08-17 14:30:45
```

---

# 2️⃣ Import

সবচেয়ে সহজ:

```python
from datetime import datetime
```

তারপর:

```python
datetime.now()
```

---

# 3️⃣ `datetime()` Constructor ⭐⭐⭐

Basic syntax:

```python
datetime(
    year,
    month,
    day,
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)
```

Example:

```python
dt = datetime(
    2026,
    12,
    31,
    23,
    59,
    59
)

print(dt)
```

Output:

```text
2026-12-31 23:59:59
```

---

# 4️⃣ Current Date & Time — `now()`

```python
from datetime import datetime

now = datetime.now()

print(now)
```

Output-এর মতো:

```text
2026-08-17 17:45:20.123456
```

এটাই সবচেয়ে বেশি ব্যবহৃত method-গুলোর একটি।

---

# 5️⃣ `today()`

```python
now = datetime.today()

print(now)
```

`datetime.today()` বর্তমান local date এবং time দেয়।

সাধারণভাবে:

```python
datetime.now()
```

ব্যবহার করাই বেশি পরিষ্কার।

---

# 6️⃣ Components ⭐⭐⭐

```python
dt = datetime.now()

print(dt.year)
print(dt.month)
print(dt.day)

print(dt.hour)
print(dt.minute)
print(dt.second)
print(dt.microsecond)
```

Structure:

```text
datetime
├── year
├── month
├── day
├── hour
├── minute
├── second
└── microsecond
```

---

# 7️⃣ `.date()` ⭐⭐⭐

একটি `datetime` থেকে শুধু date:

```python
dt = datetime.now()

d = dt.date()

print(d)
```

Output:

```text
2026-08-17
```

Type:

```python
print(type(d))
```

```text
<class 'datetime.date'>
```

---

# 8️⃣ `.time()` ⭐⭐⭐

শুধু time:

```python
dt = datetime.now()

t = dt.time()

print(t)
```

Output:

```text
17:45:20.123456
```

Type:

```python
print(type(t))
```

```text
<class 'datetime.time'>
```

---

# 9️⃣ Date + Time → Datetime

Day 3-এ আমরা এটা দেখেছি।

```python
from datetime import date, time, datetime

d = date(2026, 8, 17)

t = time(14, 30)

dt = datetime.combine(
    d,
    t
)

print(dt)
```

Output:

```text
2026-08-17 14:30:00
```

এটা scheduling system-এ খুব useful।

---

# 🔟 `datetime.combine()` with `time`

```python
d = date.today()
t = time(18, 30)

dt = datetime.combine(d, t)

print(dt)
```

মানে:

```text
Today's Date
     +
18:30
     ↓
Complete datetime
```

---

# 1️⃣1️⃣ `isoformat()` ⭐⭐⭐

Datetime → ISO string:

```python
dt = datetime(
    2026,
    8,
    17,
    14,
    30,
    45
)

print(dt.isoformat())
```

Output:

```text
2026-08-17T14:30:45
```

খেয়াল করো:

```text
2026-08-17T14:30:45
          ↑
          T
```

ISO 8601 representation-এ date এবং time আলাদা করতে `T` ব্যবহার করা হয়।

---

# 1️⃣2️⃣ ISO String → Datetime ⭐⭐⭐

```python
text = "2026-08-17T14:30:45"

dt = datetime.fromisoformat(text)

print(dt)
```

Output:

```text
2026-08-17 14:30:45
```

Flow:

```text
String
   ↓
fromisoformat()
   ↓
datetime object
```

---

# 1️⃣3️⃣ JSON + Datetime

এটা তোমার আগের `json` course-এর সাথে খুব গুরুত্বপূর্ণ connection।

এটা সরাসরি:

```python
import json

data = {
    "created_at": datetime.now()
}

json.dumps(data)
```

করলে সমস্যা হবে, কারণ standard JSON সরাসরি Python `datetime` object serialize করতে পারে না।

তাই:

```python
data = {
    "created_at": datetime.now().isoformat()
}
```

তারপর:

```python
json.dumps(data)
```

Output:

```json
{
    "created_at": "2026-08-17T17:45:20.123456"
}
```

API development-এ এই pattern খুব common।

---

# 1️⃣4️⃣ `replace()` ⭐⭐⭐

Datetime-এর কোনো component পরিবর্তন করতে:

```python
dt = datetime(
    2026,
    8,
    17,
    14,
    30
)

new_dt = dt.replace(
    year=2027
)

print(new_dt)
```

Output:

```text
2027-08-17 14:30:00
```

একসাথে:

```python
new_dt = dt.replace(
    year=2027,
    month=12,
    day=25,
    hour=10,
    minute=15
)
```

---

# 1️⃣5️⃣ `datetime` Immutable

এটা করা যাবে না:

```python
dt.year = 2027
```

কারণ `datetime` immutable।

ব্যবহার করবে:

```python
dt = dt.replace(
    year=2027
)
```

---

# 1️⃣6️⃣ Comparison ⭐⭐⭐

দুইটি datetime compare করা যায়।

```python
start = datetime(
    2026,
    8,
    17,
    9,
    0
)

end = datetime(
    2026,
    8,
    17,
    17,
    0
)

print(start < end)
```

Output:

```text
True
```

---

# 1️⃣7️⃣ Event Check

```python
event = datetime(
    2026,
    12,
    25,
    10,
    0
)

now = datetime.now()

if event > now:
    print("Event is upcoming.")
else:
    print("Event has passed.")
```

---

# 1️⃣8️⃣ DateTime Difference

দুইটি datetime subtract করলে `timedelta` পাওয়া যায়।

```python
start = datetime(
    2026,
    8,
    17,
    9,
    0
)

end = datetime(
    2026,
    8,
    17,
    17,
    0
)

difference = end - start

print(difference)
```

Output:

```text
8:00:00
```

`timedelta` আমরা Day 8-এ বিস্তারিত করব।

---

# 1️⃣9️⃣ `weekday()`

```python
dt = datetime.now()

print(dt.weekday())
```

```text
Monday    → 0
Tuesday   → 1
Wednesday → 2
Thursday  → 3
Friday    → 4
Saturday  → 5
Sunday    → 6
```

---

# 2️⃣0️⃣ `isoweekday()`

```python
print(dt.isoweekday())
```

```text
Monday    → 1
Tuesday   → 2
Wednesday → 3
Thursday  → 4
Friday    → 5
Saturday  → 6
Sunday    → 7
```

---

# 2️⃣1️⃣ `isocalendar()`

একটি datetime কোন ISO week-এর মধ্যে আছে জানতে:

```python
dt = datetime.now()

print(dt.isocalendar())
```

এতে পাওয়া যায়:

```text
ISO year
ISO week
ISO weekday
```

Specific:

```python
info = dt.isocalendar()

print(info.year)
print(info.week)
print(info.weekday)
```

এটি reporting এবং weekly analytics-এর কাজে লাগতে পারে।

---

# 2️⃣2️⃣ `date()` + `time()` আবার

```python
dt = datetime.now()

print("Date:", dt.date())
print("Time:", dt.time())
```

Output:

```text
Date: 2026-08-17
Time: 17:45:20.123456
```

---

# 2️⃣3️⃣ `datetime.min`

```python
print(datetime.min)
```

এটি `datetime` class-এর সর্বনিম্ন representable datetime।

---

# 2️⃣4️⃣ `datetime.max`

```python
print(datetime.max)
```

এটি সর্বোচ্চ representable datetime।

---

# 2️⃣5️⃣ `datetime.resolution`

```python
print(datetime.resolution)
```

Output:

```text
0:00:00.000001
```

অর্থাৎ:

```text
1 microsecond
```

---

# 2️⃣6️⃣ Practical Example — Login Time

ধরো user login করেছে:

```python
login_time = datetime.now()

print(
    "Login:",
    login_time.isoformat()
)
```

JSON/API-friendly:

```python
login_data = {
    "login_time": login_time.isoformat()
}

print(login_data)
```

---

# 2️⃣7️⃣ Practical Example — Created At / Updated At

Backend application-এ খুব common:

```python
created_at = datetime.now()
updated_at = datetime.now()

print("Created:", created_at)
print("Updated:", updated_at)
```

Database/API response-এ এগুলো সাধারণত timestamp হিসেবে রাখা হয়।

---

# 2️⃣8️⃣ Practical Example — Event Scheduler

```python
from datetime import datetime

event_time = datetime(
    2026,
    9,
    1,
    15,
    30
)

now = datetime.now()

if event_time > now:
    print("Upcoming event")
elif event_time == now:
    print("Event is happening now")
else:
    print("Event has ended")
```

---

# 2️⃣9️⃣ Practical Example — Appointment

```python
appointment = datetime(
    2026,
    9,
    10,
    10,
    30
)

now = datetime.now()

if appointment > now:
    print("Appointment is upcoming.")
else:
    print("Appointment time has passed.")
```

---

# 3️⃣0️⃣ `datetime` → JSON → API

একটি practical flow:

```text
datetime object
      ↓
isoformat()
      ↓
string
      ↓
JSON
      ↓
API
```

Example:

```python
from datetime import datetime
import json

data = {
    "event": "Python Exam",
    "scheduled_at": datetime(
        2026,
        9,
        10,
        10,
        30
    ).isoformat()
}

json_data = json.dumps(data)

print(json_data)
```

Output:

```json
{
    "event": "Python Exam",
    "scheduled_at": "2026-09-10T10:30:00"
}
```

এটা তোমার **Python + Django REST API** কাজের জন্য খুব গুরুত্বপূর্ণ pattern।

---

# 🧪 Day 4 Practice

### Exercise 1

এই datetime তৈরি করো:

```text
2026-12-31 23:59:59
```

তারপর আলাদা করে print করো:

```text
year
month
day
hour
minute
second
```

---

### Exercise 2

বর্তমান datetime থেকে:

```text
date
time
weekday
ISO format
```

print করো।

---

### Exercise 3

এই ISO string:

```text
2026-10-25T14:30:00
```

কে datetime object-এ convert করো।

---

### Exercise 4 ⭐

দুটি datetime:

```text
Start: 2026-08-17 09:00
End:   2026-08-17 17:30
```

এর difference বের করো।

---

### Exercise 5 ⭐⭐

একটি program বানাও:

```text
Enter event datetime:
2026-12-25 10:30
```

তারপর বলবে:

```text
Upcoming Event
```

অথবা:

```text
Event Passed
```

---

### Exercise 6 🔥

এই data:

```python
events = [
    {
        "name": "Python Exam",
        "datetime": "2026-09-10T10:00:00"
    },
    {
        "name": "Project Presentation",
        "datetime": "2026-09-20T15:30:00"
    },
    {
        "name": "Final Exam",
        "datetime": "2026-12-01T09:00:00"
    }
]
```

প্রতিটি string-কে `datetime` object-এ convert করো এবং **সবচেয়ে কাছের upcoming event** বের করার চেষ্টা করো।

---

# 🏆 Day 4 Mini Project

## 📅 Event Scheduler

Input:

```text
==============================
       EVENT SCHEDULER
==============================

Event name:
Python Exam

Event date:
2026-09-10

Event time:
10:30

==============================
```

Program internally:

```text
date
  +
time
  ↓
datetime
  ↓
compare with datetime.now()
  ↓
Upcoming / Passed
```

শেষে:

```text
Event: Python Exam
Scheduled: 2026-09-10 10:30:00
Status: Upcoming
```

---

# 📌 Day 4 Cheat Sheet

```python
from datetime import datetime
```

### Current

```python
datetime.now()
```

### Today

```python
datetime.today()
```

### Create

```python
datetime(
    2026,
    8,
    17,
    14,
    30
)
```

### Components

```python
dt.year
dt.month
dt.day
dt.hour
dt.minute
dt.second
dt.microsecond
```

### Extract date

```python
dt.date()
```

### Extract time

```python
dt.time()
```

### Date + time

```python
datetime.combine(d, t)
```

### ISO

```python
dt.isoformat()
```

### ISO → datetime

```python
datetime.fromisoformat(text)
```

### Modify

```python
dt.replace(
    hour=10
)
```

### Compare

```python
dt1 < dt2
dt1 > dt2
dt1 == dt2
```

### Difference

```python
dt2 - dt1
```

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅ ← YOU ARE HERE
Day 5  → Current Date/Time
Day 6  → strftime()
Day 7  → strptime()
Day 8  → timedelta
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**পরের Day 5-এ `now()`, `today()`, UTC/current time-এর concept, system time বনাম application time এবং কোন ক্ষেত্রে কোনটা ব্যবহার করবে—এসব পরিষ্কার করব।**



# 🐍 Python `datetime` — Day 5

## Current Date & Time — `now()`, `today()`, UTC এবং Time Concepts

Official documentation: [Python `datetime` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

আজকের মূল লক্ষ্য হলো **কখন কোন current-time function ব্যবহার করবে** সেটা পরিষ্কারভাবে বোঝা।

```text
Current Time
     │
     ├── datetime.now()
     ├── datetime.today()
     ├── datetime.now(timezone.utc)
     └── datetime.now(ZoneInfo(...))
```

---

# 1️⃣ `datetime.now()` ⭐⭐⭐

সবচেয়ে basic current local date + time:

```python
from datetime import datetime

now = datetime.now()

print(now)
```

উদাহরণ:

```text
2026-08-17 18:20:35.123456
```

এখানে:

```text
2026-08-17 → Date
18:20:35   → Time
```

---

# 2️⃣ `datetime.today()`

```python
from datetime import datetime

today = datetime.today()

print(today)
```

এটাও current **local datetime** দেয়।

তাই beginner হিসেবে:

```python
datetime.now()
```

ব্যবহার করাই সবচেয়ে পরিষ্কার।

---

# 3️⃣ `date.today()` বনাম `datetime.today()`

এগুলো গুলিয়ে ফেলবে না।

### শুধু Date:

```python
from datetime import date

today = date.today()

print(today)
```

Output:

```text
2026-08-17
```

### Date + Time:

```python
from datetime import datetime

now = datetime.now()

print(now)
```

Output:

```text
2026-08-17 18:20:35
```

### মনে রাখো:

|Function|Result|
|---|---|
|`date.today()`|শুধু date|
|`datetime.today()`|date + time|
|`datetime.now()`|date + time|

---

# 4️⃣ `datetime.now()` কেন বেশি ব্যবহার করব?

কারণ এটা খুব পরিষ্কারভাবে বোঝায়:

> "আমি এখনকার datetime চাই।"

```python
now = datetime.now()
```

Backend application-এ:

```python
created_at = datetime.now()
```

এরকম code দেখতে পারো।

---

# 5️⃣ Local Time কী?

Local time হলো তোমার computer/system-এর configured timezone অনুযায়ী সময়।

```python
from datetime import datetime

now = datetime.now()

print(now)
```

এটি timezone information ছাড়াই একটি **naive datetime** দেয়।

এখানে গুরুত্বপূর্ণ distinction:

```text
naive datetime
      ↓
timezone information নেই
```

---

# 6️⃣ Naive vs Aware Datetime ⭐⭐⭐

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ concept।

### Naive

```python
from datetime import datetime

dt = datetime.now()

print(dt.tzinfo)
```

Output:

```text
None
```

অর্থাৎ:

```text
datetime
   ↓
timezone information নেই
   ↓
Naive
```

### Aware

Timezone explicitly দেওয়া হলে datetime timezone-aware হতে পারে।

```python
from datetime import datetime, timezone

dt = datetime.now(timezone.utc)

print(dt)
print(dt.tzinfo)
```

এখানে timezone information আছে।

```text
datetime
   ↓
UTC timezone
   ↓
Aware datetime
```

---

# 7️⃣ UTC কী? 🌍

UTC হলো:

**Coordinated Universal Time**

Software system-এ একটি common reference time হিসেবে UTC খুব গুরুত্বপূর্ণ।

বিশেষ করে:

```text
Backend
API
Database
Cloud
Distributed Systems
Logging
```

এগুলোতে UTC ব্যবহার করা খুব common।

---

# 8️⃣ Current UTC Time ⭐⭐⭐

Modern Python-এ:

```python
from datetime import datetime, timezone

utc_now = datetime.now(timezone.utc)

print(utc_now)
```

উদাহরণ:

```text
2026-08-17 12:20:35+00:00
```

শেষের:

```text
+00:00
```

মানে UTC offset।

---

# 9️⃣ `timezone.utc`

```python
from datetime import timezone

print(timezone.utc)
```

এটি Python-এর built-in UTC timezone object।

তাই:

```python
datetime.now(timezone.utc)
```

মানে:

> Current time as an aware UTC datetime.

---

# 🔟 Naive UTC নিয়ে সতর্কতা

পুরনো code-এ তুমি দেখতে পারো:

```python
datetime.utcnow()
```

কিন্তু modern Python development-এ timezone-aware UTC-এর জন্য:

```python
datetime.now(timezone.utc)
```

ব্যবহার করা ভালো।

অর্থাৎ:

```python
# Prefer
datetime.now(timezone.utc)
```

---

# 1️⃣1️⃣ Local vs UTC

ধরো:

```python
from datetime import datetime, timezone

local_time = datetime.now()

utc_time = datetime.now(timezone.utc)

print("Local:", local_time)
print("UTC:", utc_time)
```

Conceptually:

```text
Local Time
     ↓
তোমার system/location-এর local clock

UTC
     ↓
Global reference time
```

---

# 1️⃣2️⃣ `tzinfo`

Datetime-এর timezone information দেখতে:

```python
from datetime import datetime, timezone

local_time = datetime.now()

utc_time = datetime.now(timezone.utc)

print(local_time.tzinfo)
print(utc_time.tzinfo)
```

Result conceptually:

```text
None
UTC
```

---

# 1️⃣3️⃣ `utcoffset()`

Aware datetime-এর UTC offset দেখতে:

```python
from datetime import datetime, timezone

dt = datetime.now(timezone.utc)

print(dt.utcoffset())
```

UTC-এর ক্ষেত্রে:

```text
0:00:00
```

---

# 1️⃣4️⃣ `timestamp()` ⭐⭐⭐

একটি datetime থেকে Unix timestamp পাওয়া যায়।

```python
from datetime import datetime

dt = datetime.now()

timestamp = dt.timestamp()

print(timestamp)
```

Output-এর মতো:

```text
1786962035.123
```

এটি একটি number।

Concept:

```text
datetime
   ↓
timestamp()
   ↓
Unix timestamp
```

Timestamp আমরা **Day 10-এ বিস্তারিত** করব।

---

# 1️⃣5️⃣ `fromtimestamp()`

Timestamp থেকে local datetime:

```python
from datetime import datetime

timestamp = 1786962035

dt = datetime.fromtimestamp(
    timestamp
)

print(dt)
```

Flow:

```text
timestamp
    ↓
fromtimestamp()
    ↓
datetime
```

---

# 1️⃣6️⃣ UTC Timestamp

UTC context-এর জন্য:

```python
from datetime import datetime, timezone

timestamp = 1786962035

dt = datetime.fromtimestamp(
    timestamp,
    timezone.utc
)

print(dt)
```

এখানে তুমি একটি timezone-aware UTC datetime পাবে।

---

# 1️⃣7️⃣ Practical: Logging

একটি application-এর log:

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)

print(
    f"[{now.isoformat()}] User logged in"
)
```

Output-এর মতো:

```text
[2026-08-17T12:20:35+00:00] User logged in
```

এটা production backend/logging-এ খুব useful pattern।

---

# 1️⃣8️⃣ Practical: Created At

```python
from datetime import datetime, timezone

user = {
    "name": "Rahim",
    "created_at": datetime.now(
        timezone.utc
    ).isoformat()
}

print(user)
```

Result:

```python
{
    "name": "Rahim",
    "created_at": "2026-08-17T12:20:35+00:00"
}
```

এটা JSON/API-friendly।

---

# 1️⃣9️⃣ Practical: API Data

ধরো API থেকে:

```json
{
    "created_at": "2026-08-17T12:20:35+00:00"
}
```

Python:

```python
from datetime import datetime

text = "2026-08-17T12:20:35+00:00"

dt = datetime.fromisoformat(text)

print(dt)
print(dt.tzinfo)
```

এখন `dt` timezone-aware।

---

# 2️⃣0️⃣ Current Date Only

যদি শুধু current date দরকার:

```python
from datetime import date

today = date.today()

print(today)
```

যেমন:

```text
2026-08-17
```

---

# 2️⃣1️⃣ Current Time Only

শুধু current time দরকার হলে:

```python
from datetime import datetime

current_time = datetime.now().time()

print(current_time)
```

Output:

```text
18:20:35.123456
```

---

# 2️⃣2️⃣ Current UTC Date

```python
from datetime import datetime, timezone

utc_date = datetime.now(
    timezone.utc
).date()

print(utc_date)
```

---

# 2️⃣3️⃣ Current UTC Time

```python
from datetime import datetime, timezone

utc_time = datetime.now(
    timezone.utc
).time()

print(utc_time)
```

---

# 2️⃣4️⃣ Important: Naive Datetime Compare করা

দুটি naive datetime:

```python
from datetime import datetime

dt1 = datetime.now()
dt2 = datetime.now()

print(dt1 < dt2)
```

এটা ঠিক আছে কারণ দুটো একই ধরনের naive datetime।

---

# 2️⃣5️⃣ Naive + Aware Mix করা যাবে না ⚠️

যেমন:

```python
from datetime import datetime, timezone

naive = datetime.now()

aware = datetime.now(
    timezone.utc
)
```

তারপর:

```python
naive < aware
```

করলে সমস্যা হবে।

কারণ:

```text
Naive
  VS
Aware
```

তাদের সরাসরি compare করা উচিত নয়।

---

# 2️⃣6️⃣ কেন এটা গুরুত্বপূর্ণ?

ধরো তোমার application:

```text
Bangladesh
USA
UK
Japan
```

সব জায়গার user ব্যবহার করছে।

যদি শুধু local naive datetime রাখো:

```text
2026-08-17 10:00
```

তাহলে প্রশ্ন:

> কোন timezone-এর 10:00?

বোঝা কঠিন।

Timezone-aware datetime:

```text
2026-08-17T10:00:00+06:00
```

হলে offset জানা যায়।

---

# 2️⃣7️⃣ Best Practice Concept ⭐⭐⭐

Production application-এর জন্য সাধারণ ধারণা:

```text
Store
  ↓
UTC
  ↓
Database/API

Display
  ↓
User's local timezone
```

মানে:

```text
Database
    ↓
UTC datetime
    ↓
User-এর timezone
    ↓
UI
```

Timezone conversion আমরা **Day 11–12**-তে বিস্তারিত করব।

---

# 2️⃣8️⃣ `now()` বনাম `today()` — Final Comparison

|Function|Result|Use|
|---|---|---|
|`date.today()`|Date only|আজকের তারিখ|
|`datetime.today()`|Local datetime|Current local datetime|
|`datetime.now()`|Local datetime|সাধারণত preferred|
|`datetime.now(timezone.utc)`|Aware UTC datetime|Backend/API/UTC|

---

# 🧪 Day 5 Practice

## Exercise 1

Print করো:

```text
Current Date
Current Time
Current Datetime
```

---

## Exercise 2

Print করো:

```text
Local datetime
UTC datetime
```

তারপর তাদের `tzinfo` দেখাও।

---

## Exercise 3

এই code-এর output explain করো:

```python
from datetime import datetime, timezone

a = datetime.now()
b = datetime.now(timezone.utc)

print(a)
print(a.tzinfo)

print(b)
print(b.tzinfo)
```

---

## Exercise 4 ⭐

একটি log system বানাও:

```text
[2026-08-17T12:30:00+00:00] Application started
[2026-08-17T12:30:05+00:00] User logged in
```

UTC ব্যবহার করবে।

---

## Exercise 5 ⭐⭐

একটি dictionary বানাও:

```python
{
    "username": "atiar",
    "created_at": ...
}
```

`created_at`-এ UTC datetime-এর ISO string রাখো।

---

## Exercise 6 🔥

একটি program বানাও যেটা output করবে:

```text
==============================
       TIME INFORMATION
==============================

Local Time : ...
UTC Time   : ...

Local TZ   : ...
UTC TZ     : ...

==============================
```

---

# 🏆 Day 5 Mini Project

## 🌍 UTC Logger

```python
from datetime import datetime, timezone

def log(message):
    now = datetime.now(timezone.utc)

    print(
        f"[{now.isoformat()}] {message}"
    )


log("Application started")
log("User logged in")
log("Processing completed")
```

Output-এর মতো:

```text
[2026-08-17T12:30:00+00:00] Application started
[2026-08-17T12:30:01+00:00] User logged in
[2026-08-17T12:30:02+00:00] Processing completed
```

এখানে তুমি একসাথে শিখলে:

```text
datetime.now()
timezone.utc
aware datetime
tzinfo
isoformat()
UTC logging
```

---

# 📌 Day 5 Cheat Sheet

```python
from datetime import date, datetime, timezone
```

### Current date

```python
date.today()
```

### Local datetime

```python
datetime.now()
```

### Current local date/time

```python
datetime.today()
```

### UTC datetime

```python
datetime.now(timezone.utc)
```

### Timezone info

```python
dt.tzinfo
```

### UTC offset

```python
dt.utcoffset()
```

### Current time

```python
datetime.now().time()
```

### Current UTC date

```python
datetime.now(
    timezone.utc
).date()
```

### ISO string

```python
dt.isoformat()
```

---

# 🚀 Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅ ← YOU ARE HERE
Day 6  → strftime()                  ⏭️
Day 7  → strptime()
Day 8  → timedelta
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 6-এ আমরা `strftime()` পুরোপুরি শিখব—একটি datetime/date/time object-কে যেকোনো সুন্দর string format-এ কীভাবে convert করতে হয়।**


# 🐍 Python `datetime` — Day 6

## `strftime()` — Date/Time → String

আজকের topic খুবই important, কারণ Python backend, Django, API, logging, report, file naming—সব জায়গায় date/time সুন্দর format করার দরকার হয়।

Official documentation: [Python `strftime()` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#datetime.datetime.strftime)

আজকের মূল concept:

```text
datetime/date/time object
          ↓
      strftime()
          ↓
       String
```

---

# 1️⃣ `strftime()` কী?

`strftime()` ব্যবহার করে একটি date/time object-কে **নিজের পছন্দের string format**-এ convert করা যায়।

```python
from datetime import datetime

dt = datetime(2026, 8, 17, 14, 30)

result = dt.strftime("%Y-%m-%d")

print(result)
```

Output:

```text
2026-08-17
```

এখানে:

```text
datetime object
      ↓
strftime()
      ↓
"2026-08-17"
```

---

# 2️⃣ Basic Syntax

```python
object.strftime(format)
```

Example:

```python
dt.strftime("%Y-%m-%d")
```

---

# 3️⃣ সবচেয়ে গুরুত্বপূর্ণ Format Codes ⭐⭐⭐

|Code|Meaning|Example|
|---|---|---|
|`%Y`|4-digit year|`2026`|
|`%y`|2-digit year|`26`|
|`%m`|Month number|`08`|
|`%B`|Full month name|`August`|
|`%b`|Short month name|`Aug`|
|`%d`|Day|`17`|
|`%A`|Full weekday|`Monday`|
|`%a`|Short weekday|`Mon`|
|`%H`|Hour 24-hour|`14`|
|`%I`|Hour 12-hour|`02`|
|`%M`|Minute|`30`|
|`%S`|Second|`45`|
|`%f`|Microsecond|`123456`|
|`%p`|AM/PM|`PM`|

এগুলো **মুখস্থ করার চেয়ে নিয়মিত ব্যবহার করে শেখা** ভালো।

---

# 4️⃣ `%Y` — Year

```python
dt.strftime("%Y")
```

Output:

```text
2026
```

---

# 5️⃣ `%y` — Short Year

```python
dt.strftime("%y")
```

Output:

```text
26
```

Difference:

```text
%Y → 2026
%y → 26
```

---

# 6️⃣ `%m` — Month Number

```python
dt.strftime("%m")
```

Output:

```text
08
```

August = `08`

---

# 7️⃣ `%B` — Full Month Name

```python
dt.strftime("%B")
```

Output:

```text
August
```

---

# 8️⃣ `%b` — Short Month

```python
dt.strftime("%b")
```

Output:

```text
Aug
```

---

# 9️⃣ `%d` — Day

```python
dt.strftime("%d")
```

Output:

```text
17
```

---

# 🔟 Weekday — `%A`

```python
dt.strftime("%A")
```

Output:

```text
Monday
```

Short form:

```python
dt.strftime("%a")
```

Output:

```text
Mon
```

---

# 1️⃣1️⃣ Date Format ⭐⭐⭐

### `YYYY-MM-DD`

```python
dt.strftime("%Y-%m-%d")
```

Output:

```text
2026-08-17
```

### `DD-MM-YYYY`

```python
dt.strftime("%d-%m-%Y")
```

Output:

```text
17-08-2026
```

### `DD/MM/YYYY`

```python
dt.strftime("%d/%m/%Y")
```

Output:

```text
17/08/2026
```

---

# 1️⃣2️⃣ Month Name Format

```python
dt.strftime("%d %B %Y")
```

Output:

```text
17 August 2026
```

আরও সুন্দর:

```python
dt.strftime("%A, %d %B %Y")
```

Output:

```text
Monday, 17 August 2026
```

---

# 1️⃣3️⃣ Time Format ⭐⭐⭐

ধরো:

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    14,
    30,
    45
)
```

### 24-hour

```python
print(dt.strftime("%H:%M:%S"))
```

Output:

```text
14:30:45
```

---

# 1️⃣4️⃣ 12-hour Format

```python
print(dt.strftime("%I:%M:%S %p"))
```

Output:

```text
02:30:45 PM
```

খুব গুরুত্বপূর্ণ:

```text
%H → 24-hour
%I → 12-hour
%p → AM/PM
```

---

# 1️⃣5️⃣ শুধুমাত্র Hour

```python
dt.strftime("%H")
```

```text
14
```

12-hour:

```python
dt.strftime("%I")
```

```text
02
```

---

# 1️⃣6️⃣ Minute এবং Second

```python
print(dt.strftime("%M"))
print(dt.strftime("%S"))
```

Output:

```text
30
45
```

---

# 1️⃣7️⃣ Microsecond

```python
dt = datetime(
    2026,
    8,
    17,
    14,
    30,
    45,
    123456
)

print(dt.strftime("%f"))
```

Output:

```text
123456
```

---

# 1️⃣8️⃣ Combine Date + Time ⭐⭐⭐

```python
formatted = dt.strftime(
    "%Y-%m-%d %H:%M:%S"
)

print(formatted)
```

Output:

```text
2026-08-17 14:30:45
```

এটা খুব common format।

---

# 1️⃣9️⃣ Human-Friendly Format

```python
formatted = dt.strftime(
    "%A, %d %B %Y at %I:%M %p"
)

print(formatted)
```

Output:

```text
Monday, 17 August 2026 at 02:30 PM
```

এটি UI/report-এর জন্য useful।

---

# 2️⃣0️⃣ `strftime()` with `date`

`strftime()` শুধু `datetime`-এর জন্য নয়।

```python
from datetime import date

d = date(2026, 8, 17)

print(d.strftime("%d %B %Y"))
```

Output:

```text
17 August 2026
```

---

# 2️⃣1️⃣ `strftime()` with `time`

```python
from datetime import time

t = time(14, 30, 45)

print(t.strftime("%H:%M:%S"))
```

Output:

```text
14:30:45
```

---

# 2️⃣2️⃣ Literal Text ব্যবহার

Format-এর মধ্যে নিজের text লিখতে পারো।

```python
dt.strftime(
    "Date: %Y-%m-%d"
)
```

Output:

```text
Date: 2026-08-17
```

আরও:

```python
dt.strftime(
    "Today is %A, %d %B %Y"
)
```

Output:

```text
Today is Monday, 17 August 2026
```

---

# 2️⃣3️⃣ `strftime()` vs `str()`

### `str()`

Python-এর default representation:

```python
print(str(dt))
```

Output:

```text
2026-08-17 14:30:45
```

### `strftime()`

নিজের format:

```python
print(
    dt.strftime("%d/%m/%Y")
)
```

Output:

```text
17/08/2026
```

তাই:

```text
str()
   ↓
Default representation

strftime()
   ↓
Custom representation
```

---

# 2️⃣4️⃣ `strftime()` vs `isoformat()`

এগুলোও আলাদা।

### `isoformat()`

```python
dt.isoformat()
```

Output:

```text
2026-08-17T14:30:45
```

### `strftime()`

```python
dt.strftime(
    "%d/%m/%Y %I:%M %p"
)
```

Output:

```text
17/08/2026 02:30 PM
```

### কখন কোনটা?

|Method|Best use|
|---|---|
|`isoformat()`|API/data interchange|
|`strftime()`|Human-readable/custom format|

---

# 2️⃣5️⃣ Real-world Example — Blog

```python
from datetime import datetime

published_at = datetime(
    2026,
    8,
    17,
    14,
    30
)

display_date = published_at.strftime(
    "%d %B %Y"
)

print(display_date)
```

Output:

```text
17 August 2026
```

UI-তে:

```text
Published: 17 August 2026
```

---

# 2️⃣6️⃣ Real-world Example — Log

```python
from datetime import datetime

now = datetime.now()

log_time = now.strftime(
    "%Y-%m-%d %H:%M:%S"
)

print(
    f"[{log_time}] Application started"
)
```

Output:

```text
[2026-08-17 18:30:10] Application started
```

---

# 2️⃣7️⃣ Real-world Example — File Name ⭐⭐⭐

Date দিয়ে unique-ish filename তৈরি করা যায়:

```python
from datetime import datetime

now = datetime.now()

filename = now.strftime(
    "report_%Y%m%d_%H%M%S.txt"
)

print(filename)
```

Output-এর মতো:

```text
report_20260817_183010.txt
```

এটি file/report generation-এ useful।

---

# 2️⃣8️⃣ Real-world Example — Backup

```python
from datetime import datetime

now = datetime.now()

backup_name = now.strftime(
    "backup_%Y-%m-%d_%H-%M-%S.zip"
)

print(backup_name)
```

Output:

```text
backup_2026-08-17_18-30-10.zip
```

---

# 2️⃣9️⃣ Real-world Example — Birthday

```python
from datetime import datetime

birthday = datetime(
    2005,
    5,
    20
)

print(
    birthday.strftime(
        "%d %B, %Y"
    )
)
```

Output:

```text
20 May, 2005
```

---

# 3️⃣0️⃣ `strftime()` with UTC

Day 5-এ আমরা UTC শিখেছি।

```python
from datetime import datetime, timezone

utc_now = datetime.now(timezone.utc)

print(
    utc_now.strftime(
        "%Y-%m-%d %H:%M:%S %Z"
    )
)
```

এখানে `%Z` timezone name দেখাতে পারে।

---

# 3️⃣1️⃣ গুরুত্বপূর্ণ আরও কিছু Codes

|Code|Meaning|
|---|---|
|`%j`|Day of year|
|`%U`|Week number, Sunday first|
|`%W`|Week number, Monday first|
|`%z`|UTC offset|
|`%Z`|Timezone name|
|`%%`|Literal `%`|

সবগুলো এখন মুখস্থ করার প্রয়োজন নেই।

---

# 3️⃣2️⃣ `%z` — UTC Offset

```python
from datetime import datetime, timezone

dt = datetime.now(timezone.utc)

print(
    dt.strftime("%Y-%m-%d %H:%M:%S %z")
)
```

UTC হলে output-এর মতো:

```text
2026-08-17 12:30:00 +0000
```

---

# 3️⃣3️⃣ `%Z` — Timezone Name

```python
print(
    dt.strftime("%Z")
)
```

UTC-aware datetime-এর ক্ষেত্রে সাধারণত:

```text
UTC
```

---

# 3️⃣4️⃣ `%j` — Day of Year

```python
dt.strftime("%j")
```

এটি বছরের কততম দিন তা দেখায়।

যেমন:

```text
229
```

---

# 3️⃣5️⃣ `%` কীভাবে Print করবে?

যদি literal `%` দরকার হয়:

```python
dt.strftime(
    "Progress: 80%%"
)
```

Output:

```text
Progress: 80%
```

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Pattern

এটা ভালোভাবে বুঝে রাখো:

```text
              FORMAT
                 ↓
datetime ──→ strftime() ──→ string
```

Example:

```python
dt.strftime(
    "%Y-%m-%d %H:%M:%S"
)
```

---

# 🧪 Day 6 Practice

## Exercise 1

এই datetime:

```python
dt = datetime(
    2026,
    8,
    17,
    14,
    35,
    50
)
```

Output করো:

```text
2026
08
17
14
35
50
```

শুধু `strftime()` ব্যবহার করে।

---

## Exercise 2

Output:

```text
17 August 2026
```

---

## Exercise 3

Output:

```text
Monday, 17 August 2026
```

---

## Exercise 4

Output:

```text
02:35 PM
```

---

## Exercise 5 ⭐

Output:

```text
2026-08-17 14:35:50
```

---

## Exercise 6 ⭐⭐

একটি filename বানাও:

```text
report_20260817_143550.pdf
```

---

## Exercise 7 🔥

একটি log system বানাও:

```text
[2026-08-17 14:35:50] User logged in
```

---

# 🏆 Day 6 Mini Project

## 📄 Report Generator

একটি program বানাও যেটা current datetime নিয়ে এই ধরনের output দেবে:

```text
================================
        DAILY REPORT
================================

Generated On:
Monday, 17 August 2026

Generated Time:
02:35 PM

File Name:
report_20260817_143550.pdf

================================
```

তোমাকে ব্যবহার করতে হবে:

```python
datetime.now()
strftime()
```

---

# 📌 Day 6 Cheat Sheet

```python
from datetime import datetime

dt = datetime.now()
```

### Year

```python
dt.strftime("%Y")
```

### Month

```python
dt.strftime("%m")
```

### Month name

```python
dt.strftime("%B")
```

### Day

```python
dt.strftime("%d")
```

### Weekday

```python
dt.strftime("%A")
```

### 24-hour

```python
dt.strftime("%H")
```

### 12-hour

```python
dt.strftime("%I")
```

### Minute

```python
dt.strftime("%M")
```

### Second

```python
dt.strftime("%S")
```

### AM/PM

```python
dt.strftime("%p")
```

### Common format

```python
dt.strftime(
    "%Y-%m-%d %H:%M:%S"
)
```

### Human format

```python
dt.strftime(
    "%A, %d %B %Y"
)
```

### Time format

```python
dt.strftime(
    "%I:%M %p"
)
```

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅ ← YOU ARE HERE
Day 7  → strptime()                  ⏭️
Day 8  → timedelta
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 7-এ আমরা এর উল্টোটা শিখব: `strptime()` — অর্থাৎ `"17 August 2026"` বা `"2026-08-17 14:30:00"`-এর মতো string কীভাবে Python `datetime` object-এ convert করতে হয়।**

# 🐍 Python `datetime` — Day 7

## `strptime()` — String → Date/Time Object

আজ আমরা `strftime()`-এর **উল্টো operation** শিখব।

Official documentation: [Python `datetime.strptime()` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#datetime.datetime.strptime)

মনে রাখবে:

```text
strftime()
datetime → String

strptime()
String → datetime
```

---

# 1️⃣ `strptime()` কী?

ধরো তোমার কাছে string আছে:

```python
"2026-08-17 14:30:00"
```

এটা এখনো Python `datetime` object নয়।

```python
from datetime import datetime

text = "2026-08-17 14:30:00"

dt = datetime.strptime(
    text,
    "%Y-%m-%d %H:%M:%S"
)

print(dt)
print(type(dt))
```

Output:

```text
2026-08-17 14:30:00
<class 'datetime.datetime'>
```

---

# 2️⃣ Basic Syntax

```python
datetime.strptime(
    string,
    format
)
```

দুটি জিনিস দিতে হয়:

```text
1. Input string
2. String-এর format
```

---

# 3️⃣ কেন Format দিতে হয়? ⭐⭐⭐

Python-কে বলতে হবে string-এর কোন অংশ কী।

এই string:

```text
2026-08-17
```

এর format:

```text
%Y-%m-%d
```

অর্থাৎ:

```text
2026 → %Y
08   → %m
17   → %d
```

তাই:

```python
dt = datetime.strptime(
    "2026-08-17",
    "%Y-%m-%d"
)
```

---

# 4️⃣ Simple Date Conversion

```python
from datetime import datetime

text = "2026-08-17"

dt = datetime.strptime(
    text,
    "%Y-%m-%d"
)

print(dt)
```

Output:

```text
2026-08-17 00:00:00
```

কারণ আমরা time দিইনি।

---

# 5️⃣ Date + Time ⭐⭐⭐

Input:

```text
2026-08-17 14:30:45
```

Format:

```text
%Y-%m-%d %H:%M:%S
```

Code:

```python
from datetime import datetime

text = "2026-08-17 14:30:45"

dt = datetime.strptime(
    text,
    "%Y-%m-%d %H:%M:%S"
)

print(dt)
```

---

# 6️⃣ `strftime()` vs `strptime()` ⭐⭐⭐

এটা অবশ্যই পরিষ্কার হতে হবে।

### `strftime()`

```python
dt.strftime("%Y-%m-%d")
```

```text
datetime
    ↓
  string
```

### `strptime()`

```python
datetime.strptime(
    "2026-08-17",
    "%Y-%m-%d"
)
```

```text
string
   ↓
datetime
```

সহজে মনে রাখো:

> **f = formatting → object থেকে format করা**

> **p = parsing → string parse করা**

---

# 7️⃣ Common Formats

## Format 1

```python
text = "17-08-2026"

dt = datetime.strptime(
    text,
    "%d-%m-%Y"
)
```

---

## Format 2

```python
text = "17/08/2026"

dt = datetime.strptime(
    text,
    "%d/%m/%Y"
)
```

---

## Format 3

```python
text = "17 August 2026"

dt = datetime.strptime(
    text,
    "%d %B %Y"
)
```

---

## Format 4

```python
text = "17 Aug 2026"

dt = datetime.strptime(
    text,
    "%d %b %Y"
)
```

---

# 8️⃣ Time String → Datetime

```python
text = "14:30:45"

dt = datetime.strptime(
    text,
    "%H:%M:%S"
)

print(dt)
```

Output:

```text
1900-01-01 14:30:45
```

কারণ `strptime()` একটি `datetime` তৈরি করছে এবং date দেওয়া হয়নি।

---

# 9️⃣ 12-Hour Time

String:

```text
02:30 PM
```

Format:

```text
%I:%M %p
```

Code:

```python
text = "02:30 PM"

dt = datetime.strptime(
    text,
    "%I:%M %p"
)

print(dt)
```

Output-এর মতো:

```text
1900-01-01 14:30:00
```

---

# 🔟 AM / PM ⭐⭐⭐

```python
from datetime import datetime

text = "08:45 PM"

dt = datetime.strptime(
    text,
    "%I:%M %p"
)

print(dt.hour)
```

Output:

```text
20
```

অর্থাৎ:

```text
08:45 PM
     ↓
20:45
```

---

# 1️⃣1️⃣ Full Date + 12-Hour Time

Input:

```text
17 August 2026 02:30 PM
```

Code:

```python
text = "17 August 2026 02:30 PM"

dt = datetime.strptime(
    text,
    "%d %B %Y %I:%M %p"
)

print(dt)
```

Output:

```text
2026-08-17 14:30:00
```

---

# 1️⃣2️⃣ Extract Components After Parsing

```python
text = "17 August 2026 02:30 PM"

dt = datetime.strptime(
    text,
    "%d %B %Y %I:%M %p"
)

print(dt.year)
print(dt.month)
print(dt.day)
print(dt.hour)
print(dt.minute)
```

Output:

```text
2026
8
17
14
30
```

---

# 1️⃣3️⃣ Parsing API Data ⭐⭐⭐

ধরো API থেকে:

```json
{
    "created_at": "2026-08-17T14:30:00"
}
```

Python:

```python
text = "2026-08-17T14:30:00"

dt = datetime.strptime(
    text,
    "%Y-%m-%dT%H:%M:%S"
)

print(dt)
```

এখানে `T`-টাও format-এর অংশ:

```text
%Y-%m-%dT%H:%M:%S
          ↑
        literal T
```

তবে ISO-format string হলে:

```python
datetime.fromisoformat(text)
```

আরও convenient হতে পারে।

---

# 1️⃣4️⃣ `strptime()` vs `fromisoformat()`

### ISO format

```python
text = "2026-08-17T14:30:00"

dt = datetime.fromisoformat(text)
```

### Custom format

```python
text = "17/08/2026 02:30 PM"

dt = datetime.strptime(
    text,
    "%d/%m/%Y %I:%M %p"
)
```

তাই:

|Situation|Use|
|---|---|
|Standard ISO string|`fromisoformat()`|
|Custom date format|`strptime()`|

---

# 1️⃣5️⃣ Invalid Input ⚠️

ধরো:

```python
text = "2026-08-17"

dt = datetime.strptime(
    text,
    "%d-%m-%Y"
)
```

Format match করবে না।

তখন `ValueError` হতে পারে।

---

# 1️⃣6️⃣ User Input Handle করা ⭐⭐⭐

এখানে `try-except` ব্যবহার করো।

```python
from datetime import datetime

text = input(
    "Enter date (DD-MM-YYYY): "
)

try:
    dt = datetime.strptime(
        text,
        "%d-%m-%Y"
    )

    print("Valid date:", dt)

except ValueError:
    print("Invalid date format!")
```

User যদি দেয়:

```text
17-08-2026
```

তাহলে:

```text
Valid date: 2026-08-17 00:00:00
```

---

# 1️⃣7️⃣ User Input + Time

```python
text = input(
    "Enter datetime (YYYY-MM-DD HH:MM): "
)

try:
    dt = datetime.strptime(
        text,
        "%Y-%m-%d %H:%M"
    )

    print("Valid:", dt)

except ValueError:
    print("Invalid datetime!")
```

Input:

```text
2026-09-10 14:30
```

---

# 1️⃣8️⃣ Convert String → Datetime → Different String

এটা খুব important real-world pattern।

Input:

```text
17-08-2026
```

Convert:

```python
text = "17-08-2026"

dt = datetime.strptime(
    text,
    "%d-%m-%Y"
)
```

তারপর অন্য format:

```python
result = dt.strftime(
    "%Y/%m/%d"
)

print(result)
```

Output:

```text
2026/08/17
```

Flow:

```text
"17-08-2026"
      ↓
  strptime()
      ↓
datetime object
      ↓
  strftime()
      ↓
"2026/08/17"
```

🔥 এই pattern খুব গুরুত্বপূর্ণ।

---

# 1️⃣9️⃣ Database Data Formatting

ধরো database থেকে:

```text
2026-08-17 14:30:00
```

তুমি user-এর UI-তে দেখাতে চাও:

```text
17 August 2026, 02:30 PM
```

Code:

```python
from datetime import datetime

db_value = "2026-08-17 14:30:00"

dt = datetime.strptime(
    db_value,
    "%Y-%m-%d %H:%M:%S"
)

display = dt.strftime(
    "%d %B %Y, %I:%M %p"
)

print(display)
```

Output:

```text
17 August 2026, 02:30 PM
```

---

# 2️⃣0️⃣ Django/API Context ⭐⭐⭐

Backend থেকে অনেক সময়:

```text
2026-08-17T14:30:00
```

এরকম datetime আসে।

তুমি যদি শুধু display করতে চাও:

```python
dt = datetime.fromisoformat(
    "2026-08-17T14:30:00"
)

display = dt.strftime(
    "%d %B %Y"
)
```

Output:

```text
17 August 2026
```

---

# 2️⃣1️⃣ Parsing Different Separators

Input:

```text
2026/08/17
```

Format:

```python
"%Y/%m/%d"
```

Code:

```python
dt = datetime.strptime(
    "2026/08/17",
    "%Y/%m/%d"
)
```

---

# 2️⃣2️⃣ Parsing Month Names

Full month:

```python
dt = datetime.strptime(
    "17 August 2026",
    "%d %B %Y"
)
```

Short month:

```python
dt = datetime.strptime(
    "17 Aug 2026",
    "%d %b %Y"
)
```

---

# 2️⃣3️⃣ Parsing Weekday

```python
text = "Monday, 17 August 2026"

dt = datetime.strptime(
    text,
    "%A, %d %B %Y"
)

print(dt)
```

Output:

```text
2026-08-17 00:00:00
```

---

# 2️⃣4️⃣ Microseconds

Input:

```text
2026-08-17 14:30:45.123456
```

Format:

```python
"%Y-%m-%d %H:%M:%S.%f"
```

Code:

```python
text = "2026-08-17 14:30:45.123456"

dt = datetime.strptime(
    text,
    "%Y-%m-%d %H:%M:%S.%f"
)

print(dt.microsecond)
```

Output:

```text
123456
```

---

# 2️⃣5️⃣ Timezone Offset Parsing

String:

```text
2026-08-17T14:30:00+00:00
```

এখানে timezone offset আছে।

`%z` ব্যবহার করা যায়:

```python
text = "2026-08-17T14:30:00+0000"

dt = datetime.strptime(
    text,
    "%Y-%m-%dT%H:%M:%S%z"
)

print(dt)
print(dt.tzinfo)
```

Output-এর মতো:

```text
2026-08-17 14:30:00+00:00
UTC
```

ISO strings-এর জন্য `fromisoformat()` অনেক সময় সহজ।

---

# 2️⃣6️⃣ Important Format Codes Review

|Code|Meaning|
|---|---|
|`%Y`|4-digit year|
|`%y`|2-digit year|
|`%m`|Month|
|`%B`|Full month|
|`%b`|Short month|
|`%d`|Day|
|`%A`|Full weekday|
|`%a`|Short weekday|
|`%H`|24-hour|
|`%I`|12-hour|
|`%M`|Minute|
|`%S`|Second|
|`%f`|Microsecond|
|`%p`|AM/PM|
|`%z`|UTC offset|
|`%Z`|Timezone name|

---

# 🧠 2️⃣7️⃣ সবচেয়ে গুরুত্বপূর্ণ Difference

### Formatting

```python
dt.strftime(format)
```

মানে:

```text
Object → String
```

### Parsing

```python
datetime.strptime(
    string,
    format
)
```

মানে:

```text
String → Object
```

---

# 🔥 2️⃣8️⃣ Real-world Data Pipeline

একটি সাধারণ application flow:

```text
User Input
    ↓
"17/08/2026 02:30 PM"
    ↓
strptime()
    ↓
datetime object
    ↓
Application logic
    ↓
strftime()
    ↓
"17 August 2026, 02:30 PM"
    ↓
UI
```

---

# 🧪 Day 7 Practice

### Exercise 1

Convert:

```text
2026-08-17
```

to a `datetime`.

---

### Exercise 2

Convert:

```text
17/08/2026
```

to a `datetime`.

---

### Exercise 3

Convert:

```text
17 August 2026
```

to a `datetime`.

---

### Exercise 4

Convert:

```text
17 Aug 2026 02:30 PM
```

to a `datetime`.

---

### Exercise 5 ⭐

User input:

```text
Enter your birthday (DD-MM-YYYY):
```

তারপর valid হলে:

```text
Birthday: 2005-05-20
```

invalid হলে:

```text
Invalid date!
```

---

### Exercise 6 ⭐⭐

এই input:

```text
17-08-2026 14:30:45
```

convert করে output দাও:

```text
Monday, 17 August 2026 at 02:30 PM
```

---

### Exercise 7 🔥

একটি program বানাও:

```text
Enter date:
17/08/2026

Enter time:
02:30 PM
```

তারপর দুটোকে combine করে:

```text
2026-08-17 14:30:00
```

তৈরি করো।

---

# 🏆 Day 7 Mini Project

## 📅 Date Input Parser

Program:

```text
================================
       DATE TIME PARSER
================================

Enter date (DD/MM/YYYY):
17/08/2026

Enter time (HH:MM AM/PM):
02:30 PM

================================

Parsed Date:
2026-08-17

Parsed Time:
14:30:00

Formatted:
Monday, 17 August 2026 at 02:30 PM
================================
```

তোমার program-এ ব্যবহার করবে:

```python
datetime.strptime()
datetime.combine()
strftime()
try
except ValueError
```

---

# 📌 Day 7 Cheat Sheet

### String → datetime

```python
dt = datetime.strptime(
    text,
    "%Y-%m-%d"
)
```

### Date

```python
datetime.strptime(
    "17/08/2026",
    "%d/%m/%Y"
)
```

### Date + Time

```python
datetime.strptime(
    "17/08/2026 14:30",
    "%d/%m/%Y %H:%M"
)
```

### 12-hour

```python
datetime.strptime(
    "02:30 PM",
    "%I:%M %p"
)
```

### Custom month

```python
datetime.strptime(
    "17 August 2026",
    "%d %B %Y"
)
```

### Error handling

```python
try:
    dt = datetime.strptime(
        text,
        format
    )
except ValueError:
    print("Invalid!")
```

### Reverse operation

```python
dt.strftime(
    "%d %B %Y"
)
```

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅ ← YOU ARE HERE
Day 8  → timedelta                   ⏭️
Day 9  → Date Calculations
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 8-এ `timedelta` শিখব—যেমন “আজ থেকে 7 দিন পরে”, “2 ঘণ্টা আগে”, “দুইটি datetime-এর মধ্যে কত সময়” ইত্যাদি।**

# 🐍 Python `datetime` — Day 8

## `timedelta` — Date & Time Calculation

আজকের topic হলো **`timedelta`**। এটা `datetime` module-এর সবচেয়ে useful অংশগুলোর একটি।

Official documentation: [Python `timedelta` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#timedelta-objects)

আজ আমরা শিখব:

```text
আজ থেকে 7 দিন পরে
আজ থেকে 30 দিন আগে
2 ঘণ্টা পরে
90 মিনিট আগে
দুই datetime-এর মধ্যে কত সময়
```

---

# 1️⃣ `timedelta` কী?

`timedelta` হলো **দুইটি date/time-এর মধ্যকার duration বা সময়ের পরিমাণ** represent করার object।

```python
from datetime import timedelta
```

Concept:

```text
timedelta
   ↓
Duration
   ↓
days
hours
minutes
seconds
microseconds
```

---

# 2️⃣ Basic Example

```python
from datetime import timedelta

duration = timedelta(days=5)

print(duration)
```

Output:

```text
5 days, 0:00:00
```

---

# 3️⃣ `timedelta`-তে কী কী দেওয়া যায়?

```python
timedelta(
    days=0,
    seconds=0,
    microseconds=0,
    milliseconds=0,
    minutes=0,
    hours=0,
    weeks=0
)
```

সব একসাথে দেওয়া সম্ভব।

Example:

```python
from datetime import timedelta

duration = timedelta(
    days=2,
    hours=5,
    minutes=30
)

print(duration)
```

Output:

```text
2 days, 5:30:00
```

---

# 4️⃣ Days

```python
from datetime import timedelta

d = timedelta(days=7)

print(d)
```

```text
7 days, 0:00:00
```

---

# 5️⃣ Weeks

```python
d = timedelta(weeks=2)

print(d)
```

Output:

```text
14 days, 0:00:00
```

অর্থাৎ:

```text
2 weeks = 14 days
```

---

# 6️⃣ Hours

```python
d = timedelta(hours=5)

print(d)
```

Output:

```text
5:00:00
```

---

# 7️⃣ Minutes

```python
d = timedelta(minutes=30)

print(d)
```

Output:

```text
0:30:00
```

---

# 8️⃣ Seconds

```python
d = timedelta(seconds=45)

print(d)
```

Output:

```text
0:00:45
```

---

# 9️⃣ Combine Everything ⭐

```python
duration = timedelta(
    weeks=1,
    days=2,
    hours=3,
    minutes=20,
    seconds=15
)

print(duration)
```

Conceptually:

```text
1 week
+ 2 days
+ 3 hours
+ 20 minutes
+ 15 seconds
```

---

# 🔟 `datetime + timedelta` ⭐⭐⭐

এটাই সবচেয়ে গুরুত্বপূর্ণ।

```python
from datetime import datetime, timedelta

now = datetime.now()

future = now + timedelta(days=7)

print("Now:", now)
print("Future:", future)
```

মানে:

```text
Current datetime
      +
    7 days
      ↓
Future datetime
```

---

# 1️⃣1️⃣ আজ থেকে 7 দিন পরে

```python
from datetime import datetime, timedelta

today = datetime.now()

next_week = today + timedelta(days=7)

print(next_week)
```

---

# 1️⃣2️⃣ আজ থেকে 30 দিন পরে

```python
future = datetime.now() + timedelta(days=30)

print(future)
```

---

# 1️⃣3️⃣ আজ থেকে 1 বছর?

`timedelta`-তে `years` parameter নেই।

তাই:

```python
timedelta(years=1)
```

❌ কাজ করবে না।

কারণ এক বছর সবসময় একই সংখ্যক দিন নয়:

```text
365 days
366 days
```

Year/month calendar calculation-এর জন্য পরে `dateutil` বা অন্য approach দরকার হতে পারে।

Beginner হিসেবে এখন:

```python
timedelta(days=365)
```

ব্যবহার করতে পারো, কিন্তু এটি calendar year-এর exact equivalent নয়।

---

# 1️⃣4️⃣ Past Date — Minus

```python
from datetime import datetime, timedelta

today = datetime.now()

previous = today - timedelta(days=7)

print(previous)
```

মানে:

```text
Today
  -
7 days
  ↓
Previous date
```

---

# 1️⃣5️⃣ 2 Hours Later

```python
from datetime import datetime, timedelta

now = datetime.now()

future = now + timedelta(hours=2)

print(future)
```

---

# 1️⃣6️⃣ 30 Minutes Earlier

```python
past = datetime.now() - timedelta(minutes=30)

print(past)
```

---

# 1️⃣7️⃣ Multiple Units ⭐⭐⭐

```python
from datetime import datetime, timedelta

now = datetime.now()

future = now + timedelta(
    days=2,
    hours=5,
    minutes=30
)

print(future)
```

এখানে:

```text
Now
+
2 days
+
5 hours
+
30 minutes
```

---

# 1️⃣8️⃣ Two Datetimes Subtract করা ⭐⭐⭐

এটা খুব important।

```python
from datetime import datetime

start = datetime(2026, 8, 10)
end = datetime(2026, 8, 17)

difference = end - start

print(difference)
```

Output:

```text
7 days, 0:00:00
```

Flow:

```text
datetime
    -
datetime
    ↓
timedelta
```

---

# 1️⃣9️⃣ Difference-এর `.days`

```python
print(difference.days)
```

Output:

```text
7
```

---

# 2️⃣0️⃣ Difference-এর `.seconds`

```python
from datetime import datetime

start = datetime(2026, 8, 17, 10, 0)
end = datetime(2026, 8, 17, 15, 30)

difference = end - start

print(difference)
print(difference.days)
print(difference.seconds)
```

Output:

```text
5:30:00
0
19800
```

কারণ:

```text
5 hours 30 minutes
= 19,800 seconds
```

⚠️ `difference.seconds` পুরো duration-এর total seconds নয়; এটি days বাদ দেওয়ার পরের seconds অংশ। Total duration-এর জন্য `total_seconds()` শেখা আরও ভালো।

---

# 2️⃣1️⃣ `total_seconds()` ⭐⭐⭐

```python
from datetime import timedelta

duration = timedelta(
    days=1,
    hours=2,
    minutes=30
)

print(duration.total_seconds())
```

Output:

```text
95400.0
```

কারণ:

```text
1 day    = 86400 sec
2 hours  = 7200 sec
30 min   = 1800 sec

Total = 95400 sec
```

---

# 2️⃣2️⃣ Difference in Hours

```python
from datetime import datetime

start = datetime(2026, 8, 17, 10)
end = datetime(2026, 8, 17, 15, 30)

difference = end - start

hours = difference.total_seconds() / 3600

print(hours)
```

Output:

```text
5.5
```

---

# 2️⃣3️⃣ Difference in Minutes

```python
minutes = difference.total_seconds() / 60

print(minutes)
```

Output:

```text
330.0
```

---

# 2️⃣4️⃣ Difference in Days

```python
days = difference.total_seconds() / 86400

print(days)
```

---

# 2️⃣5️⃣ `date` + `timedelta`

শুধু `datetime` নয়, `date`-এর সাথেও ব্যবহার করা যায়।

```python
from datetime import date, timedelta

today = date.today()

future = today + timedelta(days=10)

print(today)
print(future)
```

---

# 2️⃣6️⃣ Date Subtraction

```python
from datetime import date, timedelta

today = date.today()

past = today - timedelta(days=30)

print(past)
```

---

# 2️⃣7️⃣ Deadline Calculator ⭐⭐⭐

ধরো assignment-এর deadline আজ থেকে 7 দিন পরে:

```python
from datetime import datetime, timedelta

created = datetime.now()

deadline = created + timedelta(days=7)

print("Created:", created)
print("Deadline:", deadline)
```

---

# 2️⃣8️⃣ Subscription Example

30 দিনের subscription:

```python
from datetime import datetime, timedelta

start = datetime.now()

expiry = start + timedelta(days=30)

print("Start:", start)
print("Expiry:", expiry)
```

---

# 2️⃣9️⃣ Trial Period

```python
from datetime import datetime, timedelta

trial_start = datetime.now()

trial_end = trial_start + timedelta(days=14)

print("Trial ends:", trial_end)
```

---

# 3️⃣0️⃣ Calculate Remaining Time

ধরো:

```python
from datetime import datetime, timedelta

now = datetime.now()

deadline = now + timedelta(days=3)

remaining = deadline - now

print(remaining)
```

Output-এর মতো:

```text
3 days, 0:00:00
```

---

# 3️⃣1️⃣ Check Deadline Passed কি না ⭐⭐⭐

```python
from datetime import datetime, timedelta

deadline = datetime.now() - timedelta(days=1)

now = datetime.now()

if now > deadline:
    print("Deadline passed")
else:
    print("Still remaining")
```

---

# 3️⃣2️⃣ Check Future Date

```python
from datetime import datetime, timedelta

future = datetime.now() + timedelta(days=5)

if future > datetime.now():
    print("Future date")
```

---

# 3️⃣3️⃣ Expired / Active System

```python
from datetime import datetime, timedelta

created_at = datetime.now()

expires_at = created_at + timedelta(days=7)

now = datetime.now()

if now >= expires_at:
    print("Expired")
else:
    print("Active")
```

এটা real application-এ খুব common concept।

---

# 3️⃣4️⃣ Negative `timedelta`

```python
from datetime import timedelta

d = timedelta(days=-5)

print(d)
```

Output:

```text
-5 days, 0:00:00
```

সাধারণত date calculation-এ subtraction ব্যবহার করলে code বেশি readable:

```python
today - timedelta(days=5)
```

---

# 3️⃣5️⃣ `timedelta` Comparison ⭐

দুই duration compare করা যায়:

```python
from datetime import timedelta

a = timedelta(days=5)
b = timedelta(days=10)

print(a < b)
print(a == b)
print(a > b)
```

Output:

```text
True
False
False
```

---

# 3️⃣6️⃣ Duration Multiplication

```python
from datetime import timedelta

one_day = timedelta(days=1)

five_days = one_day * 5

print(five_days)
```

Output:

```text
5 days, 0:00:00
```

---

# 3️⃣7️⃣ Duration Division

```python
from datetime import timedelta

duration = timedelta(days=10)

print(duration / 2)
```

Output:

```text
5 days, 0:00:00
```

---

# 3️⃣8️⃣ `timedelta` Attributes

```python
from datetime import timedelta

d = timedelta(
    days=2,
    seconds=3600
)

print(d.days)
print(d.seconds)
print(d.microseconds)
```

Important:

```text
days
seconds
microseconds
```

---

# 3️⃣9️⃣ Important: `.seconds` বনাম `.total_seconds()` ⚠️

ধরো:

```python
from datetime import timedelta

d = timedelta(
    days=2,
    hours=3
)

print(d.days)
print(d.seconds)
print(d.total_seconds())
```

Conceptually:

```text
days = 2

seconds = 10800
        ↓
3 hours

total_seconds()
        ↓
2 days + 3 hours
        ↓
183600 seconds
```

তাই পুরো duration seconds-এ চাইলে:

```python
d.total_seconds()
```

ব্যবহার করবে।

---

# 4️⃣0️⃣ Real-world Backend Example

ধরো user registration-এর পর 24 ঘণ্টার verification link valid:

```python
from datetime import datetime, timedelta, timezone

created_at = datetime.now(timezone.utc)

expires_at = created_at + timedelta(hours=24)

print("Created:", created_at)
print("Expires:", expires_at)
```

তারপর:

```python
now = datetime.now(timezone.utc)

if now >= expires_at:
    print("Link expired")
else:
    print("Link still valid")
```

🔥 এই concept Django/API/backend development-এ খুব useful।

---

# 🧪 Day 8 Practice

## Exercise 1

আজ থেকে:

```text
7 days পরে
```

date বের করো।

---

## Exercise 2

আজ থেকে:

```text
30 days আগে
```

date বের করো।

---

## Exercise 3

আজ থেকে:

```text
2 hours 30 minutes পরে
```

datetime বের করো।

---

## Exercise 4

এই দুই datetime-এর difference বের করো:

```python
start = datetime(2026, 8, 1)
end = datetime(2026, 8, 17)
```

---

## Exercise 5 ⭐

Difference বের করে total hours বের করো।

---

## Exercise 6 ⭐⭐

একটি subscription system বানাও:

```text
Start:
আজ

Duration:
30 days

Expiry:
আজ + 30 days
```

তারপর check করো subscription expired কিনা।

---

## Exercise 7 🔥

Verification link system:

```text
Created At:
Now

Expires:
24 hours later
```

তারপর:

```text
Active
```

অথবা:

```text
Expired
```

print করো।

---

# 🏆 Day 8 Mini Project

## ⏳ Deadline Tracker

Program-এর flow:

```text
=============================
       DEADLINE TRACKER
=============================

Created At:
2026-08-17 18:30:00

Deadline:
2026-08-24 18:30:00

Remaining:
7 days

Status:
ACTIVE
=============================
```

তোমাকে ব্যবহার করতে হবে:

```python
datetime.now()
timedelta()
datetime - datetime
total_seconds()
if/else
```

---

# 📌 Day 8 Cheat Sheet

### Import

```python
from datetime import datetime, timedelta
```

### Duration

```python
timedelta(days=7)
```

### Future

```python
datetime.now() + timedelta(days=7)
```

### Past

```python
datetime.now() - timedelta(days=7)
```

### Hours

```python
timedelta(hours=5)
```

### Minutes

```python
timedelta(minutes=30)
```

### Weeks

```python
timedelta(weeks=2)
```

### Multiple units

```python
timedelta(
    days=2,
    hours=5,
    minutes=30
)
```

### Difference

```python
end - start
```

### Total seconds

```python
difference.total_seconds()
```

### Expiry check

```python
if datetime.now() >= expires_at:
    print("Expired")
```

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ ৪টি Pattern

```python
# 1. Future
future = now + timedelta(days=7)

# 2. Past
past = now - timedelta(days=7)

# 3. Difference
difference = end - start

# 4. Total duration
seconds = difference.total_seconds()
```

এগুলো ভালোভাবে পারলে `timedelta`-এর মূল কাজগুলো তোমার হয়ে যাবে।

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅ ← YOU ARE HERE
Day 9  → Date Calculations           ⏭️
Day 10 → Timestamp
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 9-এ আমরা `date`/`datetime` নিয়ে practical date calculations, month-end, date ranges, এবং দুই date-এর মধ্যে calculation আরও ভালোভাবে করব।**


# 🐍 Python `datetime` — Day 9

## Date Calculation & Date Range

আজকের লক্ষ্য হলো `date`, `datetime`, `timedelta` ব্যবহার করে **real-world date calculation** করা।

Official documentation: [Python `datetime` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

আজ শিখবে:

```text
Date calculation
Date range
Week calculation
Month calculation
Last/next date
Working with calendar dates
Leap year concept
Date comparison
Practical examples
```

---

# 1️⃣ Date + `timedelta` Review

আগে আমরা দেখেছি:

```python
from datetime import date, timedelta

today = date.today()

future = today + timedelta(days=7)

print(today)
print(future)
```

Flow:

```text
today
  +
7 days
  ↓
future date
```

---

# 2️⃣ Date Difference

```python
from datetime import date

start = date(2026, 8, 1)
end = date(2026, 8, 17)

difference = end - start

print(difference)
print(difference.days)
```

Output:

```text
16 days, 0:00:00
16
```

⚠️ কারণ August 1 থেকে August 17 পর্যন্ত elapsed duration হলো **16 days**।

---

# 3️⃣ কোন Date আগে?

দুইটি date compare করা যায়:

```python
from datetime import date

a = date(2026, 8, 10)
b = date(2026, 8, 17)

print(a < b)
print(a > b)
print(a == b)
```

Output:

```text
True
False
False
```

---

# 4️⃣ Date Sorting ⭐⭐⭐

অনেকগুলো date থাকলে Python এগুলো sort করতে পারে।

```python
from datetime import date

dates = [
    date(2026, 8, 17),
    date(2026, 8, 5),
    date(2026, 8, 10),
    date(2026, 8, 1),
]

dates.sort()

for d in dates:
    print(d)
```

Output:

```text
2026-08-01
2026-08-05
2026-08-10
2026-08-17
```

এটা database records, events, deadlines ইত্যাদিতে খুব useful।

---

# 5️⃣ Latest Date বের করা

```python
latest = max(dates)

print(latest)
```

Output:

```text
2026-08-17
```

---

# 6️⃣ Earliest Date

```python
earliest = min(dates)

print(earliest)
```

Output:

```text
2026-08-01
```

---

# 7️⃣ আজকের Weekday

```python
from datetime import date

today = date.today()

print(today.weekday())
```

`weekday()`:

```text
Monday    → 0
Tuesday   → 1
Wednesday → 2
Thursday  → 3
Friday    → 4
Saturday  → 5
Sunday    → 6
```

---

# 8️⃣ `isoweekday()` ⭐

আরেকটি method:

```python
today.isoweekday()
```

এখানে:

```text
Monday    → 1
Tuesday   → 2
Wednesday → 3
Thursday  → 4
Friday    → 5
Saturday  → 6
Sunday    → 7
```

Difference:

|Method|Monday|Sunday|
|---|--:|--:|
|`weekday()`|0|6|
|`isoweekday()`|1|7|

---

# 9️⃣ Weekday Name

`datetime` object দিয়ে:

```python
from datetime import datetime

dt = datetime.now()

print(dt.strftime("%A"))
```

Output:

```text
Monday
```

---

# 🔟 আজ Weekend কিনা?

```python
from datetime import date

today = date.today()

if today.weekday() >= 5:
    print("Weekend")
else:
    print("Weekday")
```

কারণ:

```text
Saturday = 5
Sunday   = 6
```

---

# 1️⃣1️⃣ আগামী 7 দিনের Date Range ⭐⭐⭐

```python
from datetime import date, timedelta

today = date.today()

for i in range(7):
    d = today + timedelta(days=i)
    print(d)
```

Output-এর মতো:

```text
2026-08-17
2026-08-18
2026-08-19
2026-08-20
2026-08-21
2026-08-22
2026-08-23
```

---

# 1️⃣2️⃣ আগামী 30 দিনের Range

```python
from datetime import date, timedelta

today = date.today()

for i in range(30):
    d = today + timedelta(days=i)
    print(d)
```

---

# 1️⃣3️⃣ Past 7 Days

```python
from datetime import date, timedelta

today = date.today()

for i in range(7):
    d = today - timedelta(days=i)
    print(d)
```

---

# 1️⃣4️⃣ Date Range Function ⭐⭐⭐

Reusable function:

```python
from datetime import date, timedelta

def date_range(start, days):
    dates = []

    for i in range(days):
        dates.append(
            start + timedelta(days=i)
        )

    return dates
```

Use:

```python
start = date(2026, 8, 17)

result = date_range(start, 7)

for d in result:
    print(d)
```

---

# 1️⃣5️⃣ Start Date থেকে End Date পর্যন্ত

ধরো:

```python
start = date(2026, 8, 1)
end = date(2026, 8, 10)
```

সব date বের করতে:

```python
from datetime import date, timedelta

current = start

while current <= end:
    print(current)
    current += timedelta(days=1)
```

Output:

```text
2026-08-01
2026-08-02
2026-08-03
...
2026-08-10
```

---

# 1️⃣6️⃣ Inclusive vs Exclusive ⭐⭐⭐

এই code:

```python
range(7)
```

মানে 7টি value:

```text
0 1 2 3 4 5 6
```

তাই:

```python
today + timedelta(days=i)
```

দিলে আজসহ 7টি date পাওয়া যায়।

কিন্তু যদি **আজ থেকে 7 দিন পর পর্যন্ত** চাই:

```python
for i in range(8):
    print(today + timedelta(days=i))
```

তখন:

```text
Today
+1
+2
+3
+4
+5
+6
+7
```

---

# 1️⃣7️⃣ Month Calculation — Important ⚠️

`timedelta`-তে:

```python
timedelta(months=1)
```

❌ নেই।

কারণ:

```text
January   → 31 days
February  → 28/29 days
April     → 30 days
```

তাই "1 month পরে" এবং "30 days পরে" সবসময় একই নয়।

---

# 1️⃣8️⃣ Month-এর শেষ দিন বের করা

Standard library-এর `calendar` module ব্যবহার করতে পারো।

```python
import calendar

year = 2026
month = 8

last_day = calendar.monthrange(
    year,
    month
)[1]

print(last_day)
```

Output:

```text
31
```

`monthrange()` return করে:

```text
(first_weekday, number_of_days)
```

তাই:

```python
calendar.monthrange(2026, 8)
```

এর second value হলো month-এর total days।

---

# 1️⃣9️⃣ February-এর শেষ দিন

```python
import calendar

print(
    calendar.monthrange(2026, 2)[1]
)
```

Output:

```text
28
```

Leap year হলে:

```python
print(
    calendar.monthrange(2024, 2)[1]
)
```

Output:

```text
29
```

---

# 2️⃣0️⃣ Current Month-এর শেষ দিন

```python
from datetime import date
import calendar

today = date.today()

last_day = calendar.monthrange(
    today.year,
    today.month
)[1]

print(last_day)
```

---

# 2️⃣1️⃣ Current Month-এর শেষ Date

```python
from datetime import date
import calendar

today = date.today()

last_day = calendar.monthrange(
    today.year,
    today.month
)[1]

month_end = date(
    today.year,
    today.month,
    last_day
)

print(month_end)
```

---

# 2️⃣2️⃣ Current Month-এর প্রথম Date

খুব সহজ:

```python
from datetime import date

today = date.today()

month_start = date(
    today.year,
    today.month,
    1
)

print(month_start)
```

---

# 2️⃣3️⃣ Current Month Range ⭐⭐⭐

```python
from datetime import date, timedelta
import calendar

today = date.today()

start = date(
    today.year,
    today.month,
    1
)

last_day = calendar.monthrange(
    today.year,
    today.month
)[1]

end = date(
    today.year,
    today.month,
    last_day
)

current = start

while current <= end:
    print(current)
    current += timedelta(days=1)
```

এটা calendar/report generation-এ useful।

---

# 2️⃣4️⃣ Leap Year

Leap year হলো এমন year যেখানে February-তে 29 দিন থাকে।

Python-এর `calendar`:

```python
import calendar

print(calendar.isleap(2024))
```

Output:

```text
True
```

আর:

```python
print(calendar.isleap(2026))
```

Output:

```text
False
```

---

# 2️⃣5️⃣ Leap Year Check

```python
import calendar

year = 2028

if calendar.isleap(year):
    print("Leap year")
else:
    print("Not leap year")
```

---

# 2️⃣6️⃣ Days in a Month Function

```python
import calendar

def days_in_month(year, month):
    return calendar.monthrange(
        year,
        month
    )[1]

print(days_in_month(2026, 2))
print(days_in_month(2026, 8))
```

Output:

```text
28
31
```

---

# 2️⃣7️⃣ Next Day

```python
from datetime import date, timedelta

today = date.today()

next_day = today + timedelta(days=1)

print(next_day)
```

---

# 2️⃣8️⃣ Previous Day

```python
previous_day = today - timedelta(days=1)

print(previous_day)
```

---

# 2️⃣9️⃣ Next Week

```python
next_week = today + timedelta(weeks=1)

print(next_week)
```

---

# 3️⃣0️⃣ Previous Week

```python
previous_week = today - timedelta(weeks=1)

print(previous_week)
```

---

# 3️⃣1️⃣ Check Date Range ⭐⭐⭐

ধরো:

```python
start = date(2026, 8, 1)
end = date(2026, 8, 31)

target = date(2026, 8, 17)
```

Check:

```python
if start <= target <= end:
    print("Inside range")
else:
    print("Outside range")
```

এটা booking, events, deadlines ইত্যাদিতে useful।

---

# 3️⃣2️⃣ Event Date Checker

```python
from datetime import date

event_start = date(2026, 8, 20)
event_end = date(2026, 8, 25)

today = date.today()

if event_start <= today <= event_end:
    print("Event is running")
elif today < event_start:
    print("Event is upcoming")
else:
    print("Event has ended")
```

---

# 3️⃣3️⃣ Age Calculation — Basic Version

ধরো birthday:

```python
from datetime import date

birthday = date(2005, 5, 20)
today = date.today()

age = today.year - birthday.year

if (
    today.month,
    today.day
) < (
    birthday.month,
    birthday.day
):
    age -= 1

print(age)
```

এখানে শুধু:

```text
current year - birth year
```

করলেই সবসময় সঠিক age হয় না।

Birthday এখনও আসেনি কিনা সেটাও check করতে হয়।

---

# 3️⃣4️⃣ Days Until Birthday

ধরো birthday:

```python
from datetime import date

today = date.today()

birthday = date(
    today.year,
    12,
    25
)

days_left = birthday - today

print(days_left.days)
```

এখানে যদি birthday already passed হয়, তাহলে next year handle করতে হবে।

---

# 3️⃣5️⃣ Date Difference in Human Terms

```python
from datetime import date

start = date(2026, 1, 1)
today = date(2026, 8, 17)

days = (today - start).days

print(
    f"{days} days have passed."
)
```

---

# 3️⃣6️⃣ Business/Working Days — Basic Concept

শুধু weekdays count করতে চাইলে:

```python
from datetime import date, timedelta

start = date(2026, 8, 17)
end = date(2026, 8, 23)

current = start
working_days = 0

while current <= end:

    if current.weekday() < 5:
        working_days += 1

    current += timedelta(days=1)

print(working_days)
```

এখানে:

```text
Monday-Friday → Working day
Saturday-Sunday → Weekend
```

তবে Bangladesh-এর actual public holidays হিসাব করতে আলাদা holiday data দরকার হবে।

---

# 3️⃣7️⃣ Practical Project — Monthly Report

ধরো তুমি monthly report তৈরি করবে।

```python
from datetime import date, timedelta
import calendar

today = date.today()

start = date(
    today.year,
    today.month,
    1
)

last_day = calendar.monthrange(
    today.year,
    today.month
)[1]

end = date(
    today.year,
    today.month,
    last_day
)

print("Report period:")
print("Start:", start)
print("End:", end)
```

Output-এর মতো:

```text
Report period:
Start: 2026-08-01
End: 2026-08-31
```

---

# 3️⃣8️⃣ Practical Project — Event Scheduler

```python
from datetime import date, timedelta

event_start = date.today()

event_end = event_start + timedelta(days=7)

print("Event starts:", event_start)
print("Event ends:", event_end)

today = date.today()

if today < event_start:
    print("Upcoming")
elif today <= event_end:
    print("Running")
else:
    print("Finished")
```

---

# 🧪 Day 9 Practice

## Exercise 1

আজকের date বের করো এবং:

```text
Tomorrow
Yesterday
Next Week
Last Week
```

print করো।

---

## Exercise 2

এই dates sort করো:

```python
dates = [
    date(2026, 8, 20),
    date(2026, 8, 5),
    date(2026, 8, 15),
    date(2026, 8, 1),
]
```

---

## Exercise 3

এই list থেকে:

```python
dates = [
    date(2026, 8, 20),
    date(2026, 8, 5),
    date(2026, 8, 15),
    date(2026, 8, 1),
]
```

`earliest` এবং `latest` বের করো।

---

## Exercise 4 ⭐

`2026` সালের প্রতিটি month-এ কয়দিন আছে বের করো।

Expected concept:

```text
January   → 31
February  → 28
March     → 31
...
```

---

## Exercise 5 ⭐

একটি function বানাও:

```python
days_in_month(year, month)
```

যেমন:

```python
days_in_month(2024, 2)
```

Output:

```text
29
```

---

## Exercise 6 ⭐⭐

একটি function বানাও:

```python
get_month_range(year, month)
```

যেটা return করবে:

```text
start_date
end_date
```

যেমন:

```python
get_month_range(2026, 8)
```

ফল:

```text
2026-08-01
2026-08-31
```

---

## Exercise 7 🔥

একটি event system বানাও:

```text
Start Date: 2026-08-20
End Date:   2026-08-25
```

Current date অনুযায়ী print করবে:

```text
UPCOMING
RUNNING
FINISHED
```

---

# 🏆 Day 9 Mini Project

## 📅 Monthly Calendar Information

Program-এর output এমন হবে:

```text
================================
       MONTH INFORMATION
================================

Year  : 2026
Month : August

First Date:
2026-08-01

Last Date:
2026-08-31

Total Days:
31

Leap Year:
No

================================
```

তোমাকে ব্যবহার করতে হবে:

```python
date
timedelta
calendar.monthrange()
calendar.isleap()
strftime()
```

---

# 📌 Day 9 Cheat Sheet

### Today

```python
date.today()
```

### Tomorrow

```python
date.today() + timedelta(days=1)
```

### Yesterday

```python
date.today() - timedelta(days=1)
```

### Difference

```python
end - start
```

### Difference days

```python
(end - start).days
```

### Weekday

```python
d.weekday()
```

### ISO weekday

```python
d.isoweekday()
```

### Earliest

```python
min(dates)
```

### Latest

```python
max(dates)
```

### Month days

```python
calendar.monthrange(year, month)[1]
```

### Leap year

```python
calendar.isleap(year)
```

### Month start

```python
date(year, month, 1)
```

### Date range

```python
current = start

while current <= end:
    print(current)
    current += timedelta(days=1)
```

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ Concepts

```text
date + timedelta
        ↓
Future date

date - timedelta
        ↓
Past date

date - date
        ↓
timedelta

min(dates)
        ↓
Earliest

max(dates)
        ↓
Latest

calendar.monthrange()
        ↓
Days in month

calendar.isleap()
        ↓
Leap year
```

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations           ✅ ← YOU ARE HERE
Day 10 → Timestamp                   ⏭️
Day 11 → Timezone
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 10-এ `timestamp` এবং Unix time শিখব—API, database, logging এবং computer systems-এ timestamp কেন ব্যবহার হয় এবং datetime ↔ timestamp conversion কীভাবে করতে হয়।**



# 🐍 Python `datetime` — Day 10

## Unix Timestamp & Epoch Time

আজকের topic খুব important, বিশেষ করে **API, database, backend, logging এবং distributed systems**-এ।

Official documentation: [Python `datetime` documentation — timestamps](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#datetime.datetime.timestamp)

আজ শিখবে:

```text
Unix Timestamp
Epoch
datetime → timestamp
timestamp → datetime
UTC timestamp
Milliseconds
API timestamp
Database timestamp
Real-world practice
```

---

# 1️⃣ Unix Timestamp কী?

Unix timestamp হলো একটি নির্দিষ্ট starting point থেকে elapsed time-এর হিসাব।

Unix-এর starting point:

```text
1970-01-01 00:00:00 UTC
```

এটাকে বলা হয়:

> **Unix Epoch**

উদাহরণ:

```text
1970-01-01 00:00:00 UTC
        ↓
       0
```

আর বর্তমানে একটি date/time-এর timestamp হতে পারে:

```text
17 August 2026
        ↓
timestamp
        ↓
প্রায় 1787... seconds
```

অর্থাৎ timestamp সাধারণত **seconds since Unix Epoch** হিসেবে ব্যবহৃত হয়।

---

# 2️⃣ কেন Timestamp ব্যবহার করা হয়? ⭐⭐⭐

ধরো:

```text
17 August 2026, 14:30:00
```

এটা মানুষের জন্য readable।

কিন্তু computer system-এর জন্য একটি numeric value নিয়ে কাজ করা অনেক সহজ:

```text
1786977000
```

তাই API, database, logs ইত্যাদিতে timestamp খুব common।

---

# 3️⃣ Current Timestamp

Python:

```python
from datetime import datetime

now = datetime.now()

timestamp = now.timestamp()

print(timestamp)
```

Output-এর মতো:

```text
1787........
```

এটা `float` হবে।

```python
print(type(timestamp))
```

Output:

```text
<class 'float'>
```

কারণ seconds-এর সাথে fractional অংশও থাকতে পারে।

---

# 4️⃣ `time.time()` দিয়েও Timestamp

Python-এর `time` module-এ:

```python
import time

timestamp = time.time()

print(timestamp)
```

এটাও current Unix timestamp দেয়।

Difference:

```text
datetime.now().timestamp()
        ↓
datetime object থেকে timestamp

time.time()
        ↓
current timestamp directly
```

---

# 5️⃣ Timestamp → `datetime` ⭐⭐⭐

এবার উল্টোটা।

```python
from datetime import datetime

timestamp = 1786977000

dt = datetime.fromtimestamp(timestamp)

print(dt)
```

Flow:

```text
timestamp
    ↓
fromtimestamp()
    ↓
datetime
```

---

# 6️⃣ `datetime` → Timestamp

```python
from datetime import datetime

dt = datetime.now()

timestamp = dt.timestamp()

print(timestamp)
```

Flow:

```text
datetime
    ↓
timestamp()
    ↓
Unix timestamp
```

---

# 7️⃣ দুটো একসাথে মনে রাখো

### datetime → timestamp

```python
dt.timestamp()
```

### timestamp → datetime

```python
datetime.fromtimestamp(timestamp)
```

🔥 এই দুটো Day 10-এর সবচেয়ে important অংশ।

---

# 8️⃣ Epoch কী?

Unix Epoch:

```text
1970-01-01 00:00:00 UTC
```

Python:

```python
from datetime import datetime, timezone

epoch = datetime(
    1970,
    1,
    1,
    tzinfo=timezone.utc
)

print(epoch)
```

---

# 9️⃣ Epoch-এর Timestamp

```python
print(epoch.timestamp())
```

Output:

```text
0.0
```

কারণ:

```text
Epoch
 ↓
0 seconds
```

---

# 🔟 Epoch থেকে 1 Day পরে

```python
from datetime import datetime, timedelta, timezone

epoch = datetime(
    1970,
    1,
    1,
    tzinfo=timezone.utc
)

one_day_later = epoch + timedelta(days=1)

print(one_day_later)
print(one_day_later.timestamp())
```

Output:

```text
1970-01-02 00:00:00+00:00
86400.0
```

কারণ:

```text
1 day = 24 × 60 × 60
     = 86400 seconds
```

---

# 1️⃣1️⃣ Timestamp থেকে UTC Datetime ⭐⭐⭐

এখানে একটি গুরুত্বপূর্ণ distinction আছে।

```python
datetime.fromtimestamp(timestamp)
```

এটি সাধারণত **local timezone** অনুযায়ী datetime তৈরি করে।

UTC চাইলে:

```python
from datetime import datetime, timezone

dt = datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)

print(dt)
```

অর্থাৎ:

```text
fromtimestamp(timestamp)
        ↓
local time

fromtimestamp(timestamp, timezone.utc)
        ↓
UTC time
```

---

# 1️⃣2️⃣ `utcfromtimestamp()` সম্পর্কে

পুরনো code-এ তুমি দেখতে পারো:

```python
datetime.utcfromtimestamp(timestamp)
```

বর্তমান Python documentation অনুযায়ী timezone-aware UTC datetime-এর জন্য এই approach বেশি appropriate:

```python
datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)
```

তাই নতুন code-এ timezone-aware datetime ব্যবহার করার অভ্যাস করো।

---

# 1️⃣3️⃣ Timestamp থেকে Date

ধরো:

```python
from datetime import datetime

timestamp = 1786977000

dt = datetime.fromtimestamp(timestamp)

print(dt.date())
```

এতে শুধু:

```text
YYYY-MM-DD
```

এর মতো date পাওয়া যাবে।

---

# 1️⃣4️⃣ Timestamp থেকে Time

```python
print(dt.time())
```

এতে time অংশ পাওয়া যাবে।

---

# 1️⃣5️⃣ Timestamp Integer করা

Timestamp সাধারণত:

```text
1786977000.12345
```

এর মতো float হতে পারে।

যদি integer seconds দরকার হয়:

```python
timestamp = int(datetime.now().timestamp())

print(timestamp)
```

---

# 1️⃣6️⃣ Seconds বনাম Milliseconds ⭐⭐⭐

অনেক API timestamp **milliseconds**-এ দেয়।

Python:

```python
timestamp_seconds = datetime.now().timestamp()

timestamp_milliseconds = int(
    timestamp_seconds * 1000
)

print(timestamp_milliseconds)
```

Concept:

```text
Seconds:
1786977000

Milliseconds:
1786977000000
```

কারণ:

```text
1 second = 1000 milliseconds
```

---

# 1️⃣7️⃣ Milliseconds → Datetime

যদি API থেকে milliseconds আসে:

```python
timestamp_ms = 1786977000000

timestamp_seconds = timestamp_ms / 1000

dt = datetime.fromtimestamp(
    timestamp_seconds
)

print(dt)
```

🔥 এই conversion API development-এ খুব useful।

---

# 1️⃣8️⃣ API Example

ধরো API response:

```json
{
    "created_at": 1786977000000
}
```

Python:

```python
timestamp_ms = 1786977000000

timestamp_seconds = timestamp_ms / 1000

created_at = datetime.fromtimestamp(
    timestamp_seconds
)

print(created_at)
```

Flow:

```text
API
 ↓
milliseconds
 ↓
/ 1000
 ↓
seconds
 ↓
fromtimestamp()
 ↓
datetime
```

---

# 1️⃣9️⃣ Timestamp Compare করা ⭐⭐⭐

ধরো:

```python
from datetime import datetime

created = datetime.now().timestamp()

later = created + 3600

if later > created:
    print("Later")
```

Timestamp numeric হওয়ায় comparison সহজ।

---

# 2️⃣0️⃣ Timestamp Difference

```python
from datetime import datetime
import time

start = datetime.now().timestamp()

# কিছু operation...

end = datetime.now().timestamp()

difference = end - start

print(difference)
```

এখানে elapsed seconds পাওয়া যায়।

---

# 2️⃣1️⃣ Performance Measurement

Performance measurement-এর জন্য Python-এর `time.perf_counter()` আরও উপযুক্ত।

```python
import time

start = time.perf_counter()

# code
total = sum(range(1000000))

end = time.perf_counter()

print(
    "Time:",
    end - start,
    "seconds"
)
```

এখানে মনে রাখবে:

```text
Unix timestamp
    ↓
Real-world time representation

perf_counter()
    ↓
Elapsed/performance measurement
```

দুটো একই purpose-এর জন্য নয়।

---

# 2️⃣2️⃣ Database Example ⭐⭐⭐

ধরো database-এ stored value:

```text
1786977000
```

Python:

```python
from datetime import datetime

created_at = datetime.fromtimestamp(
    1786977000
)

print(
    created_at.strftime(
        "%d %B %Y, %I:%M %p"
    )
)
```

Output-এর মতো:

```text
17 August 2026, 02:30 PM
```

Flow:

```text
Database
   ↓
Timestamp
   ↓
datetime
   ↓
strftime()
   ↓
User-friendly text
```

---

# 2️⃣3️⃣ Log System Example

একটি application log:

```text
1786977000 User logged in
```

Python:

```python
timestamp = 1786977000

dt = datetime.fromtimestamp(timestamp)

print(
    dt,
    "User logged in"
)
```

এতে machine-friendly timestamp থেকে human-readable log তৈরি করা যায়।

---

# 2️⃣4️⃣ Expiry Timestamp ⭐⭐⭐

আগের Day 8-এর expiry concept-কে timestamp দিয়ে করা যায়।

```python
from datetime import datetime, timedelta

created = datetime.now()

expires = created + timedelta(hours=24)

expires_timestamp = expires.timestamp()

print(expires_timestamp)
```

তারপর check:

```python
now_timestamp = datetime.now().timestamp()

if now_timestamp >= expires_timestamp:
    print("Expired")
else:
    print("Active")
```

---

# 2️⃣5️⃣ Better Approach: Datetime Comparison

শুধু expiry check-এর জন্য timestamp দরকার না-ও হতে পারে:

```python
from datetime import datetime, timedelta

created = datetime.now()
expires = created + timedelta(hours=24)

if datetime.now() >= expires:
    print("Expired")
else:
    print("Active")
```

এটা অনেক সময় বেশি readable।

Timestamp ব্যবহার করবে যখন **external system/API/database format** timestamp-based।

---

# 2️⃣6️⃣ UTC Timestamp ⭐⭐⭐

Backend application-এ timezone খুব গুরুত্বপূর্ণ।

Modern Python:

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)

print(now)
```

তারপর:

```python
timestamp = now.timestamp()

print(timestamp)
```

UTC-based timestamp পাওয়া যাবে।

---

# 2️⃣7️⃣ UTC Timestamp → UTC Datetime

```python
from datetime import datetime, timezone

timestamp = 1786977000

dt = datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)

print(dt)
```

Output-এর মতো:

```text
2026-08-17 08:30:00+00:00
```

এখানে `+00:00` UTC offset বোঝাচ্ছে।

---

# 2️⃣8️⃣ Timestamp সবসময় UTC?

একটি Unix timestamp **একটি absolute point in time** represent করে।

একই timestamp:

```text
Bangladesh time
UTC
USA time
Japan time
```

এগুলোতে different clock time হিসেবে display হতে পারে, কিন্তু instant একই।

Example concept:

```text
Timestamp
   ↓
Same instant
   ↓
UTC       → 08:30
Bangladesh → 14:30
Japan      → 17:30
```

অর্থাৎ timestamp নিজে "Bangladesh time" বা "USA time" নয়।

---

# 2️⃣9️⃣ `datetime.timestamp()` এবং Naive Datetime ⚠️

এইটা advanced but important:

```python
dt = datetime.now()

dt.timestamp()
```

এখানে `dt` timezone-naive।

Python local timezone context ব্যবহার করতে পারে।

আর:

```python
dt = datetime.now(timezone.utc)

dt.timestamp()
```

এটা timezone-aware UTC datetime।

Backend applications-এ timezone-aware datetime ব্যবহার করা generally safer।

---

# 3️⃣0️⃣ ISO String বনাম Timestamp

API দুটি format দিতে পারে:

### ISO 8601

```text
2026-08-17T14:30:00+06:00
```

### Unix timestamp

```text
1786977000
```

Python-এ:

```python
datetime.fromisoformat(...)
```

অথবা:

```python
datetime.fromtimestamp(...)
```

ব্যবহার করে convert করা যায়।

---

# 3️⃣1️⃣ Timestamp → ISO String

```python
from datetime import datetime, timezone

timestamp = 1786977000

dt = datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)

iso = dt.isoformat()

print(iso)
```

Output-এর মতো:

```text
2026-08-17T08:30:00+00:00
```

---

# 3️⃣2️⃣ ISO String → Timestamp

```python
from datetime import datetime

text = "2026-08-17T14:30:00+06:00"

dt = datetime.fromisoformat(text)

timestamp = dt.timestamp()

print(timestamp)
```

Flow:

```text
ISO String
   ↓
fromisoformat()
   ↓
datetime
   ↓
timestamp()
   ↓
Unix Timestamp
```

---

# 3️⃣3️⃣ Timestamp Round Trip ⭐⭐⭐

একটি datetime:

```python
from datetime import datetime, timezone

original = datetime.now(timezone.utc)

timestamp = original.timestamp()

converted = datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)

print(original)
print(converted)
```

Concept:

```text
datetime
   ↓
timestamp
   ↓
datetime
```

এটাকে round-trip conversion হিসেবে ভাবতে পারো।

---

# 🧪 Day 10 Practice

## Exercise 1

Current Unix timestamp বের করো।

---

## Exercise 2

একটি fixed timestamp:

```python
timestamp = 0
```

এটা datetime-এ convert করো।

Expected concept:

```text
1970-01-01
```

---

## Exercise 3

Current datetime → timestamp → datetime conversion করো।

---

## Exercise 4 ⭐

Milliseconds timestamp তৈরি করো:

```text
datetime → milliseconds
```

---

## Exercise 5 ⭐

এই milliseconds:

```python
timestamp_ms = 1786977000000
```

datetime-এ convert করো।

---

## Exercise 6 ⭐⭐

একটি expiry system বানাও:

```text
Created At = Now
Expiry = 24 hours
```

তারপর expiry timestamp print করো।

---

## Exercise 7 🔥

API-style data:

```python
data = {
    "created_at": 1786977000000
}
```

`created_at` milliseconds থেকে সুন্দর format-এ convert করো:

```text
17 August 2026, 02:30 PM
```

---

# 🏆 Day 10 Mini Project

## 🕐 Timestamp Converter

Program:

```text
====================================
       TIMESTAMP CONVERTER
====================================

1. Current Timestamp
2. Timestamp → Date
3. Date → Timestamp
4. Milliseconds → Date

Choose:
```

Example:

```text
Choose: 2

Enter timestamp:
1786977000

Date:
2026-08-17

Time:
14:30:00

UTC:
2026-08-17 08:30:00+00:00
====================================
```

এই project-এ ব্যবহার করবে:

```python
datetime.timestamp()
datetime.fromtimestamp()
datetime.now()
timezone.utc
isoformat()
strftime()
```

---

# 📌 Day 10 Cheat Sheet

### Current timestamp

```python
datetime.now().timestamp()
```

### UTC current datetime

```python
datetime.now(timezone.utc)
```

### Datetime → timestamp

```python
dt.timestamp()
```

### Timestamp → local datetime

```python
datetime.fromtimestamp(timestamp)
```

### Timestamp → UTC datetime

```python
datetime.fromtimestamp(
    timestamp,
    tz=timezone.utc
)
```

### Seconds → milliseconds

```python
int(timestamp * 1000)
```

### Milliseconds → seconds

```python
timestamp_ms / 1000
```

### Timestamp → ISO

```python
dt.isoformat()
```

### ISO → datetime

```python
datetime.fromisoformat(text)
```

---

# 🧠 Day 10-এর Core Concept

```text
                    Unix Epoch
                        │
                        ▼
               1970-01-01 00:00 UTC
                        │
                        │ elapsed seconds
                        ▼
                  TIMESTAMP
                        │
            ┌───────────┴───────────┐
            ▼                       ▼
   fromtimestamp()             timestamp()
            │                       ▲
            ▼                       │
       datetime  ──────────────────┘
```

সবচেয়ে গুরুত্বপূর্ণ:

```python
# datetime → timestamp
dt.timestamp()

# timestamp → datetime
datetime.fromtimestamp(timestamp)
```

আর backend/API-এর ক্ষেত্রে এই distinction মনে রাখবে:

```text
Seconds       → সাধারণ Unix timestamp
Milliseconds  → API-তে প্রায়ই দেখা যায়
UTC           → server/backend-এর জন্য গুরুত্বপূর্ণ
```

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations           ✅
Day 10 → Timestamp                   ✅ ← YOU ARE HERE
Day 11 → Timezone                    ⏭️
Day 12 → UTC + zoneinfo
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 11-এ আমরা `timezone`, timezone-aware বনাম naive datetime, UTC, এবং Bangladesh-এর `Asia/Dhaka` timezone নিয়ে কাজ করব।**

# 🐍 Python `datetime` — Day 11

## Timezone, UTC & Naive vs Aware Datetime

আজকের topic খুব important—বিশেষ করে **Django, REST API, database, authentication, logging এবং production backend**-এর জন্য।

Official documentation: [Python `datetime` timezone documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com#aware-and-naive-objects)

আজ আমরা শিখব:

```text
1. Timezone কী
2. UTC কী
3. Naive datetime
4. Aware datetime
5. timezone.utc
6. Asia/Dhaka
7. zoneinfo
8. UTC ↔ Bangladesh time
9. API/backend best practices
```

---

# 1️⃣ Timezone কী?

Timezone হলো পৃথিবীর কোনো নির্দিষ্ট অঞ্চলের **local time rule**।

উদাহরণ:

```text
UTC
Asia/Dhaka
Asia/Tokyo
Europe/London
America/New_York
```

একই মুহূর্তে বিভিন্ন timezone-এ clock time আলাদা হতে পারে।

উদাহরণ:

```text
UTC          → 08:00
Bangladesh   → 14:00
Japan        → 17:00
```

কিন্তু এগুলো **একই মুহূর্ত**।

---

# 2️⃣ UTC কী? ⭐⭐⭐

UTC = **Coordinated Universal Time**

এটা একটি global reference time।

Python:

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)

print(now)
```

Output-এর মতো:

```text
2026-08-17 08:00:00+00:00
```

এখানে:

```text
+00:00
```

মানে UTC offset হলো 0।

---

# 3️⃣ Naive Datetime কী?

যে `datetime` object-এর timezone information নেই তাকে **naive datetime** বলা হয়।

```python
from datetime import datetime

dt = datetime.now()

print(dt)
print(dt.tzinfo)
```

Output:

```text
2026-08-17 14:00:00
None
```

অর্থাৎ:

```text
dt.tzinfo
    ↓
None
```

এটা naive datetime।

---

# 4️⃣ Aware Datetime কী? ⭐⭐⭐

যে datetime object-এর timezone information আছে তাকে **aware datetime** বলা হয়।

```python
from datetime import datetime, timezone

dt = datetime.now(timezone.utc)

print(dt)
print(dt.tzinfo)
```

Output-এর মতো:

```text
2026-08-17 08:00:00+00:00
UTC
```

এটা timezone-aware datetime।

---

# 5️⃣ Naive vs Aware

|Type|Timezone information|
|---|---|
|Naive|নেই|
|Aware|আছে|

Example:

```python
# Naive
datetime.now()
```

```python
# Aware
datetime.now(timezone.utc)
```

সহজে মনে রাখো:

```text
Naive
↓
"I know the clock time,
but not the timezone."

Aware
↓
"I know the clock time
and the timezone."
```

---

# 6️⃣ `timezone.utc`

Python-এর standard library-তেই UTC timezone আছে।

```python
from datetime import timezone

print(timezone.utc)
```

তারপর:

```python
from datetime import datetime, timezone

dt = datetime.now(timezone.utc)

print(dt)
```

---

# 7️⃣ Bangladesh Time — `Asia/Dhaka` ⭐⭐⭐

Bangladesh-এর timezone হলো:

```text
Asia/Dhaka
```

Modern Python-এ `zoneinfo` ব্যবহার করা যায়।

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dhaka_time = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka_time)
```

Output-এর মতো:

```text
2026-08-17 14:00:00+06:00
```

এখানে:

```text
+06:00
```

মানে UTC থেকে 6 ঘণ্টা এগিয়ে।

---

# 8️⃣ `zoneinfo` কী?

`zoneinfo` Python-এর standard library module।

Import:

```python
from zoneinfo import ZoneInfo
```

তারপর:

```python
ZoneInfo("Asia/Dhaka")
```

Timezone object তৈরি করে।

---

# 9️⃣ Current Dhaka Time

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dhaka = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka)
```

এটা Bangladesh-এর current local time দেয়।

---

# 🔟 UTC Time

```python
from datetime import datetime, timezone

utc = datetime.now(timezone.utc)

print(utc)
```

---

# 1️⃣1️⃣ UTC → Dhaka ⭐⭐⭐

ধরো UTC datetime:

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc_time = datetime.now(timezone.utc)

dhaka_time = utc_time.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print("UTC:", utc_time)
print("Dhaka:", dhaka_time)
```

Flow:

```text
UTC datetime
     ↓
astimezone()
     ↓
Asia/Dhaka
```

---

# 1️⃣2️⃣ Dhaka → UTC

উল্টো conversion:

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dhaka_time = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

utc_time = dhaka_time.astimezone(
    ZoneInfo("UTC")
)

print("Dhaka:", dhaka_time)
print("UTC:", utc_time)
```

---

# 1️⃣3️⃣ `astimezone()` ⭐⭐⭐

এই method timezone conversion-এর জন্য।

Syntax:

```python
dt.astimezone(target_timezone)
```

Example:

```python
converted = dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

---

# 1️⃣4️⃣ UTC → Japan

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc = datetime.now(timezone.utc)

tokyo = utc.astimezone(
    ZoneInfo("Asia/Tokyo")
)

print(tokyo)
```

---

# 1️⃣5️⃣ UTC → London

```python
london = utc.astimezone(
    ZoneInfo("Europe/London")
)

print(london)
```

---

# 1️⃣6️⃣ UTC → New York

```python
new_york = utc.astimezone(
    ZoneInfo("America/New_York")
)

print(new_york)
```

Notice করো:

```text
Asia/Dhaka
Asia/Tokyo
Europe/London
America/New_York
```

Timezone identifierগুলো সাধারণত **IANA timezone names**।

---

# 1️⃣7️⃣ কেন `+06:00` manually দেওয়া ভালো নয়?

তুমি হয়তো ভাবতে পারো:

```python
timezone(timedelta(hours=6))
```

এটা দিয়ে Bangladesh time তৈরি করব।

Technically fixed offset তৈরি করা যায়।

কিন্তু real timezone-এর জন্য:

```python
ZoneInfo("Asia/Dhaka")
```

ব্যবহার করা ভালো।

কারণ timezone শুধু একটা fixed number না—তার historical এবং regional rules থাকতে পারে।

---

# 1️⃣8️⃣ Timezone Conversion বনাম Changing Clock Time

এটা খুব important।

```python
utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

এখানে:

```text
Same instant
Different local representation
```

অর্থাৎ:

```text
UTC       → 08:00
Dhaka     → 14:00
```

দুটো একই মুহূর্ত।

---

# 1️⃣9️⃣ Aware Datetime Compare করা ⭐⭐⭐

দুটি timezone-aware datetime compare করা যায়।

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print(utc == dhaka)
```

Output:

```text
True
```

কারণ:

```text
Same instant
```

শুধু timezone representation আলাদা।

---

# 2️⃣0️⃣ Naive + Aware Compare করলে সমস্যা ⚠️

ধরো:

```python
from datetime import datetime, timezone

naive = datetime.now()

aware = datetime.now(timezone.utc)

print(naive < aware)
```

এটা সাধারণত:

```text
TypeError
```

দেবে।

কারণ:

```text
naive
+
aware
```

এভাবে directly compare করা যায় না।

---

# 2️⃣1️⃣ Naive Datetime-কে Aware করা

ধরো তুমি জানো এই datetime আসলে UTC:

```python
from datetime import datetime, timezone

naive = datetime(
    2026,
    8,
    17,
    8,
    0
)
```

এটা naive।

এটার timezone information **attach** করতে:

```python
aware = naive.replace(
    tzinfo=timezone.utc
)

print(aware)
```

Output:

```text
2026-08-17 08:00:00+00:00
```

⚠️ এখানে খুব গুরুত্বপূর্ণ বিষয়:

`replace(tzinfo=...)` timezone **conversion করে না**।

এটা শুধু timezone information attach করে।

---

# 2️⃣2️⃣ `replace()` বনাম `astimezone()` ⭐⭐⭐

### `replace()`

```python
dt.replace(tzinfo=timezone.utc)
```

মানে:

```text
এই datetime-কে UTC হিসেবে interpret করো
```

Clock time বদলায় না।

---

### `astimezone()`

```python
dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

মানে:

```text
Same instant
→ অন্য timezone-এর local clock time
```

Clock time পরিবর্তিত হতে পারে।

---

# 2️⃣3️⃣ Example

ধরো:

```python
from datetime import datetime, timezone

dt = datetime(
    2026,
    8,
    17,
    8,
    0,
    tzinfo=timezone.utc
)
```

Dhaka:

```python
from zoneinfo import ZoneInfo

dhaka = dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka)
```

Output:

```text
2026-08-17 14:00:00+06:00
```

কারণ:

```text
08:00 UTC
+
6 hours
=
14:00 Dhaka
```

---

# 2️⃣4️⃣ Timezone Name

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dt = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

print(dt.tzinfo)
```

---

# 2️⃣5️⃣ `utcoffset()`

Timezone থেকে UTC offset বের করতে:

```python
print(
    dt.utcoffset()
)
```

Dhaka-এর জন্য সাধারণত:

```text
6:00:00
```

---

# 2️⃣6️⃣ `tzname()`

```python
print(
    dt.tzname()
)
```

এটা timezone-এর name/abbreviation দিতে পারে।

তবে timezone abbreviation-এর উপর application logic নির্ভর না করাই ভালো; `Asia/Dhaka`-এর মতো IANA zone identifier বেশি নির্ভরযোগ্য।

---

# 2️⃣7️⃣ Current Time in Multiple Countries

```python
from datetime import datetime
from zoneinfo import ZoneInfo

zones = [
    "UTC",
    "Asia/Dhaka",
    "Asia/Tokyo",
    "Europe/London",
    "America/New_York"
]

for zone in zones:
    dt = datetime.now(
        ZoneInfo(zone)
    )

    print(zone, ":", dt)
```

---

# 2️⃣8️⃣ User Timezone Display ⭐⭐⭐

Backend-এ সাধারণ pattern:

```text
Database
   ↓
UTC datetime
   ↓
User timezone
   ↓
Frontend
```

ধরো database-এ UTC:

```python
utc_time = datetime.now(timezone.utc)
```

User Bangladesh-এ:

```python
user_time = utc_time.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

---

# 2️⃣9️⃣ Django/Backend-এর জন্য গুরুত্বপূর্ণ Pattern 🔥

Production backend-এ সাধারণ approach:

```text
Store
  ↓
UTC

Process
  ↓
UTC / timezone-aware

Display
  ↓
User's local timezone
```

অর্থাৎ:

```text
Database → UTC
Frontend → Local timezone
```

এতে বিভিন্ন দেশের user-এর সময় correctly handle করা সহজ হয়।

---

# 3️⃣0️⃣ API Example

API response:

```text
2026-08-17T08:00:00+00:00
```

Python:

```python
from datetime import datetime

text = "2026-08-17T08:00:00+00:00"

dt = datetime.fromisoformat(text)

print(dt)
```

তারপর Dhaka:

```python
from zoneinfo import ZoneInfo

dhaka = dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka)
```

---

# 3️⃣1️⃣ Output Formatting

```python
formatted = dhaka.strftime(
    "%d %B %Y, %I:%M %p"
)

print(formatted)
```

Output:

```text
17 August 2026, 02:00 PM
```

---

# 3️⃣2️⃣ Timezone-Aware `strptime()`

আগের Day 7-এর `strptime()`-এর সাথে timezone ব্যবহার করা যায়।

যেমন:

```python
from datetime import datetime

text = "2026-08-17 08:00 +0000"

dt = datetime.strptime(
    text,
    "%Y-%m-%d %H:%M %z"
)

print(dt)
```

এখানে `%z` timezone offset parse করে।

---

# 3️⃣3️⃣ ISO 8601 + Timezone ⭐⭐⭐

সবচেয়ে common API format:

```text
2026-08-17T08:00:00+00:00
```

Parse:

```python
from datetime import datetime

dt = datetime.fromisoformat(
    "2026-08-17T08:00:00+00:00"
)

print(dt)
```

তারপর:

```python
from zoneinfo import ZoneInfo

dhaka = dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka)
```

---

# 3️⃣4️⃣ Timezone-Aware `now()`

Avoid:

```python
datetime.now()
```

যখন তোমার application-এর জন্য timezone-aware time দরকার।

Prefer:

```python
datetime.now(timezone.utc)
```

অথবা user-specific timezone:

```python
datetime.now(
    ZoneInfo("Asia/Dhaka")
)
```

---

# 3️⃣5️⃣ Common Mistakes ⚠️

### Mistake 1

```python
datetime.now()
```

এর timezone নেই।

এটা সবসময় ভুল নয়, কিন্তু timezone-sensitive application-এ সমস্যা করতে পারে।

---

### Mistake 2

Naive এবং aware datetime compare করা:

```python
naive < aware
```

❌

---

### Mistake 3

`replace()` দিয়ে timezone conversion করা:

```python
dt.replace(
    tzinfo=ZoneInfo("Asia/Dhaka")
)
```

যদি `dt` আগে থেকেই অন্য timezone-এর instant represent করে, এটা conversion নয়।

---

### Mistake 4

Manual timezone offset hard-code করা:

```python
+ timedelta(hours=6)
```

Timezone conversion-এর বদলে।

Prefer:

```python
astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

---

# 🧪 Day 11 Practice

## Exercise 1

Current UTC time বের করো:

```python
datetime.now(timezone.utc)
```

---

## Exercise 2

Current Bangladesh time বের করো:

```python
ZoneInfo("Asia/Dhaka")
```

---

## Exercise 3

UTC time → Bangladesh time convert করো।

---

## Exercise 4

Bangladesh time → UTC convert করো।

---

## Exercise 5 ⭐

এই datetime:

```python
dt = datetime(
    2026,
    8,
    17,
    8,
    30,
    tzinfo=timezone.utc
)
```

এটাকে Dhaka time-এ convert করো।

---

## Exercise 6 ⭐

Naive datetime এবং aware datetime তৈরি করো।

তারপর:

```python
tzinfo
```

print করে difference দেখো।

---

## Exercise 7 ⭐⭐

এই API response parse করো:

```python
text = "2026-08-17T08:30:00+00:00"
```

তারপর Bangladesh local time-এ convert করো।

Expected:

```text
2026-08-17 14:30:00+06:00
```

---

# 🏆 Day 11 Mini Project

## 🌍 World Clock

একটি program বানাও:

```text
====================================
           WORLD CLOCK
====================================

UTC:
2026-08-17 08:30

Dhaka:
2026-08-17 14:30

Tokyo:
2026-08-17 17:30

London:
2026-08-17 09:30

New York:
2026-08-17 04:30

====================================
```

Use:

```python
datetime.now(timezone.utc)

ZoneInfo("Asia/Dhaka")
ZoneInfo("Asia/Tokyo")
ZoneInfo("Europe/London")
ZoneInfo("America/New_York")

astimezone()
strftime()
```

---

# 📌 Day 11 Cheat Sheet

### UTC

```python
from datetime import timezone

timezone.utc
```

### Current UTC

```python
datetime.now(timezone.utc)
```

### Dhaka

```python
from zoneinfo import ZoneInfo

ZoneInfo("Asia/Dhaka")
```

### Current Dhaka time

```python
datetime.now(
    ZoneInfo("Asia/Dhaka")
)
```

### Convert timezone

```python
dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

### Timezone info

```python
dt.tzinfo
```

### UTC offset

```python
dt.utcoffset()
```

### Naive → aware, when you KNOW the naive value represents UTC

```python
dt.replace(
    tzinfo=timezone.utc
)
```

### ISO string → aware datetime

```python
datetime.fromisoformat(text)
```

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Concept

```text
              DATETIME
                  │
          ┌───────┴────────┐
          │                │
        Naive            Aware
          │                │
      No timezone      Has timezone
                           │
                    ┌──────┴──────┐
                    │             │
                   UTC        Asia/Dhaka
                                  │
                            astimezone()
```

আর এই patternটা মনে রাখবে:

```python
utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

**UTC → local timezone conversion = `astimezone()`**

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations           ✅
Day 10 → Timestamp                   ✅
Day 11 → Timezone                    ✅ ← YOU ARE HERE
Day 12 → UTC + zoneinfo              ⏭️
Day 13 → Comparison + Sorting
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 12-এ `zoneinfo` আরও গভীরভাবে শিখব—timezone conversion, IANA timezone database, `fold`, DST concept, এবং production-ready timezone handling।**


# 🐍 Python `datetime` — Day 12

## `zoneinfo` Deep Dive + Production Timezone Handling

আজকের Day 12-এ আমরা `zoneinfo`-কে ভালোভাবে শিখব। এটা Python-এর **standard library**-এর অংশ এবং real-world application-এ timezone handle করার জন্য খুব গুরুত্বপূর্ণ।

Official documentation: [Python `zoneinfo` documentation](https://docs.python.org/3/library/zoneinfo.html?utm_source=chatgpt.com)

---

## 🎯 আজকের Learning Goals

আজ তুমি শিখবে:

```text
1. ZoneInfo কী
2. IANA timezone
3. ZoneInfo তৈরি করা
4. UTC ↔ local timezone
5. Multiple timezone conversion
6. `available_timezones()`
7. DST কী
8. `fold`
9. `replace()` বনাম `astimezone()`
10. Production timezone pattern
```

---

# 1️⃣ `zoneinfo` কী?

Python-এর:

```python
from zoneinfo import ZoneInfo
```

`ZoneInfo` ব্যবহার করে named timezone তৈরি করা যায়।

Example:

```python
from zoneinfo import ZoneInfo

dhaka = ZoneInfo("Asia/Dhaka")

print(dhaka)
```

Output:

```text
Asia/Dhaka
```

---

# 2️⃣ IANA Timezone কী?

Timezone-এর জন্য সাধারণত এই ধরনের নাম ব্যবহার করা হয়:

```text
Asia/Dhaka
Asia/Tokyo
Europe/London
America/New_York
Australia/Sydney
```

এগুলো **IANA time zone identifiers**।

তাই:

❌ শুধু:

```text
Dhaka
Tokyo
London
```

না লিখে,

✅ ব্যবহার করবে:

```text
Asia/Dhaka
Asia/Tokyo
Europe/London
```

---

# 3️⃣ Dhaka Time তৈরি করা

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dt = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

print(dt)
```

Output-এর মতো:

```text
2026-08-17 14:30:00+06:00
```

---

# 4️⃣ `tzinfo` কী?

```python
print(dt.tzinfo)
```

Output:

```text
Asia/Dhaka
```

অর্থাৎ datetime জানে:

```text
আমি কোন timezone-এর?
```

---

# 5️⃣ UTC থেকে Dhaka

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print("UTC   :", utc)
print("Dhaka :", dhaka)
```

Flow:

```text
UTC
 ↓
astimezone()
 ↓
Asia/Dhaka
```

---

# 6️⃣ Dhaka থেকে Tokyo

```python
from zoneinfo import ZoneInfo

tokyo = dhaka.astimezone(
    ZoneInfo("Asia/Tokyo")
)

print(tokyo)
```

---

# 7️⃣ একই মুহূর্ত, Different Timezone ⭐⭐⭐

ধরো:

```python
utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)

tokyo = utc.astimezone(
    ZoneInfo("Asia/Tokyo")
)
```

তখন:

```text
UTC       → 08:30
Dhaka     → 14:30
Tokyo     → 17:30
```

কিন্তু:

```python
print(utc == dhaka)
print(utc == tokyo)
```

Output:

```text
True
True
```

কারণ তিনটিই একই instant represent করছে।

---

# 8️⃣ `astimezone()` — সবচেয়ে গুরুত্বপূর্ণ ⭐⭐⭐

Syntax:

```python
dt.astimezone(target_timezone)
```

Example:

```python
japan = dt.astimezone(
    ZoneInfo("Asia/Tokyo")
)
```

মনে রাখো:

> `astimezone()` = একই মুহূর্তকে অন্য timezone-এ দেখানো।

---

# 9️⃣ `replace(tzinfo=...)` বনাম `astimezone()`

এই দুটো গুলিয়ে ফেলবে না।

### `replace()`

```python
dt.replace(
    tzinfo=ZoneInfo("Asia/Dhaka")
)
```

এটা timezone **convert করে না**।

এটা datetime-এর timezone information পরিবর্তন/attach করে।

---

### `astimezone()`

```python
dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

এটা একই instant রেখে local clock time convert করে।

### সহজ উদাহরণ

```text
replace()
    ↓
"এই clock time-টাকে এই timezone হিসেবে ধরো"

astimezone()
    ↓
"এই instant-টাকে অন্য timezone-এ দেখাও"
```

---

# 🔟 Fixed Offset বনাম Real Timezone

তুমি চাইলে:

```python
from datetime import timezone, timedelta

tz = timezone(
    timedelta(hours=6)
)
```

এটা একটি **fixed UTC offset**।

কিন্তু:

```python
ZoneInfo("Asia/Dhaka")
```

একটি named timezone।

Production application-এ named timezone দরকার হলে `ZoneInfo` ব্যবহার করাই ভালো।

---

# 1️⃣1️⃣ `ZoneInfo("UTC")`

UTC-এর জন্যও:

```python
from zoneinfo import ZoneInfo

utc = ZoneInfo("UTC")
```

ব্যবহার করা যায়।

তবে `datetime`-এর:

```python
timezone.utc
```

এটিও valid এবং convenient।

---

# 1️⃣2️⃣ Multiple Timezone Converter

একটি reusable function বানাই:

```python
from zoneinfo import ZoneInfo

def convert_timezone(dt, timezone_name):
    return dt.astimezone(
        ZoneInfo(timezone_name)
    )
```

Use:

```python
from datetime import datetime, timezone

utc = datetime.now(timezone.utc)

dhaka = convert_timezone(
    utc,
    "Asia/Dhaka"
)

tokyo = convert_timezone(
    utc,
    "Asia/Tokyo"
)

print(dhaka)
print(tokyo)
```

---

# 1️⃣3️⃣ Available Timezones ⭐⭐⭐

Python environment-এ available timezone names দেখতে:

```python
from zoneinfo import available_timezones

zones = available_timezones()

print(len(zones))
```

Specific timezone আছে কিনা:

```python
print("Asia/Dhaka" in zones)
```

Output:

```text
True
```

---

# 1️⃣4️⃣ Timezone List দেখা

```python
from zoneinfo import available_timezones

zones = sorted(
    available_timezones()
)

for zone in zones:
    print(zone)
```

⚠️ হাজার হাজার timezone থাকতে পারে, তাই সাধারণত সব print করার দরকার নেই।

---

# 1️⃣5️⃣ User Input থেকে Timezone

ধরো user input দিল:

```text
Asia/Dhaka
```

Python:

```python
from zoneinfo import ZoneInfo

zone_name = input(
    "Enter timezone: "
)

zone = ZoneInfo(zone_name)

print(zone)
```

তারপর:

```python
from datetime import datetime

now = datetime.now(zone)

print(now)
```

---

# 1️⃣6️⃣ Invalid Timezone Handle করা

User ভুল input দিতে পারে।

```python
from zoneinfo import ZoneInfo, ZoneInfoNotFoundError

try:
    zone = ZoneInfo("Invalid/Zone")
    print(zone)

except ZoneInfoNotFoundError:
    print("Timezone not found")
```

Production application-এ validation important।

---

# 1️⃣7️⃣ DST কী? ⭐⭐⭐

DST = **Daylight Saving Time**

কিছু timezone বছরে নির্দিষ্ট সময়ে clock পরিবর্তন করে।

উদাহরণ:

```text
Winter
↓
UTC-5

Summer
↓
UTC-4
```

এ কারণে:

```text
একটি timezone-এর UTC offset
সবসময় একই নাও হতে পারে।
```

---

# 1️⃣8️⃣ কেন `ZoneInfo` গুরুত্বপূর্ণ?

ধরো:

```python
from zoneinfo import ZoneInfo

ny = ZoneInfo("America/New_York")
```

তারপর:

```python
from datetime import datetime

dt = datetime(
    2026,
    1,
    15,
    12,
    tzinfo=ny
)

print(dt)
```

আর summer-এর date:

```python
dt2 = datetime(
    2026,
    7,
    15,
    12,
    tzinfo=ny
)

print(dt2)
```

দুটির UTC offset আলাদা হতে পারে।

এটাই named timezone ব্যবহারের বড় সুবিধা।

---

# 1️⃣9️⃣ `utcoffset()` দিয়ে Check

```python
print(dt.utcoffset())
print(dt2.utcoffset())
```

এতে ওই datetime-এর UTC offset দেখতে পারবে।

---

# 2️⃣0️⃣ Bangladesh-এর ক্ষেত্রে

Bangladesh সাধারণত:

```text
UTC+06:00
```

তাই:

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dhaka = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

print(dhaka.utcoffset())
```

সাধারণত:

```text
6:00:00
```

Bangladesh-এ বর্তমানে DST ব্যবহার করা হয় না, তাই Dhaka-এর offset সাধারণত UTC+6 থাকে।

---

# 2️⃣1️⃣ DST-এর সবচেয়ে Interesting বিষয় — `fold` ⭐⭐⭐

কিছু timezone-এ clock পিছিয়ে গেলে একই local clock time **দুইবার** আসতে পারে।

যেমন conceptually:

```text
01:30
02:30
01:30
02:30
```

তখন প্রশ্ন:

```text
01:30 কোনটা?
```

Python `fold` দিয়ে এই ambiguity handle করতে পারে।

---

# 2️⃣2️⃣ `fold=0` এবং `fold=1`

Example:

```python
from datetime import datetime
from zoneinfo import ZoneInfo

dt = datetime(
    2026,
    11,
    1,
    1,
    30,
    tzinfo=ZoneInfo("America/New_York"),
    fold=0
)

print(dt)
```

আর:

```python
dt2 = dt.replace(fold=1)

print(dt2)
```

এখানে:

```text
fold=0
↓
first occurrence

fold=1
↓
second occurrence
```

এটা advanced timezone handling-এ দরকার হয়।

---

# 2️⃣3️⃣ `fold` কখন গুরুত্বপূর্ণ?

সাধারণ Dhaka-based application-এ সাধারণত তোমাকে এটা নিয়ে চিন্তা করতে হবে না।

কিন্তু:

```text
International application
Booking system
Flight system
Calendar
Scheduling software
```

এগুলোতে DST timezone থাকলে `fold` important হতে পারে।

---

# 2️⃣4️⃣ UTC-তে Store করা ⭐⭐⭐

Production application-এর একটি common strategy:

```text
User
 ↓
Local Time
 ↓
Convert to UTC
 ↓
Database
```

যেমন:

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

user_time = datetime.now(
    ZoneInfo("Asia/Dhaka")
)

utc_time = user_time.astimezone(
    timezone.utc
)

print(utc_time)
```

---

# 2️⃣5️⃣ Database থেকে UTC → User Time

ধরো database থেকে UTC datetime পেয়েছ:

```python
from datetime import datetime, timezone

db_time = datetime.now(timezone.utc)
```

User Bangladesh:

```python
from zoneinfo import ZoneInfo

user_time = db_time.astimezone(
    ZoneInfo("Asia/Dhaka")
)

print(user_time)
```

Flow:

```text
DATABASE
   ↓
UTC
   ↓
User timezone
   ↓
UI
```

---

# 2️⃣6️⃣ API Response-এর জন্য

Backend থেকে:

```python
dt = datetime.now(timezone.utc)

print(dt.isoformat())
```

Output:

```text
2026-08-17T08:30:00+00:00
```

এটা API-এর জন্য খুব useful format।

Frontend চাইলে user-এর timezone অনুযায়ী display করতে পারে।

---

# 2️⃣7️⃣ User Timezone Preference

ধরো database:

```python
user_timezone = "Asia/Dhaka"
```

তারপর:

```python
from zoneinfo import ZoneInfo
from datetime import datetime, timezone

utc = datetime.now(timezone.utc)

user_time = utc.astimezone(
    ZoneInfo(user_timezone)
)

print(user_time)
```

এভাবে application-এ user-specific timezone support করা যায়।

---

# 2️⃣8️⃣ Real-world Function ⭐⭐⭐

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

def get_user_time(timezone_name):
    utc = datetime.now(timezone.utc)

    return utc.astimezone(
        ZoneInfo(timezone_name)
    )
```

Use:

```python
print(
    get_user_time("Asia/Dhaka")
)

print(
    get_user_time("Asia/Tokyo")
)
```

---

# 2️⃣9️⃣ Better Function — Format সহ

```python
def get_user_time(
    timezone_name,
    format_string="%Y-%m-%d %H:%M:%S"
):
    utc = datetime.now(timezone.utc)

    local = utc.astimezone(
        ZoneInfo(timezone_name)
    )

    return local.strftime(format_string)
```

Use:

```python
print(
    get_user_time("Asia/Dhaka")
)
```

---

# 3️⃣0️⃣ Timezone Converter Project

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc = datetime.now(timezone.utc)

zones = {
    "Dhaka": "Asia/Dhaka",
    "Tokyo": "Asia/Tokyo",
    "London": "Europe/London",
    "New York": "America/New_York",
}

print("UTC:", utc)

for name, zone in zones.items():

    local = utc.astimezone(
        ZoneInfo(zone)
    )

    print(
        f"{name}: {local}"
    )
```

---

# 3️⃣1️⃣ Production Rule ⭐⭐⭐⭐⭐

এই rule মনে রাখো:

```text
                TIMEZONE STRATEGY

Database
   ↓
UTC / timezone-aware
   ↓
Backend processing
   ↓
UTC / timezone-aware
   ↓
User timezone
   ↓
Display
```

আর:

```text
Don't:
naive datetime everywhere

Prefer:
timezone-aware datetime
```

---

# 3️⃣2️⃣ Common Mistakes

### ❌ Mistake 1

```python
datetime.now()
```

timezone-sensitive backend code-এ blindly ব্যবহার করা।

---

### ❌ Mistake 2

```python
dt.replace(
    tzinfo=ZoneInfo("Asia/Dhaka")
)
```

কে timezone conversion মনে করা।

---

### ❌ Mistake 3

```python
dt + timedelta(hours=6)
```

দিয়ে timezone conversion করা।

---

### ❌ Mistake 4

User-এর local time সরাসরি database-এ store করা।

---

### ❌ Mistake 5

Timezone string hard-code করে application-এর সব জায়গায় আলাদা আলাদা logic লেখা।

Better:

```python
user_timezone = "Asia/Dhaka"
```

তারপর:

```python
ZoneInfo(user_timezone)
```

---

# 🧪 Day 12 Practice

### Exercise 1

Current UTC বের করো।

### Exercise 2

Current Dhaka time বের করো।

### Exercise 3

UTC → Dhaka → Tokyo conversion করো।

### Exercise 4

`available_timezones()` ব্যবহার করে check করো:

```text
Asia/Dhaka
Asia/Tokyo
Europe/London
```

available কিনা।

### Exercise 5 ⭐

একটি function বানাও:

```python
convert_timezone(dt, timezone_name)
```

### Exercise 6 ⭐⭐

এই UTC datetime:

```python
dt = datetime(
    2026,
    8,
    17,
    8,
    30,
    tzinfo=timezone.utc
)
```

এগুলোতে convert করো:

```text
Asia/Dhaka
Asia/Tokyo
Europe/London
America/New_York
```

### Exercise 7 🔥

একটি **World Clock** বানাও যেখানে user timezone name input দিলে সেই timezone-এর current time দেখাবে।

Example:

```text
Enter timezone: Asia/Dhaka

Current Time:
2026-08-17 14:30:00+06:00
```

---

# 🏆 Day 12 Mini Project

## 🌍 Timezone Converter

Input:

```text
Enter date:
2026-08-17 08:30

Enter source timezone:
UTC

Enter target timezone:
Asia/Dhaka
```

Output:

```text
================================

Source:
2026-08-17 08:30 UTC

Target:
2026-08-17 14:30 Asia/Dhaka

================================
```

তোমার code-এ ব্যবহার করবে:

```python
datetime
timezone
ZoneInfo
astimezone()
strptime()
strftime()
```

---

# 📌 Day 12 Cheat Sheet

```python
from zoneinfo import ZoneInfo
```

### Dhaka

```python
ZoneInfo("Asia/Dhaka")
```

### UTC

```python
ZoneInfo("UTC")
```

### Current timezone time

```python
datetime.now(
    ZoneInfo("Asia/Dhaka")
)
```

### Convert

```python
dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

### Available zones

```python
from zoneinfo import available_timezones

available_timezones()
```

### Offset

```python
dt.utcoffset()
```

### DST ambiguity

```python
dt.fold
```

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ ৫টি জিনিস

```text
1. ZoneInfo
      ↓
   Named timezone

2. astimezone()
      ↓
   Timezone conversion

3. timezone-aware datetime
      ↓
   Production-friendly

4. UTC
      ↓
   Common backend/database reference

5. zoneinfo
      ↓
   IANA timezone rules
```

### সবচেয়ে গুরুত্বপূর্ণ pattern:

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

utc = datetime.now(timezone.utc)

dhaka = utc.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

এটাই আজকের core pattern। 🔥

---

## 🚀 `datetime` Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations            ✅
Day 10 → Unix Timestamp              ✅
Day 11 → Timezone Basics              ✅
Day 12 → zoneinfo Deep Dive           ✅ ← YOU ARE HERE
Day 13 → Comparison + Sorting         ⏭️
Day 14 → Real-world Patterns
Day 15 → 🔥 Final Project
```

**Day 13-এ datetime/date comparison, sorting, filtering এবং real-world deadline/event data নিয়ে কাজ করব।**


# 🐍 Python `datetime` — Day 13

## Comparison, Sorting & Filtering Dates

আজকের লক্ষ্য হলো `date` এবং `datetime` নিয়ে **compare, sort, filter এবং deadline/event system** তৈরি করা।

Official documentation: [Python `datetime` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

---

## 🎯 আজ যা শিখবে

```text
1. Date comparison
2. Datetime comparison
3. == != < > <= >=
4. Sorting dates
5. Sorting datetime
6. Filtering
7. Upcoming events
8. Expired events
9. Deadline checker
10. Nearest date
11. Oldest/Newest record
12. Real-world project
```

---

# 1️⃣ Date Comparison

```python
from datetime import date

a = date(2026, 8, 10)
b = date(2026, 8, 17)

print(a < b)
print(a > b)
print(a == b)
```

Output:

```text
True
False
False
```

কারণ:

```text
August 10 < August 17
```

---

# 2️⃣ সব Comparison Operator

Python-এ:

```python
a == b
a != b
a < b
a > b
a <= b
a >= b
```

Example:

```python
from datetime import date

today = date.today()
deadline = date(2026, 8, 20)

if today < deadline:
    print("Deadline is upcoming")
```

---

# 3️⃣ আজ Deadline কিনা?

```python
from datetime import date

today = date.today()
deadline = date(2026, 8, 17)

if today == deadline:
    print("Deadline is today")
```

---

# 4️⃣ Deadline Passed কিনা

```python
if today > deadline:
    print("Deadline passed")
else:
    print("Deadline not passed")
```

---

# 5️⃣ Deadline Future কিনা

```python
if deadline > today:
    print("Upcoming")
```

---

# 6️⃣ Date Difference ⭐⭐⭐

```python
from datetime import date

today = date.today()
deadline = date(2026, 8, 25)

remaining = deadline - today

print(remaining.days)
```

যদি deadline future হয়:

```text
remaining.days
```

দিয়ে কতদিন বাকি আছে পাওয়া যাবে।

---

# 7️⃣ Deadline Status Function

Reusable function:

```python
from datetime import date

def deadline_status(deadline):
    today = date.today()

    if deadline < today:
        return "Expired"

    elif deadline == today:
        return "Today"

    else:
        return "Upcoming"
```

Use:

```python
deadline = date(2026, 8, 25)

print(deadline_status(deadline))
```

---

# 8️⃣ Days Remaining Function

```python
from datetime import date

def days_remaining(deadline):
    today = date.today()

    return (deadline - today).days
```

Use:

```python
deadline = date(2026, 8, 25)

print(days_remaining(deadline))
```

---

# 9️⃣ Date Sorting ⭐⭐⭐

Python date automatically sort করতে পারে।

```python
from datetime import date

dates = [
    date(2026, 8, 20),
    date(2026, 8, 5),
    date(2026, 8, 15),
    date(2026, 8, 1),
]

dates.sort()

for d in dates:
    print(d)
```

Output:

```text
2026-08-01
2026-08-05
2026-08-15
2026-08-20
```

---

# 🔟 Reverse Sorting

Latest → oldest:

```python
dates.sort(reverse=True)

for d in dates:
    print(d)
```

Output:

```text
2026-08-20
2026-08-15
2026-08-05
2026-08-01
```

---

# 1️⃣1️⃣ `sorted()` vs `.sort()`

### `.sort()`

Original list পরিবর্তন করে:

```python
dates.sort()
```

### `sorted()`

নতুন list return করে:

```python
sorted_dates = sorted(dates)
```

Example:

```python
dates = [3, 1, 2]

new_dates = sorted(dates)

print(dates)
print(new_dates)
```

Output:

```text
[3, 1, 2]
[1, 2, 3]
```

---

# 1️⃣2️⃣ Earliest Date

```python
earliest = min(dates)

print(earliest)
```

---

# 1️⃣3️⃣ Latest Date

```python
latest = max(dates)

print(latest)
```

---

# 1️⃣4️⃣ Datetime Sorting

```python
from datetime import datetime

records = [
    datetime(2026, 8, 17, 15, 30),
    datetime(2026, 8, 17, 10, 30),
    datetime(2026, 8, 17, 20, 30),
]

records.sort()

for dt in records:
    print(dt)
```

Output:

```text
2026-08-17 10:30:00
2026-08-17 15:30:00
2026-08-17 20:30:00
```

---

# 1️⃣5️⃣ Real-world Event Data ⭐⭐⭐

ধরো:

```python
from datetime import date

events = [
    {
        "name": "Python Exam",
        "date": date(2026, 8, 20)
    },
    {
        "name": "Project Demo",
        "date": date(2026, 8, 18)
    },
    {
        "name": "Assignment",
        "date": date(2026, 8, 25)
    }
]
```

এখন date অনুযায়ী sort:

```python
events.sort(
    key=lambda event: event["date"]
)
```

Print:

```python
for event in events:
    print(
        event["name"],
        event["date"]
    )
```

---

# 1️⃣6️⃣ `key=` কী?

এই code:

```python
events.sort(
    key=lambda event: event["date"]
)
```

মানে:

> প্রতিটি dictionary-এর `date` value ব্যবহার করে sorting করো।

---

# 1️⃣7️⃣ Latest Event First

```python
events.sort(
    key=lambda event: event["date"],
    reverse=True
)
```

এখন:

```text
Latest
  ↓
Oldest
```

---

# 1️⃣8️⃣ Upcoming Events ⭐⭐⭐

আজকের পরে যেসব event:

```python
from datetime import date

today = date.today()

upcoming = [
    event
    for event in events
    if event["date"] > today
]

for event in upcoming:
    print(event)
```

এখানে আমরা **list comprehension + datetime comparison** ব্যবহার করেছি।

---

# 1️⃣9️⃣ Today's Events

```python
today_events = [
    event
    for event in events
    if event["date"] == today
]
```

---

# 2️⃣0️⃣ Past Events

```python
past_events = [
    event
    for event in events
    if event["date"] < today
]
```

---

# 2️⃣1️⃣ তিনটি Category

```text
event date < today
        ↓
      PAST

event date == today
        ↓
      TODAY

event date > today
        ↓
    UPCOMING
```

Python:

```python
for event in events:

    if event["date"] < today:
        status = "PAST"

    elif event["date"] == today:
        status = "TODAY"

    else:
        status = "UPCOMING"

    print(event["name"], status)
```

---

# 2️⃣2️⃣ Event Status Function

আরও clean:

```python
from datetime import date

def get_status(event_date):
    today = date.today()

    if event_date < today:
        return "PAST"

    if event_date == today:
        return "TODAY"

    return "UPCOMING"
```

Use:

```python
for event in events:
    print(
        event["name"],
        get_status(event["date"])
    )
```

---

# 2️⃣3️⃣ Days Until Event ⭐⭐⭐

```python
from datetime import date

today = date.today()

for event in events:

    days = (
        event["date"] - today
    ).days

    print(
        event["name"],
        days
    )
```

Output concept:

```text
Python Exam    3
Project Demo   1
Assignment     8
```

Negative হলে event already passed।

---

# 2️⃣4️⃣ Better Event Display

```python
for event in events:

    days = (
        event["date"] - today
    ).days

    print(
        f"{event['name']}: "
        f"{days} days"
    )
```

---

# 2️⃣5️⃣ Nearest Upcoming Event 🔥

প্রথমে upcoming events:

```python
upcoming = [
    event
    for event in events
    if event["date"] >= today
]
```

তারপর sort:

```python
upcoming.sort(
    key=lambda event: event["date"]
)
```

তারপর:

```python
if upcoming:
    nearest = upcoming[0]

    print(
        "Next event:",
        nearest["name"]
    )
```

---

# 2️⃣6️⃣ `min()` দিয়ে Nearest Event

আরও compact:

```python
nearest = min(
    upcoming,
    key=lambda event: event["date"]
)
```

---

# 2️⃣7️⃣ Event List Example ⭐⭐⭐

```python
from datetime import date

events = [
    {
        "name": "Python Exam",
        "date": date(2026, 8, 20)
    },
    {
        "name": "Project Demo",
        "date": date(2026, 8, 18)
    },
    {
        "name": "Assignment",
        "date": date(2026, 8, 25)
    },
    {
        "name": "Old Meeting",
        "date": date(2026, 8, 10)
    }
]

today = date(2026, 8, 17)

upcoming = [
    event
    for event in events
    if event["date"] >= today
]

upcoming.sort(
    key=lambda event: event["date"]
)

for event in upcoming:
    print(
        event["name"],
        event["date"]
    )
```

---

# 2️⃣8️⃣ Datetime Filtering

এবার শুধু date না, time-ও থাকবে।

```python
from datetime import datetime

appointments = [
    datetime(2026, 8, 17, 10, 0),
    datetime(2026, 8, 17, 14, 0),
    datetime(2026, 8, 17, 18, 0),
]
```

Current time:

```python
now = datetime.now()
```

Future appointments:

```python
upcoming = [
    appointment
    for appointment in appointments
    if appointment > now
]
```

---

# 2️⃣9️⃣ Sort Appointments

```python
appointments.sort()

for appointment in appointments:
    print(appointment)
```

---

# 3️⃣0️⃣ Today's Appointments

```python
today = date.today()

today_appointments = [
    appointment
    for appointment in appointments
    if appointment.date() == today
]
```

খেয়াল করো:

```python
appointment.date()
```

`datetime` থেকে `date` বের করে।

---

# 3️⃣1️⃣ Date থেকে Datetime

```python
from datetime import date, datetime, time

d = date(2026, 8, 17)

dt = datetime.combine(
    d,
    time(10, 30)
)

print(dt)
```

Output:

```text
2026-08-17 10:30:00
```

---

# 3️⃣2️⃣ `datetime.combine()` ⭐⭐⭐

Syntax:

```python
datetime.combine(
    date_object,
    time_object
)
```

Example:

```python
d = date(2026, 8, 20)
t = time(15, 30)

dt = datetime.combine(d, t)
```

---

# 3️⃣3️⃣ Date Range Filtering

ধরো:

```python
start = date(2026, 8, 15)
end = date(2026, 8, 25)
```

যে events range-এর মধ্যে:

```python
filtered = [
    event
    for event in events
    if start <= event["date"] <= end
]
```

এটা খুব important pattern।

---

# 3️⃣4️⃣ Month Filtering

ধরো শুধু August-এর events চাই:

```python
august_events = [
    event
    for event in events
    if event["date"].year == 2026
    and event["date"].month == 8
]
```

---

# 3️⃣5️⃣ Year Filtering

```python
year_events = [
    event
    for event in events
    if event["date"].year == 2026
]
```

---

# 3️⃣6️⃣ Weekday Filtering

শুধু Monday-এর events:

```python
monday_events = [
    event
    for event in events
    if event["date"].weekday() == 0
]
```

---

# 3️⃣7️⃣ Weekend Events

```python
weekend_events = [
    event
    for event in events
    if event["date"].weekday() >= 5
]
```

---

# 3️⃣8️⃣ Sorting by Multiple Fields

ধরো events:

```python
events = [
    {
        "name": "Exam A",
        "date": date(2026, 8, 20),
        "priority": 2
    },
    {
        "name": "Exam B",
        "date": date(2026, 8, 20),
        "priority": 1
    }
]
```

Date + priority অনুযায়ী:

```python
events.sort(
    key=lambda e: (
        e["date"],
        e["priority"]
    )
)
```

এটা real-world application-এ খুব useful।

---

# 3️⃣9️⃣ Deadline Manager 🔥

```python
from datetime import date

tasks = [
    {
        "task": "Learn Python",
        "deadline": date(2026, 8, 20)
    },
    {
        "task": "Build API",
        "deadline": date(2026, 8, 18)
    },
    {
        "task": "Finish Project",
        "deadline": date(2026, 8, 25)
    }
]

today = date(2026, 8, 17)

tasks.sort(
    key=lambda task: task["deadline"]
)

for task in tasks:

    remaining = (
        task["deadline"] - today
    ).days

    print(
        task["task"],
        "→",
        remaining,
        "days"
    )
```

---

# 4️⃣0️⃣ Priority + Deadline

আরও advanced:

```python
tasks = [
    {
        "task": "API",
        "deadline": date(2026, 8, 20),
        "priority": 1
    },
    {
        "task": "Frontend",
        "deadline": date(2026, 8, 18),
        "priority": 2
    }
]
```

Sort:

```python
tasks.sort(
    key=lambda task: (
        task["deadline"],
        task["priority"]
    )
)
```

---

# 4️⃣1️⃣ Timezone-aware Datetime Sorting ⭐⭐⭐

Timezone-aware datetime হলে:

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

events = [
    datetime(
        2026,
        8,
        17,
        14,
        0,
        tzinfo=ZoneInfo("Asia/Dhaka")
    ),
    datetime(
        2026,
        8,
        17,
        10,
        0,
        tzinfo=timezone.utc
    )
]

events.sort()

for event in events:
    print(event)
```

Python absolute instant অনুযায়ী aware datetime compare করতে পারে।

---

# 4️⃣2️⃣ Naive + Aware Mix করা যাবে না ⚠️

এই ধরনের list:

```python
events = [
    datetime.now(),
    datetime.now(timezone.utc)
]
```

sort করলে সমস্যা হতে পারে।

কারণ:

```text
Naive
+
Aware
```

একসাথে compare করা যায় না।

Production code-এ একই timezone strategy maintain করো।

---

# 4️⃣3️⃣ Real-world Pattern

Backend system-এ:

```text
Database
   ↓
UTC-aware datetime
   ↓
Filter
   ↓
Sort
   ↓
Convert to user timezone
   ↓
Display
```

এটা খুব common architecture।

---

# 🧪 Day 13 Practice

## Exercise 1

দুটি date compare করো:

```python
a = date(2026, 8, 10)
b = date(2026, 8, 20)
```

Check:

```text
a < b
a > b
a == b
```

---

## Exercise 2

এই dates ascending order-এ sort করো:

```python
dates = [
    date(2026, 8, 25),
    date(2026, 8, 5),
    date(2026, 8, 18),
    date(2026, 8, 1),
]
```

---

## Exercise 3

Earliest এবং latest date বের করো।

---

## Exercise 4 ⭐

একটি deadline function বানাও:

```python
deadline_status(deadline)
```

Return:

```text
PAST
TODAY
UPCOMING
```

---

## Exercise 5 ⭐

এই events থেকে শুধু upcoming events বের করো:

```python
events = [
    {
        "name": "Exam",
        "date": date(2026, 8, 20)
    },
    {
        "name": "Meeting",
        "date": date(2026, 8, 10)
    },
    {
        "name": "Project",
        "date": date(2026, 8, 25)
    }
]
```

---

## Exercise 6 ⭐⭐

Upcoming events-কে nearest-first sort করো।

---

## Exercise 7 🔥

একটি **Task Deadline Manager** বানাও:

প্রতিটি task-এর:

```text
name
deadline
priority
```

থাকবে।

Output:

```text
Task              Deadline       Days Left    Priority
------------------------------------------------------
API               2026-08-18     1            1
Python             2026-08-20     3            2
Project            2026-08-25     8            1
```

---

# 🏆 Day 13 Mini Project

## 📅 Event Manager

তোমার program-এ থাকবে:

```text
====================================
          EVENT MANAGER
====================================

1. Show all events
2. Show upcoming events
3. Show past events
4. Show today's events
5. Show next event
6. Sort by date
7. Search by month
8. Search by date range
```

Example:

```text
Upcoming Events
------------------------------------

Project Demo
2026-08-18
1 day left

Python Exam
2026-08-20
3 days left

Assignment
2026-08-25
8 days left
```

এই project-এ আজকের প্রায় সব concept ব্যবহার হবে:

```python
date
datetime
timedelta
sorted()
sort()
min()
max()
lambda
list comprehension
comparison
filtering
```

---

# 📌 Day 13 Cheat Sheet

### Compare

```python
a < b
a > b
a == b
a != b
```

### Difference

```python
(b - a).days
```

### Sort

```python
dates.sort()
```

### Reverse

```python
dates.sort(reverse=True)
```

### New sorted list

```python
sorted_dates = sorted(dates)
```

### Earliest

```python
min(dates)
```

### Latest

```python
max(dates)
```

### Sort dictionary records

```python
items.sort(
    key=lambda x: x["date"]
)
```

### Filter

```python
[
    x for x in items
    if x["date"] > today
]
```

### Date range

```python
start <= d <= end
```

### Date → datetime

```python
datetime.combine(d, t)
```

### Datetime → date

```python
dt.date()
```

---

# 🧠 Day 13-এর Core Pattern

এই patternটা খুব ভালোভাবে আয়ত্ত করো:

```python
from datetime import date

today = date.today()

upcoming = [
    event
    for event in events
    if event["date"] >= today
]

upcoming.sort(
    key=lambda event: event["date"]
)
```

এখানে একসাথে:

```text
comparison
+
filtering
+
list comprehension
+
sorting
+
lambda
```

ব্যবহার হয়েছে।

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations           ✅
Day 10 → Unix Timestamp              ✅
Day 11 → Timezone Basics             ✅
Day 12 → zoneinfo Deep Dive          ✅
Day 13 → Comparison + Sorting        ✅ ← YOU ARE HERE
Day 14 → Real-world Patterns         ⏭️
Day 15 → 🔥 Final Project
```

**Day 14-এ আমরা `datetime`-এর real-world patterns—logging, scheduling, API data, database timestamps, age calculation, expiry, recurring tasks এবং reusable utility functions—একসাথে practice করব।**


# 🐍 Python `datetime` — Day 14

## Real-World Applications & Production Patterns

আজ আমরা `datetime`-কে শুধু শেখার জন্য না, **real application-এ কীভাবে ব্যবহার করতে হয়** সেটা শিখব।

Official documentation: [Python `datetime` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

---

## 🎯 আজকের লক্ষ্য

```text
1. Age calculation
2. Expiry system
3. Login/session expiry
4. API timestamps
5. Logging
6. File timestamps
7. Scheduling
8. Reminder system
9. Recurring dates
10. Database timestamp pattern
11. Utility functions
12. Production best practices
```

---

# 1️⃣ Age Calculation

ধরো জন্মতারিখ:

```python
from datetime import date

birth_date = date(2000, 5, 10)
today = date.today()
```

শুধু:

```python
today.year - birth_date.year
```

করলে সবসময় exact age পাওয়া যাবে না।

কারণ এ বছরের birthday এসেছে কিনা দেখতে হবে।

```python
age = today.year - birth_date.year

if (today.month, today.day) < (
    birth_date.month,
    birth_date.day
):
    age -= 1

print(age)
```

### Reusable function

```python
from datetime import date

def calculate_age(birth_date):
    today = date.today()

    age = today.year - birth_date.year

    if (today.month, today.day) < (
        birth_date.month,
        birth_date.day
    ):
        age -= 1

    return age
```

Use:

```python
birth = date(2000, 5, 10)

print(calculate_age(birth))
```

---

# 2️⃣ Expiry System ⭐⭐⭐

এটা e-commerce, subscription, OTP, token ইত্যাদিতে খুব common।

ধরো:

```python
from datetime import datetime, timedelta

created_at = datetime.now()
expires_at = created_at + timedelta(hours=24)

print(expires_at)
```

Check:

```python
now = datetime.now()

if now >= expires_at:
    print("Expired")
else:
    print("Still valid")
```

---

# 3️⃣ Expiry Function

```python
def is_expired(expires_at):
    return datetime.now() >= expires_at
```

Use:

```python
if is_expired(expires_at):
    print("Expired")
```

---

# 4️⃣ Better: UTC-based Expiry ⭐⭐⭐⭐⭐

Production backend-এ timezone-aware UTC ব্যবহার করা ভালো।

```python
from datetime import datetime, timezone, timedelta

created_at = datetime.now(timezone.utc)

expires_at = (
    created_at
    + timedelta(hours=24)
)

now = datetime.now(timezone.utc)

if now >= expires_at:
    print("Expired")
else:
    print("Valid")
```

Pattern:

```text
UTC now
  ↓
+ duration
  ↓
expiry time
  ↓
compare with UTC now
```

---

# 5️⃣ OTP Expiration

ধরো OTP 5 মিনিট valid:

```python
from datetime import datetime, timezone, timedelta

created_at = datetime.now(timezone.utc)

expires_at = (
    created_at
    + timedelta(minutes=5)
)
```

Check:

```python
now = datetime.now(timezone.utc)

if now > expires_at:
    print("OTP expired")
else:
    print("OTP valid")
```

---

# 6️⃣ Remaining Time

```python
remaining = expires_at - now

print(remaining)
```

Seconds:

```python
print(remaining.total_seconds())
```

---

# 7️⃣ Countdown

```python
remaining = expires_at - now

if remaining.total_seconds() > 0:
    print(
        f"{remaining.total_seconds():.0f} "
        "seconds remaining"
    )
else:
    print("Expired")
```

---

# 8️⃣ Session Expiration

ধরো session 30 minutes:

```python
session_created = datetime.now(timezone.utc)

session_expires = (
    session_created
    + timedelta(minutes=30)
)
```

Check:

```python
if datetime.now(timezone.utc) >= session_expires:
    print("Session expired")
```

এখানে `datetime` backend authentication-এর সাথে directly useful।

---

# 9️⃣ API Timestamp ⭐⭐⭐

Backend API-তে timestamp পাঠাতে:

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)

response = {
    "created_at": now.isoformat()
}

print(response)
```

Output-এর মতো:

```text
{
    "created_at": "2026-08-17T08:30:00+00:00"
}
```

---

# 🔟 ISO 8601 কেন?

API-এর জন্য:

```text
2026-08-17T08:30:00+00:00
```

এর মতো format খুব useful কারণ:

- machine-readable
    
- timezone information থাকে
    
- বিভিন্ন language/framework সহজে parse করতে পারে
    

---

# 1️⃣1️⃣ API Response Parse

ধরো API থেকে:

```python
text = "2026-08-17T08:30:00+00:00"
```

Parse:

```python
from datetime import datetime

dt = datetime.fromisoformat(text)

print(dt)
```

---

# 1️⃣2️⃣ Logging ⭐⭐⭐

Application-এ event কখন ঘটেছে সেটা record করতে timestamp লাগে।

```python
from datetime import datetime, timezone

timestamp = datetime.now(timezone.utc)

print(
    f"[{timestamp.isoformat()}] "
    "User logged in"
)
```

Output:

```text
[2026-08-17T08:30:00+00:00] User logged in
```

---

# 1️⃣3️⃣ Simple Logger

```python
from datetime import datetime, timezone

def log(message):
    timestamp = datetime.now(timezone.utc)

    print(
        f"[{timestamp.isoformat()}] "
        f"{message}"
    )
```

Use:

```python
log("Server started")
log("User logged in")
log("API request received")
```

Output:

```text
[2026-08-17T08:30:00+00:00] Server started
[2026-08-17T08:30:02+00:00] User logged in
[2026-08-17T08:30:05+00:00] API request received
```

---

# 1️⃣4️⃣ File Modification Time

Python-এর `os` module-এর সাথে `datetime` খুব সুন্দরভাবে কাজ করে।

```python
import os
from datetime import datetime

timestamp = os.path.getmtime("example.txt")

dt = datetime.fromtimestamp(timestamp)

print(dt)
```

এখানে:

```text
os
 ↓
Unix timestamp
 ↓
datetime
```

---

# 1️⃣5️⃣ File Creation Time

Platform অনুযায়ী semantics আলাদা হতে পারে, তবে Python-এ:

```python
timestamp = os.path.getctime(
    "example.txt"
)

dt = datetime.fromtimestamp(timestamp)

print(dt)
```

Filesystem metadata নিয়ে কাজ করার সময় OS/platform differences মাথায় রাখতে হবে।

---

# 1️⃣6️⃣ Scheduling

ধরো:

```python
from datetime import datetime

target = datetime(
    2026,
    8,
    20,
    10,
    30
)

now = datetime.now()

if now >= target:
    print("Run task")
else:
    print("Wait")
```

এটাই scheduling-এর basic concept।

---

# 1️⃣7️⃣ Time Until Event

```python
remaining = target - now

print(
    f"{remaining.days} days remaining"
)
```

আরও detail:

```python
print(
    remaining.total_seconds()
)
```

---

# 1️⃣8️⃣ Reminder System 🔔

```python
from datetime import datetime, timedelta

reminder_time = (
    datetime.now()
    + timedelta(minutes=10)
)

print(
    "Reminder:",
    reminder_time
)
```

তারপর:

```python
if datetime.now() >= reminder_time:
    print("🔔 Reminder!")
```

---

# 1️⃣9️⃣ Recurring Task

প্রতিদিন:

```python
from datetime import datetime, timedelta

next_run = datetime.now()

for i in range(5):
    print(next_run)

    next_run += timedelta(days=1)
```

Output concept:

```text
Day 1
Day 2
Day 3
Day 4
Day 5
```

---

# 2️⃣0️⃣ Weekly Schedule

```python
next_week = (
    datetime.now()
    + timedelta(days=7)
)

print(next_week)
```

---

# 2️⃣1️⃣ Monthly Schedule — সতর্কতা ⚠️

Month-এর length একই নয়:

```text
January   → 31
February  → 28/29
April     → 30
```

তাই:

```python
timedelta(days=30)
```

সবসময় "এক মাস পরে" বোঝায় না।

যেমন:

```text
January 31
+ 30 days
≠ February 28/29
```

Calendar-month arithmetic-এর জন্য `dateutil`-এর মতো external library কাজে লাগতে পারে, কিন্তু আজ আমরা standard `datetime`-এর মধ্যেই থাকছি।

---

# 2️⃣2️⃣ Start of Day

ধরো একটি datetime:

```python
from datetime import datetime

dt = datetime(
    2026,
    8,
    17,
    15,
    45,
    30
)
```

দিনের শুরু:

```python
start_of_day = dt.replace(
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)

print(start_of_day)
```

Output:

```text
2026-08-17 00:00:00
```

---

# 2️⃣3️⃣ End of Day

```python
end_of_day = dt.replace(
    hour=23,
    minute=59,
    second=59,
    microsecond=999999
)

print(end_of_day)
```

তবে database filtering-এ অনেক সময় **half-open interval** ব্যবহার করা safer:

```text
[start_of_day, next_day_start)
```

অর্থাৎ:

```python
start = dt.replace(
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)

next_day = start + timedelta(days=1)
```

তারপর:

```text
start <= timestamp < next_day
```

এটা খুব useful production pattern।

---

# 2️⃣4️⃣ Today's Records

ধরো database/API থেকে records পেয়েছ:

```python
records = [
    {
        "name": "A",
        "created_at": datetime(2026, 8, 17, 10, 0)
    },
    {
        "name": "B",
        "created_at": datetime(2026, 8, 16, 15, 0)
    }
]
```

আজ:

```python
today = datetime(2026, 8, 17)

start = today.replace(
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)

end = start + timedelta(days=1)
```

Filter:

```python
today_records = [
    record
    for record in records
    if start <= record["created_at"] < end
]
```

---

# 2️⃣5️⃣ Start of Week

Python:

```python
from datetime import datetime, timedelta

today = datetime.now()

start_of_week = (
    today
    - timedelta(days=today.weekday())
)

start_of_week = start_of_week.replace(
    hour=0,
    minute=0,
    second=0,
    microsecond=0
)

print(start_of_week)
```

`weekday()`:

```text
Monday    → 0
Tuesday   → 1
Wednesday → 2
Thursday  → 3
Friday    → 4
Saturday  → 5
Sunday    → 6
```

---

# 2️⃣6️⃣ Date Range Generator

ধরো:

```python
from datetime import date, timedelta

start = date(2026, 8, 17)
end = date(2026, 8, 22)

current = start

while current <= end:
    print(current)

    current += timedelta(days=1)
```

Output:

```text
2026-08-17
2026-08-18
2026-08-19
2026-08-20
2026-08-21
2026-08-22
```

---

# 2️⃣7️⃣ Reusable Date Range Function

```python
def date_range(start, end):
    current = start

    while current <= end:
        yield current
        current += timedelta(days=1)
```

Use:

```python
for d in date_range(
    date(2026, 8, 17),
    date(2026, 8, 22)
):
    print(d)
```

এখানে `yield` ব্যবহার করেছি, তাই এটা generator।

---

# 2️⃣8️⃣ Business Days

Simple version:

```python
def is_weekday(d):
    return d.weekday() < 5
```

Use:

```python
if is_weekday(date.today()):
    print("Working day")
```

---

# 2️⃣9️⃣ Count Working Days

```python
def count_weekdays(start, end):
    count = 0
    current = start

    while current <= end:

        if current.weekday() < 5:
            count += 1

        current += timedelta(days=1)

    return count
```

Use:

```python
result = count_weekdays(
    date(2026, 8, 17),
    date(2026, 8, 31)
)

print(result)
```

⚠️ এটা শুধু Saturday/Sunday বাদ দেয়; country-specific holidays জানে না।

---

# 3️⃣0️⃣ Database Timestamp Pattern ⭐⭐⭐⭐⭐

Backend model-এ সাধারণ concept:

```text
created_at
updated_at
deleted_at
expires_at
```

Example:

```python
created_at = datetime.now(timezone.utc)
updated_at = datetime.now(timezone.utc)
```

সবসময় একই timezone strategy রাখা গুরুত্বপূর্ণ।

---

# 3️⃣1️⃣ `created_at` বনাম `updated_at`

```text
created_at
↓
Record প্রথম কখন তৈরি হয়েছে

updated_at
↓
Record সর্বশেষ কখন পরিবর্তিত হয়েছে
```

Example:

```python
record = {
    "created_at": datetime.now(timezone.utc),
    "updated_at": datetime.now(timezone.utc)
}
```

---

# 3️⃣2️⃣ Soft Delete

তুমি production backend-এ দেখবে:

```text
deleted_at = NULL
```

মানে active।

যদি:

```python
deleted_at = datetime.now(timezone.utc)
```

তাহলে deleted হিসেবে ধরা যায়।

Concept:

```text
deleted_at = None
        ↓
      Active

deleted_at != None
        ↓
      Deleted
```

---

# 3️⃣3️⃣ Expiry Utility

একটি reusable utility বানাও:

```python
from datetime import datetime, timezone, timedelta

def create_expiry(minutes):
    now = datetime.now(timezone.utc)

    return now + timedelta(
        minutes=minutes
    )
```

Use:

```python
expires_at = create_expiry(30)

print(expires_at)
```

---

# 3️⃣4️⃣ Check Expiry

```python
def is_expired(expires_at):
    now = datetime.now(timezone.utc)

    return now >= expires_at
```

Use:

```python
if is_expired(expires_at):
    print("Expired")
```

---

# 3️⃣5️⃣ Remaining Seconds

```python
def remaining_seconds(expires_at):
    now = datetime.now(timezone.utc)

    remaining = expires_at - now

    return max(
        0,
        int(remaining.total_seconds())
    )
```

Use:

```python
print(
    remaining_seconds(expires_at)
)
```

---

# 3️⃣6️⃣ Production Utility Module

তুমি চাইলে:

```text
project/
│
├── utils/
│   └── datetime_utils.py
│
└── app.py
```

`datetime_utils.py`:

```python
from datetime import datetime, timezone, timedelta


def utc_now():
    return datetime.now(timezone.utc)


def expires_after(minutes):
    return utc_now() + timedelta(
        minutes=minutes
    )


def is_expired(expires_at):
    return utc_now() >= expires_at
```

তারপর অন্য file:

```python
from utils.datetime_utils import (
    utc_now,
    expires_after,
    is_expired
)
```

এটা real project structure-এর জন্য ভালো pattern।

---

# 3️⃣7️⃣ Testing-এর জন্য একটা গুরুত্বপূর্ণ Pattern ⭐⭐⭐⭐⭐

Business logic-এর ভিতরে বারবার:

```python
datetime.now()
```

লিখলে test করা কঠিন হতে পারে।

Better architecture-এ current time dependency আলাদা রাখা যায়।

Simple example:

```python
def is_expired(expires_at, now):
    return now >= expires_at
```

তারপর:

```python
now = datetime.now(timezone.utc)

if is_expired(expires_at, now):
    print("Expired")
```

Test করার সময় fake `now` দেওয়া যায়।

এটা production software engineering-এ খুব useful concept।

---

# 3️⃣8️⃣ API → Database → Frontend Flow 🔥

একটি real application ধরো:

```text
Frontend
   │
   │ request
   ↓
Django REST API
   │
   ↓
Validate datetime
   │
   ↓
Convert/normalize
   │
   ↓
Database
   │
   ↓
UTC timestamp
   │
   ↓
API response
   │
   ↓
Frontend
   │
   ↓
User timezone
```

এখানে `datetime` শুধু একটা Python class না—পুরো system-এর অংশ।

---

# 3️⃣9️⃣ Production Rules ⭐⭐⭐⭐⭐

### Rule 1

Timezone-sensitive application-এ:

```python
datetime.now(timezone.utc)
```

ব্যবহার করো।

### Rule 2

Naive এবং aware datetime mix করো না।

### Rule 3

Timezone conversion-এর জন্য:

```python
astimezone()
```

ব্যবহার করো।

### Rule 4

API timestamp-এ timezone information রাখো।

Example:

```text
2026-08-17T08:30:00+00:00
```

### Rule 5

Month arithmetic-এ blindly:

```python
timedelta(days=30)
```

কে "1 month" ধরে নিও না।

---

# 🧪 Day 14 Practice

## Exercise 1 — Age Calculator

Function:

```python
calculate_age(birth_date)
```

---

## Exercise 2 — Expiry Checker

একটি OTP-এর expiry time:

```text
5 minutes
```

তৈরি করো।

তারপর check করো expired কিনা।

---

## Exercise 3 — API Timestamp

Current UTC time:

```python
datetime.now(timezone.utc)
```

কে ISO format-এ convert করো।

---

## Exercise 4 — Today's Records

একটি list থেকে শুধু আজকের records বের করো।

---

## Exercise 5 — Date Range

দুটি date-এর মাঝের সব date print করো।

---

## Exercise 6 ⭐

শুধু weekdays count করো।

---

## Exercise 7 ⭐⭐

একটি utility module তৈরি করো:

```text
datetime_utils.py
```

এর মধ্যে:

```python
utc_now()
expires_after()
is_expired()
remaining_seconds()
```

রাখো।

---

# 🏆 Day 14 Mini Project

## ⏰ Task & Reminder Manager

একটি application বানাও যেখানে task:

```python
{
    "title": "Learn Django",
    "created_at": ...,
    "deadline": ...,
    "priority": 1
}
```

থাকবে।

Program:

```text
====================================
       TASK & REMINDER MANAGER
====================================

1. Show all tasks
2. Show today's tasks
3. Show upcoming tasks
4. Show expired tasks
5. Show nearest deadline
6. Sort by deadline
7. Show remaining time
8. Add task
```

Example:

```text
Task: Learn Django

Created:
2026-08-17 08:00 UTC

Deadline:
2026-08-20 08:00 UTC

Remaining:
2 days 23 hours

Status:
UPCOMING
```

এখানে তুমি ব্যবহার করবে:

```text
datetime
date
time
timedelta
timezone
ZoneInfo
strftime
strptime
comparison
sorting
filtering
ISO format
```

---

# 📌 Day 14 Cheat Sheet

### Current UTC

```python
datetime.now(timezone.utc)
```

### Add duration

```python
dt + timedelta(days=1)
```

### Subtract duration

```python
dt - timedelta(hours=2)
```

### Difference

```python
end - start
```

### Seconds

```python
delta.total_seconds()
```

### ISO

```python
dt.isoformat()
```

### Parse ISO

```python
datetime.fromisoformat(text)
```

### Convert timezone

```python
dt.astimezone(
    ZoneInfo("Asia/Dhaka")
)
```

### Date part

```python
dt.date()
```

### Time part

```python
dt.time()
```

### Date + Time

```python
datetime.combine(d, t)
```

---

# 🧠 Day 14-এর সবচেয়ে গুরুত্বপূর্ণ Pattern

Production backend-এর জন্য এই patternটা মাথায় রাখো:

```python
from datetime import datetime, timezone, timedelta

created_at = datetime.now(timezone.utc)

expires_at = (
    created_at
    + timedelta(hours=24)
)

if datetime.now(timezone.utc) >= expires_at:
    print("Expired")
```

এবং API-এর জন্য:

```python
created_at.isoformat()
```

এগুলো তুমি **Django/DRF, authentication, JWT/session expiry, database records, logging, notification এবং scheduling system**-এ বারবার দেখতে পাবে।

---

# 🚀 Course Progress

```text
Day 1  → datetime Fundamentals       ✅
Day 2  → date Object                 ✅
Day 3  → time Object                 ✅
Day 4  → datetime Object             ✅
Day 5  → Current Date/Time + UTC     ✅
Day 6  → strftime()                  ✅
Day 7  → strptime()                  ✅
Day 8  → timedelta                   ✅
Day 9  → Date Calculations           ✅
Day 10 → Unix Timestamp              ✅
Day 11 → Timezone Basics              ✅
Day 12 → zoneinfo Deep Dive           ✅
Day 13 → Comparison + Sorting         ✅
Day 14 → Real-world Patterns          ✅ ← YOU ARE HERE
Day 15 → 🔥 Final Project
```

**Day 15 হবে `datetime` course-এর final project—একটা complete Date/Time Manager বানিয়ে Day 1–14-এর সব concept একসাথে ব্যবহার করব।**

# 🐍 Python `datetime` — Day 15

# 🔥 Final Project: Date & Time Manager

আজ আমাদের **`datetime` complete course-এর final day**। আজ Day 1–14-এর সবচেয়ে গুরুত্বপূর্ণ concept একসাথে ব্যবহার করে একটি ছোট কিন্তু বাস্তবধর্মী project বানাব।

Official documentation: [Python `datetime` documentation](https://docs.python.org/3/library/datetime.html?utm_source=chatgpt.com)

---

## 🎯 Final Project কী বানাব?

আমরা বানাব:

```text
========================================
        DATE & TIME MANAGER
========================================

1. Show current date/time
2. Add event
3. Show all events
4. Show upcoming events
5. Show today's events
6. Show expired events
7. Show next event
8. Search by date
9. Search by month
10. Sort events
11. Delete event
12. Exit
```

---

# 1️⃣ Project Structure

প্রথমে:

```text
datetime_manager/
│
├── main.py
├── datetime_utils.py
└── README.md
```

আজ প্রথমে সবকিছু `main.py`-তে করব। পরে চাইলে আলাদা module-এ ভাগ করা যাবে।

---

# 2️⃣ Import

```python
from datetime import datetime, date, timezone
```

---

# 3️⃣ Event Data Structure

আমাদের event হবে:

```python
{
    "id": 1,
    "title": "Python Exam",
    "date": date(2026, 8, 20),
    "time": "10:30",
    "description": "Python final exam"
}
```

Multiple events:

```python
events = [
    {
        "id": 1,
        "title": "Python Exam",
        "date": date(2026, 8, 20),
        "time": "10:30",
        "description": "Python final exam"
    },
    {
        "id": 2,
        "title": "Project Demo",
        "date": date(2026, 8, 18),
        "time": "15:00",
        "description": "Final project presentation"
    }
]
```

---

# 4️⃣ Current Date/Time

```python
def show_current_datetime():
    now = datetime.now()

    print("\nCurrent Date & Time:")
    print(now.strftime("%Y-%m-%d %H:%M:%S"))
```

---

# 5️⃣ Add Event

প্রথমে user থেকে title নেব:

```python
def add_event(events):

    title = input("Event title: ")
```

Date:

```python
date_text = input(
    "Date (YYYY-MM-DD): "
)

event_date = datetime.strptime(
    date_text,
    "%Y-%m-%d"
).date()
```

Time:

```python
event_time = input(
    "Time (HH:MM): "
)
```

Description:

```python
description = input(
    "Description: "
)
```

তারপর event:

```python
event = {
    "id": len(events) + 1,
    "title": title,
    "date": event_date,
    "time": event_time,
    "description": description
}
```

Add:

```python
events.append(event)
```

---

# 6️⃣ Complete `add_event()`

```python
def add_event(events):

    title = input("Event title: ")

    date_text = input(
        "Date (YYYY-MM-DD): "
    )

    try:
        event_date = datetime.strptime(
            date_text,
            "%Y-%m-%d"
        ).date()
    except ValueError:
        print("Invalid date format.")
        return

    event_time = input(
        "Time (HH:MM): "
    )

    description = input(
        "Description: "
    )

    event = {
        "id": len(events) + 1,
        "title": title,
        "date": event_date,
        "time": event_time,
        "description": description
    }

    events.append(event)

    print("Event added successfully!")
```

---

# 7️⃣ Show All Events

```python
def show_events(events):

    if not events:
        print("No events found.")
        return

    for event in events:

        print("\n--------------------")

        print("ID:", event["id"])
        print("Title:", event["title"])
        print("Date:", event["date"])
        print("Time:", event["time"])
        print(
            "Description:",
            event["description"]
        )
```

---

# 8️⃣ Sort Events

```python
def sort_events(events):

    events.sort(
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )
```

এখানে:

```python
key=lambda event: (
    event["date"],
    event["time"]
)
```

মানে:

```text
Date
 ↓
Time
```

অনুযায়ী sort।

---

# 9️⃣ Upcoming Events

```python
def show_upcoming(events):

    today = date.today()

    upcoming = [
        event
        for event in events
        if event["date"] >= today
    ]

    upcoming.sort(
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )

    show_events(upcoming)
```

---

# 🔟 Today's Events

```python
def show_today(events):

    today = date.today()

    today_events = [
        event
        for event in events
        if event["date"] == today
    ]

    show_events(today_events)
```

---

# 1️⃣1️⃣ Expired Events

```python
def show_expired(events):

    today = date.today()

    expired = [
        event
        for event in events
        if event["date"] < today
    ]

    show_events(expired)
```

---

# 1️⃣2️⃣ Next Event ⭐⭐⭐

```python
def show_next_event(events):

    today = date.today()

    upcoming = [
        event
        for event in events
        if event["date"] >= today
    ]

    if not upcoming:
        print("No upcoming events.")
        return

    next_event = min(
        upcoming,
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )

    print("\nNext Event")
    print("--------------------")
    print("Title:", next_event["title"])
    print("Date:", next_event["date"])
    print("Time:", next_event["time"])
```

---

# 1️⃣3️⃣ Search by Date

User date input:

```python
def search_by_date(events):

    text = input(
        "Enter date (YYYY-MM-DD): "
    )

    try:
        search_date = datetime.strptime(
            text,
            "%Y-%m-%d"
        ).date()
    except ValueError:
        print("Invalid date.")
        return
```

Filter:

```python
    results = [
        event
        for event in events
        if event["date"] == search_date
    ]

    show_events(results)
```

---

# 1️⃣4️⃣ Search by Month

```python
def search_by_month(events):

    year = int(input("Year: "))
    month = int(input("Month: "))

    results = [
        event
        for event in events
        if event["date"].year == year
        and event["date"].month == month
    ]

    show_events(results)
```

---

# 1️⃣5️⃣ Delete Event

```python
def delete_event(events):

    try:
        event_id = int(
            input("Enter event ID: ")
        )
    except ValueError:
        print("Invalid ID.")
        return
```

Find:

```python
    for event in events:

        if event["id"] == event_id:

            events.remove(event)

            print("Event deleted.")
            return

    print("Event not found.")
```

---

# 1️⃣6️⃣ Main Menu

এখন menu:

```python
def menu():

    print("""
========================================
        DATE & TIME MANAGER
========================================

1. Show current date/time
2. Add event
3. Show all events
4. Show upcoming events
5. Show today's events
6. Show expired events
7. Show next event
8. Search by date
9. Search by month
10. Sort events
11. Delete event
12. Exit

========================================
""")
```

---

# 1️⃣7️⃣ Main Program

```python
def main():

    events = []

    while True:

        menu()

        choice = input(
            "Enter choice: "
        )

        if choice == "1":
            show_current_datetime()

        elif choice == "2":
            add_event(events)

        elif choice == "3":
            show_events(events)

        elif choice == "4":
            show_upcoming(events)

        elif choice == "5":
            show_today(events)

        elif choice == "6":
            show_expired(events)

        elif choice == "7":
            show_next_event(events)

        elif choice == "8":
            search_by_date(events)

        elif choice == "9":
            search_by_month(events)

        elif choice == "10":
            sort_events(events)
            print("Events sorted.")

        elif choice == "11":
            delete_event(events)

        elif choice == "12":
            print("Goodbye!")
            break

        else:
            print("Invalid choice.")
```

শেষে:

```python
if __name__ == "__main__":
    main()
```

---

# 1️⃣8️⃣ Complete Code

এখন সবকিছু একসাথে:

```python
from datetime import datetime, date


def show_current_datetime():

    now = datetime.now()

    print("\nCurrent Date & Time:")
    print(
        now.strftime(
            "%Y-%m-%d %H:%M:%S"
        )
    )


def add_event(events):

    title = input("Event title: ")

    date_text = input(
        "Date (YYYY-MM-DD): "
    )

    try:
        event_date = datetime.strptime(
            date_text,
            "%Y-%m-%d"
        ).date()

    except ValueError:
        print("Invalid date format.")
        return

    event_time = input(
        "Time (HH:MM): "
    )

    description = input(
        "Description: "
    )

    event = {
        "id": len(events) + 1,
        "title": title,
        "date": event_date,
        "time": event_time,
        "description": description
    }

    events.append(event)

    print("Event added successfully!")


def show_events(events):

    if not events:
        print("No events found.")
        return

    for event in events:

        print("\n--------------------")

        print("ID:", event["id"])
        print("Title:", event["title"])
        print("Date:", event["date"])
        print("Time:", event["time"])
        print(
            "Description:",
            event["description"]
        )


def sort_events(events):

    events.sort(
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )


def show_upcoming(events):

    today = date.today()

    upcoming = [
        event
        for event in events
        if event["date"] >= today
    ]

    upcoming.sort(
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )

    show_events(upcoming)


def show_today(events):

    today = date.today()

    today_events = [
        event
        for event in events
        if event["date"] == today
    ]

    show_events(today_events)


def show_expired(events):

    today = date.today()

    expired = [
        event
        for event in events
        if event["date"] < today
    ]

    show_events(expired)


def show_next_event(events):

    today = date.today()

    upcoming = [
        event
        for event in events
        if event["date"] >= today
    ]

    if not upcoming:
        print("No upcoming events.")
        return

    next_event = min(
        upcoming,
        key=lambda event: (
            event["date"],
            event["time"]
        )
    )

    print("\nNext Event")
    print("--------------------")
    print("Title:", next_event["title"])
    print("Date:", next_event["date"])
    print("Time:", next_event["time"])


def search_by_date(events):

    text = input(
        "Enter date (YYYY-MM-DD): "
    )

    try:
        search_date = datetime.strptime(
            text,
            "%Y-%m-%d"
        ).date()

    except ValueError:
        print("Invalid date.")
        return

    results = [
        event
        for event in events
        if event["date"] == search_date
    ]

    show_events(results)


def search_by_month(events):

    try:
        year = int(input("Year: "))
        month = int(input("Month: "))

    except ValueError:
        print("Invalid input.")
        return

    results = [
        event
        for event in events
        if event["date"].year == year
        and event["date"].month == month
    ]

    show_events(results)


def delete_event(events):

    try:
        event_id = int(
            input("Enter event ID: ")
        )

    except ValueError:
        print("Invalid ID.")
        return

    for event in events:

        if event["id"] == event_id:

            events.remove(event)

            print("Event deleted.")
            return

    print("Event not found.")


def menu():

    print("""
========================================
        DATE & TIME MANAGER
========================================

1. Show current date/time
2. Add event
3. Show all events
4. Show upcoming events
5. Show today's events
6. Show expired events
7. Show next event
8. Search by date
9. Search by month
10. Sort events
11. Delete event
12. Exit

========================================
""")


def main():

    events = []

    while True:

        menu()

        choice = input(
            "Enter choice: "
        )

        if choice == "1":
            show_current_datetime()

        elif choice == "2":
            add_event(events)

        elif choice == "3":
            show_events(events)

        elif choice == "4":
            show_upcoming(events)

        elif choice == "5":
            show_today(events)

        elif choice == "6":
            show_expired(events)

        elif choice == "7":
            show_next_event(events)

        elif choice == "8":
            search_by_date(events)

        elif choice == "9":
            search_by_month(events)

        elif choice == "10":
            sort_events(events)
            print("Events sorted.")

        elif choice == "11":
            delete_event(events)

        elif choice == "12":
            print("Goodbye!")
            break

        else:
            print("Invalid choice.")


if __name__ == "__main__":
    main()
```

---

# 🧠 এখন বুঝি আমরা কী কী ব্যবহার করলাম

এই project-এর ভিতরে:

|Concept|কোথায় ব্যবহার করেছি|
|---|---|
|`date`|Event date|
|`datetime`|Current time|
|`strptime()`|User input parse|
|`strftime()`|Date display|
|`.date()`|datetime → date|
|`date.today()`|Today's events|
|`<` `>=` `==`|Date comparison|
|`sort()`|Event sorting|
|`sorted()` concept|Sorting|
|`min()`|Next event|
|`lambda`|Sort key|
|List comprehension|Filtering|
|`.year`|Month search|
|`.month`|Month search|
|`try/except`|Invalid date|
|Functions|Reusable logic|

---

# 🔥 Final Challenge — তুমি নিজে করবে

উপরের code copy করে শুধু run করলেই হবে না।

নিজে নিচের features add করার চেষ্টা করো:

### Challenge 1

Event-এর **days remaining** দেখাও।

```text
Python Exam
2026-08-20
3 days remaining
```

Hint:

```python
(event["date"] - date.today()).days
```

---

### Challenge 2

Priority যোগ করো:

```python
{
    "priority": 1
}
```

তারপর:

```text
1 = High
2 = Medium
3 = Low
```

---

### Challenge 3

Date range search:

```text
Start date:
End date:
```

তারপর:

```python
start <= event["date"] <= end
```

---

### Challenge 4 🔥

`time`-কে string হিসেবে না রেখে `datetime.time` হিসেবে store করো।

এখন sorting হবে:

```python
key=lambda event: (
    event["date"],
    event["time"]
)
```

---

### Challenge 5 🔥🔥

সব event JSON file-এ save করো।

তখন তোমার project হবে:

```text
datetime_manager/
│
├── main.py
├── datetime_utils.py
├── events.json
└── README.md
```

এখানে তুমি **`datetime + json + pathlib`**—তিনটা standard library module একসাথে ব্যবহার করবে। এটা তোমার আগের শেখা modules-গুলোর সঙ্গে খুব ভালো integration practice।

---

# 🏆 `datetime` Course Complete

```text
Day 01  Fundamentals                  ✅
Day 02  date                          ✅
Day 03  time                          ✅
Day 04  datetime                      ✅
Day 05  Current time / UTC            ✅
Day 06  strftime                      ✅
Day 07  strptime                      ✅
Day 08  timedelta                     ✅
Day 09  Date calculations             ✅
Day 10  Unix timestamp                ✅
Day 11  Timezone                      ✅
Day 12  zoneinfo                      ✅
Day 13  Comparison / sorting          ✅
Day 14  Real-world patterns           ✅
Day 15  Final Project                 ✅
```

## 🎓 তোমার শেখা মূল skill

```text
datetime
   │
   ├── date
   ├── time
   ├── timedelta
   ├── timezone
   ├── zoneinfo
   ├── formatting
   ├── parsing
   ├── comparison
   ├── sorting
   ├── filtering
   ├── timestamps
   ├── expiry
   ├── scheduling
   └── API / backend timestamps
```

**এখন `datetime`-এর syntax মুখস্থ করার চেয়ে এই ১৫ দিনের concepts দিয়ে ২–৩টা ছোট project বানানো বেশি valuable।** এরপর তোমার Python standard-library সিরিজে পরের module শুরু করলে একইভাবে **Day 1 → Day 15 + final project** pattern অনুসরণ করতে পারবে।



