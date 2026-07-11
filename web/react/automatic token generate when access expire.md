React + Axios হলে সবচেয়ে ভালো approach হলো **Axios instance + response interceptor** ব্যবহার করা। এতে আপনার সব API call-এর জন্য token expiry check, refresh token call, নতুন access token save, এবং failed request retry—সব automatic হবে।

### ১. Axios instance তৈরি করুন

`api.js`

```javascript
import axios from "axios";

const api = axios.create({
    baseURL: "http://localhost:8000/api",
});


// Request interceptor - প্রতিটি request এ access token যোগ করবে
api.interceptors.request.use(
    (config) => {
        const token = localStorage.getItem("access");

        if (token) {
            config.headers.Authorization = `Bearer ${token}`;
        }

        return config;
    },
    (error) => Promise.reject(error)
);


let isRefreshing = false;
let failedQueue = [];

const processQueue = (error, token = null) => {
    failedQueue.forEach((promise) => {
        if (error) {
            promise.reject(error);
        } else {
            promise.resolve(token);
        }
    });

    failedQueue = [];
};


// Response interceptor - 401 হলে refresh করবে
api.interceptors.response.use(
    (response) => response,

    async (error) => {
        const originalRequest = error.config;

        if (
            error.response?.status === 401 &&
            !originalRequest._retry
        ) {

            if (isRefreshing) {
                return new Promise((resolve, reject) => {
                    failedQueue.push({
                        resolve,
                        reject
                    });
                })
                .then(token => {
                    originalRequest.headers.Authorization =
                        `Bearer ${token}`;

                    return api(originalRequest);
                });
            }


            originalRequest._retry = true;
            isRefreshing = true;

            try {
                const refresh = localStorage.getItem("refresh");

                const response = await axios.post(
                    "http://localhost:8000/api/token/refresh/",
                    {
                        refresh: refresh
                    }
                );


                const newAccess = response.data.access;

                localStorage.setItem(
                    "access",
                    newAccess
                );


                processQueue(null, newAccess);


                originalRequest.headers.Authorization =
                    `Bearer ${newAccess}`;


                return api(originalRequest);


            } catch (refreshError) {

                processQueue(refreshError, null);

                localStorage.removeItem("access");
                localStorage.removeItem("refresh");

                window.location.href = "/login";

                return Promise.reject(refreshError);

            } finally {
                isRefreshing = false;
            }
        }


        return Promise.reject(error);
    }
);


export default api;
```

---

### ২. এখন সব API call এ এই `api` ব্যবহার করবেন

```javascript
import api from "./api";


const getUsers = async () => {
    const response = await api.get("/users/");
    return response.data;
};


const createOrder = async (data) => {
    const response = await api.post("/orders/", data);
    return response.data;
};
```

এখন flow হবে:

```
Component
   |
   |
api.get()
   |
   ▼
Axios Request Interceptor
   |
   ▼
Access Token attach
   |
   ▼
Django API
   |
   ├── 200 → Data return
   |
   └── 401
          |
          ▼
     Refresh Token API
          |
          ▼
     New Access Token
          |
          ▼
     localStorage update
          |
          ▼
     Original API আবার call
```

এখন আপনার project-এ ১০টা বা ১০০০টা API থাকলেও token refresh logic এক জায়গা থেকেই handle হবে।

একটা production improvement হিসেবে সাধারণত **একাধিক API একসাথে 401 দিলে যাতে একসাথে অনেক refresh request না যায়**, তার জন্য `isRefreshing + failedQueue` pattern ব্যবহার করা হয় (উপরের code-এ সেটাই আছে)।


---------------
