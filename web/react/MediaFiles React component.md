
``` js
import React, { useState } from "react";
import "./MediaUploadForm.css"; // we'll create this CSS

function MediaUploadForm() {
    const [mediaFiles, setMediaFiles] = useState([]);

    const handleFileChange = (e) => {
        const files = Array.from(e.target.files);
        setMediaFiles(files);
    };

    const handleSubmit = (e) => {
        e.preventDefault();
        if (!mediaFiles.length) return alert("Please select files");

        const formData = new FormData();
        mediaFiles.forEach((file) => formData.append("media", file));

        // Replace this with your API call
        fetch("/api/upload", {
            method: "POST",
            body: formData,
        })
            .then((res) => res.json())
            .then((data) => {
                console.log(data)
                alert("Files uploaded successfully!");
                setMediaFiles([]);
            })
        .catch((err) => {
            console.log(err)
            alert("Upload failed!")
        });
    };

    return (
        <div className="upload-container">
            <h2>Upload Images & Videos</h2>
            <form onSubmit={handleSubmit} className="upload-form">
                <label className="file-input-label">
                    Choose Files
                    <input
                        type="file"
                        accept="image/*,video/*"
                        multiple
                        onChange={handleFileChange}
                    />
                </label>

                <div className="preview-grid">
                    {mediaFiles.map((file, idx) => {
                        const url = URL.createObjectURL(file);
                        return (
                            <div className="media-card" key={idx}>
                                {file.type.startsWith("image/") ? (
                                    <img src={url} alt={file.name} />
                                ) : (
                                    <video src={url} controls />
                                )}
                                <p className="media-name">{file.name}</p>
                            </div>
                        );
                    })}
                </div>

                <button type="submit" className="upload-btn">
                    Upload
                </button>
            </form>
        </div>
    );
}

export default MediaUploadForm;

```



Okay, let’s break it down simply. 😄

---

### **What is FormData?**

**`FormData`** is a special JavaScript object that lets you **store key-value pairs**, just like a form in HTML, but it can also handle **files (images, videos, documents)**.

* Think of it as a **container** where you put your form data before sending it to a server.
* It is mainly used for **uploading files** via **`fetch` or `XMLHttpRequest`**.

---

### **Why not just send JSON?**

* JSON is **text-only**. You **cannot send raw files like images or videos** directly in JSON easily.
* FormData handles **binary files** automatically.

---

### **Example: Using FormData**

```javascript
// Suppose user selected some files
const files = [file1, file2]; // could be from input type="file"

// Create a FormData object
const formData = new FormData();

// Add files to it
files.forEach((file) => {
  formData.append("media", file); // "media" is the key your backend expects
});

// Add other form fields
formData.append("title", "My Cool Video");

// Send to server
fetch("/api/upload", {
  method: "POST",
  body: formData,
})
  .then((res) => res.json())
  .then((data) => console.log("Success:", data))
  .catch((err) => console.error("Error:", err));
```

---

### **How backend sees it:**

In **Django**:

```python
def upload_view(request):
    if request.method == "POST":
        files = request.FILES.getlist("media")  # matches the FormData key
        title = request.POST.get("title")
        # save files or process them
```

✅ Key points:

1. Use **`append(key, value)`** to add data.
2. Can store **files + normal text** together.
3. Sends data as **`multipart/form-data`**, which is what servers expect for file uploads.

---

If you want, I can draw a **simple diagram showing FormData → React → Server flow** so it’s super easy to visualize.

Do you want me to do that?
