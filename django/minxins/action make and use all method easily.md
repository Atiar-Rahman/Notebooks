তুমি যে pageটা দেখছো (`ModelViewSet` docs), সেখানে মূলত বুঝতে হবে:

👉 **ViewSet-এর ভিতরে 3টা layer থাকে**

1. Built-in actions (list, create, retrieve…)
    
2. Custom `@action`
    
3. Helper methods (`get_queryset`, `get_object`, etc.)
    

এখন তুমি জানতে চাও:  
👉 “কোন action/function কোথায় use করবো?”

আমি একদম পরিষ্কারভাবে ভেঙে দিচ্ছি।

---

# 1. Built-in Actions (auto methods)

`ModelViewSet` নিজেই এগুলো দেয়:

|Action|কখন চলে|ভিতরে কী use করবে|
|---|---|---|
|`list()`|GET `/students/`|`self.get_queryset()`|
|`retrieve()`|GET `/students/1/`|`self.get_object()`|
|`create()`|POST `/students/`|`serializer.save()`|
|`update()`|PUT `/students/1/`|`self.get_object()`|
|`partial_update()`|PATCH|`self.get_object()`|
|`destroy()`|DELETE|`self.get_object()`|

---

## Example (retrieve)

```python
def retrieve(self, request, *args, **kwargs):
    obj = self.get_object()
    serializer = self.get_serializer(obj)
    return Response(serializer.data)
```

---

# 2. Custom `@action` (নিজের API বানানো)

## (A) detail=True → single object

```python
@action(detail=True, methods=['post'])
def publish(self, request, pk=None):
```

👉 use করো:

- `self.get_object()` → single object
    
- `request.data` → input data
    

```python
student = self.get_object()
```

---

## (B) detail=False → list-level

```python
@action(detail=False, methods=['get'])
def names(self, request):
```

👉 use করো:

- `self.get_queryset()` → list data
    

```python
students = self.get_queryset()
```

---

# 3. Helper methods (সব জায়গায় use করা যায়)

## 🔹 `self.get_queryset()`

👉 কখন ব্যবহার:

- list data
    
- custom action (multiple objects)
    
- filtering
    

```python
self.get_queryset()
```

---

## 🔹 `self.get_object()`

👉 কখন ব্যবহার:

- detail view
    
- custom action (single object)
    

```python
self.get_object()
```

---

## 🔹 `self.get_serializer()`

👉 কখন ব্যবহার:

- data validate
    
- response serialize
    

```python
serializer = self.get_serializer(data=request.data)
```

---

## 🔹 `self.get_serializer_class()`

👉 কখন ব্যবহার:

- different action → different serializer
    

```python
def get_serializer_class(self):
    if self.action == "names":
        return StudentNameSerializer
```

---

## 🔹 `self.request`

👉 সব জায়গায় available

```python
user = self.request.user
data = self.request.data
```

---

# 4. কখন কোনটা use করবো (simple rule)

## 👉 Single object (1 item)

- retrieve
    
- update
    
- destroy
    
- `@action(detail=True)`
    

✔ use:

```python
self.get_object()
```

---

## 👉 Multiple object (list)

- list
    
- `@action(detail=False)`
    

✔ use:

```python
self.get_queryset()
```

---

## 👉 Input validation / save

- create
    
- update
    
- custom action
    

✔ use:

```python
serializer = self.get_serializer(...)
serializer.is_valid()
serializer.save()
```

---

# 5. তোমার confusion clear line

👉 “একেক জায়গায় একেক জিনিস কেন?”

কারণ:

- DRF একই class থেকে **multiple endpoint বানায়**
    
- তাই context অনুযায়ী:
    
    - কখনো single object
        
    - কখনো list
        
    - কখনো input data
        

---

# Final summary (মনে রাখার shortcut)

👉 Single object → `get_object()`  
👉 List object → `get_queryset()`  
👉 Input data → `request.data`  
👉 Output → `serializer.data`  
👉 Logic switch → `self.action`

---

চাও তাহলে আমি তোমাকে একটা **complete real project flow (Student API full CRUD + custom actions)** diagram আকারে বুঝিয়ে দিতে পারি — তখন 100% crystal clear হয়ে যাবে।

---------
DRF `ViewSet`-এ **helper methods** বলতে এমন built-in methods বোঝায় যেগুলো আপনি বিভিন্ন action-এর ভিতরে reuse করেন। এগুলো নিজে override বা call করে আপনি logic clean রাখেন।

---

# 🔧 DRF ViewSet Helper Methods

## 1. `self.get_queryset()`

👉 বর্তমান request অনুযায়ী queryset দেয়

```python
queryset = self.get_queryset()
```

✔ Use case:

* list view
* custom action (multiple objects)

---

## 2. `self.get_object()`

👉 URL-এর `pk` অনুযায়ী single object আনে

```python
obj = self.get_object()
```

✔ Use case:

* retrieve
* update
* destroy
* `@action(detail=True)`

---

## 3. `self.get_serializer()`

👉 serializer instance তৈরি করে

```python
serializer = self.get_serializer(data=request.data)
```

✔ Use case:

* create/update
* custom action validation
* response formatting

---

## 4. `self.get_serializer_class()`

👉 কোন serializer ব্যবহার হবে সেটা decide করে

```python
def get_serializer_class(self):
    if self.action == "list":
        return StudentListSerializer
```

✔ Use case:

* different action → different serializer

---

## 5. `self.check_permissions(request)`

👉 user permission check করে

```python
self.check_permissions(request)
```

✔ Use case:

* custom action-এর ভিতরে manual permission check

---

## 6. `self.check_object_permissions(request, obj)`

👉 single object-এর permission check করে

```python
obj = self.get_object()
self.check_object_permissions(request, obj)
```

✔ Use case:

* detail custom action

---

## 7. `self.filter_queryset(queryset)`

👉 filtering backend apply করে

```python
qs = self.filter_queryset(self.get_queryset())
```

✔ Use case:

* search, filter, ordering support

---

## 8. `self.paginate_queryset(queryset)`

👉 pagination handle করে

```python
page = self.paginate_queryset(queryset)
```

✔ Use case:

* list endpoint

---

## 9. `self.get_paginated_response(data)`

👉 paginated response তৈরি করে

```python
return self.get_paginated_response(serializer.data)
```

---

# 🧠 Quick Mind Map

| Method                       | কাজ                     |
| ---------------------------- | ----------------------- |
| `get_queryset()`             | list data               |
| `get_object()`               | single object           |
| `get_serializer()`           | serializer বানানো       |
| `get_serializer_class()`     | serializer select করা   |
| `check_permissions()`        | permission check        |
| `check_object_permissions()` | object-level permission |
| `filter_queryset()`          | filtering apply         |
| `paginate_queryset()`        | pagination              |
| `get_paginated_response()`   | paginated output        |

---

# 🔥 Simple rule মনে রাখো

* 📦 Data আনতে → `get_queryset()` / `get_object()`
* 🧾 Data process → `get_serializer()`
* 🔐 Security → `check_permissions`
* 🎯 Output control → `filter + paginate`

---

চাও তাহলে আমি এগুলো ব্যবহার করে একটা **real Student API (list + custom action + filter + pagination সব একসাথে)** বানিয়ে দেখাতে পারি — তখন পুরো flow একদম clear হয়ে যাবে।
হ্যাঁ — তুমি যে **cdrf.co ModelViewSet page** দেখছো, সেখানে থাকা methods গুলো মূলত **helper methods (base-level building blocks)** হিসেবেই কাজ করে।

কিন্তু সবগুলো same type না। আমি cleanভাবে ভাগ করে দিচ্ছি 👇

---

# 🔥 1. সত্যিকারের Helper Methods (সবচেয়ে important)

এগুলো তুমি almost সব জায়গায় use করো:

## ✅ `get_queryset()`

👉 data list করার base source

```python
self.get_queryset()
```

---

## ✅ `get_object()`

👉 single object আনে (pk based)

```python
self.get_object()
```

---

## ✅ `get_serializer()`

👉 serializer বানায়

```python
self.get_serializer(data=request.data)
```

---

## ✅ `get_serializer_class()`

👉 কোন serializer use হবে decide করে

```python
self.get_serializer_class()
```

---

## ✅ `filter_queryset()`

👉 filter backend apply করে

```python
self.filter_queryset(queryset)
```

---

## ✅ `paginate_queryset()`

👉 pagination handle করে

```python
self.paginate_queryset(queryset)
```

---

## ✅ `get_paginated_response()`

👉 paginated response দেয়

```python
self.get_paginated_response(data)
```

---

# 🔐 2. Permission/Validation helper methods

## ✅ `check_permissions()`

👉 general permission check

```python
self.check_permissions(request)
```

---

## ✅ `check_object_permissions()`

👉 single object permission check

```python
self.check_object_permissions(request, obj)
```

---

# ⚙️ 3. Internal framework methods (normally override কম করা হয়)

## ⚠️ এগুলো internal flow handle করে:

* `list()`
* `create()`
* `retrieve()`
* `update()`
* `destroy()`

👉 এগুলো technically helper না, এগুলো **action methods (CRUD handlers)**

---

# 🧠 4. Important clarity (তোমার confusion point)

👉 এই page-এর সব method = helper না

### 3 ধরনের জিনিস আছে:

## 1️⃣ Helper methods (reuse)

→ get_queryset, get_object

## 2️⃣ Action methods (CRUD)

→ list, create, update

## 3️⃣ Lifecycle hooks (optional override)

→ perform_create, perform_update

---

# 🔥 5. Lifecycle hooks (extra important)

## ✅ `perform_create()`

```python
def perform_create(self, serializer):
    serializer.save()
```

👉 save logic customize করার জায়গা

---

## ✅ `perform_update()`

```python
def perform_update(self, serializer):
    serializer.save()
```

---

## ✅ `perform_destroy()`

```python
def perform_destroy(self, instance):
    instance.delete()
```

---

# 🧩 Final simple answer

👉 তোমার প্রশ্নের direct answer:

### ❓ “এই page-এর method গুলো helper method?”

✔️ সব না
✔️ কিছু helper
✔️ কিছু action (CRUD)
✔️ কিছু lifecycle hook

---

# 🧠 One-line memory trick

👉 **Helper = get something**
👉 **Action = do something (CRUD)**
👉 **Hook = customize something**

---

চাও তাহলে আমি তোমাকে একটা **full flow diagram (request → viewset → helper → serializer → DB)** এভাবে দেখাতে পারি — তখন পুরো DRF architecture একদম crystal clear হয়ে যাবে।
