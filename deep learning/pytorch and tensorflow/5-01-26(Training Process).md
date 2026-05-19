
# 🔁 Neural Network Training Process (Details)

## 1️⃣ Training Process কী?

**Training process** হলো এমন একটি ধাপসমূহের সিরিজ যেখানে
👉 একটি neural network **data থেকে শেখে**
👉 **loss কমায়**
👉 **weights & bias আপডেট করে**

🎯 Goal: **Minimum loss + Better accuracy**

---

## 2️⃣ Training Process–এর Overall Flow

```
Input Data
   ↓
Forward Propagation
   ↓
Loss Calculation
   ↓
Backward Propagation
   ↓
Weight Update (Optimizer)
   ↓
Repeat (Epochs)
```

---

## 3️⃣ Step-by-Step Training Process (Details)

---

## 🔹 Step 1: Data Input

* Training data: (X, y)
* X = features
* y = true label

```python
inputs, labels
```

---

## 🔹 Step 2: Forward Propagation

* Input → Layer → Activation → Output
* Model prediction তৈরি হয়

```python
outputs = model(inputs)
```

📌 কোনো weight update হয় না

---

## 🔹 Step 3: Loss Calculation

Loss = Prediction কতটা ভুল

### Common Loss Functions:

* Classification → CrossEntropyLoss
* Regression → MSELoss

```python
loss = loss_fn(outputs, labels)
```

🎯 Objective: Loss minimize করা

---

## 🔹 Step 4: Backward Propagation 🔥

* Loss থেকে gradients বের হয়
* Chain Rule ব্যবহার হয়

```python
loss.backward()
```

📌 `requires_grad=True` থাকা parameters-এর জন্য gradient হিসাব হয়

---

## 🔹 Step 5: Optimizer Step (Weight Update)

Optimizer gradients ব্যবহার করে weights আপডেট করে

```python
optimizer.step()
```

Formula:
[
w = w - \eta \frac{\partial L}{\partial w}
]

---

## 🔹 Step 6: Zero Gradient (Important ⚠️)

PyTorch-এ gradients accumulate হয়

```python
optimizer.zero_grad()
```

📌 নতুন iteration শুরু করার আগে অবশ্যই দিতে হবে

---

## 🔹 Step 7: Epoch Completion

* 1 epoch = পুরো dataset একবার model দিয়ে pass
* Training বহু epoch পর্যন্ত চলে

```python
for epoch in range(epochs):
```

---

## 4️⃣ Complete Training Loop (PyTorch)

```python
for epoch in range(epochs):
    optimizer.zero_grad()
    
    outputs = model(inputs)
    loss = loss_fn(outputs, labels)
    
    loss.backward()
    optimizer.step()
```

---

## 5️⃣ Training vs Validation

| Training         | Validation     |
| ---------------- | -------------- |
| Weight update হয় | Update হয় না   |
| `model.train()`  | `model.eval()` |
| Gradient আছে     | Gradient নেই   |

```python
with torch.no_grad():
    val_output = model(val_data)
```

---

## 6️⃣ Key Training Hyperparameters 🔥

| Parameter     | Role                |
| ------------- | ------------------- |
| Epochs        | Training repetition |
| Batch size    | Data chunk size     |
| Learning rate | Step size           |
| Optimizer     | Weight update rule  |
| Loss function | Error measurement   |

---

## 7️⃣ Batch Training Types

| Type          | Description               |
| ------------- | ------------------------- |
| Batch GD      | Full dataset              |
| Mini-batch GD | Small batch (most common) |
| Stochastic GD | One sample                |

---

## 8️⃣ Overfitting & Underfitting

| Problem      | Cause             |
| ------------ | ----------------- |
| Overfitting  | Too complex model |
| Underfitting | Too simple model  |

### Solutions:

* Regularization
* Dropout
* Early stopping

---

## 9️⃣ Training Stopping Criteria

* Fixed epochs
* Validation loss stops improving
* Early stopping

---

## 🔟 Exam-Ready Answer (5–8 Marks)

> **The training process of a neural network consists of forward propagation, loss computation, backward propagation, and weight update using an optimizer. This process is repeated for multiple epochs until the loss is minimized and the model achieves good performance.**

---

## Viva One-Liners 🔥

* Training = learning weights
* Forward pass → prediction
* Backward pass → gradient
* Optimizer updates parameters
* Epoch = one full dataset pass

---

## Diagram Summary (Easy Memory)

```
Input → Model → Output
           ↓
         Loss
           ↓
        Backward
           ↓
       Optimizer
```

---


# 📦 Dataset & DataLoader (PyTorch)

---

## 1️⃣ Dataset কী?

**Dataset** হলো এমন একটি object যা:

* Data সংরক্ষণ করে
* একেকটি sample কীভাবে load হবে সেটা define করে

👉 Dataset বলে দেয়

> “একটা sample কেমন হবে?”

---

## 2️⃣ PyTorch-এ Dataset এর ধরন

### 🔹 (A) Built-in Dataset

PyTorch কিছু dataset আগেই দেয়:

* MNIST
* CIFAR-10
* Fashion-MNIST
* ImageNet

```python
from torchvision.datasets import MNIST
```

---

### 🔹 (B) Custom Dataset (🔥 Exam favorite)

নিজের dataset বানাতে হলে:
👉 `torch.utils.data.Dataset` inherit করতে হয়

---

## 3️⃣ Custom Dataset – Required Methods

| Method          | কাজ               |
| --------------- | ----------------- |
| `__init__()`    | Data load         |
| `__len__()`     | Total samples     |
| `__getitem__()` | One sample return |

---

### 🔸 Custom Dataset Example

```python
from torch.utils.data import Dataset

class MyDataset(Dataset):
    def __init__(self, data, labels):
        self.data = data
        self.labels = labels

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]
```

📌 PyTorch internally `__getitem__()` call করে

---

## 4️⃣ DataLoader কী?

**DataLoader**:

* Dataset থেকে data নেয়
* Batch তৈরি করে
* Shuffle করে
* Parallel loading করে

👉 DataLoader বলে দেয়

> “Data কীভাবে model-এ যাবে?”

---

## 5️⃣ DataLoader কেন দরকার?

Without DataLoader ❌:

* Manual batch
* Slow training

With DataLoader ✅:

* Faster training
* Automatic batching
* GPU efficient

---

## 6️⃣ DataLoader Parameters (🔥 Important)

```python
from torch.utils.data import DataLoader

loader = DataLoader(
    dataset,
    batch_size=32,
    shuffle=True,
    num_workers=2
)
```

| Parameter     | Meaning                    |
| ------------- | -------------------------- |
| `batch_size`  | Samples per batch          |
| `shuffle`     | Data randomize             |
| `num_workers` | Parallel loading           |
| `drop_last`   | Last incomplete batch drop |

---

## 7️⃣ Dataset vs DataLoader (Difference)

| Dataset           | DataLoader      |
| ----------------- | --------------- |
| Data define করে   | Data load করে   |
| One sample return | Batch return    |
| Static            | Dynamic         |
| No shuffle        | Shuffle support |

---

## 8️⃣ Training Loop-এ DataLoader ব্যবহার

```python
for inputs, labels in dataloader:
    outputs = model(inputs)
    loss = loss_fn(outputs, labels)
    loss.backward()
    optimizer.step()
    optimizer.zero_grad()
```

---

## 9️⃣ Transform in Dataset (Images)

Images-এর জন্য `transform` খুব গুরুত্বপূর্ণ

```python
from torchvision import transforms

transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])
```

```python
dataset = MNIST(root='./data',
                train=True,
                transform=transform)
```

---

## 🔟 Map-Style vs Iterable-Style Dataset

| Type      | Description             |
| --------- | ----------------------- |
| Map-style | `__getitem__()` ব্যবহার |
| Iterable  | Stream data             |

---

## 1️⃣1️⃣ Dataset Split (Train / Test)

```python
from torch.utils.data import random_split

train_ds, test_ds = random_split(dataset, [8000, 2000])
```

---

## 1️⃣2️⃣ Real-Life Example (Easy Memory)

* **Dataset** = Book
* **DataLoader** = Pages reader (batch wise)

---

## 🔥 Exam Answer (5 Marks)

> **In PyTorch, Dataset defines how individual data samples are accessed, while DataLoader handles batching, shuffling, and parallel loading of data during training, making model training efficient and scalable.**

---

## Viva One-Liners

* Dataset = data source
* DataLoader = data feeder
* Dataset returns sample
* DataLoader returns batch

---

## Common Mistakes ⚠️

❌ Forgetting `__len__()`
❌ Forgetting `__getitem__()`
❌ `shuffle=False` in training
❌ Too many `num_workers`

---

## 🔚 Short Summary

```
Dataset → Single Sample
DataLoader → Batch of Samples
```

---
# ✅ How to Use **Any Dataset** to Create a DataLoader (PyTorch)

আমি **৩টা common case** দেখাচ্ছি — যেকোনো dataset এটাই follow করলে হবে।

---

## 🟢 CASE 1: Dataset already in memory (NumPy / Tensor)

### Step 1️⃣ Import

```python
import torch
from torch.utils.data import Dataset, DataLoader
```

### Step 2️⃣ Create Custom Dataset

```python
class CustomDataset(Dataset):
    def __init__(self, X, y):
        self.X = torch.tensor(X, dtype=torch.float32)
        self.y = torch.tensor(y)

    def __len__(self):
        return len(self.X)

    def __getitem__(self, idx):
        return self.X[idx], self.y[idx]
```

### Step 3️⃣ Create DataLoader

```python
dataset = CustomDataset(X, y)

dataloader = DataLoader(
    dataset,
    batch_size=32,
    shuffle=True
)
```

✔️ Done — model ready to train

---

## 🟢 CASE 2: Dataset from files (CSV / Excel) 🔥 (Very common)

### Example: CSV Dataset

#### Step 1️⃣ Read CSV

```python
import pandas as pd

data = pd.read_csv("data.csv")
X = data.iloc[:, :-1].values
y = data.iloc[:, -1].values
```

#### Step 2️⃣ Custom Dataset

```python
class CSVDataset(Dataset):
    def __init__(self, X, y):
        self.X = torch.tensor(X, dtype=torch.float32)
        self.y = torch.tensor(y)

    def __len__(self):
        return len(self.X)

    def __getitem__(self, idx):
        return self.X[idx], self.y[idx]
```

#### Step 3️⃣ DataLoader

```python
dataset = CSVDataset(X, y)
loader = DataLoader(dataset, batch_size=64, shuffle=True)
```

---

## 🟢 CASE 3: Image Dataset (Folder structure) 🔥🔥

```
dataset/
 ├── cat/
 ├── dog/
```

### Step 1️⃣ Use ImageFolder

```python
from torchvision.datasets import ImageFolder
from torchvision import transforms
```

### Step 2️⃣ Transform

```python
transform = transforms.Compose([
    transforms.Resize((224,224)),
    transforms.ToTensor()
])
```

### Step 3️⃣ Dataset + DataLoader

```python
dataset = ImageFolder("dataset/", transform=transform)

loader = DataLoader(
    dataset,
    batch_size=16,
    shuffle=True,
    num_workers=2
)
```

---

## 🟢 CASE 4: Text Dataset (Basic)

```python
class TextDataset(Dataset):
    def __init__(self, texts, labels):
        self.texts = texts
        self.labels = labels

    def __len__(self):
        return len(self.texts)

    def __getitem__(self, idx):
        return self.texts[idx], self.labels[idx]
```

➡️ Tokenization সাধারণত model-এর আগে করা হয়

---

## 🟡 Training Loop Example (Universal)

```python
for inputs, labels in dataloader:
    outputs = model(inputs)
    loss = loss_fn(outputs, labels)
    loss.backward()
    optimizer.step()
    optimizer.zero_grad()
```

---

## 🔥 Dataset → DataLoader Flow (Easy Memory)

```
Raw Data → Dataset → DataLoader → Model
```

---

## 🧠 Exam Answer (5 Marks)

> **To create a DataLoader from any dataset in PyTorch, the dataset must be wrapped inside a Dataset class implementing `__len__()` and `__getitem__()` methods. The DataLoader then batches, shuffles, and loads the data efficiently during training.**

---

## Viva One-Liners

* Dataset defines sample
* DataLoader defines batch
* Custom dataset = flexibility
* DataLoader = performance

---

## ⚠️ Common Mistakes

❌ Forgetting tensor conversion
❌ Wrong dtype
❌ No shuffle during training
❌ Wrong folder structure (images)

---

## 🔚 One-Line Summary

> **Any dataset → wrap in Dataset → pass to DataLoader**

---

নিচে **PyTorch-এ Train–Validation Split**–এর **complete, exam-friendly, step-by-step explanation** দেওয়া হলো 👇
(🔥 neural network training-এর সবচেয়ে important step)

---

# 🟢 Train–Validation Split in PyTorch

---

## 1️⃣ কেন Train–Validation Split দরকার?

* **Train Set:** Model শেখে
* **Validation Set:** Model evaluate হয়, unseen data এর উপর performance check করার জন্য
* Prevents **overfitting**

> **Tip:** Test set আলাদা রাখা উচিত final evaluation এর জন্য

---

## 2️⃣ Split করার সাধারণ Ratio

| Split      | Ratio  |
| ---------- | ------ |
| Train      | 70–80% |
| Validation | 20–30% |

---

## 3️⃣ Method 1: Using `torch.utils.data.random_split`

```python
from torch.utils.data import random_split, DataLoader

dataset = CustomDataset(X, y)

train_size = int(0.8 * len(dataset))
val_size = len(dataset) - train_size

train_dataset, val_dataset = random_split(dataset, [train_size, val_size])

train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
val_loader = DataLoader(val_dataset, batch_size=32, shuffle=False)
```

📌 Note:

* Train: shuffle=True
* Validation: shuffle=False (evaluation)

---

## 4️⃣ Method 2: Using `sklearn.model_selection.train_test_split`

```python
from sklearn.model_selection import train_test_split

X_train, X_val, y_train, y_val = train_test_split(
    X, y, test_size=0.2, random_state=42
)

train_dataset = CustomDataset(X_train, y_train)
val_dataset = CustomDataset(X_val, y_val)

train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
val_loader = DataLoader(val_dataset, batch_size=32, shuffle=False)
```

✅ Useful when data is in **NumPy / Pandas**

---

## 5️⃣ Image Dataset Split (Folder Structure)

ImageFolder + Subset Example:

```python
from torchvision.datasets import ImageFolder
from torch.utils.data import random_split

dataset = ImageFolder("dataset/", transform=transform)

train_size = int(0.8 * len(dataset))
val_size = len(dataset) - train_size
train_dataset, val_dataset = random_split(dataset, [train_size, val_size])
```

---

## 6️⃣ Training Loop with Validation

```python
for epoch in range(epochs):
    # Training
    model.train()
    for inputs, labels in train_loader:
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = loss_fn(outputs, labels)
        loss.backward()
        optimizer.step()
    
    # Validation
    model.eval()
    with torch.no_grad():
        val_loss = 0
        for inputs, labels in val_loader:
            outputs = model(inputs)
            loss = loss_fn(outputs, labels)
            val_loss += loss.item()
    val_loss /= len(val_loader)
    print(f"Epoch {epoch+1}, Val Loss: {val_loss}")
```

📌 Key Points:

* `model.train()` → training mode (Dropout active)
* `model.eval()` → evaluation mode (Dropout off)
* `torch.no_grad()` → no gradient calculation (memory efficient)

---

## 7️⃣ Common Mistakes

* Validation loader-এ shuffle=True ❌
* Using same dataset for train & validation ❌
* Forgetting `model.eval()` during validation ❌

---

## 8️⃣ Exam Answer (5–8 Marks)

> **Train–Validation Split divides the dataset into two parts: training set for learning and validation set for evaluating model performance. In PyTorch, it can be done using `random_split` or `sklearn`’s `train_test_split`. The training loader uses shuffle=True, while the validation loader uses shuffle=False.**

---

## 9️⃣ Viva One-Liners

* Train set = model learns
* Validation set = model performance check
* `random_split` = PyTorch method
* Always `model.eval()` for validation

---

## 🔚 Short Summary (Easy Memory)

```
Dataset → Split → Train Loader / Validation Loader → Model
```

---

নিচে **PyTorch-এ Neural Network এর Training Loop**–এর **complete, step-by-step, exam + viva-ready explanation** দেওয়া হলো 👇
(🔥 খুবই গুরুত্বপূর্ণ topic – সব exam ও project এ লাগে)

---

# 🔁 Training Loop in PyTorch (Complete Details)

---

## 1️⃣ Training Loop কি?

**Training loop** হলো এমন একটি কোড structure যেখানে:

* Model **forward pass** করে
* **Loss calculate** করে
* **Backward pass** করে (gradients বের করে)
* **Optimizer step** ব্যবহার করে weights update করে
* একাধিক epoch ধরে repeat করা হয়

> লক্ষ্য: **Loss minimize + Accuracy increase**

---

## 2️⃣ Training Loop এর Step-by-Step Flow

```
1️⃣ Epoch Loop Start
2️⃣ Model.train() → set training mode
3️⃣ Batch Loop Start
4️⃣ optimizer.zero_grad() → reset gradients
5️⃣ Forward Pass → outputs = model(inputs)
6️⃣ Compute Loss → loss = loss_fn(outputs, labels)
7️⃣ Backward Pass → loss.backward()
8️⃣ Optimizer Step → optimizer.step()
9️⃣ Batch Loop End
10️⃣ Validation Loop (optional) → model.eval()
11️⃣ Epoch Loop End
```

---

## 3️⃣ Complete PyTorch Training Loop Example

```python
import torch
import torch.nn as nn
from torch.utils.data import DataLoader

# Assume: model, train_loader, val_loader, loss_fn, optimizer defined

epochs = 10

for epoch in range(epochs):
    # ==================== Training ====================
    model.train()  # Training mode
    running_loss = 0.0
    
    for inputs, labels in train_loader:
        inputs, labels = inputs.to(device), labels.to(device)
        
        optimizer.zero_grad()           # Reset gradients
        outputs = model(inputs)         # Forward pass
        loss = loss_fn(outputs, labels) # Compute loss
        loss.backward()                 # Backward pass (gradients)
        optimizer.step()                # Update weights
        
        running_loss += loss.item()
    
    avg_train_loss = running_loss / len(train_loader)
    
    # ==================== Validation ====================
    model.eval()  # Evaluation mode
    val_loss = 0.0
    correct = 0
    total = 0
    with torch.no_grad():  # Disable gradient calculation
        for inputs, labels in val_loader:
            inputs, labels = inputs.to(device), labels.to(device)
            outputs = model(inputs)
            loss = loss_fn(outputs, labels)
            val_loss += loss.item()
            
            # For classification accuracy
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()
    
    avg_val_loss = val_loss / len(val_loader)
    val_accuracy = 100 * correct / total
    
    print(f"Epoch [{epoch+1}/{epochs}], "
          f"Train Loss: {avg_train_loss:.4f}, "
          f"Val Loss: {avg_val_loss:.4f}, "
          f"Val Accuracy: {val_accuracy:.2f}%")
```

---

## 4️⃣ Key Components Explained

| Component               | Explanation                                                    |
| ----------------------- | -------------------------------------------------------------- |
| `model.train()`         | Enables training mode (Dropout & BatchNorm active)             |
| `model.eval()`          | Evaluation mode (Dropout off, BatchNorm in eval mode)          |
| `optimizer.zero_grad()` | Clear accumulated gradients                                    |
| `loss.backward()`       | Compute gradients                                              |
| `optimizer.step()`      | Update weights using gradients                                 |
| `torch.no_grad()`       | Disable gradient calculation for validation (memory efficient) |

---

## 5️⃣ Optional: Learning Rate Scheduler

```python
from torch.optim.lr_scheduler import StepLR

scheduler = StepLR(optimizer, step_size=5, gamma=0.1)

for epoch in range(epochs):
    # Training...
    scheduler.step()  # Adjust learning rate
```

---

## 6️⃣ Things to Monitor

* Training loss decreasing ✅
* Validation loss decreasing ✅
* Validation accuracy increasing ✅
* Watch out for overfitting ❌

---

## 7️⃣ Common Mistakes (Exam / Viva Alert ⚠️)

* Forgetting `model.train()` / `model.eval()`
* Forgetting `optimizer.zero_grad()`
* Calculating accuracy without `torch.no_grad()`
* Using same dataset for train & validation

---

## 8️⃣ Exam Answer (5–8 Marks)

> **The training loop in PyTorch is a repetitive process where the model performs forward propagation to generate predictions, calculates the loss, performs backward propagation to compute gradients, and updates the model parameters using an optimizer. This loop runs for multiple epochs, optionally evaluating the model on a validation set after each epoch.**

---

## 9️⃣ Viva One-Liners

* **Forward pass = prediction**
* **Backward pass = gradients**
* **Optimizer step = weight update**
* **model.train() = training mode**
* **model.eval() = evaluation mode**

---

## 10️⃣ Diagram (Easy Memory)

```
[Input Batch] → [Model] → [Output]
       ↓             ↑
       └─ Loss ─ Backprop ─ Optimizer
```

---

নিচে **PyTorch-এ Neural Network Evaluation / Validation Loop**–এর **complete, exam + viva-ready explanation** দেওয়া হলো 👇
(🔥 Training-এর পর evaluation বুঝতে হলে অবশ্যই জানতেই হবে)

---

# 🟢 Evaluation / Validation Loop in PyTorch

---

## 1️⃣ Evaluation Loop কি?

**Evaluation loop** হলো এমন একটি process যেখানে:

* Model নতুন বা validation data-এ run করা হয়
* **Predictions generate করা হয়**
* **Loss এবং metrics** (accuracy, F1-score, etc.) calculate করা হয়
* Weight update হয় না (no learning)

> উদ্দেশ্য: Model কতটা ভালো perform করছে unseen data-এ তা দেখার জন্য

---

## 2️⃣ Evaluation এর Step-by-Step Flow

```
1️⃣ model.eval() → Set evaluation mode
2️⃣ torch.no_grad() → Disable gradient calculation
3️⃣ Loop through validation/test loader
4️⃣ Forward pass: outputs = model(inputs)
5️⃣ Compute loss: loss_fn(outputs, labels)
6️⃣ Compute metrics: accuracy, precision, etc.
7️⃣ Aggregate results over all batches
```

---

## 3️⃣ Complete PyTorch Evaluation Loop Example

```python
import torch

# Assume: model, val_loader, loss_fn already defined
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model.eval()  # Set evaluation mode
val_loss = 0.0
correct = 0
total = 0

with torch.no_grad():  # Disable gradients for evaluation
    for inputs, labels in val_loader:
        inputs, labels = inputs.to(device), labels.to(device)
        
        outputs = model(inputs)           # Forward pass
        loss = loss_fn(outputs, labels)  # Compute loss
        val_loss += loss.item()           # Accumulate loss
        
        # Compute accuracy
        _, predicted = torch.max(outputs.data, 1)
        total += labels.size(0)
        correct += (predicted == labels).sum().item()

# Average loss and accuracy
avg_val_loss = val_loss / len(val_loader)
val_accuracy = 100 * correct / total

print(f'Validation Loss: {avg_val_loss:.4f}, Accuracy: {val_accuracy:.2f}%')
```

---

## 4️⃣ Key Points Explained

| Component                  | Explanation                                                         |
| -------------------------- | ------------------------------------------------------------------- |
| `model.eval()`             | Sets model to evaluation mode (Dropout off, BatchNorm in eval mode) |
| `torch.no_grad()`          | Prevents gradient calculation → saves memory & speeds up evaluation |
| `outputs = model(inputs)`  | Forward pass only                                                   |
| `loss_fn(outputs, labels)` | Measure error on validation set                                     |
| Metrics (`accuracy, F1`)   | Evaluate model performance                                          |

---

## 5️⃣ Metrics Commonly Used

* **Classification:** Accuracy, Precision, Recall, F1-score, Confusion Matrix
* **Regression:** MSE, MAE, R²

```python
from sklearn.metrics import accuracy_score

y_true = [...]
y_pred = [...]
accuracy_score(y_true, y_pred)
```

---

## 6️⃣ Training + Evaluation Combined

Training loop usually includes evaluation at the end of each epoch:

```python
for epoch in range(epochs):
    # ----- Training -----
    model.train()
    for inputs, labels in train_loader:
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = loss_fn(outputs, labels)
        loss.backward()
        optimizer.step()
    
    # ----- Validation -----
    model.eval()
    with torch.no_grad():
        val_loss = 0
        correct = 0
        total = 0
        for inputs, labels in val_loader:
            outputs = model(inputs)
            loss = loss_fn(outputs, labels)
            val_loss += loss.item()
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()
    print(f"Epoch {epoch+1}, Val Loss: {val_loss/len(val_loader):.4f}, Val Accuracy: {100*correct/total:.2f}%")
```

---

## 7️⃣ Common Mistakes (Exam / Viva Alert ⚠️)

* Forgetting `model.eval()` ❌ → Dropout/BatchNorm behave incorrectly
* Using `optimizer.step()` or `loss.backward()` ❌
* Forgetting `torch.no_grad()` ❌ → Extra memory usage
* Computing accuracy incorrectly ❌

---

## 8️⃣ Exam Answer (5–8 Marks)

> **An evaluation loop in PyTorch runs the trained model on validation or test data to measure performance. During evaluation, `model.eval()` is called to disable Dropout and BatchNorm updates, and `torch.no_grad()` is used to save memory. Loss and metrics such as accuracy are computed for each batch and averaged over the entire dataset.**

---

## 9️⃣ Viva One-Liners

* **model.eval() → evaluation mode**
* **torch.no_grad() → no gradients**
* **Loss measures performance**
* **Metrics check accuracy / F1 / error**
* **No weight updates in evaluation**

---

## 10️⃣ Easy Memory Diagram

```
[Validation/Test Loader] → [Model.eval()] → [Forward Pass] → [Loss & Metrics]
```

---
নিচে **PyTorch-এ Model Accuracy & Loss Tracking**–এর **complete, exam + viva-ready explanation** দেওয়া হলো 👇
(🔥 খুবই গুরুত্বপূর্ণ – training evaluation ও plotting এর জন্য)

---

# 📊 Model Accuracy & Loss Tracking in PyTorch

---

## 1️⃣ কেন Tracking দরকার?

Training/validation চলাকালীন:

* **Loss tracking:** Shows how well the model is learning
* **Accuracy tracking:** Shows model performance on classification tasks
* **Helps detect:** overfitting, underfitting, learning stagnation

> Goal: Visualize & monitor training progress

---

## 2️⃣ Variables to Track

```python
train_losses = []
val_losses = []
train_accuracies = []
val_accuracies = []
```

* Store **per epoch** loss & accuracy
* Later plot using `matplotlib`

---

## 3️⃣ Training + Validation Loop with Tracking

```python
import torch
import matplotlib.pyplot as plt

train_losses, val_losses = [], []
train_acc, val_acc = [], []

for epoch in range(epochs):
    # --------- Training ---------
    model.train()
    running_loss = 0
    correct = 0
    total = 0
    for inputs, labels in train_loader:
        inputs, labels = inputs.to(device), labels.to(device)
        
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = loss_fn(outputs, labels)
        loss.backward()
        optimizer.step()
        
        running_loss += loss.item()
        _, predicted = torch.max(outputs.data, 1)
        total += labels.size(0)
        correct += (predicted == labels).sum().item()
    
    train_losses.append(running_loss / len(train_loader))
    train_acc.append(100 * correct / total)
    
    # --------- Validation ---------
    model.eval()
    val_loss = 0
    correct = 0
    total = 0
    with torch.no_grad():
        for inputs, labels in val_loader:
            inputs, labels = inputs.to(device), labels.to(device)
            outputs = model(inputs)
            loss = loss_fn(outputs, labels)
            val_loss += loss.item()
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()
    
    val_losses.append(val_loss / len(val_loader))
    val_acc.append(100 * correct / total)
    
    print(f"Epoch {epoch+1}, "
          f"Train Loss: {train_losses[-1]:.4f}, "
          f"Val Loss: {val_losses[-1]:.4f}, "
          f"Train Acc: {train_acc[-1]:.2f}%, "
          f"Val Acc: {val_acc[-1]:.2f}%")
```

---

## 4️⃣ Plotting Loss & Accuracy

```python
# Plot Loss
plt.figure(figsize=(12,5))
plt.subplot(1,2,1)
plt.plot(train_losses, label='Train Loss')
plt.plot(val_losses, label='Validation Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.legend()
plt.title('Loss vs Epoch')

# Plot Accuracy
plt.subplot(1,2,2)
plt.plot(train_acc, label='Train Accuracy')
plt.plot(val_acc, label='Validation Accuracy')
plt.xlabel('Epoch')
plt.ylabel('Accuracy (%)')
plt.legend()
plt.title('Accuracy vs Epoch')
plt.show()
```

📌 Visualization helps detect:

* Overfitting: train_loss ↓ but val_loss ↑
* Underfitting: train_loss & val_loss high
* Good fit: train_loss ≈ val_loss ↓

---

## 5️⃣ Tips for Accurate Tracking

* Always **use `model.eval()`** for validation
* Use **`torch.no_grad()`** for validation/test
* Track **metrics per epoch**, not per batch
* Save best model weights based on validation loss

---

## 6️⃣ Optional: Advanced Tracking

* **TensorBoard**

```python
from torch.utils.tensorboard import SummaryWriter
writer = SummaryWriter()

writer.add_scalar('Loss/train', train_loss, epoch)
writer.add_scalar('Loss/val', val_loss, epoch)
writer.add_scalar('Accuracy/train', train_acc, epoch)
writer.add_scalar('Accuracy/val', val_acc, epoch)
```

* **Weights & Gradients visualization**

---

## 7️⃣ Exam Answer (5–8 Marks)

> **Model accuracy and loss tracking involves recording the loss and evaluation metrics of a model during training and validation for each epoch. This helps monitor learning progress, detect overfitting or underfitting, and visualize performance. In PyTorch, losses and accuracies are appended to lists and plotted using tools like matplotlib or TensorBoard.**

---

## 8️⃣ Viva One-Liners

* **Loss shows model error**
* **Accuracy shows correct predictions**
* **Track train & val separately**
* **Plot for visualization**
* **Overfitting = train↑, val↓**

---

## 🔚 Easy Memory Diagram

```
Epoch Loop
 ├── Training → train_loss, train_acc
 └── Validation → val_loss, val_acc
       ↓
   Plot / Monitor
```

---

