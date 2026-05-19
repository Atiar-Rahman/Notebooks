Absolutely! For **image datasets**, you can split into **train / validation / test** in multiple ways depending on how your images are stored. I’ll explain step by step.

---

## **1️⃣ If you have images in folders by class**

Suppose your dataset looks like this:

```
dataset/
    cats/
        cat1.jpg
        cat2.jpg
        ...
    dogs/
        dog1.jpg
        dog2.jpg
        ...
```

You want to split into **train, val, test** folders like:

```
dataset_split/
    train/
        cats/
        dogs/
    val/
        cats/
        dogs/
    test/
        cats/
        dogs/
```

Here’s a Python example using `os` and `shutil`:

```python
import os
import shutil
import random

# Original dataset folder
dataset_dir = "dataset"
# Where to save split dataset
output_dir = "dataset_split"

# Split ratios
train_ratio = 0.7
val_ratio = 0.15
test_ratio = 0.15

# Create folders
for split in ['train', 'val', 'test']:
    for cls in os.listdir(dataset_dir):
        os.makedirs(os.path.join(output_dir, split, cls), exist_ok=True)

# Split and copy images
for cls in os.listdir(dataset_dir):
    images = os.listdir(os.path.join(dataset_dir, cls))
    random.shuffle(images)

    n_total = len(images)
    n_train = int(n_total * train_ratio)
    n_val = int(n_total * val_ratio)

    train_imgs = images[:n_train]
    val_imgs = images[n_train:n_train+n_val]
    test_imgs = images[n_train+n_val:]

    for img in train_imgs:
        shutil.copy(os.path.join(dataset_dir, cls, img),
                    os.path.join(output_dir, 'train', cls, img))
    for img in val_imgs:
        shutil.copy(os.path.join(dataset_dir, cls, img),
                    os.path.join(output_dir, 'val', cls, img))
    for img in test_imgs:
        shutil.copy(os.path.join(dataset_dir, cls, img),
                    os.path.join(output_dir, 'test', cls, img))
```

✅ This will create **train/val/test splits with folders** ready for PyTorch or TensorFlow.

---

## **2️⃣ Using TensorFlow `image_dataset_from_directory` directly**

If you don’t want to manually copy files, TensorFlow can do it **on the fly**:

```python
import tensorflow as tf

dataset_dir = "dataset"

train_ds = tf.keras.utils.image_dataset_from_directory(
    dataset_dir,
    validation_split=0.3,  # 30% for val+test
    subset="training",
    seed=42,
    image_size=(224, 224),
    batch_size=32
)

val_ds = tf.keras.utils.image_dataset_from_directory(
    dataset_dir,
    validation_split=0.3,
    subset="validation",
    seed=42,
    image_size=(224, 224),
    batch_size=32
)
```

> Note: This gives **train and validation**. If you want a **separate test set**, you can either reserve a folder for it or do another split.

---

## **3️⃣ PyTorch `ImageFolder` + `random_split`**

```python
from torchvision import datasets, transforms
from torch.utils.data import random_split, DataLoader

transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor()
])

dataset = datasets.ImageFolder("dataset", transform=transform)

train_size = int(0.7 * len(dataset))
val_size = int(0.15 * len(dataset))
test_size = len(dataset) - train_size - val_size

train_ds, val_ds, test_ds = random_split(dataset, [train_size, val_size, test_size])

train_loader = DataLoader(train_ds, batch_size=32, shuffle=True)
val_loader = DataLoader(val_ds, batch_size=32)
test_loader = DataLoader(test_ds, batch_size=32)
```

✅ This is clean and avoids copying files.

---

