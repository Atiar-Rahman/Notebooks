Below is **Day-2 FastAPI – Request & Response Handling (A → Z)**, fully structured with **concepts, examples, and a mini-task (file upload API)**.  
This is everything you need to complete Day-2 confidently.

---

# 🚀 **Day 2 – Request & Response Handling (Full A → Z Guide)**

---

# 1️⃣ **Request Body (Using Pydantic Models)**

Use Pydantic models to define data structure for JSON body.

### ✔ Example

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    age: int
    email: str

@app.post("/create-user")
def create_user(user: User):
    return {"message": "User created!", "data": user}
```

### Test JSON

```json
{
  "name": "Atiar",
  "age": 22,
  "email": "test@gmail.com"
}
```

---

# 2️⃣ **Response Models (Control What You Return)**

Use `response_model` to **filter output**.

### ✔ Example

```python
class UserIn(BaseModel):
    name: str
    password: str

class UserOut(BaseModel):
    name: str

@app.post("/register", response_model=UserOut)
def register(user: UserIn):
    return user
```

👉 Even if user sends password, it will NOT return back.

---

# 3️⃣ **Response Status Codes**

Set status code using:

```python
from fastapi import status
```

### ✔ Example

```python
from fastapi import FastAPI, status

@app.post("/items", status_code=status.HTTP_201_CREATED)
def create_item():
    return {"message": "Item created"}
```

Common status codes:

- `200 OK`
    
- `201 Created`
    
- `204 No Content`
    
- `400 Bad Request`
    
- `404 Not Found`
    
- `500 Server Error`
    

---

# 4️⃣ **Handling Form Data + File Uploads**

## 📌 Form Data (e.g., login forms)

Use `Form` instead of body.

```python
from fastapi import Form

@app.post("/login")
def login(username: str = Form(...), password: str = Form(...)):
    return {"username": username}
```

---

## 📌 File Upload (image/doc)

Use `UploadFile` and `File`.

```python
from fastapi import UploadFile, File

@app.post("/upload")
def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename, "type": file.content_type}
```

---

# 5️⃣ **Response Objects (Custom Response)**

FastAPI allows you to customize responses.

### ✔ JSONResponse

```python
from fastapi.responses import JSONResponse

@app.get("/custom")
def custom():
    return JSONResponse(content={"message": "Custom response"}, status_code=200)
```

---

### ✔ HTMLResponse

```python
from fastapi.responses import HTMLResponse

@app.get("/html")
def show_html():
    return HTMLResponse("<h1>Hello World</h1>")
```

---

### ✔ FileResponse (Download files)

```python
from fastapi.responses import FileResponse

@app.get("/download")
def download():
    return FileResponse("sample.pdf", filename="myfile.pdf")
```

---

# 🎯 **Mini Task – File Upload API (Image/Document)**

Below is the **complete task**, from creating the API → saving file → returning file info.

---

## ✔ Step 1: Create Upload Endpoint

```python
from fastapi import FastAPI, UploadFile, File
import shutil
import os

app = FastAPI()

UPLOAD_DIR = "uploads"
os.makedirs(UPLOAD_DIR, exist_ok=True)

@app.post("/upload-file")
async def upload_file(file: UploadFile = File(...)):
    file_location = f"{UPLOAD_DIR}/{file.filename}"

    with open(file_location, "wb") as buffer:
        shutil.copyfileobj(file.file, buffer)

    return {
        "filename": file.filename,
        "content_type": file.content_type,
        "saved_to": file_location
    }
```

---

## ✔ Step 2: Accept Only Images (Optional)

```python
@app.post("/upload-image")
async def upload_image(file: UploadFile = File(...)):
    if not file.filename.lower().endswith((".jpg", ".jpeg", ".png")):
        return {"error": "Only image files allowed!"}

    file_path = f"uploads/{file.filename}"

    with open(file_path, "wb") as buffer:
        shutil.copyfileobj(file.file, buffer)

    return {"message": "Image uploaded", "path": file_path}
```

---

## ✔ Step 3: Accept Multiple Files

```python
from typing import List

@app.post("/upload-multiple")
async def upload_multiple(files: List[UploadFile] = File(...)):
    file_paths = []

    for file in files:
        path = f"uploads/{file.filename}"
        with open(path, "wb") as buffer:
            shutil.copyfileobj(file.file, buffer)
        file_paths.append(path)

    return {"uploaded_files": file_paths}
```

---

# 🎉 **Day-2 Summary (What You Completed)**

✔ Request Body (Pydantic models)  
✔ Response Models  
✔ Response Status Codes  
✔ Form Data  
✔ File Uploads (image/doc)  
✔ Response Objects  
✔ Mini Task (Full File Upload API)

---

# 🚀 Ready for Day 3?

Day-3 Topics:

- Path parameters advanced
    
- Query + Request body combination
    
- Dependency Injection
    
- Middleware
    
- Cookies + Headers
    

Tell me if you want Day-3 guide!

Below is **Day-3 FastAPI – Advanced Topics (A → Z Complete Guide)**  
Includes **Path Parameters (advanced), Query + Body combo, Dependency Injection, Middleware, Cookies & Headers** with clean examples.

---

# 🚀 **Day 3 – COMPLETE ADVANCED GUIDE**

---

# 1️⃣ **Advanced Path Parameters**

## ✔ Path parameters with validation (`Path()`)

```python
from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/items/{item_id}")
def get_item(item_id: int = Path(gt=0, lt=100)):
    return {"item_id": item_id}
```

Constraints:

- `gt` → greater than
    
- `ge` → greater or equal
    
- `lt` → less than
    
- `le` → less or equal
    

---

## ✔ Path ordering: static first, dynamic later

Correct:

```
/users/me
/users/{user_id}
```

Incorrect (FastAPI will confuse routes):

```
/users/{user_id}
/users/me
```

---

## ✔ Path parameter with ENUM validation

```python
from enum import Enum

class Category(str, Enum):
    laptop = "laptop"
    phone = "phone"
    tv = "tv"

@app.get("/products/{category}")
def get_category(category: Category):
    return {"category": category}
```

---

## ✔ Capture ALL remaining path (path converter)

Useful for file paths.

```python
@app.get("/files/{file_path:path}")
def read_file(file_path: str):
    return {"path": file_path}
```

URL:

```
/files/images/2024/january/photo.png
```

---

# 2️⃣ **Query + Request Body Combination**

You can mix:

- Path parameters
    
- Query parameters
    
- Request body
    

### ✔ Example

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.put("/items/{item_id}")
def update_item(
    item_id: int,
    item: Item,
    q: str | None = None,
    limit: int = 10
):
    return {
        "item_id": item_id,
        "item": item,
        "query": q,
        "limit": limit
    }
```

👉 Example URL:

```
PUT /items/10?q=phone&limit=5
```

---

# 3️⃣ **Dependency Injection (DI)**

FastAPI's most powerful feature.

Used for:

- DB sessions
    
- Authentication
    
- Reusable functions
    

---

## ✔ Simple DI Example (Function Dependency)

```python
from fastapi import Depends

def get_token():
    return "sample-token"

@app.get("/secure")
def secure(token: str = Depends(get_token)):
    return {"token": token}
```

---

## ✔ DI With Parameters

```python
def verify_user(active: bool = True):
    return {"active": active}

@app.get("/user")
def user(info=Depends(verify_user)):
    return info
```

---

## ✔ Class as Dependency

```python
class Settings:
    def __init__(self):
        self.app_name = "FastAPI App"

def get_settings():
    return Settings()

@app.get("/config")
def config(settings: Settings = Depends(get_settings)):
    return {"app": settings.app_name}
```

---

# 4️⃣ **Middleware (Run code before/after request)**

Used for:

- Logging
    
- Authentication
    
- Changing response
    
- Adding headers
    

---

### ✔ Example: Logging Middleware

```python
from fastapi import Request
from fastapi.middleware.cors import CORSMiddleware

@app.middleware("http")
async def log_requests(request: Request, call_next):
    print("Request path:", request.url.path)
    response = await call_next(request)
    print("Response status:", response.status_code)
    return response
```

---

### ✔ Adding CORS Middleware

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

---

# 5️⃣ **Cookies + Headers**

---

# 🍪 **Cookies**

## ✔ Set a Cookie

```python
from fastapi import Response

@app.get("/set-cookie")
def set_cookie(response: Response):
    response.set_cookie(key="username", value="atiar")
    return {"message": "Cookie set!"}
```

---

## ✔ Read a Cookie

```python
from fastapi import Cookie

@app.get("/get-cookie")
def get_cookie(username: str = Cookie(None)):
    return {"cookie_value": username}
```

---

# 📌 **Delete Cookie**

```python
@app.get("/delete-cookie")
def delete_cookie(response: Response):
    response.delete_cookie("username")
    return {"message": "Cookie deleted!"}
```

---

# 📨 **Headers**

## ✔ Read request headers

```python
from fastapi import Header

@app.get("/header")
def read_header(user_agent: str = Header(None)):
    return {"User-Agent": user_agent}
```

---

## ✔ Send custom response header

```python
from fastapi.responses import JSONResponse

@app.get("/custom-header")
def custom_header():
    response = JSONResponse({"message": "Hello"})
    response.headers["X-API-Version"] = "1.0.0"
    return response
```

---

# 🎉 **Day-3 Summary**

|Topic|Status|
|---|---|
|Advanced Path Parameters|✔ Completed|
|Query + Body|✔ Completed|
|Dependency Injection|✔ Completed|
|Middleware|✔ Completed|
|Cookies|✔ Completed|
|Headers|✔ Completed|

---

# 🚀 Next: Day-4 (Big Concepts)

Day-4 includes:

- Authentication (OAuth2 + JWT)
    
- Password hashing
    
- User registration + login
    
- Protecting routes
    
- Authorization roles
    
- Email verification (optional)
    

If you want **Day-4 A → Z complete guide**, just tell me:  
**"Give me Day-4"**