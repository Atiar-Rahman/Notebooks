
# ✅ **Static Memory vs Heap Memory**

## 🟦 **Static Memory (Static / Global / Compile-time Memory)**

### **Where it is stored?**

- Stored in the **static/global memory area** (also called _Data Segment_).
    

### **Who allocates it?**

- Allocated **at compile time** or **program start**.
    
- Deallocated **automatically when the program ends**.
    

### **How to allocate?**

- Global variables
    
- Static local variables
    
- Static class members
    

### **Examples**

```cpp
int x = 10;          // global → static memory
static int y = 5;    // static local → static memory

void fun() {
    static int count = 0; // persists across function calls
}
```

### **Properties**

- Fixed size (known at compile time)
    
- Lifetime = entire program run
    
- Not flexible
    
- Faster access
    

---

# 🟩 **Heap Memory (Dynamic Memory)**

### **Where it is stored?**

- Stored in the **heap region**.
    

### **Who allocates it?**

- Developer manually allocates.
    
- Must manually **free the memory**.
    

### **How to allocate?**

C:

```c
int* p = (int*) malloc(sizeof(int));
free(p);
```

C++:

```cpp
int* p = new int;
delete p;
```

### **Properties**

- Size decided at runtime (flexible)
    
- Slower than static memory
    
- If not freed → **memory leak**
    
- Good for:
    
    - Large data
        
    - Unknown size data
        
    - Long-lived objects
        

---

# 📌 Key Differences

|Feature|Static Memory|Heap Memory|
|---|---|---|
|Allocation|Compile time|Runtime|
|Lifetime|Whole program|Until `free`/`delete`|
|Size|Fixed|Flexible|
|Speed|Fast|Slower|
|Location|Data Segment|Heap|
|Management|Automatic|Manual|

---

# 🧠 Short Summary

- **Static memory** → allocated once, lasts forever, no manual delete.
    
- **Heap memory** → you control, flexible, must `free()` or `delete`.
    

---

In C++, you can declare **dynamic variables** using the **heap** with the `new` keyword.  
Dynamic variables are created at **runtime**, and you control their lifetime.

---

# ✅ **Dynamic Variable Declaration in C++**

## 1️⃣ **Dynamic integer**

```cpp
int* p = new int;     // allocate memory
*p = 10;              // assign value
cout << *p;           // use value
delete p;             // free memory
```

---

## 2️⃣ **Dynamic array**

```cpp
int* arr = new int[5];   // array of size 5 created at runtime

arr[0] = 10;
arr[1] = 20;

delete[] arr;            // free array memory
```

---

## 3️⃣ **Dynamic object**

```cpp
class Student {
public:
    int id;
};

Student* s = new Student;  
s->id = 101;

delete s;
```

---

# 📌 Rules to Remember

### ✅ Use `new` to allocate

### ❌ Always use `delete` (or `delete[]` for arrays)

### ⚠️ Forgetting `delete` → **memory leak**

---

# 🟦 Full Example

```cpp
#include <iostream>
using namespace std;

int main() {
    // dynamic int
    int* x = new int;
    *x = 50;
    cout << "Value: " << *x << endl;

    // dynamic array
    int n;
    cout << "Enter size: ";
    cin >> n;

    int* arr = new int[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    delete x;
    delete[] arr;
}
```

---
In C++, **you cannot directly increase the size of a dynamic array** created with `new[]`.  
But you _can_ resize it by creating a new bigger array and copying the old elements.

---

# ✅ **Method 1: Manually Resize Dynamic Array**

### Steps:

1. Create a new array with bigger size
    
2. Copy old data
    
3. Delete old array
    
4. Point to new array
    

### Example:

```cpp
int* resizeArray(int* arr, int oldSize, int newSize) {
    int* newArr = new int[newSize];

    // copy old elements
    for (int i = 0; i < oldSize; i++) {
        newArr[i] = arr[i];
    }

    delete[] arr; // free old memory
    return newArr; // return new pointer
}

int main() {
    int size = 3;
    int* arr = new int[size];

    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;

    // increase size
    int newSize = 5;
    arr = resizeArray(arr, size, newSize);

    arr[3] = 40;
    arr[4] = 50;

    for (int i = 0; i < newSize; i++) {
        cout << arr[i] << " ";
    }

    delete[] arr;
}
```

---

# ✅ **Method 2: Use `std::vector` (Recommended)**

Best and safest way — it does resizing automatically.

```cpp
#include <vector>

vector<int> arr;
arr.push_back(10);
arr.push_back(20);

// increase size
arr.resize(5);

// add more values
arr[3] = 40;
arr[4] = 50;
```

Advantages of vector:

- Auto resizing
    
- No manual memory management
    
- No memory leaks
    
- Faster and safer
    

---

# 🟦 Summary

|Method|How|
|---|---|
|Manual|Create new array → copy elements → delete old array|
|Best way|Use `std::vector`|

---

