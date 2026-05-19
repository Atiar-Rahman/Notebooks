
---

## **Decision Tree in Data Mining**

**Definition:**  
A **Decision Tree** is a **supervised learning algorithm** used for **classification and regression**.  
It models decisions and their possible consequences as a **tree structure**.

- **Internal nodes:** Test on an attribute
    
- **Branches:** Outcome of the test
    
- **Leaf nodes:** Class labels (or predicted values)
    

---

## **Purpose**

- Predict the **class** of new data points
    
- Visualize **decision-making rules**
    
- Handle both **categorical and numerical data**
    

---

## **Key Concepts**

1. **Root Node:** The top-most node representing the **entire dataset**
    
2. **Internal Nodes:** Attributes used to **split the data**
    
3. **Leaf Nodes:** Outcome (class label)
    
4. **Splitting:** Dividing a node into two or more sub-nodes based on an attribute
    
5. **Pruning:** Removing nodes that do not provide significant information to **avoid `overfitting`**
    
6. **Branch / `Subtree`:** A subsection of the tree
    

---

## **Decision Tree Algorithms**

- **`ID3` (Iterative `Dichotomiser` 3):** Uses **Information Gain** to select attributes
    
- **`C4.5`:** Improvement of I`D3`; handles **continuous attributes and missing values**
    
- **CART (Classification and Regression Tree):** Uses **`Gini` Index**; can handle regression
    

---

## **How a Decision Tree Works (Step-by-Step Example)**

**Dataset:** Predict whether a person plays tennis based on weather

|Outlook|Temperature|Humidity|Wind|PlayTennis|
|---|---|---|---|---|
|Sunny|Hot|High|Weak|No|
|Sunny|Hot|High|Strong|No|
|Overcast|Hot|High|Weak|Yes|
|Rain|Mild|High|Weak|Yes|
|Rain|Cool|Normal|Weak|Yes|

**Step 1: Choose the best attribute for root**

- Use **Information Gain** (ID3) or **Gini Index** (CART)
    
- Suppose **Outlook** has the highest information gain → root node
    

**Step 2: Split dataset based on Outlook**

- Outlook = Sunny → subset 1
    
- Outlook = Overcast → subset 2
    
- Outlook = Rain → subset 3
    

**Step 3: Repeat splitting for each node**

- For subset 1 (Sunny), find attribute with highest gain → Humidity
    
- Continue until all leaves are pure (contain single class)
    

**Step 4: Tree Construction Complete**

**Decision Rules Example:**

- If Outlook = Sunny AND Humidity = High → PlayTennis = No
    
- If Outlook = Overcast → PlayTennis = Yes
    
- If Outlook = Rain AND Wind = Weak → PlayTennis = Yes
    

---

## **Advantages of Decision Trees**

- Easy to understand and visualize
    
- Handles **categorical and numerical data**
    
- Non-linear relationships between features do not affect performance
    

## **Disadvantages**

- Can **overfit** on training data
    
- Sensitive to **noisy data**
    
- Small variations in data can lead to different trees
    

---

Decision trees are used in **finance (loan prediction), healthcare (disease prediction), marketing (customer behavior), and more**.

---

Perfect! Let’s make a **visual decision tree** for the Tennis dataset example I gave earlier.

---

### **Dataset Recap**

|Outlook|Temperature|Humidity|Wind|PlayTennis|
|---|---|---|---|---|
|Sunny|Hot|High|Weak|No|
|Sunny|Hot|High|Strong|No|
|Overcast|Hot|High|Weak|Yes|
|Rain|Mild|High|Weak|Yes|
|Rain|Cool|Normal|Weak|Yes|

**Assumption:** Using **ID3**, we select **Outlook** as the root (highest Information Gain).

---

### **Decision Tree (Visual)**

```
                [Outlook]
               /    |    \
           Sunny  Overcast  Rain
           /         |        \
     [Humidity]      Yes    [Wind]
      /      \               /   \
   High      Normal        Weak  Strong
    No         Yes          Yes    ?
```

---

### **Explanation of the Tree**

1. **Root Node:** Outlook
    
    - Splits dataset into **Sunny**, **Overcast**, and **Rain**
        
2. **Sunny Subset:**
    
    - Use **Humidity** as next split
        
    - Humidity = High → PlayTennis = No
        
    - Humidity = Normal → PlayTennis = Yes
        
3. **Overcast Subset:**
    
    - All examples → PlayTennis = Yes
        
4. **Rain Subset:**
    
    - Use **Wind** as next split
        
    - Wind = Weak → PlayTennis = Yes
        
    - Wind = Strong → Could be No (depending on dataset)
        

---

✅ **Decision Rules from Tree**

- If Outlook = Sunny AND Humidity = High → No
    
- If Outlook = Sunny AND Humidity = Normal → Yes
    
- If Outlook = Overcast → Yes
    
- If Outlook = Rain AND Wind = Weak → Yes
    
- If Outlook = Rain AND Wind = Strong → (depends on dataset, maybe No)
    

---

This tree makes it **easy to visualize how decisions are made** and which attributes influence the outcome the most.

---
**mathematical calculation of a decision tree using the ``ID3`` algorithm** (which uses **Information Gain**) for a simple dataset.

---

## **Step 1: Understand the Dataset**

**Dataset (Play Tennis Example):**

|Outlook|Humidity|PlayTennis|
|---|---|---|
|Sunny|High|No|
|Sunny|High|No|
|Overcast|High|Yes|
|Rain|High|Yes|
|Rain|Normal|Yes|

We want to build a **decision tree** to predict PlayTennis.

---

## **Step 2: Calculate Entropy for the Dataset**

**Entropy formula:**

$Entropy(S) = - \sum_{i=1}^{c} p_i \log_2(p_i)$

Where:

- pi = proportion of class i in set S
    
- c = number of classes
    

**`Step` `2a`: Count classes**

- `PlayTennis` = Yes → 3
    
- `PlayTennis` = No → 2
    
- Total = 5
    

**Step `2b`: Compute probabilities**

- $p_{Yes} = 3/5 = 0.6$
    
- $p_{No} = 2/5 = 0.4$
    

**Step 2c: Compute Entropy of Dataset**

$Entropy(S) = -(0.6 \log_2 0.6 + 0.4 \log_2 0.4)$ 
$Entropy(S) = -(0.6 \times -0.737 + 0.4 \times -1.322)$ 
$Entropy(S) = 0.442 + 0.529 = 0.971$

**Entropy(S) ≈ 0.971 bits**

---

## **Step 3: Calculate Entropy for Each Attribute**

### **Attribute: Outlook**

- Values: Sunny, Overcast, Rain
    

**Subset `Entropies`:**

1. **Sunny (2 examples: No, No)**
    

$Entropy(Sunny) = -(0/2 \log_2 0 + 2/2 \log_2 1) = 0$

2. **Overcast (1 example: Yes)**
    

$Entropy(Overcast) = 0 \quad \text{(pure)}$

3. **Rain (2 examples: Yes, Yes)**
    

$Entropy(Rain) = 0 \quad \text{(pure)}$

**Weighted Entropy for Outlook:**

$Entropy_{Outlook} = \frac{2}{5} \times 0 + \frac{1}{5} \times 0 + \frac{2}{5} \times 0 = 0$

---

### **Attribute: Humidity**

- Values: High, Normal
    

**Subset Entropies:**

1. **High (4 examples: No, No, Yes, Yes)**
    

- Yes = 2, No = 2 → p=0.5p = 0.5 each
    

$Entropy(High) = - (0.5 \log_2 0.5 + 0.5 \log_2 0.5) = 1$

2. **Normal (1 example: Yes)**
    

$Entropy(Normal) = 0$

**Weighted Entropy for Humidity:**

$Entropy_{Humidity} = \frac{4}{5} \times 1 + \frac{1}{5} \times 0 = 0.8$

---

## **Step 4: Calculate Information Gain**

$IG(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} Entropy(S_v)$

1. **Gain for Outlook:**
    

$IG(S, Outlook) = 0.971 - 0 = 0.971$

2. **Gain for Humidity:**
    

$IG(S, Humidity) = 0.971 - 0.8 = 0.171$

---

## **Step 5: Choose the Best Attribute**

- **Outlook** has the **highest information gain (0.971)** → becomes the **root node**
    
- Split dataset based on Outlook and repeat steps for subsets until all leaves are pure.
    

---

✅ **Summary of Mathematical Steps:**

1. Calculate **Entropy of the dataset**
    
2. Calculate **Entropy of each attribute** (weighted by subset size)
    
3. Compute **Information Gain** = Dataset Entropy − Attribute Entropy
    
4. Select attribute with **highest Information Gain** as node
    
5. Recursively repeat for subsets
    

---

[example](https://www.youtube.com/watch?v=pX0-Ajk06B4&list=PLMW5djzR9cKM0MFFfLvtzJfc11itguKIE&index=16&ab_channel=Networkingpro)
