
# project title: 
## Real Time Suspicious Behavior Detection System using CCTV Footage

#### main Goal:
CCTV ভিডিও থেকে real-time এ suspicious vs normal behavior detect করা এবং alert দেওয়া।



## Core Components / pipeline
- **Video Input**
    
    - Live CCTV (RTSP) বা stored video
        
- **Person Detection**
    
    - **YOLOv8** → মানুষ detect করবে
        
- **Person Tracking**
    
    - **Deep SORT** → একই মানুষকে frame-to-frame track করবে
        
- **Action / Behavior Recognition**
    
    - **CNN + LSTM** অথবা
        
    - **SlowFast / I3D** (advanced)
        
    - Classes: `Suspicious` vs `Normal`
        
- **(Optional – Bonus)**
    
    - Anomaly Detection (ConvLSTM / GANomaly)
        
- **Alert System**
    
    - Suspicious হলে:
        
        - bounding box red
            
        - label + confidence
            
        - future scope: sound / notification

### Dataset Plan
UCF Crime Dataset

Images / video থেকে:

-  Suspicious
-  Normal

### 🛠️ **Tech Stack**

- **Backend / ML**: Python, PyTorch, OpenCV
- **Models**: YOLOv8, Deep SORT, CNN-LSTM
- **API**: Django REST Framework
- **Deployment**: PC / GPU (future: Jetson)
### 📊 Evaluation
- Accuracy
- Precision, Recall, F1-score
- Confusion Matrix
- Real-time FPS
### 📌 Final Deliverables
- Trained model (.pth)
- Full pipeline code
- Django REST API
- Demo video
- Report + architecture diagram


খুব ভালো প্রশ্ন 👍
**সংক্ষিপ্ত উত্তর:**
👉 **হ্যাঁ, database রাখা উচিত** — কিন্তু **heavy না**, smart ভাবে।

এটা examiner + viva দুই জায়গাতেই plus point হবে।

---

## ❓ Database কেন লাগবে?

Real-time detection নিজে নিজে DB ছাড়াও চলতে পারে, কিন্তু **final year project হিসেবে DB থাকলে projectটা complete & professional দেখায়**।

Database লাগবে মূলত:

1. **Detected suspicious events log রাখতে**
2. **Video / camera info store করতে**
3. **Future analysis + report generate করতে**
4. **Admin dashboard বানাতে (future scope)**

---

## 🧠 Database না রাখলে কী হবে?

* Real-time demo চলবে ✔️
* কিন্তু:

  * History থাকবে না ❌
  * Analytics দেখাতে পারবে না ❌
  * Examiner বলবে: *“Data persist কোথায়?”* ❌

👉 তাই **DB recommended**

---

## 🗄️ Recommended Database

* **SQLite** (simple, final year enough) ✅
* বা **PostgreSQL / MySQL** (extra plus)

👉 Django হলে default SQLite দিয়েই শুরু করো।

---

## 🧩 Database Design (Simple & Clean)

### 1️⃣ Camera Table

```text
Camera
------
id (PK)
camera_name
location
stream_url
is_active
created_at
```

**কেন লাগবে?**

* Multiple CCTV support
* Location-wise alert

---

### 2️⃣ Detection Event Table (MOST IMPORTANT)

```text
DetectionEvent
--------------
id (PK)
camera_id (FK)
event_type        (Suspicious / Normal)
confidence_score
frame_image_path
timestamp
```

**Use:**

* কবে suspicious detect হলো
* Confidence কত ছিল
* Screenshot দেখানো

---

### 3️⃣ Person Track Table (Optional – Bonus)

```text
PersonTrack
-----------
id (PK)
event_id (FK)
track_id
start_time
end_time
```

**Use:**

* Same person কতক্ষণ suspicious ছিল

---

### 4️⃣ System Log (Optional)

```text
SystemLog
---------
id (PK)
message
log_type
created_at
```

---

## 🎯 Minimum Database (Exam-safe version)

👉 যদি কম রাখতে চাও, **এই ২টা টেবিলই যথেষ্ট**:

✅ Camera
✅ DetectionEvent

---

## 🧪 Example Django Model (Simple)

```python
class DetectionEvent(models.Model):
    EVENT_CHOICES = (
        ('suspicious', 'Suspicious'),
        ('normal', 'Normal'),
    )

    camera_name = models.CharField(max_length=100)
    event_type = models.CharField(max_length=20, choices=EVENT_CHOICES)
    confidence = models.FloatField()
    image = models.ImageField(upload_to='events/')
    created_at = models.DateTimeField(auto_now_add=True)
```

---

## 🧠 Viva-Ready Answer (Examiner বললে)

> **Q:** Database কেন ব্যবহার করছো?
> **A:**
> “To store detected events for auditing, future analysis, and alert history. It also enables scalability for multi-camera environments.”

---

## 🔮 Future Scope (Mention করলে extra mark)

* Event analytics dashboard
* Heatmap of suspicious zones
* Police / authority notification system

---

### এখন বলো 👇

👉 **তুমি simple version রাখবে নাকি advanced DB design চাও?**
আমি চাইলে:

* ER Diagram এঁকে দেব
* Django models + migrations
* API endpoints design করে দেব





