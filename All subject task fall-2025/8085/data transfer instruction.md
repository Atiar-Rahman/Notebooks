## 📘 Data Transfer Instructions (8085 Microprocessor)

**Data Transfer Instructions** হলো সেই instruction গুলো যেগুলো শুধু **data এক জায়গা থেকে আরেক জায়গায় পাঠায়**, কিন্তু **data পরিবর্তন করে না** (no arithmetic / no logical operation).

---

## 🔹 1️⃣ MOV Instruction

![Image](https://www.tutorialspoint.com/assets/questions/media/15682/architecture_of_8085.jpg)

![Image](https://www.tutorialspoint.com/assets/questions/media/15705/40_1.jpg)

![Image](https://scanftree.com/microprocessor/Architechture-of-8085-block.PNG)

![Image](https://static.righto.com/images/8085/register_a_act.png)

### 👉 Format:

```
MOV destination, source
```

### 👉 কাজ:

একটা register থেকে অন্য register-এ data কপি করে।

### 👉 Example:

```
MOV A, B   ; B এর data A তে যাবে
MOV D, C
MOV M, A   ; A → memory (HL address)
```

### 👉 Important:

* Register ↔ Register
* Register ↔ Memory (HL pair ব্যবহার করে)
* Memory ↔ Register
* Memory ↔ Memory ❌ (possible না)

---

## 🔹 2️⃣ MVI (Move Immediate)

### 👉 Format:

```
MVI register, 8-bit data
```

### 👉 কাজ:

সরাসরি 8-bit data register বা memory তে পাঠায়।

### 👉 Example:

```
MVI A, 25H
MVI B, 0AH
MVI M, 55H
```

---

## 🔹 3️⃣ LXI (Load Register Pair Immediate)

### 👉 Format:

```
LXI rp, 16-bit data
```

### 👉 কাজ:

Register pair (BC / DE / HL / SP) এ 16-bit data লোড করে।

### 👉 Example:

```
LXI H, 2050H
LXI B, 1234H
LXI SP, 3000H
```

---

## 🔹 4️⃣ LDA (Load Accumulator Direct)

### 👉 Format:

```
LDA 16-bit address
```

### 👉 কাজ:

Memory থেকে Accumulator (A) তে data লোড করে।

### 👉 Example:

```
LDA 2050H
```

👉 2050H memory location এর data → A তে যাবে

---

## 🔹 5️⃣ STA (Store Accumulator Direct)

### 👉 Format:

```
STA 16-bit address
```

### 👉 কাজ:

Accumulator এর data memory তে store করে।

### 👉 Example:

```
STA 3050H
```

👉 A এর data → 3050H memory তে যাবে

---

## 🔹 6️⃣ LHLD (Load HL Direct)

### 👉 Format:

```
LHLD 16-bit address
```

### 👉 কাজ:

Memory থেকে HL pair এ data লোড করে।

👉 address → L
👉 address+1 → H

---

## 🔹 7️⃣ SHLD (Store HL Direct)

### 👉 Format:

```
SHLD 16-bit address
```

### 👉 কাজ:

HL pair এর data memory তে store করে।

---

## 🔹 8️⃣ LDAX

### 👉 Format:

```
LDAX B
LDAX D
```

### 👉 কাজ:

BC বা DE register pair এর address থেকে A তে data লোড করে।

---

## 🔹 9️⃣ STAX

### 👉 Format:

```
STAX B
STAX D
```

### 👉 কাজ:

Accumulator এর data BC বা DE address এ store করে।

---

# 🔥 Summary Table

| Instruction | কাজ                          |
| ----------- | ---------------------------- |
| MOV         | Register ↔ Register / Memory |
| MVI         | Immediate 8-bit load         |
| LXI         | Immediate 16-bit load        |
| LDA         | Memory → A                   |
| STA         | A → Memory                   |
| LHLD        | Memory → HL                  |
| SHLD        | HL → Memory                  |
| LDAX        | (BC/DE) → A                  |
| STAX        | A → (BC/DE)                  |

---

## 🎯 Important Points (Exam Focused)

* Data Transfer instruction **flag change করে না**
* Memory access এর জন্য HL pair বেশি ব্যবহার হয়
* Memory ↔ Memory direct possible না
* LXI শুধু register pair এর জন্য

---


# **8085 Data Transfer Instructions** গুলো একদম **Memory Level Diagram সহ** বুঝবো — যেন exam এ লিখতে পারো 🔥

---

# 🔹 1️⃣ MOV Instruction (Register ↔ Register)

## Example:

```
MOV A, B
```

## 🔎 কাজ:

B register এর data → A register এ কপি হবে

### 🧠 Memory Level Diagram:

```
Before:
B = 45H
A = 00H

Operation:
A ← B

After:
B = 45H
A = 45H
```

👉 **Note:**

* Data change হয় না
* Flag change হয় না

---

# 🔹 2️⃣ MOV M, A  (Register → Memory)

## Example:

```
MOV M, A
```

ধরি:

```
HL = 2050H
A = 32H
```

### 🧠 Diagram:

```
Address Bus → 2050H
Data Bus → 32H

Memory[2050H] = 32H
```

👉 M মানে memory location pointed by HL

---

# 🔹 3️⃣ MVI Instruction

## Example:

```
MVI B, 25H
```

### 🧠 Diagram:

```
Immediate Data (25H) → B register

Before:
B = 00H

After:
B = 25H
```

👉 8-bit data সরাসরি register এ যায়

---

# 🔹 4️⃣ LXI Instruction (16-bit Load)

## Example:

```
LXI H, 2050H
```

### 🧠 Diagram:

```
High byte → H = 20H
Low byte  → L = 50H

HL = 2050H
```

👉 Register pair এ 16-bit data লোড হয়

---

# 🔹 5️⃣ LDA (Load Accumulator Direct)

## Example:

```
LDA 3050H
```

ধরি:

```
Memory[3050H] = 7AH
```

### 🧠 Diagram:

```
Address Bus → 3050H
Data Bus ← 7AH

A ← 7AH
```

👉 Memory → Accumulator

---

# 🔹 6️⃣ STA (Store Accumulator Direct)

## Example:

```
STA 3050H
```

ধরি:

```
A = 9CH
```

### 🧠 Diagram:

```
Address Bus → 3050H
Data Bus → 9CH

Memory[3050H] = 9CH
```

👉 Accumulator → Memory

---

# 🔹 7️⃣ LHLD

## Example:

```
LHLD 2050H
```

ধরি:

```
Memory[2050H]   = 34H
Memory[2051H]   = 12H
```

### 🧠 Diagram:

```
L ← Memory[2050H] = 34H
H ← Memory[2051H] = 12H

HL = 1234H
```

👉 Lower address → L
👉 Next address → H

---

# 🔹 8️⃣ SHLD

## Example:

```
SHLD 2050H
```

ধরি:

```
HL = 1234H
(H=12H, L=34H)
```

### 🧠 Diagram:

```
Memory[2050H] = 34H
Memory[2051H] = 12H
```

👉 L আগে যায়, তারপর H

---

# 🔹 9️⃣ LDAX

## Example:

```
LDAX B
```

ধরি:

```
BC = 3000H
Memory[3000H] = 88H
```

### 🧠 Diagram:

```
Address from BC → 3000H
A ← Memory[3000H] = 88H
```

👉 BC বা DE pair ব্যবহার হয়

---

# 🔹 🔟 STAX

## Example:

```
STAX D
```

ধরি:

```
DE = 4000H
A = 55H
```

### 🧠 Diagram:

```
Memory[4000H] = 55H
```

---

# 🎯 Exam Important Notes

✅ Data Transfer instruction flag change করে না
✅ Memory ↔ Memory direct possible না
✅ HL pair memory pointer হিসেবে বেশি ব্যবহৃত হয়
✅ LXI শুধু register pair এর জন্য

---

তুমি একদম ঠিক বলেছো 👍
8085 এ **Flag Register 8-bit হলেও সবগুলো bit flag হিসেবে ব্যবহার হয় না**।

এখন পুরো বিষয়টা পরিষ্কারভাবে diagram সহ বুঝি 👇

---

# 📌 8085 Flag Register

![Image](https://images.saymedia-content.com/.image/ar_16%3A9%2Cc_fill%2Ccs_srgb%2Cq_auto%3Aeco%2Cw_1200/MTc2MjcyMzk5ODM3MTc3MDIy/flag-register-of-8085.png)

![Image](https://qph.cf2.quoracdn.net/main-qimg-7ed3cb68cedcfe145c1b54ce0d2f2dc0)

![Image](https://2.bp.blogspot.com/-Ub-uMBcRKdI/VTNmxslcz-I/AAAAAAAAEUQ/PQnffddFT3I/s1600/Programming%2BModel.jpg)

## 🔹 Flag Register = 8 bit

| Bit | 7 | 6 | 5 | 4  | 3 | 2 | 1 | 0  |
| --- | - | - | - | -- | - | - | - | -- |
| Use | S | Z | X | AC | X | P | X | CY |

👉 এখানে

* **X = Unused bit**
* মোট 8 bit
* কিন্তু **মাত্র 5টি flag active**

---

# 🔹 কেন 8 bit কিন্তু 5টা flag?

কারণ 8085 একটি **8-bit processor**।
Processor internal architecture অনুযায়ী register size 8 bit।

কিন্তু Intel শুধুমাত্র দরকারি 5টা condition flag implement করেছে।

---

# 🔹 এখন প্রতিটা Flag ব্যাখ্যা করি

---

## 1️⃣ Carry Flag (CY)

📍 Bit position = 0

### কাজ:

যদি addition এর সময় carry বের হয়
বা subtraction এ borrow লাগে

### Example:

```id="j4z8p3"
FFH + 01H = 100H
```

👉 Carry = 1

---

## 2️⃣ Auxiliary Carry (AC)

📍 Bit position = 4

### কাজ:

Lower nibble (D3 → D4) এ carry হলে

### Example:

```id="c0g4mk"
0FH + 01H = 10H
```

👉 AC = 1

👉 Mainly used in **BCD arithmetic (DAA instruction)**

---

## 3️⃣ Sign Flag (S)

📍 Bit position = 7

### কাজ:

Result এর MSB (Most Significant Bit) যদি 1 হয়

* MSB = 1 → Negative number
* MSB = 0 → Positive number

---

## 4️⃣ Zero Flag (Z)

📍 Bit position = 6

### কাজ:

Result যদি 00H হয়

```id="4xchle"
25H - 25H = 00H
```

👉 Z = 1

---

## 5️⃣ Parity Flag (P)

📍 Bit position = 2

### কাজ:

Result এ 1 এর সংখ্যা count করে

* Even number of 1 → P = 1
* Odd number of 1 → P = 0

Example:

```id="pahq5e"
00000011 → 2টা 1 → Even → P = 1
```

---

# 🔥 Important Concept

### Flag Register + Accumulator = PSW

PSW = Program Status Word

```id="b2r8xz"
PSW = A + Flag Register
```

Stack operation এ:

```id="g52y0k"
PUSH PSW
POP PSW
```

---

# 🎯 Exam লিখার জন্য সংক্ষিপ্ত উত্তর

* 8085 এ flag register 8-bit
* কিন্তু 5টি flag implemented
* এগুলো arithmetic & logical operation এর condition indicate করে
* Flags automatically update হয় operation শেষে

---
