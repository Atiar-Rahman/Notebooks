
  
**Video (Action / Activity) Recognition-এ আসলে অনেক model আছে** — আমি তোমাকে **complete + categorized list** দিচ্ছি, যেন তুমি বুঝতে পারো **কতগুলো আছে, কোনটা classical, কোনটা modern, কোনটা practical**।

---

# 🎥 Video Models – COMPLETE LIST (2026-ready)

## 🔵 A. Classical / Traditional (Baseline)

_(Low compute, old but still useful)_

1. **Optical Flow + SVM**
    
2. **HOG + HOF**
    
3. **Improved Dense Trajectories (IDT)**
    
4. **Bag of Visual Words (BoVW)**
    

📌 এখন mostly comparison / baseline হিসেবে use হয়

---

## 🟢 B. CNN-based (Frame / Short Clip)

5. **2D CNN + LSTM**
    
6. **2D CNN + GRU**
    
7. **CNN + Temporal Pooling**
    
8. **TSN (Temporal Segment Network)**
    

---

## 🔴 C. 3D CNN Models (Most Important 🔥)

9. **C3D**
    
10. **R3D (ResNet-3D)**
    
11. **R(2+1)D**
    
12. **P3D**
    
13. **I3D (Inflated 3D ConvNet)**
    
14. **X3D**
    
15. **3D DenseNet**
    
16. **3D MobileNet**
    
17. **MC3 (Mixed Conv3D)**
    

📌 **Most thesis projects stay here**

---

## 🟣 D. Two-Stream Models (RGB + Motion)

18. **Two-Stream CNN**
    
19. **Two-Stream I3D**
    
20. **TSM (Temporal Shift Module)**
    
21. **STM (Spatiotemporal Module)**
    

---

## 🟠 E. Multi-Pathway Models (Advanced)

22. **SlowFast**
    
23. **SlowOnly**
    
24. **FastOnly**
    
25. **OmniPath Networks**
    

⚠️ Mostly PyTorch, research-heavy

---

## 🟡 F. Transformer-Based Video Models (Modern 🚀)

26. **TimeSformer**
    
27. **Video Swin Transformer**
    
28. **ViViT**
    
29. **MViT (Multiscale Vision Transformer)**
    
30. **VideoMAE**
    
31. **Action Transformer**
    
32. **MaskFeat**
    

🔥 State-of-the-art but heavy

---

## 🔷 G. Lightweight / Mobile Models

33. **MoViNet (Google)**
    
34. **Tiny Video Networks**
    
35. **ShuffleNet-3D**
    
36. **MobileNetV3-3D**
    

📌 Best for **real-time + webcam**

---

## ⚫ H. Graph-Based Models (Skeleton / Pose)

37. **ST-GCN**
    
38. **2S-AGCN**
    
39. **PoseC3D**
    
40. **CTR-GCN**
    

📌 Uses OpenPose / MediaPipe

---

## 🟤 I. Self-Supervised / Pretraining Models

41. **VideoMAE (Self-supervised)**
    
42. **Masked Video Autoencoders**
    
43. **Contrastive Video Learning (CVRL)**
    
44. **SimCLR-Video**
    
45. **MoCo-Video**
    

---

## 🔢 TOTAL COUNT (Approx)

|Category|Count|
|---|---|
|Classical|4|
|CNN + RNN|4|
|3D CNN|9|
|Two-Stream|4|
|Multi-Path|4|
|Transformer|7|
|Lightweight|4|
|Graph-based|4|
|Self-supervised|5|

### ✅ **Total ≈ 45+ Video Models**

(Variants ধরলে 60+ হয়)

---

# 🏆 For YOU (Based on Your Background 👇)

তুমি যেহেতু  
✔ TensorFlow ব্যবহার করো  
✔ CPU-friendly চাই  
✔ Final-year / research project করছ

### 👉 BEST CHOICES

```
C3D
R(2+1)D
I3D-inspired
TSM
MoViNet
```

---

## 🔥 চাইলে আমি পারি:

1️⃣ **এই list টা PDF / thesis-ready table বানাতে**  
2️⃣ **TensorFlow-supported models mark করে দিতে**  
3️⃣ **Which model for which dataset (UCF101, Kinetics)**  
4️⃣ **Beginner → Advanced learning roadmap**  
5️⃣ **Webcam-ready model shortlist**

👉 বলো, কোনটা দরকার 😎


এটা খুবই smart প্রশ্ন 👌
**সবচেয়ে বড় skill হলো—কোনটা না করলেও সমস্যা নেই জানা** 😄
চল একদম **clear, no-nonsense skip list** দিই।

---

# 🚫 Video Models You Can **Skip Safely**

*(No guilt, no loss, still expert level)*

আমি 3 ভাগে ভাগ করেছি 👇

---

## ❌ 1️⃣ Definitely Skip (Outdated / Low ROI)

এইগুলো এখন **research বা industry-তে practically dead**:

* Optical Flow + SVM
* HOG / HOF
* Dense Trajectories
* BoVW

📌 Reason:

* Deep learning আসার আগে ছিল
* Implement করা কষ্ট + result poor
* CV/Thesis value নাই

✅ **100% skip**

---

## ❌ 2️⃣ Skip If Using TensorFlow + CPU

এইগুলো **heavy + PyTorch-biased**:

* SlowFast
* OmniPath
* MViT
* X3D (official impl)
* Action Transformer

📌 Reason:

* Mostly PyTorch only
* GPU mandatory
* TensorFlow support weak / unofficial

✅ **Skip unless future GPU + PyTorch plan থাকে**

---

## ❌ 3️⃣ Skip If You’re Not Doing Pose-Based Research

Skeleton / Pose based:

* ST-GCN
* 2S-AGCN
* CTR-GCN

📌 Reason:

* OpenPose / MediaPipe dependency
* Totally different pipeline
* Not needed for RGB surveillance

✅ **Skip unless human pose is core focus**

---

## ⚠️ 4️⃣ Optional Skip (Time Saver)

These are good models, but **similar concept already covered elsewhere**:

* P3D (covered by R(2+1)D)
* MC3 (covered by R3D)
* Two-Stream Optical Flow version
* FastOnly / SlowOnly

📌 Reason:

* Learning gain low
* Same idea, different name

---

# ✅ Models You SHOULD NOT Skip (Core Set 🔥)

If you do ONLY these, you’re **solid expert**:

### 🟢 MUST DO

* CNN + LSTM
* **C3D**
* **R(2+1)D**
* **I3D-inspired**
* **MoViNet** (real-time)

---

# 🧠 Final Safe List Summary

| Category         | Do / Skip        |
| ---------------- | ---------------- |
| Classical ML     | ❌ Skip           |
| CNN + LSTM       | ✅ Do             |
| 3D CNN Core      | ✅ Do             |
| Heavy Multi-path | ❌ Skip           |
| Transformers     | ❌ Skip (for now) |
| Lightweight      | ✅ Do             |
| Pose-based       | ❌ Skip           |

---

# 🏆 Golden Rule (Remember This)

> **Depth > Breadth**

7–8 models done properly

> 30 models done half-baked

---

## 👉 Next Step (Pick One)

**1️⃣** Final **model shortlist + learning order**
**2️⃣** Thesis-ready comparison table (accuracy, FPS, params)
**3️⃣** Unified framework starter code (TensorFlow)
**4️⃣** Real-time surveillance system design

বল, কোনটা নিয়ে আগাবো 😎



------------

# Image classification Model list
---

Are you asking for a **list of image classification models** used in deep learning and computer vision, or something more specific like **pretrained models available in libraries**? I’ll start with a comprehensive overview of the main ones:

---

### **Classic / Pioneering Models**

1. **LeNet-5 (1998)**
    
    - One of the first CNNs, used for digit recognition (MNIST).
        
    - Simple architecture: Conv → Pool → FC layers.
        
2. **AlexNet (2012)**
    
    - Won ImageNet 2012.
        
    - ReLU activations, dropout, and GPU training.
        
3. **VGGNet (2014)**
    
    - VGG16, VGG19.
        
    - Deep CNN with 3x3 conv filters stacked, simple and effective.
        
4. **GoogLeNet / Inception (2014)**
    
    - Introduced the **Inception module** (parallel convolutions).
        
    - Reduced computation compared to VGG.
        
5. **ResNet (2015)**
    
    - ResNet50, ResNet101, ResNet152.
        
    - Introduced **residual connections** to combat vanishing gradients.
        

---

### **Lightweight / Mobile-Friendly Models**

1. **MobileNet (v1, v2, v3)**
    
    - Depthwise separable convolutions for efficiency.
        
2. **SqueezeNet**
    
    - Very small model (~1.2M parameters) with similar accuracy to AlexNet.
        
3. **EfficientNet**
    
    - Scales depth, width, and resolution systematically.
        
    - EfficientNet-B0 to B7 variants.
        

---

### **Attention & Transformer-Based Models**

1. **Vision Transformer (ViT)**
    
    - Treats image patches like tokens in NLP transformers.
        
2. **Swin Transformer**
    
    - Hierarchical transformer with shifted windows.
        
3. **DeiT (Data-efficient Image Transformer)**
    
    - Efficient training with fewer data.
        
4. **ConvNeXt**
    
    - Modernized ResNet-style CNNs with some transformer design ideas.
        

---

### **Specialty / High-Performance Models**

1. **DenseNet**
    
    - Dense connections between layers to improve feature reuse.
        
2. **RegNet**
    
    - Network design with regular patterns; balances efficiency and accuracy.
        
3. **NFNet (Normalizing-Free Network)**
    
    - High accuracy without batch normalization.
        
4. **ResNeXt**
    
    - ResNet with “cardinality” (parallel paths) for better performance.
        

---

If you want, I can also **make a table with all these models showing parameters, top-1 accuracy on ImageNet, and inference speed** — it’s really handy for choosing a model.

Do you want me to make that table?