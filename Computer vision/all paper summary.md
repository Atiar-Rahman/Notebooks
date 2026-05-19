
#  **“Suspicious Activity Detection in Surveillance Footage”** (ICECTA 2019) 

---

## 📝 Paper Summary

**1. Paper Information**

- **Title:** Suspicious Activity Detection in Surveillance Footage
    
- **Authors:** Sathyajit Loganathan, Gayashan Kariyawasam, Prasanna Sumathipala
    
- **Publication:** 2019 International Conference on Electrical and Computing Technologies and Applications (ICECTA)
    
- **DOI / Source:** IEEE Xplore
    

**2. Keywords**

- Gun Detection, Abandoned Luggage Detection, Computer Vision, Surveillance
    

**3. Background / Motivation**

- Urban areas face rising crime rates, requiring reliable surveillance.
    
- Manual monitoring is tiring and prone to errors.
    
- AI-powered intelligent surveillance systems can reduce risks but require breaking down tasks into simpler components.
    
- This study focuses on **two critical suspicious activities**:
    
    1. **Gun-based crimes**
        
    2. **Abandoned luggage detection**
        

**4. Objectives**

- Detect guns in surveillance footage to prevent gun-related crimes.
    
- Detect abandoned luggage in public areas to prevent terrorist threats.
    

**5. Methodology / Approach**  
**A. Gun Detection**

- Dataset: 3908 images (from IMFDB, Soft Computing datasets, YouTube, Google Images).
    
- Test data: 100 surveillance frames + benchmark dataset.
    
- Preprocessing: Manual bounding-box annotation, XML conversion.
    
- Model: **Faster R-CNN (TensorFlow, Inception v2 backbone, pretrained on MS-COCO)**, fine-tuned on custom gun dataset.
    
- Training time: ~20 hours on GPU.
    

**B. Abandoned Luggage Detection**

- Step 1: **Static Object Detection** using double background subtraction.
    
- Step 2: **Validation** with **ResNet-101** (MS-COCO pretrained) to classify stationary objects as luggage or not.
    
- Tested on **PETS 2006 dataset** with different scenarios and difficulty levels.
    

**6. Results / Findings**  
**Gun Detection**

- Training accuracy: **91.3%**, Testing accuracy: **89.4%**
    
- Confusion matrix showed good classification (low false positives).
    
- Able to detect guns in real surveillance-like scenarios.
    

**Abandoned Luggage Detection**

- Achieved **low false alarm rate** and high detection rate.
    
- Computation time: ~0.2s per frame → suitable for real-time.
    
- Worked well across PETS sequences, except under sudden illumination changes.
    

**7. Contributions**

- Developed a **deep neural network gun detector** fine-tuned on limited but realistic datasets.
    
- Proposed a **two-step luggage detection pipeline** combining background subtraction + deep learning validation.
    
- Demonstrated **real-time applicability** with high accuracy and efficiency.
    

**8. Limitations / Weaknesses**

- Gun detection limited by dataset size and diversity.
    
- System performance decreases in crowded or highly dynamic environments.
    
- Abandoned luggage detector struggles with sudden illumination changes.
    

**9. Future Work**

- Try different architectures for faster gun detection.
    
- Improve real-time performance for resource-constrained devices.
    
- Incorporate multimodal data (beyond video).
    
- Address robustness under illumination changes for luggage detection.
    

**10. Conclusion**

- The paper presents a **practical approach for intelligent surveillance** by targeting high-risk activities (guns and abandoned luggage).
    
- Both methods show **high accuracy and computational efficiency**, making them suitable for integration into real-time surveillance systems.
    
- The proposed techniques can **significantly enhance public safety** by providing automated early warning of potential threats.
    

---




#  **“Re-purposing Machine Learning Models: A Human Action Recognition Model Turned Violence Detector” (IEEE LACCI 2023)** 

---

# 📝 Complete Paper Summary

**1. Paper Information**

- **Title:** Re-purposing Machine Learning Models: A Human Action Recognition Model Turned Violence Detector
    
- **Authors:** Letícia Portela, Angel Ayala, Bruno Fernandes, Igor Farias, Gervásio Neto, Mouglas Eugenio Nasário Gomes
    
- **Publication:** IEEE Latin American Conference on Computational Intelligence (LACCI), 2023
    
- **DOI:** 10.1109/LACCI58595.2023.10409475
    

**2. Keywords**

- Model Re-purposing, Violence Detection, Human Action Recognition (HAR), Anomaly Detection, Computer Vision
    

**3. Background / Motivation**

- Human Action Recognition (HAR) is widely used in computer vision for identifying human activities.
    
- Training HAR models requires large datasets (e.g., Kinetics400/600), but **violence detection datasets are scarce** and often lack diversity.
    
- Existing violence datasets (e.g., Hockey Fights, Violent Scenes) are small and not realistic enough.
    
- Motivation: **Instead of training from scratch**, reuse powerful pre-trained HAR models to detect violent vs. non-violent activities.
    

**4. Objectives**

- Re-purpose existing HAR models for violence detection.
    
- Reduce dependence on large labeled violence datasets.
    
- Test performance on real-world violence detection datasets.
    

**5. Methodology / Approach**

- **Base Models:**
    
    - **ST-GCN (Spatial-Temporal Graph Convolutional Network):** Uses skeleton data, pretrained on Kinetics400. Paired with **SVM classifier**.
        
    - **MoViNet (Mobile Video Network):** Lightweight, efficient video CNN, pretrained on Kinetics600. Paired with **MLP classifier**.
        
- **Datasets:**
    
    - **UCF-Crime:** 1900 surveillance videos, 128 hours, 13 anomaly classes (benchmark dataset).
        
    - **Brazilian Violence (BV):** Real-life local surveillance videos (fights + normal actions).
        
- **Pre-processing:**
    
    - Videos segmented into 1-second clips.
        
    - UCF-Crime: manual labeling of violence segments (since only video-level labels available).
        
    - Both datasets split into **70% training, 30% testing**.
        
- **Evaluation Metrics:**
    
    - ROC Curve & AUC
        
    - Cohen’s Kappa (agreement score)
        
    - Accuracy, Sensitivity (Recall), Specificity, Precision
        

**6. Results / Findings**

- **ST-GCN + SVM**:
    
    - AUC: 0.93 (UCF-Crime), 0.80 (BV), 0.93 (combined)
        
    - Accuracy: 0.75 (UCF), 0.81 (BV)
        
    - High Sensitivity (0.93–0.96) → detects violent cases well.
        
    - Very low Precision (as low as 0.03) → too many false positives.
        
- **MoViNet + MLP**:
    
    - AUC: 0.96 (UCF), 0.99 (BV), 0.96 (combined)
        
    - Accuracy: 0.78 (UCF), 0.94 (BV)
        
    - Sensitivity: 0.89–0.97 (very good at detecting positives).
        
    - Specificity: up to 0.93 (good at detecting negatives).
        
    - Precision: still low (0.03–0.52) → imbalance problem.
        
    - BV dataset better classified by MoViNet than ST-GCN.
        

**7. Main Contributions**

- Demonstrated how **pre-trained HAR models can be repurposed** for violence detection without full retraining.
    
- Proposed two architectures: **ST-GCN + SVM** and **MoViNet + MLP**.
    
- Achieved **high AUC scores** across both datasets, showing good classification ability.
    
- Showed potential for **real-time violence detection in surveillance systems**.
    

**8. Limitations / Weaknesses**

- Very low **precision** → too many false alarms in real-world deployment.
    
- Low **Kappa scores** → predictions not well-aligned with actual labels.
    
- Datasets are unbalanced (normal > violent videos).
    
- UCF-Crime labeling is coarse (video-level, not frame-level).
    

**9. Future Work**

- Improve classifier calibration to balance precision vs. recall.
    
- Explore better dataset balancing or synthetic data generation.
    
- Extend model evaluation to other real-world datasets.
    
- Fine-tune or hybrid-train HAR models for better violence-specific performance.
    

**10. Conclusion**

- Re-purposing HAR models for violence detection is **feasible and effective**.
    
- Both ST-GCN and MoViNet achieved **high AUC and sensitivity**, making them good at detecting violent actions.
    
- However, **false alarms remain a major issue**, requiring future refinement.
    
- The study shows a **cost-effective and resource-efficient way** to adapt pre-trained models for public safety applications.
    

---
#  **“Real-time Human Activity Recognition Using ResNet and 3D Convolutional Neural Networks” (ACCESS 2021)** 

---

# 📝 Paper Summary

**1. Paper Information**

- **Title:** Real-time Human Activity Recognition Using ResNet and 3D Convolutional Neural Networks
    
- **Authors:** Archana N., Hareesh K.
    
- **Publication:** 2021 2nd International Conference on Advances in Computing, Communication, Embedded and Secure Systems (ACCESS)
    
- **DOI:** 10.1109/ACCESS51619.2021.9563316
    

**2. Keywords**

- Real-time Human Activity Recognition, Spatio-temporal Features, 3D CNN, ResNet-18, Kinetics-400 Dataset
    

**3. Background / Motivation**

- Human activity recognition (HAR) is essential for computer vision applications (surveillance, healthcare, etc.).
    
- Traditional methods (optical flow, handcrafted features) are limited in handling complex scenarios.
    
- Deep learning (CNN, LSTM, 3D CNN) improved HAR, but **LSTM-attention models are computationally heavy** for real-time.
    
- Motivation: Design a **lightweight and accurate real-time HAR system** using only **ResNet + 3D CNN** (no LSTM).
    

**4. Objectives**

- Develop a real-time HAR system combining **ResNet-18** and **3D CNN**.
    
- Achieve high accuracy while reducing overfitting and computational cost.
    
- Validate on a large-scale dataset (Kinetics-400).
    

**5. Methodology / Approach**

- **Model:** Modified ResNet-18 integrated with **3D CNN** for extracting both **spatial + temporal features**.
    
- **Dataset:** **Kinetics-400**, containing 400 action classes (e.g., cooking, sports, person-person interactions).
    
- **Data split:** 80% training, 20% testing.
    
- **Data Augmentation:** random rotation, horizontal/vertical flips, etc., to avoid overfitting.
    
- **Training:** 16-frame video clips, gradient descent optimizer, backpropagation with cross-entropy loss.
    
- **Implementation:** TensorFlow + Keras; real-time inference via sliding window over video frames.
    

**6. Results / Findings**

- **ResNet-18 + 3D CNN** effectively captured **spatio-temporal features**.
    
- Training accuracy improved with more iterations; after ~50 iterations, loss stabilized (no gradient vanishing due to ResNet skip connections).
    
- The Kinetics-400 dataset’s diversity helped prevent overfitting.
    
- Correct predictions included activities like _drawing_ and _balloon blowing_, while failures occurred in some visually similar actions.
    
- Demonstrated **real-time inference capability** with reliable recognition.
    

**7. Contributions**

- Proposed a real-time HAR framework without LSTM/attention mechanisms.
    
- Combined **ResNet-18 (residual learning)** with **3D CNN** for efficient spatio-temporal feature learning.
    
- Validated effectiveness using large-scale dataset (Kinetics-400).
    

**8. Limitations**

- Some misclassifications in visually similar or complex activities.
    
- Performance can still degrade under heavy occlusion or camera motion.
    
- Not tested on smaller, real-world surveillance datasets.
    

**9. Conclusion**

- The proposed **ResNet-18 + 3D CNN** model improves HAR reliability for real-time applications.
    
- Achieved **robust accuracy** and reduced overfitting compared to traditional deep models.
    
- Useful in applications like **surveillance, prison monitoring, healthcare activity recognition**.
    
- Future scope: extending to more lightweight architectures for edge devices and adapting to uncontrolled real-world environments.
    

---

#  "Human Activity Recognition System from Different Poses with CNN "

---

# 📝 Paper Summary

---

### 1. Paper Information

**Title:** Human Activity Recognition System from Different Poses with CNN  
**Authors:** Md. Atikuzzaman, Tarafder Razibur Rahman, Eashita Wazed, Md. Parvez Hossain, Md. Zahidul Islam  
**Published in:** 2nd International Conference on Sustainable Technologies for Industry 4.0 (STI), Dhaka, 2020

---

### 2. Keywords

Human Activity Recognition, CNN, HAAR Classifier, Pose Detection, Video Frame Recognition

---

### 3. Background / Motivation

- Human Activity Recognition (HAR) is useful in health monitoring, elder care, fitness, and surveillance.
    
- Sensor-based approaches (wearables, mobile devices) are not always practical, especially for elderly people.
    
- Vision-based recognition (using cameras) is a promising alternative but requires accurate detection and efficient recognition.
    

---

### 4. Objectives / Aim

- Develop a **vision-based HAR system** that detects humans from videos/images and recognizes activities.
    
- Achieve **high accuracy and efficiency** while minimizing computation time.
    
- Recognize **five human activities**: Walking, Running, Standing, Sitting, Laying.
    

---

### 5. Methodology / Approach

The system has **three modules**:

1. **Human Pose Detection** – Used HAAR Feature-based Classifier to detect humans in frames.
    
2. **Human Pose Segmentation** – Cropped detected humans and resized to 64×64 pixels.
    
3. **Activity Recognition** – Applied Convolutional Neural Network (CNN) for classification.
    

- **Dataset:** 5648 images collected from CCTV/laptop cameras in varying environments (indoor, outdoor, day, night).
    
- **Preprocessing:** Converted RGB → grayscale, resized to 64×64.
    
- **CNN Architecture:** Multiple Conv2D, Batch Normalization, ReLU, MaxPooling, Dropout, Dense layers.
    
- **Training/Validation split:** 80% training, 20% testing.
    

---

### 6. Experiments / Implementation

- Dataset distribution:
    
    - Laying: 566 images
        
    - Running: 1016 images
        
    - Sitting: 1152 images
        
    - Standing: 1591 images
        
    - Walking: 1323 images
        
- Hardware: 4GB RAM, Core i5 CPU (no GPU).
    
- Training done for **20 epochs**.
    

---

### 7. Results / Findings

- **Human Pose Detection (HAAR classifier):** 99.86% accuracy.
    
- **Activity Recognition (CNN classifier):** 99.82% accuracy.
    
- CNN achieved good convergence (low train/validation loss).
    
- Confusion matrix: Only **2 misclassifications** across all classes.
    
- Precision & Recall: ~100% across all activity types.
    

---

### 8. Main Contributions

- Developed a **hybrid HAR system** (HAAR + CNN).
    
- Demonstrated **state-of-the-art accuracy (≈99.8%)** for vision-based HAR.
    
- Showed HAR can be implemented **without high-end GPUs** using grayscale inputs.
    

---

### 9. Limitations / Weaknesses

- Recognizes only **five activities**.
    
- Dataset size is limited and lacks diversity in lighting/weather.
    
- System trained on grayscale images only (not RGB).
    
- Performance may drop on more complex or large-scale datasets.
    

---

### 10. Future Work / Open Issues

- Expand dataset with more diverse activities, lighting, and weather conditions.
    
- Train on **RGB images** using GPUs for deeper CNN architectures.
    
- Extend system to detect more complex activities/events.
    
- Develop real-time applications for **surveillance, healthcare, and smart environments**.
    

---

### 11. Conclusion

- Proposed HAR system achieved **99.82% recognition accuracy** and **99.86% detection accuracy**.
    
- The system is practical for monitoring and surveillance applications.
    
- With more data and GPU support, performance and scalability can be further improved.
    

---

**visual workflow diagram** (showing Dataset → Detection → Segmentation → CNN → Prediction → Results