You’ve shared an 8086 assembly program (DOS interrupt-based). Let’s go through it clearly and clean up a few small issues.

---

## 📌 What This Program Does

This program:

1. Takes a **single character input** from the keyboard
    
2. Moves it into register **BL**
    
3. Prints a **new line**
    
4. Displays the same character back on the screen
    

---

## 🧾 Corrected & Clean Version of the Code

(Just fixing formatting and a small comment issue)

```asm
.MODEL SMALL
.STACK 100H

.CODE
MAIN PROC

    MOV AH, 1        ; Read a character from keyboard
    INT 21H

    MOV BL, AL       ; Save input character into BL

    MOV AH, 2
    MOV DL, 0DH      ; Carriage return
    INT 21H

    MOV DL, 0AH      ; Line feed (new line)
    INT 21H

    MOV AH, 2        ; Display the character stored in BL
    MOV DL, BL
    INT 21H

    MOV AH, 4CH      ; Return control to DOS
    INT 21H

MAIN ENDP
END MAIN
```

---

## 🔍 Line-by-Line Explanation

- `MOV AH, 1`  
    → DOS function to **read a character** from keyboard
    
- `INT 21H`  
    → Calls DOS interrupt (input stored in **AL**)
    
- `MOV BL, AL`  
    → Saves the input character into **BL**
    

---

### New Line Section

- `MOV DL, 0DH` → Carriage return (`\r`)
    
- `MOV DL, 0AH` → Line feed (`\n`)
    

👉 Together, they move the cursor to a new line.

---

### Output Section

- `MOV AH, 2` → DOS function to **print a character**
    
- `MOV DL, BL` → Load saved character
    
- `INT 21H` → Display it
    

---

### Program Exit

- `MOV AH, 4CH`
    
- `INT 21H`  
    → Properly exits the program and returns control to DOS
    

---

## 🧠 Key Concept

- **AL** → Used for input
    
- **BL** → Temporary storage
    
- **DL** → Used for output character
    
- **INT 21H** → Main DOS interrupt for I/O operations
    

---

# Perform addition, subtraction, multiplication and division of 6 and 2 these two numbers in a single code.

simple **8086 assembly program** (DOS-based) that performs **addition, subtraction, multiplication, and division** on the numbers **6 and 2** in one code.

---

## 🧾 Assembly Program

```asm id="3k9d2p"
.MODEL SMALL
.STACK 100H

.DATA
    NUM1 DB 6
    NUM2 DB 2

    ADD_RES DB ?
    SUB_RES DB ?
    MUL_RES DB ?
    DIV_RES DB ?

.CODE
MAIN PROC

    MOV AX, @DATA
    MOV DS, AX

    ; -------- Addition --------
    MOV AL, NUM1
    ADD AL, NUM2
    MOV ADD_RES, AL

    ; -------- Subtraction --------
    MOV AL, NUM1
    SUB AL, NUM2
    MOV SUB_RES, AL

    ; -------- Multiplication --------
    MOV AL, NUM1
    MOV BL, NUM2
    MUL BL           ; AX = AL * BL
    MOV MUL_RES, AL  ; lower byte stored

    ; -------- Division --------
    MOV AL, NUM1
    MOV AH, 0
    MOV BL, NUM2
    DIV BL           ; AL = quotient, AH = remainder
    MOV DIV_RES, AL  ; store quotient

    ; -------- Exit --------
    MOV AH, 4CH
    INT 21H

MAIN ENDP
END MAIN
```

---

## 📊 Results (Conceptually)

* Addition → 6 + 2 = **8**
* Subtraction → 6 − 2 = **4**
* Multiplication → 6 × 2 = **12**
* Division → 6 ÷ 2 = **3** (remainder 0)

---

## 🔍 Key Notes

* `ADD`, `SUB`, `MUL`, `DIV` are core arithmetic instructions.
* `MUL` stores result in **AX** (for 8-bit operands).
* `DIV` stores:

  * Quotient → **AL**
  * Remainder → **AH**
* This program **stores results in memory**, not printing them.

---

# Take two single digit integer inputs from and perform addition, subtraction, multiplication and division on two numbers.



Here’s a complete **8086 assembly program** (DOS interrupt-based) that:

* Takes **two single-digit inputs** from the keyboard
* Performs **addition, subtraction, multiplication, and division**
* Displays the results (as single digits)

---

## 🧾 Assembly Code

```asm id="6p2x9a"
.MODEL SMALL
.STACK 100H

.DATA
    MSG1 DB 'Enter first digit: $'
    MSG2 DB 0DH,0AH,'Enter second digit: $'
    NL   DB 0DH,0AH,'$'

.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    ; ---- Input first number ----
    MOV AH, 9
    LEA DX, MSG1
    INT 21H

    MOV AH, 1
    INT 21H
    SUB AL, 30H      ; convert ASCII → number
    MOV BL, AL       ; store first number

    ; ---- Input second number ----
    MOV AH, 9
    LEA DX, MSG2
    INT 21H

    MOV AH, 1
    INT 21H
    SUB AL, 30H
    MOV CL, AL       ; store second number

    ; ---- New line ----
    MOV AH, 9
    LEA DX, NL
    INT 21H

    ; ---- Addition ----
    MOV AL, BL
    ADD AL, CL
    ADD AL, 30H      ; convert to ASCII
    MOV DL, AL
    MOV AH, 2
    INT 21H

    ; ---- New line ----
    MOV AH, 9
    LEA DX, NL
    INT 21H

    ; ---- Subtraction ----
    MOV AL, BL
    SUB AL, CL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 2
    INT 21H

    ; ---- New line ----
    MOV AH, 9
    LEA DX, NL
    INT 21H

    ; ---- Multiplication ----
    MOV AL, BL
    MOV AH, 0
    MUL CL           ; AX = AL * CL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 2
    INT 21H

    ; ---- New line ----
    MOV AH, 9
    LEA DX, NL
    INT 21H

    ; ---- Division ----
    MOV AL, BL
    MOV AH, 0
    DIV CL           ; AL = quotient
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 2
    INT 21H

    ; ---- Exit ----
    MOV AH, 4CH
    INT 21H

MAIN ENDP
END MAIN
```

---

## 🔍 How It Works

* **Input**: Uses `INT 21H` with `AH=1` to read a character
* Converts ASCII → number using `SUB AL, 30H`
* Stores numbers in **BL** and **CL**
* Performs operations using:

  * `ADD`, `SUB`, `MUL`, `DIV`
* Converts result back to ASCII using `ADD AL, 30H`
* Displays result using `AH=2`

---

## ⚠️ Important Notes

* Works correctly for **single-digit results only (0–9)**
* Multiplication may exceed one digit (e.g., 9×9=81), but this code only prints the **last digit**
* Division assumes **second number ≠ 0**

---

