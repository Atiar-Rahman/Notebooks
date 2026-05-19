তুমি যে **Stack and Subroutines (8085 Microprocessor)** PDF দিয়েছ, আমি এখানকার **প্রতিটি গুরুত্বপূর্ণ term সহজ ভাষায় example সহ explain** করছি।

---

# 1. Stack

**Definition:**
Stack হলো RAM-এর কিছু memory location যেখানে program execution এর সময় **temporary data store** করা হয়। 

**Important rule:**
Stack কাজ করে **LIFO (Last In First Out)** principle দিয়ে।

### Example (Real life)

একটা **plate stack** ভাবো।

```
Plate1
Plate2
Plate3  ← Last added
```

তুমি যদি plate বের করো:

```
Plate3 → first বের হবে
```

মানে **Last In → First Out**

### Example (Memory)

```
2099
2098
2097
```

যদি data push করো:

```
2098 → H register
2097 → L register
```

---

# 2. Stack Pointer (SP)

**Definition:**
Stack Pointer হলো একটি **16-bit register** যা stack এর **top location** নির্দেশ করে। 

### Example

```
LXI SP, 2099H
```

Meaning:

```
SP = 2099H
```

এখন stack এর top address = **2099**

---

# 3. Stack Growth Direction

8085-এ stack **backwards grow করে**।

মানে address **কমতে থাকে**।

Example:

```
Start SP = 2099

Push করলে:

2099
2098
2097
```

SP কমতে থাকে।

---

# 4. PUSH Instruction

**Definition:**
Register pair এর data **stack এ store** করার instruction। 

Syntax:

```
PUSH register pair
```

Example:

```
LXI SP,2099H
LXI H,42F2H
PUSH H
```

HL register pair:

```
H = 42
L = F2
```

### Step by Step

1️⃣ SP = 2099

2️⃣ SP decrement → 2098
Memory[2098] = H (42)

3️⃣ SP decrement → 2097
Memory[2097] = L (F2)

Memory:

```
Address   Data
2098      42
2097      F2
```

---

# 5. POP Instruction

**Definition:**
Stack থেকে data **register pair এ ফিরিয়ে আনে**। 

Syntax:

```
POP register pair
```

Example:

```
POP H
```

### Step by Step

1️⃣ SP = 2097

```
L = Memory[2097] = F2
```

2️⃣ SP increment → 2098

```
H = Memory[2098] = 42
```

3️⃣ SP increment → 2099

HL register আবার:

```
H = 42
L = F2
```

---

# 6. PUSH PSW

PSW = **Program Status Word**

এতে থাকে:

```
A register
Flag register
```

Instruction:

```
PUSH PSW
```

### Example

```
A = 12
Flag = 80
```

Stack এ store হবে:

```
Address   Data
FFFC      12
FFFB      80
```

---

# 7. POP PSW

Stack থেকে **A এবং Flag register** restore করে।

Instruction:

```
POP PSW
```

Example:

```
Flag = Memory[SP]
A = Memory[SP+1]
```

---

# 8. Stack Operation Rule

### PUSH

```
Decrement SP
Store data
```

Example

```
SP = 2000
After PUSH → 1999
```

### POP

```
Use data
Increment SP
```

Example

```
SP = 1999
After POP → 2000
```

---

# 9. Subroutine

**Definition:**
Subroutine হলো **একটা small program block** যা main program বারবার ব্যবহার করতে পারে। 

Example:

ধরো program এ অনেক জায়গায় **delay** দরকার।

তুমি বারবার code না লিখে:

```
CALL DELAY
```

ব্যবহার করবে।

---

# 10. CALL Instruction

CALL ব্যবহার করে **subroutine execute করা হয়**।

Syntax:

```
CALL address
```

Example:

```
CALL 2050H
```

Meaning:

```
Go to memory location 2050
Execute subroutine
```

### What happens internally

1️⃣ Next instruction address stack এ push হয়

2️⃣ Program control → subroutine

---

# 11. RET Instruction

RET ব্যবহার করে **main program এ ফিরে আসে**।

Syntax:

```
RET
```

Example flow:

```
Main Program
CALL 2050

Subroutine
2050: instruction
2051: instruction
2052: RET
```

RET হলে program আবার:

```
CALL এর পরের instruction
```

এ চলে যায়।

---

# 12. Conditional CALL

Condition true হলে call হবে।

Example instructions:

| Instruction | Meaning           |
| ----------- | ----------------- |
| CC          | Call if carry = 1 |
| CNC         | Call if carry = 0 |
| CZ          | Call if zero = 1  |
| CNZ         | Call if zero = 0  |

Example:

```
CZ 3000H
```

Meaning:

```
Zero flag = 1 হলে
3000 address এ subroutine call হবে
```

---

# 13. Conditional Return

Condition true হলে return করবে।

| Instruction | Meaning             |
| ----------- | ------------------- |
| RC          | Return if carry = 1 |
| RNC         | Return if carry = 0 |
| RZ          | Return if zero = 1  |
| RNZ         | Return if zero = 0  |

Example:

```
RZ
```

Meaning:

```
Zero flag = 1 হলে
main program এ ফিরে যাবে
```

---

# 14. Advantages of Subroutine

1️⃣ Code reuse করা যায়
2️⃣ Program ছোট হয়
3️⃣ Debugging সহজ হয়
4️⃣ Complex program সহজ হয়

---

✅ **Very Simple Program Example**

```
LXI SP,2099H

CALL DELAY

MOV A,B

DELAY:
MVI C,FF
DCR C
JNZ DELAY
RET
```

Flow:

```
Main Program
   ↓
CALL DELAY
   ↓
Subroutine run
   ↓
RET
   ↓
Back to Main Program
```

---

# Stack and Subroutine in 8085 (Short Note – 5 Marks)

## Stack

Stack হলো RAM-এর একটি অংশ যেখানে program execution এর সময় **temporary data store** করা হয়। এটি **LIFO (Last In First Out)** principle অনুসরণ করে। 

Stack এর top address **Stack Pointer (SP)** দ্বারা নির্দেশ করা হয়, যা একটি **16-bit register**। সাধারণত stack memory এর **highest address থেকে শুরু হয় এবং নিচের দিকে grow করে**। 

Stack এ data store ও retrieve করার জন্য দুটি instruction ব্যবহার করা হয়:

### PUSH

Register pair এর data stack এ store করার জন্য ব্যবহৃত হয়।

Example:

```
LXI SP,2099H
LXI H,42F2H
PUSH H
```

এখানে HL register pair এর data stack এ store হবে।

### POP

Stack থেকে data register pair এ ফিরিয়ে আনার জন্য ব্যবহৃত হয়।

Example:

```
POP H
```

এতে stack এর data আবার HL register pair এ ফিরে আসে।

---

## Subroutine

Subroutine হলো একটি **instruction group** যা main program থেকে আলাদা করে লেখা হয় এবং নির্দিষ্ট কাজ বারবার করার জন্য ব্যবহার করা হয়। 

Main program থেকে subroutine execute করার জন্য **CALL instruction** ব্যবহার করা হয় এবং কাজ শেষ হলে **RET instruction** ব্যবহার করে main program এ ফিরে আসে।

### CALL Instruction

Subroutine call করার জন্য ব্যবহৃত হয়।

Example:

```
CALL 2050H
```

এটি program control কে address 2050H এ পাঠায়।

### RET Instruction

Subroutine শেষ হলে main program এ ফিরে আসে।

Example:

```
RET
```

---

## Advantages of Subroutine

1. Program ছোট এবং organized হয়
2. Code reuse করা যায়
3. Debugging সহজ হয়
4. Complex program সহজে তৈরি করা যায়

---


# Stack and Subroutine in 8085 Microprocessor

## 1. Stack

Stack হলো RAM এর একটি অংশ যেখানে program execution চলাকালীন **temporary data store করা হয়**। এটি **LIFO (Last In First Out)** principle অনুসরণ করে।

Stack এর top address নির্দেশ করে **Stack Pointer (SP)** register, যা একটি **16-bit register**। সাধারণত stack memory এর **highest address থেকে শুরু হয়ে নিচের দিকে grow করে**।

Stack initialize করার জন্য নিচের instruction ব্যবহার করা হয়:

```
LXI SP, 2099H
```

এখানে stack pointer এর value **2099H** সেট করা হয়।

---

# 2. Stack Operation

Stack এ data store ও retrieve করার জন্য দুটি instruction ব্যবহার করা হয়।

## PUSH Instruction

Register pair এর data stack এ store করার জন্য PUSH ব্যবহার করা হয়।

Example:

```
LXI SP, 2099H
LXI H, 42F2H
PUSH H
```

### PUSH Operation

```
SP = 2099

After PUSH

Address    Data
2098       42
2097       F2
```

Steps:

1. SP → 2098 (decrement)
    
2. H register store
    
3. SP → 2097 (decrement)
    
4. L register store
    

---

## POP Instruction

Stack থেকে data register pair এ ফিরিয়ে আনার জন্য POP ব্যবহার করা হয়।

Example:

```
POP H
```

### POP Operation

```
Address    Data
2098       42
2097       F2
```

Steps:

1. L ← Memory(2097)
    
2. SP increment → 2098
    
3. H ← Memory(2098)
    
4. SP increment → 2099
    

---

# 3. Subroutine

Subroutine হলো একটি **instruction group** যা main program থেকে আলাদা করে লেখা হয় এবং নির্দিষ্ট কাজ বারবার করার জন্য ব্যবহার করা হয়।

যখন main program subroutine call করে, তখন program execution subroutine এ চলে যায় এবং কাজ শেষ হলে আবার main program এ ফিরে আসে।

Subroutine ব্যবহার করার জন্য দুটি instruction আছে:

1. **CALL**
    
2. **RET**
    

---

# 4. CALL Instruction

CALL instruction subroutine execute করার জন্য ব্যবহার করা হয়।

Syntax:

```
CALL address
```

Example:

```
CALL 2050H
```

Operation:

1. Next instruction address stack এ store হয়
    
2. Program control subroutine address এ চলে যায়
    

CALL instruction একটি **3-byte instruction**।

---

# 5. RET Instruction

RET instruction subroutine শেষ হলে main program এ ফিরে আসে।

Syntax:

```
RET
```

Operation:

1. Stack থেকে return address নেওয়া হয়
    
2. Program execution আবার main program এ চলে যায়
    

RET একটি **1-byte instruction**।

---

# 6. Example Program

```
LXI SP, 2099H
CALL DELAY
MOV A,B

DELAY:
MVI C,FFH
DCR C
JNZ DELAY
RET
```

Program Flow

```
Main Program
     ↓
CALL DELAY
     ↓
Subroutine Execution
     ↓
RET
     ↓
Back to Main Program
```

---

# 7. Advantages of Subroutine

1. Complex program ছোট ছোট অংশে ভাগ করা যায়
    
2. Code reuse করা যায়
    
3. Program size কমে
    
4. Debugging সহজ হয়
    

---

✅ যদি চাও আমি তোমাকে **8085 Stack & Subroutine এর “1 page super-short revision sheet (exam এর আগে 2 মিনিটে revise)”** বানিয়ে দিতে পারি। এটা exam এর আগে খুব কাজে লাগে।