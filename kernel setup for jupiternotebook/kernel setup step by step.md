To set up a **virtual environment (venv)** for TensorFlow and make it available as a Jupyter/IPython kernel, follow these steps:

---

### 🛠 Steps (Linux/Mac/Windows)

#### 1. Create and activate venv

```bash
# Create venv (choose your folder name, e.g. tf_env)
python -m venv tf_env

# Activate venv
# Windows (PowerShell):
tf_env\Scripts\activate
# Linux/Mac:
source tf_env/bin/activate
```

#### 2. Upgrade pip

```bash
pip install --upgrade pip
```

#### 3. Install TensorFlow (latest stable version)

```bash
pip install tensorflow
```

👉 If you have GPU support and compatible drivers, install GPU version:

```bash
pip install tensorflow[and-cuda]
```

#### 4. Install Jupyter + IPython kernel

```bash
pip install jupyter ipykernel
```

#### 5. Add the venv as a Jupyter kernel

```bash
python -m ipykernel install --user --name=tf_env --display-name "Python (tf_env)"
```

- `--name=tf_env`: internal name of kernel
    
- `--display-name "Python (tf_env)"`: how it appears in Jupyter Notebook/Lab
    

#### 6. Run Jupyter Notebook

```bash
jupyter notebook
```

Then select **Kernel → Change Kernel → Python (tf_env)**.

---

### ✅ Verify TensorFlow

In a notebook cell, run:

```python
import tensorflow as tf
print(tf.__version__)
print("GPU available:", tf.config.list_physical_devices('GPU'))
```

---

Do you want me to also give you a **ready one-liner setup script** (so you can just copy–paste and create the whole venv + kernel at once)?



চমৎকার 👍  
আপনার venv এর path হলো:

```
/home/atiar/venv-folder/tf_env
```

মানে আপনার **Python executable** আছে এখানে:

```
/home/atiar/venv-folder/tf_env/bin/python
```

---

## 🔹 VS Code এ সেটআপ করার ধাপ

### 1. Jupyter kernel register করুন (একবারই লাগবে)

টার্মিনালে run করুন:

```bash
/home/atiar/venv-folder/tf_env/bin/python -m ipykernel install --user --name=tf_env --display-name "Python (tf_env)"
```

এখন Jupyter/VS Code list এ **Python (tf_env)** নামে আসবে।

---

### 2. Project ফোল্ডার খুলুন

VS Code → `File → Open Folder` → আপনার project folder (`~/projects/my_project/` ইত্যাদি)।

---

### 3. Kernel select করুন

- Notebook (`.ipynb`) খুললে উপরে **Select Kernel** বাটনে click করুন।
    
- Kernel list থেকে **Python (tf_env)** choose করুন।
    

👉 যদি না আসে → “Enter interpreter path” ক্লিক করুন → এই path দিন:

```
/home/atiar/venv-folder/tf_env/bin/python
```

---

### 4. (Optional) VS Code auto-config (`.vscode/settings.json`)

Project folder এর ভেতরে `.vscode/settings.json` ফাইল বানান এবং লিখুন:

```json
{
    "python.defaultInterpreterPath": "/home/atiar/venv-folder/tf_env/bin/python",
    "jupyter.pythonInterpreter": "/home/atiar/venv-folder/tf_env/bin/python"
}
```

এবার থেকে project খুললেই VS Code আপনার TensorFlow venv automatically select করবে ✅

---

### 5. Verify

Notebook cell বা Python ফাইলে run করুন:

```python
import sys, tensorflow as tf
print(sys.executable)  # /home/atiar/venv-folder/tf_env/bin/python হওয়া উচিত
print(tf.__version__)
```

---

👉 এখন আপনার tf_env external folder থেকেও VS Code এ smooth কাজ করবে।

আপনি কি চান আমি `.vscode/settings.json` ফাইলটা আপনাকে full ready-to-use বানিয়ে দিই যাতে একেবারে কপি–পেস্ট করলেই হয়ে যায়?