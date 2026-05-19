

# ✅ **Python Dictionary (A to Z) – With Examples**

---

## **A — Accessing values**

You access a value using its **key**.

```python
student = {"name": "Rahim", "age": 16}
print(student["name"])
```

**Output:** `Rahim`

---

## **C — Clear()**

Removes _all_ items.

```python
d = {"a": 1, "b": 2}
d.clear()
print(d)
```

**Output:** `{}`

---

## **C — Copy()**

Creates a shallow copy.

```python
d1 = {"x": 10}
d2 = d1.copy()
```

---

## **D — Delete (del keyword)**

Remove a specific key.

```python
d = {"a": 1, "b": 2}
del d["a"]
```

---

## **E — Empty dictionary**

```python
d = {}
```

---

## **F — Fromkeys()**

Creates a dictionary from a list of keys.

```python
keys = ["a", "b", "c"]
d = dict.fromkeys(keys, 0)
print(d)
```

**Output:** `{'a': 0, 'b': 0, 'c': 0}`

---

## **G — Get()**

Safer way to access a key (no error if key missing).

```python
d = {"name": "Akash"}
print(d.get("age", "Not Found"))
```

---

## **I — Items()**

Returns key–value pairs.

```python
d = {"a": 1, "b": 2}
print(d.items())
```

---

## **K — Keys()**

Returns all keys.

```python
d = {"a": 1, "b": 2}
print(d.keys())
```

---

## **L — Length (len())**

Number of items.

```python
len({"a": 1, "b": 2})   # 2
```

---

## **M — Merge dictionaries**

Python 3.9+:

```python
d1 = {"a": 1}
d2 = {"b": 2}
d3 = d1 | d2
```

---

## **P — Pop()**

Remove an item by key and return value.

```python
d = {"a": 1, "b": 2}
value = d.pop("a")
```

---

## **P — Popitem()**

Removes the last inserted item.

```python
d = {"x": 10, "y": 20}
d.popitem()
```

---

## **S — Setdefault()**

If key exists → returns value  
If not → insert key with default value.

```python
d = {"name": "Ali"}
d.setdefault("age", 15)
```

---

## **U — Update()**

Update dictionary with another dictionary.

```python
d1 = {"a": 1}
d1.update({"b": 2})
```

---

## **V — Values()**

Returns all values.

```python
d = {"a": 10, "b": 20}
print(d.values())
```

---

## **Z — Zip to dict**

Make a dict from two lists.

```python
keys = ["name", "age"]
vals = ["Rafi", 16]

d = dict(zip(keys, vals))
print(d)
```

---

# 🎁 **Bonus: Full Practical Example**

```python
student = {
    "name": "Arman",
    "class": 9,
    "marks": {"math": 80, "science": 75}
}

# Access
print(student["name"])

# Add new item
student["roll"] = 23

# Update
student.update({"class": 10})

# Loop
for key, value in student.items():
    print(key, ":", value)
```

---

# **Python Dictionary Practice Problems (50)**

---

## **Beginner (1–15)**

1. Create a dictionary for a student with keys: `"name"`, `"age"`, `"class"`.
    
2. Print all keys of the dictionary.
    
3. Print all values of the dictionary.
    
4. Print the value of `"name"` using `get()`.
    
5. Add a new key `"roll"` with a value.
    
6. Update the `"class"` value to a new number.
    
7. Delete the `"age"` key.
    
8. Clear all items in the dictionary.
    
9. Copy a dictionary into a new one.
    
10. Use `fromkeys()` to create a dictionary with keys `"a"`, `"b"`, `"c"` and default value `0`.
    
11. Check if `"name"` exists in the dictionary.
    
12. Print the length of a dictionary.
    
13. Merge two dictionaries: `{"a": 1}` and `{"b": 2}`.
    
14. Loop through dictionary and print key–value pairs.
    
15. Use `setdefault()` to add a key `"score"` with default `50`.
    

---

## **Intermediate (16–35)**

16. Create a dictionary where keys are numbers `1–5` and values are squares of keys.
    
17. Convert two lists into a dictionary using `zip()` (`["a", "b"]` & `[1, 2]`).
    
18. Remove a key using `pop()` and print removed value.
    
19. Remove the last inserted item using `popitem()`.
    
20. Count frequency of each character in a string using a dictionary.
    
21. Count frequency of words in a sentence using a dictionary.
    
22. Sort a dictionary by keys.
    
23. Sort a dictionary by values.
    
24. Reverse lookup: find key(s) for a given value.
    
25. Create a nested dictionary for 2 students with their marks.
    
26. Access a nested value (e.g., math marks of student 1).
    
27. Update a nested value.
    
28. Merge two dictionaries using `update()`.
    
29. Print all keys in sorted order.
    
30. Print all values in descending order.
    
31. Use a dictionary to store employee details: name, salary, department.
    
32. Find the sum of all numeric values in a dictionary.
    
33. Find the maximum and minimum value in a dictionary.
    
34. Convert dictionary keys to a list.
    
35. Convert dictionary values to a list.
    

---

## **Advanced (36–50)**

36. Remove dictionary items with value less than 10.
    
37. Count how many values are even numbers.
    
38. Invert a dictionary: values become keys, keys become values.
    
39. Merge multiple dictionaries in a loop.
    
40. Create a dictionary from user input (3 key–value pairs).
    
41. Create a dictionary that stores lists as values.
    
42. Flatten a nested dictionary into a single dictionary.
    
43. Group items from a list by frequency using a dictionary.
    
44. Implement a simple phone book using dictionary.
    
45. Check if two dictionaries are equal.
    
46. Filter dictionary to keep only keys starting with `"a"`.
    
47. Combine two dictionaries and sum values of common keys.
    
48. Create a dictionary that counts vowels in a string.
    
49. Create a dictionary that counts consonants in a string.
    
50. Create a dictionary from a list where keys are elements and values are lengths of strings.
    

---

💡 **Tips for Practice:**

- Try solving using **loops**, **dict methods**, and **comprehensions**.
    
- Use **nested dictionaries** to handle more complex data.
    
- Start small (Beginner) → then move Intermediate → then Advanced.
    

---


---

# **Python Dictionary Solutions – All 50 Problems**

---

## **Beginner (1–15)**

```python
# 1. Create a dictionary for a student
student = {"name": "Rahim", "age": 16, "class": 10}

# 2. Print all keys
print(student.keys())

# 3. Print all values
print(student.values())

# 4. Print value of "name" using get()
print(student.get("name"))

# 5. Add a new key "roll"
student["roll"] = 23
print(student)

# 6. Update the "class"
student["class"] = 11
print(student)

# 7. Delete the "age" key
del student["age"]
print(student)

# 8. Clear all items
student.clear()
print(student)

# 9. Copy a dictionary
student = {"name": "Rahim", "age": 16}
student_copy = student.copy()
print(student_copy)

# 10. Fromkeys()
keys = ["a", "b", "c"]
d = dict.fromkeys(keys, 0)
print(d)

# 11. Check if "name" exists
print("name" in student)

# 12. Print length
print(len(student))

# 13. Merge two dictionaries (Python 3.9+)
d1 = {"a": 1}
d2 = {"b": 2}
d3 = d1 | d2
print(d3)

# 14. Loop through dictionary
for key, value in student.items():
    print(key, value)

# 15. Setdefault()
student.setdefault("score", 50)
print(student)
```

---

## **Intermediate (16–35)**

```python
# 16. Dictionary with squares
squares = {i: i**2 for i in range(1, 6)}
print(squares)

# 17. Two lists into a dictionary
keys = ["a", "b"]
vals = [1, 2]
d = dict(zip(keys, vals))
print(d)

# 18. Remove key using pop()
value = d.pop("a")
print(value, d)

# 19. Remove last item
d.popitem()
print(d)

# 20. Character frequency in string
text = "hello"
freq = {}
for c in text:
    freq[c] = freq.get(c, 0) + 1
print(freq)

# 21. Word frequency
sentence = "I love Python and I love coding"
words = sentence.split()
word_count = {}
for w in words:
    word_count[w] = word_count.get(w, 0) + 1
print(word_count)

# 22. Sort by keys
unsorted = {"b": 2, "a": 1}
sorted_by_key = dict(sorted(unsorted.items()))
print(sorted_by_key)

# 23. Sort by values
sorted_by_value = dict(sorted(unsorted.items(), key=lambda x: x[1]))
print(sorted_by_value)

# 24. Reverse lookup (find keys for value 1)
d = {"a": 1, "b": 2, "c": 1}
keys_for_1 = [k for k, v in d.items() if v == 1]
print(keys_for_1)

# 25. Nested dictionary
students = {
    "student1": {"math": 80, "science": 75},
    "student2": {"math": 85, "science": 90}
}

# 26. Access nested value
print(students["student1"]["math"])

# 27. Update nested value
students["student2"]["science"] = 95
print(students)

# 28. Merge dictionaries
d1 = {"a": 1}
d2 = {"b": 2}
d1.update(d2)
print(d1)

# 29. Print sorted keys
print(sorted(students.keys()))

# 30. Print values descending
vals = [v["math"] for v in students.values()]
print(sorted(vals, reverse=True))

# 31. Employee dictionary
employee = {"name": "Ali", "salary": 20000, "department": "IT"}
print(employee)

# 32. Sum of numeric values
nums = {"a": 5, "b": 10, "c": 15}
total = sum(nums.values())
print(total)

# 33. Max and min values
print(max(nums.values()), min(nums.values()))

# 34. Dictionary keys to list
keys_list = list(nums.keys())
print(keys_list)

# 35. Dictionary values to list
values_list = list(nums.values())
print(values_list)
```

---

## **Advanced (36–50)**

```python
# 36. Remove items with value < 10
d = {"a": 5, "b": 15, "c": 8}
d = {k: v for k, v in d.items() if v >= 10}
print(d)

# 37. Count even numbers
nums = {"a": 2, "b": 3, "c": 4}
count_even = sum(1 for v in nums.values() if v % 2 == 0)
print(count_even)

# 38. Invert dictionary
d = {"a": 1, "b": 2}
inv = {v: k for k, v in d.items()}
print(inv)

# 39. Merge multiple dictionaries
dicts = [{"a": 1}, {"b": 2}, {"c": 3}]
merged = {}
for d in dicts:
    merged.update(d)
print(merged)

# 40. Dictionary from user input
# (Example values)
user_dict = {}
for i in range(3):
    key = input("Enter key: ")
    value = input("Enter value: ")
    user_dict[key] = value
print(user_dict)

# 41. Dictionary with lists as values
d = {"a": [1,2], "b": [3,4]}
print(d)

# 42. Flatten nested dictionary
nested = {"x": {"y": 1, "z": 2}}
flat = {}
for k1, v1 in nested.items():
    for k2, v2 in v1.items():
        flat[k2] = v2
print(flat)

# 43. Group items by frequency
items = ["apple","banana","apple","orange"]
freq = {}
for item in items:
    freq[item] = freq.get(item,0)+1
print(freq)

# 44. Simple phone book
phone_book = {"Ali": "0170000000", "Rahim": "0180000000"}
print(phone_book["Ali"])

# 45. Check equality
d1 = {"a": 1}
d2 = {"a": 1}
print(d1 == d2)

# 46. Filter keys starting with 'a'
d = {"apple": 5, "banana": 10, "avocado": 15}
filtered = {k:v for k,v in d.items() if k.startswith("a")}
print(filtered)

# 47. Combine dictionaries, sum common keys
d1 = {"a": 2, "b": 3}
d2 = {"a": 4, "c": 5}
combined = {}
for k in set(d1)|set(d2):
    combined[k] = d1.get(k,0) + d2.get(k,0)
print(combined)

# 48. Count vowels in string
text = "hello world"
vowels = "aeiou"
v_count = {v: text.count(v) for v in vowels if v in text}
print(v_count)

# 49. Count consonants
cons_count = {}
for c in text:
    if c.isalpha() and c not in vowels:
        cons_count[c] = cons_count.get(c,0)+1
print(cons_count)

# 50. Dictionary from list with lengths
words = ["apple", "hi", "python"]
d = {w: len(w) for w in words}
print(d)
```

---

💡 **Tips:**

- Copy each block and run it.
    
- Try modifying values and experimenting.
    
- For nested dicts, practice looping and flattening.
    

---


