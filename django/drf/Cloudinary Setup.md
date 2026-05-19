
# 🧠 কেন শুধু এটা যথেষ্ট না?

```python
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

👉 এটা শুধু Django-কে বলে:
“file কোথায় save হবে” (Cloudinary)

❗ কিন্তু Django এখনো জানে না:

* কোন Cloudinary account?
* API key কী?
* secret কী?

---

# ✅ Minimum Complete Setup (Must Have)

## 1️⃣ Install

```bash
pip install cloudinary django-cloudinary-storage
```

---

## 2️⃣ Installed Apps

```python
INSTALLED_APPS = [
    'cloudinary',
    'cloudinary_storage',
]
```

---

## 3️⃣ 🔐 Cloudinary Config (VERY IMPORTANT)

```python
import cloudinary

cloudinary.config(
    cloud_name="your_cloud_name",
    api_key="your_api_key",
    api_secret="your_api_secret"
)
```

👉 ❗ এইটা না দিলে upload fail করবে

---

## 4️⃣ Storage সেট করা

```python
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

---

# 🎯 Final Verdict

| Config               | Required? |
| -------------------- | --------- |
| install packages     | ✅         |
| INSTALLED_APPS       | ✅         |
| cloudinary.config    | ✅         |
| DEFAULT_FILE_STORAGE | ✅         |

👉 চারটা ছাড়া system complete না

---

# ⚡ Shortcut (Pro Way)

👉 তুমি চাইলে `.env` use করতে পারো:

```python
CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'xxx',
    'API_KEY': 'xxx',
    'API_SECRET': 'xxx'
}
```

👉 এটা clean + production ready ✅

---




# **Django REST Framework (DRF)** প্রজেক্টে **Cloudinary-তে file upload** (PDF, DOCX, ZIP, etc.) করা **image upload-এর মতোই প্রায় same process** 👍
তবে কিছু **important difference** আছে, যেগুলো জানা দরকার।

---

## 🔥 Core Idea (Short Answer)

👉 Image upload আর file upload দুটোই Cloudinary-তে একইভাবে হয়
👉 শুধু upload type এবং validation একটু আলাদা

---

## 🧠 1. Image vs File Upload (Difference)

| বিষয়             | Image Upload | File Upload           |
| ---------------- | ------------ | --------------------- |
| Resource Type    | `image`      | `raw`                 |
| Preview          | Possible     | Not possible          |
| Format           | JPG, PNG     | PDF, DOCX, ZIP        |
| Cloudinary param | default      | `resource_type="raw"` |

---

## ⚙️ 2. Cloudinary Setup (Same for both)

```bash
pip install cloudinary
```

**settings.py**

```python
CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'your_name',
    'API_KEY': 'your_key',
    'API_SECRET': 'your_secret'
}
```

# Cloudinary Storage add into setting
---
```
pip install django-cloudinary-storage
```

```
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

# media root and media url `thakbe`


## 📦 3. Model (Same Structure)

```python
from cloudinary.models import CloudinaryField

class Document(models.Model):
    title = models.CharField(max_length=100)
    file = CloudinaryField(resource_type="raw")  # 👈 important
```

👉 Image হলে:

```python
image = CloudinaryField('image')
```

👉 File হলে:

```python
file = CloudinaryField(resource_type="raw")
```

---

## 🔗 4. Serializer (Same)

```python
from rest_framework import serializers

class DocumentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Document
        fields = '__all__'
```

---

## 🚀 5. View (Same)

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.parsers import MultiPartParser, FormParser

class UploadDocumentView(APIView):
    parser_classes = (MultiPartParser, FormParser)

    def post(self, request):
        serializer = DocumentSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors)
```

---

## 📤 6. Frontend (Same)

```javascript
const formData = new FormData();
formData.append("title", "My File");
formData.append("file", selectedFile);

fetch("/api/upload/", {
  method: "POST",
  body: formData
});
```

---

## ⚠️ 7. Important Tips (VERY IMPORTANT)

### ✅ File Upload-এর জন্য

```python
CloudinaryField(resource_type="raw")
```

না দিলে upload fail করবে ❌

---

### ✅ Validation (Recommended)

```python
def validate_file(self, value):
    if value.size > 5 * 1024 * 1024:
        raise serializers.ValidationError("File too large")
    return value
```

---

### ✅ Allowed file types

```python
import os

def validate_file(self, value):
    ext = os.path.splitext(value.name)[1]
    if ext not in ['.pdf', '.docx']:
        raise serializers.ValidationError("Unsupported file type")
    return value
```

---

## 🧩 Real-world Example (Use Case)

👉 Scholarship system (তোমার project অনুযায়ী)

* Resume upload (PDF)
* Transcript upload
* Multiple documents upload

```python
class ApplicationDocument(models.Model):
    application = models.ForeignKey(Application, on_delete=models.CASCADE)
    file = CloudinaryField(resource_type="raw")
```

---

## ✅ Final Verdict

👉 **YES — Same process**
👉 শুধু এইটা মনে রাখো:

🔥 Image → default
🔥 File → `resource_type="raw"`

---

## 💡 Pro Tip (Advanced)

👉 Multiple file upload করতে চাইলে:

```python
files = request.FILES.getlist('files')
```

---
# Multiple file upload করতে চাইলে:

ঠিক আছে — আমি তোমাকে **DRF + Cloudinary full production-ready Multiple File Upload System** complete করে দিচ্ছি 🚀
(তোমার scholarship project অনুযায়ী scalable design)

---

# 🧠 🎯 Goal

👉 এক API call-এ multiple files upload
👉 Cloudinary-তে save হবে
👉 validation থাকবে
👉 clean DB design (production-ready)

---

# 🏗️ 1. Model Design (Best Practice)

```python
from django.db import models
from cloudinary.models import CloudinaryField
import uuid

class Application(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    student_name = models.CharField(max_length=100)

class ApplicationDocument(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    application = models.ForeignKey(
        Application,
        on_delete=models.CASCADE,
        related_name="documents"
    )
    file = CloudinaryField(resource_type="raw")  # 👈 must
    uploaded_at = models.DateTimeField(auto_now_add=True)
```

---

# 🔍 2. Serializer (Multiple File Support)

```python
from rest_framework import serializers
import os

class MultiFileUploadSerializer(serializers.Serializer):
    application_id = serializers.UUIDField()
    files = serializers.ListField(
        child=serializers.FileField()
    )

    def validate_files(self, files):
        allowed_ext = ['.pdf', '.docx', '.png', '.jpg']
        max_size = 5 * 1024 * 1024  # 5MB

        for file in files:
            ext = os.path.splitext(file.name)[1].lower()

            if ext not in allowed_ext:
                raise serializers.ValidationError(
                    f"{file.name} unsupported file type"
                )

            if file.size > max_size:
                raise serializers.ValidationError(
                    f"{file.name} too large (max 5MB)"
                )

        return files
```

---

# ⚙️ 3. View (Core Logic)

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.parsers import MultiPartParser, FormParser
from django.shortcuts import get_object_or_404

class MultiFileUploadView(APIView):
    parser_classes = (MultiPartParser, FormParser)

    def post(self, request):
        serializer = MultiFileUploadSerializer(data=request.data)

        if serializer.is_valid():
            application_id = serializer.validated_data['application_id']
            files = serializer.validated_data['files']

            application = get_object_or_404(Application, id=application_id)

            uploaded_files = []

            for file in files:
                doc = ApplicationDocument.objects.create(
                    application=application,
                    file=file
                )
                uploaded_files.append({
                    "id": str(doc.id),
                    "file_url": doc.file.url
                })

            return Response({
                "message": "Files uploaded successfully",
                "files": uploaded_files
            })

        return Response(serializer.errors, status=400)
```

---

# 🔗 4. URL

```python
from django.urls import path
from .views import MultiFileUploadView

urlpatterns = [
    path('upload-multiple/', MultiFileUploadView.as_view()),
]
```

---

# 🌐 5. Frontend (React / JS)

```javascript
const formData = new FormData();

formData.append("application_id", "UUID_HERE");

// multiple files add
for (let i = 0; i < files.length; i++) {
  formData.append("files", files[i]);
}

fetch("/api/upload-multiple/", {
  method: "POST",
  body: formData
});
```

---

# 🧪 6. Postman Test

👉 Body → form-data

| Key            | Type                   |
| -------------- | ---------------------- |
| application_id | text                   |
| files          | file (multiple select) |

---

# 🔥 7. Response Example

```json
{
  "message": "Files uploaded successfully",
  "files": [
    {
      "id": "uuid-1",
      "file_url": "https://res.cloudinary.com/..."
    },
    {
      "id": "uuid-2",
      "file_url": "https://res.cloudinary.com/..."
    }
  ]
}
```

---

# 🚀 8. Advanced Upgrade (Production Tips)

### ✅ Bulk insert optimization

```python
ApplicationDocument.objects.bulk_create([...])
```

---

### ✅ File type field add করো

```python
file_type = models.CharField(max_length=20)
```

---

### ✅ Soft delete support

```python
is_deleted = models.BooleanField(default=False)
```

---

### ✅ Limit number of files

```python
if len(files) > 5:
    raise serializers.ValidationError("Max 5 files allowed")
```

---

# 🧠 Final Architecture (Clean)

👉 **Application (1) → (N) Documents**

```
Application
   └── ApplicationDocument (multiple files)
```

---

# 💥 Summary

✔ Same as single upload
✔ Loop দিয়ে multiple create
✔ `request.FILES.getlist()` internally handled
✔ Cloudinary → `resource_type="raw"` must

---

চলো এখন পুরোটা **production-level clean architecture** দিয়ে করি 🚀
তুমি যেগুলো চেয়েছো — সব একসাথে organizedভাবে দিচ্ছি:

---

# 🧠 🔥 Final System Overview

👉 Scholarship system structure:

```
Application
   ├── Resume (single file)
   └── Documents (multiple files)
```

---

# 🏗️ 1. Updated Models (Best Practice)

```python
from django.db import models
from cloudinary.models import CloudinaryField
import uuid

class Application(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    student_name = models.CharField(max_length=100)

    # ✅ Resume (single file)
    resume = CloudinaryField(resource_type="raw", null=True, blank=True)


class ApplicationDocument(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    application = models.ForeignKey(
        Application,
        on_delete=models.CASCADE,
        related_name="documents"
    )
    file = CloudinaryField(resource_type="raw")
    uploaded_at = models.DateTimeField(auto_now_add=True)
```

---

# 🔐 2. Serializers

```python
from rest_framework import serializers
import os

class DocumentSerializer(serializers.ModelSerializer):
    class Meta:
        model = ApplicationDocument
        fields = ['id', 'file']


class ResumeSerializer(serializers.ModelSerializer):
    class Meta:
        model = Application
        fields = ['resume']


class MultiFileUploadSerializer(serializers.Serializer):
    files = serializers.ListField(child=serializers.FileField())

    def validate_files(self, files):
        allowed_ext = ['.pdf', '.docx']
        for file in files:
            ext = os.path.splitext(file.name)[1].lower()
            if ext not in allowed_ext:
                raise serializers.ValidationError(f"{file.name} not allowed")
        return files
```

---

# 🚀 3. DRF ViewSet (Clean Architecture)

```python
from rest_framework.viewsets import ModelViewSet
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.parsers import MultiPartParser, FormParser
from django.shortcuts import get_object_or_404

class ApplicationViewSet(ModelViewSet):
    queryset = Application.objects.all()
    serializer_class = ResumeSerializer
    parser_classes = (MultiPartParser, FormParser)

    # 🔥 1. Upload Multiple Documents
    @action(detail=True, methods=['post'])
    def upload_documents(self, request, pk=None):
        application = self.get_object()
        files = request.FILES.getlist('files')

        uploaded = []

        for file in files:
            doc = ApplicationDocument.objects.create(
                application=application,
                file=file
            )
            uploaded.append({
                "id": doc.id,
                "url": doc.file.url
            })

        return Response({"files": uploaded})

    # 🔥 2. Delete Multiple Documents
    @action(detail=True, methods=['delete'])
    def delete_documents(self, request, pk=None):
        application = self.get_object()
        ids = request.data.get('ids', [])

        docs = ApplicationDocument.objects.filter(
            id__in=ids,
            application=application
        )

        deleted_count = docs.count()
        docs.delete()

        return Response({
            "message": f"{deleted_count} files deleted"
        })

    # 🔥 3. Update / Replace Documents
    @action(detail=True, methods=['put'])
    def replace_documents(self, request, pk=None):
        application = self.get_object()

        # delete old
        application.documents.all().delete()

        # upload new
        files = request.FILES.getlist('files')

        new_docs = []
        for file in files:
            doc = ApplicationDocument.objects.create(
                application=application,
                file=file
            )
            new_docs.append({
                "id": doc.id,
                "url": doc.file.url
            })

        return Response({
            "message": "Documents replaced",
            "files": new_docs
        })

    # 🔥 4. Upload / Replace Resume
    @action(detail=True, methods=['put'])
    def upload_resume(self, request, pk=None):
        application = self.get_object()

        file = request.FILES.get('resume')

        if not file:
            return Response({"error": "No file provided"}, status=400)

        application.resume = file
        application.save()

        return Response({
            "message": "Resume uploaded",
            "resume_url": application.resume.url
        })
```

---

# 🔗 4. Router Setup

```python
from rest_framework.routers import DefaultRouter
from .views import ApplicationViewSet

router = DefaultRouter()
router.register('applications', ApplicationViewSet)

urlpatterns = router.urls
```

---

# 📡 5. API Endpoints

## 📤 Upload Multiple Files

```
POST /applications/{id}/upload_documents/
```

## ❌ Delete Multiple Files

```
DELETE /applications/{id}/delete_documents/
```

```json
{
  "ids": ["uuid1", "uuid2"]
}
```

---

## 🔁 Replace Documents

```
PUT /applications/{id}/replace_documents/
```

---

## 📄 Resume Upload

```
PUT /applications/{id}/upload_resume/
```

---

# 🌐 6. Frontend Example

```javascript
const formData = new FormData();

files.forEach(file => {
  formData.append("files", file);
});

fetch(`/applications/${id}/upload_documents/`, {
  method: "POST",
  body: formData
});
```

---

# ⚡ 7. Pro-Level Improvements

### ✅ Soft Delete (recommended)

```python
is_deleted = models.BooleanField(default=False)
```

---

### ✅ File Type Tracking

```python
file_type = models.CharField(max_length=20)
```

---

### ✅ Limit files

```python
if len(files) > 5:
    return Response({"error": "Max 5 files"})
```

---

# 🧠 Final Takeaway

✔ Resume → single file (Application table)
✔ Documents → multiple (separate table)
✔ Upload / Delete / Replace → clean API actions
✔ ViewSet → scalable + interview-ready

---

# React Compoment how  use

চলো এখন তোমাকে একটা **full React component (production-style)** দেখাই — যেখানে থাকবে:

✅ Resume upload (single file)
✅ Multiple documents upload
✅ Delete documents
✅ Replace documents
✅ Clean UI + state handling

---

# ⚛️ 🔥 Full React Component (Upload System)

```javascript
import React, { useState } from "react";

const ApplicationUpload = ({ applicationId }) => {
  const [resume, setResume] = useState(null);
  const [documents, setDocuments] = useState([]);
  const [uploadedDocs, setUploadedDocs] = useState([]);

  // ✅ Resume Upload
  const handleResumeUpload = async () => {
    if (!resume) return alert("Select resume");

    const formData = new FormData();
    formData.append("resume", resume);

    const res = await fetch(
      `/applications/${applicationId}/upload_resume/`,
      {
        method: "PUT",
        body: formData,
      }
    );

    const data = await res.json();
    alert("Resume uploaded!");
    console.log(data);
  };

  // ✅ Multiple Documents Upload
  const handleDocumentsUpload = async () => {
    if (documents.length === 0) return alert("Select files");

    const formData = new FormData();

    documents.forEach((file) => {
      formData.append("files", file);
    });

    const res = await fetch(
      `/applications/${applicationId}/upload_documents/`,
      {
        method: "POST",
        body: formData,
      }
    );

    const data = await res.json();
    setUploadedDocs([...uploadedDocs, ...data.files]);
  };

  // ✅ Delete Documents
  const handleDelete = async (id) => {
    const res = await fetch(
      `/applications/${applicationId}/delete_documents/`,
      {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          ids: [id],
        }),
      }
    );

    await res.json();

    setUploadedDocs(uploadedDocs.filter((doc) => doc.id !== id));
  };

  // ✅ Replace Documents
  const handleReplace = async () => {
    if (documents.length === 0) return alert("Select files");

    const formData = new FormData();

    documents.forEach((file) => {
      formData.append("files", file);
    });

    const res = await fetch(
      `/applications/${applicationId}/replace_documents/`,
      {
        method: "PUT",
        body: formData,
      }
    );

    const data = await res.json();
    setUploadedDocs(data.files);
  };

  return (
    <div style={{ padding: "20px", maxWidth: "600px" }}>
      <h2>📄 Application File Upload</h2>

      {/* 🔥 Resume Upload */}
      <div>
        <h3>Upload Resume</h3>
        <input
          type="file"
          onChange={(e) => setResume(e.target.files[0])}
        />
        <button onClick={handleResumeUpload}>Upload Resume</button>
      </div>

      <hr />

      {/* 🔥 Documents Upload */}
      <div>
        <h3>Upload Documents</h3>
        <input
          type="file"
          multiple
          onChange={(e) => setDocuments([...e.target.files])}
        />

        <div style={{ marginTop: "10px" }}>
          <button onClick={handleDocumentsUpload}>
            Upload Documents
          </button>

          <button onClick={handleReplace} style={{ marginLeft: "10px" }}>
            Replace All
          </button>
        </div>
      </div>

      <hr />

      {/* 🔥 Uploaded Documents List */}
      <div>
        <h3>Uploaded Documents</h3>

        {uploadedDocs.length === 0 && <p>No files uploaded</p>}

        {uploadedDocs.map((doc) => (
          <div
            key={doc.id}
            style={{
              display: "flex",
              justifyContent: "space-between",
              marginBottom: "10px",
              border: "1px solid #ddd",
              padding: "8px",
            }}
          >
            <a href={doc.url} target="_blank" rel="noreferrer">
              View File
            </a>

            <button onClick={() => handleDelete(doc.id)}>
              Delete
            </button>
          </div>
        ))}
      </div>
    </div>
  );
};

export default ApplicationUpload;
```

---

# 🎯 কী কী শিখলে এখানে

## ✅ Resume Upload

👉 Single file → `PUT /upload_resume/`

## ✅ Multiple Upload

👉 `FormData.append("files", file)` multiple times

## ✅ Delete API

👉 JSON body দিয়ে ids পাঠানো

## ✅ Replace API

👉 পুরানো delete + নতুন upload

---

# 🧠 Pro UI Upgrade Ideas

👉 চাইলে এগুলো add করতে পারো:

### 🔥 Drag & Drop (pro UX)

* `react-dropzone`

### 🔥 Progress bar

* upload progress track

### 🔥 File preview

* PDF icon / image preview

### 🔥 Toast notification

* success / error

---

# 🚀 Next Level (Highly Recommended)

👉 তুমি যদি production SaaS বানাও:

* use Axios (better than fetch)
* add auth token (JWT)
* error handling middleware
* loading spinner

---

# 💥 Final কথা

এই component দিয়ে তুমি:

✅ Full file system build করতে পারবে
✅ Resume + Documents clean separation
✅ Interview-ready code
✅ Real SaaS level feature

---

ঠিক বলেছো — এগুলো ছাড়া production SaaS complete না ❌
চলো আমি তোমাকে **Axios + JWT + Error Handling + Loading Spinner** দিয়ে full upgrade version দেখাই 🚀

---

# ⚛️ 🔥 1. Axios Setup (with JWT)

👉 প্রথমে install করো:

```bash
npm install axios
```

---

## 📦 axios instance (best practice)

```javascript
// src/api/axios.js

import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:8000",
});

// 🔐 JWT token attach
api.interceptors.request.use((config) => {
  const token = localStorage.getItem("access_token");

  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }

  return config;
});

// ❌ Global error handling
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      alert("Session expired. Please login again.");
    }

    return Promise.reject(error);
  }
);

export default api;
```

---

# 🔄 2. Updated React Component (Production Ready)

```javascript
import React, { useState } from "react";
import api from "./api/axios";

const ApplicationUpload = ({ applicationId }) => {
  const [resume, setResume] = useState(null);
  const [documents, setDocuments] = useState([]);
  const [uploadedDocs, setUploadedDocs] = useState([]);
  const [loading, setLoading] = useState(false);

  // 🔄 Resume Upload
  const handleResumeUpload = async () => {
    if (!resume) return alert("Select resume");

    const formData = new FormData();
    formData.append("resume", resume);

    try {
      setLoading(true);

      const res = await api.put(
        `/applications/${applicationId}/upload_resume/`,
        formData
      );

      alert("Resume uploaded!");
      console.log(res.data);
    } catch (err) {
      alert(err.response?.data?.error || "Upload failed");
    } finally {
      setLoading(false);
    }
  };

  // 📤 Upload Documents
  const handleDocumentsUpload = async () => {
    if (documents.length === 0) return alert("Select files");

    const formData = new FormData();
    documents.forEach((file) => formData.append("files", file));

    try {
      setLoading(true);

      const res = await api.post(
        `/applications/${applicationId}/upload_documents/`,
        formData
      );

      setUploadedDocs([...uploadedDocs, ...res.data.files]);
    } catch (err) {
      alert("Upload failed");
    } finally {
      setLoading(false);
    }
  };

  // ❌ Delete Document
  const handleDelete = async (id) => {
    try {
      setLoading(true);

      await api.delete(
        `/applications/${applicationId}/delete_documents/`,
        {
          data: { ids: [id] },
        }
      );

      setUploadedDocs(uploadedDocs.filter((doc) => doc.id !== id));
    } catch (err) {
      alert("Delete failed");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div style={{ padding: "20px" }}>
      <h2>🚀 SaaS File Upload</h2>

      {/* 🔥 Loading Spinner */}
      {loading && <p>⏳ Processing...</p>}

      {/* Resume */}
      <div>
        <h3>Resume</h3>
        <input type="file" onChange={(e) => setResume(e.target.files[0])} />
        <button onClick={handleResumeUpload}>Upload Resume</button>
      </div>

      <hr />

      {/* Documents */}
      <div>
        <h3>Documents</h3>
        <input
          type="file"
          multiple
          onChange={(e) => setDocuments([...e.target.files])}
        />
        <button onClick={handleDocumentsUpload}>Upload Docs</button>
      </div>

      <hr />

      {/* List */}
      <div>
        <h3>Files</h3>
        {uploadedDocs.map((doc) => (
          <div key={doc.id}>
            <a href={doc.url} target="_blank" rel="noreferrer">
              View
            </a>
            <button onClick={() => handleDelete(doc.id)}>Delete</button>
          </div>
        ))}
      </div>
    </div>
  );
};

export default ApplicationUpload;
```

---

# 🧠 3. What You Achieved (Production Level)

## 🔐 JWT Auth

👉 সব request-এ auto token attach

---

## ⚠️ Global Error Handling

👉 401 হলে auto logout alert

---

## 🔄 Loading State

👉 user বুঝতে পারে system কাজ করছে

---

## 💡 Clean Code

👉 reusable axios instance
👉 try/catch + finally

---

# 🚀 4. Next-Level Upgrades (Real SaaS)

👉 এখন এগুলো করলে তুমি 🔥 senior level হয়ে যাবে:

---

### 🎯 Progress Bar (VERY IMPORTANT)

```javascript
onUploadProgress: (progressEvent) => {
  const percent = Math.round(
    (progressEvent.loaded * 100) / progressEvent.total
  );
  console.log(percent);
}
```

---

### 🎯 Toast UI (no alert)

👉 use:

* React Toastify

---

### 🎯 Global State

👉 use:

* Redux Toolkit
* অথবা Zustand (lightweight)

---

### 🎯 Secure Token Storage

❌ localStorage (risk)
✅ httpOnly cookie (best)

---

# 💥 Final কথা

এই setup দিয়ে তুমি:

✅ Real SaaS-level frontend
✅ DRF API perfectly integrated
✅ Scalable architecture
✅ Interview-ready system

---

👉 চাইলে next step:

🔥 Full Auth System (Login/Register + JWT Refresh)
🔥 Role-based access (Admin/Student)
🔥 File preview UI (Google Drive style)
🔥 Drag & Drop uploader (pro level)

Just bolo — next level build করি 🚀
চলো এখন তোমাকে একদম **SaaS-level complete roadmap + working structure** দিই 🚀
(তুমি চাইলে এটাকেই full project বানাতে পারবে)

---

# 🧠 🔥 What We Will Build

👉 Full system:

* 🔐 Auth (JWT + Refresh)
* 👥 Role-based access (Admin / Student)
* 📁 File preview (Google Drive style)
* 🖱️ Drag & Drop uploader

---

# 🔐 1. Full Auth System (DRF + JWT)

👉 আমরা use করবো:

* Djoser
* Simple JWT

---

## ⚙️ Backend Setup

```bash
pip install djoser djangorestframework-simplejwt
```

---

## 🔧 settings.py

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}

from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=60),
    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),
}
```

---

## 🔗 URLs

```python
urlpatterns = [
    path('auth/', include('djoser.urls')),
    path('auth/', include('djoser.urls.jwt')),
]
```

---

## 📡 API Endpoints

| কাজ      | API                  |
| -------- | -------------------- |
| Register | `/auth/users/`       |
| Login    | `/auth/jwt/create/`  |
| Refresh  | `/auth/jwt/refresh/` |

---

# 👥 2. Role-Based Access (Admin / Student)

## 🏗️ Custom User Model

```python
class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('student', 'Student'),
    )
    role = models.CharField(max_length=10, choices=ROLE_CHOICES)
```

---

## 🔐 Permission Class

```python
from rest_framework.permissions import BasePermission

class IsAdmin(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == "admin"


class IsStudent(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == "student"
```

---

## 🎯 Usage

```python
permission_classes = [IsAdmin]
```

---

# 📁 3. File Preview UI (Google Drive Style)

## 🎯 Idea

👉 File type detect করে preview দেখানো

---

## ⚛️ React Component

```javascript
const FilePreview = ({ file }) => {
  const url = file.url;

  if (url.endsWith(".pdf")) {
    return <iframe src={url} width="100%" height="400px" />;
  }

  if (url.match(/\.(jpg|png|jpeg)$/)) {
    return <img src={url} alt="preview" width="200" />;
  }

  return <a href={url}>Download File</a>;
};
```

---

# 🖱️ 4. Drag & Drop Upload (Pro Level)

👉 আমরা use করবো:

* react-dropzone

---

## 📦 Install

```bash
npm install react-dropzone
```

---

## ⚛️ Component

```javascript
import { useDropzone } from "react-dropzone";
import api from "./api/axios";

const DragDropUpload = ({ applicationId }) => {
  const onDrop = async (acceptedFiles) => {
    const formData = new FormData();

    acceptedFiles.forEach((file) => {
      formData.append("files", file);
    });

    await api.post(
      `/applications/${applicationId}/upload_documents/`,
      formData
    );

    alert("Uploaded!");
  };

  const { getRootProps, getInputProps } = useDropzone({ onDrop });

  return (
    <div
      {...getRootProps()}
      style={{
        border: "2px dashed #aaa",
        padding: "40px",
        textAlign: "center",
      }}
    >
      <input {...getInputProps()} />
      <p>Drag & drop files here</p>
    </div>
  );
};
```

---

# 🎯 5. Google Drive Style UI (Simple Layout)

```javascript
<div style={{ display: "grid", gridTemplateColumns: "repeat(3, 1fr)" }}>
  {files.map(file => (
    <div key={file.id} style={{ border: "1px solid #ddd", padding: "10px" }}>
      <FilePreview file={file} />
    </div>
  ))}
</div>
```

---

# ⚡ 6. Pro Architecture (Frontend)

```
src/
 ├── api/
 │    └── axios.js
 ├── components/
 │    ├── Upload/
 │    ├── Preview/
 │    └── DragDrop/
 ├── pages/
 │    ├── Dashboard.jsx
 │    ├── Login.jsx
 │    └── Register.jsx
```

---

# 🚀 7. Next-Level (Real SaaS Features)

👉 এগুলো করলে তুমি 🔥 industry ready:

---

### 🔥 Token Auto Refresh

👉 Axios interceptor দিয়ে refresh token call

---

### 🔥 Protected Routes

```javascript
if (!token) return <Navigate to="/login" />;
```

---

### 🔥 File Security

👉 Signed URL (Cloudinary)

---

### 🔥 Role ভিত্তিক UI

```javascript
if (user.role === "admin") {
  // admin dashboard
}
```

---

# 💥 Final Takeaway

তুমি এখন build করতে পারো:

✅ Full Authentication System
✅ Role-based SaaS app
✅ Advanced file upload system
✅ Google Drive style UI

---

👉 চাইলে আমি next step এ বানিয়ে দিতে পারি:

🔥 Full Django + React project (folder structure সহ)
🔥 ER Diagram + API documentation
🔥 Deployment (Vercel + Render / AWS)

Just bolo — full SaaS বানাই 🚀
ঠিক আছে — তুমি frontend বুঝতে পারোনি, এটা একদম normal 👍
আমি এখন **একদম basic থেকে step-by-step সহজভাবে বুঝাই** (zero confusion) 🚀

---

# 🧠 🎯 Frontend এ কী হচ্ছে (Simple Idea)

👉 React frontend এর কাজ:

1. File select করা
2. Backend API তে পাঠানো
3. Response নিয়ে UI update করা

---

# 🧱 Step 1: Simple File Upload (1 file)

## 📦 Basic Code

```javascript
import React, { useState } from "react";

function SimpleUpload() {
  const [file, setFile] = useState(null);

  const handleUpload = async () => {
    const formData = new FormData();
    formData.append("file", file);

    await fetch("http://localhost:8000/upload/", {
      method: "POST",
      body: formData,
    });

    alert("Uploaded!");
  };

  return (
    <div>
      <input type="file" onChange={(e) => setFile(e.target.files[0])} />
      <button onClick={handleUpload}>Upload</button>
    </div>
  );
}

export default SimpleUpload;
```

---

## 🔍 এখানে কী হচ্ছে?

👉 `useState` → file store করে
👉 `input type="file"` → file select
👉 `FormData()` → file backend এ পাঠানোর format
👉 `fetch()` → API call

---

# 📁 Step 2: Multiple File Upload

```javascript
const [files, setFiles] = useState([]);

<input
  type="file"
  multiple
  onChange={(e) => setFiles([...e.target.files])}
/>
```

---

## 📤 Upload Logic

```javascript
const handleUpload = async () => {
  const formData = new FormData();

  files.forEach((file) => {
    formData.append("files", file);
  });

  await fetch("/upload-multiple/", {
    method: "POST",
    body: formData,
  });
};
```

---

# 🔐 Step 3: Axios + Token (Simple Explanation)

👉 `fetch` → basic
👉 Axios → advanced

---

## 📦 Axios Example

```javascript
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:8000",
});

api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");

  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }

  return config;
});
```

👉 এর মানে:
**সব request এ auto token attach হবে**

---

# 🔄 Step 4: Loading State (Important)

```javascript
const [loading, setLoading] = useState(false);
```

---

## ব্যবহার

```javascript
setLoading(true);

// API call

setLoading(false);
```

---

## UI তে দেখানো

```javascript
{loading && <p>Loading...</p>}
```

---

# 🧩 Step 5: File List Show করা

```javascript
{files.map((file, index) => (
  <p key={index}>{file.name}</p>
))}
```

---

# 🧠 Full Simple Version (Easy Final Code)

```javascript
import React, { useState } from "react";

function UploadApp() {
  const [files, setFiles] = useState([]);
  const [loading, setLoading] = useState(false);

  const handleUpload = async () => {
    const formData = new FormData();

    files.forEach((file) => {
      formData.append("files", file);
    });

    setLoading(true);

    await fetch("http://localhost:8000/upload/", {
      method: "POST",
      body: formData,
    });

    setLoading(false);
    alert("Uploaded!");
  };

  return (
    <div>
      <h2>File Upload</h2>

      <input
        type="file"
        multiple
        onChange={(e) => setFiles([...e.target.files])}
      />

      <button onClick={handleUpload}>Upload</button>

      {loading && <p>Uploading...</p>}

      <h3>Selected Files:</h3>
      {files.map((file, i) => (
        <p key={i}>{file.name}</p>
      ))}
    </div>
  );
}

export default UploadApp;
```

---

# 💥 Simple Language Summary

👉 React frontend এ ৩টা main জিনিস:

1. **State** → file store করে
2. **FormData** → backend এ পাঠায়
3. **API call** → upload করে

---

# 🚀 Next Step (আমি তোমাকে guide করতে পারি)

👉 তুমি যদি এখন বলো:

* “drag drop bujhte chai”
* “axios fully bujhte chai”
* “auth + login frontend”

👉 আমি একদম beginner → pro step-by-step বানিয়ে দিবো 👍
ঠিক আছে — এবার তোমাকে **Axios একদম A→Z (Beginner → Pro)** বুঝাই 🚀
(React + DRF context এ, real example সহ)

---

# 🧠 🔥 Axios কী?

👉 Axios হলো একটা **HTTP client**
👉 Backend API call করার জন্য use হয়

👉 সহজভাবে:
**Frontend ↔ Backend communication tool**

---

# ⚡ Axios vs fetch (Why Axios?)

| Feature         | fetch | Axios |
| --------------- | ----- | ----- |
| JSON auto parse | ❌     | ✅     |
| Error handling  | Hard  | Easy  |
| Interceptor     | ❌     | ✅     |
| Cleaner code    | ❌     | ✅     |

---

# 🧱 1. Basic Setup

```bash
npm install axios
```

---

## 📦 Basic GET Request

```javascript
import axios from "axios";

axios.get("http://localhost:8000/api/todos/")
  .then(res => console.log(res.data))
  .catch(err => console.log(err));
```

---

## 🔍 What happens?

👉 GET → data fetch
👉 `.then()` → success
👉 `.catch()` → error

---

# 📤 2. POST Request (Create Data)

```javascript
axios.post("http://localhost:8000/api/todos/", {
  title: "Learn Axios"
})
.then(res => console.log(res.data));
```

---

# 🔄 3. PUT / PATCH (Update)

```javascript
// PUT → full update
axios.put("/api/todos/1/", {
  title: "Updated"
});

// PATCH → partial update
axios.patch("/api/todos/1/", {
  title: "Partial Update"
});
```

---

# ❌ 4. DELETE

```javascript
axios.delete("/api/todos/1/")
  .then(() => console.log("Deleted"));
```

---

# 📁 5. File Upload (VERY IMPORTANT)

```javascript
const formData = new FormData();
formData.append("file", file);

axios.post("/upload/", formData, {
  headers: {
    "Content-Type": "multipart/form-data"
  }
});
```

---

# 🔐 6. JWT Token Add করা

## ❌ Normal way (not scalable)

```javascript
axios.get("/api/", {
  headers: {
    Authorization: "Bearer YOUR_TOKEN"
  }
});
```

---

## ✅ Best Practice (Axios Instance)

```javascript
const api = axios.create({
  baseURL: "http://localhost:8000"
});

api.interceptors.request.use(config => {
  const token = localStorage.getItem("access_token");

  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }

  return config;
});
```

👉 এখন সব request এ token auto যাবে 🔥

---

# 🔁 7. Response Handle করা

```javascript
try {
  const res = await axios.get("/api/");
  console.log(res.data);
} catch (err) {
  console.log(err.response.data);
}
```

---

# ⚠️ 8. Global Error Handling (PRO)

```javascript
api.interceptors.response.use(
  res => res,
  err => {
    if (err.response?.status === 401) {
      alert("Login again!");
    }
    return Promise.reject(err);
  }
);
```

---

# 🔄 9. Loading State (React)

```javascript
const [loading, setLoading] = useState(false);

const fetchData = async () => {
  try {
    setLoading(true);

    const res = await axios.get("/api/data");

    console.log(res.data);
  } finally {
    setLoading(false);
  }
};
```

---

# 📊 10. Multiple API Call

```javascript
const [users, todos] = await Promise.all([
  axios.get("/users"),
  axios.get("/todos")
]);
```

---

# 🚀 11. Upload Progress (Pro Feature)

```javascript
axios.post("/upload/", formData, {
  onUploadProgress: (progressEvent) => {
    const percent = Math.round(
      (progressEvent.loaded * 100) / progressEvent.total
    );
    console.log(percent + "%");
  }
});
```

---

# 🧩 12. Full Production Example (Clean)

```javascript
// api.js
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:8000",
});

api.interceptors.request.use(config => {
  const token = localStorage.getItem("token");
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

export default api;
```

---

## 🔥 Use in Component

```javascript
import api from "./api";

const fetchTodos = async () => {
  try {
    const res = await api.get("/api/todos/");
    console.log(res.data);
  } catch (err) {
    console.log("Error");
  }
};
```

---

# 🧠 Final Summary (Golden Rules)

👉 Axios use করলে:

✅ GET → data fetch
✅ POST → create
✅ PUT/PATCH → update
✅ DELETE → delete
✅ FormData → file upload
✅ Interceptor → token + error handle

---

# 💥 Real SaaS Mindset

👉 তুমি যদি serious developer হও:

* Always use axios instance
* Never repeat headers
* Use interceptors
* Handle errors globally

---

# 🚀 Next Step (Highly Recommended)

👉 এখন এগুলো করলে তুমি 🔥 pro হয়ে যাবে:

* “Axios + JWT Refresh Token system”
* “React Query (no manual fetch anymore)”
* “Central API service layer”

---

👉 বলো — next কোনটা শিখতে চাও:
🔥 JWT refresh auto system
🔥 React Query full guide
🔥 Full frontend architecture
