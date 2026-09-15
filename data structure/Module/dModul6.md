Doubly linked list operation

Insertion:
- at head
- at tail
- at any position
Deletion:
- at head
- at tail
- at any position
printing:
- forward
- backward
Input: 
Array vs singly vs doubly



# What is Doubly link list

A **doubly linked list (DLL)** is a type of **linked data structure** where each node contains **three parts**:

1. **Data** – stores the actual value.
    
2. **Pointer to the next node** – links to the node after the current one.
    
3. **Pointer to the previous node** – links to the node before the current one.
    

This allows traversal **both forward and backward**, unlike a **singly linked list** which can only be traversed forward.

### Structure of a Node in Doubly Linked List

```
+---------+-----------+-----------+
| Prev Ptr|   Data    | Next Ptr  |
+---------+-----------+-----------+
```

- **Prev Ptr** → points to the previous node (or `NULL` if it's the first node).
    
- **Data** → contains the value.
    
- **Next Ptr** → points to the next node (or `NULL` if it's the last node).
    

### Example (Forward and Backward)

Suppose we have nodes containing 10, 20, 30:

**Forward traversal:** 10 → 20 → 30  
**Backward traversal:** 30 → 20 → 10

### Advantages

- Can traverse both ways (forward and backward).
    
- Easier to insert or delete a node from **any position** compared to singly linked lists.
    

### Disadvantages

- Uses extra memory for the `prev` pointer.
    
- Slightly more complex to implement.
    

### Operations

|Operation|Complexity|
|---|---|
|Insertion at beginning|O(1)|
|Insertion at end|O(1) if tail is known, else O(n)|
|Deletion|O(1) if node reference known, else O(n)|
|Traversal|O(n)|

``` cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address
        Node* prev;//previous value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}

void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
    
}

int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  Forward(head);
  Backward(c);
  return 0;
}
```


**doubly linked list (DLL) C++ code**. I’ll break it down into sections.

---

## 1️⃣ **Node Class Definition**

```cpp
class Node{
    public:
        int val;       // stores the value of the node
        Node* next;    // pointer to the next node
        Node* prev;    // pointer to the previous node

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
```

**Explanation:**

* We define a `Node` class to represent each element of the doubly linked list.
* Each node has three parts:

  * `val` → stores the value (like 10, 20, 30…).
  * `next` → pointer to the next node in the list.
  * `prev` → pointer to the previous node in the list.
* The constructor `Node(int val)` initializes the node’s value and sets both `next` and `prev` to `NULL` initially.

---

## 2️⃣ **Forward Traversal Function**

```cpp
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}
```

**Step-by-step:**

* Start at the `head` of the list.
* Use a temporary pointer `temp` to traverse.
* While `temp` is not `NULL`:

  * Print `temp->val` (current node value).
  * Move to the next node using `temp = temp->next`.
* This prints the list **from head to tail**.

---

## 3️⃣ **Backward Traversal Function**

```cpp
void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
}
```

**Step-by-step:**

* Start at the `tail` of the list.
* Use a temporary pointer `temp` to traverse backward.
* While `temp` is not `NULL`:

  * Print `temp->val` (current node value).
  * Move to the previous node using `temp = temp->prev`.
* This prints the list **from tail to head**.

---

## 4️⃣ **Main Function**

```cpp
int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  Forward(head);
  Backward(c);
  return 0;
}
```

**Step-by-step:**

1. **Create nodes**

```cpp
Node* head = new Node(10);
Node* a = new Node(20);
Node* b = new Node(30);
Node* c = new Node(40);
```

* Four nodes are created with values 10, 20, 30, 40.

2. **Link nodes forward and backward**

```cpp
head->next = a; // 10 → 20
a->prev = head; // 20 ← 10

a->next = b;    // 20 → 30
b->prev = a;    // 30 ← 20

b->next = c;    // 30 → 40
c->prev = b;    // 40 ← 30
```

* Now the list is **fully connected** as a doubly linked list:

```
NULL <- 10 <-> 20 <-> 30 <-> 40 -> NULL
```

3. **Traverse forward**

```cpp
Forward(head); 
```

* Prints: `10 20 30 40`

4. **Traverse backward**

```cpp
Backward(c);
```

* Prints: `40 30 20 10`

---

✅ **Final Output:**

```
10 20 30 40 40 30 20 10
```

* First four numbers → forward traversal
* Last four numbers → backward traversal

---

# Insert at head

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address
        Node* prev;//previous value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}

void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
    
}

void Insert_at_head(Node* &head,int val){
    Node* newnode = new Node(val);

    newnode->next=head;
    head->prev=newnode;
    head = newnode;

}

int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  Insert_at_head(head,45);
  Forward(head);
//   Backward(c);
  return 0;
}
```

The **new part** in your code is the function:

```cpp
void Insert_at_head(Node* &head,int val){
    Node* newnode = new Node(val);

    newnode->next=head;
    head->prev=newnode;
    head = newnode;
}
```

Let’s break it down **step by step**:

---

### 1️⃣ **Function Purpose**

`Insert_at_head` adds a **new node at the beginning** of the doubly linked list.

* The list head is updated to point to this new node.
* The previous first node’s `prev` pointer is updated to point back to the new node.

---

### 2️⃣ **Step-by-step Execution**

1. **Create a new node**

```cpp
Node* newnode = new Node(val);
```

* A new node is created with the value `val` (in your case, 45).
* Its `next` and `prev` pointers are initially `NULL`.

---

2. **Link new node to current head**

```cpp
newnode->next = head;
```

* The new node’s `next` now points to the **current head node** (which had value 10).

---

3. **Link old head back to new node**

```cpp
head->prev = newnode;
```

* The old head node’s `prev` now points to the new node.
* This keeps the doubly linked list **bidirectionally linked**.

---

4. **Update head pointer**

```cpp
head = newnode;
```

* The `head` of the list is updated to the new node.
* Now 45 becomes the **first node** in the list.

---

### ✅ **Before and After**

**Before insertion:**

```
10 <-> 20 <-> 30 <-> 40
```

**After `Insert_at_head(head, 45)`:**

```
45 <-> 10 <-> 20 <-> 30 <-> 40
```

* Forward traversal now prints: `45 10 20 30 40`

---


# Insert at tail

``` cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address
        Node* prev;//previous value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}

void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
    
}

void Insert_at_head(Node* &head,Node* &tail,int val){
    Node* newnode = new Node(val);
    
    if(head==NULL){
        head = newnode;
        tail = newnode;
        return;
    }
    newnode->next=head;
    head->prev=newnode;
    head = newnode;

}

void Insert_at_tail(Node* & head,Node* &tail,int val){
    Node* newnode = new Node(100);

    if(head==NULL){
        head = newnode;
        tail = newnode;
        return;
    }
    tail->next = newnode;
    newnode->prev = tail;
    tail = newnode;
}

int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  Insert_at_head(head,c,45);
  Insert_at_tail(head,c,34);
  Forward(head);
//   Backward(c);
  return 0;
}
```

the **Insert at head** and **Insert at tail** functions. Here’s a clear explanation:

---

### 1️⃣ **Insert at Head**

```cpp
void Insert_at_head(Node* &head, Node* &tail, int val){
    Node* newnode = new Node(val);
    
    if(head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    newnode->next = head; // new node points to current head
    head->prev = newnode; // old head points back to new node
    head = newnode;       // update head to new node
}
```

**Explanation (step by step):**

1. **Create a new node** with the given value.
2. **Check if list is empty**:

   * If yes → make new node both head and tail.
3. **Otherwise**:

   * Link `newnode->next` to current head.
   * Link current head’s `prev` to new node.
   * Update `head` to point to new node.

**Effect:** Adds a node at the **start** of the doubly linked list.

---

### 2️⃣ **Insert at Tail**

```cpp
void Insert_at_tail(Node* &head, Node* &tail, int val){
    Node* newnode = new Node(val);

    if(head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    tail->next = newnode; // old tail points to new node
    newnode->prev = tail; // new node points back to old tail
    tail = newnode;       // update tail to new node
}
```

**Explanation (step by step):**

1. **Create a new node** with the given value.
2. **Check if list is empty**:

   * If yes → make new node both head and tail.
3. **Otherwise**:

   * Link old tail’s `next` to new node.
   * Link new node’s `prev` to old tail.
   * Update `tail` to point to new node.

**Effect:** Adds a node at the **end** of the doubly linked list.

---

✅ **Key points about the new part:**

* Both functions take **head and tail by reference** so they can update the actual pointers.
* They handle **empty list** case gracefully.
* Maintains **bidirectional links** (`next` and `prev`) correctly.

---



# Insert at any position

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address
        Node* prev;//previous value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}

void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
    
}

void Insert_at_head(Node* &head,Node* &tail,int val){
    Node* newnode = new Node(val);
    
    if(head==NULL){
        head = newnode;
        tail = newnode;
        return;
    }
    newnode->next=head;
    head->prev=newnode;
    head = newnode;

}

void Insert_at_tail(Node* & head,Node* &tail,int val){
    Node* newnode = new Node(100);

    if(head==NULL){
        head = newnode;
        tail = newnode;
        return;
    }
    tail->next = newnode;
    newnode->prev = tail;
    tail = newnode;
}

void Insert_at_any_position(Node* &head,Node* &tail, int pos,int val){
    Node* newnode = new Node(val);

    Node* temp = head;
    for(int i=0;i<pos;i++){
        temp = temp->next;
    }

    newnode->next = temp->next;
    temp->next->prev = newnode;

    temp->next = newnode;
    newnode->prev = temp;
}

int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  Insert_at_head(head,c,45);
  Insert_at_tail(head,c,34);
  Insert_at_any_position(head,c,2,500);
  Forward(head);
//   Backward(c);
  return 0;
}
```

this code is the **`Insert_at_any_position`** function. Let’s break it **step by step**.

---

### 1️⃣ **Function: Insert at Any Position**

```cpp
void Insert_at_any_position(Node* &head, Node* &tail, int pos, int val){
    Node* newnode = new Node(val);  // create new node

    Node* temp = head;
    for(int i = 0; i < pos; i++){
        temp = temp->next;          // move temp to the node after which we want to insert
    }

    newnode->next = temp->next;     // new node points to temp's next node
    temp->next->prev = newnode;     // next node's prev points to new node

    temp->next = newnode;           // temp's next points to new node
    newnode->prev = temp;           // new node's prev points to temp
}
```

---

### 2️⃣ **Step-by-Step Explanation**

1. **Create a new node** with value `val`.

   ```cpp
   Node* newnode = new Node(val);
   ```

2. **Move to the position where to insert**

   ```cpp
   Node* temp = head;
   for(int i=0; i<pos; i++){
       temp = temp->next;
   }
   ```

   * `temp` points to the node **after which** we want to insert the new node.
   * `pos` is **0-based index** (0 → first node, 1 → second node, …).

3. **Link new node with the next node**

   ```cpp
   newnode->next = temp->next;
   temp->next->prev = newnode;
   ```

   * `newnode->next` points to the node after `temp`.
   * The next node’s `prev` is updated to point back to the new node.

4. **Link new node with the previous node**

   ```cpp
   temp->next = newnode;
   newnode->prev = temp;
   ```

   * `temp->next` now points to the new node.
   * `newnode->prev` points to `temp`.

✅ **Effect:** The new node is inserted **between two existing nodes**.

---

### 3️⃣ **Example**

Original list (after head and tail insertion):

```
45 <-> 10 <-> 20 <-> 30 <-> 40 <-> 34
```

Call:

```cpp
Insert_at_any_position(head, c, 2, 500);
```

* `pos = 2` → we move 2 steps from head: 45 → 10 → 20
* Insert 500 **after node 20**

**Updated list:**

```
45 <-> 10 <-> 20 <-> 500 <-> 30 <-> 40 <-> 34
```

---

### 4️⃣ **Key Points**

* Works **only for positions in the middle** (not head or tail).
* Must ensure `temp->next` exists, otherwise it may crash at the end.
* After insertion, all `next` and `prev` pointers are **correctly updated**, so the DLL stays consistent.

---
# delete at head

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address
        Node* prev;//previous value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
        this->prev=NULL;
    }
};
void Forward(Node* head){
    Node* temp=head;
    while(temp!=NULL){
        cout<<temp->val<<" ";
        temp=temp->next;
    }
}

void Backward(Node* tail){
    Node* temp = tail;
    while (temp!=NULL)
    {
        cout<<temp->val<<" ";
        temp=temp->prev;
    }
    
}

void delete_at_head(Node* &head,Node* tail){
    Node* deleteNode = head;
    head=head->next;
    delete deleteNode;
    if(head==NULL){
        tail = NULL;
        return;
    }
    head->prev=NULL;
    
}

int main(){
  Node* head = new Node(10);
  Node* a = new Node(20);
  Node* b = new Node(30);
  Node* c = new Node(40);

  head->next=a;
  a->prev=head;
  a->next=b;
  b->prev=a;
  b->next=c;
  c->prev=b;

  
  delete_at_head(head,c);
  Forward(head);
//   Backward(c);
  return 0;
}
```

### Explain


---

### 1️⃣ **Function: Delete at Head**

```cpp
void delete_at_head(Node* &head, Node* tail){
    Node* deleteNode = head;       // store the current head to delete
    head = head->next;             // move head to the next node
    delete deleteNode;             // free memory of old head

    if(head == NULL){              // if list became empty
        tail = NULL;
        return;
    }

    head->prev = NULL;             // new head's prev must be NULL
}
```

---

### 2️⃣ **Step-by-Step Explanation**

1. **Store current head node to delete**

```cpp
Node* deleteNode = head;
```

* We need to free memory of the old head after moving the head pointer.

2. **Move head to the next node**

```cpp
head = head->next;
```

* Now `head` points to the second node in the list.

3. **Delete the old head node**

```cpp
delete deleteNode;
```

* Frees memory occupied by the original head.

4. **Check if list is now empty**

```cpp
if(head == NULL){
    tail = NULL;
    return;
}
```

* If there was only one node, after deletion the list becomes empty.
* Both `head` and `tail` should now be `NULL`.

5. **Update the new head’s prev pointer**

```cpp
head->prev = NULL;
```

* The new head node has **no previous node**, so `prev` must be `NULL`.

---

### 3️⃣ **Before Deletion**

Original list:

```
10 <-> 20 <-> 30 <-> 40
head → 10
tail → 40
```

---

### 4️⃣ **After `delete_at_head(head, c);`**

* Node `10` is deleted.
* `head` now points to `20`.
* `prev` of new head (`20`) is `NULL`.

Updated list:

```
20 <-> 30 <-> 40
head → 20
tail → 40
```

---

### 5️⃣ **Forward Traversal Output**

```cpp
Forward(head);
```

Prints:

```
20 30 40
```

---

### ⚠️ **Note**

* Your function **doesn’t update `tail` properly** if there’s only one node left, because `tail` is passed **by value**, not reference.
* To fix this, you should pass `tail` as reference:

```cpp
void delete_at_head(Node* &head, Node* &tail){ ... }
```

This ensures that `tail` in the main function is updated when the list becomes empty.

---

