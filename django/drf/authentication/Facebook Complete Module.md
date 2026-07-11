
অবশ্যই করা যাবে। তবে **একটা message-এ "Facebook complete" দেওয়া বাস্তবসম্মত না।**

আপনি Google শিখেছেন **১০+ commit**-এ।
GitHub শিখেছেন **provider + endpoint + callback + service integration** করে।

Facebook-ও একইভাবে **production quality** করতে হবে।

### Facebook Complete Module

আমি এটাকে **১২টি commit**-এ শেখাব:

1. Facebook Developer Console & App Setup
2. Django Settings & Environment Configuration
3. Facebook OAuth Provider (`facebook.py`)
4. Provider Factory Integration
5. Facebook Login Endpoint
6. Facebook Callback Endpoint
7. OAuth Service Integration
8. Facebook Account Linking (`OAuthAccount`)
9. Error Handling & Exceptions
10. Generic OAuth Refactor (`/auth/<provider>/...`)
11. React Integration
12. Testing + Postman + Production Deployment

এভাবে করলে আপনি শুধু Facebook না, **যেকোনো OAuth provider** (Microsoft, Apple, LinkedIn, Discord) নিজে implement করতে পারবেন।

---

### আমি যেভাবে শেখাব

প্রতিটি commit-এ থাকবে:

* Folder structure
* Complete code
* কোথায় file create করবেন
* কী পরিবর্তন করবেন
* কী test করবেন
* Git commit message

Google এবং GitHub-এর মতোই **copy-paste করে project-এ implement** করতে পারবেন।

---

## তাহলে আমরা শুরু করি:

### **Commit 1**

```bash
feat(facebook): setup facebook developer application
```

এখান থেকে শুরু করে শেষ commit পর্যন্ত পুরো Facebook OAuth implement করব।



---------

দারুণ। এখন থেকে Django code শুরু হবে।

---

# Commit 2

```bash
git checkout feature/facebook-oauth
```

```bash
git commit -m "feat(facebook): add facebook configuration"
```

---

# Goal

এই commit শেষে আপনার project Facebook OAuth-এর জন্য configuration ready হবে।

---

# Step 1 — `.env`

Add করুন:

```env
FACEBOOK_APP_ID=your_app_id

FACEBOOK_APP_SECRET=your_app_secret

FACEBOOK_REDIRECT_URI=http://localhost:8000/api/v1/auth/facebook/callback/
```

Example:

```env
FACEBOOK_APP_ID=123456789012345

FACEBOOK_APP_SECRET=8b5a3xxxxxxxxxxxxxxxxxx

FACEBOOK_REDIRECT_URI=http://localhost:8000/api/v1/auth/facebook/callback/
```

---

# Step 2 — `settings.py`

Google/GitHub-এর নিচে add করুন।

```python
FACEBOOK_APP_ID = env(
    "FACEBOOK_APP_ID"
)

FACEBOOK_APP_SECRET = env(
    "FACEBOOK_APP_SECRET"
)

FACEBOOK_REDIRECT_URI = env(
    "FACEBOOK_REDIRECT_URI"
)
```

---

# Step 3 — Create Constants (Recommended)

Create file:

```text
apps/authentication/constants.py
```

```python
GOOGLE = "google"

GITHUB = "github"

FACEBOOK = "facebook"
```

এখন থেকে string লিখবেন না।

Instead of

```python
provider = "facebook"
```

use

```python
from .constants import FACEBOOK

provider = FACEBOOK
```

---

# Step 4 — Verify Settings

Run shell

```bash
python manage.py shell
```

```python
from django.conf import settings

settings.FACEBOOK_APP_ID
```

Output

```text
'123456789012345'
```

---

```python
settings.FACEBOOK_APP_SECRET
```

Output

```text
'8b5a3xxxxxxxxxxxx'
```

---

```python
settings.FACEBOOK_REDIRECT_URI
```

Output

```text
'http://localhost:8000/api/v1/auth/facebook/callback/'
```

---

# Folder Structure

```
apps/

authentication/

├── constants.py     ⭐

├── providers/
│
├── services/
│
├── factory.py
│
├── views.py
│
└── urls.py
```

---

# Test

সবগুলো check করুন:

```python
from django.conf import settings

print(settings.FACEBOOK_APP_ID)

print(settings.FACEBOOK_APP_SECRET)

print(settings.FACEBOOK_REDIRECT_URI)
```

কোনো exception আসা যাবে না।

---

# Commit

```bash
git add .

git commit -m "feat(facebook): add facebook configuration"
```

---

## Commit 2 Complete ✅

পরবর্তী **Commit 3**-এ আমরা `FacebookOAuthProvider` implement করব, যেখানে থাকবে:

* `get_authorization_url()`
* `exchange_code()`
* `get_user_info()`
* `normalize_user()`

এবং Facebook provider-কে Google ও GitHub-এর মতো একই interface-এ আনা হবে।
দারুণ। এবার **Commit 3**-এ আমরা পুরো `FacebookOAuthProvider` তৈরি করব। লক্ষ্য হচ্ছে Google ও GitHub-এর মতো **একই interface** রাখা, যাতে `OAuthAuthenticationService`-এ কোনো পরিবর্তন না লাগে।

---

# Commit 3

```bash
git commit -m "feat(facebook): implement facebook oauth provider"
```

---

# Step 1: Create File

```
apps/
└── authentication/
    └── providers/
        └── facebook.py
```

---

# Step 2: Base Structure

```python
import httpx

from django.conf import settings


class FacebookOAuthProvider:

    AUTHORIZATION_URL = (
        "https://www.facebook.com/v23.0/dialog/oauth"
    )

    TOKEN_URL = (
        "https://graph.facebook.com/v23.0/oauth/access_token"
    )

    USER_INFO_URL = (
        "https://graph.facebook.com/me"
    )
```

---

# Step 3: Authorization URL

```python
def get_authorization_url(self):

    params = {

        "client_id":
        settings.FACEBOOK_APP_ID,

        "redirect_uri":
        settings.FACEBOOK_REDIRECT_URI,

        "scope":
        "email,public_profile",

        "response_type":
        "code"

    }

    return str(
        httpx.URL(
            self.AUTHORIZATION_URL,
            params=params
        )
    )
```

---

# Step 4: Exchange Code

> **Method signature Google/GitHub-এর মতোই রাখবেন।**

```python
def exchange_code(
    self,
    code,
    redirect_uri,
):

    response = httpx.get(

        self.TOKEN_URL,

        params={

            "client_id":
            settings.FACEBOOK_APP_ID,

            "client_secret":
            settings.FACEBOOK_APP_SECRET,

            "redirect_uri":
            redirect_uri,

            "code":
            code,

        }

    )

    response.raise_for_status()

    return response.json()
```

Facebook response:

```json
{
    "access_token":"EAAB...",
    "token_type":"bearer",
    "expires_in":5183944
}
```

---

# Step 5: Get User Information

```python
def get_user_info(
    self,
    access_token,
):

    response = httpx.get(

        self.USER_INFO_URL,

        params={

            "fields":
            "id,name,email,picture",

            "access_token":
            access_token,

        }

    )

    response.raise_for_status()

    return response.json()
```

Facebook response:

```json
{
  "id":"123456789",
  "name":"Md Atiar Rahman",
  "email":"atiar@gmail.com",
  "picture":{
      "data":{
          "url":"https://...."
      }
  }
}
```

---

# Step 6: Normalize User

Google, GitHub, Facebook—সব provider একই format return করবে।

```python
def normalize_user(
    self,
    user_data,
):

    return {

        "provider_user_id":
        user_data["id"],

        "email":
        user_data.get("email"),

        "full_name":
        user_data.get("name"),

        "profile_image":
        user_data.get(
            "picture",
            {}
        ).get(
            "data",
            {}
        ).get(
            "url"
        )

    }
```

---

# Final Provider Interface

এখন তিনটি provider-এর interface একই হওয়া উচিত।

```python
provider.get_authorization_url()

provider.exchange_code(
    code,
    redirect_uri
)

provider.get_user_info(
    access_token
)

provider.normalize_user(
    user_data
)
```

---

# Test

Shell:

```bash
python manage.py shell
```

```python
from apps.authentication.providers.facebook import (
    FacebookOAuthProvider
)

provider = FacebookOAuthProvider()

provider.get_authorization_url()
```

Expected:

```text
https://www.facebook.com/v23.0/dialog/oauth?client_id=...
```

---

# Folder Structure

```
authentication/

providers/

├── google.py

├── github.py

└── facebook.py   ✅
```

---

# Commit

```bash
git add .

git commit -m "feat(facebook): implement facebook oauth provider"
```

---

## Commit 3 Complete ✅

**Commit 4**-এ আমরা `factory.py` update করব, যাতে:

```python
get_oauth_provider("facebook")
```

এক লাইনে `FacebookOAuthProvider()` return করে। তারপর Facebook Login endpoint বানানো শুরু করব।


--------

দারুণ। এখন Facebook provider-কে আপনার existing architecture-এ plug-in করব।

---

# Commit 4

```bash
git commit -m "feat(facebook): register facebook provider in oauth factory"
```

---

# Goal

এখন থেকে

```python
get_oauth_provider("facebook")
```

call করলে

```python
FacebookOAuthProvider()
```

return করবে।

---

# Step 1 — Update `factory.py`

File

```text
apps/authentication/factory.py
```

---

Import add করুন

```python
from apps.authentication.providers.facebook import (
    FacebookOAuthProvider
)
```

---

আগে যদি এমন থাকে

```python
from apps.authentication.providers.google import (
    GoogleOAuthProvider
)

from apps.authentication.providers.github import (
    GithubOAuthProvider
)
```

তাহলে হবে

```python
from apps.authentication.providers.google import (
    GoogleOAuthProvider
)

from apps.authentication.providers.github import (
    GithubOAuthProvider
)

from apps.authentication.providers.facebook import (
    FacebookOAuthProvider
)
```

---

# Step 2 — Register Provider

আগে

```python
def get_oauth_provider(provider):

    if provider == "google":

        return GoogleOAuthProvider()


    if provider == "github":

        return GithubOAuthProvider()


    raise ValueError(
        "Unsupported provider"
    )
```

Update করুন

```python
from .constants import (
    GOOGLE,
    GITHUB,
    FACEBOOK,
)


def get_oauth_provider(provider):

    if provider == GOOGLE:

        return GoogleOAuthProvider()


    if provider == GITHUB:

        return GithubOAuthProvider()


    if provider == FACEBOOK:

        return FacebookOAuthProvider()


    raise ValueError(
        f"Unsupported provider: {provider}"
    )
```

---

# Step 3 — Shell Test

```bash
python manage.py shell
```

---

Google

```python
from apps.authentication.factory import (
    get_oauth_provider
)

provider = get_oauth_provider("google")

type(provider)
```

Output

```python
GoogleOAuthProvider
```

---

Github

```python
provider = get_oauth_provider("github")

type(provider)
```

Output

```python
GithubOAuthProvider
```

---

Facebook

```python
provider = get_oauth_provider("facebook")

type(provider)
```

Output

```python
FacebookOAuthProvider
```

---

# Step 4 — Authorization URL Test

```python
provider = get_oauth_provider(
    "facebook"
)

provider.get_authorization_url()
```

Expected

```text
https://www.facebook.com/v23.0/dialog/oauth?client_id=...
```

---

# Final Factory

এখন Factory এই তিনটা provider handle করছে।

```text
                     Factory

                         │

        ┌────────────────┼───────────────┐

        │                │               │

   GoogleProvider   GithubProvider   FacebookProvider
```

---

# Commit

```bash
git add .

git commit -m "feat(facebook): register facebook provider in oauth factory"
```

---

## ✅ Commit 4 Complete

এখন `OAuthAuthenticationService` কোনো পরিবর্তন ছাড়াই Facebook provider ব্যবহার করতে পারবে।

### পরবর্তী Commit 5

আমরা বানাব:

```text
GET /api/v1/auth/facebook/login/
```

যেটা response দেবে:

```json
{
    "authorization_url": "https://www.facebook.com/..."
}
```

তারপর browser থেকে Facebook Login শুরু করা যাবে।


---------


দারুণ। এখন Facebook provider-কে আপনার existing architecture-এ plug-in করব।

---

# Commit 4

```bash
git commit -m "feat(facebook): register facebook provider in oauth factory"
```

---

# Goal

এখন থেকে

```python
get_oauth_provider("facebook")
```

call করলে

```python
FacebookOAuthProvider()
```

return করবে।

---

# Step 1 — Update `factory.py`

File

```text
apps/authentication/factory.py
```

---

Import add করুন

```python
from apps.authentication.providers.facebook import (
    FacebookOAuthProvider
)
```

---

আগে যদি এমন থাকে

```python
from apps.authentication.providers.google import (
    GoogleOAuthProvider
)

from apps.authentication.providers.github import (
    GithubOAuthProvider
)
```

তাহলে হবে

```python
from apps.authentication.providers.google import (
    GoogleOAuthProvider
)

from apps.authentication.providers.github import (
    GithubOAuthProvider
)

from apps.authentication.providers.facebook import (
    FacebookOAuthProvider
)
```

---

# Step 2 — Register Provider

আগে

```python
def get_oauth_provider(provider):

    if provider == "google":

        return GoogleOAuthProvider()


    if provider == "github":

        return GithubOAuthProvider()


    raise ValueError(
        "Unsupported provider"
    )
```

Update করুন

```python
from .constants import (
    GOOGLE,
    GITHUB,
    FACEBOOK,
)


def get_oauth_provider(provider):

    if provider == GOOGLE:

        return GoogleOAuthProvider()


    if provider == GITHUB:

        return GithubOAuthProvider()


    if provider == FACEBOOK:

        return FacebookOAuthProvider()


    raise ValueError(
        f"Unsupported provider: {provider}"
    )
```

---

# Step 3 — Shell Test

```bash
python manage.py shell
```

---

Google

```python
from apps.authentication.factory import (
    get_oauth_provider
)

provider = get_oauth_provider("google")

type(provider)
```

Output

```python
GoogleOAuthProvider
```

---

Github

```python
provider = get_oauth_provider("github")

type(provider)
```

Output

```python
GithubOAuthProvider
```

---

Facebook

```python
provider = get_oauth_provider("facebook")

type(provider)
```

Output

```python
FacebookOAuthProvider
```

---

# Step 4 — Authorization URL Test

```python
provider = get_oauth_provider(
    "facebook"
)

provider.get_authorization_url()
```

Expected

```text
https://www.facebook.com/v23.0/dialog/oauth?client_id=...
```

---

# Final Factory

এখন Factory এই তিনটা provider handle করছে।

```text
                     Factory

                         │

        ┌────────────────┼───────────────┐

        │                │               │

   GoogleProvider   GithubProvider   FacebookProvider
```

---

# Commit

```bash
git add .

git commit -m "feat(facebook): register facebook provider in oauth factory"
```

---

## ✅ Commit 4 Complete

এখন `OAuthAuthenticationService` কোনো পরিবর্তন ছাড়াই Facebook provider ব্যবহার করতে পারবে।

### পরবর্তী Commit 5

আমরা বানাব:

```text
GET /api/v1/auth/facebook/login/
```

যেটা response দেবে:

```json
{
    "authorization_url": "https://www.facebook.com/..."
}
```

তারপর browser থেকে Facebook Login শুরু করা যাবে।


-----------

দারুণ। এবার **Commit 6**-এ Facebook OAuth-এর মূল login flow complete করব।

এখানে আমরা নতুন কোনো authentication logic লিখব না। **আগের `OAuthAuthenticationService` reuse করব।**

---

# Commit 6

```bash
git commit -m "feat(facebook): add facebook callback endpoint"
```

---

# Step 1 — `views.py`

Import:

```python
from .constants import FACEBOOK
from .exceptions import OAuthException
from .factory import get_oauth_provider
from .services.oauth import OAuthAuthenticationService

from rest_framework.response import Response
from rest_framework.views import APIView
```

---

Add View:

```python
class FacebookCallbackView(APIView):

    authentication_classes = []
    permission_classes = []

    def get(self, request):

        code = request.query_params.get("code")

        if not code:

            return Response(
                {
                    "error": "Authorization code is required."
                },
                status=400,
            )

        try:

            provider = get_oauth_provider(
                FACEBOOK
            )

            service = OAuthAuthenticationService(
                provider
            )

            result = service.authenticate(
                code
            )

            user = result["user"]

            return Response(
                {
                    "user": {
                        "id": str(user.id),
                        "email": user.email,
                        "full_name": user.full_name,
                    },
                    "tokens": result["tokens"],
                }
            )

        except OAuthException as exc:

            return Response(
                {
                    "error": {
                        "message": exc.message,
                        "details": exc.extra,
                    }
                },
                status=exc.status_code,
            )
```

---

# Step 2 — `urls.py`

Import

```python
from .views import (
    FacebookLoginView,
    FacebookCallbackView,
)
```

Add URL

```python
path(
    "facebook/callback/",
    FacebookCallbackView.as_view(),
    name="facebook-callback",
),
```

---

## URLs

এখন থাকবে

```text
GET /api/v1/auth/facebook/login/

GET /api/v1/auth/facebook/callback/
```

---

# Step 3 — Browser Test

Open

```text
http://127.0.0.1:8000/api/v1/auth/facebook/login/
```

Response:

```json
{
    "authorization_url": "https://www.facebook.com/..."
}
```

---

Browser-এ URL open করুন।

Facebook Login করুন।

Redirect হবে

```text
http://localhost:8000/api/v1/auth/facebook/callback/?code=AQ....
```

---

Expected Response

```json
{
    "user": {
        "id": "uuid",
        "email": "atiar@gmail.com",
        "full_name": "Md Atiar Rahman"
    },
    "tokens": {
        "access": "...",
        "refresh": "..."
    }
}
```

---

# Step 4 — Verify Database

Shell

```bash
python manage.py shell
```

```python
from apps.authentication.models import OAuthAccount

OAuthAccount.objects.all()
```

Expected

```text
<QuerySet [
    google - atiar@gmail.com,
    github - atiar@gmail.com,
    facebook - atiar@gmail.com
]>
```

---

## ⚠️ একটি গুরুত্বপূর্ণ জিনিস

আপনার `OAuthAuthenticationService` যদি Google-এর জন্য এভাবে call করে:

```python
provider.exchange_code(
    code=code,
    redirect_uri=provider.redirect_uri,
)
```

তাহলে `FacebookOAuthProvider.exchange_code()`-এর signature **একই হতে হবে**:

```python
def exchange_code(
    self,
    code,
    redirect_uri,
):
    ...
```

এবং `get_user_info()`-ও Google/GitHub-এর মতো একই interface follow করবে।

---

# Commit

```bash
git add .

git commit -m "feat(facebook): add facebook callback endpoint"
```

---

## Commit 6 শেষে Flow

```text
Browser
      │
      ▼
/facebook/login/
      │
      ▼
Facebook Login
      │
      ▼
Facebook Callback
      │
      ▼
OAuthAuthenticationService
      │
      ▼
OAuthAccount
      │
      ▼
JWT Token
```

**Commit 7**-এ আমরা Facebook account linking verify করব এবং existing user-এর সাথে Facebook account link করার production-ready flow implement করব।
দারুণ। এখন পর্যন্ত Facebook OAuth login flow তৈরি হয়েছে। এখন **Commit 7**-এ আমরা production-এর সবচেয়ে গুরুত্বপূর্ণ feature implement করব।

# Commit 7

```bash
git commit -m "feat(facebook): implement facebook account linking"
```

---

# Problem

ধরুন database-এ আগে থেকেই user আছে।

```text
User

email = atiar@gmail.com
```

এখন সেই user Facebook দিয়ে login করল।

Facebook return করল:

```text
email = atiar@gmail.com
provider_user_id = 1029384756
```

যদি আমরা নতুন User create করি তাহলে হবে

```text
User

atiar@gmail.com

atiar@gmail.com
```

❌ Duplicate User

---

# Correct Flow

```text
Facebook Login

        │

        ▼

OAuthAccount exists?

        │

   +----+----+

   │         │

  Yes        No

   │         │

Login     Search User by Email

              │

        +-----+------+

        │            │

     Exists        Not Exists

        │            │

 Link Account    Create User

        │            │

        └──────┬─────┘

               ▼

        OAuthAccount Create

               ▼

            JWT Token
```

---

# Step 1

`OAuthAuthenticationService`

বর্তমান code যদি এমন থাকে

```python
user = self.get_or_create_user(
    normalized_data
)
```

Replace করুন।

---

# Step 2

Add

```python
oauth_account = OAuthAccount.objects.filter(
    provider=self.provider.name,
    provider_user_id=normalized_data["provider_user_id"],
).select_related("user").first()

if oauth_account:

    return oauth_account.user
```

---

# Step 3

Email lookup

```python
user = User.objects.filter(
    email=normalized_data["email"]
).first()
```

---

# Step 4

Existing user

```python
if user:

    OAuthAccount.objects.create(

        user=user,

        provider=self.provider.name,

        provider_user_id=normalized_data["provider_user_id"],

        email=normalized_data["email"]

    )

    return user
```

---

# Step 5

New User

```python
user = self.create_user(
    normalized_data
)

OAuthAccount.objects.create(

    user=user,

    provider=self.provider.name,

    provider_user_id=normalized_data["provider_user_id"],

    email=normalized_data["email"]

)

return user
```

---

# Final Method

Flow হবে

```text
Provider

↓

Normalize

↓

OAuthAccount ?

↓

Email ?

↓

Create User

↓

Create OAuthAccount

↓

JWT
```

---

# Test 1

প্রথমবার Facebook login

Database

```text
User

1

OAuthAccount

facebook
```

---

# Test 2

আবার Facebook login

Database

```text
User

still 1

OAuthAccount

still 1
```

Duplicate হবে না।

---

# Test 3

আগে Google login

পরে Facebook login

Database

```text
User

1
```

OAuthAccount

```text
google

facebook
```

একই User-এর সাথে দুইটা provider link হবে।

---

# Shell Verify

```python
User.objects.count()
```

Expected

```text
1
```

---

```python
OAuthAccount.objects.count()
```

Expected

```text
2
```

---

```python
user = User.objects.first()

user.oauth_accounts.all()
```

Expected

```text
<QuerySet [

google,

facebook

]>
```

---

# Commit

```bash
git add .

git commit -m "feat(facebook): implement facebook account linking"
```

---

## Commit 7 Complete ✅

এখন আপনার system-এর capability হবে:

* ✅ Email + Password Login
* ✅ Google Login
* ✅ GitHub Login
* ✅ Facebook Login
* ✅ Multiple providers linked to the same user account
* ✅ Duplicate user creation রোধ

এটাই production-grade account linking pattern, যা বড় SaaS এবং e-commerce application-এ সাধারণভাবে ব্যবহৃত হয়।
