তোমার current situation (DRF + JWT already done, এখন social login add করছো) অনুযায়ী আমি **production-friendly কিন্তু easy approach** দিবো:

**Follow করবে:**

✅ `django-allauth`  
✅ `dj-rest-auth`  
✅ `simplejwt`  
✅ `.env` থেকে Google credentials load করবে

এটা real project এ use করা হয়।

---

## Step 1: Install

```bash
pip install django-allauth
pip install dj-rest-auth
pip install djangorestframework-simplejwt
pip install django-environ
```

---

## Step 2: settings.py

### Installed apps

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "django.contrib.sites",

    # DRF
    "rest_framework",

    # auth
    "dj_rest_auth",
    "dj_rest_auth.registration",

    # allauth
    "allauth",
    "allauth.account",
    "allauth.socialaccount",
    "allauth.socialaccount.providers.google",
]
```

---

## Step 3: SITE_ID

```python
SITE_ID = 1
```

---

## Step 4: Authentication backend

settings.py

```python
AUTHENTICATION_BACKENDS = [

    "django.contrib.auth.backends.ModelBackend",

    "allauth.account.auth_backends.AuthenticationBackend",
]
```

---

## Step 5: JWT config

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": [

        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ]

}
```

---

## Step 6: .env file

project root:

```
.env
```

add:

```env
GOOGLE_CLIENT_ID=xxxx.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=xxxx
```

---

## Step 7: settings.py env load

```python
import os


SOCIALACCOUNT_PROVIDERS = {

    "google": {

        "APP": {

            "client_id": os.getenv(
                "GOOGLE_CLIENT_ID"
            ),

            "secret": os.getenv(
                "GOOGLE_CLIENT_SECRET"
            ),

            "key": "",
        },

        "SCOPE": [
            "profile",
            "email",
        ],

        "AUTH_PARAMS": {
            "access_type": "online",
        },
    }
}
```

---

## Step 8: migrate

```bash
python manage.py migrate
```

---

## Step 9: Google OAuth setup

Google Cloud Console:

Create:

```
OAuth Client ID
```

Type:

```
Web Application
```

Redirect URL:

```
http://localhost:8000/accounts/google/login/callback/
```

copy:

```
Client ID
Client Secret
```

put `.env`

---

## Step 10: create social login API

app:

```
accounts
```

views.py

```python
from dj_rest_auth.registration.views import SocialLoginView
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter


class GoogleLoginView(SocialLoginView):

    adapter_class = GoogleOAuth2Adapter
```

---

## Step 11: urls.py

accounts/urls.py

```python
from django.urls import path
from .views import GoogleLoginView


urlpatterns = [

    path(
        "google/",
        GoogleLoginView.as_view()
    ),

]
```

main urls.py

```python
urlpatterns = [

    path(
        "api/auth/",
        include("accounts.urls")
    ),

]
```

---

## Step 12: Test

POST:

```
http://127.0.0.1:8000/api/auth/google/
```

body:

```json
{
    "access_token":"GOOGLE_ACCESS_TOKEN"
}
```

Response:

```json
{
    "access":"jwt_access_token",
    "refresh":"jwt_refresh_token"
}
```

---

## Final folder:

```
project
│
├── core
│    └── settings.py
│
├── accounts
│    ├── views.py
│    ├── urls.py
│
├── .env
└── manage.py
```

এটাই follow করো। তোমার existing JWT auth এর সাথে conflict হবে না।

--------
Google এর মতোই GitHub আর Facebook integrate হবে। `django-allauth + dj-rest-auth` use করলে শুধু **provider change** হবে।

তুমি যে setup করেছো সেটার উপরেই add করবে।

---

## 1. Install providers

`django-allauth` এর সাথে provider আসে, শুধু apps এ add করতে হবে।

### settings.py

```python
INSTALLED_APPS = [

    "allauth",
    "allauth.account",
    "allauth.socialaccount",

    "allauth.socialaccount.providers.google",
    "allauth.socialaccount.providers.github",
    "allauth.socialaccount.providers.facebook",

]
```

---

## 2. .env এ credentials রাখো

```env
GOOGLE_CLIENT_ID=xxxx
GOOGLE_CLIENT_SECRET=xxxx


GITHUB_CLIENT_ID=xxxx
GITHUB_CLIENT_SECRET=xxxx


FACEBOOK_CLIENT_ID=xxxx
FACEBOOK_CLIENT_SECRET=xxxx
```

---

## 3. settings.py এ providers add

```python
import os


SOCIALACCOUNT_PROVIDERS = {


    "google": {

        "APP": {
            "client_id": os.getenv("GOOGLE_CLIENT_ID"),
            "secret": os.getenv("GOOGLE_CLIENT_SECRET"),
            "key": "",
        }
    },


    "github": {

        "APP": {
            "client_id": os.getenv("GITHUB_CLIENT_ID"),
            "secret": os.getenv("GITHUB_CLIENT_SECRET"),
            "key": "",
        }
    },


    "facebook": {

        "APP": {
            "client_id": os.getenv("FACEBOOK_CLIENT_ID"),
            "secret": os.getenv("FACEBOOK_CLIENT_SECRET"),
            "key": "",
        }
    },

}
```

---

# GitHub Setup

GitHub এ:

```
Settings
  ↓
Developer settings
  ↓
OAuth Apps
  ↓
New OAuth App
```

Fill:

Application name:

```
My DRF App
```

Homepage:

```
http://localhost:3000
```

Callback:

```
http://localhost:8000/accounts/github/login/callback/
```

Create করলে পাবে:

```
Client ID
Client Secret
```

.env এ বসাও।

---

# Facebook Setup

Facebook Developer:

Create App

তারপর:

```
Products
 ↓
Facebook Login
 ↓
Settings
```

Valid OAuth Redirect URI:

```
http://localhost:8000/accounts/facebook/login/callback/
```

পাবে:

```
App ID
App Secret
```

.env এ বসাও।

---

# 4. Views

accounts/views.py

```python
from dj_rest_auth.registration.views import SocialLoginView

from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter
from allauth.socialaccount.providers.github.views import GitHubOAuth2Adapter
from allauth.socialaccount.providers.facebook.views import FacebookOAuth2Adapter



class GoogleLogin(SocialLoginView):
    adapter_class = GoogleOAuth2Adapter



class GithubLogin(SocialLoginView):
    adapter_class = GitHubOAuth2Adapter



class FacebookLogin(SocialLoginView):
    adapter_class = FacebookOAuth2Adapter
```

---

# 5. URLs

accounts/urls.py

```python
urlpatterns = [


path(
    "google/",
    GoogleLogin.as_view()
),


path(
    "github/",
    GithubLogin.as_view()
),


path(
    "facebook/",
    FacebookLogin.as_view()
),


]
```

---

এখন API:

### Google

```
POST

/api/auth/google/
```

### Github

```
POST

/api/auth/github/
```

### Facebook

```
POST

/api/auth/facebook/
```

Body:

```json
{
 "access_token":"provider_token"
}
```

Response:

```json
{
 "access":"jwt...",
 "refresh":"jwt..."
}
```

---

তোমার architecture হবে:

```
Frontend
   |
   |-- Google token
   |-- Github token
   |-- Facebook token
        |
        v
DRF
        |
        v
django-allauth
        |
        v
User create/login
        |
        v
SimpleJWT
```

একই flow, শুধু provider আলাদা।



তোমার backend এখন `dj-rest-auth + allauth + JWT` দিয়ে ready। React থেকে implementation হবে:

Flow:

```
React
 |
 | Google/Github/Facebook OAuth
 |
Provider token নেয়
 |
DRF API তে পাঠায়
 |
Backend JWT return করে
 |
localStorage/cookie এ রাখো
```

React এ easiest way: **@react-oauth/google** (Google), **react-github-login / custom OAuth** (GitHub), Facebook এর জন্য **react-facebook-login**।

---

## 1. Install

```bash
npm install @react-oauth/google axios jwt-decode
```

---

# Google Login

## main.jsx

Google provider wrap করো:

```jsx
import { GoogleOAuthProvider } from "@react-oauth/google";


<GoogleOAuthProvider clientId="GOOGLE_CLIENT_ID">

    <App />

</GoogleOAuthProvider>
```

---

## GoogleButton.jsx

```jsx
import { GoogleLogin } from "@react-oauth/google";
import axios from "axios";


const GoogleButton = () => {


const googleLogin = async (credentialResponse)=>{


    const token = credentialResponse.credential;


    const res = await axios.post(
        "http://localhost:8000/api/auth/google/",
        {
            access_token: token
        }
    );


    console.log(res.data);


    localStorage.setItem(
        "access",
        res.data.access
    );


    localStorage.setItem(
        "refresh",
        res.data.refresh
    );

}



return (

<GoogleLogin

onSuccess={googleLogin}

onError={()=>console.log("failed")}

/>

)


}

export default GoogleButton;
```

---

# Github Login

Install:

```bash
npm install react-github-login
```

Component:

```jsx
import GitHubLogin from "react-github-login";
import axios from "axios";


function GithubButton(){


const success = async(response)=>{


const res = await axios.post(

"http://localhost:8000/api/auth/github/",

{
 access_token: response.code
}

)


console.log(res.data)

}



return (

<GitHubLogin

clientId="GITHUB_CLIENT_ID"

onSuccess={success}

onFailure={(err)=>console.log(err)}

/>

)


}


export default GithubButton;
```

---

# Facebook Login

Install:

```bash
npm install react-facebook-login
```

Component:

```jsx
import FacebookLogin from "react-facebook-login";
import axios from "axios";


function FacebookButton(){


const responseFacebook = async(response)=>{


const res = await axios.post(

"http://localhost:8000/api/auth/facebook/",

{
access_token: response.accessToken
}

)


console.log(res.data)

}



return (

<FacebookLogin

appId="FACEBOOK_APP_ID"

callback={responseFacebook}

/>

)

}


export default FacebookButton;
```

---

## API response

Backend দিবে:

```json
{
 "access":"eyJhbGc...",
 "refresh":"eyJhbGc..."
}
```

Save:

```javascript
localStorage.setItem(
"access",
data.access
)
```

---

## Axios interceptor (recommended)

api.js

```javascript
import axios from "axios";


const api = axios.create({

baseURL:"http://localhost:8000/api"

})


api.interceptors.request.use(config=>{


const token = localStorage.getItem("access")


if(token){

config.headers.Authorization =
`Bearer ${token}`

}


return config;


})


export default api;
```

---

তাহলে protected API call:

```javascript
api.get("/profile/")
```

automatically JWT পাঠাবে।

---

Production এ access token localStorage না রেখে **httpOnly cookie** use করা better, কিন্তু learning/project এর জন্য এই flow ঠিক আছে।

-----
