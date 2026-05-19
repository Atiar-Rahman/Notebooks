

# 🔹 **Min-Max Normalization**

**Definition:**  
Min-Max normalization is a **data preprocessing technique** that scales the data to a **specific range**, usually **[0, 1]** or **[-1, 1]**.

**Purpose:**

- Makes data comparable
    
- Helps machine learning algorithms converge faster
    
- Avoids features with large values dominating features with small values
    

$---$

## $🔹 **Formula**$

$Xnormalized=X−Xmin⁡Xmax⁡−Xmin⁡X_{\text{normalized}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}$

$Where:$

- $XX = original value$
    
- $Xmin⁡X_{\min} = minimum value in the dataset$
    
- $Xmax⁡X_{\max} = maximum value in the dataset$
    
- $XnormalizedX_{\text{normalized}} = scaled value between 0 and 1$
    

$**Optional:** To scale to [a, b], use:$

$X′=a+(X−Xmin⁡)(b−a)Xmax⁡−Xmin⁡X' = a + \frac{(X - X_{\min})(b - a)}{X_{\max} - X_{\min}}$

$---$

## $🔹 **Step-by-Step Example**$

### $Original data:$

$`[50, 20, 80, 100]`$

### $Step 1: Find min and max$

- $Xmin⁡=20X_{\min} = 20$
    
- $Xmax⁡=100X_{\max} = 100$
    

### $Step 2: Apply formula for each value$

1. $For 50:$
    

$X_{\text{norm}} = \frac{50-20}{100-20} = \frac{30}{80} = 0.375$

2. $For 20:$
    

$X_{\text{norm}} = \frac{20-20}{100-20} = 0/80 = 0$

3. $For 80:$
    

$Xnorm=80−20/100−20=60/80=0.75X_{\text{norm}} = \frac{80-20}{100-20} = 60/80 = 0.75$

4. $For 100:$
    

$Xnorm=100−20/100−20=80/80=1X_{\text{norm}} = \frac{100-20}{100-20} = 80/80 = 1$

### $✅ **Normalized data:**$

$`[0.375, 0, 0.75, 1]`$

$---$

## $🔹 **Advantages**$

- $Scales all features to the same range$
    
- $Preserves relationships between original data$
    
- $Useful for algorithms like **KNN, Neural Networks, SVM**$
    

## $⚠️ **Disadvantages**$

- $Sensitive to **outliers** (extreme values can compress most data into a small range)$
    

$---$

$If you want, I can also explain **Z-score normalization** and compare it with **Min-Max normalization** to see when to use which.$

$Do you want me to do that?$