তুমি যেহেতু Django-তে `MultiPartParser` ব্যবহার করছো, তাই React থেকে **file upload করতে হলে `FormData` ব্যবহার করতে হবে** — JSON না ❌

আমি তোমাকে full production-ready flow দেখাচ্ছি 👇

---

# 🔥 1. React থেকে File Send (Correct Way)

```javascript
import axios from "axios";

const uploadTodo = async (data) => {
  const formData = new FormData();

  formData.append("title", data.title);
  formData.append("description", data.description);
  formData.append("file", data.file); // 👈 file field name must match serializer

  try {
    const res = await axios.post(
      "http://127.0.0.1:8000/api/todos/upload/",
      formData,
      {
        headers: {
          "Content-Type": "multipart/form-data",
          Authorization: `Bearer ${localStorage.getItem("access")}`, // JWT থাকলে
        },
      }
    );

    console.log(res.data);
  } catch (err) {
    console.error(err.response?.data);
  }
};
```

---

# 🧠 2. Form Example (React)

```javascript
import { useState } from "react";

export default function TodoForm() {
  const [form, setForm] = useState({
    title: "",
    description: "",
    file: null,
  });

  const handleChange = (e) => {
    if (e.target.name === "file") {
      setForm({ ...form, file: e.target.files[0] });
    } else {
      setForm({ ...form, [e.target.name]: e.target.value });
    }
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    uploadTodo(form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="title" onChange={handleChange} placeholder="Title" />
      <input name="description" onChange={handleChange} placeholder="Description" />

      <input type="file" name="file" onChange={handleChange} />

      <button type="submit">Upload</button>
    </form>
  );
}
```

---

# ⚠️ 3. Django Side Check (VERY IMPORTANT)

### ✅ Model

```python
class Todo(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    title = models.CharField(max_length=255)
    description = models.TextField()
    file = models.FileField(upload_to="todos/", null=True, blank=True)
```

---

### ✅ Serializer

```python
class TodoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Todo
        fields = "__all__"
```

---

# 🚨 Common Mistakes (95% dev এখানে ভুল করে)

❌ JSON দিয়ে file পাঠানো  
❌ `Content-Type: application/json` দেওয়া  
❌ `file` field name mismatch  
❌ `request.FILES` ignore করা  
❌ axios এ headers ভুল দেওয়া

---

# ⚡ Debug Tips

```python
def post(self, request):
    print(request.data)
    print(request.FILES)  # 👈 MUST check

    ...
```

---

# 🔥 Pro Tips (Production Level)

- multiple file upload চাইলে:
    

```javascript
formData.append("files", file1);
formData.append("files", file2);
```

- progress bar:
    

```javascript
onUploadProgress: (progressEvent) => {
  const percent = Math.round((progressEvent.loaded * 100) / progressEvent.total);
  console.log(percent);
}
```

---

# ✅ Summary

👉 React → `FormData`  
👉 Django → `MultiPartParser`  
👉 field name must match  
👉 Auth header লাগবে (IsAuthenticated)

---

চাও হলে আমি তোমার জন্য 👇 বানিয়ে দিতে পারি:

- 🔥 Drag & Drop file upload UI
    
- 📊 Upload progress bar (like Google Drive)
    
- 📁 Multiple file upload system (production ready)
    
- 🧠 Resume / document system (তোমার scholarship project এর জন্য)
    

বললেই next level version দেখাব 🚀