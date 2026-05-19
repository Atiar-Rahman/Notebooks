Sure! Let’s go step by step and make it clear.

---

## **`Apriori` Algorithm in Data Mining**

**Definition:**  
The **`Apriori` Algorithm** is a popular **association rule mining algorithm** used to find **frequent `itemsets`** and generate **strong association rules** from transactional databases.  
It is widely used in **market basket analysis**.

**Purpose:**

- Discover **relationships between items** in large datasets
    
- Identify patterns like _“Customers who buy X also buy Y”_
    

---

## **Key Concepts**

1. **Itemset** – A set of items in a transaction
    
    - Example: `{Bread, Milk, Butter}`
        
2. **Support** – How frequently an itemset occurs in the dataset
    

$\text{Support}(A) = \frac{\text{Number of transactions containing A}}{\text{Total transactions}}$

3. **Confidence** – How often a rule is true
    

$\text{Confidence}(A \rightarrow B) = \frac{\text{Support}(A \cup B)}{\text{Support}(A)}$

4. **Frequent `Itemset`** – `Itemsets` `wose` **support ≥ minimum support threshold**
    
5. **Strong Rule** – Rules whose **confidence ≥ minimum confidence threshold**
    

---

## **`Apriori` Algorithm Steps**

1. **Generate candidate 1-`itemsets` (`C1`)** – List all single items from transactions.
    
2. **Scan the database to find frequent 1-`itemsets` (`L1`)** – Keep items with support ≥ minimum support.
    
3. **Generate candidate 2-`itemsets` (`C2`)** – Combine items from `L1.`
    
4. **Scan database to find frequent 2-`itemsets` (`L2`)** – Keep `itemsets` with support ≥ minimum support.
    
5. **Repeat** for k-`itemsets` (`Lk`) until no more frequent `itemsets`.
    
6. **Generate strong association rules** from frequent `itemsets` using confidence.
    

---

## **Step-by-Step Example**

**Transactions:**

|TID|Items|
|---|---|
|1|{Bread, Milk}|
|2|{Bread, Diaper, Beer, Eggs}|
|3|{Milk, Diaper, Beer, Cola}|
|4|{Bread, Milk, Diaper, Beer}|
|5|{Bread, Milk, Diaper, Cola}|

**Step 1: Candidate 1-itemsets (C1)**  
`{Bread, Milk, Diaper, Beer, Eggs, Cola}`

**Step 2: Frequent 1-itemsets (L1, min support 60%)**

- Bread: 4/5 = 80% → ✅
    
- Milk: 4/5 = 80% → ✅
    
- Diaper: 4/5 = 80% → ✅
    
- Beer: 3/5 = 60% → ✅
    
- Eggs: 1/5 = 20% → ❌
    
- Cola: 2/5 = 40% → ❌
    

**L1 = {Bread, Milk, Diaper, Beer}**

**Step 3: Candidate 2-itemsets (C2)**

- {Bread, Milk}, {Bread, Diaper}, {Bread, Beer}, {Milk, Diaper}, {Milk, Beer}, {Diaper, Beer}
    

**Step 4: Frequent 2-itemsets (L2)**

- {Bread, Milk}: 3/5 = 60% → ✅
    
- {Bread, Diaper}: 3/5 = 60% → ✅
    
- {Bread, Beer}: 2/5 = 40% → ❌
    
- {Milk, Diaper}: 3/5 = 60% → ✅
    
- {Milk, Beer}: 2/5 = 40% → ❌
    
- {Diaper, Beer}: 3/5 = 60% → ✅
    

**L2 = {Bread, Milk}, {Bread, Diaper}, {Milk, Diaper}, {Diaper, Beer}**

**Step 5: Candidate 3-itemsets (C3)**

- {Bread, Milk, Diaper}, {Milk, Diaper, Beer}, {Bread, Diaper, Beer}, {Bread, Milk, Beer}
    

**Step 6: Frequent 3-itemsets (L3)**

- {Bread, Milk, Diaper}: 2/5 = 40% → ❌
    
- {Milk, Diaper, Beer}: 2/5 = 40% → ❌
    
- {Bread, Diaper, Beer}: 2/5 = 40% → ❌
    
- {Bread, Milk, Beer}: 1/5 = 20% → ❌
    

**No more frequent 3-itemsets. Stop.**

---

## **Step 7: Generate Strong Association Rules**

From L2, using **confidence ≥ 70%**:

- {Diaper} → {Beer} = Support({Diaper, Beer})/Support({Diaper}) = 3/4 = 75% → ✅
    
- {Beer} → {Diaper} = 3/3 = 100% → ✅
    

---

## **Advantages**

- Simple and easy to understand
    
- Effective for **market basket analysis**
    

## **Disadvantages**

- Scans database **multiple times** → slow for large datasets
    
- Generates **many candidate `itemsets`** → memory intensive
    

---

