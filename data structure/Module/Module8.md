Sure! Let’s go **step by step** to understand **arrays of objects in C++**. I’ll explain with examples so it’s crystal clear.

---

## **1. What is an Array of Objects?**

In C++, an **array of objects** is simply an array where each element is an **object of a class**.

For example:

```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    int roll;
    double gpa;

    void display() {
        cout << "Name: " << name << ", Roll: " << roll << ", GPA: " << gpa << endl;
    }
};

int main() {
    // Array of 3 Student objects
    Student students[3];

    // Assign values to each object
    students[0].name = "Ati";
    students[0].roll = 1;
    students[0].gpa = 3.5;

    students[1].name = "Rahim";
    students[1].roll = 2;
    students[1].gpa = 3.8;

    students[2].name = "Karim";
    students[2].roll = 3;
    students[2].gpa = 3.2;

    // Display all students
    for (int i = 0; i < 3; i++) {
        students[i].display();
    }

    return 0;
}
```

**Output:**

```
Name: Ati, Roll: 1, GPA: 3.5
Name: Rahim, Roll: 2, GPA: 3.8
Name: Karim, Roll: 3, GPA: 3.2
```

---

## **2. Key Points**

1. **Declaration:**

   ```cpp
   ClassName arrayName[arraySize];
   ```

   Example: `Student students[5];` → creates an array of 5 `Student` objects.

2. **Accessing Objects:**
   Use **dot operator** to access data members or methods of objects in the array:

   ```cpp
   students[0].name = "John";
   students[0].display();
   ```

3. **Initialization at Declaration (C++11+):**

   ```cpp
   Student students[2] = { {"Ali", 1, 3.5}, {"Babu", 2, 3.7} };
   ```

4. **Using Loops:**
   Arrays are perfect with loops for **assigning values** or **displaying them**.

---

## **3. Array of Objects with Constructor**

You can also **initialize objects using a constructor**:

```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    int roll;
    double gpa;

    Student(string n = "", int r = 0, double g = 0.0) {
        name = n;
        roll = r;
        gpa = g;
    }

    void display() {
        cout << "Name: " << name << ", Roll: " << roll << ", GPA: " << gpa << endl;
    }
};

int main() {
    // Array of objects using constructor
    Student students[3] = { {"Ati", 1, 3.5}, {"Rahim", 2, 3.8}, {"Karim", 3, 3.2} };

    for (int i = 0; i < 3; i++) {
        students[i].display();
    }

    return 0;
}
```

---

## **4. Dynamic Array of Objects**

If you don’t know the size at compile time, use `new`:

```cpp
int n;
cout << "Enter number of students: ";
cin >> n;

Student* students = new Student[n];  // dynamic array

for (int i = 0; i < n; i++) {
    string name;
    int roll;
    double gpa;
    cout << "Enter name, roll, gpa for student " << i+1 << ": ";
    cin >> name >> roll >> gpa;
    students[i] = Student(name, roll, gpa);
}

for (int i = 0; i < n; i++) {
    students[i].display();
}

delete[] students; // free memory
```

✅ **Dynamic arrays** are useful when the number of objects is unknown at compile time.

---

### **Summary**

* An array of objects is an array where each element is an object.
* Access objects using **array index** and **dot operator**.
* Can use **loops** for input/output.
* Can initialize with **constructors**.
* Can also create **dynamic arrays** when size is unknown.

---


``` cpp
#include<bits/stdc++.h>
using namespace std;

class Student{
    public:
    string name;
    int roll;
    int marks;
};

int main(){
    
    int n;
    cin>>n;
    // Student rakib;
    Student arr[n];

    for(int i=0;i<n;i++){
        cin>>arr[i].name>>arr[i].roll>>arr[i].marks;
    }
    for (int i = 0; i < n; i++)
    {
        cout << " " << arr[i].name << " " << arr[i].roll << " " << arr[i].marks<<endl;
    }

    return 0;
}
```

I’ll **explain your code line by line**, very clearly and simply.

---

```cpp
#include<bits/stdc++.h>
```

🔹 This header file includes **almost all standard C++ libraries**
(like `iostream`, `string`, `vector`, `algorithm`, etc.)
➡ Commonly used in competitive programming.

---

```cpp
using namespace std;
```

🔹 Allows you to use standard library names (`cin`, `cout`, `string`)
**without writing `std::` every time**.

---

```cpp
class Student{
```

🔹 Defines a **class named `Student`**.
A class is a **user-defined data type**.

---

```cpp
public:
```

🔹 Access specifier.
Members under `public` can be accessed **from outside the class**.

---

```cpp
string name;
```

🔹 Data member to store **student name** (string type).

---

```cpp
int roll;
```

🔹 Data member to store **roll number**.

---

```cpp
int marks;
```

🔹 Data member to store **marks** of the student.

---

```cpp
};
```

🔹 Ends the class definition.

---

```cpp
int main(){
```

🔹 Program execution starts from the `main()` function.

---

```cpp
int n;
```

🔹 Declares an integer variable `n`
➡ It will store **number of students**.

---

```cpp
cin>>n;
```

🔹 Takes input from user and stores it in `n`.

Example input:

```
3
```

Means → there are **3 students**.

---

```cpp
Student arr[n];
```

🔹 Creates an **array of objects**
➡ `arr` is an array containing `n` objects of type `Student`.

Example:

```
arr[0], arr[1], arr[2] ...
```

Each element has:

* `name`
* `roll`
* `marks`

⚠️ Note: This is **variable length array** (works in GCC).
In standard C++, `vector<Student>` is safer.

---

```cpp
for(int i=0;i<n;i++){
```

🔹 Loop runs from `0` to `n-1`
➡ Used to input data for each student.

---

```cpp
cin>>arr[i].name>>arr[i].roll>>arr[i].marks;
```

🔹 Takes input for:

* `arr[i].name`
* `arr[i].roll`
* `arr[i].marks`

Example input:

```
Ati 1 85
```

Here:

* `arr[i].name = "Ati"`
* `arr[i].roll = 1`
* `arr[i].marks = 85`

---

```cpp
}
```

🔹 Ends the input loop.

---

```cpp
for (int i = 0; i < n; i++)
```

🔹 Another loop to **display all student data**.

---

```cpp
{
    cout << " " << arr[i].name << " " 
         << arr[i].roll << " " 
         << arr[i].marks << endl;
}
```

🔹 Prints:

* student name
* roll number
* marks
  for each object in the array.

Example output:

```
 Ati 1 85
 Rahim 2 90
 Karim 3 78
```

---

```cpp
return 0;
```

🔹 Ends the program successfully.

---

## ✅ What This Program Does (Summary)

1. Takes number of students `n`
2. Creates an **array of `Student` objects**
3. Inputs name, roll, marks for each student
4. Prints all student information

---

## 🔍 Important Concept Used

* **Class**
* **Array of Objects**
* **Loop with object access**
* **Dot operator (`.`)**

---


```cpp
#include<bits/stdc++.h>
using namespace std;

class Student{
    public:
    string name;
    int roll;
    int marks;
};

int main(){
    
    int n;
    cin>>n;
    // Student rakib;
    Student arr[n];

    for(int i=0;i<n;i++){
        cin.ignore();
        getline(cin,arr[i].name);
        cin>>arr[i].roll>>arr[i].marks;
    }
    for (int i = 0; i < n; i++)
    {
        cout << " " << arr[i].name << " " << arr[i].roll << " " << arr[i].marks<<endl;
    }

    return 0;
}
```

get input by the user name has space


## min and maximum find within array of object

```cpp
#include<bits/stdc++.h>
using namespace std;

class Student
{
public:
    string name;
    int roll;
    int marks;
};

int main(){
    int n;
    cin>>n;
    Student arr[n];
    for(int i =0; i<n;i++){
        cin>>arr[i].name>>arr[i].roll>>arr[i].marks;
    }
    Student mn;
    mn.marks=INT_MAX;

    for (int i=0;i<n;i++){
        if(arr[i].marks<mn.marks){
            mn=arr[i];
        }
    }

    cout<<mn.name<<" "<< mn.roll<<" " <<mn.marks<<" "<<endl;

    return 0;
}
```


## sort array of object
### I
```cpp
#include<bits/stdc++.h>
using namespace std;

class Student{
    public:
    string name;
    int roll;
    int marks;

};

bool cmp(Student l, Student r){
    if (l.marks<r.marks){
        return true;
    }
    return false;
}

int main(){
  int n;
  cin>>n;
  Student arr[n];
  for(int i=0;i<n;i++){
    cin>>arr[i].name>>arr[i].roll>>arr[i].marks;
  }
  sort(arr,arr+n,cmp); // cmp is custiom compare function.
  for (int i = 0; i < n; i++)
  {
      cout << " " << arr[i].name << " " << arr[i].roll << " " << arr[i].marks<<endl;
  }
    return 0;
}
```

### II

