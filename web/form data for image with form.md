If you're using **React Hook Form (RHF)** and need to submit **text fields + one image** to a Django REST Framework backend, the correct approach is to use **`FormData`**.

---

# 1. Install React Hook Form

```bash
npm install react-hook-form
```

---

# 2. React Form

```jsx
import { useForm } from "react-hook-form";
import axios from "axios";

export default function ProductForm() {
  const {
    register,
    handleSubmit,
    reset,
    formState: { errors },
  } = useForm();

  const onSubmit = async (data) => {
    try {
      const formData = new FormData();

      formData.append("title", data.title);
      formData.append("price", data.price);
      formData.append("description", data.description);

      // image
      formData.append("image", data.image[0]);

      const res = await axios.post(
        "http://127.0.0.1:8000/api/products/",
        formData,
        {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        }
      );

      console.log(res.data);
      reset();
    } catch (err) {
      console.log(err.response?.data);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>

      <input
        type="text"
        placeholder="Title"
        {...register("title", {
          required: "Title is required",
        })}
      />
      <p>{errors.title?.message}</p>

      <input
        type="number"
        placeholder="Price"
        {...register("price", {
          required: "Price is required",
        })}
      />
      <p>{errors.price?.message}</p>

      <textarea
        placeholder="Description"
        {...register("description")}
      />

      <input
        type="file"
        accept="image/*"
        {...register("image", {
          required: "Image is required",
        })}
      />
      <p>{errors.image?.message}</p>

      <button type="submit">
        Submit
      </button>

    </form>
  );
}
```

---

# 3. What `data` looks like

When submitting,

```js
console.log(data);
```

prints something like

```js
{
  title: "Laptop",
  price: "1200",
  description: "Gaming Laptop",
  image: FileList
}
```

Since `image` is a **FileList**, you need the first file:

```js
data.image[0]
```

---

# 4. FormData

```js
const formData = new FormData();

formData.append("title", data.title);
formData.append("price", data.price);
formData.append("description", data.description);
formData.append("image", data.image[0]);
```

---

# 5. Axios POST

```js
await axios.post(url, formData, {
  headers: {
    "Content-Type": "multipart/form-data",
  },
});
```

---

# 6. Django REST Framework

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = "__all__"
```

Model

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField()
    image = models.ImageField(upload_to="products/")
```

View

```python
from rest_framework.parsers import MultiPartParser, FormParser

class ProductCreateAPIView(CreateAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    parser_classes = [MultiPartParser, FormParser]
```

---

# 7. API receives

```text
title = Laptop
price = 1200
description = Gaming Laptop
image = laptop.jpg
```

---

# 8. Multiple Images (Bonus)

```jsx
<input
    type="file"
    multiple
    {...register("images")}
/>
```

```js
const formData = new FormData();

for (const file of data.images) {
    formData.append("images", file);
}
```

---

# 9. Reusable Helper Function

```js
const createFormData = (data) => {
  const formData = new FormData();

  Object.keys(data).forEach((key) => {
    if (key === "image") {
      formData.append(key, data.image[0]);
    } else {
      formData.append(key, data[key]);
    }
  });

  return formData;
};
```

Usage:

```js
const onSubmit = async (data) => {
  const formData = createFormData(data);

  await axios.post("/api/products/", formData);
};
```

This keeps your submit handler clean and is especially useful when your forms have many fields.

> **Tip:** Do **not** manually `JSON.stringify()` the data when uploading files. Files must be sent as `multipart/form-data` using `FormData`; otherwise, Django won't receive the uploaded image correctly.




হ্যাঁ। **Image, Video, Audio বা যেকোনো File** পাঠাতে হলে **`FormData`** ব্যবহার করতে হবে।

কারণ JSON শুধু **text data** পাঠাতে পারে। কিন্তু file (image, video, audio, pdf, zip ইত্যাদি) পাঠানোর জন্য HTTP request-এর `multipart/form-data` encoding লাগে।

---

# Rule

|Data Type|JSON|FormData|
|---|---|---|
|String|✅|✅|
|Number|✅|✅|
|Boolean|✅|✅|
|Array/Object|✅|✅ (প্রয়োজনে stringify)|
|Image|❌|✅|
|Video|❌|✅|
|Audio|❌|✅|
|PDF|❌|✅|
|ZIP|❌|✅|

---

# Example 1: Only Text

```jsx
const data = {
    title: "React Course",
    price: 1000
}

axios.post("/api/course/", data)
```

Network Request

```json
{
    "title": "React Course",
    "price": 1000
}
```

এখানে FormData লাগবে না।

---

# Example 2: Text + Image

```jsx
const formData = new FormData();

formData.append("title", data.title);
formData.append("price", data.price);
formData.append("image", data.image[0]);

axios.post("/api/course/", formData);
```

Request

```
multipart/form-data

title = React Course
price = 1000
image = react.png
```

---

# Example 3: Text + Video

```jsx
const formData = new FormData();

formData.append("title", data.title);
formData.append("video", data.video[0]);

await axios.post("/api/videos/", formData);
```

```
title = Django Tutorial

video = lesson1.mp4
```

---

# Example 4: Text + Audio

```jsx
const formData = new FormData();

formData.append("title", data.title);
formData.append("audio", data.audio[0]);

await axios.post("/api/audio/", formData);
```

```
title = English Lesson

audio = lesson.mp3
```

---

# Example 5: Image + Video + Audio Together

ধরো একটি Social Media Post বানাচ্ছো।

```jsx
const formData = new FormData();

formData.append("caption", data.caption);

formData.append("image", data.image[0]);

formData.append("video", data.video[0]);

formData.append("audio", data.audio[0]);

await axios.post("/api/post/", formData);
```

Backend receive করবে

```
caption = Hello World

image = photo.jpg

video = intro.mp4

audio = music.mp3
```

---

# React Hook Form Example

```jsx
<input
    type="file"
    accept="image/*"
    {...register("image")}
/>

<input
    type="file"
    accept="video/*"
    {...register("video")}
/>

<input
    type="file"
    accept="audio/*"
    {...register("audio")}
/>
```

Submit

```jsx
const onSubmit = async (data) => {
    const formData = new FormData();

    formData.append("title", data.title);

    if (data.image?.length) {
        formData.append("image", data.image[0]);
    }

    if (data.video?.length) {
        formData.append("video", data.video[0]);
    }

    if (data.audio?.length) {
        formData.append("audio", data.audio[0]);
    }

    await axios.post("/api/upload/", formData);
};
```

---

# Multiple Images

```jsx
<input
    type="file"
    multiple
    {...register("images")}
/>
```

```jsx
const formData = new FormData();

for (const file of data.images) {
    formData.append("images", file);
}
```

Backend

```
images[0]
images[1]
images[2]
```

---

# Multiple Videos

```jsx
for (const file of data.videos) {
    formData.append("videos", file);
}
```

---

# Dynamic Solution (Production Ready)

যদি form-এ text এবং file দুই ধরনের field-ই থাকে, তাহলে একটি helper function ব্যবহার করতে পারো:

```jsx
const createFormData = (data) => {
    const formData = new FormData();

    Object.entries(data).forEach(([key, value]) => {
        if (value instanceof FileList) {
            // Single file
            if (value.length === 1) {
                formData.append(key, value[0]);
            } else {
                // Multiple files
                Array.from(value).forEach((file) => {
                    formData.append(key, file);
                });
            }
        } else {
            formData.append(key, value);
        }
    });

    return formData;
};
```

ব্যবহার:

```jsx
const onSubmit = async (data) => {
    const formData = createFormData(data);

    await axios.post("/api/upload/", formData);
};
```

## কখন FormData ব্যবহার করবে?

- ✅ শুধু text (name, email, price, title) → **JSON**
    
- ✅ Text + Image → **FormData**
    
- ✅ Text + Video → **FormData**
    
- ✅ Text + Audio → **FormData**
    
- ✅ Text + PDF/DOCX → **FormData**
    
- ✅ এক বা একাধিক যেকোনো file → **FormData**
    

**মনে রাখার সহজ নিয়ম:** যদি request-এর মধ্যে **একটিও `File` অবজেক্ট থাকে**, তাহলে সাধারণত `FormData` ব্যবহার করাই সঠিক পদ্ধতি।

হ্যাঁ, **`FormData` দিয়ে সব ধরনের data পাঠানো যায়**, তবে কিছু data type-এর জন্য একটু আলাদা করে handle করতে হয়।

## FormData কী কী পাঠাতে পারে?

| Data Type   | FormData Support  | Example      |
| ----------- | ----------------- | ------------ |
| String      | ✅                 | name, title  |
| Number      | ✅                 | price, age   |
| Boolean     | ✅                 | is_active    |
| Image       | ✅                 | photo.jpg    |
| Video       | ✅                 | intro.mp4    |
| Audio       | ✅                 | music.mp3    |
| PDF         | ✅                 | cv.pdf       |
| ZIP         | ✅                 | project.zip  |
| JSON Object | ✅ (stringify করে) | address      |
| Array       | ✅                 | tags, images |

---

## Example 1: String + Number

```js
const formData = new FormData();

formData.append("name", "Atiar");
formData.append("age", 24);
formData.append("salary", 50000);
```

Backend

```text
name = Atiar
age = 24
salary = 50000
```

---

## Example 2: Boolean

```js
formData.append("is_active", true);
```

Backend-এ এটি সাধারণত string হিসেবে আসে:

```text
is_active = "true"
```

DRF serializer সাধারণত এটিকে Boolean-এ convert করে নিতে পারে।

---

## Example 3: Image

```js
formData.append("image", data.image[0]);
```

---

## Example 4: Object

Object সরাসরি append করা যাবে না।

❌ ভুল

```js
formData.append("address", {
    city: "Dhaka",
    country: "Bangladesh"
});
```

এটি পাঠাবে:

```text
[object Object]
```

✅ সঠিক

```js
formData.append(
    "address",
    JSON.stringify({
        city: "Dhaka",
        country: "Bangladesh",
    })
);
```

Backend (DRF)

```python
import json

address = json.loads(request.data["address"])
```

---

## Example 5: Array

```js
const tags = ["React", "NextJS", "Django"];

tags.forEach(tag => {
    formData.append("tags", tag);
});
```

অথবা

```js
formData.append("tags", JSON.stringify(tags));
```

---

## Example 6: Everything Together

```js
const formData = new FormData();

formData.append("title", data.title);
formData.append("price", data.price);
formData.append("is_active", data.is_active);

formData.append("image", data.image[0]);
formData.append("video", data.video[0]);
formData.append("audio", data.audio[0]);

formData.append(
    "address",
    JSON.stringify(data.address)
);

formData.append(
    "tags",
    JSON.stringify(data.tags)
);

await axios.post("/api/products/", formData);
```

---

## React Hook Form Example

```js
const onSubmit = (data) => {
    const formData = new FormData();

    Object.entries(data).forEach(([key, value]) => {
        if (value instanceof FileList) {
            formData.append(key, value[0]);
        } else if (typeof value === "object" && value !== null) {
            formData.append(key, JSON.stringify(value));
        } else {
            formData.append(key, value);
        }
    });

    axios.post("/api/products/", formData);
};
```

---

## Production Best Practice

* **শুধু text data** → JSON (`application/json`)
* **যদি একটিও file (image/video/audio/pdf) থাকে** → `FormData` (`multipart/form-data`)
* **Object বা Array** → `JSON.stringify()` করে `FormData`-তে যোগ করো, তারপর backend-এ `json.loads()` দিয়ে parse করো।

এভাবে `FormData` ব্যবহার করে প্রায় সব ধরনের data একসাথে একটি request-এ পাঠানো যায়।
