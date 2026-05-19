
---

## 🔹 What is an Activation Function?

- In a **neural network**, every neuron receives some input → does some math → sends output.
    
- But if we only use math like addition & multiplication, the network will just behave like a **linear equation** (a straight line).
    
- **Activation functions** add **non-linearity**, so the network can learn **complex patterns** (like recognizing faces, objects, speech, etc.).
    

👉 Without activation → only simple patterns.  
👉 With activation → complex & powerful learning.

---

## 🔹 Types of Activation Functions

### 1. **Sigmoid**

f(x)=1/1+e−x

- Output: between **0 and 1**
    
- Good for probabilities
    
- Problem: vanishing gradient (training gets stuck for big + or – values)
    

---

### 2. **Tanh (Hyperbolic Tangent)**

f(x)=tanh⁡(x)= `(2/(1+e^-2x))-1`
- Output: between **-1 and 1**
    
- Better than sigmoid (centered at 0)
    
- Still suffers from vanishing gradient
    

---

### 3. **ReLU (Rectified Linear Unit)**

f(x)=max⁡(0,x)

- If x > 0 → output x
    
- If x ≤ 0 → output 0
    
- Very popular in deep learning
    
- Problem: "dying ReLU" (some neurons stop learning if stuck at 0)
    

---

### 4. **Leaky ReLU**

`f(x)={x,0.01x​ ,if x>0, if x≤0​`


- Fixes ReLU problem by allowing a small negative slope
    

---

### 5. **Softmax**

`f(xi​)=e^xi/∑j​e^xj​​​`

- Used in **output layer** for classification
    
- Converts numbers into probabilities (sum = 1)
    

---

## 🔹 Summary (When to Use)

- **Sigmoid / Tanh** → old, good for small networks.
    
- **ReLU** → default for hidden layers.
    
- **Leaky ReLU** → fix ReLU problem.
    
- **Softmax** → final output for multi-class classification.
    

---

⚡ In short:  
**Activation functions decide whether a neuron should "fire" or not, and they make neural networks powerful enough to learn complex data.**

---
