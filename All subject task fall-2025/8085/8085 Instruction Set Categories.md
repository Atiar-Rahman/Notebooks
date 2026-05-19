
# 📘 8085 Instruction Set Categories

## 1️⃣ Data Transfer Instructions (83 instructions | 13 types)

👉 **Purpose:** Copy data from one place to another.
👉 **Important:** Data is copied, not changed.

### Common Instructions:

* **MOV** – Move data between registers
* **MVI** – Move immediate data to register
* **LXI** – Load register pair with 16-bit data
* **LDA / STA** – Load/Store accumulator from/to memory
* **LHLD / SHLD** – Load/Store HL pair direct
* **LDAX / STAX** – Load/Store using register pair
* **XCHG** – Exchange HL and DE

### Example:

```
MVI A, 25H   ; Load 25H into accumulator
MOV B, A     ; Copy A to B
```

---

## 2️⃣ Arithmetic Instructions (62 instructions | 14 types)

👉 **Purpose:** Perform mathematical operations.

### Common Instructions:

* **ADD** – Add register to accumulator
* **ADI** – Add immediate data
* **SUB** – Subtract register from accumulator
* **SUI** – Subtract immediate data
* **INR / DCR** – Increment / Decrement
* **INX / DCX** – Increment / Decrement register pair
* **DAD** – 16-bit addition
* **CMA** – Complement accumulator
* **DAA** – Decimal adjust accumulator

### Example:

```
MVI A, 10H
ADI 05H     ; A = 10H + 05H = 15H
```

---

## 3️⃣ Logical Instructions (43 instructions | 15 types)

👉 **Purpose:** Perform logical operations (bitwise).

### Common Instructions:

* **ANA** – AND operation
* **ANI** – AND immediate
* **ORA** – OR operation
* **ORI** – OR immediate
* **XRA** – XOR operation
* **XRI** – XOR immediate
* **CMP** – Compare
* **RLC / RRC / RAL / RAR** – Rotate accumulator
* **CMA** – Complement accumulator

### Example:

```
MVI A, 0FH
ANI 03H     ; A = 03H
```

---

## 4️⃣ Stack Instructions (15 instructions | 9 types)

👉 **Purpose:** Work with stack memory (LIFO – Last In First Out).

### Common Instructions:

* **PUSH** – Put data into stack
* **POP** – Get data from stack
* **XTHL** – Exchange HL with top of stack
* **SPHL** – Copy HL to Stack Pointer

### Example:

```
PUSH B
POP D
```

---

## 5️⃣ Branch Instructions (36 instructions | 8 types)

👉 **Purpose:** Change program execution path (jump or call).

### Common Instructions:

* **JMP** – Unconditional jump
* **JZ / JNZ** – Jump if Zero / Not Zero
* **JC / JNC** – Jump if Carry / Not Carry
* **JP / JM** – Jump if Positive / Minus
* **CALL** – Call subroutine
* **RET** – Return from subroutine

### Example:

```
JZ 2000H
```

---

## 6️⃣ I/O Instructions (2 instructions | 2 types)

👉 **Purpose:** Communicate with input/output devices.

### Instructions:

* **IN** – Read from input port
* **OUT** – Send data to output port

### Example:

```
IN 01H
OUT 02H
```

---

## 7️⃣ Interrupt Instructions (5 instructions | 5 types)

👉 **Purpose:** Handle interrupt signals.

### Instructions:

* **RST 0**
* **RST 1**
* **RST 2**
* **RST 3**
* **RST 4** (up to RST 7 in full set)

👉 RST = Restart (call fixed memory location)

---

# 📊 Summary Table

| Category      | Purpose              | Example   |
| ------------- | -------------------- | --------- |
| Data Transfer | Copy data            | MOV, MVI  |
| Arithmetic    | Math operations      | ADD, SUB  |
| Logical       | Bit operations       | AND, XOR  |
| Stack         | Stack handling       | PUSH, POP |
| Branch        | Jump/Call            | JMP, JZ   |
| I/O           | Device communication | IN, OUT   |
| Interrupt     | Interrupt handling   | RST       |

---


## 📘 Data Transfer Instructions (8085)

Data Transfer Instructions in the **Intel 8085** are used to **copy data from one location to another**.

👉 Important point:

- Data is **copied**, not deleted from the source.
    
- The original value remains unchanged.
    

---

# 🔹 Types of Data Transfer Instructions (with examples)

## 1️⃣ MOV (Move Register to Register)

**Purpose:** Copy data from one register to another.

**Syntax:**

```
MOV destination, source
```

**Example:**

```
MOV B, C
```

👉 Copies data from register C to register B.  
👉 C remains unchanged.

---

## 2️⃣ MVI (Move Immediate Data)

**Purpose:** Load 8-bit immediate data into a register or memory.

**Syntax:**

```
MVI register, data
```

**Example:**

```
MVI A, 25H
```

👉 Loads 25H into accumulator (A).

Another example:

```
MVI M, 10H
```

👉 Stores 10H into memory location pointed by HL pair.

---

## 3️⃣ LXI (Load Register Pair Immediate)

**Purpose:** Load 16-bit data into a register pair.

**Syntax:**

```
LXI register_pair, 16-bit data
```

**Example:**

```
LXI H, 2500H
```

👉 Loads 25H into H and 00H into L.

---

## 4️⃣ LDA (Load Accumulator Direct)

**Purpose:** Load accumulator from a memory location.

**Syntax:**

```
LDA address
```

**Example:**

```
LDA 2050H
```

👉 Loads A with data stored at memory location 2050H.

---

## 5️⃣ STA (Store Accumulator Direct)

**Purpose:** Store accumulator data into memory.

**Syntax:**

```
STA address
```

**Example:**

```
STA 3000H
```

👉 Stores accumulator value into memory location 3000H.

---

## 6️⃣ LHLD (Load HL Direct)

**Purpose:** Load HL pair directly from memory.

**Example:**

```
LHLD 2500H
```

👉 L ← content of 2500H  
👉 H ← content of 2501H

---

## 7️⃣ SHLD (Store HL Direct)

**Purpose:** Store HL pair directly into memory.

**Example:**

```
SHLD 2600H
```

👉 Stores L into 2600H  
👉 Stores H into 2601H

---

## 8️⃣ LDAX (Load Accumulator Indirect)

**Purpose:** Load accumulator using register pair (BC or DE).

**Example:**

```
LDAX B
```

👉 A ← content of memory location pointed by BC.

---

## 9️⃣ STAX (Store Accumulator Indirect)

**Purpose:** Store accumulator using register pair.

**Example:**

```
STAX D
```

👉 Memory location pointed by DE ← A

---

## 🔟 XCHG (Exchange Registers)

**Purpose:** Exchange contents of HL and DE register pairs.

**Example:**

```
XCHG
```

👉 HL ↔ DE

---

# 📌 Small Complete Example Program

```
MVI A, 20H
MOV B, A
LXI H, 2500H
MOV M, B
```

### What happens?

- A = 20H
    
- B = 20H
    
- HL = 2500H
    
- Memory[2500H] = 20H
    

---

# ✅ Key Points for Exam

✔ Used to transfer data  
✔ No arithmetic operation  
✔ Flags are not affected  
✔ Includes register, memory, and immediate data transfer

---
## 📘 Arithmetic Instructions (8085)

Arithmetic Instructions in the **Intel 8085** are used to perform **mathematical operations** like addition, subtraction, increment, and decrement.

👉 These instructions usually affect the **flag register** (Zero, Carry, Sign, Parity, Auxiliary Carry).

---

# 🔹 Types of Arithmetic Instructions (with examples)

## 1️⃣ ADD (Add Register to Accumulator)

**Purpose:** Add register value to Accumulator (A).

**Syntax:**

```
ADD register
```

**Example:**

```
MVI A, 10H
MVI B, 05H
ADD B
```

👉 A = 10H + 05H = 15H
👉 Result stored in A

---

## 2️⃣ ADI (Add Immediate Data)

**Purpose:** Add 8-bit immediate data to Accumulator.

**Syntax:**

```
ADI data
```

**Example:**

```
MVI A, 20H
ADI 10H
```

👉 A = 20H + 10H = 30H

---

## 3️⃣ ADC (Add with Carry)

**Purpose:** Add register + Carry flag to Accumulator.

**Example:**

```
ADC B
```

👉 A = A + B + Carry

---

## 4️⃣ SUB (Subtract Register)

**Purpose:** Subtract register value from Accumulator.

**Syntax:**

```
SUB register
```

**Example:**

```
MVI A, 15H
MVI B, 05H
SUB B
```

👉 A = 15H − 05H = 10H

---

## 5️⃣ SUI (Subtract Immediate)

**Purpose:** Subtract immediate data from Accumulator.

**Example:**

```
MVI A, 20H
SUI 05H
```

👉 A = 1BH (20H − 05H)

---

## 6️⃣ SBB (Subtract with Borrow)

**Purpose:** Subtract register + Carry (borrow).

```
SBB C
```

👉 A = A − C − Carry

---

## 7️⃣ INR (Increment Register)

**Purpose:** Increase register value by 1.

**Example:**

```
MVI B, 09H
INR B
```

👉 B = 0AH

---

## 8️⃣ DCR (Decrement Register)

**Purpose:** Decrease register value by 1.

**Example:**

```
MVI C, 05H
DCR C
```

👉 C = 04H

---

## 9️⃣ INX (Increment Register Pair)

**Purpose:** Increase register pair by 1.

**Example:**

```
LXI H, 2500H
INX H
```

👉 HL = 2501H

---

## 🔟 DCX (Decrement Register Pair)

**Purpose:** Decrease register pair by 1.

**Example:**

```
LXI D, 3000H
DCX D
```

👉 DE = 2FFFH

---

## 1️⃣1️⃣ DAD (Double Add)

**Purpose:** Add register pair to HL pair (16-bit addition).

**Example:**

```
LXI H, 2000H
LXI D, 1000H
DAD D
```

👉 HL = 3000H

---

# 📌 Small Complete Example Program

```
MVI A, 10H
MVI B, 05H
ADD B
INR A
```

### What happens?

* A = 10H
* B = 05H
* After ADD → A = 15H
* After INR → A = 16H

---

# ✅ Important Points for Exam

✔ Most arithmetic operations use Accumulator (A)
✔ Flags are affected
✔ Supports 8-bit and 16-bit operations
✔ Includes addition, subtraction, increment, decrement

---


## 📘 Logical Instructions (8085)

Logical Instructions in the **Intel 8085** are used to perform **bitwise operations** (AND, OR, XOR, Compare, Rotate, Complement).

👉 These instructions work **bit by bit** (0 and 1).
👉 They affect flags (Zero, Sign, Parity, Carry, Auxiliary Carry).

---

# 🔹 Types of Logical Instructions (with examples)

## 1️⃣ ANA (AND Register)

**Purpose:** Perform AND operation between Accumulator and register.

**Rule:**
1 AND 1 = 1
Other combinations = 0

**Example:**

```
MVI A, 0FH     ; 00001111
MVI B, 03H     ; 00000011
ANA B
```

👉 A = 03H (00000011)

---

## 2️⃣ ANI (AND Immediate)

**Purpose:** AND immediate data with Accumulator.

**Example:**

```
MVI A, 0FH
ANI 05H
```

👉 A = 05H

---

## 3️⃣ ORA (OR Register)

**Purpose:** OR operation between Accumulator and register.

**Rule:**
If any bit is 1 → result is 1

**Example:**

```
MVI A, 0AH     ; 00001010
MVI B, 05H     ; 00000101
ORA B
```

👉 A = 0FH (00001111)

---

## 4️⃣ ORI (OR Immediate)

**Purpose:** OR immediate data with Accumulator.

**Example:**

```
MVI A, 02H
ORI 01H
```

👉 A = 03H

---

## 5️⃣ XRA (XOR Register)

**Purpose:** XOR operation between Accumulator and register.

**Rule:**
If bits are different → 1
If same → 0

**Example:**

```
MVI A, 0AH     ; 00001010
MVI B, 03H     ; 00000011
XRA B
```

👉 A = 09H

---

## 6️⃣ XRI (XOR Immediate)

**Purpose:** XOR immediate data with Accumulator.

**Example:**

```
MVI A, 05H
XRI 03H
```

👉 A = 06H

---

## 7️⃣ CMP (Compare Register)

**Purpose:** Compare register with Accumulator.

👉 It performs subtraction internally
👉 Result is not stored
👉 Only flags are affected

**Example:**

```
MVI A, 10H
MVI B, 10H
CMP B
```

👉 Zero flag = 1 (because equal)

---

## 8️⃣ CMA (Complement Accumulator)

**Purpose:** Change all bits (0 → 1, 1 → 0)

**Example:**

```
MVI A, 0FH     ; 00001111
CMA
```

👉 A = F0H (11110000)

---

## 9️⃣ CMC (Complement Carry)

**Purpose:** Reverse Carry flag value.

---

## 🔟 STC (Set Carry)

**Purpose:** Set Carry flag to 1.

---

## 1️⃣1️⃣ Rotate Instructions

### RLC (Rotate Left)

```
RLC
```

👉 MSB goes to LSB and Carry

### RRC (Rotate Right)

```
RRC
```

👉 LSB goes to MSB and Carry

### RAL (Rotate Left through Carry)

### RAR (Rotate Right through Carry)

---

# 📌 Small Complete Example Program

```
MVI A, 05H
MVI B, 03H
ANA B
CMA
```

### What happens?

* A = 05H
* B = 03H
* After ANA → A = 01H
* After CMA → A = FEH

---

# ✅ Important Points for Exam

✔ Logical instructions work bit by bit
✔ Mostly use Accumulator
✔ Flags are affected
✔ Used for masking, comparing, bit testing

---

## 📘 Branch Instructions (8085)

Branch Instructions in the **Intel 8085** are used to **change the normal sequence of program execution**.

👉 Normally, the program runs line by line.
👉 Branch instructions make the program **jump to another memory location**.
👉 These are mainly used for **decision making and loops**.

---

# 🔹 Types of Branch Instructions (with examples)

Branch instructions are mainly 3 types:

1. **Jump Instructions**
2. **Call Instructions**
3. **Return Instructions**

---

# 1️⃣ Jump Instructions

## 🔸 JMP (Unconditional Jump)

**Purpose:** Jump to given address without any condition.

**Syntax:**

```
JMP address
```

**Example:**

```
JMP 2000H
```

👉 Program control directly goes to memory location 2000H.

---

## 🔸 Conditional Jump Instructions

These jumps happen only if a condition is true.

| Instruction | Meaning             |
| ----------- | ------------------- |
| JZ          | Jump if Zero        |
| JNZ         | Jump if Not Zero    |
| JC          | Jump if Carry       |
| JNC         | Jump if No Carry    |
| JP          | Jump if Positive    |
| JM          | Jump if Minus       |
| JPE         | Jump if Parity Even |
| JPO         | Jump if Parity Odd  |

---

### Example (JZ):

```
MVI A, 00H
CMP A
JZ 2500H
```

👉 Since A = 0, Zero flag = 1
👉 Program jumps to 2500H

---

# 2️⃣ CALL Instructions

## 🔸 CALL (Unconditional Call)

**Purpose:** Call a subroutine.

```
CALL 3000H
```

👉 Program jumps to 3000H
👉 Return address is stored in stack
👉 After finishing subroutine, it returns

---

## 🔸 Conditional CALL

| Instruction | Meaning          |
| ----------- | ---------------- |
| CZ          | Call if Zero     |
| CNZ         | Call if Not Zero |
| CC          | Call if Carry    |
| CNC         | Call if No Carry |

Example:

```
CZ 3000H
```

👉 Calls subroutine only if Zero flag = 1

---

# 3️⃣ Return Instructions

## 🔸 RET (Return)

**Purpose:** Return from subroutine.

```
RET
```

👉 Program returns to original location.

---

## 🔸 Conditional RET

| Instruction | Meaning            |
| ----------- | ------------------ |
| RZ          | Return if Zero     |
| RNZ         | Return if Not Zero |
| RC          | Return if Carry    |
| RNC         | Return if No Carry |

Example:

```
RZ
```

👉 Return only if Zero flag = 1

---

# 📌 Small Complete Example Program

```
MVI A, 05H
MVI B, 05H
CMP B
JZ SAME
MVI C, 00H
JMP END

SAME: MVI C, 01H
END: HLT
```

### What happens?

* A = 05H
* B = 05H
* CMP → Zero flag = 1
* JZ SAME → Jump happens
* C = 01H

---

# ✅ Important Points for Exam

✔ Used for decision making
✔ Change program sequence
✔ Based on flag conditions
✔ Includes Jump, Call, Return

---


## 📘 Stack Instructions (8085)

Stack Instructions in the **Intel 8085** are used to work with the **stack memory**.

👉 Stack follows **LIFO (Last In First Out)** rule.
👉 Stack works using a special register called **Stack Pointer (SP)**.
👉 Stack grows **downward** (from higher address to lower address).

---

# 🔹 What is Stack?

Stack is a temporary memory area used to:

* Store return addresses (during CALL)
* Store register values
* Save data temporarily

---

# 🔹 Main Stack Instructions (with examples)

## 1️⃣ PUSH (Store Data in Stack)

**Purpose:** Store register pair data into stack.

**Syntax:**

```id="p1x8wa"
PUSH register_pair
```

(Register pairs: BC, DE, HL, PSW)

**Example:**

```id="m5z2rt"
LXI H, 2500H
PUSH H
```

👉 Contents of HL are stored in stack
👉 SP decreases by 2

---

## 2️⃣ POP (Get Data from Stack)

**Purpose:** Retrieve data from stack to register pair.

**Syntax:**

```id="c7v3ek"
POP register_pair
```

**Example:**

```id="z9k1lp"
POP D
```

👉 Data from stack goes to DE
👉 SP increases by 2

---

## 3️⃣ XTHL (Exchange HL with Top of Stack)

**Purpose:** Exchange HL register with top stack values.

**Example:**

```id="w2h6ns"
XTHL
```

👉 HL ↔ Top of Stack

---

## 4️⃣ SPHL (Copy HL to Stack Pointer)

**Purpose:** Load Stack Pointer with HL value.

**Example:**

```id="t4q8yb"
LXI H, 4000H
SPHL
```

👉 SP = 4000H

---

## 5️⃣ PCHL (Load PC from HL)

**Purpose:** Copy HL into Program Counter.

```id="r8u4dx"
PCHL
```

👉 Program jumps to address stored in HL

---

# 📌 Small Complete Example Program

```id="k3n7bt"
LXI H, 2500H
LXI D, 3000H
PUSH H
PUSH D
POP B
POP H
```

### What happens?

1. HL = 2500H
2. DE = 3000H
3. PUSH H → Stack stores 2500H
4. PUSH D → Stack stores 3000H
5. POP B → BC = 3000H
6. POP H → HL = 2500H

👉 This shows LIFO rule.

---

# 📌 Stack Diagram Example

If SP = 5000H and we do:

```
PUSH H
```

Stack will store:

* High byte at 4FFFH
* Low byte at 4FFEH

SP becomes 4FFEH

---

# ✅ Important Points for Exam

✔ Stack works on LIFO principle
✔ Controlled by Stack Pointer (SP)
✔ PUSH → SP decreases
✔ POP → SP increases
✔ Used in subroutine calls

---


## 📘 I/O Instructions (8085)

I/O Instructions in the **Intel 8085** are used to communicate with **input and output devices** like keyboard, switches, display, printer, etc.

👉 8085 uses **port addresses** to communicate with devices.
👉 It supports **256 input ports** and **256 output ports** (00H–FFH).
👉 Only the **Accumulator (A)** is used for I/O data transfer.

---

# 🔹 Types of I/O Instructions

There are only **2 I/O instructions** in 8085:

1. **IN**
2. **OUT**

---

## 1️⃣ IN Instruction

**Purpose:** Read data from an input port into Accumulator.

**Syntax:**

```id="i3k9vx"
IN port_address
```

**Example:**

```id="a8m2ql"
IN 01H
```

👉 Reads data from input port 01H
👉 Stores that data in Accumulator (A)

### Example Program:

```id="t9w4ps"
IN 05H
MOV B, A
```

👉 Read data from port 05H
👉 Store it into register B

---

## 2️⃣ OUT Instruction

**Purpose:** Send data from Accumulator to output port.

**Syntax:**

```id="q6n7ty"
OUT port_address
```

**Example:**

```id="z1c8re"
MVI A, 55H
OUT 02H
```

👉 Sends 55H to output port 02H

---

# 📌 Small Complete Example Program

```id="x4v2mn"
IN 01H
ADI 01H
OUT 02H
```

### What happens?

1. Read data from input port 01H
2. Add 1 to that data
3. Send result to output port 02H

---

# 📌 Simple Real-Life Example

If:

* Port 01H → connected to switches
* Port 02H → connected to LED display

Then:

```id="l8p5jk"
IN 01H
OUT 02H
```

👉 Whatever value comes from switches
👉 That value is shown on LED

---

# ✅ Important Points for Exam

✔ Only Accumulator is used in I/O
✔ Uses 8-bit port address (00H–FFH)
✔ IN → Input from device
✔ OUT → Output to device
✔ Does not affect flags

---


## 📘 Interrupt Instructions (8085)

Interrupt Instructions in the **Intel 8085** are used to **control and handle interrupts**.

👉 **Interrupt** = A signal that temporarily stops the current program and executes another important task.
👉 After completing the interrupt task, the CPU returns to the main program.

---

# 🔹 What Happens During Interrupt?

1. Current program execution stops
2. Address of next instruction is saved in stack
3. CPU jumps to a fixed memory location
4. After finishing, it returns using RET

---

# 🔹 Types of Interrupt Instructions

There are mainly **2 types**:

1. **Software Interrupts (RST instructions)**
2. **Interrupt Control Instructions (Enable/Disable)**

---

# 1️⃣ Software Interrupt Instructions (RST)

RST = Restart

They are like CALL instructions to fixed memory locations.

| Instruction | Address |
| ----------- | ------- |
| RST 0       | 0000H   |
| RST 1       | 0008H   |
| RST 2       | 0010H   |
| RST 3       | 0018H   |
| RST 4       | 0020H   |
| RST 5       | 0028H   |
| RST 6       | 0030H   |
| RST 7       | 0038H   |

---

## 🔸 Example: RST 1

```id="r2m8vn"
RST 1
```

👉 Program jumps to memory location 0008H
👉 Return address stored in stack

---

# 2️⃣ Interrupt Control Instructions

## 🔸 EI (Enable Interrupt)

**Purpose:** Enable all maskable interrupts.

```id="p6x3qa"
EI
```

👉 Interrupts are allowed

---

## 🔸 DI (Disable Interrupt)

**Purpose:** Disable all maskable interrupts.

```id="v8k2js"
DI
```

👉 Interrupts are blocked

---

## 🔸 SIM (Set Interrupt Mask)

**Purpose:** Mask (control) hardware interrupts.

---

## 🔸 RIM (Read Interrupt Mask)

**Purpose:** Check interrupt status.

---

# 📌 Small Complete Example Program

```id="n5y7tc"
EI
MVI A, 05H
RST 2
HLT
```

### What happens?

1. Interrupts enabled
2. A = 05H
3. RST 2 → Program jumps to 0010H
4. After RET, program continues

---

# 📌 Why Interrupt is Important?

✔ Handle urgent tasks
✔ Used in keyboard, I/O devices
✔ Saves CPU time
✔ Supports multitasking

---

# ✅ Important Points for Exam

✔ Interrupt temporarily stops program
✔ Return address saved in stack
✔ RST = Software interrupt
✔ EI enables, DI disables interrupts
✔ After interrupt, use RET to return

---

🎉 Now you have explained all 8085 instruction types:

* Data Transfer
* Arithmetic
* Logical
* Branch
* Stack
* I/O
* Interrupt

