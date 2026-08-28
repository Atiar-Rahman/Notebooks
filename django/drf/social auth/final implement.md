Your backend:

```python
from dj_rest_auth.registration.views import SocialLoginView
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter


class GoogleLoginView(SocialLoginView):
    adapter_class = GoogleOAuth2Adapter
```

uses `GoogleOAuth2Adapter`, which by default expects a **Google OAuth access token**.

So your current React code:

```javascript
const token = credentialResponse.credential;

{
    access_token: token
}
```

is **not correct** because:

```javascript
credentialResponse.credential
```

from:

```javascript
<GoogleLogin />
```

is an **ID token**, not an access token.

---

## Solution 1 (Recommended): Use `useGoogleLogin` with access token

Change your React implementation:

```javascript
import { useGoogleLogin } from "@react-oauth/google";
import axios from "axios";

const GoogleButton = () => {

    const googleLogin = useGoogleLogin({
        onSuccess: async (tokenResponse) => {

            const res = await axios.post(
                "http://localhost:8000/api/auth/google/",
                {
                    access_token: tokenResponse.access_token
                }
            );

            console.log(res.data);

            localStorage.setItem("access", res.data.access);
            localStorage.setItem("refresh", res.data.refresh);
        },

        onError: () => {
            console.log("Google Login Failed");
        }
    });


    return (
        <button onClick={googleLogin}>
            Login with Google
        </button>
    );
};

export default GoogleButton;
```

Now the request body becomes:

```json
{
    "access_token": "ya29.xxxxxxxxx"
}
```

which matches `GoogleOAuth2Adapter`.

---

## Solution 2: Keep `<GoogleLogin />`

If you want to keep:

```javascript
import { GoogleLogin } from "@react-oauth/google";
```

then your backend needs to handle `id_token`.

Your request would be:

```javascript
{
    "id_token": credentialResponse.credential
}
```

but `GoogleOAuth2Adapter` alone is not designed for that flow.

---

### Your current setup should be:

React:

```
useGoogleLogin()
        |
        ↓
access_token
        |
        ↓
POST /api/auth/google/
        |
        ↓
GoogleOAuth2Adapter
        |
        ↓
Django user + JWT tokens
```

So for your existing Django code, switch from `GoogleLogin` to `useGoogleLogin`.

না, **দুটো একসাথে দেওয়ার দরকার নেই**। একটি দিলেই হবে — কিন্তু কোনটা দেবেন সেটা আপনার backend flow-এর উপর নির্ভর করে।

আপনার Django code:

```python
from dj_rest_auth.registration.views import SocialLoginView
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter


class GoogleLoginView(SocialLoginView):
    adapter_class = GoogleOAuth2Adapter
```

এখানে `GoogleOAuth2Adapter` ব্যবহার করছেন, তাই সাধারণত **শুধু `access_token` দিতে হবে**।

Request body:

```json
{
  "access_token": "your_google_access_token"
}
```

---

`id_token` ব্যবহার করতে চাইলে backend-এ আলাদা configuration/adapter দরকার হতে পারে। আপনার বর্তমান setup-এর জন্য:

✅ ব্যবহার করুন:

```json
{
  "access_token": "..."
}
```

❌ এভাবে দেওয়ার প্রয়োজন নেই:

```json
{
  "access_token": "...",
  "id_token": "..."
}
```

---

আপনার React code-এ যদি:

```javascript
<GoogleLogin />
```

ব্যবহার করেন, সেটা `id_token` দেয়।

আর যদি আপনার Django backend অনুযায়ী `access_token` পাঠাতে চান, তাহলে:

```javascript
useGoogleLogin({
    onSuccess: (tokenResponse) => {
        console.log(tokenResponse.access_token);
    }
})
```

ব্যবহার করুন।


এই error এর মানে হলো আপনার Next.js project-এ **`@react-oauth/google` package install করা নেই** অথবা dependency resolve করতে পারছে না।

Error:

```text
Module not found: Can't resolve '@react-oauth/google'
```

মানে এই import:

```javascript
import { useGoogleLogin } from "@react-oauth/google";
```

এর package খুঁজে পাচ্ছে না।

---

## Step 1: Package install করুন

আপনার Next.js project folder-এ গিয়ে চালান:

```bash
npm install @react-oauth/google
```

অথবা yarn ব্যবহার করলে:

```bash
yarn add @react-oauth/google
```

তারপর server restart করুন:

```bash
npm run dev
```

---

## Step 2: Next.js Client Component করুন

আপনি `app/page.js` ব্যবহার করছেন, তাই `GoogleButton.jsx`-এ উপরে যোগ করুন:

```javascript
"use client";

import { useGoogleLogin } from "@react-oauth/google";
import axios from "axios";
```

কারণ `useGoogleLogin` একটি React hook, এটি server component-এ চলবে না।

---

## Step 3: GoogleOAuthProvider যোগ করুন

`app/layout.js` এ:

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function RootLayout({ children }) {

    return (
        <html lang="en">
            <body>
                <GoogleOAuthProvider clientId="YOUR_GOOGLE_CLIENT_ID">
                    {children}
                </GoogleOAuthProvider>
            </body>
        </html>
    );
}
```

`YOUR_GOOGLE_CLIENT_ID` এর জায়গায় Google Cloud Console থেকে পাওয়া Client ID দিন।

Example:

```javascript
clientId="1234567890-abc.apps.googleusercontent.com"
```

---

## Step 4: GoogleButton.jsx

```javascript
"use client";

import { useGoogleLogin } from "@react-oauth/google";
import axios from "axios";

const GoogleButton = () => {

    const googleLogin = useGoogleLogin({
        onSuccess: async (tokenResponse) => {

            const res = await axios.post(
                "http://localhost:8000/api/auth/google/",
                {
                    access_token: tokenResponse.access_token,
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
        },

        onError: () => {
            console.log("Google Login Failed");
        },
    });


    return (
        <button onClick={googleLogin}>
            Login with Google
        </button>
    );
};

export default GoogleButton;
```

---

যদি package install করার পরও একই error থাকে, তাহলে দেখুন:

```bash
npm list @react-oauth/google
```

এটা package installed কিনা দেখাবে।


এই error এর মানে হলো:

```
Google OAuth components must be used within GoogleOAuthProvider
```

আপনি `useGoogleLogin()` ব্যবহার করছেন, কিন্তু আপনার component tree-এর উপরে `GoogleOAuthProvider` নেই।

`useGoogleLogin` কাজ করার জন্য পুরো app-কে provider দিয়ে wrap করতে হবে।

---

## Next.js App Router হলে (`app/` folder)

আপনার `app/layout.js` এ করুন:

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <GoogleOAuthProvider clientId="YOUR_GOOGLE_CLIENT_ID">
          {children}
        </GoogleOAuthProvider>
      </body>
    </html>
  );
}
```

এখানে:

```javascript
id="4h2t5k"
YOUR_GOOGLE_CLIENT_ID
```

এর জায়গায় Google Cloud Console থেকে পাওয়া Client ID বসাবেন।

Example:

```javascript
id="h6b8e9"
123456789012-abcd1234.apps.googleusercontent.com
```

---

## Better approach: আলাদা Provider component বানান

`components/GoogleProvider.jsx`

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function GoogleProvider({ children }) {
    return (
        <GoogleOAuthProvider clientId="YOUR_GOOGLE_CLIENT_ID">
            {children}
        </GoogleOAuthProvider>
    );
}
```

তারপর `app/layout.js`:

```javascript
import GoogleProvider from "@/components/GoogleProvider";

export default function RootLayout({ children }) {
    return (
        <html lang="en">
            <body>
                <GoogleProvider>
                    {children}
                </GoogleProvider>
            </body>
        </html>
    );
}
```

---

## তারপর আপনার `GoogleButton.jsx` ঠিক থাকবে:

```javascript
"use client";

import { useGoogleLogin } from "@react-oauth/google";

const GoogleButton = () => {

    const googleLogin = useGoogleLogin({
        onSuccess: (tokenResponse) => {
            console.log(tokenResponse.access_token);
        },
    });

    return (
        <button onClick={googleLogin}>
            Login with Google
        </button>
    );
};

export default GoogleButton;
```

---

### মনে রাখবেন:

* `GoogleOAuthProvider` → একবার পুরো app-এর উপরে দিতে হয়।
* `useGoogleLogin` → শুধু client component-এ ব্যবহার করা যায় (`"use client";` লাগবে)।
* `clientId` অবশ্যই Google Cloud Console-এর OAuth Client ID হতে হবে।


আপনার `GoogleButton.jsx` code **ঠিক আছে**। এখন যে error পাচ্ছেন:

```
Google OAuth components must be used within GoogleOAuthProvider
```

এটা এই component-এর সমস্যা না। সমস্যা হলো আপনার app-এ `GoogleOAuthProvider` wrap করা হয়নি।

আপনার Next.js `app` router হলে এভাবে করুন।

### 1. `app/layout.js` ঠিক করুন

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <GoogleOAuthProvider clientId="YOUR_GOOGLE_CLIENT_ID">
          {children}
        </GoogleOAuthProvider>
      </body>
    </html>
  );
}
```

এখানে:

```text
YOUR_GOOGLE_CLIENT_ID
```

এর জায়গায় Google Cloud Console-এর OAuth Client ID বসাবেন।

Example:

```text
123456789012-abcxyz.apps.googleusercontent.com
```

---

### 2. যদি `layout.js`-এ `"use client"` দিতে না চান (recommended)

একটা আলাদা provider বানান:

`components/GoogleProvider.jsx`

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function GoogleProvider({ children }) {
  return (
    <GoogleOAuthProvider clientId="YOUR_GOOGLE_CLIENT_ID">
      {children}
    </GoogleOAuthProvider>
  );
}
```

তারপর `app/layout.js`:

```javascript
import GoogleProvider from "@/components/GoogleProvider";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <GoogleProvider>
          {children}
        </GoogleProvider>
      </body>
    </html>
  );
}
```

---

### 3. আপনার `GoogleButton.jsx`

এটা যেমন আছে তেমনই থাকবে:

```javascript
"use client";

import { useGoogleLogin } from "@react-oauth/google";
import axios from "axios";

const GoogleButton = () => {
  const googleLogin = useGoogleLogin({
    onSuccess: async (tokenResponse) => {
      const res = await axios.post(
        "http://localhost:8000/api/auth/google/",
        {
          access_token: tokenResponse.access_token,
        }
      );

      console.log(res.data);

      localStorage.setItem("access", res.data.access);
      localStorage.setItem("refresh", res.data.refresh);
    },

    onError: () => {
      console.log("Google Login Failed");
    },
  });

  return (
    <button onClick={googleLogin}>
      Login with Google
    </button>
  );
};

export default GoogleButton;
```

---

Provider যোগ করার পরে **Next.js server বন্ধ করে আবার চালান**:

```bash
npm run dev
```

তারপর Google button কাজ করবে।


আপনার Google login frontend পর্যন্ত ঠিকভাবে কাজ করছে। এখন সমস্যা Google না, **Django backend connection**।

মূল error:

```
POST http://localhost:8000/api/auth/google/ net::ERR_CONNECTION_REFUSED
```

এর মানে:

> React `localhost:8000` এ request পাঠাচ্ছে, কিন্তু সেখানে Django server চলছে না বা reachable না।

---

## 1. Django server চলছে কিনা দেখুন

Backend folder-এ গিয়ে চালান:

```bash
python manage.py runserver
```

সঠিক হলে দেখাবে:

```
Starting development server at http://127.0.0.1:8000/
```

---

## 2. URL মিলিয়ে নিন

আপনার React:

```javascript
axios.post(
  "http://localhost:8000/api/auth/google/",
  {
    access_token: tokenResponse.access_token,
  }
)
```

Django `urls.py` এ এমন কিছু থাকতে হবে:

### project urls.py

```python
path("api/", include("apps.api.urls")),
```

### apps/api/urls.py

```python
from django.urls import path
from apps.users.views import GoogleLoginView

urlpatterns = [
    path(
        "auth/google/",
        GoogleLoginView.as_view(),
        name="google-login"
    ),
]
```

তাহলে final URL হবে:

```
http://localhost:8000/api/auth/google/
```

---

## 3. CORS issue আসতে পারে

যদি frontend:

```
http://localhost:3000
```

এ চলে, Django-তে install করুন:

```bash
pip install django-cors-headers
```

`settings.py`:

```python
INSTALLED_APPS = [
    ...
    "corsheaders",
]
```

Middleware:

```python
MIDDLEWARE = [
    "corsheaders.middleware.CorsMiddleware",
    ...
]
```

তারপর:

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
]
```

---

## 4. `localhost` এর বদলে `127.0.0.1` try করুন

কখনো IPv6/localhost resolving সমস্যা হয়।

React:

```javascript
axios.post(
  "http://127.0.0.1:8000/api/auth/google/",
  {
    access_token: tokenResponse.access_token,
  }
)
```

---

## 5. আপনার Django console দেখুন

Google button চাপার পরে Django terminal-এ কিছু আসছে কিনা দেখুন।

যদি **কিছুই না আসে** → Django server চলছে না / URL ভুল।

যদি আসে:

```
POST /api/auth/google/
```

তারপর error দেয় → backend configuration issue।

এখন প্রথমে নিশ্চিত করুন:

1. `python manage.py runserver` চলছে কিনা
2. Browser থেকে খুললে `http://localhost:8000` কাজ করে কিনা।
আপনার frontend এখন ঠিকভাবে request পাঠাচ্ছে। এখন Django backend-এর configuration সমস্যা।

মূল error:

```text
django.core.exceptions.ImproperlyConfigured: unknown provider: google
```

এর মানে:

> Django Allauth Google provider খুঁজে পাচ্ছে না।

আপনার `settings.py`-তে Google provider install করা আছে বলে মনে হচ্ছে:

```python
"allauth.socialaccount.providers.google",
```

কিন্তু আরো কিছু configuration লাগবে।

---

## 1. `SITE_ID` ঠিক আছে কিনা দেখুন

`settings.py`:

```python
SITE_ID = 1
```

থাকতে হবে।

---

## 2. `SOCIALACCOUNT_PROVIDERS` যোগ করুন

`settings.py` এ যোগ করুন:

```python
SOCIALACCOUNT_PROVIDERS = {
    "google": {
        "APP": {
            "client_id": "YOUR_GOOGLE_CLIENT_ID",
            "secret": "YOUR_GOOGLE_CLIENT_SECRET",
            "key": "",
        }
    }
}
```

এখানে Google Cloud Console থেকে:

* Client ID
* Client Secret

দিতে হবে।

---

## 3. Database-এ SocialApp তৈরি করুন

Django shell চালান:

```bash
python manage.py shell
```

তারপর:

```python
from allauth.socialaccount.models import SocialApp
from django.contrib.sites.models import Site

app = SocialApp.objects.create(
    provider="google",
    name="Google",
    client_id="YOUR_GOOGLE_CLIENT_ID",
    secret="YOUR_GOOGLE_CLIENT_SECRET",
)

site = Site.objects.get(id=1)

app.sites.add(site)
```

তারপর:

```python
exit()
```

---

## 4. Migration চালান

```bash
python manage.py migrate
```

---

## 5. Installed apps check করুন

আপনার `INSTALLED_APPS` এ order এমন হওয়া ভালো:

```python
INSTALLED_APPS = [

    "django.contrib.sites",

    "allauth",
    "allauth.account",
    "allauth.socialaccount",
    "allauth.socialaccount.providers.google",

    "rest_framework",

    "dj_rest_auth",
    "dj_rest_auth.registration",

    ...
]
```

---

## 6. Request এখন এমন থাকবে

আপনার React:

```javascript
{
    access_token: tokenResponse.access_token
}
```

ঠিক আছে।

---

## কেন error হচ্ছিল?

Flow:

```
React
 |
 | access_token
 ↓
dj-rest-auth
 |
 ↓
GoogleOAuth2Adapter
 |
 ↓
allauth খুঁজছে "google" provider
 |
 ❌ provider পাওয়া যাচ্ছে না
```

Provider install/configure করার পরে:

```
React
 |
 ↓
GoogleOAuth2Adapter
 |
 ↓
Google provider
 |
 ↓
User create/login
 |
 ↓
JWT access + refresh
```

---

সবচেয়ে আগে check করুন:

```bash
python manage.py shell
```

তারপর:

```python
from allauth.socialaccount.providers import registry
registry.get_class("google")
```

যদি `GoogleProvider` দেখায় → provider ঠিক আছে।
যদি error দেয় → `INSTALLED_APPS` বা migration সমস্যা আছে।
হ্যাঁ, Next.js-এ **environment variable (`.env`) থেকে Google Client ID load করা ভালো practice**।

### 1. Root project-এ `.env.local` তৈরি করুন

যেখানে `package.json` আছে সেখানে:

```env
NEXT_PUBLIC_GOOGLE_CLIENT_ID=1041201164554-708j5cgn8dk0mfls74ns31sj4rpqfp0a.apps.googleusercontent.com
```

> Next.js client component-এ ব্যবহার করতে হলে variable name-এর শুরুতে `NEXT_PUBLIC_` থাকতে হবে।

---

### 2. Provider component update করুন

`components/GoogleProvider.jsx`

```javascript
"use client";

import { GoogleOAuthProvider } from "@react-oauth/google";

export default function GoogleProvider({ children }) {
  return (
    <GoogleOAuthProvider
      clientId={process.env.NEXT_PUBLIC_GOOGLE_CLIENT_ID}
    >
      {children}
    </GoogleOAuthProvider>
  );
}
```

---

### 3. Next.js server restart করুন

Environment variable নতুন করে load করার জন্য:

```bash
npm run dev
```

বন্ধ করে আবার চালান।

---

### 4. Optional: Check করতে পারেন

Temporary:

```javascript
console.log(process.env.NEXT_PUBLIC_GOOGLE_CLIENT_ID);
```

Browser console-এ Client ID দেখাবে।

---

### Security note

Google **Client ID secret না**। এটা frontend-এ থাকা স্বাভাবিক।

কিন্তু:

❌ `.env.local` এ রাখবেন না:

```env
GOOGLE_CLIENT_SECRET=xxxxx
```

Frontend code-এ কখনো secret expose করবেন না।

আপনার Django backend-এর জন্য:

```env
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
```

আলাদা backend `.env` এ রাখবেন।
হ্যাঁ, frontend-এ Google login চালানোর জন্য **Client ID লাগবেই**। কারণ Google browser-এর ভিতরে OAuth flow শুরু করার সময় Client ID দিয়ে জানতে পারে কোন Google OAuth application ব্যবহার হচ্ছে।

তবে frontend-এ **শুধু Client ID** যাবে, **Client Secret যাবে না**।

আপনার ক্ষেত্রে:

### Frontend `.env.local`

```env
NEXT_PUBLIC_GOOGLE_CLIENT_ID=1041201164554-708j5cgn8dk0mfls74ns31sj4rpqfp0a.apps.googleusercontent.com
```

তারপর:

```jsx
<GoogleOAuthProvider
  clientId={process.env.NEXT_PUBLIC_GOOGLE_CLIENT_ID}
>
  {children}
</GoogleOAuthProvider>
```

এটাই সঠিক।

---

### Backend `.env`

Django-তে আলাদা রাখবেন:

```env
GOOGLE_CLIENT_ID=1041201164554-708j5cgn8dk0mfls74ns31sj4rpqfp0a.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_secret_here
```

কারণ Django ব্যবহার করবে:

* access token verify করতে
* Google API call করতে
* SocialApp configuration করতে

---

### মনে রাখবেন

Google OAuth এ:

```
Client ID      → Public → Frontend এ যাবে ✅
Client Secret  → Private → শুধু Backend এ থাকবে ✅
```

Client ID প্রকাশ হয়ে গেলেও সমস্যা নেই। নিরাপত্তা আসে মূলত:

* Authorized JavaScript origins
* Authorized redirect URIs
* Backend token verification

এসব দিয়ে।
