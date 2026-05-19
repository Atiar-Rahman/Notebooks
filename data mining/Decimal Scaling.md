
---

## **Decimal Scaling Normalization**

**Definition:**  
Decimal scaling is a **data normalization technique** where values are scaled by moving the decimal point of the values.  
The number of decimal points moved depends on the **maximum absolute value** in the dataset.

**Purpose:**

- To bring all data values into a **smaller, comparable range**, usually between -1 and 1.
    
- Simple and easy to compute.
    

---

### **Formula**

$X_{\text{normalized}} = \frac{X}{10^j}$

Where:

- X = original value
    
- j = smallest integer such that $∣Xnormalized∣<1|X_{\text{normalized}}| < 1$
    
- $X_{\text{normalized}} = normalized value$
    

**How to find jj:**

- Find the **maximum absolute value** in the dataset.
    
- Count how many digits are in that value → move decimal point accordingly.
    

---

### **Step-by-Step Example**

**Original Data:**  
`[50, 200, 800, 1000]`

**Step 1: Find maximum absolute value**  
$∣X_{\max}| = 1000$

**Step 2: Determine jj**

- Maximum value = 1000 → 4 digits
    
- To make it < 1: j=4 → divide each value by 104=1000010^4 = 10000
    

**Step 3: Apply formula**

- 50 → 50 / 10000 = 0.005
    
- 200 → 200 / 10000 = 0.02
    
- 800 → 800 / 10000 = 0.08
    
- 1000 → 1000 / 10000 = 0.1
    

**Normalized Data:**  
`[0.005, 0.02, 0.08, 0.1]`

---

### **Advantages**

- Simple and easy to implement
    
- Preserves the relative relationships between values
    
- Good for small datasets
    

### **Disadvantages**

- Sensitive to outliers
    
- Range is **not fixed** to 0–1; depends on max value
    

---

