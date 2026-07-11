যদি JWT authentication ব্যবহার করেন, তাহলে frontend থেকে POST API call করার সময় `Authorization` header-এ token পাঠাতে হবে।

সাধারণত format হয়:

```http
Authorization: Bearer <jwt_token>
```

যদি আপনার backend বিশেষভাবে `JWT` prefix চায়, তাহলে:

```http
Authorization: JWT <jwt_token>
```

### JavaScript (Fetch API)

```javascript
const token = localStorage.getItem("token");

fetch("https://api.example.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": `JWT ${token}` // অথবা Bearer ${token}
  },
  body: JSON.stringify({
    title: "Hello",
    description: "Test"
  })
})
.then(res => res.json())
.then(data => console.log(data))
.catch(err => console.error(err));
```

---

### Axios

```javascript
import axios from "axios";

const token = localStorage.getItem("token");

axios.post(
  "https://api.example.com/posts",
  {
    title: "Hello",
    description: "Test"
  },
  {
    headers: {
      Authorization: `JWT ${token}` // অথবা Bearer ${token}
    }
  }
)
.then(res => console.log(res.data))
.catch(err => console.log(err));
```

---

### API Class ব্যবহার করলে

```javascript
class ApiService {
  constructor() {
    this.baseUrl = "https://api.example.com";
  }

  async post(url, data) {
    const token = localStorage.getItem("token");

    const response = await fetch(`${this.baseUrl}${url}`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `JWT ${token}`
      },
      body: JSON.stringify(data)
    });

    return response.json();
  }
}

// ব্যবহার
const api = new ApiService();

api.post("/posts", {
  title: "Hello",
  description: "World"
}).then(data => {
  console.log(data);
});
```

### যদি Backend-এ লেখা থাকে:

```
Authorization: jwt token
```

তাহলে header হবে:

```javascript
headers: {
  Authorization: `JWT ${token}`
}
```

অথবা backend যদি lowercase `jwt` চায়:

```javascript
headers: {
  Authorization: `jwt ${token}`
}
```

**একটা বিষয় নিশ্চিত করুন:** আপনার backend আসলে কোন format expect করছে—`Bearer`, `JWT`, নাকি `jwt`। কারণ এগুলো backend implementation-এর উপর নির্ভর করে।

আপনি যদি **Flutter**, **React**, **React Native**, **Angular**, বা **Vue** ব্যবহার করেন, জানালে সেই framework অনুযায়ী উদাহরণ দেখাতে পারি।


-------
