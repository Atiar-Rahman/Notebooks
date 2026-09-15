# 🚀 Complete C Programming Course

### Phase 1 — C Fundamentals

1. C কী, কেন শিখব, Compiler কী
    
2. C setup + প্রথম program
    
3. `printf()` এবং `scanf()`
    
4. Variables
    
5. Data Types
    
6. Constants
    
7. Operators
    
8. Type Casting
    
9. Comments + coding style
    

### Phase 2 — Decision Making

10. `if`
    
11. `if-else`
    
12. `else-if`
    
13. Nested `if`
    
14. `switch-case`
    
15. Ternary operator
    

### Phase 3 — Loops

16. `for`
    
17. `while`
    
18. `do-while`
    
19. `break`
    
20. `continue`
    
21. Nested loops
    
22. Pattern problems
    

### Phase 4 — Functions

23. Function basics
    
24. Parameters & arguments
    
25. Return value
    
26. Call by value
    
27. Recursion
    
28. Scope & lifetime
    
29. Header files
    

### Phase 5 — Arrays & Strings

30. 1D Array
    
31. Array traversal
    
32. Searching
    
33. Sorting
    
34. 2D Array / Matrix
    
35. Strings
    
36. String functions
    
37. Array of strings
    

### Phase 6 — Pointers 🔥

38. Pointer basics
    
39. Address operator `&`
    
40. Dereference `*`
    
41. Pointer + Array
    
42. Pointer + Function
    
43. Pointer + String
    
44. Pointer to Pointer
    
45. Dynamic Memory Allocation
    

### Phase 7 — Structures

46. `struct`
    
47. Nested structure
    
48. Array of structures
    
49. Pointer to structure
    
50. `typedef`
    
51. `union`
    
52. `enum`
    

### Phase 8 — File Handling

53. File concept
    
54. `fopen()`
    
55. `fclose()`
    
56. Read/write file
    
57. `fprintf()` / `fscanf()`
    
58. Binary files
    

### Phase 9 — Advanced C

59. Preprocessor
    
60. Macros
    
61. Command-line arguments
    
62. Storage classes
    
63. Memory layout
    
64. Stack vs Heap
    
65. Function pointers
    
66. Dynamic data structures
    

### Phase 10 — Data Structures with C

67. Linked List
    
68. Singly Linked List
    
69. Doubly Linked List
    
70. Stack
    
71. Queue
    
72. Circular Queue
    
73. Tree basics
    
74. Binary Search Tree
    
75. Graph basics
    

### Phase 11 — Practical Projects

শেষে কয়েকটি project বানাব:

- 🏦 Bank Management System
    
- 📚 Student Management System
    
- 🛒 Mini E-commerce CLI
    
- 📁 File Management System
    
- 🧮 Calculator
    
- 📝 Quiz Application
    
- 🏧 ATM Simulation [phase by phase complete tutorial give me start phase 1]


-------------

# 🚀 Phase 1 — C Fundamentals

এই Phase-এ তুমি C-এর একদম foundation তৈরি করবে।

### Phase 1-এর Roadmap

1. **C কী, কেন শিখব, Compiler কী**
    
2. **C setup + প্রথম program**
    
3. **`printf()` এবং `scanf()`**
    
4. **Variables**
    
5. **Data Types**
    
6. **Constants**
    
7. **Operators**
    
8. **Type Casting**
    
9. **Comments + Coding Style**
    

---

# 📘 Lesson 1 — C কী, কেন শিখব, Compiler কী?

## 1. C কী?

**C হলো একটি general-purpose programming language।**

এটি 1970-এর দশকে **Dennis Ritchie** Bell Labs-এ তৈরি করেন।

C-কে অনেক সময় **middle-level programming language** বলা হয়, কারণ এটি একই সঙ্গে:

- Hardware-এর কাছাকাছি কাজ করতে পারে
    
- আবার high-level programming-এর মতো structured code লিখতেও দেয়
    

C দিয়ে operating system, embedded software, system utilities, compilers এবং অনেক performance-critical software তৈরি করা হয়েছে।

---

## 2. C কেন শিখব?

C শেখার সবচেয়ে বড় সুবিধা হলো এটি programming-এর fundamental concepts খুব পরিষ্কারভাবে শেখায়।

বিশেষ করে:

- Variable
    
- Data type
    
- Memory
    
- Pointer
    
- Function
    
- Array
    
- Structure
    
- Dynamic memory
    
- Data structure
    

C ভালোভাবে জানলে পরে C++, Java, Rust, Go ইত্যাদি language শেখার সময় অনেক concept সহজ লাগে।

### বিশেষ করে Pointer

C শেখার সময় আমরা পরে দেখব:

```c
int x = 10;
int *p = &x;
```

এখানে `p` কীভাবে memory address ধরে রাখে—এই ধরনের বিষয় C তোমাকে সরাসরি বুঝতে সাহায্য করবে।

---

# 3. Programming Language আসলে কী?

ধরো তুমি computer-কে বললে:

> "10 আর 20 যোগ করো।"

Computer নিজে মানুষের ভাষা বুঝে না।

তাই আমরা programming language ব্যবহার করে instruction লিখি।

যেমন C-তে:

```c
10 + 20
```

এর মাধ্যমে আমরা computer-কে computation-এর instruction দিতে পারি।

কিন্তু এখানেও একটি সমস্যা আছে।

Computer শেষ পর্যন্ত **machine code** execute করে।

তাহলে C code → machine code কীভাবে যায়?

এখানেই আসে **Compiler**।

---

# 4. Compiler কী?

**Compiler হলো এমন একটি program যা source code-কে machine-executable code-এ translate করে।**

সহজভাবে:

```text
তুমি
 ↓
C Code
 ↓
Compiler
 ↓
Machine Code
 ↓
Computer
```

উদাহরণ:

```c
#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```

এটা আমরা সরাসরি CPU-কে দিতে পারি না।

Compiler এটিকে এমন form-এ translate করে যেটা computer execute করতে পারে।

---

# 5. Source Code কী?

তুমি যে C program লিখবে সেটাই হলো **source code**।

উদাহরণ:

```c
#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```

ধরো file-এর নাম:

```text
hello.c
```

`.c` extension দেখে বোঝা যায় এটি C source file।

---

# 6. Compiler-এর উদাহরণ

C-এর জন্য জনপ্রিয় compiler হলো:

- GCC
    
- Clang
    
- Microsoft Visual C
    

আমরা beginner হিসেবে **GCC** ব্যবহার করতে পারি।

Terminal-এ:

```bash
gcc hello.c -o hello
```

এখানে:

```text
gcc
```

→ compiler

```text
hello.c
```

→ আমাদের C source file

```text
-o hello
```

→ output program-এর নাম `hello`

তারপর program run করা যায়।

Linux/macOS:

```bash
./hello
```

Windows-এ সাধারণত:

```bash
hello.exe
```

---

# 7. Compiler কি শুধু translate করে?

Beginner level-এ তুমি ভাবতে পারো:

> **Compiler = C code → executable program**

কিন্তু বাস্তবে compilation process-এর মধ্যে কয়েকটি ধাপ থাকে।

সাধারণভাবে:

```text
Source Code
     ↓
Preprocessing
     ↓
Compilation
     ↓
Assembly
     ↓
Linking
     ↓
Executable
```

এই বিষয়গুলো আমরা পরে **Advanced C**-তে বিস্তারিত দেখব।

এখন শুধু flow-টা মনে রাখো।

---

# 8. Compiler Error কী?

ধরো তুমি লিখলে:

```c
#include <stdio.h>

int main() {
    printf("Hello World"
    return 0;
}
```

এখানে `printf()`-এর পরে closing `)` নেই।

Compiler code check করার সময় error দেখাবে।

অর্থাৎ:

```text
C Code
  ↓
Compiler
  ↓
Error ❌
```

Error পাওয়া programming-এর খুব স্বাভাবিক অংশ।

**Error মানেই তুমি programming পারো না—এমন নয়।**

বরং error পড়তে এবং ঠিক করতে শেখা programming-এর গুরুত্বপূর্ণ skill।

---

# 🧠 আজকের মূল ধারণা

এই ৫টি জিনিস মনে রাখো:

|Term|অর্থ|
|---|---|
|C|Programming language|
|Source Code|Programmer-এর লেখা C code|
|Compiler|Source code translate/compile করে|
|Machine Code|Computer-এর executable instruction|
|Executable|Run করা যায় এমন program|

Flow:

```text
Programmer
    ↓
C Source Code
    ↓
Compiler
    ↓
Executable Program
    ↓
Computer
```

---

# 📝 Practice

নিজের ভাষায় উত্তর দেওয়ার চেষ্টা করো:

**1. C কী?**

**2. C শেখার দুটি সুবিধা লেখো।**

**3. Compiler কী কাজ করে?**

**4. `.c` file বলতে কী বোঝায়?**

**5. এই flow-টি পূরণ করো:**

```text
C Source Code
      ↓
   ________
      ↓
Executable
```

### 🎯 ছোট Challenge

ভাবো তুমি একটি C program লিখেছ:

```text
sum.c
```

এখন বলো:

> `sum.c` কোন ধরনের file এবং সেটিকে executable program-এ পরিণত করার জন্য কোন ধরনের software প্রয়োজন?

এরপর আমরা **Lesson 2 — C Setup + প্রথম Program**-এ গিয়ে সত্যিকারের প্রথম C program লিখব।

----
# 🚀 Lesson 2 — C Setup + প্রথম C Program

আজকের লক্ষ্য: **C-এর environment setup করা এবং নিজের প্রথম C program লেখা ও run করা।**

---

## 1. আমাদের কী কী লাগবে?

C programming-এর জন্য মূলত দরকার:

1. **C Compiler** — যেমন GCC
    
2. **Code Editor / IDE** — যেখানে code লিখবে
    
3. **Terminal** — program compile ও run করার জন্য
    

Beginner হিসেবে আমরা **GCC + VS Code** ব্যবহার করতে পারি।

---

# 2. GCC কী?

**GCC = GNU Compiler Collection**

এটি C program compile করার জন্য বহুল ব্যবহৃত compiler।

Terminal-এ নিচের command দিয়ে check করতে পারো GCC আগে থেকেই আছে কি না:

```bash
gcc --version
```

যদি version information আসে, তাহলে GCC installed আছে।

যদি এমন কিছু আসে:

```text
gcc: command not found
```

তাহলে GCC install করতে হবে।

---

# 3. VS Code কী?

VS Code হলো একটি **code editor**।

এতে আমরা C code লিখব।

VS Code-এ C/C++ extension ব্যবহার করলে:

- Syntax highlighting
    
- Error detection
    
- Code completion
    
- Debugging
    

ইত্যাদি সুবিধা পাওয়া যায়।

---

# 4. প্রথম Program

এবার আমাদের সবচেয়ে famous C program:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");

    return 0;
}
```

এটাই তোমার প্রথম C program। 🎉

---

# 5. Code-টি বুঝি

একবারে সব মুখস্থ করার দরকার নেই। এখন line by line বুঝি।

### প্রথম লাইন

```c
#include <stdio.h>
```

`stdio.h` হলো C-এর একটি standard header file।

`printf()` ব্যবহার করার জন্য এটি দরকার।

এখন শুধু মনে রাখো:

> `printf()` ব্যবহার করতে সাধারণত `#include <stdio.h>` লিখি।

---

## 6. `main()` কী?

```c
int main()
```

`main()` হলো program-এর **entry point**।

সহজভাবে ভাবো:

```text
Program শুরু
     ↓
   main()
     ↓
পরবর্তী statements
```

C program run করলে execution সাধারণত `main()` function থেকে শুরু হয়।

---

# 7. `{ }` কী?

```c
int main() {

}
```

এই `{ }` দিয়ে একটি **block** বোঝানো হয়।

`main()`-এর ভিতরের statements এখানে থাকবে।

যেমন:

```c
int main() {
    printf("Hello");
}
```

---

# 8. `printf()` কী?

```c
printf("Hello, World!\n");
```

`printf()` screen-এ output দেখায়।

তাই:

```c
printf("Hello");
```

এর output হবে:

```text
Hello
```

আর:

```c
printf("Hello, World!\n");
```

এর output:

```text
Hello, World!
```

এখানে `\n` মানে **new line**।

---

# 9. `return 0;` কী?

```c
return 0;
```

এটি `main()` function থেকে value return করে।

Beginner হিসেবে এখন এটুকু মনে রাখো:

> `return 0;` সাধারণত program সফলভাবে শেষ হয়েছে—এটি বোঝাতে ব্যবহৃত হয়।

---

# 10. Semicolon `;`

C-তে অনেক statement-এর শেষে `;` দিতে হয়।

যেমন:

```c
printf("Hello");
return 0;
```

কিন্তু এগুলো ভুল:

```c
printf("Hello")
return 0
```

কারণ এখানে semicolon নেই।

---

# 11. এবার নিজের Program বানাও

`hello.c` নামে একটি file তৈরি করো।

তার মধ্যে লিখো:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");

    return 0;
}
```

Save করো।

---

# 12. Compile করা

Terminal খুলে সেই folder-এ যাও যেখানে `hello.c` আছে।

তারপর:

```bash
gcc hello.c -o hello
```

যদি কোনো error না আসে, তাহলে compilation সফল হয়েছে।

---

# 13. Program Run করা

### Windows

```bash
hello.exe
```

### Linux/macOS

```bash
./hello
```

Output:

```text
Hello, World!
```

🎉 **Congratulations! তুমি তোমার প্রথম C program run করেছ।**

---

# 14. এবার একটু পরিবর্তন করি

`Hello, World!`-এর জায়গায় নিজের message লিখো:

```c
#include <stdio.h>

int main() {
    printf("I am learning C programming!\n");

    return 0;
}
```

Output:

```text
I am learning C programming!
```

---

# 🧪 Practice 1

এমন একটি program লেখো যার output হবে:

```text
My name is Alex.
I am learning C.
C is interesting!
```

Hint:

```c
printf("...");
printf("...");
printf("...");
```

---

# 🧪 Practice 2 — একটি গুরুত্বপূর্ণ experiment

এই code চালাও:

```c
#include <stdio.h>

int main() {
    printf("Hello\n");
    printf("World\n");

    return 0;
}
```

Output:

```text
Hello
World
```

তারপর `\n` সরিয়ে দেখো:

```c
printf("Hello");
printf("World");
```

Output কী হয়, সেটা নিজে observe করো।

এতে `\n` কী করে সেটা পরিষ্কার হয়ে যাবে।

---

# 🧠 আজকের Cheat Sheet

```text
#include <stdio.h>
        ↓
printf() ব্যবহারের জন্য header

int main()
        ↓
Program-এর entry point

printf()
        ↓
Output দেখায়

\n
        ↓
New line

;
        ↓
Statement শেষ

return 0;
        ↓
main() থেকে সফল termination signal
```

### আজকের সবচেয়ে গুরুত্বপূর্ণ program

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");

    return 0;
}
```

**পরের Lesson: `printf()` এবং `scanf()` — কীভাবে output দেখাব এবং user-এর কাছ থেকে input নেব।**


----
# 🚀 Lesson 3 — `printf()` এবং `scanf()`

আজ আমরা C-এর সবচেয়ে গুরুত্বপূর্ণ দুইটি function শিখব:

- `printf()` → **output দেখাতে**
    
- `scanf()` → **user-এর কাছ থেকে input নিতে**
    

---

## 1. `printf()` — Output

আগের lesson-এ দেখেছিলে:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");

    return 0;
}
```

Output:

```text
Hello, World!
```

অর্থাৎ:

> `printf()` screen-এ information দেখায়।

---

# 2. একাধিক `printf()`

```c
#include <stdio.h>

int main() {
    printf("Hello\n");
    printf("I am learning C\n");
    printf("This is my first program\n");

    return 0;
}
```

Output:

```text
Hello
I am learning C
This is my first program
```

---

# 3. `\n` কী?

`\n` হলো **newline character**।

```c
printf("Hello\nWorld");
```

Output:

```text
Hello
World
```

কিন্তু:

```c
printf("Hello World");
```

Output:

```text
Hello World
```

---

# 4. একই line-এ output

```c
printf("Hello ");
printf("World");
```

Output:

```text
Hello World
```

কারণ প্রথম `printf()`-এ `\n` নেই।

---

# 5. কিছু গুরুত্বপূর্ণ Escape Sequence

|Escape sequence|কাজ|
|---|---|
|`\n`|New line|
|`\t`|Tab|
|`\"`|Double quote|
|`\\`|Backslash|

উদাহরণ:

```c
printf("Name:\tAlex\n");
printf("Age:\t15\n");
```

Output:

```text
Name:   Alex
Age:    15
```

---

# 6. `printf()`-এ Variable ব্যবহার

ধরো:

```c
int age = 15;
```

তুমি age print করতে পারো:

```c
printf("%d", age);
```

Output:

```text
15
```

এখানে `%d` হলো একটি **format specifier**।

এটি বলে:

> এখানে একটি integer value আসবে।

---

# 7. Format Specifier

এখন কয়েকটি গুরুত্বপূর্ণ format specifier দেখে রাখো:

|Data|Format|
|---|---|
|`int`|`%d`|
|`float`|`%f`|
|`double`|`%lf`|
|`char`|`%c`|
|String|`%s`|

String এবং data types আমরা পরের lessons-এ বিস্তারিত শিখব।

---

# 8. `printf()` Example

```c
#include <stdio.h>

int main() {
    int age = 15;

    printf("My age is %d\n", age);

    return 0;
}
```

Output:

```text
My age is 15
```

এখানে:

```c
printf("My age is %d\n", age);
```

`%d` জায়গায় `age`-এর value বসেছে।

---

# 9. একাধিক Variable

```c
#include <stdio.h>

int main() {
    int age = 15;
    int year = 2026;

    printf("Age = %d\n", age);
    printf("Year = %d\n", year);

    return 0;
}
```

Output:

```text
Age = 15
Year = 2026
```

---

# 🔥 এবার `scanf()`

এখন আমরা user-এর কাছ থেকে input নেব।

উদাহরণ:

```c
#include <stdio.h>

int main() {
    int age;

    printf("Enter your age: ");
    scanf("%d", &age);

    printf("Your age is %d\n", age);

    return 0;
}
```

Program run করলে:

```text
Enter your age: 15
Your age is 15
```

---

# 10. `scanf()` কী করছে?

এই line:

```c
scanf("%d", &age);
```

এখানে:

```text
%d
```

→ আমরা integer input নিচ্ছি।

আর:

```text
&age
```

→ `age` variable-এর memory address দেওয়া হচ্ছে।

**`&` নিয়ে এখন বেশি চিন্তা করার দরকার নেই।** Pointer lesson-এ আমরা এটা অনেক বিস্তারিত শিখব।

এখন শুধু rule:

> `scanf()` দিয়ে variable-এ input নেওয়ার সময় সাধারণত `&variable` লিখতে হয়।

---

# 11. User-এর কাছ থেকে দুইটি সংখ্যা

```c
#include <stdio.h>

int main() {
    int a;
    int b;

    printf("Enter first number: ");
    scanf("%d", &a);

    printf("Enter second number: ");
    scanf("%d", &b);

    printf("First = %d\n", a);
    printf("Second = %d\n", b);

    return 0;
}
```

যদি user দেয়:

```text
10
20
```

Output:

```text
First = 10
Second = 20
```

---

# 12. দুইটি সংখ্যা যোগ করা

এবার একটু interesting করি।

```c
#include <stdio.h>

int main() {
    int a;
    int b;
    int sum;

    printf("Enter first number: ");
    scanf("%d", &a);

    printf("Enter second number: ");
    scanf("%d", &b);

    sum = a + b;

    printf("Sum = %d\n", sum);

    return 0;
}
```

Input:

```text
10
20
```

Output:

```text
Sum = 30
```

এখানে পুরো flow:

```text
User
 ↓
scanf()
 ↓
Variables
 ↓
Calculation
 ↓
printf()
 ↓
Output
```

---

# 13. একটি গুরুত্বপূর্ণ ভুল

এটা লিখবে না:

```c
scanf("%d", age);
```

যদি `age` একটি `int` variable হয়।

Beginner হিসেবে মনে রাখো:

```c
scanf("%d", &age);
```

---

# 14. `printf()` + `scanf()` একসঙ্গে

এটি ভালোভাবে বুঝে রাখো:

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    printf("You entered: %d\n", number);

    return 0;
}
```

এখানে:

### Step 1

```c
int number;
```

Variable তৈরি।

### Step 2

```c
printf("Enter a number: ");
```

User-কে message দেখানো।

### Step 3

```c
scanf("%d", &number);
```

User-এর input নেওয়া।

### Step 4

```c
printf("You entered: %d\n", number);
```

Input আবার দেখানো।

---

# 🧪 Practice 1

এমন একটি program লেখো যেখানে user তার **age** input দেবে।

Expected interaction:

```text
Enter your age: 15
Your age is 15
```

---

# 🧪 Practice 2

User-এর কাছ থেকে দুইটি integer নাও এবং তাদের:

- যোগফল
    
- বিয়োগফল
    
- গুণফল
    

print করো।

যেমন:

```text
Enter first number: 10
Enter second number: 5

Sum = 15
Difference = 5
Product = 50
```

---

# 🎯 Mini Challenge

User-এর কাছ থেকে তিনটি number নাও এবং তাদের যোগফল বের করো।

Structure:

```text
Enter number 1:
Enter number 2:
Enter number 3:

Total = ...
```

নিজে আগে চেষ্টা করো।

---

## 🧠 আজকের Cheat Sheet

```text
printf()
    ↓
Output

scanf()
    ↓
Input

%d
    ↓
Integer

&variable
    ↓
scanf()-এ variable-এর address

\n
    ↓
New line
```

সবচেয়ে গুরুত্বপূর্ণ pattern:

```c
int number;

printf("Enter a number: ");
scanf("%d", &number);

printf("You entered %d\n", number);
```

পরের Lesson-এ আমরা **Variables** খুব ভালোভাবে শিখব—variable কী, কীভাবে declare/initialize করতে হয়, naming rules, এবং memory-তে variable কীভাবে কাজ করে।


----

# 🚀 Lesson 4 — Variables

আজ আমরা C-এর অন্যতম fundamental concept **Variable** শিখব।

Variable ভালোভাবে বুঝলে পরের **Data Types, Constants, Operators, Arrays**—সবকিছু অনেক সহজ হবে।

---

# 1. Variable কী?

সহজভাবে:

> **Variable হলো computer memory-এর একটি named location যেখানে কোনো data রাখা যায়।**

ধরো তোমার কাছে একটি box আছে:

```text
┌──────────────┐
│     25       │
└──────────────┘
     age
```

এখানে:

- `age` → variable-এর নাম
    
- `25` → variable-এর value
    

C-তে:

```c
int age = 25;
```

---

# 2. Variable Declare করা

Variable তৈরি করার basic syntax:

```c
data_type variable_name;
```

উদাহরণ:

```c
int age;
```

এখানে:

```text
int
 ↓
Data type

age
 ↓
Variable name
```

এখন `age` variable তৈরি হয়েছে।

---

# 3. Value Assign করা

Variable তৈরি করার পরে value দিতে পারো:

```c
int age;

age = 15;
```

এখানে `=` হলো **assignment operator**।

এর অর্থ:

> ডান পাশের value বাম পাশের variable-এ রাখো।

অর্থাৎ:

```text
15
 ↓
age
```

---

# 4. Declaration + Initialization

দুইটি আলাদা statement না লিখে একসঙ্গে করা যায়:

```c
int age = 15;
```

এখানে variable declare এবং value assign—দুটিই হয়েছে।

এটাকে বলা হয় **initialization**।

---

# 5. Variable-এর Value পরিবর্তন করা

Variable-এর value পরে পরিবর্তন করা যায়।

```c
#include <stdio.h>

int main() {
    int age = 15;

    printf("%d\n", age);

    age = 16;

    printf("%d\n", age);

    return 0;
}
```

Output:

```text
15
16
```

অর্থাৎ variable-এর value পরিবর্তন করা সম্ভব।

---

# 6. একাধিক Variable

```c
int age = 15;
int year = 2026;
int score = 95;
```

প্রতিটি variable আলাদা data রাখছে।

```text
age   → 15
year  → 2026
score → 95
```

---

# 7. Variable Print করা

```c
#include <stdio.h>

int main() {
    int age = 15;

    printf("Age = %d\n", age);

    return 0;
}
```

Output:

```text
Age = 15
```

`%d` ব্যবহার করেছি কারণ `age` হলো `int`।

---

# 8. Variable দিয়ে Calculation

Variable-এর সবচেয়ে গুরুত্বপূর্ণ ব্যবহারগুলোর একটি হলো calculation।

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;

    int sum = a + b;

    printf("Sum = %d\n", sum);

    return 0;
}
```

Output:

```text
Sum = 30
```

এখানে:

```c
int sum = a + b;
```

প্রথমে:

```text
a = 10
b = 20
```

তারপর:

```text
10 + 20 = 30
```

এবং:

```text
sum = 30
```

---

# 9. `=` আর `==` এক জিনিস নয়

এটি খুব গুরুত্বপূর্ণ।

### `=`

Assignment:

```c
age = 15;
```

অর্থ:

> age-এর মধ্যে 15 রাখো।

### `==`

Comparison:

```c
age == 15
```

অর্থ:

> age কি 15-এর সমান?

`==` আমরা **if/else** lesson-এ বিস্তারিত ব্যবহার করব।

এখন শুধু পার্থক্যটা মনে রাখো:

```text
=   → assign
==  → compare
```

---

# 10. Variable Naming Rules

Variable-এর নাম দেওয়ার কিছু নিয়ম আছে।

### ✅ Valid

```c
age
studentAge
student_age
number1
totalMarks
```

### ❌ Invalid

```c
1number
student age
total-marks
```

কারণ:

- নাম number দিয়ে শুরু করা যায় না
    
- space ব্যবহার করা যায় না
    
- `-` সাধারণ variable name-এর অংশ হিসেবে ব্যবহার করা যায় না
    

---

# 11. Variable Name-এর ক্ষেত্রে Case Sensitive

C হলো **case-sensitive** language।

অর্থাৎ:

```c
age
Age
AGE
```

এই তিনটি আলাদা identifier।

উদাহরণ:

```c
int age = 15;
int Age = 20;
```

এখানে দুটি আলাদা variable।

---

# 12. ভালো Variable Name

এভাবে:

```c
int x = 15;
```

কাজ করবে।

কিন্তু:

```c
int studentAge = 15;
```

আরও readable।

আর:

```c
int aVeryImportantStudentAgeNumber = 15;
```

অতিরিক্ত বড় এবং অপ্রয়োজনীয়।

সাধারণত এমন নাম ব্যবহার করো যেটা variable-এর কাজ বোঝায়:

```c
int age;
int totalMarks;
int studentCount;
int price;
```

---

# 13. Variable + `scanf()`

এখন আগের lesson-এর knowledge ব্যবহার করি।

```c
#include <stdio.h>

int main() {
    int age;

    printf("Enter your age: ");
    scanf("%d", &age);

    printf("Your age is %d\n", age);

    return 0;
}
```

এখানে:

```c
int age;
```

→ variable তৈরি

```c
scanf("%d", &age);
```

→ user-এর input variable-এ রাখা

```c
printf("%d", age);
```

→ variable-এর value output করা

---

# 14. Variable-এর Value ব্যবহার করে Calculation

```c
#include <stdio.h>

int main() {
    int length;
    int width;
    int area;

    printf("Enter length: ");
    scanf("%d", &length);

    printf("Enter width: ");
    scanf("%d", &width);

    area = length * width;

    printf("Area = %d\n", area);

    return 0;
}
```

যদি input হয়:

```text
Enter length: 10
Enter width: 5
```

Output:

```text
Area = 50
```

---

# 15. Variable-এর ভিতরে Variable-এর value

এটাও সম্ভব:

```c
int a = 10;
int b = a;
```

তখন:

```text
a = 10
b = 10
```

পরে `a` পরিবর্তন করলেও `b` automatically পরিবর্তন হবে না।

```c
a = 20;
```

এখন:

```text
a = 20
b = 10
```

---

# 16. গুরুত্বপূর্ণ বিষয়: Uninitialized Variable

এটা করা যায়:

```c
int age;
```

কিন্তু তখন `age`-এর কোনো নির্ভরযোগ্য value set করা হয়নি।

তাই value দেওয়ার আগে এমন variable ব্যবহার করা উচিত নয়:

```c
int age;

printf("%d", age);  // ❌
```

বরং:

```c
int age = 15;
printf("%d", age);  // ✅
```

অথবা user input নাও:

```c
int age;

scanf("%d", &age);

printf("%d", age);  // ✅
```

---

# 🧠 Variable-এর Mental Model

এটা মাথায় রাখো:

```text
        Memory
┌─────────────────┐
│                 │
│  age → 15       │
│                 │
│  score → 90     │
│                 │
│  year → 2026    │
│                 │
└─────────────────┘
```

Variable হলো memory-এর data-কে একটি meaningful নাম দিয়ে access করার সহজ উপায়।

---

# 🧪 Practice 1

একটি program লেখো যেখানে:

- `age = 15`
    
- `year = 2026`
    
- `score = 95`
    

এগুলো output করবে।

Expected:

```text
Age = 15
Year = 2026
Score = 95
```

---

# 🧪 Practice 2

User-এর কাছ থেকে:

```text
length
width
```

নিয়ে rectangle-এর area বের করো।

Formula:

```text
Area = length × width
```

---

# 🔥 Mini Challenge

User-এর কাছ থেকে একটি number নাও।

তারপর output করো:

```text
Number = 10
Double = 20
Triple = 30
```

যদি input হয় `10`।

Hint:

```c
double = number * 2;
triple = number * 3;
```

---

## 🎯 আজকের Cheat Sheet

```text
Variable তৈরি:
int age;

Value দেওয়া:
age = 15;

Declare + initialize:
int age = 15;

Output:
printf("%d", age);

Input:
scanf("%d", &age);
```

সবচেয়ে গুরুত্বপূর্ণ:

```c
int age = 15;

age = 16;
```

প্রথমে `age`-এর value `15`, পরে সেটি `16` হয়েছে।

---

### পরের Lesson → **Lesson 5 — Data Types**

সেখানে আমরা `int`, `float`, `double`, `char` এবং তাদের মধ্যে পার্থক্য শিখব, এবং **কখন কোন data type ব্যবহার করতে হয়** সেটা practical example দিয়ে দেখব।


---

# 🚀 Lesson 5 — Data Types

আজ আমরা শিখব **Data Type** কী, কেন দরকার, এবং C-এর সবচেয়ে গুরুত্বপূর্ণ data types কীভাবে ব্যবহার করতে হয়।

---

# 1. Data Type কী?

**Data Type বলে দেয় একটি variable কী ধরনের data রাখবে।**

যেমন:

```c
int age = 15;
```

এখানে `age` একটি integer রাখছে।

আবার:

```c
float price = 99.50;
```

এখানে `price` decimal number রাখছে।

সহজভাবে:

```text
Variable → কী ধরনের data রাখবে?
                ↓
            Data Type
```

---

# 2. কেন Data Type দরকার?

Computer memory-তে data রাখার জন্য compiler-কে জানতে হয়:

- Data-এর ধরন কী?
    
- কতটা memory প্রয়োজন?
    
- কীভাবে data interpret করতে হবে?
    
- কোন operation করা যাবে?
    

তাই আমরা variable declaration-এর সময় data type লিখি।

```c
int age;
float height;
char grade;
```

---

# 3. `int` — Integer

`int` ব্যবহার করা হয় **পূর্ণসংখ্যার** জন্য।

উদাহরণ:

```c
int age = 15;
int score = 95;
int temperature = 30;
```

এগুলোতে decimal নেই।

```text
10
25
100
-5
0
```

সবগুলো integer।

### Example

```c
#include <stdio.h>

int main() {
    int age = 15;

    printf("Age = %d\n", age);

    return 0;
}
```

Output:

```text
Age = 15
```

`int` print করার জন্য `%d` ব্যবহার করি।

---

# 4. `float` — Decimal Number

`float` ব্যবহার করা হয় decimal/fractional number-এর জন্য।

```c
float height = 5.5;
float price = 99.99;
float temperature = 36.5;
```

Print:

```c
#include <stdio.h>

int main() {
    float price = 99.99;

    printf("Price = %f\n", price);

    return 0;
}
```

Output দেখতে এমন হতে পারে:

```text
Price = 99.989998
```

কারণ floating-point number-এর representation-এর কারণে precision difference হতে পারে।

---

# 5. Decimal কত ঘর দেখাব?

`printf()`-এ precision specify করা যায়।

```c
printf("%.2f", price);
```

এখানে:

```text
.2
 ↓
দুই decimal place
```

যেমন:

```c
#include <stdio.h>

int main() {
    float price = 99.99;

    printf("Price = %.2f\n", price);

    return 0;
}
```

Output:

```text
Price = 99.99
```

---

# 6. `double`

`double`-ও decimal number রাখে, তবে সাধারণত `float`-এর চেয়ে বেশি precision দেয়।

```c
double pi = 3.141592653589793;
```

Example:

```c
#include <stdio.h>

int main() {
    double pi = 3.141592653589793;

    printf("Pi = %.15f\n", pi);

    return 0;
}
```

`double` print করার ক্ষেত্রে `printf()`-এ সাধারণত `%f` ব্যবহার করা হয়।

---

# 7. `char` — একটি Character

`char` একটি single character রাখে।

```c
char grade = 'A';
char gender = 'M';
char symbol = '#';
```

খেয়াল করো:

### Character:

```c
'A'
```

### String:

```c
"Alex"
```

একটি `char`-এর জন্য single quotes ব্যবহার করি।

Print:

```c
printf("%c", grade);
```

Example:

```c
#include <stdio.h>

int main() {
    char grade = 'A';

    printf("Grade = %c\n", grade);

    return 0;
}
```

Output:

```text
Grade = A
```

---

# 8. `char` এবং Number

C-তে `char` internally একটি numeric character code-এর সঙ্গে সম্পর্কিত।

যেমন:

```c
char letter = 'A';

printf("%c\n", letter);
printf("%d\n", letter);
```

দুটি output পাওয়া যাবে:

```text
A
65
```

এখানে `65` ASCII encoding-এ `A`-এর code।

এখন ASCII নিয়ে বেশি চিন্তা করার দরকার নেই; পরে প্রয়োজন হলে বিস্তারিত দেখব।

---

# 9. String কি Data Type?

Beginner হিসেবে একটি গুরুত্বপূর্ণ বিষয়:

C-তে Java/Python-এর মতো built-in `string` data type নেই।

আমরা character array ব্যবহার করে string রাখি।

যেমন:

```c
char name[] = "Alex";
```

এটি আমরা **Strings lesson**-এ বিস্তারিত শিখব।

এখন শুধু মনে রাখো:

```text
char → একটি character
char[] → string-এর জন্য ব্যবহৃত হয়
```

---

# 10. `sizeof()` — Data কত memory নেয়?

C-তে `sizeof()` operator দিয়ে কোনো type বা variable কত bytes memory নেয় তা জানা যায়।

```c
#include <stdio.h>

int main() {
    printf("%zu\n", sizeof(int));
    printf("%zu\n", sizeof(float));
    printf("%zu\n", sizeof(double));
    printf("%zu\n", sizeof(char));

    return 0;
}
```

Output system/compiler অনুযায়ী ভিন্ন হতে পারে। অনেক সাধারণ system-এ এমন দেখা যায়:

```text
4
4
8
1
```

কিন্তু **এগুলো সব computer-এ guaranteed নয়**।

তাই এখন মূল ধারণা:

> `sizeof()` → কোনো type/variable-এর storage size bytes-এ জানায়।

---

# 11. Data Type + Variable

একটি সুন্দর example:

```c
#include <stdio.h>

int main() {
    int age = 15;
    float height = 5.5;
    double pi = 3.1415926535;
    char grade = 'A';

    printf("Age = %d\n", age);
    printf("Height = %.2f\n", height);
    printf("Pi = %.10f\n", pi);
    printf("Grade = %c\n", grade);

    return 0;
}
```

Output:

```text
Age = 15
Height = 5.50
Pi = 3.1415926535
Grade = A
```

---

# 12. `scanf()`-এ Data Types

এখানে একটু গুরুত্বপূর্ণ পার্থক্য আছে।

### Integer

```c
int age;

scanf("%d", &age);
```

### Float

```c
float price;

scanf("%f", &price);
```

### Double

```c
double pi;

scanf("%lf", &pi);
```

### Character

```c
char grade;

scanf(" %c", &grade);
```

`%c`-এর আগে space রাখার বিষয়টি পরে input handling-এ আরও পরিষ্কার হবে।

---

# 13. Complete Input Example

```c
#include <stdio.h>

int main() {
    int age;
    float height;
    char grade;

    printf("Enter age: ");
    scanf("%d", &age);

    printf("Enter height: ");
    scanf("%f", &height);

    printf("Enter grade: ");
    scanf(" %c", &grade);

    printf("\nAge = %d\n", age);
    printf("Height = %.2f\n", height);
    printf("Grade = %c\n", grade);

    return 0;
}
```

---

# 14. কোন Data Type কখন ব্যবহার করব?

সহজ rule:

|Data|Type|
|---|---|
|`15`|`int`|
|`-20`|`int`|
|`3.14`|`float` / `double`|
|`99.99`|`float` / `double`|
|`'A'`|`char`|
|`"Hello"`|`char[]`|

---

# 15. একটি Common Mistake

এটা:

```c
int price = 99.99;
```

সঠিক choice নয়, কারণ `int` পূর্ণসংখ্যার জন্য।

Decimal value দরকার হলে:

```c
float price = 99.99;
```

অথবা:

```c
double price = 99.99;
```

ব্যবহার করো।

---

# 16. Integer Division — খুব গুরুত্বপূর্ণ 🔥

এখন একটি interesting ব্যাপার:

```c
#include <stdio.h>

int main() {
    int a = 5;
    int b = 2;

    printf("%d\n", a / b);

    return 0;
}
```

Output:

```text
2
```

অনেকে ভাবতে পারে `2.5` হবে।

কিন্তু দুই operand-ই `int`, তাই **integer division** হচ্ছে।

যদি decimal result চাও:

```c
#include <stdio.h>

int main() {
    double result;

    result = 5.0 / 2.0;

    printf("%.2f\n", result);

    return 0;
}
```

Output:

```text
2.50
```

Type casting lesson-এ আমরা আরও গভীরে যাব।

---

# 🧠 আজকের Mental Model

মনে রাখো:

```text
int
 ↓
পূর্ণসংখ্যা

float
 ↓
decimal number

double
 ↓
আরও precision-এর decimal number

char
 ↓
একটি character
```

আর:

```text
%d → int
%f → float
%f → double-এর printf output
%c → char
%s → string
```

`scanf()`-এ:

```text
%d  → int
%f  → float
%lf → double
%c  → char
```

---

# 🧪 Practice 1

এই variables তৈরি করো:

```text
age = 16
height = 5.7
grade = A
```

তারপর সুন্দরভাবে print করো।

Expected:

```text
Age = 16
Height = 5.70
Grade = A
```

---

# 🧪 Practice 2

User-এর কাছ থেকে নাও:

- Age
    
- Height
    
- Grade
    

তারপর সবগুলো print করো।

---

# 🔥 Mini Challenge

একটি program বানাও যেখানে user:

```text
Enter price:
Enter quantity:
```

দেবে।

তারপর:

```text
Total = price × quantity
```

calculate করবে।

**Hint:** `price` এবং `Total`-এর জন্য decimal result দরকার হতে পারে, তাই data type বেছে নেওয়ার সময় চিন্তা করো।

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়

Data type শুধু syntax নয়। যখন variable বানাবে, নিজেকে জিজ্ঞেস করবে:

> **"এই variable-এ আমি কী ধরনের data রাখছি?"**

তারপর সেই অনুযায়ী type নির্বাচন করবে।

পরের Lesson → **Lesson 6 — Constants**: কীভাবে এমন value তৈরি করব যেটা program চলাকালীন পরিবর্তন করা যাবে না, `const` কী, এবং `#define` কীভাবে কাজ করে।

----
# 🚀 Lesson 6 — Constants

আজ আমরা শিখব **Constant** কী, কেন ব্যবহার করি, `const` কীভাবে কাজ করে, এবং `#define` সম্পর্কে।

---

# 1. Constant কী?

**Constant হলো এমন একটি value যা program চলার সময় পরিবর্তন করার কথা নয়।**

উদাহরণ:

```c
const int DAYS_IN_WEEK = 7;
```

এখানে `DAYS_IN_WEEK`-এর value `7`।

আমরা পরে এটাকে পরিবর্তন করতে পারি না।

---

# 2. Variable বনাম Constant

Variable:

```c
int age = 15;

age = 16;
```

এখানে value পরিবর্তন করা যায়।

Constant:

```c
const int days = 7;

days = 8;  // ❌
```

এখানে compiler error দেবে।

সহজভাবে:

```text
Variable
   ↓
Value পরিবর্তন করা যায়

Constant
   ↓
Value পরিবর্তন করার কথা নয়
```

---

# 3. `const` Keyword

C-তে constant variable তৈরি করার সবচেয়ে সহজ উপায়:

```c
const int MAX_SCORE = 100;
```

এখানে:

```text
const
 ↓
Value পরিবর্তন করা যাবে না

int
 ↓
Data type

MAX_SCORE
 ↓
Constant-এর নাম

100
 ↓
Value
```

---

# 4. Example

```c
#include <stdio.h>

int main() {
    const int DAYS_IN_WEEK = 7;

    printf("Days in a week = %d\n", DAYS_IN_WEEK);

    return 0;
}
```

Output:

```text
Days in a week = 7
```

---

# 5. Constant পরিবর্তন করার চেষ্টা

```c
#include <stdio.h>

int main() {
    const int DAYS_IN_WEEK = 7;

    DAYS_IN_WEEK = 8;

    return 0;
}
```

এটি compile করলে error হবে।

কারণ `DAYS_IN_WEEK` একটি `const` variable।

---

# 6. কেন Constant ব্যবহার করব?

ধরো একটি program-এ তুমি বারবার `100` ব্যবহার করছ:

```c
if (score <= 100) {
    ...
}
```

আরও অনেক জায়গায়:

```c
if (marks == 100) {
    ...
}
```

এখানে `100` আসলে maximum score।

তাই:

```c
const int MAX_SCORE = 100;
```

তারপর:

```c
if (score <= MAX_SCORE) {
    ...
}
```

এতে code-এর meaning পরিষ্কার হয়।

---

# 7. Naming Convention

Constant-এর নাম সাধারণত uppercase লেখা হয়:

```c
const int MAX_SCORE = 100;
const int DAYS_IN_WEEK = 7;
const int MONTHS_IN_YEAR = 12;
```

এটি C-এর বাধ্যতামূলক rule নয়।

অর্থাৎ:

```c
const int maxScore = 100;
```

এটিও valid।

কিন্তু uppercase convention ব্যবহার করলে code দেখে সহজে বোঝা যায় যে এটি একটি constant।

---

# 8. `const` দিয়ে বিভিন্ন Data Type

শুধু `int` নয়।

### Integer

```c
const int MAX_USERS = 100;
```

### Float

```c
const float PI = 3.14f;
```

### Double

```c
const double PI = 3.141592653589793;
```

### Character

```c
const char GRADE = 'A';
```

---

# 9. `const` বনাম `#define`

C-তে constant-এর আরেকটি পুরোনো/প্রচলিত পদ্ধতি হলো:

```c
#define PI 3.14159
```

এটি `const` থেকে আলাদা।

সহজভাবে এখন:

```text
const
 ↓
Typed constant variable

#define
 ↓
Preprocessor macro
```

`#define` আমরা **Preprocessor** lesson-এ বিস্তারিত শিখব।

---

# 10. `#define` Example

```c
#include <stdio.h>

#define DAYS_IN_WEEK 7

int main() {
    printf("%d\n", DAYS_IN_WEEK);

    return 0;
}
```

Output:

```text
7
```

এখানে `DAYS_IN_WEEK` একটি macro।

---

# 11. `const` নাকি `#define`?

Beginner হিসেবে সাধারণ constant value-এর ক্ষেত্রে `const` ব্যবহার করা ভালো অভ্যাস:

```c
const int MAX_SCORE = 100;
```

কারণ এটি একটি নির্দিষ্ট data type-এর object তৈরি করে।

`#define` সম্পর্কে বিস্তারিত পরে **Preprocessor** chapter-এ দেখব।

---

# 12. Practical Example — Circle

ধরো circle-এর area:

```text
Area = π × r × r
```

আমরা π-এর জন্য constant ব্যবহার করতে পারি:

```c
#include <stdio.h>

int main() {
    const double PI = 3.141592653589793;
    double radius = 5;

    double area = PI * radius * radius;

    printf("Area = %.2f\n", area);

    return 0;
}
```

Output:

```text
Area = 78.54
```

এখানে `PI` পরিবর্তন হওয়ার দরকার নেই, তাই constant হিসেবে রাখা হয়েছে।

---

# 13. User Input এবং `const`

একটি গুরুত্বপূর্ণ বিষয়:

```c
const int age;
```

তারপর:

```c
scanf("%d", &age);
```

এভাবে constant-এর মধ্যে input নেওয়া ঠিক নয়।

কারণ user input নেওয়ার value পরিবর্তনশীল।

তার জন্য সাধারণ variable:

```c
int age;

scanf("%d", &age);
```

ব্যবহার করবে।

---

# 14. কখন Constant ব্যবহার করব?

যেসব value program-এর logic-এ fixed:

```text
Days in a week = 7
Months in a year = 12
Maximum score = 100
Pi ≈ 3.14159
```

এসবের জন্য constant useful।

কিন্তু:

```text
User's age
User's score
Product quantity
User's name
```

এসব সাধারণত variable হবে।

---

# 🧪 Practice 1

এই constants তৈরি করো:

```text
MAX_SCORE = 100
DAYS_IN_WEEK = 7
MONTHS_IN_YEAR = 12
```

তারপর `printf()` দিয়ে তিনটিই print করো।

---

# 🧪 Practice 2

Circle-এর area বের করো।

User radius input দেবে:

```text
Enter radius: 10
```

তারপর:

```text
Area = 314.16
```

এর জন্য `PI`-কে `const` হিসেবে রাখো।

---

# 🔥 Mini Challenge

একটি program বানাও যেখানে:

```text
const double TAX_RATE = ...
```

তারপর user একটি product price input দেবে এবং tax যোগ করে final price বের করবে।

এখানে লক্ষ্য হলো **constant কেন useful সেটা নিজে অনুভব করা**।

---

# 🧠 আজকের Cheat Sheet

### Variable

```c
int age = 15;
age = 16;
```

Value পরিবর্তন করা যায়।

### Constant

```c
const int DAYS = 7;
```

Value পরিবর্তন করা উচিত/যায় না।

### Macro

```c
#define PI 3.14159
```

এটি preprocessor macro; পরে বিস্তারিত শিখব।

---

## 🎯 আজকের Core Concept

```text
Variable
    ↓
পরিবর্তনশীল data

Constant
    ↓
Fixed data
```

পরের Lesson → **Lesson 7 — Operators** 🔥

সেখানে আমরা `+`, `-`, `*`, `/`, `%`, comparison operators, logical operators এবং assignment operators দিয়ে বাস্তব calculation ও condition তৈরি করা শুরু করব।


---
# 🚀 Lesson 7 — Operators

আজ আমরা C-এর **Operators** শিখব। Operator হলো এমন symbol/চিহ্ন যা data-এর উপর কোনো operation করে।

যেমন:

```c
a + b
```

এখানে `+` হলো operator।

C-তে operators খুব গুরুত্বপূর্ণ, কারণ calculation, comparison, condition—সব জায়গাতেই এগুলো ব্যবহার হবে।

---

# 1. Arithmetic Operators

সবচেয়ে basic operators:

|Operator|কাজ|Example|
|---|---|---|
|`+`|যোগ|`a + b`|
|`-`|বিয়োগ|`a - b`|
|`*`|গুণ|`a * b`|
|`/`|ভাগ|`a / b`|
|`%`|ভাগশেষ|`a % b`|

---

## `+` Addition

```c
int a = 10;
int b = 5;

int result = a + b;
```

Result:

```text
15
```

---

## `-` Subtraction

```c
int result = a - b;
```

যদি:

```text
a = 10
b = 5
```

তাহলে:

```text
result = 5
```

---

## `*` Multiplication

```c
int result = a * b;
```

`10 × 5 = 50`

---

## `/` Division

```c
int result = a / b;
```

যদি:

```text
a = 10
b = 5
```

তাহলে:

```text
result = 2
```

কিন্তু মনে রেখো:

```c
int result = 5 / 2;
```

Result হবে:

```text
2
```

কারণ দুইটি operand-ই integer।

Decimal result চাইলে:

```c
double result = 5.0 / 2.0;
```

Result:

```text
2.5
```

---

# 2. `%` Modulus Operator 🔥

`%` **ভাগশেষ** বের করে।

```c
int result = 10 % 3;
```

10 কে 3 দিয়ে ভাগ করলে:

```text
10 ÷ 3
Quotient = 3
Remainder = 1
```

তাই:

```text
result = 1
```

আর:

```c
17 % 5
```

এর result:

```text
2
```

---

## `%` কোথায় ব্যবহার হয়?

ধরো কোনো number even নাকি odd সেটা বের করতে চাই।

```c
int number = 10;

if (number % 2 == 0) {
    printf("Even");
}
```

এখানে:

```text
10 % 2 = 0
```

তাই numberটি even।

`if` আমরা পরের Phase-এ বিস্তারিত শিখব।

---

# 3. Assignment Operator `=`

আমরা আগেও দেখেছি:

```c
int age = 15;
```

এখানে `=` value assign করে।

```c
age = 20;
```

মানে:

> `age`-এর মধ্যে `20` রাখো।

---

# 4. Compound Assignment Operators

C-তে shortcut assignment আছে।

ধরো:

```c
int x = 10;

x = x + 5;
```

এটা সংক্ষেপে লেখা যায়:

```c
x += 5;
```

দুটোর result একই:

```text
x = 15
```

আরও:

|Operator|Example|Equivalent|
|---|---|---|
|`+=`|`x += 5`|`x = x + 5`|
|`-=`|`x -= 5`|`x = x - 5`|
|`*=`|`x *= 5`|`x = x * 5`|
|`/=`|`x /= 5`|`x = x / 5`|
|`%=`|`x %= 5`|`x = x % 5`|

---

# 5. Increment `++`

`++` একটি variable-এর value **1 বাড়ায়**।

```c
int x = 10;

x++;
```

এখন:

```text
x = 11
```

এটি equivalent:

```c
x = x + 1;
```

---

# 6. Decrement `--`

`--` value 1 কমায়।

```c
int x = 10;

x--;
```

এখন:

```text
x = 9
```

Equivalent:

```c
x = x - 1;
```

---

# 7. Pre-increment এবং Post-increment

এটা একটু advanced, কিন্তু এখন থেকেই basic idea দেখে রাখো।

### Post-increment

```c
x++;
```

### Pre-increment

```c
++x;
```

দুটিই শেষে `x`-এর value 1 বাড়ায়।

কিন্তু কোনো expression-এর ভিতরে ব্যবহারের সময় তাদের আচরণ আলাদা হতে পারে।

যেমন:

```c
int x = 5;
int y = x++;
```

এখানে `y` প্রথমে `5` পাবে, তারপর `x` হবে `6`।

অন্যদিকে:

```c
int x = 5;
int y = ++x;
```

এখানে আগে `x` হবে `6`, তারপর `y` হবে `6`।

এখন শুধু এই concept মনে রাখো। পরে loops-এর সময় আরও practice করব।

---

# 8. Relational Operators

এগুলো দুইটি value compare করে।

|Operator|অর্থ|
|---|---|
|`==`|Equal|
|`!=`|Not equal|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater than or equal|
|`<=`|Less than or equal|

উদাহরণ:

```c
10 > 5
```

সত্য।

```c
10 < 5
```

মিথ্যা।

---

# 9. `=` বনাম `==` 🔥

এটি beginner-এর সবচেয়ে common mistakeগুলোর একটি।

### Assignment

```c
x = 10;
```

মানে:

> x-এর মধ্যে 10 রাখো।

### Comparison

```c
x == 10
```

মানে:

> x কি 10-এর সমান?

মনে রাখো:

```text
=   → value assign
==  → equality check
```

---

# 10. Logical Operators

Logical operators দিয়ে একাধিক condition combine করা যায়।

|Operator|অর্থ|
|---|---|
|`&&`|AND|
|`||
|`!`|NOT|

### AND `&&`

দুটি condition-ই true হতে হবে।

```text
A && B
```

মানে:

```text
A সত্য
এবং
B সত্য
```

### OR `||`

কমপক্ষে একটি true হলেই হবে।

```text
A || B
```

### NOT `!`

True-কে false এবং false-কে true করে।

এগুলো আমরা `if` lesson-এ অনেক practical example দিয়ে ব্যবহার করব।

---

# 11. একটি Real Example

ধরো:

```c
int age = 18;
```

আমরা check করতে পারি:

```c
age >= 18
```

এটি true হবে।

আর:

```c
age < 18
```

false হবে।

---

# 12. Operator Precedence

একটি expression-এ একাধিক operator থাকলে কোনটি আগে calculate হবে, তার rules আছে।

যেমন:

```c
int result = 10 + 5 * 2;
```

এখানে আগে multiplication:

```text
5 × 2 = 10
```

তারপর:

```text
10 + 10 = 20
```

তাই:

```text
result = 20
```

---

# 13. Parentheses ব্যবহার করো

যদি তুমি আগে addition করতে চাও:

```c
int result = (10 + 5) * 2;
```

এখন:

```text
10 + 5 = 15
15 × 2 = 30
```

তাই:

```text
result = 30
```

Beginner হিসেবে একটি ভালো অভ্যাস:

> Complex expression হলে parentheses ব্যবহার করো।

এতে code পড়া এবং ভুল কমানো সহজ হয়।

---

# 14. Complete Operator Example

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 3;

    printf("Addition = %d\n", a + b);
    printf("Subtraction = %d\n", a - b);
    printf("Multiplication = %d\n", a * b);
    printf("Division = %d\n", a / b);
    printf("Remainder = %d\n", a % b);

    return 0;
}
```

Output:

```text
Addition = 13
Subtraction = 7
Multiplication = 30
Division = 3
Remainder = 1
```

---

# 15. User Input দিয়ে Calculator

এবার আগের lessons combine করি:

```c
#include <stdio.h>

int main() {
    int a, b;

    printf("Enter first number: ");
    scanf("%d", &a);

    printf("Enter second number: ");
    scanf("%d", &b);

    printf("Sum = %d\n", a + b);
    printf("Difference = %d\n", a - b);
    printf("Product = %d\n", a * b);

    if (b != 0) {
        printf("Quotient = %d\n", a / b);
        printf("Remainder = %d\n", a % b);
    }

    return 0;
}
```

এখানে নতুন করে:

```c
if (b != 0)
```

ব্যবহার করা হয়েছে, কারণ zero দিয়ে division করা যাবে না। `if` আমরা পরের Phase-এ বিস্তারিত শিখব।

---

# 🧪 Practice 1

User-এর কাছ থেকে দুইটি integer নাও এবং বের করো:

```text
Sum
Difference
Product
Quotient
Remainder
```

---

# 🧪 Practice 2

এই expression-এর result আগে নিজে অনুমান করো:

```c
int result = 10 + 5 * 2;
```

তারপর:

```c
int result = (10 + 5) * 2;
```

দুটির result কেন আলাদা হয় তা বোঝার চেষ্টা করো।

---

# 🔥 Mini Challenge

User একটি number দেবে।

Program output করবে:

```text
Number = 17
Previous = 16
Next = 18
Double = 34
Triple = 51
Remainder when divided by 2 = 1
```

Hint:

```c
number - 1
number + 1
number * 2
number * 3
number % 2
```

---

# 🧠 আজকের Cheat Sheet

```text
Arithmetic
+   -   *   /   %

Assignment
=
+=  -=  *=  /=  %=

Increment / Decrement
++  --

Comparison
==  !=  >  <  >=  <=

Logical
&&  ||  !
```

সবচেয়ে গুরুত্বপূর্ণ তিনটি মনে রাখো:

```text
=   → assign
==  → compare
%   → remainder
```

### 🎯 আজকের Core Idea

```text
Data
 ↓
Operators
 ↓
Calculation / Comparison
 ↓
Result
```

পরের Lesson → **Lesson 8 — Type Casting** 🔥  
সেখানে দেখব `int` থেকে `float`/`double`-এ conversion কীভাবে করা যায়, কেন `5 / 2` → `2` হয়, এবং কীভাবে সেটাকে `2.5` করা যায়।

---
# 🚀 Lesson 8 — Type Casting

আজকের lesson খুব গুরুত্বপূর্ণ, কারণ এখানে আমরা শিখব **এক data type-এর value অন্য data type-এ কীভাবে convert করতে হয়**।

বিশেষ করে এই classic problem:

```c
int result = 5 / 2;
```

কেন `2` হয়, `2.5` নয়?

চলো বুঝি।

---

# 1. Type Casting কী?

**Type casting হলো একটি value-কে অন্য data type হিসেবে ব্যবহার করার জন্য convert করা।**

যেমন:

```text
int
 ↓
double
```

অথবা:

```text
double
 ↓
int
```

---

# 2. সবচেয়ে সহজ Example

ধরো:

```c
int x = 10;
```

আমরা এটাকে `double` হিসেবে ব্যবহার করতে পারি:

```c
(double)x
```

এখানে:

```text
(double)
   ↓
বলছে x-কে double হিসেবে treat করো
```

---

# 3. C-এর Casting Syntax

Basic syntax:

```c
(type) value
```

উদাহরণ:

```c
(double) x
```

আরও:

```c
(float) x
(char) x
(int) x
```

---

# 4. কেন Type Casting দরকার?

এই code দেখো:

```c
#include <stdio.h>

int main() {
    int a = 5;
    int b = 2;

    printf("%d\n", a / b);

    return 0;
}
```

Output:

```text
2
```

কিন্তু mathematical answer:

```text
5 ÷ 2 = 2.5
```

কেন C `2` দিল?

কারণ:

```text
int / int
   ↓
integer division
   ↓
2
```

---

# 5. Casting দিয়ে সমাধান 🔥

আমরা `a`-কে `double` করে দিতে পারি:

```c
#include <stdio.h>

int main() {
    int a = 5;
    int b = 2;

    double result = (double)a / b;

    printf("%.2f\n", result);

    return 0;
}
```

Output:

```text
2.50
```

এখানে:

```c
(double)a
```

এর কারণে expression-টি floating-point division হিসেবে evaluate হয়েছে।

---

# 6. Step by Step

ধরো:

```c
int a = 5;
int b = 2;
```

প্রথমে:

```c
(double)a
```

হলে:

```text
5
↓
5.0
```

তারপর:

```text
5.0 / 2
↓
2.5
```

তাই result:

```text
2.5
```

---

# 7. Implicit Conversion

সবসময় manually casting করতে হয় না।

C অনেক সময় নিজে থেকেই type conversion করে।

উদাহরণ:

```c
int a = 5;
double b = 2.0;

double result = a / b;
```

এখানে `a` automatically floating-point type-এর সঙ্গে compatible form-এ convert হবে।

ফলে:

```text
5 / 2.0
↓
2.5
```

এটাকে সাধারণভাবে **implicit conversion** বলা হয়।

---

# 8. Explicit Casting

যখন আমরা নিজেরা conversion বলে দিই:

```c
(double)a
```

এটি **explicit type casting**।

দুটি concept:

```text
Implicit
↓
Compiler নিজে conversion করে

Explicit
↓
Programmer নিজে conversion বলে দেয়
```

---

# 9. Double থেকে Int

এবার উল্টো দিকে যাই।

```c
double price = 99.99;

int x = (int)price;
```

এখন:

```text
price = 99.99
x     = 99
```

এখানে decimal অংশটি রাখা হয়নি।

---

# 10. এটি Rounding নয়

এটি খুব গুরুত্বপূর্ণ।

```c
double x = 7.9;
int y = (int)x;
```

`y` হবে:

```text
7
```

এটা `8` হবে না।

অর্থাৎ সাধারণ cast **rounding করে না**, fractional part বাদ দেয়।

আর:

```c
double x = 7.2;
int y = (int)x;
```

হলেও:

```text
y = 7
```

---

# 11. Negative Number-এর ক্ষেত্রে

উদাহরণ:

```c
double x = -7.9;
int y = (int)x;
```

সাধারণভাবে result হবে:

```text
-7
```

অর্থাৎ fractional অংশ বাদ যায়।

---

# 12. `char` Casting

C-তে character এবং integer-এর মধ্যে conversion করা যায়।

উদাহরণ:

```c
char ch = 'A';

printf("%d\n", (int)ch);
```

ASCII-এর ক্ষেত্রে output:

```text
65
```

আবার:

```c
int x = 66;

printf("%c\n", (char)x);
```

Output:

```text
B
```

এখানে character encoding-এর বিষয় আছে; এখন ASCII-এর basic idea জানলেই যথেষ্ট।

---

# 13. Average বের করার সময় Type Casting 🔥

ধরো তিনটি marks:

```c
int a = 80;
int b = 90;
int c = 70;
```

Average:

```c
int average = (a + b + c) / 3;
```

এখানে result integer হবে।

যদি decimal average দরকার হয়:

```c
double average = (double)(a + b + c) / 3;
```

তাহলে:

```text
80 + 90 + 70 = 240

240 / 3 = 80.0
```

যদি এমন values হয়:

```text
80 + 91 + 70 = 241
```

তাহলে:

```text
241 / 3 = 80.333...
```

এবং `double` সেটা রাখতে পারবে।

---

# 14. Practical Average Program

```c
#include <stdio.h>

int main() {
    int mark1, mark2, mark3;
    double average;

    printf("Enter mark 1: ");
    scanf("%d", &mark1);

    printf("Enter mark 2: ");
    scanf("%d", &mark2);

    printf("Enter mark 3: ");
    scanf("%d", &mark3);

    average = (double)(mark1 + mark2 + mark3) / 3;

    printf("Average = %.2f\n", average);

    return 0;
}
```

যদি input:

```text
80
91
70
```

হয়, output:

```text
Average = 80.33
```

---

# 15. Casting-এর একটি Common Mistake

এটা:

```c
double result = (double)(5 / 2);
```

তোমাকে `2.0` দেবে, `2.5` নয়।

কেন?

কারণ প্রথমে:

```text
5 / 2
↓
2
```

তারপর:

```text
(double)2
↓
2.0
```

অর্থাৎ casting **division-এর পরে** হয়েছে।

সঠিক:

```c
double result = (double)5 / 2;
```

এখানে:

```text
(double)5
↓
5.0

5.0 / 2
↓
2.5
```

🔥 এই পার্থক্যটি খুব গুরুত্বপূর্ণ।

---

# 16. Another Example

ভুল:

```c
double result = (double)(10 / 4);
```

Result:

```text
2.0
```

সঠিক:

```c
double result = (double)10 / 4;
```

Result:

```text
2.5
```

---

# 17. Type Casting-এর Mental Model

এই দুইটা expression-এর পার্থক্য মনে রাখো:

```text
(double)(5 / 2)
       ↓
আগে division
       ↓
2
       ↓
2.0
```

কিন্তু:

```text
(double)5 / 2
       ↓
5.0 / 2
       ↓
2.5
```

---

# 🧪 Practice 1

নিজে অনুমান করো:

```c
int a = 7;
int b = 2;

double x = a / b;
double y = (double)a / b;
```

তাহলে:

```text
x = ?
y = ?
```

---

# 🧪 Practice 2

এই program-এ average বের করো:

```text
Mark 1 = 85
Mark 2 = 92
Mark 3 = 78
Mark 4 = 91
```

Average যেন decimal-এ আসে।

---

# 🔥 Mini Challenge

User-এর কাছ থেকে দুটি integer নাও:

```text
Enter numerator:
Enter denominator:
```

তারপর:

```text
Integer division = ...
Decimal division = ...
```

উদাহরণ:

```text
Enter numerator: 7
Enter denominator: 2

Integer division = 3
Decimal division = 3.50
```

Hint:

```c
a / b
```

এবং:

```c
(double)a / b
```

দুটো ব্যবহার করো।

---

# 🧠 আজকের Cheat Sheet

### Explicit casting

```c
(double)x
```

### Integer → Double

```c
int x = 5;
double y = (double)x;
```

### Double → Integer

```c
double x = 5.9;
int y = (int)x;
```

`y` হবে `5`।

### Integer division

```c
5 / 2
```

→ `2`

### Decimal division

```c
(double)5 / 2
```

→ `2.5`

### সবচেয়ে গুরুত্বপূর্ণ

```c
(double)(5 / 2)  // 2.0
(double)5 / 2    // 2.5
```

---

## 🎯 Phase 1-এর শেষ Lesson

পরের Lesson → **Lesson 9 — Comments + Coding Style**

সেখানে আমরা শিখব code-এর মধ্যে notes কীভাবে লিখতে হয়, `//` এবং `/* */` কী, এবং **clean/readable C code** কীভাবে লিখতে হয়।

----
# 🚀 Lesson 9 — Comments + Coding Style

🎉 **Phase 1-এর শেষ Lesson!**

আজ আমরা শিখব:

1. Comment কী
    
2. `//` single-line comment
    
3. `/* ... */` multi-line comment
    
4. Comment কেন ব্যবহার করি
    
5. ভালো variable naming
    
6. Indentation ও formatting
    
7. Clean C code কীভাবে লিখতে হয়
    

---

# 1. Comment কী?

**Comment হলো code-এর মধ্যে programmer-এর জন্য লেখা note, যেটা compiler সাধারণত executable instruction হিসেবে বিবেচনা করে না।**

যেমন:

```c
int age = 15; // User's age
```

এখানে:

```text
int age = 15;
```

→ actual code

```text
// User's age
```

→ comment

Comment program-এর logic বোঝাতে সাহায্য করে।

---

# 2. Single-Line Comment — `//`

`//` দিয়ে comment শুরু করলে ওই line-এর বাকি অংশ comment হয়ে যায়।

```c
#include <stdio.h>

int main() {
    // This is a comment
    printf("Hello\n");

    return 0;
}
```

Program output:

```text
Hello
```

Comment output-এ দেখা যায় না।

---

# 3. Code-এর শেষে Comment

এভাবেও লেখা যায়:

```c
int age = 15; // Store the user's age
```

এটি খুব useful হতে পারে।

---

# 4. Multi-Line Comment

একাধিক line comment করতে:

```c
/*
This is a multi-line comment.
It can contain multiple lines.
The compiler ignores this as code.
*/
```

Example:

```c
#include <stdio.h>

int main() {

    /*
       This program calculates
       the sum of two numbers.
    */

    int a = 10;
    int b = 20;

    printf("%d\n", a + b);

    return 0;
}
```

---

# 5. `//` বনাম `/* */`

|Syntax|ব্যবহার|
|---|---|
|`// comment`|Single line|
|`/* comment */`|Multiple lines|

সাধারণভাবে ছোট note-এর জন্য:

```c
// Calculate total
```

আর বড় explanation-এর জন্য:

```c
/*
    Calculate the total
    price after applying
    the discount.
*/
```

---

# 6. Comment কেন ব্যবহার করব?

Comment-এর উদ্দেশ্য হলো **code বোঝানো**।

ধরো:

```c
int x = 365;
```

এখানে `365` কেন?

Code দেখে বোঝা কঠিন।

কিন্তু:

```c
int days = 365; // Number of days in a normal year
```

এখন meaning পরিষ্কার।

---

# 7. বেশি Comment-ও ভালো নয়

এটা:

```c
// Create an integer variable called age
int age = 15;
```

অপ্রয়োজনীয়।

কারণ code নিজেই পরিষ্কার।

ভালো:

```c
int age = 15;
```

আর যদি বিশেষ explanation দরকার হয়, তখন comment দাও।

---

# 8. ভালো Variable Naming

খারাপ:

```c
int x;
int y;
int z;
```

যদি এগুলোর অর্থ বোঝা না যায়।

ভালো:

```c
int age;
int totalMarks;
int studentCount;
```

এতে code নিজেই অনেকটা explain করে।

---

# 9. Naming Convention

C-তে বিভিন্ন style দেখা যায়।

### snake_case

```c
student_age
total_marks
maximum_score
```

### camelCase

```c
studentAge
totalMarks
maximumScore
```

দুটিই valid।

তুমি একটি style বেছে নিয়ে consistently ব্যবহার করতে পারো।

---

# 10. Constant Naming

Constant-এর জন্য uppercase convention খুব common:

```c
const int MAX_SCORE = 100;
const int DAYS_IN_WEEK = 7;
```

---

# 11. Indentation

এই code কাজ করবে:

```c
#include <stdio.h>
int main(){
int age=15;
printf("%d\n",age);
return 0;
}
```

কিন্তু পড়তে কষ্ট হয়।

ভালো formatting:

```c
#include <stdio.h>

int main() {
    int age = 15;

    printf("%d\n", age);

    return 0;
}
```

দুটোই একই কাজ করে, কিন্তু দ্বিতীয়টি অনেক বেশি readable।

---

# 12. Indentation কেন গুরুত্বপূর্ণ?

Code block-এর ভিতরের code একটু ভিতরে রাখলে structure বোঝা যায়।

যেমন:

```c
int main() {
    int age = 15;

    if (age >= 18) {
        printf("Adult\n");
    }

    return 0;
}
```

এখানে কোন code কোন block-এর ভিতরে আছে সহজে বোঝা যায়।

---

# 13. এক Statement প্রতি Line

এভাবে:

```c
int age = 15; int score = 90; printf("%d %d", age, score);
```

valid হতে পারে, কিন্তু readability খারাপ।

ভালো:

```c
int age = 15;
int score = 90;

printf("%d %d", age, score);
```

---

# 14. Meaningful Spacing

এটা:

```c
int a=10;
int b=20;
int sum=a+b;
```

এর চেয়ে:

```c
int a = 10;
int b = 20;

int sum = a + b;
```

অনেক পরিষ্কার।

---

# 15. Function-এর Formatting

আজ আমরা function-এর details এখনো শেখিনি, কিন্তু formatting-এর example:

```c
int calculateSum(int a, int b) {
    return a + b;
}
```

এভাবে indentation রাখলে structure পরিষ্কার থাকে।

---

# 16. একটি Clean Program

এখন Phase 1-এর অনেক concept একসঙ্গে ব্যবহার করি:

```c
#include <stdio.h>

int main() {
    // Declare variables
    int firstNumber;
    int secondNumber;

    // Get input from the user
    printf("Enter first number: ");
    scanf("%d", &firstNumber);

    printf("Enter second number: ");
    scanf("%d", &secondNumber);

    // Calculate and display the sum
    int sum = firstNumber + secondNumber;

    printf("Sum = %d\n", sum);

    return 0;
}
```

এখানে আমরা ব্যবহার করেছি:

- `#include`
    
- `main()`
    
- Variables
    
- `int`
    
- `printf()`
    
- `scanf()`
    
- Operators
    
- Comments
    
- Proper indentation
    

---

# 17. Comment-এর একটি গুরুত্বপূর্ণ ব্যবহার

কখনো debugging করার সময় code সাময়িকভাবে disable করতে comment ব্যবহার করা হয়।

যেমন:

```c
printf("Step 1\n");
// printf("Step 2\n");
printf("Step 3\n");
```

Output:

```text
Step 1
Step 3
```

`Step 2` line comment হয়ে যাওয়ায় execute হয়নি।

তবে debugging-এর জন্য বড় codebase-এ comments রেখে যাওয়া সবসময় ভালো practice নয়।

---

# 🧠 Clean Code-এর 7টি Rule

আজ থেকে চেষ্টা করো:

### 1️⃣ Meaningful names

```c
int studentAge;
```

### 2️⃣ Proper indentation

```c
if (condition) {
    statement;
}
```

### 3️⃣ Spaces ব্যবহার

```c
int total = a + b;
```

### 4️⃣ অপ্রয়োজনীয় comment নয়

Code যদি নিজেই clear হয়, comment দরকার নেই।

### 5️⃣ প্রয়োজনীয় জায়গায় comment

Complex logic হলে explanation দাও।

### 6️⃣ Consistent style

একবার `camelCase` ব্যবহার করলে অযথা `snake_case`-এ switch করো না।

### 7️⃣ Code ছোট ছোট logical অংশে রাখো

একটি বিশাল block না বানিয়ে structure পরিষ্কার রাখো।

---

# 🧪 Practice 1

এই messy code-টি clean করো:

```c
#include <stdio.h>
int main(){int age=15;int score=90;printf("Age=%d\n",age);printf("Score=%d\n",score);return 0;}
```

লক্ষ্য:

- Proper indentation
    
- Proper spacing
    
- Meaningful formatting
    

---

# 🧪 Practice 2

একটি program লেখো যেখানে:

```text
First number:
Second number:
```

input নেওয়া হবে এবং:

```text
Sum
Difference
Product
```

দেখাবে।

তার code-এ **কমপক্ষে ২টি useful comment** যোগ করো।

---

# 🔥 Phase 1 Final Challenge

এবার Phase 1-এর সব concept combine করো।

একটি ছোট **Student Information Program** বানাও।

Program:

1. Student-এর age input নেবে
    
2. তিনটি marks input নেবে
    
3. Total বের করবে
    
4. Average বের করবে
    
5. Student-এর grade input নেবে
    
6. সুন্দরভাবে সব information print করবে
    

Expected structure:

```text
Enter age: 16
Enter mark 1: 80
Enter mark 2: 90
Enter mark 3: 85
Enter grade: A

--- Student Information ---
Age = 16
Mark 1 = 80
Mark 2 = 90
Mark 3 = 85
Total = 255
Average = 85.00
Grade = A
```

এখানে তোমাকে ব্যবহার করতে হবে:

```text
Variables
Data types
Constants (যেখানে দরকার)
printf()
scanf()
Operators
Type casting
Comments
Clean coding style
```

---

# 🎉 Phase 1 Complete!

তুমি এখন C-এর foundation-এর এই বিষয়গুলো জানো:

```text
✅ C কী
✅ Compiler
✅ C setup
✅ প্রথম program
✅ printf()
✅ scanf()
✅ Variables
✅ Data Types
✅ Constants
✅ Operators
✅ Type Casting
✅ Comments
✅ Coding Style
```

### 🚀 Next: Phase 2 — Decision Making

এখন program-কে **decision নিতে শেখাব**।

আমাদের Phase 2:

```text
10. if
11. if-else
12. else-if
13. Nested if
14. switch-case
15. Ternary operator
```

প্রথমে শুরু হবে **Lesson 10 — `if` Statement**, যেখানে আমরা program-কে শেখাব:

> **"যদি এই condition সত্য হয়, তাহলে এই কাজ করো।"**


---
# 🚀 Phase 2 — Decision Making

# Lesson 10 — `if` Statement

এখন থেকে C program শুধু একের পর এক instruction execute করবে না—**condition অনুযায়ী decision নিতে পারবে।**

আজকের মূল বিষয়:

```c
if (condition) {
    // condition true হলে এই code চলবে
}
```

---

# 1. `if` কী?

`if` ব্যবহার করা হয় কোনো condition **সত্য (`true`) হলে** নির্দিষ্ট code execute করার জন্য।

সহজভাবে:

```text
যদি condition সত্য হয়
        ↓
    কাজ করো
```

উদাহরণ:

```c
#include <stdio.h>

int main() {
    int age = 18;

    if (age >= 18) {
        printf("You are an adult.\n");
    }

    return 0;
}
```

Output:

```text
You are an adult.
```

কারণ:

```text
18 >= 18
```

সত্য।

---

# 2. `if`-এর Syntax

```c
if (condition) {
    statement;
}
```

এখানে:

```text
if
 ↓
Decision keyword

condition
 ↓
যে বিষয়টি check করা হবে

{ }
 ↓
Condition true হলে যে code চলবে
```

---

# 3. Comparison Operator দিয়ে Condition

`if`-এর সঙ্গে আমরা comparison operators ব্যবহার করি।

```text
==    Equal
!=    Not equal
>     Greater than
<     Less than
>=    Greater than or equal
<=    Less than or equal
```

উদাহরণ:

```c
int age = 20;

if (age > 18) {
    printf("Age is greater than 18.\n");
}
```

এখানে:

```text
20 > 18
```

true, তাই `printf()` execute হবে।

---

# 4. Condition False হলে কী হয়?

```c
#include <stdio.h>

int main() {
    int age = 15;

    if (age >= 18) {
        printf("You are an adult.\n");
    }

    return 0;
}
```

এখানে:

```text
15 >= 18
```

false।

তাই `printf()` execute হবে না।

Output:

```text
কোনো output নেই
```

এটাই `if`-এর মূল behavior।

---

# 5. User Input + `if`

এবার `scanf()` ব্যবহার করি।

```c
#include <stdio.h>

int main() {
    int age;

    printf("Enter your age: ");
    scanf("%d", &age);

    if (age >= 18) {
        printf("You are eligible.\n");
    }

    return 0;
}
```

যদি input:

```text
20
```

তাহলে:

```text
You are eligible.
```

কিন্তু input:

```text
15
```

হলে কোনো output হবে না।

---

# 6. Even Number Check

`%` operator মনে আছে?

```c
number % 2
```

এর মাধ্যমে even/odd check করা যায়।

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number % 2 == 0) {
        printf("The number is even.\n");
    }

    return 0;
}
```

যদি:

```text
Enter a number: 10
```

তাহলে:

```text
The number is even.
```

কারণ:

```text
10 % 2 = 0
```

---

# 7. Positive Number Check

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number > 0) {
        printf("Positive number.\n");
    }

    return 0;
}
```

Input:

```text
25
```

Output:

```text
Positive number.
```

কিন্তু:

```text
-5
```

দিলে condition false হবে।

---

# 8. একাধিক `if`

একটি program-এ একাধিক `if` থাকতে পারে।

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number > 0) {
        printf("Positive\n");
    }

    if (number % 2 == 0) {
        printf("Even\n");
    }

    return 0;
}
```

Input:

```text
10
```

Output:

```text
Positive
Even
```

কারণ দুটি condition-ই true।

---

# 9. `if` + Logical AND `&&`

দুটি condition একসঙ্গে সত্য হতে চাইলে `&&` ব্যবহার করি।

```c
int age = 20;

if (age >= 18 && age <= 60) {
    printf("Age is in the range.\n");
}
```

এখানে দুটোই true হতে হবে:

```text
age >= 18
AND
age <= 60
```

---

# 10. `if` + Logical OR `||`

কমপক্ষে একটি condition true হলেই চলবে।

```c
int day = 6;

if (day == 6 || day == 7) {
    printf("Weekend.\n");
}
```

এখানে:

```text
day == 6
OR
day == 7
```

যেকোনো একটি সত্য হলেই message print হবে।

---

# 11. NOT `!`

`!` condition-এর logical opposite তৈরি করে।

উদাহরণ:

```c
int isReady = 0;

if (!isReady) {
    printf("Not ready.\n");
}
```

এখানে `isReady` false/zero হওয়ায় `!isReady` true হবে।

Boolean concept আমরা একটু পরে আরও পরিষ্কারভাবে দেখব।

---

# 12. C-তে `0` এবং Non-zero

C-তে condition-এর ক্ষেত্রে:

```text
0
```

মানে false।

আর সাধারণভাবে:

```text
যেকোনো non-zero value
```

মানে true।

উদাহরণ:

```c
if (0) {
    printf("Hello");
}
```

কিছু print হবে না।

কিন্তু:

```c
if (5) {
    printf("Hello");
}
```

Output:

```text
Hello
```

এখনকার জন্য এটুকু মনে রাখো:

```text
0       → false
non-zero → true
```

---

# 13. `if` Block-এর `{}`

এইভাবে লিখলে:

```c
if (age >= 18) {
    printf("Adult\n");
    printf("Eligible\n");
}
```

দুটি statement-ই condition true হলে execute হবে।

**Beginner হিসেবে সবসময় `{}` ব্যবহার করার অভ্যাস করো**, এমনকি একটি statement হলেও।

---

# 14. একটি Real Example — Pass Check

```c
#include <stdio.h>

int main() {
    int marks;

    printf("Enter marks: ");
    scanf("%d", &marks);

    if (marks >= 40) {
        printf("You passed.\n");
    }

    return 0;
}
```

Input:

```text
75
```

Output:

```text
You passed.
```

---

# 15. আরেকটি Example — Discount

ধরো product-এর price 1000-এর বেশি হলে discount message দেখাবে।

```c
#include <stdio.h>

int main() {
    double price;

    printf("Enter price: ");
    scanf("%lf", &price);

    if (price >= 1000) {
        printf("You get a discount!\n");
    }

    return 0;
}
```

---

# 🧪 Practice 1

একটি program লেখো যেখানে user একটি number দেবে।

যদি number:

```text
> 100
```

হয়, তাহলে print করবে:

```text
Number is greater than 100.
```

---

# 🧪 Practice 2

User-এর কাছ থেকে একটি integer নাও।

যদি সেটা **5 দিয়ে divisible** হয়:

```text
Divisible by 5
```

দেখাবে।

Hint:

```c
number % 5 == 0
```

---

# 🧪 Practice 3

User-এর age নাও।

যদি age `13` বা তার বেশি এবং `19` বা তার কম হয়:

```text
Teenager
```

print করো।

Hint:

```c
age >= 13 && age <= 19
```

---

# 🔥 Mini Challenge

একটি program বানাও যেখানে user একটি number input দেবে।

Program শুধু নিচের condition-গুলো অনুযায়ী message দেখাবে:

- number positive হলে → `Positive`
    
- number even হলে → `Even`
    
- number 100-এর বেশি হলে → `Greater than 100`
    

যেমন input:

```text
120
```

Output:

```text
Positive
Even
Greater than 100
```

---

# 🧠 আজকের Cheat Sheet

### Basic

```c
if (condition) {
    // code
}
```

### Comparison

```text
==  !=  >  <  >=  <=
```

### Logical

```text
&&  → AND
||  → OR
!   → NOT
```

### C condition

```text
0       → false
non-zero → true
```

### Example

```c
if (age >= 18) {
    printf("Adult\n");
}
```

---

## 🎯 আজকের মূল ধারণা

আগে program ছিল:

```text
Input
 ↓
Calculation
 ↓
Output
```

এখন যোগ হলো:

```text
Input
 ↓
Condition?
 ↙      ↘
Yes      No
 ↓        ↓
Action   Nothing
```

পরের Lesson → **Lesson 11 — `if-else`**।

সেখানে শিখব, condition **true হলে এক কাজ এবং false হলে অন্য কাজ** কীভাবে করানো যায়।

---

# 🚀 Lesson 11 — `if-else`

গত lesson-এ আমরা শিখেছি:

```c
if (condition) {
    // condition true হলে
}
```

কিন্তু যদি condition **false** হয় এবং তখনও আমাদের কিছু করতে হয়?

তখন ব্যবহার করব **`if-else`**।

---

# 1. `if-else` কী?

সহজভাবে:

```text
যদি condition সত্য হয়
        ↓
      কাজ A

নাহলে
        ↓
      কাজ B
```

Syntax:

```c
if (condition) {
    // true হলে
} else {
    // false হলে
}
```

---

# 2. সবচেয়ে সহজ Example

```c
#include <stdio.h>

int main() {
    int age = 15;

    if (age >= 18) {
        printf("Adult\n");
    } else {
        printf("Not an adult\n");
    }

    return 0;
}
```

এখানে:

```text
age = 15

15 >= 18
   ↓
 false
   ↓
else
   ↓
Not an adult
```

Output:

```text
Not an adult
```

---

# 3. User Input দিয়ে `if-else`

```c
#include <stdio.h>

int main() {
    int age;

    printf("Enter your age: ");
    scanf("%d", &age);

    if (age >= 18) {
        printf("Adult\n");
    } else {
        printf("Not an adult\n");
    }

    return 0;
}
```

যদি input:

```text
20
```

Output:

```text
Adult
```

যদি input:

```text
15
```

Output:

```text
Not an adult
```

---

# 4. Even / Odd

`if-else` শেখার জন্য এটি একটি classic problem।

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number % 2 == 0) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }

    return 0;
}
```

Input:

```text
7
```

কারণ:

```text
7 % 2 = 1
```

তাই output:

```text
Odd
```

Input:

```text
10
```

কারণ:

```text
10 % 2 = 0
```

তাই:

```text
Even
```

---

# 5. Pass / Fail

ধরো passing mark `40`।

```c
#include <stdio.h>

int main() {
    int marks;

    printf("Enter marks: ");
    scanf("%d", &marks);

    if (marks >= 40) {
        printf("Pass\n");
    } else {
        printf("Fail\n");
    }

    return 0;
}
```

Input:

```text
75
```

Output:

```text
Pass
```

Input:

```text
32
```

Output:

```text
Fail
```

---

# 6. Positive / Negative

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number >= 0) {
        printf("Non-negative\n");
    } else {
        printf("Negative\n");
    }

    return 0;
}
```

এখানে `0`-কে non-negative ধরা হয়েছে।

---

# 7. `if-else`-এ শুধু একটি Branch চলে

এটি খুব গুরুত্বপূর্ণ।

```c
if (condition) {
    printf("A\n");
} else {
    printf("B\n");
}
```

একটি execution-এ:

```text
A অথবা B
```

**দুটো একসঙ্গে নয়।**

Condition true হলে `if` block।

Condition false হলে `else` block।

---

# 8. `if` বনাম `if-else`

### শুধু `if`

```c
if (age >= 18) {
    printf("Adult\n");
}
```

Condition false হলে কিছুই হবে না।

### `if-else`

```c
if (age >= 18) {
    printf("Adult\n");
} else {
    printf("Minor\n");
}
```

Condition false হলেও `else`-এর code চলবে।

---

# 9. দুইটি Number-এর মধ্যে বড়টি বের করা

এটি খুব useful problem।

```c
#include <stdio.h>

int main() {
    int a, b;

    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);

    if (a > b) {
        printf("%d is greater\n", a);
    } else {
        printf("%d is greater\n", b);
    }

    return 0;
}
```

যদি:

```text
10 7
```

Output:

```text
10 is greater
```

---

# ⚠️ কিন্তু এখানে একটি সমস্যা আছে

যদি input হয়:

```text
10 10
```

তাহলে:

```c
if (a > b)
```

false।

তাই `else` চলবে:

```text
10 is greater
```

যদিও দুইটিই equal।

এখানে আমাদের তিনটি possibility:

```text
a > b
a < b
a == b
```

এটি সমাধান করতে পরের lesson-এর **`else-if`** ব্যবহার করব।

---

# 10. `else`-এর ভিতরে আবার `if`

এটাকে technically nested decision হিসেবে ব্যবহার করা যায়:

```c
if (a > b) {
    printf("A is greater\n");
} else {
    if (a == b) {
        printf("Equal\n");
    } else {
        printf("B is greater\n");
    }
}
```

কিন্তু এই ধরনের code আরও সুন্দরভাবে `else-if` দিয়ে লেখা যায়:

```c
if (a > b) {
    printf("A is greater\n");
} else if (a == b) {
    printf("Equal\n");
} else {
    printf("B is greater\n");
}
```

এটাই পরের lesson-এর বিষয়।

---

# 11. `if-else` + Logical Operators

একাধিক condition ব্যবহার করা যায়।

উদাহরণ:

```c
int age = 20;

if (age >= 18 && age <= 60) {
    printf("Eligible age range\n");
} else {
    printf("Outside age range\n");
}
```

---

# 12. `if-else` + `&&`

ধরো exam-এ pass করতে:

- marks ≥ 40
    
- attendance ≥ 75
    

দুটিই দরকার।

```c
#include <stdio.h>

int main() {
    int marks;
    int attendance;

    printf("Enter marks: ");
    scanf("%d", &marks);

    printf("Enter attendance percentage: ");
    scanf("%d", &attendance);

    if (marks >= 40 && attendance >= 75) {
        printf("Eligible\n");
    } else {
        printf("Not eligible\n");
    }

    return 0;
}
```

এখানে `&&` এর কারণে **দুটো condition-ই true** হতে হবে।

---

# 13. `if-else` + `||`

ধরো weekend হলো Saturday অথবা Sunday:

```c
int day = 6;

if (day == 6 || day == 7) {
    printf("Weekend\n");
} else {
    printf("Weekday\n");
}
```

---

# 🧪 Practice 1 — Even/Odd

একটি integer input নাও।

Output:

```text
Even
```

অথবা:

```text
Odd
```

---

# 🧪 Practice 2 — Positive/Negative

একটি number input নাও।

Positive হলে:

```text
Positive
```

Negative হলে:

```text
Negative
```

**Bonus:** `0` আলাদাভাবে handle করার চেষ্টা করো।

---

# 🧪 Practice 3 — Pass/Fail

Marks input নাও।

```text
marks >= 40 → Pass
marks < 40  → Fail
```

---

# 🔥 Mini Challenge — Largest of Two

দুটি integer input নাও।

Output:

```text
First number is greater
```

অথবা:

```text
Second number is greater
```

অথবা:

```text
Both numbers are equal
```

**Hint:** এখানে শুধু `if-else` দিয়ে cleanভাবে তিনটি possibility handle করা কঠিন। তুমি চাইলে nested `if` ব্যবহার করে চেষ্টা করতে পারো।

---

# 🧠 আজকের Cheat Sheet

### Basic syntax

```c
if (condition) {
    // true
} else {
    // false
}
```

### Example

```c
if (number % 2 == 0) {
    printf("Even\n");
} else {
    printf("Odd\n");
}
```

### মনে রাখো

```text
if
 ↓
condition TRUE

else
 ↓
condition FALSE
```

একটি `if-else` execution-এ সাধারণত **একটি branch** execute হবে।

---

## 🎯 আজকের Challenge

নিজে লিখে দেখো:

```text
Enter a number: 25

Positive
Odd
```

এখানে **দুটি আলাদা `if-else`** ব্যবহার করবে:

1. Positive/Negative
    
2. Even/Odd
    

এতে বুঝবে কখন একাধিক independent decision দরকার।

---

### পরের Lesson → **Lesson 12 — `else-if` 🔥**

সেখানে আমরা একাধিক possibility handle করব:

```text
90–100 → A+
80–89  → A
70–79  → B
60–69  → C
40–59  → D
< 40   → F
```

এটাই real-world decision making-এর খুব গুরুত্বপূর্ণ অংশ।

---


# 🚀 Lesson 12 — `else-if`

আজ আমরা শিখব কীভাবে **একাধিক condition** পরীক্ষা করতে হয়।

`if-else`-এ ছিল দুইটা possibility:

```text
if → true
else → false
```

কিন্তু বাস্তবে অনেক সময় ৩, ৪, ৫ বা তার বেশি possibility থাকে।

যেমন:

```text
90+  → A+
80+  → A
70+  → B
60+  → C
40+  → D
<40  → F
```

এখানে ব্যবহার করব **`else-if`**।

---

# 1. `else-if` কী?

Basic structure:

```c
if (condition1) {
    // condition1 true
}
else if (condition2) {
    // condition2 true
}
else if (condition3) {
    // condition3 true
}
else {
    // কোনো condition true নয়
}
```

Program উপর থেকে নিচে condition check করে।

---

# 2. প্রথম Example

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number > 0) {
        printf("Positive\n");
    }
    else if (number < 0) {
        printf("Negative\n");
    }
    else {
        printf("Zero\n");
    }

    return 0;
}
```

এখানে তিনটি possibility:

```text
number > 0  → Positive
number < 0  → Negative
number == 0 → Zero
```

---

# 3. Program কীভাবে সিদ্ধান্ত নেয়?

ধরো input:

```text
-5
```

Program প্রথমে check করবে:

```text
-5 > 0
```

False।

তারপর:

```text
-5 < 0
```

True।

তাই:

```text
Negative
```

এরপর আর নিচের condition check করার দরকার নেই।

---

# 4. `else-if` Chain

এটাকে একটি chain হিসেবে ভাবতে পারো:

```text
          condition 1?
          /         \
       true        false
        ↓            ↓
      কাজ       condition 2?
                   /    \
                true    false
                 ↓        ↓
                কাজ    condition 3?
```

---

# 5. Grade Calculator 🔥

এটি `else-if`-এর classic example।

```c
#include <stdio.h>

int main() {
    int marks;

    printf("Enter marks: ");
    scanf("%d", &marks);

    if (marks >= 90) {
        printf("Grade: A+\n");
    }
    else if (marks >= 80) {
        printf("Grade: A\n");
    }
    else if (marks >= 70) {
        printf("Grade: B\n");
    }
    else if (marks >= 60) {
        printf("Grade: C\n");
    }
    else if (marks >= 40) {
        printf("Grade: D\n");
    }
    else {
        printf("Grade: F\n");
    }

    return 0;
}
```

---

# 6. এখানে একটি গুরুত্বপূর্ণ বিষয় 🔥

তুমি হয়তো ভাবতে পারো:

```text
90 >= 90 → A+
90 >= 80 → A
90 >= 70 → B
...
```

তাহলে কি একাধিক grade print হবে?

**না।**

কারণ `else-if` chain-এ প্রথম true condition পাওয়ার পর সেই branch execute হয় এবং chain শেষ হয়ে যায়।

Input:

```text
90
```

Output:

```text
Grade: A+
```

শুধু এটিই।

---

# 7. Condition-এর Order খুব গুরুত্বপূর্ণ

এই code:

```c
if (marks >= 40) {
    printf("D\n");
}
else if (marks >= 60) {
    printf("C\n");
}
else if (marks >= 80) {
    printf("A\n");
}
```

এটি ভুলভাবে কাজ করবে।

ধরো marks:

```text
85
```

প্রথম condition:

```text
85 >= 40
```

True!

তাই সরাসরি:

```text
D
```

print হবে।

নিচের conditions আর check হবে না।

### সঠিক order:

```c
if (marks >= 80) {
    printf("A\n");
}
else if (marks >= 60) {
    printf("C\n");
}
else if (marks >= 40) {
    printf("D\n");
}
else {
    printf("F\n");
}
```

**বড় threshold আগে, ছোট threshold পরে।**

---

# 8. Number Range

ধরো temperature অনুযায়ী message:

```text
30+       → Hot
20–29     → Warm
10–19     → Cool
Below 10  → Cold
```

Code:

```c
#include <stdio.h>

int main() {
    int temperature;

    printf("Enter temperature: ");
    scanf("%d", &temperature);

    if (temperature >= 30) {
        printf("Hot\n");
    }
    else if (temperature >= 20) {
        printf("Warm\n");
    }
    else if (temperature >= 10) {
        printf("Cool\n");
    }
    else {
        printf("Cold\n");
    }

    return 0;
}
```

---

# 9. Positive / Negative / Zero

আরেকটি গুরুত্বপূর্ণ pattern:

```c
if (number > 0) {
    printf("Positive\n");
}
else if (number < 0) {
    printf("Negative\n");
}
else {
    printf("Zero\n");
}
```

এখানে `else` automatically বোঝাচ্ছে:

```text
number > 0 নয়
এবং
number < 0 নয়
```

তাহলে বাকি possibility:

```text
number == 0
```

---

# 10. `else-if` বনাম Multiple `if`

এটা খুব গুরুত্বপূর্ণ।

### Multiple `if`

```c
if (marks >= 40) {
    printf("Pass\n");
}

if (marks >= 60) {
    printf("Good\n");
}

if (marks >= 80) {
    printf("Excellent\n");
}
```

যদি marks = 85 হয়, তিনটিই print হতে পারে।

```text
Pass
Good
Excellent
```

---

### `else-if`

```c
if (marks >= 80) {
    printf("Excellent\n");
}
else if (marks >= 60) {
    printf("Good\n");
}
else if (marks >= 40) {
    printf("Pass\n");
}
else {
    printf("Fail\n");
}
```

marks = 85 হলে:

```text
Excellent
```

শুধু একটি branch।

---

# 11. কখন Multiple `if`?

যখন conditions **independent**।

যেমন:

```text
Number positive?
Number even?
Number greater than 100?
```

একটি number একই সঙ্গে তিনটিই হতে পারে।

তাই:

```c
if (number > 0) {
    printf("Positive\n");
}

if (number % 2 == 0) {
    printf("Even\n");
}

if (number > 100) {
    printf("Greater than 100\n");
}
```

---

# 12. কখন `else-if`?

যখন একটি value-এর **একটিমাত্র category** নির্বাচন করতে চাই।

যেমন:

```text
90+ → A+
80+ → A
70+ → B
60+ → C
```

এখানে `else-if` ভালো।

---

# 13. Calculator Example

Operator input নিয়ে calculation করা যায়।

```c
#include <stdio.h>

int main() {
    double a, b;
    char operator;

    printf("Enter expression (e.g. 10 + 5): ");
    scanf("%lf %c %lf", &a, &operator, &b);

    if (operator == '+') {
        printf("Result = %.2f\n", a + b);
    }
    else if (operator == '-') {
        printf("Result = %.2f\n", a - b);
    }
    else if (operator == '*') {
        printf("Result = %.2f\n", a * b);
    }
    else if (operator == '/') {
        if (b != 0) {
            printf("Result = %.2f\n", a / b);
        }
        else {
            printf("Cannot divide by zero.\n");
        }
    }
    else {
        printf("Invalid operator.\n");
    }

    return 0;
}
```

এখানে আমরা একসঙ্গে ব্যবহার করেছি:

- `if`
    
- `else-if`
    
- `else`
    
- nested `if`
    
- comparison
    
- arithmetic operators
    
- `char`
    
- `scanf()`
    

---

# 14. Nested `if` কী হলো?

উপরের calculator-এ:

```c
else if (operator == '/') {
    if (b != 0) {
        printf("%.2f\n", a / b);
    }
    else {
        printf("Cannot divide by zero.\n");
    }
}
```

একটি `if`-এর ভিতরে আরেকটি `if`।

এটিই **nested if**।

এটি আমাদের পরের lesson-এর মূল topic।

---

# 🧪 Practice 1 — Grade

এই grading system implement করো:

```text
90–100 → A+
80–89  → A
70–79  → B
60–69  → C
40–59  → D
0–39   → F
```

---

# 🧪 Practice 2 — Number Category

User একটি number দেবে।

Output:

```text
Positive
Negative
Zero
```

`else-if` ব্যবহার করবে।

---

# 🧪 Practice 3 — Age Category

User age দেবে:

```text
0–12    → Child
13–19   → Teenager
20–59   → Adult
60+     → Senior
```

এটি `else-if` দিয়ে implement করো।

---

# 🔥 Mini Challenge — Electricity Bill

ধরো:

```text
0–100 units    → 5 টাকা/unit
101–200        → 7 টাকা/unit
201+           → 10 টাকা/unit
```

User units input দেবে।

তারপর `else-if` ব্যবহার করে প্রতি unit-এর rate বের করো।

**Bonus:** পরে total bill হিসাব করার চেষ্টা করো।

---

# 🧠 আজকের Cheat Sheet

### Basic structure

```c
if (condition1) {
    // ...
}
else if (condition2) {
    // ...
}
else {
    // ...
}
```

### গুরুত্বপূর্ণ নিয়ম

```text
উপর থেকে নিচে condition check হয়
          ↓
প্রথম true condition execute হয়
          ↓
বাকি chain skip হয়
```

### Multiple `if`

```text
একাধিক independent condition
```

### `else-if`

```text
একাধিক mutually exclusive possibility
```

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ ধারণা

**Multiple `if` বনাম `else-if` ঠিকভাবে বুঝতে পারা খুব গুরুত্বপূর্ণ।**

```text
Independent conditions
       ↓
   multiple if


One category নির্বাচন
       ↓
    else-if
```

পরের Lesson → **Lesson 13 — Nested `if` 🔥**

সেখানে আমরা শিখব কীভাবে **একটি condition-এর ভিতরে আরেকটি condition** check করতে হয়।

---
# 🚀 Lesson 13 — Nested `if`

আজ আমরা শিখব **Nested `if`**।

Nested মানে হলো **একটির ভিতরে আরেকটি**।

তাই Nested `if` হলো:

> একটি `if` block-এর ভিতরে আরেকটি `if` statement।

---

# 1. Basic Structure

```c
if (condition1) {

    if (condition2) {
        // condition1 এবং condition2 দুটোই true হলে
    }

}
```

ভাবতে পারো:

```text
প্রথম দরজা
   ↓
Condition 1?
   ↓ Yes
দ্বিতীয় দরজা
   ↓
Condition 2?
   ↓ Yes
   কাজ
```

---

# 2. সহজ Example

ধরো, কোনো student-এর marks `40` বা তার বেশি হলে সে pass করেছে।

তারপর pass করা student-এর মধ্যে marks `80` বা তার বেশি হলে তাকে excellent বলা হবে।

```c
#include <stdio.h>

int main() {
    int marks;

    printf("Enter marks: ");
    scanf("%d", &marks);

    if (marks >= 40) {

        if (marks >= 80) {
            printf("Excellent\n");
        }
    }

    return 0;
}
```

Input:

```text
85
```

Output:

```text
Excellent
```

কারণ:

```text
85 >= 40  → true
85 >= 80  → true
```

---

# 3. Nested `if` কেন ব্যবহার করব?

যখন **একটি condition সত্য হওয়ার পরেই** আরেকটি condition পরীক্ষা করার দরকার হয়।

উদাহরণ:

```text
Student pass করেছে?
       ↓ Yes
Marks খুব ভালো?
       ↓ Yes
Excellent
```

---

# 4. Nested `if-else`

Nested `if`-এর ভিতরে `else`-ও থাকতে পারে।

```c
#include <stdio.h>

int main() {
    int age;

    printf("Enter age: ");
    scanf("%d", &age);

    if (age >= 18) {

        if (age >= 60) {
            printf("Senior adult\n");
        } else {
            printf("Adult\n");
        }

    } else {
        printf("Minor\n");
    }

    return 0;
}
```

এখানে প্রথম decision:

```text
age >= 18?
```

যদি `false`:

```text
Minor
```

যদি `true`, তখন দ্বিতীয় decision:

```text
age >= 60?
```

---

# 5. Flow বুঝে নাও

ধরো:

```text
age = 65
```

Program:

```text
age >= 18?
     ↓
    YES
     ↓
age >= 60?
     ↓
    YES
     ↓
Senior adult
```

আর:

```text
age = 30
```

হলে:

```text
age >= 18?
     ↓
    YES
     ↓
age >= 60?
     ↓
    NO
     ↓
Adult
```

আর:

```text
age = 15
```

হলে:

```text
age >= 18?
     ↓
     NO
     ↓
Minor
```

---

# 6. Nested `if` দিয়ে Login Logic

ধরো username এবং password দুটোই সঠিক হতে হবে।

```c
#include <stdio.h>

int main() {
    int usernameCorrect = 1;
    int passwordCorrect = 1;

    if (usernameCorrect) {

        if (passwordCorrect) {
            printf("Login successful\n");
        } else {
            printf("Incorrect password\n");
        }

    } else {
        printf("Incorrect username\n");
    }

    return 0;
}
```

এখানে:

```text
Username correct?
       ↓ Yes
Password correct?
       ↓ Yes
Login successful
```

---

# 7. Nested `if` বনাম `&&`

উপরের example-টা আমরা `&&` দিয়েও লিখতে পারি:

```c
if (usernameCorrect && passwordCorrect) {
    printf("Login successful\n");
}
```

তাহলে প্রশ্ন:

> কখন Nested `if` ব্যবহার করব?

যখন দ্বিতীয় decision-এর উপর **আলাদা action** দরকার হয়।

যেমন:

```c
if (usernameCorrect) {

    if (passwordCorrect) {
        printf("Login successful\n");
    } else {
        printf("Wrong password\n");
    }

} else {
    printf("Wrong username\n");
}
```

এখানে কোনটা ভুল হয়েছে সেটা আলাদাভাবে জানানো হচ্ছে।

---

# 8. Another Example — Exam Eligibility

ধরো:

- Marks ≥ 40 হলে pass
    
- Pass করার পরে attendance ≥ 75 হলে eligible
    

```c
#include <stdio.h>

int main() {
    int marks;
    int attendance;

    printf("Enter marks: ");
    scanf("%d", &marks);

    printf("Enter attendance: ");
    scanf("%d", &attendance);

    if (marks >= 40) {

        if (attendance >= 75) {
            printf("Eligible for final result\n");
        } else {
            printf("Attendance too low\n");
        }

    } else {
        printf("Failed the exam\n");
    }

    return 0;
}
```

---

# 9. Nested `if`-এর স্তর

Technically তুমি এমনও করতে পারো:

```c
if (condition1) {

    if (condition2) {

        if (condition3) {
            printf("All conditions are true\n");
        }

    }

}
```

কিন্তু অনেক বেশি nesting হলে code পড়া কঠিন হয়ে যায়।

তাই:

> **প্রয়োজন ছাড়া অনেক level-এর nested `if` ব্যবহার করো না।**

---

# 10. `else` কোন `if`-এর সঙ্গে যুক্ত?

এটি beginner-দের জন্য গুরুত্বপূর্ণ।

```c
if (condition1) {

    if (condition2) {
        printf("A\n");
    } else {
        printf("B\n");
    }

}
```

এখানে `else` **ভেতরের `if`-এর** সঙ্গে যুক্ত:

```text
if (condition2)
      ↓
    else
```

Indentation দেখে বিষয়টি পরিষ্কার হয়।

---

# 11. Braces `{}` ব্যবহার করো

এই ধরনের code avoid করো:

```c
if (condition1)
    if (condition2)
        printf("Hello");
    else
        printf("Bye");
```

এখানে visually confusion হতে পারে।

এর বদলে:

```c
if (condition1) {
    if (condition2) {
        printf("Hello");
    } else {
        printf("Bye");
    }
}
```

এটা অনেক পরিষ্কার।

---

# 12. Nested `if` দিয়ে তিনটি Number

ধরো তিনটি number-এর মধ্যে সবচেয়ে বড়টি বের করতে চাই।

একটি approach:

```c
#include <stdio.h>

int main() {
    int a, b, c;

    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);

    if (a > b) {

        if (a > c) {
            printf("%d is largest\n", a);
        } else {
            printf("%d is largest\n", c);
        }

    } else {

        if (b > c) {
            printf("%d is largest\n", b);
        } else {
            printf("%d is largest\n", c);
        }
    }

    return 0;
}
```

এখানে প্রথমে `a` বনাম `b` compare করা হচ্ছে।

তারপর winner-এর সঙ্গে `c` compare করা হচ্ছে।

---

# 13. Nested `if` + Even/Odd

আরেকটি ছোট example:

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number > 0) {

        if (number % 2 == 0) {
            printf("Positive even number\n");
        } else {
            printf("Positive odd number\n");
        }

    } else {
        printf("Number is not positive\n");
    }

    return 0;
}
```

এখানে:

```text
number positive?
       ↓ Yes
even?
 ↙       ↘
Yes       No
 ↓         ↓
Positive  Positive
Even      Odd
```

---

# 14. Nested `if` কখন ব্যবহার না করাই ভালো?

ধরো:

```c
if (age >= 18) {
    if (age <= 60) {
        printf("Adult range\n");
    }
}
```

এখানে সহজেই লেখা যায়:

```c
if (age >= 18 && age <= 60) {
    printf("Adult range\n");
}
```

দ্বিতীয়টি অনেক cleaner।

তাই:

> **Nested `if` এবং logical operators—দুটির মধ্যে পরিস্থিতি অনুযায়ী সহজ code বেছে নাও।**

---

# 🧪 Practice 1 — Positive Even/Odd

একটি number input নাও।

যদি positive হয়, তখন check করবে:

```text
Even → Positive Even
Odd  → Positive Odd
```

আর positive না হলে:

```text
Not Positive
```

---

# 🧪 Practice 2 — Student Eligibility

Input:

```text
Marks
Attendance
```

Rules:

```text
Marks >= 40
    ↓
Attendance >= 75
    ↓
Eligible
```

যদি marks কম হয়:

```text
Failed
```

যদি marks ঠিক থাকে কিন্তু attendance কম হয়:

```text
Attendance too low
```

---

# 🧪 Practice 3 — Largest of Three

তিনটি integer input নাও:

```text
10 25 15
```

Output:

```text
Largest = 25
```

**Nested `if` ব্যবহার করে চেষ্টা করো।**

---

# 🔥 Mini Challenge — Login System

একটি simple login checker বানাও।

Input:

```text
Enter username: ...
Enter password: ...
```

ধরো:

```text
correct username = 1234
correct password = 5678
```

Rules:

```text
Username ভুল
    ↓
Invalid username

Username ঠিক
    ↓
Password ভুল
    ↓
Invalid password

Username + password দুটোই ঠিক
    ↓
Login successful
```

**Nested `if` ব্যবহার করে implement করো।**

---

# 🧠 আজকের Cheat Sheet

### Nested `if`

```c
if (condition1) {

    if (condition2) {
        // কাজ
    }

}
```

### Nested `if-else`

```c
if (condition1) {

    if (condition2) {
        // A
    } else {
        // B
    }

} else {
    // C
}
```

### কখন ব্যবহার করবে?

```text
প্রথম condition
      ↓
সেটা true হলে
      ↓
দ্বিতীয় decision দরকার
      ↓
Nested if
```

### কিন্তু simple হলে:

```c
if (a && b) {
    ...
}
```

অনেক সময় nested `if`-এর চেয়ে cleaner।

---

## 🎯 আজকের Core Concept

এখন পর্যন্ত decision making-এর তিনটি level তুমি জানো:

```text
if
 ↓
একটি condition


if-else
 ↓
দুটি possibility


if-else-if
 ↓
অনেক possibility


nested if
 ↓
এক condition-এর ভিতরে আরেক decision
```

পরের Lesson → **Lesson 14 — `switch-case` 🔥**

সেখানে `if-else-if` ছাড়াও অনেকগুলো fixed option—যেমন menu, day, calculator operator—আরও সুন্দরভাবে handle করতে শিখব।

---
# 🚀 Lesson 14 — `switch-case`

আজ আমরা শিখব **`switch-case`**।

`switch-case` ব্যবহার করা হয় যখন একটি value-এর ভিত্তিতে **কয়েকটি নির্দিষ্ট option-এর মধ্যে একটি নির্বাচন** করতে হয়।

যেমন:

```text
1 → Monday
2 → Tuesday
3 → Wednesday
...
```

এ ধরনের problem-এ `switch` অনেক readable হতে পারে।

---

# 1. Basic Syntax

```c
switch (value) {
    case 1:
        // code
        break;

    case 2:
        // code
        break;

    case 3:
        // code
        break;

    default:
        // কোনো case match না করলে
}
```

এখানে:

```text
switch
  ↓
কোন value check করব?

case
  ↓
কোন value-এর জন্য কী কাজ হবে?

break
  ↓
switch থেকে বের হয়ে যাও

default
  ↓
কোনো case match না হলে
```

---

# 2. সবচেয়ে সহজ Example

```c
#include <stdio.h>

int main() {
    int day = 1;

    switch (day) {
        case 1:
            printf("Monday\n");
            break;

        case 2:
            printf("Tuesday\n");
            break;

        case 3:
            printf("Wednesday\n");
            break;

        default:
            printf("Invalid day\n");
    }

    return 0;
}
```

Output:

```text
Monday
```

কারণ:

```text
day = 1
```

তাই `case 1` execute হয়েছে।

---

# 3. `break` কেন?

`break` খুব গুরুত্বপূর্ণ।

ধরো:

```c
switch (day) {
    case 1:
        printf("Monday\n");

    case 2:
        printf("Tuesday\n");

    case 3:
        printf("Wednesday\n");
}
```

এখানে `break` নেই।

যদি `day = 1` হয়, তাহলে শুধু Monday নয়, পরের case-গুলোর code-ও execute হতে পারে।

Output হতে পারে:

```text
Monday
Tuesday
Wednesday
```

এটাকে **fall-through** বলা হয়।

সাধারণ beginner code-এ প্রতিটি case-এর শেষে:

```c
break;
```

দেওয়ার অভ্যাস করো।

---

# 4. `default`

যদি কোনো `case` match না করে:

```c
default:
    printf("Invalid choice\n");
```

execute হবে।

Example:

```c
#include <stdio.h>

int main() {
    int day;

    printf("Enter day number: ");
    scanf("%d", &day);

    switch (day) {
        case 1:
            printf("Monday\n");
            break;

        case 2:
            printf("Tuesday\n");
            break;

        case 3:
            printf("Wednesday\n");
            break;

        default:
            printf("Invalid day\n");
    }

    return 0;
}
```

Input:

```text
7
```

Output:

```text
Invalid day
```

---

# 5. `switch` দিয়ে Calculator

এটি খুব common use case।

```c
#include <stdio.h>

int main() {
    double a, b;
    char op;

    printf("Enter expression (e.g. 10 + 5): ");
    scanf("%lf %c %lf", &a, &op, &b);

    switch (op) {
        case '+':
            printf("Result = %.2f\n", a + b);
            break;

        case '-':
            printf("Result = %.2f\n", a - b);
            break;

        case '*':
            printf("Result = %.2f\n", a * b);
            break;

        case '/':
            if (b != 0) {
                printf("Result = %.2f\n", a / b);
            } else {
                printf("Cannot divide by zero.\n");
            }
            break;

        default:
            printf("Invalid operator\n");
    }

    return 0;
}
```

Input:

```text
10 * 5
```

Output:

```text
Result = 50.00
```

---

# 6. Multiple Case একই কাজ করতে পারে

ধরো:

```text
1 → Monday
2 → Tuesday
6 → Saturday
7 → Sunday
```

Weekend check করতে:

```c
switch (day) {
    case 6:
    case 7:
        printf("Weekend\n");
        break;

    default:
        printf("Weekday\n");
}
```

এখানে `case 6`-এর কোনো code নেই।

তাই execution `case 7`-এর code-এর দিকে এগিয়ে যায়।

এটি **intentional fall-through**।

এখানে সেটা আমরা ইচ্ছা করেই ব্যবহার করেছি।

---

# 7. `switch` কোন ধরনের value নিয়ে কাজ করে?

Beginner level-এ সাধারণত:

```text
int
char
```

এর মতো integral values নিয়ে `switch` ব্যবহার করবে।

উদাহরণ:

```c
char grade = 'A';

switch (grade) {
    case 'A':
        printf("Excellent\n");
        break;

    case 'B':
        printf("Good\n");
        break;

    default:
        printf("Other grade\n");
}
```

---

# 8. `switch` বনাম `if-else-if`

ধরো:

```text
1 → Add
2 → Subtract
3 → Multiply
4 → Divide
```

`switch` খুব natural:

```c
switch (choice) {
    case 1:
        printf("Add\n");
        break;

    case 2:
        printf("Subtract\n");
        break;

    case 3:
        printf("Multiply\n");
        break;

    case 4:
        printf("Divide\n");
        break;

    default:
        printf("Invalid choice\n");
}
```

কিন্তু range-based condition:

```text
marks >= 90
marks >= 80
marks >= 70
```

এর জন্য `if-else-if` বেশি উপযোগী।

---

# 9. খুব গুরুত্বপূর্ণ পার্থক্য

### `switch`

নির্দিষ্ট value match:

```c
case 1:
case 2:
case 3:
```

### `if`

Comparison/range:

```c
if (marks >= 90)
```

সহজভাবে:

```text
Fixed choices
    ↓
 switch

Ranges / complex conditions
    ↓
 if / else-if
```

---

# 10. Menu Program

এখন একটি বাস্তব menu বানাই।

```c
#include <stdio.h>

int main() {
    int choice;

    printf("=== MENU ===\n");
    printf("1. Start\n");
    printf("2. Settings\n");
    printf("3. Help\n");
    printf("4. Exit\n");

    printf("Enter your choice: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("Starting...\n");
            break;

        case 2:
            printf("Opening settings...\n");
            break;

        case 3:
            printf("Opening help...\n");
            break;

        case 4:
            printf("Goodbye!\n");
            break;

        default:
            printf("Invalid choice.\n");
    }

    return 0;
}
```

এ ধরনের menu আমরা পরে **Bank Management System**, **ATM**, **Student Management System** project-এ অনেক ব্যবহার করব।

---

# 11. `switch`-এর ভিতরে `if`

হ্যাঁ, করা যায়।

যেমন calculator:

```c
switch (op) {
    case '/':
        if (b != 0) {
            printf("%.2f\n", a / b);
        } else {
            printf("Cannot divide by zero.\n");
        }
        break;
}
```

অর্থাৎ `switch` এবং `if` একসঙ্গে ব্যবহার করা যায়।

---

# 12. Common Mistake — `break` ভুলে যাওয়া

ভুল:

```c
switch (choice) {
    case 1:
        printf("One\n");

    case 2:
        printf("Two\n");
        break;
}
```

`choice = 1` হলে `One` print করার পর `case 2`-তেও ঢুকে যাবে।

সাধারণভাবে লিখবে:

```c
switch (choice) {
    case 1:
        printf("One\n");
        break;

    case 2:
        printf("Two\n");
        break;
}
```

---

# 13. Common Mistake — `=` ব্যবহার

`switch`-এ:

```c
switch (choice) {
```

এখানে `choice` value হিসেবে দেওয়া হয়।

`case`-এ:

```c
case 1:
```

এখানে `:` ব্যবহার হয়।

এভাবে লিখবে না:

```c
case choice = 1:
```

---

# 14. `switch` দিয়ে Grade

যদি grade letter already জানা থাকে:

```c
#include <stdio.h>

int main() {
    char grade;

    printf("Enter grade: ");
    scanf(" %c", &grade);

    switch (grade) {
        case 'A':
            printf("Excellent\n");
            break;

        case 'B':
            printf("Very good\n");
            break;

        case 'C':
            printf("Good\n");
            break;

        case 'D':
            printf("Pass\n");
            break;

        case 'F':
            printf("Fail\n");
            break;

        default:
            printf("Invalid grade\n");
    }

    return 0;
}
```

লক্ষ্য করো:

```c
scanf(" %c", &grade);
```

`%c`-এর আগে space রাখা হয়েছে, যাতে input buffer-এর leftover whitespace নিয়ে সমস্যা কম হয়।

---

# 🧪 Practice 1 — Day Menu

User input:

```text
1
```

Output:

```text
Monday
```

এভাবে:

```text
1 → Monday
2 → Tuesday
3 → Wednesday
4 → Thursday
5 → Friday
6 → Saturday
7 → Sunday
```

`switch-case` দিয়ে বানাও।

---

# 🧪 Practice 2 — Simple Calculator

User দেবে:

```text
10 + 5
```

Supported:

```text
+
-
*
/
```

`switch` ব্যবহার করে result বের করো।

---

# 🧪 Practice 3 — Menu

Menu:

```text
1. Burger
2. Pizza
3. Sandwich
4. Exit
```

User choice অনুযায়ী message দেখাও।

---

# 🔥 Mini Challenge — ATM Menu

একটি simple ATM menu বানাও:

```text
=== ATM ===

1. Check Balance
2. Deposit
3. Withdraw
4. Exit
```

`switch-case` ব্যবহার করো।

এখন শুধু menu/action message দেখালেই হবে:

```text
1 → Your balance is ...
2 → Deposit selected
3 → Withdraw selected
4 → Goodbye
```

Actual banking logic আমরা **Practical Projects**-এ পরে করব।

---

# 🧠 আজকের Cheat Sheet

### Syntax

```c
switch (value) {
    case 1:
        // code
        break;

    case 2:
        // code
        break;

    default:
        // fallback
}
```

### `break`

```text
case শেষ
 ↓
switch থেকে বের হও
```

### `default`

```text
কোনো case match না করলে
```

### `switch` কখন?

```text
Fixed value
   ↓
switch
```

### `if-else` কখন?

```text
Range / comparison / complex condition
   ↓
if-else
```

---

## 🎯 Phase 2 Progress

এখন পর্যন্ত:

```text
10. ✅ if
11. ✅ if-else
12. ✅ else-if
13. ✅ Nested if
14. ✅ switch-case
15. ⏳ Ternary operator
```

পরের Lesson → **Lesson 15 — Ternary Operator `?:`**

এখানে শিখব কীভাবে ছোট `if-else` decision-কে **এক লাইনে** লেখা যায়।

---

# 🚀 Lesson 15 — Ternary Operator `?:`

আজ **Phase 2 — Decision Making**-এর শেষ lesson।

আমরা শিখব **Ternary Operator**:

```c
condition ? value_if_true : value_if_false;
```

এটি মূলত ছোট `if-else`-কে সংক্ষেপে লেখার একটি উপায়।

---

# 1. Ternary Operator কী?

ধরো:

```c
if (age >= 18) {
    printf("Adult\n");
} else {
    printf("Minor\n");
}
```

এটাকে ছোট করে লেখা যায়:

```c
age >= 18 ? printf("Adult\n") : printf("Minor\n");
```

এটাই ternary operator।

---

# 2. Syntax

```c
condition ? expression1 : expression2;
```

এখানে:

```text
condition
   ↓
সত্য?
 ↙   ↘
Yes   No
 ↓     ↓
expr1 expr2
```

উদাহরণ:

```c
int age = 20;

age >= 18 ? printf("Adult") : printf("Minor");
```

Output:

```text
Adult
```

---

# 3. তিনটি অংশ আছে

Ternary-এর নাম **ternary** কারণ এতে তিনটি অংশ থাকে:

```c
age >= 18 ? printf("Adult") : printf("Minor");
```

### Part 1

```c
age >= 18
```

Condition

### Part 2

```c
printf("Adult")
```

True হলে

### Part 3

```c
printf("Minor")
```

False হলে

---

# 4. Variable-এর সঙ্গে Ternary

Ternary শুধু `printf()`-এর জন্য নয়।

ধরো:

```c
int age = 20;

char *result = (age >= 18) ? "Adult" : "Minor";

printf("%s\n", result);
```

Output:

```text
Adult
```

এখানে condition অনুযায়ী `result`-এ value রাখা হচ্ছে।

---

# 5. Even / Odd

একটি classic example:

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    printf("%s\n", (number % 2 == 0) ? "Even" : "Odd");

    return 0;
}
```

Input:

```text
7
```

Output:

```text
Odd
```

Input:

```text
10
```

Output:

```text
Even
```

---

# 6. দুইটি Number-এর বড়টি

```c
#include <stdio.h>

int main() {
    int a, b, max;

    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);

    max = (a > b) ? a : b;

    printf("Maximum = %d\n", max);

    return 0;
}
```

যদি:

```text
10 25
```

তাহলে:

```text
Maximum = 25
```

এখানে:

```c
max = (a > b) ? a : b;
```

মানে:

```text
a > b সত্য?
   ↓
 Yes → max = a
 No  → max = b
```

---

# 7. Positive / Negative

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    printf("%s\n", (number >= 0) ? "Non-negative" : "Negative");

    return 0;
}
```

---

# 8. Pass / Fail

```c
#include <stdio.h>

int main() {
    int marks;

    printf("Enter marks: ");
    scanf("%d", &marks);

    printf("%s\n", (marks >= 40) ? "Pass" : "Fail");

    return 0;
}
```

এটি equivalent:

```c
if (marks >= 40) {
    printf("Pass");
} else {
    printf("Fail");
}
```

---

# 9. Ternary দিয়ে Calculation

```c
#include <stdio.h>

int main() {
    int a, b, max;

    scanf("%d %d", &a, &b);

    max = (a > b) ? a : b;

    printf("%d\n", max);

    return 0;
}
```

এখানে ternary একটি **value return করছে**:

```text
a > b
 ↓
true → a
false → b
```

তারপর সেই value `max`-এ রাখা হচ্ছে।

---

# 10. `if-else` বনাম Ternary

### `if-else`

```c
if (number % 2 == 0) {
    printf("Even\n");
} else {
    printf("Odd\n");
}
```

### Ternary

```c
printf("%s\n", (number % 2 == 0) ? "Even" : "Odd");
```

দুটোর কাজ একই।

---

# 11. কখন Ternary ব্যবহার করবে?

Ternary ভালো যখন decision **খুব ছোট এবং simple**।

উদাহরণ:

```c
max = (a > b) ? a : b;
```

এটি খুব readable।

কিন্তু এমন কিছু:

```c
if (marks >= 90) {
    ...
} else if (marks >= 80) {
    ...
} else if (marks >= 70) {
    ...
}
```

এটাকে ternary দিয়ে লিখলে:

```c
grade = marks >= 90 ? "A+" :
        marks >= 80 ? "A" :
        marks >= 70 ? "B" :
        marks >= 60 ? "C" :
        "F";
```

এটা technically সম্ভব, কিন্তু beginner code হিসেবে সহজে readable নয়।

তাই **অতিরিক্ত nested ternary এড়িয়ে চলো।**

---

# 12. Nested Ternary

একটির ভিতরে আরেকটি ternary লেখা যায়:

```c
int number = 10;

char *result = (number > 0)
               ? "Positive"
               : (number < 0)
                 ? "Negative"
                 : "Zero";
```

এটি কাজ করবে।

কিন্তু:

> Beginner হিসেবে এমন code প্রয়োজন ছাড়া ব্যবহার না করাই ভালো।

এর বদলে:

```c
if (number > 0) {
    printf("Positive");
} else if (number < 0) {
    printf("Negative");
} else {
    printf("Zero");
}
```

অনেক বেশি readable।

---

# 13. Parentheses ব্যবহার করো

এভাবে:

```c
max = (a > b) ? a : b;
```

এটি পরিষ্কার।

যদিও অনেক ক্ষেত্রে parentheses ছাড়া কাজ করতে পারে, beginner হিসেবে condition-কে parentheses-এর মধ্যে রাখার অভ্যাস ভালো।

---

# 14. Ternary দিয়ে Absolute Value

একটি number-এর absolute value বের করার সহজ উপায়:

```c
#include <stdio.h>

int main() {
    int number;
    int absolute;

    printf("Enter a number: ");
    scanf("%d", &number);

    absolute = (number < 0) ? -number : number;

    printf("Absolute value = %d\n", absolute);

    return 0;
}
```

Input:

```text
-25
```

Output:

```text
Absolute value = 25
```

---

# 15. Ternary-এর সবচেয়ে গুরুত্বপূর্ণ Pattern

এই pattern মনে রাখো:

```c
variable = (condition) ? value1 : value2;
```

উদাহরণ:

```c
int max = (a > b) ? a : b;
```

```c
int min = (a < b) ? a : b;
```

```c
int abs = (x < 0) ? -x : x;
```

---

# 🧪 Practice 1 — Even/Odd

Ternary ব্যবহার করে:

```text
10 → Even
7  → Odd
```

print করো।

---

# 🧪 Practice 2 — Maximum

দুটি number input নিয়ে ternary দিয়ে maximum বের করো।

Example:

```text
Input: 15 27
Output: Maximum = 27
```

---

# 🧪 Practice 3 — Pass/Fail

```text
marks >= 40 → Pass
marks < 40  → Fail
```

Ternary দিয়ে implement করো।

---

# 🔥 Mini Challenge — Maximum of Three

তিনটি number-এর maximum বের করার চেষ্টা করো **ternary operator** দিয়ে।

Hint:

```c
int maxAB = (a > b) ? a : b;
int maxABC = (maxAB > c) ? maxAB : c;
```

তারপর:

```c
printf("Maximum = %d\n", maxABC);
```

---

# 🧠 আজকের Cheat Sheet

### Syntax

```c
condition ? value1 : value2;
```

### Variable assignment

```c
result = (condition) ? value1 : value2;
```

### Example

```c
max = (a > b) ? a : b;
```

মানে:

```text
a > b?
 ↓
Yes → a
No  → b
```

---

# 🎉 Phase 2 Complete!

তুমি এখন Decision Making-এর মূল বিষয়গুলো জানো:

```text
10. ✅ if
11. ✅ if-else
12. ✅ else-if
13. ✅ Nested if
14. ✅ switch-case
15. ✅ Ternary operator
```

এখন C program **decision নিতে পারে**। 🔥

---

# 🚀 Next: Phase 3 — Loops

এবার আমরা এমন code লিখব যা একই কাজ **বারবার automatically** করতে পারে।

### Lesson 16 — `for` Loop

শিখব:

```c
for (initialization; condition; update) {
    // repeated code
}
```

এবং প্রথমবার এমন program লিখব:

```text
1
2
3
4
5
...
100
```

তারপর multiplication table, sum, counting এবং আরও অনেক problem।


# 🚀 Phase 3 — Loops

# Lesson 16 — `for` Loop

এখন আমরা C-এর **Loops** শুরু করছি। 🔥

এতদিন যদি 1 থেকে 5 print করতে চাইতে, লিখতে হতো:

```c
printf("1\n");
printf("2\n");
printf("3\n");
printf("4\n");
printf("5\n");
```

এটা বিরক্তিকর এবং inefficient।

`for` loop দিয়ে:

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

একই কাজ অনেক সহজে করা যায়।

---

# 1. Loop কী?

**Loop = একই ধরনের কাজ বারবার করা।**

যেমন:

```text
Print Hello 5 times
Print 1 to 100
Calculate 1 + 2 + ... + 100
Print multiplication table
```

---

# 2. `for` Loop-এর Syntax

```c
for (initialization; condition; update) {
    // repeated code
}
```

উদাহরণ:

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

এখানে তিনটি অংশ:

```text
initialization
      ↓
condition
      ↓
update
```

---

# 3. তিনটি অংশ বুঝে নাও

এই loop:

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

### ① Initialization

```c
int i = 1;
```

Loop শুরু হওয়ার আগে `i`-কে 1 করা হচ্ছে।

### ② Condition

```c
i <= 5
```

Condition true থাকা পর্যন্ত loop চলবে।

### ③ Update

```c
i++
```

প্রতিবার loop শেষ হওয়ার পর `i` এক করে বাড়বে।

---

# 4. Loop কীভাবে চলে?

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

এটি এমনভাবে চলে:

```text
i = 1
 ↓
1 <= 5 ? YES
 ↓
print 1
 ↓
i++
 ↓
i = 2
 ↓
2 <= 5 ? YES
 ↓
print 2
 ↓
...
 ↓
i = 5
 ↓
5 <= 5 ? YES
 ↓
print 5
 ↓
i = 6
 ↓
6 <= 5 ? NO
 ↓
Loop শেষ
```

Output:

```text
1
2
3
4
5
```

---

# 5. প্রথম Full Program

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 10; i++) {
        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 6. `i++` কী?

```c
i++;
```

মানে:

```c
i = i + 1;
```

অর্থাৎ:

```text
1 → 2 → 3 → 4 → 5
```

একইভাবে:

```c
i--;
```

মানে:

```c
i = i - 1;
```

---

# 7. 10 থেকে 1 পর্যন্ত

শুধু update পরিবর্তন করলেই হবে:

```c
#include <stdio.h>

int main() {

    for (int i = 10; i >= 1; i--) {
        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

---

# 8. শুধু Even Numbers

1 থেকে 20 পর্যন্ত even numbers:

```c
#include <stdio.h>

int main() {

    for (int i = 2; i <= 20; i += 2) {
        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

এখানে:

```c
i += 2;
```

মানে:

```c
i = i + 2;
```

---

# 9. শুধু Odd Numbers

```c
for (int i = 1; i <= 20; i += 2) {
    printf("%d\n", i);
}
```

Output:

```text
1
3
5
7
9
11
13
15
17
19
```

---

# 10. `for` Loop দিয়ে 1 থেকে N

User একটি `N` দেবে।

```c
#include <stdio.h>

int main() {
    int n;

    printf("Enter N: ");
    scanf("%d", &n);

    for (int i = 1; i <= n; i++) {
        printf("%d\n", i);
    }

    return 0;
}
```

Input:

```text
5
```

Output:

```text
1
2
3
4
5
```

---

# 11. 1 থেকে N পর্যন্ত Sum 🔥

এটি খুব গুরুত্বপূর্ণ loop problem।

ধরো:

```text
1 + 2 + 3 + 4 + 5
```

Result:

```text
15
```

Code:

```c
#include <stdio.h>

int main() {
    int n;
    int sum = 0;

    printf("Enter N: ");
    scanf("%d", &n);

    for (int i = 1; i <= n; i++) {
        sum = sum + i;
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Input:

```text
5
```

Loop-এর ভিতরে:

```text
sum = 0

i = 1 → sum = 1
i = 2 → sum = 3
i = 3 → sum = 6
i = 4 → sum = 10
i = 5 → sum = 15
```

Output:

```text
Sum = 15
```

---

# 12. Multiplication Table

User একটি number দেবে:

```text
5
```

আমরা চাই:

```text
5 x 1 = 5
5 x 2 = 10
...
5 x 10 = 50
```

Code:

```c
#include <stdio.h>

int main() {
    int n;

    printf("Enter a number: ");
    scanf("%d", &n);

    for (int i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", n, i, n * i);
    }

    return 0;
}
```

Input:

```text
5
```

Output:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

---

# 13. `for` Loop-এর Scope

এই:

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

এখানে `i` সাধারণত loop-এর scope-এর মধ্যে থাকে।

তাই loop-এর বাইরে:

```c
printf("%d", i);
```

লিখলে সমস্যা হবে।

আরেকভাবে লিখতে পারো:

```c
int i;

for (i = 1; i <= 5; i++) {
    printf("%d\n", i);
}

printf("%d\n", i);
```

এক্ষেত্রে `i` loop-এর বাইরেও scope-এ আছে।

---

# 14. Infinite Loop ⚠️

এই code:

```c
for (;;) {
    printf("Hello\n");
}
```

এর কোনো condition নেই।

তাই এটি theoretically চলতেই থাকবে।

```text
Hello
Hello
Hello
Hello
...
```

Beginner হিসেবে ভুল করে এমন loop বানিয়ে ফেললে program বন্ধ করতে হতে পারে।

---

# 15. Condition বাদ দেওয়া

`for`-এর তিনটি অংশ technically optional।

যেমন:

```c
int i = 1;

for (; i <= 5; i++) {
    printf("%d\n", i);
}
```

এটাও valid।

কিন্তু beginner হিসেবে প্রথমে standard form ব্যবহার করো:

```c
for (int i = 1; i <= 5; i++)
```

---

# 16. `i += 5`

শুধু 1 করে বাড়াতে হবে এমন নয়।

```c
for (int i = 0; i <= 20; i += 5) {
    printf("%d\n", i);
}
```

Output:

```text
0
5
10
15
20
```

---

# 17. Reverse Counting

```c
for (int i = 20; i >= 0; i -= 2) {
    printf("%d\n", i);
}
```

Output:

```text
20
18
16
14
12
10
8
6
4
2
0
```

---

# 18. `for` Loop দিয়ে Factorial

`5!`:

```text
5 × 4 × 3 × 2 × 1 = 120
```

Code:

```c
#include <stdio.h>

int main() {
    int n;
    int factorial = 1;

    printf("Enter a number: ");
    scanf("%d", &n);

    for (int i = 1; i <= n; i++) {
        factorial = factorial * i;
    }

    printf("Factorial = %d\n", factorial);

    return 0;
}
```

Input:

```text
5
```

Output:

```text
Factorial = 120
```

---

# 19. `for` Loop + `if`

Loop-এর ভিতরে decision নেওয়া যায়।

উদাহরণ: 1 থেকে 20-এর মধ্যে শুধু divisible by 3 numbers:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 20; i++) {

        if (i % 3 == 0) {
            printf("%d\n", i);
        }

    }

    return 0;
}
```

Output:

```text
3
6
9
12
15
18
```

এখানে:

```text
for
 ↓
প্রতিটি number
 ↓
if
 ↓
3 দিয়ে divisible?
 ↓
Yes → print
```

---

# 🧪 Practice 1

`for` loop দিয়ে:

```text
1
2
3
...
100
```

print করো।

---

# 🧪 Practice 2

1 থেকে 100-এর মধ্যে সব **even numbers** print করো।

Expected:

```text
2
4
6
...
100
```

---

# 🧪 Practice 3

User একটি `N` input দেবে।

1 থেকে `N` পর্যন্ত সব সংখ্যার sum বের করো।

Example:

```text
Input: 10
Output: Sum = 55
```

---

# 🧪 Practice 4

User একটি number input দেবে এবং তার multiplication table `1` থেকে `10` পর্যন্ত print করবে।

---

# 🔥 Mini Challenge — Count Divisible Numbers

User দুটি number দেবে:

```text
start
end
```

তারপর `start` থেকে `end` পর্যন্ত কতগুলো number **5 দিয়ে divisible**, সেটা count করো।

Example:

```text
Start: 1
End: 20

Count = 4
```

কারণ:

```text
5, 10, 15, 20
```

---

# 🧠 আজকের Cheat Sheet

### Basic

```c
for (initialization; condition; update) {
    // repeated code
}
```

### Counting up

```c
for (int i = 1; i <= 10; i++)
```

### Counting down

```c
for (int i = 10; i >= 1; i--)
```

### Step by 2

```c
for (int i = 2; i <= 20; i += 2)
```

### Sum

```c
int sum = 0;

for (int i = 1; i <= n; i++) {
    sum = sum + i;
}
```

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়

এই pattern-টা মুখস্থ না করে **বোঝো**:

```c
for (int i = 1; i <= n; i++) {
    printf("%d\n", i);
}
```

এর অর্থ:

```text
শুরু → i = 1
       ↓
check → i <= n ?
       ↓
কাজ
       ↓
i বাড়াও
       ↓
আবার check
       ↓
...
```

তুমি এখন C-তে **repetition** করতে পারো। 🔥

### Phase 3 Progress

```text
16. ✅ for
17. ⏳ while
18. ⏳ do-while
19. ⏳ break
20. ⏳ continue
21. ⏳ Nested loops
22. ⏳ Pattern problems
```

পরের Lesson → **Lesson 17 — `while` Loop**।

----

# 🚀 Lesson 17 — `while` Loop

আজ আমরা C-এর দ্বিতীয় loop শিখব: **`while` loop**।

`for` loop-এর মতোই `while` বারবার code execute করে। তবে `while` সাধারণত তখন খুব useful, যখন **কতবার loop চলবে সেটা আগে থেকেই পরিষ্কার নয়**, কিন্তু একটি condition যতক্ষণ সত্য থাকবে ততক্ষণ কাজ করতে হবে।

---

# 1. Basic Syntax

```c
while (condition) {
    // repeated code
}
```

সহজভাবে:

```text
condition সত্য?
   ↓
 Yes
   ↓
code execute
   ↓
আবার condition check
   ↓
...
   ↓
False → loop শেষ
```

---

# 2. সবচেয়ে সহজ Example

```c
#include <stdio.h>

int main() {
    int i = 1;

    while (i <= 5) {
        printf("%d\n", i);
        i++;
    }

    return 0;
}
```

Output:

```text
1
2
3
4
5
```

---

# 3. `while` কীভাবে কাজ করে?

এই code:

```c
int i = 1;

while (i <= 5) {
    printf("%d\n", i);
    i++;
}
```

এভাবে চলে:

```text
i = 1
 ↓
1 <= 5 → YES
 ↓
print 1
 ↓
i = 2
 ↓
2 <= 5 → YES
 ↓
print 2
 ↓
...
 ↓
i = 5
 ↓
5 <= 5 → YES
 ↓
print 5
 ↓
i = 6
 ↓
6 <= 5 → NO
 ↓
Loop শেষ
```

---

# 4. `for` বনাম `while`

একই কাজ `for` দিয়ে:

```c
for (int i = 1; i <= 5; i++) {
    printf("%d\n", i);
}
```

`while` দিয়ে:

```c
int i = 1;

while (i <= 5) {
    printf("%d\n", i);
    i++;
}
```

দুটোতেই output:

```text
1
2
3
4
5
```

### মূল পার্থক্য

`for`:

```text
Initialization
Condition
Update
```

সব এক লাইনে থাকে।

`while`:

```text
Initialization → আগে
Condition       → while-এর মধ্যে
Update          → loop-এর ভিতরে
```

---

# 5. `while`-এ Update ভুলে গেলে ⚠️

এই code:

```c
int i = 1;

while (i <= 5) {
    printf("%d\n", i);
}
```

সমস্যা হলো `i` কখনো বাড়ছে না।

তাই:

```text
i = 1
1 <= 5 → true
print 1
1 <= 5 → true
print 1
1 <= 5 → true
...
```

এটি **infinite loop** হয়ে যাবে।

সঠিক:

```c
while (i <= 5) {
    printf("%d\n", i);
    i++;
}
```

---

# 6. User Input দিয়ে `while`

User যতক্ষণ positive number দিচ্ছে, ততক্ষণ input নেওয়া যায়।

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter a positive number: ");
    scanf("%d", &number);

    while (number > 0) {
        printf("You entered %d\n", number);

        printf("Enter another number: ");
        scanf("%d", &number);
    }

    printf("Loop ended.\n");

    return 0;
}
```

যদি input হয়:

```text
5
8
3
-1
```

তাহলে প্রথম তিনটি value-এর জন্য loop চলবে।

`-1` দিলে:

```text
number > 0
```

false হয়ে যাবে।

---

# 7. Sentinel Value

একটি বিশেষ value দিয়ে loop বন্ধ করার technique-কে **sentinel-controlled loop** বলা হয়।

যেমন:

```text
-1 → Stop
```

Example:

```c
#include <stdio.h>

int main() {
    int number;

    printf("Enter numbers (-1 to stop): ");
    scanf("%d", &number);

    while (number != -1) {
        printf("Number = %d\n", number);

        printf("Enter another number: ");
        scanf("%d", &number);
    }

    printf("Stopped.\n");

    return 0;
}
```

এখানে `-1` কোনো normal data হিসেবে process না করে loop বন্ধ করার signal হিসেবে ব্যবহৃত হচ্ছে।

---

# 8. `while` দিয়ে 1 থেকে 10

```c
#include <stdio.h>

int main() {
    int i = 1;

    while (i <= 10) {
        printf("%d\n", i);
        i++;
    }

    return 0;
}
```

---

# 9. `while` দিয়ে Reverse Counting

```c
#include <stdio.h>

int main() {
    int i = 10;

    while (i >= 1) {
        printf("%d\n", i);
        i--;
    }

    return 0;
}
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

---

# 10. Even Numbers

```c
#include <stdio.h>

int main() {
    int i = 2;

    while (i <= 20) {
        printf("%d\n", i);
        i += 2;
    }

    return 0;
}
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

---

# 11. `while` দিয়ে Sum

1 থেকে `N` পর্যন্ত sum:

```c
#include <stdio.h>

int main() {
    int n;
    int i = 1;
    int sum = 0;

    printf("Enter N: ");
    scanf("%d", &n);

    while (i <= n) {
        sum += i;
        i++;
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Input:

```text
5
```

Output:

```text
Sum = 15
```

---

# 12. `while` দিয়ে Multiplication Table

```c
#include <stdio.h>

int main() {
    int n;
    int i = 1;

    printf("Enter a number: ");
    scanf("%d", &n);

    while (i <= 10) {
        printf("%d x %d = %d\n", n, i, n * i);
        i++;
    }

    return 0;
}
```

---

# 13. `while` + `if`

Loop-এর ভিতরে decision নেওয়া যায়।

```c
#include <stdio.h>

int main() {
    int i = 1;

    while (i <= 20) {

        if (i % 2 == 0) {
            printf("%d\n", i);
        }

        i++;
    }

    return 0;
}
```

এখানে 1 থেকে 20 পর্যন্ত ঘুরে শুধু even numbers print হবে।

---

# 14. Number-এর Digit Count

এটি `while` loop-এর খুব গুরুত্বপূর্ণ application।

ধরো:

```text
number = 5832
```

এখানে 4টি digit।

Code:

```c
#include <stdio.h>

int main() {
    int number;
    int count = 0;

    printf("Enter a number: ");
    scanf("%d", &number);

    while (number != 0) {
        number = number / 10;
        count++;
    }

    printf("Digits = %d\n", count);

    return 0;
}
```

কীভাবে?

```text
5832 / 10 → 583
583 / 10  → 58
58 / 10   → 5
5 / 10    → 0
```

প্রতিবার এক digit কমে যাচ্ছে।

তাই:

```text
count = 4
```

> এখানে আপাতত positive integer দিয়ে practice করো। Negative numbers-এর handling পরে আলাদা করে শিখব।

---

# 15. Digit Sum 🔥

ধরো:

```text
1234
```

আমরা চাই:

```text
1 + 2 + 3 + 4 = 10
```

এর জন্য `% 10` দিয়ে শেষ digit বের করা যায়।

```c
#include <stdio.h>

int main() {
    int number;
    int sum = 0;

    printf("Enter a number: ");
    scanf("%d", &number);

    while (number != 0) {
        int digit = number % 10;
        sum += digit;
        number /= 10;
    }

    printf("Digit sum = %d\n", sum);

    return 0;
}
```

Input:

```text
1234
```

ধাপে ধাপে:

```text
1234 % 10 → 4
123  % 10 → 3
12   % 10 → 2
1    % 10 → 1
```

তাই:

```text
4 + 3 + 2 + 1 = 10
```

Output:

```text
Digit sum = 10
```

---

# 16. Reverse Number

`while` loop-এর সবচেয়ে famous beginner problem-গুলোর একটি।

Input:

```text
1234
```

Output:

```text
4321
```

Code:

```c
#include <stdio.h>

int main() {
    int number;
    int reverse = 0;

    printf("Enter a number: ");
    scanf("%d", &number);

    while (number != 0) {
        int digit = number % 10;

        reverse = reverse * 10 + digit;

        number /= 10;
    }

    printf("Reverse = %d\n", reverse);

    return 0;
}
```

মূল logic:

```text
শেষ digit বের করো
      ↓
reverse-এর শেষে যোগ করো
      ↓
original number থেকে শেষ digit বাদ দাও
      ↓
আবার করো
```

---

# 17. `while` কখন বেশি useful?

`for` ভালো যখন iteration count জানা থাকে:

```text
1 থেকে 100
10 বার
20 বার
```

`while` ভালো যখন condition-based repetition দরকার:

```text
যতক্ষণ input valid
যতক্ষণ user stop না করে
যতক্ষণ number > 0
যতক্ষণ game চলছে
```

তবে এগুলো কঠোর নিয়ম নয়—দুই loop দিয়েই অনেক একই কাজ করা যায়।

---

# 18. `while (1)`

এভাবে লিখলে:

```c
while (1) {
    printf("Hello\n");
}
```

এটি infinite loop।

পরে `break` শিখলে এমন loop-এর ভিতর থেকে বের হতে পারব।

উদাহরণ হিসেবে menu program-এ এটি useful হতে পারে:

```text
Menu
 ↓
User choice
 ↓
কাজ
 ↓
আবার Menu
 ↓
Exit?
```

এটি আমরা পরে আরও ভালোভাবে ব্যবহার করব।

---

# 🧪 Practice 1

`while` ব্যবহার করে:

```text
1
2
3
...
50
```

print করো।

---

# 🧪 Practice 2

1 থেকে 100 পর্যন্ত সব odd numbers print করো।

---

# 🧪 Practice 3

User একটি positive integer দেবে।

তার **digit count** বের করো।

Example:

```text
Input: 98765
Output: Digits = 5
```

---

# 🧪 Practice 4

User একটি number দেবে।

তার digit sum বের করো।

Example:

```text
Input: 583
Output: Digit sum = 16
```

কারণ:

```text
5 + 8 + 3 = 16
```

---

# 🔥 Mini Challenge — Reverse + Palindrome

প্রথমে number reverse করো।

তারপর original number এবং reverse number compare করো।

Example:

```text
Input: 121
Reverse: 121
Result: Palindrome
```

আর:

```text
Input: 123
Reverse: 321
Result: Not Palindrome
```

Hint:

```c
while (number != 0) {
    int digit = number % 10;
    reverse = reverse * 10 + digit;
    number /= 10;
}
```

**Important:** reverse করার আগে original number-টি অন্য variable-এ রেখে দাও, কারণ loop-এর মধ্যে `number` পরিবর্তন হয়ে যায়।

---

# 🧠 আজকের Cheat Sheet

### Basic

```c
while (condition) {
    // code
}
```

### Counter

```c
int i = 1;

while (i <= 10) {
    printf("%d\n", i);
    i++;
}
```

### Reverse

```c
i--;
```

### Step

```c
i += 2;
```

### Digit extraction

```c
digit = number % 10;
```

### Last digit বাদ দেওয়া

```c
number /= 10;
```

---

## 🎯 `for` vs `while`

|Situation|ভালো choice|
|---|---|
|কতবার চলবে জানা আছে|`for`|
|Condition-based repetition|`while`|
|Counting|`for` সাধারণত সহজ|
|User input-এর উপর নির্ভরশীল|`while` অনেক সময় সুবিধাজনক|
|Digit processing|`while` খুব common|

---

# 📚 Phase 3 Progress

```text
16. ✅ for
17. ✅ while
18. ⏳ do-while
19. ⏳ break
20. ⏳ continue
21. ⏳ Nested loops
22. ⏳ Pattern problems
```

পরের Lesson → **Lesson 18 — `do-while` Loop**

সেখানে দেখব `while` আর `do-while`-এর সবচেয়ে গুরুত্বপূর্ণ পার্থক্য: **`do-while` loop-এর body অন্তত একবার execute হয়।**

----

# 🚀 Lesson 18 — `do-while` Loop

আজ আমরা Phase 3-এর তৃতীয় loop শিখব:

```c
do {
    // code
} while (condition);
```

`do-while` হলো এমন একটি loop যেখানে **condition check করার আগে code অন্তত একবার execute হয়।**

---

# 1. Basic Syntax

```c
do {
    // code
} while (condition);
```

⚠️ লক্ষ্য করো, `while`-এর শেষে **semicolon `;`** আছে।

```c
} while (condition);
```

---

# 2. `while` বনাম `do-while`

### `while`

```c
while (condition) {
    printf("Hello\n");
}
```

এখানে আগে condition check হবে।

```text
condition?
 ↓
false → কিছুই হবে না
```

### `do-while`

```c
do {
    printf("Hello\n");
} while (condition);
```

এখানে আগে code execute হবে।

```text
code execute
 ↓
condition?
 ↓
true → আবার
false → stop
```

---

# 3. সবচেয়ে গুরুত্বপূর্ণ Example

```c
#include <stdio.h>

int main() {
    int i = 10;

    do {
        printf("%d\n", i);
        i++;
    } while (i <= 5);

    return 0;
}
```

এখানে:

```text
i = 10
```

এবং:

```text
i <= 5
```

false।

তবুও output হবে:

```text
10
```

কারণ `do-while` আগে body execute করেছে, তারপর condition check করেছে।

---

# 4. `while` করলে কী হতো?

```c
int i = 10;

while (i <= 5) {
    printf("%d\n", i);
    i++;
}
```

এখানে output:

```text
কিছুই নেই
```

কারণ প্রথমেই:

```text
10 <= 5 → false
```

তাই body একবারও execute হয়নি।

---

# 5. Execution Flow

এই code:

```c
int i = 1;

do {
    printf("%d\n", i);
    i++;
} while (i <= 5);
```

চলবে:

```text
i = 1
 ↓
print 1
 ↓
i = 2
 ↓
2 <= 5?
 ↓ YES
print 2
 ↓
...
 ↓
print 5
 ↓
i = 6
 ↓
6 <= 5?
 ↓ NO
STOP
```

Output:

```text
1
2
3
4
5
```

---

# 6. Basic Counting

```c
#include <stdio.h>

int main() {
    int i = 1;

    do {
        printf("%d\n", i);
        i++;
    } while (i <= 10);

    return 0;
}
```

Output:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 7. `do-while` দিয়ে User Input

এখানেই `do-while` খুব useful।

ধরো, user-কে একটি positive number দিতে হবে।

```c
#include <stdio.h>

int main() {
    int number;

    do {
        printf("Enter a positive number: ");
        scanf("%d", &number);
    } while (number <= 0);

    printf("You entered: %d\n", number);

    return 0;
}
```

এখানে user অন্তত একবার prompt পাবে।

যদি input:

```text
-5
```

তাহলে:

```text
number <= 0 → true
```

তাই আবার input চাইবে।

যদি:

```text
10
```

দেয়:

```text
number <= 0 → false
```

loop শেষ।

---

# 8. Validation-এর জন্য খুব Useful

ধরো marks `0` থেকে `100`-এর মধ্যে হতে হবে।

```c
#include <stdio.h>

int main() {
    int marks;

    do {
        printf("Enter marks (0-100): ");
        scanf("%d", &marks);
    } while (marks < 0 || marks > 100);

    printf("Valid marks = %d\n", marks);

    return 0;
}
```

Input:

```text
150
```

আবার input চাইবে।

Input:

```text
75
```

তাহলে:

```text
Valid marks = 75
```

---

# 9. Menu Program

`do-while` menu program-এর জন্য অত্যন্ত useful।

ধরো:

```text
=== MENU ===
1. Hello
2. About
3. Exit
```

আমরা চাই user যতক্ষণ Exit না করে, menu আবার দেখাবে।

```c
#include <stdio.h>

int main() {
    int choice;

    do {
        printf("\n=== MENU ===\n");
        printf("1. Hello\n");
        printf("2. About\n");
        printf("3. Exit\n");

        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Hello!\n");
                break;

            case 2:
                printf("This is a C program.\n");
                break;

            case 3:
                printf("Goodbye!\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 3);

    return 0;
}
```

এখানে flow:

```text
Menu
 ↓
Choice
 ↓
Action
 ↓
Choice == 3?
 ↙       ↘
NO       YES
 ↓        ↓
Menu     Exit
```

এই pattern পরে **ATM**, **Bank Management System**, **Student Management System**-এ অনেক ব্যবহার করবে।

---

# 10. `do-while` + `switch`

এটি খুব common combination:

```c
do {
    // show menu

    scanf("%d", &choice);

    switch (choice) {
        case 1:
            // option 1
            break;

        case 2:
            // option 2
            break;

        case 3:
            // exit
            break;
    }

} while (choice != 3);
```

এটা ভালোভাবে বুঝে রাখো।

---

# 11. `while` দিয়ে একই Menu

`while` দিয়েও করা যায়:

```c
int choice = 0;

while (choice != 3) {

    printf("1. Hello\n");
    printf("2. About\n");
    printf("3. Exit\n");

    scanf("%d", &choice);

    // actions
}
```

কিন্তু `do-while` এখানে natural কারণ menu **অন্তত একবার দেখাতেই হবে**।

---

# 12. Password Validation

একটি simple example:

```c
#include <stdio.h>

int main() {
    int password;

    do {
        printf("Enter password: ");
        scanf("%d", &password);
    } while (password != 1234);

    printf("Access granted!\n");

    return 0;
}
```

যতক্ষণ password `1234` নয়, input চাইবে।

⚠️ এটি শুধু C শেখার example; বাস্তব application-এ password এভাবে hard-code/store করা নিরাপদ নয়।

---

# 13. Number Guessing Style

ধরো secret number:

```c
int secret = 7;
int guess;
```

User যতক্ষণ সঠিক না দেয়:

```c
#include <stdio.h>

int main() {
    int secret = 7;
    int guess;

    do {
        printf("Guess the number: ");
        scanf("%d", &guess);

        if (guess < secret) {
            printf("Too low!\n");
        } else if (guess > secret) {
            printf("Too high!\n");
        }

    } while (guess != secret);

    printf("Correct!\n");

    return 0;
}
```

Input:

```text
3
```

Output:

```text
Too low!
```

তারপর আবার input।

---

# 14. `do-while`-এর গুরুত্বপূর্ণ Rule

এই semicolon ভুলবে না:

✅ Correct:

```c
do {
    printf("Hello");
} while (condition);
```

❌ Wrong:

```c
do {
    printf("Hello");
} while (condition)
```

C syntax অনুযায়ী `do-while` statement-এর শেষে `;` লাগে।

---

# 15. Infinite `do-while`

এভাবে:

```c
do {
    printf("Hello\n");
} while (1);
```

এটি infinite loop।

কারণ:

```text
1 = true
```

তাই condition সবসময় true।

পরে `break` শিখলে এই ধরনের loop control করতে পারবে।

---

# 16. `do-while` কোথায় ব্যবহার করবে?

বিশেষ করে:

### Input validation

```text
Input নাও
 ↓
Valid?
 ↓ No → আবার input
```

### Menu

```text
Menu দেখাও
 ↓
Choice নাও
 ↓
কাজ করো
 ↓
Exit?
 ↓ No → Menu
```

### Game

```text
Game চালাও
 ↓
Game শেষ?
 ↓ No → আবার চালাও
```

### User interaction

যেখানে প্রথমে অন্তত একবার action করানো দরকার।

---

# 🧪 Practice 1 — Positive Number

`do-while` ব্যবহার করে user-এর কাছ থেকে positive number নাও।

যতক্ষণ input:

```text
<= 0
```

ততক্ষণ আবার input চাইবে।

---

# 🧪 Practice 2 — Marks Validation

Marks:

```text
0 থেকে 100
```

এর বাইরে হলে আবার input চাইবে।

Example:

```text
Enter marks: 150
Enter marks: -10
Enter marks: 85
```

শেষে:

```text
Valid marks = 85
```

---

# 🧪 Practice 3 — Menu

এই menu বানাও:

```text
=== MENU ===
1. Add
2. Subtract
3. Multiply
4. Exit
```

`do-while + switch` ব্যবহার করো।

Exit না করা পর্যন্ত menu আবার দেখাবে।

---

# 🔥 Mini Challenge — ATM Menu

আজকের lesson-এর সবচেয়ে ভালো practice:

```text
=== ATM ===

1. Check Balance
2. Deposit
3. Withdraw
4. Exit
```

`do-while + switch` ব্যবহার করো।

ধরো শুরুতে:

```c
int balance = 1000;
```

Rules:

```text
1 → Balance দেখাবে
2 → Deposit amount নেবে
3 → Withdraw amount নেবে
4 → Exit
```

এখন শুধু basic logic implement করো।

---

# 🧠 `while` বনাম `do-while`

|`while`|`do-while`|
|---|---|
|আগে condition check|আগে body execute|
|0 বারও চলতে পারে|অন্তত 1 বার চলে|
|`while (condition)`|`do { } while (condition);`|
|Condition-first|Action-first|
|General loops|Validation/menu-তে খুব useful|

সবচেয়ে গুরুত্বপূর্ণ পার্থক্য:

```text
while:
condition → code

do-while:
code → condition
```

---

# 🎯 Phase 3 Progress

```text
16. ✅ for
17. ✅ while
18. ✅ do-while
19. ⏳ break
20. ⏳ continue
21. ⏳ Nested loops
22. ⏳ Pattern problems
```

## পরের Lesson → Lesson 19 — `break`

সেখানে শিখব কীভাবে loop **মাঝপথে সম্পূর্ণ বন্ধ** করা যায় এবং `for`, `while`, `do-while`-এর ভিতরে `break` কীভাবে কাজ করে।

---

# 🚀 Lesson 19 — `break`

আজ আমরা শিখব **`break` statement**।

`break` ব্যবহার করে কোনো loop বা `switch`-এর execution **সঙ্গে সঙ্গে বন্ধ** করে বের হয়ে আসা যায়।

---

# 1. `break` কী?

সহজভাবে:

```c
break;
```

মানে:

> **এখানেই থামো এবং loop/switch থেকে বের হয়ে যাও।**

উদাহরণ:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 10; i++) {

        if (i == 5) {
            break;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
```

`i == 5` হলে:

```c
break;
```

execute হয়েছে এবং loop শেষ হয়ে গেছে।

---

# 2. Flow বুঝে নাও

```text
i = 1
 ↓
print 1
 ↓
i = 2
 ↓
print 2
 ↓
...
 ↓
i = 5
 ↓
i == 5?
 ↓ YES
break
 ↓
Loop শেষ
```

তাই `5` print হয়নি, কারণ `break` check হওয়ার পরেই loop থেকে বের হয়ে গেছে।

---

# 3. `break` কোথায় কাজ করে?

`break` সাধারণত ব্যবহার করা হয়:

```text
for
while
do-while
switch
```

এর মধ্যে।

---

# 4. `for` Loop-এ `break`

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 100; i++) {

        if (i == 10) {
            break;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
5
6
7
8
9
```

---

# 5. `while` Loop-এ `break`

```c
#include <stdio.h>

int main() {
    int i = 1;

    while (i <= 10) {

        if (i == 6) {
            break;
        }

        printf("%d\n", i);
        i++;
    }

    return 0;
}
```

Output:

```text
1
2
3
4
5
```

---

# 6. `do-while`-এ `break`

```c
#include <stdio.h>

int main() {
    int i = 1;

    do {

        if (i == 4) {
            break;
        }

        printf("%d\n", i);
        i++;

    } while (i <= 10);

    return 0;
}
```

Output:

```text
1
2
3
```

---

# 7. `break` বনাম Loop Condition

ধরো:

```c
for (int i = 1; i <= 100; i++) {
    if (i == 5) {
        break;
    }

    printf("%d\n", i);
}
```

এখানে loop-এর normal condition:

```c
i <= 100
```

কিন্তু আমরা চাইছি:

```text
i == 5 হলে আগেই stop
```

তাই `break` ব্যবহার করেছি।

অর্থাৎ:

> Loop-এর normal condition-এর আগেই কোনো বিশেষ কারণে বের হতে চাইলে `break` খুব useful।

---

# 8. Search-এর সময় `break`

এটি খুব গুরুত্বপূর্ণ practical use।

ধরো 1 থেকে 100-এর মধ্যে `37` খুঁজছি।

```c
#include <stdio.h>

int main() {
    int target = 37;

    for (int i = 1; i <= 100; i++) {

        if (i == target) {
            printf("Found!\n");
            break;
        }
    }

    return 0;
}
```

`37` পাওয়া গেলে আর `38, 39, ... 100` check করার দরকার নেই।

তাই:

```text
37 পাওয়া গেছে
      ↓
break
      ↓
search শেষ
```

এটা বড় data-এর ক্ষেত্রে খুব useful হতে পারে।

---

# 9. User Input Search

ধরো 10টি number input নিতে হবে। কিন্তু `-1` দিলে আর input নিতে হবে না।

```c
#include <stdio.h>

int main() {
    int number;

    for (int i = 1; i <= 10; i++) {

        printf("Enter number: ");
        scanf("%d", &number);

        if (number == -1) {
            break;
        }

        printf("You entered: %d\n", number);
    }

    return 0;
}
```

Input:

```text
10
20
30
-1
```

`-1` পাওয়ার সঙ্গে সঙ্গে loop শেষ।

---

# 10. Infinite Loop + `break`

এটি খুব important pattern:

```c
while (1) {

    // কাজ

    if (condition) {
        break;
    }
}
```

যেমন:

```c
#include <stdio.h>

int main() {
    int number;

    while (1) {
        printf("Enter 0 to exit: ");
        scanf("%d", &number);

        if (number == 0) {
            break;
        }

        printf("You entered %d\n", number);
    }

    printf("Program ended.\n");

    return 0;
}
```

এখানে:

```text
while (1)
   ↓
চলতেই থাকবে
   ↓
user 0 দেয়?
   ↓
YES
   ↓
break
   ↓
শেষ
```

---

# 11. `break` + `switch`

`switch`-এ আমরা আগেই `break` দেখেছি:

```c
switch (choice) {

    case 1:
        printf("One\n");
        break;

    case 2:
        printf("Two\n");
        break;

    default:
        printf("Invalid\n");
}
```

এখানে `break` loop থেকে নয়, **switch থেকে বের হওয়ার জন্য** ব্যবহৃত হচ্ছে।

---

# 12. খুব গুরুত্বপূর্ণ — Nested Loop

ধরো:

```c
for (int i = 1; i <= 3; i++) {

    for (int j = 1; j <= 3; j++) {

        if (j == 2) {
            break;
        }

        printf("%d %d\n", i, j);
    }
}
```

এখানে `break` কোন loop বন্ধ করবে?

**শুধু সবচেয়ে কাছের/ভেতরের loop।**

Output:

```text
1 1
2 1
3 1
```

কারণ প্রতিটি `i`-এর জন্য:

```text
j = 1 → print
j = 2 → break inner loop
```

Outer loop চলতেই থাকে।

---

# 13. Nested Loop-এর Flow

```text
Outer loop
    ↓
 Inner loop
    ↓
 j == 2?
    ↓ YES
 break
    ↓
Inner loop শেষ
    ↓
Outer loop আবার
```

এটি খুব গুরুত্বপূর্ণ।

---

# 14. `break` পুরো Program বন্ধ করে না

ধরো:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 10; i++) {

        if (i == 5) {
            break;
        }

        printf("%d\n", i);
    }

    printf("Program continues...\n");

    return 0;
}
```

Output:

```text
1
2
3
4
Program continues...
```

অর্থাৎ `break`:

```text
loop শেষ করে
```

কিন্তু:

```text
program necessarily শেষ করে না
```

---

# 15. `break` বনাম `return`

এ দুটো গুলিয়ে ফেলো না।

### `break`

শুধু loop/switch থেকে বের হয়:

```c
break;
```

### `return`

Function থেকে বের হয়:

```c
return 0;
```

উদাহরণ:

```c
for (int i = 1; i <= 10; i++) {

    if (i == 5) {
        break;
    }
}

printf("After loop\n");
```

`break` হওয়ার পর `"After loop"` print হবে।

কিন্তু:

```c
if (i == 5) {
    return 0;
}
```

হলে `main()` function-ই শেষ হয়ে যাবে।

---

# 16. Prime Number Check-এ `break`

এটি `break`-এর খুব সুন্দর application।

কোনো number prime কিনা check করতে তার ছোট divisor খুঁজতে পারি।

```c
#include <stdio.h>

int main() {
    int n;
    int isPrime = 1;

    printf("Enter a number: ");
    scanf("%d", &n);

    if (n < 2) {
        isPrime = 0;
    } else {

        for (int i = 2; i < n; i++) {

            if (n % i == 0) {
                isPrime = 0;
                break;
            }
        }
    }

    if (isPrime) {
        printf("Prime\n");
    } else {
        printf("Not Prime\n");
    }

    return 0;
}
```

ধরো:

```text
n = 15
```

Loop:

```text
15 % 2 → no
15 % 3 → yes
```

`3` দিয়ে divisible পাওয়া গেছে।

তাই:

```text
break
 ↓
আর check করার দরকার নেই
```

---

# 17. Search Example

Array এখনও officially শেখা হয়নি—Phase 5-এ শিখব। তাই এখন simple range search দেখি।

```c
#include <stdio.h>

int main() {
    int target = 7;

    for (int i = 1; i <= 10; i++) {

        if (i == target) {
            printf("Found %d\n", target);
            break;
        }
    }

    return 0;
}
```

---

# 🧪 Practice 1

`1` থেকে `100` পর্যন্ত loop চালাও।

কিন্তু `50` এ পৌঁছালে `break` করো।

Expected output:

```text
1
2
3
...
49
```

---

# 🧪 Practice 2

User সর্বোচ্চ 10টি number input দেবে।

কিন্তু user `0` দিলে input নেওয়া বন্ধ করবে।

Hint:

```c
if (number == 0) {
    break;
}
```

---

# 🧪 Practice 3

`1` থেকে `100` পর্যন্ত প্রথম number খুঁজে বের করো যেটি:

```text
7 দিয়ে divisible
```

Hint:

```c
if (i % 7 == 0) {
    printf("%d\n", i);
    break;
}
```

Expected:

```text
7
```

---

# 🔥 Mini Challenge — First Divisor

User একটি integer `n` দেবে।

`2` থেকে শুরু করে তার প্রথম divisor খুঁজে বের করো।

Example:

```text
Input: 91
```

Output:

```text
First divisor = 7
```

কারণ:

```text
91 % 2 → not divisible
91 % 3 → not divisible
...
91 % 7 → divisible
```

তারপর `break` করবে।

---

# 🧠 আজকের Cheat Sheet

### Basic

```c
break;
```

### Loop থেকে বের হও

```c
for (...) {

    if (condition) {
        break;
    }
}
```

### Infinite loop control

```c
while (1) {

    if (condition) {
        break;
    }
}
```

### Important

```text
break
 ↓
সবচেয়ে কাছের loop/switch থেকে বের হয়
```

Nested loop-এ:

```text
break
 ↓
inner loop বন্ধ
 ↓
outer loop চলতে পারে
```

---

# 🎯 Phase 3 Progress

```text
16. ✅ for
17. ✅ while
18. ✅ do-while
19. ✅ break
20. ⏳ continue
21. ⏳ Nested loops
22. ⏳ Pattern problems
```

## পরের Lesson → Lesson 20 — `continue`

`break` যেখানে **পুরো loop বন্ধ করে**, `continue` সেখানে **শুধু current iteration skip করে পরের iteration-এ চলে যায়**।

এটা `break`-এর সঙ্গে পার্থক্য বুঝতে খুব গুরুত্বপূর্ণ।

---
# 🚀 Lesson 20 — `continue`

আজ আমরা শিখব **`continue` statement**।

`break` যেখানে loop **পুরোপুরি বন্ধ করে**, `continue` সেখানে **শুধু বর্তমান iteration skip করে** এবং loop-এর পরের iteration-এ চলে যায়।

---

# 1. `continue` কী?

Syntax:

```c
continue;
```

সহজভাবে:

```text
বর্তমান iteration
      ↓
continue
      ↓
বাকি code skip
      ↓
পরের iteration
```

---

# 2. সবচেয়ে সহজ Example

1 থেকে 10 পর্যন্ত print করব, কিন্তু `5` বাদ দেব:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 10; i++) {

        if (i == 5) {
            continue;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
6
7
8
9
10
```

`i == 5` হলে:

```c
continue;
```

হয়েছে।

তাই `printf()` execute হয়নি।

কিন্তু loop **বন্ধও হয়নি**।

---

# 3. `break` বনাম `continue`

এটা খুব ভালোভাবে বুঝে রাখো।

### `break`

```c
if (i == 5) {
    break;
}
```

মানে:

```text
1
2
3
4
STOP
```

### `continue`

```c
if (i == 5) {
    continue;
}
```

মানে:

```text
1
2
3
4
SKIP 5
6
7
8
9
10
```

### মনে রাখার সহজ উপায়

```text
break    → বের হয়ে যাও
continue → বাদ দিয়ে এগিয়ে যাও
```

---

# 4. `continue` কীভাবে কাজ করে?

এই code:

```c
for (int i = 1; i <= 5; i++) {

    if (i == 3) {
        continue;
    }

    printf("%d\n", i);
}
```

Flow:

```text
i = 1
 ↓
condition true
 ↓
i == 3? No
 ↓
print 1
 ↓
i++

i = 2
 ↓
print 2
 ↓
i++

i = 3
 ↓
i == 3? YES
 ↓
continue
 ↓
printf skip
 ↓
i++

i = 4
 ↓
print 4

i = 5
 ↓
print 5
```

Output:

```text
1
2
4
5
```

---

# 5. Even Numbers বাদ দিয়ে Odd Numbers

`continue` ব্যবহার করে 1 থেকে 20-এর মধ্যে শুধু odd numbers:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 20; i++) {

        if (i % 2 == 0) {
            continue;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
3
5
7
9
11
13
15
17
19
```

Logic:

```text
even?
 ↓
YES → skip
 ↓
NO → print
```

---

# 6. Odd Numbers বাদ দিয়ে Even Numbers

```c
for (int i = 1; i <= 20; i++) {

    if (i % 2 != 0) {
        continue;
    }

    printf("%d\n", i);
}
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

---

# 7. `continue` + `if`

এটি খুব common pattern:

```c
for (int i = 1; i <= 100; i++) {

    if (condition) {
        continue;
    }

    // কাজ
}
```

অর্থাৎ:

> যেগুলো process করতে চাই না, সেগুলো শুরুতেই skip করে দাও।

---

# 8. 3 দিয়ে Divisible Numbers বাদ

1 থেকে 20-এর মধ্যে যেগুলো 3 দিয়ে divisible **নয়**, সেগুলো print:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 20; i++) {

        if (i % 3 == 0) {
            continue;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
4
5
7
8
10
11
13
14
16
17
19
20
```

---

# 9. User Input-এর সঙ্গে `continue`

ধরো 5টি number input নেব।

Negative number হলে সেটা process করব না।

```c
#include <stdio.h>

int main() {
    int number;

    for (int i = 1; i <= 5; i++) {

        printf("Enter number: ");
        scanf("%d", &number);

        if (number < 0) {
            continue;
        }

        printf("Accepted: %d\n", number);
    }

    return 0;
}
```

Input:

```text
10
-5
20
-2
30
```

Output:

```text
Accepted: 10
Accepted: 20
Accepted: 30
```

Negative numbers skip হয়েছে।

---

# 10. `continue` এবং `break` একসঙ্গে

দুটো একসঙ্গে ব্যবহার করা যায়।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 20; i++) {

        if (i % 2 == 0) {
            continue;
        }

        if (i > 15) {
            break;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
3
5
7
9
11
13
15
```

Flow:

```text
even → continue
odd → check i > 15
      ↓
     true → break
```

---

# 11. খুব গুরুত্বপূর্ণ: `while`-এ `continue`

এখানে beginner-রা একটি common mistake করে।

এই code:

```c
int i = 1;

while (i <= 10) {

    if (i == 5) {
        continue;
    }

    printf("%d\n", i);
    i++;
}
```

এটি **infinite loop** হয়ে যাবে।

কেন?

যখন:

```text
i = 5
```

তখন:

```c
continue;
```

হবে।

ফলে:

```c
i++;
```

execute হবে না।

তাই `i` সবসময় 5 থাকবে।

---

# 12. Correct `while` Version

Update আগে করে দিতে পারো:

```c
#include <stdio.h>

int main() {
    int i = 0;

    while (i < 10) {

        i++;

        if (i == 5) {
            continue;
        }

        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
6
7
8
9
10
```

এখানে `i++` `continue`-এর আগে হচ্ছে।

---

# 13. `for` Loop-এ কেন সহজ?

`for` loop-এ:

```c
for (int i = 1; i <= 10; i++) {

    if (i == 5) {
        continue;
    }

    printf("%d\n", i);
}
```

`continue` হলে loop-এর **update expression**:

```c
i++
```

তারপর execute হয়।

তাই `for` loop-এ `continue` ব্যবহার তুলনামূলকভাবে সহজ।

---

# 14. `continue` `do-while`-এ

`do-while`-এও ব্যবহার করা যায়, তবে update-এর জায়গা নিয়ে সতর্ক থাকতে হবে।

```c
int i = 0;

do {
    i++;

    if (i == 3) {
        continue;
    }

    printf("%d\n", i);

} while (i <= 5);
```

Output:

```text
1
2
4
5
6
```

এখানে `continue` হলে control condition check-এর দিকে যায়।

---

# 15. `continue` কি Loop বন্ধ করে?

**না।**

এটাই সবচেয়ে গুরুত্বপূর্ণ।

```text
continue
   ↓
current iteration শেষ/skip
   ↓
next iteration
```

আর:

```text
break
   ↓
loop শেষ
```

---

# 16. বাস্তব Example — শুধু Valid Data Process

ধরো 10টি marks input নিতে হবে।

Invalid marks:

```text
marks < 0
marks > 100
```

এসব skip করতে পারি:

```c
#include <stdio.h>

int main() {
    int marks;

    for (int i = 1; i <= 10; i++) {

        printf("Enter marks: ");
        scanf("%d", &marks);

        if (marks < 0 || marks > 100) {
            printf("Invalid marks. Skipping...\n");
            continue;
        }

        printf("Valid marks = %d\n", marks);
    }

    return 0;
}
```

এখানে invalid input-এর জন্য নিচের processing হবে না।

---

# 17. `continue` দিয়ে Filter করা

একটি useful mindset:

```text
সব data loop করো
      ↓
যেগুলো দরকার নেই
      ↓
continue
      ↓
যেগুলো দরকার
      ↓
process
```

এটাকে তুমি **filtering** হিসেবে ভাবতে পারো।

---

# 🧪 Practice 1

1 থেকে 50 পর্যন্ত print করো।

কিন্তু সব **multiple of 5** skip করবে।

Expected শুরু:

```text
1
2
3
4
6
7
8
9
11
...
```

---

# 🧪 Practice 2

1 থেকে 100 পর্যন্ত শুধু এমন number print করো যেগুলো:

- even
    
- এবং 3 দিয়ে divisible নয়
    

Hint:

```c
if (i % 2 != 0 || i % 3 == 0) {
    continue;
}
```

---

# 🧪 Practice 3

5টি number input নাও।

Negative number হলে:

```text
Invalid
```

print করে `continue` করো।

Positive number হলে:

```text
Valid
```

print করো।

---

# 🔥 Mini Challenge — Sum of Positive Numbers

User 10টি integer input দেবে।

- Positive হলে sum-এ যোগ করবে।
    
- Zero/negative হলে skip করবে।
    

Example:

```text
Input:
10
-5
20
0
7
-2
3
8
-1
4
```

শুধু positive numbers:

```text
10 + 20 + 7 + 3 + 8 + 4
```

Output:

```text
Sum = 52
```

---

# 🧠 আজকের Cheat Sheet

### `continue`

```c
continue;
```

### Skip current iteration

```c
for (...) {

    if (condition) {
        continue;
    }

    // process
}
```

### `break`

```text
loop → STOP
```

### `continue`

```text
current iteration → SKIP
next iteration → CONTINUE
```

---

# 🎯 Phase 3 Progress

```text
16. ✅ for
17. ✅ while
18. ✅ do-while
19. ✅ break
20. ✅ continue
21. ⏳ Nested loops
22. ⏳ Pattern problems
```

## 🚀 Next: Lesson 21 — Nested Loops

এবার আমরা **একটি loop-এর ভিতরে আরেকটি loop** চালাব।

যেমন:

```text
1 2 3
1 2 3
1 2 3
```

এবং এখান থেকেই আমরা আস্তে আস্তে **pattern problems**-এর দিকে যাব।

---
# 🚀 Lesson 21 — Nested Loops

এখন আমরা শিখব **Nested Loop** — অর্থাৎ **একটি loop-এর ভিতরে আরেকটি loop**।

এটা C-তে খুব গুরুত্বপূর্ণ, কারণ পরে:

- Matrix
    
- 2D Array
    
- Pattern problems
    
- Tables
    
- Data structures
    

এসব বুঝতে nested loop দরকার হবে।

---

# 1. Nested Loop কী?

একটি loop-এর ভিতরে আরেকটি loop:

```c
for (...) {

    for (...) {
        // inner loop
    }

}
```

এখানে:

- বাইরের loop = **Outer loop**
    
- ভেতরের loop = **Inner loop**
    

---

# 2. সবচেয়ে সহজ Example

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 3; j++) {
            printf("%d %d\n", i, j);
        }

    }

    return 0;
}
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

---

# 3. কীভাবে কাজ করছে?

প্রথমে:

```text
i = 1
```

তারপর inner loop পুরোটা চলে:

```text
j = 1
j = 2
j = 3
```

তারপর outer loop:

```text
i = 2
```

আবার inner loop পুরোটা:

```text
j = 1
j = 2
j = 3
```

তারপর:

```text
i = 3
```

আবার:

```text
j = 1
j = 2
j = 3
```

অর্থাৎ:

```text
Outer i=1
    Inner j=1
    Inner j=2
    Inner j=3

Outer i=2
    Inner j=1
    Inner j=2
    Inner j=3

Outer i=3
    Inner j=1
    Inner j=2
    Inner j=3
```

---

# 4. সবচেয়ে গুরুত্বপূর্ণ ধারণা

যদি outer loop `3` বার চলে এবং inner loop প্রতিবার `4` বার চলে:

```text
3 × 4 = 12
```

অর্থাৎ inner loop মোট **12 বার** execute করবে।

উদাহরণ:

```c
for (int i = 1; i <= 3; i++) {

    for (int j = 1; j <= 4; j++) {
        printf("*");
    }

}
```

Inner loop:

```text
4 বার
```

Outer loop:

```text
3 বার
```

মোট:

```text
3 × 4 = 12
```

---

# 5. Rectangle Pattern ⭐

Nested loop-এর classic use:

```text
****
****
****
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 4; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
****
****
****
```

---

# 6. এখানে `i` এবং `j` কী করছে?

```c
for (int i = 1; i <= 3; i++)
```

এটি **row** control করছে।

```c
for (int j = 1; j <= 4; j++)
```

এটি **column** control করছে।

তাই:

```text
3 rows × 4 columns
```

একটি rectangle তৈরি হয়েছে।

---

# 7. Row এবং Column বুঝে নাও

Output:

```text
****
****
****
```

এখানে:

```text
Rows = 3
Columns = 4
```

Visual:

```text
      columns
       ↓↓↓↓
      ****
      ****
      ****
      ↑
     rows
```

এটা পরের **2D Array/Matrix** lesson-এ খুব কাজে লাগবে।

---

# 8. Number Pattern

এবার `*`-এর বদলে number:

```text
1234
1234
1234
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 4; j++) {
            printf("%d", j);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
1234
1234
1234
```

---

# 9. Row Number Print করা

এবার:

```text
1111
2222
3333
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 4; j++) {
            printf("%d", i);
        }

        printf("\n");
    }

    return 0;
}
```

এখানে:

- `i` = row number
    
- `j` = কতবার print হবে
    

---

# 10. দুই ধরনের Number Pattern-এর পার্থক্য

### `j` print করলে

```c
printf("%d", j);
```

Output:

```text
1234
1234
1234
```

### `i` print করলে

```c
printf("%d", i);
```

Output:

```text
1111
2222
3333
```

এই পার্থক্যটা pattern problem-এ খুব গুরুত্বপূর্ণ।

---

# 11. Square Pattern

5 × 5:

```text
*****
*****
*****
*****
*****
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= 5; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 12. Triangle Pattern ⭐

এবার:

```text
*
**
***
****
*****
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

এখানে গুরুত্বপূর্ণ বিষয়:

```c
j <= i
```

Outer loop যত বাড়ছে, inner loop-এর কাজও তত বাড়ছে।

---

# 13. Triangle-এর Flow

```text
i = 1
    j = 1 → *

i = 2
    j = 1 → *
    j = 2 → *

i = 3
    j = 1 → *
    j = 2 → *
    j = 3 → *
```

তাই:

```text
*
**
***
```

---

# 14. Reverse Triangle

চাই:

```text
*****
****
***
**
*
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 5; i >= 1; i--) {

        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 15. Number Triangle

```text
1
12
123
1234
12345
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("%d", j);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 16. Repeated Number Triangle

```text
1
22
333
4444
55555
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("%d", i);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 17. Multiplication Tables

Nested loop দিয়ে একসঙ্গে অনেক multiplication table তৈরি করা যায়।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= 10; j++) {
            printf("%d x %d = %d\n", i, j, i * j);
        }

        printf("\n");
    }

    return 0;
}
```

এখানে:

```text
i = table number
j = multiplier
```

---

# 18. Nested `while` Loop

Nested loop শুধু `for` দিয়েই হয় না।

```c
#include <stdio.h>

int main() {
    int i = 1;

    while (i <= 3) {

        int j = 1;

        while (j <= 3) {
            printf("%d %d\n", i, j);
            j++;
        }

        i++;
    }

    return 0;
}
```

এটাও nested loop।

---

# 19. Nested `do-while`

এভাবেও করা যায়:

```c
int i = 1;

do {
    int j = 1;

    do {
        printf("%d %d\n", i, j);
        j++;
    } while (j <= 3);

    i++;
} while (i <= 3);
```

তবে pattern problems-এ সাধারণত `for` loop বেশি readable।

---

# 20. Nested Loop + `break`

মনে আছে, `break` সবচেয়ে কাছের loop থেকে বের হয়।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 5; j++) {

            if (j == 3) {
                break;
            }

            printf("%d ", j);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
1 2
1 2
1 2
```

কারণ `break` শুধু inner loop বন্ধ করছে।

---

# 21. Nested Loop + `continue`

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 3; i++) {

        for (int j = 1; j <= 5; j++) {

            if (j == 3) {
                continue;
            }

            printf("%d ", j);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
1 2 4 5
1 2 4 5
1 2 4 5
```

শুধু inner loop-এর current iteration skip হয়েছে।

---

# 22. Nested Loop-এর Golden Rule 🧠

Pattern problem দেখলে প্রথমে ভাবো:

### Step 1

কতগুলো **row**?

```c
for (int i = 1; i <= rows; i++)
```

### Step 2

প্রতিটি row-তে কতগুলো **column/item**?

```c
for (int j = 1; j <= columns; j++)
```

### Step 3

প্রতিটি position-এ কী print হবে?

```c
printf("*");
```

অথবা:

```c
printf("%d", j);
```

---

# 🧪 Practice 1

এই pattern তৈরি করো:

```text
****
****
****
****
```

Hint:

```text
4 rows
4 columns
```

---

# 🧪 Practice 2

```text
*
**
***
****
*****
```

---

# 🧪 Practice 3

```text
12345
12345
12345
12345
12345
```

---

# 🧪 Practice 4

```text
11111
22222
33333
44444
55555
```

---

# 🔥 Mini Challenge 1

এই pattern তৈরি করো:

```text
1
12
123
1234
12345
```

---

# 🔥 Mini Challenge 2

এই pattern:

```text
12345
1234
123
12
1
```

Hint:

Outer loop:

```c
for (int i = 5; i >= 1; i--)
```

Inner loop:

```c
for (int j = 1; j <= i; j++)
```

---

# 🔥 Mini Challenge 3 — Multiplication Grid

এই ধরনের output তৈরি করো:

```text
1 2 3 4 5
2 4 6 8 10
3 6 9 12 15
4 8 12 16 20
5 10 15 20 25
```

Hint:

```c
printf("%d ", i * j);
```

---

# 🧠 আজকের Cheat Sheet

### Nested loop

```c
for (...) {

    for (...) {

    }

}
```

### Rectangle

```c
for (int i = 1; i <= rows; i++) {
    for (int j = 1; j <= columns; j++) {
        printf("*");
    }
    printf("\n");
}
```

### Increasing triangle

```c
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        printf("*");
    }
    printf("\n");
}
```

### Reverse triangle

```c
for (int i = 5; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        printf("*");
    }
    printf("\n");
}
```

---

# 🎯 Phase 3 Progress

```text
16. ✅ for
17. ✅ while
18. ✅ do-while
19. ✅ break
20. ✅ continue
21. ✅ Nested loops
22. ⏳ Pattern problems
```

## 🚀 Next: Lesson 22 — Pattern Problems

এটাই Phase 3-এর শেষ lesson।

আমরা `*`, numbers, spaces ব্যবহার করে বিভিন্ন pattern বানাব এবং **pattern দেখে কীভাবে loop-এর logic বের করতে হয়** সেটা শিখব।


----

# 🚀 Lesson 22 — Pattern Problems

আজ **Phase 3 — Loops**-এর শেষ lesson। 🎉

Pattern problems দেখতে সহজ হলেও এগুলো nested loop বোঝার জন্য অসাধারণ practice।

আজ আমরা শিখব কীভাবে কোনো pattern দেখে:

1. **কতগুলো row আছে**
    
2. প্রতি row-তে **কতগুলো character**
    
3. **কী print করতে হবে**
    
4. কোথায় **space** লাগবে
    

— এগুলো বের করতে হয়।

---

# 1. Pattern Problem-এর Basic Formula

প্রথমে এই structure মনে রাখো:

```c
for (int i = 1; i <= rows; i++) {

    for (int j = 1; j <= columns; j++) {
        // print something
    }

    printf("\n");
}
```

এখানে:

```text
i → row
j → column
```

---

# 2. Pattern 1 — Square

চাই:

```text
*****
*****
*****
*****
*****
```

এখানে:

```text
Rows = 5
Columns = 5
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= 5; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 3. Pattern 2 — Rectangle

```text
*******
*******
*******
*******
```

এখানে:

```text
Rows = 4
Columns = 7
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 4; i++) {

        for (int j = 1; j <= 7; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

### Golden rule

```text
Outer loop → কতগুলো line
Inner loop → প্রতি line-এ কতগুলো *
```

---

# 4. Pattern 3 — Increasing Triangle

```text
*
**
***
****
*****
```

এখানে লক্ষ্য করো:

```text
Row 1 → 1 star
Row 2 → 2 stars
Row 3 → 3 stars
Row 4 → 4 stars
Row 5 → 5 stars
```

তাই:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

মূল logic:

```c
j <= i
```

---

# 5. Pattern 4 — Decreasing Triangle

```text
*****
****
***
**
*
```

এখানে:

```text
5
4
3
2
1
```

তাই:

```c
#include <stdio.h>

int main() {

    for (int i = 5; i >= 1; i--) {

        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 6. Pattern 5 — Number Triangle

```text
1
12
123
1234
12345
```

এখানে প্রতি row-তে:

```text
1 থেকে i
```

print হচ্ছে।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("%d", j);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 7. Pattern 6 — Repeated Row Number

```text
1
22
333
4444
55555
```

এখানে প্রতি row-তে `j` নয়, **`i` print হচ্ছে**।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("%d", i);
        }

        printf("\n");
    }

    return 0;
}
```

### পার্থক্য

```c
printf("%d", j);
```

দিলে:

```text
123
```

আর:

```c
printf("%d", i);
```

দিলে:

```text
333
```

---

# 8. Pattern 7 — Reverse Number Triangle

```text
12345
1234
123
12
1
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 5; i >= 1; i--) {

        for (int j = 1; j <= i; j++) {
            printf("%d", j);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 9. Pattern 8 — Right-Aligned Triangle ⭐

এবার একটু কঠিন:

```text
    *
   **
  ***
 ****
*****
```

এখানে শুধু `*` নয়, **spaces**-ও print করতে হবে।

প্রথম row:

```text
    *
```

মানে:

```text
4 spaces + 1 star
```

দ্বিতীয়:

```text
   **
```

মানে:

```text
3 spaces + 2 stars
```

তাই:

```text
Row → Spaces + Stars

1 → 4 + 1
2 → 3 + 2
3 → 2 + 3
4 → 1 + 4
5 → 0 + 5
```

---

# 10. Right-Aligned Triangle Code

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        // spaces
        for (int j = 1; j <= 5 - i; j++) {
            printf(" ");
        }

        // stars
        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 11. Pattern 9 — Pyramid ⭐🔥

চাই:

```text
    *
   ***
  *****
 *******
*********
```

এখানে প্রতি row:

```text
Spaces + Stars
```

### Spaces

```text
4
3
2
1
0
```

অর্থাৎ:

```c
5 - i
```

### Stars

```text
1
3
5
7
9
```

Formula:

```c
2 * i - 1
```

---

# 12. Pyramid Code

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        // spaces
        for (int j = 1; j <= 5 - i; j++) {
            printf(" ");
        }

        // stars
        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

এটি pattern problem-এর খুব গুরুত্বপূর্ণ formula।

---

# 13. Pyramid-এর Formula বুঝে নাও

```text
Row 1:
spaces = 4
stars  = 1

Row 2:
spaces = 3
stars  = 3

Row 3:
spaces = 2
stars  = 5

Row 4:
spaces = 1
stars  = 7

Row 5:
spaces = 0
stars  = 9
```

তাই:

```text
spaces = n - i
stars  = 2i - 1
```

---

# 14. Pattern 10 — Inverted Pyramid

```text
*********
 *******
  *****
   ***
    *
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 5; i >= 1; i--) {

        // spaces
        for (int j = 1; j <= 5 - i; j++) {
            printf(" ");
        }

        // stars
        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("*");
        }

        printf("\n");
    }

    return 0;
}
```

---

# 15. Pattern 11 — Number Pyramid

```text
    1
   123
  12345
 1234567
123456789
```

Code:

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= 5 - i; j++) {
            printf(" ");
        }

        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("%d", j);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 16. Pattern 12 — 0/1 Triangle

```text
1
01
101
0101
10101
```

এখানে একটু logic লাগবে।

একটি number-এর parity অনুযায়ী:

```c
(i + j) % 2
```

ব্যবহার করা যায়।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {

            if ((i + j) % 2 == 0) {
                printf("1");
            } else {
                printf("0");
            }
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
1
01
101
0101
10101
```

---

# 17. Pattern 13 — Multiplication Grid

```text
1 2 3 4 5
2 4 6 8 10
3 6 9 12 15
4 8 12 16 20
5 10 15 20 25
```

এখানে:

```c
i * j
```

ব্যবহার করব।

```c
#include <stdio.h>

int main() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= 5; j++) {
            printf("%d ", i * j);
        }

        printf("\n");
    }

    return 0;
}
```

---

# 18. Pattern Problem Solve করার Strategy 🧠

কোনো pattern দেখেই code লিখতে যেও না।

প্রথমে **row table** বানাও।

ধরো:

```text
    *
   ***
  *****
 *******
*********
```

Table:

|Row|Spaces|Stars|
|--:|--:|--:|
|1|4|1|
|2|3|3|
|3|2|5|
|4|1|7|
|5|0|9|

তারপর formula:

```text
Spaces = n - i
Stars = 2*i - 1
```

এভাবেই pattern solve করবে।

---

# 19. Pattern Problem-এর 4-Step Method

### Step 1 — Rows

কতটি line?

```c
for (int i = 1; i <= n; i++)
```

### Step 2 — Spaces

Spaces-এর pattern বের করো।

### Step 3 — Main character

`*`, number বা অন্য কিছু কতবার print হবে বের করো।

### Step 4 — Newline

প্রতি row শেষে:

```c
printf("\n");
```

---

# 🧪 Practice Set

এখন নিজে চেষ্টা করো।

### Practice 1

```text
*
**
***
****
*****
```

---

### Practice 2

```text
*****
****
***
**
*
```

---

### Practice 3

```text
12345
1234
123
12
1
```

---

### Practice 4

```text
1
22
333
4444
55555
```

---

### Practice 5

```text
    *
   **
  ***
 ****
*****
```

---

### Practice 6

```text
    *
   ***
  *****
 *******
*********
```

---

# 🔥 Challenge 1 — Hollow Square

এবার ভিতরটা ফাঁকা:

```text
*****
*   *
*   *
*   *
*****
```

Hint:

Boundary হলে `*`, otherwise space।

Condition:

```c
if (i == 1 || i == n || j == 1 || j == n)
```

---

# 🔥 Challenge 2 — Hollow Rectangle

```text
*******
*     *
*     *
*******
```

এখানে:

```text
Rows = 4
Columns = 7
```

Boundary logic ব্যবহার করো।

---

# 🔥 Challenge 3 — Diamond

সবচেয়ে challenging pattern:

```text
    *
   ***
  *****
 *******
  *****
   ***
    *
```

Hint: এটাকে দুই ভাগে ভাবো:

```text
Upper pyramid
+
Lower inverted pyramid
```

একবারে পুরো pattern solve করার চেষ্টা না করে **দুইটা nested-loop section** বানাও।

---

# 🧠 আজকের Most Important Formulas

### Increasing triangle

```text
stars = i
```

```c
for (int j = 1; j <= i; j++)
```

### Decreasing triangle

```text
stars = i
```

কিন্তু:

```c
for (int i = n; i >= 1; i--)
```

### Right-aligned triangle

```text
spaces = n - i
stars  = i
```

### Pyramid

```text
spaces = n - i
stars  = 2*i - 1
```

---

# 🎉 Phase 3 Complete!

তুমি এখন C-এর loops-এর পুরো foundation শেষ করেছ:

```text
16. ✅ for
17. ✅ while
18. ✅ do-while
19. ✅ break
20. ✅ continue
21. ✅ Nested loops
22. ✅ Pattern problems
```

### এখন তুমি পারো:

```text
Counting
   ↓
Repetition
   ↓
Condition-based loops
   ↓
Skip / Stop
   ↓
Nested loops
   ↓
Patterns
```

---

# 🚀 Next Phase — Functions

এবার শুরু হবে:

## Phase 4 — Functions

```text
23. Function basics
24. Parameters & arguments
25. Return value
26. Call by value
27. Recursion
28. Scope & lifetime
29. Header files
```

### Lesson 23 — Function Basics

আমরা শিখব:

```c
return_type function_name() {
    // code
}
```

এবং কেন বড় program-কে ছোট ছোট reusable অংশে ভাগ করার জন্য **function** এত গুরুত্বপূর্ণ।

---
# 🚀 Lesson 23 — Function Basics

Phase 4 শুরু! 🎉

এখন থেকে আমরা C program-কে **ছোট ছোট reusable অংশে ভাগ করা** শিখব।

---

# 1. Function কী?

Function হলো এমন একটি **নির্দিষ্ট কাজের জন্য তৈরি code block**, যাকে প্রয়োজন হলে বারবার call করা যায়।

ধরো, তোমাকে 10 বার একই কাজ করতে হবে।

Function ছাড়া:

```text
একই code
একই code
একই code
...
```

Function ব্যবহার করলে:

```text
Function তৈরি
    ↓
প্রয়োজন হলে call
    ↓
আবার call
    ↓
আবার call
```

---

# 2. প্রথম Function

```c
#include <stdio.h>

void hello() {
    printf("Hello!\n");
}

int main() {

    hello();

    return 0;
}
```

Output:

```text
Hello!
```

এখানে:

```c
void hello()
```

হলো function-এর definition।

আর:

```c
hello();
```

হলো function call।

---

# 3. Function-এর Basic Structure

```c
return_type function_name() {

    // statements

}
```

উদাহরণ:

```c
void greet() {
    printf("Good morning!\n");
}
```

এখানে:

|অংশ|অর্থ|
|---|---|
|`void`|কিছু return করবে না|
|`greet`|Function-এর নাম|
|`()`|Parameters-এর জায়গা|
|`{ }`|Function body|

---

# 4. Function Call কী?

Function বানালেই সেটা automatically execute হয় না।

```c
void greet() {
    printf("Hello\n");
}
```

এটা শুধু function **define** করেছে।

Execute করতে:

```c
greet();
```

লিখতে হবে।

সম্পূর্ণ program:

```c
#include <stdio.h>

void greet() {
    printf("Hello\n");
}

int main() {

    greet();

    return 0;
}
```

---

# 5. Function একাধিকবার Call করা যায়

এটাই function-এর বড় সুবিধা।

```c
#include <stdio.h>

void greet() {
    printf("Hello!\n");
}

int main() {

    greet();
    greet();
    greet();

    return 0;
}
```

Output:

```text
Hello!
Hello!
Hello!
```

একই code তিনবার লিখতে হয়নি।

---

# 6. Function কেন ব্যবহার করব?

ধরো একটা বড় program:

```text
Bank Management System
```

সব code `main()`-এর মধ্যে লিখলে:

```text
main()
 ├── account creation
 ├── deposit
 ├── withdrawal
 ├── balance
 ├── login
 └── transaction
```

খুব বড় এবং difficult হয়ে যাবে।

Function ব্যবহার করলে:

```text
main()
 ├── createAccount()
 ├── deposit()
 ├── withdraw()
 ├── checkBalance()
 └── login()
```

এটা অনেক বেশি organized।

---

# 7. `main()`-ও একটি Function

এটা খুব গুরুত্বপূর্ণ।

আমরা সবসময় লিখি:

```c
int main()
```

`main()` নিজেও একটি function।

Program execution সাধারণত `main()` থেকেই শুরু হয়।

```text
Program
   ↓
main()
   ↓
other functions
```

---

# 8. `void` Function

যে function কোনো value return করে না, সেখানে:

```c
void
```

ব্যবহার করি।

উদাহরণ:

```c
void printNumber() {
    printf("10\n");
}
```

Call:

```c
printNumber();
```

---

# 9. Function-এর ভিতরে Variable

```c
#include <stdio.h>

void showNumber() {

    int x = 10;

    printf("%d\n", x);
}

int main() {

    showNumber();

    return 0;
}
```

Output:

```text
10
```

এখানে `x` function-এর ভিতরের variable।

এটা আমরা পরে **scope** lesson-এ বিস্তারিত শিখব।

---

# 10. একটি Function-এর মধ্যে Loop

Function-এর মধ্যে যেকোনো valid C code থাকতে পারে।

```c
#include <stdio.h>

void printNumbers() {

    for (int i = 1; i <= 5; i++) {
        printf("%d\n", i);
    }
}

int main() {

    printNumbers();

    return 0;
}
```

Output:

```text
1
2
3
4
5
```

অর্থাৎ function-এর মধ্যে:

- `if`
    
- loop
    
- variable
    
- অন্য function call
    

সবই থাকতে পারে।

---

# 11. Function + Pattern

আগের lesson-এর pattern-কে function-এর মধ্যে রাখতে পারি।

```c
#include <stdio.h>

void pattern() {

    for (int i = 1; i <= 5; i++) {

        for (int j = 1; j <= i; j++) {
            printf("*");
        }

        printf("\n");
    }
}

int main() {

    pattern();

    return 0;
}
```

Output:

```text
*
**
***
****
*****
```

---

# 12. Function Declaration / Prototype

একটি গুরুত্বপূর্ণ বিষয়।

ধরো `main()`-এর আগে function definition নেই:

```c
#include <stdio.h>

int main() {

    greet();

    return 0;
}

void greet() {
    printf("Hello\n");
}
```

কিছু compiler configuration-এ এটি সমস্যা তৈরি করবে, কারণ compiler `greet()` সম্পর্কে আগে জানে না।

তাই function prototype দিতে পারি:

```c
#include <stdio.h>

void greet();

int main() {

    greet();

    return 0;
}

void greet() {
    printf("Hello\n");
}
```

এখানে:

```c
void greet();
```

কে বলা হয় **function declaration/prototype**।

---

# 13. Function Prototype কেন?

এটা compiler-কে আগে জানিয়ে দেয়:

> `greet` নামে একটি function আছে, এটি কোনো value return করে না এবং কোনো parameter নেয় না।

তারপর নিচে আমরা function-এর আসল definition দিতে পারি।

Structure:

```text
Function prototype
       ↓
main()
       ↓
Function definition
```

---

# 14. Declaration বনাম Definition

দুটোর পার্থক্য:

### Declaration

```c
void greet();
```

শুধু জানাচ্ছে function আছে।

### Definition

```c
void greet() {
    printf("Hello\n");
}
```

এখানে function-এর আসল কাজ লেখা হয়েছে।

---

# 15. Function Naming

Function-এর নাম meaningful রাখো।

❌ খারাপ:

```c
void x() {
}
```

ভালো:

```c
void printMenu() {
}
```

আরও উদাহরণ:

```c
calculateSum()
printResult()
showMenu()
checkBalance()
findMaximum()
```

Function name দেখেই যেন বোঝা যায় function কী করে।

---

# 16. Function দিয়ে Code Organize করা

একটি simple calculator:

```c
#include <stdio.h>

void add() {
    int a = 10;
    int b = 20;

    printf("Sum = %d\n", a + b);
}

void subtract() {
    int a = 20;
    int b = 10;

    printf("Difference = %d\n", a - b);
}

int main() {

    add();
    subtract();

    return 0;
}
```

Output:

```text
Sum = 30
Difference = 10
```

পরে আমরা parameters এবং return value শিখলে calculator আরও powerful হবে।

---

# 17. Function-এর মধ্যে Function Call

একটি function অন্য function-কে call করতে পারে।

```c
#include <stdio.h>

void second() {
    printf("Second function\n");
}

void first() {

    printf("First function\n");

    second();
}

int main() {

    first();

    return 0;
}
```

Output:

```text
First function
Second function
```

Flow:

```text
main()
 ↓
first()
 ↓
second()
 ↓
back to first()
 ↓
back to main()
```

---

# 18. Function Execution Flow

এই program:

```c
#include <stdio.h>

void hello() {
    printf("Hello\n");
}

void bye() {
    printf("Bye\n");
}

int main() {

    hello();
    bye();

    return 0;
}
```

Flow:

```text
main()
 ↓
hello()
 ↓
"Hello"
 ↓
back to main()
 ↓
bye()
 ↓
"Bye"
 ↓
back to main()
 ↓
return 0
```

---

# 19. `void` মানে কী?

```c
void greet()
```

এখানে `void` মানে:

> Function কোনো value return করবে না।

কিন্তু function শুধু `void` হতে হবে এমন নয়।

যেমন:

```c
int add()
```

এটা integer return করতে পারে।

এটা আমরা পরের lesson-এ বিস্তারিত দেখব।

---

# 20. Function-এর 4টি Basic Type

এগুলো এখন শুধু concept হিসেবে মনে রাখো।

### 1. No parameter, no return

```c
void hello()
```

### 2. Parameter আছে, return নেই

```c
void hello(char name[])
```

### 3. Parameter নেই, return আছে

```c
int getNumber()
```

### 4. Parameter আছে, return আছে

```c
int add(int a, int b)
```

এই চার ধরনের function আমরা ধাপে ধাপে শিখব।

---

# 🧪 Practice 1

একটি function তৈরি করো:

```c
void welcome()
```

যেটা print করবে:

```text
Welcome to C Programming!
```

তারপর `main()` থেকে function-টি call করো।

---

# 🧪 Practice 2

একটি function:

```c
void printNumbers()
```

যেটা:

```text
1
2
3
4
5
```

print করবে।

Hint:

Function-এর ভিতরে `for` loop ব্যবহার করো।

---

# 🧪 Practice 3

এই তিনটি function তৈরি করো:

```c
void start()
void menu()
void exitMessage()
```

Output:

```text
Program Started
Main Menu
Program Ended
```

তারপর `main()` থেকে সঠিক order-এ call করো।

---

# 🔥 Mini Challenge

একটি function তৈরি করো:

```c
void multiplicationTable()
```

যেটা `5`-এর multiplication table print করবে:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
...
5 x 10 = 50
```

Function-এর ভিতরে loop ব্যবহার করবে।

---

# 🧠 আজকের Cheat Sheet

### Function definition

```c
void greet() {
    printf("Hello");
}
```

### Function call

```c
greet();
```

### Prototype

```c
void greet();
```

### Function-এর basic structure

```c
return_type function_name(parameters) {

    // body

}
```

### মনে রাখবে

```text
Function define করা ≠ Function execute করা
```

Execute করতে:

```c
functionName();
```

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ⏳ Parameters & arguments
25. ⏳ Return value
26. ⏳ Call by value
27. ⏳ Recursion
28. ⏳ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 24: Parameters & Arguments

এবার function-কে **data পাঠানো** শিখব।

যেমন:

```c
add(10, 20);
```

এবং বুঝব:

**parameter** আর **argument**-এর মধ্যে পার্থক্য কী।

---
# 🚀 Lesson 24 — Parameters & Arguments

আজ আমরা শিখব কীভাবে **function-এর মধ্যে বাইরে থেকে data পাঠানো যায়**।

আগের lesson-এ আমরা function বানিয়েছিলাম:

```c
void greet() {
    printf("Hello\n");
}
```

কিন্তু যদি আমরা চাই:

```text
greet("Rahim")
greet("Karim")
greet("Nadia")
```

তাহলে function-এর মধ্যে **parameter** ব্যবহার করতে হবে।

---

# 1. Parameter কী?

Parameter হলো function-এর definition-এ থাকা variable, যেটার মাধ্যমে function data গ্রহণ করে।

উদাহরণ:

```c
void greet(char name[]) {
    printf("Hello %s\n", name);
}
```

এখানে:

```c
char name[]
```

হলো **parameter**।

---

# 2. Argument কী?

Function call করার সময় যে actual value পাঠানো হয়, সেটা হলো **argument**।

```c
greet("Rahim");
```

এখানে:

```text
"Rahim" → argument
name    → parameter
```

সহজভাবে:

```text
Parameter = function যে জায়গায় data গ্রহণ করে
Argument  = function call করার সময় যে data পাঠাই
```

---

# 3. প্রথম Simple Example

```c
#include <stdio.h>

void greet(int age) {
    printf("Age = %d\n", age);
}

int main() {

    greet(15);

    return 0;
}
```

Output:

```text
Age = 15
```

এখানে:

```c
int age
```

= parameter

এবং:

```c
greet(15);
```

এর `15`

= argument।

---

# 4. একাধিক Parameter

একটি function একাধিক parameter নিতে পারে।

```c
#include <stdio.h>

void add(int a, int b) {
    printf("Sum = %d\n", a + b);
}

int main() {

    add(10, 20);

    return 0;
}
```

Output:

```text
Sum = 30
```

এখানে:

```text
Parameters:
a
b

Arguments:
10
20
```

---

# 5. Parameter Matching

খুব গুরুত্বপূর্ণ:

```c
add(10, 20);
```

এর ক্ষেত্রে:

```text
a = 10
b = 20
```

অর্থাৎ order গুরুত্বপূর্ণ।

```c
add(10, 20);
```

এবং:

```c
add(20, 10);
```

দুটো আলাদা argument order।

যদিও addition-এর ক্ষেত্রে result একই হবে:

```text
30
```

কিন্তু subtraction করলে পার্থক্য হবে।

---

# 6. Subtraction Example

```c
#include <stdio.h>

void subtract(int a, int b) {
    printf("Result = %d\n", a - b);
}

int main() {

    subtract(20, 5);
    subtract(5, 20);

    return 0;
}
```

Output:

```text
Result = 15
Result = -15
```

তাই:

```text
a এবং b-এর position গুরুত্বপূর্ণ।
```

---

# 7. Variable পাঠানো

শুধু direct value নয়, variable-ও argument হিসেবে পাঠানো যায়।

```c
#include <stdio.h>

void square(int n) {
    printf("Square = %d\n", n * n);
}

int main() {

    int number = 7;

    square(number);

    return 0;
}
```

Output:

```text
Square = 49
```

এখানে:

```text
number = 7
      ↓
square(number)
      ↓
n = 7
```

---

# 8. Expression-ও পাঠানো যায়

```c
#include <stdio.h>

void show(int n) {
    printf("%d\n", n);
}

int main() {

    show(10 + 5);
    show(20 * 2);

    return 0;
}
```

Output:

```text
15
40
```

Argument হিসেবে expression evaluate হয়ে value পাঠানো হয়েছে।

---

# 9. Different Data Types

Parameter-এর type argument-এর expected type-এর সঙ্গে compatible হওয়া উচিত।

```c
#include <stdio.h>

void show(double number) {
    printf("%.2f\n", number);
}

int main() {

    show(10.5);

    return 0;
}
```

Output:

```text
10.50
```

---

# 10. Multiple Data Types

একটি function-এ বিভিন্ন type-এর parameter থাকতে পারে।

```c
#include <stdio.h>

void student(char name[], int age, float marks) {
    printf("Name: %s\n", name);
    printf("Age: %d\n", age);
    printf("Marks: %.2f\n", marks);
}

int main() {

    student("Rahim", 16, 85.5);

    return 0;
}
```

Output:

```text
Name: Rahim
Age: 16
Marks: 85.50
```

এখানে:

```text
name  → string
age   → int
marks → float
```

---

# 11. Function Call-এর সময় কী হয়?

এই code:

```c
void add(int a, int b) {
    printf("%d\n", a + b);
}

add(10, 20);
```

ভাবতে পারো:

```text
add(10, 20)
    ↓
a = 10
b = 20
    ↓
a + b
    ↓
30
```

---

# 12. Function বারবার Different Data নিতে পারে

এটাই parameter-এর বড় সুবিধা।

```c
#include <stdio.h>

void square(int n) {
    printf("Square of %d = %d\n", n, n * n);
}

int main() {

    square(2);
    square(5);
    square(10);
    square(20);

    return 0;
}
```

Output:

```text
Square of 2 = 4
Square of 5 = 25
Square of 10 = 100
Square of 20 = 400
```

একটি function, কিন্তু বিভিন্ন data।

---

# 13. Parameter ছাড়া বনাম Parameter সহ

### Parameter ছাড়া

```c
void square() {
    printf("25\n");
}
```

এটা সবসময় একই কাজ করবে।

### Parameter সহ

```c
void square(int n) {
    printf("%d\n", n * n);
}
```

এখন:

```c
square(5);
square(10);
square(20);
```

সব different result দিতে পারে।

---

# 14. User Input + Function

এটা খুব useful pattern।

```c
#include <stdio.h>

void checkEvenOdd(int n) {

    if (n % 2 == 0) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }
}

int main() {

    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    checkEvenOdd(number);

    return 0;
}
```

যদি input:

```text
17
```

তাহলে:

```text
Odd
```

Flow:

```text
User input
    ↓
number
    ↓
checkEvenOdd(number)
    ↓
n = number
    ↓
check
```

---

# 15. Function + Loop + Parameter

একটি number-এর multiplication table:

```c
#include <stdio.h>

void table(int n) {

    for (int i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", n, i, n * i);
    }
}

int main() {

    table(5);

    return 0;
}
```

Output:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
...
5 x 10 = 50
```

এখন:

```c
table(7);
```

করলে 7-এর table হবে।

---

# 16. Multiple Parameters + Calculation

```c
#include <stdio.h>

void rectangle(int length, int width) {

    int area = length * width;

    printf("Area = %d\n", area);
}

int main() {

    rectangle(10, 5);

    return 0;
}
```

Output:

```text
Area = 50
```

---

# 17. Parameter-এর নাম Function-এর ভিতরের Variable

এই code:

```c
void add(int a, int b) {
    printf("%d\n", a + b);
}
```

এখানে `a` এবং `b` function-এর ভিতরে variable-এর মতো কাজ করে।

তুমি তাদের নিয়ে:

```c
a + b
a * b
a - b
a / b
```

ইত্যাদি করতে পারো।

---

# 18. Parameter-এর Scope

```c
void show(int n) {

    printf("%d\n", n);
}
```

`n` শুধু এই function-এর ভিতরে ব্যবহার করা যায়।

`main()`-এ সরাসরি:

```c
printf("%d", n);
```

লিখলে কাজ করবে না।

Scope নিয়ে আমরা Lesson 28-এ বিস্তারিত শিখব।

---

# 19. Parameter-এর সংখ্যা

### Zero parameter

```c
void hello()
```

### One parameter

```c
void show(int n)
```

### Two parameters

```c
void add(int a, int b)
```

### Three parameters

```c
void student(char name[], int age, float marks)
```

প্রয়োজন অনুযায়ী parameter নেওয়া যায়।

---

# 20. Function Prototype with Parameters

Function যদি `main()`-এর পরে থাকে:

```c
#include <stdio.h>

void add(int a, int b);

int main() {

    add(10, 20);

    return 0;
}

void add(int a, int b) {

    printf("Sum = %d\n", a + b);
}
```

উপরে:

```c
void add(int a, int b);
```

হলো prototype।

---

# 21. Parameter এবং Argument — Final Comparison

এই code দেখো:

```c
void multiply(int x, int y) {
    printf("%d\n", x * y);
}

int main() {

    multiply(4, 5);

    return 0;
}
```

### Parameters:

```text
x
y
```

### Arguments:

```text
4
5
```

মনে রাখো:

> **Definition-এর ভিতরে → parameter**  
> **Call-এর ভিতরে → argument**

---

# 22. একটি গুরুত্বপূর্ণ Example

```c
#include <stdio.h>

void compare(int a, int b) {

    if (a > b) {
        printf("%d is greater\n", a);
    } else if (b > a) {
        printf("%d is greater\n", b);
    } else {
        printf("Both are equal\n");
    }
}

int main() {

    compare(10, 20);
    compare(50, 30);
    compare(7, 7);

    return 0;
}
```

Output:

```text
20 is greater
50 is greater
Both are equal
```

একটি function বিভিন্ন input নিয়ে বিভিন্ন result তৈরি করছে।

---

# 🧪 Practice 1

একটি function তৈরি করো:

```c
void printSquare(int n)
```

যেটা `n`-এর square print করবে।

Example:

```c
printSquare(6);
```

Output:

```text
36
```

---

# 🧪 Practice 2

Function:

```c
void findMaximum(int a, int b)
```

দুটি সংখ্যার মধ্যে বড় সংখ্যাটি print করবে।

Example:

```c
findMaximum(25, 17);
```

Output:

```text
25
```

---

# 🧪 Practice 3

Function:

```c
void printRange(int start, int end)
```

`start` থেকে `end` পর্যন্ত number print করবে।

Example:

```c
printRange(5, 10);
```

Output:

```text
5
6
7
8
9
10
```

---

# 🔥 Mini Challenge

একটি function তৈরি করো:

```c
void calculate(int a, int b)
```

যেটা print করবে:

```text
Sum = ...
Difference = ...
Product = ...
```

Example:

```c
calculate(10, 5);
```

Expected:

```text
Sum = 15
Difference = 5
Product = 50
```

---

# 🔥 Mini Challenge 2

Function:

```c
void multiplicationTable(int n)
```

তারপর `main()` থেকে user-এর input নিয়ে function-এ পাঠাও।

Expected flow:

```text
Enter number: 7

7 x 1 = 7
7 x 2 = 14
...
7 x 10 = 70
```

---

# 🧠 আজকের Cheat Sheet

### Parameter

```c
void add(int a, int b)
```

`a`, `b` = parameters

### Argument

```c
add(10, 20);
```

`10`, `20` = arguments

### Variable পাঠানো

```c
int x = 10;

add(x, 20);
```

### Multiple parameters

```c
void student(char name[], int age, float marks)
```

### মূল নিয়ম

```text
Function definition → Parameter
Function call       → Argument
```

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ⏳ Return value
26. ⏳ Call by value
27. ⏳ Recursion
28. ⏳ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 25: Return Value

এবার আমরা function থেকে **result ফিরিয়ে আনা** শিখব।

যেমন:

```c
int result = add(10, 20);
```

এখানে function শুধু screen-এ print করবে না—**একটি value return করবে**, যেটা পরে অন্য calculation-এ ব্যবহার করা যাবে।

---
# 🚀 Lesson 25 — Return Value

আজ আমরা শিখব **function থেকে value ফেরত আনা**।

এটা খুব গুরুত্বপূর্ণ, কারণ function শুধু `printf()` করে result দেখানোর জন্য নয়—function একটি **result তৈরি করে caller-এর কাছে ফেরতও দিতে পারে**।

---

# 1. `return` কী?

`return` দিয়ে function থেকে কোনো value ফেরত পাঠানো যায়।

উদাহরণ:

```c
int add(int a, int b) {
    return a + b;
}
```

এখানে:

```c
return a + b;
```

মানে:

> `a + b`-এর result function থেকে ফেরত পাঠাও।

---

# 2. প্রথম Example

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {

    int result = add(10, 20);

    printf("Result = %d\n", result);

    return 0;
}
```

Output:

```text
Result = 30
```

Flow:

```text
add(10, 20)
     ↓
a = 10
b = 20
     ↓
a + b
     ↓
30
     ↓
return 30
     ↓
result = 30
```

---

# 3. `void` বনাম `return`

এটা খুব গুরুত্বপূর্ণ।

### `void` function

```c
void add(int a, int b) {
    printf("%d\n", a + b);
}
```

এটি result **print** করছে।

### `int` function

```c
int add(int a, int b) {
    return a + b;
}
```

এটি result **return** করছে।

তারপর:

```c
int result = add(10, 20);
```

result অন্য জায়গায় ব্যবহার করা যাবে।

---

# 4. Print বনাম Return

ধরো:

```c
void square(int n) {
    printf("%d\n", n * n);
}
```

এটা screen-এ result দেখায়।

কিন্তু:

```c
int square(int n) {
    return n * n;
}
```

এখন আমরা করতে পারি:

```c
int result = square(5);
```

অথবা:

```c
printf("%d\n", square(5));
```

অথবা:

```c
int x = square(5) + 10;
```

এটাই `return`-এর শক্তি।

---

# 5. Return Type কী?

Function declaration-এর প্রথম অংশ বলে দেয় function কী ধরনের value return করবে।

```c
int add(...)
```

মানে integer return করবে।

```c
float average(...)
```

মানে float return করবে।

```c
double calculate(...)
```

মানে double return করবে।

```c
char getGrade(...)
```

মানে character return করবে।

---

# 6. `int` Return

```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int main() {

    int result = square(7);

    printf("Square = %d\n", result);

    return 0;
}
```

Output:

```text
Square = 49
```

---

# 7. `float` Return

```c
#include <stdio.h>

float half(float n) {
    return n / 2;
}

int main() {

    float result = half(10);

    printf("%.2f\n", result);

    return 0;
}
```

Output:

```text
5.00
```

---

# 8. `double` Return

```c
#include <stdio.h>

double calculate(double a, double b) {
    return a / b;
}

int main() {

    double result = calculate(10.0, 3.0);

    printf("%.2f\n", result);

    return 0;
}
```

Output:

```text
3.33
```

---

# 9. `char` Return

একটি function character-ও return করতে পারে।

```c
#include <stdio.h>

char getGrade() {
    return 'A';
}

int main() {

    char grade = getGrade();

    printf("Grade = %c\n", grade);

    return 0;
}
```

Output:

```text
Grade = A
```

---

# 10. Function-এর Return Value Directly ব্যবহার

সবসময় variable-এ রাখতে হবে এমন নয়।

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {

    printf("%d\n", add(10, 20));

    return 0;
}
```

Output:

```text
30
```

---

# 11. Return Value দিয়ে Calculation

এটাই সবচেয়ে useful।

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {

    int result = add(10, 20) * 2;

    printf("%d\n", result);

    return 0;
}
```

Flow:

```text
add(10, 20)
     ↓
30
     ↓
30 × 2
     ↓
60
```

Output:

```text
60
```

---

# 12. Function-এর Return Value অন্য Function-এ পাঠানো

এটা একটু advanced কিন্তু খুব useful।

```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

void show(int n) {
    printf("Result = %d\n", n);
}

int main() {

    show(square(5));

    return 0;
}
```

Flow:

```text
square(5)
   ↓
25
   ↓
show(25)
   ↓
Result = 25
```

---

# 13. `return` Function Execution বন্ধ করে

`return` শুধু value ফেরত দেয় না, function-এর execution-ও শেষ করে।

```c
#include <stdio.h>

int test() {

    printf("Hello\n");

    return 10;

    printf("World\n");
}

int main() {

    int x = test();

    printf("%d\n", x);

    return 0;
}
```

Output:

```text
Hello
10
```

`return 10;`-এর পর:

```c
printf("World\n");
```

execute হবে না।

---

# 14. Conditional Return

একটি function-এর মধ্যে condition অনুযায়ী different value return করা যায়।

```c
#include <stdio.h>

int maximum(int a, int b) {

    if (a > b) {
        return a;
    }

    return b;
}

int main() {

    int result = maximum(10, 25);

    printf("Maximum = %d\n", result);

    return 0;
}
```

Output:

```text
Maximum = 25
```

---

# 15. Multiple `return`

একটি function-এ একাধিক `return` থাকতে পারে।

```c
int absolute(int n) {

    if (n < 0) {
        return -n;
    }

    return n;
}
```

যদি:

```text
absolute(-10)
```

হয়:

```text
10
```

আর:

```text
absolute(10)
```

হলে:

```text
10
```

---

# 16. Boolean-style Function

C-তে condition check করে `1` বা `0` return করা যায়।

```c
#include <stdio.h>

int isEven(int n) {

    if (n % 2 == 0) {
        return 1;
    }

    return 0;
}

int main() {

    if (isEven(10)) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }

    return 0;
}
```

Output:

```text
Even
```

এখানে function:

```text
Even → 1
Odd  → 0
```

return করছে।

---

# 17. আরও Short Version

উপরের function এভাবে লেখা যায়:

```c
int isEven(int n) {
    return n % 2 == 0;
}
```

কারণ C-তে comparison expression:

```c
n % 2 == 0
```

সত্য হলে `1`, মিথ্যা হলে `0` দেয়।

---

# 18. User Input + Return Value

এখন function-এর result ব্যবহার করে program বানাই।

```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int main() {

    int number;

    printf("Enter number: ");
    scanf("%d", &number);

    int result = square(number);

    printf("Square = %d\n", result);

    return 0;
}
```

Input:

```text
6
```

Output:

```text
Square = 36
```

---

# 19. Calculator Example

একটি function দিয়ে addition:

```c
int add(int a, int b) {
    return a + b;
}
```

Subtraction:

```c
int subtract(int a, int b) {
    return a - b;
}
```

Multiplication:

```c
int multiply(int a, int b) {
    return a * b;
}
```

সম্পূর্ণ program:

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

int main() {

    printf("Add = %d\n", add(10, 5));
    printf("Subtract = %d\n", subtract(10, 5));
    printf("Multiply = %d\n", multiply(10, 5));

    return 0;
}
```

Output:

```text
Add = 15
Subtract = 5
Multiply = 50
```

---

# 20. `return` Type অবশ্যই Match করা উচিত

যদি function:

```c
int add(int a, int b)
```

হয়, তাহলে integer-compatible value return করা উচিত:

```c
return a + b;
```

ভুল ধরনের return নিয়ে compiler warning বা unexpected behavior হতে পারে।

---

# 21. `void` Function-এ `return`

`void` function কোনো value return করে না।

তবে শুধু function থেকে বের হতে:

```c
return;
```

ব্যবহার করা যায়।

উদাহরণ:

```c
void check(int n) {

    if (n < 0) {
        return;
    }

    printf("%d\n", n);
}
```

`n < 0` হলে function সেখানেই শেষ।

---

# 22. একটি Function থেকে একটি Value

Beginner level-এ এই ধারণাটা মনে রাখো:

```c
int add(int a, int b) {
    return a + b;
}
```

একটি function call:

```c
add(10, 20)
```

একটি result দেয়:

```text
30
```

তারপর সেই result তুমি যেখানে দরকার ব্যবহার করতে পারো।

---

# 23. Function Composition

এখন একটু interesting:

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int square(int n) {
    return n * n;
}

int main() {

    int result = square(add(2, 3));

    printf("%d\n", result);

    return 0;
}
```

Flow:

```text
add(2, 3)
    ↓
5
    ↓
square(5)
    ↓
25
```

Output:

```text
25
```

এটা বড় program design-এর foundation।

---

# 24. Return Value দিয়ে Condition

```c
#include <stdio.h>

int isPositive(int n) {
    return n > 0;
}

int main() {

    int number;

    scanf("%d", &number);

    if (isPositive(number)) {
        printf("Positive\n");
    } else {
        printf("Not positive\n");
    }

    return 0;
}
```

Function result সরাসরি `if`-এর condition হিসেবে ব্যবহার করা হয়েছে।

---

# 🧪 Practice 1

Function তৈরি করো:

```c
int cube(int n)
```

যেটা `n`-এর cube return করবে।

Example:

```c
cube(4)
```

Output/result:

```text
64
```

---

# 🧪 Practice 2

Function:

```c
int maximum(int a, int b)
```

দুটি সংখ্যার বড়টি return করবে।

তারপর:

```c
int result = maximum(15, 25);
```

দিয়ে result print করো।

---

# 🧪 Practice 3

Function:

```c
int isOdd(int n)
```

Odd হলে `1`, even হলে `0` return করবে।

তারপর `if` ব্যবহার করে:

```text
Odd
```

অথবা:

```text
Even
```

print করো।

---

# 🔥 Mini Challenge

একটি calculator তৈরি করো যেখানে চারটি function থাকবে:

```c
int add(int a, int b);
int subtract(int a, int b);
int multiply(int a, int b);
int divide(int a, int b);
```

`main()` থেকে user-এর দুটি number input নিয়ে চারটি result বের করো।

**Note:** integer division ব্যবহার করলে `10 / 3` এর result `3` হবে। Decimal result চাইলে পরে `float`/`double` ব্যবহার করবে।

---

# 🔥 Mini Challenge 2 — Factorial

Function:

```c
int factorial(int n)
```

যেটা `n!` return করবে।

Example:

```text
factorial(5)
```

Result:

```text
120
```

Hint:

```text
5 × 4 × 3 × 2 × 1 = 120
```

Loop দিয়ে এখনই solve করার চেষ্টা করো। Recursion আমরা Lesson 27-এ আলাদাভাবে শিখব।

---

# 🧠 আজকের Cheat Sheet

### Return value

```c
int add(int a, int b) {
    return a + b;
}
```

### Result store

```c
int result = add(10, 20);
```

### Direct use

```c
printf("%d", add(10, 20));
```

### Condition

```c
if (isEven(n)) {
    ...
}
```

### Function execution stop

```c
return;
```

### Value + execution stop

```c
return value;
```

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ✅ Return value
26. ⏳ Call by value
27. ⏳ Recursion
28. ⏳ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 26: Call by Value

এবার দেখব function-এ variable পাঠালে **original variable-এর কী হয়**।

বিশেষ করে এই প্রশ্নের উত্তর:

```c
int x = 10;

change(x);
```

`change()`-এর ভিতরে `x` পরিবর্তন করলে কি `main()`-এর আসল `x`-ও পরিবর্তন হবে?

এটাই **Call by Value** বোঝার মূল বিষয়।

----
# 🚀 Lesson 26 — Call by Value

আজ আমরা C-এর খুব গুরুত্বপূর্ণ একটি concept শিখব:

> **Call by Value**

এটা বুঝতে পারলে পরে **Pointers** শেখা অনেক সহজ হবে।

---

# 1. Call by Value কী?

যখন কোনো variable function-এ argument হিসেবে পাঠানো হয়, C সাধারণত সেই variable-এর **value-এর একটি copy** function-এ পাঠায়।

অর্থাৎ:

```text
Original variable
      ↓
    value
      ↓
    copy
      ↓
Function parameter
```

তাই function-এর parameter পরিবর্তন করলে সাধারণত **original variable পরিবর্তন হয় না**।

---

# 2. প্রথম Example

```c
#include <stdio.h>

void change(int x) {
    x = 100;
}

int main() {

    int number = 10;

    change(number);

    printf("%d\n", number);

    return 0;
}
```

Output:

```text
10
```

অনেকে শুরুতে ভাবতে পারে output `100` হবে।

কিন্তু তা হবে না।

---

# 3. কী ঘটেছে?

শুরুতে:

```text
number = 10
```

তারপর:

```c
change(number);
```

C এখানে `number`-এর value `10`-এর একটি copy function-এ পাঠায়।

তাই function-এর ভিতরে:

```text
number → 10
           ↓
        copy → x = 10
```

তারপর:

```c
x = 100;
```

হলে:

```text
number = 10
x      = 100
```

Function শেষ হলে `x` চলে যায়।

তাই `number` এখনও:

```text
10
```

---

# 4. Visualize করো

```text
main()

number
┌─────────┐
│   10    │
└─────────┘
     │
     │ copy value
     ↓
change()

x
┌─────────┐
│   10    │
└─────────┘

x = 100

x
┌─────────┐
│   100   │
└─────────┘

number
┌─────────┐
│   10    │
└─────────┘
```

দুটো আলাদা variable।

---

# 5. আরও একটি Example

```c
#include <stdio.h>

void increase(int x) {
    x++;
}

int main() {

    int n = 5;

    increase(n);

    printf("%d\n", n);

    return 0;
}
```

Output:

```text
5
```

`x` হয়েছে `6`, কিন্তু `n` হয়েছে না।

---

# 6. `x++` কেন original পরিবর্তন করে না?

কারণ:

```c
increase(n);
```

এখানে:

```text
n-এর value → copy → x
```

Function-এর ভিতরে:

```c
x++;
```

শুধু `x` পরিবর্তন করছে।

```text
Before:

n = 5
x = 5

After x++:

n = 5
x = 6
```

---

# 7. দুইটা Variable Example

```c
#include <stdio.h>

void change(int a, int b) {

    a = 100;
    b = 200;
}

int main() {

    int x = 10;
    int y = 20;

    change(x, y);

    printf("x = %d\n", x);
    printf("y = %d\n", y);

    return 0;
}
```

Output:

```text
x = 10
y = 20
```

কারণ:

```text
x → copy → a
y → copy → b
```

---

# 8. Function Result দিয়ে Original পরিবর্তন করতে পারি

একটি গুরুত্বপূর্ণ technique:

```c
#include <stdio.h>

int increase(int x) {
    return x + 1;
}

int main() {

    int n = 5;

    n = increase(n);

    printf("%d\n", n);

    return 0;
}
```

Output:

```text
6
```

এখানে কী হলো?

```text
n = 5
 ↓
increase(5)
 ↓
6
 ↓
n = 6
```

Function সরাসরি original variable পরিবর্তন করেনি।

বরং **new value return করেছে**, তারপর আমরা সেই value দিয়ে `n` update করেছি।

---

# 9. এই Pattern খুব গুরুত্বপূর্ণ

```c
x = function(x);
```

উদাহরণ:

```c
x = square(x);
```

অথবা:

```c
age = increase(age);
```

অথবা:

```c
number = absolute(number);
```

---

# 10. Call by Value দিয়ে Swap কেন কাজ করে না?

ধরো আমরা দুইটি variable swap করতে চাই:

```text
a = 10
b = 20
```

আমরা লিখলাম:

```c
#include <stdio.h>

void swap(int a, int b) {

    int temp = a;
    a = b;
    b = temp;
}

int main() {

    int x = 10;
    int y = 20;

    swap(x, y);

    printf("x = %d\n", x);
    printf("y = %d\n", y);

    return 0;
}
```

Output:

```text
x = 10
y = 20
```

কেন?

Function-এর ভিতরে শুধু copy swap হয়েছে:

```text
Before:

x = 10
y = 20

a = 10
b = 20
```

Function-এর ভিতরে:

```text
a = 20
b = 10
```

কিন্তু:

```text
x = 10
y = 20
```

অপরিবর্তিত।

---

# 11. তাহলে Function-এর ভিতরে Swap হয়েছিল?

হ্যাঁ।

Function-এর ভিতরে:

```text
a = 10
b = 20

     ↓ swap

a = 20
b = 10
```

কিন্তু `a` এবং `b` হলো copies।

তাই বাইরে:

```text
x = 10
y = 20
```

থেকেছে।

---

# 12. Call by Value-এর মূল ধারণা

এই diagram মনে রাখো:

```text
main()

x = 10
 │
 │ value copied
 ↓
function()

a = 10

a = 100

Function শেষ

x = 10
```

### Golden Rule ⭐

> **Call by Value → value-এর copy পাঠানো হয়।**

---

# 13. Function-এর Parameter পরিবর্তন

এই code:

```c
void test(int x) {
    x = 50;
}
```

এখানে `x` function-এর local parameter।

যদি:

```c
int number = 10;

test(number);
```

হয়, তাহলে:

```text
number = 10
x = 10
```

`x` পরিবর্তন করলে:

```text
number = 10
x = 50
```

---

# 14. Strings-এর ক্ষেত্রে একটু সাবধান ⚠️

C-তে arrays এবং pointers-এর কারণে বিষয়টা পরে আরও nuanced হবে।

এখন শুধু মনে রাখো:

```text
int
float
char
double
```

এর মতো সাধারণ scalar value function-এ পাঠালে value copy হয়।

Arrays/pointers আমরা **Phase 6 — Pointers**-এ বিস্তারিত শিখব।

---

# 15. Call by Value কেন Useful?

এটা অনেক নিরাপদ হতে পারে, কারণ function-এর parameter পরিবর্তন করলেও caller-এর variable সরাসরি পরিবর্তিত হয় না।

উদাহরণ:

```c
int calculate(int x) {
    x = x * 2;
    return x;
}
```

তুমি করতে পারো:

```c
int n = 10;

int result = calculate(n);
```

তখন:

```text
n      = 10
result = 20
```

---

# 16. Real Example — Discount

ধরো:

```c
#include <stdio.h>

float discount(float price) {

    price = price * 0.9;

    return price;
}

int main() {

    float price = 1000;

    float finalPrice = discount(price);

    printf("Original = %.2f\n", price);
    printf("Final = %.2f\n", finalPrice);

    return 0;
}
```

Output:

```text
Original = 1000.00
Final = 900.00
```

এখানে function-এর ভিতরে `price` পরিবর্তিত হলেও `main()`-এর `price` unchanged।

---

# 17. Call by Value-এর Flow

```text
main()
  │
  │ price = 1000
  ↓
discount(price)
  │
  │ copy
  ↓
parameter = 1000
  │
  │ × 0.9
  ↓
900
  │
  │ return
  ↓
finalPrice = 900

Original price = 1000
```

---

# 18. Return + Call by Value একসাথে

এটি খুব common pattern:

```c
#include <stdio.h>

int doubleValue(int x) {
    return x * 2;
}

int main() {

    int n = 10;

    int result = doubleValue(n);

    printf("n = %d\n", n);
    printf("result = %d\n", result);

    return 0;
}
```

Output:

```text
n = 10
result = 20
```

---

# 19. Common Beginner Mistake ❌

অনেকে ভাবতে পারে:

```c
void change(int x) {
    x = 100;
}

int main() {

    int x = 10;

    change(x);

    printf("%d", x);
}
```

Output:

```text
100
```

কিন্তু output হবে:

```text
10
```

কারণ একই নাম `x` হলেও এগুলো একই variable নয়।

```text
main()          function

x = 10          x = 10
                  ↓
                x = 100
```

দুটি আলাদা scope/variable context।

---

# 20. Name একই হলেও Variable একই নয়

```c
void test(int x) {
    x = 50;
}

int main() {

    int x = 10;

    test(x);

    printf("%d", x);
}
```

এখানে দুটো `x` আছে:

```text
main-এর x
function-এর x
```

Function-এর `x` হলো parameter-এর local copy।

---

# 🧪 Practice 1

এই function-এর output কী হবে?

```c
#include <stdio.h>

void change(int x) {
    x = 100;
}

int main() {

    int x = 20;

    change(x);

    printf("%d\n", x);

    return 0;
}
```

**নিজে আগে predict করো।**

---

# 🧪 Practice 2

এই program complete করো:

```c
int increase(int n) {
    // এখানে n-এর value 1 বাড়িয়ে return করো
}

int main() {

    int x = 10;

    x = increase(x);

    printf("%d\n", x);

    return 0;
}
```

Expected output:

```text
11
```

---

# 🔥 Challenge — Swap

প্রথমে এই function লিখে দেখো:

```c
void swap(int a, int b) {

    // swap a and b

}
```

তারপর:

```c
int x = 10;
int y = 20;

swap(x, y);
```

এর পর `x` এবং `y` কেন swap হচ্ছে না—নিজে explain করার চেষ্টা করো।

**এটাই Pointers শেখার জন্য সবচেয়ে গুরুত্বপূর্ণ motivation।**

---

# 🧠 আজকের Cheat Sheet

### Call by Value

```c
function(x);
```

সাধারণ value parameter-এর ক্ষেত্রে:

```text
x-এর value
   ↓
copy
   ↓
parameter
```

### Function-এর ভিতরে:

```c
parameter = newValue;
```

করলে caller-এর original variable সাধারণত পরিবর্তিত হয় না।

### Original update করতে return ব্যবহার করা যায়:

```c
x = function(x);
```

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ✅ Return value
26. ✅ Call by value
27. ⏳ Recursion
28. ⏳ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 27: Recursion

এবার C-এর সবচেয়ে interesting concepts-এর একটি:

```c
int factorial(int n) {
    return n * factorial(n - 1);
}
```

একটি function **নিজেকেই call করবে**!

আমরা শিখব recursion কীভাবে কাজ করে, **base case** কেন দরকার, এবং recursion দিয়ে factorial, sum, countdown ইত্যাদি কীভাবে solve করা যায়।

-----

# 🚀 Lesson 27 — Recursion

আজ আমরা C-এর সবচেয়ে interesting conceptগুলোর একটি শিখব:

> **একটি function যখন নিজেকেই call করে, তাকে Recursion বলে।**

প্রথমে একটু অদ্ভুত মনে হবে 😄, কিন্তু কয়েকটা example দেখলে ব্যাপারটা পরিষ্কার হয়ে যাবে।

---

# 1. Recursion কী?

সাধারণ function:

```c
void hello() {
    printf("Hello\n");
}
```

এখানে function অন্য code execute করছে।

Recursion-এ:

```c
void test() {
    test();
}
```

`test()` নিজেকেই call করছে।

```text
test()
  ↓
test()
  ↓
test()
  ↓
test()
  ↓
...
```

এভাবে চলতেই থাকবে—যদি আমরা থামার condition না দিই।

---

# 2. Base Case কেন দরকার?

Recursion-এ অবশ্যই একটি **base case** থাকতে হবে।

Base case হলো:

> যে condition পূরণ হলে recursion আর চলবে না।

উদাহরণ:

```c
void countdown(int n) {

    if (n == 0) {
        return;
    }

    printf("%d\n", n);

    countdown(n - 1);
}
```

এখানে:

```c
if (n == 0)
```

হলো **base case**।

---

# 3. প্রথম Recursion Example — Countdown

```c
#include <stdio.h>

void countdown(int n) {

    if (n == 0) {
        return;
    }

    printf("%d\n", n);

    countdown(n - 1);
}

int main() {

    countdown(5);

    return 0;
}
```

Output:

```text
5
4
3
2
1
```

---

# 4. এটা কীভাবে কাজ করছে?

`countdown(5)`:

```text
countdown(5)
    ↓
print 5
    ↓
countdown(4)
    ↓
print 4
    ↓
countdown(3)
    ↓
print 3
    ↓
countdown(2)
    ↓
print 2
    ↓
countdown(1)
    ↓
print 1
    ↓
countdown(0)
    ↓
return
```

---

# 5. Recursion-এর 2টি অংশ ⭐

প্রায় সব recursion problem-এ এই দুইটি জিনিস খুঁজবে:

### 1. Base Case

কখন recursion থামবে?

```c
if (n == 0) {
    return;
}
```

### 2. Recursive Case

কোথায় function নিজেকে call করছে?

```c
countdown(n - 1);
```

---

# 6. Base Case না থাকলে কী হবে?

এই code:

```c
void test(int n) {
    printf("%d\n", n);
    test(n - 1);
}
```

কখনো stop করবে না।

এটা ভুল recursion।

কারণ:

```text
No base case
     ↓
function keeps calling itself
     ↓
eventually stack overflow
```

তাই:

> **Recursion = Base Case + Recursive Call**

---

# 7. Recursion দিয়ে 1 থেকে N

এবার উল্টোভাবে:

```text
1
2
3
4
5
```

Code:

```c
#include <stdio.h>

void printNumbers(int n) {

    if (n == 0) {
        return;
    }

    printNumbers(n - 1);

    printf("%d\n", n);
}

int main() {

    printNumbers(5);

    return 0;
}
```

Output:

```text
1
2
3
4
5
```

---

# 8. এখানে গুরুত্বপূর্ণ পার্থক্য

আগের example:

```c
printf("%d\n", n);
countdown(n - 1);
```

এখানে print **recursive call-এর আগে**।

কিন্তু এবার:

```c
printNumbers(n - 1);
printf("%d\n", n);
```

print **recursive call-এর পরে**।

এতে output order বদলে যায়।

---

# 9. Recursion-এর Call Stack

এখানে C একটি **call stack** ব্যবহার করে।

ধরো:

```c
printNumbers(3);
```

প্রথমে:

```text
printNumbers(3)
```

তারপর:

```text
printNumbers(3)
      ↓
printNumbers(2)
      ↓
printNumbers(1)
      ↓
printNumbers(0)
```

`0`-এ গিয়ে recursion stop করে।

তারপর functionগুলো একে একে ফিরে আসে:

```text
printNumbers(0) → return
printNumbers(1) → print 1 → return
printNumbers(2) → print 2 → return
printNumbers(3) → print 3 → return
```

তাই output:

```text
1
2
3
```

---

# 10. Factorial — সবচেয়ে গুরুত্বপূর্ণ Example ⭐

আমরা জানি:

```text
5! = 5 × 4 × 3 × 2 × 1
```

এবং:

```text
5! = 5 × 4!
4! = 4 × 3!
3! = 3 × 2!
```

তাই mathematical relationship:

```text
n! = n × (n - 1)!
```

এটাই recursion-এর জন্য perfect।

---

# 11. Recursive Factorial

```c
#include <stdio.h>

int factorial(int n) {

    if (n == 0) {
        return 1;
    }

    return n * factorial(n - 1);
}

int main() {

    int result = factorial(5);

    printf("%d\n", result);

    return 0;
}
```

Output:

```text
120
```

---

# 12. Factorial কীভাবে কাজ করে?

`factorial(5)`:

```text
factorial(5)
= 5 × factorial(4)

= 5 × 4 × factorial(3)

= 5 × 4 × 3 × factorial(2)

= 5 × 4 × 3 × 2 × factorial(1)

= 5 × 4 × 3 × 2 × 1 × factorial(0)
```

Base case:

```c
factorial(0) = 1
```

তাই:

```text
5 × 4 × 3 × 2 × 1
= 120
```

---

# 13. কেন Base Case `return 1`?

কারণ:

```text
0! = 1
```

তাই:

```c
if (n == 0) {
    return 1;
}
```

Recursion-এর শেষ value হলো `1`।

---

# 14. Factorial-এর Stack Flow

```text
factorial(5)
    ↓
factorial(4)
    ↓
factorial(3)
    ↓
factorial(2)
    ↓
factorial(1)
    ↓
factorial(0)
```

তারপর result ফিরে আসে:

```text
factorial(0) = 1
       ↑
factorial(1) = 1
       ↑
factorial(2) = 2
       ↑
factorial(3) = 6
       ↑
factorial(4) = 24
       ↑
factorial(5) = 120
```

---

# 15. Recursion বনাম Loop

Factorial loop দিয়েও করা যায়:

```c
int factorial(int n) {

    int result = 1;

    for (int i = 1; i <= n; i++) {
        result *= i;
    }

    return result;
}
```

Recursion:

```c
int factorial(int n) {

    if (n == 0) {
        return 1;
    }

    return n * factorial(n - 1);
}
```

দুটোই কাজ করে।

---

# 16. কখন Recursion ব্যবহার করব?

সব problem recursion দিয়ে solve করতে হবে—এমন নয়।

Recursion বিশেষভাবে useful যখন problem নিজেই ছোট version-এ ভেঙে যায়।

যেমন:

```text
Factorial
Tree traversal
Directory traversal
Divide and conquer
Graph algorithms
Backtracking
```

Data Structures phase-এ recursion আরও useful হবে।

---

# 17. Sum of Numbers

এবার:

```text
1 + 2 + 3 + 4 + 5 = 15
```

Recursive relationship:

```text
sum(n) = n + sum(n - 1)
```

Code:

```c
#include <stdio.h>

int sum(int n) {

    if (n == 0) {
        return 0;
    }

    return n + sum(n - 1);
}

int main() {

    printf("%d\n", sum(5));

    return 0;
}
```

Output:

```text
15
```

---

# 18. Sum-এর Flow

```text
sum(5)
= 5 + sum(4)
= 5 + 4 + sum(3)
= 5 + 4 + 3 + sum(2)
= 5 + 4 + 3 + 2 + sum(1)
= 5 + 4 + 3 + 2 + 1 + sum(0)
```

Base:

```text
sum(0) = 0
```

Result:

```text
15
```

---

# 19. Power Function

ধরো:

```text
2³ = 2 × 2 × 2 = 8
```

Relationship:

```text
power(base, exponent)
=
base × power(base, exponent - 1)
```

Code:

```c
#include <stdio.h>

int power(int base, int exponent) {

    if (exponent == 0) {
        return 1;
    }

    return base * power(base, exponent - 1);
}

int main() {

    printf("%d\n", power(2, 3));

    return 0;
}
```

Output:

```text
8
```

---

# 20. Fibonacci — Famous Recursion Problem 🔥

Fibonacci sequence:

```text
0 1 1 2 3 5 8 13 ...
```

Relationship:

```text
F(n) = F(n - 1) + F(n - 2)
```

Base cases:

```text
F(0) = 0
F(1) = 1
```

Code:

```c
#include <stdio.h>

int fibonacci(int n) {

    if (n == 0) {
        return 0;
    }

    if (n == 1) {
        return 1;
    }

    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {

    printf("%d\n", fibonacci(6));

    return 0;
}
```

Output:

```text
8
```

কারণ:

```text
F(6) = 8
```

---

# 21. Fibonacci কেন দুইবার Call করছে?

এই line:

```c
return fibonacci(n - 1) + fibonacci(n - 2);
```

মানে:

```text
                F(6)
               /    \
            F(5)    F(4)
            / \      / \
          F(4) F(3) F(3) F(2)
```

এখানে একই calculation অনেকবার হচ্ছে।

তাই beginner-level Fibonacci recursion সহজ হলেও বড় `n`-এর জন্য inefficient।

পরে optimization/data structures-এর সময় এটার better approach শিখবে।

---

# 22. Recursion-এর সবচেয়ে বড় Danger

অনেক recursive call হলে stack-এর memory ব্যবহার হয়।

যদি recursion কখনো stop না করে:

```text
function
 ↓
function
 ↓
function
 ↓
function
 ↓
...
```

তাহলে **stack overflow** হতে পারে।

তাই সবসময় check করো:

### প্রশ্ন 1:

```text
Base case আছে?
```

### প্রশ্ন 2:

```text
প্রতিটি recursive call কি base case-এর দিকে যাচ্ছে?
```

---

# 23. ভুল Recursion

❌:

```c
int factorial(int n) {
    return n * factorial(n);
}
```

এখানে `n` কখনো কমছে না।

তাই:

```text
factorial(5)
→ factorial(5)
→ factorial(5)
→ factorial(5)
→ ...
```

Stop করবে না।

---

# 24. সঠিক Recursion

```c
int factorial(int n) {

    if (n == 0) {
        return 1;
    }

    return n * factorial(n - 1);
}
```

এখানে:

```text
5
4
3
2
1
0
```

প্রতিবার `n` কমছে।

---

# 25. Recursion-এর 3-Step Formula 🧠

কোনো recursion problem দেখলে:

### Step 1 — Base Case

```c
if (...) {
    return ...;
}
```

### Step 2 — Smaller Problem

```text
n → n - 1
```

অথবা problem-এর smaller version।

### Step 3 — Recursive Call

```c
function(smaller_problem);
```

---

# 🧪 Practice 1

একটি recursive function:

```c
void countdown(int n)
```

যেটা:

```text
5
4
3
2
1
```

print করবে।

---

# 🧪 Practice 2

একটি function:

```c
int sum(int n)
```

যেটা `1` থেকে `n` পর্যন্ত যোগফল return করবে।

Example:

```text
sum(5) = 15
```

---

# 🧪 Practice 3

একটি function:

```c
int factorial(int n)
```

recursive approach দিয়ে লিখো।

Test:

```text
factorial(5)
```

Expected:

```text
120
```

---

# 🔥 Challenge 1 — Reverse Number

একটি number-এর digits reverse করার recursive approach নিয়ে ভাবো।

Example:

```text
1234 → 4321
```

Hint: এখানে শুধু recursion নয়, `%` এবং `/` operator-ও লাগবে।

---

# 🔥 Challenge 2 — Digit Sum

একটি function:

```c
int digitSum(int n)
```

যেটা number-এর digitগুলোর যোগফল return করবে।

Example:

```text
12345
```

Result:

```text
15
```

কারণ:

```text
1 + 2 + 3 + 4 + 5 = 15
```

Hint:

```text
last digit = n % 10
remaining  = n / 10
```

---

# 🧠 আজকের Cheat Sheet

### Recursion

```c
function() {
    function();
}
```

### Base case

```c
if (condition) {
    return;
}
```

### Recursive case

```c
function(smaller_problem);
```

### Factorial

```c
int factorial(int n) {

    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}
```

### Golden Rule ⭐

> **Recursion-এর সবচেয়ে গুরুত্বপূর্ণ অংশ হলো Base Case।**

আর দ্বিতীয় গুরুত্বপূর্ণ বিষয়:

> **Recursive call-কে অবশ্যই কোনোভাবে base case-এর দিকে এগোতে হবে।**

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ✅ Return value
26. ✅ Call by value
27. ✅ Recursion
28. ⏳ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 28: Scope & Lifetime

এবার আমরা বুঝব:

```c
int x = 10;
```

এই `x` **কোথায় ব্যবহার করা যাবে**, কখন তৈরি হয়, কখন শেষ হয়, এবং কেন একই নামের variable বিভিন্ন জায়গায় আলাদা হতে পারে।

এটা বুঝলে **local variable, global variable, block scope, lifetime**—সব পরিষ্কার হবে।

---

# 🚀 Lesson 28 — Scope & Lifetime

আজ আমরা শিখব **Scope** এবং **Lifetime**। দুটো দেখতে কাছাকাছি হলেও একই জিনিস নয়।

সহজভাবে:

> **Scope = variable কোথায় ব্যবহার করা যাবে।**  
> **Lifetime = variable কতক্ষণ memory-তে থাকে।**

---

# 1. Scope কী?

ধরো:

```c
int main() {

    int age = 15;

    printf("%d\n", age);

    return 0;
}
```

এখানে `age` `main()`-এর ভিতরে তৈরি হয়েছে।

তাই `age`-কে `main()`-এর ভিতরের জায়গা থেকে ব্যবহার করা যায়।

এটাই তার **scope**।

---

# 2. Local Variable

Function-এর ভিতরে তৈরি variable হলো সাধারণত **local variable**।

```c
#include <stdio.h>

void test() {

    int x = 10;

    printf("%d\n", x);
}

int main() {

    test();

    return 0;
}
```

এখানে:

```c
int x = 10;
```

হলো local variable।

`x` শুধু `test()` function-এর ভিতরে ব্যবহার করা যায়।

---

# 3. বাইরে থেকে Local Variable ব্যবহার করা যাবে না

❌ এই code ভুল:

```c
#include <stdio.h>

void test() {

    int x = 10;
}

int main() {

    printf("%d\n", x);

    return 0;
}
```

কারণ `x` `test()`-এর local variable।

```text
test()
 └── x

main()
 └── x নেই
```

---

# 4. Function-এর Parameter-ও Local

```c
void add(int a, int b) {

    printf("%d\n", a + b);
}
```

এখানে:

```text
a
b
```

দুটিই function-এর local scope-এ থাকে।

`main()` থেকে সরাসরি:

```c
printf("%d", a);
```

করা যাবে না।

---

# 5. Block Scope

C-তে `{ }` দিয়ে তৈরি block-এরও scope থাকতে পারে।

```c
#include <stdio.h>

int main() {

    int x = 10;

    if (x > 5) {

        int y = 20;

        printf("%d\n", y);
    }

    return 0;
}
```

`y` শুধু `if` block-এর ভিতরে ব্যবহার করা যায়।

---

# 6. Block-এর বাইরে `y` নেই

❌:

```c
int main() {

    if (1) {

        int y = 20;
    }

    printf("%d\n", y);

    return 0;
}
```

এটা কাজ করবে না।

কারণ:

```text
if block
 └── y

outside
 └── y নেই
```

---

# 7. Nested Block

একটি block-এর ভিতরে আরেকটি block থাকতে পারে।

```c
#include <stdio.h>

int main() {

    int a = 10;

    {
        int b = 20;

        {
            int c = 30;

            printf("%d %d %d\n", a, b, c);
        }
    }

    return 0;
}
```

ভেতরের block সাধারণত বাইরের scope-এর variable দেখতে পারে।

```text
Outer
 └── a

    Inner
     └── b

        More Inner
         └── c
```

শেষের block থেকে `a`, `b`, `c` দেখা যায়।

---

# 8. বাইরের Variable ভিতরে ব্যবহার করা যায়

```c
#include <stdio.h>

int main() {

    int x = 10;

    if (x > 5) {

        printf("%d\n", x);
    }

    return 0;
}
```

Output:

```text
10
```

কারণ `x` বাইরের scope-এ আছে এবং inner block সেটাকে দেখতে পারে।

---

# 9. Inner Variable বাইরে ব্যবহার করা যায় না

```text
Outer scope
    ↓
Inner scope
```

Inner scope বাইরের variable access করতে পারে।

কিন্তু:

```text
Inner scope
    ↓
Outer scope
```

এভাবে outer scope inner-এর variable দেখতে পারে না।

---

# 10. Same Name Variable

C-তে nested scope-এ একই নামের variable তৈরি করা সম্ভব।

```c
#include <stdio.h>

int main() {

    int x = 10;

    {
        int x = 20;

        printf("Inside = %d\n", x);
    }

    printf("Outside = %d\n", x);

    return 0;
}
```

Output:

```text
Inside = 20
Outside = 10
```

কেন?

কারণ দুটি `x` আলাদা scope-এর।

---

# 11. Shadowing

যখন inner scope-এর variable outer scope-এর একই নামের variable-কে temporarily hide করে, তাকে **shadowing** বলা হয়।

```c
int x = 10;

{
    int x = 20;

    printf("%d\n", x);
}
```

Inner block-এর `x` outer `x`-কে shadow করছে।

---

# 12. Function-এর ক্ষেত্রেও Same Name

```c
#include <stdio.h>

void test() {

    int x = 20;

    printf("Function: %d\n", x);
}

int main() {

    int x = 10;

    test();

    printf("Main: %d\n", x);

    return 0;
}
```

Output:

```text
Function: 20
Main: 10
```

দুটো `x` আলাদা variable।

---

# 13. Global Variable

Function-এর বাইরে variable declare করলে সেটা **global variable** হতে পারে।

```c
#include <stdio.h>

int x = 10;

void test() {

    printf("%d\n", x);
}

int main() {

    printf("%d\n", x);

    test();

    return 0;
}
```

Output:

```text
10
10
```

এখানে:

```c
int x = 10;
```

global scope-এ আছে।

---

# 14. Global Variable অনেক Function থেকে Access করা যায়

```c
#include <stdio.h>

int score = 100;

void showScore() {
    printf("Score = %d\n", score);
}

void changeScore() {
    score = 200;
}

int main() {

    showScore();

    changeScore();

    showScore();

    return 0;
}
```

Output:

```text
Score = 100
Score = 200
```

কারণ দুই function-ই global `score` access করছে।

---

# 15. Global Variable পরিবর্তন করা যায়

```c
int count = 0;

void increase() {
    count++;
}
```

তারপর:

```c
increase();
increase();
increase();
```

`count` হবে:

```text
3
```

---

# 16. Global বনাম Local

|বিষয়|Local|Global|
|---|---|---|
|কোথায় declare?|function/block-এর ভিতরে|function-এর বাইরে|
|Scope|নির্দিষ্ট block/function|file/program-এর broader scope|
|অন্য function থেকে access|সাধারণত না|সম্ভব|
|Lifetime|সাধারণ automatic local-এর ক্ষেত্রে block execution পর্যন্ত|সাধারণত পুরো program execution|

---

# 17. Lifetime কী?

এবার দ্বিতীয় concept।

**Scope** বলছে:

> কোথায় variable-কে দেখা/ব্যবহার করা যায়?

**Lifetime** বলছে:

> কতক্ষণ variable-এর objectটি exist করে?

উদাহরণ:

```c
void test() {

    int x = 10;

}
```

`x` function-এর block-এ তৈরি হয় এবং block execution শেষ হলে সাধারণ automatic `x`-এর lifetime শেষ হয়।

---

# 18. Scope ≠ Lifetime

এটা খুব গুরুত্বপূর্ণ।

দুটো আলাদা প্রশ্ন:

```text
Scope:
"আমি কোথা থেকে x-কে access করতে পারি?"

Lifetime:
"x কতক্ষণ exist করে?"
```

---

# 19. Local Variable-এর Lifetime

```c
#include <stdio.h>

void test() {

    int x = 10;

    printf("%d\n", x);
}

int main() {

    test();

    test();

    return 0;
}
```

প্রতিবার `test()` call হলে local `x`-এর একটি নতুন execution instance তৈরি হয়।

ধারণাগতভাবে:

```text
First test()
    x = 10
    function ends
    ↓
x-এর lifetime শেষ

Second test()
    নতুন x
```

---

# 20. Local Variable কি আগের Value মনে রাখে?

সাধারণ local automatic variable:

```c
void test() {

    int x = 0;

    x++;

    printf("%d\n", x);
}
```

যদি:

```c
test();
test();
test();
```

call করো, প্রত্যেক invocation-এ `x` initialize হবে `0` দিয়ে।

Output:

```text
1
1
1
```

---

# 21. Static Variable

এখন একটি বিশেষ variable:

```c
static int x = 0;
```

এটি function call-এর মধ্যে value ধরে রাখতে পারে।

```c
#include <stdio.h>

void test() {

    static int x = 0;

    x++;

    printf("%d\n", x);
}

int main() {

    test();
    test();
    test();

    return 0;
}
```

Output:

```text
1
2
3
```

---

# 22. Static Variable কেন এমন হলো?

প্রথম call:

```text
x = 0
x++
x = 1
```

Function শেষ হলেও static `x`-এর lifetime শেষ হয় না।

দ্বিতীয় call:

```text
x = 1
x++
x = 2
```

তৃতীয়:

```text
x = 2
x++
x = 3
```

---

# 23. Static-এর Scope বনাম Lifetime

এই example:

```c
void test() {

    static int count = 0;

    count++;
}
```

`count`:

- **Scope:** `test()` function-এর ভিতরের declaration-এর scope
    
- **Lifetime:** পুরো program execution-এর সময়
    

এটাই দেখায়:

> Scope এবং lifetime একই জিনিস নয়।

---

# 24. Global Variable-এর Lifetime

Global variable:

```c
int score = 100;
```

সাধারণত program শুরু থেকে program শেষ হওয়া পর্যন্ত exist করে।

তাই:

```text
Program starts
     ↓
global variable exists
     ↓
functions run
     ↓
Program ends
     ↓
global variable lifetime ends
```

---

# 25. Local Block Example

```c
#include <stdio.h>

int main() {

    int a = 10;

    if (a > 5) {

        int b = 20;

        printf("%d\n", a);
        printf("%d\n", b);
    }

    printf("%d\n", a);

    return 0;
}
```

এখানে:

```text
a → main-এর scope
b → if block-এর scope
```

`if` block-এর বাইরে `b` ব্যবহার করা যাবে না।

---

# 26. Loop-এর Variable Scope

Modern C-তে:

```c
#include <stdio.h>

int main() {

    for (int i = 0; i < 5; i++) {
        printf("%d\n", i);
    }

    return 0;
}
```

এখানে `i`-এর scope `for` statement-এর associated region-এর মধ্যে।

তাই loop-এর পরে:

```c
printf("%d", i);
```

লিখলে কাজ করবে না।

---

# 27. Function Parameter-এর Scope

```c
void add(int a, int b) {

    int result = a + b;

    printf("%d\n", result);
}
```

এখানে:

```text
a
b
result
```

সবগুলো function-এর local context-এর মধ্যে।

---

# 28. Global এবং Local একই নাম

```c
#include <stdio.h>

int x = 100;

void test() {

    int x = 50;

    printf("%d\n", x);
}

int main() {

    test();

    printf("%d\n", x);

    return 0;
}
```

Output:

```text
50
100
```

কারণ function-এর local `x` global `x`-কে shadow করছে।

---

# 29. কোন Variable আগে খোঁজা হয়?

যদি একই নামের variable থাকে, C সাধারণত সবচেয়ে কাছের applicable scope-এর declaration ব্যবহার করে।

```text
inner block x
     ↓
outer block x
     ↓
global x
```

অর্থাৎ inner scope-এর declaration আগে priority পায়।

---

# 30. Scope শেখার সহজ Diagram

```text
Global Scope
│
├── global variable
│
├── main()
│   │
│   ├── local variable
│   │
│   └── if block
│       └── block variable
│
└── test()
    └── local variable
```

এক scope-এর variable অন্য scope-এ automatically visible হবে—এমন নয়।

---

# 31. Lifetime মনে রাখার সহজ উপায়

### সাধারণ Local

```text
Block starts
    ↓
variable created
    ↓
block ends
    ↓
variable lifetime ends
```

### Static

```text
Block starts
    ↓
variable exists
    ↓
block ends
    ↓
variable remains
    ↓
program ends
    ↓
lifetime ends
```

### Global

```text
Program starts
    ↓
exists
    ↓
program ends
    ↓
lifetime ends
```

---

# 32. একটি Practical Example

Counter তৈরি করি।

### Normal local variable:

```c
#include <stdio.h>

void counter() {

    int count = 0;

    count++;

    printf("%d\n", count);
}

int main() {

    counter();
    counter();
    counter();

    return 0;
}
```

Output:

```text
1
1
1
```

### Static:

```c
#include <stdio.h>

void counter() {

    static int count = 0;

    count++;

    printf("%d\n", count);
}

int main() {

    counter();
    counter();
    counter();

    return 0;
}
```

Output:

```text
1
2
3
```

---

# 🧪 Practice 1

Output কী হবে?

```c
#include <stdio.h>

int x = 100;

void test() {
    int x = 50;
    printf("%d\n", x);
}

int main() {
    test();
    printf("%d\n", x);

    return 0;
}
```

নিজে আগে predict করো।

---

# 🧪 Practice 2

Output কী হবে?

```c
#include <stdio.h>

void test() {

    static int count = 0;

    count++;

    printf("%d\n", count);
}

int main() {

    test();
    test();
    test();
    test();

    return 0;
}
```

---

# 🧪 Practice 3

এই code-এ কোন variable কোথায় ব্যবহার করা যাবে সেটা identify করো:

```c
int global = 10;

int main() {

    int a = 20;

    if (a > 10) {

        int b = 30;

        printf("%d\n", global);
        printf("%d\n", a);
        printf("%d\n", b);
    }

    return 0;
}
```

Identify:

```text
global → ?
a      → ?
b      → ?
```

---

# 🔥 Mini Challenge

একটি function তৈরি করো:

```c
void counter()
```

যেটা প্রতিবার call করলে:

```text
Call 1 → 1
Call 2 → 2
Call 3 → 3
Call 4 → 4
Call 5 → 5
```

দেখাবে।

**Hint:** `static` ব্যবহার করো।

---

# 🧠 আজকের Cheat Sheet

### Scope

```text
কোথায় variable access করা যায়
```

### Lifetime

```text
কতক্ষণ variable exist করে
```

### Local

```c
void test() {
    int x = 10;
}
```

### Global

```c
int x = 10;

int main() {
}
```

### Block scope

```c
if (condition) {
    int x = 10;
}
```

### Static

```c
static int count = 0;
```

Function শেষ হলেও static object's lifetime শেষ হয় না; পরের call-এ value থাকে।

---

# 🎯 Phase 4 Progress

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ✅ Return value
26. ✅ Call by value
27. ✅ Recursion
28. ✅ Scope & lifetime
29. ⏳ Header files
```

## 🚀 Next → Lesson 29: Header Files

এটাই **Phase 4-এর শেষ lesson**।

আমরা শিখব:

```c
#include <stdio.h>
```

এর `<stdio.h>` আসলে কী, header file কেন দরকার, নিজের **custom header file** কীভাবে বানানো যায়, এবং বড় C program-কে একাধিক `.c` ও `.h` file-এ কীভাবে ভাগ করা হয়।

----

# 🚀 Lesson 29 — Header Files

আজ **Phase 4 — Functions**-এর শেষ lesson।

আমরা শিখব:

```c
#include <stdio.h>
```

এর `stdio.h` কী, header file কেন লাগে, নিজের `.h` file কীভাবে বানাতে হয়, এবং বড় C program কীভাবে multiple files-এ ভাগ করা যায়।

---

# 1. Header File কী?

Header file হলো এমন একটি file যেখানে সাধারণত রাখা হয়:

- Function declaration / prototype
    
- Macro
    
- `typedef`
    
- `struct` declaration
    
- Constant বা অন্যান্য shared declaration
    

Header file-এর extension সাধারণত:

```text
.h
```

যেমন:

```text
stdio.h
math.h
string.h
```

---

# 2. `#include <stdio.h>` কী?

আমরা প্রায় প্রতিটি C program-এ দেখি:

```c
#include <stdio.h>
```

`stdio.h` হলো C standard library-এর একটি header।

এতে input/output সম্পর্কিত বিভিন্ন declaration থাকে, যেমন:

```c
printf()
scanf()
```

তাই compiler-কে এগুলোর declaration জানানো হয়।

---

# 3. Header File নিজে Function-এর Implementation নয়

ধরো:

```c
#include <stdio.h>
```

এটা এমন নয় যে `printf()`-এর পুরো code তোমার `.c` file-এর মধ্যে লিখে দেওয়া হচ্ছে।

Header মূলত compiler-কে প্রয়োজনীয় **declaration/interface information** দেয়।

Function-এর actual implementation library-এর অন্য অংশে থাকে এবং linking-এর সময় program-এর সঙ্গে যুক্ত হয়।

---

# 4. Declaration বনাম Definition

এটা খুব গুরুত্বপূর্ণ।

### Declaration:

```c
int add(int a, int b);
```

এটা compiler-কে বলছে:

> `add()` নামে একটি function আছে, এটি দুইটি `int` নেবে এবং `int` return করবে।

### Definition:

```c
int add(int a, int b) {
    return a + b;
}
```

এখানে function-এর actual implementation আছে।

---

# 5. Header File-এ সাধারণত Declaration

যেমন:

```c
// calculator.h

int add(int a, int b);
int subtract(int a, int b);
```

এখানে function-এর implementation নেই।

তারপর `.c` file-এ:

```c
// calculator.c

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}
```

---

# 6. নিজের Header File বানানো

ধরো আমাদের project:

```text
project/
│
├── main.c
├── calculator.c
└── calculator.h
```

### `calculator.h`

```c
#ifndef CALCULATOR_H
#define CALCULATOR_H

int add(int a, int b);
int subtract(int a, int b);

#endif
```

### `calculator.c`

```c
#include "calculator.h"

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}
```

### `main.c`

```c
#include <stdio.h>
#include "calculator.h"

int main() {

    printf("Sum = %d\n", add(10, 5));
    printf("Difference = %d\n", subtract(10, 5));

    return 0;
}
```

---

# 7. `< >` বনাম `" "`

এটা খুব গুরুত্বপূর্ণ।

### Standard/system header:

```c
#include <stdio.h>
```

### নিজের header:

```c
#include "calculator.h"
```

Beginner হিসেবে মনে রাখো:

```text
<...> → system/standard include-এর জন্য সাধারণত ব্যবহৃত হয়
"..." → নিজের/project header-এর জন্য সাধারণত ব্যবহৃত হয়
```

---

# 8. Header Guard কী?

এই অংশটা:

```c
#ifndef CALCULATOR_H
#define CALCULATOR_H

// declarations

#endif
```

হলো **header guard**।

এর উদ্দেশ্য হলো একই header একাধিকবার include হয়ে declaration-এর সমস্যা তৈরি করা থেকে রক্ষা করা।

---

# 9. Header Guard কীভাবে কাজ করে?

প্রথমবার:

```c
#ifndef CALCULATOR_H
```

চেক করে `CALCULATOR_H` আগে define করা হয়েছে কি না।

না হলে:

```c
#define CALCULATOR_H
```

তারপর header-এর content process হয়।

পরেরবার একই header include হলে:

```text
CALCULATOR_H already defined
        ↓
content skip
```

---

# 10. কেন Header Guard দরকার?

ধরো:

```c
#include "calculator.h"
#include "calculator.h"
```

একই header দুইবার include করা হলো।

Header guard থাকলে compiler effectively দ্বিতীয়বার declarations-এর content skip করতে পারে।

তাই custom header-এর জন্য header guard ব্যবহার করা ভালো practice।

---

# 11. `#include` আসলে কী?

`#include` হলো **preprocessor directive**।

যেমন:

```c
#include <stdio.h>
```

Preprocessor compilation-এর আগে include directive process করে।

সহজভাবে:

```text
Source code
    ↓
Preprocessor
    ↓
Compiler
    ↓
Object code
    ↓
Linker
    ↓
Executable
```

---

# 12. C Program Build Process

একটি C program সাধারণত কয়েকটি ধাপ পার করে:

```text
.c files
   ↓
Preprocessing
   ↓
Compilation
   ↓
Object files
   ↓
Linking
   ↓
Executable
```

এটা C বোঝার জন্য খুব গুরুত্বপূর্ণ foundation।

---

# 13. Multiple `.c` Files কেন?

বড় program-এ সব code এক file-এ রাখলে code দ্রুত messy হয়ে যায়।

ধরো একটি project:

```text
Bank Management System
```

তাহলে আলাদা করা যায়:

```text
main.c
account.c
customer.c
transaction.c
account.h
customer.h
transaction.h
```

প্রতিটি file নির্দিষ্ট কাজ করবে।

---

# 14. ছোট Project Structure

ধরো আমরা calculator বানাচ্ছি:

```text
calculator/
│
├── main.c
├── calculator.c
└── calculator.h
```

Responsibility:

```text
main.c
   ↓
program control

calculator.c
   ↓
calculation functions

calculator.h
   ↓
function declarations
```

এটা clean design-এর শুরু।

---

# 15. Complete Example

### `calculator.h`

```c
#ifndef CALCULATOR_H
#define CALCULATOR_H

int add(int a, int b);
int subtract(int a, int b);
int multiply(int a, int b);

#endif
```

### `calculator.c`

```c
#include "calculator.h"

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}
```

### `main.c`

```c
#include <stdio.h>
#include "calculator.h"

int main() {

    printf("Add = %d\n", add(10, 5));
    printf("Subtract = %d\n", subtract(10, 5));
    printf("Multiply = %d\n", multiply(10, 5));

    return 0;
}
```

---

# 16. Compile কীভাবে?

যদি GCC ব্যবহার করো এবং তিনটি file একই folder-এ থাকে:

```bash
gcc main.c calculator.c -o calculator
```

তারপর Linux/macOS-এ:

```bash
./calculator
```

Windows-এ সাধারণত:

```bash
calculator.exe
```

Output:

```text
Add = 15
Subtract = 5
Multiply = 50
```

---

# 17. গুরুত্বপূর্ণ বিষয়

এই command:

```bash
gcc main.c calculator.c -o calculator
```

মানে আমরা দুইটি source file compile/link করে একটি executable তৈরি করছি।

```text
main.c
calculator.c
   ↓
 GCC
   ↓
calculator
```

---

# 18. Header-এ Function Definition রাখা উচিত?

Beginner level-এ সাধারণভাবে:

❌ এভাবে না:

```c
// calculator.h

int add(int a, int b) {
    return a + b;
}
```

বরং:

```c
// calculator.h

int add(int a, int b);
```

এবং:

```c
// calculator.c

int add(int a, int b) {
    return a + b;
}
```

অর্থাৎ:

```text
.h → interface/declarations
.c → implementation
```

এটা সব situation-এর absolute rule নয়, কিন্তু beginner project-এর জন্য খুব ভালো convention।

---

# 19. `math.h`

C standard library-তে অনেক header আছে।

যেমন:

```c
#include <math.h>
```

এতে mathematical functions-এর declarations পাওয়া যায়।

উদাহরণ:

```c
#include <stdio.h>
#include <math.h>

int main() {

    double result = sqrt(25.0);

    printf("%.2f\n", result);

    return 0;
}
```

Output:

```text
5.00
```

কিছু GCC environment-এ math library link করার জন্য:

```bash
gcc main.c -o main -lm
```

প্রয়োজন হতে পারে।

---

# 20. `string.h`

String-related functions-এর জন্য:

```c
#include <string.h>
```

যেমন:

```c
strlen()
strcpy()
strcmp()
```

আমরা এগুলো Phase 5 — Arrays & Strings-এ বিস্তারিত শিখব।

---

# 21. Common Standard Headers

কিছু গুরুত্বপূর্ণ header:

|Header|প্রধান ব্যবহার|
|---|---|
|`stdio.h`|Input/output|
|`stdlib.h`|General utilities, memory allocation ইত্যাদি|
|`string.h`|String functions|
|`math.h`|Mathematical functions|
|`ctype.h`|Character classification/conversion|
|`time.h`|Date/time related functions|

---

# 22. Header File-এ কী কী থাকতে পারে?

Custom header-এ রাখতে পারো:

### Function declaration

```c
int add(int a, int b);
```

### `struct`

```c
struct Student {
    int id;
    float marks;
};
```

### `typedef`

```c
typedef unsigned int uint;
```

### Macro

```c
#define MAX 100
```

এগুলো আমরা পরের phases-এ আরও বিস্তারিত শিখব।

---

# 23. `.h` File কি সরাসরি Run করা যায়?

সাধারণত `.h` file executable program নয়।

যেমন:

```text
calculator.h
```

এটা নিজে run করার জন্য নয়।

এটা অন্য source file-এ include করা হয়:

```c
#include "calculator.h"
```

---

# 24. Header File-এর মূল ধারণা

একটি বড় project-এ:

```text
                  calculator.h
                 /             \
                ↓               ↓
           calculator.c       main.c
                ↓               ↓
          implementation      usage
```

Header হলো দুই অংশের মধ্যে **interface/contract**-এর মতো কাজ করতে পারে।

---

# 25. কেন Header File শেখা গুরুত্বপূর্ণ?

কারণ পরের দিকে তুমি যখন project বানাবে:

```text
🏦 Bank Management System
📚 Student Management System
🛒 E-commerce CLI
```

তখন সব code এক `main.c`-এ না রেখে আলাদা করতে পারবে।

যেমন:

```text
bank.h
bank.c
customer.h
customer.c
transaction.h
transaction.c
main.c
```

এতে project maintain করা সহজ হয়।

---

# 🧪 Practice 1

নিজের `math_utils.h` তৈরি করো:

```c
int square(int n);
int cube(int n);
```

তারপর `math_utils.c`-তে তাদের definition লিখো।

---

# 🧪 Practice 2

এই structure তৈরি করো:

```text
myproject/
│
├── main.c
├── math_utils.c
└── math_utils.h
```

`main.c` থেকে:

```c
square(5)
cube(3)
```

call করে result print করো।

---

# 🔥 Mini Project — Modular Calculator

তিনটি file বানাও:

```text
calculator.h
calculator.c
main.c
```

Functions:

```c
int add(int a, int b);
int subtract(int a, int b);
int multiply(int a, int b);
int divide(int a, int b);
```

তারপর `main.c`-তে user-এর দুইটি number input নিয়ে সব operation-এর result দেখাও।

**Extra challenge:** `divide()`-এর আগে `b == 0` কিনা check করো।

---

# 🧠 আজকের Cheat Sheet

### Header

```text
.h
```

সাধারণত declarations/interface রাখে।

### Source

```text
.c
```

সাধারণত implementation রাখে।

### Standard header

```c
#include <stdio.h>
```

### Custom header

```c
#include "calculator.h"
```

### Function declaration

```c
int add(int a, int b);
```

### Function definition

```c
int add(int a, int b) {
    return a + b;
}
```

### Header guard

```c
#ifndef MY_HEADER_H
#define MY_HEADER_H

// declarations

#endif
```

---

# 🎉 Phase 4 সম্পূর্ণ!

তুমি এখন Functions-এর পুরো foundation শেষ করেছ:

```text
23. ✅ Function basics
24. ✅ Parameters & arguments
25. ✅ Return value
26. ✅ Call by value
27. ✅ Recursion
28. ✅ Scope & lifetime
29. ✅ Header files
```

## 🚀 Next Phase — Phase 5: Arrays & Strings

এখন আমরা এমন data নিয়ে কাজ করব যেখানে **একটি variable-এর মধ্যে একাধিক value** রাখা যায়।

### Lesson 30 → 1D Array

শুরু করব:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

তারপর শিখব:

```text
Array কী
Index কী
0 থেকে indexing কেন
Array input
Array traversal
Array + loop
```

এখান থেকেই তোমার C programming অনেক বেশি practical হতে শুরু করবে।

---

# 🚀 Lesson 30 — 1D Array

এখন শুরু হলো **Phase 5 — Arrays & Strings**।

আজকের topic:

> **1D Array — একই ধরনের একাধিক value একটি variable-এর মধ্যে রাখা।**

---

# 1. Array কী?

ধরো তোমার 5 জন student's marks রাখতে হবে।

Array ছাড়া:

```c
int mark1 = 80;
int mark2 = 75;
int mark3 = 90;
int mark4 = 65;
int mark5 = 88;
```

এটা manageable, কিন্তু অনেক data হলে ঝামেলা।

Array দিয়ে:

```c
int marks[5] = {80, 75, 90, 65, 88};
```

একটি `marks` array-তেই 5টি value রাখা হলো।

```text
marks
┌────┬────┬────┬────┬────┐
│ 80 │ 75 │ 90 │ 65 │ 88 │
└────┴────┴────┴────┴────┘
```

---

# 2. Array Declaration

Syntax:

```c
data_type array_name[size];
```

Example:

```c
int numbers[5];
```

মানে:

```text
Type  → int
Name  → numbers
Size  → 5
```

এখানে 5টি `int` value রাখার জায়গা তৈরি হয়।

---

# 3. Array Index

এখানে সবচেয়ে গুরুত্বপূর্ণ rule:

> **C array-এর indexing 0 থেকে শুরু হয়।**

যদি:

```c
int numbers[5];
```

হয়, তাহলে index:

```text
Index:    0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
numbers: │ 10 │ 20 │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
```

শেষ index:

```text
size - 1
```

অর্থাৎ:

```text
5 - 1 = 4
```

---

# 4. Array-এর একটি Element Access করা

```c
#include <stdio.h>

int main() {

    int numbers[5] = {10, 20, 30, 40, 50};

    printf("%d\n", numbers[0]);
    printf("%d\n", numbers[1]);
    printf("%d\n", numbers[4]);

    return 0;
}
```

Output:

```text
10
20
50
```

---

# 5. `numbers[0]` মানে কী?

এটা array-এর প্রথম element।

```text
numbers[0] → 10
numbers[1] → 20
numbers[2] → 30
numbers[3] → 40
numbers[4] → 50
```

---

# 6. কেন Index 0 থেকে?

C array-এর প্রথম element-কে index `0` দিয়ে identify করে।

তাই:

```text
First element → [0]
Second        → [1]
Third         → [2]
...
```

এটা C-এর খুব গুরুত্বপূর্ণ convention।

---

# 7. Array Initialize করা

Declaration-এর সময় value দেওয়া যায়:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

এটাকে initialization বলা হয়।

---

# 8. Size না দিলেও চলে

```c
int numbers[] = {10, 20, 30, 40, 50};
```

এখানে compiler element count থেকে size নির্ধারণ করতে পারে।

অর্থাৎ এটি effectively:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

---

# 9. আংশিক Initialization

```c
int numbers[5] = {10, 20};
```

তাহলে বাকি element-গুলো zero-initialized হবে:

```text
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │  0 │  0 │  0 │
└────┴────┴────┴────┴────┘
```

অর্থাৎ:

```c
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 0;
numbers[3] = 0;
numbers[4] = 0;
```

---

# 10. সব Value Zero করতে

```c
int numbers[5] = {0};
```

ফলে:

```text
0 0 0 0 0
```

---

# 11. Array Element পরিবর্তন করা

Array-এর element পরে change করা যায়:

```c
#include <stdio.h>

int main() {

    int numbers[5] = {10, 20, 30, 40, 50};

    numbers[2] = 100;

    printf("%d\n", numbers[2]);

    return 0;
}
```

Output:

```text
100
```

আগে:

```text
10 20 30 40 50
```

পরে:

```text
10 20 100 40 50
```

---

# 12. Array + Loop 🔥

Array-এর সবচেয়ে বড় সুবিধা হলো loop-এর সঙ্গে ব্যবহার করা যায়।

```c
#include <stdio.h>

int main() {

    int numbers[5] = {10, 20, 30, 40, 50};

    for (int i = 0; i < 5; i++) {
        printf("%d\n", numbers[i]);
    }

    return 0;
}
```

Output:

```text
10
20
30
40
50
```

---

# 13. Loop কীভাবে Array Access করছে?

প্রথম iteration:

```text
i = 0
numbers[0]
```

দ্বিতীয়:

```text
i = 1
numbers[1]
```

তারপর:

```text
i = 2 → numbers[2]
i = 3 → numbers[3]
i = 4 → numbers[4]
```

তাই সাধারণ pattern:

```c
for (int i = 0; i < size; i++) {
    printf("%d", array[i]);
}
```

এটা খুব গুরুত্বপূর্ণ pattern। ⭐

---

# 14. Array Input নেওয়া

User-এর কাছ থেকে 5টি number নিতে পারি:

```c
#include <stdio.h>

int main() {

    int numbers[5];

    for (int i = 0; i < 5; i++) {
        scanf("%d", &numbers[i]);
    }

    for (int i = 0; i < 5; i++) {
        printf("%d\n", numbers[i]);
    }

    return 0;
}
```

Input:

```text
10 20 30 40 50
```

Output:

```text
10
20
30
40
50
```

---

# 15. `&numbers[i]` কেন?

এটা মনে করো:

```c
scanf("%d", &numbers[i]);
```

`scanf()`-কে value কোথায় store করতে হবে সেই address দিতে হয়।

Pointers lesson-এ আমরা `&` আরও গভীরভাবে শিখেছি/শিখব; এখানে আপাতত মনে রাখো:

```text
scanf → input store করার address চায়
```

---

# 16. Array-এর Size

যদি:

```c
int numbers[10];
```

তাহলে valid indices:

```text
0 1 2 3 4 5 6 7 8 9
```

`10` নয়।

কারণ শেষ index:

```text
10 - 1 = 9
```

---

# 17. Out of Bounds ⚠️

এটা ভুল:

```c
int numbers[5];

numbers[5] = 100;
```

কারণ valid:

```text
numbers[0]
numbers[1]
numbers[2]
numbers[3]
numbers[4]
```

`numbers[5]` array-এর বাইরে।

এ ধরনের access **undefined behavior** তৈরি করতে পারে।

তাই rule:

> `0 <= index < size`

---

# 18. Array Memory Concept

Array-এর elements memory-তে ধারাবাহিকভাবে রাখা হয়।

ধারণাগতভাবে:

```text
numbers[0] numbers[1] numbers[2] numbers[3]
    ↓          ↓          ↓          ↓
  memory     memory     memory     memory
```

যেহেতু সব element একই type-এর, element-এর size একই হয়।

Pointers lesson-এ আমরা এর memory behavior আরও গভীরভাবে দেখব।

---

# 19. Character Array

Array শুধু `int`-এর জন্য নয়।

```c
char letters[5] = {'A', 'B', 'C', 'D', 'E'};
```

এখানে:

```text
Index:    0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
         │ A  │ B  │ C  │ D  │ E  │
         └────┴────┴────┴────┴────┘
```

String-এর জন্য character array আরও গুরুত্বপূর্ণ হবে পরের lessons-এ।

---

# 20. Float Array

```c
float prices[3] = {10.5, 20.75, 30.25};
```

Access:

```c
printf("%.2f\n", prices[1]);
```

Output:

```text
20.75
```

---

# 21. Array-এর সব Element-এর Sum

এটা খুব common problem:

```c
#include <stdio.h>

int main() {

    int numbers[5] = {10, 20, 30, 40, 50};

    int sum = 0;

    for (int i = 0; i < 5; i++) {
        sum += numbers[i];
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Output:

```text
Sum = 150
```

Pattern:

```text
sum = 0

sum += array[0]
sum += array[1]
sum += array[2]
...
```

---

# 22. Average

Sum বের করে average:

```c
#include <stdio.h>

int main() {

    int marks[5] = {80, 70, 90, 60, 100};

    int sum = 0;

    for (int i = 0; i < 5; i++) {
        sum += marks[i];
    }

    float average = sum / 5.0;

    printf("Average = %.2f\n", average);

    return 0;
}
```

Output:

```text
Average = 80.00
```

---

# 23. Maximum Value

```c
#include <stdio.h>

int main() {

    int numbers[5] = {25, 10, 80, 45, 60};

    int max = numbers[0];

    for (int i = 1; i < 5; i++) {

        if (numbers[i] > max) {
            max = numbers[i];
        }
    }

    printf("Max = %d\n", max);

    return 0;
}
```

Output:

```text
Max = 80
```

এখানে আমরা প্রথম element-কে initial maximum ধরেছি।

---

# 24. Minimum Value

একইভাবে:

```c
#include <stdio.h>

int main() {

    int numbers[5] = {25, 10, 80, 45, 60};

    int min = numbers[0];

    for (int i = 1; i < 5; i++) {

        if (numbers[i] < min) {
            min = numbers[i];
        }
    }

    printf("Min = %d\n", min);

    return 0;
}
```

Output:

```text
Min = 10
```

---

# 25. Reverse Order-এ Print

Array:

```text
10 20 30 40 50
```

Reverse:

```text
50 40 30 20 10
```

Code:

```c
#include <stdio.h>

int main() {

    int numbers[5] = {10, 20, 30, 40, 50};

    for (int i = 4; i >= 0; i--) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
50 40 30 20 10
```

---

# 26. User Input + Maximum

একটি practical example:

```c
#include <stdio.h>

int main() {

    int numbers[5];

    printf("Enter 5 numbers:\n");

    for (int i = 0; i < 5; i++) {
        scanf("%d", &numbers[i]);
    }

    int max = numbers[0];

    for (int i = 1; i < 5; i++) {

        if (numbers[i] > max) {
            max = numbers[i];
        }
    }

    printf("Maximum = %d\n", max);

    return 0;
}
```

---

# 27. Array Size বের করা

যদি একই scope-এ actual array object থাকে:

```c
int numbers[] = {10, 20, 30, 40, 50};
```

তাহলে:

```c
int size = sizeof(numbers) / sizeof(numbers[0]);
```

এখানে:

```text
sizeof(numbers)
```

পুরো array-এর bytes দেয়।

আর:

```text
sizeof(numbers[0])
```

একটি element-এর bytes দেয়।

তাই:

```text
array bytes / element bytes
= element count
```

অর্থাৎ:

```text
5
```

---

# 28. Complete Example

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    printf("Size = %d\n", size);

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
Size = 5
10 20 30 40 50
```

এটা একটি খুব useful pattern।

---

# 29. একটি গুরুত্বপূর্ণ Limitation

এইভাবে:

```c
int size = sizeof(numbers) / sizeof(numbers[0]);
```

array object-এর scope-এ কাজ করে।

কিন্তু function-এ array parameter হিসেবে পাঠালে বিষয়টি আলাদা—সেখানে `sizeof` দিয়ে original array-এর element count সাধারণভাবে পাওয়া যায় না।

এটা আমরা array + function এবং পরে pointers-এ বিস্তারিত দেখব।

---

# 30. Array Declaration বনাম Initialization

### Declaration:

```c
int numbers[5];
```

### Initialization:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

### Size inference:

```c
int numbers[] = {10, 20, 30, 40, 50};
```

---

# 🧪 Practice 1 — Print Array

এই array-এর সব element loop দিয়ে print করো:

```c
int numbers[6] = {5, 10, 15, 20, 25, 30};
```

Expected:

```text
5 10 15 20 25 30
```

---

# 🧪 Practice 2 — Sum

Input:

```text
10 20 30 40 50
```

Output:

```text
Sum = 150
```

নিজে program লিখো।

---

# 🧪 Practice 3 — Maximum

এই array:

```c
int numbers[7] = {12, 45, 7, 89, 23, 56, 10};
```

Maximum বের করো।

Expected:

```text
89
```

---

# 🔥 Challenge — Second Largest

এই array:

```c
int numbers[7] = {12, 45, 7, 89, 23, 56, 10};
```

Largest:

```text
89
```

Second largest:

```text
56
```

**Hint:** প্রথমে maximum/second maximum track করার logic নিয়ে ভাবো।

---

# 🧠 আজকের Cheat Sheet

### Array declaration

```c
int numbers[5];
```

### Initialization

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

### Indexing

```text
0 → first
1 → second
...
size - 1 → last
```

### Access

```c
numbers[2]
```

### Change

```c
numbers[2] = 100;
```

### Traversal

```c
for (int i = 0; i < size; i++) {
    printf("%d ", numbers[i]);
}
```

### Size

```c
sizeof(numbers) / sizeof(numbers[0])
```

### Golden Rule ⭐

> **Array-এর size যদি `N` হয়, valid index হলো `0` থেকে `N-1` পর্যন্ত।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ⏳ Array traversal
32. ⏳ Searching
33. ⏳ Sorting
34. ⏳ 2D Array / Matrix
35. ⏳ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 31: Array Traversal

পরের lesson-এ আমরা শুধু array print করব না—**একটি array-এর প্রতিটি element systematically visit, process এবং modify** করার বিভিন্ন pattern শিখব।

যেমন:

```text
Print all
Sum
Average
Count even/odd
Count positive/negative
Reverse
Copy array
Update elements
Find frequency
```

এগুলোই পরে **Searching, Sorting এবং Data Structures**-এর foundation হবে।


----

# 🚀 Lesson 31 — Array Traversal

আজ আমরা শিখব **Array Traversal**।

> **Traversal মানে হলো array-এর প্রতিটি element একে একে visit/process করা।**

Array:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

Traversal করলে:

```text
10 → 20 → 30 → 40 → 50
```

---

# 1. সবচেয়ে গুরুত্বপূর্ণ Traversal Pattern ⭐

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", numbers[i]);
}
```

এটাই array traversal-এর basic pattern।

আর যদি size variable থাকে:

```c
int size = 5;

for (int i = 0; i < size; i++) {
    printf("%d ", numbers[i]);
}
```

---

# 2. Index কীভাবে পরিবর্তন হচ্ছে?

ধরো:

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

Loop:

```c
for (int i = 0; i < 5; i++)
```

তাহলে:

```text
i = 0 → numbers[0] → 10
i = 1 → numbers[1] → 20
i = 2 → numbers[2] → 30
i = 3 → numbers[3] → 40
i = 4 → numbers[4] → 50
```

তারপর:

```text
i = 5
```

কিন্তু condition:

```c
i < 5
```

false।

Loop শেষ।

---

# 3. Full Program

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

---

# 4. Traversal + Sum

Traversal শুধু print করার জন্য নয়।

প্রতিটি element-এর উপর calculation করতে পারি।

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int sum = 0;

    for (int i = 0; i < size; i++) {
        sum += numbers[i];
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Output:

```text
Sum = 150
```

---

# 5. Traversal + Even Numbers

শুধু even numbers print করি:

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 15, 22, 31, 40, 57};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    for (int i = 0; i < size; i++) {

        if (numbers[i] % 2 == 0) {
            printf("%d ", numbers[i]);
        }
    }

    return 0;
}
```

Output:

```text
10 22 40
```

---

# 6. Odd Numbers

```c
for (int i = 0; i < size; i++) {

    if (numbers[i] % 2 != 0) {
        printf("%d ", numbers[i]);
    }
}
```

Example output:

```text
15 31 57
```

---

# 7. Count Even Numbers

এবার print না করে count করব।

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 15, 22, 31, 40, 57};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int count = 0;

    for (int i = 0; i < size; i++) {

        if (numbers[i] % 2 == 0) {
            count++;
        }
    }

    printf("Even = %d\n", count);

    return 0;
}
```

Output:

```text
Even = 3
```

---

# 8. Count Odd Numbers

```c
int count = 0;

for (int i = 0; i < size; i++) {

    if (numbers[i] % 2 != 0) {
        count++;
    }
}

printf("Odd = %d\n", count);
```

---

# 9. Positive এবং Negative Count

```c
#include <stdio.h>

int main() {

    int numbers[] = {-5, 10, -3, 8, 0, -7, 12};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int positive = 0;
    int negative = 0;

    for (int i = 0; i < size; i++) {

        if (numbers[i] > 0) {
            positive++;
        }
        else if (numbers[i] < 0) {
            negative++;
        }
    }

    printf("Positive = %d\n", positive);
    printf("Negative = %d\n", negative);

    return 0;
}
```

Output:

```text
Positive = 3
Negative = 3
```

`0` কোনো positive বা negative নয়।

---

# 10. Find Maximum

Traversal-এর সবচেয়ে common problem:

```c
#include <stdio.h>

int main() {

    int numbers[] = {25, 10, 80, 45, 60};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int max = numbers[0];

    for (int i = 1; i < size; i++) {

        if (numbers[i] > max) {
            max = numbers[i];
        }
    }

    printf("Maximum = %d\n", max);

    return 0;
}
```

Output:

```text
Maximum = 80
```

---

# 11. Find Minimum

```c
int min = numbers[0];

for (int i = 1; i < size; i++) {

    if (numbers[i] < min) {
        min = numbers[i];
    }
}

printf("Minimum = %d\n", min);
```

---

# 12. কেন `i = 1` থেকে শুরু?

কারণ:

```c
int max = numbers[0];
```

আমরা already প্রথম element-কে maximum ধরে নিয়েছি।

তাই comparison শুরু হবে দ্বিতীয় element থেকে:

```text
numbers[1]
numbers[2]
numbers[3]
...
```

---

# 13. Average

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int sum = 0;

    for (int i = 0; i < size; i++) {
        sum += numbers[i];
    }

    double average = (double)sum / size;

    printf("Average = %.2f\n", average);

    return 0;
}
```

Output:

```text
Average = 30.00
```

এখানে:

```c
(double)sum
```

ব্যবহার করে integer division এড়ানো হয়েছে।

---

# 14. Reverse Traversal

Forward:

```text
0 → 1 → 2 → 3 → 4
```

Reverse:

```text
4 → 3 → 2 → 1 → 0
```

Code:

```c
for (int i = size - 1; i >= 0; i--) {
    printf("%d ", numbers[i]);
}
```

Example:

```text
10 20 30 40 50
```

Output:

```text
50 40 30 20 10
```

---

# 15. Array Modify করা

Traversal-এর সময় element পরিবর্তনও করা যায়।

ধরো সব number-এর সঙ্গে `5` যোগ করব:

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    for (int i = 0; i < size; i++) {
        numbers[i] += 5;
    }

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
15 25 35 45 55
```

---

# 16. সব Element Double করা

```c
for (int i = 0; i < size; i++) {
    numbers[i] *= 2;
}
```

যদি আগে:

```text
10 20 30
```

হয়, পরে:

```text
20 40 60
```

---

# 17. Array Copy করা

একটি array থেকে অন্য array:

```c
#include <stdio.h>

int main() {

    int source[] = {10, 20, 30, 40, 50};
    int copy[5];

    for (int i = 0; i < 5; i++) {
        copy[i] = source[i];
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", copy[i]);
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

---

# 18. Array Reverse করে নতুন Array বানানো

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 40, 50};
    int reversed[5];

    for (int i = 0; i < 5; i++) {
        reversed[i] = numbers[4 - i];
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", reversed[i]);
    }

    return 0;
}
```

Output:

```text
50 40 30 20 10
```

---

# 19. User Input + Traversal

```c
#include <stdio.h>

int main() {

    int numbers[5];

    for (int i = 0; i < 5; i++) {

        printf("Enter number %d: ", i + 1);
        scanf("%d", &numbers[i]);
    }

    printf("Numbers: ");

    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Possible input:

```text
10
20
30
40
50
```

Output:

```text
Numbers: 10 20 30 40 50
```

---

# 20. Traversal-এর General Formula ⭐

যখন array process করবে, এই structure মাথায় রাখো:

```c
for (int i = 0; i < size; i++) {

    // array[i] নিয়ে কাজ
}
```

তারপর কাজটা বদলাবে।

### Print:

```c
printf("%d", array[i]);
```

### Sum:

```c
sum += array[i];
```

### Count:

```c
count++;
```

### Modify:

```c
array[i] *= 2;
```

### Condition:

```c
if (array[i] > 50)
```

এটাই array programming-এর fundamental pattern।

---

# 21. একাধিক কাজ এক traversal-এ

ধরো একই সঙ্গে:

- Sum
    
- Maximum
    
- Even count
    

করতে চাই।

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 25, 40, 15, 80};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int sum = 0;
    int evenCount = 0;
    int max = numbers[0];

    for (int i = 0; i < size; i++) {

        sum += numbers[i];

        if (numbers[i] % 2 == 0) {
            evenCount++;
        }

        if (numbers[i] > max) {
            max = numbers[i];
        }
    }

    printf("Sum = %d\n", sum);
    printf("Even = %d\n", evenCount);
    printf("Max = %d\n", max);

    return 0;
}
```

Output:

```text
Sum = 170
Even = 3
Max = 80
```

একটি loop-এই তিনটি কাজ হয়ে গেল।

---

# 22. Frequency Counting-এর Basic Idea

ধরো:

```text
2 5 2 8 2 5
```

`2` কতবার আছে?

Traversal করে count করা যায়:

```c
int count = 0;

for (int i = 0; i < size; i++) {

    if (numbers[i] == 2) {
        count++;
    }
}
```

Output:

```text
2 appears 3 times
```

এটাই searching/frequency problems-এর foundation।

---

# 23. `break` দিয়ে Traversal Stop করা

যদি প্রথম `50` পেলেই stop করতে চাই:

```c
for (int i = 0; i < size; i++) {

    if (numbers[i] == 50) {
        printf("Found\n");
        break;
    }
}
```

`break` encounter করলে loop শেষ হয়ে যায়।

---

# 24. `continue` দিয়ে Element Skip

Negative numbers বাদ দিয়ে শুধু positive print:

```c
for (int i = 0; i < size; i++) {

    if (numbers[i] < 0) {
        continue;
    }

    printf("%d ", numbers[i]);
}
```

`continue` current iteration skip করে পরের iteration-এ যায়।

---

# 25. Common Mistake ❌

Array:

```c
int numbers[5];
```

ভুল:

```c
for (int i = 0; i <= 5; i++)
```

কারণ `i == 5` হলে:

```c
numbers[5]
```

হয়ে যাবে।

সঠিক:

```c
for (int i = 0; i < 5; i++)
```

অথবা:

```c
for (int i = 0; i < size; i++)
```

---

# 26. আরেকটি Common Mistake ❌

```c
int numbers[5];

for (int i = 0; i < 5; i++) {
    printf("%d", numbers[i]);
}
```

এখানে array initialize/input করা হয়নি।

Local automatic array-এর uninitialized elements-এর value নির্ভরযোগ্যভাবে ধরে নেওয়া যাবে না।

তাই আগে:

```c
int numbers[5] = {0};
```

অথবা input:

```c
scanf("%d", &numbers[i]);
```

দাও।

---

# 🧪 Practice 1

এই array থেকে শুধু `50`-এর বেশি numbers print করো:

```c
int numbers[] = {10, 60, 25, 80, 45, 100, 30};
```

Expected:

```text
60 80 100
```

---

# 🧪 Practice 2

এই array-তে কতগুলো even number আছে বের করো:

```c
int numbers[] = {12, 7, 8, 19, 22, 31, 44};
```

Expected:

```text
Even = 4
```

---

# 🧪 Practice 3

Array-এর সব element-এর square করে array-তে store করো।

Input:

```text
2 3 4 5
```

Output:

```text
4 9 16 25
```

Hint:

```c
numbers[i] = numbers[i] * numbers[i];
```

---

# 🔥 Challenge — Second Largest

এই array:

```c
int numbers[] = {12, 45, 7, 89, 23, 56, 10};
```

Expected:

```text
Largest = 89
Second Largest = 56
```

একটি traversal দিয়ে করার চেষ্টা করো।

---

# 🧠 আজকের Cheat Sheet

### Forward traversal

```c
for (int i = 0; i < size; i++) {
    // array[i]
}
```

### Reverse traversal

```c
for (int i = size - 1; i >= 0; i--) {
    // array[i]
}
```

### Sum

```c
sum += array[i];
```

### Count

```c
count++;
```

### Modify

```c
array[i] = ...;
```

### Condition

```c
if (array[i] > ...)
```

### Golden Rule ⭐

> **Array-এর উপর প্রায় যেকোনো basic operation শুরু হয় একটি traversal loop দিয়ে।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ⏳ Searching
33. ⏳ Sorting
34. ⏳ 2D Array / Matrix
35. ⏳ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 32: Searching

পরের lesson-এ আমরা array-এর মধ্যে কোনো নির্দিষ্ট value **খুঁজে বের করা** শিখব।

যেমন:

```text
Array: 10 25 40 15 80

Search: 40

Result:
Found at index 2
```

তারপর শিখব **Linear Search**, search না পাওয়া গেলে কী হবে, এবং কেন searching data structures-এর জন্য এত গুরুত্বপূর্ণ।

---

# 🚀 Lesson 32 — Searching in Array

আজ আমরা শিখব কীভাবে একটি array-এর মধ্যে নির্দিষ্ট কোনো value **খুঁজে বের করতে হয়**।

সবচেয়ে আগে শিখব:

> **Linear Search**

---

# 1. Searching কী?

ধরো array:

```c
int numbers[] = {10, 25, 40, 15, 80};
```

আমরা খুঁজতে চাই:

```text
40
```

তাহলে একে একে check করব:

```text
10 → ❌
25 → ❌
40 → ✅ Found!
```

এটাই searching।

---

# 2. Linear Search

**Linear Search** মানে হলো array-এর শুরু থেকে একে একে প্রতিটি element check করা।

```text
Array:
┌────┬────┬────┬────┬────┐
│ 10 │ 25 │ 40 │ 15 │ 80 │
└────┴────┴────┴────┴────┘
   ↑
 Check

   10 ❌
        25 ❌
             40 ✅
```

---

# 3. Basic Linear Search

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 25, 40, 15, 80};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int target = 40;
    int found = 0;

    for (int i = 0; i < size; i++) {

        if (numbers[i] == target) {
            found = 1;
            printf("Found at index %d\n", i);
            break;
        }
    }

    if (!found) {
        printf("Not found\n");
    }

    return 0;
}
```

Output:

```text
Found at index 2
```

---

# 4. `found` Variable কেন?

আমরা লিখেছি:

```c
int found = 0;
```

এর অর্থ:

```text
0 → এখনো পাওয়া যায়নি
1 → পাওয়া গেছে
```

যখন target পাওয়া যায়:

```c
found = 1;
```

শেষে:

```c
if (!found)
```

মানে:

```text
found যদি 0 হয়
```

তাহলে:

```text
Not found
```

---

# 5. `break` কেন?

এই অংশটি:

```c
if (numbers[i] == target) {
    found = 1;
    printf("Found at index %d\n", i);
    break;
}
```

Target পাওয়ার পর আর array-এর বাকি element check করার দরকার নেই।

তাই:

```c
break;
```

দিয়ে loop stop করি।

---

# 6. Search না পাওয়া গেলে

Array:

```text
10 25 40 15 80
```

Search:

```text
100
```

কোনোটিই match করবে না।

Output:

```text
Not found
```

---

# 7. User-এর কাছ থেকে Search Value নেওয়া

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 25, 40, 15, 80};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int target;

    printf("Enter number to search: ");
    scanf("%d", &target);

    int found = 0;

    for (int i = 0; i < size; i++) {

        if (numbers[i] == target) {
            printf("Found at index %d\n", i);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Not found\n");
    }

    return 0;
}
```

Input:

```text
40
```

Output:

```text
Found at index 2
```

---

# 8. প্রথম Occurrence

ধরো:

```text
10 20 30 20 40
```

Search:

```text
20
```

20 দুইবার আছে:

```text
10 20 30 20 40
    ↑       ↑
```

সাধারণ linear search-এ `break` থাকলে প্রথমটিই পাওয়া যাবে:

```text
Found at index 1
```

---

# 9. সব Occurrence খুঁজতে চাইলে

`break` ব্যবহার করব না।

```c
#include <stdio.h>

int main() {

    int numbers[] = {10, 20, 30, 20, 40, 20};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int target = 20;
    int count = 0;

    for (int i = 0; i < size; i++) {

        if (numbers[i] == target) {
            printf("Found at index %d\n", i);
            count++;
        }
    }

    printf("Total occurrences = %d\n", count);

    return 0;
}
```

Output:

```text
Found at index 1
Found at index 3
Found at index 5
Total occurrences = 3
```

---

# 10. শুধু Count করতে চাইলে

```c
int count = 0;

for (int i = 0; i < size; i++) {

    if (numbers[i] == target) {
        count++;
    }
}

printf("Found %d times\n", count);
```

---

# 11. Search Function বানানো

এখন Functions-এর knowledge ব্যবহার করি।

```c
int search(int numbers[], int size, int target) {

    for (int i = 0; i < size; i++) {

        if (numbers[i] == target) {
            return i;
        }
    }

    return -1;
}
```

তারপর:

```c
#include <stdio.h>

int search(int numbers[], int size, int target) {

    for (int i = 0; i < size; i++) {

        if (numbers[i] == target) {
            return i;
        }
    }

    return -1;
}

int main() {

    int numbers[] = {10, 25, 40, 15, 80};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    int target = 40;

    int result = search(numbers, size, target);

    if (result != -1) {
        printf("Found at index %d\n", result);
    }
    else {
        printf("Not found\n");
    }

    return 0;
}
```

Output:

```text
Found at index 2
```

---

# 12. `-1` কেন?

Array-এর valid index:

```text
0, 1, 2, 3, 4
```

`-1` valid index নয়।

তাই আমরা convention হিসেবে:

```text
0 বা positive → found
-1             → not found
```

ব্যবহার করতে পারি।

এটা খুব useful pattern।

---

# 13. Search Function-এর Logic

```text
search()
   ↓
প্রতিটি element check
   ↓
match?
 ┌───────┴───────┐
 YES             NO
 ↓                ↓
return index    continue
                  ↓
              শেষ পর্যন্ত
                  ↓
              return -1
```

---

# 14. Linear Search-এর Time Complexity

ধরো array-তে:

```text
1000 elements
```

Target প্রথম element হলে:

```text
1 comparison
```

Target শেষের দিকে হলে:

```text
1000 comparisons
```

তাই Linear Search-এর worst-case complexity:

```text
O(n)
```

এখানে `n` হলো array-এর number of elements।

Complexity এখন পুরোপুরি মুখস্থ করার দরকার নেই; idea বুঝে রাখো।

---

# 15. Search করার সময় Array Sorted হওয়া লাগে?

**না।**

Linear Search-এর জন্য array এমন হতে পারে:

```text
80 10 45 5 100 20
```

তবুও search করা যাবে।

---

# 16. Search-এর Example

Array:

```text
7 25 13 90 42
```

Target:

```text
90
```

Search process:

```text
7  → no
25 → no
13 → no
90 → YES
```

Index:

```text
3
```

---

# 17. Character Array-এ Search

```c
#include <stdio.h>

int main() {

    char letters[] = {'A', 'B', 'C', 'D', 'E'};

    int size = sizeof(letters) / sizeof(letters[0]);

    char target = 'C';

    for (int i = 0; i < size; i++) {

        if (letters[i] == target) {
            printf("Found at index %d\n", i);
            break;
        }
    }

    return 0;
}
```

Output:

```text
Found at index 2
```

Strings নিয়ে আমরা পরে বিস্তারিত করব।

---

# 18. Search + User Input

একটি complete beginner program:

```c
#include <stdio.h>

int main() {

    int numbers[5];

    printf("Enter 5 numbers:\n");

    for (int i = 0; i < 5; i++) {
        scanf("%d", &numbers[i]);
    }

    int target;

    printf("Enter number to search: ");
    scanf("%d", &target);

    int found = 0;

    for (int i = 0; i < 5; i++) {

        if (numbers[i] == target) {

            printf("Found at index %d\n", i);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Not found\n");
    }

    return 0;
}
```

---

# 19. Common Mistake ❌

Search করতে গিয়ে:

```c
if (numbers[i] = target)
```

লিখবে না।

এটা assignment।

সঠিক:

```c
if (numbers[i] == target)
```

এখানে:

```text
=   → assignment
==  → comparison
```

---

# 20. Common Mistake ❌

Loop:

```c
for (int i = 0; i <= size; i++)
```

এটা ভুল।

সঠিক:

```c
for (int i = 0; i < size; i++)
```

কারণ শেষ valid index:

```text
size - 1
```

---

# 21. Search-এর তিনটি গুরুত্বপূর্ণ Pattern ⭐

### Pattern 1 — First match

```c
for (int i = 0; i < size; i++) {
    if (array[i] == target) {
        printf("%d", i);
        break;
    }
}
```

### Pattern 2 — All matches

```c
for (int i = 0; i < size; i++) {
    if (array[i] == target) {
        printf("%d ", i);
    }
}
```

### Pattern 3 — Function

```c
int search(int array[], int size, int target) {

    for (int i = 0; i < size; i++) {

        if (array[i] == target) {
            return i;
        }
    }

    return -1;
}
```

তৃতীয় pattern-টা সবচেয়ে reusable।

---

# 🧪 Practice 1

এই array:

```c
int numbers[] = {15, 25, 35, 45, 55};
```

`45` search করো।

Expected:

```text
Found at index 3
```

---

# 🧪 Practice 2

এই array:

```c
int numbers[] = {10, 20, 10, 30, 10, 40};
```

`10` কতবার আছে বের করো।

Expected:

```text
3
```

---

# 🧪 Practice 3

User-এর কাছ থেকে:

1. 10টি number input নাও
    
2. একটি target input নাও
    
3. target-এর প্রথম index print করো
    
4. না পেলে `Not found` print করো
    

---

# 🔥 Challenge — All Positions

এই array:

```c
int numbers[] = {5, 10, 5, 20, 5, 30, 10};
```

Target:

```text
5
```

Output:

```text
Found at index 0
Found at index 2
Found at index 4
```

তারপর:

```text
Total = 3
```

---

# 🧠 আজকের Cheat Sheet

### Linear Search

```c
for (int i = 0; i < size; i++) {

    if (array[i] == target) {
        // found
    }
}
```

### First match

```c
break;
```

### Not found

```c
return -1;
```

### Count occurrences

```c
count++;
```

### Complexity

```text
Linear Search → O(n)
```

### সবচেয়ে গুরুত্বপূর্ণ ধারণা ⭐

> **Linear Search array-এর শুরু থেকে একে একে element check করে যতক্ষণ না target পাওয়া যায় বা array শেষ হয়।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ✅ Searching
33. ⏳ Sorting
34. ⏳ 2D Array / Matrix
35. ⏳ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 33: Sorting

এবার আমরা array-এর data **ছোট থেকে বড়** বা **বড় থেকে ছোট** সাজানো শিখব।

উদাহরণ:

```text
Before:
40 10 30 20 50

After:
10 20 30 40 50
```

প্রথমে **Bubble Sort** দিয়ে শুরু করব, তারপর কেন sorting algorithms-এর efficiency গুরুত্বপূর্ণ সেটা বুঝব।

---
# 🚀 Lesson 33 — Sorting

আজ আমরা শিখব **Array Sorting**।

> **Sorting মানে data-কে একটি নির্দিষ্ট order-এ সাজানো।**

সবচেয়ে common:

### Ascending

```text
10 20 30 40 50
```

### Descending

```text
50 40 30 20 10
```

আজ আমরা প্রথমে **Bubble Sort** শিখব।

---

# 1. Sorting কেন দরকার?

ধরো:

```text
45 12 89 23 7
```

এভাবে data রাখা আছে।

Sorting করলে:

```text
7 12 23 45 89
```

এতে পরে:

- Searching সহজ হতে পারে
    
- Minimum/maximum বোঝা সহজ হয়
    
- Data সুন্দরভাবে display করা যায়
    
- অনেক algorithm sorted data-এর সুবিধা নেয়
    

---

# 2. Bubble Sort কী?

Bubble Sort-এর মূল idea:

> **পাশাপাশি দুইটি element compare করো, ভুল order হলে swap করো।**

ধরো:

```text
40 10 30 20
```

প্রথম comparison:

```text
40 10
```

40 > 10, তাই swap:

```text
10 40 30 20
```

তারপর:

```text
40 30
```

swap:

```text
10 30 40 20
```

তারপর:

```text
40 20
```

swap:

```text
10 30 20 40
```

একটি pass শেষে সবচেয়ে বড় value ডানদিকে চলে যায়:

```text
10 30 20 40
          ↑
        largest
```

---

# 3. Swap কী?

দুটি variable:

```c
int a = 10;
int b = 20;
```

এগুলো swap করতে temporary variable ব্যবহার করা যায়:

```c
int temp;

temp = a;
a = b;
b = temp;
```

ফলে:

```text
Before:
a = 10
b = 20

After:
a = 20
b = 10
```

---

# 4. প্রথম Bubble Sort Code

```c
#include <stdio.h>

int main() {

    int numbers[] = {40, 10, 30, 20};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    for (int i = 0; i < size - 1; i++) {

        for (int j = 0; j < size - 1 - i; j++) {

            if (numbers[j] > numbers[j + 1]) {

                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;
            }
        }
    }

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
10 20 30 40
```

---

# 5. Nested Loop কেন?

Bubble Sort-এ:

```c
for (int i = 0; i < size - 1; i++)
```

এবং:

```c
for (int j = 0; j < size - 1 - i; j++)
```

দুটি loop আছে।

কারণ sorting-এর জন্য একাধিক **pass** দরকার হয়।

---

# 6. `i` কী করছে?

Outer loop:

```c
i
```

এটা pass count করে।

ধরো 5টি element:

```text
size = 5
```

তাহলে maximum:

```text
4 passes
```

কারণ:

```text
size - 1
```

---

# 7. `j` কী করছে?

Inner loop adjacent elements compare করে:

```text
numbers[j]
numbers[j + 1]
```

যেমন:

```text
j = 0
numbers[0] vs numbers[1]

j = 1
numbers[1] vs numbers[2]

j = 2
numbers[2] vs numbers[3]
```

---

# 8. প্রথম Pass বিস্তারিত

Array:

```text
40 10 30 20
```

### Step 1

```text
40 10 → swap
```

হয়:

```text
10 40 30 20
```

### Step 2

```text
40 30 → swap
```

হয়:

```text
10 30 40 20
```

### Step 3

```text
40 20 → swap
```

হয়:

```text
10 30 20 40
```

Pass শেষ:

```text
10 30 20 40
          ↑
        largest
```

---

# 9. দ্বিতীয় Pass

এখন শেষের `40` already correct position-এ।

তাই:

```text
10 30 20
```

এর মধ্যে কাজ করলেই হবে।

```text
10 30 → no swap
30 20 → swap
```

Result:

```text
10 20 30 40
```

---

# 10. কেন `size - 1 - i`?

এই অংশ:

```c
j < size - 1 - i
```

খুব গুরুত্বপূর্ণ।

প্রতিটি pass-এর শেষে একটি বড় element সঠিক জায়গায় চলে যায়।

তাই পরের pass-এ সেটাকে আবার compare করার প্রয়োজন নেই।

---

# 11. Ascending Sort

আমরা ব্যবহার করেছি:

```c
if (numbers[j] > numbers[j + 1])
```

অর্থাৎ:

```text
বাম > ডান
```

হলে swap।

ফলে:

```text
ছোট → বড়
```

অর্থাৎ ascending order।

---

# 12. Descending Sort

এবার:

```c
if (numbers[j] < numbers[j + 1])
```

ব্যবহার করো।

Complete:

```c
#include <stdio.h>

int main() {

    int numbers[] = {40, 10, 30, 20};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    for (int i = 0; i < size - 1; i++) {

        for (int j = 0; j < size - 1 - i; j++) {

            if (numbers[j] < numbers[j + 1]) {

                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;
            }
        }
    }

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Output:

```text
40 30 20 10
```

---

# 13. User Input নিয়ে Sort

এখন practical program:

```c
#include <stdio.h>

int main() {

    int numbers[5];

    printf("Enter 5 numbers:\n");

    for (int i = 0; i < 5; i++) {
        scanf("%d", &numbers[i]);
    }

    for (int i = 0; i < 5 - 1; i++) {

        for (int j = 0; j < 5 - 1 - i; j++) {

            if (numbers[j] > numbers[j + 1]) {

                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;
            }
        }
    }

    printf("Sorted: ");

    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

Input:

```text
50 20 40 10 30
```

Output:

```text
Sorted: 10 20 30 40 50
```

---

# 14. Bubble Sort Function বানানো

আমরা function ব্যবহার করতে পারি:

```c
void bubbleSort(int numbers[], int size) {

    for (int i = 0; i < size - 1; i++) {

        for (int j = 0; j < size - 1 - i; j++) {

            if (numbers[j] > numbers[j + 1]) {

                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;
            }
        }
    }
}
```

তারপর:

```c
int main() {

    int numbers[] = {50, 20, 40, 10, 30};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    bubbleSort(numbers, size);

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

---

# 15. Full Reusable Program

```c
#include <stdio.h>

void bubbleSort(int numbers[], int size) {

    for (int i = 0; i < size - 1; i++) {

        for (int j = 0; j < size - 1 - i; j++) {

            if (numbers[j] > numbers[j + 1]) {

                int temp = numbers[j];

                numbers[j] = numbers[j + 1];

                numbers[j + 1] = temp;
            }
        }
    }
}

int main() {

    int numbers[] = {50, 20, 40, 10, 30};

    int size = sizeof(numbers) / sizeof(numbers[0]);

    bubbleSort(numbers, size);

    printf("Sorted array: ");

    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }

    return 0;
}
```

---

# 16. একটি Important Observation 🔥

Bubble Sort array-টাকেই পরিবর্তন করে।

Before:

```text
50 20 40 10 30
```

After:

```text
10 20 30 40 50
```

আলাদা sorted array বানানো হয়নি।

একে বলা যায় **in-place sorting**।

---

# 17. Already Sorted Array

ধরো:

```text
10 20 30 40 50
```

এটা আগে থেকেই sorted।

Basic Bubble Sort তবুও multiple comparisons করতে পারে।

এটা optimize করা যায়।

---

# 18. Optimized Bubble Sort

একটি `swapped` variable ব্যবহার করা যায়:

```c
void bubbleSort(int numbers[], int size) {

    for (int i = 0; i < size - 1; i++) {

        int swapped = 0;

        for (int j = 0; j < size - 1 - i; j++) {

            if (numbers[j] > numbers[j + 1]) {

                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;

                swapped = 1;
            }
        }

        if (swapped == 0) {
            break;
        }
    }
}
```

যদি কোনো pass-এ একবারও swap না হয়:

```text
array already sorted
```

তাই loop stop করা যায়।

---

# 19. Bubble Sort Complexity

Basic Bubble Sort-এর worst-case time complexity:

```text
O(n²)
```

মানে elements বাড়লে কাজের পরিমাণ দ্রুত বাড়ে।

উদাহরণ হিসেবে ধারণা:

```text
n = 10
→ roughly quadratic amount of comparisons

n = 100
→ much more work

n = 1000
→ significantly more
```

তাই বড় data-এর জন্য Bubble Sort সাধারণত efficient choice নয়।

---

# 20. Bubble Sort কখন শেখা দরকার?

বাস্তব project-এ সবসময় Bubble Sort ব্যবহার করা হয় না।

তবুও শেখা গুরুত্বপূর্ণ কারণ এতে:

- Nested loops
    
- Comparison
    
- Swapping
    
- Array manipulation
    
- Algorithmic thinking
    

এসব খুব ভালোভাবে বোঝা যায়।

---

# 21. Sorting-এর Basic Pattern ⭐

মনে রাখো:

```c
for (int i = 0; i < size - 1; i++) {

    for (int j = 0; j < size - 1 - i; j++) {

        if (array[j] > array[j + 1]) {

            // swap
        }
    }
}
```

তারপর swap:

```c
int temp = array[j];
array[j] = array[j + 1];
array[j + 1] = temp;
```

---

# 22. Sorting-এর পরে Searching

এখন একটি গুরুত্বপূর্ণ connection:

আমরা আগে শিখেছি:

```text
Lesson 32
Linear Search
```

এখন:

```text
Lesson 33
Sorting
```

পরের দিকে sorted array-এর জন্য আরও efficient searching algorithm আছে:

> **Binary Search**

উদাহরণ:

```text
Sorted:
10 20 30 40 50 60 70 80
```

তখন মাঝখান থেকে search শুরু করা যায়।

Binary Search আমরা পরে data structures-এর context-এও দেখব।

---

# 🧪 Practice 1

এই array ascending order-এ sort করো:

```c
int numbers[] = {50, 10, 40, 20, 30};
```

Expected:

```text
10 20 30 40 50
```

---

# 🧪 Practice 2

Descending order:

```c
int numbers[] = {15, 80, 25, 60, 10};
```

Expected:

```text
80 60 25 15 10
```

---

# 🧪 Practice 3

User-এর কাছ থেকে 10টি number input নিয়ে ascending order-এ sort করো।

---

# 🔥 Challenge — Sort + Search

প্রথমে:

```text
10টি number input
```

তারপর:

```text
ascending sort
```

তারপর:

```text
target input
```

তারপর target search করো।

Output-এর মতো:

```text
Sorted:
10 20 30 40 50 60 70 80

Search: 50

Found at index 4
```

---

# 🧠 আজকের Cheat Sheet

### Ascending

```c
if (array[j] > array[j + 1])
```

### Descending

```c
if (array[j] < array[j + 1])
```

### Swap

```c
int temp = array[j];
array[j] = array[j + 1];
array[j + 1] = temp;
```

### Bubble Sort

```text
Adjacent comparison
       ↓
Wrong order?
       ↓
Swap
       ↓
Repeat
```

### Complexity

```text
Bubble Sort → O(n²)
```

### সবচেয়ে গুরুত্বপূর্ণ ধারণা ⭐

> **Bubble Sort-এ প্রতিটি pass-এর মাধ্যমে বড় element-গুলো ধীরে ধীরে array-এর ডানদিকে চলে যায়।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ✅ Searching
33. ✅ Sorting
34. ⏳ 2D Array / Matrix
35. ⏳ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 34: 2D Array / Matrix

এবার আমরা এক-dimensional array থেকে **দুই-dimensional array**-এ যাব।

যেমন:

```c
int matrix[3][3];
```

এবং শিখব:

```text
Rows & columns
Matrix input/output
Nested loops
Matrix addition
Diagonal
Transpose
```

এখান থেকেই C-এর **matrix এবং nested-loop problems** শুরু হবে।

----
# 🚀 Lesson 34 — 2D Array / Matrix

আজ আমরা শিখব **2D Array**, যাকে সাধারণভাবে **Matrix** হিসেবেও দেখা যায়।

এটা 1D array-এর পরের গুরুত্বপূর্ণ step।

---

# 1. 2D Array কী?

1D Array:

```text
10 20 30 40
```

2D Array হলো **row + column**:

```text
10 20 30
40 50 60
70 80 90
```

এখানে:

```text
3 rows
3 columns
```

C-তে:

```c
int matrix[3][3];
```

---

# 2. 2D Array-এর Structure

ধরো:

```c
int matrix[3][3] = {
    {10, 20, 30},
    {40, 50, 60},
    {70, 80, 90}
};
```

এভাবে দেখতে পারো:

```text
          Column
          0    1    2
       ┌────┬────┬────┐
Row 0  │ 10 │ 20 │ 30 │
       ├────┼────┼────┤
Row 1  │ 40 │ 50 │ 60 │
       ├────┼────┼────┤
Row 2  │ 70 │ 80 │ 90 │
       └────┴────┴────┘
```

---

# 3. Declaration

Syntax:

```c
data_type array_name[rows][columns];
```

Example:

```c
int matrix[3][4];
```

মানে:

```text
3 rows
4 columns
```

মোট element:

```text
3 × 4 = 12
```

---

# 4. Initialization

```c
int matrix[2][3] = {
    {10, 20, 30},
    {40, 50, 60}
};
```

এখানে:

```text
Row 0 → 10 20 30
Row 1 → 40 50 60
```

---

# 5. Element Access

2D array-তে দুইটি index লাগে:

```c
matrix[row][column]
```

যেমন:

```c
matrix[0][0]
```

মানে:

```text
প্রথম row
প্রথম column
```

Value:

```text
10
```

---

# 6. আরও কিছু Example

```c
matrix[0][1]
```

= `20`

```c
matrix[1][0]
```

= `40`

```c
matrix[2][2]
```

= `90`

অর্থাৎ:

```text
matrix[row][column]
```

---

# 7. 2D Array Print করার জন্য Nested Loop ⭐

এখানে nested loop খুব গুরুত্বপূর্ণ।

```c
#include <stdio.h>

int main() {

    int matrix[3][3] = {
        {10, 20, 30},
        {40, 50, 60},
        {70, 80, 90}
    };

    for (int i = 0; i < 3; i++) {

        for (int j = 0; j < 3; j++) {

            printf("%d ", matrix[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
10 20 30
40 50 60
70 80 90
```

---

# 8. `i` এবং `j` কী করছে?

Outer loop:

```c
for (int i = 0; i < 3; i++)
```

সাধারণত **row** control করে।

Inner loop:

```c
for (int j = 0; j < 3; j++)
```

সাধারণত **column** control করে।

তাই:

```text
i → row
j → column
```

এটা খুব ভালোভাবে মনে রাখো।

---

# 9. Traversal কীভাবে হচ্ছে?

Matrix:

```text
10 20 30
40 50 60
70 80 90
```

Traversal:

```text
matrix[0][0] → 10
matrix[0][1] → 20
matrix[0][2] → 30

matrix[1][0] → 40
matrix[1][1] → 50
matrix[1][2] → 60

matrix[2][0] → 70
matrix[2][1] → 80
matrix[2][2] → 90
```

---

# 10. User Input

User-এর কাছ থেকে matrix input নেওয়া:

```c
#include <stdio.h>

int main() {

    int matrix[2][3];

    printf("Enter 6 numbers:\n");

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 3; j++) {

            scanf("%d", &matrix[i][j]);
        }
    }

    printf("Matrix:\n");

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 3; j++) {

            printf("%d ", matrix[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Input:

```text
1 2 3
4 5 6
```

Output:

```text
1 2 3
4 5 6
```

---

# 11. Matrix-এর সব Element-এর Sum

```c
#include <stdio.h>

int main() {

    int matrix[2][3] = {
        {10, 20, 30},
        {40, 50, 60}
    };

    int sum = 0;

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 3; j++) {

            sum += matrix[i][j];
        }
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Output:

```text
Sum = 210
```

---

# 12. Row-wise Sum

ধরো:

```text
10 20 30
40 50 60
```

প্রথম row-এর sum:

```text
10 + 20 + 30 = 60
```

দ্বিতীয়:

```text
40 + 50 + 60 = 150
```

Code:

```c
#include <stdio.h>

int main() {

    int matrix[2][3] = {
        {10, 20, 30},
        {40, 50, 60}
    };

    for (int i = 0; i < 2; i++) {

        int sum = 0;

        for (int j = 0; j < 3; j++) {
            sum += matrix[i][j];
        }

        printf("Row %d sum = %d\n", i, sum);
    }

    return 0;
}
```

Output:

```text
Row 0 sum = 60
Row 1 sum = 150
```

---

# 13. Column-wise Sum

এবার column:

```text
10 20 30
40 50 60
```

Column 0:

```text
10 + 40 = 50
```

Column 1:

```text
20 + 50 = 70
```

Column 2:

```text
30 + 60 = 90
```

Code:

```c
#include <stdio.h>

int main() {

    int matrix[2][3] = {
        {10, 20, 30},
        {40, 50, 60}
    };

    for (int j = 0; j < 3; j++) {

        int sum = 0;

        for (int i = 0; i < 2; i++) {
            sum += matrix[i][j];
        }

        printf("Column %d sum = %d\n", j, sum);
    }

    return 0;
}
```

Output:

```text
Column 0 sum = 50
Column 1 sum = 70
Column 2 sum = 90
```

খেয়াল করো:

```text
Row sum    → i বাইরে, j ভিতরে
Column sum → j বাইরে, i ভিতরে
```

---

# 14. Main Diagonal

Square matrix:

```text
10 20 30
40 50 60
70 80 90
```

Main diagonal:

```text
10
   50
      90
```

অর্থাৎ:

```text
matrix[0][0]
matrix[1][1]
matrix[2][2]
```

Pattern:

```c
matrix[i][i]
```

---

# 15. Main Diagonal Print

```c
#include <stdio.h>

int main() {

    int matrix[3][3] = {
        {10, 20, 30},
        {40, 50, 60},
        {70, 80, 90}
    };

    for (int i = 0; i < 3; i++) {
        printf("%d ", matrix[i][i]);
    }

    return 0;
}
```

Output:

```text
10 50 90
```

---

# 16. Main Diagonal Sum

```c
int sum = 0;

for (int i = 0; i < 3; i++) {
    sum += matrix[i][i];
}

printf("Diagonal sum = %d\n", sum);
```

Output:

```text
Diagonal sum = 150
```

---

# 17. Secondary Diagonal

Matrix:

```text
10 20 30
40 50 60
70 80 90
```

Secondary diagonal:

```text
      30
   50
70
```

Indices:

```text
matrix[0][2]
matrix[1][1]
matrix[2][0]
```

Pattern:

```c
matrix[i][size - 1 - i]
```

---

# 18. Secondary Diagonal Code

```c
#include <stdio.h>

int main() {

    int matrix[3][3] = {
        {10, 20, 30},
        {40, 50, 60},
        {70, 80, 90}
    };

    for (int i = 0; i < 3; i++) {
        printf("%d ", matrix[i][2 - i]);
    }

    return 0;
}
```

Output:

```text
30 50 70
```

---

# 19. Matrix Addition 🔥

দুটি matrix:

```text
A:
1 2
3 4
```

```text
B:
5 6
7 8
```

Addition:

```text
6  8
10 12
```

Rule:

```text
C[i][j] = A[i][j] + B[i][j]
```

---

# 20. Matrix Addition Code

```c
#include <stdio.h>

int main() {

    int A[2][2] = {
        {1, 2},
        {3, 4}
    };

    int B[2][2] = {
        {5, 6},
        {7, 8}
    };

    int C[2][2];

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 2; j++) {

            C[i][j] = A[i][j] + B[i][j];
        }
    }

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 2; j++) {

            printf("%d ", C[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
6 8
10 12
```

---

# 21. Matrix Subtraction

একইভাবে:

```c
C[i][j] = A[i][j] - B[i][j];
```

Example:

```text
A:
10 20
30 40

B:
1 2
3 4
```

Result:

```text
9 18
27 36
```

---

# 22. Transpose

Matrix:

```text
1 2 3
4 5 6
```

Transpose:

```text
1 4
2 5
3 6
```

অর্থাৎ:

```text
row → column
column → row
```

Formula:

```c
transpose[j][i] = matrix[i][j];
```

---

# 23. Transpose Code

```c
#include <stdio.h>

int main() {

    int matrix[2][3] = {
        {1, 2, 3},
        {4, 5, 6}
    };

    int transpose[3][2];

    for (int i = 0; i < 2; i++) {

        for (int j = 0; j < 3; j++) {

            transpose[j][i] = matrix[i][j];
        }
    }

    for (int i = 0; i < 3; i++) {

        for (int j = 0; j < 2; j++) {

            printf("%d ", transpose[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
1 4
2 5
3 6
```

---

# 24. Matrix Multiplication — Basic Idea

এটা একটু advanced, কিন্তু concept জানা দরকার।

যদি:

```text
A = 2×3
B = 3×2
```

তাহলে:

```text
A × B
```

এর result হবে:

```text
2×2
```

Matrix multiplication-এ তিনটি loop লাগে।

Basic pattern:

```c
for (int i = 0; i < rowsA; i++) {

    for (int j = 0; j < colsB; j++) {

        result[i][j] = 0;

        for (int k = 0; k < colsA; k++) {

            result[i][j] += A[i][k] * B[k][j];
        }
    }
}
```

এটা আপাতত শুধু pattern হিসেবে রাখো। পরে আবার বিস্তারিত practice করব।

---

# 25. 2D Array-এর সবচেয়ে গুরুত্বপূর্ণ Pattern ⭐

সাধারণ traversal:

```c
for (int i = 0; i < rows; i++) {

    for (int j = 0; j < cols; j++) {

        printf("%d ", matrix[i][j]);
    }

    printf("\n");
}
```

মনে রাখো:

```text
i → row
j → column
```

---

# 26. 1D বনাম 2D

|1D|2D|
|---|---|
|`array[i]`|`matrix[i][j]`|
|একটি index|দুইটি index|
|সাধারণত একটি line|rows + columns|
|একটি loop|সাধারণত nested loop|

---

# 27. Common Mistake ❌

যদি:

```c
int matrix[3][4];
```

তাহলে:

```text
rows = 3
columns = 4
```

valid row:

```text
0, 1, 2
```

valid column:

```text
0, 1, 2, 3
```

`matrix[3][0]` valid নয়।

---

# 28. Common Mistake ❌

এটা:

```c
for (int i = 0; i < 3; i++) {

    for (int j = 0; j < 4; i++) {
```

ভুল।

Inner loop-এ সাধারণত:

```c
j++
```

হবে:

```c
for (int j = 0; j < 4; j++)
```

---

# 29. Practical Example — Student Marks

ধরো:

```text
3 students
4 subjects
```

তাহলে:

```c
int marks[3][4];
```

এখানে:

```text
row → student
column → subject
```

Input:

```text
80 70 90 85
60 75 80 70
90 95 85 90
```

প্রতিটি row-এর sum বের করে student-এর total marks বের করা যায়।

এটা বাস্তব project-এ খুব useful pattern।

---

# 🧪 Practice 1 — Matrix Print

এই matrix print করো:

```c
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

Expected:

```text
1 2 3
4 5 6
7 8 9
```

---

# 🧪 Practice 2 — Total Sum

এই matrix-এর সব element-এর sum বের করো:

```c
int matrix[2][3] = {
    {10, 20, 30},
    {40, 50, 60}
};
```

Expected:

```text
210
```

---

# 🧪 Practice 3 — Diagonal

এই matrix-এর main diagonal print করো:

```c
int matrix[3][3] = {
    {5, 2, 8},
    {4, 9, 1},
    {7, 6, 3}
};
```

Expected:

```text
5 9 3
```

---

# 🔥 Challenge — Matrix Addition

দুটি `3×3` matrix user-এর কাছ থেকে input নাও এবং তাদের যোগফল print করো।

Expected structure:

```text
Enter Matrix A:
...

Enter Matrix B:
...

Result:
...
```

---

# 🧠 আজকের Cheat Sheet

### Declaration

```c
int matrix[rows][columns];
```

### Access

```c
matrix[i][j]
```

### Traversal

```c
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < columns; j++) {
        // matrix[i][j]
    }
}
```

### Main diagonal

```c
matrix[i][i]
```

### Secondary diagonal

```c
matrix[i][size - 1 - i]
```

### Matrix addition

```c
C[i][j] = A[i][j] + B[i][j];
```

### Transpose

```c
transpose[j][i] = matrix[i][j];
```

### Golden Rule ⭐

> **2D array-এর ক্ষেত্রে সাধারণত outer loop row এবং inner loop column control করে।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ✅ Searching
33. ✅ Sorting
34. ✅ 2D Array / Matrix
35. ⏳ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 35: Strings

এবার C-এর খুব গুরুত্বপূর্ণ একটি topic:

```c
char name[] = "Rahim";
```

আমরা শিখব:

- String কী
    
- Character array কী
    
- `'\0'` null character
    
- String input/output
    
- `fgets()`
    
- String-এর length
    
- String traversal
    
- String comparison-এর basic ধারণা
    

**String বোঝার জন্য character array এবং `'\0'` ভালোভাবে বোঝা সবচেয়ে গুরুত্বপূর্ণ।**

----

# 🚀 Lesson 35 — Strings in C

আজ থেকে C-এর সবচেয়ে গুরুত্বপূর্ণ topicগুলোর একটি শুরু করছি:

> **String**

C-তে String আলাদা কোনো built-in data type নয়। String মূলত **একটি character array**, যার শেষে বিশেষ `'\0'` character থাকে।

---

# 1. Character কী?

একটি মাত্র character রাখার জন্য:

```c
char ch = 'A';
```

খেয়াল করো:

```text
'A'
```

এখানে **single quotation** ব্যবহার হয়েছে।

আর:

```c
char name[] = "Rahim";
```

এখানে **double quotation** ব্যবহার হয়েছে, কারণ এটি একটি string।

---

# 2. String কী?

```c
char name[] = "Rahim";
```

Memory-তে এটাকে ধারণাগতভাবে এমন ভাবতে পারো:

```text
┌─────┬─────┬─────┬─────┬─────┬──────┐
│  R  │  a  │  h  │  i  │  m  │ '\0' │
└─────┴─────┴─────┴─────┴─────┴──────┘
   0     1     2     3     4      5
```

শেষের:

```c
'\0'
```

কে বলা হয় **null character**।

এটি C-কে জানায়:

> "এখানেই string শেষ।"

---

# 3. String Declaration

দুটি common way:

```c
char name[20];
```

এটা একটি character array, যেখানে সর্বোচ্চ 19টি character-এর string এবং শেষে `'\0'` রাখা যায়।

অথবা:

```c
char name[] = "Rahim";
```

Compiler প্রয়োজনীয় size নির্ধারণ করবে।

`"Rahim"`-এর জন্য:

```text
5 characters + '\0'
= 6 positions
```

---

# 4. String Print

```c
#include <stdio.h>

int main() {

    char name[] = "Rahim";

    printf("%s\n", name);

    return 0;
}
```

Output:

```text
Rahim
```

String print করার format specifier:

```text
%s
```

---

# 5. `%c` বনাম `%s`

### একটি character:

```c
char ch = 'A';

printf("%c", ch);
```

Output:

```text
A
```

### একটি string:

```c
char name[] = "Rahim";

printf("%s", name);
```

Output:

```text
Rahim
```

তাই:

```text
%c → character
%s → string
```

---

# 6. String-এর প্রতিটি Character দেখা

String আসলে character array হওয়ায় index ব্যবহার করা যায়।

```c
#include <stdio.h>

int main() {

    char name[] = "Rahim";

    printf("%c\n", name[0]);
    printf("%c\n", name[1]);
    printf("%c\n", name[2]);
    printf("%c\n", name[3]);
    printf("%c\n", name[4]);

    return 0;
}
```

Output:

```text
R
a
h
i
m
```

---

# 7. String Traversal ⭐

String-এর প্রতিটি character loop দিয়ে দেখতে পারি।

```c
#include <stdio.h>

int main() {

    char name[] = "Rahim";

    for (int i = 0; name[i] != '\0'; i++) {
        printf("%c\n", name[i]);
    }

    return 0;
}
```

Output:

```text
R
a
h
i
m
```

সবচেয়ে গুরুত্বপূর্ণ condition:

```c
name[i] != '\0'
```

মানে:

> যতক্ষণ string শেষ হয়নি, ততক্ষণ loop চালাও।

---

# 8. `'\0'` কেন এত গুরুত্বপূর্ণ?

ধরো:

```text
Rahim
```

C internally ধারণাগতভাবে রাখে:

```text
R a h i m \0
```

যখন `%s` ব্যবহার করো:

```c
printf("%s", name);
```

C characterগুলো print করতে থাকে যতক্ষণ না:

```c
'\0'
```

পায়।

---

# 9. String-এর Length

আগের example:

```text
Rahim
```

এখানে actual characters:

```text
5
```

কিন্তু array-তে জায়গা:

```text
6
```

কারণ:

```text
5 characters + '\0'
```

---

# 10. `sizeof()` দিয়ে Size

```c
#include <stdio.h>

int main() {

    char name[] = "Rahim";

    printf("%zu\n", sizeof(name));

    return 0;
}
```

Output:

```text
6
```

কারণ `sizeof()` `'\0'`-সহ পুরো array-এর size দেয়।

---

# 11. `strlen()` দিয়ে String Length

C-এর `<string.h>` library-তে `strlen()` আছে।

```c
#include <stdio.h>
#include <string.h>

int main() {

    char name[] = "Rahim";

    printf("%zu\n", strlen(name));

    return 0;
}
```

Output:

```text
5
```

এখানে:

```text
sizeof(name) → 6
strlen(name) → 5
```

কারণ `strlen()` null character-কে length-এর মধ্যে count করে না।

---

# 12. User Input — `scanf()`

একটি word input নিতে:

```c
#include <stdio.h>

int main() {

    char name[20];

    printf("Enter your name: ");
    scanf("%19s", name);

    printf("Hello, %s\n", name);

    return 0;
}
```

Input:

```text
Rahim
```

Output:

```text
Hello, Rahim
```

এখানে `%19s` ব্যবহার করে array-এর সীমার মধ্যে input রাখার চেষ্টা করা হচ্ছে।

---

# 13. `scanf("%s")`-এর সমস্যা

ধরো user input দিল:

```text
Rahim Ahmed
```

`scanf("%s", name)` সাধারণত প্রথম whitespace পর্যন্ত নেয়।

ফলে:

```text
Rahim
```

পাওয়া যাবে, পুরো:

```text
Rahim Ahmed
```

নয়।

---

# 14. পুরো Line Input — `fgets()` ⭐

একটি line বা spaces-সহ string নেওয়ার জন্য `fgets()` খুব useful।

```c
#include <stdio.h>

int main() {

    char name[50];

    printf("Enter your full name: ");
    fgets(name, sizeof(name), stdin);

    printf("Hello, %s", name);

    return 0;
}
```

Input:

```text
Rahim Ahmed
```

Output:

```text
Hello, Rahim Ahmed
```

---

# 15. `fgets()` কী করছে?

```c
fgets(name, sizeof(name), stdin);
```

এখানে:

```text
name
```

→ যেখানে input রাখা হবে

```text
sizeof(name)
```

→ maximum কতটা জায়গা ব্যবহার করা যাবে

```text
stdin
```

→ keyboard থেকে input

---

# 16. `fgets()`-এর একটি বিষয়

User Enter চাপলে `fgets()` অনেক ক্ষেত্রে newline `'\n'`-ও string-এর মধ্যে রেখে দিতে পারে।

যেমন:

```text
"Rahim\n"
```

তাই প্রয়োজনে newline remove করা যায়:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char name[50];

    fgets(name, sizeof(name), stdin);

    name[strcspn(name, "\n")] = '\0';

    printf("%s\n", name);

    return 0;
}
```

এটা এখনই পুরোপুরি মুখস্থ করার দরকার নেই। `strcspn()` আমরা পরের lesson-এ বিস্তারিত দেখব।

---

# 17. String-এর Character পরিবর্তন

String array হওয়ায় individual character পরিবর্তন করা যায়:

```c
#include <stdio.h>

int main() {

    char name[] = "Rahim";

    name[0] = 'K';

    printf("%s\n", name);

    return 0;
}
```

Output:

```text
Kahim
```

---

# 18. String Reverse — Basic Idea

ধরো:

```text
HELLO
```

Reverse:

```text
OLLEH
```

String-এর length বের করে শেষ থেকে শুরু করলে reverse করা যায়।

Basic idea:

```c
for (int i = length - 1; i >= 0; i--) {
    printf("%c", name[i]);
}
```

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char name[] = "HELLO";

    int length = strlen(name);

    for (int i = length - 1; i >= 0; i--) {
        printf("%c", name[i]);
    }

    return 0;
}
```

Output:

```text
OLLEH
```

---

# 19. String-এর Vowel Count

String:

```text
"education"
```

এর মধ্যে `a, e, i, o, u` count করতে পারি।

```c
#include <stdio.h>

int main() {

    char text[] = "education";

    int count = 0;

    for (int i = 0; text[i] != '\0'; i++) {

        if (text[i] == 'a' ||
            text[i] == 'e' ||
            text[i] == 'i' ||
            text[i] == 'o' ||
            text[i] == 'u') {

            count++;
        }
    }

    printf("Vowels = %d\n", count);

    return 0;
}
```

Output:

```text
Vowels = 5
```

---

# 20. Character Count

String-এর কতগুলো character আছে সেটা manually count করা যায়:

```c
#include <stdio.h>

int main() {

    char text[] = "Programming";

    int count = 0;

    while (text[count] != '\0') {
        count++;
    }

    printf("Length = %d\n", count);

    return 0;
}
```

Output:

```text
Length = 11
```

এটা `strlen()` internally কী ধরনের কাজ করে তার basic idea দেয়।

---

# 21. String Copy করার Basic ধারণা

ধরো:

```c
char source[] = "Hello";
char destination[20];
```

Character by character copy করা যায়:

```c
int i = 0;

while (source[i] != '\0') {
    destination[i] = source[i];
    i++;
}

destination[i] = '\0';
```

এখানে শেষের:

```c
destination[i] = '\0';
```

অত্যন্ত গুরুত্বপূর্ণ।

কারণ destination-কে proper C string বানাতে null terminator দরকার।

---

# 22. String কি `=` দিয়ে Copy করা যায়?

এভাবে নয়:

```c
char a[20];
char b[] = "Hello";

a = b;   // ❌
```

Array assignment C-তে এভাবে করা যায় না।

String copy করার জন্য আমরা পরে:

```c
strcpy()
```

শিখব।

---

# 23. String Comparison-এর Basic Idea

দুটি string:

```text
"apple"
"apple"
```

এগুলো same কিনা check করতে সরাসরি:

```c
if (a == b)
```

ব্যবহার করা ঠিক নয়।

String comparison-এর জন্য `<string.h>`-এর:

```c
strcmp()
```

ব্যবহার করা হয়।

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char a[] = "hello";
    char b[] = "hello";

    if (strcmp(a, b) == 0) {
        printf("Same\n");
    }
    else {
        printf("Different\n");
    }

    return 0;
}
```

Output:

```text
Same
```

`strcmp()` আমরা পরের lesson-এ বিস্তারিত করব।

---

# 24. Important String Functions

`<string.h>`-এ অনেক useful function আছে:

|Function|কাজ|
|---|---|
|`strlen()`|length|
|`strcpy()`|copy|
|`strcat()`|concatenate|
|`strcmp()`|compare|
|`strchr()`|character search|
|`strstr()`|substring search|

আজ শুধু ধারণা রাখো।

পরের lesson-এ এগুলো একে একে হাতে-কলমে শিখব।

---

# 25. String vs Character Array

এখানে subtle difference বুঝো।

```c
char letters[] = {'A', 'B', 'C'};
```

এটা একটি character array, কিন্তু valid C string নয়, কারণ শেষে:

```c
'\0'
```

নেই।

অন্যদিকে:

```c
char letters[] = {'A', 'B', 'C', '\0'};
```

এটি valid C string।

আর:

```c
char letters[] = "ABC";
```

compiler automatically `'\0'` রাখে।

---

# 26. সবচেয়ে গুরুত্বপূর্ণ Diagram 🔥

```text
char name[] = "CAT";

Memory:

Index       0     1     2      3
          ┌─────┬─────┬─────┬──────┐
          │ 'C' │ 'A' │ 'T' │ '\0' │
          └─────┴─────┴─────┴──────┘
```

তাই:

```c
name[0] → 'C'
name[1] → 'A'
name[2] → 'T'
name[3] → '\0'
```

---

# 27. Common Mistake ❌

ভুল:

```c
char name[5] = "Hello";
```

`"Hello"`-তে:

```text
5 characters
+ '\0'
= 6
```

তাই এই declaration যথেষ্ট নয়।

সঠিক:

```c
char name[6] = "Hello";
```

অথবা:

```c
char name[] = "Hello";
```

---

# 28. Common Mistake ❌

Character:

```c
char ch = "A";    // ❌
```

সঠিক:

```c
char ch = 'A';    // ✅
```

String:

```c
char text[] = "A";  // ✅
```

মনে রাখো:

```text
'A' → character
"A" → string
```

---

# 29. Common Mistake ❌

String print করতে:

```c
printf("%c", name);
```

ভুল।

সঠিক:

```c
printf("%s", name);
```

কারণ:

```text
%c → একটি character
%s → একটি string
```

---

# 30. Practical Program — Name + Length

```c
#include <stdio.h>
#include <string.h>

int main() {

    char name[50];

    printf("Enter your name: ");

    fgets(name, sizeof(name), stdin);

    name[strcspn(name, "\n")] = '\0';

    printf("Name: %s\n", name);
    printf("Length: %zu\n", strlen(name));

    return 0;
}
```

Input:

```text
Rahim Ahmed
```

Output:

```text
Name: Rahim Ahmed
Length: 11
```

---

# 🧪 Practice 1

এই string-এর প্রতিটি character আলাদা line-এ print করো:

```c
char text[] = "PROGRAM";
```

Expected:

```text
P
R
O
G
R
A
M
```

---

# 🧪 Practice 2

এই string-এর length বের করো:

```c
char text[] = "Bangladesh";
```

`strlen()` ব্যবহার করতে পারো।

---

# 🧪 Practice 3

User-এর কাছ থেকে একটি word নিয়ে:

1. String input নাও
    
2. Length print করো
    
3. প্রতিটি character print করো
    

---

# 🔥 Challenge

User-এর কাছ থেকে একটি string নাও এবং:

- কতগুলো vowel আছে বের করো
    
- কতগুলো consonant আছে বের করো
    
- string-এর length বের করো
    

Example:

```text
Input:
Programming
```

Possible output:

```text
Length: 11
Vowels: 3
Consonants: 8
```

---

# 🧠 আজকের Cheat Sheet

### String declaration

```c
char name[] = "Rahim";
```

### Character

```c
char ch = 'A';
```

### String print

```c
printf("%s", name);
```

### Character print

```c
printf("%c", name[0]);
```

### String traversal

```c
for (int i = 0; name[i] != '\0'; i++) {
    printf("%c", name[i]);
}
```

### Length

```c
strlen(name);
```

### Full-line input

```c
fgets(name, sizeof(name), stdin);
```

### String-এর শেষ

```text
'\0'
```

### Golden Rule ⭐

> **C string = character array + শেষের `'\0'` null character।**

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ✅ Searching
33. ✅ Sorting
34. ✅ 2D Array / Matrix
35. ✅ Strings
36. ⏳ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 36: String Functions

এবার `<string.h>` library নিয়ে hands-on করব:

```c
strlen()
strcpy()
strcat()
strcmp()
strchr()
strstr()
```

বিশেষ করে **`strlen`, `strcpy`, `strcat`, `strcmp`** ভালোভাবে শিখব—কারণ এগুলো C-তে string handling-এর foundation।

-----

# 🚀 Lesson 36 — String Functions in C

আজ আমরা `<string.h>` library-এর গুরুত্বপূর্ণ string functions শিখব।

```c
#include <string.h>
```

আজকের মূল functions:

```text
strlen()  → length
strcpy()  → copy
strcat()  → join
strcmp()  → compare
strchr()  → character search
strstr()  → substring search
```

---

# 1. `strlen()` — String Length

`strlen()` string-এর কতগুলো actual character আছে তা দেয়।

```c
#include <stdio.h>
#include <string.h>

int main() {

    char name[] = "Rahim";

    printf("Length = %zu\n", strlen(name));

    return 0;
}
```

Output:

```text
Length = 5
```

মনে রাখবে:

```text
strlen("Rahim") → 5
```

`'\0'` count হয় না।

---

## `strlen()` বনাম `sizeof()`

```c
char name[] = "Rahim";
```

তখন:

```c
strlen(name) → 5
sizeof(name) → 6
```

কারণ:

```text
R a h i m \0
```

---

# 2. `strcpy()` — String Copy

ধরো:

```c
char source[] = "Hello";
char destination[20];
```

`source` থেকে `destination`-এ copy:

```c
strcpy(destination, source);
```

Complete example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char source[] = "Hello";
    char destination[20];

    strcpy(destination, source);

    printf("%s\n", destination);

    return 0;
}
```

Output:

```text
Hello
```

### Syntax

```c
strcpy(destination, source);
```

মনে রাখবে:

> **যেখানে copy হবে → আগে, যেখান থেকে copy হবে → পরে।**

---

# 3. `strcpy()` কীভাবে কাজ করে?

ধরো:

```text
source:
H e l l o \0
```

`strcpy()` ধারণাগতভাবে copy করে:

```text
destination:
H e l l o \0
```

শেষের `'\0'`-ও copy হয়।

---

# 4. Destination-এর জায়গা গুরুত্বপূর্ণ ⚠️

এটা:

```c
char source[] = "Hello";
char destination[3];

strcpy(destination, source);
```

ভুল/অনিরাপদ, কারণ destination যথেষ্ট বড় নয়।

`"Hello"`-এর জন্য প্রয়োজন:

```text
5 characters + '\0'
= 6 bytes
```

তাই:

```c
char destination[20];
```

এর মতো যথেষ্ট capacity রাখতে হবে।

---

# 5. `strcat()` — String Concatenation

দুটি string জোড়া লাগাতে:

```c
strcat()
```

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char first[30] = "Hello ";
    char second[] = "World";

    strcat(first, second);

    printf("%s\n", first);

    return 0;
}
```

Output:

```text
Hello World
```

---

# 6. `strcat()` কী করছে?

Before:

```text
first:
Hello 
```

```text
second:
World
```

After:

```text
first:
Hello World
```

Syntax:

```c
strcat(destination, source);
```

অর্থাৎ `second`-কে `first`-এর শেষে যোগ করা হয়েছে।

---

# 7. `strcat()`-এর জন্য জায়গা রাখতে হবে

এটা মনে রাখবে:

```c
char first[30] = "Hello ";
```

কারণ `first`-এর মধ্যে নতুন string যোগ হবে।

যদি destination-এর capacity যথেষ্ট না হয়, সমস্যা হতে পারে।

---

# 8. `strcmp()` — String Compare ⭐

দুটি string একই কিনা check করতে:

```c
strcmp()
```

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char a[] = "hello";
    char b[] = "hello";

    if (strcmp(a, b) == 0) {
        printf("Same\n");
    }
    else {
        printf("Different\n");
    }

    return 0;
}
```

Output:

```text
Same
```

---

# 9. `strcmp()` Result

`strcmp(a, b)`:

```text
0          → দুই string equal
negative   → a lexicographically আগে
positive   → a lexicographically পরে
```

সবচেয়ে গুরুত্বপূর্ণ:

```c
strcmp(a, b) == 0
```

মানে দুই string equal।

---

# 10. Example

```c
char a[] = "apple";
char b[] = "banana";
```

```c
strcmp(a, b)
```

এর result negative হতে পারে, কারণ `"apple"` alphabetically `"banana"`-এর আগে।

উল্টো:

```c
strcmp(b, a)
```

positive হতে পারে।

তবে সাধারণ programming-এ exact negative বা positive value মুখস্থ করার প্রয়োজন নেই।

**Zero = equal** — এটা সবচেয়ে গুরুত্বপূর্ণ।

---

# 11. ❌ String Compare এ `==` নয়

এটা করো না:

```c
if (a == b)
```

String-এর content compare করার জন্য ব্যবহার করো:

```c
if (strcmp(a, b) == 0)
```

এটি C শেখার সময় খুব common mistake।

---

# 12. Practical — Password-like Comparison

ধরো:

```c
char correct[] = "hello";
char input[] = "hello";
```

তাহলে:

```c
if (strcmp(correct, input) == 0) {
    printf("Matched\n");
}
else {
    printf("Not matched\n");
}
```

Output:

```text
Matched
```

বাস্তব authentication system-এর নিরাপত্তা অবশ্যই আরও জটিল; এখানে শুধু string comparison শেখার example।

---

# 13. `strchr()` — Character Search

একটি string-এর মধ্যে নির্দিষ্ট character খুঁজতে:

```c
strchr()
```

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char text[] = "programming";

    char *result = strchr(text, 'g');

    if (result != NULL) {
        printf("Character found\n");
    }
    else {
        printf("Character not found\n");
    }

    return 0;
}
```

Output:

```text
Character found
```

এখানে:

```c
strchr(text, 'g')
```

মানে:

> `text`-এর মধ্যে প্রথম `'g'` খুঁজো।

---

# 14. `strchr()` এবং Pointer

এখানে:

```c
char *result;
```

দেখছো।

এটা pointer।

Pointer আমরা Phase 6-এ অনেক বিস্তারিত শিখব।

এখন শুধু বুঝো:

```c
strchr()
```

character পাওয়া গেলে তার location-এর দিকে pointer return করে।

না পেলে:

```c
NULL
```

return করে।

---

# 15. `strstr()` — Substring Search 🔥

একটি string-এর মধ্যে আরেকটি ছোট string খুঁজতে:

```c
strstr()
```

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char text[] = "I love programming";

    char *result = strstr(text, "programming");

    if (result != NULL) {
        printf("Found\n");
    }
    else {
        printf("Not found\n");
    }

    return 0;
}
```

Output:

```text
Found
```

---

# 16. Substring কী?

String:

```text
programming
```

এর মধ্যে:

```text
gram
```

একটি substring।

আর:

```text
program
```

এটাও substring।

কিন্তু:

```text
xyz
```

নেই।

---

# 17. `strstr()` Example

```c
char text[] = "C programming is fun";

if (strstr(text, "programming") != NULL) {
    printf("Word found");
}
```

Output:

```text
Word found
```

---

# 18. সব Functions একসাথে

```c
#include <stdio.h>
#include <string.h>

int main() {

    char a[50] = "Hello";
    char b[] = "World";

    // strlen
    printf("Length: %zu\n", strlen(a));

    // strcpy
    char copy[50];
    strcpy(copy, a);

    printf("Copy: %s\n", copy);

    // strcat
    strcat(a, " ");
    strcat(a, b);

    printf("Joined: %s\n", a);

    // strcmp
    if (strcmp(copy, "Hello") == 0) {
        printf("Strings are same\n");
    }

    // strchr
    if (strchr(a, 'W') != NULL) {
        printf("W found\n");
    }

    // strstr
    if (strstr(a, "World") != NULL) {
        printf("World found\n");
    }

    return 0;
}
```

---

# 19. `strcpy()` বনাম `strcat()`

খুব সহজভাবে:

```text
strcpy()
↓
একটি string copy করে
```

```text
strcat()
↓
একটি string-এর শেষে আরেকটি string যোগ করে
```

Example:

```c
strcpy(a, b);
```

মানে:

```text
b → a
```

আর:

```c
strcat(a, b);
```

মানে:

```text
a + b → a
```

---

# 20. `strlen()` বনাম `strcmp()`

```text
strlen()
↓
কত বড় string?

strcmp()
↓
দুটি string একই/কোন order-এ?
```

---

# 21. একটি Practical Program

User-এর কাছ থেকে দুইটি string নিয়ে compare:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char first[50];
    char second[50];

    printf("Enter first string: ");
    fgets(first, sizeof(first), stdin);

    printf("Enter second string: ");
    fgets(second, sizeof(second), stdin);

    first[strcspn(first, "\n")] = '\0';
    second[strcspn(second, "\n")] = '\0';

    if (strcmp(first, second) == 0) {
        printf("Both strings are same.\n");
    }
    else {
        printf("Strings are different.\n");
    }

    return 0;
}
```

Input:

```text
hello
hello
```

Output:

```text
Both strings are same.
```

---

# 22. Practical Program — Join Two Names

```c
#include <stdio.h>
#include <string.h>

int main() {

    char first[50];
    char last[50];
    char fullName[110];

    printf("First name: ");
    fgets(first, sizeof(first), stdin);

    printf("Last name: ");
    fgets(last, sizeof(last), stdin);

    first[strcspn(first, "\n")] = '\0';
    last[strcspn(last, "\n")] = '\0';

    strcpy(fullName, first);
    strcat(fullName, " ");
    strcat(fullName, last);

    printf("Full name: %s\n", fullName);

    return 0;
}
```

---

# 23. Common Mistake ❌ — `strcpy()` Destination

সঠিক:

```c
strcpy(destination, source);
```

ভুলভাবে উল্টো করলে expected result পাওয়া যাবে না।

মনে রাখো:

```text
destination ← source
```

---

# 24. Common Mistake ❌ — `strcat()`

যেখানে result থাকবে, সেই array-এর যথেষ্ট capacity থাকতে হবে।

```c
char result[100] = "Hello ";
char word[] = "Programming";

strcat(result, word);
```

এখানে `result`-এ extra জায়গা আছে।

---

# 25. Common Mistake ❌ — `strcmp()`

এটা:

```c
if (strcmp(a, b))
```

শুধু equal check-এর জন্য ব্যবহার করলে confusion হতে পারে।

স্পষ্টভাবে:

```c
if (strcmp(a, b) == 0)
```

লেখা ভালো।

---

# 26. Function Summary ⭐

|Function|কাজ|Example|
|---|---|---|
|`strlen()`|length|`strlen(s)`|
|`strcpy()`|copy|`strcpy(a,b)`|
|`strcat()`|join|`strcat(a,b)`|
|`strcmp()`|compare|`strcmp(a,b)`|
|`strchr()`|character search|`strchr(s,'a')`|
|`strstr()`|substring search|`strstr(s,"cat")`|

---

# 🧪 Practice 1

```c
char text[] = "Programming";
```

এর:

1. Length বের করো
    
2. প্রথম character print করো
    
3. শেষ character print করো
    

---

# 🧪 Practice 2

দুটি string:

```c
char first[] = "Hello";
char second[] = "World";
```

এগুলো join করে:

```text
Hello World
```

print করো।

---

# 🧪 Practice 3

User-এর কাছ থেকে দুটি string নাও এবং check করো তারা একই কিনা।

---

# 🔥 Challenge

একটি sentence input নাও।

তারপর user-এর কাছ থেকে একটি word নাও।

`strstr()` ব্যবহার করে check করো word-টি sentence-এর মধ্যে আছে কিনা।

Example:

```text
Sentence: I love C programming
Word: programming

Found
```

অন্যদিকে:

```text
Word: Python

Not found
```

---

# 🧠 আজকের Cheat Sheet

```c
strlen(s);
```

→ length

```c
strcpy(dest, src);
```

→ copy

```c
strcat(dest, src);
```

→ join

```c
strcmp(a, b) == 0
```

→ equal

```c
strchr(s, 'a')
```

→ character search

```c
strstr(s, "abc")
```

→ substring search

এবং সবগুলোর জন্য:

```c
#include <string.h>
```

---

# 🎯 Phase 5 Progress

```text
30. ✅ 1D Array
31. ✅ Array traversal
32. ✅ Searching
33. ✅ Sorting
34. ✅ 2D Array / Matrix
35. ✅ Strings
36. ✅ String functions
37. ⏳ Array of strings
```

## 🚀 Next → Lesson 37: Array of Strings

এবার আমরা একসাথে অনেকগুলো string রাখব:

```c
char names[5][20];
```

যেমন:

```text
Rahim
Karim
Sakib
Nadia
Rafi
```

এবং শিখব **input, output, traversal, sorting এবং string search**।


---
# 🚀 Lesson 37 — Array of Strings

এটাই **Phase 5-এর শেষ lesson**। আজ আমরা একসাথে অনেকগুলো string store এবং process করব।

ধরো আমাদের কাছে 5 জনের নাম আছে:

```text
Rahim
Karim
Sakib
Nadia
Rafi
```

একটি string-এর জন্য:

```c
char name[20];
```

অনেকগুলো string-এর জন্য:

```c
char names[5][20];
```

এটাই **array of strings**।

---

# 1. `char names[5][20]` মানে কী?

```c
char names[5][20];
```

এখানে:

```text
5  → মোট 5টি string
20 → প্রতিটি string-এর capacity 20 characters
```

ধারণাগতভাবে:

```text
names
 │
 ├── names[0] → "Rahim"
 ├── names[1] → "Karim"
 ├── names[2] → "Sakib"
 ├── names[3] → "Nadia"
 └── names[4] → "Rafi"
```

---

# 2. Direct Initialization

এভাবে সরাসরি values দেওয়া যায়:

```c
#include <stdio.h>

int main() {

    char names[5][20] = {
        "Rahim",
        "Karim",
        "Sakib",
        "Nadia",
        "Rafi"
    };

    return 0;
}
```

---

# 3. সব Names Print

একটি string print করতে:

```c
printf("%s", name);
```

তাই array of strings-এর জন্য loop:

```c
#include <stdio.h>

int main() {

    char names[5][20] = {
        "Rahim",
        "Karim",
        "Sakib",
        "Nadia",
        "Rafi"
    };

    for (int i = 0; i < 5; i++) {
        printf("%s\n", names[i]);
    }

    return 0;
}
```

Output:

```text
Rahim
Karim
Sakib
Nadia
Rafi
```

---

# 4. `names[i]` কী?

এটা খুব গুরুত্বপূর্ণ।

যদি:

```c
char names[5][20];
```

তাহলে:

```c
names[0]
```

হলো প্রথম string।

```c
names[1]
```

দ্বিতীয় string।

অর্থাৎ:

```text
names[0] → first string
names[1] → second string
names[2] → third string
```

---

# 5. Nested Loop দিয়ে Character দেখা

চাইলে প্রতিটি string-এর প্রতিটি character-ও দেখতে পারি:

```c
#include <stdio.h>

int main() {

    char names[3][20] = {
        "Rahim",
        "Karim",
        "Sakib"
    };

    for (int i = 0; i < 3; i++) {

        for (int j = 0; names[i][j] != '\0'; j++) {

            printf("%c ", names[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
R a h i m
K a r i m
S a k i b
```

এখানে:

```text
i → কোন string
j → সেই string-এর কোন character
```

---

# 6. User Input — Multiple Strings

User-এর কাছ থেকে 5টি name:

```c
#include <stdio.h>

int main() {

    char names[5][20];

    for (int i = 0; i < 5; i++) {

        printf("Enter name %d: ", i + 1);

        scanf("%19s", names[i]);
    }

    printf("\nNames:\n");

    for (int i = 0; i < 5; i++) {
        printf("%s\n", names[i]);
    }

    return 0;
}
```

Input:

```text
Rahim
Karim
Sakib
Nadia
Rafi
```

Output:

```text
Names:
Rahim
Karim
Sakib
Nadia
Rafi
```

---

# 7. Spaces-সহ Name Input

যদি:

```text
Rahim Ahmed
```

এর মতো full name নিতে চাও, `fgets()` ব্যবহার করা ভালো।

```c
#include <stdio.h>

int main() {

    char names[3][50];

    for (int i = 0; i < 3; i++) {

        printf("Enter full name: ");

        fgets(names[i], sizeof(names[i]), stdin);
    }

    printf("\nNames:\n");

    for (int i = 0; i < 3; i++) {
        printf("%s", names[i]);
    }

    return 0;
}
```

তবে `fgets()` এবং আগের input function একসাথে ব্যবহার করলে newline/input-buffer বিষয়টি খেয়াল করতে হয়।

---

# 8. Array of Strings + `strlen()`

প্রতিটি string-এর length বের করা যায়:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char names[4][20] = {
        "Rahim",
        "Karim",
        "Sakib",
        "Nadia"
    };

    for (int i = 0; i < 4; i++) {

        printf("%s = %zu characters\n",
               names[i],
               strlen(names[i]));
    }

    return 0;
}
```

Output:

```text
Rahim = 5 characters
Karim = 5 characters
Sakib = 5 characters
Nadia = 5 characters
```

---

# 9. String Search 🔎

ধরো:

```text
Rahim
Karim
Sakib
Nadia
Rafi
```

User `"Sakib"` search করবে।

`strcmp()` ব্যবহার করব:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char names[5][20] = {
        "Rahim",
        "Karim",
        "Sakib",
        "Nadia",
        "Rafi"
    };

    char target[20];

    printf("Search name: ");
    scanf("%19s", target);

    int found = 0;

    for (int i = 0; i < 5; i++) {

        if (strcmp(names[i], target) == 0) {

            printf("Found at index %d\n", i);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Not found\n");
    }

    return 0;
}
```

Input:

```text
Sakib
```

Output:

```text
Found at index 2
```

---

# 10. `strcmp()` কেন?

আমরা আগে শিখেছি:

```c
names[i] == target
```

string-এর content compare করার জন্য ঠিক নয়।

তাই:

```c
strcmp(names[i], target) == 0
```

ব্যবহার করি।

---

# 11. Array of Strings Sorting 🔥

এখন আমাদের আগের **sorting lesson** কাজে লাগবে।

Names:

```text
Sakib
Rahim
Nadia
Karim
```

Alphabetical order:

```text
Karim
Nadia
Rahim
Sakib
```

Bubble Sort-এর সঙ্গে `strcmp()` ব্যবহার করা যায়।

---

# 12. String Bubble Sort

```c
#include <stdio.h>
#include <string.h>

int main() {

    char names[4][20] = {
        "Sakib",
        "Rahim",
        "Nadia",
        "Karim"
    };

    for (int i = 0; i < 4 - 1; i++) {

        for (int j = 0; j < 4 - 1 - i; j++) {

            if (strcmp(names[j], names[j + 1]) > 0) {

                char temp[20];

                strcpy(temp, names[j]);
                strcpy(names[j], names[j + 1]);
                strcpy(names[j + 1], temp);
            }
        }
    }

    for (int i = 0; i < 4; i++) {
        printf("%s\n", names[i]);
    }

    return 0;
}
```

Output:

```text
Karim
Nadia
Rahim
Sakib
```

---

# 13. এখানে কী হচ্ছে?

এই condition:

```c
strcmp(names[j], names[j + 1]) > 0
```

মানে:

> বর্তমান string alphabetically পরের string-এর পরে হলে swap করো।

তারপর swap:

```c
char temp[20];

strcpy(temp, names[j]);
strcpy(names[j], names[j + 1]);
strcpy(names[j + 1], temp);
```

কারণ string array-কে সরাসরি:

```c
names[j] = names[j + 1];
```

এভাবে assign করা যায় না।

---

# 14. String Swap Pattern ⭐

মুখস্থ রাখার মতো pattern:

```c
char temp[20];

strcpy(temp, a);
strcpy(a, b);
strcpy(b, temp);
```

এটা string swap-এর basic pattern।

---

# 15. Ascending vs Descending

Alphabetical ascending:

```c
if (strcmp(names[j], names[j + 1]) > 0)
```

Descending:

```c
if (strcmp(names[j], names[j + 1]) < 0)
```

---

# 16. Longest Name বের করা

এবার array of strings + `strlen()` ব্যবহার করি।

```c
#include <stdio.h>
#include <string.h>

int main() {

    char names[5][20] = {
        "Rahim",
        "Christopher",
        "Sakib",
        "Nadia",
        "Karim"
    };

    int longestIndex = 0;

    for (int i = 1; i < 5; i++) {

        if (strlen(names[i]) > strlen(names[longestIndex])) {
            longestIndex = i;
        }
    }

    printf("Longest name: %s\n", names[longestIndex]);

    return 0;
}
```

Output:

```text
Longest name: Christopher
```

---

# 17. Shortest Name

একই idea:

```c
int shortestIndex = 0;

for (int i = 1; i < 5; i++) {

    if (strlen(names[i]) < strlen(names[shortestIndex])) {
        shortestIndex = i;
    }
}
```

---

# 18. Array of Strings + Number

বাস্তব program-এ শুধু name নয়, name-এর সঙ্গে marks/ID-ও লাগতে পারে।

এখন:

```text
Rahim → 85
Karim → 92
Sakib → 78
```

এভাবে related data রাখা যায়, কিন্তু সেখানে **structure** আরও ভালো solution হবে।

Structures আমরা Phase 7-এ শিখব।

---

# 19. Memory Concept

যদি:

```c
char names[5][20];
```

তাহলে মোট capacity:

```text
5 × 20 = 100 chars
```

ধারণাগতভাবে:

```text
names[0] → 20 chars
names[1] → 20 chars
names[2] → 20 chars
names[3] → 20 chars
names[4] → 20 chars
```

প্রতিটি row আলাদা character array হিসেবে ভাবতে পারো।

---

# 20. Common Mistake ❌

এটা:

```c
char names[5];
```

**5টি string** রাখে না।

এটা 5টি `char` রাখে।

5টি string-এর জন্য:

```c
char names[5][20];
```

---

# 21. Common Mistake ❌

এটা:

```c
printf("%c\n", names[i]);
```

ভুল, কারণ `names[i]` একটি পুরো string।

সঠিক:

```c
printf("%s\n", names[i]);
```

---

# 22. Common Mistake ❌

String compare:

```c
if (names[i] == target)
```

এর পরিবর্তে:

```c
if (strcmp(names[i], target) == 0)
```

ব্যবহার করো।

---

# 23. Full Practical Program 🔥

এবার একটি ছোট **Name Manager**:

```c
#include <stdio.h>
#include <string.h>

int main() {

    char names[5][30];

    // Input
    for (int i = 0; i < 5; i++) {

        printf("Enter name %d: ", i + 1);

        scanf("%29s", names[i]);
    }

    // Display
    printf("\nNames:\n");

    for (int i = 0; i < 5; i++) {
        printf("%d. %s\n", i + 1, names[i]);
    }

    // Search
    char target[30];

    printf("\nSearch name: ");
    scanf("%29s", target);

    int found = 0;

    for (int i = 0; i < 5; i++) {

        if (strcmp(names[i], target) == 0) {

            printf("Found at position %d\n", i + 1);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Name not found.\n");
    }

    return 0;
}
```

এখানে আমরা একসাথে ব্যবহার করলাম:

```text
Array
Loop
String
scanf
strcmp
Searching
```

এটাই C শেখার আসল উদ্দেশ্য—আগের concepts একসাথে ব্যবহার করা।

---

# 🧪 Practice 1

এই names print করো:

```c
char names[5][20] = {
    "Rahim",
    "Karim",
    "Sakib",
    "Nadia",
    "Rafi"
};
```

---

# 🧪 Practice 2

5টি name input নিয়ে **alphabetical order-এ sort** করো।

Hint:

```c
strcmp()
strcpy()
```

এবং Bubble Sort ব্যবহার করবে।

---

# 🧪 Practice 3

5টি name input নিয়ে user-এর target name search করো।

Expected:

```text
Search: Nadia

Found at position 4
```

---

# 🔥 Challenge

একটি program বানাও যেখানে:

1. 5টি name input নেবে
    
2. সব names print করবে
    
3. alphabetical order-এ sort করবে
    
4. sorted names print করবে
    
5. একটি name search করবে
    
6. প্রতিটি name-এর length print করবে
    

Output-এর structure:

```text
Names:
Rahim
Sakib
Nadia
Karim
Rafi

Sorted:
Karim
Nadia
Rahim
Rafi
Sakib

Search: Rafi
Found

Lengths:
Karim = 5
Nadia = 5
Rahim = 5
Rafi = 4
Sakib = 5
```

---

# 🧠 আজকের Cheat Sheet

### Array of strings

```c
char names[5][20];
```

### Access

```c
names[i]
```

### Print

```c
printf("%s", names[i]);
```

### Compare

```c
strcmp(names[i], target) == 0
```

### Length

```c
strlen(names[i])
```

### Copy

```c
strcpy(destination, source);
```

### String sorting

```c
if (strcmp(names[j], names[j + 1]) > 0)
```

### String swap

```c
char temp[20];

strcpy(temp, names[j]);
strcpy(names[j], names[j + 1]);
strcpy(names[j + 1], temp);
```

---

# 🎉 Phase 5 Complete!

তুমি এখন পর্যন্ত শিখেছ:

```text
30. ✅ 1D Array
31. ✅ Array Traversal
32. ✅ Searching
33. ✅ Sorting
34. ✅ 2D Array / Matrix
35. ✅ Strings
36. ✅ String Functions
37. ✅ Array of Strings
```

এখন আমরা C-এর সবচেয়ে গুরুত্বপূর্ণ এবং একটু challenging অংশে ঢুকব:

# 🔥 Phase 6 — Pointers

```text
38. ⏳ Pointer Basics
39. ⏳ Address Operator &
40. ⏳ Dereference *
41. ⏳ Pointer + Array
42. ⏳ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next: Lesson 38 — Pointer Basics

Pointer শুরু করার মূল idea হবে:

```c
int x = 10;
int *p = &x;
```

এখানে আমরা বুঝব **variable-এর value, address, এবং pointer-এর মধ্যে আসলে কী সম্পর্ক**।

---

# 🔥 Lesson 38 — Pointer Basics

আজ থেকে **Phase 6 — Pointers** শুরু।

Pointers প্রথমে একটু confusing মনে হতে পারে, কিন্তু একবার **value → address → pointer** এই তিনটি সম্পর্ক বুঝে ফেললে পরের topics অনেক সহজ হবে।

---

# 1. Pointer কী?

সহজ ভাষায়:

> **Pointer হলো এমন একটি variable, যার মধ্যে অন্য একটি variable-এর memory address রাখা যায়।**

সাধারণ variable:

```c
int x = 10;
```

এখানে `x`-এর মধ্যে আছে:

```text
10
```

Pointer:

```c
int *p;
```

`p` একটি pointer variable।

---

# 2. আগে Memory বুঝি

ধরো:

```c
int x = 10;
```

ধারণাগতভাবে memory এমন হতে পারে:

```text
Address        Value
┌──────────┬────────┐
│  1000    │   10   │
└──────────┴────────┘
```

এখানে:

```text
x-এর value    = 10
x-এর address  = 1000
```

**বাস্তব address 1000 হবে এমন নয়।** এটা শুধু বোঝানোর জন্য।

---

# 3. Address কী?

Variable memory-তে কোথাও রাখা থাকে।

তার সেই location-এর একটি address থাকে।

C-তে address বের করার জন্য ব্যবহার করি:

```c
&
```

এটাকে বলা হয়:

> **Address-of operator**

Example:

```c
int x = 10;

printf("%p", (void *)&x);
```

এটা `x`-এর memory address দেখাবে।

---

# 4. প্রথম Pointer Program

```c
#include <stdio.h>

int main() {

    int x = 10;

    int *p = &x;

    printf("Value of x = %d\n", x);
    printf("Address of x = %p\n", (void *)&x);
    printf("Value of p = %p\n", (void *)p);

    return 0;
}
```

Output-এর address প্রতিবার এমন হতে পারে:

```text
Value of x = 10
Address of x = 0x7ffd1234
Value of p = 0x7ffd1234
```

এখানে লক্ষ্য করো:

```text
&p == address of x
```

অর্থাৎ:

```text
p
↓
x-এর address
```

---

# 5. `int *p` মানে কী?

```c
int *p;
```

এখানে:

```text
int
```

বলছে pointer কোন ধরনের object-এর address রাখবে।

আর:

```text
*
```

বলছে `p` একটি pointer।

তাই:

```c
int *p;
```

মানে:

> `p` একটি pointer, যা একটি `int` variable-এর address ধারণ করতে পারে।

---

# 6. Pointer Diagram 🔥

ধরো:

```c
int x = 10;
int *p = &x;
```

ধারণাগতভাবে:

```text
        x
   ┌──────────┐
   │    10    │
   └──────────┘
       ↑
       │
       │ address
       │
   ┌──────────┐
   │    p     │
   │  &x      │
   └──────────┘
```

অর্থাৎ:

```text
x → value 10
p → x-এর address
```

---

# 7. Pointer-এর Value কী?

এটা:

```c
printf("%p", (void *)p);
```

pointer-এর মধ্যে থাকা **address** print করে।

যদি:

```c
p = &x;
```

তাহলে:

```text
p = x-এর address
```

---

# 8. `*p` কী?

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

যদি:

```c
int x = 10;
int *p = &x;
```

তাহলে:

```c
*p
```

মানে:

> Pointer যে address-এর দিকে point করছে, সেই address-এ থাকা value।

তাই:

```c
printf("%d\n", *p);
```

Output:

```text
10
```

---

# 9. `*`-এর দুইটি গুরুত্বপূর্ণ ব্যবহার

C-তে `*` দেখে beginner-রা confuse হয়।

### Declaration:

```c
int *p;
```

এখানে `*` বলছে:

> `p` একটি pointer।

### Dereference:

```c
*p
```

এখানে `*` বলছে:

> Pointer যে জায়গায় point করছে, সেই জায়গার value access করো।

---

# 10. প্রথম Full Example

```c
#include <stdio.h>

int main() {

    int x = 10;

    int *p = &x;

    printf("x = %d\n", x);
    printf("&x = %p\n", (void *)&x);
    printf("p = %p\n", (void *)p);
    printf("*p = %d\n", *p);

    return 0;
}
```

Conceptually:

```text
x   → 10
&x  → address of x
p   → address of x
*p  → 10
```

এটা খুব ভালোভাবে বুঝে রাখো। 🔥

---

# 11. Pointer দিয়ে Variable Change করা

এটাই pointer-এর সবচেয়ে powerful feature।

```c
#include <stdio.h>

int main() {

    int x = 10;

    int *p = &x;

    *p = 50;

    printf("x = %d\n", x);

    return 0;
}
```

Output:

```text
x = 50
```

কিন্তু আমরা সরাসরি:

```c
x = 50;
```

লিখিনি।

লিখেছি:

```c
*p = 50;
```

কারণ `p` `x`-এর address ধরে রেখেছে।

---

# 12. কীভাবে এটা কাজ করল?

আগে:

```text
x
┌─────┐
│ 10  │
└─────┘
  ↑
  │
  p
```

তারপর:

```c
*p = 50;
```

ফলে:

```text
x
┌─────┐
│ 50  │
└─────┘
  ↑
  │
  p
```

Pointer-এর মাধ্যমে `x`-এর value পরিবর্তিত হয়েছে।

---

# 13. Pointer দিয়ে Multiple Changes

```c
#include <stdio.h>

int main() {

    int x = 10;

    int *p = &x;

    *p = 20;
    printf("%d\n", x);

    *p = 30;
    printf("%d\n", x);

    *p = 100;
    printf("%d\n", x);

    return 0;
}
```

Output:

```text
20
30
100
```

---

# 14. Pointer-এর Type

Pointer-এর type সাধারণত pointed-to object-এর type-এর সঙ্গে মেলে।

```c
int x = 10;
int *p = &x;
```

`int` pointer।

একইভাবে:

```c
float price = 10.5f;
float *p = &price;
```

এবং:

```c
char ch = 'A';
char *p = &ch;
```

---

# 15. Examples

### Integer

```c
int x = 10;
int *p = &x;
```

### Float

```c
float x = 5.5f;
float *p = &x;
```

### Character

```c
char x = 'A';
char *p = &x;
```

Basic rule:

```text
int variable   → int *
float variable → float *
char variable  → char *
```

---

# 16. Pointer Size

একটি interesting বিষয়:

```c
int *p;
char *q;
double *r;
```

তিনটি pointer-এর pointed-to type আলাদা হলেও pointer-এর নিজের size একই হতে পারে একটি নির্দিষ্ট system-এ।

কারণ pointer-এর কাজ হলো **address রাখা**।

তবে pointer-এর size system/architecture-এর উপর নির্ভর করে।

এখন exact byte মুখস্থ করার দরকার নেই।

---

# 17. `sizeof()` দিয়ে দেখা

```c
#include <stdio.h>

int main() {

    int x = 10;
    int *p = &x;

    printf("Size of int = %zu\n", sizeof(x));
    printf("Size of pointer = %zu\n", sizeof(p));

    return 0;
}
```

অনেক modern 64-bit system-এ pointer-এর size 8 bytes হতে পারে, কিন্তু portable C code-এ নির্দিষ্ট size ধরে নেওয়া উচিত নয়।

---

# 18. Pointer নিজেও একটি Variable

Pointer-এরও নিজের address থাকে।

ধরো:

```c
int x = 10;
int *p = &x;
```

এখন:

```c
&p
```

মানে:

> `p` pointer variable নিজে memory-তে কোথায় আছে?

তাই:

```text
x-এর address → &x
p-এর address → &p
```

দুটো আলাদা জিনিস।

---

# 19. খুব গুরুত্বপূর্ণ পার্থক্য

ধরো:

```c
int x = 10;
int *p = &x;
```

তাহলে:

```text
x   → 10
&x  → x-এর address
p   → x-এর address
*p  → 10
&p  → p-এর address
```

এগুলো একসাথে মনে রাখো।

---

# 20. Pointer Chain Diagram

```text
x = 10

┌─────────────┐
│      10     │
└─────────────┘
      x
      ↑
      │
      │ address
      │
┌─────────────┐
│   address   │
└─────────────┘
      p
```

আর:

```text
*p → 10
```

---

# 21. Pointer দিয়ে Swap-এর Basic Idea

Pointers-এর একটি classic use হলো দুই variable-এর value modify করা।

ধরো:

```c
int a = 10;
int b = 20;
```

Pointer:

```c
int *p = &a;
int *q = &b;
```

এখন:

```c
int temp = *p;
*p = *q;
*q = temp;
```

ফলে:

```text
a = 20
b = 10
```

পরের lesson-এ function-এর সঙ্গে pointer ব্যবহার করে এই concept আরও গুরুত্বপূর্ণভাবে দেখব।

---

# 22. `NULL` Pointer

Pointer যদি কোনো valid object-এর address না ধরে, তাকে `NULL` করা যায়:

```c
int *p = NULL;
```

মানে:

> `p` এখন কোনো valid object-কে point করছে না।

Check:

```c
if (p == NULL) {
    printf("Pointer is NULL\n");
}
```

এটা pointer programming-এর খুব গুরুত্বপূর্ণ safety habit।

---

# 23. NULL Pointer Dereference করা যাবে না ❌

এটা করো না:

```c
int *p = NULL;

printf("%d", *p);
```

কারণ `p` কোনো valid object-কে point করছে না।

Pointer ব্যবহার করার আগে নিশ্চিত হওয়া দরকার যে এটি valid address ধারণ করছে।

---

# 24. Uninitialized Pointer-এর বিপদ ⚠️

এটা dangerous:

```c
int *p;

*p = 10;
```

কারণ `p` initialize করা হয়নি।

সঠিক example:

```c
int x;

int *p = &x;

*p = 10;
```

এখন `p` validভাবে `x`-কে point করছে।

---

# 25. Pointer Declaration-এর Style

এই দুটো একই:

```c
int *p;
```

এবং:

```c
int* p;
```

কিন্তু C code-এ অনেক developer:

```c
int *p;
```

style ব্যবহার করেন।

বিশেষ করে multiple declaration-এর সময় সতর্ক হও:

```c
int *p, q;
```

এখানে:

```text
p → pointer
q → normal int
```

দুটো pointer নয়।

যদি দুটোই pointer হয়:

```c
int *p, *q;
```

---

# 26. Practical Example

```c
#include <stdio.h>

int main() {

    int age = 15;

    int *ptr = &age;

    printf("Age: %d\n", age);
    printf("Age through pointer: %d\n", *ptr);

    *ptr = 16;

    printf("Updated age: %d\n", age);

    return 0;
}
```

Concept:

```text
age = 15
   ↓
ptr = &age
   ↓
*ptr = 16
   ↓
age = 16
```

---

# 27. Pointer-এর Three Golden Symbols 🔥

আজকের সবচেয়ে গুরুত্বপূর্ণ তিনটি:

### `&`

```c
&x
```

মানে:

> `x`-এর address

### `*` declaration

```c
int *p;
```

মানে:

> `p` একটি pointer

### `*` dereference

```c
*p
```

মানে:

> pointer যে object-কে point করছে তার value

---

# 28. একটি Mental Model

ধরো:

```c
int money = 500;
int *p = &money;
```

ভাবো:

```text
money-এর ভিতরে:
┌───────┐
│  500  │
└───────┘

p-এর ভিতরে:
┌──────────────┐
│ money-এর     │
│ address      │
└──────────────┘
```

তাই:

```c
money
```

→ 500

```c
p
```

→ address

```c
*p
```

→ 500

```c
&money
```

→ address

---

# 🧪 Practice 1

এই code-এর output কী হবে অনুমান করো:

```c
int x = 25;
int *p = &x;

printf("%d\n", x);
printf("%d\n", *p);

*p = 100;

printf("%d\n", x);
```

---

# 🧪 Practice 2

একটি program লিখো:

```text
x = 50
```

তার pointer তৈরি করো এবং pointer ব্যবহার করে `x`-এর value `100` করো।

Expected:

```text
Before: 50
After: 100
```

---

# 🧪 Practice 3

তিনটি জিনিস print করো:

```text
x-এর value
x-এর address
pointer-এর মাধ্যমে x-এর value
```

Hint:

```c
x
&x
*p
```

---

# 🔥 Challenge

দুটি variable:

```c
int a = 10;
int b = 20;
```

দুটি pointer ব্যবহার করে তাদের value swap করো।

Expected:

```text
Before:
a = 10
b = 20

After:
a = 20
b = 10
```

**কোনো built-in swap function ব্যবহার করবে না।**

---

# 🧠 আজকের Cheat Sheet

```c
int x = 10;
```

→ normal variable

```c
&x
```

→ `x`-এর address

```c
int *p = &x;
```

→ `p`-তে `x`-এর address রাখা

```c
p
```

→ address

```c
*p
```

→ সেই address-এর value

```c
*p = 50;
```

→ pointer-এর মাধ্যমে `x`-এর value পরিবর্তন

```c
int *p = NULL;
```

→ pointer কোনো valid object-কে point করছে না

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ⏳ Address operator &
40. ⏳ Dereference *
41. ⏳ Pointer + Array
42. ⏳ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 39 — Address Operator `&`

পরের lesson-এ আমরা `&` এবং memory address আরও গভীরভাবে দেখব—বিশেষ করে **কেন `scanf()`-এ `&age` লিখি কিন্তু string input-এ সাধারণত `&name` লিখি না**।

----

# 🔥 Lesson 39 — Address Operator `&`

আজ আমরা C-এর **Address Operator `&`** বিস্তারিতভাবে শিখব।

আগের lesson-এ দেখেছিলাম:

```c
int x = 10;
int *p = &x;
```

এখানে `&x` হলো **x-এর memory address**।

---

# 1. `&` কী?

C-তে:

```c
&variable
```

মানে:

> **এই variable-এর memory address দাও।**

Example:

```c
int age = 15;

printf("%p\n", (void *)&age);
```

এটি `age` যেখানে memory-তে আছে সেই address দেখাবে।

Output এমন হতে পারে:

```text
0x7ffd8a123450
```

Address তোমার computer-এ আলাদা হবে।

---

# 2. Value বনাম Address

ধরো:

```c
int x = 50;
```

তখন:

```text
x
↓
50
```

আর:

```c
&x
```

মানে:

```text
&x
↓
x-এর memory address
```

তাই:

```text
x   → value
&x  → address
```

---

# 3. একটি Complete Example

```c
#include <stdio.h>

int main() {

    int x = 50;

    printf("Value = %d\n", x);
    printf("Address = %p\n", (void *)&x);

    return 0;
}
```

Possible output:

```text
Value = 50
Address = 0x7ffd12345678
```

আবার program চালালে address বদলাতে পারে।

---

# 4. `&` কেন দরকার?

সবচেয়ে গুরুত্বপূর্ণ জায়গা:

```c
scanf()
```

ধরো:

```c
int age;

scanf("%d", &age);
```

এখানে `scanf()`-কে বলা হচ্ছে:

> user যে value দেবে, সেটা `age` variable-এর address-এ গিয়ে রাখো।

---

# 5. `scanf()`-এর ভিতরের Idea

ধরো:

```c
int age;
```

Memory:

```text
Address        Value
┌──────────┬─────────┐
│  1000    │    ?    │
└──────────┴─────────┘
```

তারপর:

```c
scanf("%d", &age);
```

`&age` হলো:

```text
1000
```

User যদি:

```text
15
```

দেয়, তাহলে `scanf()` সেই address-এ 15 রাখে।

ফলে:

```text
Address        Value
┌──────────┬─────────┐
│  1000    │   15    │
└──────────┴─────────┘
```

---

# 6. `&age` বনাম `age`

এটা খুব গুরুত্বপূর্ণ।

```c
printf("%d", age);
```

এখানে আমরা **value** চাই।

কিন্তু:

```c
scanf("%d", &age);
```

এখানে আমরা **address** দিচ্ছি।

তাই:

```text
printf → value
scanf  → address
```

`scanf()`-এর ক্ষেত্রে format specifier অনুযায়ী pointer/address দেওয়ার প্রয়োজন হয়।

---

# 7. ভুল Example ❌

এটা:

```c
int age;

scanf("%d", age);
```

ভুল, কারণ `%d`-এর জন্য `scanf()`-কে একটি `int` object-এর address দিতে হয়।

সঠিক:

```c
scanf("%d", &age);
```

---

# 8. কেন `scanf()`-এ Address লাগে?

কারণ `scanf()`-কে variable-এর value **পরিবর্তন করতে হবে**।

ধরো:

```c
int x;
```

যদি `scanf()` শুধু `x`-এর current value পায়, তাহলে কোথায় নতুন value রাখতে হবে সেটা জানবে কীভাবে?

তাই:

```c
&x
```

দিয়ে তার memory location জানানো হয়।

---

# 9. Pointer-এর সঙ্গে Connection 🔥

ধরো:

```c
int x = 10;

int *p = &x;
```

এখানে:

```text
&x
 ↓
address of x
 ↓
p
```

অর্থাৎ:

```c
p == &x
```

address-এর দিক থেকে একই location।

---

# 10. `&x` এবং `p`

ধরো:

```c
int x = 10;
int *p = &x;
```

তাহলে:

```c
printf("%p\n", (void *)&x);
printf("%p\n", (void *)p);
```

দুটির address একই হবে।

Conceptually:

```text
&x ─────┐
        ↓
     x-এর address
        ↑
        │
p ──────┘
```

---

# 11. `&p` কিন্তু অন্য জিনিস!

এখানে beginner-রা খুব সহজেই confuse হয়।

```c
int x = 10;
int *p = &x;
```

তখন:

```text
&x → x-এর address
p  → x-এর address
&p → p-এর নিজের address
```

অর্থাৎ:

```c
&p
```

**x-এর address নয়।**

এটা `p` pointer variable-এর address।

---

# 12. Example

```c
#include <stdio.h>

int main() {

    int x = 10;
    int *p = &x;

    printf("x address  = %p\n", (void *)&x);
    printf("p value    = %p\n", (void *)p);
    printf("p address  = %p\n", (void *)&p);

    return 0;
}
```

এখানে প্রথম দুইটির address একই হবে:

```text
x address → 0x...
p value   → 0x...
```

কিন্তু:

```text
p address → অন্য address
```

কারণ `p` নিজেও একটি variable।

---

# 13. Multiple Variables

```c
int a = 10;
int b = 20;
int c = 30;
```

তাহলে:

```c
&a
&b
&c
```

তিনটি আলাদা memory address।

Example:

```c
printf("%p\n", (void *)&a);
printf("%p\n", (void *)&b);
printf("%p\n", (void *)&c);
```

---

# 14. `&` শুধু `int`-এর জন্য নয়

### Integer

```c
int x = 10;
printf("%p", (void *)&x);
```

### Float

```c
float price = 5.5f;
printf("%p", (void *)&price);
```

### Character

```c
char grade = 'A';
printf("%p", (void *)&grade);
```

সব ক্ষেত্রেই `&` variable-এর address দেয়।

---

# 15. `&` এবং `*` — বিপরীত ধারণা

এগুলো ভালোভাবে বুঝে রাখো:

```c
int x = 10;
int *p = &x;
```

এখানে:

```text
&x
↓
address বের করে
```

আর:

```text
*p
↓
address থেকে value বের করে
```

সহজ mental model:

```text
x
↓
value

&x
↓
address

p
↓
address

*p
↓
value
```

---

# 16. Visual Model 🔥

```text
              x
        ┌───────────┐
        │    10     │
        └───────────┘
              ↑
              │
             &x
              │
              │
        ┌───────────┐
        │     p     │
        │  &x       │
        └───────────┘
```

এখন:

```c
*p
```

করলে pointer যেখানে point করছে সেই `x`-এর value:

```text
10
```

---

# 17. `scanf()`-এর আরও Example

### Integer

```c
int age;

scanf("%d", &age);
```

### Float

```c
float price;

scanf("%f", &price);
```

### Character

```c
char grade;

scanf(" %c", &grade);
```

এখানে space `" %c"` সাধারণত আগের whitespace এড়িয়ে যেতে সাহায্য করে।

---

# 18. String-এর ক্ষেত্রে কী হয়?

এখানে একটি গুরুত্বপূর্ণ বিষয়।

```c
char name[20];

scanf("%19s", name);
```

এখানে সাধারণত:

```c
&name
```

লিখি না।

কেন?

কারণ array expression `name` অনেক expression context-এ তার প্রথম element-এর address হিসেবে ব্যবহৃত হয়।

অর্থাৎ:

```text
name
↓
&name[0]
```

এর সঙ্গে `&name` একই type নয়।

এটা এখন শুধু ধারণা হিসেবে মনে রাখো; array এবং pointer-এর সম্পর্ক Lesson 41-এ বিস্তারিত দেখব।

---

# 19. `scanf()` Example

```c
#include <stdio.h>

int main() {

    int age;
    float height;
    char grade;

    printf("Age: ");
    scanf("%d", &age);

    printf("Height: ");
    scanf("%f", &height);

    printf("Grade: ");
    scanf(" %c", &grade);

    printf("\nAge = %d\n", age);
    printf("Height = %.2f\n", height);
    printf("Grade = %c\n", grade);

    return 0;
}
```

---

# 20. Pointer ব্যবহার করে Address নেওয়া

আমরা সরাসরি:

```c
int *p = &x;
```

লিখতে পারি।

আবার:

```c
int x = 10;
int *p;

p = &x;
```

দুটোই valid।

---

# 21. Pointer Reassignment

একটি pointer অন্য variable-এর address-ও রাখতে পারে।

```c
#include <stdio.h>

int main() {

    int a = 10;
    int b = 20;

    int *p = &a;

    printf("%d\n", *p);

    p = &b;

    printf("%d\n", *p);

    return 0;
}
```

Output:

```text
10
20
```

প্রথমে:

```text
p → a
```

পরে:

```text
p → b
```

---

# 22. `&` দিয়ে Pointer তৈরি

```c
int x = 100;

int *p = &x;
```

এই একটি line-এ তিনটি concept:

```text
x
↓
100

&x
↓
x-এর address

p
↓
x-এর address
```

---

# 23. `&` কি সব জায়গায় ব্যবহার করা যায়?

না।

`&` সাধারণত এমন expression-এর সঙ্গে ব্যবহার করা হয় যার একটি addressable object আছে।

যেমন:

```c
int x = 10;

&x
```

valid।

কিন্তু সাধারণভাবে:

```c
&(x + 5)
```

valid নয়, কারণ `x + 5` কোনো stored variable/object নয় যার address তুমি এভাবে নিতে পারো।

---

# 24. একটি Important Rule

যখন দেখবে:

```c
&variable
```

নিজেকে জিজ্ঞেস করবে:

> **আমি variable-এর value চাই, নাকি variable কোথায় আছে সেই address চাই?**

যদি address:

```c
&variable
```

যদি pointer দিয়ে সেই address-এর value access:

```c
*pointer
```

---

# 25. Mini Program — Address Inspector

```c
#include <stdio.h>

int main() {

    int age = 15;
    float marks = 87.5f;
    char grade = 'A';

    printf("age value     = %d\n", age);
    printf("age address   = %p\n", (void *)&age);

    printf("marks value   = %.2f\n", marks);
    printf("marks address = %p\n", (void *)&marks);

    printf("grade value   = %c\n", grade);
    printf("grade address = %p\n", (void *)&grade);

    return 0;
}
```

এখানে `%p` ব্যবহার করে pointer/address print করা হচ্ছে। Portable C-তে `%p`-এর সঙ্গে `(void *)` cast ব্যবহার করা ভালো।

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ Concept

এই চারটি relationship মুখস্থ না করে **বোঝো**:

```text
int x = 10;

x
↓
10

&x
↓
x-এর address

int *p = &x;

p
↓
x-এর address

*p
↓
10
```

---

# 🧪 Practice 1

Output predict করো:

```c
int x = 25;
int *p = &x;

printf("%d\n", x);
printf("%d\n", *p);

*p = 50;

printf("%d\n", x);
```

---

# 🧪 Practice 2

একটি program লিখো যেখানে:

```text
a = 100
b = 200
```

তারপর:

- `a`-এর address print করবে
    
- `b`-এর address print করবে
    
- `a`-এর জন্য একটি pointer বানাবে
    
- pointer-এর value print করবে
    

---

# 🧪 Practice 3 — `scanf()`

একটি program লিখো যেখানে user-এর কাছ থেকে:

```text
Age
Marks
Grade
```

নেবে।

`scanf()` ব্যবহার করবে এবং সঠিকভাবে `&` ব্যবহার করবে।

---

# 🔥 Challenge

এই programটি complete করো:

```c
#include <stdio.h>

int main() {

    int a, b;

    printf("Enter a: ");
    // input

    printf("Enter b: ");
    // input

    int *p = /* a-এর address */;
    int *q = /* b-এর address */;

    printf("a = %d\n", /* pointer দিয়ে a-এর value */);
    printf("b = %d\n", /* pointer দিয়ে b-এর value */);

    return 0;
}
```

লক্ষ্য:

```text
scanf()
&
pointer
*
```

— এই চারটি concept একসাথে ব্যবহার করা।

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ⏳ Dereference *
41. ⏳ Pointer + Array
42. ⏳ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 40 — Dereference `*`

পরের lesson-এ আমরা `*p`-কে আরও গভীরভাবে বুঝব এবং দেখব কীভাবে pointer দিয়ে **অন্য variable-এর value read ও modify** করা যায়।

---

# 🔥 Lesson 40 — Dereference Operator `*`

আজ আমরা Pointer-এর দ্বিতীয় সবচেয়ে গুরুত্বপূর্ণ অংশ শিখব:

```c
*p
```

এটাকে বলে **dereference**।

আগের lesson-এ:

```c
int x = 10;
int *p = &x;
```

শিখেছিলাম:

```text
x   → 10
&x  → x-এর address
p   → x-এর address
```

আজ বুঝব:

```text
*p  → x-এর value
```

---

# 1. Dereference কী?

সহজভাবে:

> **Pointer-এর মধ্যে থাকা address-এ গিয়ে সেই address-এর value access করাকে dereference বলে।**

ধরো:

```c
int x = 10;
int *p = &x;
```

তাহলে:

```c
*p
```

এর value:

```text
10
```

কারণ `p` `x`-এর address ধরে রেখেছে।

---

# 2. প্রথম Example

```c
#include <stdio.h>

int main() {

    int x = 10;
    int *p = &x;

    printf("x = %d\n", x);
    printf("*p = %d\n", *p);

    return 0;
}
```

Output:

```text
x = 10
*p = 10
```

অর্থাৎ:

```text
x  == *p
```

value-এর দিক থেকে।

---

# 3. Visualize করি

ধরো memory:

```text
Address        Value
┌──────────┬──────────┐
│  1000    │    10    │
└──────────┴──────────┘
       ↑
       │
      p
```

এখানে:

```text
p  → 1000
```

আর:

```text
*p
```

মানে:

> 1000 address-এ গিয়ে value নাও।

ফলে:

```text
*p → 10
```

---

# 4. `p` বনাম `*p`

এটা খুব গুরুত্বপূর্ণ:

```c
int x = 10;
int *p = &x;
```

তখন:

|Expression|Meaning|
|---|---|
|`x`|x-এর value|
|`&x`|x-এর address|
|`p`|x-এর address|
|`*p`|x-এর value|
|`&p`|p-এর নিজের address|

এগুলো ভালোভাবে বুঝে ফেললে pointer-এর অনেকটা foundation তৈরি হয়ে যাবে।

---

# 5. Dereference দিয়ে Value পরিবর্তন

এটাই pointer-এর সবচেয়ে powerful use।

```c
#include <stdio.h>

int main() {

    int x = 10;
    int *p = &x;

    *p = 100;

    printf("x = %d\n", x);

    return 0;
}
```

Output:

```text
x = 100
```

আমরা লিখিনি:

```c
x = 100;
```

বরং:

```c
*p = 100;
```

কিন্তু `x`-এর value বদলে গেছে।

---

# 6. কেন `x` বদলে গেল?

কারণ:

```text
p → x-এর address
```

তাই:

```text
*p
```

মানে:

```text
x-এর memory location-এর value
```

সুতরাং:

```c
*p = 100;
```

মানে:

> x যেখানে আছে সেখানে 100 রাখো।

---

# 7. Step-by-Step

```c
int x = 10;
```

```text
x = 10
```

তারপর:

```c
int *p = &x;
```

```text
p → x
```

তারপর:

```c
*p = 50;
```

ফলে:

```text
x = 50
```

তারপর:

```c
*p = 90;
```

ফলে:

```text
x = 90
```

---

# 8. Dereference দিয়ে Increment

```c
#include <stdio.h>

int main() {

    int x = 10;
    int *p = &x;

    (*p)++;

    printf("%d\n", x);

    return 0;
}
```

Output:

```text
11
```

কারণ:

```text
*p = x
```

তাই:

```c
(*p)++;
```

মানে:

```c
x++;
```

---

# 9. Dereference দিয়ে Decrement

```c
(*p)--;
```

যদি:

```text
x = 10
```

তাহলে:

```text
x = 9
```

---

# 10. Arithmetic Operations

Pointer দিয়ে value modify করা যায়:

```c
*p = *p + 10;
```

যদি:

```text
x = 20
```

তাহলে:

```text
x = 30
```

আর:

```c
*p = *p * 2;
```

তাহলে:

```text
x = 40
```

---

# 11. Example

```c
#include <stdio.h>

int main() {

    int number = 10;
    int *p = &number;

    *p = *p + 5;

    printf("Number = %d\n", number);

    return 0;
}
```

Output:

```text
Number = 15
```

---

# 12. `*p` Expression হিসেবে

এইগুলো সব valid:

```c
printf("%d", *p);

int y = *p;

if (*p > 10) {
    printf("Large");
}
```

কারণ `*p` একটি value-এর মতো behave করে।

---

# 13. `*p` Assignment-এর Left Side-এও হতে পারে

```c
*p = 500;
```

এখানে `*p` হলো এমন location যেখানে value রাখা যায়।

এটাকে সহজভাবে ভাবতে পারো:

```text
*p
↓
p যে object-কে point করছে
```

তাই সেখানে নতুন value assign করা যায়।

---

# 14. দুইটি Variable এবং দুইটি Pointer

```c
#include <stdio.h>

int main() {

    int a = 10;
    int b = 20;

    int *p = &a;
    int *q = &b;

    printf("%d\n", *p);
    printf("%d\n", *q);

    return 0;
}
```

Output:

```text
10
20
```

---

# 15. Pointer Reassignment

```c
#include <stdio.h>

int main() {

    int a = 10;
    int b = 20;

    int *p = &a;

    printf("%d\n", *p);

    p = &b;

    printf("%d\n", *p);

    return 0;
}
```

Output:

```text
10
20
```

কারণ প্রথমে:

```text
p → a
```

তারপর:

```text
p → b
```

---

# 16. Pointer দিয়ে কোন Variable পরিবর্তন হবে?

ধরো:

```c
int a = 10;
int b = 20;

int *p = &a;
```

এখন:

```c
*p = 100;
```

তাহলে:

```text
a = 100
b = 20
```

কারণ `p` শুধু `a`-কে point করছে।

---

# 17. তারপর Pointer অন্যদিকে

```c
p = &b;
```

এখন:

```c
*p = 200;
```

তাহলে:

```text
a = 100
b = 200
```

---

# 18. Pointer দিয়ে Swap 🔥

এবার আমরা একটি classic problem করি।

```c
#include <stdio.h>

int main() {

    int a = 10;
    int b = 20;

    int *p = &a;
    int *q = &b;

    int temp = *p;

    *p = *q;
    *q = temp;

    printf("a = %d\n", a);
    printf("b = %d\n", b);

    return 0;
}
```

Output:

```text
a = 20
b = 10
```

---

# 19. Swap কীভাবে হলো?

শুরুতে:

```text
a = 10
b = 20
```

Pointers:

```text
p → a
q → b
```

তাই:

```text
*p = 10
*q = 20
```

তারপর:

```c
int temp = *p;
```

তাই:

```text
temp = 10
```

তারপর:

```c
*p = *q;
```

ফলে:

```text
a = 20
```

শেষে:

```c
*q = temp;
```

ফলে:

```text
b = 10
```

---

# 20. `*` Declaration বনাম Dereference

আবার গুরুত্বপূর্ণ distinction:

### Declaration

```c
int *p;
```

এখানে `*` বলছে:

> `p` একটি pointer।

### Dereference

```c
*p
```

এখানে `*` বলছে:

> `p` যে object-কে point করছে তার value access করো।

একই symbol, কিন্তু context অনুযায়ী meaning আলাদা।

---

# 21. NULL Pointer ⚠️

```c
int *p = NULL;
```

এখন:

```c
*p
```

করা যাবে না।

কারণ `p` কোনো valid object-কে point করছে না।

সঠিক pattern:

```c
if (p != NULL) {
    printf("%d\n", *p);
}
```

---

# 22. Uninitialized Pointer ⚠️

এটা বিপজ্জনক:

```c
int *p;

*p = 100;
```

`p` কোথায় point করছে জানা নেই।

সঠিক:

```c
int x;

int *p = &x;

*p = 100;
```

এখন:

```text
x = 100
```

---

# 23. Pointer দিয়ে User Input

এখন `scanf()`-কে আবার নতুনভাবে বুঝতে পারো।

```c
int age;

scanf("%d", &age);
```

এখানে:

```text
&age
↓
age-এর address
```

`scanf()` সেই address ব্যবহার করে `age`-এর value লিখে।

---

# 24. Pointer Variable ব্যবহার করে `scanf()`

ধরো:

```c
int age;
int *p = &age;
```

তাহলে:

```c
scanf("%d", p);
```

এটাও কাজ করবে।

কারণ:

```text
p → age-এর address
```

এবং `scanf()`-এর `%d` একটি `int *` address চায়।

Complete example:

```c
#include <stdio.h>

int main() {

    int age;
    int *p = &age;

    printf("Enter age: ");
    scanf("%d", p);

    printf("Age = %d\n", age);

    return 0;
}
```

---

# 25. `scanf("%d", &age)` বনাম `scanf("%d", p)`

যদি:

```c
int age;
int *p = &age;
```

তাহলে:

```c
scanf("%d", &age);
```

এবং:

```c
scanf("%d", p);
```

দুটিই একই memory location-এর address দিচ্ছে।

কারণ:

```text
p == &age
```

---

# 26. Function-এর আগে এই Concept গুরুত্বপূর্ণ

পরের lessons-এ আমরা এমন function লিখব:

```c
void change(int *p)
```

তারপর:

```c
change(&x);
```

Function-এর ভিতরে:

```c
*p = 100;
```

এভাবে function থেকে caller-এর variable পরিবর্তন করা যায়।

এটাই pointers-এর অন্যতম গুরুত্বপূর্ণ practical use।

---

# 27. একটি Realistic Example

ধরো account balance:

```c
int balance = 1000;
int *ptr = &balance;
```

তারপর:

```c
*ptr = *ptr + 500;
```

balance হয়ে যাবে:

```text
1500
```

অর্থাৎ pointer ব্যবহার করে যে object-কে point করছে তার stored value পরিবর্তন করা যায়।

---

# 28. Dereference-এর Mental Model

সবসময় এই প্রশ্ন করো:

> **`p` কোথায় point করছে?**

যদি:

```c
int x = 10;
int *p = &x;
```

তাহলে:

```text
p
↓
x
```

এখন:

```text
*p
↓
x-এর value
↓
10
```

---

# 29. Super Important Table ⭐

```text
int x = 10;
int *p = &x;
```

|Expression|Result|
|---|---|
|`x`|`10`|
|`&x`|x-এর address|
|`p`|x-এর address|
|`*p`|`10`|
|`&p`|p-এর address|

এই table-টা বুঝে ফেললে pointer-এর basic অনেক পরিষ্কার হয়ে যাবে।

---

# 🧪 Practice 1

Output predict করো:

```c
int x = 20;
int *p = &x;

*p = 50;

printf("%d\n", x);
printf("%d\n", *p);
```

---

# 🧪 Practice 2

এই code complete করো:

```c
int a = 10;
int b = 30;

int *p = &a;
int *q = &b;

// এখানে pointer ব্যবহার করে
// a = 30
// b = 10
```

---

# 🧪 Practice 3

একটি integer input নাও।

তারপর pointer ব্যবহার করে:

```text
Original: 10
Double: 20
```

করো।

Hint:

```c
*p = *p * 2;
```

---

# 🔥 Challenge — Maximum Using Pointers

দুটি integer:

```text
a = 45
b = 72
```

দুটি pointer ব্যবহার করে কোনটি বড় সেটা বের করো।

Expected:

```text
Maximum = 72
```

Condition-এ pointer-এর value ব্যবহার করবে:

```c
*p
*q
```

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ⏳ Pointer + Array
42. ⏳ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 41 — Pointer + Array

এটা খুব গুরুত্বপূর্ণ lesson। আমরা দেখব:

```c
int arr[5] = {10, 20, 30, 40, 50};
```

এর সঙ্গে:

```c
int *p = arr;
```

এর কী সম্পর্ক, কেন `arr` অনেক ক্ষেত্রে প্রথম element-এর address-এর মতো behave করে, এবং কীভাবে pointer ব্যবহার করে **array traversal** করা যায়।

----

# 🔥 Lesson 41 — Pointer + Array

এটা C-এর সবচেয়ে গুরুত্বপূর্ণ pointer concepts-এর একটি। আজ আমরা বুঝব:

```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;
```

এখানে **array এবং pointer-এর সম্পর্ক কী**, কীভাবে pointer দিয়ে array access করা যায়, এবং `arr[i]` ও `*(arr + i)` কেন একই value দেয়।

---

# 1. আগে Array মনে করি

ধরো:

```c
int arr[5] = {10, 20, 30, 40, 50};
```

Array:

```text
Index:     0    1    2    3    4
          ┌────┬────┬────┬────┬────┐
Value:    │ 10 │ 20 │ 30 │ 40 │ 50 │
          └────┴────┴────┴────┴────┘
```

C-তে array-এর elements memory-তে **পরপর** থাকে।

---

# 2. Array-এর Address

ধরো:

```c
int arr[5] = {10, 20, 30, 40, 50};
```

তাহলে:

```c
&arr[0]
```

হলো প্রথম element-এর address।

আর খুব গুরুত্বপূর্ণ:

```c
arr
```

বেশিরভাগ expression context-এ প্রথম element-এর address-এর মতো behave করে।

অর্থাৎ:

```text
arr
↓
&arr[0]
```

---

# 3. Pointer দিয়ে Array ধরতে পারি

```c
int arr[5] = {10, 20, 30, 40, 50};

int *p = arr;
```

এখন:

```text
p
↓
arr[0]
```

অর্থাৎ:

```text
*p
```

দিলে:

```text
10
```

---

# 4. প্রথম Example

```c
#include <stdio.h>

int main() {

    int arr[5] = {10, 20, 30, 40, 50};

    int *p = arr;

    printf("%d\n", *p);

    return 0;
}
```

Output:

```text
10
```

কারণ:

```text
p → arr[0]
```

তাই:

```text
*p → arr[0] → 10
```

---

# 5. `arr` এবং `&arr[0]`

এই দুটো:

```c
arr
```

এবং:

```c
&arr[0]
```

সাধারণ expression-এ একই প্রথম element-এর address নির্দেশ করে।

তাই:

```c
int *p = arr;
```

এবং:

```c
int *p = &arr[0];
```

দুটোই valid।

---

# 6. Pointer দিয়ে দ্বিতীয় Element

ধরো:

```c
int arr[5] = {10, 20, 30, 40, 50};

int *p = arr;
```

তাহলে:

```c
*(p + 1)
```

এর value:

```text
20
```

কারণ:

```text
p       → arr[0]
p + 1   → arr[1]
p + 2   → arr[2]
```

---

# 7. পুরো Array

```text
arr
 ↓
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │
└────┴────┴────┴────┴────┘
 ↑
 p
```

তারপর:

```text
p + 1 → 20
p + 2 → 30
p + 3 → 40
p + 4 → 50
```

Dereference করলে:

```text
*(p + 0) → 10
*(p + 1) → 20
*(p + 2) → 30
*(p + 3) → 40
*(p + 4) → 50
```

---

# 8. `arr[i]` বনাম `*(arr + i)` 🔥

এটা C-এর খুব famous relationship:

```c
arr[i]
```

এবং:

```c
*(arr + i)
```

একই element access করে।

যেমন:

```c
arr[2]
```

মানে:

```c
*(arr + 2)
```

তাই:

```c
printf("%d\n", arr[2]);
printf("%d\n", *(arr + 2));
```

দুটিই:

```text
30
```

দেবে।

---

# 9. কেন এমন?

C-এর indexing internally pointer arithmetic-এর সঙ্গে closely related।

Conceptually:

```text
arr[i]
↓
*(arr + i)
```

তাই:

```text
arr[0] → *(arr + 0)
arr[1] → *(arr + 1)
arr[2] → *(arr + 2)
```

---

# 10. Example

```c
#include <stdio.h>

int main() {

    int arr[5] = {10, 20, 30, 40, 50};

    printf("%d\n", arr[0]);
    printf("%d\n", *(arr + 0));

    printf("%d\n", arr[3]);
    printf("%d\n", *(arr + 3));

    return 0;
}
```

Output:

```text
10
10
40
40
```

---

# 11. Pointer Arithmetic কী?

ধরো:

```c
int *p = arr;
```

তখন:

```c
p + 1
```

মানে "এক byte সামনে যাও" **নয়**।

বরং:

> পরের `int` object-এর দিকে যাও।

যদি `sizeof(int)` 4 bytes হয়, তাহলে conceptually:

```text
p      → address 1000
p + 1  → address 1004
p + 2  → address 1008
```

কিন্তু exact address system-এর ওপর নির্ভর করবে।

---

# 12. কেন `p + 1` এক element এগোয়?

কারণ compiler জানে:

```c
int *p;
```

মানে `p` একটি `int`-এর দিকে point করছে।

তাই pointer arithmetic type-aware।

যেমন:

```c
char *p;
```

হলে `p + 1` পরের `char` object-এর দিকে যায়।

---

# 13. Pointer দিয়ে Array Print

```c
#include <stdio.h>

int main() {

    int arr[5] = {10, 20, 30, 40, 50};

    int *p = arr;

    for (int i = 0; i < 5; i++) {
        printf("%d\n", *(p + i));
    }

    return 0;
}
```

Output:

```text
10
20
30
40
50
```

---

# 14. Array Traversal — দুইভাবে

### Normal Array

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", arr[i]);
}
```

### Pointer

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", *(arr + i));
}
```

দুটোই একই elements access করছে।

---

# 15. Pointer Increment

Pointer-কে increment করা যায়:

```c
p++;
```

ধরো:

```text
p → arr[0]
```

তারপর:

```c
p++;
```

তাহলে:

```text
p → arr[1]
```

আবার:

```c
p++;
```

তাহলে:

```text
p → arr[2]
```

---

# 16. Example

```c
#include <stdio.h>

int main() {

    int arr[3] = {10, 20, 30};

    int *p = arr;

    printf("%d\n", *p);

    p++;
    printf("%d\n", *p);

    p++;
    printf("%d\n", *p);

    return 0;
}
```

Output:

```text
10
20
30
```

---

# 17. `p++` কী করছে?

প্রথমে:

```text
p → arr[0]
```

তারপর:

```c
p++;
```

হলে:

```text
p → arr[1]
```

আবার:

```c
p++;
```

হলে:

```text
p → arr[2]
```

---

# 18. Pointer দিয়ে Reverse Traversal

Array:

```c
int arr[5] = {10, 20, 30, 40, 50};
```

শেষ element-এর address:

```c
int *p = &arr[4];
```

তারপর:

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", *p);
    p--;
}
```

Output:

```text
50 40 30 20 10
```

---

# 19. Pointer দিয়ে Array Modify

Pointer শুধু read করতে পারে না—**modify-ও করতে পারে**।

```c
#include <stdio.h>

int main() {

    int arr[3] = {10, 20, 30};

    int *p = arr;

    *p = 100;

    printf("%d\n", arr[0]);

    return 0;
}
```

Output:

```text
100
```

কারণ:

```text
p → arr[0]
```

তাই:

```c
*p = 100;
```

মানে:

```c
arr[0] = 100;
```

---

# 20. পরের Element Modify

```c
*(p + 1) = 200;
```

তাহলে:

```text
arr[1] = 200
```

Example:

```c
#include <stdio.h>

int main() {

    int arr[3] = {10, 20, 30};

    int *p = arr;

    *(p + 1) = 200;

    printf("%d %d %d\n",
           arr[0],
           arr[1],
           arr[2]);

    return 0;
}
```

Output:

```text
10 200 30
```

---

# 21. Pointer দিয়ে পুরো Array Modify

```c
#include <stdio.h>

int main() {

    int arr[5] = {1, 2, 3, 4, 5};

    int *p = arr;

    for (int i = 0; i < 5; i++) {
        *(p + i) = *(p + i) * 2;
    }

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

Output:

```text
2 4 6 8 10
```

---

# 22. Pointer Increment Style

এই:

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", *(p + i));
}
```

এর বদলে pointer নিজেই এগিয়ে নিতে পারি:

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", *p);
    p++;
}
```

দুটোতেই array traverse করা হচ্ছে।

---

# 23. Important: `p++` বনাম `(*p)++`

এ দুটো এক নয়!

### `p++`

```c
p++;
```

মানে:

> pointer-কে পরের element-এর দিকে move করো।

### `(*p)++`

```c
(*p)++;
```

মানে:

> pointer যে value-কে point করছে সেটি 1 বাড়াও।

🔥 এই পার্থক্য খুব গুরুত্বপূর্ণ।

---

# 24. Example

```c
int arr[3] = {10, 20, 30};

int *p = arr;
```

যদি:

```c
p++;
```

হয়:

```text
p → arr[1]
```

কিন্তু:

```c
(*p)++;
```

হলে:

```text
arr[0] = 11
```

Pointer নিজে move করে না।

---

# 25. আরেকটি Important Difference

```c
*p++
```

এবং:

```c
(*p)++
```

এক নয়।

`*p++` operator precedence-এর কারণে সাধারণভাবে interpreted হয়:

```c
*(p++)
```

অর্থাৎ pointer increment হবে, তারপর পুরনো pointed-to value expression-এ ব্যবহৃত হবে।

আর:

```c
(*p)++
```

pointed-to value increment করে।

Beginner হিসেবে ambiguous code না লিখে parentheses ব্যবহার করাই ভালো।

---

# 26. Array-এর বাইরে যেও না ⚠️

ধরো:

```c
int arr[3] = {10, 20, 30};
int *p = arr;
```

Valid:

```text
p       → arr[0]
p + 1   → arr[1]
p + 2   → arr[2]
```

Array-এর element access হিসেবে:

```text
*(p + 3)
```

করো না।

এটা array bounds-এর বাইরে চলে যাবে এবং undefined behavior হতে পারে।

---

# 27. একটি Subtle কিন্তু Important Rule

C-তে pointer arithmetic array-এর context-এ খুব useful।

```c
p + 1
```

এর মানে next element।

কিন্তু pointer arithmetic **arbitrary unrelated objects-এর মধ্যে** ব্যবহার করা যাবে না।

এখন শুধু এই rule মনে রাখো:

> Pointer যখন একই array-এর elements-এর মধ্যে point করছে, তখন `+`, `-`, `++`, `--` ব্যবহার করা যায়।

---

# 28. Array Name Reassign করা যায় না

এটা করা যাবে না:

```c
int arr[3] = {10, 20, 30};

arr = arr + 1;   // ❌
```

কারণ `arr` একটি array, normal modifiable pointer variable নয়।

কিন্তু:

```c
int *p = arr;

p++;
```

valid।

কারণ `p` একটি pointer variable।

---

# 29. `arr` বনাম `p`

```c
int arr[3] = {10, 20, 30};
int *p = arr;
```

এখন:

```text
arr → array
p   → pointer variable
```

তাই:

```c
p++;
```

valid।

কিন্তু:

```c
arr++;
```

invalid।

---

# 30. `sizeof(arr)` বনাম `sizeof(p)` 🔥

এখানে একটি গুরুত্বপূর্ণ difference:

```c
int arr[5];
int *p = arr;
```

তখন:

```c
sizeof(arr)
```

পুরো array-এর size দেয়।

কিন্তু:

```c
sizeof(p)
```

শুধু pointer-এর size দেয়।

Example যদি `int` 4 bytes হয় এবং pointer 8 bytes হয়:

```text
sizeof(arr) = 20
sizeof(p)   = 8
```

এগুলো system অনুযায়ী ভিন্ন হতে পারে।

---

# 31. Function-এর সঙ্গে Array + Pointer

C-তে array function-এ pass করার সময় pointer concept খুব গুরুত্বপূর্ণ।

যেমন:

```c
void printArray(int *p, int size)
```

এখানে:

```c
int arr[5] = {10, 20, 30, 40, 50};

printArray(arr, 5);
```

`arr` function call-এ প্রথম element-এর address হিসেবে pass হতে পারে।

পরের lesson-এ আমরা এটাকে বিস্তারিতভাবে **Pointer + Function** হিসেবে শিখব।

---

# 32. Complete Example — Sum Using Pointer

```c
#include <stdio.h>

int main() {

    int arr[5] = {10, 20, 30, 40, 50};

    int *p = arr;

    int sum = 0;

    for (int i = 0; i < 5; i++) {
        sum += *(p + i);
    }

    printf("Sum = %d\n", sum);

    return 0;
}
```

Output:

```text
Sum = 150
```

---

# 33. Maximum Using Pointer

```c
#include <stdio.h>

int main() {

    int arr[5] = {12, 45, 7, 89, 34};

    int *p = arr;
    int max = *p;

    for (int i = 1; i < 5; i++) {

        if (*(p + i) > max) {
            max = *(p + i);
        }
    }

    printf("Maximum = %d\n", max);

    return 0;
}
```

Output:

```text
Maximum = 89
```

---

# 34. আজকের Golden Formula 🔥

Array:

```c
int arr[5];
```

Pointer:

```c
int *p = arr;
```

তখন:

```text
arr[0]      == *p
arr[1]      == *(p + 1)
arr[2]      == *(p + 2)
arr[3]      == *(p + 3)
arr[4]      == *(p + 4)
```

আর:

```text
arr[i] == *(arr + i)
```

এটা C-এর একটি অত্যন্ত গুরুত্বপূর্ণ relationship।

---

# 🧠 Cheat Sheet

```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;
```

### First element

```c
*p
```

→ `10`

### Second

```c
*(p + 1)
```

→ `20`

### Third

```c
*(p + 2)
```

→ `30`

### Pointer move

```c
p++;
```

→ পরের element

### Value change

```c
(*p)++;
```

→ current element-এর value 1 বাড়ে

### Array indexing

```c
arr[i]
```

সমতুল্য:

```c
*(arr + i)
```

---

# 🧪 Practice 1

Output কী হবে?

```c
int arr[] = {5, 10, 15, 20};

int *p = arr;

printf("%d\n", *p);

p++;

printf("%d\n", *p);
```

---

# 🧪 Practice 2

এই array:

```c
int arr[5] = {2, 4, 6, 8, 10};
```

pointer ব্যবহার করে সব element print করো।

**`arr[i]` ব্যবহার করবে না।**

---

# 🧪 Practice 3

Pointer ব্যবহার করে array-এর সব value **double** করো।

Input:

```text
1 2 3 4 5
```

Expected:

```text
2 4 6 8 10
```

---

# 🔥 Challenge

Pointer ব্যবহার করে একটি array-এর:

1. Sum
    
2. Maximum
    
3. Minimum
    

বের করো।

Array:

```c
int arr[7] = {15, 3, 42, 8, 27, 11, 5};
```

**Challenge-এর শর্ত:** element access করার সময় `arr[i]` ব্যবহার করবে না। ব্যবহার করবে:

```c
*(p + i)
```

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ✅ Pointer + Array
42. ⏳ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 42 — Pointer + Function

এখানে আমরা C-এর একটি অত্যন্ত গুরুত্বপূর্ণ বিষয় শিখব:

```c
void change(int *p)
```

কীভাবে pointer function-এর মাধ্যমে **original variable পরিবর্তন** করতে দেয়, এবং কেন C-তে সাধারণভাবে **call by value** হলেও pointer ব্যবহার করে caller-এর data modify করা যায়।


----
# 🔥 Lesson 42 — Pointer + Function

আজ আমরা **Pointer + Function** শিখব। এটা C-এর সবচেয়ে গুরুত্বপূর্ণ concepts-এর একটি, কারণ এখান থেকেই বুঝবে কীভাবে একটি function **original variable-এর value পরিবর্তন** করতে পারে।

---

# 1. আগে Function-এর Basic

ধরো:

```c
void change(int x)
{
    x = 100;
}
```

এখন:

```c
int main()
{
    int a = 10;

    change(a);

    printf("%d\n", a);
}
```

Output:

```text
10
```

কেন `100` হলো না?

কারণ C-তে function argument সাধারণভাবে **copy হিসেবে যায়**।

---

# 2. Call by Value

```c
int a = 10;

change(a);
```

ধারণাগতভাবে:

```text
main-এর a
   │
   │ copy
   ↓
function-এর x
```

তাই:

```c
x = 100;
```

করলে function-এর `x` বদলায়।

কিন্তু original `a` বদলায় না।

---

# 3. Pointer দিয়ে সমাধান 🔥

আমরা `a`-এর address function-এ পাঠাতে পারি।

```c
void change(int *p)
{
    *p = 100;
}
```

তারপর:

```c
int a = 10;

change(&a);
```

এখন `a` পরিবর্তন হবে।

---

# 4. Complete Example

```c
#include <stdio.h>

void change(int *p)
{
    *p = 100;
}

int main()
{
    int a = 10;

    printf("Before = %d\n", a);

    change(&a);

    printf("After = %d\n", a);

    return 0;
}
```

Output:

```text
Before = 10
After = 100
```

---

# 5. কীভাবে কাজ করল?

Main-এ:

```c
int a = 10;
```

তারপর:

```c
change(&a);
```

এখানে:

```text
&a
 ↓
a-এর address
```

Function receives:

```c
int *p
```

অর্থাৎ:

```text
p → a
```

তারপর:

```c
*p = 100;
```

মানে:

> `p` যে variable-কে point করছে তার value 100 করো।

সেটা হলো `a`।

তাই:

```text
a = 100
```

---

# 6. Visual Diagram

```text
main()

a
┌───────┐
│  10   │
└───────┘
   ↑
   │
   │ &a
   │
   p
┌──────────────┐
│ address of a │
└──────────────┘
```

Function:

```c
*p = 100;
```

এর ফলে:

```text
a
┌───────┐
│ 100   │
└───────┘
```

---

# 7. Function Declaration

এখানে:

```c
void change(int *p)
```

মানে:

- `change` একটি function
    
- এটি কিছু return করে না → `void`
    
- এটি একটি `int` object-এর address নেয় → `int *p`
    

---

# 8. Function Call

```c
change(&a);
```

এখানে `&a` হলো:

```text
a-এর address
```

Function-এর:

```c
int *p
```

সেই address গ্রহণ করে।

তাই:

```text
p → a
```

---

# 9. Normal Function বনাম Pointer Function

### Pointer ছাড়া

```c
void change(int x)
{
    x = 100;
}
```

Call:

```c
change(a);
```

Original `a` পরিবর্তন হবে না।

### Pointer সহ

```c
void change(int *x)
{
    *x = 100;
}
```

Call:

```c
change(&a);
```

Original `a` পরিবর্তন হবে।

---

# 10. আরেকটি Example — Increment

```c
#include <stdio.h>

void increment(int *x)
{
    (*x)++;
}

int main()
{
    int n = 10;

    increment(&n);

    printf("%d\n", n);

    return 0;
}
```

Output:

```text
11
```

---

# 11. `(*x)++` কেন?

এখানে:

```c
(*x)++;
```

মানে:

> `x` যে variable-কে point করছে তার value 1 বাড়াও।

এটা:

```c
x++;
```

এর মতো নয়।

`x++` pointer-কে move করবে।

---

# 12. Function দিয়ে দুইটি Variable পরিবর্তন

ধরো:

```c
int a = 10;
int b = 20;
```

আমরা function দিয়ে দুটোই change করতে পারি।

```c
void change(int *x, int *y)
{
    *x = 100;
    *y = 200;
}
```

Call:

```c
change(&a, &b);
```

Complete:

```c
#include <stdio.h>

void change(int *x, int *y)
{
    *x = 100;
    *y = 200;
}

int main()
{
    int a = 10;
    int b = 20;

    change(&a, &b);

    printf("a = %d\n", a);
    printf("b = %d\n", b);

    return 0;
}
```

Output:

```text
a = 100
b = 200
```

---

# 13. Pointer Function দিয়ে Swap 🔥

এবার classic swap:

```c
#include <stdio.h>

void swap(int *a, int *b)
{
    int temp = *a;

    *a = *b;
    *b = temp;
}

int main()
{
    int x = 10;
    int y = 20;

    printf("Before: x = %d, y = %d\n", x, y);

    swap(&x, &y);

    printf("After: x = %d, y = %d\n", x, y);

    return 0;
}
```

Output:

```text
Before: x = 10, y = 20
After: x = 20, y = 10
```

---

# 14. Swap-এর ভিতরে কী হচ্ছে?

Call:

```c
swap(&x, &y);
```

Function-এর ভিতরে:

```text
a → x
b → y
```

তাই:

```text
*a → x-এর value
*b → y-এর value
```

শুরুতে:

```text
*a = 10
*b = 20
```

তারপর:

```c
temp = *a;
```

```text
temp = 10
```

তারপর:

```c
*a = *b;
```

```text
x = 20
```

শেষে:

```c
*b = temp;
```

```text
y = 10
```

---

# 15. কেন `swap(x, y)` কাজ করবে না?

যদি function হয়:

```c
void swap(int *a, int *b)
```

তাহলে call করতে হবে:

```c
swap(&x, &y);
```

কারণ function address চায়।

এটা:

```c
swap(x, y);
```

সঠিক type-এর argument নয়।

---

# 16. Function দিয়ে দুটি Number-এর Sum

এখানে pointer দরকার নেই যদি শুধু একটি value return করতে চাই:

```c
int add(int a, int b)
{
    return a + b;
}
```

কিন্তু pointer-এর ব্যবহার বুঝতে আমরা অন্যভাবে output দিতে পারি:

```c
void add(int a, int b, int *result)
{
    *result = a + b;
}
```

Call:

```c
int result;

add(10, 20, &result);
```

এখন:

```text
result = 30
```

---

# 17. Complete Example

```c
#include <stdio.h>

void add(int a, int b, int *result)
{
    *result = a + b;
}

int main()
{
    int result;

    add(10, 20, &result);

    printf("Result = %d\n", result);

    return 0;
}
```

Output:

```text
Result = 30
```

---

# 18. কেন এটা Useful?

একটি function সাধারণভাবে একটি value return করতে পারে:

```c
return value;
```

কিন্তু pointer ব্যবহার করলে function-এর মাধ্যমে **multiple outputs** পরিবর্তন করা সম্ভব।

যেমন:

```c
void calculate(int a, int b, int *sum, int *difference)
{
    *sum = a + b;
    *difference = a - b;
}
```

---

# 19. Multiple Outputs 🔥

```c
#include <stdio.h>

void calculate(
    int a,
    int b,
    int *sum,
    int *difference
)
{
    *sum = a + b;
    *difference = a - b;
}

int main()
{
    int sum;
    int difference;

    calculate(20, 8, &sum, &difference);

    printf("Sum = %d\n", sum);
    printf("Difference = %d\n", difference);

    return 0;
}
```

Output:

```text
Sum = 28
Difference = 12
```

এখানে function দুটি output তৈরি করেছে।

---

# 20. Pointer + Array + Function 🔥🔥

এখন আগের lesson-এর সঙ্গে আজকের lesson combine করি।

```c
void printArray(int *p, int size)
{
    for (int i = 0; i < size; i++)
    {
        printf("%d ", *(p + i));
    }
}
```

Main:

```c
int arr[] = {10, 20, 30, 40, 50};

printArray(arr, 5);
```

Complete:

```c
#include <stdio.h>

void printArray(int *p, int size)
{
    for (int i = 0; i < size; i++)
    {
        printf("%d ", *(p + i));
    }
}

int main()
{
    int arr[] = {10, 20, 30, 40, 50};

    printArray(arr, 5);

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

---

# 21. Function-এর ভিতরে Array Modify

আরও powerful example:

```c
#include <stdio.h>

void doubleArray(int *p, int size)
{
    for (int i = 0; i < size; i++)
    {
        *(p + i) *= 2;
    }
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5};

    doubleArray(arr, 5);

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

Output:

```text
2 4 6 8 10
```

Function-এর ভিতরে array-এর original values পরিবর্তন হয়েছে।

---

# 22. কেন Array Function-এ Modify করা যায়?

কারণ function call:

```c
doubleArray(arr, 5);
```

এখানে `arr` প্রথম element-এর address-এর মতো pass হয়।

তাই:

```text
p → arr[0]
```

এবং:

```c
*(p + i)
```

দিয়ে original array-এর elements access করা যায়।

---

# 23. একটি Important Clarification

C-তে technically **"call by reference" নামে আলাদা parameter-passing mechanism নেই**।

C মূলত **pass by value** ব্যবহার করে।

Pointer ব্যবহার করলে:

```c
change(&x);
```

এখানে `x`-এর address-টির একটি **copy** function-এর pointer parameter-এ যায়।

তবুও সেই copied address একই object-কে point করে, তাই:

```c
*p = 100;
```

দিয়ে original object পরিবর্তন করা যায়।

এটা terminology হিসেবে খুব গুরুত্বপূর্ণ।

---

# 24. এই Diagram মনে রাখো

```text
main:

x = 10
│
│ &x
↓
address
│
│ copy
↓
function:

p = address of x
│
│
↓
*p = x
```

অর্থাৎ function-এর `p` আলাদা pointer variable হলেও সেটি `x`-এর একই object-কে point করছে।

---

# 25. NULL Check

Pointer parameter ব্যবহার করার সময় কখনও কখনও NULL check করা যায়:

```c
void change(int *p)
{
    if (p != NULL)
    {
        *p = 100;
    }
}
```

Call:

```c
int x = 10;

change(&x);
```

এটা valid।

কিন্তু:

```c
change(NULL);
```

হলে function `*p` dereference করবে না, কারণ check আছে।

---

# 26. Dangerous Version

এটা:

```c
void change(int *p)
{
    *p = 100;
}
```

এরপর:

```c
change(NULL);
```

করলে invalid dereference হবে।

তাই pointer parameter-এর contract বোঝা গুরুত্বপূর্ণ।

---

# 27. Real-World Example — Bank Balance

ধরো:

```c
void deposit(int *balance, int amount)
{
    *balance += amount;
}
```

Main:

```c
int balance = 1000;

deposit(&balance, 500);
```

তারপর:

```text
balance = 1500
```

Complete:

```c
#include <stdio.h>

void deposit(int *balance, int amount)
{
    *balance += amount;
}

int main()
{
    int balance = 1000;

    deposit(&balance, 500);

    printf("Balance = %d\n", balance);

    return 0;
}
```

এটা তোমার পরের **Bank Management System** project-এ খুব কাজে আসবে।

---

# 28. Real-World Example — Score

```c
void addBonus(int *score)
{
    *score += 10;
}
```

Call:

```c
int score = 80;

addBonus(&score);
```

Result:

```text
score = 90
```

---

# 29. আজকের Golden Pattern 🔥

যখন function-কে original variable modify করতে দিতে চাও:

### Step 1

Function parameter pointer:

```c
void change(int *p)
```

### Step 2

Function call-এ address:

```c
change(&x);
```

### Step 3

Function-এর ভিতরে dereference:

```c
*p = ...;
```

তিনটি একসাথে:

```text
int *p
  +
&x
  +
*p
```

---

# 🧠 Cheat Sheet

### Normal

```c
void change(int x)
{
    x = 100;
}
```

```c
change(a);
```

→ original `a` পরিবর্তন হয় না।

### Pointer

```c
void change(int *x)
{
    *x = 100;
}
```

```c
change(&a);
```

→ original `a` পরিবর্তন হয়।

---

# 🧪 Practice 1 — Increment

একটি function লেখো:

```c
void increment(int *x)
```

যেটি original variable-এর value 1 বাড়াবে।

Expected:

```text
Before = 10
After = 11
```

---

# 🧪 Practice 2 — Swap

এই function complete করো:

```c
void swap(int *a, int *b)
{
    // তোমার code
}
```

Main:

```c
int x = 100;
int y = 200;

swap(&x, &y);
```

Expected:

```text
x = 200
y = 100
```

---

# 🧪 Practice 3 — Multiple Outputs

এই function complete করো:

```c
void calculate(int a, int b, int *sum, int *product)
{
    // তোমার code
}
```

যাতে:

```text
a = 5
b = 4

sum = 9
product = 20
```

হয়।

---

# 🔥 Challenge — Array Function

একটি function বানাও:

```c
void findMinMax(int *arr, int size, int *min, int *max)
```

এটি একটি array থেকে একই সঙ্গে:

- Minimum
    
- Maximum
    

বের করবে।

Input:

```c
int arr[] = {12, 5, 87, 34, 9, 42};
```

Expected:

```text
Minimum = 5
Maximum = 87
```

**শর্ত:** `min` এবং `max` function-এর বাইরে পাওয়া যেতে হবে—তাই pointer ব্যবহার করতে হবে।

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ✅ Pointer + Array
42. ✅ Pointer + Function
43. ⏳ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 43 — Pointer + String

এবার আমরা দেখব:

```c
char name[] = "Rahim";
char *p = name;
```

কীভাবে string-এর প্রতিটি character pointer দিয়ে access করা যায়, `char *` এবং character array-এর সম্পর্ক কী, এবং pointer ব্যবহার করে string traversal কীভাবে করা হয়।

---
# 🔥 Lesson 43 — Pointer + String

আজ আমরা **Pointer + String** শিখব। C-তে String আর Pointer-এর সম্পর্ক খুবই গুরুত্বপূর্ণ—বিশেষ করে পরে **String functions, dynamic memory, data structures** শেখার সময়।

---

# 1. C-তে String কী?

C-তে আলাদা `string` data type নেই।

String হলো একটি **character array**, যার শেষে থাকে special character:

```c
'\0'
```

যাকে বলে **null character**।

যেমন:

```c
char name[] = "Rahim";
```

Memory-তে conceptually:

```text
┌────┬────┬────┬────┬────┬────┐
│ R  │ a  │ h  │ i  │ m  │ \0 │
└────┴────┴────┴────┴────┴────┘
   0    1    2    3    4    5
```

---

# 2. String-এর Pointer

ধরো:

```c
char name[] = "Rahim";
```

এখন:

```c
char *p = name;
```

এখানে:

```text
p
↓
name[0]
↓
'R'
```

তাই:

```c
printf("%c\n", *p);
```

Output:

```text
R
```

---

# 3. Complete Example

```c
#include <stdio.h>

int main()
{
    char name[] = "Rahim";

    char *p = name;

    printf("%c\n", *p);

    return 0;
}
```

Output:

```text
R
```

---

# 4. Pointer Increment

এখন:

```c
p++;
```

হলে pointer পরের character-এর দিকে যাবে।

```text
প্রথমে:

p → R

p++;

p → a
```

তাই:

```c
printf("%c\n", *p);
```

Output:

```text
a
```

---

# 5. পুরো String Traverse

```c
#include <stdio.h>

int main()
{
    char name[] = "Rahim";

    char *p = name;

    while (*p != '\0')
    {
        printf("%c", *p);
        p++;
    }

    return 0;
}
```

Output:

```text
Rahim
```

---

# 6. `'\0'` কেন গুরুত্বপূর্ণ?

String:

```c
char name[] = "Rahim";
```

আসলে memory-তে:

```text
R a h i m \0
```

`'\0'` দেখে program বুঝতে পারে:

> String শেষ।

তাই:

```c
while (*p != '\0')
```

মানে:

> যতক্ষণ character string-এর শেষের null character নয়, ততক্ষণ এগিয়ে যাও।

---

# 7. Pointer দিয়ে Character-by-Character

```c
char name[] = "Hello";

char *p = name;
```

তাহলে:

```text
*p       → H
*(p + 1) → e
*(p + 2) → l
*(p + 3) → l
*(p + 4) → o
```

এবং:

```text
*(p + 5) → '\0'
```

---

# 8. `name[i]` বনাম `*(name + i)`

Array-এর মতো String-এর ক্ষেত্রেও:

```c
name[i]
```

এবং:

```c
*(name + i)
```

একই character access করে।

যেমন:

```c
char name[] = "Rahim";
```

তাহলে:

```c
name[2]
```

→ `h`

এবং:

```c
*(name + 2)
```

→ `h`

---

# 9. Example

```c
#include <stdio.h>

int main()
{
    char name[] = "Programming";

    for (int i = 0; name[i] != '\0'; i++)
    {
        printf("%c ", name[i]);
    }

    printf("\n");

    for (char *p = name; *p != '\0'; p++)
    {
        printf("%c ", *p);
    }

    return 0;
}
```

দুই loop-ই একই string traverse করছে।

---

# 10. Pointer দিয়ে String Length

আমরা এখনো `strlen()` ব্যবহার করছি না।

নিজে বানাই:

```c
#include <stdio.h>

int main()
{
    char text[] = "Hello";

    char *p = text;

    int length = 0;

    while (*p != '\0')
    {
        length++;
        p++;
    }

    printf("Length = %d\n", length);

    return 0;
}
```

Output:

```text
Length = 5
```

---

# 11. Function + String + Pointer 🔥

আগের lesson-এর function-এর সঙ্গে combine করি।

```c
void printString(char *p)
{
    while (*p != '\0')
    {
        printf("%c", *p);
        p++;
    }
}
```

Call:

```c
char name[] = "Rahim";

printString(name);
```

Complete:

```c
#include <stdio.h>

void printString(char *p)
{
    while (*p != '\0')
    {
        printf("%c", *p);
        p++;
    }
}

int main()
{
    char name[] = "Rahim";

    printString(name);

    return 0;
}
```

Output:

```text
Rahim
```

---

# 12. String Function-এ `char *`

এখানে:

```c
void printString(char *p)
```

মানে function একটি `char`-এর address গ্রহণ করছে।

Call:

```c
printString(name);
```

এখানে `name` প্রথম character-এর address-এর মতো pass হচ্ছে।

তাই:

```text
p → name[0]
```

---

# 13. Pointer দিয়ে String Modify

যেহেতু `name` একটি character array:

```c
char name[] = "Rahim";
```

তাই pointer দিয়ে character পরিবর্তন করা যায়।

```c
#include <stdio.h>

int main()
{
    char name[] = "Rahim";

    char *p = name;

    *p = 'K';

    printf("%s\n", name);

    return 0;
}
```

Output:

```text
Kahim
```

কারণ:

```text
p → name[0]
```

এবং:

```c
*p = 'K';
```

মানে:

```c
name[0] = 'K';
```

---

# 14. দ্বিতীয় Character Change

```c
*(p + 1) = 'O';
```

তাহলে:

```text
Rahim
```

হয়ে যাবে:

```text
ROhim
```

Complete:

```c
#include <stdio.h>

int main()
{
    char name[] = "Rahim";

    char *p = name;

    *(p + 1) = 'O';

    printf("%s\n", name);

    return 0;
}
```

Output:

```text
ROhim
```

---

# 15. পুরো String Uppercase

ASCII-এর basic behavior ব্যবহার করে lowercase character uppercase করা যায়:

```c
#include <stdio.h>

int main()
{
    char text[] = "hello";

    char *p = text;

    while (*p != '\0')
    {
        if (*p >= 'a' && *p <= 'z')
        {
            *p = *p - 'a' + 'A';
        }

        p++;
    }

    printf("%s\n", text);

    return 0;
}
```

Output:

```text
HELLO
```

এখানে pointer সরাসরি original character array modify করছে।

---

# 16. String-এর শেষে Pointer

```c
char text[] = "Hello";

char *p = text;
```

যদি:

```c
while (*p != '\0')
{
    p++;
}
```

শেষে `p` গিয়ে `'\0'`-এর location-এ থাকবে।

অর্থাৎ:

```text
H e l l o \0
          ↑
          p
```

---

# 17. String Copy — Pointer দিয়ে

নিজের `strcpy()`-এর basic version বানাই:

```c
#include <stdio.h>

void copyString(char *dest, char *src)
{
    while (*src != '\0')
    {
        *dest = *src;

        dest++;
        src++;
    }

    *dest = '\0';
}

int main()
{
    char source[] = "Hello";
    char destination[20];

    copyString(destination, source);

    printf("%s\n", destination);

    return 0;
}
```

Output:

```text
Hello
```

---

# 18. Copy কীভাবে কাজ করছে?

শুরুতে:

```text
source:

H e l l o \0
↑
src


destination:

_ _ _ _ _ _ 
↑
dest
```

তারপর:

```c
*dest = *src;
```

প্রথম character copy:

```text
H
```

তারপর:

```c
dest++;
src++;
```

দুটো pointer-ই পরের character-এ যায়।

এভাবে শেষ পর্যন্ত:

```text
Hello\0
```

copy হয়।

---

# 19. `char *p = name` বনাম `char name[]`

এ দুটো দেখতে কাছাকাছি হলেও এক জিনিস নয়।

### Character array

```c
char name[] = "Rahim";
```

এখানে একটি array তৈরি হয়, যার characters modify করা যায়।

### Pointer to string literal

```c
char *p = "Rahim";
```

এখানে `p` একটি string literal-এর দিকে point করে।

**String literal modify করার চেষ্টা করা উচিত নয়।**

যেমন:

```c
*p = 'K';   // ❌
```

এটি undefined behavior হতে পারে।

---

# 20. নিরাপদ Rule ⭐

যদি string modify করতে চাও:

```c
char text[] = "Hello";
```

তারপর:

```c
char *p = text;
```

এটা ব্যবহার করো।

যদি শুধু read করতে চাও, string literal-এর ক্ষেত্রে:

```c
const char *p = "Hello";
```

লেখা ভালো practice।

---

# 21. `printf("%s", p)`

যদি:

```c
char name[] = "Rahim";
char *p = name;
```

তাহলে:

```c
printf("%s\n", p);
```

Output:

```text
Rahim
```

কারণ `%s` একটি null-terminated string-এর শুরু address আশা করে।

---

# 22. `%c` বনাম `%s`

এটা খুব গুরুত্বপূর্ণ:

```c
printf("%c", *p);
```

→ একটি character।

আর:

```c
printf("%s", p);
```

→ পুরো string।

যেমন:

```text
p → "Hello"
```

তাহলে:

```c
*p
```

→ `H`

কিন্তু:

```c
p
```

→ `"Hello"`-এর শুরু address।

---

# 23. `scanf()` দিয়ে String

একটি single-word string:

```c
char name[50];

scanf("%49s", name);
```

এখানে `name`-এর আগে `&` দরকার নেই।

কারণ `name` expression নিজেই প্রথম element-এর address-এর মতো behave করে।

---

# 24. Pointer দিয়ে `scanf()`

যদি:

```c
char name[50];

char *p = name;
```

তাহলে:

```c
scanf("%49s", p);
```

এটাও valid।

কারণ `p` প্রথম character-এর address ধরে রেখেছে।

---

# 25. Space সহ String

`scanf("%s", ...)` সাধারণত whitespace-এ থেমে যায়।

যেমন input:

```text
Md Rahim
```

তাহলে `%s` শুধু প্রথম অংশ নিতে পারে।

Space সহ line input-এর জন্য `fgets()` শেখা ভালো।

Example:

```c
char name[100];

fgets(name, sizeof(name), stdin);
```

এটা পরের string/file handling-এর সময় আরও বিস্তারিত করব।

---

# 26. Pointer দিয়ে String Compare-এর Basic Idea

দুটি string:

```c
char a[] = "cat";
char b[] = "cat";
```

Pointer দিয়ে character-by-character compare করা যায়:

```c
int same = 1;

char *p = a;
char *q = b;

while (*p != '\0' || *q != '\0')
{
    if (*p != *q)
    {
        same = 0;
        break;
    }

    p++;
    q++;
}
```

যদি সব character একই হয়, strings same।

---

# 27. Pointer দিয়ে Reverse String

ধরো:

```c
char text[] = "Hello";
```

প্রথমে end পর্যন্ত যাই:

```c
char *p = text;

while (*p != '\0')
{
    p++;
}
```

এখন `p` `'\0'`-এর location-এ।

তারপর এক ধাপ পিছিয়ে:

```c
p--;
```

এখন:

```text
H e l l o \0
        ↑
        p
```

তারপর backward traversal করা যায়।

---

# 28. তবে একটা বিষয় ⚠️

Pointer দিয়ে reverse print করা সহজ:

```c
while (p >= text)
{
    printf("%c", *p);
    p--;
}
```

কিন্তু pointer comparison-এর rules এবং object bounds carefully মানতে হয়। Beginner code-এ reverse করার জন্য index-based approach অনেক সময় পরিষ্কার।

---

# 29. Pointer + String + Function

এখন তিনটা concept একসাথে:

```c
#include <stdio.h>

int stringLength(char *p)
{
    int length = 0;

    while (*p != '\0')
    {
        length++;
        p++;
    }

    return length;
}

int main()
{
    char text[] = "Programming";

    int length = stringLength(text);

    printf("Length = %d\n", length);

    return 0;
}
```

Output:

```text
Length = 11
```

---

# 30. আজকের সবচেয়ে গুরুত্বপূর্ণ Pattern 🔥

String:

```c
char text[] = "Hello";
```

Pointer:

```c
char *p = text;
```

Character:

```c
*p
```

Next character:

```c
*(p + 1)
```

Pointer move:

```c
p++;
```

String শেষ কিনা:

```c
*p == '\0'
```

Traverse:

```c
while (*p != '\0')
{
    // কাজ
    p++;
}
```

---

# 🧠 Golden Table

ধরো:

```c
char text[] = "Hello";
char *p = text;
```

|Expression|Meaning|
|---|---|
|`text`|প্রথম character-এর address-এর মতো|
|`&text[0]`|প্রথম character-এর address|
|`p`|প্রথম character-এর address|
|`*p`|`H`|
|`*(p + 1)`|`e`|
|`*(p + 2)`|`l`|
|`text[2]`|`l`|
|`*(text + 2)`|`l`|
|`*p == '\0'`|string শেষ হয়েছে কি না|

---

# 🧪 Practice 1

Output কী হবে?

```c
char text[] = "CProgramming";

char *p = text;

printf("%c\n", *p);

p += 2;

printf("%c\n", *p);
```

---

# 🧪 Practice 2

Pointer ব্যবহার করে এই string-এর প্রতিটি character print করো:

```c
char text[] = "Bangladesh";
```

শর্ত:

```c
text[i]
```

ব্যবহার করবে না।

---

# 🧪 Practice 3

একটি function বানাও:

```c
int stringLength(char *p)
```

যেটি pointer ব্যবহার করে string-এর length return করবে।

`strlen()` ব্যবহার করবে না।

---

# 🔥 Challenge

এই function বানাও:

```c
void reversePrint(char *p)
```

যেটি string-টি reverse order-এ print করবে।

Input:

```text
Hello
```

Expected:

```text
olleH
```

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ✅ Pointer + Array
42. ✅ Pointer + Function
43. ✅ Pointer + String
44. ⏳ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 44 — Pointer to Pointer

এবার pointer-এর আরও এক level গভীরে যাব:

```c
int x = 10;

int *p = &x;
int **q = &p;
```

এখানে `q` কীভাবে `p`-এর address ধরে, এবং `**q` কীভাবে শেষ পর্যন্ত `x`-এর value `10`-এ পৌঁছে যায়—সেটা step-by-step দেখব।


----

# 🔥 Lesson 44 — Pointer to Pointer (`**`)

আজ আমরা Pointer-এর আরেকটি গুরুত্বপূর্ণ level শিখব:

```c
int **q;
```

এটাকে বলে **pointer to pointer**।

আগে ছিল:

```c
int x = 10;
int *p = &x;
```

এখন আমরা `p`-এর address-ও আরেকটি pointer দিয়ে ধরব।

---

# 1. প্রথমে Normal Variable

```c
int x = 10;
```

এখানে:

```text
x → 10
```

---

# 2. একটি Pointer

```c
int *p = &x;
```

এখন:

```text
p → x
```

অর্থাৎ:

```text
*p → 10
```

Diagram:

```text
p
│
│ points to
▼
x
┌──────┐
│  10  │
└──────┘
```

---

# 3. Pointer-এরও Address আছে

`p` নিজেও একটি variable।

তাই `p`-এর address আছে:

```c
&p
```

এখন আমরা `p`-এর address রাখব আরেকটি pointer-এ:

```c
int **q = &p;
```

এখানে:

```text
q → p → x
```

🔥 এটাই pointer to pointer।

---

# 4. Complete Example

```c
#include <stdio.h>

int main()
{
    int x = 10;

    int *p = &x;
    int **q = &p;

    printf("x = %d\n", x);
    printf("*p = %d\n", *p);
    printf("**q = %d\n", **q);

    return 0;
}
```

Output:

```text
x = 10
*p = 10
**q = 10
```

তিনটিই একই value `10` access করছে।

---

# 5. সবচেয়ে গুরুত্বপূর্ণ Diagram 🔥

```text
        q
        │
        ▼
      ┌───────┐
      │   p   │
      └───┬───┘
          │
          ▼
      ┌───────┐
      │   x   │
      │  10   │
      └───────┘
```

অর্থাৎ:

```text
q  →  p  →  x
```

---

# 6. `q` কী রাখে?

```c
int **q = &p;
```

তাই:

```text
q = p-এর address
```

আর:

```c
*q
```

মানে:

> `q` যে variable-কে point করছে তার value।

`q` যেহেতু `p`-কে point করছে:

```text
*q → p
```

---

# 7. `**q` কী?

এখন:

```c
*q
```

দিলে আমরা `p`-এ পৌঁছাই।

আর:

```c
**q
```

দিলে `p` যেটাকে point করছে সেখানে পৌঁছাই।

অর্থাৎ:

```text
**q → x → 10
```

---

# 8. Step-by-Step

ধরো:

```c
int x = 10;
int *p = &x;
int **q = &p;
```

### `x`

```text
x → 10
```

### `p`

```text
p → x
```

### `q`

```text
q → p
```

তাই:

```text
q
↓
p
↓
x
↓
10
```

---

# 9. `*q`

```c
printf("%p\n", (void *)*q);
```

`*q` হলো `p`-এর stored address।

অর্থাৎ:

```text
*q == p
```

Pointer value-এর দিক থেকে।

---

# 10. `**q`

```c
printf("%d\n", **q);
```

Output:

```text
10
```

কারণ:

```text
q → p → x
```

দুইবার dereference:

```text
*q  → p
**q → x-এর value
```

---

# 11. `***` কি সম্ভব?

হ্যাঁ!

```c
int x = 10;

int *p = &x;
int **q = &p;
int ***r = &q;
```

এখন:

```text
r → q → p → x
```

তাই:

```c
*r
```

→ `q`

```c
**r
```

→ `p`

```c
***r
```

→ `x`-এর value `10`

---

# 12. Example

```c
#include <stdio.h>

int main()
{
    int x = 10;

    int *p = &x;
    int **q = &p;
    int ***r = &q;

    printf("%d\n", x);
    printf("%d\n", *p);
    printf("%d\n", **q);
    printf("%d\n", ***r);

    return 0;
}
```

Output:

```text
10
10
10
10
```

তবে বাস্তব C programming-এ `***` সাধারণত খুব কম দরকার হয়।

---

# 13. Pointer to Pointer দিয়ে Original Value Change

এটা খুব গুরুত্বপূর্ণ।

```c
int x = 10;

int *p = &x;
int **q = &p;
```

এখন:

```c
**q = 100;
```

তাহলে:

```text
x = 100
```

কারণ:

```text
q → p → x
```

দুইবার dereference করে `x`-এ পৌঁছেছি।

---

# 14. Complete Example

```c
#include <stdio.h>

int main()
{
    int x = 10;

    int *p = &x;
    int **q = &p;

    **q = 500;

    printf("x = %d\n", x);

    return 0;
}
```

Output:

```text
x = 500
```

---

# 15. `q` দিয়ে Pointer Change করা

এবার আরও interesting:

```c
int a = 10;
int b = 20;

int *p = &a;
int **q = &p;
```

এখন:

```c
*q = &b;
```

এর মানে:

> `p`-এর ভিতরে `b`-এর address রাখো।

তাই:

```text
আগে:

q → p → a

পরে:

q → p → b
```

---

# 16. Complete Example

```c
#include <stdio.h>

int main()
{
    int a = 10;
    int b = 20;

    int *p = &a;
    int **q = &p;

    printf("%d\n", *p);

    *q = &b;

    printf("%d\n", *p);

    return 0;
}
```

Output:

```text
10
20
```

---

# 17. কীভাবে হলো?

শুরুতে:

```text
p → a
```

তাই:

```text
*p = 10
```

তারপর:

```c
*q = &b;
```

যেহেতু:

```text
q → p
```

তাই `*q` হলো `p`।

অর্থাৎ:

```c
*q = &b;
```

মূলত:

```c
p = &b;
```

এর মতো।

এখন:

```text
p → b
```

তাই:

```text
*p = 20
```

---

# 18. কেন Pointer to Pointer দরকার?

এটি বিশেষভাবে useful যখন কোনো function-কে **একটি pointer variable-কে পরিবর্তন করতে** দিতে হয়।

Normal pointer parameter:

```c
void change(int *p)
```

এখানে function pointed-to value change করতে পারে।

কিন্তু function যদি **pointer-এর নিজের address/value পরিবর্তন করতে চায়**, তখন pointer to pointer দরকার হতে পারে:

```c
void change(int **p)
```

---

# 19. Function + Pointer to Pointer 🔥

ধরো:

```c
void changePointer(int **p)
{
    static int value = 100;

    *p = &value;
}
```

এখানে function `p` যে pointer variable-কে represent করছে তার value পরিবর্তন করছে।

---

# 20. সহজ Example

```c
#include <stdio.h>

void pointToB(int **p, int *b)
{
    *p = b;
}

int main()
{
    int a = 10;
    int b = 20;

    int *p = &a;

    printf("Before = %d\n", *p);

    pointToB(&p, &b);

    printf("After = %d\n", *p);

    return 0;
}
```

Output:

```text
Before = 10
After = 20
```

---

# 21. Function Call বুঝি

আমরা লিখেছি:

```c
pointToB(&p, &b);
```

এখানে:

```text
&p → p-এর address
&b → b-এর address
```

Function:

```c
void pointToB(int **p, int *b)
```

তাই:

```text
p → original pointer variable
b → b
```

তারপর:

```c
*p = b;
```

মানে original pointer `p`-কে `b`-এর address দাও।

---

# 22. Real Use Case — Dynamic Memory

Pointer to pointer সবচেয়ে বেশি দেখতে পাবে dynamic memory/data structures-এ।

যেমন:

```c
void createNode(Node **head)
```

Linked List-এ `head` pointer পরিবর্তন করার সময় `Node **` খুব common।

এটা আমরা Data Structures phase-এ বিস্তারিতভাবে ব্যবহার করব।

---

# 23. 2D Dynamic Data

Pointer to pointer অনেক সময় dynamic 2D data structure তৈরিতেও ব্যবহৃত হয়।

Conceptually:

```text
int **matrix
```

এখানে `matrix` একটি pointer structure-এর দিকে point করতে পারে, যেখানে প্রতিটি row-এর জন্য আলাদা pointer থাকতে পারে।

এটা Dynamic Memory Allocation lesson-এ বিস্তারিত করব।

---

# 24. Command-Line Arguments

C-এর `main()`-এ তুমি এমন signature দেখতে পারো:

```c
int main(int argc, char **argv)
```

এখানে:

```text
argv
```

হলো pointer-এর একটি array-like structure এবং `char **argv` syntax pointer-related concept-এর সঙ্গে যুক্ত।

এটাও Advanced C-তে বিস্তারিত দেখব।

---

# 25. Pointer to Pointer বনাম Pointer

খুব পরিষ্কার করে:

### Pointer

```c
int *p;
```

মানে:

> `p` একটি `int` object-এর address রাখে।

### Pointer to Pointer

```c
int **q;
```

মানে:

> `q` একটি `int *` pointer-এর address রাখে।

অর্থাৎ:

```text
int *p
    ↑
    │
int **q
```

---

# 26. Type Matching

যদি:

```c
int x;
int *p = &x;
```

তাহলে:

```c
int **q = &p;
```

কারণ:

```text
&p → int **
```

এখানে types match করছে।

কিন্তু:

```c
int **q = &x;   // ❌
```

সঠিক নয়, কারণ `&x` হলো `int *`, `int **` নয়।

---

# 27. তিন Level একসাথে

```c
int x = 10;

int *p = &x;
int **q = &p;
int ***r = &q;
```

এখন:

|Expression|কী বোঝায়|
|---|---|
|`x`|`10`|
|`p`|`x`-এর address|
|`*p`|`10`|
|`q`|`p`-এর address|
|`*q`|`p`|
|`**q`|`10`|
|`r`|`q`-এর address|
|`*r`|`q`|
|`**r`|`p`|
|`***r`|`10`|

---

# 28. Visual Cheat Sheet 🔥

```text
r
│
▼
q
│
▼
p
│
▼
x
│
▼
10
```

একবার dereference:

```text
*r → q
```

দুইবার:

```text
**r → p
```

তিনবার:

```text
***r → 10
```

---

# 29. NULL-এর ক্ষেত্রেও সাবধান ⚠️

যদি:

```c
int **q = NULL;
```

তাহলে:

```c
*q
```

dereference করা যাবে না।

আর:

```c
int *p = NULL;
int **q = &p;
```

এখানে:

```text
q → p
```

valid হলেও:

```c
**q
```

করলে সমস্যা হবে, কারণ `p` কোনো valid object-কে point করছে না।

Pointer-এর প্রতিটি level valid কিনা বুঝতে হবে।

---

# 30. Common Mistake

অনেকে লিখে:

```c
int x = 10;
int *p = &x;
int **q = p;    // ❌
```

এটা ভুল type।

কারণ:

```text
p  → int *
q  → int **
```

সঠিক:

```c
int **q = &p;
```

---

# 31. Another Common Mistake

```c
int x = 10;
int **q;

*q = &x;   // ❌
```

এখানে `q` initialized নয়।

`q` আগে একটি valid `int *` object-এর address point করতে হবে:

```c
int *p = &x;
int **q = &p;
```

---

# 🧪 Practice 1

Output কী হবে?

```c
int x = 50;

int *p = &x;
int **q = &p;

printf("%d\n", **q);
```

---

# 🧪 Practice 2

Code complete করো:

```c
int a = 10;
int b = 20;

int *p = &a;
int **q = &p;

// q ব্যবহার করে p-কে b-এর দিকে point করাও
```

শেষে:

```c
printf("%d\n", *p);
```

Expected:

```text
20
```

---

# 🧪 Practice 3

এই code-এর output predict করো:

```c
int a = 5;

int *p = &a;
int **q = &p;

**q = 99;

printf("%d\n", a);
```

---

# 🔥 Challenge — Pointer Reassignment Function

এই function complete করো:

```c
void changePointer(int **p, int *newAddress)
{
    // তোমার code
}
```

তারপর:

```c
int a = 10;
int b = 50;

int *p = &a;

changePointer(&p, &b);

printf("%d\n", *p);
```

Expected:

```text
50
```

---

# 🎯 Phase 6 Progress

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ✅ Pointer + Array
42. ✅ Pointer + Function
43. ✅ Pointer + String
44. ✅ Pointer to Pointer
45. ⏳ Dynamic Memory Allocation
```

## 🚀 Next → Lesson 45 — Dynamic Memory Allocation

এটা Pointer Phase-এর শেষ এবং অত্যন্ত গুরুত্বপূর্ণ lesson।

আমরা শিখব:

```c
malloc()
calloc()
realloc()
free()
```

এবং বুঝব **Heap memory**, runtime-এ memory নেওয়া, memory release করা, এবং কেন `free()` না করলে **memory leak** হতে পারে।

---
# 🔥 Lesson 45 — Dynamic Memory Allocation

আজ আমরা C-এর Pointer Phase-এর শেষ এবং সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি শিখব:

> **Program চলার সময় প্রয়োজন অনুযায়ী memory নেওয়া এবং পরে সেটা ছেড়ে দেওয়া।**

এটাকে বলে **Dynamic Memory Allocation (DMA)**।

আমরা শিখব:

```c
malloc()
calloc()
realloc()
free()
```

---

# 1. কেন Dynamic Memory Allocation দরকার?

আগে আমরা array এভাবে বানাতাম:

```c
int arr[5];
```

এখানে size আগে থেকেই জানা:

```text
5 elements
```

কিন্তু ধরো user বলল:

```text
আমি 1000টা number রাখতে চাই।
```

তাহলে আগে থেকে:

```c
int arr[1000];
```

লিখে রাখা সবসময় practical নয়।

আবার user যদি বলে:

```text
আমি 5টা number রাখব।
```

তাহলে 1000 element-এর জায়গা unnecessarily নেওয়া হতে পারে।

Dynamic allocation-এর মাধ্যমে runtime-এ প্রয়োজনমতো memory নেওয়া যায়।

---

# 2. Stack বনাম Heap

এখানে আগের concept মনে রাখো।

সাধারণ local variable:

```c
int x = 10;
```

সাধারণত **stack storage** ব্যবহার করে।

Dynamic memory:

```c
malloc(...)
```

ব্যবহার করলে memory নেওয়া হয় **heap** থেকে।

Conceptually:

```text
Memory
┌─────────────────────┐
│ Code                │
├─────────────────────┤
│ Global / Static     │
├─────────────────────┤
│ Heap       ↓        │
│                     │
│                     │
│        ↑            │
│ Stack               │
└─────────────────────┘
```

এখন আমাদের মূল focus:

> **Heap memory**

---

# 3. `malloc()` কী?

`malloc` = **memory allocation**

Syntax:

```c
malloc(size);
```

এটি নির্দিষ্ট সংখ্যক **bytes** memory allocate করার চেষ্টা করে।

Example:

```c
int *p = malloc(sizeof(int));
```

এখানে একটি `int` রাখার মতো memory চাওয়া হচ্ছে।

---

# 4. `<stdlib.h>` লাগবে

`malloc()`, `calloc()`, `realloc()`, `free()` ব্যবহার করতে:

```c
#include <stdlib.h>
```

লাগবে।

Complete:

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *p = malloc(sizeof(int));

    return 0;
}
```

---

# 5. `sizeof()` কেন?

আমরা সরাসরি:

```c
malloc(4);
```

লিখতে চাই না।

কারণ সব system-এ `int`-এর size একই হওয়া বাধ্যতামূলক নয়।

তাই:

```c
sizeof(int)
```

ব্যবহার করি।

```c
int *p = malloc(sizeof(int));
```

মানে:

> একটি `int` রাখার জন্য যত byte দরকার, তত memory allocate করো।

---

# 6. Memory পাওয়ার পর কী করব?

`malloc()` একটি memory block-এর address return করে।

তাই:

```c
int *p = malloc(sizeof(int));
```

conceptually:

```text
p
│
▼
┌──────────┐
│  memory  │
│          │
└──────────┘
```

এখন:

```c
*p = 50;
```

লিখতে পারি।

---

# 7. Complete Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *p = malloc(sizeof(int));

    *p = 50;

    printf("%d\n", *p);

    free(p);

    return 0;
}
```

Output:

```text
50
```

---

# 8. `free()` কেন?

আমরা:

```c
malloc()
```

দিয়ে memory নিয়েছি।

কাজ শেষ হলে:

```c
free(p);
```

দিয়ে সেই memory release করতে হবে।

Pattern:

```text
malloc()
   ↓
use memory
   ↓
free()
```

এটা খুব গুরুত্বপূর্ণ।

---

# 9. Memory Leak

যদি:

```c
int *p = malloc(sizeof(int));
```

করো কিন্তু:

```c
free(p);
```

না করো, তাহলে allocated memory release না হয়ে থাকতে পারে।

এ ধরনের সমস্যা:

> **Memory leak**

বলে।

তাই dynamic memory ব্যবহার করলে `free()` মনে রাখা খুব গুরুত্বপূর্ণ।

---

# 10. `malloc()` Memory Initialize করে?

না।

```c
int *p = malloc(sizeof(int));
```

এর পর `*p`-এর value ধরে নেওয়া যাবে না।

Memory-এর content unspecified হতে পারে।

তাই নিজে value assign করো:

```c
*p = 100;
```

---

# 11. `calloc()` কী?

`calloc()`-ও memory allocate করে।

Syntax:

```c
calloc(number_of_elements, size_of_each_element);
```

যেমন:

```c
int *arr = calloc(5, sizeof(int));
```

মানে:

> 5টি `int` রাখার জন্য memory allocate করো।

---

# 12. `malloc()` বনাম `calloc()`

### `malloc`

```c
malloc(5 * sizeof(int));
```

### `calloc`

```c
calloc(5, sizeof(int));
```

দুটোই memory allocation করতে পারে।

কিন্তু `calloc()` allocated memory-কে zero-initialize করে।

তাই:

```c
int *arr = calloc(5, sizeof(int));
```

এর পরে elements-এর initial value zero হবে।

---

# 13. `calloc()` Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *arr = calloc(5, sizeof(int));

    for (int i = 0; i < 5; i++)
    {
        printf("%d ", arr[i]);
    }

    free(arr);

    return 0;
}
```

Output:

```text
0 0 0 0 0
```

---

# 14. Dynamic Array 🔥

এখন আসল ব্যবহার।

ধরো user বলবে কতগুলো number রাখতে চায়।

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n;

    printf("Enter size: ");
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));

    for (int i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }

    free(arr);

    return 0;
}
```

এখানে `n` runtime-এ জানা যাচ্ছে।

তারপর:

```c
malloc(n * sizeof(int))
```

দিয়ে `n`টি integer-এর memory নেওয়া হচ্ছে।

---

# 15. Example Run

Input:

```text
Enter size: 5
10 20 30 40 50
```

Output:

```text
10 20 30 40 50
```

Memory conceptually:

```text
arr
 ↓
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │
└────┴────┴────┴────┴────┘
```

---

# 16. `arr[i]` কীভাবে কাজ করে?

Dynamic array-এর ক্ষেত্রেও:

```c
arr[i]
```

ব্যবহার করা যায়।

কারণ:

```text
arr[i]
```

মূলত pointer arithmetic-এর সঙ্গে সম্পর্কিত।

Conceptually:

```c
arr[i]
```

এর equivalent:

```c
*(arr + i)
```

তাই:

```c
arr[2]
```

এবং:

```c
*(arr + 2)
```

একই element access করে।

---

# 17. `malloc()` Failure Check করা জরুরি

`malloc()` memory allocate করতে না পারলে `NULL` return করতে পারে।

তাই:

```c
int *arr = malloc(n * sizeof(int));

if (arr == NULL)
{
    printf("Memory allocation failed\n");
    return 1;
}
```

এটা ভালো practice।

---

# 18. Better Dynamic Array Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n;

    printf("Enter size: ");
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));

    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (int i = 0; i < n; i++)
    {
        arr[i] = i + 1;
    }

    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }

    free(arr);

    return 0;
}
```

---

# 19. `realloc()` কী?

ধরো প্রথমে:

```c
int *arr = malloc(5 * sizeof(int));
```

তুমি 5টি element-এর জায়গা নিয়েছ।

পরে বুঝলে 10টি element দরকার।

তখন:

```c
arr = realloc(arr, 10 * sizeof(int));
```

ব্যবহার করা যায়।

`realloc()` একটি existing allocation-এর size পরিবর্তন করার চেষ্টা করে।

---

# 20. `realloc()` Example

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *arr = malloc(5 * sizeof(int));

    if (arr == NULL)
    {
        return 1;
    }

    for (int i = 0; i < 5; i++)
    {
        arr[i] = i + 1;
    }

    int *temp = realloc(arr, 10 * sizeof(int));

    if (temp == NULL)
    {
        free(arr);
        return 1;
    }

    arr = temp;

    for (int i = 5; i < 10; i++)
    {
        arr[i] = i + 1;
    }

    for (int i = 0; i < 10; i++)
    {
        printf("%d ", arr[i]);
    }

    free(arr);

    return 0;
}
```

Output:

```text
1 2 3 4 5 6 7 8 9 10
```

---

# 21. কেন `temp` ব্যবহার করলাম?

Beginner-দের জন্য খুব গুরুত্বপূর্ণ।

এভাবে সরাসরি:

```c
arr = realloc(arr, newSize);
```

লিখলে allocation fail করলে original pointer হারিয়ে যাওয়ার ঝুঁকি থাকে।

তাই:

```c
int *temp = realloc(arr, newSize);
```

তারপর check:

```c
if (temp == NULL)
{
    free(arr);
    return 1;
}
```

তারপর:

```c
arr = temp;
```

এটা safer pattern।

---

# 22. `realloc()` সবসময় একই address রাখবে?

না।

এটা:

```text
আগে:
arr → memory A
```

থেকে নতুন জায়গায় move করতে পারে:

```text
পরে:
arr → memory B
```

তাই `realloc()` return value ব্যবহার করা গুরুত্বপূর্ণ।

---

# 23. `realloc()` Existing Data কী করে?

যদি resize সফল হয়, existing elements-এর value যতটা সম্ভব preserve করা হয়।

ধরো:

```text
আগে:

10 20 30 40 50
```

Size বাড়ালে:

```text
10 20 30 40 50 _ _ _ _ _
```

নতুন অংশ initialize করা হবে না `realloc()` দ্বারা।

নতুন elements নিজে assign করতে হবে।

---

# 24. Size কমানোও সম্ভব

```c
int *temp = realloc(arr, 3 * sizeof(int));
```

এতে allocation ছোট হতে পারে।

তবে size কমালে যে অংশ বাদ পড়ে, সেটি আর access করা যাবে না।

---

# 25. `free()` এর পর Pointer

```c
free(p);
```

এর পর `p`-এর মধ্যে পুরনো address থাকতে পারে।

এ ধরনের pointer-কে **dangling pointer** বলা হয়।

ভালো practice:

```c
free(p);
p = NULL;
```

---

# 26. কেন `NULL` করব?

```c
free(p);
p = NULL;
```

এখন:

```text
p → NULL
```

এতে accidental reuse-এর ঝুঁকি কমে।

তবে মনে রাখবে:

```c
free(NULL);
```

নিজে নিরাপদ—কিন্তু freed pointer-কে dereference করা নিরাপদ নয়।

---

# 27. Double Free ⚠️

এটা করো না:

```c
free(p);
free(p);
```

একই allocation একাধিকবার free করা undefined behavior।

Better:

```c
free(p);
p = NULL;
```

তারপর:

```c
free(p);
```

`p` NULL হলে `free` করা safe।

---

# 28. Use After Free ⚠️

এটা ভুল:

```c
free(p);

printf("%d\n", *p);
```

কারণ memory already released।

এটাকে **use-after-free** বলা হয়।

---

# 29. `malloc()` + Struct

Dynamic memory শুধু integer array-এর জন্য নয়।

যেমন:

```c
struct Student
{
    int id;
    float marks;
};
```

একটি student-এর জন্য dynamic memory:

```c
struct Student *s =
    malloc(sizeof(struct Student));
```

তারপর:

```c
s->id = 101;
s->marks = 85.5;
```

এটা Structures phase-এ আরও ভালোভাবে ব্যবহার করব।

---

# 30. Dynamic String

ধরো user-এর string size আগে জানা নেই।

তখন dynamically character memory নেওয়া যায়:

```c
char *name = malloc(100 * sizeof(char));
```

তারপর:

```c
scanf("%99s", name);
```

শেষে:

```c
free(name);
```

---

# 31. `malloc()`-এর Return Type

`malloc()` একটি `void *` return করে।

Conceptually:

```c
void *malloc(size);
```

C-তে সাধারণত explicit cast করার দরকার নেই:

```c
int *p = malloc(sizeof(int));
```

এটাই preferred C style।

এভাবে লিখলেও:

```c
int *p = (int *)malloc(sizeof(int));
```

কিন্তু C code-এ cast সাধারণত unnecessary।

---

# 32. `sizeof(*p)` Trick 🔥

এটা খুব সুন্দর pattern:

```c
int *p = malloc(sizeof *p);
```

এখানে:

```c
sizeof *p
```

`int`-এর size দিচ্ছে।

আর dynamic array:

```c
int *arr = malloc(n * sizeof *arr);
```

এটা type change করলেও ভুল হওয়ার সম্ভাবনা কমায়।

---

# 33. Dynamic Array Function-এ

```c
void printArray(int *arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
}
```

Main:

```c
int *arr = malloc(n * sizeof *arr);

printArray(arr, n);

free(arr);
```

এখানে:

```text
malloc
 ↓
dynamic array
 ↓
function
 ↓
free
```

---

# 34. Full Practical Example 🔥

User size দেবে, numbers দেবে, তারপর আমরা sum বের করব।

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int n;

    printf("How many numbers? ");
    scanf("%d", &n);

    int *arr = malloc(n * sizeof *arr);

    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    int sum = 0;

    for (int i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
        sum += arr[i];
    }

    printf("Sum = %d\n", sum);

    free(arr);

    return 0;
}
```

Example:

```text
How many numbers? 4
10 20 30 40
Sum = 100
```

---

# 35. `malloc`, `calloc`, `realloc`, `free` — একসাথে

|Function|কাজ|
|---|---|
|`malloc()`|memory allocate|
|`calloc()`|multiple elements allocate + zero-initialize|
|`realloc()`|existing allocation resize|
|`free()`|allocated memory release|

---

# 36. Memory Lifecycle 🔥

একটি typical dynamic allocation:

```text
          malloc()
             ↓
       Memory allocated
             ↓
          Use it
             ↓
          realloc()
        ↙          ↘
    resize        fail
       ↓             ↓
     use            handle
       ↓
      free()
       ↓
 Memory released
```

---

# 37. খুব গুরুত্বপূর্ণ Rules

### Rule 1

`malloc()` করলে:

```c
free();
```

মনে রাখো।

### Rule 2

`free()` করার পরে:

```c
*p
```

করো না।

### Rule 3

`realloc()` result check করো।

### Rule 4

`malloc()`/`calloc()` result `NULL` কিনা check করা ভালো।

### Rule 5

Array-এর বাইরে access করো না।

যদি:

```c
malloc(5 * sizeof(int))
```

করো, valid indices:

```text
0 1 2 3 4
```

---

# 38. Common Mistake — Wrong Size

ভুল:

```c
int *arr = malloc(n);
```

এটা `n` bytes allocate করে, `n` integers নয়।

সঠিক:

```c
int *arr = malloc(n * sizeof *arr);
```

---

# 39. Common Mistake — Missing Header

ভুল:

```c
#include <stdio.h>

int *p = malloc(...);
```

`malloc()`-এর জন্য:

```c
#include <stdlib.h>
```

দাও।

---

# 40. Common Mistake — Forgetting `free()`

```c
int *arr = malloc(100 * sizeof *arr);

/* কাজ */

return 0;
```

Better:

```c
free(arr);
return 0;
```

বিশেষ করে দীর্ঘসময় চলা program-এর ক্ষেত্রে resource management খুব গুরুত্বপূর্ণ।

---

# 41. `calloc()` বনাম `malloc()`

সহজভাবে মনে রাখো:

```c
malloc(n * sizeof *arr);
```

→ allocate করে, initialization করে না।

```c
calloc(n, sizeof *arr);
```

→ allocate করে এবং allocated bytes zero-initialize করে।

---

# 42. একটা গুরুত্বপূর্ণ Precision

`calloc()`-এর ক্ষেত্রে আমরা সাধারণত বলি "elements zero হয়"। Integer/character-এর মতো সাধারণ types-এর জন্য এটা expected zero representation দেয়। তবে C-এর object representation-এর বিষয়গুলো আরও গভীর; এখন beginner level-এ এই rule-টাই যথেষ্ট।

---

# 🧪 Practice 1 — Dynamic Integer

User-এর কাছ থেকে `n` নাও।

তারপর:

```c
malloc()
```

ব্যবহার করে `n`টি integer রাখার জায়গা বানাও।

সব input নেওয়ার পরে:

- Sum
    
- Average
    

print করো।

শেষে `free()` করো।

---

# 🧪 Practice 2 — `calloc()`

```c
int *arr = calloc(10, sizeof *arr);
```

ব্যবহার করে 10টি integer allocate করো।

তারপর সবগুলো print করো।

Expected:

```text
0 0 0 0 0 0 0 0 0 0
```

---

# 🧪 Practice 3 — `realloc()`

প্রথমে:

```text
5 elements
```

এর memory allocate করো।

তারপর:

```text
10 elements
```

করতে `realloc()` ব্যবহার করো।

শেষে 10টি value print করো।

---

# 🔥 Challenge — Dynamic Array + Maximum

User `n` input দেবে।

তারপর dynamically `n` integers রাখবে।

Example:

```text
How many? 6

12 45 7 89 23 10
```

Output:

```text
Maximum = 89
Minimum = 7
```

শর্ত:

- `malloc()` ব্যবহার করবে
    
- `NULL` check করবে
    
- array ব্যবহার করবে
    
- শেষে `free()` করবে
    
- কোনো fixed-size `int arr[100]` ব্যবহার করবে না
    

---

# 🎯 PHASE 6 COMPLETE! 🎉

তোমার Pointer Phase এখন পুরো শেষ:

```text
38. ✅ Pointer Basics
39. ✅ Address operator &
40. ✅ Dereference *
41. ✅ Pointer + Array
42. ✅ Pointer + Function
43. ✅ Pointer + String
44. ✅ Pointer to Pointer
45. ✅ Dynamic Memory Allocation
```

## 🏆 Phase 6-এর Core Formula

```text
Pointer
   ↓
Address (&)
   ↓
Dereference (*)
   ↓
Array
   ↓
Function
   ↓
String
   ↓
Pointer to Pointer
   ↓
Dynamic Memory
```

এগুলো ভালোভাবে বুঝতে পারলে C-এর অনেক কঠিন topic অনেক সহজ হয়ে যাবে।

---

# 🚀 এরপর: Phase 7 — Structures

পরবর্তী Lesson:

## **Lesson 46 — `struct`**

এখানে আমরা শিখব কীভাবে একসঙ্গে বিভিন্ন ধরনের data রাখা যায়:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

তারপর:

```c
struct Student s1;
```

এর মাধ্যমে একটি complete student record তৈরি করব।

এটাই পরে তোমার **Student Management System**, **Bank Management System** ইত্যাদি project-এর foundation হবে।

---
# 🏗️ Lesson 46 — `struct` in C

আজ থেকে শুরু **Phase 7 — Structures**।

এখন পর্যন্ত আমরা আলাদা আলাদা variable নিয়ে কাজ করেছি:

```c
int id;
char name[50];
float marks;
```

কিন্তু একজন Student-এর information তো logically একসাথে থাকা উচিত।

C-এর `struct` আমাদের বিভিন্ন data type-এর variable-কে **একটি custom data structure-এর মধ্যে group** করতে দেয়।

---

# 1. `struct` কী?

`struct` = **structure**

এটি ব্যবহার করে নিজের একটি data type তৈরি করতে পারো।

Example:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

এখানে আমরা `Student` নামে একটি structure তৈরি করেছি।

এর মধ্যে আছে:

```text
Student
├── id     → int
├── name   → char array
└── marks  → float
```

---

# 2. Structure Declare করা

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

খেয়াল করো শেষে:

```c
};
```

এর `;` অবশ্যই দিতে হবে।

---

# 3. Structure Variable

Structure তৈরি করার পরে variable:

```c
struct Student s1;
```

এখন `s1` একটি Student structure।

Conceptually:

```text
s1
┌─────────────────────┐
│ id                  │
├─────────────────────┤
│ name[50]             │
├─────────────────────┤
│ marks                │
└─────────────────────┘
```

---

# 4. Member Access — `.` Operator

Structure-এর member access করতে `.` ব্যবহার করি।

```c
s1.id = 101;
```

```c
s1.marks = 85.5;
```

String:

```c
strcpy(s1.name, "Rahim");
```

তাই:

```c
s1.id
s1.name
s1.marks
```

সবগুলো `s1`-এর আলাদা member।

---

# 5. Complete Example

```c
#include <stdio.h>
#include <string.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student s1;

    s1.id = 101;
    strcpy(s1.name, "Rahim");
    s1.marks = 85.5;

    printf("ID: %d\n", s1.id);
    printf("Name: %s\n", s1.name);
    printf("Marks: %.2f\n", s1.marks);

    return 0;
}
```

Output:

```text
ID: 101
Name: Rahim
Marks: 85.50
```

---

# 6. কেন `strcpy()`?

এটা:

```c
s1.name = "Rahim";
```

C-তে সাধারণ character array-এর ক্ষেত্রে valid assignment নয়।

তাই:

```c
strcpy(s1.name, "Rahim");
```

ব্যবহার করেছি।

এর জন্য:

```c
#include <string.h>
```

লাগে।

---

# 7. Structure Initialization

Variable declare করার সময়ই value দিতে পারো:

```c
struct Student s1 = {
    101,
    "Rahim",
    85.5
};
```

এখন:

```c
s1.id
```

→ `101`

```c
s1.name
```

→ `"Rahim"`

```c
s1.marks
```

→ `85.5`

---

# 8. Designated Initialization 🔥

আরও পরিষ্কারভাবে:

```c
struct Student s1 = {
    .id = 101,
    .name = "Rahim",
    .marks = 85.5
};
```

এতে কোন value কোন member-এর জন্য তা স্পষ্ট।

---

# 9. একাধিক Structure Variable

```c
struct Student s1;
struct Student s2;
struct Student s3;
```

তিনটি আলাদা Student:

```text
s1 → Student 1
s2 → Student 2
s3 → Student 3
```

প্রতিটির নিজের আলাদা data আছে।

---

# 10. Example

```c
#include <stdio.h>
#include <string.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};
    struct Student s2 = {102, "Karim", 90.0};

    printf("%d %s %.2f\n", s1.id, s1.name, s1.marks);
    printf("%d %s %.2f\n", s2.id, s2.name, s2.marks);

    return 0;
}
```

Output:

```text
101 Rahim 85.50
102 Karim 90.00
```

---

# 11. Structure-এর ভিতরে Array

আগেই দেখেছি:

```c
char name[50];
```

Structure-এর member হিসেবে array রাখা যায়।

আরও example:

```c
struct Student
{
    int id;
    char name[50];
    int marks[5];
};
```

এখন:

```c
s1.marks[0]
s1.marks[1]
```

ইত্যাদি ব্যবহার করা যাবে।

---

# 12. Structure + Different Data Types 🔥

এটাই `struct`-এর বড় সুবিধা।

```c
struct Product
{
    int id;
    char name[50];
    float price;
    int quantity;
};
```

একটি `Product`-এর মধ্যে:

```text
int
char array
float
int
```

সব একসাথে রাখা যায়।

---

# 13. Real-Life Example — Bank Account

```c
struct Account
{
    int accountNumber;
    char name[50];
    float balance;
};
```

Variable:

```c
struct Account account1;
```

Data:

```c
account1.accountNumber = 1001;
account1.balance = 5000.0;
```

এটা পরে **Bank Management System** project-এ কাজে লাগবে।

---

# 14. Structure + Function

Structure function-এর argument হিসেবেও পাঠানো যায়।

```c
void printStudent(struct Student s)
{
    printf("ID: %d\n", s.id);
    printf("Name: %s\n", s.name);
    printf("Marks: %.2f\n", s.marks);
}
```

Main:

```c
struct Student s1 = {101, "Rahim", 85.5};

printStudent(s1);
```

---

# 15. Complete Example

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

void printStudent(struct Student s)
{
    printf("ID: %d\n", s.id);
    printf("Name: %s\n", s.name);
    printf("Marks: %.2f\n", s.marks);
}

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};

    printStudent(s1);

    return 0;
}
```

---

# 16. Structure Pass by Value

উপরের:

```c
printStudent(s1);
```

এখানে structure-এর একটি copy function-এ যায়।

তাই function:

```c
void printStudent(struct Student s)
```

এর `s` পরিবর্তন করলে original `s1` পরিবর্তন হবে না।

---

# 17. Structure Pass by Pointer

বড় structure copy না করে pointer পাঠানো যায়:

```c
void printStudent(struct Student *s)
{
    printf("ID: %d\n", s->id);
}
```

Call:

```c
printStudent(&s1);
```

এখানে আমাদের আগের Pointer knowledge কাজে লাগছে।

---

# 18. `.` বনাম `->` 🔥

এটা খুব গুরুত্বপূর্ণ।

### Structure variable:

```c
s1.id
```

### Structure pointer:

```c
p->id
```

যদি:

```c
struct Student *p = &s1;
```

তাহলে:

```c
p->id
```

মূলত:

```c
(*p).id
```

এর shorthand।

---

# 19. Example

```c
#include <stdio.h>

struct Student
{
    int id;
    float marks;
};

int main()
{
    struct Student s1 = {101, 85.5};

    struct Student *p = &s1;

    printf("%d\n", p->id);
    printf("%.2f\n", p->marks);

    return 0;
}
```

Output:

```text
101
85.50
```

---

# 20. `->` কীভাবে কাজ করে?

ধরো:

```c
struct Student *p = &s1;
```

তাহলে:

```c
p->id
```

equivalent:

```c
(*p).id
```

কারণ:

```text
p
↓
s1
↓
id
```

---

# 21. Structure Member Modify

Pointer ব্যবহার করে original structure modify করা যায়:

```c
void updateMarks(struct Student *s)
{
    s->marks = 95.0;
}
```

Call:

```c
updateMarks(&s1);
```

এখন original:

```text
s1.marks
```

পরিবর্তিত হবে।

---

# 22. Complete Example

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

void updateMarks(struct Student *s)
{
    s->marks = 95.0;
}

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};

    printf("Before: %.2f\n", s1.marks);

    updateMarks(&s1);

    printf("After: %.2f\n", s1.marks);

    return 0;
}
```

Output:

```text
Before: 85.50
After: 95.00
```

---

# 23. Structure Size — `sizeof`

```c
printf("%zu\n", sizeof(struct Student));
```

এটি structure-এর total size in bytes দেয়।

তবে একটা গুরুত্বপূর্ণ বিষয়:

**Structure-এর size সবসময় member sizes-এর simple sum নাও হতে পারে।**

কারণ compiler **padding/alignment** যোগ করতে পারে।

---

# 24. Padding সম্পর্কে Basic Idea

ধরো:

```c
struct Example
{
    char a;
    int b;
};
```

তুমি ভাবতে পারো:

```text
char = 1 byte
int  = 4 bytes
total = 5 bytes
```

কিন্তু actual structure size 5 হওয়া বাধ্যতামূলক নয়।

Compiler alignment-এর জন্য extra padding দিতে পারে।

এটা আমরা Advanced C-এর **Memory Layout** lesson-এ বিস্তারিত দেখব।

---

# 25. `struct` এর ভিতরে `struct`

একটি structure-এর member হিসেবে অন্য structure রাখা যায়।

যেমন:

```c
struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};
```

এখন:

```c
s1.birthDate.day
s1.birthDate.month
s1.birthDate.year
```

ব্যবহার করা যায়।

এটা পরের lesson:

> **Lesson 47 — Nested Structure**

এ বিস্তারিত করব।

---

# 26. `typedef` দিয়ে সহজ নাম

এখন:

```c
struct Student s1;
```

লিখতে হচ্ছে।

পরে `typedef` ব্যবহার করে:

```c
typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;
```

তারপর:

```c
Student s1;
```

লিখতে পারবে।

এটা **Lesson 50 — `typedef`**-এ বিস্তারিত হবে।

---

# 27. Structure + Array

একই ধরনের অনেক Student রাখতে:

```c
struct Student students[100];
```

এখন:

```c
students[0]
students[1]
students[2]
```

প্রতিটিই একটি complete `Student` structure।

যেমন:

```c
students[0].id
students[0].name
students[0].marks
```

এটাই পরবর্তীতে **Student Management System**-এর foundation।

---

# 28. ছোট Student Database

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student students[3] =
    {
        {101, "Rahim", 85.5},
        {102, "Karim", 90.0},
        {103, "Hasan", 78.5}
    };

    for (int i = 0; i < 3; i++)
    {
        printf("ID: %d\n", students[i].id);
        printf("Name: %s\n", students[i].name);
        printf("Marks: %.2f\n\n",
               students[i].marks);
    }

    return 0;
}
```

এখানে আমরা **Array + Structure + Loop** একসাথে ব্যবহার করছি।

---

# 29. Structure-এর সবচেয়ে গুরুত্বপূর্ণ Syntax

### Define:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

### Create:

```c
struct Student s1;
```

### Access:

```c
s1.id
s1.name
s1.marks
```

### Pointer:

```c
struct Student *p = &s1;
```

### Pointer access:

```c
p->id
p->name
p->marks
```

---

# 🧠 `.` vs `->`

এটা মুখস্থ করে রাখো:

```text
struct variable
        ↓
       .
        ↓
   s1.id
```

আর:

```text
struct pointer
        ↓
       ->
        ↓
   p->id
```

আর:

```c
p->id
```

মানে:

```c
(*p).id
```

---

# 🧪 Practice 1

একটি structure তৈরি করো:

```c
struct Book
```

যার member হবে:

```text
id
title
price
```

তারপর একটি book variable তৈরি করে values assign করো এবং print করো।

---

# 🧪 Practice 2

এই structure তৈরি করো:

```c
struct Rectangle
{
    float length;
    float width;
};
```

তারপর একটি function:

```c
float area(struct Rectangle r)
```

বানিয়ে rectangle-এর area return করো।

Formula:

```text
Area = length × width
```

---

# 🧪 Practice 3

এই structure:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

ব্যবহার করে 3 জন student-এর data রাখো এবং সবচেয়ে বেশি marks পাওয়া student-এর তথ্য print করো।

---

# 🔥 Challenge

একটি `struct Product` তৈরি করো:

```text
id
name
price
quantity
```

তারপর 5টি product-এর array তৈরি করো।

Program যেন:

1. সব product print করে
    
2. সবচেয়ে expensive product বের করে
    
3. মোট inventory value বের করে
    

Inventory value:

```text
price × quantity
```

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ⏳ Nested structure
48. ⏳ Array of structures
49. ⏳ Pointer to structure
50. ⏳ typedef
51. ⏳ union
52. ⏳ enum
```

## 🚀 Next → Lesson 47 — Nested Structure

পরের lesson-এ আমরা এমন structure বানাব:

```c
struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};
```

অর্থাৎ **একটি structure-এর ভিতরে আরেকটি structure**।

----

# 🏗️ Lesson 47 — Nested Structure

আজ আমরা শিখব **Nested Structure**।

সহজ ভাষায়:

> একটি `struct`-এর ভিতরে আরেকটি `struct` রাখাকে **Nested Structure** বলে।

এটা real-world data model করার জন্য খুব useful।

---

# 1. কেন Nested Structure?

ধরো একজন Student-এর তথ্য:

```text
Student
├── id
├── name
└── birth date
    ├── day
    ├── month
    └── year
```

এখানে `birth date` নিজেই একটি আলাদা concept।

তাই আমরা আলাদা `Date` structure বানাতে পারি।

---

# 2. প্রথমে `Date` Structure

```c
struct Date
{
    int day;
    int month;
    int year;
};
```

এখন `Date` একটি structure।

---

# 3. Student-এর ভিতরে Date

```c
struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};
```

এখানে:

```c
struct Date birthDate;
```

হলো nested structure member।

---

# 4. Complete Example

```c
#include <stdio.h>

struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};

int main()
{
    struct Student s1;

    s1.id = 101;

    s1.birthDate.day = 15;
    s1.birthDate.month = 8;
    s1.birthDate.year = 2005;

    printf("ID: %d\n", s1.id);
    printf("Birth Date: %d-%d-%d\n",
           s1.birthDate.day,
           s1.birthDate.month,
           s1.birthDate.year);

    return 0;
}
```

Output:

```text
ID: 101
Birth Date: 15-8-2005
```

---

# 5. এখানে `.` কতবার?

এটা খুব গুরুত্বপূর্ণ।

আমাদের:

```c
s1.birthDate.day
```

এখানে:

```text
s1
 ↓
birthDate
 ↓
day
```

অর্থাৎ:

```text
Student → Date → day
```

তাই দুইবার `.` ব্যবহার হয়েছে।

---

# 6. Visual Structure

```text
s1
│
├── id
│
├── name
│
└── birthDate
      │
      ├── day
      ├── month
      └── year
```

তাই:

```c
s1.id
```

এবং:

```c
s1.birthDate.day
```

---

# 7. Structure Initialization

Nested structure declare করার সময় initialize করা যায়:

```c
struct Student s1 =
{
    101,
    "Rahim",
    {15, 8, 2005}
};
```

এখানে:

```text
101
Rahim
15
8
2005
```

ক্রম অনুযায়ী members initialize হবে।

---

# 8. Designated Initialization

আরও readable:

```c
struct Student s1 =
{
    .id = 101,
    .name = "Rahim",
    .birthDate =
    {
        .day = 15,
        .month = 8,
        .year = 2005
    }
};
```

এটা বড় structure-এর ক্ষেত্রে খুব useful।

---

# 9. Nested Structure-এর আরেকটি Example

ধরো একটি Employee:

```c
struct Address
{
    char city[50];
    char country[50];
};

struct Employee
{
    int id;
    char name[50];
    struct Address address;
};
```

এখন:

```c
employee.address.city
```

এবং:

```c
employee.address.country
```

ব্যবহার করতে পারি।

---

# 10. Complete Example

```c
#include <stdio.h>

struct Address
{
    char city[50];
    char country[50];
};

struct Employee
{
    int id;
    char name[50];
    struct Address address;
};

int main()
{
    struct Employee e1 =
    {
        101,
        "Rahim",
        {"Dhaka", "Bangladesh"}
    };

    printf("ID: %d\n", e1.id);
    printf("Name: %s\n", e1.name);
    printf("City: %s\n", e1.address.city);
    printf("Country: %s\n", e1.address.country);

    return 0;
}
```

---

# 11. Nested Structure + Function

একটি nested structure function-এ পাঠানো যায়।

```c
void printStudent(struct Student s)
{
    printf("ID: %d\n", s.id);

    printf("Birth Date: %d-%d-%d\n",
           s.birthDate.day,
           s.birthDate.month,
           s.birthDate.year);
}
```

Call:

```c
printStudent(s1);
```

---

# 12. Nested Structure + Pointer

এখন Pointer-এর knowledge কাজে লাগাই।

```c
struct Student *p = &s1;
```

Student-এর normal member:

```c
p->id
```

কিন্তু nested member:

```c
p->birthDate.day
```

---

# 13. `p->birthDate.day` কীভাবে কাজ করে?

এটা দেখতে একটু বড়:

```c
p->birthDate.day
```

প্রথমে:

```text
p
↓
Student
```

তারপর:

```text
birthDate
```

তারপর:

```text
day
```

তাই:

```text
p → Student → birthDate → day
```

---

# 14. Equivalent Expression

এই:

```c
p->birthDate.day
```

এর equivalent:

```c
(*p).birthDate.day
```

কারণ `p` একটি structure pointer।

---

# 15. Function দিয়ে Birth Date Update

```c
void changeBirthYear(struct Student *s)
{
    s->birthDate.year = 2006;
}
```

Call:

```c
changeBirthYear(&s1);
```

এখন:

```c
s1.birthDate.year
```

পরিবর্তিত হবে।

---

# 16. Nested Structure + Array

এখন 3টি Student:

```c
struct Student students[3];
```

প্রতিটি Student-এর নিজের Date আছে।

```text
students[0]
 ├── id
 ├── name
 └── birthDate
      ├── day
      ├── month
      └── year

students[1]
 ├── id
 ├── name
 └── birthDate
      ├── day
      ├── month
      └── year
```

---

# 17. Example

```c
#include <stdio.h>

struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};

int main()
{
    struct Student students[2] =
    {
        {101, "Rahim", {15, 8, 2005}},
        {102, "Karim", {20, 3, 2006}}
    };

    for (int i = 0; i < 2; i++)
    {
        printf("ID: %d\n", students[i].id);
        printf("Name: %s\n", students[i].name);

        printf("Birth Date: %d-%d-%d\n\n",
               students[i].birthDate.day,
               students[i].birthDate.month,
               students[i].birthDate.year);
    }

    return 0;
}
```

---

# 18. Real-World Data Modeling 🔥

Nested structure-এর সবচেয়ে বড় সুবিধা হলো data logically organize করা।

ধরো:

```text
Bank Account
│
├── account number
├── holder
│
└── address
     ├── city
     ├── district
     └── country
```

C:

```c
struct Address
{
    char city[50];
    char district[50];
    char country[50];
};

struct Account
{
    int accountNumber;
    char holder[50];
    struct Address address;
};
```

এখন:

```c
account.address.city
```

দিয়ে city access করা যাবে।

---

# 19. Nested Structure আরও গভীর হতে পারে

Technically:

```c
struct A
{
    int x;
};

struct B
{
    struct A a;
};

struct C
{
    struct B b;
};
```

এখন:

```c
c.b.a.x
```

possible।

তবে খুব deeply nested structure code unnecessarily complex করতে পারে। Logical grouping যেখানে দরকার, সেখানেই ব্যবহার করা ভালো।

---

# 20. Structure ভিতরে Pointer-ও থাকতে পারে

Nested structure শুধু structure member-এ সীমাবদ্ধ নয়।

যেমন:

```c
struct Person
{
    char name[50];
};

struct Company
{
    struct Person *manager;
};
```

এখানে `Company`-এর মধ্যে `Person`-এর pointer আছে।

এটা পরবর্তীতে **Pointer to Structure** এবং Data Structures-এর সময় আরও গুরুত্বপূর্ণ হবে।

---

# 21. Structure-এর ভিতরে Array of Structure

এটাও possible:

```c
struct Team
{
    char name[50];
    struct Student members[10];
};
```

এখানে:

```text
Team
└── members
     ├── Student
     ├── Student
     ├── Student
     └── ...
```

এ ধরনের hierarchical data model অনেক জায়গায় কাজে লাগে।

---

# 22. একটি গুরুত্বপূর্ণ Rule

Nested structure define করার আগে inner structure-এর definition জানা থাকতে হবে।

সঠিক:

```c
struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    struct Date birthDate;
};
```

এখানে `Date` আগে define করা হয়েছে।

---

# 23. Common Mistake

ভুল:

```c
struct Student
{
    int id;
    struct Date birthDate;
};

struct Date
{
    int day;
    int month;
    int year;
};
```

এখানে `Student` definition-এর সময় compiler `struct Date`-এর complete definition জানে না।

Beginner level-এ সহজ rule:

> **যে structure-কে member হিসেবে ব্যবহার করবে, তার definition আগে লিখো।**

---

# 24. Nested Structure + `scanf()`

User input নেওয়া যায়:

```c
struct Student s;

printf("Enter ID: ");
scanf("%d", &s.id);

printf("Enter birth day: ");
scanf("%d", &s.birthDate.day);

printf("Enter birth month: ");
scanf("%d", &s.birthDate.month);

printf("Enter birth year: ");
scanf("%d", &s.birthDate.year);
```

খেয়াল করো nested member-এর address:

```c
&s.birthDate.day
```

---

# 25. Complete Input Example

```c
#include <stdio.h>

struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};

int main()
{
    struct Student s;

    printf("Enter ID: ");
    scanf("%d", &s.id);

    printf("Enter name: ");
    scanf("%49s", s.name);

    printf("Enter birth date: ");
    scanf("%d %d %d",
          &s.birthDate.day,
          &s.birthDate.month,
          &s.birthDate.year);

    printf("\nStudent Information\n");
    printf("ID: %d\n", s.id);
    printf("Name: %s\n", s.name);
    printf("Birth Date: %d-%d-%d\n",
           s.birthDate.day,
           s.birthDate.month,
           s.birthDate.year);

    return 0;
}
```

---

# 26. `.` এবং `->` আবার

এটা ভালোভাবে আয়ত্ত করো।

### Normal structure:

```c
s.birthDate.day
```

### Structure pointer:

```c
p->birthDate.day
```

### Equivalent:

```c
(*p).birthDate.day
```

---

# 🧠 Golden Pattern

```text
Normal:

s.member


Nested:

s.member.submember


Pointer:

p->member


Pointer + Nested:

p->member.submember
```

---

# 🧪 Practice 1

এই structure তৈরি করো:

```c
struct Address
{
    char city[50];
    char country[50];
};

struct Person
{
    char name[50];
    struct Address address;
};
```

একজন Person-এর data initialize করে print করো।

---

# 🧪 Practice 2

একটি:

```c
struct Date
```

এবং:

```c
struct Employee
```

তৈরি করো।

Employee-এর মধ্যে থাকবে:

```text
id
name
joiningDate
```

যেখানে `joiningDate` হবে `struct Date`।

তারপর employee-এর complete information print করো।

---

# 🔥 Challenge

একটি **Student Record** তৈরি করো:

```text
Student
│
├── id
├── name
├── marks
└── address
     ├── city
     ├── district
     └── country
```

তারপর 3 জন Student-এর array বানাও এবং:

1. সব student print করো
    
2. নির্দিষ্ট district-এর students print করো
    
3. সবচেয়ে বেশি marks পাওয়া student print করো
    

এখানে একসাথে ব্যবহার করবে:

```text
struct
nested struct
array
loop
function
```

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ✅ Nested structure
48. ⏳ Array of structures
49. ⏳ Pointer to structure
50. ⏳ typedef
51. ⏳ union
52. ⏳ enum
```

## 🚀 Next → Lesson 48 — Array of Structures

পরের lesson-এ আমরা একসাথে অনেকগুলো record manage করব:

```c
struct Student students[100];
```

তারপর **search, sort, highest marks, input/output**—সব একসাথে করব। এটি তোমার ভবিষ্যতের **Student Management System** project-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 🚀 Lesson 48 — Array of Structures

আজ আমরা শিখব কীভাবে **একসাথে অনেকগুলো structure variable** রাখতে হয়।

আগের lesson-এ ছিল:

```c
struct Student s1;
```

একজন Student।

এখন যদি 100 জন Student রাখতে চাই?

```c
struct Student students[100];
```

এটাই **Array of Structures**।

---

# 1. Array of Structures কী?

ধরো:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

এখন:

```c
struct Student students[3];
```

মানে:

```text
students
│
├── students[0]
├── students[1]
└── students[2]
```

প্রতিটি element একটি **complete `struct Student`**।

---

# 2. Visualize করি

```text
students[0]
┌──────────────────┐
│ id    = 101      │
│ name  = Rahim    │
│ marks = 85.5     │
└──────────────────┘

students[1]
┌──────────────────┐
│ id    = 102      │
│ name  = Karim    │
│ marks = 90.0     │
└──────────────────┘

students[2]
┌──────────────────┐
│ id    = 103      │
│ name  = Hasan    │
│ marks = 78.5     │
└──────────────────┘
```

---

# 3. Declaration

```c
struct Student students[100];
```

এখানে:

- `students` → array
    
- `100` → maximum elements
    
- প্রতিটি element → `struct Student`
    

---

# 4. Access করা

প্রথম student-এর ID:

```c
students[0].id
```

দ্বিতীয় student-এর name:

```c
students[1].name
```

তৃতীয় student-এর marks:

```c
students[2].marks
```

Pattern:

```text
array[index].member
```

🔥 এই pattern খুব গুরুত্বপূর্ণ।

---

# 5. Initialization

একসাথে values দিতে পারো:

```c
struct Student students[3] =
{
    {101, "Rahim", 85.5},
    {102, "Karim", 90.0},
    {103, "Hasan", 78.5}
};
```

---

# 6. সব Student Print

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student students[3] =
    {
        {101, "Rahim", 85.5},
        {102, "Karim", 90.0},
        {103, "Hasan", 78.5}
    };

    for (int i = 0; i < 3; i++)
    {
        printf("ID: %d\n", students[i].id);
        printf("Name: %s\n", students[i].name);
        printf("Marks: %.2f\n\n", students[i].marks);
    }

    return 0;
}
```

Output:

```text
ID: 101
Name: Rahim
Marks: 85.50

ID: 102
Name: Karim
Marks: 90.00

ID: 103
Name: Hasan
Marks: 78.50
```

---

# 7. Loop-এর ভিতরে কী হচ্ছে?

এই line:

```c
students[i].id
```

যখন:

```text
i = 0
```

তখন:

```c
students[0].id
```

যখন:

```text
i = 1
```

তখন:

```c
students[1].id
```

যখন:

```text
i = 2
```

তখন:

```c
students[2].id
```

অর্থাৎ loop দিয়ে সব record access করা যায়।

---

# 8. User Input নেওয়া

এবার user-এর কাছ থেকে 3 জন Student-এর information নিই।

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student students[3];

    for (int i = 0; i < 3; i++)
    {
        printf("\nStudent %d\n", i + 1);

        printf("ID: ");
        scanf("%d", &students[i].id);

        printf("Name: ");
        scanf("%49s", students[i].name);

        printf("Marks: ");
        scanf("%f", &students[i].marks);
    }

    printf("\n--- Student List ---\n");

    for (int i = 0; i < 3; i++)
    {
        printf("%d %s %.2f\n",
               students[i].id,
               students[i].name,
               students[i].marks);
    }

    return 0;
}
```

---

# 9. কেন Name-এর আগে `&` নেই?

এখানে:

```c
scanf("%49s", students[i].name);
```

`students[i].name` একটি character array।

Array expression প্রথম element-এর address-এর মতো behave করে।

তাই:

```c
&students[i].name
```

এখানে ব্যবহার করার দরকার নেই।

---

# 10. Search by ID 🔎

এখন array of structures দিয়ে search করা যাক।

```c
int searchId;

printf("Enter ID to search: ");
scanf("%d", &searchId);

for (int i = 0; i < 3; i++)
{
    if (students[i].id == searchId)
    {
        printf("Found!\n");
        printf("Name: %s\n", students[i].name);
        printf("Marks: %.2f\n", students[i].marks);
    }
}
```

এখানে আমরা আগের:

```text
Array
+
Loop
+
if
+
struct
```

সব একসাথে ব্যবহার করছি।

---

# 11. Search Function

Code clean রাখতে function বানানো ভালো।

```c
void searchStudent(struct Student students[],
                   int n,
                   int id)
{
    for (int i = 0; i < n; i++)
    {
        if (students[i].id == id)
        {
            printf("Found!\n");
            printf("Name: %s\n", students[i].name);
            printf("Marks: %.2f\n", students[i].marks);
            return;
        }
    }

    printf("Student not found.\n");
}
```

Call:

```c
searchStudent(students, 3, 102);
```

---

# 12. Array Function-এ কীভাবে যায়?

এই parameter:

```c
struct Student students[]
```

function-এর মধ্যে array-এর প্রথম element-এর address-এর মতো কাজ করে।

তাই:

```c
students[i]
```

দিয়ে elements access করা যায়।

আর size আলাদা parameter হিসেবে পাঠানো ভালো:

```c
void searchStudent(struct Student students[],
                   int n,
                   int id)
```

কারণ function-এর মধ্যে সাধারণভাবে array-এর element count automatically জানা যায় না।

---

# 13. Highest Marks 🏆

এবার সবচেয়ে বেশি marks পাওয়া Student বের করি।

```c
int maxIndex = 0;

for (int i = 1; i < 3; i++)
{
    if (students[i].marks > students[maxIndex].marks)
    {
        maxIndex = i;
    }
}

printf("Top Student: %s\n",
       students[maxIndex].name);

printf("Marks: %.2f\n",
       students[maxIndex].marks);
```

---

# 14. কীভাবে কাজ করছে?

ধরো:

```text
Rahim → 85
Karim → 90
Hasan → 78
```

প্রথমে:

```text
maxIndex = 0
```

মানে:

```text
Rahim
```

তারপর Karim:

```text
90 > 85
```

তাই:

```text
maxIndex = 1
```

তারপর Hasan:

```text
78 > 90
```

false।

শেষে:

```text
maxIndex = 1
```

অর্থাৎ Karim।

---

# 15. Average Marks

```c
float sum = 0;

for (int i = 0; i < 3; i++)
{
    sum += students[i].marks;
}

float average = sum / 3;

printf("Average = %.2f\n", average);
```

---

# 16. Total Student Count

Array-এর fixed size:

```c
struct Student students[100];
```

কিন্তু actual student যদি 10 জন হয়, তাহলে:

```c
int n = 10;
```

ব্যবহার করবে।

Pattern:

```c
for (int i = 0; i < n; i++)
```

এটা practical programming-এ খুব common।

---

# 17. Array Size Automatically বের করা

যদি একই scope-এ actual array থাকে:

```c
struct Student students[5];
```

তাহলে:

```c
int n = sizeof(students) / sizeof(students[0]);
```

এখানে:

```text
sizeof(students)
```

→ পুরো array-এর size।

আর:

```text
sizeof(students[0])
```

→ একটি Student-এর size।

তাই division:

```text
5
```

দেবে।

---

# 18. গুরুত্বপূর্ণ সতর্কতা ⚠️

Function-এ:

```c
void printStudents(struct Student students[])
```

দেওয়ার পরে সেখানে:

```c
sizeof(students)
```

দিয়ে original array-এর element count বের করা যাবে না।

কারণ function parameter হিসেবে এটি array-এর pointer-এর মতো behave করে।

তাই:

```c
void printStudents(struct Student students[], int n)
```

এভাবে `n` পাঠানো ভালো।

---

# 19. Sorting Students by Marks

এবার আগের Sorting lesson-এর concept ব্যবহার করি।

ধরো:

```text
Rahim 85
Karim 90
Hasan 78
```

Marks অনুযায়ী ascending sort করতে পারি।

```c
for (int i = 0; i < n - 1; i++)
{
    for (int j = 0; j < n - i - 1; j++)
    {
        if (students[j].marks > students[j + 1].marks)
        {
            struct Student temp = students[j];

            students[j] = students[j + 1];
            students[j + 1] = temp;
        }
    }
}
```

এখানে পুরো structure swap হচ্ছে।

---

# 20. Structure Swap 🔥

এটা খুব powerful:

```c
struct Student temp;

temp = students[i];
students[i] = students[j];
students[j] = temp;
```

একটি assignment দিয়েই পুরো structure copy হয়।

অর্থাৎ:

```text
id
name
marks
```

সব copy হয়।

---

# 21. Descending Sort

Highest marks আগে চাইলে:

```c
if (students[j].marks < students[j + 1].marks)
```

ব্যবহার করো।

তাহলে:

```text
90
85
78
```

হবে।

---

# 22. Nested Structure + Array

আগের lesson-এর concept-ও combine করা যায়।

```c
struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    char name[50];
    struct Date birthDate;
};
```

তারপর:

```c
struct Student students[3];
```

Access:

```c
students[0].birthDate.day
```

Pattern:

```text
array[index].nested.member
```

---

# 23. Structure Pointer + Array

এখন pointer-এর knowledge:

```c
struct Student *p = students;
```

এখানে `p` প্রথম Student-এর দিকে point করছে।

তাই:

```c
p->id
```

প্রথম Student-এর ID।

---

# 24. Pointer দিয়ে Next Student

```c
(p + 1)->id
```

দ্বিতীয় Student-এর ID।

```c
(p + 2)->id
```

তৃতীয় Student-এর ID।

এখানে:

```text
p
↓
students[0]

p + 1
↓
students[1]

p + 2
↓
students[2]
```

---

# 25. Pointer দিয়ে Loop

```c
struct Student *p = students;

for (int i = 0; i < n; i++)
{
    printf("%d %s %.2f\n",
           p->id,
           p->name,
           p->marks);

    p++;
}
```

এখানে `p++` পরের Student-এর দিকে যায়।

---

# 26. Full Mini Student Database 🔥

এবার আগের সব concept combine করি।

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

void printStudents(struct Student students[], int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("ID: %d\n", students[i].id);
        printf("Name: %s\n", students[i].name);
        printf("Marks: %.2f\n\n", students[i].marks);
    }
}

int main()
{
    struct Student students[3] =
    {
        {101, "Rahim", 85.5},
        {102, "Karim", 90.0},
        {103, "Hasan", 78.5}
    };

    printStudents(students, 3);

    return 0;
}
```

এটা ভবিষ্যতের **Student Management System**-এর basic foundation।

---

# 27. আরও Practical Design

একটি Student Management System-এ আমরা পরে এমন structure রাখতে পারি:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

তারপর:

```c
struct Student students[100];
int studentCount = 0;
```

তারপর functions:

```text
addStudent()
displayStudents()
searchStudent()
updateStudent()
deleteStudent()
sortStudents()
```

🔥 এগুলো সব পরে project-এ করব।

---

# 28. `const` দিয়ে Read-Only Function

যদি function structure modify না করে, pointer parameter-এ `const` ব্যবহার করা যায়:

```c
void printStudent(const struct Student *s)
{
    printf("%d\n", s->id);
}
```

এতে function-এর ভিতরে accidentally:

```c
s->id = 500;
```

করার চেষ্টা compiler-এর কাছে সমস্যা তৈরি করবে।

এটা বড় program-এ ভালো practice।

---

# 29. Array of Structures + Dynamic Memory

আগের Dynamic Memory lesson-ও এখানে combine করা যায়:

```c
struct Student *students =
    malloc(n * sizeof *students);
```

এখন runtime-এ `n` জন Student-এর জায়গা নেওয়া যায়।

এটা পরবর্তীতে বড় project এবং Data Structures-এ খুব কাজে লাগবে।

---

# 30. Memory Concept

যদি:

```c
struct Student students[3];
```

হয়:

```text
students
│
▼
┌─────────────┐
│ Student 0   │
├─────────────┤
│ Student 1   │
├─────────────┤
│ Student 2   │
└─────────────┘
```

আর:

```c
students[1]
```

দ্বিতীয় পুরো structure।

তারপর:

```c
students[1].marks
```

দ্বিতীয় structure-এর marks।

---

# 🧠 Golden Syntax

### Array declaration

```c
struct Student students[100];
```

### Access

```c
students[i].id
```

### Nested

```c
students[i].birthDate.year
```

### Pointer

```c
struct Student *p = students;
```

### Pointer member

```c
p->id
```

### Next structure

```c
(p + 1)->id
```

---

# 🧪 Practice 1

এই structure তৈরি করো:

```c
struct Book
{
    int id;
    char title[50];
    float price;
};
```

তারপর 5টি Book-এর array বানাও এবং সবগুলো print করো।

---

# 🧪 Practice 2

5 জন Student-এর:

```text
id
name
marks
```

input নাও।

তারপর:

- সর্বোচ্চ marks
    
- সর্বনিম্ন marks
    
- average marks
    

print করো।

---

# 🧪 Practice 3 — Search

Student array থেকে ID input নিয়ে student search করো।

যদি পাওয়া যায়:

```text
Student Found
ID: ...
Name: ...
Marks: ...
```

না পাওয়া গেলে:

```text
Student Not Found
```

---

# 🔥 Challenge — Sort

10 জন Student input নাও।

Marks অনুযায়ী **descending order**-এ sort করো।

Expected:

```text
Student Ranking

1. Karim  - 95
2. Rahim  - 91
3. Hasan  - 87
4. ...
```

শর্ত:

- `struct`
    
- array
    
- loop
    
- function
    
- sorting
    

সব ব্যবহার করবে।

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ✅ Nested structure
48. ✅ Array of structures
49. ⏳ Pointer to structure
50. ⏳ typedef
51. ⏳ union
52. ⏳ enum
```

## 🚀 Next → Lesson 49 — Pointer to Structure

পরের lesson-এ আমরা পুরোপুরি focus করব:

```c
struct Student *p;
```

এবং:

```c
p->id
p->name
p->marks
```

কেন `.` নয়, `->` ব্যবহার করতে হয়—এটা pointer arithmetic এবং function-এর সঙ্গে গভীরভাবে বুঝব।

----

# 🔥 Lesson 49 — Pointer to Structure

আজকের topic খুব গুরুত্বপূর্ণ, কারণ এখান থেকেই `struct` + `pointer` একসাথে ব্যবহার শুরু হবে।

আমরা শিখব:

- Structure pointer কী
    
- `&` দিয়ে structure-এর address নেওয়া
    
- `*` দিয়ে dereference
    
- `->` operator
    
- `.` বনাম `->`
    
- Function-এ structure pointer পাঠানো
    
- Structure modify করা
    
- Array of structures + pointer
    

---

# 1. Structure মনে করি

আমাদের structure:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

একটি variable:

```c
struct Student s1;
```

এখন `s1` একটি complete Student।

---

# 2. Structure-এর Address

আমরা জানি:

```c
int x = 10;
int *p = &x;
```

একইভাবে structure-এর address নেওয়া যায়:

```c
struct Student s1;

struct Student *p = &s1;
```

এখানে:

```text
s1
 ↓
একটি Student structure

p
 ↓
s1-এর address
```

---

# 3. `struct Student *p` কী?

এই declaration:

```c
struct Student *p;
```

মানে:

> `p` এমন একটি pointer, যা `struct Student`-এর address রাখতে পারে।

এটা সাধারণ pointer-এর মতোই, শুধু pointer-এর type হলো:

```c
struct Student
```

---

# 4. Complete Example

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};

    struct Student *p = &s1;

    printf("ID: %d\n", p->id);
    printf("Name: %s\n", p->name);
    printf("Marks: %.2f\n", p->marks);

    return 0;
}
```

Output:

```text
ID: 101
Name: Rahim
Marks: 85.50
```

---

# 5. `.` বনাম `->` 🔥

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়।

যদি তোমার কাছে **structure variable** থাকে:

```c
s1.id
```

তাহলে `.` ব্যবহার করবে।

কিন্তু যদি **structure pointer** থাকে:

```c
p->id
```

তাহলে `->` ব্যবহার করবে।

### মনে রাখো:

```text
Structure variable
        ↓
       .

Structure pointer
        ↓
       ->
```

---

# 6. একই কাজ দুইভাবে

ধরো:

```c
struct Student s1 = {101, "Rahim", 85.5};
struct Student *p = &s1;
```

Direct:

```c
s1.id
```

Pointer দিয়ে:

```c
p->id
```

দুটোই একই `id` access করছে।

---

# 7. `->` আসলে কী?

এই:

```c
p->id
```

এর equivalent:

```c
(*p).id
```

অর্থাৎ:

```c
p->id
```

হলো shorthand for:

```c
(*p).id
```

---

# 8. কেন `(*p).id`?

ধরো:

```c
struct Student *p = &s1;
```

`p` হলো address।

তাই:

```c
*p
```

মানে সেই address-এর structure।

তারপর:

```c
(*p).id
```

মানে সেই structure-এর `id`।

---

# 9. Parentheses কেন দরকার?

ভুল:

```c
*p.id
```

কারণ `.` operator-এর precedence বেশি।

সঠিক:

```c
(*p).id
```

তাই C language-এ shortcut দেওয়া হয়েছে:

```c
p->id
```

---

# 10. সব Member Access

```c
p->id
p->name
p->marks
```

Nested structure থাকলে:

```c
p->birthDate.day
```

এখানে `p` pointer, কিন্তু `birthDate` নিজে structure member।

---

# 11. Pointer দিয়ে Value Modify

Pointer ব্যবহার করে original structure পরিবর্তন করা যায়।

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};

    struct Student *p = &s1;

    p->marks = 95.0;

    printf("Marks: %.2f\n", s1.marks);

    return 0;
}
```

Output:

```text
Marks: 95.00
```

কারণ `p` সরাসরি `s1`-কে point করছে।

---

# 12. Memory Concept

ধরো:

```c
struct Student s1 = {101, "Rahim", 85.5};
```

Conceptually:

```text
Memory
┌─────────────────────┐
│ s1                  │
│                     │
│ id = 101            │
│ name = "Rahim"      │
│ marks = 85.5        │
└─────────────────────┘
          ▲
          │
          │ address
          │
          p
```

তাই:

```c
p->marks
```

শেষ পর্যন্ত `s1.marks`-এই পৌঁছায়।

---

# 13. Function-এ Structure Pointer

এটাই pointer-to-structure-এর সবচেয়ে useful application।

ধরো:

```c
void updateMarks(struct Student *s)
{
    s->marks = 100;
}
```

Call:

```c
updateMarks(&s1);
```

---

# 14. Complete Example

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

void updateMarks(struct Student *s)
{
    s->marks = 100.0;
}

int main()
{
    struct Student s1 = {101, "Rahim", 85.5};

    printf("Before: %.2f\n", s1.marks);

    updateMarks(&s1);

    printf("After: %.2f\n", s1.marks);

    return 0;
}
```

Output:

```text
Before: 85.50
After: 100.00
```

---

# 15. কেন Pointer ব্যবহার করলাম?

যদি আমরা লিখি:

```c
void updateMarks(struct Student s)
```

তাহলে function-এ structure-এর copy যাবে।

কিন্তু:

```c
void updateMarks(struct Student *s)
```

দিলে original structure-এর address যায়।

তাই function original data modify করতে পারে।

---

# 16. Pass by Value বনাম Pointer

### Pass by value

```c
void update(struct Student s)
```

```text
Original
   ↓
 copy তৈরি
   ↓
function
```

Original সাধারণত পরিবর্তিত হয় না।

### Pointer

```c
void update(struct Student *s)
```

```text
Original
   ↑
   │
address
   │
function
```

Original modify করা যায়।

---

# 17. Structure Array + Pointer 🔥

ধরো:

```c
struct Student students[3] =
{
    {101, "Rahim", 85.5},
    {102, "Karim", 90.0},
    {103, "Hasan", 78.5}
};
```

এখন:

```c
struct Student *p = students;
```

`p` প্রথম element-কে point করছে।

---

# 18. প্রথম Student

```c
p->id
```

মানে:

```c
students[0].id
```

---

# 19. দ্বিতীয় Student

```c
(p + 1)->id
```

মানে:

```c
students[1].id
```

তৃতীয়:

```c
(p + 2)->id
```

মানে:

```c
students[2].id
```

---

# 20. Pointer Arithmetic

এখানে:

```c
p + 1
```

মানে এক byte এগোনো নয়।

এটা এক **পুরো `struct Student`** পরের element-এ যায়।

যেমন:

```text
p
↓
students[0]

p + 1
↓
students[1]

p + 2
↓
students[2]
```

Compiler structure-এর size জানে।

---

# 21. Pointer দিয়ে Loop

```c
#include <stdio.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student students[3] =
    {
        {101, "Rahim", 85.5},
        {102, "Karim", 90.0},
        {103, "Hasan", 78.5}
    };

    struct Student *p = students;

    for (int i = 0; i < 3; i++)
    {
        printf("%d %s %.2f\n",
               p->id,
               p->name,
               p->marks);

        p++;
    }

    return 0;
}
```

Output:

```text
101 Rahim 85.50
102 Karim 90.00
103 Hasan 78.50
```

---

# 22. Pointer + Function + Array

এখন আরও practical:

```c
void printStudents(struct Student *students, int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("%d %s %.2f\n",
               students[i].id,
               students[i].name,
               students[i].marks);
    }
}
```

Call:

```c
printStudents(students, 3);
```

এখানে:

```c
struct Student *students
```

প্রথম Student-এর address receive করছে।

---

# 23. Pointer দিয়ে Array Modify

```c
void increaseMarks(struct Student *students, int n)
{
    for (int i = 0; i < n; i++)
    {
        students[i].marks += 5;
    }
}
```

Call:

```c
increaseMarks(students, 3);
```

সব Student-এর marks 5 করে বাড়বে।

---

# 24. `p[i]` বনাম `p->`

যদি:

```c
struct Student *p = students;
```

তাহলে:

```c
p[i].id
```

ব্যবহার করা যায়।

এবং:

```c
(p + i)->id
```

এটাও একই element access করে।

অর্থাৎ:

```c
p[i].id
```

এবং:

```c
(p + i)->id
```

একই `id`-তে পৌঁছায়।

---

# 25. Nested Structure + Pointer

ধরো:

```c
struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int id;
    struct Date birthDate;
};
```

Pointer:

```c
struct Student *p = &s1;
```

তাহলে:

```c
p->birthDate.year
```

দিয়ে year access করা যাবে।

---

# 26. Pointer দিয়ে Nested Data Modify

```c
p->birthDate.year = 2007;
```

এতে original:

```c
s1.birthDate.year
```

পরিবর্তিত হবে।

---

# 27. `const struct` Pointer

যদি শুধু data read করতে চাও:

```c
void printStudent(const struct Student *s)
{
    printf("%d\n", s->id);
    printf("%s\n", s->name);
    printf("%.2f\n", s->marks);
}
```

এখানে function structure modify করবে না।

এটা ভালো coding practice।

---

# 28. NULL Pointer ⚠️

Structure pointer-এর default value:

```c
struct Student *p;
```

এখানে `p` initialized নয়।

এভাবে সরাসরি:

```c
p->id
```

করা dangerous।

Pointer initialize করতে পারো:

```c
struct Student *p = NULL;
```

কিন্তু `NULL` pointer dereference করা যাবে না।

তাই:

```c
if (p != NULL)
{
    printf("%d\n", p->id);
}
```

---

# 29. Dynamic Structure

Dynamic memory-এর সাথে structure pointer খুব গুরুত্বপূর্ণ।

```c
struct Student *p;

p = malloc(sizeof *p);
```

তারপর:

```c
p->id = 101;
p->marks = 85.5;
```

শেষে:

```c
free(p);
```

এর জন্য:

```c
#include <stdlib.h>
```

প্রয়োজন।

---

# 30. Complete Dynamic Example

```c
#include <stdio.h>
#include <stdlib.h>

struct Student
{
    int id;
    char name[50];
    float marks;
};

int main()
{
    struct Student *p;

    p = malloc(sizeof *p);

    if (p == NULL)
    {
        printf("Memory allocation failed.\n");
        return 1;
    }

    p->id = 101;
    p->marks = 85.5;

    printf("ID: %d\n", p->id);
    printf("Marks: %.2f\n", p->marks);

    free(p);

    return 0;
}
```

এখানে `p` heap-এ থাকা একটি `Student` object-এর দিকে point করছে।

Dynamic Memory Allocation আমরা Phase 6-এ শিখেছি; এখন structure-এর সাথে সেটা ব্যবহার করছি।

---

# 31. `malloc()` কেন `sizeof *p`?

আমরা লিখতে পারতাম:

```c
malloc(sizeof(struct Student))
```

কিন্তু:

```c
malloc(sizeof *p)
```

খুব convenient।

কারণ `p` যদি পরে অন্য compatible structure pointer হয়, expression-টি automatically তার type অনুযায়ী size নেয়।

---

# 32. Structure Pointer-এর Real-Life Use

ধরো Bank system:

```c
struct Account
{
    int accountNumber;
    char name[50];
    float balance;
};
```

Function:

```c
void deposit(struct Account *account, float amount)
{
    account->balance += amount;
}
```

Call:

```c
deposit(&account1, 500);
```

এখন original account-এর balance পরিবর্তিত হবে।

এটাই ভবিষ্যতের **Bank Management System**-এ ব্যবহার করতে পারবে।

---

# 33. আরেকটি Example — Product

```c
struct Product
{
    int id;
    float price;
    int quantity;
};
```

Function:

```c
void increaseQuantity(struct Product *p, int amount)
{
    p->quantity += amount;
}
```

Call:

```c
increaseQuantity(&product, 10);
```

---

# 34. `.` বনাম `->` — Final Cheat Sheet

|Situation|Syntax|
|---|---|
|Structure variable|`s.id`|
|Structure pointer|`p->id`|
|Address|`&s`|
|Dereference|`*p`|
|Equivalent of `p->id`|`(*p).id`|
|Array structure|`students[i].id`|
|Pointer + array|`(p+i)->id`|
|Nested structure|`s.date.year`|
|Pointer + nested|`p->date.year`|

---

# 🧠 Golden Rule

শুধু এটা মনে রাখলেও অনেকটা হয়ে যাবে:

```text
struct variable → .
struct pointer  → ->
```

Example:

```c
struct Student s;
struct Student *p = &s;

s.id       // .
p->id      // ->
```

---

# 🧪 Practice 1

এই structure:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

একটি Student তৈরি করো।

তারপর:

```c
struct Student *p
```

ব্যবহার করে:

- ID print
    
- Name print
    
- Marks print
    

করো।

---

# 🧪 Practice 2

Function বানাও:

```c
void increaseMarks(struct Student *s)
```

যা Student-এর marks **10** বাড়াবে।

Example:

```text
Before: 80
After: 90
```

---

# 🧪 Practice 3

5টি Student-এর array বানাও:

```c
struct Student students[5];
```

তারপর pointer ব্যবহার করে সব Student print করো।

Hint:

```c
struct Student *p = students;
```

তারপর:

```c
p++;
```

---

# 🔥 Challenge

একটি function বানাও:

```c
void findTopper(struct Student *students, int n)
```

যা:

1. array-এর সব Student check করবে
    
2. highest marks বের করবে
    
3. topper-এর ID, name, marks print করবে
    

**শর্ত:** function-এর ভিতরে `students[i].marks` ব্যবহার না করে pointer notation ব্যবহার করার চেষ্টা করো:

```c
(students + i)->marks
```

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ✅ Nested structure
48. ✅ Array of structures
49. ✅ Pointer to structure
50. ⏳ typedef
51. ⏳ union
52. ⏳ enum
```

## 🚀 Next → Lesson 50 — `typedef`

পরের lesson-এ দেখব কেন বারবার:

```c
struct Student s1;
```

লেখার বদলে আমরা:

```c
typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;
```

লিখে শুধু:

```c
Student s1;
```

ব্যবহার করতে পারি।

-----

# 🚀 Lesson 50 — `typedef` in C

আজ আমরা শিখব **`typedef`**।

`typedef` প্রথমে একটু অদ্ভুত লাগতে পারে, কিন্তু concept খুব simple:

> `typedef` ব্যবহার করে কোনো existing data type-এর জন্য **নতুন নাম (alias)** দেওয়া যায়।

বিশেষ করে `struct`-এর সাথে এটা খুব বেশি ব্যবহার হয়।

---

# 1. Basic `typedef`

ধরো:

```c
typedef int Number;
```

এখন:

```c
Number x = 10;
```

মূলত একই:

```c
int x = 10;
```

অর্থাৎ:

```text
Number → int-এর নতুন নাম
```

---

# 2. কেন দরকার?

ধরো:

```c
unsigned long int
```

বারবার লিখতে বিরক্তিকর।

তাই:

```c
typedef unsigned long int ULong;
```

এখন:

```c
ULong x = 1000;
```

---

# 3. Syntax

General syntax:

```c
typedef existing_type new_name;
```

Example:

```c
typedef int Age;
```

তারপর:

```c
Age age = 15;
```

---

# 4. `typedef` Structure-এর সাথে 🔥

আমরা আগে লিখতাম:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

তারপর variable:

```c
struct Student s1;
```

`typedef` ব্যবহার করলে:

```c
typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;
```

এখন:

```c
Student s1;
```

লিখলেই হবে।

---

# 5. Full Example

```c
#include <stdio.h>

typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;

int main()
{
    Student s1 = {101, "Rahim", 85.5};

    printf("ID: %d\n", s1.id);
    printf("Name: %s\n", s1.name);
    printf("Marks: %.2f\n", s1.marks);

    return 0;
}
```

Output:

```text
ID: 101
Name: Rahim
Marks: 85.50
```

---

# 6. আসলে কী পরিবর্তন হলো?

`typedef` ছাড়া:

```c
struct Student s1;
struct Student s2;
struct Student s3;
```

`typedef` সহ:

```c
Student s1;
Student s2;
Student s3;
```

Structure-এর definition একই থাকে।

শুধু লেখাটা shorter হয়।

---

# 7. `typedef struct` দুইভাবে লেখা যায়

### Style 1 — Anonymous structure

```c
typedef struct
{
    int id;
    char name[50];
} Student;
```

এখন:

```c
Student s1;
```

---

### Style 2 — Named structure

```c
typedef struct Student
{
    int id;
    char name[50];
} Student;
```

এখন দুটোই valid:

```c
struct Student s1;
```

এবং:

```c
Student s2;
```

---

# 8. Difference

### Anonymous:

```c
typedef struct
{
    int id;
} Student;
```

এখানে structure tag নেই।

তাই সাধারণত:

```c
Student s1;
```

ব্যবহার করবে।

---

### Named:

```c
typedef struct Student
{
    int id;
} Student;
```

এখানে:

```text
struct tag = Student
typedef name = Student
```

দুটোই একই spelling হলেও technically দুটো আলাদা concept।

---

# 9. Structure Pointer + `typedef`

আগে:

```c
struct Student *p;
```

এখন:

```c
Student *p;
```

উদাহরণ:

```c
Student s1 = {101, "Rahim", 85.5};

Student *p = &s1;

printf("%d\n", p->id);
```

---

# 10. Function Parameter

আগে:

```c
void printStudent(struct Student *s)
```

এখন:

```c
void printStudent(Student *s)
```

Example:

```c
void printStudent(Student *s)
{
    printf("ID: %d\n", s->id);
    printf("Name: %s\n", s->name);
    printf("Marks: %.2f\n", s->marks);
}
```

Call:

```c
printStudent(&s1);
```

---

# 11. Array of Structures

`typedef` ব্যবহার করলে:

```c
Student students[100];
```

এটা অনেক cleaner।

আগে:

```c
struct Student students[100];
```

---

# 12. Complete Student Example

```c
#include <stdio.h>

typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;

void printStudents(Student students[], int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("%d %s %.2f\n",
               students[i].id,
               students[i].name,
               students[i].marks);
    }
}

int main()
{
    Student students[3] =
    {
        {101, "Rahim", 85.5},
        {102, "Karim", 90.0},
        {103, "Hasan", 78.5}
    };

    printStudents(students, 3);

    return 0;
}
```

এটা আগের code-এর তুলনায় অনেক clean।

---

# 13. `typedef` + Nested Structure

এখন আগের Nested Structure-টাকে আরও সুন্দর করি।

```c
typedef struct
{
    int day;
    int month;
    int year;
} Date;
```

তারপর:

```c
typedef struct
{
    int id;
    char name[50];
    Date birthDate;
} Student;
```

এখন:

```c
Student s1;
```

এবং:

```c
s1.birthDate.year
```

---

# 14. Complete Example

```c
#include <stdio.h>

typedef struct
{
    int day;
    int month;
    int year;
} Date;

typedef struct
{
    int id;
    char name[50];
    Date birthDate;
} Student;

int main()
{
    Student s1 =
    {
        101,
        "Rahim",
        {15, 8, 2005}
    };

    printf("ID: %d\n", s1.id);
    printf("Name: %s\n", s1.name);

    printf("Birth Date: %d-%d-%d\n",
           s1.birthDate.day,
           s1.birthDate.month,
           s1.birthDate.year);

    return 0;
}
```

---

# 15. `typedef` শুধু Structure-এর জন্য নয়

এটা মনে রাখা গুরুত্বপূর্ণ।

`typedef` যেকোনো existing type-এর alias দিতে পারে।

### `int`

```c
typedef int Integer;

Integer x = 10;
```

### `float`

```c
typedef float Decimal;

Decimal price = 99.5;
```

### `char`

```c
typedef char Character;

Character grade = 'A';
```

---

# 16. Pointer-এর Alias

এটাও করা যায়:

```c
typedef int* IntPtr;
```

তারপর:

```c
IntPtr p;
```

মূলত:

```c
int *p;
```

এর মতো।

⚠️ তবে pointer typedef-এর ক্ষেত্রে readability নিয়ে সতর্ক থাকতে হয়।

---

# 17. `typedef` বনাম `#define`

দুটোকে beginner level-এ confuse করা হয়।

### `typedef`

```c
typedef int Number;
```

এটি একটি **type alias** তৈরি করে।

### `#define`

```c
#define PI 3.14159
```

এটি preprocessor-এর **text replacement**।

দুটো একই জিনিস নয়।

---

# 18. `typedef` কোনো নতুন type তৈরি করে?

সাধারণভাবে beginner হিসেবে মনে রাখো:

> `typedef` existing type-এর জন্য একটি নতুন নাম দেয়।

যেমন:

```c
typedef int Number;
```

`Number` এখানে `int`-এর alias।

---

# 19. `typedef` + Function Pointer

এটা একটু advanced, কিন্তু conceptটা দেখো।

Normal function pointer:

```c
int (*operation)(int, int);
```

`typedef` দিয়ে:

```c
typedef int (*Operation)(int, int);
```

এখন:

```c
Operation op;
```

এটা পরে **Function Pointer** lesson-এ বিস্তারিত করব।

---

# 20. `typedef` + `enum`

পরের দিকে:

```c
typedef enum
{
    RED,
    GREEN,
    BLUE
} Color;
```

এখন:

```c
Color c = RED;
```

এটাও খুব common pattern।

---

# 21. `typedef` + `union`

পরের lesson-এর topic `union`।

সেখানে:

```c
typedef union
{
    int i;
    float f;
} Data;
```

এখন:

```c
Data d;
```

লিখতে পারবে।

---

# 22. Real Project Style 🔥

বড় C project-এ প্রায়ই header file-এ type definitions রাখা হয়।

যেমন `student.h`:

```c
#ifndef STUDENT_H
#define STUDENT_H

typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;

void printStudent(Student *s);

#endif
```

তারপর অন্য `.c` file-এ:

```c
#include "student.h"
```

এবং:

```c
Student s1;
```

এভাবে project organized রাখা যায়।

---

# 23. একটি গুরুত্বপূর্ণ Naming Convention

তুমি চাইলে:

```c
typedef struct
{
    int id;
} Student;
```

এভাবে type-এর নাম capital letter দিয়ে রাখতে পারো।

যেমন:

```text
Student
Book
Product
Employee
Date
Account
```

এটা বাধ্যতামূলক নয়; project-এর coding convention অনুসরণ করাই আসল।

---

# 24. `typedef` ব্যবহার করে Student System

এখন আমাদের আগের Student Management-এর code অনেক clean:

```c
#include <stdio.h>

typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;

void addStudent(Student *s)
{
    printf("Enter ID: ");
    scanf("%d", &s->id);

    printf("Enter Name: ");
    scanf("%49s", s->name);

    printf("Enter Marks: ");
    scanf("%f", &s->marks);
}

void printStudent(const Student *s)
{
    printf("\nID: %d\n", s->id);
    printf("Name: %s\n", s->name);
    printf("Marks: %.2f\n", s->marks);
}

int main()
{
    Student s1;

    addStudent(&s1);
    printStudent(&s1);

    return 0;
}
```

এখানে একসাথে ব্যবহার হয়েছে:

```text
typedef
struct
pointer
function
scanf
printf
```

🔥 এটা এখন real-world C code-এর মতো দেখতে শুরু করেছে।

---

# 25. কখন `typedef` ব্যবহার করা ভালো?

বিশেষ করে:

### 1. Structure

```c
typedef struct {...} Student;
```

### 2. Complex types

যেমন function pointer।

### 3. Project-wide data types

যেমন:

```c
typedef unsigned long ulong;
```

তবে অপ্রয়োজনীয়ভাবে প্রতিটি primitive type-এর alias বানানো উচিত নয়। Code readable হচ্ছে কিনা সেটাও দেখতে হবে।

---

# 🧠 Cheat Sheet

### Without typedef

```c
struct Student
{
    int id;
};

struct Student s;
```

### With typedef

```c
typedef struct
{
    int id;
} Student;

Student s;
```

### Pointer

```c
Student *p = &s;
```

### Access

```c
s.id
p->id
```

### Array

```c
Student students[100];
```

### Function

```c
void printStudent(Student *s)
```

---

# 🧪 Practice 1

`Book` নামে একটি typedef structure তৈরি করো:

```text
id
title
price
```

তারপর:

```c
Book b1;
```

ব্যবহার করে data assign ও print করো।

---

# 🧪 Practice 2

এই দুইটি type তৈরি করো:

```c
Date
Student
```

`Student`-এর মধ্যে `Date birthDate` রাখো।

তারপর:

```c
Student s1;
```

দিয়ে পুরো তথ্য print করো।

---

# 🧪 Practice 3

`Product` নামে typedef structure বানাও:

```text
id
name
price
quantity
```

তারপর:

```c
Product products[5];
```

ব্যবহার করে 5টি product রাখো এবং inventory value calculate করো।

Formula:

```text
price × quantity
```

---

# 🔥 Challenge

একটি ছোট **Student Management Core** বানাও:

```c
typedef struct
{
    int id;
    char name[50];
    float marks;
} Student;
```

তারপর functions:

```c
void addStudent(Student *s);
void printStudent(const Student *s);
void updateMarks(Student *s);
```

ব্যবহার করো।

লক্ষ্য হলো এই তিনটি concept একসাথে comfortable হওয়া:

```text
typedef
    ↓
struct
    ↓
pointer
```

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ✅ Nested structure
48. ✅ Array of structures
49. ✅ Pointer to structure
50. ✅ typedef
51. ⏳ union
52. ⏳ enum
```

## 🚀 Next → Lesson 51 — `union`

পরের lesson-এ দেখব `struct` আর `union`-এর মধ্যে আসল পার্থক্য কী এবং কেন `union`-এর members একই memory space share করে।

----
# 🚀 Lesson 51 — `union` in C

আজ আমরা শিখব **`union`**।

`union` দেখতে অনেকটা `struct`-এর মতো, কিন্তু সবচেয়ে গুরুত্বপূর্ণ পার্থক্য হলো:

> **`struct`-এর প্রতিটি member-এর আলাদা memory থাকে, কিন্তু `union`-এর সব member একই memory space share করে।**

এটাই আজকের মূল concept। 🔥

---

# 1. `struct` vs `union`

প্রথমে `struct`:

```c
struct Data
{
    int i;
    float f;
    char c;
};
```

এখানে `i`, `f`, `c` প্রত্যেকটির নিজের জায়গা থাকে।

অন্যদিকে:

```c
union Data
{
    int i;
    float f;
    char c;
};
```

এখানে তিনটি member **একই memory location share করে**।

---

# 2. Basic `union` Syntax

```c
union Data
{
    int i;
    float f;
    char c;
};
```

Variable:

```c
union Data d;
```

তারপর:

```c
d.i = 10;
```

অথবা:

```c
d.f = 20.5;
```

অথবা:

```c
d.c = 'A';
```

কিন্তু একই সময়ে তিনটি value independentভাবে রাখা যায় না।

---

# 3. `struct`-এর Example

```c
#include <stdio.h>

struct Data
{
    int i;
    float f;
    char c;
};

int main()
{
    struct Data d;

    d.i = 10;
    d.f = 20.5;
    d.c = 'A';

    printf("%d\n", d.i);
    printf("%.2f\n", d.f);
    printf("%c\n", d.c);

    return 0;
}
```

এখানে তিনটি value আলাদাভাবে থাকে।

---

# 4. একই Example with `union`

```c
#include <stdio.h>

union Data
{
    int i;
    float f;
    char c;
};

int main()
{
    union Data d;

    d.i = 10;
    printf("i = %d\n", d.i);

    d.f = 20.5;
    printf("f = %.2f\n", d.f);

    d.c = 'A';
    printf("c = %c\n", d.c);

    return 0;
}
```

এখানে প্রত্যেকবার নতুন member-এ value assign করার সময় shared memory-এর content বদলে যায়।

---

# 5. সবচেয়ে গুরুত্বপূর্ণ বিষয় 🔥

ধরো:

```c
union Data
{
    int i;
    float f;
};
```

তারপর:

```c
union Data d;

d.i = 10;
```

এখন `i`-এর value valid।

তারপর:

```c
d.f = 20.5;
```

এখন union-এর shared memory-তে `float` value রাখা হয়েছে।

তাই আগের `d.i` value-কে independentভাবে ধরে রাখা যাবে না।

---

# 6. Visualize

### `struct`

```text
struct
┌──────────────┐
│ int i        │
├──────────────┤
│ float f      │
├──────────────┤
│ char c       │
└──────────────┘
```

প্রতিটি member-এর আলাদা storage।

### `union`

```text
union
┌──────────────┐
│              │
│ i / f / c    │
│              │
└──────────────┘
      ↑
   shared
   memory
```

একই memory location।

---

# 7. Memory Size 🔥

`struct`-এর size সাধারণত সব members-এর জন্য প্রয়োজনীয় storage-এর সমষ্টি, padding-সহ।

`union`-এর size সাধারণত সবচেয়ে বড় member-কে ধারণ করার মতো যতটা storage দরকার, অন্তত ততটাই হয়, alignment-এর বিষয়ও থাকতে পারে।

Example:

```c
union Data
{
    int i;
    double d;
    char c;
};
```

যদি:

```text
int    = 4 bytes
double = 8 bytes
char   = 1 byte
```

হয়, তাহলে union-এর size সাধারণত `double`-এর প্রয়োজনীয় storage অনুযায়ী হবে।

অর্থাৎ প্রায়:

```text
8 bytes
```

---

# 8. `sizeof()` দিয়ে দেখা

```c
#include <stdio.h>

struct DataStruct
{
    int i;
    double d;
    char c;
};

union DataUnion
{
    int i;
    double d;
    char c;
};

int main()
{
    printf("Struct: %zu bytes\n",
           sizeof(struct DataStruct));

    printf("Union: %zu bytes\n",
           sizeof(union DataUnion));

    return 0;
}
```

তোমার compiler/platform অনুযায়ী `struct`-এর size padding/alignment-এর কারণে কিছুটা ভিন্ন হতে পারে।

---

# 9. `typedef union`

যেমন আমরা `struct`-এ করেছিলাম:

```c
typedef struct
{
    int id;
} Student;
```

ঠিক একইভাবে:

```c
typedef union
{
    int i;
    float f;
    char c;
} Data;
```

এখন:

```c
Data d;
```

ব্যবহার করা যাবে।

---

# 10. Complete Example

```c
#include <stdio.h>

typedef union
{
    int i;
    float f;
    char c;
} Data;

int main()
{
    Data d;

    d.i = 100;
    printf("Integer: %d\n", d.i);

    d.f = 25.5;
    printf("Float: %.2f\n", d.f);

    d.c = 'A';
    printf("Character: %c\n", d.c);

    return 0;
}
```

---

# 11. `union` কখন ব্যবহার করব?

Union useful যখন:

> একই memory location-এ বিভিন্ন ধরনের data-এর মধ্যে **একবারে একটি** রাখতে হবে।

বিশেষ করে:

- memory-sensitive systems
    
- embedded systems
    
- hardware-related programming
    
- protocol/data representation
    
- variant data
    
- low-level programming
    

---

# 12. Real-Life Example — Payment

ধরো একটি payment system-এ payment-এর ধরন হতে পারে:

```text
Cash
Card
Mobile
```

একটি transaction-এ একসাথে সব ধরনের payment information দরকার নেই।

তাই একটি union ব্যবহার করা যেতে পারে:

```c
typedef union
{
    float cashAmount;
    int cardNumber;
    int mobileNumber;
} PaymentData;
```

কিন্তু এখানে একটি গুরুত্বপূর্ণ সমস্যা আছে:

**Union নিজে জানে না বর্তমানে কোন member valid।**

তাই সাধারণত একটি আলাদা `enum` বা tag ব্যবহার করা হয়।

---

# 13. Tagged Union 🔥

এটা খুব গুরুত্বপূর্ণ real-world pattern।

```c
#include <stdio.h>

typedef enum
{
    CASH,
    CARD
} PaymentType;

typedef union
{
    float cashAmount;
    int cardNumber;
} PaymentData;

typedef struct
{
    PaymentType type;
    PaymentData data;
} Payment;
```

এখানে:

```text
Payment
├── type
└── data
    ├── cashAmount
    └── cardNumber
```

`type` বলে দিচ্ছে কোন union member valid।

---

# 14. Cash Payment

```c
Payment p;

p.type = CASH;
p.data.cashAmount = 500.0;
```

এখানে:

```text
type = CASH
```

তাই:

```c
p.data.cashAmount
```

valid data।

---

# 15. Card Payment

```c
p.type = CARD;
p.data.cardNumber = 12345;
```

এখন:

```text
type = CARD
```

তাই:

```c
p.data.cardNumber
```

valid member।

---

# 16. `switch` দিয়ে ব্যবহার

```c
switch (p.type)
{
    case CASH:
        printf("Cash: %.2f\n",
               p.data.cashAmount);
        break;

    case CARD:
        printf("Card: %d\n",
               p.data.cardNumber);
        break;
}
```

এখানে আমরা তিনটি concept combine করেছি:

```text
enum
+
union
+
struct
```

🔥 এগুলো পরে আরও ভালোভাবে ব্যবহার করব।

---

# 17. Structure + Union

আরেকটি common pattern:

```c
typedef struct
{
    int id;

    union
    {
        int age;
        float salary;
    } info;

} Person;
```

এখন:

```c
Person p;

p.id = 101;
p.info.age = 20;
```

অথবা:

```c
p.info.salary = 25000.0;
```

কিন্তু `age` এবং `salary` একই union storage share করছে।

---

# 18. Union Pointer

Union-এর pointer-ও structure-এর মতো:

```c
Data d;

Data *p = &d;
```

তারপর:

```c
p->i = 100;
```

অথবা:

```c
p->f = 25.5;
```

কারণ `->` pointer-to-union-এর member access-এর ক্ষেত্রেও কাজ করে।

---

# 19. Union + Function

```c
void setInteger(Data *d, int value)
{
    d->i = value;
}
```

Call:

```c
setInteger(&d, 100);
```

এখানে `d` pointer দিয়ে original union modify হচ্ছে।

---

# 20. গুরুত্বপূর্ণ ⚠️

এই ধরনের code:

```c
d.i = 10;
printf("%d\n", d.i);

d.f = 20.5;
printf("%.2f\n", d.f);
```

ঠিক আছে, কারণ প্রত্যেকবার যে member-এ value লিখেছ, সেই member-টাই read করছ।

কিন্তু:

```c
d.i = 10;
d.f = 20.5;

printf("%d\n", d.i);
```

এখানে `d.i`-কে আগের `10` হিসেবে ধরে নেওয়া যাবে না।

কারণ পরে `d.f`-তে লিখে shared storage-এর content পরিবর্তন হয়েছে।

---

# 21. Struct vs Union

|বিষয়|`struct`|`union`|
|---|---|---|
|Members|আলাদা storage|একই storage share করে|
|একসাথে সব value রাখা|✅|❌|
|Size|সব members + padding/alignment-এর উপর নির্ভর|সবচেয়ে বড় member + alignment-এর উপর নির্ভর|
|Memory efficient|তুলনামূলক কম|তুলনামূলক বেশি|
|সাধারণ data record|✅|সাধারণত নয়|
|Variant data|সম্ভব, কিন্তু আলাদা design দরকার|✅ useful|

---

# 22. খুব সহজে মনে রাখো

### `struct`

> **সবগুলো একসাথে**

```text
A + B + C
```

### `union`

> **একই জায়গায়, একবারে একটি**

```text
A / B / C
```

🔥 এই difference ভুলবে না।

---

# 23. একটি Practical Example

ধরো sensor system-এ একটি sensor value কখনো integer, কখনো floating-point:

```c
typedef union
{
    int integerValue;
    float floatValue;
} SensorValue;
```

তারপর:

```c
SensorValue value;

value.floatValue = 23.5;
```

এখানে floating-point representation রাখার জন্য shared memory ব্যবহার হচ্ছে।

---

# 24. কখন `union` ব্যবহার না করাই ভালো?

যদি তোমার সত্যিই একই সময়ে সব data দরকার হয়, তাহলে `union` ব্যবহার করো না।

যেমন:

```c
struct Student
{
    int id;
    char name[50];
    float marks;
};
```

এখানে `id`, `name`, `marks` সব একসাথে দরকার।

তাই `struct` সঠিক।

---

# 🧠 Golden Rule

```text
STRUCT
→ Each member has separate storage
→ All members can hold values simultaneously

UNION
→ Members share storage
→ Usually one active member at a time
```

---

# 🧪 Practice 1

এই union তৈরি করো:

```c
typedef union
{
    int i;
    float f;
    char c;
} Data;
```

তারপর প্রত্যেক member-এ value assign করে print করো।

---

# 🧪 Practice 2

`struct` এবং `union`-এর `sizeof()` compare করো।

```c
struct Test
{
    int i;
    float f;
    char c;
};

union TestUnion
{
    int i;
    float f;
    char c;
};
```

তারপর:

```c
printf("%zu\n", sizeof(struct Test));
printf("%zu\n", sizeof(union TestUnion));
```

নিজের compiler-এ output দেখো।

---

# 🧪 Practice 3

একটি tagged payment system বানাও:

```text
CASH
CARD
```

`enum` দিয়ে type এবং `union` দিয়ে data রাখবে।

তারপর `switch` দিয়ে payment information print করবে।

---

# 🔥 Challenge

একটি `Person` type বানাও:

```text
id
type
data
```

`type` হতে পারে:

```text
STUDENT
EMPLOYEE
```

Student হলে:

```text
roll
```

Employee হলে:

```text
salary
```

`union` ব্যবহার করে এমন design তৈরি করো যাতে একই memory space-এ `roll` অথবা `salary` রাখা যায়।

Hint:

```c
typedef enum
{
    STUDENT,
    EMPLOYEE
} PersonType;
```

তারপর `union` এবং `struct` combine করো।

---

# 🎯 Phase 7 Progress

```text
46. ✅ struct
47. ✅ Nested structure
48. ✅ Array of structures
49. ✅ Pointer to structure
50. ✅ typedef
51. ✅ union
52. ⏳ enum
```

## 🚀 Next → Lesson 52 — `enum`

শেষ structure-related topic হিসেবে `enum` শিখব। সেখানে দেখব কীভাবে:

```c
enum
```

দিয়ে meaningful names ব্যবহার করা যায়, এবং `switch-case`, `struct`, `union`-এর সাথে কীভাবে combine করা যায়।


----

# 🚀 Lesson 52 — `enum` in C

এটা **Phase 7 — Structures**-এর শেষ lesson। 🎉

আজ আমরা শিখব:

- `enum` কী
    
- কেন ব্যবহার করি
    
- enum values
    
- custom values
    
- `typedef enum`
    
- `switch` + enum
    
- `struct` + enum
    
- `union` + enum
    
- real-world example
    

---

# 1. `enum` কী?

`enum` = **Enumeration**

এটি related কিছু named integer constants তৈরি করতে ব্যবহার করা হয়।

যেমন একটি traffic light-এর তিনটি state:

```text
RED
YELLOW
GREEN
```

C-তে:

```c
enum TrafficLight
{
    RED,
    YELLOW,
    GREEN
};
```

এখন:

```c
enum TrafficLight light;
```

---

# 2. Value কী হয়?

যদি আমরা লিখি:

```c
enum TrafficLight
{
    RED,
    YELLOW,
    GREEN
};
```

তাহলে default values হয়:

```text
RED    = 0
YELLOW = 1
GREEN  = 2
```

অর্থাৎ compiler সাধারণত প্রথম নামকে `0` দিয়ে শুরু করে এবং পরেরগুলো এক করে বাড়ায়।

---

# 3. Complete Example

```c
#include <stdio.h>

enum TrafficLight
{
    RED,
    YELLOW,
    GREEN
};

int main()
{
    enum TrafficLight light;

    light = GREEN;

    printf("%d\n", light);

    return 0;
}
```

Output:

```text
2
```

কারণ:

```text
RED    → 0
YELLOW → 1
GREEN  → 2
```

---

# 4. কিন্তু Number না লিখে Name কেন?

এই:

```c
if (light == 2)
```

দেখলে বোঝা কঠিন `2` কী।

কিন্তু:

```c
if (light == GREEN)
```

দেখলেই বোঝা যায়।

🔥 এটাই `enum`-এর বড় সুবিধা:

> **Code readable করা।**

---

# 5. `switch` + `enum` 🔥

`enum` এবং `switch` একসাথে খুব সুন্দর কাজ করে।

```c
#include <stdio.h>

enum TrafficLight
{
    RED,
    YELLOW,
    GREEN
};

int main()
{
    enum TrafficLight light = GREEN;

    switch (light)
    {
        case RED:
            printf("Stop\n");
            break;

        case YELLOW:
            printf("Wait\n");
            break;

        case GREEN:
            printf("Go\n");
            break;
    }

    return 0;
}
```

Output:

```text
Go
```

---

# 6. `typedef enum`

আগের `struct` ও `union`-এর মতো enum-এও `typedef` ব্যবহার করা যায়।

```c
typedef enum
{
    RED,
    YELLOW,
    GREEN
} TrafficLight;
```

এখন:

```c
TrafficLight light;
```

লিখলেই হবে।

আগের:

```c
enum TrafficLight light;
```

লিখতে হবে না।

---

# 7. Complete Example

```c
#include <stdio.h>

typedef enum
{
    RED,
    YELLOW,
    GREEN
} TrafficLight;

int main()
{
    TrafficLight light = GREEN;

    if (light == GREEN)
    {
        printf("Go\n");
    }

    return 0;
}
```

---

# 8. Custom Values

Default values:

```c
enum Level
{
    LOW,
    MEDIUM,
    HIGH
};
```

হলে:

```text
LOW    = 0
MEDIUM = 1
HIGH   = 2
```

তুমি চাইলে নিজে value দিতে পারো:

```c
enum Level
{
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30
};
```

এখন:

```text
LOW    = 10
MEDIUM = 20
HIGH   = 30
```

---

# 9. Partial Custom Values

```c
enum Number
{
    A = 5,
    B,
    C
};
```

তাহলে:

```text
A = 5
B = 6
C = 7
```

আবার:

```c
enum Number
{
    A = 5,
    B = 10,
    C
};
```

তাহলে:

```text
A = 5
B = 10
C = 11
```

---

# 10. Duplicate Values সম্ভব

```c
enum Result
{
    SUCCESS = 1,
    OK = 1,
    FAILED = 0
};
```

এখানে:

```text
SUCCESS = 1
OK      = 1
FAILED  = 0
```

এটা technically valid।

---

# 11. Enum Variable

```c
TrafficLight light;
```

তারপর:

```c
light = RED;
```

অথবা:

```c
light = GREEN;
```

---

# 12. Enum সাধারণত Integer-Based

Enum constants integer values represent করে।

যেমন:

```c
printf("%d\n", GREEN);
```

Output:

```text
2
```

তবে `enum`-কে শুধু "integer-এর fancy নাম" হিসেবে না দেখে **meaningful set of named states** হিসেবে ভাবা ভালো।

---

# 13. `enum` + User Input

ধরো menu:

```text
1. Add
2. Search
3. Exit
```

Enum:

```c
typedef enum
{
    ADD = 1,
    SEARCH = 2,
    EXIT = 3
} MenuOption;
```

তারপর:

```c
int choice;

scanf("%d", &choice);

switch (choice)
{
    case ADD:
        printf("Add selected\n");
        break;

    case SEARCH:
        printf("Search selected\n");
        break;

    case EXIT:
        printf("Exit selected\n");
        break;

    default:
        printf("Invalid choice\n");
}
```

এটা CLI project-এ অনেক কাজে লাগবে।

---

# 14. `enum` + `struct` 🔥

এবার দুটো combine করি।

```c
typedef enum
{
    STUDENT,
    TEACHER
} PersonType;
```

তারপর:

```c
typedef struct
{
    char name[50];
    PersonType type;
} Person;
```

এখন:

```c
Person p;

p.type = STUDENT;
```

---

# 15. Complete Example

```c
#include <stdio.h>

typedef enum
{
    STUDENT,
    TEACHER
} PersonType;

typedef struct
{
    char name[50];
    PersonType type;
} Person;

int main()
{
    Person p = {"Rahim", STUDENT};

    printf("Name: %s\n", p.name);

    if (p.type == STUDENT)
    {
        printf("Type: Student\n");
    }
    else
    {
        printf("Type: Teacher\n");
    }

    return 0;
}
```

---

# 16. `enum` + `union` 🔥🔥

এটাই আগের lesson-এর tagged union-এর complete idea।

```c
typedef enum
{
    STUDENT,
    EMPLOYEE
} PersonType;

typedef union
{
    int roll;
    float salary;
} PersonData;

typedef struct
{
    PersonType type;
    PersonData data;
} Person;
```

এখন:

```c
Person p;
```

Student:

```c
p.type = STUDENT;
p.data.roll = 25;
```

Employee:

```c
p.type = EMPLOYEE;
p.data.salary = 30000;
```

---

# 17. `switch` দিয়ে Tagged Union

```c
switch (p.type)
{
    case STUDENT:
        printf("Roll: %d\n", p.data.roll);
        break;

    case EMPLOYEE:
        printf("Salary: %.2f\n", p.data.salary);
        break;
}
```

এখানে `type` বলে দিচ্ছে union-এর কোন member ব্যবহার করতে হবে।

---

# 18. Full Example 🔥

```c
#include <stdio.h>

typedef enum
{
    STUDENT,
    EMPLOYEE
} PersonType;

typedef union
{
    int roll;
    float salary;
} PersonData;

typedef struct
{
    char name[50];
    PersonType type;
    PersonData data;
} Person;

int main()
{
    Person p;

    p.type = STUDENT;

    printf("Enter name: ");
    scanf("%49s", p.name);

    printf("Enter roll: ");
    scanf("%d", &p.data.roll);

    printf("\nName: %s\n", p.name);

    switch (p.type)
    {
        case STUDENT:
            printf("Type: Student\n");
            printf("Roll: %d\n", p.data.roll);
            break;

        case EMPLOYEE:
            printf("Type: Employee\n");
            printf("Salary: %.2f\n", p.data.salary);
            break;
    }

    return 0;
}
```

এখানে:

```text
struct
   +
union
   +
enum
   +
switch
```

সব একসাথে ব্যবহার হয়েছে।

---

# 19. Enum দিয়ে State Machine

Enum-এর আরেকটি গুরুত্বপূর্ণ ব্যবহার হলো **program state**।

```c
typedef enum
{
    START,
    RUNNING,
    PAUSED,
    STOPPED
} State;
```

তারপর:

```c
State state = START;
```

এবং:

```c
switch (state)
{
    case START:
        printf("Starting...\n");
        break;

    case RUNNING:
        printf("Running...\n");
        break;

    case PAUSED:
        printf("Paused...\n");
        break;

    case STOPPED:
        printf("Stopped.\n");
        break;
}
```

Games, embedded systems, menus এবং বিভিন্ন application-এ state management-এর জন্য এই pattern খুব useful।

---

# 20. Enum + Functions

Function parameter-এ enum ব্যবহার করা যায়:

```c
void printState(State state)
{
    switch (state)
    {
        case START:
            printf("Start\n");
            break;

        case RUNNING:
            printf("Running\n");
            break;

        case PAUSED:
            printf("Paused\n");
            break;

        case STOPPED:
            printf("Stopped\n");
            break;
    }
}
```

Call:

```c
printState(RUNNING);
```

---

# 21. Enum-এর একটি Important Limitation ⚠️

`enum` **string store করে না**।

যেমন:

```c
typedef enum
{
    RED,
    GREEN,
    BLUE
} Color;
```

এখানে `RED` নিজে `"RED"` string নয়।

এটা একটি integer-like enumeration constant।

তাই:

```c
printf("%s\n", RED);
```

সঠিক নয়।

---

# 22. Enum থেকে String চাইলে

নিজে mapping করতে পারো:

```c
const char *colorName(Color color)
{
    switch (color)
    {
        case RED:
            return "RED";

        case GREEN:
            return "GREEN";

        case BLUE:
            return "BLUE";

        default:
            return "UNKNOWN";
    }
}
```

তারপর:

```c
printf("%s\n", colorName(GREEN));
```

Output:

```text
GREEN
```

---

# 23. `enum` কোথায় বেশি ব্যবহার করবে?

### Menu

```text
ADD
SEARCH
UPDATE
DELETE
EXIT
```

### Status

```text
PENDING
APPROVED
REJECTED
```

### User type

```text
ADMIN
USER
GUEST
```

### Game state

```text
START
PLAYING
PAUSED
GAME_OVER
```

### Payment type

```text
CASH
CARD
MOBILE
```

---

# 24. Real Project Example — Bank

আমাদের ভবিষ্যতের Bank Management System-এ:

```c
typedef enum
{
    ACTIVE,
    BLOCKED,
    CLOSED
} AccountStatus;
```

তারপর:

```c
typedef struct
{
    int accountNumber;
    char name[50];
    float balance;
    AccountStatus status;
} Account;
```

এখন:

```c
Account account;
account.status = ACTIVE;
```

এটা:

```c
account.status = 1;
```

এর চেয়ে অনেক বেশি readable।

---

# 25. Real Project Example — Quiz

Quiz application-এ:

```c
typedef enum
{
    EASY,
    MEDIUM,
    HARD
} Difficulty;
```

তারপর:

```c
typedef struct
{
    char question[200];
    Difficulty difficulty;
} Question;
```

এখন:

```c
Question q;

q.difficulty = HARD;
```

---

# 26. `enum` + Array

Enum values দিয়ে array index করাও সম্ভব।

```c
typedef enum
{
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY
} Day;
```

তারপর:

```c
int temperature[5];
```

এখন:

```c
temperature[MONDAY] = 30;
temperature[FRIDAY] = 28;
```

এতে code readable হয়।

---

# 27. Enum Values Automatically Increment

```c
enum Day
{
    MONDAY,
    TUESDAY,
    WEDNESDAY
};
```

Conceptually:

```text
MONDAY    = 0
TUESDAY   = 1
WEDNESDAY = 2
```

তাই:

```c
temperature[MONDAY]
```

মানে:

```c
temperature[0]
```

---

# 28. কিন্তু সবসময় 0 থেকে শুরু করতে হবে না

```c
enum HttpStatus
{
    OK = 200,
    NOT_FOUND = 404,
    SERVER_ERROR = 500
};
```

এখন:

```c
printf("%d\n", NOT_FOUND);
```

Output:

```text
404
```

এই ধরনের meaningful numeric constants-এর জন্য enum useful হতে পারে।

---

# 29. `enum` বনাম `#define`

আগে আমরা লিখতে পারতাম:

```c
#define RED 0
#define GREEN 1
#define BLUE 2
```

কিন্তু:

```c
enum Color
{
    RED,
    GREEN,
    BLUE
};
```

সাধারণত related named values-কে এক group হিসেবে প্রকাশ করার জন্য বেশি readable।

---

# 30. সবকিছু একসাথে 🧠

এখন Phase 7-এর সবচেয়ে গুরুত্বপূর্ণ combination:

```c
typedef enum
{
    STUDENT,
    EMPLOYEE
} PersonType;

typedef union
{
    int roll;
    float salary;
} PersonData;

typedef struct
{
    int id;
    char name[50];
    PersonType type;
    PersonData data;
} Person;
```

এখানে:

```text
typedef
  ↓
enum ───────→ type
  ↓
union ──────→ data
  ↓
struct ─────→ complete object
```

এটা বুঝতে পারলে Phase 7-এর core concepts অনেকটাই clear। 🔥

---

# 🧠 Final Cheat Sheet

### Enum declaration

```c
enum Color
{
    RED,
    GREEN,
    BLUE
};
```

### Enum variable

```c
enum Color c = RED;
```

### Typedef

```c
typedef enum
{
    RED,
    GREEN,
    BLUE
} Color;
```

### Custom values

```c
typedef enum
{
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30
} Level;
```

### Switch

```c
switch (c)
{
    case RED:
        break;

    case GREEN:
        break;
}
```

### Struct + enum

```c
typedef struct
{
    char name[50];
    Color color;
} Item;
```

### Union + enum

```c
typedef struct
{
    Type type;
    Data data;
} Object;
```

---

# 🧪 Practice 1

এই enum তৈরি করো:

```text
PENDING
APPROVED
REJECTED
```

তারপর `switch` ব্যবহার করে প্রতিটির জন্য message print করো।

---

# 🧪 Practice 2

একটি `Day` enum তৈরি করো:

```text
SATURDAY
SUNDAY
MONDAY
TUESDAY
WEDNESDAY
THURSDAY
FRIDAY
```

একটি day input নিয়ে সেটা weekend নাকি weekday সেটা নির্ণয় করো।

---

# 🧪 Practice 3

একটি:

```c
typedef enum
```

দিয়ে:

```text
EASY
MEDIUM
HARD
```

তৈরি করো।

তারপর একটি `Question` struct বানাও যার মধ্যে থাকবে:

```text
question
difficulty
```

---

# 🔥 Final Challenge — Mini User System

এই design তৈরি করো:

```c
typedef enum
{
    ADMIN,
    USER
} UserType;
```

এবং:

```c
typedef struct
{
    int id;
    char name[50];
    UserType type;
} User;
```

তারপর 3 জন User input নাও এবং `switch` দিয়ে প্রত্যেকের type print করো।

Expected:

```text
ID: 101
Name: Rahim
Type: ADMIN

ID: 102
Name: Karim
Type: USER
```

---

# 🎉 Phase 7 Complete!

```text
46. ✅ struct
47. ✅ Nested structure
48. ✅ Array of structures
49. ✅ Pointer to structure
50. ✅ typedef
51. ✅ union
52. ✅ enum
```

## 🚀 এখন শুরু হবে Phase 8 — File Handling

পরের lesson:

# 📁 Lesson 53 — File Concept

সেখানে আমরা শিখব:

```text
Program
   ↓
RAM
   ↓
Program বন্ধ
   ↓
Data হারিয়ে যায়
```

এরপর কীভাবে file ব্যবহার করে data **স্থায়ীভাবে save** করা যায়:

```text
Program
   ↓
File
   ↓
Data saved
   ↓
Program আবার চালু
   ↓
Data আবার read
```

এটাই আমাদের ভবিষ্যতের **Student Management, Bank Management এবং E-commerce** project-গুলোকে অনেক বেশি বাস্তবসম্মত করবে।

----
# 🎓 Student Management System — Complete C Project

চলো Phase 1–7-এর concepts একসাথে ব্যবহার করে একটি **menu-driven Student Management System** বানাই।

এই version-এ থাকবে:

- ➕ Add student
    
- 📋 Display all students
    
- 🔍 Search by ID
    
- ✏️ Update student
    
- 🗑️ Delete student
    
- 📊 Calculate average marks
    
- 🏆 Find highest marks
    
- 💾 File-এ data save
    
- 📂 Program চালু হলে data load
    
- 🚪 Exit
    

এখানে আমরা `struct`, `typedef`, `enum`, array, function, pointer, string, loop, `switch`, file handling—সব ব্যবহার করব।

---

# 📁 Project Structure

শুরুতে একটি file দিয়েই বানাও:

```text
StudentManagement/
└── main.c
```

পরবর্তীতে চাইলে এটাকে multiple `.c` এবং `.h` file-এ ভাগ করা যাবে।

---

# 1. Complete `main.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 100
#define FILE_NAME "students.dat"

/* ==============================
   ENUM
   ============================== */

typedef enum
{
    ACTIVE,
    INACTIVE
} StudentStatus;


/* ==============================
   STRUCT
   ============================== */

typedef struct
{
    int id;
    char name[50];
    int age;
    float marks;
    StudentStatus status;
} Student;


/* ==============================
   GLOBAL DATA
   ============================== */

Student students[MAX_STUDENTS];
int studentCount = 0;


/* ==============================
   FUNCTION DECLARATIONS
   ============================== */

void addStudent(void);
void displayStudents(void);
void searchStudent(void);
void updateStudent(void);
void deleteStudent(void);
void showStatistics(void);

void saveToFile(void);
void loadFromFile(void);

int findStudentIndexById(int id);

void clearInputBuffer(void);
void pauseScreen(void);

void printStudent(const Student *s);
void printMenu(void);


/* ==============================
   MAIN
   ============================== */

int main(void)
{
    int choice;

    loadFromFile();

    while (1)
    {
        printMenu();

        printf("Enter your choice: ");
        scanf("%d", &choice);

        clearInputBuffer();

        switch (choice)
        {
            case 1:
                addStudent();
                break;

            case 2:
                displayStudents();
                break;

            case 3:
                searchStudent();
                break;

            case 4:
                updateStudent();
                break;

            case 5:
                deleteStudent();
                break;

            case 6:
                showStatistics();
                break;

            case 7:
                saveToFile();
                printf("\nData saved successfully.\n");
                printf("Goodbye!\n");
                return 0;

            default:
                printf("\nInvalid choice!\n");
        }

        pauseScreen();
    }

    return 0;
}


/* ==============================
   MENU
   ============================== */

void printMenu(void)
{
    printf("\n");
    printf("========================================\n");
    printf("       STUDENT MANAGEMENT SYSTEM        \n");
    printf("========================================\n");

    printf("1. Add Student\n");
    printf("2. Display All Students\n");
    printf("3. Search Student\n");
    printf("4. Update Student\n");
    printf("5. Delete Student\n");
    printf("6. Statistics\n");
    printf("7. Save & Exit\n");

    printf("========================================\n");
}


/* ==============================
   ADD STUDENT
   ============================== */

void addStudent(void)
{
    Student s;

    if (studentCount >= MAX_STUDENTS)
    {
        printf("\nStudent storage is full!\n");
        return;
    }

    printf("\n========== ADD STUDENT ==========\n");

    printf("Enter ID: ");
    scanf("%d", &s.id);
    clearInputBuffer();

    if (findStudentIndexById(s.id) != -1)
    {
        printf("A student with this ID already exists!\n");
        return;
    }

    printf("Enter name: ");
    fgets(s.name, sizeof(s.name), stdin);

    s.name[strcspn(s.name, "\n")] = '\0';

    printf("Enter age: ");
    scanf("%d", &s.age);

    printf("Enter marks: ");
    scanf("%f", &s.marks);

    clearInputBuffer();

    s.status = ACTIVE;

    students[studentCount] = s;
    studentCount++;

    saveToFile();

    printf("\nStudent added successfully!\n");
}


/* ==============================
   DISPLAY STUDENTS
   ============================== */

void displayStudents(void)
{
    int i;

    if (studentCount == 0)
    {
        printf("\nNo students found.\n");
        return;
    }

    printf("\n========== ALL STUDENTS ==========\n");

    for (i = 0; i < studentCount; i++)
    {
        printStudent(&students[i]);
    }
}


/* ==============================
   PRINT ONE STUDENT
   ============================== */

void printStudent(const Student *s)
{
    printf("\n----------------------------------\n");

    printf("ID     : %d\n", s->id);
    printf("Name   : %s\n", s->name);
    printf("Age    : %d\n", s->age);
    printf("Marks  : %.2f\n", s->marks);

    if (s->status == ACTIVE)
    {
        printf("Status : Active\n");
    }
    else
    {
        printf("Status : Inactive\n");
    }

    printf("----------------------------------\n");
}


/* ==============================
   SEARCH STUDENT
   ============================== */

void searchStudent(void)
{
    int id;
    int index;

    printf("\n========== SEARCH STUDENT ==========\n");

    printf("Enter student ID: ");
    scanf("%d", &id);

    clearInputBuffer();

    index = findStudentIndexById(id);

    if (index == -1)
    {
        printf("\nStudent not found!\n");
        return;
    }

    printStudent(&students[index]);
}


/* ==============================
   FIND STUDENT INDEX
   ============================== */

int findStudentIndexById(int id)
{
    int i;

    for (i = 0; i < studentCount; i++)
    {
        if (students[i].id == id)
        {
            return i;
        }
    }

    return -1;
}


/* ==============================
   UPDATE STUDENT
   ============================== */

void updateStudent(void)
{
    int id;
    int index;

    printf("\n========== UPDATE STUDENT ==========\n");

    printf("Enter student ID: ");
    scanf("%d", &id);

    clearInputBuffer();

    index = findStudentIndexById(id);

    if (index == -1)
    {
        printf("\nStudent not found!\n");
        return;
    }

    printf("\nCurrent information:");
    printStudent(&students[index]);

    printf("\nEnter new name: ");
    fgets(
        students[index].name,
        sizeof(students[index].name),
        stdin
    );

    students[index].name[
        strcspn(students[index].name, "\n")
    ] = '\0';

    printf("Enter new age: ");
    scanf("%d", &students[index].age);

    printf("Enter new marks: ");
    scanf("%f", &students[index].marks);

    clearInputBuffer();

    saveToFile();

    printf("\nStudent updated successfully!\n");
}


/* ==============================
   DELETE STUDENT
   ============================== */

void deleteStudent(void)
{
    int id;
    int index;
    int i;
    char confirm;

    printf("\n========== DELETE STUDENT ==========\n");

    printf("Enter student ID: ");
    scanf("%d", &id);

    clearInputBuffer();

    index = findStudentIndexById(id);

    if (index == -1)
    {
        printf("\nStudent not found!\n");
        return;
    }

    printStudent(&students[index]);

    printf("\nAre you sure you want to delete? (y/n): ");
    scanf("%c", &confirm);

    clearInputBuffer();

    if (confirm != 'y' && confirm != 'Y')
    {
        printf("\nDelete cancelled.\n");
        return;
    }

    /*
       Shift all students after the deleted
       student one position to the left.
    */

    for (i = index; i < studentCount - 1; i++)
    {
        students[i] = students[i + 1];
    }

    studentCount--;

    saveToFile();

    printf("\nStudent deleted successfully!\n");
}


/* ==============================
   STATISTICS
   ============================== */

void showStatistics(void)
{
    int i;
    int highestIndex = 0;
    float total = 0;
    float average;

    if (studentCount == 0)
    {
        printf("\nNo students available.\n");
        return;
    }

    for (i = 0; i < studentCount; i++)
    {
        total += students[i].marks;

        if (students[i].marks >
            students[highestIndex].marks)
        {
            highestIndex = i;
        }
    }

    average = total / studentCount;

    printf("\n========== STATISTICS ==========\n");

    printf("Total Students : %d\n", studentCount);
    printf("Average Marks  : %.2f\n", average);

    printf("\nHighest Marks:\n");

    printStudent(&students[highestIndex]);
}


/* ==============================
   SAVE TO FILE
   ============================== */

void saveToFile(void)
{
    FILE *file;

    file = fopen(FILE_NAME, "wb");

    if (file == NULL)
    {
        printf("\nError: Could not open file for saving.\n");
        return;
    }

    fwrite(
        &studentCount,
        sizeof(studentCount),
        1,
        file
    );

    fwrite(
        students,
        sizeof(Student),
        studentCount,
        file
    );

    fclose(file);
}


/* ==============================
   LOAD FROM FILE
   ============================== */

void loadFromFile(void)
{
    FILE *file;

    file = fopen(FILE_NAME, "rb");

    if (file == NULL)
    {
        /*
           File does not exist yet.
           This is normal for first run.
        */
        return;
    }

    fread(
        &studentCount,
        sizeof(studentCount),
        1,
        file
    );

    if (studentCount < 0 ||
        studentCount > MAX_STUDENTS)
    {
        studentCount = 0;
        fclose(file);
        return;
    }

    fread(
        students,
        sizeof(Student),
        studentCount,
        file
    );

    fclose(file);
}


/* ==============================
   CLEAR INPUT BUFFER
   ============================== */

void clearInputBuffer(void)
{
    int c;

    while ((c = getchar()) != '\n' &&
           c != EOF)
    {
        /* discard */
    }
}


/* ==============================
   PAUSE SCREEN
   ============================== */

void pauseScreen(void)
{
    printf("\nPress Enter to continue...");
    getchar();
}
```

---

# 🧠 Projectটা কীভাবে কাজ করছে?

পুরো program-এর architecture:

```text
                 main()
                   │
                   ▼
             loadFromFile()
                   │
                   ▼
             ┌───────────┐
             │   MENU    │
             └───────────┘
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
     Add        Search       Update
       │           │           │
       └───────────┼───────────┘
                   ▼
             students[]
                   │
                   ▼
              saveToFile()
                   │
                   ▼
             students.dat
```

---

# 1. Student Structure

আমাদের মূল data model:

```c
typedef struct
{
    int id;
    char name[50];
    int age;
    float marks;
    StudentStatus status;
} Student;
```

প্রতিটি student-এর:

```text
ID
Name
Age
Marks
Status
```

থাকছে।

---

# 2. Status-এর জন্য `enum`

আমরা আগের lesson-এর `enum` ব্যবহার করেছি:

```c
typedef enum
{
    ACTIVE,
    INACTIVE
} StudentStatus;
```

তাই:

```c
s.status = ACTIVE;
```

লেখা যায়।

এর চেয়ে:

```c
s.status = 0;
```

অনেক কম readable।

---

# 3. Student Array

```c
Student students[MAX_STUDENTS];
```

আমরা সর্বোচ্চ:

```c
#define MAX_STUDENTS 100
```

জন student রাখতে পারি।

বর্তমানে কয়জন আছে সেটা:

```c
int studentCount = 0;
```

দিয়ে track করছি।

---

# 4. Add Student

যখন user:

```text
1. Add Student
```

select করে:

```c
addStudent();
```

call হয়।

তারপর:

```c
Student s;
```

একটি নতুন temporary student তৈরি করে।

Data নেওয়ার পর:

```c
students[studentCount] = s;
studentCount++;
```

দিয়ে array-তে রাখি।

---

# 5. কেন `&s.id`?

এটা:

```c
scanf("%d", &s.id);
```

কারণ `scanf()`-কে variable-এর **address** দিতে হয়।

আমরা Phase 6-এ pointer শিখেছিলাম:

```text
&s.id
  ↓
address
```

---

# 6. Name Input

আমরা ব্যবহার করেছি:

```c
fgets(s.name, sizeof(s.name), stdin);
```

এটা:

```c
scanf("%s", s.name);
```

এর চেয়ে ভালো কারণ `fgets()` space-সহ name নিতে পারে।

যেমন:

```text
Md Rahim Hasan
```

---

# 7. `strcspn()` কেন?

`fgets()` সাধারণত Enter চাপলে newline `\n`-ও string-এর মধ্যে রাখতে পারে।

তাই:

```c
s.name[strcspn(s.name, "\n")] = '\0';
```

newline সরিয়ে দেয়।

---

# 8. Search Algorithm

আমরা ID দিয়ে search করছি:

```c
for (i = 0; i < studentCount; i++)
{
    if (students[i].id == id)
    {
        return i;
    }
}
```

যদি পাওয়া যায়:

```text
index
```

return করবে।

না পাওয়া গেলে:

```c
return -1;
```

---

# 9. Update

Update-এর জন্য প্রথমে student খুঁজি:

```c
index = findStudentIndexById(id);
```

তারপর:

```c
students[index].name
students[index].age
students[index].marks
```

update করি।

---

# 10. Delete 🔥

এখানে একটা গুরুত্বপূর্ণ array concept আছে।

ধরো:

```text
Index:   0      1      2      3
         ↓      ↓      ↓      ↓
ID:     101    102    103    104
```

আমরা `102` delete করলাম।

তখন:

```text
101    103    104
```

করতে হবে।

তাই:

```c
for (i = index; i < studentCount - 1; i++)
{
    students[i] = students[i + 1];
}
```

প্রতিটি পরের element এক ঘর বামে চলে আসে।

তারপর:

```c
studentCount--;
```

---

# 11. Statistics

আমরা total marks:

```c
total += students[i].marks;
```

এবং average:

```c
average = total / studentCount;
```

calculate করছি।

Highest marks:

```c
if (students[i].marks >
    students[highestIndex].marks)
{
    highestIndex = i;
}
```

---

# 12. File Handling 🔥

এই project-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

আমরা:

```c
#define FILE_NAME "students.dat"
```

ব্যবহার করছি।

Program বন্ধ হয়ে গেলেও data থাকবে।

---

## Save

```c
file = fopen(FILE_NAME, "wb");
```

`wb` = **write binary**

তারপর:

```c
fwrite(...)
```

দিয়ে data save করি।

শেষে:

```c
fclose(file);
```

---

## Load

Program শুরু হলে:

```c
loadFromFile();
```

তার মধ্যে:

```c
file = fopen(FILE_NAME, "rb");
```

`rb` = **read binary**

তারপর:

```c
fread(...)
```

দিয়ে saved data আবার memory-তে আনি।

---

# 13. Program প্রথমবার চালালে

প্রথমবার:

```text
students.dat
```

নাও থাকতে পারে।

তখন:

```c
file = fopen(FILE_NAME, "rb");
```

fail করবে।

আমরা simply:

```c
if (file == NULL)
{
    return;
}
```

করেছি।

এটা error নয়—প্রথম run-এ file না থাকাটাই স্বাভাবিক।

---

# 14. Program চালানোর Example

প্রথমে:

```text
========================================
       STUDENT MANAGEMENT SYSTEM
========================================
1. Add Student
2. Display All Students
3. Search Student
4. Update Student
5. Delete Student
6. Statistics
7. Save & Exit
========================================
Enter your choice: 1
```

তারপর:

```text
========== ADD STUDENT ==========

Enter ID: 101
Enter name: Rahim Hasan
Enter age: 18
Enter marks: 87.5

Student added successfully!
```

আবার menu:

```text
Enter your choice: 1
```

আরেকজন:

```text
Enter ID: 102
Enter name: Karim
Enter age: 19
Enter marks: 92
```

---

# 15. Display

`2` দিলে:

```text
========== ALL STUDENTS ==========

----------------------------------
ID     : 101
Name   : Rahim Hasan
Age    : 18
Marks  : 87.50
Status : Active
----------------------------------

----------------------------------
ID     : 102
Name   : Karim
Age    : 19
Marks  : 92.00
Status : Active
----------------------------------
```

---

# 16. Search

```text
Enter your choice: 3

========== SEARCH STUDENT ==========

Enter student ID: 102
```

Output:

```text
----------------------------------
ID     : 102
Name   : Karim
Age    : 19
Marks  : 92.00
Status : Active
----------------------------------
```

---

# 17. Statistics

```text
Enter your choice: 6
```

Output:

```text
========== STATISTICS ==========

Total Students : 2
Average Marks  : 89.75

Highest Marks:

----------------------------------
ID     : 102
Name   : Karim
Age    : 19
Marks  : 92.00
Status : Active
----------------------------------
```

---

# 18. Compile & Run

যদি GCC থাকে:

### Linux / macOS

```bash
gcc main.c -o student
```

তারপর:

```bash
./student
```

### Windows

```bash
gcc main.c -o student.exe
```

তারপর:

```bash
student.exe
```

যদি compiler warning দেখতে চাও:

```bash
gcc -Wall -Wextra -pedantic main.c -o student
```

এটা ব্যবহার করার অভ্যাস করা ভালো।

---

# 🧩 এই Project-এ কোন কোন C Concept ব্যবহার হলো?

|Concept|Project-এ কোথায়|
|---|---|
|Variables|`studentCount`, `choice`|
|Data types|`int`, `float`, `char`|
|`if/else`|search/delete/status|
|`switch`|main menu|
|`for`|array traversal|
|Functions|পুরো project|
|Arrays|`students[]`|
|Strings|`name[]`|
|`struct`|`Student`|
|`typedef`|`Student`, `StudentStatus`|
|`enum`|`ACTIVE`, `INACTIVE`|
|Pointers|`Student *`|
|`->`|`s->id`|
|File handling|`fopen`, `fread`, `fwrite`, `fclose`|
|Binary file|`students.dat`|

---

# 🔥 তোমার Project Roadmap

এখন এই project-টা **একবার copy করে শুধু run করলেই শেষ না**। শেখার জন্য এটাকে ধাপে ধাপে নিজে rebuild করো:

### Level 1

শুধু:

```text
Add
Display
Exit
```

### Level 2

যোগ করো:

```text
Search
```

### Level 3

যোগ করো:

```text
Update
Delete
```

### Level 4

যোগ করো:

```text
Statistics
```

### Level 5

যোগ করো:

```text
Save
Load
```

### Level 6 🔥

নিজে add করো:

```text
Sort by marks
Sort by name
Find lowest marks
Count passed students
Count failed students
```

### Level 7 🔥🔥

আরও professional করো:

```text
Login
Admin/User roles
Input validation
Separate header files
Separate source files
```

---

## 🎯 Next Step

তোমার **Phase 8 File Handling**-এ এখন আমরা এই project-এর file অংশটা আরও গভীরভাবে শিখব।

পরের lesson:

**Lesson 53 — File Concept**

সেখানে `students.dat`-এর মতো file কেন দরকার, RAM বনাম storage, text file বনাম binary file, এবং `FILE *` আসলে কী—এসব একদম zero থেকে বুঝব।

---
# 🏦 Bank Management System — Complete C Project

চলো এবার একটি **complete menu-driven Bank Management System** বানাই। এটি beginner-to-intermediate level project এবং তোমার শেখা C concepts একসাথে ব্যবহার করবে।

### Features

- ➕ Create account
    
- 📋 Display all accounts
    
- 🔍 Search account
    
- 💰 Deposit
    
- 💸 Withdraw
    
- 🔄 Transfer money
    
- ✏️ Update account
    
- 🗑️ Delete account
    
- 📊 Bank statistics
    
- 💾 Save data to file
    
- 📂 Load data when program starts
    
- 🚪 Exit
    

> **Note:** এটি শেখার জন্য simulation project। Real banking/security system হিসেবে ব্যবহার করার জন্য নয়।

---

# 📁 Project Structure

শুরুতে একটি file:

```text
BankManagement/
└── main.c
```

---

# 1. Complete `main.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ACCOUNTS 100
#define FILE_NAME "accounts.dat"


/* =====================================
   ENUM
   ===================================== */

typedef enum
{
    ACTIVE,
    BLOCKED,
    CLOSED
} AccountStatus;


/* =====================================
   STRUCT
   ===================================== */

typedef struct
{
    int accountNumber;
    char name[50];
    int age;
    char phone[20];
    float balance;
    AccountStatus status;
} Account;


/* =====================================
   GLOBAL DATA
   ===================================== */

Account accounts[MAX_ACCOUNTS];
int accountCount = 0;


/* =====================================
   FUNCTION DECLARATIONS
   ===================================== */

void printMenu(void);

void createAccount(void);
void displayAllAccounts(void);
void searchAccount(void);
void depositMoney(void);
void withdrawMoney(void);
void transferMoney(void);
void updateAccount(void);
void deleteAccount(void);
void showStatistics(void);

void saveToFile(void);
void loadFromFile(void);

int findAccountIndex(int accountNumber);

void printAccount(const Account *account);

void clearInputBuffer(void);
void pauseScreen(void);


/* =====================================
   MAIN
   ===================================== */

int main(void)
{
    int choice;

    loadFromFile();

    while (1)
    {
        printMenu();

        printf("Enter your choice: ");
        scanf("%d", &choice);

        clearInputBuffer();

        switch (choice)
        {
            case 1:
                createAccount();
                break;

            case 2:
                displayAllAccounts();
                break;

            case 3:
                searchAccount();
                break;

            case 4:
                depositMoney();
                break;

            case 5:
                withdrawMoney();
                break;

            case 6:
                transferMoney();
                break;

            case 7:
                updateAccount();
                break;

            case 8:
                deleteAccount();
                break;

            case 9:
                showStatistics();
                break;

            case 10:
                saveToFile();

                printf("\nData saved successfully.\n");
                printf("Thank you for using the Bank Management System.\n");

                return 0;

            default:
                printf("\nInvalid choice!\n");
        }

        pauseScreen();
    }

    return 0;
}


/* =====================================
   MENU
   ===================================== */

void printMenu(void)
{
    printf("\n");
    printf("============================================\n");
    printf("         BANK MANAGEMENT SYSTEM             \n");
    printf("============================================\n");

    printf("1.  Create Account\n");
    printf("2.  Display All Accounts\n");
    printf("3.  Search Account\n");
    printf("4.  Deposit Money\n");
    printf("5.  Withdraw Money\n");
    printf("6.  Transfer Money\n");
    printf("7.  Update Account\n");
    printf("8.  Delete Account\n");
    printf("9.  Bank Statistics\n");
    printf("10. Save & Exit\n");

    printf("============================================\n");
}


/* =====================================
   CREATE ACCOUNT
   ===================================== */

void createAccount(void)
{
    Account account;

    if (accountCount >= MAX_ACCOUNTS)
    {
        printf("\nBank account storage is full!\n");
        return;
    }

    printf("\n========== CREATE ACCOUNT ==========\n");

    printf("Enter account number: ");
    scanf("%d", &account.accountNumber);

    clearInputBuffer();

    if (findAccountIndex(account.accountNumber) != -1)
    {
        printf("\nAccount number already exists!\n");
        return;
    }

    printf("Enter account holder name: ");
    fgets(account.name, sizeof(account.name), stdin);

    account.name[strcspn(account.name, "\n")] = '\0';


    printf("Enter age: ");
    scanf("%d", &account.age);

    clearInputBuffer();


    printf("Enter phone number: ");
    fgets(account.phone, sizeof(account.phone), stdin);

    account.phone[strcspn(account.phone, "\n")] = '\0';


    printf("Enter initial deposit: ");
    scanf("%f", &account.balance);

    clearInputBuffer();


    if (account.balance < 0)
    {
        printf("\nInitial deposit cannot be negative.\n");
        return;
    }


    account.status = ACTIVE;

    accounts[accountCount] = account;

    accountCount++;

    saveToFile();

    printf("\nAccount created successfully!\n");
}


/* =====================================
   DISPLAY ALL ACCOUNTS
   ===================================== */

void displayAllAccounts(void)
{
    int i;

    if (accountCount == 0)
    {
        printf("\nNo accounts found.\n");
        return;
    }

    printf("\n========== ALL ACCOUNTS ==========\n");

    for (i = 0; i < accountCount; i++)
    {
        printAccount(&accounts[i]);
    }
}


/* =====================================
   PRINT ONE ACCOUNT
   ===================================== */

void printAccount(const Account *account)
{
    printf("\n--------------------------------------------\n");

    printf("Account Number : %d\n",
           account->accountNumber);

    printf("Name           : %s\n",
           account->name);

    printf("Age            : %d\n",
           account->age);

    printf("Phone          : %s\n",
           account->phone);

    printf("Balance        : %.2f\n",
           account->balance);


    printf("Status         : ");

    switch (account->status)
    {
        case ACTIVE:
            printf("Active\n");
            break;

        case BLOCKED:
            printf("Blocked\n");
            break;

        case CLOSED:
            printf("Closed\n");
            break;

        default:
            printf("Unknown\n");
    }

    printf("--------------------------------------------\n");
}


/* =====================================
   SEARCH ACCOUNT
   ===================================== */

void searchAccount(void)
{
    int accountNumber;
    int index;

    printf("\n========== SEARCH ACCOUNT ==========\n");

    printf("Enter account number: ");
    scanf("%d", &accountNumber);

    clearInputBuffer();

    index = findAccountIndex(accountNumber);

    if (index == -1)
    {
        printf("\nAccount not found!\n");
        return;
    }

    printAccount(&accounts[index]);
}


/* =====================================
   FIND ACCOUNT
   ===================================== */

int findAccountIndex(int accountNumber)
{
    int i;

    for (i = 0; i < accountCount; i++)
    {
        if (accounts[i].accountNumber == accountNumber)
        {
            return i;
        }
    }

    return -1;
}


/* =====================================
   DEPOSIT
   ===================================== */

void depositMoney(void)
{
    int accountNumber;
    int index;
    float amount;

    printf("\n========== DEPOSIT MONEY ==========\n");

    printf("Enter account number: ");
    scanf("%d", &accountNumber);

    clearInputBuffer();

    index = findAccountIndex(accountNumber);

    if (index == -1)
    {
        printf("\nAccount not found!\n");
        return;
    }


    if (accounts[index].status != ACTIVE)
    {
        printf("\nThis account is not active.\n");
        return;
    }


    printf("Enter deposit amount: ");
    scanf("%f", &amount);

    clearInputBuffer();


    if (amount <= 0)
    {
        printf("\nInvalid deposit amount.\n");
        return;
    }


    accounts[index].balance += amount;

    saveToFile();

    printf("\nDeposit successful!\n");
    printf("New balance: %.2f\n",
           accounts[index].balance);
}


/* =====================================
   WITHDRAW
   ===================================== */

void withdrawMoney(void)
{
    int accountNumber;
    int index;
    float amount;

    printf("\n========== WITHDRAW MONEY ==========\n");

    printf("Enter account number: ");
    scanf("%d", &accountNumber);

    clearInputBuffer();

    index = findAccountIndex(accountNumber);

    if (index == -1)
    {
        printf("\nAccount not found!\n");
        return;
    }


    if (accounts[index].status != ACTIVE)
    {
        printf("\nThis account is not active.\n");
        return;
    }


    printf("Enter withdrawal amount: ");
    scanf("%f", &amount);

    clearInputBuffer();


    if (amount <= 0)
    {
        printf("\nInvalid withdrawal amount.\n");
        return;
    }


    if (amount > accounts[index].balance)
    {
        printf("\nInsufficient balance!\n");
        return;
    }


    accounts[index].balance -= amount;

    saveToFile();

    printf("\nWithdrawal successful!\n");
    printf("New balance: %.2f\n",
           accounts[index].balance);
}


/* =====================================
   TRANSFER MONEY
   ===================================== */

void transferMoney(void)
{
    int fromAccount;
    int toAccount;

    int fromIndex;
    int toIndex;

    float amount;

    printf("\n========== TRANSFER MONEY ==========\n");


    printf("Enter sender account number: ");
    scanf("%d", &fromAccount);

    clearInputBuffer();


    printf("Enter receiver account number: ");
    scanf("%d", &toAccount);

    clearInputBuffer();


    if (fromAccount == toAccount)
    {
        printf("\nSender and receiver cannot be the same.\n");
        return;
    }


    fromIndex = findAccountIndex(fromAccount);
    toIndex = findAccountIndex(toAccount);


    if (fromIndex == -1)
    {
        printf("\nSender account not found!\n");
        return;
    }


    if (toIndex == -1)
    {
        printf("\nReceiver account not found!\n");
        return;
    }


    if (accounts[fromIndex].status != ACTIVE)
    {
        printf("\nSender account is not active.\n");
        return;
    }


    if (accounts[toIndex].status != ACTIVE)
    {
        printf("\nReceiver account is not active.\n");
        return;
    }


    printf("Enter transfer amount: ");
    scanf("%f", &amount);

    clearInputBuffer();


    if (amount <= 0)
    {
        printf("\nInvalid transfer amount.\n");
        return;
    }


    if (amount > accounts[fromIndex].balance)
    {
        printf("\nInsufficient balance!\n");
        return;
    }


    accounts[fromIndex].balance -= amount;

    accounts[toIndex].balance += amount;


    saveToFile();


    printf("\nTransfer successful!\n");

    printf("Sender new balance: %.2f\n",
           accounts[fromIndex].balance);
}


/* =====================================
   UPDATE ACCOUNT
   ===================================== */

void updateAccount(void)
{
    int accountNumber;
    int index;

    printf("\n========== UPDATE ACCOUNT ==========\n");

    printf("Enter account number: ");
    scanf("%d", &accountNumber);

    clearInputBuffer();


    index = findAccountIndex(accountNumber);


    if (index == -1)
    {
        printf("\nAccount not found!\n");
        return;
    }


    printf("\nCurrent account information:");

    printAccount(&accounts[index]);


    printf("\nEnter new name: ");

    fgets(
        accounts[index].name,
        sizeof(accounts[index].name),
        stdin
    );

    accounts[index].name[
        strcspn(accounts[index].name, "\n")
    ] = '\0';


    printf("Enter new age: ");
    scanf("%d", &accounts[index].age);

    clearInputBuffer();


    printf("Enter new phone number: ");

    fgets(
        accounts[index].phone,
        sizeof(accounts[index].phone),
        stdin
    );

    accounts[index].phone[
        strcspn(accounts[index].phone, "\n")
    ] = '\0';


    saveToFile();

    printf("\nAccount updated successfully!\n");
}


/* =====================================
   DELETE ACCOUNT
   ===================================== */

void deleteAccount(void)
{
    int accountNumber;
    int index;
    int i;

    char confirm;

    printf("\n========== DELETE ACCOUNT ==========\n");

    printf("Enter account number: ");
    scanf("%d", &accountNumber);

    clearInputBuffer();


    index = findAccountIndex(accountNumber);


    if (index == -1)
    {
        printf("\nAccount not found!\n");
        return;
    }


    printAccount(&accounts[index]);


    /*
       Do not delete an account that
       still has money.
    */

    if (accounts[index].balance > 0)
    {
        printf("\nCannot delete an account with positive balance.\n");
        printf("Withdraw or transfer the remaining balance first.\n");

        return;
    }


    printf("\nAre you sure? (y/n): ");
    scanf("%c", &confirm);

    clearInputBuffer();


    if (confirm != 'y' && confirm != 'Y')
    {
        printf("\nDelete cancelled.\n");
        return;
    }


    for (i = index; i < accountCount - 1; i++)
    {
        accounts[i] = accounts[i + 1];
    }


    accountCount--;

    saveToFile();

    printf("\nAccount deleted successfully!\n");
}


/* =====================================
   BANK STATISTICS
   ===================================== */

void showStatistics(void)
{
    int i;

    int activeAccounts = 0;
    int blockedAccounts = 0;
    int closedAccounts = 0;

    float totalBalance = 0;
    float highestBalance = 0;

    int highestIndex = -1;


    if (accountCount == 0)
    {
        printf("\nNo accounts available.\n");
        return;
    }


    for (i = 0; i < accountCount; i++)
    {
        totalBalance += accounts[i].balance;


        switch (accounts[i].status)
        {
            case ACTIVE:
                activeAccounts++;
                break;

            case BLOCKED:
                blockedAccounts++;
                break;

            case CLOSED:
                closedAccounts++;
                break;
        }


        if (highestIndex == -1 ||
            accounts[i].balance > highestBalance)
        {
            highestBalance = accounts[i].balance;
            highestIndex = i;
        }
    }


    printf("\n========== BANK STATISTICS ==========\n");

    printf("Total Accounts   : %d\n",
           accountCount);

    printf("Active Accounts  : %d\n",
           activeAccounts);

    printf("Blocked Accounts : %d\n",
           blockedAccounts);

    printf("Closed Accounts  : %d\n",
           closedAccounts);

    printf("Total Balance    : %.2f\n",
           totalBalance);


    if (highestIndex != -1)
    {
        printf("\nHighest Balance Account:\n");

        printAccount(&accounts[highestIndex]);
    }
}


/* =====================================
   SAVE DATA
   ===================================== */

void saveToFile(void)
{
    FILE *file;


    file = fopen(FILE_NAME, "wb");


    if (file == NULL)
    {
        printf("\nError: Could not open file.\n");
        return;
    }


    fwrite(
        &accountCount,
        sizeof(accountCount),
        1,
        file
    );


    fwrite(
        accounts,
        sizeof(Account),
        accountCount,
        file
    );


    fclose(file);
}


/* =====================================
   LOAD DATA
   ===================================== */

void loadFromFile(void)
{
    FILE *file;


    file = fopen(FILE_NAME, "rb");


    if (file == NULL)
    {
        /*
           File does not exist on first run.
        */

        return;
    }


    fread(
        &accountCount,
        sizeof(accountCount),
        1,
        file
    );


    if (accountCount < 0 ||
        accountCount > MAX_ACCOUNTS)
    {
        accountCount = 0;

        fclose(file);

        return;
    }


    fread(
        accounts,
        sizeof(Account),
        accountCount,
        file
    );


    fclose(file);
}


/* =====================================
   CLEAR INPUT BUFFER
   ===================================== */

void clearInputBuffer(void)
{
    int c;

    while ((c = getchar()) != '\n' &&
           c != EOF)
    {
        /* discard input */
    }
}


/* =====================================
   PAUSE
   ===================================== */

void pauseScreen(void)
{
    printf("\nPress Enter to continue...");

    getchar();
}
```

---

# 🧠 Project Architecture

এই project-টাকে এভাবে ভাবো:

```text
                    main()
                      │
                      ▼
                loadFromFile()
                      │
                      ▼
                ┌──────────┐
                │   MENU   │
                └──────────┘
                      │
       ┌──────┬───────┼───────┬──────┐
       ▼      ▼       ▼       ▼      ▼
     Create Search  Deposit Withdraw Transfer
       │      │       │       │      │
       └──────┴───────┴───────┴──────┘
                      │
                      ▼
                  accounts[]
                      │
                      ▼
                saveToFile()
                      │
                      ▼
                accounts.dat
```

---

# 🏦 Account Structure

আমাদের মূল data type:

```c
typedef struct
{
    int accountNumber;
    char name[50];
    int age;
    char phone[20];
    float balance;
    AccountStatus status;
} Account;
```

প্রতিটি account-এর মধ্যে আছে:

```text
Account
├── accountNumber
├── name
├── age
├── phone
├── balance
└── status
```

---

# 🔥 `enum` দিয়ে Account Status

```c
typedef enum
{
    ACTIVE,
    BLOCKED,
    CLOSED
} AccountStatus;
```

তাই:

```c
account.status = ACTIVE;
```

এর মতো readable code লিখতে পারি।

---

# 💰 Deposit

মূল logic:

```c
accounts[index].balance += amount;
```

ধরো:

```text
Balance = 5000
Deposit = 2000
```

তাহলে:

```text
5000 + 2000 = 7000
```

---

# 💸 Withdraw

মূল logic:

```c
if (amount > accounts[index].balance)
{
    printf("Insufficient balance!");
    return;
}
```

তারপর:

```c
accounts[index].balance -= amount;
```

ধরো:

```text
Balance = 5000
Withdraw = 1500
```

তাহলে:

```text
5000 - 1500 = 3500
```

---

# 🔄 Transfer Money

Transfer-এর সবচেয়ে গুরুত্বপূর্ণ অংশ:

```c
accounts[fromIndex].balance -= amount;
accounts[toIndex].balance += amount;
```

ধরো:

```text
Account A = 10,000
Account B = 5,000

Transfer = 2,000
```

Result:

```text
A = 8,000
B = 7,000
```

এখানে আমরা দুটো account একসাথে modify করছি।

---

# 🗑️ Delete Logic

আমাদের design-এ একটা useful rule আছে:

> Balance positive থাকলে account delete করা যাবে না।

```c
if (accounts[index].balance > 0)
{
    printf("Cannot delete...");
    return;
}
```

তাই আগে balance zero করতে হবে।

তারপর array shift:

```c
for (i = index; i < accountCount - 1; i++)
{
    accounts[i] = accounts[i + 1];
}
```

---

# 📊 Statistics

Program calculate করবে:

```text
Total Accounts
Active Accounts
Blocked Accounts
Closed Accounts
Total Balance
Highest Balance Account
```

মূল calculation:

```c
totalBalance += accounts[i].balance;
```

---

# 💾 File Persistence

Program বন্ধ করলেও data হারাবে না।

Save:

```c
fopen("accounts.dat", "wb");
```

Load:

```c
fopen("accounts.dat", "rb");
```

Save:

```c
fwrite(...)
```

Load:

```c
fread(...)
```

ফলে:

```text
Program Run
    ↓
accounts.dat read
    ↓
RAM
    ↓
User operations
    ↓
accounts.dat updated
```

---

# ▶️ Compile

GCC ব্যবহার করলে:

### Linux / macOS

```bash
gcc -Wall -Wextra -pedantic main.c -o bank
```

Run:

```bash
./bank
```

### Windows

```bash
gcc -Wall -Wextra -pedantic main.c -o bank.exe
```

Run:

```bash
bank.exe
```

---

# 🖥️ Example Run

Program শুরু:

```text
============================================
         BANK MANAGEMENT SYSTEM
============================================
1.  Create Account
2.  Display All Accounts
3.  Search Account
4.  Deposit Money
5.  Withdraw Money
6.  Transfer Money
7.  Update Account
8.  Delete Account
9.  Bank Statistics
10. Save & Exit
============================================

Enter your choice:
```

### Create

```text
Enter your choice: 1

========== CREATE ACCOUNT ==========

Enter account number: 1001
Enter account holder name: Rahim Hasan
Enter age: 20
Enter phone number: 01700000000
Enter initial deposit: 5000

Account created successfully!
```

### Deposit

```text
Enter your choice: 4

========== DEPOSIT MONEY ==========

Enter account number: 1001
Enter deposit amount: 2500

Deposit successful!
New balance: 7500.00
```

### Withdraw

```text
Enter your choice: 5

========== WITHDRAW MONEY ==========

Enter account number: 1001
Enter withdrawal amount: 1000

Withdrawal successful!
New balance: 6500.00
```

---

# 🔄 Transfer Example

ধরো:

```text
1001 → 6500
1002 → 3000
```

Transfer:

```text
1001 → 1002
Amount = 2000
```

Result:

```text
1001 → 4500
1002 → 5000
```

---

# 🧠 এই Project-এ তুমি কী কী শিখলে?

|C Concept|ব্যবহার|
|---|---|
|Variables|`choice`, `amount`|
|Constants|`MAX_ACCOUNTS`|
|`if/else`|validation|
|`switch`|menu/status|
|`for`|searching/deleting/statistics|
|Functions|পুরো project|
|Array|`accounts[]`|
|String|name/phone|
|`struct`|`Account`|
|`typedef`|custom types|
|`enum`|account status|
|Pointer|`Account *`|
|`->`|pointer member access|
|File|`accounts.dat`|
|`fopen()`|file open|
|`fread()`|file read|
|`fwrite()`|file write|
|`fclose()`|file close|

---

# 🚀 এবার Project-টা আরও Professional করো

বর্তমান version ভালো learning project। কিন্তু তুমি যদি এটাকে **advanced C project** বানাতে চাও, পরের version-এ এগুলো যোগ করো:

### Level 1

```text
✅ Create
✅ Search
✅ Deposit
✅ Withdraw
✅ Transfer
```

### Level 2

```text
🔲 Transaction history
🔲 Sort accounts
🔲 Search by name
🔲 Minimum/maximum balance
```

### Level 3

```text
🔲 Admin login
🔲 Account PIN
🔲 Login attempts
🔲 Change PIN
```

### Level 4

```text
🔲 Separate .h files
🔲 Separate .c files
🔲 Dynamic memory
🔲 Linked list
```

### Level 5 🔥

```text
🔲 Transaction structure
🔲 Transaction history file
🔲 Multiple account types
🔲 Interest calculation
🔲 Monthly statement
```

---

# ⚠️ একটি গুরুত্বপূর্ণ বাস্তব-world বিষয়

এই educational project-এ balance `float` হিসেবে রাখা হয়েছে:

```c
float balance;
```

Real financial software-এ floating-point money calculations সরাসরি ব্যবহার করা সাধারণত ভালো design নয়। শেখার project-এ `float` দিয়ে concept বোঝা সহজ; production financial software-এ নির্ভুল monetary representation এবং আরও শক্তিশালী security/validation architecture দরকার।

---

# 🎯 তোমার পরবর্তী Upgrade

এই project-এর **Version 2** বানানোর সবচেয়ে ভালো ধাপ হবে:

```text
Bank Management System V2
│
├── Account
│   ├── Account Number
│   ├── Name
│   ├── Phone
│   ├── Balance
│   └── Status
│
├── Transaction
│   ├── Transaction ID
│   ├── Account Number
│   ├── Type
│   ├── Amount
│   └── Date
│
├── Account File
│
└── Transaction File
```

এতে **deposit, withdraw এবং transfer-এর history** রাখা যাবে—এবং তোমার `struct + enum + array + pointer + file handling` আরও গভীরভাবে practice হবে।


----
# 📝 Quiz Application — Complete C Project

চলো এবার একটি **complete Quiz Application in C** বানাই। এতে থাকবে:

- 👤 Player name
    
- ❓ Multiple-choice questions
    
- ✅ Answer checking
    
- 📊 Score calculation
    
- 🎯 Percentage
    
- 🏆 Grade/result
    
- 🔄 Replay option
    
- 💾 Result file-এ save
    

---

## 📁 Project Structure

```text
QuizApplication/
└── main.c
```

## `main.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define TOTAL_QUESTIONS 10
#define OPTION_COUNT 4
#define NAME_SIZE 50
#define FILE_NAME "quiz_results.txt"


/* =====================================
   QUESTION STRUCTURE
   ===================================== */

typedef struct
{
    char question[200];

    char options[OPTION_COUNT][100];

    int correctAnswer;

} Question;


/* =====================================
   FUNCTION DECLARATIONS
   ===================================== */

void showWelcome(void);

void askQuestions(
    Question questions[],
    int total,
    int *score
);

void showResult(
    const char name[],
    int score,
    int total
);

void saveResult(
    const char name[],
    int score,
    int total
);

void clearInputBuffer(void);

void pauseScreen(void);


/* =====================================
   MAIN
   ===================================== */

int main(void)
{
    char playerName[NAME_SIZE];

    int score;

    char playAgain;


    /*
       Quiz questions
    */

    Question questions[TOTAL_QUESTIONS] =
    {
        {
            "Which language is known as a system programming language?",

            {
                "Python",
                "C",
                "HTML",
                "SQL"
            },

            2
        },

        {
            "Which symbol is used to end a C statement?",

            {
                ".",
                ":",
                ";",
                ","
            },

            3
        },

        {
            "Which function is used to print output in C?",

            {
                "scanf()",
                "printf()",
                "print()",
                "output()"
            },

            2
        },

        {
            "Which header file is required for printf()?",

            {
                "stdlib.h",
                "string.h",
                "stdio.h",
                "math.h"
            },

            3
        },

        {
            "Which operator is used to get the address of a variable?",

            {
                "*",
                "&",
                "#",
                "@"
            },

            2
        },

        {
            "Which loop executes its body at least once?",

            {
                "for",
                "while",
                "do-while",
                "nested loop"
            },

            3
        },

        {
            "Which data type is commonly used for decimal values?",

            {
                "int",
                "char",
                "float",
                "void"
            },

            3
        },

        {
            "Which keyword is used to define a structure?",

            {
                "structure",
                "struct",
                "record",
                "object"
            },

            2
        },

        {
            "Which function is used to open a file?",

            {
                "open()",
                "file()",
                "fopen()",
                "openFile()"
            },

            3
        },

        {
            "Which keyword is used to return a value from a function?",

            {
                "send",
                "return",
                "back",
                "value"
            },

            2
        }
    };


    do
    {
        score = 0;


        showWelcome();


        printf("Enter your name: ");

        fgets(
            playerName,
            sizeof(playerName),
            stdin
        );


        playerName[
            strcspn(playerName, "\n")
        ] = '\0';


        printf("\nGood luck, %s!\n",
               playerName);


        pauseScreen();


        /*
           Start quiz
        */

        askQuestions(
            questions,
            TOTAL_QUESTIONS,
            &score
        );


        /*
           Show final result
        */

        showResult(
            playerName,
            score,
            TOTAL_QUESTIONS
        );


        /*
           Save result
        */

        saveResult(
            playerName,
            score,
            TOTAL_QUESTIONS
        );


        /*
           Replay
        */

        printf("\nDo you want to play again? (y/n): ");

        scanf("%c", &playAgain);

        clearInputBuffer();


    } while (
        playAgain == 'y' ||
        playAgain == 'Y'
    );


    printf("\nThank you for playing!\n");

    return 0;
}


/* =====================================
   WELCOME SCREEN
   ===================================== */

void showWelcome(void)
{
    printf("\n");
    printf("============================================\n");
    printf("             C QUIZ APPLICATION             \n");
    printf("============================================\n");

    printf("Answer the following multiple-choice\n");
    printf("questions and test your C programming\n");
    printf("knowledge.\n");

    printf("============================================\n");
}


/* =====================================
   ASK QUESTIONS
   ===================================== */

void askQuestions(
    Question questions[],
    int total,
    int *score
)
{
    int i;

    int answer;


    for (i = 0; i < total; i++)
    {
        printf("\n");
        printf("--------------------------------------------\n");

        printf("Question %d of %d\n",
               i + 1,
               total);

        printf("--------------------------------------------\n");


        printf("%s\n\n",
               questions[i].question);


        /*
           Display options
        */

        for (int j = 0; j < OPTION_COUNT; j++)
        {
            printf(
                "%d. %s\n",
                j + 1,
                questions[i].options[j]
            );
        }


        /*
           Get answer
        */

        printf("\nYour answer (1-4): ");

        scanf("%d", &answer);

        clearInputBuffer();


        /*
           Validate answer
        */

        if (answer < 1 || answer > 4)
        {
            printf("Invalid answer!");

            continue;
        }


        /*
           Check answer
        */

        if (answer == questions[i].correctAnswer)
        {
            printf("\nCorrect! +1 point\n");

            (*score)++;
        }
        else
        {
            printf("\nWrong answer.\n");

            printf(
                "Correct answer: %d. %s\n",
                questions[i].correctAnswer,
                questions[i]
                    .options[
                        questions[i].correctAnswer - 1
                    ]
            );
        }


        printf(
            "Current score: %d/%d\n",
            *score,
            i + 1
        );
    }
}


/* =====================================
   SHOW RESULT
   ===================================== */

void showResult(
    const char name[],
    int score,
    int total
)
{
    float percentage;

    percentage =
        ((float)score / total) * 100;


    printf("\n");
    printf("============================================\n");
    printf("                 QUIZ RESULT                \n");
    printf("============================================\n");


    printf("Player     : %s\n",
           name);

    printf("Score      : %d/%d\n",
           score,
           total);

    printf("Percentage : %.2f%%\n",
           percentage);


    printf("\nGrade      : ");


    if (percentage >= 80)
    {
        printf("A\n");
        printf("Excellent performance!\n");
    }
    else if (percentage >= 60)
    {
        printf("B\n");
        printf("Good job!\n");
    }
    else if (percentage >= 40)
    {
        printf("C\n");
        printf("Keep practicing!\n");
    }
    else
    {
        printf("F\n");
        printf("Keep learning and try again!\n");
    }


    printf("============================================\n");
}


/* =====================================
   SAVE RESULT
   ===================================== */

void saveResult(
    const char name[],
    int score,
    int total
)
{
    FILE *file;

    float percentage;


    file = fopen(
        FILE_NAME,
        "a"
    );


    if (file == NULL)
    {
        printf(
            "\nCould not save result.\n"
        );

        return;
    }


    percentage =
        ((float)score / total) * 100;


    fprintf(
        file,
        "Player: %s | Score: %d/%d | Percentage: %.2f%%\n",
        name,
        score,
        total,
        percentage
    );


    fclose(file);


    printf("\nResult saved successfully.\n");
}


/* =====================================
   CLEAR INPUT BUFFER
   ===================================== */

void clearInputBuffer(void)
{
    int c;


    while (
        (c = getchar()) != '\n' &&
        c != EOF
    )
    {
        /* discard */
    }
}


/* =====================================
   PAUSE
   ===================================== */

void pauseScreen(void)
{
    printf("\nPress Enter to start the quiz...");

    getchar();
}
```

---

# 🧠 Project-এর মূল ধারণা

আমাদের question-এর জন্য:

```c
typedef struct
{
    char question[200];

    char options[4][100];

    int correctAnswer;

} Question;
```

একটি question-এর মধ্যে থাকে:

```text
Question
├── question
├── option 1
├── option 2
├── option 3
├── option 4
└── correct answer
```

---

# ❓ Question তৈরি

যেমন:

```c
{
    "Which function is used to print output in C?",

    {
        "scanf()",
        "printf()",
        "print()",
        "output()"
    },

    2
}
```

এখানে:

```text
Question:
Which function is used to print output in C?

1. scanf()
2. printf()
3. print()
4. output()

Correct answer = 2
```

---

# 🎯 Score Calculation

প্রতিবার correct answer হলে:

```c
(*score)++;
```

ধরো 10টি question-এর মধ্যে 8টি correct:

```text
Score = 8/10
```

Percentage:

```c
percentage = ((float)score / total) * 100;
```

Result:

```text
Score      : 8/10
Percentage : 80.00%
Grade      : A
```

---

# 🏆 Grading System

```text
80% - 100% → A
60% - 79%  → B
40% - 59%  → C
Below 40%  → F
```

এখানে `if / else-if / else` practice হচ্ছে।

---

# 💾 Result File

Result automatically:

```text
quiz_results.txt
```

এ save হবে।

আমরা:

```c
fopen(FILE_NAME, "a");
```

ব্যবহার করেছি।

`"a"` মানে **append**—আগের result মুছে না দিয়ে নতুন result শেষে যোগ হবে।

Example:

```text
Player: Rahim | Score: 8/10 | Percentage: 80.00%
Player: Karim | Score: 6/10 | Percentage: 60.00%
Player: Rahim | Score: 10/10 | Percentage: 100.00%
```

---

# ▶️ Compile

GCC থাকলে:

```bash
gcc -Wall -Wextra -pedantic main.c -o quiz
```

তারপর:

```bash
./quiz
```

Windows:

```bash
gcc -Wall -Wextra -pedantic main.c -o quiz.exe
```

তারপর:

```bash
quiz.exe
```

---

# 🖥️ Example

```text
============================================
             C QUIZ APPLICATION
============================================
Answer the following multiple-choice
questions and test your C programming
knowledge.
============================================

Enter your name: Rahim

Good luck, Rahim!

Press Enter to start the quiz...
```

তারপর:

```text
--------------------------------------------
Question 1 of 10
--------------------------------------------

Which language is known as a system programming language?

1. Python
2. C
3. HTML
4. SQL

Your answer (1-4): 2

Correct! +1 point
Current score: 1/1
```

শেষে:

```text
============================================
                 QUIZ RESULT
============================================
Player     : Rahim
Score      : 8/10
Percentage : 80.00%

Grade      : A
Excellent performance!
============================================

Result saved successfully.

Do you want to play again? (y/n):
```

---

# 🔥 এই Project-এ কী কী C Concept ব্যবহার হয়েছে?

|Concept|কোথায়|
|---|---|
|`struct`|`Question`|
|Array|questions/options|
|String|question/name/options|
|Functions|পুরো project|
|Pointer|`int *score`|
|`if/else`|grading|
|`for` loop|questions/options|
|`do-while`|replay|
|`switch`|চাইলে ভবিষ্যতে menu|
|Type casting|percentage|
|File handling|result saving|
|`fopen()`|file open|
|`fprintf()`|result write|
|`fclose()`|file close|
|`strlen`-related string handling|`strcspn()`|

### 🎯 সবচেয়ে গুরুত্বপূর্ণ অংশ

এই project-এর পর তোমার পরের logical upgrade হবে:

```text
Quiz Application V2
│
├── Question Bank
├── Random Questions
├── Timer
├── Multiple Categories
├── Difficulty Levels
├── Leaderboard
└── Admin Add/Edit Questions
```

এগুলো করলে project-টা অনেক বেশি বাস্তব **CLI quiz game**-এর মতো হবে।

---

# 🎮 CLI Quiz Game — Complete C Project

এবার আগের Quiz Application-কে একটা proper **CLI Quiz Game** বানাই।

### Features

- 👤 Player name
    
- 🎮 Main menu
    
- 📚 Categories
    
- 🎯 Difficulty levels
    
- 🔀 Random questions
    
- ❤️ 3 lives
    
- ⭐ Score system
    
- 🔥 Streak bonus
    
- 💡 Hint
    
- 🏆 High score / leaderboard
    
- 💾 Save scores to file
    
- 📊 Final result
    
- 🔄 Play again
    

---

# 📁 Project Structure

```text
CLIQuizGame/
└── main.c
```

# `main.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_QUESTIONS 15
#define OPTIONS 4
#define MAX_NAME 50
#define MAX_SCORES 100

#define SCORE_FILE "leaderboard.txt"


/* =========================================
   ENUMS
   ========================================= */

typedef enum
{
    EASY = 1,
    MEDIUM,
    HARD
} Difficulty;


typedef enum
{
    C_PROGRAMMING = 1,
    GENERAL_KNOWLEDGE,
    SCIENCE
} Category;


/* =========================================
   QUESTION STRUCTURE
   ========================================= */

typedef struct
{
    char question[250];

    char options[OPTIONS][100];

    int correctAnswer;

    Category category;

    Difficulty difficulty;

} Question;


/* =========================================
   SCORE STRUCTURE
   ========================================= */

typedef struct
{
    char name[MAX_NAME];

    int score;

} Score;


/* =========================================
   FUNCTION DECLARATIONS
   ========================================= */

void showTitle(void);

void showMainMenu(void);

void showCategories(void);

void showDifficulty(void);

int selectCategory(void);

int selectDifficulty(void);

void startGame(
    const char playerName[],
    Question questions[],
    int total
);

void shuffleQuestions(
    Question questions[],
    int total
);

int askQuestion(
    Question *q,
    int questionNumber,
    int *score,
    int *streak,
    int *hintUsed
);

void showFinalResult(
    const char name[],
    int score,
    int total
);

void showLeaderboard(void);

void saveScore(
    const char name[],
    int score
);

void sortScores(
    Score scores[],
    int count
);

int loadScores(
    Score scores[]
);

void clearInputBuffer(void);

void pauseScreen(void);


/* =========================================
   QUESTION BANK
   ========================================= */

Question questionBank[MAX_QUESTIONS] =
{

    /* ================= C ================= */

    {
        "Which function is used to print output in C?",

        {
            "scanf()",
            "printf()",
            "print()",
            "output()"
        },

        2,
        C_PROGRAMMING,
        EASY
    },


    {
        "Which symbol ends a C statement?",

        {
            ".",
            ":",
            ";",
            ","
        },

        3,
        C_PROGRAMMING,
        EASY
    },


    {
        "Which header file contains printf()?",

        {
            "stdlib.h",
            "string.h",
            "stdio.h",
            "math.h"
        },

        3,
        C_PROGRAMMING,
        EASY
    },


    {
        "Which operator gives the address of a variable?",

        {
            "*",
            "&",
            "#",
            "%"
        },

        2,
        C_PROGRAMMING,
        MEDIUM
    },


    {
        "Which keyword defines a structure?",

        {
            "structure",
            "struct",
            "record",
            "class"
        },

        2,
        C_PROGRAMMING,
        EASY
    },


    /* ================= GENERAL KNOWLEDGE ================= */

    {
        "What is the capital of Bangladesh?",

        {
            "Chittagong",
            "Dhaka",
            "Khulna",
            "Rajshahi"
        },

        2,
        GENERAL_KNOWLEDGE,
        EASY
    },


    {
        "How many days are there in a leap year?",

        {
            "365",
            "366",
            "364",
            "360"
        },

        2,
        GENERAL_KNOWLEDGE,
        EASY
    },


    {
        "Which is the largest ocean?",

        {
            "Atlantic Ocean",
            "Indian Ocean",
            "Pacific Ocean",
            "Arctic Ocean"
        },

        3,
        GENERAL_KNOWLEDGE,
        EASY
    },


    {
        "Which planet is known as the Red Planet?",

        {
            "Earth",
            "Mars",
            "Jupiter",
            "Venus"
        },

        2,
        GENERAL_KNOWLEDGE,
        EASY
    },


    {
        "How many continents are there?",

        {
            "5",
            "6",
            "7",
            "8"
        },

        3,
        GENERAL_KNOWLEDGE,
        MEDIUM
    },


    /* ================= SCIENCE ================= */

    {
        "What is the chemical formula of water?",

        {
            "CO2",
            "H2O",
            "O2",
            "NaCl"
        },

        2,
        SCIENCE,
        EASY
    },


    {
        "What force pulls objects toward Earth?",

        {
            "Magnetism",
            "Friction",
            "Gravity",
            "Electricity"
        },

        3,
        SCIENCE,
        EASY
    },


    {
        "What is the boiling point of water at sea level?",

        {
            "50 C",
            "75 C",
            "100 C",
            "150 C"
        },

        3,
        SCIENCE,
        MEDIUM
    },


    {
        "Which organ pumps blood through the body?",

        {
            "Lung",
            "Brain",
            "Heart",
            "Kidney"
        },

        3,
        SCIENCE,
        EASY
    },


    {
        "Which gas do humans need for respiration?",

        {
            "Carbon dioxide",
            "Oxygen",
            "Nitrogen",
            "Hydrogen"
        },

        2,
        SCIENCE,
        EASY
    }
};


/* =========================================
   MAIN
   ========================================= */

int main(void)
{
    int choice;

    char playerName[MAX_NAME];


    srand((unsigned int)time(NULL));


    while (1)
    {
        showTitle();

        showMainMenu();


        printf("Enter choice: ");

        scanf("%d", &choice);

        clearInputBuffer();


        switch (choice)
        {
            case 1:

                printf("\nEnter player name: ");

                fgets(
                    playerName,
                    sizeof(playerName),
                    stdin
                );

                playerName[
                    strcspn(playerName, "\n")
                ] = '\0';


                startGame(
                    playerName,
                    questionBank,
                    MAX_QUESTIONS
                );

                break;


            case 2:

                showLeaderboard();

                pauseScreen();

                break;


            case 3:

                printf("\nThanks for playing!\n");

                return 0;


            default:

                printf("\nInvalid choice!\n");

                pauseScreen();
        }
    }


    return 0;
}


/* =========================================
   TITLE
   ========================================= */

void showTitle(void)
{
    printf("\n");
    printf("============================================\n");
    printf("              C CLI QUIZ GAME               \n");
    printf("============================================\n");
}


/* =========================================
   MAIN MENU
   ========================================= */

void showMainMenu(void)
{
    printf("\n");
    printf("1. Start Game\n");
    printf("2. Leaderboard\n");
    printf("3. Exit\n");

    printf("--------------------------------------------\n");
}


/* =========================================
   START GAME
   ========================================= */

void startGame(
    const char playerName[],
    Question questions[],
    int total
)
{
    int category;

    int difficulty;

    int score = 0;

    int streak = 0;

    int lives = 3;

    int hintUsed = 0;

    int questionCount = 0;


    Question selected[MAX_QUESTIONS];


    printf("\n============================================\n");
    printf("                GAME SETUP                  \n");
    printf("============================================\n");


    category = selectCategory();

    difficulty = selectDifficulty();


    /*
       Select matching questions
    */

    for (int i = 0; i < total; i++)
    {
        if (
            questions[i].category == category &&
            questions[i].difficulty == difficulty
        )
        {
            selected[questionCount] =
                questions[i];

            questionCount++;
        }
    }


    if (questionCount == 0)
    {
        printf(
            "\nNo questions available for this selection.\n"
        );

        pauseScreen();

        return;
    }


    shuffleQuestions(
        selected,
        questionCount
    );


    /*
       Maximum 5 questions per game
    */

    if (questionCount > 5)
    {
        questionCount = 5;
    }


    printf("\n");
    printf("============================================\n");
    printf("              GAME STARTED                 \n");
    printf("============================================\n");

    printf("Player: %s\n", playerName);

    printf("Lives : %d\n", lives);

    printf("Questions: %d\n", questionCount);


    pauseScreen();


    /*
       Ask questions
    */

    for (int i = 0; i < questionCount; i++)
    {
        int correct;


        correct = askQuestion(
            &selected[i],
            i + 1,
            &score,
            &streak,
            &hintUsed
        );


        if (!correct)
        {
            lives--;

            streak = 0;

            printf("\nYou lost a life!");

            printf(
                "\nLives remaining: %d\n",
                lives
            );


            if (lives == 0)
            {
                printf(
                    "\nGame Over!\n"
                );

                break;
            }
        }


        printf("\nCurrent score: %d\n",
               score);
    }


    showFinalResult(
        playerName,
        score,
        questionCount
    );


    saveScore(
        playerName,
        score
    );


    pauseScreen();
}


/* =========================================
   SELECT CATEGORY
   ========================================= */

int selectCategory(void)
{
    int choice;


    showCategories();


    printf("Select category: ");

    scanf("%d", &choice);

    clearInputBuffer();


    if (
        choice < C_PROGRAMMING ||
        choice > SCIENCE
    )
    {
        printf(
            "\nInvalid category. C Programming selected.\n"
        );

        return C_PROGRAMMING;
    }


    return choice;
}


/* =========================================
   CATEGORIES
   ========================================= */

void showCategories(void)
{
    printf("\n");
    printf("========== CATEGORIES ==========\n");

    printf("1. C Programming\n");
    printf("2. General Knowledge\n");
    printf("3. Science\n");
}


/* =========================================
   SELECT DIFFICULTY
   ========================================= */

int selectDifficulty(void)
{
    int choice;


    showDifficulty();


    printf("Select difficulty: ");

    scanf("%d", &choice);

    clearInputBuffer();


    if (
        choice < EASY ||
        choice > HARD
    )
    {
        printf(
            "\nInvalid difficulty. Easy selected.\n"
        );

        return EASY;
    }


    return choice;
}


/* =========================================
   DIFFICULTY
   ========================================= */

void showDifficulty(void)
{
    printf("\n");
    printf("========== DIFFICULTY ==========\n");

    printf("1. Easy\n");
    printf("2. Medium\n");
    printf("3. Hard\n");
}


/* =========================================
   ASK QUESTION
   ========================================= */

int askQuestion(
    Question *q,
    int questionNumber,
    int *score,
    int *streak,
    int *hintUsed
)
{
    int answer;

    int useHint;


    printf("\n");
    printf("============================================\n");

    printf(
        "Question %d\n",
        questionNumber
    );

    printf("============================================\n");


    printf("%s\n\n",
           q->question);


    for (int i = 0; i < OPTIONS; i++)
    {
        printf(
            "%d. %s\n",
            i + 1,
            q->options[i]
        );
    }


    /*
       Hint
    */

    if (!(*hintUsed))
    {
        printf("\n5. Use Hint\n");
    }


    printf("\nYour answer: ");

    scanf("%d", &answer);

    clearInputBuffer();


    /*
       Hint
    */

    if (
        answer == 5 &&
        !(*hintUsed)
    )
    {
        printf(
            "\nHint: The correct answer starts with option %c.\n",
            'A' + q->correctAnswer - 1
        );


        *hintUsed = 1;


        printf(
            "\nEnter answer again: "
        );

        scanf("%d", &answer);

        clearInputBuffer();
    }


    /*
       Validate
    */

    if (
        answer < 1 ||
        answer > 4
    )
    {
        printf("\nInvalid answer.\n");

        return 0;
    }


    /*
       Correct
    */

    if (
        answer == q->correctAnswer
    )
    {
        int points = 10;


        (*streak)++;


        /*
           Streak bonus
        */

        if (*streak >= 3)
        {
            points += 5;

            printf(
                "\n🔥 Streak bonus! +5\n"
            );
        }


        *score += points;


        printf(
            "\nCorrect! +%d points\n",
            points
        );


        return 1;
    }


    /*
       Wrong
    */

    printf("\nWrong answer!\n");


    printf(
        "Correct answer: %d. %s\n",
        q->correctAnswer,
        q->options[
            q->correctAnswer - 1
        ]
    );


    return 0;
}


/* =========================================
   SHUFFLE QUESTIONS
   ========================================= */

void shuffleQuestions(
    Question questions[],
    int total
)
{
    for (int i = total - 1; i > 0; i--)
    {
        int j =
            rand() % (i + 1);


        Question temp =
            questions[i];

        questions[i] =
            questions[j];

        questions[j] =
            temp;
    }
}


/* =========================================
   FINAL RESULT
   ========================================= */

void showFinalResult(
    const char name[],
    int score,
    int total
)
{
    float maxScore;

    float percentage;


    /*
       Maximum score assumes
       10 points per question.
    */

    maxScore =
        total * 10;


    percentage =
        (score / maxScore) * 100;


    printf("\n");
    printf("============================================\n");
    printf("                GAME RESULT                 \n");
    printf("============================================\n");


    printf(
        "Player     : %s\n",
        name
    );


    printf(
        "Score      : %.0f/%0.f\n",
        (float)score,
        maxScore
    );


    printf(
        "Percentage : %.2f%%\n",
        percentage
    );


    if (percentage >= 80)
    {
        printf(
            "Rank       : ⭐ Excellent\n"
        );
    }
    else if (percentage >= 60)
    {
        printf(
            "Rank       : 👍 Good\n"
        );
    }
    else if (percentage >= 40)
    {
        printf(
            "Rank       : 🙂 Keep Practicing\n"
        );
    }
    else
    {
        printf(
            "Rank       : 📚 Beginner\n"
        );
    }


    printf("============================================\n");
}


/* =========================================
   SAVE SCORE
   ========================================= */

void saveScore(
    const char name[],
    int score
)
{
    FILE *file;


    file = fopen(
        SCORE_FILE,
        "a"
    );


    if (file == NULL)
    {
        printf(
            "\nCould not save score.\n"
        );

        return;
    }


    fprintf(
        file,
        "%s %d\n",
        name,
        score
    );


    fclose(file);
}


/* =========================================
   LOAD SCORES
   ========================================= */

int loadScores(
    Score scores[]
)
{
    FILE *file;

    int count = 0;


    file = fopen(
        SCORE_FILE,
        "r"
    );


    if (file == NULL)
    {
        return 0;
    }


    while (
        count < MAX_SCORES &&
        fscanf(
            file,
            "%49s %d",
            scores[count].name,
            &scores[count].score
        ) == 2
    )
    {
        count++;
    }


    fclose(file);


    return count;
}


/* =========================================
   SORT SCORES
   ========================================= */

void sortScores(
    Score scores[],
    int count
)
{
    for (int i = 0; i < count - 1; i++)
    {
        for (int j = 0; j < count - i - 1; j++)
        {
            if (
                scores[j].score <
                scores[j + 1].score
            )
            {
                Score temp =
                    scores[j];

                scores[j] =
                    scores[j + 1];

                scores[j + 1] =
                    temp;
            }
        }
    }
}


/* =========================================
   LEADERBOARD
   ========================================= */

void showLeaderboard(void)
{
    Score scores[MAX_SCORES];

    int count;


    count = loadScores(scores);


    if (count == 0)
    {
        printf(
            "\nNo scores available yet.\n"
        );

        return;
    }


    sortScores(
        scores,
        count
    );


    printf("\n");
    printf("============================================\n");
    printf("                 LEADERBOARD                \n");
    printf("============================================\n");


    int limit = count;


    if (limit > 10)
    {
        limit = 10;
    }


    for (int i = 0; i < limit; i++)
    {
        printf(
            "%2d. %-20s %4d points\n",
            i + 1,
            scores[i].name,
            scores[i].score
        );
    }


    printf("============================================\n");
}


/* =========================================
   CLEAR INPUT BUFFER
   ========================================= */

void clearInputBuffer(void)
{
    int c;


    while (
        (c = getchar()) != '\n' &&
        c != EOF
    )
    {
        /* discard */
    }
}


/* =========================================
   PAUSE
   ========================================= */

void pauseScreen(void)
{
    printf(
        "\nPress Enter to continue..."
    );

    getchar();
}
```

---

# 🎮 Game Flow

Program চালু করলে:

```text
============================================
              C CLI QUIZ GAME
============================================

1. Start Game
2. Leaderboard
3. Exit
```

`1` দিলে:

```text
Enter player name: Rahim

========== CATEGORIES ==========

1. C Programming
2. General Knowledge
3. Science

Select category: 1
```

তারপর:

```text
========== DIFFICULTY ==========

1. Easy
2. Medium
3. Hard

Select difficulty: 1
```

তারপর random questions শুরু হবে।

---

# ❤️ Lives System

প্রতিটি game-এ:

```text
❤️ Lives = 3
```

Wrong answer হলে:

```text
Wrong answer!

You lost a life!
Lives remaining: 2
```

তিনটি ভুল হলে:

```text
Game Over!
```

---

# ⭐ Score System

সঠিক answer:

```text
Correct! +10 points
```

পরপর 3টি correct হলে:

```text
🔥 Streak bonus! +5
```

অর্থাৎ:

```text
Normal correct = 10
3rd consecutive correct = 15
```

---

# 💡 Hint System

প্রতিটি game-এ একবার hint ব্যবহার করা যাবে:

```text
5. Use Hint
```

তারপর:

```text
Hint: The correct answer starts with option B.
```

Hint ব্যবহার করার পর আবার answer দিতে হবে।

---

# 🔀 Random Questions

এই function:

```c
shuffleQuestions(selected, questionCount);
```

Fisher-Yates style shuffle ব্যবহার করে questions-এর order random করে।

মূল অংশ:

```c
int j = rand() % (i + 1);

Question temp = questions[i];

questions[i] = questions[j];

questions[j] = temp;
```

আর `main()`-এ:

```c
srand((unsigned int)time(NULL));
```

দিয়ে random seed করা হয়েছে।

ফলে প্রতিবার একই order-এ question আসবে না।

---

# 🏆 Leaderboard

Game শেষ হলে score:

```text
leaderboard.txt
```

এ save হবে।

যেমন:

```text
Rahim 85
Karim 70
Hasan 95
```

Leaderboard select করলে program scoreগুলো sort করে:

```text
============================================
                 LEADERBOARD
============================================

 1. Hasan                    95 points
 2. Rahim                    85 points
 3. Karim                    70 points
```

---

# ⚠️ একটা ছোট Limitation

এই version-এ player name **একটি word** হিসেবে leaderboard file-এ রাখা হচ্ছে, কারণ:

```c
fscanf(file, "%49s %d", ...)
```

ব্যবহার করেছি।

তাই:

```text
Rahim
```

ঠিকভাবে কাজ করবে।

কিন্তু:

```text
Rahim Hasan
```

দিলে leaderboard-এ পুরো নাম handle হবে না।

এটা ইচ্ছাকৃতভাবে simple রাখা হয়েছে যাতে তুমি file parsing এবং struct-এর মূল concept আগে বুঝতে পারো।

---

# 🧠 এই Project-এ Advanced C Concepts

এবার আগের Quiz Application-এর তুলনায় অনেক বেশি concept একসাথে এসেছে:

|Concept|ব্যবহার|
|---|---|
|`struct`|`Question`, `Score`|
|`enum`|Category, Difficulty|
|2D array|Options|
|Array of structures|Question bank|
|Pointer|`Question *`, `int *`|
|Function|Game modules|
|`for`|questions/options|
|`while`|menu/file loading|
|`if/else`|answer/score|
|File handling|leaderboard|
|`rand()`|randomization|
|`srand()`|random seed|
|`time()`|random seed|
|String handling|player name|
|Sorting|leaderboard|
|Bubble sort|score ordering|
|Type casting|percentage|

---

# 🏗️ Project Architecture

```text
                   main()
                     │
                     ▼
                Main Menu
              ┌──────┼──────┐
              │      │      │
              ▼      ▼      ▼
            Game  Leaderboard Exit
              │       │
              ▼       ▼
          Category   Load File
              │       │
              ▼       ▼
         Difficulty  Sort
              │       │
              ▼       ▼
          Questions Leaderboard
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
     Answer  Hint   Score
       │      │      │
       └──────┼──────┘
              ▼
          Final Result
              │
              ▼
       Save leaderboard
```

---

# ▶️ Compile

Linux/macOS:

```bash
gcc -Wall -Wextra -pedantic main.c -o quiz
./quiz
```

Windows:

```bash
gcc -Wall -Wextra -pedantic main.c -o quiz.exe
quiz.exe
```

---

# 🚀 এরপর Project-টাকে আরও বড় করা যায়

তোমার current version:

```text
CLI Quiz Game
├── Categories
├── Difficulty
├── Random questions
├── Lives
├── Hint
├── Streak
├── Score
└── Leaderboard
```

এর **next professional version** হলে architecture হবে:

```text
CLIQuizGame/
│
├── main.c
├── quiz.c
├── quiz.h
├── questions.c
├── questions.h
├── leaderboard.c
├── leaderboard.h
│
└── data/
    ├── questions.dat
    └── leaderboard.dat
```

এটা করলে তুমি **multi-file C programming, header files, modular programming এবং binary file handling** একসাথে practice করতে পারবে।


---
