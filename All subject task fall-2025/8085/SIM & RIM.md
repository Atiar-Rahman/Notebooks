
# 1. SIM Instruction

**SIM = Set Interrupt Mask**

SIM হলো একটি **1-byte instruction** যা interrupt system control করতে ব্যবহার করা হয়। 

Opcode:

```id="c5nl0m"
SIM → 30H
```

SIM execute করার সময় **Accumulator (A register)** এর bit গুলো দেখে microprocessor decide করে কি কাজ হবে। তাই SIM চালানোর আগে accumulator এ value load করতে হয়। 

---

# 2. Interrupt Masking / Unmasking

**Masking** মানে interrupt **disable করা**
**Unmasking** মানে interrupt **enable করা**

SIM দিয়ে ৩টা interrupt control করা যায়:

```
RST 7.5
RST 6.5
RST 5.5
```

### Example

ধরো:

```id="0xd4n7"
MVI A,08H
SIM
```

Meaning:

* Accumulator এর bit অনুযায়ী interrupt mask/unmask হবে।

Example scenario:

```
RST7.5 → enabled
RST6.5 → disabled
RST5.5 → disabled
```

---

# 3. Reset RST7.5 Flip-Flop

SIM দিয়ে **RST7.5 interrupt reset** করা যায়।

### Example

```id="8ddhx9"
MVI A,10H
SIM
```

Meaning:

```
RST7.5 reset
```

---

# 4. Serial Output Data

SIM instruction **serial data output** করার জন্যও ব্যবহার হয়।

Example:

```id="mqeqt6"
MVI A,40H
SIM
```

Meaning:

```
Serial output enable
```

---

# 5. RIM Instruction

**RIM = Read Interrupt Mask**

RIM একটি **1-byte instruction** যা interrupt status read করতে ব্যবহার করা হয়। 

Opcode:

```id="rqqof9"
RIM → 20H
```

RIM execute করার পর **Accumulator এ interrupt status store হয়**।

---

# 6. Check Interrupt Mask Status

RIM দিয়ে জানা যায়:

```
RST7.5 masked ?
RST6.5 masked ?
RST5.5 masked ?
```

### Example

```id="7y06ta"
RIM
```

After execution:

```
A register = interrupt status
```

Example:

```
A = 00000101
```

Meaning:

```
RST7.5 → masked
RST6.5 → unmasked
RST5.5 → masked
```

---

# 7. Check Interrupt Enable Status

RIM দিয়ে জানা যায় **interrupt system enable আছে কি না**।

### Example

```id="u63gsq"
RIM
```

Accumulator bit check করে বুঝা যায়:

```
Interrupt enabled / disabled
```

---

# 8. Check Pending Interrupt

RIM দিয়ে বোঝা যায় **কোন interrupt pending আছে কি না**।

Example:

```id="9j77u5"
RIM
```

Result:

```
RST7.5 pending
RST6.5 not pending
RST5.5 not pending
```

---

# 9. Serial Input

RIM instruction **serial data input** করার জন্য ব্যবহার করা হয়।

Example:

```id="8jexl9"
RIM
```

Result:

```
Serial input data → Accumulator
```

---

# 10. Difference Between SIM and RIM

| Feature     | SIM                    | RIM                    |
| ----------- | ---------------------- | ---------------------- |
| Full form   | Set Interrupt Mask     | Read Interrupt Mask    |
| Purpose     | Interrupt control      | Interrupt status read  |
| Operation   | Mask/Unmask interrupts | Check interrupt status |
| Data source | Accumulator input      | Accumulator output     |
| Serial data | Serial output          | Serial input           |
| Opcode      | 30H                    | 20H                    |



---

# Simple Program Example

```id="pn5um2"
MVI A,08H
SIM

RIM
MOV B,A
```

Meaning:

1. Interrupt mask set করা
2. Interrupt status read করা
3. Status B register এ store করা

---

---

# 1. SIM Instruction (Set Interrupt Mask)

**SIM = Set Interrupt Mask**

SIM instruction ব্যবহার করা হয়:

* Interrupt **mask / unmask** করতে
* **RST7.5 reset** করতে
* **Serial output** করতে

এটি একটি **1-byte instruction** এবং opcode **30H**। 

---

# SIM Bit Structure (Accumulator)

SIM execute করার সময় **Accumulator (A register)** এর bit গুলো নিচের মত কাজ করে।

```
D7   D6   D5   D4   D3   D2   D1   D0
SOD  SOE   X  R7.5  MSE  M7.5 M6.5 M5.5
```

### Bit Explanation

| Bit | Name | Meaning                |
| --- | ---- | ---------------------- |
| D7  | SOD  | Serial Output Data     |
| D6  | SOE  | Serial Output Enable   |
| D5  | X    | Don't care             |
| D4  | R7.5 | Reset RST7.5 flip-flop |
| D3  | MSE  | Mask Set Enable        |
| D2  | M7.5 | Mask RST7.5            |
| D1  | M6.5 | Mask RST6.5            |
| D0  | M5.5 | Mask RST5.5            |



---

## Example (SIM)

Program:

```
MVI A,0EH
SIM
```

Binary of 0EH

```
00001110
```

Meaning:

```
MSE = 1  → Mask enable
M7.5 = 1 → Mask RST7.5
M6.5 = 1 → Mask RST6.5
M5.5 = 0 → Unmask RST5.5
```

Result:

```
RST7.5 → Disabled
RST6.5 → Disabled
RST5.5 → Enabled
```

---

# 2. RIM Instruction (Read Interrupt Mask)

**RIM = Read Interrupt Mask**

RIM instruction ব্যবহার করা হয়:

* Interrupt **masked / unmasked status** check করতে
* **Interrupt enabled কিনা** check করতে
* **Pending interrupt** check করতে
* **Serial input** পড়তে

এটি একটি **1-byte instruction** এবং opcode **20H**। 

---

# RIM Bit Structure (Accumulator)

RIM execute করার পরে **Accumulator এ interrupt status পাওয়া যায়।**

```
D7   D6   D5   D4   D3   D2   D1   D0
SID  P7.5 P6.5 P5.5 IE   M7.5 M6.5 M5.5
```

### Bit Explanation

| Bit | Meaning                 |
| --- | ----------------------- |
| D7  | Serial Input Data       |
| D6  | RST7.5 Pending          |
| D5  | RST6.5 Pending          |
| D4  | RST5.5 Pending          |
| D3  | Interrupt Enable Status |
| D2  | Mask RST7.5             |
| D1  | Mask RST6.5             |
| D0  | Mask RST5.5             |



---

## Example (RIM)

Program:

```
RIM
MOV B,A
```

ধরো accumulator এ result:

```
01001001
```

Meaning:

```
SID = 0
RST7.5 pending = 1
RST6.5 pending = 0
RST5.5 pending = 0
Interrupt enabled = 1
RST7.5 unmasked
RST6.5 unmasked
RST5.5 masked
```

---

# 3. Easy Exam Trick (Remember Quickly)

### SIM → **SET**

```
SIM = Set Interrupt Mask
```

Meaning:

```
Interrupt control / change
```

### RIM → **READ**

```
RIM = Read Interrupt Mask
```

Meaning:

```
Interrupt status check
```

---

### Simple Memory Trick

```
SIM → Set
RIM → Read
```

```
SIM = Interrupt control
RIM = Interrupt status
```

---

# 4. Short Comparison (Exam Table)

| Feature     | SIM                | RIM                   |
| ----------- | ------------------ | --------------------- |
| Full form   | Set Interrupt Mask | Read Interrupt Mask   |
| Opcode      | 30H                | 20H                   |
| Function    | Interrupt control  | Interrupt status read |
| Data        | Accumulator input  | Accumulator output    |
| Serial data | Output             | Input                 |



---
