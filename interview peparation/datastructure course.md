
# Complete Data Structure Tutorial (Interview Preparation)

## Course `Roadmap`

### Module 1: Introduction to Data Structure

* What is Data Structure?
* Why do we need Data Structures?
* Types of Data Structures
* Time Complexity
* Space Complexity
* Big O Notation

---

## Module 2: Arrays

Topics

* Array Basics
* Static vs Dynamic Array
* Insert
* Delete
* Update
* Traversal
* Searching
* Rotation
* Prefix Sum

Interview Problems

* Two Sum
* Best Time to Buy Stock
* Move Zeroes
* Remove Duplicates
* Rotate Array
* Product Except Self

Python Example

```python
arr = [10,20,30]

arr.append(40)

arr.insert(1,15)

arr.remove(20)

print(arr)
```

Time Complexity

| Operation     | Complexity |
| ------------- | ---------- |
| Access        | O(1)       |
| Search        | O(n)       |
| Insert End    | O(1)       |
| Insert Middle | O(n)       |
| Delete        | O(n)       |

---

# Module 3: Strings

Topics

* Immutable String
* String Operations
* Reverse String
* Palindrome
* Anagram
* Frequency Count

Interview Questions

* Valid Anagram
* Longest Common Prefix
* Reverse Words
* Longest Substring Without Repeating Characters

---

# Module 4: Linked List

Topics

* Singly Linked List
* Doubly Linked List
* Circular Linked List

Operations

* Insert
* Delete
* Search
* Reverse
* Merge

Visualization

```
10 -> 20 -> 30 -> 40 -> None
```

Python

```python
class Node:

    def __init__(self,data):
        self.data=data
        self.next=None
```

Interview Questions

* Reverse Linked List
* Detect Cycle
* Merge Two Lists
* Remove Nth Node
* Middle Node

Complexity

| Operation    | Complexity |
| ------------ | ---------- |
| Insert Front | O(1)       |
| Insert End   | O(n)       |
| Delete       | O(n)       |
| Search       | O(n)       |

---

# Module 5: Stack

Concept

LIFO

```
Top

30

20

10
```

Operations

* Push
* Pop
* Peek

Python

```python
stack=[]

stack.append(10)
stack.append(20)

stack.pop()
```

Interview Problems

* Valid Parentheses
* Min Stack
* Next Greater Element
* Daily Temperatures

Complexity

O(1)

---

# Module 6: Queue

FIFO

```
Front

10 20 30

Rear
```

Types

* Queue
* Circular Queue
* Deque
* Priority Queue

Python

```python
from collections import deque

q=deque()

q.append(10)
q.append(20)

q.popleft()
```

Interview Questions

* Implement Queue
* Sliding Window Maximum

---

# Module 7: Hash Table

Topics

* Hash Function
* Collision
* Dictionary
* Hash Set

Python

```python
student = {
    "name":"Atiar",
    "cg":3.5
}
```

Interview Questions

* Two Sum
* Group Anagrams
* Top K Frequent Elements
* Happy Number

Complexity

Average

```
Insert O(1)

Delete O(1)

Search O(1)
```

---

# Module 8: Recursion

Topics

* Base Case
* Recursive Case
* Call Stack

Example

```python
def fact(n):

    if n==1:
        return 1

    return n*fact(n-1)
```

Interview Questions

* Fibonacci
* Factorial
* Tower of Hanoi

---

# Module 9: Binary Search

Requirements

Sorted Array

Python

```python
def binary(arr,target):

    left=0
    right=len(arr)-1

    while left<=right:

        mid=(left+right)//2

        if arr[mid]==target:
            return mid

        elif arr[mid]<target:
            left=mid+1

        else:
            right=mid-1
```

Interview Questions

* Search Insert Position
* First Bad Version
* Peak Element

Complexity

```
O(log n)
```

---

# Module 10: Trees

Topics

* Binary Tree
* Binary Search Tree
* AVL Tree
* Segment Tree

Traversal

* Preorder
* Inorder
* Postorder
* Level Order

Visualization

```
        10
       /  \
      5   15
     / \
    2   7
```

Interview Questions

* Maximum Depth
* Same Tree
* Balanced Tree
* Diameter
* Lowest Common Ancestor

---

# Module 11: Heap

Types

* Min Heap
* Max Heap

Python

```python
import heapq

heap=[]

heapq.heappush(heap,5)
heapq.heappush(heap,2)

heapq.heappop(heap)
```

Interview Questions

* Kth Largest
* Merge K Lists
* Top K Elements

Complexity

Insert

```
O(log n)
```

---

# Module 12: Graph

Representation

* Adjacency List
* Adjacency Matrix

Traversal

* BFS
* DFS

Visualization

```
A

/ \

B  C

\ /

 D
```

Interview Questions

* Number of Islands
* Clone Graph
* Course Schedule
* Shortest Path

Algorithms

* BFS
* DFS
* Dijkstra
* Bellman Ford
* Floyd Warshall

---

# Module 13: Trie

Purpose

Fast String Search

Applications

* Dictionary
* Auto Complete
* Spell Checker

Interview

* Implement Trie
* Word Search

---

# Module 14: Union Find (Disjoint Set)

Operations

* Find
* Union

Applications

* Connected Components
* Kruskal Algorithm

Interview

* Number of Provinces
* Redundant Connection

---

# Module 15: Backtracking

Topics

* Decision Tree
* Recursion

Problems

* Sudoku
* N Queens
* Combination Sum
* Permutations

---

# Module 16: Greedy Algorithm

Problems

* Activity Selection
* Jump Game
* Gas Station
* Merge Intervals

---

# Module 17: Dynamic Programming

Topics

* Memoization
* Tabulation

Classic Problems

* Climbing Stairs
* House Robber
* Coin Change
* Longest Increasing Subsequence
* Knapsack
* Longest Common Subsequence

---

# Module 18: Advanced Data Structures

* Fenwick Tree
* Segment Tree
* Sparse Table
* Red Black Tree
* B Tree
* Skip List
* Suffix Array
* Suffix Tree

---

# Big-O Cheat Sheet

| Data Structure | Access   | Search   | Insert   | Delete   |
| -------------- | -------- | -------- | -------- | -------- |
| Array          | O(1)     | O(n)     | O(n)     | O(n)     |
| Linked List    | O(n)     | O(n)     | O(1)*    | O(n)     |
| Stack          | O(n)     | O(n)     | O(1)     | O(1)     |
| Queue          | O(n)     | O(n)     | O(1)     | O(1)     |
| Hash Table     | -        | O(1)     | O(1)     | O(1)     |
| BST (Average)  | O(log n) | O(log n) | O(log n) | O(log n) |
| Heap           | -        | O(n)     | O(log n) | O(log n) |

* Insert at the head.

---

# Interview Problem Roadmap

### Easy (20)

* Two Sum
* Valid Parentheses
* Reverse Linked List
* Merge Two Sorted Lists
* Binary Search
* Maximum Depth of Binary Tree
* Invert Binary Tree
* Contains Duplicate
* Valid Anagram
* Best Time to Buy Stock
* Move Zeroes
* Missing Number
* Single Number
* Symmetric Tree
* Climbing Stairs
* Linked List Cycle
* Palindrome Linked List
* Flood Fill
* Same Tree
* Min Stack

### Medium (30)

* 3Sum
* Group Anagrams
* Top K Frequent Elements
* Product of Array Except Self
* Longest Consecutive Sequence
* Number of Islands
* Course Schedule
* Clone Graph
* Kth Largest Element
* Combination Sum
* Permutations
* Subsets
* Coin Change
* House Robber
* Merge Intervals
* Rotting Oranges
* Word Search
* LRU Cache
* Validate BST
* Lowest Common Ancestor
* Diameter of Binary Tree
* Binary Tree Level Order Traversal
* Jump Game
* Partition Equal Subset Sum
* Daily Temperatures
* Search in Rotated Sorted Array
* Find Minimum in Rotated Sorted Array
* Decode Ways
* Unique Paths
* Longest Increasing Subsequence

---

# শেখার পরিকল্পনা (৪৫ দিন)

| দিন   | বিষয়                                 |
| ----- | ------------------------------------- |
| ১–৩   | Big-O, Arrays                         |
| ৪–৫   | Strings                               |
| ৬–৯   | Linked Lists                          |
| ১০–১১ | Stack                                 |
| ১২–১৩ | Queue                                 |
| ১৪–১৬ | Hash Table                            |
| ১৭–১৯ | Recursion                             |
| ২০–২২ | Binary Search                         |
| ২৩–২৮ | Trees & BST                           |
| ২৯–৩০ | Heap                                  |
| ৩১–৩৫ | Graph                                 |
| ৩৬–৩৮ | Trie & Union-Find                     |
| ৩৯–৪১ | Backtracking                          |
| ৪২–৪৫ | Dynamic Programming + Mock Interviews |

# Module 1: Introduction to Data Structures

এই মডিউল শেষ করার পর তুমি জানতে পারবে—

* Data Structure কী
* কেন Data Structure শিখতে হবে
* Data Structure-এর প্রকারভেদ
* Algorithm কী
* Time Complexity কী
* Space Complexity কী
* Big O Notation কী
* Interview-এ কী ধরনের প্রশ্ন আসে

---

# 1. Data Structure কী?

**Definition**

Data Structure হলো এমন একটি পদ্ধতি বা উপায় যার মাধ্যমে **ডেটা সংগঠিত (Organize), সংরক্ষণ (Store), এবং পরিচালনা (Manage)** করা হয়, যাতে দ্রুত ও কার্যকরভাবে (Efficiently) ডেটার উপর কাজ করা যায়।

সহজ ভাষায়,

> **Data Structure = Data + Organization + Efficient Operations**

---

## Real Life Example

ধরো তোমার একটি আলমারি আছে।

যদি সব কাপড় এলোমেলো করে রাখো,

```
Shirt
Pant
T-Shirt
Jacket
Tie
```

তাহলে একটি শার্ট খুঁজতে অনেক সময় লাগবে।

কিন্তু যদি সুন্দরভাবে সাজাও,

```
Shirts
├── White
├── Black

Pants
├── Jeans
├── Formal

T-Shirts
```

তাহলে খুব দ্রুত খুঁজে পাবে।

কম্পিউটারেও একই বিষয় ঘটে।

---

## আরেকটি উদাহরণ

ধরো একটি স্কুলে ৫০,০০০ শিক্ষার্থী আছে।

তুমি যদি একজন ছাত্রের তথ্য খুঁজতে চাও।

### খারাপ উপায়

```
Student 1

Student 2

Student 3

...

Student 50000
```

এক এক করে দেখতে হবে।

সময় লাগবে।

---

### ভালো উপায়

রোল নম্বর অনুযায়ী সাজানো

```
Roll 1001

Roll 1002

Roll 1003
```

এখন Binary Search ব্যবহার করে কয়েক ধাপেই খুঁজে পাওয়া যাবে।

---

# 2. Data Structure কেন শিখব?

কারণ বড় সফটওয়্যার সব Data Structure-এর উপর নির্ভর করে।

উদাহরণ:

### Facebook

Friends List

```
Graph
```

---

### Google Search

```
Trie
```

---

### WhatsApp

```
Queue
```

---

### Browser

```
Stack
```

---

### GPS

```
Graph
```

---

### Database

```
B-Tree
```

---

### Operating System

```
Queue

Heap

Tree
```

---

## Interview-এ কেন গুরুত্বপূর্ণ?

প্রায় সব Software Engineer Interview-এ Data Structure থেকে প্রশ্ন আসে।

যেমন:

* Reverse Linked List
* Two Sum
* Valid Parentheses
* Binary Search
* BFS
* DFS
* Heap
* Dynamic Programming

---

# 3. Data Structure-এর ধরন

দুইটি প্রধান ভাগ:

```
Data Structure

│

├── Primitive

└── Non Primitive
```

---

## Primitive Data Structure

Programming Language নিজেই দেয়।

যেমন

```
int

float

char

bool

string
```

Python-এ

```python
age = 25
price = 19.5
name = "Atiar"
is_active = True
```

---

## Non Primitive Data Structure

আমরা নিজেরা ব্যবহার বা তৈরি করি।

```
Array

Linked List

Stack

Queue

Tree

Graph

Hash Table

Heap

Trie
```

---

# 4. Linear Data Structure

ডেটা এক লাইনে সাজানো থাকে।

```
10 → 20 → 30 → 40 → 50
```

Examples

* Array
* Linked List
* Stack
* Queue

---

# 5. Non Linear Data Structure

ডেটা শাখা-প্রশাখার মতো থাকে।

```
        A

      /   \

     B     C

    / \

   D   E
```

Examples

* Tree
* Graph

---

# 6. Static vs Dynamic Data Structure

## Static

Size আগে থেকেই নির্ধারিত।

উদাহরণ (C)

```c
int arr[100];
```

Size পরিবর্তন করা যায় না।

---

## Dynamic

প্রয়োজন অনুযায়ী Size বাড়ে বা কমে।

Python List

```python
arr = []

arr.append(10)

arr.append(20)

arr.append(30)
```

Python List স্বয়ংক্রিয়ভাবে বড় হতে পারে।

---

# 7. Algorithm কী?

Data Structure ডেটা রাখে।

Algorithm সেই ডেটার উপর কাজ করে।

উদাহরণ

```
Array

↓

Sorting Algorithm

↓

Sorted Array
```

---

আরেকটি উদাহরণ

```
Linked List

↓

Reverse Algorithm

↓

Reversed Linked List
```

---

# 8. Data Structure vs Algorithm

| Data Structure | Algorithm              |
| -------------- | ---------------------- |
| Data Store করে | Data Process করে       |
| Container      | Step-by-step procedure |
| Example: Array | Example: Binary Search |

---

# 9. Time Complexity

একটি Algorithm চালাতে কত সময় লাগতে পারে, তার বৃদ্ধির হার (growth) বোঝায়।

এটি **ইনপুটের আকার (n)** অনুযায়ী বিশ্লেষণ করা হয়, বাস্তব ঘড়ির সময় নয়।

উদাহরণ

```python
for i in range(n):
    print(i)
```

Loop

```
n বার
```

Complexity

```
O(n)
```

---

আরেকটি উদাহরণ

```python
print(arr[5])
```

মাত্র একবার কাজ করছে।

```
O(1)
```

---

# 10. Space Complexity

Algorithm অতিরিক্ত কত Memory ব্যবহার করছে।

Example

```python
arr = [1, 2, 3]
```

Memory

```
3 Integer
```

---

Example

```python
new = []

for x in arr:
    new.append(x)
```

নতুন একটি List তৈরি হয়েছে।

```
Extra Memory = O(n)
```

---

# 11. Big O Notation

Big O দিয়ে বোঝানো হয় Algorithm-এর Worst Case Time Complexity।

সবচেয়ে বেশি ব্যবহৃত Complexity গুলো:

| Big O      | নাম          | উদাহরণ             |
| ---------- | ------------ | ------------------ |
| O(1)       | Constant     | Array Index Access |
| O(log n)   | Logarithmic  | Binary Search      |
| O(n)       | Linear       | Linear Search      |
| O(n log n) | Linearithmic | Merge Sort         |
| O(n²)      | Quadratic    | Nested Loop        |
| O(2ⁿ)      | Exponential  | Recursive Subsets  |
| O(n!)      | Factorial    | Permutations       |

---

## Visualization

```
Fast

O(1)

↓

O(log n)

↓

O(n)

↓

O(n log n)

↓

O(n²)

↓

O(2ⁿ)

↓

O(n!)

Slow
```

---

# 12. Big O Examples

### O(1)

```python
arr = [10, 20, 30]

print(arr[1])
```

---

### O(n)

```python
for item in arr:
    print(item)
```

---

### O(n²)

```python
for i in arr:
    for j in arr:
        print(i, j)
```

---

### O(log n)

```python
# Binary Search
```

প্রতিবার Search Space অর্ধেক হয়ে যায়।

---

# 13. Interview Questions

1. Data Structure কী?
2. Algorithm কী?
3. Data Structure এবং Algorithm-এর পার্থক্য কী?
4. Primitive এবং Non-Primitive Data Structure-এর পার্থক্য কী?
5. Linear ও Non-Linear Data Structure-এর পার্থক্য কী?
6. Static ও Dynamic Data Structure কী?
7. Time Complexity কী?
8. Space Complexity কী?
9. Big O কী?
10. O(1), O(n), O(log n)-এর উদাহরণ দাও।

---

# Module 1 Summary

* Data Structure ডেটাকে দক্ষভাবে সংরক্ষণ ও পরিচালনার পদ্ধতি।
* Algorithm হলো ডেটার উপর কাজ করার ধাপসমূহ।
* Data Structure দুই ধরনের: Primitive ও Non-Primitive।
* Non-Primitive আবার Linear ও Non-Linear হতে পারে।
* Time Complexity ইনপুট বড় হলে কাজের পরিমাণ কীভাবে বাড়ে তা বোঝায়।
* Space Complexity অতিরিক্ত মেমরি ব্যবহারের পরিমাণ বোঝায়।
* Big O Notation সাধারণত Worst Case Performance প্রকাশ করে।

---

## অনুশীলনী (Practice)

1. Data Structure কী? নিজের ভাষায় লিখো।
2. Array, Stack, Queue, Tree এবং Graph-এর একটি করে বাস্তব জীবনের উদাহরণ দাও।
3. O(1), O(n) এবং O(n²)-এর জন্য একটি করে Python কোড লেখো।
4. ব্যাখ্যা করো কেন Binary Search-এর Time Complexity `O(log n)`।
5. নিচের কোডগুলোর Time Complexity বের করো:

```python
# (ক)
for i in range(n):
    print(i)

# (খ)
for i in range(n):
    for j in range(n):
        print(i, j)

# (গ)
print(arr[0])
```

**পরবর্তী মডিউল:** **Module 2 – Arrays (সম্পূর্ণ গভীরভাবে: Memory Layout, Dynamic Array, Operations, Time Complexity, Interview Questions, এবং LeetCode Problems)।**




# Module 2: Arrays (Complete Tutorial)

এই মডিউল শেষে তুমি জানতে পারবে:

* Array কী?
* Array কীভাবে Memory-তে Store হয়?
* Static Array vs Dynamic Array
* Array-এর Operations
* Time Complexity
* Python List কীভাবে কাজ করে?
* Interview Questions
* LeetCode Problems

---

# 1. Array কী?

**Array** হলো একই ধরনের (same type) একাধিক ডেটা **পরপর (contiguous)** মেমরিতে সংরক্ষণ করার একটি Data Structure।

উদাহরণ:

```text
Index:   0    1    2    3    4

Value:  10   20   30   40   50
```

এখানে,

* `10` এর Index = 0
* `20` এর Index = 1
* `50` এর Index = 4

---

# 2. কেন Array ব্যবহার করি?

ধরো ৫ জন শিক্ষার্থীর নম্বর রাখতে হবে।

ভুল উপায়:

```python
mark1 = 85
mark2 = 92
mark3 = 75
mark4 = 80
mark5 = 88
```

সঠিক উপায়:

```python
marks = [85, 92, 75, 80, 88]
```

এখন Loop ব্যবহার করে সব নম্বর একসাথে প্রসেস করা যায়।

---

# 3. Array-এর Memory Layout

Array-এর সবচেয়ে গুরুত্বপূর্ণ বৈশিষ্ট্য হলো এটি **Contiguous Memory** ব্যবহার করে।

```text
Memory Address

1000 → 10

1004 → 20

1008 → 30

1012 → 40

1016 → 50
```

ধরা যাক একটি `int` = 4 bytes।

তাহলে,

```text
Address = Base + (Index × Size)
```

উদাহরণ

```text
Base = 1000

Index = 3

Size = 4

Address = 1000 + (3 × 4)

= 1012
```

এ কারণেই Array-তে যেকোনো Index-এ সরাসরি পৌঁছানো যায়।

---

# 4. Random Access

```python
arr = [10, 20, 30, 40, 50]

print(arr[3])
```

Output

```text
40
```

Python-কে ০ থেকে ২ পর্যন্ত ঘুরে দেখতে হয় না। এটি সরাসরি Index 3-এ যায়।

**Time Complexity**

```text
O(1)
```

---

# 5. Array Traversal

Traversal মানে Array-এর প্রতিটি Element দেখা।

```python
arr = [10, 20, 30, 40]

for item in arr:
    print(item)
```

Output

```text
10
20
30
40
```

Complexity

```text
O(n)
```

---

# 6. Insert Operation

### শেষে Insert

```python
arr = [10, 20, 30]

arr.append(40)

print(arr)
```

Output

```text
[10, 20, 30, 40]
```

Average Complexity

```text
O(1)
```

---

### মাঝখানে Insert

```python
arr = [10, 20, 30, 40]

arr.insert(2, 25)
```

Result

```text
10 20 25 30 40
```

Memory

আগে

```text
10 20 30 40
```

পরে

```text
10 20 25 30 40
```

`30` এবং `40`-কে ডানে সরাতে হয়েছে।

Complexity

```text
O(n)
```

---

# 7. Delete Operation

```python
arr = [10, 20, 30, 40]

arr.remove(20)
```

Result

```text
10 30 40
```

মেমরিতে:

আগে

```text
10 20 30 40
```

পরে

```text
10 30 40
```

`30` এবং `40` বামে সরে এসেছে।

Complexity

```text
O(n)
```

---

# 8. Update

```python
arr = [10, 20, 30]

arr[1] = 99

print(arr)
```

Output

```text
10 99 30
```

Complexity

```text
O(1)
```

---

# 9. Search

### Linear Search

```python
arr = [10, 20, 30, 40]

target = 30

for i in range(len(arr)):
    if arr[i] == target:
        print(i)
```

Complexity

```text
O(n)
```

---

### Binary Search

শুধুমাত্র Sorted Array-এর জন্য।

```text
10 20 30 40 50
```

Complexity

```text
O(log n)
```

এটি আমরা Binary Search মডিউলে বিস্তারিত শিখব।

---

# 10. Python List কি Array?

অনেকটা, কিন্তু পুরোপুরি নয়।

Python-এর `list` একটি **Dynamic Array**।

এটি নিজে থেকেই বড় বা ছোট হতে পারে।

```python
arr = []

arr.append(10)

arr.append(20)

arr.append(30)
```

---

# 11. Dynamic Array কীভাবে বড় হয়?

ধরা যাক Capacity = 4

```text
10

20

30

40
```

আর একটি Element যোগ করলাম।

```python
arr.append(50)
```

তখন Python নতুন একটি বড় Memory Allocate করে।

```text
Old

10 20 30 40

↓

New

10 20 30 40 50 _ _ _
```

এ কারণে কখনও কখনও `append()`-এ কপি করার খরচ হয়, কিন্তু গড়ে এটি `O(1)` থাকে (Amortized Analysis)।

---

# 12. Time Complexity Table

| Operation     | Complexity       |
| ------------- | ---------------- |
| Access        | O(1)             |
| Update        | O(1)             |
| Search        | O(n)             |
| Insert End    | O(1) (Amortized) |
| Insert Middle | O(n)             |
| Delete        | O(n)             |
| Traversal     | O(n)             |

---

# 13. Advantages

* দ্রুত Access (`O(1)`)
* Cache Friendly
* সহজ Implementation
* কম Memory Overhead

---

# 14. Disadvantages

* মাঝখানে Insert/Delete ধীর
* Contiguous Memory প্রয়োজন
* Static Array-এর Size পরিবর্তন করা যায় না

---

# 15. Common Interview Questions

### Q1. কেন Array Access `O(1)`?

কারণ Address Formula দিয়ে সরাসরি Memory Location বের করা যায়।

---

### Q2. Insert কেন `O(n)`?

কারণ পরের Element-গুলোকে Shift করতে হয়।

---

### Q3. Delete কেন `O(n)`?

কারণ Delete-এর পরে বাকি Element-গুলোকে বামে Shift করতে হয়।

---

### Q4. Python List কি Linked List?

**না।**

Python List হলো **Dynamic Array**।

---

### Q5. Array আর Linked List-এর পার্থক্য?

| Array             | Linked List           |
| ----------------- | --------------------- |
| Contiguous Memory | Non-Contiguous Memory |
| Access O(1)       | Access O(n)           |
| Insert O(n)       | Head-এ Insert O(1)    |
| Cache Friendly    | কম Cache Friendly     |

---

# 16. Common Mistakes

❌ Index Out of Range

```python
arr = [10, 20]

print(arr[5])
```

Error:

```text
IndexError: list index out of range
```

---

❌ Loop-এর সীমা ভুল

```python
for i in range(len(arr) + 1):
    print(arr[i])
```

সঠিক:

```python
for i in range(len(arr)):
    print(arr[i])
```

---

# 17. Interview Coding Problems

### Easy

* Two Sum
* Remove Duplicates from Sorted Array
* Move Zeroes
* Maximum Subarray
* Best Time to Buy and Sell Stock
* Contains Duplicate

### Medium

* Product of Array Except Self
* Rotate Array
* 3Sum
* Merge Intervals
* Spiral Matrix
* Set Matrix Zeroes

---

# 18. Practice Questions

### Question 1

Array-এর Access `O(1)` কেন?

---

### Question 2

Delete `O(n)` কেন?

---

### Question 3

Python List কি Static Array?

---

### Question 4

নিচের কোডের Time Complexity কত?

```python
arr = [1, 2, 3, 4, 5]

for item in arr:
    print(item)
```

---

### Question 5

নিচের কোডের Complexity কত?

```python
arr = [10, 20, 30]

arr.append(40)
```

---

# Module 2 Summary

* Array একই ধরনের ডেটা পরপর (contiguous) মেমরিতে সংরক্ষণ করে।
* Index-এর মাধ্যমে Element Access করা যায়, তাই Access ও Update `O(1)`।
* Traversal ও Linear Search `O(n)`।
* মাঝখানে Insert/Delete করতে Element Shift করতে হয়, তাই `O(n)`।
* Python-এর `list` একটি Dynamic Array, Static Array নয়।
* Dynamic Array প্রয়োজনে বড় Memory Allocate করে এবং পুরনো ডেটা কপি করে, তাই `append()`-এর গড় সময় `O(1)` (Amortized)।

### পরবর্তী মডিউল

**Module 3: Strings** — String Memory, Immutability, Common Operations, Two Pointers, Sliding Window, Interview Patterns এবং LeetCode Problems।
# Module 3: Strings (Complete Tutorial)

এই মডিউল শেষে তুমি জানতে পারবে—

* String কী?
* String কীভাবে Memory-তে Store হয়?
* Mutable vs Immutable
* String Operations
* Time Complexity
* Two Pointer Technique
* Sliding Window
* Interview Questions
* LeetCode Problems

---

# 1. String কী?

**String** হলো Character-এর একটি Sequence।

উদাহরণ:

```python
name = "Atiar"
```

Memory-তে এটি এমনভাবে কল্পনা করা যায়:

```text
Index:   0   1   2   3   4

Value:   A   t   i   a   r
```

এখানে

```
name[0] = 'A'

name[4] = 'r'
```

---

# 2. Character কী?

Character মানে একটি মাত্র Symbol।

```python
'A'

'B'

'5'

'?'
```

String

```python
"Hello"
```

Character

```python
'H'
```

---

# 3. String Memory Layout

ধরো

```python
text = "HELLO"
```

Memory

```text
Index

0 → H

1 → E

2 → L

3 → L

4 → O
```

---

# 4. Python String Immutable

Python-এর String **Immutable**।

অর্থাৎ তৈরি হওয়ার পরে পরিবর্তন করা যায় না।

ভুল

```python
text = "Hello"

text[0] = "Y"
```

Output

```text
TypeError:
'str' object does not support item assignment
```

---

## তাহলে পরিবর্তন কীভাবে করি?

নতুন String তৈরি হয়।

```python
text = "Hello"

text = "Y" + text[1:]

print(text)
```

Output

```text
Yello
```

---

# 5. কেন String Immutable?

কারণ

* নিরাপদ (Safe)
* Hash করা সহজ
* Dictionary Key হিসেবে ব্যবহার করা যায়
* Memory Optimization সম্ভব

---

# 6. String Access

```python
name = "Python"

print(name[0])

print(name[-1])
```

Output

```text
P

n
```

Complexity

```
O(1)
```

---

# 7. Traversal

```python
text = "Python"

for ch in text:
    print(ch)
```

Output

```text
P
y
t
h
o
n
```

Complexity

```
O(n)
```

---

# 8. Length

```python
text = "Bangladesh"

print(len(text))
```

Output

```text
10
```

Complexity

```
O(1)
```

Python String নিজের Length সংরক্ষণ করে।

---

# 9. Concatenation

```python
first = "Hello"

second = "World"

print(first + " " + second)
```

Output

```text
Hello World
```

Complexity

```
O(n)
```

কারণ নতুন String তৈরি হয়।

---

# 10. Repetition

```python
print("Hi " * 3)
```

Output

```text
Hi Hi Hi
```

---

# 11. String Slicing

Syntax

```python
string[start:end]
```

Example

```python
text = "Programming"

print(text[0:7])
```

Output

```text
Program
```

আরও উদাহরণ

```python
text = "Python"

print(text[:3])

print(text[2:])

print(text[-3:])
```

Output

```text
Pyt

thon

hon
```

---

# 12. Reverse String

```python
text = "Python"

print(text[::-1])
```

Output

```text
nohtyP
```

Complexity

```
O(n)
```

---

# 13. Common String Functions

### Upper

```python
print("python".upper())
```

Output

```
PYTHON
```

---

### Lower

```python
print("PYTHON".lower())
```

Output

```
python
```

---

### Strip

```python
text = " hello "

print(text.strip())
```

Output

```
hello
```

---

### Replace

```python
text = "I like Java"

print(text.replace("Java","Python"))
```

Output

```
I like Python
```

---

### Split

```python
text = "apple,banana,mango"

print(text.split(","))
```

Output

```python
['apple', 'banana', 'mango']
```

---

### Join

```python
items = ['A', 'B', 'C']

print("-".join(items))
```

Output

```text
A-B-C
```

---

# 14. Searching

```python
text = "Programming"

print("gram" in text)
```

Output

```text
True
```

---

# 15. Count

```python
text = "banana"

print(text.count("a"))
```

Output

```text
3
```

---

# 16. Palindrome

Palindrome সামনে ও পিছনে একই।

```
madam

level

racecar
```

Python

```python
word = "madam"

print(word == word[::-1])
```

Output

```
True
```

---

# 17. Anagram

দুটি String-এ একই Character থাকবে।

Example

```
listen

silent
```

Python

```python
a = "listen"

b = "silent"

print(sorted(a) == sorted(b))
```

Output

```
True
```

Complexity

```
O(n log n)
```

---

# 18. Character Frequency

```python
text = "banana"

freq = {}

for ch in text:

    freq[ch] = freq.get(ch, 0) + 1

print(freq)
```

Output

```python
{
 'b':1,
 'a':3,
 'n':2
}
```

Complexity

```
O(n)
```

---

# 19. Two Pointer Technique

খুব গুরুত্বপূর্ণ Interview Pattern।

Example

Reverse String

```text
Python

↑     ↑

L     R
```

Algorithm

* Left সামনে যাবে
* Right পিছনে যাবে
* Swap করবে

Python

```python
s = list("Python")

left = 0

right = len(s) - 1

while left < right:

    s[left], s[right] = s[right], s[left]

    left += 1

    right -= 1

print("".join(s))
```

Output

```
nohtyP
```

Complexity

```
O(n)
```

---

# 20. Sliding Window

Interview-এর সবচেয়ে গুরুত্বপূর্ণ Technique।

ধরো

```
ABCADEAF
```

Longest Unique Substring বের করতে হবে।

Window

```text
ABC

↓

BCA

↓

CAD
```

এটি `O(n²)` এর বদলে `O(n)`-এ সমাধান করতে সাহায্য করে।

---

# 21. Time Complexity Table

| Operation     | Complexity |
| ------------- | ---------- |
| Access        | O(1)       |
| Length        | O(1)       |
| Traversal     | O(n)       |
| Search (`in`) | O(n)       |
| Slice         | O(k)       |
| Reverse       | O(n)       |
| Concatenation | O(n)       |
| Replace       | O(n)       |
| Split         | O(n)       |
| Join          | O(n)       |

> এখানে `k` হলো Slice-এর দৈর্ঘ্য।

---

# 22. Common Interview Questions

### Question 1

Python String Mutable নাকি Immutable?

উত্তর

```
Immutable
```

---

### Question 2

String Reverse করার তিনটি উপায় বলো।

* Slicing
* Two Pointer
* `reversed()` ব্যবহার করে

---

### Question 3

Palindrome কী?

সামনে ও পিছনে একই String।

---

### Question 4

Anagram কী?

একই Character ভিন্ন ক্রমে সাজানো দুইটি String।

---

### Question 5

String Concatenation কেন `O(n)`?

কারণ নতুন String তৈরি করতে হয় এবং পুরোনো Character-গুলো কপি করতে হয়।

---

# 23. Common Mistakes

❌ String পরিবর্তন করার চেষ্টা

```python
text = "abc"

text[0] = "A"
```

Error

```
TypeError
```

---

❌ `+` দিয়ে Loop-এর মধ্যে বারবার String জোড়া লাগানো

```python
result = ""

for ch in chars:
    result += ch
```

বড় ইনপুটে এটি ধীর হতে পারে।

ভালো উপায়

```python
chars = ["P", "y", "t", "h", "o", "n"]

result = "".join(chars)

print(result)
```

---

# 24. Interview Problems

## Easy

* Valid Anagram
* Reverse String
* Valid Palindrome
* Longest Common Prefix
* Reverse Words in a String III
* Detect Capital

---

## Medium

* Longest Substring Without Repeating Characters
* Group Anagrams
* Minimum Window Substring
* Longest Palindromic Substring
* String Compression
* Decode String

---

# 25. Practice Questions

### Question 1

String Immutable বলতে কী বোঝায়?

---

### Question 2

নিচের কোডের Output কী?

```python
text = "Python"

print(text[::-1])
```

---

### Question 3

নিচের কোডের Time Complexity কত?

```python
for ch in text:
    print(ch)
```

---

### Question 4

Palindrome Check করার Python Code লেখো।

---

### Question 5

"listen" এবং "silent" Anagram কি না তা যাচাই করার Program লেখো।

---

# Module 3 Summary

* String হলো Character-এর Sequence।
* Python String **Immutable**; পরিবর্তন করলে নতুন String তৈরি হয়।
* Access ও Indexing `O(1)`।
* Traversal, Search, Reverse, Replace সাধারণত `O(n)`।
* Slicing দিয়ে সহজে Substring এবং Reverse করা যায়।
* **Two Pointer** ও **Sliding Window** String Interview-এর সবচেয়ে গুরুত্বপূর্ণ দুটি Pattern।
* Palindrome, Anagram এবং Character Frequency হলো খুবই সাধারণ Interview Problem।

---

## 🎯 Interview Tip

Strings নিয়ে প্রশ্ন এলে আগে এই বিষয়গুলো ভাবো:

1. **Indexing** লাগবে?
2. **Hash Map** ব্যবহার করলে দ্রুত হবে?
3. **Two Pointers** দিয়ে সমাধান সম্ভব?
4. **Sliding Window** প্রয়োগ করা যাবে?
5. String **Immutable**, তাই কি নতুন String বা List ব্যবহার করা উচিত?

এই চিন্তার ধাপগুলো অনুসরণ করলে বেশিরভাগ String Interview Problem-এর সঠিক Approach খুঁজে পাওয়া সহজ হবে।

**পরবর্তী মডিউল:** **Module 4 – Linked List** (Node, Singly Linked List, Doubly Linked List, Circular Linked List, Reverse Linked List, Cycle Detection, Merge Linked Lists, Time Complexity, এবং Interview Problems)।
