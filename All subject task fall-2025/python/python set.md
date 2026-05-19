
# 🔷 1. Set কী?

- **Unordered** (index দিয়ে access করা যায় না)
    
- **Unique elements only** (duplicate remove automatically)
    
- **Mutable** (add/remove করা যায়)
    

```python
s = {1, 2, 3, 3}
print(s)  # {1, 2, 3}
```

---

# 🔷 2. Set Create করার সব উপায়

```python
s1 = {1, 2, 3}           # normal
s2 = set([1, 2, 3, 3])   # from list
s3 = set("hello")         # from string
```

---

# 🔷 3. Access / Looping

```python
s = {1,2,3}
for x in s:
    print(x)
```

❌ `s[0]` → index access not allowed

---

# 🔷 4. Add / Remove element

```python
s.add(4)
s.remove(2)   # error if not exist
s.discard(5)  # no error if not exist
```

---

# 🔷 5. Set Operations (VERY IMPORTANT)

```python
a = {1,2,3}
b = {2,3,4}

# Union
print(a | b)  # {1,2,3,4}

# Intersection
print(a & b)  # {2,3}

# Difference
print(a - b)  # {1}

# Symmetric difference
print(a ^ b)  # {1,4}
```

---

# 🔷 6. Membership test

```python
2 in a  # True
5 in a  # False
```

---

# 🔷 7. Set methods

|Method|Description|
|---|---|
|add()|Add element|
|remove()|Remove element (error if missing)|
|discard()|Remove element (no error)|
|pop()|Remove arbitrary element|
|clear()|Empty set|
|copy()|Shallow copy|
|update()|Add multiple elements|

---

# 🔷 8. Set vs List

|Feature|Set|List|
|---|---|---|
|Mutable|✅|✅|
|Unique|✅|❌|
|Ordered|❌|✅|
|Index access|❌|✅|
|Speed|Fast|Slower|

---

# 🔷 9. Real Use Cases

1. **Remove duplicates from list**
    

```python
arr = [1,2,2,3]
arr = list(set(arr))
```

2. **Find common elements**
    

```python
a = {1,2,3}
b = {2,3,4}
a & b  # {2,3}
```

3. **Membership check fast**
    

```python
if x in set_var:
    print("exists")
```

4. **Data pipelines / ML features**
    

- Unique category detection
    
- Fast lookup
    

---

# 🔷 10. Advanced Tricks

### Nested set not allowed

```python
s = {1,2,{3,4}}  # ❌ Error
```

### Frozen set (immutable)

```python
fs = frozenset([1,2,3])
# cannot add/remove
```

---

# 🔥 Practice Problems for You

1. Remove duplicates from list
    
2. Find common elements of 3 sets
    
3. Check if set is subset / superset
    
4. Symmetric difference between two sets
    
5. Count unique words in a sentence
---

# 🟢 SECTION 1: Basic Set Operations (1–5)

---

## ✅ 1. Remove duplicates from list

```python
arr = [1,2,2,3,4,4]
unique = list(set(arr))
print(unique)  # [1,2,3,4]
```

**Explanation:** set automatically removes duplicates.

---

## ✅ 2. Check membership

```python
s = {1,2,3}
print(2 in s)   # True
print(5 in s)   # False
```

**Explanation:** set lookup is O(1) → fast.

---

## ✅ 3. Add / Remove elements

```python
s = {1,2}
s.add(3)
s.remove(1)
s.discard(5)   # no error
print(s)  # {2,3}
```

**Explanation:** add(), remove(), discard() usage.

---

## ✅ 4. Union / Intersection / Difference

```python
a = {1,2,3}
b = {2,3,4}

print(a | b)  # Union {1,2,3,4}
print(a & b)  # Intersection {2,3}
print(a - b)  # Difference {1}
print(a ^ b)  # Symmetric diff {1,4}
```

---

## ✅ 5. Clear / Copy

```python
s = {1,2,3}
t = s.copy()
s.clear()
print(s)  # set()
print(t)  # {1,2,3}
```

---

# 🟡 SECTION 2: Intermediate (6–10)

---

## ✅ 6. Find max / min element

```python
s = {5,3,9,1}
print(max(s))  # 9
print(min(s))  # 1
```

---

## ✅ 7. Subset / Superset

```python
a = {1,2}
b = {1,2,3}
print(a.issubset(b))   # True
print(b.issuperset(a)) # True
```

---

## ✅ 8. Intersection of 3 sets

```python
a = {1,2,3}
b = {2,3,4}
c = {3,4,5}
print(a & b & c)  # {3}
```

---

## ✅ 9. Symmetric difference

```python
a = {1,2,3}
b = {3,4}
print(a ^ b)  # {1,2,4}
```

---

## ✅ 10. Remove duplicates from a string

```python
s = "hello"
unique = set(s)
print(unique)  # {'e','h','l','o'}
```

---

# 🔴 SECTION 3: Advanced / Interview Level (11–15)

---

## ✅ 11. Count unique words in sentence

```python
sentence = "hello world hello"
words = sentence.split()
print(len(set(words)))  # 2
```

---

## ✅ 12. Find common elements in 2 lists

```python
a = [1,2,3]
b = [2,3,4]
print(set(a) & set(b))  # {2,3}
```

---

## ✅ 13. Find elements in list1 not in list2

```python
a = [1,2,3]
b = [2,3,4]
print(set(a) - set(b))  # {1}
```

---

## ✅ 14. Find all pairs with sum in set

```python
arr = [1,2,3,4,5]
target = 5
s = set(arr)
pairs = {(x, target-x) for x in s if target-x in s and x<target-x}
print(pairs)  # {(1,4),(2,3)}
```

**Explanation:** Using set for O(1) lookup and uniqueness.

---

## ✅ 15. Remove duplicates while maintaining order

```python
arr = [1,2,2,3,4,4]
seen = set()
res = []
for x in arr:
    if x not in seen:
        res.append(x)
        seen.add(x)
print(res)  # [1,2,3,4]
```

**Explanation:** normal set loses order, this keeps order.

---

# 🟣 BONUS: Advanced Tricks (16–20)

---

## ✅ 16. Check if two lists have no common element

```python
a = [1,2]
b = [3,4]
print(set(a).isdisjoint(set(b)))  # True
```

---

## ✅ 17. Count unique characters in string

```python
s = "interview"
print(len(set(s)))  # 7
```

---

## ✅ 18. Convert list of tuples to set of tuples

```python
lst = [(1,2),(2,3),(1,2)]
print(set(lst))  # {(1,2),(2,3)}
```

---

## ✅ 19. Remove duplicates from list of dicts

```python
lst = [{"a":1},{"a":2},{"a":1}]
unique = [dict(t) for t in {tuple(d.items()) for d in lst}]
print(unique)  # [{'a':1},{'a':2}]
```

---

## ✅ 20. Find elements appearing in exactly 2 out of 3 sets

```python
a={1,2,3}
b={2,3,4}
c={3,4,5}
res = (a&b) | (a&c) | (b&c) - (a&b&c)
print(res)  # {2,4}
```

---

💡 **Pro Tip:**

* Set interview questions mostly test **unique, fast lookup, set operations, and real-life logic**
* Always think: **“Can I do this with a set instead of list for performance?”**

---

