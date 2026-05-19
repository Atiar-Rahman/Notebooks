# Swagger api generator using drf-yasg library

### step1
```shell
pip install -U drf-yasg
```

### step2
```shell
INSTALLED_APPS = [
   ...
   'django.contrib.staticfiles',  # required for serving swagger ui's css/js files
   'drf_yasg',
   ...
]
```

### step3
```shell
...
from django.urls import re_path
from rest_framework import permissions
from drf_yasg.views import get_schema_view
from drf_yasg import openapi

...

schema_view = get_schema_view(
   openapi.Info(
      title="Snippets API",
      default_version='v1',
      description="Test description",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@snippets.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
   permission_classes=(permissions.AllowAny,),
)

urlpatterns = [
   path('swagger<format>/', schema_view.without_ui(cache_timeout=0), name='schema-json'),
   path('swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),
   path('redoc/', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),
   ...
]
```


#### step4
Security definitions  
###### here Bearer used for JWT authentication

```shell
SWAGGER_SETTINGS = {
   'SECURITY_DEFINITIONS': {
      'Bearer': {
            'type': 'apiKey',
            'name': 'Authorization',
            'in': 'header',
            'description':'Enter your jwt token format `JWT <your token>`'
      }
   }
}
```


### How to write documentation
##### Api endpoint description added
```
views er modye:

"""
this api is used for authentication

-  this is
- hellp
"""

```

this used for api endpoint description
![[Pasted image 20260316001417.png]]

`-`  is show 

![[Pasted image 20260316002017.png]]

@swaggger_auto_schema use  kore  description likha zay

![[Pasted image 20260316002312.png]]


তুমি যেটা লিখেছো সেটা **drf-yasg** ব্যবহার করে Django REST API এর **Swagger documentation auto-generate** করার পদ্ধতি।
এটা backend API develop করার সময় খুব useful — বিশেষ করে তুমি যেহেতু **Django + DRF দিয়ে AI CCTV backend** বানাচ্ছো, তখন frontend বা অন্য developer সহজে API বুঝতে পারবে।

আমি এখন **step by step সব term explain করছি example সহ।**

---

# 1️⃣ drf-yasg কি?

**drf-yasg**

👉 এটা Django REST Framework এর জন্য একটি library যা automatically API documentation তৈরি করে।

এটা দুইটা UI দেয়:

1️⃣ **Swagger UI** → interactive API testing
2️⃣ **ReDoc** → clean documentation view

---

# 2️⃣ Step 1 – Library install

```bash
pip install -U drf-yasg
```

### Explanation

* `pip` → python package manager
* `install` → package install
* `-U` → upgrade to latest version

👉 এই command run করলে **drf-yasg library project এ add হবে**

---

# 3️⃣ Step 2 – INSTALLED_APPS

```python
INSTALLED_APPS = [
   ...
   'django.contrib.staticfiles',
   'drf_yasg',
]
```

### 1️⃣ django.contrib.staticfiles

Swagger UI এর

* CSS
* JS
* images

serve করার জন্য এটা দরকার।

Swagger UI basically একটি **frontend web page**।

---

### 2️⃣ drf_yasg

এটা add করলে Django project জানবে তুমি Swagger documentation ব্যবহার করছো।

---

# 4️⃣ Step 3 – schema_view create

```python
from django.urls import re_path
from rest_framework import permissions
from drf_yasg.views import get_schema_view
from drf_yasg import openapi
```

### imports explanation

| import          | কাজ                      |
| --------------- | ------------------------ |
| re_path         | regex url                |
| permissions     | API permission           |
| get_schema_view | swagger schema generator |
| openapi         | OpenAPI specification    |

---

# 5️⃣ schema_view কি?

```python
schema_view = get_schema_view(
   openapi.Info(
      title="Snippets API",
      default_version='v1',
      description="Test description",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@snippets.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
   permission_classes=(permissions.AllowAny,),
)
```

### schema_view = Swagger configuration

এখানে API documentation এর **metadata** define করা হয়।

---

# 6️⃣ openapi.Info fields explain

### title

```python
title="Snippets API"
```

👉 API এর নাম

Example:

```
AI CCTV Surveillance API
```

---

### version

```python
default_version='v1'
```

👉 API version

Example:

```
v1
v2
v3
```

Industry example:

```
/api/v1/cameras
/api/v2/cameras
```

---

### description

```python
description="Test description"
```

👉 API এর summary

Example

```
AI CCTV surveillance backend API for detecting suspicious activities
```

---

### terms_of_service

```python
terms_of_service="https://www.google.com/policies/terms/"
```

👉 API usage rules

Example

```
https://myapi.com/terms
```

---

### contact

```python
contact=openapi.Contact(email="contact@snippets.local")
```

👉 API maintainer

Example

```
support@cctv-ai.com
```

---

### license

```python
license=openapi.License(name="BSD License")
```

👉 API license

Example

```
MIT
Apache 2.0
BSD
```

---

# 7️⃣ public=True

```python
public=True
```

👉 API documentation public

মানে:

```
anyone can see docs
```

---

# 8️⃣ permission_classes

```python
permission_classes=(permissions.AllowAny,)
```

Swagger documentation access permission।

Example:

| Permission      | Meaning          |
| --------------- | ---------------- |
| AllowAny        | সবাই দেখতে পারবে |
| IsAuthenticated | login user only  |

---

# 9️⃣ URL patterns

```python
urlpatterns = [
   path('swagger<format>/', schema_view.without_ui(cache_timeout=0), name='schema-json'),

   path('swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),

   path('redoc/', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),
]
```

---

## 1️⃣ swagger JSON schema

```
/swagger.json
```

Example:

```
http://localhost:8000/swagger.json
```

👉 API schema in JSON format

Used by

* Postman
* OpenAPI tools

---

## 2️⃣ swagger UI

```
/swagger/
```

Example

```
http://localhost:8000/swagger/
```

👉 interactive UI

তুমি এখানে

* endpoint দেখতে পারবে
* API test করতে পারবে

Example:

```
GET /api/cameras
POST /api/login
```

---

## 3️⃣ ReDoc UI

```
/redoc/
```

Example

```
http://localhost:8000/redoc/
```

👉 cleaner documentation

Used by:

* companies
* API docs site

---

# 🔟 Step 4 – Security definition

```python
SWAGGER_SETTINGS = {
   'SECURITY_DEFINITIONS': {
      'Bearer': {
            'type': 'apiKey',
            'name': 'Authorization',
            'in': 'header',
            'description':'Enter your jwt token format `JWT <your token>`'
      }
   }
}
```

Swagger কে বলা হচ্ছে:

```
API uses JWT authentication
```

---

### type

```
apiKey
```

মানে token based auth

---

### name

```
Authorization
```

header name

Example request

```
Authorization: JWT eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

---

### in

```
header
```

মানে token header এ যাবে।

---

### description

Swagger UI তে instruction দেখাবে

Example

```
JWT eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

---

# 1️⃣1️⃣ API documentation write

তুমি view এর ভিতরে docstring লিখতে পারো।

Example

```python
class LoginView(APIView):
    """
    This API is used for user authentication.

    - user login
    - return JWT token
    """
```

Swagger UI তে এটা show হবে।

---

# 1️⃣2️⃣ Bullet list

```
-
```

Example

```
- login user
- return token
```

Swagger এ list হিসেবে দেখাবে।

---

# 1️⃣3️⃣ swagger_auto_schema

Decorator ব্যবহার করে extra documentation দেওয়া যায়।

Example

```python
from drf_yasg.utils import swagger_auto_schema

class LoginView(APIView):

    @swagger_auto_schema(
        operation_description="Login user and return JWT token"
    )
    def post(self, request):
        pass
```

Swagger UI তে এটা দেখাবে।

---

# 1️⃣4️⃣ Professional example

AI CCTV API example

```python
class CameraListView(APIView):
    """
    Get all cameras in the system.

    - list all cameras
    - return camera stream urls
    """

    def get(self, request):
        pass
```

Swagger UI

```
GET /api/cameras
```

description show করবে।

---

# 1️⃣5️⃣ Real project flow

Industry API docs flow:

```
Swagger
   ↓
Frontend developer
   ↓
Reads API
   ↓
Integrates React frontend
```

---

# 🚀 তোমার AI CCTV project এ Swagger ব্যবহার করলে

Frontend easily বুঝবে

Example endpoints

```
POST /api/login
GET /api/cameras
POST /api/alerts
GET /api/events
```

সব documentation automatically show হবে।

---

**`@swagger_auto_schema`** হলো **drf-yasg** লাইব্রেরির একটি decorator।
এটা ব্যবহার করে তুমি **Swagger documentation customize** করতে পারো—যেমন:

* request body
* response
* parameters
* description
* tags
* examples
* security

নিচে **সবচেয়ে বেশি ব্যবহার হওয়া options গুলো step-by-step explain করছি example সহ।**

---

# 1️⃣ operation_description

API endpoint এর **description** লিখতে ব্যবহার হয়।

### Example

```python
@swagger_auto_schema(
    operation_description="Login user and return JWT token"
)
def post(self, request):
    pass
```

Swagger UI তে দেখাবে:

```
Login user and return JWT token
```

---

# 2️⃣ operation_summary

Short title দেয়।

### Example

```python
@swagger_auto_schema(
    operation_summary="User Login"
)
```

Swagger UI তে:

```
User Login
```

---

# 3️⃣ request_body

API তে **কি data পাঠাতে হবে** সেটা define করে।

### Example

```python
@swagger_auto_schema(
    request_body=LoginSerializer
)
def post(self, request):
    pass
```

Serializer:

```python
class LoginSerializer(serializers.Serializer):
    email = serializers.EmailField()
    password = serializers.CharField()
```

Swagger UI automatically দেখাবে:

```
{
  "email": "string",
  "password": "string"
}
```

---

# 4️⃣ responses

API response structure define করা যায়।

### Example

```python
@swagger_auto_schema(
    responses={
        200: "Login success",
        400: "Invalid credentials"
    }
)
```

Swagger UI তে show করবে।

---

### Serializer সহ response

```python
@swagger_auto_schema(
    responses={200: UserSerializer}
)
```

---

# 5️⃣ manual_parameters

Query parameters define করতে।

Example:

```
/api/cameras/?page=1
```

### Example

```python
from drf_yasg import openapi

page_param = openapi.Parameter(
    'page',
    openapi.IN_QUERY,
    description="Page number",
    type=openapi.TYPE_INTEGER
)

@swagger_auto_schema(
    manual_parameters=[page_param]
)
```

Swagger UI তে দেখাবে:

```
page : integer
```

---

# 6️⃣ tags

API group করতে ব্যবহার হয়।

### Example

```python
@swagger_auto_schema(
    tags=["Authentication"]
)
```

Swagger UI:

```
Authentication
    POST /login
    POST /register
```

---

# 7️⃣ security

JWT authentication define করতে।

Example:

```python
@swagger_auto_schema(
    security=[{'Bearer': []}]
)
```

Swagger UI তে:

```
Authorize
```

button দেখাবে।

---

# 8️⃣ examples

Example request body দেখাতে।

### Example

```python
@swagger_auto_schema(
    request_body=openapi.Schema(
        type=openapi.TYPE_OBJECT,
        properties={
            'email': openapi.Schema(type=openapi.TYPE_STRING),
            'password': openapi.Schema(type=openapi.TYPE_STRING)
        },
        example={
            "email": "admin@gmail.com",
            "password": "123456"
        }
    )
)
```

Swagger UI example দেখাবে।

---

# 9️⃣ deprecated

API deprecated mark করতে।

### Example

```python
@swagger_auto_schema(
    deprecated=True
)
```

Swagger UI তে warning দেখাবে।

---

# 🔟 method specify করা

ViewSet এ method আলাদা করে define করা যায়।

### Example

```python
@swagger_auto_schema(method='post')
```

---

# 1️⃣1️⃣ field description

Serializer field documentation improve করা যায়।

Example:

```python
class CameraSerializer(serializers.Serializer):
    name = serializers.CharField(help_text="Camera name")
    location = serializers.CharField(help_text="Camera location")
```

Swagger UI তে description দেখাবে।

---

# 1️⃣2️⃣ Complete example

```python
from drf_yasg.utils import swagger_auto_schema

class LoginView(APIView):

    @swagger_auto_schema(
        operation_summary="User Login",
        operation_description="Authenticate user and return JWT token",
        request_body=LoginSerializer,
        responses={
            200: "Login successful",
            400: "Invalid credentials"
        },
        tags=["Authentication"]
    )
    def post(self, request):
        pass
```

Swagger UI তে:

```
Authentication
   POST /login
```

---

# 🚀 AI CCTV project example

তোমার project এ:

```python
@swagger_auto_schema(
    operation_summary="List Cameras",
    operation_description="Return all CCTV cameras",
    responses={200: CameraSerializer(many=True)},
    tags=["Cameras"]
)
def get(self, request):
    pass
```

Swagger UI:

```
Cameras
   GET /api/cameras
```

---





# with example

# 1️⃣ Industry API Documentation Structure

বড় project এ Swagger সাধারণত এই structure follow করে:

```
API Documentation

Authentication
   POST /api/v1/auth/login
   POST /api/v1/auth/register

Users
   GET /api/v1/users
   GET /api/v1/users/{id}

Cameras
   GET /api/v1/cameras
   POST /api/v1/cameras

Alerts
   GET /api/v1/alerts
   POST /api/v1/alerts
```

এখানে **tags ব্যবহার করে group করা হয়**।

Example:

```python
@swagger_auto_schema(tags=["Authentication"])
```

---

# 2️⃣ Professional Serializer Documentation

Serializer field এ description দেওয়া হয়।

```python
class LoginSerializer(serializers.Serializer):
    email = serializers.EmailField(
        help_text="User email address"
    )
    password = serializers.CharField(
        help_text="User password",
        write_only=True
    )
```

Swagger UI automatically দেখাবে।

---

# 3️⃣ Professional Request + Response Documentation

Industry projects এ **request_body + responses** সবসময় define করা হয়।

Example:

```python
@swagger_auto_schema(
    operation_summary="User Login",
    operation_description="""
Authenticate user using email and password.

Returns JWT access token if authentication is successful.
""",
    request_body=LoginSerializer,
    responses={
        200: openapi.Response(
            description="Login successful",
            schema=TokenSerializer
        ),
        400: "Invalid credentials"
    },
    tags=["Authentication"]
)
```

---

# 4️⃣ Query Parameters Documentation

Industry projects এ pagination / filtering parameters define করা হয়।

Example:

```
GET /api/v1/cameras?page=1&limit=10
```

Swagger documentation:

```python
page_param = openapi.Parameter(
    'page',
    openapi.IN_QUERY,
    description="Page number",
    type=openapi.TYPE_INTEGER
)

limit_param = openapi.Parameter(
    'limit',
    openapi.IN_QUERY,
    description="Number of records per page",
    type=openapi.TYPE_INTEGER
)

@swagger_auto_schema(
    manual_parameters=[page_param, limit_param]
)
```

---

# 5️⃣ Example Request / Response

Professional API docs এ example দেওয়া হয়।

```python
@swagger_auto_schema(
    request_body=openapi.Schema(
        type=openapi.TYPE_OBJECT,
        properties={
            'email': openapi.Schema(type=openapi.TYPE_STRING),
            'password': openapi.Schema(type=openapi.TYPE_STRING),
        },
        example={
            "email": "admin@example.com",
            "password": "123456"
        }
    )
)
```

---

# 6️⃣ Error Response Documentation

Industry API docs এ error response সবসময় define করা হয়।

Example:

```
200 Success
400 Bad Request
401 Unauthorized
404 Not Found
500 Server Error
```

Example code:

```python
responses={
    200: CameraSerializer,
    401: "Unauthorized",
    404: "Camera not found"
}
```

---

# 7️⃣ Authentication Documentation

JWT authentication Swagger এ add করা হয়।

Example:

```python
SWAGGER_SETTINGS = {
    'SECURITY_DEFINITIONS': {
        'Bearer': {
            'type': 'apiKey',
            'name': 'Authorization',
            'in': 'header',
        }
    }
}
```

Swagger UI তে:

```
Authorize 🔒
```

button দেখাবে।

---

# 8️⃣ Versioned API Documentation

Professional projects এ versioned API থাকে।

Example:

```
/api/v1/cameras
/api/v2/cameras
```

Swagger:

```python
default_version='v1'
```

---

# 9️⃣ Clean View Documentation Pattern

Industry DRF view pattern:

```python
class CameraListView(APIView):

    @swagger_auto_schema(
        operation_summary="List Cameras",
        operation_description="Retrieve all registered CCTV cameras",
        responses={200: CameraSerializer(many=True)},
        tags=["Cameras"]
    )
    def get(self, request):
        pass
```

Swagger UI:

```
Cameras
   GET /api/v1/cameras
```

---

# 🔟 Real Industry Swagger Example

Example structure:

```
Authentication
   POST /auth/login
   POST /auth/logout

Users
   GET /users
   GET /users/{id}

Cameras
   GET /cameras
   POST /cameras
   DELETE /cameras/{id}

Alerts
   GET /alerts
   POST /alerts
```

---

# 1️⃣1️⃣ AI CCTV Project Swagger Structure (Best Practice)

তোমার project এর জন্য ideal structure হতে পারে:

```
Authentication
   POST /api/v1/auth/login
   POST /api/v1/auth/register

Cameras
   GET /api/v1/cameras
   POST /api/v1/cameras
   GET /api/v1/cameras/{id}

Streams
   GET /api/v1/streams

Detection
   POST /api/v1/detection/start
   POST /api/v1/detection/stop

Alerts
   GET /api/v1/alerts
```

---

# 🚀 Pro Tip (Industry)

Big companies API docs এ ব্যবহার করে:

- clear **operation_summary**
    
- detailed **operation_description**
    
- **examples**
    
- **request/response schema**
    
- **error responses**
    
- **tags**
    

এগুলো থাকলে API documentation **frontend developer easily understand করতে পারে**।

---

Django REST Framework এ **Serializer field-এ `help_text` ব্যবহার করা হয় API documentation এবং form hint দেখানোর জন্য**। যখন তুমি **drf-yasg** বা **Swagger UI** ব্যবহার করো, তখন এই `help_text` automatically Swagger documentation-এ show হয়।

এখন step-by-step বুঝি।

---

# 1️⃣ help_text কি?

`help_text` হলো **field এর description**।

এটা বলে দেয়:

* এই field কি
* কী ধরনের value দিতে হবে

---

# 2️⃣ Basic Example

```python
from rest_framework import serializers

class LoginSerializer(serializers.Serializer):
    email = serializers.EmailField(
        help_text="Enter your registered email address"
    )

    password = serializers.CharField(
        help_text="Enter your account password"
    )
```

এখানে

```
email → Enter your registered email address
password → Enter your account password
```

এই description API documentation-এ দেখাবে।

---

# 3️⃣ Swagger UI তে কী দেখাবে

Swagger UI তে field এর নিচে description show করবে।

Example:

```
email (string)
Enter your registered email address

password (string)
Enter your account password
```

---

# 4️⃣ কেন help_text ব্যবহার করি

### 1️⃣ API documentation clear করার জন্য

Frontend developer বুঝতে পারে।

Example:

```
camera_id → camera er unique id
rtsp_url → camera stream url
```

---

### 2️⃣ Auto documentation

Swagger automatically read করে।

তাই extra documentation লিখতে হয় না।

---

### 3️⃣ Django admin form hint

Django admin এও দেখাতে পারে।

Example:

```
Enter camera RTSP stream URL
```

---

# 5️⃣ Practical Example (AI CCTV project)

তোমার project এ serializer হতে পারে।

```python
class CameraSerializer(serializers.Serializer):

    name = serializers.CharField(
        help_text="Name of the CCTV camera"
    )

    location = serializers.CharField(
        help_text="Physical location of the camera"
    )

    rtsp_url = serializers.CharField(
        help_text="RTSP stream URL of the camera"
    )
```

Swagger UI তে দেখাবে:

```
name
Name of the CCTV camera

location
Physical location of the camera

rtsp_url
RTSP stream URL of the camera
```

---

# 6️⃣ help_text vs label

| Field     | কাজ               |
| --------- | ----------------- |
| label     | field title       |
| help_text | field explanation |

Example

```python
email = serializers.EmailField(
    label="User Email",
    help_text="Enter your registered email address"
)
```

Result:

```
User Email
Enter your registered email address
```

---

# 7️⃣ help_text vs error_messages

| Option         | কাজ                      |
| -------------- | ------------------------ |
| help_text      | field explanation        |
| error_messages | validation error message |

Example:

```python
password = serializers.CharField(
    help_text="Password must be at least 8 characters",
    error_messages={
        "blank": "Password cannot be empty"
    }
)
```

---

# 8️⃣ Industry Practice

Production backend এ সাধারণত

* `help_text`
* `label`
* `example`

সব ব্যবহার করা হয়।

Example:

```python
email = serializers.EmailField(
    label="User Email",
    help_text="Enter registered email address",
)
```

---

✅ **Summary**

`help_text` ব্যবহার করি কারণ:

1️⃣ API documentation clear হয়
2️⃣ Swagger UI তে description দেখায়
3️⃣ frontend developer বুঝতে পারে
4️⃣ extra documentation লিখতে হয় না

---
