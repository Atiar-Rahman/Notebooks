
**Axios** is a JavaScript library used to make **HTTP requests** from frontend applications (React, Vue, etc.) or Node.js.

Simply:

> Axios helps your app communicate with a backend API.

Example:

React app → Axios → Django/Node API → Database

```
Frontend
   |
   | GET / POST request
   ↓
Axios
   |
   ↓
Backend API
   |
   ↓
Database
```

---

## Install Axios

React project:

```bash
npm install axios
```

---

## 1. GET Request (Fetch Data)

Example: Get users

```jsx
import axios from "axios";


axios.get("https://api.example.com/users")
.then(response => {

  console.log(response.data);

})
.catch(error => {

  console.log(error);

});
```

Response:

```json
[
 {
  "id":1,
  "name":"Atiar"
 }
]
```

---

## 2. Using Axios in React Component

```jsx
import {useEffect,useState} from "react";
import axios from "axios";


function Users(){

 const [users,setUsers]=useState([]);


 useEffect(()=>{


  axios.get("https://api.example.com/users")
  .then(res=>{

    setUsers(res.data);

  })


 },[]);



 return (

  <div>

   {
    users.map(user=>

     <h1 key={user.id}>
       {user.name}
     </h1>

    )
   }

  </div>

 )

}

export default Users;
```

---

# POST Request

Send data to server.

Example: Register user

```javascript
axios.post(
 "https://api.example.com/register",
 {
   name:"Atiar",
   email:"test@gmail.com",
   password:"123456"
 }
)
.then(res=>{

 console.log(res.data);

});
```

Sends:

```json
{
 "name":"Atiar",
 "email":"test@gmail.com",
 "password":"123456"
}
```

---

# PUT Request

Update full data:

```javascript
axios.put(
 "/users/1",
 {
  name:"Rahman",
  age:25
 }
)
```

---

# PATCH Request

Update partial data:

```javascript
axios.patch(
 "/users/1",
 {
  age:26
 }
)
```

---

# DELETE Request

Delete:

```javascript
axios.delete(
 "/users/1"
)
```

---

## Axios vs Fetch

|Axios|Fetch|
|---|---|
|External library|Built-in JS|
|Automatic JSON conversion|Need `.json()`|
|Easy error handling|More manual|
|Interceptors available|No interceptor|
|Request timeout easy|More setup|

Fetch:

```javascript
fetch(url)
.then(res=>res.json())
.then(data=>console.log(data))
```

Axios:

```javascript
axios.get(url)
.then(res=>console.log(res.data))
```

---

## Axios Instance (Professional Way)

Instead of writing URL every time:

`api.js`

```javascript
import axios from "axios";


const api = axios.create({

 baseURL:"http://localhost:5000/api"

});


export default api;
```

Use:

```javascript
import api from "./api";


api.get("/users")
.then(res=>{

 console.log(res.data);

});
```

Now:

```
api.get("/users")

means

http://localhost:5000/api/users
```

---

## Axios Interceptor (JWT Auth)

Automatically add token:

```javascript
api.interceptors.request.use(
(config)=>{

 config.headers.Authorization =
 `Bearer ${token}`;

 return config;

}
)
```

Used in:

- Login systems
    
- Admin panels
    
- E-commerce
    
- Dashboards
    

---

In React projects, common stack:

```
React
 |
Axios
 |
REST API
 |
Django / Node / Laravel
 |
Database
```

Axios is basically a cleaner, more powerful alternative to `fetch()`.

--------------

না, **Axios শুধু fetch-related কাজ করে না**। Axios মূলত **HTTP client** — মানে server এর সাথে communication করার জন্য ব্যবহার হয়।

`fetch()` এর মতো GET/POST request করতে পারে, কিন্তু আরো অনেক কাজ সহজ করে।

### Axios দিয়ে যা যা করা যায়:

## 1. GET (data আনা)

```javascript
axios.get("/users")
```

যেমন:

React → Backend → Database

---

## 2. POST (data পাঠানো)

```javascript
axios.post("/users", {
  name:"Atiar",
  age:22
})
```

Form submit, registration, login এ ব্যবহার হয়।

---

## 3. PUT (পুরো data update)

```javascript
axios.put("/users/1", {
 name:"Rahim",
 age:25
})
```

---

## 4. PATCH (partial update)

```javascript
axios.patch("/users/1", {
 age:26
})
```

---

## 5. DELETE

```javascript
axios.delete("/users/1")
```

---

## 6. File upload

Image upload:

```javascript
const formData = new FormData();

formData.append(
 "image",
 file
);


axios.post(
 "/upload",
 formData
);
```

---

## 7. Header পাঠানো

JWT token:

```javascript
axios.get("/profile",{

 headers:{
  Authorization:`Bearer ${token}`
 }

})
```

---

## 8. Request timeout

```javascript
axios.get("/users",{
 timeout:5000
})
```

৫ সেকেন্ডের মধ্যে response না এলে cancel।

---

## 9. Interceptor

সব request এর আগে কিছু add করা:

```javascript
axios.interceptors.request.use(
(config)=>{

 config.headers.token="abc123";

 return config;

}
)
```

সব API call এ token চলে যাবে।

---

## 10. Multiple request একসাথে

```javascript
axios.all([
 axios.get("/users"),
 axios.get("/products")
])
.then(response=>{

 console.log(response);

})
```

---

## Fetch vs Axios

### Fetch:

```javascript
fetch("/users")
.then(res=>res.json())
.then(data=>console.log(data))
```

### Axios:

```javascript
axios.get("/users")
.then(res=>{
 console.log(res.data)
})
```

Axios এ JSON convert করা লাগে না।

---

React project এ সাধারণ flow:

```
React Component
        |
        |
     Axios
        |
        |
 REST API
        |
        |
 Backend (Django/Node)
        |
        |
 Database
```

তাই Axios শুধু `fetch()` এর replacement না, এটা **complete API communication tool**।

----

