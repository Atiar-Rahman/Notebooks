
Done ✅  
আমি তোমার **Realtime Suspicious Behaviour Detection** final year project এর জন্য complete, production-ready **database schema design** করে দিয়েছি।

এটা কভার করে:

- CCTV camera management
    
- Video storage
    
- Person detection & DeepSORT tracking
    
- Action recognition (CNN-LSTM / SlowFast)
    
- Suspicious event detection
    
- Alerts & notifications
    
- Model versioning & inference logs
    



# 📊 Database Schema Design

**Project:** Realtime Suspicious Behaviour Detection using CCTV

This schema is suitable for **Django + PostgreSQL/MySQL** and supports:

* Multiple cameras
* Video storage
* Person tracking
* Suspicious event detection
* Alerts & logs
* Model versioning

---

## 1️⃣ User & Role Management

### **users**

| Field      | Type                          | Description     |
| ---------- | ----------------------------- | --------------- |
| id         | PK                            | User ID         |
| username   | varchar                       | Login username  |
| email      | varchar                       | Email           |
| password   | varchar                       | Hashed password |
| role       | enum(admin, operator, viewer) | Access level    |
| is_active  | boolean                       | Account status  |
| created_at | timestamp                     | Created time    |

---

## 2️⃣ Camera Management

### **cameras**

| Field      | Type                  | Description       |
| ---------- | --------------------- | ----------------- |
| id         | PK                    | Camera ID         |
| name       | varchar               | Camera name       |
| location   | varchar               | Physical location |
| rtsp_url   | text                  | RTSP stream URL   |
| status     | enum(active,inactive) | Camera status     |
| fps        | int                   | Frame rate        |
| created_at | timestamp             | Added time        |

---

## 3️⃣ Video Storage (RTSP + Upload)

### **videos**

| Field       | Type                                         | Description                      |
| ----------- | -------------------------------------------- | -------------------------------- |
| id          | PK                                           | Video ID                         |
| camera_id   | FK → cameras.id (nullable)                   | Source camera (null if uploaded) |
| source_type | enum(rtsp, upload)                           | Video source                     |
| file_path   | text                                         | Video file path                  |
| uploaded_by | FK → users.id                                | Who uploaded                     |
| start_time  | timestamp                                    | Recording start                  |
| end_time    | timestamp                                    | Recording end                    |
| duration    | float                                        | Duration (sec)                   |
| status      | enum(pending, processing, completed, failed) | Processing state                 |
| created_at  | timestamp                                    | Upload/record time               |

------|-----|------------|
| id | PK | Video ID |
| camera_id | FK → cameras.id | Source camera |
| file_path | text | Video file path |
| start_time | timestamp | Recording start |
| end_time | timestamp | Recording end |
| duration | float | Duration (sec) |

---

## 4️⃣ Person Detection & Tracking

### **persons**

| Field      | Type      | Description       |
| ---------- | --------- | ----------------- |
| id         | PK        | Person ID         |
| camera_id  | FK        | Camera source     |
| track_id   | int       | DeepSORT track ID |
| first_seen | timestamp | First appearance  |
| last_seen  | timestamp | Last appearance   |

---

## 5️⃣ Activity / Action Recognition

### **activities**

| Field      | Type            | Description      |
| ---------- | --------------- | ---------------- |
| id         | PK              | Activity ID      |
| person_id  | FK → persons.id | Person           |
| label      | varchar         | Action name      |
| confidence | float           | Prediction score |
| start_time | timestamp       | Action start     |
| end_time   | timestamp       | Action end       |

---

## 6️⃣ Suspicious Events

### **events**

| Field          | Type                                        | Description          |
| -------------- | ------------------------------------------- | -------------------- |
| id             | PK                                          | Event ID             |
| camera_id      | FK                                          | Camera               |
| person_id      | FK                                          | Person involved      |
| event_type     | enum(fight, theft, fall, intrusion, normal) | Type                 |
| confidence     | float                                       | Detection confidence |
| frame_snapshot | text                                        | Image path           |
| event_time     | timestamp                                   | Occurrence time      |
| status         | enum(pending, verified, false_alarm)        | Review status        |

---

## 7️⃣ Alerts & Notifications

### **alerts**

| Field           | Type                 | Description         |
| --------------- | -------------------- | ------------------- |
| id              | PK                   | Alert ID            |
| event_id        | FK → events.id       | Linked event        |
| alert_type      | enum(email,sms,push) | Alert medium        |
| sent_at         | timestamp            | Sent time           |
| is_acknowledged | boolean              | Acknowledged or not |

---

## 8️⃣ Model Management

### **models**

| Field      | Type      | Description       |
| ---------- | --------- | ----------------- |
| id         | PK        | Model ID          |
| model_name | varchar   | YOLOv8 / CNN-LSTM |
| version    | varchar   | v1.0              |
| accuracy   | float     | Model accuracy    |
| file_path  | text      | Model file        |
| created_at | timestamp | Trained time      |

---

## 9️⃣ Inference Logs

### **inference_logs**

| Field          | Type      | Description |
| -------------- | --------- | ----------- |
| id             | PK        | Log ID      |
| model_id       | FK        | Model used  |
| camera_id      | FK        | Camera      |
| inference_time | float     | Time (ms)   |
| created_at     | timestamp | Timestamp   |

---

## 🔗 Relationships Summary

* **Camera → Videos → Persons → Activities → Events → Alerts**
* **Models → Inference Logs**
* One camera can generate many videos, persons & events

---

## ✅ Django Apps Suggestion

* accounts
* cameras
* videos
* detection
* alerts
* models

---

## 🔥 Optional (Advanced)

* Heatmap table
* Zone-based rules
* Anomaly score table
* Audit logs

---


 system এ দুইভাবে video যাবে:

---

## 🎥 Video Source Types (Clear Logic)

### 1️⃣ **RTSP Camera Video**

* `camera_id` থাকবে
* `source_type = rtsp`
* Auto-record / real-time inference

### 2️⃣ **Uploaded Video (Testing / Demo)**

* `camera_id = NULL`
* `source_type = upload`
* `uploaded_by` → user
* Manual trigger করে inference

---

## 🔁 Recommended Processing Flow (Very Important for Viva)

### 📌 Upload Video → Check Behaviour

```
User uploads video
        ↓
videos.status = pending
        ↓
Run YOLO + DeepSORT + Action Model
        ↓
events তৈরি হবে (suspicious / normal)
        ↓
videos.status = completed
```

---

## 🧠 Django App-wise Responsibility

### `videos` app

* Video upload API
* File storage
* Status tracking

### `detection` app

* Uploaded video inference
* Frame extraction
* Event creation

---

## ✅ API Endpoints Suggestion

```http
POST   /api/videos/upload/
GET    /api/videos/
POST   /api/videos/{id}/process/
GET    /api/videos/{id}/events/
```

---

## ⚡ Extra (Teacher Impression Boost)

* Upload করা video + **frame snapshot**
* Event timeline view
* Confidence score graph
* Same video multiple model দিয়ে test করা

---

Perfect! চল একেবারে **cameras app** step-by-step বানাই—তুমি পরে check করে migrate/update করতে পারবে।

আমি পুরো **Django app structure + models + serializer + viewset + urls + admin** সব operation দিয়ে দিচ্ছি cameras এর জন্য।

---

## 1️⃣ **cameras/models.py**

```python
from django.db import models

class Camera(models.Model):
    STATUS_CHOICES = (
        ('active', 'Active'),
        ('inactive', 'Inactive'),
    )
    name = models.CharField(max_length=100)
    location = models.CharField(max_length=255)
    rtsp_url = models.TextField(blank=True, null=True)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='active')
    fps = models.IntegerField(default=25)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.name} - {self.location}"
```

---

## 2️⃣ **cameras/serializers.py**

```python
from rest_framework import serializers
from .models import Camera

class CameraSerializer(serializers.ModelSerializer):
    class Meta:
        model = Camera
        fields = '__all__'
```

---

## 3️⃣ **cameras/views.py**

```python
from rest_framework import viewsets, permissions
from .models import Camera
from .serializers import CameraSerializer

class CameraViewSet(viewsets.ModelViewSet):
    queryset = Camera.objects.all().order_by('-created_at')
    serializer_class = CameraSerializer
    permission_classes = [permissions.IsAuthenticated]  # only authenticated users
```

---

## 4️⃣ **cameras/urls.py**

```python
from rest_framework.routers import DefaultRouter
from .views import CameraViewSet

router = DefaultRouter()
router.register(r'cameras', CameraViewSet)

urlpatterns = router.urls
```

---

## 5️⃣ **cameras/admin.py**

```python
from django.contrib import admin
from .models import Camera

@admin.register(Camera)
class CameraAdmin(admin.ModelAdmin):
    list_display = ['id', 'name', 'location', 'status', 'fps', 'created_at']
    list_filter = ['status', 'fps']
    search_fields = ['name', 'location']
```

---

### ✅ Check & Update Steps (Step by Step)

1. Add `'cameras'` in `INSTALLED_APPS`

```python
INSTALLED_APPS = [
    ...
    'cameras',
]
```

2. Run migrations:

```bash
python manage.py makemigrations cameras
python manage.py migrate
```

3. Create superuser:

```bash
python manage.py createsuperuser
```

4. Check **admin panel** → camera CRUD
5. Test API:

```http
GET /api/cameras/          # list all cameras
POST /api/cameras/         # create new camera
PUT /api/cameras/{id}/     # update
DELETE /api/cameras/{id}/  # delete
```

---

💡 **Pro tip:**

* তুমি চাইলে `status` update API + permissions (only admin/operator) আলাদা করে দিতে পারো।
* Postman / Swagger দিয়ে step-by-step test করা easiest way।

---

যদি চাও, আমি পরের ধাপে **Video app** এর জন্য একই **step-by-step CRUD + upload API** বানিয়ে দিতে পারি।

চাও কি আমি সেটা করবো?
