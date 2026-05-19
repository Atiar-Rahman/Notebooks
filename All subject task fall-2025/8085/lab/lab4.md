```
.MODEL SMALL
.STACK 100H

.DATA
    msg1 DB 10,13, 'Enter a number: $'
    msg2 DB 10,13, 'Even number.$'
    msg3 DB 10,13, 'Odd number.$'
    msg4 DB 10,13, 'Press N to exit or any key to continue: $'

.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

START:

    ; Show input message
    LEA DX, msg1
    MOV AH, 09H
    INT 21H

    ; Take input (single digit)
    MOV AH, 01H
    INT 21H
    SUB AL, '0' ; Convert ASCII to number

    MOV BL, AL ; Store number

    ; Check even or odd
    AND AL, 01H ; Check LSB

    CMP AL, 00H
    JE EVEN

ODD:
    LEA DX, msg3
    MOV AH, 09H
    INT 21H
    JMP CONTINUE

EVEN:
    LEA DX, msg2
    MOV AH, 09H
    INT 21H

CONTINUE:
    ; Ask user to continue
    LEA DX, msg4
    MOV AH, 09H
    INT 21H

    MOV AH, 01H
    INT 21H

    CMP AL, 'N'
    JE EXIT
    CMP AL, 'n'
    JE EXIT

    JMP START

EXIT:
    MOV AH, 4CH
    INT 21H

MAIN ENDP
END MAIN

[explain line by line]
```
Here is your **line-by-line explanation** in a simple way (perfect for viva + lab copy):

---

## 💬 Line-by-Line Explanation

---

### 🔹 Program Structure

```asm
.MODEL SMALL
```

👉 Defines memory model (small = one code + one data segment)

```asm
.STACK 100H
```

👉 Allocates stack of size 256 bytes (100H = 256)

---

### 🔹 Data Section

```asm
.DATA
```

👉 Start of data segment

```asm
msg1 DB 10,13, 'Enter a number: $'
```

👉 Message to ask user for input (`10,13` = new line)

```asm
msg2 DB 10,13, 'Even number.$'
```

👉 Message for even number

```asm
msg3 DB 10,13, 'Odd number.$'
```

👉 Message for odd number

```asm
msg4 DB 10,13, 'Press N to exit or any key to continue: $'
```

👉 Message for continue/exit

---

### 🔹 Code Section

```asm
.CODE
MAIN PROC
```

👉 Start of code and main procedure

---

### 🔹 Initialize Data Segment

```asm
MOV AX, @DATA
MOV DS, AX
```

👉 Load data segment address into DS register

---

### 🔹 Start Label (Loop Start)

```asm
START:
```

👉 Label for repeating program

---

### 🔹 Display Input Message

```asm
LEA DX, msg1
MOV AH, 09H
INT 21H
```

👉 Print "Enter a number"

---

### 🔹 Take Input

```asm
MOV AH, 01H
INT 21H
```

👉 Take single character input from user (stored in AL)

```asm
SUB AL, '0'
```

👉 Convert ASCII to number
(e.g., '5' → 5)

---

### 🔹 Store Number

```asm
MOV BL, AL
```

👉 Save input number in BL register

---

### 🔹 Check Odd/Even

```asm
AND AL, 01H
```

👉 Check last bit (LSB)

* 0 → Even
* 1 → Odd

```asm
CMP AL, 00H
JE EVEN
```

👉 If result = 0, jump to EVEN

---

### 🔹 Odd Case

```asm
ODD:
LEA DX, msg3
MOV AH, 09H
INT 21H
```

👉 Print "Odd number"

```asm
JMP CONTINUE
```

👉 Skip EVEN part and go to continue

---

### 🔹 Even Case

```asm
EVEN:
LEA DX, msg2
MOV AH, 09H
INT 21H
```

👉 Print "Even number"

---

### 🔹 Continue Section

```asm
CONTINUE:
LEA DX, msg4
MOV AH, 09H
INT 21H
```

👉 Ask user to continue or exit

---

### 🔹 Take Choice

```asm
MOV AH, 01H
INT 21H
```

👉 Take user input

```asm
CMP AL, 'N'
JE EXIT
CMP AL, 'n'
JE EXIT
```

👉 If user presses N/n → exit

---

### 🔹 Repeat Loop

```asm
JMP START
```

👉 Otherwise, repeat program

---

### 🔹 Exit Program

```asm
EXIT:
MOV AH, 4CH
INT 21H
```

👉 Terminate program

---

### 🔹 End Program

```asm
MAIN ENDP
END MAIN
```

👉 End of main procedure

---

## ✅ Summary (1–2 lines for exam)

This program takes a number, checks odd/even using `AND 01H`, prints the result, and repeats until user presses **N**.

---

If you want, I can also:

* 🔥 Make **super short viva answers**
* 📄 Convert into **PDF notes**
* 🚀 Upgrade to **multi-digit version explanation**
