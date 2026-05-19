Here’s a simple implementation of **Linear Regression using PyTorch** from scratch (no high-level wrappers like `nn.Linear`).

---

## 1️⃣ Using Basic PyTorch Tensors (From Scratch)

```python
import torch

# Generate dummy dataset
torch.manual_seed(42)
X = torch.randn(100, 1)  # 100 samples, 1 feature
true_w = torch.tensor([[3.0]])
true_b = torch.tensor([2.0])

y = X @ true_w + true_b + 0.1 * torch.randn(100, 1)

# Initialize parameters (requires_grad=True to compute gradients)
w = torch.randn(1, 1, requires_grad=True)
b = torch.randn(1, requires_grad=True)

# Hyperparameters
learning_rate = 0.01
epochs = 100

for epoch in range(epochs):
    # Forward pass
    y_pred = X @ w + b
    
    # Mean Squared Error Loss
    loss = torch.mean((y_pred - y) ** 2)
    
    # Backward pass
    loss.backward()
    
    # Update weights (Gradient Descent)
    with torch.no_grad():
        w -= learning_rate * w.grad
        b -= learning_rate * b.grad
        
        # Zero gradients
        w.grad.zero_()
        b.grad.zero_()
    
    if (epoch + 1) % 10 == 0:
        print(f"Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}")

print("\nLearned parameters:")
print("w =", w.item())
print("b =", b.item())
```

---

## 2️⃣ Using `torch.nn.Module` (Recommended Way)

```python
import torch
import torch.nn as nn
import torch.optim as optim

# Generate dataset
torch.manual_seed(42)
X = torch.randn(100, 1)
y = 3 * X + 2 + 0.1 * torch.randn(100, 1)

# Define model
class LinearRegression(nn.Module):
    def __init__(self):
        super().__init__()
        self.linear = nn.Linear(1, 1)

    def forward(self, x):
        return self.linear(x)

model = LinearRegression()

# Loss and optimizer
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)

# Training loop
epochs = 100
for epoch in range(epochs):
    # Forward pass
    y_pred = model(X)
    loss = criterion(y_pred, y)

    # Backward pass
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    if (epoch + 1) % 10 == 0:
        print(f"Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}")

# Print learned parameters
for name, param in model.named_parameters():
    print(name, param.data)
```

---

## Key Concepts Used

- `requires_grad=True` → enables automatic differentiation
    
- `loss.backward()` → computes gradients
    
- `torch.no_grad()` → disables gradient tracking during updates
    
- `optimizer.step()` → updates model parameters
    
- `nn.Linear` → built-in linear layer
    
- `nn.MSELoss()` → Mean Squared Error loss
    

---

If you'd like, I can also show:

- ✅ Linear regression with **multiple features**
    
- ✅ Mini-batch training with `DataLoader`
    
- ✅ Visualization using matplotlib
    
- ✅ Closed-form solution comparison (Normal Equation)*


Here’s **Linear Regression with Multiple Features** in PyTorch.

We’ll assume:

- ( X ) shape → `(num_samples, num_features)`
    
- ( w ) shape → `(num_features, 1)`
    
- ( y ) shape → `(num_samples, 1)`
    

---

# 1️⃣ From Scratch (Manual Gradient Descent)

```python
import torch

# Reproducibility
torch.manual_seed(42)

# Create dummy dataset
n_samples = 200
n_features = 3

X = torch.randn(n_samples, n_features)

true_w = torch.tensor([[2.0], [-3.0], [4.0]])
true_b = torch.tensor([5.0])

y = X @ true_w + true_b + 0.5 * torch.randn(n_samples, 1)

# Initialize parameters
w = torch.randn(n_features, 1, requires_grad=True)
b = torch.randn(1, requires_grad=True)

# Hyperparameters
learning_rate = 0.01
epochs = 200

for epoch in range(epochs):
    
    # Forward pass
    y_pred = X @ w + b
    
    # MSE Loss
    loss = torch.mean((y_pred - y) ** 2)
    
    # Backward pass
    loss.backward()
    
    # Update
    with torch.no_grad():
        w -= learning_rate * w.grad
        b -= learning_rate * b.grad
        
        w.grad.zero_()
        b.grad.zero_()
    
    if (epoch + 1) % 20 == 0:
        print(f"Epoch {epoch+1}, Loss: {loss.item():.4f}")

print("\nLearned weights:\n", w)
print("Learned bias:\n", b)
```

---

# 2️⃣ Using `nn.Module` (Recommended Approach)

```python
import torch
import torch.nn as nn
import torch.optim as optim

torch.manual_seed(42)

# Dataset
n_samples = 200
n_features = 3

X = torch.randn(n_samples, n_features)
true_w = torch.tensor([[2.0], [-3.0], [4.0]])
true_b = 5.0
y = X @ true_w + true_b + 0.5 * torch.randn(n_samples, 1)

# Model
model = nn.Linear(n_features, 1)

# Loss & Optimizer
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)

# Training
epochs = 200
for epoch in range(epochs):
    
    y_pred = model(X)
    loss = criterion(y_pred, y)
    
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
    
    if (epoch + 1) % 20 == 0:
        print(f"Epoch {epoch+1}, Loss: {loss.item():.4f}")

print("\nLearned parameters:")
print("Weights:\n", model.weight.data)
print("Bias:\n", model.bias.data)
```

---

# 📌 Mathematical Form

For multiple features:

[  
y = Xw + b  
]

Where:

- ( X \in \mathbb{R}^{m \times n} )
    
- ( w \in \mathbb{R}^{n \times 1} )
    
- ( b \in \mathbb{R} )
    
- ( m ) = samples
    
- ( n ) = features
    

---

# 🚀 Common Interview Follow-Up

If asked:

- What changes from single feature?  
    → Only weight dimension changes from `(1,1)` to `(n_features,1)`
    
- Why matrix multiplication works?  
    → Each sample row multiplies the weight vector
    

---

Below is a **complete end-to-end Linear Regression example using a real dataset** (multiple features) in PyTorch.

We’ll use the classic **California Housing dataset** from `sklearn`.

---

# 📌 Full Working Example (Train + Test + Evaluation)

## ✅ Step 1: Import Libraries

```python
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader, TensorDataset

from sklearn.datasets import fetch_california_housing
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import numpy as np
```

---

## ✅ Step 2: Load Dataset

```python
# Load dataset
data = fetch_california_housing()

X = data.data          # Features (8 features)
y = data.target        # House prices

# Convert to 2D target
y = y.reshape(-1, 1)
```

---

## ✅ Step 3: Train-Test Split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

## ✅ Step 4: Feature Scaling (Very Important)

```python
scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

---

## ✅ Step 5: Convert to PyTorch Tensors

```python
X_train = torch.tensor(X_train, dtype=torch.float32)
y_train = torch.tensor(y_train, dtype=torch.float32)

X_test = torch.tensor(X_test, dtype=torch.float32)
y_test = torch.tensor(y_test, dtype=torch.float32)
```

---

## ✅ Step 6: Create DataLoader (Mini-batch Training)

```python
train_dataset = TensorDataset(X_train, y_train)
train_loader = DataLoader(train_dataset, batch_size=64, shuffle=True)
```

---

## ✅ Step 7: Define Model

```python
input_size = X_train.shape[1]  # 8 features

model = nn.Linear(input_size, 1)
```

---

## ✅ Step 8: Loss & Optimizer

```python
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)
```

---

## ✅ Step 9: Training Loop

```python
epochs = 100

for epoch in range(epochs):
    for xb, yb in train_loader:
        
        predictions = model(xb)
        loss = criterion(predictions, yb)
        
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
    
    if (epoch+1) % 10 == 0:
        print(f"Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}")
```

---

## ✅ Step 10: Evaluate on Test Data

```python
model.eval()
with torch.no_grad():
    test_predictions = model(X_test)
    test_loss = criterion(test_predictions, y_test)

print("\nTest MSE:", test_loss.item())
```

---

# 🎯 What This Example Covers

✔ Real dataset  
✔ Multiple features (8 features)  
✔ Train/Test split  
✔ Feature scaling  
✔ Mini-batch training  
✔ Model evaluation

---

# 📊 Expected Output

Test MSE should be around:

```
~0.5 to 0.6 (approx)
```

(depending on random initialization)

---

If you want, I can also show:

- 📈 R² score calculation
    
- 🔍 How to interpret learned weights
    
- ⚡ GPU version
    
- 🧠 Add regularization (Ridge/L2)
    
- 🔄 Save & load the trained model
    

Tell me which one you want 🙂