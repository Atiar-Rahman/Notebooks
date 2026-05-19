## Example 1


---

## **Box Plot in Data Mining**

**Definition:**  
A **Box Plot** (or **Whisker Plot**) is a graphical representation of the **distribution of a dataset**.  
It shows the **minimum, first `quartile`, median, third `quartile`, and maximum**, and highlights **outliers**.

**Purpose:**

- Identify **central tendency** (median)
    
- Detect **spread / variability**
    
- Find **outliers** and unusual observations
    

---

## **Components of a Box Plot**

1. **Minimum (Min)** – Smallest value excluding outliers
    
2. **First `Quartile` (`Q1`)** – 25th percentile (median of lower half)
    
3. **Median `(Q2`)** – 50th percentile (middle value)
    
4. **Third `Quartile (Q3)** `– 75th percentile (median of upper half)
    
5. **Maximum (Max)** – Largest value excluding outliers
    
6. `**Interquartile Range (IQR)** – Q3 - Q1`
    
7. **Whiskers** – Lines from `Q1` to Min and `Q3` to Max
    
8. **Outliers** – Data points outside 1.5 × `IQR` from `Q1` or `Q3`
    

---

## **Step-by-Step Example**

**Dataset:**  
`[7, 8, 5, 6, 10, 15, 18, 20, 25, 30, 100]`  
(100 is an outlier)

**Step 1: Sort the data**  
`[5, 6, 7, 8, 10, 15, 18, 20, 25, 30, 100]`

**Step 2: Find Median (Q2)**

- Middle value (n=11) → 6th value = 15 → **Median = 15**
    

**Step 3: Find Q1 and Q3**

- Lower half = [5, 6, 7, 8, 10] → Median = 7 → **Q1 = 7**
    
- Upper half = [18, 20, 25, 30, 100] → Median = 25 → **Q3 = 25**
    

**Step 4: Compute `IQR`**

$\text{IQR} = Q3 - Q1 = 25 - 7 = 18$

**Step 5: Determine outliers**

- Lower bound = `Q1` - 1.5×`IQR` = 7 - 27 = -20 (no lower outliers)
    
- Upper bound = `Q3` + 1.5×`IQR` = 25 + 27 = 52
    
- Any value > 52 is an **outlier** → 100 is an outlier
    

**Step 6: Identify Min and Max (excluding outliers)**

- Min = 5, Max = 30
    

---

### **Box Plot Summary**

- **Min:** 5
    
- **Q1:** 7
    
- **Median:** 15
    
- **Q3:** 25
    
- **Max:** 30
    
- **Outlier:** 100
    

**Graphically:**

- Box spans Q1 to Q3
    
- Line inside box = median
    
- Whiskers from Min to Max
    
- Outliers shown as dots
    

---

### **Advantages**

- Quickly identifies **spread and skewness**
    
- Detects **outliers** easily
    
- Summarizes **5-number summary** (Min, Q1, Median, Q3, Max)
    

### **Disadvantages**

- Doesn’t show **frequency or distribution shape**
    
- Not suitable for small datasets
    

---

