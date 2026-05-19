ঠিক আছে 😄  
আমি আপনাকে বানিয়ে দিচ্ছি **weekly roadmap** যেখানে:

- প্রতি সপ্তাহে শেখার **specific topics**
    
- ছোট **mini-project / practice task**
    
- শেষ সপ্তাহে পুরো **full project integration**
    

---

## **Week 1: Python & ML Basics**

**Topics to Learn:**

- Python basics: loops, functions, classes
    
- Numpy, Pandas
    
- Basic ML: supervised vs unsupervised, classification
    
- Loss functions: CrossEntropy
    

**Mini Project:**

- MNIST digit classification with simple fully connected NN (CPU)
    
- Visualize loss and accuracy
    

---

## **Week 2: Deep Learning & Framework Basics**

**Topics to Learn:**

- Neural networks: forward pass, backpropagation
    
- Activation functions: ReLU, Softmax
    
- TensorFlow / PyTorch basics: model creation, compile, fit, predict
    
- Dataset loading
    

**Mini Project:**

- Train a small CNN on CIFAR-10 (32x32 images)
    
- Evaluate accuracy and confusion matrix
    

---

## **Week 3: Video & Frame Processing**

**Topics to Learn:**

- OpenCV: video read/write, frame extraction, resize
    
- Normalize frames (0–1)
    
- Clip creation from sequential frames (rolling buffer)
    

**Mini Project:**

- Extract 10-frame clips from a short video and visualize frames
    
- Create a small dataset with 2 classes (normal vs abnormal action)
    

---

## **Week 4: 3D CNN / Temporal Models**

**Topics to Learn:**

- Conv3D, MaxPooling3D, GlobalAveragePooling3D
    
- Temporal modeling: clip input shape `(frames, H, W, C)`
    
- Lightweight 3D CNN architecture for CPU
    

**Mini Project:**

- Build a small 3D CNN in TensorFlow
    
- Train on mini 10-frame dataset from Week 3
    
- Evaluate on validation clips
    

---

## **Week 5: Training & Validation Pipeline**

**Topics to Learn:**

- Training loop, epochs, batch size
    
- Validation & accuracy calculation
    
- Model save / load
    

**Mini Project:**

- Train 3D CNN on mini UCF-Crime subset
    
- Save model and reload for evaluation
    
- Check validation accuracy
    

---

## **Week 6: Realtime Prediction / Inference**

**Topics to Learn:**

- Webcam capture using OpenCV
    
- Rolling buffer → clip → prediction
    
- Overlay prediction on frames
    
- CPU-friendly latency considerations
    

**Mini Project:**

- Real-time webcam demo with 3D CNN trained in Week 5
    
- Display predicted class on live video
    

---

## **Week 7: Optimization & Deployment**

**Topics to Learn:**

- CPU inference optimization (TensorFlow Lite / ONNX)
    
- Small frame size, small clip length
    
- Optional GPU usage for faster training
    
- Data augmentation for accuracy improvement
    

**Mini Project:**

- Optimize webcam demo for speed
    
- Try batch processing or TFLite export
    

---

## **Week 8: Full Project Integration**

**Full Project:**

- Dataset: UCF-Crime (all 14 classes)
    
- Frame → clip → tf.data.Dataset / PyTorch Dataset
    
- Model: Lightweight 3D CNN / SlowFast-lite
    
- Training + validation
    
- Model save/load
    
- Realtime webcam inference (rolling buffer, overlay)
    
- Accuracy report + demo
    

---

💡 **Extra Tips:**

- প্রতি mini-project শেষে **small report** লিখুন: accuracy, loss curve, FPS
    
- Full project-এর আগে mini-project experience আপনার confidence বাড়াবে
    

---

আপনি চাইলে আমি এই roadmap এর সাথে **একটি Excel / table format weekly checklist + mini-project description** বানিয়ে দিতে পারি, যাতে আপনি শুধু follow করে step-by-step project complete করতে পারেন।


---
চমৎকার 😄  
আমি আপনাকে বানিয়ে দিচ্ছি **Weekly Checklist + Mini-Project Description** টেবিল ফরম্যাটে, যাতে আপনি এক-এক করে follow করে সহজে project complete করতে পারেন।

---

|Week|Topics to Learn|Mini Project / Practice|Deliverable|
|---|---|---|---|
|1|Python basics (loops, functions, classes), Numpy, Pandas, ML basics (classification, loss functions)|MNIST digit classification with simple fully connected NN|Train MNIST model, visualize loss/accuracy|
|2|Deep learning basics: forward/backward pass, ReLU/Softmax, TensorFlow/PyTorch basics|Train small CNN on CIFAR-10|CNN model with accuracy/confusion matrix|
|3|Video processing: OpenCV video read/write, frame extraction, resizing, normalization, clip creation|Extract 10-frame clips from short video, visualize clips|Small dataset of clips (2 classes)|
|4|3D CNN / temporal modeling: Conv3D, MaxPool3D, GlobalAveragePooling3D, CPU-friendly architecture|Build lightweight 3D CNN, train on mini dataset|3D CNN trained on 10-frame clips|
|5|Training pipeline: epochs, batch size, validation, accuracy calculation, model save/load|Train 3D CNN on mini UCF-Crime subset|Saved model + validation accuracy report|
|6|Realtime inference: webcam capture, rolling buffer, clip → prediction, overlay on frame|Real-time webcam demo using trained 3D CNN|Live prediction overlay on webcam|
|7|Optimization & deployment: CPU inference optimization (TFLite/ONNX), frame/clip size, optional GPU|Optimize webcam demo for speed, try TFLite export|Fast CPU inference demo|
|8|Full Project Integration: UCF-Crime dataset (all classes), training, validation, save/load, realtime webcam prediction|Train full model on UCF-Crime, deploy realtime demo|Full project ready with accuracy report & demo|

---

💡 **Tips to Follow:**

1. প্রতি সপ্তাহে mini-project শেষ করার পর **report করুন:**
    
    - Training loss & accuracy
        
    - FPS / latency (CPU)
        
    - Any challenges faced
        
2. Mini-project experience আপনাকে **Week 8 Full Project** এর জন্য ready করবে।
    
3. CPU-only setup হলে **small frame size (64×64)** এবং **small batch size (1–2)** দিয়ে practice করুন।
    

---

যদি চান, আমি এই weekly roadmap এর সাথে **practical file/folder structure + sample code snippet** সহ একটি **ready-to-use template** বানিয়ে দিতে পারি, যাতে প্রতিটি mini-project এবং full project smooth হবে।

