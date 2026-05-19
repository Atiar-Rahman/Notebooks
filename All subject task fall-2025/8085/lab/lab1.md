1. variable declare and print output using 8085


# 1️⃣ Register কি?

**Register** হলো CPU এর ভিতরের **ছোট ও খুব দ্রুত memory** যেখানে temporary data রাখা হয়।

Example registers (8086):

- AX
    
- BX
    
- CX
    
- DX
    

এগুলোকে **general purpose register** বলা হয়।

---

# 2️⃣ কখন Register ব্যবহার করতে হয়?

Register ব্যবহার করা হয় যখন:

### 1. Calculation করতে হবে

Arithmetic operation করতে register লাগে।

Example

```asm
MOV AX,5
MOV BX,3
ADD AX,BX
```

এখানে calculation **register এর ভিতরেই হচ্ছে**।

---

### 2. Memory থেকে data নিতে হলে

```asm
MOV AX,NUM1
```

Memory → Register

---

### 3. Loop counter হিসেবে

```asm
MOV CX,5
```

Loop এ সাধারণত **CX register** ব্যবহার করা হয়।

---

### 4. Input/Output operation

অনেক সময় data আগে register এ রাখতে হয়।

---

# 3️⃣ কেন Register ব্যবহার করা হয়?

কারণ:

|Reason|Explanation|
|---|---|
|Fast|Register CPU এর ভিতরে থাকে|
|Calculation|Arithmetic operation register এ হয়|
|Temporary storage|Temporary data store|

👉 Register ব্যবহার করলে program **fast run করে**।

---

# 4️⃣ Register ব্যবহার না করলে কি হবে?

অনেক instruction **register ছাড়া কাজই করবে না**।

Example ❌ (wrong)

```asm
ADD NUM1,NUM2
```

এটা অনেক ক্ষেত্রে allowed না।

Correct way ✔

```asm
MOV AX,NUM1
ADD AX,NUM2
```

---

# 5️⃣ Simple Example

```asm
.DATA
A DB 5
B DB 3

.CODE
MOV AL,A
ADD AL,B
```

Step

1. A → AL register
    
2. B → AL এর সাথে add
    
3. Result → AL
    

---

# 6️⃣ Easy Way to Remember

**Memory = store data**  
**Register = process data**

---

✅ **Short exam answer**

> Registers are small high-speed storage locations inside the CPU used to store temporary data and perform arithmetic or logical operations. Registers are used because most instructions of the 8086 processor operate on registers.

---


তুমি যেহেতু **Intel 8086** assembly শিখছো, নিচে **সব গুরুত্বপূর্ণ register** খুব সহজভাবে diagram ও কাজসহ দেখালাম।

---

# 8086 Registers Simple Diagram

```
            8086 CPU Registers
        -------------------------
        |   General Registers   |
        |-----------------------|
        | AX | BX | CX | DX     |
        -------------------------

        | Index Registers |
        |----------------|
        | SI | DI        |
        ------------------

        | Pointer Registers |
        |------------------|
        | SP | BP          |
        --------------------
```

---

# 1️⃣ AX – Accumulator Register

**Main calculation register**

Use:

* Arithmetic
* Multiplication
* Division
* Data transfer

Example

```asm
MOV AX,5
ADD AX,3
```

Result → AX = 8

---

# 2️⃣ BX – Base Register

**Memory address store করতে ব্যবহার হয়**

Example

```asm
MOV BX,1000H
MOV AX,[BX]
```

Meaning
Memory address 1000H থেকে data AX এ যাবে।

---

# 3️⃣ CX – Counter Register

**Loop এবং repetition এর জন্য**

Example

```asm
MOV CX,5

LOOP1:
DEC CX
JNZ LOOP1
```

Program 5 বার run হবে।

---

# 4️⃣ DX – Data Register

**Input / Output operation এর জন্য**

Example

```asm
MOV DX,03F8H
```

Port address store করতে পারে।

---

# 5️⃣ SI – Source Index

**Data copy করার সময় source address**

Example

```asm
MOV SI,2000H
```

---

# 6️⃣ DI – Destination Index

**Data copy করার সময় destination address**

Example

```asm
MOV DI,3000H
```

---

# 7️⃣ SP – Stack Pointer

**Stack এর top address ধরে**

Stack operations:

* PUSH
* POP

Example

```asm
PUSH AX
POP BX
```

---

# 8️⃣ BP – Base Pointer

**Stack memory access করার জন্য**

Example

```asm
MOV BP,1000H
```

---

# Easy Memory Trick (Exam / Viva)

```
AX → Arithmetic
BX → Base address
CX → Counter (loop)
DX → Data / I-O
SI → Source
DI → Destination
SP → Stack top
BP → Base pointer
```

---

✅ **Exam Ready Short Answer**

> The 8086 microprocessor has several registers such as AX, BX, CX, DX, SI, DI, SP and BP. AX is used for arithmetic operations, BX for base addressing, CX as loop counter, DX for data and I/O operations, SI and DI for indexing, and SP and BP for stack operations.

---
হ্যাঁ, **Intel 8086**-এ প্রতিটি register এর **একটা প্রধান কাজ থাকে**, কিন্তু অনেক ক্ষেত্রে **general purpose হওয়ার কারণে অন্য কাজেও ব্যবহার করা যায়**। নিচে সহজভাবে দেখানো হলো।

---

# 8086 Registers এবং তাদের প্রধান কাজ

| Register | প্রধান কাজ                                | Example        |
| -------- | ----------------------------------------- | -------------- |
| **AX**   | Arithmetic / accumulator                  | `ADD AX,BX`    |
| **BX**   | Memory base address                       | `MOV AX,[BX]`  |
| **CX**   | Loop counter                              | `LOOP START`   |
| **DX**   | Data / Input-Output                       | `MOV DX,PORT`  |
| **SI**   | Source index (data copy source)           | `MOV SI,2000H` |
| **DI**   | Destination index (data copy destination) | `MOV DI,3000H` |
| **SP**   | Stack pointer (stack top)                 | `PUSH AX`      |
| **BP**   | Base pointer (stack access)               | `MOV AX,[BP]`  |

---

# Example

### Arithmetic

```asm
MOV AX,5
MOV BX,3
ADD AX,BX
```

এখানে **AX calculation এর জন্য**।

---

### Loop

```asm
MOV CX,5
START:
DEC CX
JNZ START
```

এখানে **CX loop counter**।

---

### Memory access

```asm
MOV BX,1000H
MOV AX,[BX]
```

এখানে **BX address ধরে**।

---

# Important Point

✔ Register গুলো **general purpose**, তাই:

* AX → শুধু arithmetic না, data store করতেও পারে
* BX → calculation করতেও পারে
* CX → data রাখতেও পারে

👉 কিন্তু কিছু instruction **specific register prefer করে**।

---

✅ **Short exam answer**

> In 8086, registers such as AX, BX, CX, DX, SI, DI, SP and BP have specific primary purposes, but most of them are general purpose registers and can also be used for other operations depending on the instruction.

---

ভালো 👍 এখন **Intel 8086 assembly**-এর **10টা সবচেয়ে important instruction** সহজ example সহ দেখাচ্ছি। এগুলো সাধারণত **lab exam / viva** তে আসে।

---

# 1️⃣ MOV (Move Data)

এক জায়গা থেকে অন্য জায়গায় data নেয়।

```asm
MOV AX,5
MOV BX,AX
```

Meaning
AX = 5
BX = AX

---

# 2️⃣ ADD (Addition)

```asm
MOV AX,5
MOV BX,3
ADD AX,BX
```

Result
AX = 8

---

# 3️⃣ SUB (Subtraction)

```asm
MOV AX,9
MOV BX,4
SUB AX,BX
```

Result
AX = 5

---

# 4️⃣ INC (Increment)

Value 1 বাড়ায়।

```asm
MOV AX,5
INC AX
```

Result
AX = 6

---

# 5️⃣ DEC (Decrement)

Value 1 কমায়।

```asm
MOV AX,5
DEC AX
```

Result
AX = 4

---

# 6️⃣ CMP (Compare)

দুইটা value compare করে।

```asm
MOV AX,5
MOV BX,3
CMP AX,BX
```

এরপর jump instruction ব্যবহার করা হয়।

---

# 7️⃣ JMP (Jump)

Direct jump করে।

```asm
JMP START
```

Program সরাসরি **START label** এ যাবে।

---

# 8️⃣ LOOP

Loop repeat করার জন্য।

```asm
MOV CX,5

START:
LOOP START
```

Program 5 বার run হবে।

---

# 9️⃣ PUSH (Stack এ data রাখা)

```asm
PUSH AX
```

AX এর data stack এ যাবে।

---

# 🔟 POP (Stack থেকে data নেওয়া)

```asm
POP BX
```

Stack থেকে data BX এ যাবে।

---

# Easy Memory Trick

```
MOV → Move data
ADD → Addition
SUB → Subtraction
INC → +1
DEC → -1
CMP → Compare
JMP → Jump
LOOP → Repeat
PUSH → Stack store
POP → Stack remove
```

---

✅ **Exam Tip**

Teacher সাধারণত এই instruction দিয়ে program দিতে পারে:

* Add two numbers
* Subtract two numbers
* Largest number
* Loop program
* Stack example

---

8086 assembly-তে **subtraction করার জন্য `SUB` instruction** ব্যবহার করা হয়।

### Basic syntax

```asm
SUB destination, source
```

মানে:  
**destination = destination − source**

---

### Example 1

```asm
org 100h

mov ax,10
mov bx,4
sub ax,bx

ret
```

### Calculation

AX = 10 − 4 = **6**

✅ **Final: AX = 6**

---

### Example 2 (multiple subtraction)

```asm
org 100h

mov ax,20
mov bx,5
mov cx,3

sub ax,bx
sub ax,cx

ret
```

### Calculation

1️⃣ AX = 20 − 5 = **15**  
2️⃣ AX = 15 − 3 = **12**

✅ **Final: AX = 12**

---

### Important rule

❌ এটা হবে না:

```asm
sub 5, ax
```

✔ সবসময় **register বা memory destination** হতে হবে।

---

### Quick trick

Addition:

```
ADD AX,BX   ; AX = AX + BX
```

Subtraction:

```
SUB AX,BX   ; AX = AX - BX
```

---

হ্যাঁ, **অবশ্যই 2 বা তার বেশি সংখ্যা একসাথে যোগ বা বিয়োগ করা যায়**, কিন্তু 8086-এ direct 3+ operand support নেই। অর্থাৎ **একটি `ADD` বা `SUB` instruction শুধু 2 operand নিতে পারে**।

### কীভাবে করা যায়

#### উদাহরণ: 3+4+6+2 যোগ করা

```asm
mov ax, 3
add ax, 4    ; AX = 3 + 4 = 7
add ax, 6    ; AX = 7 + 6 = 13
add ax, 2    ; AX = 13 + 2 = 15
```

#### উদাহরণ: 20 − 5 − 3 − 2

```asm
mov ax, 20
sub ax, 5    ; AX = 15
sub ax, 3    ; AX = 12
sub ax, 2    ; AX = 10
```

💡 **Key point:** প্রতিটি ADD/SUB instruction **দুটি operand** নেয়:

1. Destination (result রাখা হবে)
    
2. Source (যা যোগ/বিয়োগ হবে)
    

তাই একাধিক সংখ্যা যোগ বা বিয়োগ করতে হলে **একটার পর একটা instruction** দিতে হবে।

---

ঠিক বলছো, **8086-এ এক লাইনে একাধিক সংখ্যা add বা sub করা যায় না**। 😅

### কেন

- `ADD` / `SUB` instruction **সরাসরি শুধু ২টি operand** নিতে পারে:
    
    ```asm
    ADD destination, source
    SUB destination, source
    ```
    
- একাধিক সংখ্যা যোগ করতে হলে **একটার পর একটা instruction** দিতে হবে, যেমন:
    

```asm
mov ax, 3
add ax, 4
add ax, 6
add ax, 2
```

- এক লাইনে লিখলে error হবে, যেমন:
    

```asm
add ax, 3, 4, 6  ; ❌ এটা কাজ করবে না
```

### সংক্ষেপে

- ✅ একাধিক সংখ্যা যোগ/বিয়োগ সম্ভব
    
- ✅ তবে **প্রতিটি ADD/SUB instruction শুধু ২ operand নিতে পারে**
    
- 🔹 এক লাইনে একাধিক number direct করা সম্ভব নয়
    

---------

### 1️⃣ Basic Syntax

```asm
MUL source
```

- **source**: register বা memory (8-bit বা 16-bit)
    
- **destination**: implicit, AX (8-bit) বা DX:AX (16-bit)
    

---

### 2️⃣ Rules

|Operand size|Implicit destination|Notes|
|---|---|---|
|8-bit (AL)|AX|AX = AL * source|
|16-bit (AX)|DX:AX|32-bit result = AX * source|

> **Unsigned multiplication** হয়। Signed multiplication এর জন্য **IMUL** ব্যবহার হয়।

---

### 3️⃣ Examples

#### Example 1: 8-bit multiplication

```asm
mov al, 5
mov bl, 4
mul bl   ; AX = AL * BL = 5*4 = 20
```

- AL = 5, BL = 4
    
- AX = 20
    
- AH = upper 8 bits of result (0 in this case)
    

---

#### Example 2: 16-bit multiplication

```asm
mov ax, 3000
mov bx, 2
mul bx   ; DX:AX = AX * BX = 3000 * 2 = 6000
```

- AX = 3000, BX = 2
    
- Result = 6000 stored in AX (DX = 0 here)
    

---

### 4️⃣ IMUL (Signed multiplication)

```asm
mov ax, -3
mov bx, 4
imul bx   ; AX = -12
```

- Signed numbers এর জন্য IMUL ব্যবহার করতে হবে।
    

---

### Quick Summary

- `MUL` → unsigned, result stored in AX (8-bit) or DX:AX (16-bit)
    
- `IMUL` → signed
    
- একবারে **একটি operand** নিতে পারে, destination **implicit**
    

---

## 1️⃣ Basic Syntax

```asm
DIV source
```

- **source** = divisor (register বা memory)
    
- **destination** = implicit, dividend এর উপর নির্ভর করে:
    

|Operand size|Dividend register|Quotient →|Remainder →|
|---|---|---|---|
|8-bit|AX|AL|AH|
|16-bit|DX:AX|AX|DX|

> `DIV` **unsigned division** করে। Signed division এর জন্য `IDIV` ব্যবহার হয়।

---

## 2️⃣ Examples

### Example 1: 8-bit division

```asm
mov ax, 20   ; dividend
mov bl, 4    ; divisor
div bl       ; AX / BL
```

- AX = 20, BL = 4
    
- Quotient → AL = 5
    
- Remainder → AH = 0
    

---

### Example 2: 16-bit division

```asm
mov ax, 6000   ; lower 16-bit of dividend
mov dx, 0      ; upper 16-bit of dividend
mov bx, 300    ; divisor
div bx         ; DX:AX / BX
```

- Dividend = DX:AX = 6000
    
- Divisor = BX = 300
    
- Quotient → AX = 20
    
- Remainder → DX = 0
    

---

### 3️⃣ Important Rules

1. **Dividend size must match operand size**
    
    - 8-bit divisor → AX is dividend
        
    - 16-bit divisor → DX:AX is dividend
        
2. **Division by zero** → CPU **exception**
    
3. **Signed division** → Use `IDIV`
    

---

### Quick Example Table

|Instruction|Dividend|Divisor|Quotient|Remainder|
|---|---|---|---|---|
|`DIV BL`|AX|BL|AL|AH|
|`DIV BX`|DX:AX|BX|AX|DX|

---

যদি **negative value বা signed number** নিয়ে কাজ করছ, তাহলে 8086 এ **signed instructions** ব্যবহার করতে হবে। 😎

---

## 1️⃣ Key Rules

|Operation|Unsigned|Signed|
|---|---|---|
|Addition|ADD|IADD → Actually `ADD` works same for signed too|
|Subtraction|SUB|ISUB → Actually `SUB` works same for signed too|
|Multiplication|MUL|IMUL|
|Division|DIV|IDIV|

---

### 2️⃣ Explanation

- **ADD / SUB**:
    
    - Addition & subtraction **signed & unsigned** এক instruction দিয়ে করা যায়।
        
    - CPU overflow flag (OF) দেখে negative/positive result detect করা যায়।
        
- **MUL / DIV**:
    
    - **MUL / DIV** → unsigned multiplication/division
        
    - **IMUL / IDIV** → signed multiplication/division
        
    - Negative number হলে অবশ্যই **IMUL / IDIV** ব্যবহার করতে হবে
        

---

### 3️⃣ Example: Multiplication

#### Unsigned

```asm
mov ax, 4
mov bx, 3
mul bx    ; AX = 12
```

#### Signed

```asm
mov ax, -4
mov bx, 3
imul bx   ; AX = -12
```

---

### 4️⃣ Example: Division

#### Unsigned

```asm
mov ax, 12
mov bl, 5
div bl    ; AL = 2, AH = remainder
```

#### Signed

```asm
mov ax, -12
mov bl, 5
idiv bl   ; AL = -2, AH = remainder
```

---

✅ **Rule of thumb:**

- **Negative numbers → IMUL / IDIV**
    
- **Positive numbers → MUL / DIV**
    
- **ADD / SUB** works for both signed & unsigned
    

---

```asm
org 100h

; --------------------------
; Unsigned multiplication & division
; --------------------------
mov ax, 6      ; unsigned number 6
mov bx, 4      ; unsigned number 4
mul bx         ; AX = 6 * 4 = 24 (unsigned multiplication)
; result = AX (24)

mov cx, 5      ; unsigned divisor
div cx         ; AX / CX = quotient in AL, remainder in AH
; quotient = 24 / 5 = 4, remainder = 4

; --------------------------
; Signed multiplication & division
; --------------------------
mov ax, -6     ; signed number -6
mov bx, 4      ; signed number 4
imul bx        ; AX = -6 * 4 = -24 (signed multiplication)
; result = AX (-24)

mov cx, 5      ; signed divisor
idiv cx        ; AX / CX = quotient = -24 / 5 = -4, remainder = -4
; quotient = AX, remainder = DX (for 16-bit division, here small numbers DX=0)

ret
```

---

### Explanation step by step

1. **Unsigned**:
    
    - `mul bx` → 6 × 4 = 24
        
    - `div cx` → 24 ÷ 5 → quotient = 4 (AL), remainder = 4 (AH)
        
2. **Signed**:
    
    - `imul bx` → -6 × 4 = -24
        
    - `idiv cx` → -24 ÷ 5 → quotient = -4, remainder = -4
        

---

💡 **Key points**:

- `MUL` / `DIV` → **unsigned only**
    
- `IMUL` / `IDIV` → **signed only**
    
- `ADD` / `SUB` → signed & unsigned একসাথে ব্যবহার করা যায়
    
- Division remainder কখনও ignore করলে, quotient integer division হিসাবেই আসে
    

---


 **8086 instructions এ `destination` ও `source` বুঝতে চাচ্ছো**। 

---

### 1️⃣ সাধারণ নিয়ম

**Instruction:**

```asm
ADD destination, source
SUB destination, source
MUL source
IMUL source
DIV source
IDIV source
```

|Instruction|Destination|Source|Notes|
|---|---|---|---|
|ADD / SUB|Explicit|Explicit|2 operand, result in destination|
|MUL / IMUL|Implicit|Explicit|Destination = AX (8-bit) বা DX:AX (16-bit), source = register/mem|
|DIV / IDIV|Implicit|Explicit|Dividend = AX (8-bit) বা DX:AX (16-bit), quotient → AX/AL, remainder → DX/AH|

---

### 2️⃣ Example: ADD / SUB

```asm
mov ax, 5
mov bx, 3
add ax, bx   ; destination = AX, source = BX → AX = 8
sub ax, 2    ; destination = AX, source = 2 → AX = 6
```

✅ **Destination এখানে explicit**

---

### 3️⃣ Example: MUL / IMUL

```asm
mov ax, 6
mov bx, 4
mul bx       ; destination = AX (implicit), source = BX
imul bx      ; destination = AX (implicit), source = BX
```

- এখানে **AX (16-bit) implicit** → কোনো explicit destination নেই
    
- শুধুমাত্র **source** দিতে হয়
    

---

### 4️⃣ Example: DIV / IDIV

```asm
mov ax, 24
mov bl, 5
div bl       ; dividend = AX (implicit), divisor = BL (source)
idiv bl      ; dividend = AX (signed), divisor = BL
```

- again **destination implicit** (AX/AL for quotient, DX/AH for remainder)
    
- only **source** দেওয়া লাগে
    

---

### ✅ সংক্ষেপে

|Instruction type|Destination needed?|Source needed?|
|---|---|---|
|ADD / SUB|Yes|Yes|
|MUL / IMUL|Implicit|Yes|
|DIV / IDIV|Implicit|Yes|

💡 **Rule of thumb**:

- **ADD/SUB → dest + src**
    
- **MUL/IMUL/DIV/IDIV → only source, dest implicit**
    

---


### Key Rules

1️⃣ **ADD / SUB** → immediate number দেওয়া যায়

```asm
mov ax, 5
add ax, 3    ; OK, AX = 8
sub ax, 2    ; OK, AX = 6
```

2️⃣ **MUL / IMUL / DIV / IDIV** → **register বা memory operand লাগবে**, direct number **না**

❌ ভুল:

```asm
imul 4    ; 8086 error
div 5     ; 8086 error
```

✅ ঠিক:

```asm
mov bx, 4
imul bx   ; AX = AX * 4

mov cx, 5
idiv cx   ; AX / CX
```

---

### 3️⃣ Practical Rule of Thumb

- **Immediate numbers:** শুধু **ADD / SUB** তে direct ব্যবহার করা যায়
    
- **MUL / DIV / IMUL / IDIV:**
    
    1. আগে number → register বা memory এ রাখো
        
    2. তারপর multiply/divide instruction এ সেই register/memory use করো
        

---

### 4️⃣ Example: Negative result multiply

```asm
mov ax, -2
mov bx, 4
imul bx    ; AX = -2 * 4 = -8
```

---

💡 **Tip:**  
যদি তুমি মনে করো “এটাতে time loss হয়” → এটা ঠিক, কিন্তু 8086 এর limitation।

- সব arithmetic operation **register-based** করতে হয়
    
- Compiler এই limitation handle করে, কিন্তু assembly তে সব manually করতে হয়
    

---

