ভালো প্রশ্ন 👍 — “any project-এ use করা যাবে এমন reusable signal” কীভাবে লিখবে, সেটাই দেখাই।
এটা এমনভাবে বানাবো যাতে তুমি যেকোনো Django/DRF project-এ copy করে use করতে পারো 🔥

---

# 🎯 Goal

👉 reusable + clean + plug-and-play CORS signal

---

# 🧱 1. Dedicated app বানাও (recommended)

```bash
python manage.py startapp core
```

👉 structure:

```bash
core/
    __init__.py
    apps.py
    cors_signals.py   👈 reusable logic
```

---

# ⚙️ 2. settings.py এ add করো

```python
INSTALLED_APPS = [
    "corsheaders",
    "core",   # 👈 important
]
```

---

# ⚡ 3. Reusable Signal Code

```python
# core/cors_signals.py

from corsheaders.signals import check_request_enabled
from django.conf import settings


def allow_cors_dynamic(sender, request, **kwargs):
    origin = request.headers.get("Origin")

    if not origin:
        return False

    # ✅ 1. settings থেকে dynamic list
    allowed_origins = getattr(settings, "DYNAMIC_CORS_ORIGINS", [])

    if origin in allowed_origins:
        return True

    # ✅ 2. public API allow
    if request.path.startswith("/api/public/"):
        return True

    # ✅ 3. localhost always allow (dev সুবিধা)
    if origin.startswith("http://localhost") or origin.startswith("http://127.0.0.1"):
        return True

    return False


check_request_enabled.connect(allow_cors_dynamic)
```

---

# 🔗 4. Signal connect করা

```python
# core/apps.py

from django.apps import AppConfig

class CoreConfig(AppConfig):
    name = "core"

    def ready(self):
        from . import cors_signals
```

---

# 🧠 5. settings.py (dynamic control)

```python
DYNAMIC_CORS_ORIGINS = [
    "https://client1.com",
    "https://client2.com",
]
```

---

# 🚀 এখন কী হলো?

👉 তুমি যেকোনো project-এ:

* শুধু `core` app copy করো
* settings update করো

👉 আর কাজ হয়ে যাবে 😎

---

# 🔥 Advanced (optional DB support)

চাও তো DB থেকেও নিতে পারো:

```python
from core.models import AllowedOrigin

if AllowedOrigin.objects.filter(domain=origin).exists():
    return True
```

---

# 🎯 Flow

```text
Request →
    Origin check →
        settings match? ✅
        public API? ✅
        localhost? ✅
    else ❌
```

---

# ⚠️ Common mistakes

❌ `apps.py ready()` না লিখা
❌ app `INSTALLED_APPS` এ না দেওয়া
❌ `Origin` header handle না করা

---

# 💬 Final Summary

* signal = project-wide listener
* একবার লিখলেই সব app-এ কাজ করবে
* reusable করতে হলে:
  👉 separate app বানাও
  👉 settings-driven logic রাখো

---

# 🚀 Pro Tip

👉 এটাকে package বানিয়েও reuse করতে পারো (pip install style)

---

চাও তো আমি এটাকে **mini pip package বানানোর step** দেখাতে পারি — future project-এ এক লাইনে use করতে পারবা 😎



চলো এবার তোমার CORS signal-টা **mini pip package** বানাই—যাতে future project-এ এক লাইনে install করে use করতে পারো 🔥

---

# 🎯 Goal

👉 reusable Django CORS signal package
👉 `pip install my-cors-signal` টাইপ use

---

# 🧱 1. Folder Structure বানাও

```bash
my-cors-signal/
│
├── cors_signal/
│   ├── __init__.py
│   ├── apps.py
│   ├── signals.py
│
├── pyproject.toml   👈 modern packaging
├── README.md
├── LICENSE
```

---

# ⚡ 2. Signal Code (core logic)

```python
# cors_signal/signals.py

from corsheaders.signals import check_request_enabled
from django.conf import settings


def allow_cors_dynamic(sender, request, **kwargs):
    origin = request.headers.get("Origin")

    if not origin:
        return False

    allowed = getattr(settings, "DYNAMIC_CORS_ORIGINS", [])

    if origin in allowed:
        return True

    if request.path.startswith("/api/public/"):
        return True

    return False


check_request_enabled.connect(allow_cors_dynamic)
```

---

# 🔗 3. apps.py (auto load signal)

```python
# cors_signal/apps.py

from django.apps import AppConfig


class CorsSignalConfig(AppConfig):
    name = "cors_signal"

    def ready(self):
        from . import signals
```

---

# 🧠 4. **init**.py

```python
default_app_config = "cors_signal.apps.CorsSignalConfig"
```

---

# ⚙️ 5. pyproject.toml (modern setup)

```toml
[project]
name = "django-cors-dynamic-signal"
version = "0.1.0"
description = "Reusable dynamic CORS signal for Django"
authors = [{name = "Your Name"}]
dependencies = [
    "django>=4.2",
    "django-cors-headers"
]

[build-system]
requires = ["setuptools", "wheel"]
build-backend = "setuptools.build_meta"
```

---

# 📘 6. README.md (short doc)

```md
# Django CORS Dynamic Signal

## Install
pip install django-cors-dynamic-signal

## Usage
Add to INSTALLED_APPS:

cors_signal

## Settings
DYNAMIC_CORS_ORIGINS = [
    "https://example.com"
]
```

---

# 🛠️ 7. Build package

```bash
pip install build
python -m build
```

👉 output:

```bash
dist/
    django_cors_dynamic_signal-0.1.0-py3-none-any.whl
```

---

# 📦 8. Local install test

```bash
pip install dist/*.whl
```

---

# 🚀 9. Project এ use

```python
INSTALLED_APPS = [
    "corsheaders",
    "cors_signal",   # 👈 তোমার package
]
```

```python
DYNAMIC_CORS_ORIGINS = [
    "https://client1.com",
]
```

👉 done 😎 signal auto run করবে

---

# 🌍 10. (Optional) PyPI publish

```bash
pip install twine
twine upload dist/*
```

👉 এরপর:

```bash
pip install django-cors-dynamic-signal
```

---

# 🎯 Final Flow

```text
install →
add app →
settings set →
signal auto run ✅
```

---

# ⚠️ Pro Tips

* version change না করলে re-upload হবে না
* name unique হতে হবে (PyPI)
* `.gitignore` এ `dist/` add করো

---

# 💬 Simple Summary

👉 reusable করতে চাইলে → package বানাও
👉 apps.py → signal auto load
👉 settings → dynamic control

---

চাও তো আমি এটাকে **GitHub repo + professional structure + CI/CD setup** করে দেখাতে পারি 😎
