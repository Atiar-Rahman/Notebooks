```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

int main(){
  
    Node a(10),b(20),c(30);
    

    a.next=&b;
    b.next=&c;

    // cout<<a.val<<" "<<b.val<<" "<<c.val<<endl; 
    cout<<a.val<<endl;
    cout<<a.next->val<<endl;
    cout<<a.next->next->val<<endl;
    cout<<a.next->val<<endl;

    return 0;
}
```


### **Code Breakdown**

#### 1️⃣ Includes and namespace

```cpp
#include<bits/stdc++.h>
using namespace std;
```

- `#include<bits/stdc++.h>` includes **all standard C++ libraries**.
    
- `using namespace std;` avoids writing `std::` before standard objects like `cout`.
    

---

#### 2️⃣ Node class

```cpp
class Node{
    public:
        int val;     // node value
        Node* next;  // pointer to next node

    Node(int val ){
        this->val = val;
        this->next = NULL;
    }
};
```

- You created a **Node class** for a linked list.
    
- `val` stores the **data**.
    
- `next` stores the **address of the next node**.
    
- Constructor `Node(int val)` initializes `val` and sets `next` to `NULL`.
    

---

#### 3️⃣ Creating nodes

```cpp
Node a(10), b(20), c(30);
```

- You created **three Node objects**:
    
    - `a` with value `10`
        
    - `b` with value `20`
        
    - `c` with value `30`
        
- Currently, all `next` pointers are `NULL`.
    

---

#### 4️⃣ Linking nodes

```cpp
a.next = &b;
b.next = &c;
```

- `a.next = &b;` → `a` points to `b`.
    
- `b.next = &c;` → `b` points to `c`.
    
- `c.next` is still `NULL`.
    

**Visualization:**

```
a -> b -> c -> NULL
10 -> 20 -> 30 -> NULL
```

---

#### 5️⃣ Printing values

```cpp
cout << a.val << endl;            // prints 10
cout << a.next->val << endl;      // prints 20 (a's next node value)
cout << a.next->next->val << endl;// prints 30 (b's next node value)
cout << a.next->val << endl;      // prints 20 (again a's next node)
```

**Explanation:**

- `a.val` → value of `a` node.
    
- `a.next->val` → value of node that `a` points to (which is `b`).
    
- `a.next->next->val` → value of node `b` points to (which is `c`).
    

**Output:**

```
10
20
30
20
```

---

✅ **Key Points:**

1. `Node* next` is a **pointer to the next node**.
    
2. `->` is used to **access members of a pointer object**.
    
3. You manually linked nodes instead of dynamically allocating memory (which is fine for small examples).
    

---

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};


int main(){
  
    Node* head = new Node(10);
    Node* a = new Node(20);
    Node* b = new Node(30);

    head->next=a;
    a->next=b;

    cout<<head->val<<endl;
    cout<<head->next->val<<endl;
    cout<<head->next->next->val<<endl;

    return 0;
}
```

# break Down 

### **1️⃣ Includes and namespace**

```cpp
#include<bits/stdc++.h>
using namespace std;
```

* `#include<bits/stdc++.h>` → includes all standard C++ libraries.
* `using namespace std;` → so we don’t have to write `std::` before `cout`.

---

### **2️⃣ Node class**

```cpp
class Node{
    public:
        int val;     // store node value
        Node* next;  // pointer to next node

    Node(int val ){
        this->val = val;
        this->next = NULL; // initially no next node
    }
};
```

* `Node` has:

  * `val`: the value/data of the node.
  * `next`: pointer to the next node in the linked list.
* The constructor sets the node's value and initializes `next` to `NULL`.

---

### **3️⃣ Creating nodes dynamically**

```cpp
Node* head = new Node(10);
Node* a = new Node(20);
Node* b = new Node(30);
```

* `new Node(10)` creates a node **on the heap** (dynamic memory) and returns its address.
* `head`, `a`, `b` are **pointers** to these nodes.
* Initially, all `next` pointers are `NULL`.

---

### **4️⃣ Linking nodes**

```cpp
head->next = a;
a->next = b;
```

* `head->next = a;` → the first node points to the second node.
* `a->next = b;` → the second node points to the third node.

**Memory visualization:**

```
head → Node(10) → Node(20) → Node(30) → NULL
```

* `head` points to Node 10.
* Node 10's `next` points to Node 20.
* Node 20's `next` points to Node 30.
* Node 30's `next` is `NULL` (end of list).

---

### **5️⃣ Accessing and printing node values**

```cpp
cout << head->val << endl;            // 10
cout << head->next->val << endl;      // 20
cout << head->next->next->val << endl;// 30
```

* `head->val` → value of the first node (10)
* `head->next->val` → value of the second node (20)
* `head->next->next->val` → value of the third node (30)

**Output:**

```
10
20
30
```

---

### **✅ Key Differences vs Your Previous Code**

1. **Previous code** used **stack-allocated objects**:

   ```cpp
   Node a(10), b(20), c(30);
   ```

   * Nodes are automatically destroyed when `main()` ends.

2. **Current code** uses **heap-allocated nodes**:

   ```cpp
   Node* head = new Node(10);
   ```

   * You must free memory with `delete` if needed (optional here since program ends immediately).

3. `->` is used to access members of a **pointer**, while `.` is used for **direct objects**.

---



```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};


int main(){
  
    Node* head = new Node(10);
    Node* a = new Node(20);
    Node* b = new Node(30);
    Node* c = new Node(40);

    head->next=a;
    a->next=b;
    b->next=c;

    Node* temp;
    temp=head;
    
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
    temp=head;
    while (temp != NULL)
    {
        cout << temp->val << endl;
        temp = temp->next;
    }
    return 0;
}
```


### **1️⃣ Temporary pointer**

```cpp
Node* temp;
temp = head;
```

* You created a **pointer `temp`** to traverse the linked list.
* Initially, it points to the **head of the list**.

---

### **2️⃣ First `while` loop**

```cpp
while(temp != NULL){
    cout << temp->val << endl;
    temp = temp->next;
}
```

* This **traverses the linked list** from head to the end:

  1. Checks if `temp` is not `NULL` (i.e., there is a node to visit).
  2. Prints the current node's value.
  3. Moves `temp` to the **next node** using `temp = temp->next`.

* After this loop, `temp` becomes `NULL` because it reached the end of the list.

---

### **3️⃣ Resetting `temp`**

```cpp
temp = head;
```

* Since `temp` is now `NULL`, you **reset it to the head** to traverse the list again.

---

### **4️⃣ Second `while` loop**

```cpp
while (temp != NULL)
{
    cout << temp->val << endl;
    temp = temp->next;
}
```

* This is **exactly the same traversal as before**, just printing the list **again**.
* Output will repeat all node values in order: `10 20 30 40`.

---

✅ **Key Concept Introduced: Traversal with a temporary pointer**

* `head` always points to the start of the list.
* `temp` is a **temporary pointer used to walk through the list**.
* `while(temp != NULL)` is the standard way to traverse a **singly linked list**.

---

```cpp
#include<bits/stdc++.h>
using namespace std;

void fun(int* p){
    int y=100;
    p=&y;
    // cout<<"in fun "<< *p<<endl;
}

int main(){
    int x=10;
    int* p = &x;
    fun(p);
    cout << "in main " << *p << endl;

    return 0;
}
```

Sure! Let’s carefully go **step by step** and explain what’s happening in your code. This is a **pointer and function behavior** question.

---

### **1️⃣ Function definition**

```cpp
void fun(int* p){
    int y = 100;
    p = &y;
    // cout<<"in fun "<< *p <<endl;
}
```

* `fun` takes an **integer pointer** `p` as an argument.
* Inside `fun`:

  1. `int y = 100;` → creates a **local integer variable `y`** on the **stack**.
  2. `p = &y;` → changes the **local copy of pointer `p`** to point to `y`.
* **Important:** This `p` is a **copy of the pointer** passed from `main`. Changing it inside `fun` **does NOT affect the pointer in `main`**.

---

### **2️⃣ Main function**

```cpp
int x = 10;
int* p = &x;
fun(p);
cout << "in main " << *p << endl;
```

* `x = 10;` → integer variable on the stack.
* `int* p = &x;` → `p` points to `x`.
* `fun(p);` → passes the pointer `p` **by value**.
* Inside `fun`, `p` is **changed to point to `y`**, but this change is **local to `fun`**.
* Back in `main`, `p` still points to `x`.

---

### **3️⃣ Output**

```cpp
cout << "in main " << *p << endl;
```

* `*p` → value of the variable that `p` points to.
* `p` still points to `x`, which is `10`.
* **Output:**

```
in main 10
```

---

### ✅ **Key Concepts**

1. **Pointer is passed by value**:

   * `fun(int* p)` creates a **copy** of the pointer.
   * Modifying `p` inside `fun` does **not change the original pointer** in `main`.

2. **Local variable lifetime**:

   * `y` is local to `fun`. Even if `p` in `main` somehow pointed to `y`, it would be **invalid after `fun` returns**.

3. If you wanted `fun` to modify the original pointer `p` in `main`, you would need to pass a **pointer to pointer**:

```cpp
void fun(int** p){
    int y = 100;
    *p = &y;
}
```

---




# Link list operation

##### Insertion
- at head -> O(1)
- at tail -> O(n)
- at any position -> O(n)
##### Deletion
-  at head
- at tail
- at any position
##### printing
- forward
- backward
##### sorting
- Ascending
- Descending

# insert at head

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}

void insert_at_head(Node* &head,int value){
    Node* newnode= new Node(value);

    newnode->next=head;
    head=newnode;
}

int main(){
    
    Node* head = new Node(10);
    Node* a = new Node(12);
    Node* b = new Node(14);

    head->next=a;
    a->next=b;

    insert_at_head(head,100);

    Print(head);

    return 0;
}
```


### **1️⃣ Print function**

```cpp
void Print(Node* head){
    Node* temp;
    temp = head;
    while(temp != NULL){
        cout << temp->val << endl;
        temp = temp->next;
    }
}
```

* `Print` takes the **head of a linked list**.
* It creates a **temporary pointer** `temp` to traverse the list.
* **Loop:**

  * While `temp` is not `NULL`:

    1. Print the value of the current node: `temp->val`.
    2. Move to the next node: `temp = temp->next`.
* Stops when it reaches the end (`temp == NULL`).

**Purpose:** Print all the values in the linked list **in order**.

---

### **2️⃣ insert_at_head function**

```cpp
void insert_at_head(Node* &head, int value){
    Node* newnode = new Node(value);

    newnode->next = head;
    head = newnode;
}
```

* **Arguments:** `Node* &head` → reference to the head pointer.

  * Using `&` allows the function to **modify the original head pointer** in `main`.
* `Node* newnode = new Node(value);` → create a **new node** with the given value.
* `newnode->next = head;` → new node points to the **current head**.
* `head = newnode;` → update head to be the **new node**.

**Purpose:** Insert a new node **at the beginning** of the linked list.

---

### **3️⃣ main function**

```cpp
Node* head = new Node(10);
Node* a = new Node(12);
Node* b = new Node(14);

head->next = a;
a->next = b;

insert_at_head(head, 100);

Print(head);
```

* Creates a linked list: `10 -> 12 -> 14`.
* `insert_at_head(head, 100);` → inserts `100` at the beginning:

```
100 -> 10 -> 12 -> 14
```

* `Print(head);` → prints all node values:

```
100
10
12
14
```

---

### **✅ Key Points**

1. Passing `Node* &head` by reference allows **modifying the head pointer**.
2. `new Node(value)` creates a **dynamic node** on the heap.
3. `Print` uses a **temporary pointer** to traverse without changing the actual head.

---


# insert at tail
```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}


void insert_at_tail(Node* &head,int val){
    Node* newnode = new Node(val);
    Node* temp = head;

    while(temp->next!=NULL){
        temp=temp->next;
    }
    // right now temp is at last node
    temp->next = newnode;
}

int main(){
    
    Node* head = new Node(10);
    Node* a = new Node(12);
    Node* b = new Node(14);

    head->next=a;
    a->next=b;

    insert_at_tail(head,100);

    Print(head);

    return 0;
}
```

Sure! Let’s focus on the **new part** in this code: the `insert_at_tail` function and how it works.

---

### **1️⃣ insert_at_tail function**

```cpp
void insert_at_tail(Node* &head, int val){
    Node* newnode = new Node(val);  // Step 1: create new node
    Node* temp = head;              // Step 2: start from head

    while(temp->next != NULL){      // Step 3: traverse to last node
        temp = temp->next;
    }
    // right now temp is at last node
    temp->next = newnode;           // Step 4: attach new node at end
}
```

**Step-by-step explanation:**

1. **Create a new node:**

   ```cpp
   Node* newnode = new Node(val);
   ```

   * `newnode` contains the value `val`.
   * Its `next` is `NULL` by default (end of list).

2. **Traverse to the last node:**

   ```cpp
   Node* temp = head;
   while(temp->next != NULL){
       temp = temp->next;
   }
   ```

   * Start from `head`.
   * Move `temp` forward until you reach the **node whose `next` is NULL** (the last node).

3. **Attach the new node at the end:**

   ```cpp
   temp->next = newnode;
   ```

   * Make the last node point to the new node.
   * Now `newnode` becomes the **new tail** of the list.

---

### **2️⃣ main function**

```cpp
Node* head = new Node(10);
Node* a = new Node(12);
Node* b = new Node(14);

head->next = a;
a->next = b;

insert_at_tail(head, 100);

Print(head);
```

* Original list: `10 -> 12 -> 14`
* After `insert_at_tail(head, 100);`:

```
10 -> 12 -> 14 -> 100
```

* `Print(head);` outputs:

```
10
12
14
100
```

---

### ✅ **Key Points**

1. `Node* &head` allows modifying the **head pointer** if the list is empty. (In this code, head is not empty.)
2. `while(temp->next != NULL)` ensures we **stop at the last node**.
3. New node is **always appended at the end** with `temp->next = newnode`.
4. This function **traverses the list once**, so **time complexity = O(n)**.

---

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}


void insert_at_tail(Node* &head,int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        return;
    }

    Node *temp = head;
    while(temp->next!=NULL){
        temp=temp->next;
    }
    // right now temp is at last node
    temp->next = newnode;
}

int main(){
    
    Node* head = NULL;
    insert_at_tail(head, 100);
    insert_at_tail(head, 101);
    insert_at_tail(head, 102);
    insert_at_tail(head, 103);
    Print(head);

    return 0;
}
```

# insert at any position
```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}


void insert_at_tail(Node* &head,int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        return;
    }

    Node *temp = head;
    while(temp->next!=NULL){
        temp=temp->next;
    }
    // right now temp is at last node
    temp->next = newnode;
}

void insert_at_any_position(Node* &head,int pos, int val){
    Node* newnode = new Node(val);
    if(head==NULL){
        head=newnode;
        return;
    }

    Node* temp = head;

    for(int i=0;i<pos-1;i++){
        temp=temp->next;
    }
    // temp position e
    newnode->next=temp->next;
    temp->next = newnode;
}

int main(){
    
    Node* head = NULL;
    insert_at_tail(head, 100);
    insert_at_tail(head, 101);
    insert_at_tail(head, 102);
    insert_at_tail(head, 103);
    insert_at_any_position(head,2,500);
    Print(head);

    return 0;
}
```


### **1️⃣ Updated `insert_at_tail`**

```cpp
void insert_at_tail(Node* &head,int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        return;
    }

    Node *temp = head;
    while(temp->next != NULL){
        temp = temp->next;
    }
    temp->next = newnode;
}
```

**Changes / Improvements:**

* **Handles empty list**:

  ```cpp
  if (head == NULL){
      head = newnode;
      return;
  }
  ```

  * If `head` is `NULL`, the list is empty.
  * The new node becomes the head directly.
* Otherwise, traverses the list until the **last node** and appends the new node.
* This makes the function **robust** for both empty and non-empty lists.

---

### **2️⃣ New function: `insert_at_any_position`**

```cpp
void insert_at_any_position(Node* &head,int pos, int val){
    Node* newnode = new Node(val);
    if(head == NULL){
        head = newnode;
        return;
    }

    Node* temp = head;

    for(int i = 0; i < pos - 1; i++){
        temp = temp->next;
    }
    // temp is now at position (pos-1)
    newnode->next = temp->next;
    temp->next = newnode;
}
```

**Step-by-step explanation:**

1. Create a new node:

   ```cpp
   Node* newnode = new Node(val);
   ```

2. If list is empty (`head == NULL`), make new node the head:

   ```cpp
   head = newnode;
   ```

3. Otherwise, traverse to the node **just before the desired position**:

   ```cpp
   for(int i = 0; i < pos - 1; i++){
       temp = temp->next;
   }
   ```

   * `pos` is **0-based index** (first node is position 0).
   * After loop, `temp` points to **node at position pos-1**.

4. Insert the new node:

   ```cpp
   newnode->next = temp->next; // link new node to next node
   temp->next = newnode;       // link previous node to new node
   ```

**Example:**

* Current list: `100 -> 101 -> 102 -> 103`
* Insert at `pos = 2` with `val = 500`:

```
Step 1: temp points to node 101 (position 1)
Step 2: newnode->next = temp->next → points to 102
Step 3: temp->next = newnode → now node 101 points to 500
```

* New list:

```
100 -> 101 -> 500 -> 102 -> 103
```

---

### **3️⃣ main function**

```cpp
Node* head = NULL;
insert_at_tail(head, 100);
insert_at_tail(head, 101);
insert_at_tail(head, 102);
insert_at_tail(head, 103);
insert_at_any_position(head, 2, 500);
Print(head);
```

* Start with empty list (`head = NULL`).
* Insert 100, 101, 102, 103 at tail → list: `100 -> 101 -> 102 -> 103`
* Insert 500 at position 2 → list: `100 -> 101 -> 500 -> 102 -> 103`
* `Print(head)` outputs:

```
100
101
500
102
103
```

---

### ✅ **Key Points / Takeaways**

1. `insert_at_tail` now **handles empty lists**, making it safer.
2. `insert_at_any_position` can **insert anywhere in the list**:

   * Beginning (pos=0)
   * Middle
   * End
3. Always traverse to the **node before the desired position**.
4. **Pointer manipulation** is key: adjust `next` pointers carefully.
5. Using `Node* &head` ensures we can **update head** if needed.

---



# linked list user input

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}


void insert_at_tail(Node* &head,Node* &tail, int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    tail->next = newnode;
    tail = newnode;

}


int main(){
    
    Node* head = NULL;
    Node* tail = NULL;

    int val;
    while(true){
        cin>> val;
        if(val==-1){
            break;
        }
        insert_at_tail(head,tail,val);
    }
    Print(head);
    return 0;
}
```

## Explain code
## **1️⃣ Node class**

```cpp
class Node{
public:
    int val;     // value of the node
    Node* next;  // pointer to next node

    Node(int val ){
        this->val = val;
        this->next = NULL;
    }
};
```

* Each node stores a value and a pointer to the next node.
* Constructor sets the value and initializes `next` to `NULL`.

---

## **2️⃣ Print function**

```cpp
void Print(Node* head){
    Node* temp = head;
    while(temp != NULL){
        cout << temp->val << endl;
        temp = temp->next;
    }
}
```

* `temp` is used to **traverse the list**.
* Prints all node values in order.
* Stops when `temp` reaches `NULL` (end of list).

---

## **3️⃣ insert_at_tail function**

```cpp
void insert_at_tail(Node* &head, Node* &tail, int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    tail->next = newnode;
    tail = newnode;
}
```

**Step by step:**

1. **Create a new node**:

   ```cpp
   Node* newnode = new Node(val);
   ```

   * Its `next` is `NULL`.

2. **Check if the list is empty**:

   ```cpp
   if (head == NULL){
       head = newnode;
       tail = newnode;
       return;
   }
   ```

   * If empty, **both head and tail point to the new node**.

3. **Otherwise, append to the tail**:

   ```cpp
   tail->next = newnode; // last node points to new node
   tail = newnode;       // move tail pointer to new last node
   ```

   * Updating `tail` by reference ensures **next insertion is O(1)**.

---

## **4️⃣ main function**

```cpp
Node* head = NULL;
Node* tail = NULL;

int val;
while(true){
    cin >> val;
    if(val == -1) break;
    insert_at_tail(head, tail, val);
}

Print(head);
```

**Step by step:**

1. Start with **empty list** (`head = NULL`, `tail = NULL`).
2. Read values from input until `-1`.
3. For each value, **insert at tail** in **O(1)** time.
4. After reading all values, print the list.

**Example input:**

```
10 20 30 -1
```

**Output:**

```
10
20
30
```

---

## ✅ **Key Points**

1. `Node* &head` and `Node* &tail` → **passed by reference** to allow modifying the original pointers.
2. Using a **tail pointer** makes tail insertion **O(1)** instead of O(n).
3. Handles **empty list** automatically.
4. `Print` traverses safely until `NULL`.

---

# Reverse Print

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node{
    public:
        int val;//node value
        Node* next;//next value address

    Node(int val ){
        this->val=val;
        this->next=NULL;
    }
};

void Print(Node* head){
    Node* temp;
    temp=head;
    while(temp!=NULL){
        cout<<temp->val<<endl;
        temp = temp->next;
    }
}


void ReversePrint(Node* temp){
    
    // base case
    if(temp==NULL){
        return;
    }
    ReversePrint(temp->next);
    cout<<temp->val<<endl;
}


void insert_at_tail(Node* &head,Node* &tail, int val){
   
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    tail->next = newnode;
    tail = newnode;

}


int main(){
    
    Node* head = NULL;
    Node* tail = NULL;

    int val;
    while(true){
        cin>> val;
        if(val==-1){
            break;
        }
        insert_at_tail(head,tail,val);
    }
    ReversePrint(head);
    return 0;
}
```

## 1️⃣ `ReversePrint` function (MAIN NEW CONCEPT)

```cpp
void ReversePrint(Node* temp){
    
    // base case
    if(temp == NULL){
        return;
    }
    ReversePrint(temp->next);
    cout << temp->val << endl;
}
```

### 🔹 How it works

This function prints the linked list **in reverse order** using **recursion**.

#### Step-by-step logic:

1. **Base case**

   ```cpp
   if(temp == NULL) return;
   ```

   * Stops recursion when the end of the list is reached.

2. **Recursive call**

   ```cpp
   ReversePrint(temp->next);
   ```

   * Keeps calling itself until `temp` becomes `NULL`.
   * This moves recursion **forward to the last node first**.

3. **Print while returning**

   ```cpp
   cout << temp->val << endl;
   ```

   * Printing happens **after** the recursive call.
   * So values are printed while recursion **unwinds**, i.e., in reverse order.

---

### 🔁 Example Execution

If the list is:

```
10 → 20 → 30 → NULL
```

Call stack goes like:

```
ReversePrint(10)
 → ReversePrint(20)
   → ReversePrint(30)
     → ReversePrint(NULL)  // stop
```

Now printing starts:

```
30
20
10
```

✅ **No pointers are changed**
✅ **List structure remains the same**

---

## 2️⃣ `insert_at_tail` (unchanged but important)

```cpp
void insert_at_tail(Node* &head, Node* &tail, int val){
    Node* newnode = new Node(val);

    if (head == NULL){
        head = newnode;
        tail = newnode;
        return;
    }

    tail->next = newnode;
    tail = newnode;
}
```

* Inserts nodes in **O(1)** time using `tail`.
* Handles empty list correctly.

---

## 3️⃣ `main` function

```cpp
Node* head = NULL;
Node* tail = NULL;

int val;
while(true){
    cin >> val;
    if(val == -1){
        break;
    }
    insert_at_tail(head, tail, val);
}

ReversePrint(head);
```

### What happens:

1. Builds a linked list from user input until `-1`.
2. Calls `ReversePrint(head)` to print values **from last to first**.

---

## 🧪 Example Input

```
10 20 30 40 -1
```

### Output

```
40
30
20
10
```

---

## ✅ Key Takeaways

* `ReversePrint` uses **recursion**, not pointer reversal.
* Printing happens **after recursive calls**, causing reverse order.
* Time complexity: **O(n)**
* Extra space: **O(n)** (call stack)
* Linked list remains unchanged.

---

