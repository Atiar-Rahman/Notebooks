
Django REST Framework (DRF)-এ **throttling** ব্যবহার করা হয় API-তে একজন user/client কতবার request করতে পারবে সেটা সীমাবদ্ধ করার জন্য।

### 1. `settings.py` এ throttle configure করো

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],
    "DEFAULT_THROTTLE_RATES": {
        "anon": "10/minute",
        "user": "100/minute",
    },
}
```

এখানে:

* Anonymous user → প্রতি মিনিটে সর্বোচ্চ **10 requests**
* Authenticated user → প্রতি মিনিটে সর্বোচ্চ **100 requests**

### 2. View-তে আলাদাভাবে throttle দিতে পারো

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.throttling import UserRateThrottle


class MyThrottle(UserRateThrottle):
    scope = "my_api"


class MyView(APIView):
    throttle_classes = [MyThrottle]

    def get(self, request):
        return Response({"message": "Hello"})
```

তারপর `settings.py`:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_RATES": {
        "my_api": "5/minute",
    }
}
```

এখন `MyView`-তে একজন authenticated user প্রতি মিনিটে সর্বোচ্চ **5 বার** request করতে পারবে।

### 3. Function-based view হলে

```python
from rest_framework.decorators import api_view, throttle_classes
from rest_framework.throttling import UserRateThrottle
from rest_framework.response import Response


class MyThrottle(UserRateThrottle):
    scope = "my_api"


@api_view(["GET"])
@throttle_classes([MyThrottle])
def my_view(request):
    return Response({"message": "Hello"})
```

Limit অতিক্রম করলে DRF সাধারণত **HTTP 429 Too Many Requests** response দেয়।

**সহজভাবে:**
`Throttle = API request-এর rate limiter`। Login API, OTP/API abuse prevention, expensive endpoints ইত্যাদিতে এটা খুব কাজে লাগে।


---
