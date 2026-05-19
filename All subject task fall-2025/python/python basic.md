

```python
arr = input().strip().split()
print(arr)
```

---

## 🧩 Line 1: `arr = input().strip().split()`

This line takes input from the user and processes it into a **list of strings**.  
Let’s understand what happens in **each part**:

---

### 🔹 `input()`

- This function reads a **line of text** entered by the user.
    
- It always returns a **string** (even if you type numbers).
    

**Example:**

```python
x = input()
# Suppose you type: hello world python
print(x)
```

🖨️ Output:

```
hello world python
```

---

### 🔹 `.strip()`

- Removes **leading and trailing `whitespace`** (spaces, tabs, or newlines) from the string.
    
- Ensures clean input even if the user accidentally adds extra spaces.
    

**Example:**

```python
x = "   hello world   "
print(x.strip())
```

🖨️ Output:

```
hello world
```

Without `.strip()`, you might have unwanted spaces in your data.

---

### 🔹 `.split()`

- Splits a string into **a list of words** (based on spaces by default).
    
- Every space separates one element in the list.
    

**Example:**

```python
x = "hello world python"
print(x.split())
```

🖨️ Output:

```
['hello', 'world', 'python']
```

If you want to split by something else (like commas), you can pass a delimiter:

```python
x = "apple,banana,mango"
print(x.split(','))
```

🖨️ Output:

```
['apple', 'banana', 'mango']
```

---

### 🧠 Putting it all together:

```python
arr = input().strip().split()
```

means:

1. Take a line of input.
    
2. Remove extra spaces.
    
3. Split it into a list of words.
    

---

**Example:**

```
Input → "   insert 0 5   "
```

After `.strip()` → `"insert 0 5"`  
After `.split()` → `['insert', '0', '5']`

So:

```python
arr = ['insert', '0', '5']
```

---

## 🖨️ Line 2: `print(arr)`

- This simply prints the **list** created above.
    
- You’ll see square brackets and quotes because `arr` is a **Python list**.
    

**Example:**

```python
arr = input().strip().split()
print(arr)
```

```
Input →  hello world python
Output → ['hello', 'world', 'python']
```

---

✅ **Summary Table**

|Part|Meaning|Example Input|Output|
|---|---|---|---|
|`input()`|Take input as string|`"a b c"`|`"a b c"`|
|`.strip()`|Remove outer spaces|`" a b c "`|`"a b c"`|
|`.split()`|Split into list|`"a b c"`|`['a', 'b', 'c']`|
|`print(arr)`|Print the list||`['a', 'b', 'c']`|

---

