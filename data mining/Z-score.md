Sure! Here’s a clean explanation of **Z-score normalization** without Obsidian formatting:

---

## **Z-Score Normalization**

**Definition:**  
Z-score normalization (or standardization) scales data so that it has a **mean of 0** and a **standard deviation of 1**.  
It is useful when the data has different scales or units.

---

### **Formula**

Z=X−μσZ = \frac{X - \mu}{\sigma}

Where:

- XX = original value
    
- μ\mu = mean of the dataset
    
- σ\sigma = standard deviation of the dataset
    
- ZZ = normalized value
    

---

### **Step-by-Step Example**

**Original Data:**  
`[50, 20, 80, 100]`

**Step 1: Compute Mean (μ\mu)**

$μ=50+20+80+1004=2504=62.5\mu = \frac{50 + 20 + 80 + 100}{4} = \frac{250}{4} = 62.5$

**Step 2: Compute Standard Deviation (σ\sigma)**

$σ=∑(Xi−μ)2N\sigma = \sqrt{\frac{\sum (X_i - \mu)^2}{N}}$

Calculations:

- (50 - 62.5)² = 156.25
    
- (20 - 62.5)² = 1806.25
    
- (80 - 62.5)² = 306.25
    
- (100 - 62.5)² = 1406.25
    

Sum = 3675

$σ=36754=918.75≈30.32\sigma = \sqrt{\frac{3675}{4}} = \sqrt{918.75} \approx 30.32$

**Step 3: Compute Z-score for each value**

- 50 → (50 - 62.5)/30.32 ≈ -0.41
    
- 20 → (20 - 62.5)/30.32 ≈ -1.40
    
- 80 → (80 - 62.5)/30.32 ≈ 0.58
    
- 100 → (100 - 62.5)/30.32 ≈ 1.24
    

**Z-Score Normalized Data:**  
`[-0.41, -1.40, 0.58, 1.24]`

---

### **Advantages**

- Handles features with different scales
    
- Less sensitive to outliers compared to Min-Max normalization
    
- Useful for algorithms like KNN, PCA, SVM, and Logistic Regression
    

### **Disadvantages**

- Not bounded between 0 and 1
    
- Sensitive to skewed distributions
    

---

If you want, I can also make a **comparison table between Min-Max normalization and Z-score normalization** so it’s easy to remember.

Do you want me to do that?