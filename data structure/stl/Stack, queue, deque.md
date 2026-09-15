

1. stack(LIFO - Last in first out)
###### definition: 
A stack is linear data structure where the last element  added is the first one remove - like a stack of plates

###### implementation
You can use a list or the `collections.deque`  module.

###### syntax
```python
stack = []

#push element (add to top)
stack.append(3)
stack.append(5)
stack.append(6)

# pop elements(remove from top)
stack.pop()
stack.pop()
```

###### key points
-  operates on LIFO
-  common operations
	-  push()-> append()
	-  pop() -> pop()
-  use when you need reversal or backtracking(e.g. undo feature, recursion)

2.  Queue(FIFO - First In First Out)
###### definition:
A queue is a linear data structure where the first element added is the first one removed like people standing in line.

###### Implementation:
best implemented using `collection.deque` for efficiency (list are slow for this)


###### syntax
```python
from collections import deque

queue = deque()

# Enqueue (add to end)
queue.append(10)
queue.append(20)
queue.append(30)

# Dequeue (remove from front)
queue.popleft()  # Removes 10
queue.popleft()  # Removes 20

```


###### key points
-  Operates on FIFO principle
-  Common operations:
	-  `enqueue() -> append()`
	-  `dequeue() -> popleft()`
- used in task scheduling, buffering, and `BFS`algorithm


3.  `Deque()` (Double Ended queue)
###### definition:
A `deque`  allows insertion and deletion from both ends  efficiently  - left and right

###### implementation:
use the `collection.deque`  class

###### syntax
``` python
from collections import deque

dq = deque([10, 20, 30])

# Add to right
dq.append(40)

# Add to left
dq.appendleft(0)

# Remove from right
dq.pop()

# Remove from left
dq.popleft()

```

###### key points
-  supports LIFO and FIFO
-  fast O(1) operations from both ends
-  useful for sliding window, palindrome checking, etc

###### summery table
|Feature|**Stack**|**Queue**|**Deque**|
|---|---|---|---|
|Principle|LIFO|FIFO|Both (LIFO & FIFO)|
|Implementation|`list` or `deque`|`deque`|`collections.deque`|
|Add Operation|`append()`|`append()`|`append()`, `appendleft()`|
|Remove Operation|`pop()`|`popleft()`|`pop()`, `popleft()`|
|Efficiency|O(1) with deque|O(1) with deque|O(1) both ends|
|Typical Uses|Undo, recursion|Scheduling, BFS|Sliding window, bidirectional|

## 🧩 Queue Implementation Using List

### ➤ Concept:

A **Queue** follows the **FIFO (First In, First Out)** principle:

- **Enqueue** → add an element to the **end** of the list
    
- **Dequeue** → remove an element from the **front** of the list
    

---

### ✅ **Example Code**

```python
# Queue implementation using list
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        """Add an element to the end of the queue"""
        self.queue.append(item)

    def dequeue(self):
        """Remove and return the element from the front of the queue"""
        if len(self.queue) < 1:
            return None
        return self.queue.pop(0)   # Removes the first element

    def peek(self):
        """Return the front element without removing it"""
        if len(self.queue) < 1:
            return None
        return self.queue[0]

    def is_empty(self):
        """Check if the queue is empty"""
        return len(self.queue) == 0

    def size(self):
        """Return the number of elements in the queue"""
        return len(self.queue)

# Example usage
q = Queue()
q.enqueue(10)
q.enqueue(20)
q.enqueue(30)
print("Queue:", q.queue)

print("Dequeued:", q.dequeue())
print("After dequeue:", q.queue)

print("Front element:", q.peek())
print("Queue size:", q.size())
```

---

### 🧠 Output Example

```
Queue: [10, 20, 30]
Dequeued: 10
After dequeue: [20, 30]
Front element: 20
Queue size: 2
```

---

### ⚙️ **Efficiency Note**

Using a **list** for a queue works, but it has a **performance issue**:

- `append()` → ✅ O(1)
    
- `pop(0)` → ❌ O(n) ← because removing the first element shifts all others one step left
    

That’s why in **real applications**, we prefer:

```python
from collections import deque
```

because `deque` provides **O(1)** time for both ends.

---

Excellent question 👍 — and you’re thinking in exactly the right direction!

Let’s break it down carefully 👇

---

### 🧠 When you do `pop(0)` on a list:

In Python, a **list** is an **ordered sequence**, so every element has an **index**.

Let’s say you start with this list:

```python
queue = [10, 20, 30, 40]
```

Now you run:

```python
queue.pop(0)
```

This will:

- Remove the **first element** (`10`).
    
- Shift **all other elements** one position to the **left**.
    
- So now `20` moves to index `0`, `30` moves to index `1`, and so on.
    

Resulting list:

```python
queue = [20, 30, 40]
```

Now if you check:

```python
queue[0]
```

✅ You will get `20`.

---

### 🧩 Example Demonstration:

```python
queue = [10, 20, 30, 40]

print("Before pop:", queue)
queue.pop(0)
print("After first pop:", queue)
print("Now queue[0] =", queue[0])
```

**Output:**

```
Before pop: [10, 20, 30, 40]
After first pop: [20, 30, 40]
Now queue[0] = 20
```

---

### ⚙️ But — Performance Warning ⚠️

Every time you call `pop(0)`, Python:

- Removes the first element ✅
    
- Shifts **every remaining element** to fill the gap ❌
    

That’s why `pop(0)` is **O(n)** (linear time).

If you want to efficiently remove from the front of a queue, use **`collections.deque`**, which provides **O(1)** `popleft()`:

```python
from collections import deque

queue = deque([10, 20, 30, 40])
queue.popleft()  # removes 10 quickly
print(queue)  # deque([20, 30, 40])
```

---

✅ **Summary:**

- After `pop(0)`, yes — the second element becomes the new index `0`.
    
- But repeated `pop(0)` is **inefficient** — prefer `deque` for real queues.

