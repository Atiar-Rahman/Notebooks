Absolutely. Here’s a **complete beginner-to-advanced C++ course roadmap** you can follow in order.

## C++ Complete Course

### 1. Getting Started

Learn:

- What C++ is
    
- Installing a compiler/IDE
    
- `main()`
    
- `#include`
    
- `cout` and `cin`
    
- Comments
    
- Compilation and execution
    

Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

---

### 2. Variables & Data Types

Learn:

- `int`
    
- `float`
    
- `double`
    
- `char`
    
- `bool`
    
- `string`
    
- Constants
    
- Variable declaration and initialization
    

```cpp
int age = 15;
double price = 99.5;
char grade = 'A';
bool passed = true;
string name = "Alex";
```

---

### 3. Input & Output

Learn:

- `cout`
    
- `cin`
    
- `getline()`
    
- Multiple inputs
    

```cpp
string name;
int age;

cout << "Name: ";
getline(cin, name);

cout << "Age: ";
cin >> age;
```

---

### 4. Operators

Learn:

- Arithmetic: `+ - * / %`
    
- Assignment: `= += -= *= /=`
    
- Comparison: `== != > < >= <=`
    
- Logical: `&& || !`
    
- Increment/decrement: `++ --`
    

---

### 5. Conditions

Learn:

- `if`
    
- `else`
    
- `else if`
    
- Nested conditions
    
- `switch`
    

```cpp
int age;
cin >> age;

if (age >= 18)
    cout << "Adult";
else
    cout << "Minor";
```

---

### 6. Loops

Master:

- `for`
    
- `while`
    
- `do while`
    
- `break`
    
- `continue`
    

```cpp
for (int i = 1; i <= 10; i++) {
    cout << i << '\n';
}
```

Practice problems:

1. Print 1–100
    
2. Print even numbers
    
3. Multiplication table
    
4. Sum of numbers
    
5. Factorial
    
6. Reverse a number
    
7. Check palindrome
    
8. Check prime number
    

---

### 7. Functions

Learn:

- Creating functions
    
- Parameters
    
- Return values
    
- Function overloading
    
- Default arguments
    
- Scope
    

```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    cout << add(5, 3);
}
```

---

### 8. Arrays

Learn:

- One-dimensional arrays
    
- Two-dimensional arrays
    
- Traversing arrays
    
- Finding max/min
    
- Searching
    
- Sorting basics
    

```cpp
int numbers[5] = {10, 20, 30, 40, 50};

for (int i = 0; i < 5; i++) {
    cout << numbers[i] << '\n';
}
```

---

### 9. Strings

Learn:

- `string`
    
- String indexing
    
- `length()`
    
- `substr()`
    
- `find()`
    
- String comparison
    
- Character manipulation
    

---

### 10. Pointers

This is an important C++ topic.

Learn:

- Addresses
    
- `&`
    
- `*`
    
- Pointer variables
    
- Pointers and arrays
    
- Pointers and functions
    
- `nullptr`
    

```cpp
int x = 10;
int* p = &x;

cout << x << '\n';
cout << *p << '\n';
```

---

### 11. References

Learn:

- Reference variables
    
- Pass by reference
    
- References vs pointers
    

```cpp
void change(int& x) {
    x = 100;
}
```

---

### 12. Dynamic Memory

Learn the concepts behind:

- `new`
    
- `delete`
    
- Dynamic arrays
    
- Why modern C++ generally prefers smart pointers and containers
    

---

# Object-Oriented Programming

### 13. Classes & Objects

Learn:

- Classes
    
- Objects
    
- Data members
    
- Member functions
    
- `public`
    
- `private`
    
- `protected`
    

```cpp
class Student {
public:
    string name;
    int age;

    void introduce() {
        cout << name << " " << age;
    }
};
```

---

### 14. Constructors & Destructors

Learn:

- Default constructor
    
- Parameterized constructor
    
- Constructor overloading
    
- Destructor
    
- Initialization lists
    

---

### 15. Encapsulation

Learn:

- Private data
    
- Getters
    
- Setters
    
- Data protection
    

---

### 16. Inheritance

Learn:

- Base class
    
- Derived class
    
- Single inheritance
    
- Multilevel inheritance
    
- Multiple inheritance
    
- Hierarchical inheritance
    

---

### 17. Polymorphism

Learn:

- Function overloading
    
- Operator overloading
    
- Function overriding
    
- Virtual functions
    
- Runtime polymorphism
    

---

### 18. Abstraction

Learn:

- Abstract classes
    
- Pure virtual functions
    
- Interfaces using classes
    

---

# Modern C++

### 19. STL — Standard Template Library

This is **extremely important** for competitive programming and professional C++.

Learn:

**Containers**

- `vector`
    
- `array`
    
- `deque`
    
- `list`
    
- `stack`
    
- `queue`
    
- `priority_queue`
    
- `set`
    
- `multiset`
    
- `map`
    
- `multimap`
    
- `unordered_set`
    
- `unordered_map`
    

Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> nums = {10, 20, 30};

    nums.push_back(40);

    for (int x : nums)
        cout << x << ' ';
}
```

---

### 20. Iterators

Learn:

- `begin()`
    
- `end()`
    
- `rbegin()`
    
- `rend()`
    
- Iterator operations
    
- Range-based loops
    

---

### 21. STL Algorithms

Master:

- `sort()`
    
- `reverse()`
    
- `find()`
    
- `count()`
    
- `max_element()`
    
- `min_element()`
    
- `binary_search()`
    
- `lower_bound()`
    
- `upper_bound()`
    

---

### 22. Lambda Functions

```cpp
auto square = [](int x) {
    return x * x;
};

cout << square(5);
```

---

### 23. Exception Handling

Learn:

- `try`
    
- `catch`
    
- `throw`
    
- Custom exceptions
    

---

### 24. File Handling

Learn:

- `ofstream`
    
- `ifstream`
    
- `fstream`
    
- Reading files
    
- Writing files
    

---

### 25. Templates

Learn:

- Function templates
    
- Class templates
    
- Generic programming
    

```cpp
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}
```

---

### 26. Smart Pointers

Learn:

- `unique_ptr`
    
- `shared_ptr`
    
- `weak_ptr`
    
- RAII
    
- Ownership
    

These are important in modern C++.

---

# Data Structures & Algorithms

After learning the language, move into DSA.

### 27. Complexity

Learn:

- Big O
    
- Big Ω
    
- Big Θ
    
- Time complexity
    
- Space complexity
    

---

### 28. Searching

- Linear search
    
- Binary search
    

---

### 29. Sorting

- Bubble sort
    
- Selection sort
    
- Insertion sort
    
- Merge sort
    
- Quick sort
    
- Heap sort
    
- STL sorting
    

---

### 30. Linked Lists

Learn:

- Singly linked list
    
- Doubly linked list
    
- Circular linked list
    
- Insertion
    
- Deletion
    
- Searching
    
- Reversal
    

---

### 31. Stack & Queue

Learn:

- Stack
    
- Queue
    
- Deque
    
- Applications
    

---

### 32. Recursion

Learn:

- Base case
    
- Recursive case
    
- Factorial
    
- Fibonacci
    
- Backtracking
    

---

### 33. Trees

Learn:

- Binary trees
    
- Binary search trees
    
- Tree traversal
    
    - Preorder
        
    - Inorder
        
    - Postorder
        
- Height
    
- Balanced trees
    
- Heaps
    

---

### 34. Graphs

Learn:

- Vertices and edges
    
- Directed/undirected graphs
    
- Weighted graphs
    
- Adjacency matrix
    
- Adjacency list
    
- BFS
    
- DFS
    

---

### 35. Advanced Algorithms

Learn:

- Greedy algorithms
    
- Divide and conquer
    
- Dynamic programming
    
- Backtracking
    
- Dijkstra
    
- Floyd–Warshall
    
- Minimum spanning trees
    
- Topological sorting
    

---

# Projects

Don't only watch tutorials—**build projects**.

### Beginner

1. Calculator
    
2. Number guessing game
    
3. Unit converter
    
4. Simple quiz
    
5. Student grade calculator
    

### Intermediate

6. Bank account simulator
    
7. Contact manager
    
8. Library management system
    
9. Expense tracker
    
10. Tic-Tac-Toe
    

### Advanced

11. File-based student management system
    
12. Inventory management system
    
13. Chess game
    
14. Graph algorithm visualizer
    
15. Command-line text editor
    

---

## Recommended Learning Order

**C++ Basics → Control Flow → Functions → Arrays → Strings → Pointers → OOP → STL → Modern C++ → DSA → Projects**

A good rule is:

> **Learn a concept → write code → solve 5–10 problems → build a small project → move on.**




---

# Lesson 1 — C++ Basics

Welcome to **C++ Lesson 1**. We'll start from absolute zero.

## 1. What is C++?

**C++** is a programming language used to build things such as:

- Games
    
- Desktop applications
    
- Operating systems
    
- Embedded software
    
- High-performance programs
    
- Competitive programming solutions
    

A C++ program is written as text and then **compiled** into a program the computer can execute.

---

## 2. Your First C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

Let's understand every part.

### `#include <iostream>`

This gives our program access to input/output features such as `cout` and `cin`.

### `using namespace std;`

This lets us write:

```cpp
cout
```

instead of:

```cpp
std::cout
```

### `int main()`

`main()` is where the program starts executing.

```cpp
int main() {
    
}
```

The `{ }` contain the instructions belonging to `main()`.

### `cout`

`cout` displays something on the screen.

```cpp
cout << "Hello";
```

Output:

```text
Hello
```

### `return 0;`

This tells the operating system that the program finished successfully.

---

# 3. Statements

Most C++ instructions end with a semicolon `;`.

```cpp
cout << "Hello";
cout << "World";
```

Forgetting the semicolon is a very common beginner error.

---

# 4. Printing Multiple Things

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "My name is Alex.";
    cout << "I am learning C++.";
    
    return 0;
}
```

Output:

```text
My name is Alex.I am learning C++.
```

Notice that everything appears on one line.

To create a new line, use `\n`.

```cpp
cout << "My name is Alex.\n";
cout << "I am learning C++.\n";
```

Output:

```text
My name is Alex.
I am learning C++.
```

You can also use `endl`:

```cpp
cout << "Hello" << endl;
cout << "World" << endl;
```

For now, I recommend getting comfortable with `\n`.

---

# 5. Comments

Comments are notes for humans. The compiler ignores them.

### Single-line comment

```cpp
// This is a comment
cout << "Hello";
```

### Multiple-line comment

```cpp
/*
This is
a multiple-line
comment
*/
cout << "Hello";
```

Comments are useful for explaining your code.

---

# 6. Your First Small Program

Try this:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "====================\n";
    cout << "    My C++ Program\n";
    cout << "====================\n";
    cout << "I am learning C++!\n";
    
    return 0;
}
```

You should get:

```text
====================
    My C++ Program
====================
I am learning C++!
```

---

# 7. Important Rules

Remember these:

### Rule 1 — C++ is case-sensitive

These are different:

```cpp
cout
Cout
COUT
```

Usually you'll use lowercase `cout`.

### Rule 2 — Strings use quotation marks

Correct:

```cpp
cout << "Hello";
```

Incorrect:

```cpp
cout << Hello;
```

### Rule 3 — Statements usually end with `;`

```cpp
cout << "Hello";
```

### Rule 4 — `main()` is the starting point

```cpp
int main() {
    // program starts here
}
```

---

# 8. Practice

Try writing programs that produce these outputs.

### Exercise 1

```text
Hello
I am learning C++
```

### Exercise 2

```text
****************
* C++ Student  *
****************
```

### Exercise 3

Print your:

- Name
    
- Age
    
- Favorite subject
    
- Why you want to learn programming
    

Use only `cout` and `\n`.

---

## Mini Challenge 🧠

What will this program print?

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "A\n";
    cout << "B\n";
    cout << "C";
    return 0;
}
```

**Answer:**

```text
A
B
C
```

---

### Lesson 1 Goal

By the end of this lesson, you should understand:

**`#include` → `main()` → `cout` → `\n` → `return 0`**

Next, **Lesson 2** should be **variables and data types**, where you'll learn how C++ stores information like names, ages, numbers, and true/false values.


---

# Lesson 2 — Variables & Data Types

In Lesson 1, you learned how to print things with `cout`.

Now we'll learn how a program can **store information**.

---

## 1. What is a Variable?

A **variable** is a named place in memory used to store a value.

For example:

```cpp
int age = 15;
```

Here:

- `int` → data type
    
- `age` → variable name
    
- `15` → value
    

Think of it like a labeled box:

**age → 15**

You can use the variable later:

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 15;

    cout << age;

    return 0;
}
```

Output:

```text
15
```

---

# 2. Creating Variables

The general form is:

```cpp
data_type variable_name = value;
```

Examples:

```cpp
int age = 15;
double height = 1.65;
char grade = 'A';
bool isStudent = true;
string name = "Alex";
```

Each stores a different type of information.

---

# 3. `int`

`int` stores **whole numbers**.

```cpp
int age = 15;
int score = 95;
int apples = 10;
```

You can perform calculations:

```cpp
int a = 10;
int b = 5;

cout << a + b;
```

Output:

```text
15
```

---

# 4. `double`

`double` stores numbers with decimal values.

```cpp
double price = 99.99;
double temperature = 36.5;
double pi = 3.14159;
```

Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    double price = 25.50;

    cout << price;

    return 0;
}
```

Output:

```text
25.5
```

---

# 5. `float`

`float` also stores decimal numbers.

```cpp
float temperature = 36.5;
```

For most beginner programs, you can use `double` when you need decimal numbers.

---

# 6. `char`

`char` stores **one character**.

Use **single quotes**:

```cpp
char grade = 'A';
char symbol = '#';
char letter = 'X';
```

This is different:

```cpp
char grade = "A"; // ❌
```

A `char` uses `' '`.

---

# 7. `string`

A `string` stores text.

```cpp
string name = "Alex";
string country = "Bangladesh";
```

For `string`, include:

```cpp
#include <string>
```

Although `iostream` commonly makes it available in simple programs, explicitly including `<string>` is good practice.

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name = "Alex";

    cout << name;

    return 0;
}
```

Output:

```text
Alex
```

---

# 8. `bool`

A `bool` stores one of two values:

```cpp
true
false
```

Example:

```cpp
bool isStudent = true;
bool isRaining = false;
```

By default, printing a `bool` gives:

```text
1
```

for `true` and:

```text
0
```

for `false`.

You can make C++ print `true`/`false` using `boolalpha`:

```cpp
#include <iostream>
using namespace std;

int main() {
    bool isStudent = true;

    cout << boolalpha << isStudent;

    return 0;
}
```

Output:

```text
true
```

---

# 9. A Program Using Different Data Types

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name = "Alex";
    int age = 15;
    double height = 1.65;
    char grade = 'A';
    bool student = true;

    cout << "Name: " << name << '\n';
    cout << "Age: " << age << '\n';
    cout << "Height: " << height << '\n';
    cout << "Grade: " << grade << '\n';
    cout << "Student: " << boolalpha << student << '\n';

    return 0;
}
```

Output:

```text
Name: Alex
Age: 15
Height: 1.65
Grade: A
Student: true
```

---

# 10. Changing a Variable

Variables can change.

```cpp
int age = 15;

cout << age << '\n';

age = 16;

cout << age << '\n';
```

Output:

```text
15
16
```

Notice that we don't write `int` again when changing the value.

Correct:

```cpp
age = 16;
```

Not:

```cpp
int age = 16;
```

The second version tries to declare another variable with the same name in the same scope.

---

# 11. Doing Calculations

Variables can be used in calculations.

```cpp
int a = 10;
int b = 3;

cout << a + b << '\n';
cout << a - b << '\n';
cout << a * b << '\n';
cout << a / b << '\n';
cout << a % b << '\n';
```

Output:

```text
13
7
30
3
1
```

The `%` operator gives the **remainder**.

For example:

```text
10 ÷ 3 = 3 remainder 1
```

So:

```cpp
10 % 3
```

is:

```text
1
```

---

# 12. A Very Important Problem: Integer Division

Look at this:

```cpp
int a = 5;
int b = 2;

cout << a / b;
```

You might expect:

```text
2.5
```

But C++ prints:

```text
2
```

Why?

Because both numbers are `int`.

If you want the decimal result:

```cpp
double a = 5;
double b = 2;

cout << a / b;
```

Output:

```text
2.5
```

This is an important concept to remember.

---

# 13. Constants

Sometimes you don't want a variable's value to change.

Use `const`:

```cpp
const double PI = 3.14159;
```

Then:

```cpp
PI = 5;
```

would cause an error.

Constants are useful for values that should remain fixed.

---

# 14. Naming Variables

Good:

```cpp
int age;
string firstName;
double totalPrice;
```

Bad:

```cpp
int x;
int abc;
int thing;
```

Short names are sometimes useful in small calculations, but descriptive names make larger programs much easier to understand.

### Variable naming rules

You can use:

- Letters
    
- Numbers
    
- `_`
    

But a variable **cannot start with a number**.

Correct:

```cpp
int age2;
int student_age;
```

Incorrect:

```cpp
int 2age;
```

C++ keywords also can't be used as variable names:

```cpp
int return; // ❌
```

---

# 15. Quick Reference

|Type|Stores|Example|
|---|---|---|
|`int`|Whole number|`15`|
|`double`|Decimal number|`3.14`|
|`float`|Decimal number|`3.14f`|
|`char`|One character|`'A'`|
|`string`|Text|`"Hello"`|
|`bool`|True/false|`true`|

---

# 🧠 Practice

### Exercise 1

Create variables for:

- Your name
    
- Your age
    
- Your favorite number
    
- Your grade
    
- Whether you are a student
    

Then print all of them.

---

### Exercise 2

Create:

```cpp
int a = 20;
int b = 6;
```

Print:

- Addition
    
- Subtraction
    
- Multiplication
    
- Division
    
- Remainder
    

---

### Exercise 3

What does this print?

```cpp
int x = 10;
int y = 3;

cout << x + y << '\n';
cout << x / y << '\n';
cout << x % y << '\n';
```

**Answer:**

```text
13
3
1
```

---

## ⭐ Mini Challenge

Write a program that stores:

```text
Name
Age
Math marks
English marks
Science marks
```

Then calculate and print the total marks.

Don't worry about making it perfect—**try it yourself first**.

### Next lesson

**Lesson 3 — User Input (`cin`)**: you'll learn how to make your program ask the user for their name, age, numbers, and other information.

---
# Lesson 3 — User Input with `cin`

So far, your programs have only **given information to the user**.

Now we'll make programs that can **receive information from the user**.

The main tool we'll use is:

```cpp
cin
```

---

## 1. What is `cin`?

`cin` allows the user to type something into the program.

Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;

    cout << "Enter your age: ";
    cin >> age;

    cout << "Your age is " << age;

    return 0;
}
```

If the user enters:

```text
15
```

The output becomes:

```text
Enter your age: 15
Your age is 15
```

---

# 2. How `cin` Works

Look at this:

```cpp
cin >> age;
```

The `>>` operator means we're taking the value entered by the user and putting it into `age`.

Think of it like:

```text
Keyboard → cin → age
```

Before using `cin`, you need a variable to store the input:

```cpp
int age;
cin >> age;
```

---

# 3. Getting a Number

```cpp
#include <iostream>
using namespace std;

int main() {
    int number;

    cout << "Enter a number: ";
    cin >> number;

    cout << "You entered: " << number;

    return 0;
}
```

If the user enters:

```text
42
```

Output:

```text
You entered: 42
```

---

# 4. Getting Multiple Numbers

You can read several values.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    cout << "Sum = " << a + b;

    return 0;
}
```

The user could enter:

```text
10 20
```

Output:

```text
Sum = 30
```

You can also enter them on separate lines:

```text
10
20
```

`cin` will still read them correctly.

---

# 5. Getting a `double`

```cpp
double price;

cout << "Enter price: ";
cin >> price;

cout << "Price = " << price;
```

Example:

```text
Enter price: 25.50
Price = 25.5
```

---

# 6. Getting a `char`

```cpp
char grade;

cout << "Enter your grade: ";
cin >> grade;

cout << "Your grade is " << grade;
```

Input:

```text
A
```

Output:

```text
Your grade is A
```

---

# 7. Getting a `bool`

You generally won't use `cin` directly for `bool` with beginners. It's better to ask for something simple such as `1` or `0`.

```cpp
bool answer;

cout << "Enter 1 for true or 0 for false: ";
cin >> answer;

cout << boolalpha << answer;
```

Input:

```text
1
```

Output:

```text
true
```

---

# 8. Getting a String

Here's something important.

You can do:

```cpp
string name;

cin >> name;
```

If the user enters:

```text
Alex
```

it works perfectly.

But what happens if they enter:

```text
Alex Smith
```

`cin >> name` only reads:

```text
Alex
```

Why?

Because `cin >>` normally stops reading a string when it encounters whitespace.

---

# 9. `getline()`

To read an entire line, use:

```cpp
getline()
```

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;

    cout << "Enter your full name: ";
    getline(cin, name);

    cout << "Hello, " << name;

    return 0;
}
```

Input:

```text
Alex Smith
```

Output:

```text
Hello, Alex Smith
```

### Remember:

```cpp
cin >> name;
```

reads one word.

```cpp
getline(cin, name);
```

reads an entire line.

---

# 10. The `cin` + `getline()` Problem

This is one of the most common beginner problems.

Consider:

```cpp
int age;
string name;

cout << "Enter age: ";
cin >> age;

cout << "Enter name: ";
getline(cin, name);
```

You might expect the program to wait for the name.

Sometimes it appears to skip the input.

That's because `cin >> age` leaves the newline character in the input buffer.

For now, use:

```cpp
cin.ignore();
```

Example:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int age;
    string name;

    cout << "Enter age: ";
    cin >> age;

    cin.ignore();

    cout << "Enter full name: ";
    getline(cin, name);

    cout << "Name: " << name << '\n';
    cout << "Age: " << age << '\n';

    return 0;
}
```

Later, we'll learn more about input buffers and a more robust version of `ignore()`.

---

# 11. A Complete Example

Let's build a small student information program.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    int age;
    double marks;

    cout << "Enter your full name: ";
    getline(cin, name);

    cout << "Enter your age: ";
    cin >> age;

    cout << "Enter your marks: ";
    cin >> marks;

    cout << "\n--- Student Information ---\n";
    cout << "Name: " << name << '\n';
    cout << "Age: " << age << '\n';
    cout << "Marks: " << marks << '\n';

    return 0;
}
```

Example interaction:

```text
Enter your full name: Alex Smith
Enter your age: 15
Enter your marks: 87.5

--- Student Information ---
Name: Alex Smith
Age: 15
Marks: 87.5
```

---

# 12. Input + Calculation

Now let's combine what you've learned in Lessons 1–3.

```cpp
#include <iostream>
using namespace std;

int main() {
    double a, b;

    cout << "Enter first number: ";
    cin >> a;

    cout << "Enter second number: ";
    cin >> b;

    cout << "Sum = " << a + b << '\n';
    cout << "Difference = " << a - b << '\n';
    cout << "Product = " << a * b << '\n';
    cout << "Division = " << a / b << '\n';

    return 0;
}
```

If the user enters:

```text
10
2
```

the program prints:

```text
Sum = 12
Difference = 8
Product = 20
Division = 5
```

---

# 13. Common Mistakes

### Mistake 1

```cpp
cin < age; // ❌
```

Correct:

```cpp
cin >> age; // ✅
```

For `cin`, use `>>`.

---

### Mistake 2

Forgetting to declare the variable:

```cpp
cin >> age; // ❌
```

You need:

```cpp
int age;
cin >> age;
```

---

### Mistake 3

Using the wrong data type:

```cpp
int price;
cin >> price;
```

If the user enters:

```text
19.99
```

you won't get the intended decimal value.

Use:

```cpp
double price;
```

---

# 🧠 Practice Exercises

### Exercise 1 — Personal Information

Create a program that asks for:

- Full name
    
- Age
    
- Country
    

Then prints:

```text
--- Information ---
Name: ...
Age: ...
Country: ...
```

---

### Exercise 2 — Calculator

Ask the user for two numbers and print:

- Sum
    
- Difference
    
- Product
    
- Division
    

---

### Exercise 3 — Rectangle

Ask the user for:

```text
length
width
```

Calculate:

```text
area = length × width
```

and print the result.

---

### Exercise 4 — Average

Ask for three marks:

```text
Mark 1:
Mark 2:
Mark 3:
```

Calculate their average.

**Hint:**

```cpp
average = (a + b + c) / 3;
```

---

# ⭐ Challenge

Create a program that asks:

```text
Enter your name:
Enter your age:
Enter your favorite number:
```

Then prints something like:

```text
Hello, Alex!
You are 15 years old.
Your favorite number is 7.
```

Try to write it **without looking back at the examples**.

---

## What You've Learned

You now know:

```cpp
cout        // output
cin         // input
getline()   // read an entire line
cin.ignore()// handle leftover input
```

And you can combine input with variables and calculations.

**Next: Lesson 4 — Operators & Expressions**, where we'll go deeper into arithmetic, comparison, logical operators, and how C++ makes decisions with expressions.


---
