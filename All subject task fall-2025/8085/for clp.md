# 🖥️ 8086 `MOV` Operation (Step-by-Step)

`MOV` instruction দিয়ে এক জায়গা থেকে অন্য জায়গায় **data copy** করা হয়।
⚠️ এটা **copy করে**, source পরিবর্তন হয় না।

---

## 🔹 1️⃣ Register → Register

```assembly
MOV AX, BX
```

### 👉 Step by Step

ধরি:

* AX = 0000H
* BX = 0005H

Instruction run করলে:

* AX = 0005H
* BX = 0005H (same থাকে)

✔ BX change হয় না
✔ AX নতুন value পায়

---

## 🔹 2️⃣ Immediate → Register

```assembly
MOV AX, 0008H
```

👉 AX এর ভিতরে সরাসরি 0008H ঢুকে যাবে।

---

## 🔹 3️⃣ Memory → Register

```assembly
MOV AX, [2000H]
```

👉 Memory address 2000H এ যা আছে সেটা AX এ যাবে।

ধরি:

* [2000H] = 0003H
* তাহলে AX = 0003H

---

## 🔹 4️⃣ Register → Memory

```assembly
MOV [2000H], AX
```

👉 AX এর value memory 2000H তে store হবে।

---

# ⚠️ Important Rules (Exam Favourite)

❌ Memory → Memory direct allowed না

```assembly
MOV [2000H], [3000H]   ; ❌ Invalid
```

✔ প্রথমে register এ নিতে হবে:

```assembly
MOV AX, [3000H]
MOV [2000H], AX
```

---

# 🔥 8086 EMU তে Step দেখার উপায়

1. Code লিখো
2. Assemble করো
3. Step button চাপো
4. Registers window observe করো
5. Memory window check করো

---

# 🎯 Small Working Program

```assembly
MOV AX, 0005H
MOV BX, 0003H
MOV CX, AX
HLT
```

শেষে:

* AX = 0005H
* BX = 0003H
* CX = 0005H

---

# 🔥 8086 Single-Operand Instructions (একটা Operand লাগে)

Single instruction মানে যেগুলোতে **একটাই operand** থাকে (বা implicit থাকে)।
এগুলো exam এ খুব common আসে 👇

---

## 🔹 1️⃣ INC (Increment)

```assembly
INC AX
```

👉 AX = AX + 1

---

## 🔹 2️⃣ DEC (Decrement)

```assembly
DEC BX
```

👉 BX = BX - 1

---

## 🔹 3️⃣ NOT (1’s Complement)

```assembly
NOT AX
```

👉 AX এর সব bit উল্টে যাবে

---

## 🔹 4️⃣ NEG (2’s Complement)

```assembly
NEG AX
```

👉 AX = 0 - AX

---

## 🔹 5️⃣ MUL (Unsigned Multiply)

```assembly
MUL BX
```

👉 AX × BX
Result DX:AX এ যায়

---

## 🔹 6️⃣ DIV (Unsigned Divide)

```assembly
DIV BX
```

👉 AX ÷ BX
Quotient → AX
Remainder → DX

---

## 🔹 7️⃣ PUSH

```assembly
PUSH AX
```

👉 AX stack এ যায়

---

## 🔹 8️⃣ POP

```assembly
POP AX
```

👉 Stack থেকে AX এ আসে

---

## 🔹 9️⃣ JMP (Unconditional Jump)

```assembly
JMP LABEL
```

👉 Program ওই label এ চলে যাবে

---

## 🔹 🔟 CALL

```assembly
CALL PROC1
```

👉 Procedure call করে

---

## 🔹 1️⃣1️⃣ RET

```assembly
RET
```

👉 Procedure থেকে ফিরে আসে

---

# 📌 Important Viva Point

✔ INC / DEC → Carry flag change করে না
✔ MUL / DIV → AX, DX automatically use করে
✔ PUSH / POP → SP register use করে
✔ JMP → IP change করে

---

# 🎯 Very Short Exam Answer

Single operand instructions হলো যেগুলোতে একটাই operand লাগে।
Examples: INC, DEC, NOT, NEG, MUL, DIV, PUSH, POP, JMP, CALL, RET.

---
না ❌ — **Single instruction সবসময় AX এর সাথে operation হবে না।**

এটা একটা খুব common ভুল ধারণা।

---

# 🔥 Clear Explanation

Single operand instruction মানে:
👉 একটাই operand থাকবে
👉 কিন্তু সেটা যেকোনো valid register / memory হতে পারে

AX হওয়া বাধ্যতামূলক না।

---

# ✅ Example দেখে বুঝি

## 🔹 1️⃣ INC

```assembly
INC BX
```

✔ BX = BX + 1
👉 এখানে AX ব্যবহার হয়নি

---

## 🔹 2️⃣ DEC

```assembly
DEC CX
```

✔ CX = CX - 1
👉 AX দরকার নেই

---

## 🔹 3️⃣ NOT

```assembly
NOT DX
```

✔ DX এর bit উল্টে যাবে

---

# ⚠️ কিন্তু কিছু instruction AX use করে

## 🔹 MUL (Special Case)

```assembly
MUL BX
```

এখানে:

AX × BX
Result → DX:AX

👉 এখানে AX automatically use হয়
👉 কারণ architecture এ এমন design করা

---

## 🔹 DIV (Special Case)

```assembly
DIV BX
```

AX ÷ BX
Quotient → AX
Remainder → DX

👉 এখানে AX লাগে

---

# 🎯 Rule মনে রাখো

| Instruction Type      | AX বাধ্যতামূলক? |
| --------------------- | --------------- |
| INC / DEC / NOT / NEG | ❌ না            |
| MUL / DIV             | ✅ হ্যাঁ         |
| PUSH / POP            | ❌ না            |
| JMP                   | ❌ না            |

---

# 📌 Viva Ready Answer (Short)

না, single operand instruction সবসময় AX এর সাথে কাজ করে না।
শুধু MUL এবং DIV এর মতো কিছু instruction এ AX automatically ব্যবহৃত হয়।

---

চাও কি এখন:

* 🔹 MUL / DIV full example step by step?
* 🔹 Flags change table?
* 🔹 Instruction classification chart?
* 🔹 8085 এর single instruction list?

বললেই next clear করে দিচ্ছি 🚀

---------
# 🔥 8086 `MUL` / `DIV` Full Example (Step-by-Step)

আমরা Intel 8086 এর `MUL` ও `DIV` দেখবো।  
⚠️ মনে রাখবে — এই দুইটা instruction এ **AX (এবং DX)** automatically use হয়।

---

# 🟢 1️⃣ MUL (Unsigned Multiply)

## ✅ Example:

5 × 3

```assembly
MOV AX, 0005H
MOV BX, 0003H
MUL BX
HLT
```

---

## 🔎 Step by Step Execution

### ▶ Step 1

```
MOV AX,0005H
```

AX = 0005H

---

### ▶ Step 2

```
MOV BX,0003H
```

BX = 0003H

---

### ▶ Step 3

```
MUL BX
```

👉 Internally করে:  
AX × BX  
= 0005H × 0003H  
= 000FH (15 decimal)

### ✔ Result কোথায় যাবে?

Result → DX:AX

|Register|Value|
|---|---|
|AX|000FH|
|DX|0000H|

(কারণ result 16-bit এর ভিতরে fit করেছে)

---

## 📌 Important Rule

- 16-bit × 16-bit
    
- Result 32-bit হতে পারে
    
- তাই DX:AX pair use হয়
    

---

# 🔵 2️⃣ DIV (Unsigned Divide)

## ✅ Example:

15 ÷ 3

```assembly
MOV AX, 000FH
MOV BX, 0003H
DIV BX
HLT
```

---

## 🔎 Step by Step Execution

### ▶ Step 1

```
MOV AX,000FH
```

AX = 000FH (15)

---

### ▶ Step 2

```
MOV BX,0003H
```

BX = 0003H (3)

---

### ▶ Step 3

```
DIV BX
```

👉 Internally করে:  
AX ÷ BX  
= 15 ÷ 3  
= 5

### ✔ Result কোথায় যাবে?

|Register|Value|
|---|---|
|AX|0005H (Quotient)|
|DX|0000H (Remainder)|

---

# ⚠️ Very Important (Exam Favourite)

## 🔴 যদি remainder থাকে?

Example: 17 ÷ 3

```assembly
MOV AX,0011H
MOV BX,0003H
DIV BX
```

Result:

| Register | Value |
| -------- | ----- |
| AX       | 0005H |
| DX       | 0002H |

👉 Quotient → AX  
👉 Remainder → DX

---

# 🧠 Summary Table

| Instruction | Automatically Uses | Result Stored |
| ----------- | ------------------ | ------------- |
| MUL         | AX                 | DX:AX         |
| DIV         | AX                 | AX & DX       |

---

# 🎯 Viva Ready 3 Line Answer

MUL instruction AX কে implicit operand হিসেবে ব্যবহার করে এবং result DX:AX এ store হয়।  
DIV instruction AX কে dividend হিসেবে ব্যবহার করে।  
Quotient AX এ এবং remainder DX এ যায়।

---

চাও কি এখন:

- 🔹 8-bit MUL/DIV example?
    
- 🔹 Signed multiplication (IMUL/IDIV)?
    
- 🔹 Overflow case explanation?
    
- 🔹 Practice problem solve?
    

বললেই next level 🚀

----
# 🔥 8086 8-bit `MUL` / `DIV` (Step-by-Step)

আমরা Intel 8086 এর **8-bit** version দেখবো।
⚠️ 8-bit হলে **AL** automatically use হয়, আর result **AX** এ যায়।

---

# 🟢 1️⃣ 8-bit `MUL` (Unsigned)

## ✅ Example: 5 × 3

```assembly
MOV AL, 05H
MOV BL, 03H
MUL BL
HLT
```

## 🔎 Step by Step

### ▶ Step 1

`MOV AL,05H`
AL = 05H

### ▶ Step 2

`MOV BL,03H`
BL = 03H

### ▶ Step 3

`MUL BL`

👉 Internally:
AL × BL = 05H × 03H = 0FH (15 decimal)

### ✔ Result কোথায় যাবে?

8-bit × 8-bit ⇒ 16-bit result
Result → **AX**

| Register | Value |
| -------- | ----- |
| AL       | 0FH   |
| AH       | 00H   |
| AX       | 000FH |

---

## ⚠️ Overflow Case

Example: 20H × 10H
Result বড় হলে AH ≠ 00H হবে (মানে full 16-bit result লাগবে)।

---

# 🔵 2️⃣ 8-bit `DIV` (Unsigned)

## ✅ Example: 15 ÷ 3

```assembly
MOV AX, 000FH
MOV BL, 03H
DIV BL
HLT
```

## 🔎 Step by Step

### ▶ Step 1

AX = 000FH (Dividend)

⚠️ 8-bit division এ dividend হয় **AX**
(AL না, পুরো AX)

### ▶ Step 2

`DIV BL`

👉 Internally:
AX ÷ BL = 15 ÷ 3 = 5

### ✔ Result কোথায় যাবে?

| Register | Value           |
| -------- | --------------- |
| AL       | 05H (Quotient)  |
| AH       | 00H (Remainder) |

---

## 🔴 Remainder Example

17 ÷ 3

```assembly
MOV AX, 0011H
MOV BL, 03H
DIV BL
```

Result:

| Register | Value |
| -------- | ----- |
| AL       | 05H   |
| AH       | 02H   |

👉 Quotient → AL
👉 Remainder → AH

---

# 🧠 Quick Comparison

| Operation | Implicit Register | Result Stored |
| --------- | ----------------- | ------------- |
| 8-bit MUL | AL                | AX            |
| 8-bit DIV | AX                | AL & AH       |

---

# 🎯 Viva Ready 3 Line

8-bit MUL এ AL implicit operand এবং result AX এ যায়।
8-bit DIV এ AX dividend হিসেবে ব্যবহার হয়।
Quotient AL এ এবং remainder AH এ store হয়।

---

চাও কি এখন:

* 🔹 Signed IMUL/IDIV?
* 🔹 Error/Divide overflow case?
* 🔹 Full flags effect table?
* 🔹 Practice problem solve করে দেখবো?

বললেই এগাই 🚀


