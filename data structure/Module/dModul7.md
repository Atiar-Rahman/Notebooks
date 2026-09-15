# ✅ C++ STL `list` Built-in Functions (Complete Guide)

`std::list` হলো **Doubly Linked List** ভিত্তিক container।
👉 Random access নেই (array/vector এর মতো index দিয়ে সরাসরি access করা যায় না)।
👉 Insert/Delete খুব efficient (বিশেষ করে head/tail এ)।

---

# 🔹 1️⃣ Constructor

| Name                                     | Details                                   | Time Complexity |
| ---------------------------------------- | ----------------------------------------- | --------------- |
| `list<type> myList;`                     | Empty list তৈরি করে                       | O(1)            |
| `list<type> myList(N);`                  | N টি element তৈরি (garbage/default value) | O(N)            |
| `list<type> myList(N, V);`               | N টি element, সবগুলোর মান V               | O(N)            |
| `list<type> myList(list2);`              | আরেকটি list copy করে                      | O(N)            |
| `list<type> myList(A, A+N);`             | Array থেকে copy করে                       | O(N)            |
| `list<type> myList(v.begin(), v.end());` | Vector থেকে copy করে                      | O(N)            |

---

# 🔹 2️⃣ Capacity Functions

| Name                | Details                         | Time Complexity           |
| ------------------- | ------------------------------- | ------------------------- |
| `myList.size()`     | List এর size দেয়                | O(1)                      |
| `myList.max_size()` | সর্বোচ্চ কত element রাখতে পারবে | O(1)                      |
| `myList.clear()`    | সব element delete করে           | O(N)                      |
| `myList.empty()`    | খালি কিনা true/false দেয়        | O(1)                      |
| `myList.resize(N)`  | Size পরিবর্তন করে               | O(K) (difference অনুযায়ী) |

---

# 🔹 3️⃣ Modifiers

| Name                        | Details                 | Time Complexity |
| --------------------------- | ----------------------- | --------------- |
| `myList = list2`            | আরেকটি list assign      | O(N)            |
| `myList.assign(begin, end)` | Range assign            | O(N)            |
| `myList.push_back(x)`       | Tail এ element যোগ      | O(1)            |
| `myList.push_front(x)`      | Head এ element যোগ      | O(1)            |
| `myList.pop_back()`         | Tail delete             | O(1)            |
| `myList.pop_front()`        | Head delete             | O(1)            |
| `myList.insert(pos, x)`     | নির্দিষ্ট জায়গায় insert | O(N)            |
| `myList.erase(pos)`         | নির্দিষ্ট জায়গা delete  | O(N)            |

---

# 🔹 4️⃣ Non-Member Algorithms (STL `<algorithm>` থেকে)

| Name                            | Details                    | Time Complexity |
| ------------------------------- | -------------------------- | --------------- |
| `replace(begin, end, v, new_v)` | সব v কে new_v দিয়ে replace | O(N)            |
| `find(begin, end, V)`           | V খুঁজে বের করে            | O(N)            |

---

# 🔹 5️⃣ Operations (List specific)

| Name                           | Details                              | Time Complexity |
| ------------------------------ | ------------------------------------ | --------------- |
| `myList.remove(V)`             | V এর সব occurrence remove            | O(N)            |
| `myList.sort()`                | Ascending sort                       | O(N log N)      |
| `myList.sort(greater<type>())` | Descending sort                      | O(N log N)      |
| `myList.unique()`              | Duplicate remove (আগে sort করতে হবে) | O(N)            |
| `myList.reverse()`             | List reverse                         | O(N)            |

---

# 🔹 6️⃣ Element Access

⚠️ List এ direct indexing নেই।

| Name                      | Details             | Time Complexity |
| ------------------------- | ------------------- | --------------- |
| `myList.front()`          | First element       | O(1)            |
| `myList.back()`           | Last element        | O(1)            |
| `next(myList.begin(), i)` | i-th element access | O(N)            |

---

# 🔹 7️⃣ Iterators

| Name             | Details                | Time Complexity |
| ---------------- | ---------------------- | --------------- |
| `myList.begin()` | First element iterator | O(1)            |
| `myList.end()`   | Last এর পরের iterator  | O(1)            |

---

# 🎯 Important Interview Points

✅ `list` এ random access slow (O(N))
✅ Insert/Delete fast (O(1)) যদি iterator position জানা থাকে
✅ Memory overhead বেশি (doubly linked list node)
✅ `vector` বেশি use হয় competitive programming এ
✅ `list` useful যখন frequent insert/delete লাগে

---

দারুণ 🔥 এখন আমি **C++ STL `list` এর প্রতিটা term example সহ** পরিষ্কারভাবে বুঝিয়ে দিচ্ছি।

---

# 🔷 1️⃣ Constructor

### 1. `list<int> myList;`

👉 Empty list তৈরি

```cpp
#include <list>
using namespace std;

list<int> myList;   // {}
```

---

### 2. `list<int> myList(N);`

👉 N টি element তৈরি (default value = 0)

```cpp
list<int> myList(3);  
// {0, 0, 0}
```

---

### 3. `list<int> myList(N, V);`

👉 N টি element, সবগুলোর মান V

```cpp
list<int> myList(4, 5);
// {5, 5, 5, 5}
```

---

### 4. Copy Constructor

```cpp
list<int> list1 = {1,2,3};
list<int> list2(list1);
// {1,2,3}
```

---

### 5. Array থেকে copy

```cpp
int A[] = {10,20,30};
list<int> myList(A, A+3);
// {10,20,30}
```

---

### 6. Vector থেকে copy

```cpp
vector<int> v = {5,6,7};
list<int> myList(v.begin(), v.end());
// {5,6,7}
```

---

# 🔷 2️⃣ Capacity Functions

### `size()`

```cpp
list<int> L = {1,2,3};
cout << L.size();   // 3
```

---

### `max_size()`

```cpp
cout << L.max_size();  // বড় একটা সংখ্যা
```

---

### `clear()`

```cpp
L.clear();  
// {}
```

---

### `empty()`

```cpp
if(L.empty())
    cout<<"Empty";
```

---

### `resize()`

```cpp
list<int> L = {1,2,3};

L.resize(5);     
// {1,2,3,0,0}

L.resize(2);     
// {1,2}
```

---

# 🔷 3️⃣ Modifiers

### `assign()`

```cpp
list<int> L;
L.assign(3, 10);
// {10,10,10}
```

---

### `push_back()`

```cpp
L.push_back(5);
// শেষে যোগ হয়
```

---

### `push_front()`

```cpp
L.push_front(1);
// শুরুতে যোগ হয়
```

---

### `pop_back()`

```cpp
L.pop_back();
// শেষ element delete
```

---

### `pop_front()`

```cpp
L.pop_front();
// প্রথম element delete
```

---

### `insert()`

```cpp
list<int> L = {1,2,4};

auto it = next(L.begin(),2);
L.insert(it, 3);

// {1,2,3,4}
```

---

### `erase()`

```cpp
auto it = next(L.begin(),1);
L.erase(it);

// remove 2
```

---

# 🔷 4️⃣ STL Algorithm Functions

### `replace()`

```cpp
list<int> L = {1,2,2,3};

replace(L.begin(), L.end(), 2, 5);
// {1,5,5,3}
```

---

### `find()`

```cpp
auto it = find(L.begin(), L.end(), 5);

if(it != L.end())
    cout<<"Found";
```

---

# 🔷 5️⃣ List Specific Operations

### `remove()`

```cpp
list<int> L = {1,2,2,3};
L.remove(2);
// {1,3}
```

---

### `sort()`

```cpp
list<int> L = {4,1,3,2};
L.sort();
// {1,2,3,4}
```

Descending:

```cpp
L.sort(greater<int>());
// {4,3,2,1}
```

---

### `unique()`

⚠ আগে sort করতে হবে

```cpp
list<int> L = {1,2,2,3,3};
L.sort();
L.unique();
// {1,2,3}
```

---

### `reverse()`

```cpp
L.reverse();
// list উল্টে যায়
```

---

# 🔷 6️⃣ Element Access

### `front()`

```cpp
cout << L.front();
```

---

### `back()`

```cpp
cout << L.back();
```

---

### ith element access

⚠ Direct indexing নেই

```cpp
auto it = next(L.begin(), 2);
cout << *it;
```

---

# 🔷 7️⃣ Iterators

### `begin()`

```cpp
auto it = L.begin();
cout << *it;
```

---

### `end()`

```cpp
for(auto it = L.begin(); it != L.end(); it++)
{
    cout << *it << " ";
}
```

---

# 🎯 Important Understanding

| Feature                 | List          |
| ----------------------- | ------------- |
| Random Access           | ❌ O(N)        |
| Insert/Delete Head/Tail | ✅ O(1)        |
| Memory                  | বেশি লাগে     |
| Competitive Programming | কম ব্যবহার হয় |

---

তুমি চাইলে এখন আমি:

* 🔥 প্রতিটা function এর memory level diagram
* 🔥 vector vs list deep comparison
* 🔥 Interview MCQ
* 🔥 Practice problems
* 🔥 Linked List vs STL list concept mapping

কোনটা দরকার বলো 🚀
দারুণ 🔥
আজকে আমরা **C++ STL `list` এর প্রতিটা গুরুত্বপূর্ণ function memory level diagram সহ** বুঝবো।

📌 মনে রাখো:
`std::list` = **Doubly Linked List**
প্রতিটা node এর মধ্যে থাকে:

```
[ Prev Address | Data | Next Address ]
```

---

# 🔷 1️⃣ push_back()

### Code:

```cpp
list<int> L = {1,2};
L.push_back(3);
```

### Before:

```
NULL ← [1] ⇄ [2] → NULL
```

### After:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

📌 নতুন node tail এ যুক্ত হয়
⏱ O(1)

---

# 🔷 2️⃣ push_front()

```cpp
L.push_front(0);
```

### Before:

```
NULL ← [1] ⇄ [2] → NULL
```

### After:

```
NULL ← [0] ⇄ [1] ⇄ [2] → NULL
```

📌 নতুন node head এ যুক্ত হয়
⏱ O(1)

---

# 🔷 3️⃣ pop_back()

```cpp
L.pop_back();
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [1] ⇄ [2] → NULL
```

📌 Tail node remove
⏱ O(1)

---

# 🔷 4️⃣ pop_front()

```cpp
L.pop_front();
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [2] ⇄ [3] → NULL
```

📌 Head node remove
⏱ O(1)

---

# 🔷 5️⃣ insert()

```cpp
auto it = next(L.begin(),1);
L.insert(it, 99);
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [1] ⇄ [99] ⇄ [2] ⇄ [3] → NULL
```

📌 মাঝখানে insert
📌 pointer update হয় 4 জায়গায়
⏱ O(N) (position খুঁজতে)

---

# 🔷 6️⃣ erase()

```cpp
auto it = next(L.begin(),1);
L.erase(it);
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [1] ⇄ [3] → NULL
```

📌 মাঝের node delete
⏱ O(N)

---

# 🔷 7️⃣ remove(V)

```cpp
L.remove(2);
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] ⇄ [2] → NULL
```

### After:

```
NULL ← [1] ⇄ [3] → NULL
```

📌 সব 2 delete
⏱ O(N)

---

# 🔷 8️⃣ reverse()

```cpp
L.reverse();
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [3] ⇄ [2] ⇄ [1] → NULL
```

📌 সব pointer direction swap হয়
⏱ O(N)

---

# 🔷 9️⃣ sort()

```cpp
L.sort();
```

### Before:

```
NULL ← [4] ⇄ [1] ⇄ [3] ⇄ [2] → NULL
```

### After:

```
NULL ← [1] ⇄ [2] ⇄ [3] ⇄ [4] → NULL
```

📌 Linked list এ Merge Sort use হয়
⏱ O(N log N)

---

# 🔷 🔟 unique()

```cpp
L.unique();
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

📌 Adjacent duplicate remove
⏱ O(N)

---

# 🔷 resize()

```cpp
L.resize(5);
```

### Before:

```
NULL ← [1] ⇄ [2] ⇄ [3] → NULL
```

### After:

```
NULL ← [1] ⇄ [2] ⇄ [3] ⇄ [0] ⇄ [0] → NULL
```

---

# 🔷 front() & back()

Memory change হয় না
শুধু access করে

```
front() → প্রথম node
back() → শেষ node
```

---

# 🎯 Why list insert/delete fast?

কারণ:

```
Array:
[1][2][3][4]
insert করলে shift লাগে ❌

List:
[1] ⇄ [2] ⇄ [3]
pointer update হলেই কাজ ✅
```

---

# 🚀 Final Visualization

প্রতিটা node internally এমন:

```
struct Node {
   int data;
   Node* prev;
   Node* next;
};
```

Memory layout:

```
Address 1000 → prev=NULL, data=1, next=2000
Address 2000 → prev=1000, data=2, next=3000
Address 3000 → prev=2000, data=3, next=NULL
```

---

  

1. Constructor

|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|list<type>myList;|Construct a list with 0 elements.|O(1)|
|list<type>myList(N);|Construct a list with N elements and the value will be garbage.|O(N)|
|list<type>myList(N,V);|Construct a list with N elements and the value will be V.|O(N)|
|list<type>myList(list2);|Construct a list by copying another list list2.|O(N)|
|list<type>myList(A,A+N);|Construct a list by copying all elements from an array A of size N.|O(N)|
|list<type>myList(v.begin(),v.end());|Construct a list by copying all elements from a vector v.|O(N)|

  
  

2. Capacity

|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|myList.size()|Returns the size of the list.|O(1)|
|myList.max_size()|Returns the maximum size that the list can hold.|O(1)|
|myList.clear()|Clears the list elements.|O(N)|
|myList.empty()|Return true/false if the list is empty or not.|O(1)|
|myList.resize()|Change the size of the list.|O(K); where K is the difference between new size and current size.|

  
  
  
  

3. Modifiers

|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|myList= or myList.assign(list2.begin(),list2.end())|Assign another list.|O(N)|
|myList.push_back()|Add an element to the tail.|O(1)|
|myList.push_front()|Add an element to the head.|O(1)|
|myList.pop_back()|Delete the tail.|O(1)|
|myList.pop_front()|Delete the head.|O(1)|
|myList.insert()|Insert elements at a specific position.|O(N+K); where K is the number of elements to be inserted.|
|myList.erase()|Delete elements from a specific position.|O(N+K); where K is the number of elements to be deleted.|
|replace(myList.begin(),myList.end(),value,replace_value)|Replace all the value with replace_value. Not under a list STL.|O(N)|
|find(myList.begin(),myList.end(),V)|Find the value V. Not under a list STL.|O(N)|

  
  

4. Operations

|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|myList.remove(V)|Remove the value V from the list.|O(N)|
|myList.sort()|Sort the list in ascending order.|O(NlogN)|
|myList.sort(greater<type>())|Sort the list in descending order|O(NlogN)|
|myList.unique()|Deletes the duplicate values from the list. You must sort the list first.|O(N), with sort O(NlogN)|
|myList.reverse()|Reverse the list.|O(N)|

  
  
  
  

5. Element access
    
|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|myList.back()|Access the tail element.|O(1)|
|myList.front()|Access the head element.|O(1)|
|next(myList.begin(),i)|Access the ith element|O(N)|

  
  
  
  
  
  
  
  

6. Iterators

|   |   |   |
|---|---|---|
|Name|Details|Time Complexity|
|myList.begin()|Pointer to the first element.|O(1)|
|myList.end()|Pointer to the last element.|O(1)|


