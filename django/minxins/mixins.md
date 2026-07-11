
যেহেতু তুমি **Senior Django REST Framework Developer** হতে চাও, তাই **Mixins + GenericAPIView** ভালোভাবে না শিখলে ViewSet-ও পুরোপুরি বোঝা যাবে না।

এটা DRF-এর সবচেয়ে গুরুত্বপূর্ণ foundation-এর একটি।

---

# Lesson Roadmap

আজ আমরা শিখব

```
Part 1
Why GenericAPIView exists

Part 2
APIView vs GenericAPIView

Part 3
GenericAPIView attributes

Part 4
GenericAPIView methods

Part 5
Mixins

Part 6
Every mixin deeply

CreateModelMixin
ListModelMixin
RetrieveModelMixin
UpdateModelMixin
DestroyModelMixin

Part 7
Generic Views

ListAPIView
CreateAPIView
RetrieveAPIView
UpdateAPIView
DestroyAPIView
ListCreateAPIView
RetrieveUpdateAPIView
RetrieveDestroyAPIView
RetrieveUpdateDestroyAPIView

Part 8
How DRF internally works

Part 9
Real Project Examples

Part 10
Common mistakes

Part 11
Interview Questions

Part 12
Senior Level Notes
```

---

# Part 1

# Why GenericAPIView Exists

ধরো তুমি APIView দিয়ে CRUD লিখছো।

```python
class ProductAPIView(APIView):

    def get(self, request):
        products = Product.objects.all()

        serializer = ProductSerializer(products, many=True)

        return Response(serializer.data)
```

Create

```python
class ProductAPIView(APIView):

    def post(self, request):

        serializer = ProductSerializer(data=request.data)

        serializer.is_valid(raise_exception=True)

        serializer.save()

        return Response(serializer.data)
```

Update

```python
def put(...)
```

Delete

```python
def delete(...)
```

সব জায়গায় একই code

```
serializer

queryset

get_object()

get_serializer()

is_valid()

save()
```

Repeated.

DRF developer ভাবলো

> "একই জিনিস বারবার কেন লিখবো?"

তখন GenericAPIView বানানো হলো।

---

# GenericAPIView কী?

এটা হচ্ছে

```
APIView +

common reusable methods
```

এটা নিজেরা কিছু CRUD করে না।

এটা শুধু helper দেয়।

---

# Part 2

APIView vs GenericAPIView

APIView

```
Everything manually.
```

Example

```python
class Product(APIView):

    def get(self):

        ...

    def post(self):

        ...
```

GenericAPIView

```
Provides helper methods.

You still decide CRUD.
```

Example

```python
class Product(GenericAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

এখন

```
get_queryset()

get_object()

get_serializer()
```

সব ready.

---

# Part 3

Important Attributes

সবচেয়ে important.

---

## queryset

```python
queryset = Product.objects.all()
```

DRF এখান থেকে object বের করবে।

Example

```python
class ProductView(GenericAPIView):

    queryset = Product.objects.all()
```

---

## serializer_class

```python
serializer_class = ProductSerializer
```

---

## lookup_field

Default

```
pk
```

URL

```
products/5/
```

মানে

```
pk=5
```

Change করলে

```python
lookup_field = "slug"
```

URL

```
products/iphone-16/
```

---

## lookup_url_kwarg

Suppose

```
path("product/<int:id>/")
```

কিন্তু model

```
pk
```

তাহলে

```python
lookup_url_kwarg="id"
```

---

## pagination_class

Custom pagination

```python
pagination_class = MyPagination
```

---

## filter_backends

```python
filter_backends = [
    SearchFilter,
    OrderingFilter
]
```

---

## permission_classes

```python
permission_classes=[
    IsAuthenticated
]
```

---

## authentication_classes

```python
authentication_classes=[
    JWTAuthentication
]
```

---

# Part 4

Important Methods

---

## get_queryset()

সবচেয়ে important.

Instead of

```python
queryset = Product.objects.all()
```

dynamic

```python
def get_queryset(self):

    return Product.objects.filter(user=self.request.user)
```

Example

```
Admin

→ all products

Customer

→ own products
```

---

Another example

```python
def get_queryset(self):

    qs = Product.objects.all()

    category = self.request.query_params.get("category")

    if category:

        qs = qs.filter(category=category)

    return qs
```

Senior developers প্রায়ই এটা ব্যবহার করে।

---

## get_serializer()

Instead of

```python
ProductSerializer(...)
```

Use

```python
serializer = self.get_serializer(...)
```

Example

```python
serializer = self.get_serializer(products,many=True)
```

---

## get_serializer_class()

Dynamic serializer

```python
if self.request.method=="GET":

    return ProductReadSerializer

return ProductWriteSerializer
```

Interview favourite.

---

## get_object()

Instead of

```python
Product.objects.get(pk=id)
```

Use

```python
product = self.get_object()
```

Automatically

```
404

permission

lookup
```

সব করে।

---

# Part 5

Mixins

এটাই lesson-এর heart.

Mixin মানে

```
Small reusable CRUD block.
```

একটা mixin

একটা কাজ।

---

ListModelMixin

```
only list
```

CreateModelMixin

```
only create
```

RetrieveModelMixin

```
only detail
```

UpdateModelMixin

```
only update
```

DestroyModelMixin

```
only delete
```

---

ভাবো LEGO block।

```
List

Create

Update

Delete
```

যেটা লাগবে সেটা জোড়া দাও।

---

# Part 6

CreateModelMixin

এর method

```
create()
```

Internally

```python
serializer=self.get_serializer(data=request.data)

serializer.is_valid()

serializer.save()

return Response(...)
```

তুমি শুধু

```python
class Product(
    CreateModelMixin,
    GenericAPIView
):
```

---

GET request এ কাজ করবে?

না।

কারণ create() call হয়নি।

---

Example

```python
class ProductCreateView(

    CreateModelMixin,

    GenericAPIView

):

    queryset=Product.objects.all()

    serializer_class=ProductSerializer

    def post(self,request):

        return self.create(request)
```

Notice

```
self.create()
```

এইটা এসেছে mixin থেকে।

---

# ListModelMixin

Method

```
list()
```

Internally

```
queryset

serializer

pagination

response
```

সব handle করে।

Example

```python
class ProductListView(

    ListModelMixin,

    GenericAPIView

):

    queryset=Product.objects.all()

    serializer_class=ProductSerializer

    def get(self,request):

        return self.list(request)
```

---

# RetrieveModelMixin

Method

```
retrieve()
```

Internally

```
get_object()

serializer

response
```

Example

```python
class ProductDetail(

    RetrieveModelMixin,

    GenericAPIView

):

    queryset=Product.objects.all()

    serializer_class=ProductSerializer

    def get(self,request,*args,**kwargs):

        return self.retrieve(request,*args,**kwargs)
```

---

# UpdateModelMixin

Methods

```
update()

partial_update()
```

PUT

```python
return self.update(...)
```

PATCH

```python
return self.partial_update(...)
```

---

# DestroyModelMixin

Method

```
destroy()
```

Example

```python
def delete(self,request,*args,**kwargs):

    return self.destroy(request,*args,**kwargs)
```

---

# Part 7

Generic Views

এগুলো আসলে **Mixin + GenericAPIView** এর combination।

```
ListAPIView
=
ListModelMixin
+
GenericAPIView
```

```
CreateAPIView
=
CreateModelMixin
+
GenericAPIView
```

```
ListCreateAPIView
=
ListModelMixin
+
CreateModelMixin
+
GenericAPIView
```

```
RetrieveUpdateDestroyAPIView
=
Retrieve
+
Update
+
Destroy
+
GenericAPIView
```

অর্থাৎ DRF তোমার জন্য mixin গুলো আগে থেকেই জোড়া লাগিয়ে দিয়েছে।

---

# Internal Architecture

```
APIView

        ↑

GenericAPIView

        ↑

Mixins

        ↑

Concrete Generic Views

        ↑

ViewSets

        ↑

ModelViewSet
```

এটাই DRF-এর inheritance chain বুঝতে সবচেয়ে গুরুত্বপূর্ণ।

---

# Real Project Example

Blog List + Create

```python
class BlogListCreateView(ListCreateAPIView):
    queryset = Blog.objects.all()
    serializer_class = BlogSerializer
```

এখানে DRF নিজেই:

* `GET` → `list()`
* `POST` → `create()`

ম্যাপ করে দেয়।

---

# Common Mistakes

❌ `queryset` বা `get_queryset()` না দেওয়া।

❌ `serializer_class` না দেওয়া।

❌ `get_queryset()`-এ `self.request.user` ব্যবহার করতে গিয়ে anonymous user-এর কথা না ভাবা।

❌ `self.get_object()` এর বদলে `Model.objects.get()` ব্যবহার করে 404 handling হারিয়ে ফেলা।

❌ `get_serializer()` এর বদলে সরাসরি serializer instantiate করা, ফলে GenericAPIView-এর সুবিধা না পাওয়া।

❌ `partial_update()` এবং `update()`-এর পার্থক্য না বোঝা (`PATCH` বনাম `PUT`)।

---

# Interview Questions

1. APIView এবং GenericAPIView-এর মধ্যে পার্থক্য কী?
2. GenericAPIView কী কী helper method দেয়?
3. `get_queryset()` কেন `queryset`-এর চেয়ে বেশি flexible?
4. `get_serializer_class()` কখন ব্যবহার করবে?
5. `lookup_field` এবং `lookup_url_kwarg`-এর পার্থক্য কী?
6. `CreateModelMixin`-এর `create()` method internally কী করে?
7. `ListAPIView` কীভাবে তৈরি হয়েছে?
8. `ModelViewSet`-এর নিচে কোন inheritance chain কাজ করে?
9. `self.get_object()` ব্যবহার করার সুবিধা কী?
10. `PATCH` এবং `PUT` GenericAPIView-তে কীভাবে handle হয়?

---

# Senior Developer Notes

Senior DRF developer হিসেবে তোমার এগুলো মুখস্থ না হলেও পরিষ্কারভাবে বোঝা উচিত:

* `GenericAPIView` নিজে কোনো HTTP method (`get()`, `post()`, `put()`) implement করে না; এটি শুধু reusable infrastructure দেয়।
* Mixins-ও HTTP method implement করে না; তারা `list()`, `create()`, `retrieve()`, `update()`, `destroy()` এর মতো action method দেয়।
* HTTP method (`get()`, `post()`) থেকে action method (`self.list()`, `self.create()`) call করা হয়।
* Concrete Generic Views (যেমন `ListAPIView`) এই wiring আগে থেকেই করে রেখেছে।
* `ModelViewSet` একই ধারণাকে আরও এক ধাপ এগিয়ে router-এর মাধ্যমে URL mapping করে।

---

## পরবর্তী লেসন (অত্যন্ত গুরুত্বপূর্ণ)

এই লেসনটি বোঝার পর তোমার শেখা উচিত:

1. **Mixins-এর source code line by line** (DRF internals)
2. **Concrete Generic Views-এর source code**
3. **ModelViewSet কীভাবে Mixins + GenericAPIView ব্যবহার করে তৈরি হয়েছে**
4. **MRO (Method Resolution Order)** — Python inheritance কীভাবে DRF-এ কাজ করে

এই চারটি বুঝে গেলে তুমি শুধু DRF ব্যবহার করবে না, **DRF-এর design-ও বুঝতে পারবে**, যা একজন সিনিয়র Django REST Framework ডেভেলপারের গুরুত্বপূর্ণ দক্ষতা।
এখন আমরা এমন একটি লেসনে যাব যেটা খুব কম মানুষ গভীরভাবে শেখে।

# Lesson 2: Mixins + GenericAPIView Internals (Source Code Explained)

আজকের লক্ষ্য:

> **DRF কীভাবে ভিতরে কাজ করে সেটা বুঝা।**

একজন Senior Developer শুধু API ব্যবহার করে না, API-এর source code পড়তে পারে।

---

# আজ কী শিখব

```
1. DRF Request Flow

2. GenericAPIView source code

3. CreateModelMixin source code

4. ListModelMixin source code

5. RetrieveModelMixin source code

6. UpdateModelMixin source code

7. DestroyModelMixin source code

8. Multiple Inheritance

9. MRO

10. Interview Questions
```

---

# Part 1

# Request Flow

ধরো

```
GET /products/
```

এটা কখনোই সরাসরি serializer-এ যায় না।

Flow:

```
Client

↓

URL

↓

View

↓

APIView.dispatch()

↓

initial()

↓

authentication

↓

permission

↓

throttle

↓

get()

↓

list()

↓

get_queryset()

↓

filter_queryset()

↓

paginate_queryset()

↓

get_serializer()

↓

serializer.data

↓

Response

↓

render

↓

Client
```

এই flow টা DRF-এর backbone।

---

# Part 2

ধরো

```python
class ProductView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

তুমি মাত্র ৩ লাইন লিখেছো।

কিন্তু ভিতরে কী হচ্ছে?

---

## ListAPIView

Source (simplified)

```python
class ListAPIView(
    ListModelMixin,
    GenericAPIView
):

    def get(self, request, *args, **kwargs):

        return self.list(request, *args, **kwargs)
```

এখানে

```
GET

↓

list()
```

call হচ্ছে।

---

Question

list() কোথায়?

উত্তর

```
ListModelMixin
```

---

# Part 3

ListModelMixin Source

Real source অনেক বড়।

Easy version

```python
class ListModelMixin:

    def list(self, request):

        queryset = self.filter_queryset(
            self.get_queryset()
        )

        page = self.paginate_queryset(queryset)

        if page is not None:

            serializer = self.get_serializer(
                page,
                many=True
            )

            return self.get_paginated_response(
                serializer.data
            )

        serializer = self.get_serializer(
            queryset,
            many=True
        )

        return Response(serializer.data)
```

এখন line by line বুঝি।

---

## Line 1

```
self.get_queryset()
```

মানে

```
queryset =
Product.objects.all()
```

অথবা

```
get_queryset()
```

override করলে সেটা।

---

Example

```python
def get_queryset(self):

    return Product.objects.filter(
        owner=self.request.user
    )
```

এটাই use হবে।

---

## এরপর

```
filter_queryset()
```

এটা search/filter/order apply করে।

Suppose

```
?search=iphone
```

তাহলে

আগে

```
100 products
```

পরে

```
20 products
```

---

## এরপর

```
paginate_queryset()
```

Suppose

Database

```
10000 rows
```

Pagination

```
page=1
```

return

```
20 rows
```

---

## এরপর

```
get_serializer()
```

internally

```
ProductSerializer(...)
```

call করে।

---

শেষে

```
Response(serializer.data)
```

---

# Summary

মানে

```
list()

↓

queryset

↓

filter

↓

pagination

↓

serializer

↓

response
```

---

# Part 4

CreateModelMixin

Source

```python
class CreateModelMixin:

    def create(
        self,
        request,
        *args,
        **kwargs
    ):

        serializer = self.get_serializer(
            data=request.data
        )

        serializer.is_valid(
            raise_exception=True
        )

        self.perform_create(serializer)

        return Response(
            serializer.data,
            status=201
        )
```

---

সবচেয়ে গুরুত্বপূর্ণ

```
perform_create()
```

---

ওটা কী?

Source

```python
def perform_create(self, serializer):

    serializer.save()
```

---

Question

override কেন করবো?

কারণ

```
serializer.save()
```

এর আগে

extra data add করতে।

Example

```python
def perform_create(
    self,
    serializer
):

    serializer.save(
        owner=self.request.user
    )
```

এটাই real project-এ সবচেয়ে common।

---

# Part 5

RetrieveModelMixin

Source

```python
class RetrieveModelMixin:

    def retrieve(
        self,
        request,
        *args,
        **kwargs
    ):

        instance = self.get_object()

        serializer = self.get_serializer(
            instance
        )

        return Response(serializer.data)
```

---

সবচেয়ে important

```
get_object()
```

---

GenericAPIView-এর ভিতরে

simplified

```python
def get_object(self):

    queryset = self.get_queryset()

    pk = self.kwargs["pk"]

    return get_object_or_404(
        queryset,
        pk=pk
    )
```

তাই

```
Model.objects.get()
```

use করার দরকার নেই।

---

# Part 6

UpdateModelMixin

Source

```python
class UpdateModelMixin:

    def update(

        self,

        request,

        *args,

        **kwargs

    ):

        partial = kwargs.pop(
            "partial",
            False
        )

        instance = self.get_object()

        serializer = self.get_serializer(

            instance,

            data=request.data,

            partial=partial

        )

        serializer.is_valid(
            raise_exception=True
        )

        self.perform_update(serializer)

        return Response(serializer.data)
```

---

perform_update()

default

```python
serializer.save()
```

---

Override

```python
def perform_update(
    self,
    serializer
):

    serializer.save(
        updated_by=self.request.user
    )
```

---

PATCH কীভাবে?

```
partial_update()
```

Source

```python
def partial_update(

    self,

    request,

    *args,

    **kwargs

):

    kwargs["partial"] = True

    return self.update(
        request,
        *args,
        **kwargs
    )
```

এটাই magic।

---

# PUT

```
partial=False
```

সব field লাগবে।

---

PATCH

```
partial=True
```

যেটুকু দিবে সেটুকু।

---

# Part 7

DestroyModelMixin

Source

```python
class DestroyModelMixin:

    def destroy(

        self,

        request,

        *args,

        **kwargs

    ):

        instance = self.get_object()

        self.perform_destroy(
            instance
        )

        return Response(
            status=204
        )
```

Default

```python
def perform_destroy(
    self,
    instance
):

    instance.delete()
```

---

Override

Soft Delete

```python
def perform_destroy(
    self,
    instance
):

    instance.is_deleted = True

    instance.save()
```

---

# Part 8

GenericAPIView

সবচেয়ে important methods

```
get_queryset()

↓

get_object()

↓

filter_queryset()

↓

paginate_queryset()

↓

get_serializer()

↓

get_serializer_class()

↓

get_serializer_context()
```

---

Context

```python
serializer = self.get_serializer(...)
```

Internally

```python
ProductSerializer(

    context={

        "request":request,

        "view":self,

        "format":...

    }

)
```

তাই serializer-এর ভিতরে

```python
self.context["request"]
```

পাওয়া যায়।

---

# Part 9

Multiple Inheritance

ধরো

```python
class ProductView(

    CreateModelMixin,

    ListModelMixin,

    GenericAPIView

):
```

এখন

POST

```
↓

create()

↓

CreateModelMixin
```

GET

```
↓

list()

↓

ListModelMixin
```

Helper

```
↓

get_queryset()

↓

GenericAPIView
```

---

# Part 10

MRO (Method Resolution Order)

Python search order

```
ProductView

↓

CreateModelMixin

↓

ListModelMixin

↓

GenericAPIView

↓

APIView

↓

View

↓

object
```

Python উপর থেকে নিচে method খুঁজে।

---

Example

```
create()

পাবে

↓

CreateModelMixin
```

---

```
get_queryset()

পাবে

↓

GenericAPIView
```

---

```
dispatch()

পাবে

↓

APIView
```

---

# পুরো Flow

```
POST /products/

↓

URL

↓

ListCreateAPIView.post()

↓

CreateModelMixin.create()

↓

get_serializer()

↓

serializer.is_valid()

↓

perform_create()

↓

serializer.save()

↓

Response
```

---

# Real Project Override Points (Senior Developers)

প্রজেক্টে নিচের method-গুলো সবচেয়ে বেশি override করা হয়:

| Method                   | কেন Override করা হয়                                   |
| ------------------------ | ------------------------------------------------------ |
| `get_queryset()`         | Logged-in user অনুযায়ী data filter করতে               |
| `get_serializer_class()` | Read ও Write-এর জন্য আলাদা serializer ব্যবহার করতে     |
| `perform_create()`       | `request.user`, tenant, organization ইত্যাদি save করতে |
| `perform_update()`       | `updated_by` বা audit তথ্য save করতে                   |
| `perform_destroy()`      | Soft delete বা custom delete logic লিখতে               |
| `get_permissions()`      | Action বা method অনুযায়ী permission পরিবর্তন করতে     |

---

# Interview Questions

1. `ListAPIView` নিজে `list()` method implement করে কি?
2. `CreateModelMixin`-এ `perform_create()` কেন আলাদা method?
3. `partial_update()` কীভাবে `update()` reuse করে?
4. `get_object()` কেন `Model.objects.get()` থেকে ভালো?
5. `get_serializer()` এবং `ProductSerializer()`-এর মধ্যে পার্থক্য কী?
6. MRO কী এবং DRF-এ কেন গুরুত্বপূর্ণ?
7. `get_serializer_context()` কী কাজে লাগে?
8. `ListModelMixin`-এ filtering এবং pagination কোন ক্রমে execute হয়?

---

## পরবর্তী লেসন (Senior DRF Level)

এখন তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ বিষয়:

> **Generic Views → ViewSets → ModelViewSet Internals**

এই লেসনে আমরা source code ধরে দেখব:

* `GenericViewSet` কীভাবে `GenericAPIView`-কে extend করে
* `ViewSetMixin` কীভাবে `GET`, `POST`, `PUT`-কে action (`list`, `create`, `update`) এ map করে
* `ModelViewSet` আসলে কোন কোন mixin দিয়ে তৈরি
* `DefaultRouter` কীভাবে URL generate করে এবং request-কে সঠিক action-এ পাঠায়

এই লেসনটি বুঝতে পারলে DRF-এর architecture প্রায় সম্পূর্ণ পরিষ্কার হয়ে যাবে।
এখন আমরা DRF-এর **সবচেয়ে গুরুত্বপূর্ণ** লেসনে যাচ্ছি।

> **এই লেসন বুঝলে ModelViewSet আর "magic" মনে হবে না।**

অনেক Junior Developer শুধু ModelViewSet ব্যবহার করে। কিন্তু Senior Developer জানে **ModelViewSet-এর ভিতরে কী হচ্ছে।**

---

# Lesson 3: ViewSet, GenericViewSet, ModelViewSet Internals

---

# আজকের Roadmap

```text
1. What is ViewSet?
2. Why ViewSet was created?
3. APIView → GenericAPIView → GenericViewSet
4. ViewSetMixin
5. GenericViewSet
6. ReadOnlyModelViewSet
7. ModelViewSet
8. Router Internals
9. How Router maps HTTP methods
10. action attribute
11. self.action
12. get_serializer_class() with action
13. get_permissions() with action
14. MRO of ModelViewSet
15. Request lifecycle
16. Real project examples
17. Common mistakes
18. Interview questions
```

---

# Part 1

# Problem Before ViewSet

আগে আমাদের লিখতে হতো

```python
class ProductList(ListAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

```python
class ProductDetail(RetrieveAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

```python
class ProductCreate(CreateAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

```python
class ProductUpdate(UpdateAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

```python
class ProductDelete(DestroyAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

একটা Model-এর জন্য ৫টা View।

---

# DRF Team বলল

একই queryset

একই serializer

একই model

তাহলে

**একটা class-এ সব CRUD রাখা যায় না?**

এই চিন্তা থেকেই ViewSet এসেছে।

---

# Part 2

APIView

↓

GenericAPIView

↓

Generic Views

↓

ViewSet

↓

ModelViewSet

---

ViewSet নতুন CRUD বানায়নি।

আগের Mixins-ই ব্যবহার করেছে।

---

# Part 3

ViewSet কী?

ViewSet হচ্ছে

> **একটি class যেখানে CRUD method-এর নাম HTTP method না।**

APIView

```python
def get()
```

ViewSet

```python
def list()
```

APIView

```python
def post()
```

ViewSet

```python
def create()
```

APIView

```python
def put()
```

ViewSet

```python
def update()
```

APIView

```python
def patch()
```

ViewSet

```python
def partial_update()
```

APIView

```python
def delete()
```

ViewSet

```python
def destroy()
```

---

# সবচেয়ে গুরুত্বপূর্ণ

APIView

```text
GET

↓

get()
```

ViewSet

```text
GET

↓

list()
```

কে convert করছে?

উত্তর

```text
ViewSetMixin
```

---

# Part 4

ViewSetMixin

এটাই পুরো ViewSet-এর brain।

Source (simplified)

```python
class ViewSetMixin:

    @classonlymethod
    def as_view(cls, actions):

        ...
```

---

Router এখানে actions পাঠায়।

Example

```python
{
    "get": "list",
    "post": "create"
}
```

---

মানে

GET

↓

list()

POST

↓

create()

---

Router এই mapping পাঠায়।

---

# Part 5

GenericViewSet

Source

```python
class GenericViewSet(

    ViewSetMixin,

    GenericAPIView

):

    pass
```

দেখো

এখানে

কোন CRUD নেই।

শুধু

```text
ViewSetMixin

+

GenericAPIView
```

---

তাই GenericViewSet-এর কাছে আছে

```text
get_queryset()

get_object()

get_serializer()

filter_queryset()

pagination
```

সব।

---

# Part 6

ModelViewSet

Source

```python
class ModelViewSet(

    CreateModelMixin,

    RetrieveModelMixin,

    UpdateModelMixin,

    DestroyModelMixin,

    ListModelMixin,

    GenericViewSet

):

    pass
```

এটাই পুরো secret।

---

মানে

ModelViewSet নিজে কিছুই লেখেনি।

সব inheritance।

---

# Part 7

ReadOnlyModelViewSet

Source

```python
class ReadOnlyModelViewSet(

    RetrieveModelMixin,

    ListModelMixin,

    GenericViewSet

):

    pass
```

তাই

Allowed

```text
GET list

GET detail
```

Not Allowed

```text
POST

PUT

PATCH

DELETE
```

---

# Part 8

Router কী করে?

ধরো

```python
router.register(

    "products",

    ProductViewSet
)
```

Router internally

বানায়

```text
GET

/products/

↓

list
```

---

```text
POST

/products/

↓

create
```

---

```text
GET

/products/5/

↓

retrieve
```

---

```text
PUT

/products/5/

↓

update
```

---

```text
PATCH

/products/5/

↓

partial_update
```

---

```text
DELETE

/products/5/

↓

destroy
```

---

# Router Action Mapping

```text
GET collection

↓

list
```

```text
POST collection

↓

create
```

```text
GET detail

↓

retrieve
```

```text
PUT detail

↓

update
```

```text
PATCH detail

↓

partial_update
```

```text
DELETE detail

↓

destroy
```

---

# Part 9

Router internally call করে

```python
ProductViewSet.as_view({

    "get":"list",

    "post":"create"

})
```

Detail URL

```python
ProductViewSet.as_view({

    "get":"retrieve",

    "put":"update",

    "patch":"partial_update",

    "delete":"destroy"

})
```

এটাই পুরো magic।

---

# Part 10

action

সবচেয়ে important।

Suppose

```text
GET /products/
```

action

```text
list
```

---

```text
POST /products/
```

action

```text
create
```

---

```text
GET /products/5/
```

action

```text
retrieve
```

---

DRF automatically

```python
self.action
```

set করে।

---

# Part 11

Dynamic Serializer

```python
def get_serializer_class(self):

    if self.action=="list":

        return ProductListSerializer

    if self.action=="retrieve":

        return ProductDetailSerializer

    return ProductWriteSerializer
```

এটাই production standard।

---

# Part 12

Dynamic Permission

```python
def get_permissions(self):

    if self.action=="list":

        return [AllowAny()]

    return [IsAuthenticated()]
```

---

অথবা

```python
if self.action=="destroy":

    return [IsAdminUser()]
```

---

# Part 13

MRO

ModelViewSet

↓

CreateMixin

↓

RetrieveMixin

↓

UpdateMixin

↓

DestroyMixin

↓

ListMixin

↓

GenericViewSet

↓

ViewSetMixin

↓

GenericAPIView

↓

APIView

↓

View

↓

object

---

# Part 14

Full Request Flow

Client

↓

Router

↓

ViewSet.as_view()

↓

ViewSetMixin

↓

action determine

↓

list()

↓

ListModelMixin

↓

get_queryset()

↓

filter_queryset()

↓

paginate_queryset()

↓

get_serializer()

↓

Response

---

# Part 15

Real Project Example

```python
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

---

এখন

Router

নিজেই

সব endpoint বানাবে।

```text
GET

POST

PUT

PATCH

DELETE
```

---

# Senior Pattern

Read Serializer

```python
ProductReadSerializer
```

Write Serializer

```python
ProductWriteSerializer
```

```python
def get_serializer_class(self):

    if self.action in [

        "list",

        "retrieve"

    ]:

        return ProductReadSerializer

    return ProductWriteSerializer
```

Production-এ খুব common।

---

# Common Mistakes

❌ `request.method` ব্যবহার করা যেখানে `self.action` ব্যবহার করা উচিত।

❌ `list()` override করে pagination নষ্ট করে ফেলা (যদি `super().list()` ব্যবহার না করা হয়)।

❌ `retrieve()`-এ `self.get_object()` না ব্যবহার করে সরাসরি query করা।

❌ সব action-এর জন্য একই serializer ব্যবহার করা, যদিও read/write response আলাদা হওয়া উচিত।

❌ `ModelViewSet` ব্যবহার করে কিন্তু `http_method_names` বা permissions দিয়ে API সীমাবদ্ধ না করা।

---

# Interview Questions

1. `ViewSet` এবং `APIView`-এর মূল পার্থক্য কী?
2. `ViewSetMixin`-এর কাজ কী?
3. `GenericViewSet`-এ CRUD method কেন নেই?
4. `ModelViewSet` কোন কোন mixin দিয়ে তৈরি?
5. `Router` কীভাবে HTTP method-কে action-এ map করে?
6. `self.action` এবং `request.method`-এর মধ্যে পার্থক্য কী?
7. `ReadOnlyModelViewSet` কবে ব্যবহার করবে?
8. `get_serializer_class()`-এ `self.action` কেন বেশি উপযোগী?

---

## এখন তুমি যে লেভেলে পৌঁছেছ

তুমি এখন বুঝতে পারছ:

* ✅ `APIView`
* ✅ `GenericAPIView`
* ✅ Mixins
* ✅ Generic Views
* ✅ `ViewSet`
* ✅ `GenericViewSet`
* ✅ `ModelViewSet`
* ✅ Router-এর action mapping
* ✅ `self.action`
* ✅ DRF inheritance architecture

---

## পরবর্তী লেসন (Advanced DRF)

এখন আমরা এমন একটি বিষয় শিখব যা অনেক **৫+ বছরের Django Developer**-ও পুরোপুরি জানে না:

> **`@action` Decorator (Extra Endpoints) + Router Internals + `basename` + `reverse()` + Custom Routes**

এই লেসনে তুমি শিখবে কীভাবে `ModelViewSet`-এর ভিতরে Amazon, GitHub, Stripe-এর মতো professional API design করা হয় এবং custom endpoints তৈরি করা হয়।
এখন আমরা এমন একটি লেসনে যাচ্ছি যেটা **professional DRF development-এর heart**।

অনেক developer শুধু CRUD API বানাতে পারে। কিন্তু **real-world API**-তে শুধু CRUD থাকে না।

উদাহরণ:

```
POST /products/5/publish/
POST /orders/10/cancel/
POST /users/20/follow/
GET  /users/me/
POST /posts/5/like/
GET  /dashboard/stats/
```

এগুলো CRUD না।

এগুলোর জন্যই **`@action`**।

---

# Lesson 4: @action + Router Internals + basename + reverse()

---

# Roadmap

```text
1. Why @action exists
2. Collection vs Detail actions
3. @action syntax
4. detail=True
5. detail=False
6. methods=[]
7. url_path
8. url_name
9. self.action
10. basename
11. reverse_action()
12. Router internals
13. Real project examples
14. Common mistakes
15. Interview questions
```

---

# Part 1

# CRUD-এর সীমাবদ্ধতা

ধরো একটি `ProductViewSet` আছে।

CRUD endpoint:

```
GET /products/
GET /products/5/
POST /products/
PUT /products/5/
PATCH /products/5/
DELETE /products/5/
```

কিন্তু এখন requirement আসলো—

> Product publish করতে হবে।

এটা কি Create?

না।

Update?

না।

Delete?

না।

তাহলে?

```
POST /products/5/publish/
```

এই endpoint বানানোর জন্য `@action`।

---

# Part 2

ধরো

```python
class ProductViewSet(ModelViewSet):
    ...
```

এর ভিতরে

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class ProductViewSet(ModelViewSet):

    @action(detail=True, methods=["post"])
    def publish(self, request, pk=None):

        return Response({"message": "Published"})
```

Router automatically বানাবে

```
POST

/products/5/publish/
```

তুমি URL লিখোনি।

Router বানিয়েছে।

---

# Part 3

detail=True  

মানে

```
একটি object নিয়ে কাজ
```

Example

```
POST

/products/5/publish/
```

এখানে

```
pk=5
```

আছে।

---

আরও example

```
/orders/10/cancel/

/users/50/follow/

/posts/99/like/
```

সব

```
detail=True
```

---

# Part 4

detail=False

Object না।

Collection।

Example

```
GET

/products/popular/
```

অথবা

```
GET

/products/trending/
```

Code

```python
@action(detail=False)

def popular(self, request):

    return Response(...)
```

Router

```
GET

/products/popular/
```

---

আরও example

```
GET /dashboard/stats/

GET /users/me/

GET /products/top-rated/
```

---

# Part 5

methods

Default

```
GET
```

Change
 
```python
@action(

    detail=True,

    methods=["post"]
)
```

অথবা

```python
methods=["put"]
```

অথবা

```python
methods=["delete"]
```

Multiple

```python
methods=["get","post"]
```

---

# Part 6

url_path

Suppose

Function

```python
def mark_as_featured()
```

URL চাই

```
featured
```

তাহলে

```python
@action(

    detail=True,

    url_path="featured"
)
```

Function

```python
mark_as_featured()
```

URL

```
products/5/featured/
```

---

# Part 7

url_name

Suppose

```python
@action(

    detail=True,

    url_name="publish-product"
)
```

Reverse

```
product-publish-product
```

হবে।

---

# Part 8

self.action

ধরো

```
GET /products/
```

```
self.action

↓

list
```

---

```
GET /products/5/
```

↓

```
retrieve
```

---

```
POST /products/
```

↓

```
create
```

---

```
POST /products/5/publish/
```

↓

```
publish
```

এইটা খুব important।

---

# Part 9

Dynamic Permission

```python
def get_permissions(self):

    if self.action=="publish":

        return [IsAdminUser()]

    return [IsAuthenticated()]
```

Real project-এ common।

---

# Part 10

Dynamic Serializer

```python
def get_serializer_class(self):

    if self.action=="publish":

        return PublishSerializer

    return ProductSerializer
```

---

# Part 11

basename

এটা interview favourite।

Router

```python
router.register(

    "products",

    ProductViewSet,

    basename="product"
)
```

basename

```
product
```

---

URL name

```
product-list

product-detail

product-publish
```

সব basename দিয়ে শুরু।

---

যদি queryset থাকে

```python
queryset = Product.objects.all()
```

তাহলে

basename

নিজেই infer করবে।

---

যদি queryset না থাকে

```python
def get_queryset(...)
```

তাহলে

নিজে দিতে হবে।

```python
basename="product"
```

---

# Part 12

reverse_action()

Suppose

```python
self.reverse_action("publish")
```

Output

```
/products/5/publish/
```

Manual URL লিখতে হয় না।

---

# Part 13

Real Project Example

## Like Post

```python
@action(

    detail=True,

    methods=["post"]
)
def like(self, request, pk=None):

    post=self.get_object()

    ...

    return Response(...)
```

URL

```
POST

/posts/5/like/
```

---

## Cancel Order

```python
@action(

    detail=True,

    methods=["post"]
)
def cancel(...)
```

```
POST

/orders/20/cancel/
```

---

## Current User

```python
@action(

    detail=False
)
def me(...)
```

URL

```
GET

/users/me/
```

---

## Analytics

```python
@action(

    detail=False
)
def stats(...)
```

URL

```
GET

/dashboard/stats/
```

---

# Part 14

Router Internals

Router internally

```python
ViewSet.as_view({

    "get":"list",

    "post":"create"

})
```

Extra action

```python
ViewSet.as_view({

    "post":"publish"
})
```

এটাই magic।

---

# Part 15

Professional Folder Structure

```text
views/

    product.py

    order.py

    user.py

viewsets/

    product.py

    order.py
```

প্রতিটি ViewSet-এ

```
CRUD

+

Extra Actions
```

থাকে।

---

# Common Mistakes

### 1.

❌

```python
@action(detail=False)

def publish(...)
```

কিন্তু

```
publish

একটি object-এর।
```

Should be

```
detail=True
```

---

### 2.

Function-এর ভিতরে

```python
Product.objects.get(...)
```

না।

Use

```python
self.get_object()
```

---

### 3.

Permission check না করা।

```python
publish()

delete()

cancel()
```

এগুলোর জন্য সাধারণত custom permission লাগে।

---

### 4.

Business logic ViewSet-এর ভিতরে বড় করে লেখা।

ভালো pattern:

```text
ViewSet

↓

Service Layer

↓

Model
```

---

# Real Production Pattern

```python
@action(
    detail=True,
    methods=["post"]
)
def publish(self, request, pk=None):
    product = self.get_object()
    ProductService.publish(product, request.user)
    return Response({"status": "published"})
```

ViewSet ছোট থাকে।

Business logic Service Layer-এ যায়।

---

# Interview Questions

1. `@action` কেন ব্যবহার করা হয়?
2. `detail=True` এবং `detail=False`-এর পার্থক্য কী?
3. `methods` parameter-এর কাজ কী?
4. `basename` কখন manually দিতে হয়?
5. `reverse_action()` কী কাজে লাগে?
6. `self.action` কীভাবে set হয়?
7. CRUD endpoint-এর বাইরে API কীভাবে design করবে?
8. `publish()` action-এর জন্য কোন HTTP method সবচেয়ে উপযুক্ত এবং কেন?

---

# Senior Developer Notes

একজন Senior DRF Developer সাধারণত এই নিয়মগুলো অনুসরণ করে:

* **CRUD** → `ModelViewSet`-এর built-in action (`list`, `create`, `retrieve`, `update`, `destroy`)
* **Non-CRUD business operations** → `@action`
* **Complex business logic** → Service layer বা domain layer
* **Different serializers** → `get_serializer_class()` + `self.action`
* **Different permissions** → `get_permissions()` + `self.action`
* **Object retrieval** → সবসময় `self.get_object()`

---

## পরবর্তী লেসন (Senior Level)

এখন তোমার শেখা উচিত **Filtering + Search + Ordering + Pagination Internals**।

এই লেসনে আমরা শিখব:

* `filter_backends` ভিতরে কীভাবে কাজ করে
* `DjangoFilterBackend`
* `SearchFilter`
* `OrderingFilter`
* Custom Filter Backend
* Pagination-এর source code
* `select_related()` ও `prefetch_related()` দিয়ে N+1 Query সমস্যা সমাধান
* Production-ready filtering patterns

এই অংশটি বড় Django API-তে performance এবং scalability-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
এখন আমরা এমন একটি বিষয় শিখব যেটা **CRUD জানার পরে সবচেয়ে গুরুত্বপূর্ণ**।

> **Filtering + Search + Ordering + Pagination + Performance**

অনেক Junior Developer API বানাতে পারে, কিন্তু **fast API** বানাতে পারে না।

Senior Developer-এর API শুধু কাজ করে না, **efficient**-ও হয়।

---

# Lesson 5: Filtering + Search + Ordering + Pagination + Performance

---

# Roadmap

```text
Module 1 : Filtering Fundamentals
Module 2 : DjangoFilterBackend
Module 3 : SearchFilter
Module 4 : OrderingFilter
Module 5 : Pagination
Module 6 : Custom Filter Backend
Module 7 : Performance (select_related & prefetch_related)
Module 8 : N+1 Query Problem
Module 9 : Real Project Architecture
Module 10 : Common Mistakes
Module 11 : Interview Questions
```

---

# Module 1: Filtering Fundamentals

ধরো তোমার Product model আছে।

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    category = models.CharField(max_length=50)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()
```

সব data ফেরত দিচ্ছো।

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
```

User বলল—

```
শুধু Electronics চাই।
```

আগে আমরা লিখতাম

```python
def get_queryset(self):
    category = self.request.query_params.get("category")

    if category:
        return Product.objects.filter(category=category)

    return Product.objects.all()
```

এটা ঠিক।

কিন্তু DRF-এর built-in solution আরও powerful।

---

# Module 2: DjangoFilterBackend

প্রথমে install

```bash
pip install django-filter
```

settings.py

```python
INSTALLED_APPS = [
    ...
    "django_filters",
]
```

---

ViewSet

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend]

    filterset_fields = [
        "category",
        "price"
    ]
```

---

এখন URL

```
GET /products/?category=Electronics
```

Automatically filter হবে।

---

Multiple filter

```
GET

/products/?category=Electronics&price=500
```

---

# এটা ভিতরে কী করে?

Request

```
?category=Electronics
```

↓

Backend

↓

```python
queryset.filter(category="Electronics")
```

↓

Response

---

# Module 3: SearchFilter

Search exact match না।

Contains search।

View

```python
from rest_framework.filters import SearchFilter

class ProductViewSet(ModelViewSet):

    ...

    filter_backends = [
        SearchFilter
    ]

    search_fields = [
        "name"
    ]
```

---

URL

```
GET

/products/?search=iphone
```

Internally

```python
Product.objects.filter(
    name__icontains="iphone"
)
```

---

Multiple field

```python
search_fields = [

    "name",

    "category"
]
```

Search

```
?search=phone
```

দুই field-এই খুঁজবে।

---

# Advanced Search

```python
search_fields = [

    "^name"
]
```

মানে

Starts With

---

```python
search_fields = [

    "=name"
]
```

Exact Match

---

```python
search_fields = [

    "@name"
]
```

Full Text Search (PostgreSQL)

---

```python
search_fields = [

    "$name"
]
```

Regex Search

---

# Module 4: OrderingFilter

View

```python
from rest_framework.filters import OrderingFilter

filter_backends = [

    OrderingFilter
]

ordering_fields = [

    "price",

    "stock"
]
```

---

Ascending

```
GET

/products/?ordering=price
```

---

Descending

```
GET

/products/?ordering=-price
```

---

Multiple

```
?ordering=category,-price
```

---

Default

```python
ordering = [
    "-id"
]
```

---

# Module 5: Pagination

10000 product.

সব পাঠানো উচিত?

না।

DRF

↓

Pagination

---

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_PAGINATION_CLASS":

    "rest_framework.pagination.PageNumberPagination",

    "PAGE_SIZE":10
}
```

---

Response

```json
{
  "count":100,

  "next":"...",

  "previous":null,

  "results":[]
}
```

---

Custom

```python
from rest_framework.pagination import PageNumberPagination

class MyPagination(
    PageNumberPagination
):

    page_size=20
```

---

View

```python
pagination_class = MyPagination
```

---

LimitOffsetPagination

```
?limit=20

&offset=40
```

SQL

```sql
LIMIT 20

OFFSET 40
```

---

CursorPagination

Best for

```
Facebook Feed

Twitter Feed

Instagram Feed
```

কারণ new data insert হলেও pagination ভাঙে না।

---

# Module 6: Multiple Filter Backends

```python
filter_backends = [

    DjangoFilterBackend,

    SearchFilter,

    OrderingFilter
]
```

সব একসাথে।

User

```
?category=Phone

&search=iphone

&ordering=-price
```

সব apply হবে।

---

Execution

```
Queryset

↓

Filter

↓

Search

↓

Ordering

↓

Pagination

↓

Serializer
```

---

# Module 7: N+1 Query Problem

সবচেয়ে গুরুত্বপূর্ণ।

Models

```python
class Category(models.Model):

    name=models.CharField(...)
```

```python
class Product(models.Model):

    category=models.ForeignKey(...)
```

---

Serializer

```python
category.name
```

Loop

```
100 products
```

Database

```
1 query

+

100 query

=

101
```

এটাই

```
N+1 Query
```

---

# Solution

```python
queryset = Product.objects.select_related(
    "category"
)
```

Database

```
1 query
```

Finished.

---

# `ForeignKey`

Use

```python
select_related()
```

---

`OneToOne`

Use

```python
select_related()
```

---

`ManyToMany`

Use

```python
prefetch_related()
```

---

Reverse FK

Use

```python
prefetch_related()
```

---

Example

```python
queryset = Product.objects.prefetch_related(
    "tags"
)
```

---

# Module 8: Real Project Example

```python
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.select_related(

        "category"

    ).prefetch_related(

        "tags"

    )

    filter_backends=[

        DjangoFilterBackend,

        SearchFilter,

        OrderingFilter

    ]

    filterset_fields=[

        "category"

    ]

    search_fields=[

        "name"

    ]

    ordering_fields=[

        "price"

    ]
```

Production ready.

---

# Module 9: Performance Checklist

Always ask:

### 1

ForeignKey?

↓

```
select_related()
```

---

### 2

ManyToMany?

↓

```
prefetch_related()
```

---

### 3

Need all columns?

↓

```
only()

defer()

values()
```

---

### 4

Need count?

↓

```
annotate()
```

---

### 5

Need pagination?

↓

Always

---

# Common Mistakes

### ❌

Filtering inside serializer.

Never.

Filtering belongs in queryset/filter backend.

---

### ❌

```python
for product in products:

    product.category.name
```

Without

```python
select_related()
```

---

### ❌

Ordering any field

```python
ordering_fields="__all__"
```

Security risk.

Specify allowed fields explicitly.

---

### ❌

No pagination.

Large APIs ধীরে ধীরে slow হয়ে যায়।

---

### ❌

Complex filtering in `list()` method.

ভালো pattern:

* Simple → `filterset_fields`
* Complex → `FilterSet`
* Reusable → Custom Filter Backend

---

# Interview Questions

1. `DjangoFilterBackend` এবং `get_queryset()`-এর মধ্যে পার্থক্য কী?
2. `SearchFilter` কীভাবে কাজ করে?
3. `OrderingFilter` কেন `ordering_fields` চায়?
4. `PageNumberPagination`, `LimitOffsetPagination`, এবং `CursorPagination`-এর পার্থক্য কী?
5. N+1 Query Problem কী?
6. `select_related()` এবং `prefetch_related()`-এর পার্থক্য কী?
7. কখন `select_related()` ব্যবহার করা ভুল হবে?
8. কেন filtering `serializer`-এ করা উচিত নয়?

---

# Senior Developer Tips

Production API বানানোর সময় আমি সাধারণত এই flow অনুসরণ করি:

1. `get_queryset()`-এ base queryset তৈরি করি।
2. `select_related()` এবং `prefetch_related()` দিয়ে query optimize করি।
3. `DjangoFilterBackend`, `SearchFilter`, `OrderingFilter` দিয়ে filtering করি।
4. Pagination চালু রাখি।
5. যদি filter logic বড় হয়, `django-filter`-এর `FilterSet` class ব্যবহার করি।
6. Query count দেখে performance পরীক্ষা করি (যেমন Django Debug Toolbar বা query logging দিয়ে)।

---

# এখন তুমি যে লেভেলে পৌঁছেছ

তুমি এখন বুঝতে পারো:

* ✅ GenericAPIView
* ✅ Mixins
* ✅ Generic Views
* ✅ ViewSet
* ✅ ModelViewSet
* ✅ Router
* ✅ `@action`
* ✅ Filtering
* ✅ Search
* ✅ Ordering
* ✅ Pagination
* ✅ N+1 Query Problem
* ✅ `select_related()` / `prefetch_related()`

---

# পরবর্তী লেসন (Senior Django REST Framework)

এখন সবচেয়ে গুরুত্বপূর্ণ বিষয় হবে **Authentication + Permissions + Security Internals**।

এই লেসনে আমরা গভীরভাবে শিখব:

* Authentication request flow
* JWT internals
* Session vs Token vs JWT
* Permission classes
* Object-level permissions
* Custom permissions
* Authentication backends
* API security best practices
* Production security mistakes

এটি DRF-এর আরেকটি core pillar, এবং একজন Backend Developer-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
এখন আমরা DRF-এর **সবচেয়ে গুরুত্বপূর্ণ pillar**-এ আসছি।

> **Authentication + Permissions + Authorization + Security**

অনেক Junior Developer ভাবে:

> Login হয়ে গেছে = Secure API

এটা ভুল।

Production API-তে Authentication-এর পরে আরও **Permission**, **Object Permission**, **Throttle**, **Validation**, **Security**—সব একসাথে কাজ করে।

---

# Lesson 6: Authentication + Permissions + Security (Zero → Senior)

---

# Roadmap

```text
Module 1  : Authentication vs Authorization
Module 2  : DRF Request Lifecycle
Module 3  : Authentication Classes
Module 4  : Session Authentication
Module 5  : Basic Authentication
Module 6  : Token Authentication
Module 7  : JWT Authentication
Module 8  : Permission Classes
Module 9  : Object Level Permissions
Module 10 : Custom Permissions
Module 11 : Authentication & Permission Flow
Module 12 : Security Best Practices
Module 13 : Common Mistakes
Module 14 : Interview Questions
```

---

# Module 1: Authentication vs Authorization

এটা interview-এর সবচেয়ে common প্রশ্ন।

## Authentication

Authentication-এর কাজ:

> **"তুমি কে?"**

Example

```
Username: atiar

Password: ****
```

Server

↓

```
Yes

You are Atiar.
```

Authentication শেষ।

---

## Authorization (Permission)

এখন প্রশ্ন

```
Atiar কি Product Delete করতে পারবে?
```

এটা Authentication-এর কাজ না।

এটা Permission-এর কাজ।

---

সহজভাবে

```
Authentication

↓

Identity

↓

Who are you?
```

```
Permission

↓

Access

↓

What can you do?
```

---

# Module 2: DRF Request Lifecycle

ধরো

```
GET /products/
```

Flow

```
Client

↓

URL

↓

APIView.dispatch()

↓

initialize_request()

↓

perform_authentication()

↓

check_permissions()

↓

check_throttles()

↓

get()

↓

list()

↓

serializer

↓

Response
```

খেয়াল করো

Permission

**Serializer-এর আগেই**

হয়।

---

# Module 3: Authentication Classes

DRF-এ অনেক ধরনের Authentication আছে।

সবচেয়ে common

```
SessionAuthentication

BasicAuthentication

TokenAuthentication

JWTAuthentication
```

---

# Module 4: Session Authentication

Browser-এর জন্য।

Flow

```
Login

↓

Session তৈরি

↓

Session ID Cookie

↓

Browser Cookie পাঠায়

↓

Server User চিনে ফেলে
```

---

এটা Django Admin-এর মতো app-এর জন্য ভালো।

REST API-এর জন্য সাধারণত কম ব্যবহার করা হয়।

---

# Module 5: Basic Authentication

Client

```
username

password
```

প্রতি request-এ পাঠায়।

Header

```
Authorization:

Basic xxxxxxxxx
```

Production-এ খুব কম ব্যবহার হয়।

---

# Module 6: Token Authentication

Login

↓

Server

↓

```
abc123xyz
```

Token দেয়।

---

পরের request

```
Authorization

Token abc123xyz
```

Server

↓

User খুঁজে পায়।

---

Problem

একটাই Token।

Expire করে না।

Large project-এ কম ব্যবহার হয়।

---

# Module 7: JWT Authentication

সবচেয়ে popular।

Flow

```
Login

↓

Access Token

+

Refresh Token
```

---

Example

```
Access

↓

15 minutes
```

```
Refresh

↓

7 days
```

---

Request

```
Authorization

Bearer eyJhb...
```

---

Server

Token verify করে।

Database-এ না গিয়েও অনেক তথ্য decode করতে পারে।

---

JWT-এর ভিতরে

```
user_id

exp

iat

token_type
```

থাকে।

---

# Module 8: Permission Classes

সবচেয়ে important।

Allow সবাই

```python
permission_classes = [
    AllowAny
]
```

---

Login user

```python
permission_classes = [
    IsAuthenticated
]
```

---

Anonymous only

```
Custom লাগবে।
```

---

Admin only

```python
permission_classes = [
    IsAdminUser
]
```

---

Read সবাই

Write শুধু login

```python
permission_classes = [
    IsAuthenticatedOrReadOnly
]
```

---

# Permission Flow

Request

↓

Authentication

↓

User পাওয়া গেল

↓

Permission Check

↓

Allowed?

↓

View

---

# Module 9: Object Level Permission

Suppose

Blog

Owner

```
Atiar
```

---

Another User

```
Rahim
```

---

Rahim

```
DELETE

/blog/5/
```

Should fail.

---

Object Permission

```python
def has_object_permission(
    self,
    request,
    view,
    obj
):
```

Example

```python
return obj.owner == request.user
```

---

এটাই production standard।

---

# Module 10: Custom Permission

সবচেয়ে common।

```python
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.owner == request.user
```

View

```python
permission_classes = [
    IsOwner
]
```

---

আরেকটা

Admin

or

Owner

```python
return (

    request.user.is_staff

    or

    obj.owner == request.user

)
```

---

# Module 11: Dynamic Permission

ViewSet

```python
def get_permissions(self):

    if self.action=="list":

        return [AllowAny()]

    if self.action=="destroy":

        return [IsAdminUser()]

    return [IsAuthenticated()]
```

Production-এ খুব common।

---

# Module 12: Authentication + Permission Flow

Full Flow

```
Request

↓

Authentication

↓

request.user

↓

Permission

↓

Object Permission

↓

Serializer

↓

Response
```

---

খেয়াল করো

Permission fail করলে

Serializer

কখনো run হবে না।

---

# Module 13: Security Best Practices

## Never Trust Client

Bad

```python
serializer.save(
    owner=request.data["owner"]
)
```

Client

```
owner=1
```

দিয়ে অন্য user-এর নামে data বানাতে পারে।

---

Correct

```python
serializer.save(
    owner=request.user
)
```

---

## Hide Sensitive Fields

Never

```python
password
```

Response-এ পাঠিও না।

---

## Validate Everything

Never

```
Frontend validate করেছে

তাই backend লাগবে না।
```

Wrong.

Backend

Always validate.

---

## Permission First

Never

```python
Blog.objects.get(...)
```

তারপর permission।

Use

```python
self.get_object()
```

---

## Don't Expose All Methods

যদি শুধু GET লাগে

```python
http_method_names = [
    "get"
]
```

---

# Module 14: Authentication vs Permission

Authentication

↓

```
Who are you?
```

Permission

↓

```
Can you do this?
```

Object Permission

↓

```
Can you access THIS object?
```

---

# Real Project Example

```python
class BlogViewSet(ModelViewSet):

    queryset = Blog.objects.all()

    serializer_class = BlogSerializer

    authentication_classes = [

        JWTAuthentication

    ]

    permission_classes = [

        IsAuthenticated
    ]

    def perform_create(

        self,

        serializer

    ):

        serializer.save(

            owner=self.request.user
        )
```

---

# Common Mistakes

### ❌

Login user

↓

Owner request.data থেকে নেওয়া।

---

### ❌

Permission serializer-এর ভিতরে check করা।

Permission belongs in Permission Classes.

---

### ❌

সব action-এর জন্য একই permission।

Use

```
get_permissions()
```

---

### ❌

Object Permission না লেখা।

যার ফলে সবাই সবার data edit করতে পারে।

---

### ❌

JWT Access Token অনেক বেশি সময় valid রাখা।

---

# Interview Questions

1. Authentication এবং Authorization-এর পার্থক্য কী?
2. DRF request lifecycle-এ Authentication আগে না Permission?
3. Session Authentication এবং JWT-এর পার্থক্য কী?
4. `IsAuthenticatedOrReadOnly` কীভাবে কাজ করে?
5. `has_permission()` এবং `has_object_permission()`-এর পার্থক্য কী?
6. `get_permissions()` override কেন করবে?
7. কেন `serializer.save(owner=request.user)` নিরাপদ?
8. Object-level permission কখন check হয়?

---

# Senior Developer Notes

Production-এ আমি সাধারণত এই pattern অনুসরণ করি:

* **Authentication** → JWT
* **Authorization** → Permission classes
* **Object access** → Custom object permission
* **Ownership** → `perform_create()`-এ `request.user`
* **Per-action rules** → `get_permissions()`
* **Sensitive operations** (`delete`, `publish`, `approve`) → আলাদা permission class
* **Never trust client-provided ownership or role data**

---

# তোমার বর্তমান DRF লেভেল

এখন তুমি শিখেছ:

* ✅ Serializer
* ✅ GenericAPIView
* ✅ Mixins
* ✅ Generic Views
* ✅ ViewSet
* ✅ ModelViewSet
* ✅ Router
* ✅ `@action`
* ✅ Filtering
* ✅ Search
* ✅ Ordering
* ✅ Pagination
* ✅ Query Optimization
* ✅ Authentication
* ✅ Permissions
* ✅ Object Permissions
* ✅ Security Basics

---

# পরবর্তী লেসন (Senior DRF - Must Know)

এখন আমি যে বিষয়টি শেখাব, সেটি **সিনিয়র Django Backend Developer**-দের জন্য অত্যন্ত গুরুত্বপূর্ণ:

> **Transactions + Concurrency + Database Consistency**

এখানে আমরা গভীরভাবে শিখব:

* `transaction.atomic()` internals
* Nested transactions
* Savepoints
* Race conditions
* `select_for_update()`
* Optimistic vs Pessimistic locking
* Idempotency
* Double payment/order prevention
* Production concurrency patterns

এটি বড়-scale backend systems (যেমন ই-কমার্স, ব্যাংকিং, পেমেন্ট, ইনভেন্টরি) তৈরির জন্য অপরিহার্য।
এখন আমরা এমন একটি বিষয় শিখব যা **Senior Backend Developer**-দের আলাদা করে।

> তুমি আগে `transaction.atomic()` সম্পর্কে জিজ্ঞেস করেছিলে। আজ সেটা **zero → senior** শিখব।

---

# Lesson 7: Transactions + Concurrency + Database Consistency

> **Goal:** এমন API বানানো যা একসাথে হাজার request এলেও ভুল data save করবে না।

---

# Roadmap

```text
Module 1  : What is a Transaction?
Module 2  : ACID Properties
Module 3  : transaction.atomic()
Module 4  : Nested Transactions & Savepoints
Module 5  : Race Conditions
Module 6  : select_for_update()
Module 7  : Optimistic vs Pessimistic Locking
Module 8  : F() Expressions
Module 9  : Idempotency
Module 10 : Real Project Examples
Module 11 : Common Mistakes
Module 12 : Interview Questions
```

---

# Module 1: What is a Transaction?

ধরো একজন user Order করলো।

তোমার API-তে তিনটা কাজ হবে।

```text
1. Order তৈরি হবে

2. Stock কমবে

3. Payment Save হবে
```

Code

```python
order = Order.objects.create(...)

product.stock -= 1
product.save()

Payment.objects.create(...)
```

এখন ভাবো

Order save হলো।

Stock save হলো।

Payment save করার সময় error হলো।

Database

```text
Order ✔

Stock ✔

Payment ❌
```

Database inconsistent হয়ে গেল।

---

## Solution

Transaction

```text
সব সফল

অথবা

সব rollback
```

এটাই transaction।

---

# Module 2: ACID

Interview favourite।

## A

Atomicity

```text
All

or

Nothing
```

---

## C

Consistency

Database সব rule maintain করবে।

Example

```text
Stock

Never negative
```

---

## I

Isolation

এক user-এর transaction

অন্য user-এর transaction-এর সাথে interfere করবে না।

---

## D

Durability

Commit হয়ে গেলে

Server restart হলেও data থাকবে।

---

# Module 3: transaction.atomic()

Example

```python
from django.db import transaction

@transaction.atomic
def create_order(request):

    order = Order.objects.create(...)

    payment = Payment.objects.create(...)

    product.stock -= 1

    product.save()
```

---

ধরো

```python
payment = Payment.objects.create(...)
```

এখানে exception হলো।

কি হবে?

```text
Order ❌

Stock ❌

Payment ❌
```

সব rollback।

---

Context Manager

```python
from django.db import transaction

def checkout():

    with transaction.atomic():

        ...
```

Decorator আর Context Manager—দুটোই ঠিক।

---

# Module 4: Nested Transactions

```python
with transaction.atomic():

    ...

    with transaction.atomic():

        ...
```

DRF/Django এখানে **savepoint** ব্যবহার করে।

Flow

```text
Outer Transaction

↓

Savepoint

↓

Inner Transaction
```

---

যদি inner fail করে

```text
Inner

Rollback

↓

Outer

চলতে পারে
```

---

# Module 5: Race Condition

সবচেয়ে dangerous।

Stock

```text
1
```

একই সময়ে

Rahim

↓

Buy

আর

Karim

↓

Buy

দুজনই পড়লো

```text
stock=1
```

দুজনই save করলো

শেষে

```text
-1
```

Inventory নষ্ট।

---

# Module 6: select_for_update()

Solution

```python
with transaction.atomic():

    product = Product.objects.select_for_update().get(id=1)

    if product.stock == 0:
        raise ValidationError()

    product.stock -= 1

    product.save()
```

---

কি হলো?

Rahim

↓

Lock

↓

Update

↓

Commit

↓

Unlock

---

Karim

↓

Wait

↓

তারপর নতুন stock পড়বে।

Race condition শেষ।

---

# Module 7: Optimistic vs Pessimistic Locking

## Pessimistic

```python
select_for_update()
```

Database lock করে।

---

## Optimistic

Lock করে না।

শেষে check করে

Version change হয়েছে?

Example

```text
version=3
```

Save করার সময়

```text
WHERE version=3
```

যদি version 4 হয়ে যায়

↓

Conflict।

---

Django-তে সাধারণত

```text
select_for_update()
```

বেশি common।

---

# Module 8: F() Expressions

Junior

```python
product.stock -= 1
product.save()
```

Danger।

---

Senior

```python
from django.db.models import F

Product.objects.filter(id=1).update(

    stock=F("stock") - 1
)
```

Database

নিজেই

```sql
UPDATE product

SET stock = stock - 1
```

একটা query।

Safe।

Fast।

---

Increment

```python
views = F("views") + 1
```

---

# Module 9: Idempotency

Payment API

User

Double Click

```text
Pay

Pay
```

দুইটা payment?

না।

---

Idempotency

মানে

```text
একই request

১০ বার এলেও

একবারই effect হবে।
```

Stripe-এর মতো payment gateway-তে এটা খুব গুরুত্বপূর্ণ।

---

Simple Example

```python
if Payment.objects.filter(

    order=order

).exists():

    return
```

Better

Unique key

```text
Idempotency-Key
```

---

# Module 10: Real Project

Checkout

```python
@transaction.atomic
def checkout(request):

    product = Product.objects.select_for_update().get(

        id=request.data["product"]
    )

    if product.stock <= 0:

        raise ValidationError("Out of stock")

    product.stock -= 1

    product.save()

    order = Order.objects.create(

        ...

    )

    Payment.objects.create(

        ...

    )
```

সব safe।

---

# Inventory Update

Bad

```python
product.stock -= qty

product.save()
```

---

Better

```python
Product.objects.filter(

    id=id

).update(

    stock=F("stock") - qty
)
```

---

# Bank Transfer

```text
Account A

↓

-100

↓

Account B

↓

+100
```

Transaction না থাকলে

একদিকে টাকা কমলো

অন্যদিকে বাড়লো না।

---

# Module 11: Common Mistakes

## ❌

Long transaction।

Bad

```python
with transaction.atomic():

    call_external_api()

    send_email()

    generate_pdf()

    save()
```

Transaction যত ছোট হয় তত ভালো।

External API call transaction-এর বাইরে রাখো যদি সম্ভব হয়।

---

## ❌

`select_for_update()` ছাড়া inventory update।

---

## ❌

Python দিয়ে increment।

Use

```text
F()
```

---

## ❌

Payment-এ idempotency না রাখা।

---

## ❌

Transaction-এর ভিতরে unnecessary query।

---

# Interview Questions

1. Transaction কী?
2. ACID কী?
3. `transaction.atomic()` কী করে?
4. Race condition কী?
5. `select_for_update()` কেন ব্যবহার করা হয়?
6. `F()` expression কেন safer?
7. Optimistic vs Pessimistic locking-এর পার্থক্য কী?
8. Idempotency কী?
9. Nested transaction কীভাবে কাজ করে?
10. Long transaction কেন সমস্যা?

---

# Senior Developer Checklist

Checkout API লিখলে আমি সাধারণত এই sequence অনুসরণ করি:

```text
Validate Input

↓

transaction.atomic()

↓

select_for_update()

↓

Business Validation

↓

Update Stock

↓

Create Order

↓

Create Payment Record

↓

Commit

↓

Send Email (after commit)
```

**খেয়াল করো:** Email, notification, webhook, বা external API call সাধারণত commit-এর **পরে** করা ভালো। কারণ transaction rollback হলে user-কে ভুল email বা notification চলে যেতে পারে।

---

# একটি গুরুত্বপূর্ণ Production Pattern

Django-তে commit সফল হওয়ার পরে কাজ চালাতে পারো:

```python
from django.db import transaction

with transaction.atomic():
    order = Order.objects.create(...)

    transaction.on_commit(
        lambda: send_order_confirmation(order.id)
    )
```

এখানে `send_order_confirmation()` তখনই চলবে যখন transaction সফলভাবে commit হবে।

---

# এখন তোমার DRF / Django Backend Skill Set

এখন পর্যন্ত তুমি শিখেছ:

* ✅ Serializer
* ✅ GenericAPIView
* ✅ Mixins
* ✅ Generic Views
* ✅ ViewSet / ModelViewSet
* ✅ Router
* ✅ `@action`
* ✅ Filtering / Search / Ordering / Pagination
* ✅ Query Optimization
* ✅ Authentication & Permissions
* ✅ Transactions
* ✅ Concurrency
* ✅ `select_for_update()`
* ✅ `F()` Expressions
* ✅ Idempotency

---

# এখন পরবর্তী ধাপ কী?

এখন আর DRF-এর আলাদা feature নয়—**বড় application architecture** শেখার সময়।

আমি পরবর্তী লেসনে শেখাব:

> **Senior Django Project Architecture**

সেখানে আমরা শিখব:

* Fat Views vs Thin Views
* Service Layer Pattern
* Repository Pattern (কখন দরকার, কখন নয়)
* Business Logic কোথায় থাকবে?
* Serializer-এর দায়িত্ব কী?
* Model-এর দায়িত্ব কী?
* Signals কখন ব্যবহার করবে?
* Utility vs Service vs Manager
* Large project folder structure
* Testing-friendly architecture

এটি এমন একটি বিষয় যা একজন mid-level developer-কে senior mindset-এর দিকে নিয়ে যায়।
এখন থেকে আমরা **Senior Backend Architecture**-এ ঢুকছি।

এটাই সেই জায়গা যেখানে একজন **Junior** আর **Senior** Developer-এর মধ্যে সবচেয়ে বড় পার্থক্য দেখা যায়।

> **একজন Junior Django জানে। একজন Senior Django দিয়ে maintainable software বানায়।**

---

# Lesson 8: Senior Django Project Architecture (Zero → Senior)

---

# Roadmap

```text
Module 1  : MVC vs MVT vs DRF Architecture
Module 2  : Responsibilities (Model, Serializer, View)
Module 3  : Fat View vs Thin View
Module 4  : Service Layer
Module 5  : Model Methods & Custom Managers
Module 6  : Signals
Module 7  : Utilities vs Services vs Helpers
Module 8  : Large Project Folder Structure
Module 9  : Clean Architecture Rules
Module 10 : Real E-commerce Example
Module 11 : Common Mistakes
Module 12 : Interview Questions
```

---

# Module 1: DRF Architecture

অনেকেই মনে করে Flow এমন:

```text
Client
↓
View
↓
Serializer
↓
Model
↓
Database
```

আসলে Production Flow সাধারণত এমন হয়:

```text
Client
↓
ViewSet
↓
Serializer (Validation)
↓
Service Layer (Business Logic)
↓
Model / Manager
↓
Database
```

**Rule**

* Serializer = Data validation
* Service = Business logic
* Model = Data representation
* View = HTTP handling

---

# Module 2: কার দায়িত্ব কী?

## View-এর কাজ

View-এর কাজ **business logic লেখা না**।

ভালো View

```python
class OrderViewSet(ModelViewSet):

    def perform_create(self, serializer):
        OrderService.create_order(
            serializer.validated_data,
            self.request.user
        )
```

View শুধু request handle করবে।

---

## Serializer-এর কাজ

Serializer-এর কাজ

```text
Validate

Convert

Serialize

Deserialize
```

Example

```python
class ProductSerializer(serializers.ModelSerializer):

    def validate_price(self, value):
        if value <= 0:
            raise serializers.ValidationError()

        return value
```

এখানে validation থাকবে।

Business rule না।

---

## ভুল উদাহরণ

```python
class OrderSerializer(serializers.ModelSerializer):

    def create(self, validated_data):

        payment = Payment(...)

        send_email()

        create_invoice()

        update_inventory()

        notify_admin()

        ...
```

এটা Serializer-এর কাজ না।

---

# Module 3: Fat View vs Thin View

## Junior Style

```python
class OrderViewSet(ModelViewSet):

    def create(self, request):

        ...

        validate()

        check_stock()

        calculate_discount()

        calculate_tax()

        create_order()

        create_payment()

        send_email()

        notify_admin()

        log()

        analytics()

        ...
```

৫০০ লাইনের View।

Maintain করা কঠিন।

---

## Senior Style

```python
class OrderViewSet(ModelViewSet):

    def perform_create(self, serializer):

        OrderService.create_order(
            serializer.validated_data,
            self.request.user
        )
```

মাত্র ৫-১০ লাইন।

---

# Module 4: Service Layer

এটাই Senior Pattern।

Structure

```text
orders/

    services.py
```

Example

```python
class OrderService:

    @staticmethod
    def create_order(data, user):

        ...

        validate_stock()

        create_order()

        create_payment()

        update_inventory()

        return order
```

---

View

```python
OrderService.create_order(...)
```

---

Advantage

```text
Reusable

Easy testing

Readable

Maintainable
```

---

# Module 5: Model Methods

যদি logic শুধু Model-এর হয়

তাহলে

Model Method

Example

```python
class Product(models.Model):

    stock=models.IntegerField()

    def is_available(self):

        return self.stock>0
```

View

```python
if product.is_available():
```

Clean।

---

## Custom Manager

Suppose

সব active product

বারবার

```python
Product.objects.filter(
    active=True
)
```

লিখছো।

Better

```python
class ProductManager(models.Manager):

    def active(self):

        return self.filter(active=True)
```

Model

```python
objects = ProductManager()
```

Use

```python
Product.objects.active()
```

---

# Module 6: Signals

Signals powerful।

কিন্তু abuse হয়।

---

Good

```text
Create User

↓

Send Welcome Email
```

---

Bad

```text
Order Created

↓

Update Inventory

↓

Payment

↓

Invoice

↓

Analytics

↓

SMS

↓

Webhook

↓

...
```

সব Signal-এ।

Debug করা কঠিন।

---

Rule

Signal

↓

Small Side Effects

Business Logic না।

---

# Module 7: Utility vs Service

Utility

```python
calculate_age()

slugify()

generate_token()
```

Generic function।

---

Service

```python
create_order()

refund_payment()

publish_blog()
```

Business logic।

---

Helper

ছোট reusable helper।

---

# Module 8: Folder Structure

Small Project

```text
products/

    models.py

    views.py

    serializers.py
```

---

Large Project

```text
products/

    models.py

    serializers.py

    permissions.py

    filters.py

    pagination.py

    services.py

    selectors.py

    managers.py

    signals.py

    tasks.py

    validators.py

    tests/
```

এটাই Production Pattern।

---

# Module 9: Selectors Pattern

অনেক কোম্পানি

Selector ব্যবহার করে।

Example

```python
ProductSelector.get_active_products()
```

এর ভিতরে

```python
select_related()

prefetch_related()

annotate()
```

সব optimize করা থাকে।

View

```python
queryset = ProductSelector.get_active_products()
```

খুব clean।

---

# Module 10: Real E-commerce Flow

Checkout

```text
Request

↓

Serializer

↓

Validation

↓

OrderService.checkout()

↓

transaction.atomic()

↓

InventoryService

↓

PaymentService

↓

OrderManager

↓

Database

↓

Response
```

দেখো

View কিছুই করছে না।

---

# Module 11: Clean Architecture Rules

### Rule 1

View

↓

HTTP

---

### Rule 2

Serializer

↓

Validation

---

### Rule 3

Service

↓

Business Logic

---

### Rule 4

Model

↓

Data

---

### Rule 5

Manager

↓

Common Queries

---

### Rule 6

Permission

↓

Authorization

---

### Rule 7

Filter

↓

Filtering

---

### Rule 8

Pagination

↓

Pagination 😄

---

# Module 12: Common Mistakes

## ❌

1000 লাইনের View।

---

## ❌

Business Logic Serializer-এ।

---

## ❌

সব Model Method-এ।

---

## ❌

Signal দিয়ে পুরো Application চালানো।

---

## ❌

Utility নামে 5000 লাইনের file।

---

## ❌

Circular import

```text
views

↓

services

↓

views
```

---

# Interview Questions

1. Service Layer কেন দরকার?
2. Business Logic কোথায় রাখবে?
3. Serializer-এর responsibility কী?
4. Signal কখন ব্যবহার করবে?
5. Model Method এবং Service-এর পার্থক্য কী?
6. Manager কখন লিখবে?
7. Fat View কেন খারাপ?
8. Thin View-এর সুবিধা কী?

---

# Senior Decision Guide

প্রজেক্টে নতুন logic লিখতে হলে আমি সাধারণত এইভাবে সিদ্ধান্ত নিই:

| Logic                              | কোথায় রাখব?                        |
| ---------------------------------- | ----------------------------------- |
| Input validation                   | Serializer                          |
| Permission                         | Permission Class                    |
| Query optimization                 | Manager / Selector                  |
| Business workflow                  | Service                             |
| Object-specific behavior           | Model Method                        |
| Side effects (email, notification) | Signal বা `transaction.on_commit()` |
| HTTP response                      | View/ViewSet                        |

---

# বাস্তব উদাহরণ

ধরো "Order Cancel" feature।

**ভুল approach:**

```text
View
 ├─ Stock update
 ├─ Refund
 ├─ Email
 ├─ Notification
 ├─ Audit log
 └─ Analytics
```

**ভালো approach:**

```text
View
   ↓
OrderService.cancel_order()
   ├─ RefundService
   ├─ InventoryService
   ├─ AuditService
   └─ transaction.on_commit() → Email
```

এতে প্রতিটি component আলাদা test করা যায় এবং code maintain করা সহজ হয়।

---

# তোমার বর্তমান লেভেল

এখন পর্যন্ত আমরা cover করেছি:

* ✅ Serializers
* ✅ GenericAPIView
* ✅ Mixins
* ✅ Generic Views
* ✅ ViewSets
* ✅ Routers
* ✅ `@action`
* ✅ Filtering / Search / Pagination
* ✅ Authentication & Permissions
* ✅ Transactions & Concurrency
* ✅ Senior Project Architecture

---

# এখন কী শেখা উচিত?

এখন আমি যে বিষয়টি শেখাব সেটি একজন **Senior Django REST Framework Developer**-এর জন্য অত্যন্ত গুরুত্বপূর্ণ:

> **Advanced Serializer Internals (Zero → Source Code)**

এখানে আমরা গভীরভাবে শিখব:

* `to_internal_value()`
* `to_representation()`
* `run_validation()`
* `is_valid()` internals
* `create()` vs `update()`
* Nested serializer internals
* Writable nested serializers
* Bulk create/update
* `ListSerializer`
* Serializer performance optimization

এই অংশটি বুঝলে তুমি শুধু serializer ব্যবহার করবে না, **নিজের custom serializer framework-এর মতো code-ও লিখতে পারবে।**


দারুণ। এখন আমরা DRF-এর এমন একটি অংশে যাচ্ছি যা **প্রায় সব Senior Django Developer জানে**, কিন্তু অনেক Mid-level Developer পুরোপুরি বোঝে না।

> **Lesson 9: Serializer Internals (Zero → Source Code → Senior)**

এটি সম্ভবত **DRF-এর সবচেয়ে গুরুত্বপূর্ণ ক্লাস**।

---

# Roadmap

```text
Module 1  : Serializer Lifecycle
Module 2  : What happens when serializer = ProductSerializer(data=request.data)
Module 3  : is_valid() Internals
Module 4  : run_validation()
Module 5  : to_internal_value()
Module 6  : validate_<field>()
Module 7  : validate()
Module 8  : create() vs update()
Module 9  : serializer.save()
Module 10 : to_representation()
Module 11 : Nested Serializer
Module 12 : ListSerializer
Module 13 : Bulk Operations
Module 14 : Performance
Module 15 : Common Mistakes
Module 16 : Interview Questions
```

---

# Module 1: Serializer Lifecycle

ধরো request এসেছে

```http
POST /products/
```

Body

```json
{
    "name": "iPhone",
    "price": 1000
}
```

View

```python
serializer = ProductSerializer(data=request.data)

serializer.is_valid()

serializer.save()
```

**এই ৩ লাইনের ভিতরে কী হয়?**

পুরো Flow

```text
request.data

↓

Serializer()

↓

to_internal_value()

↓

Field Validation

↓

validate_<field>()

↓

validate()

↓

validated_data

↓

create()

↓

Model.save()

↓

instance

↓

to_representation()

↓

Response
```

এটাই DRF Serializer-এর complete lifecycle।

---

# Module 2: Serializer Initialization

```python
serializer = ProductSerializer(
    data=request.data
)
```

এখানে এখনও

```text
Validation হয়নি

Database save হয়নি

Model create হয়নি
```

শুধু serializer object তৈরি হয়েছে।

---

# Module 3: is_valid()

এটাই serializer-এর heart।

```python
serializer.is_valid()
```

Internally (simplified)

```python
def is_valid(self):

    self._validated_data = self.run_validation(
        self.initial_data
    )

    return True
```

অর্থাৎ

```text
is_valid()

↓

run_validation()
```

---

# Module 4: run_validation()

এটা DRF-এর main validation method।

Flow

```text
run_validation()

↓

to_internal_value()

↓

Field Validators

↓

validate_<field>()

↓

validate()

↓

validated_data
```

---

# Module 5: to_internal_value()

এটা খুব important।

Input

```json
{
    "price":"100"
}
```

Database

```python
price = models.IntegerField()
```

DRF

```text
"100"

↓

100
```

String → Integer convert করে।

এটাই

```python
to_internal_value()
```

---

আরেকটা example

Input

```json
{
    "is_active":"true"
}
```

↓

```python
True
```

---

তাই

**Input Parsing**

=

```text
to_internal_value()
```

---

# Module 6: validate_()

Example

```python
class ProductSerializer(serializers.ModelSerializer):

    def validate_price(self, value):

        if value <= 0:

            raise serializers.ValidationError(
                "Price must be positive."
            )

        return value
```

Flow

```text
price

↓

validate_price()

↓

return value
```

এটা **একটি field** validate করে।

---

# Module 7: validate()

যখন

একাধিক field একসাথে check করতে হবে।

Example

```python
class ProductSerializer(serializers.ModelSerializer):

    def validate(self, attrs):

        if attrs["sale_price"] > attrs["price"]:

            raise serializers.ValidationError(
                "Invalid sale price."
            )

        return attrs
```

এখানে

দুটি field একসাথে compare করছি।

---

Rule

```text
Single Field

↓

validate_<field>()
```

```text
Multiple Fields

↓

validate()
```

---

# Module 8: create() vs update()

Serializer

```python
serializer.save()
```

Internally

যদি

```python
instance=None
```

↓

```python
create()
```

---

যদি

```python
instance=product
```

↓

```python
update()
```

---

Example

```python
serializer = ProductSerializer(
    data=request.data
)
```

↓

Create

---

Example

```python
serializer = ProductSerializer(

    product,

    data=request.data
)
```

↓

Update

---

# Module 9: serializer.save()

Source (simplified)

```python
def save(self):

    if self.instance is None:

        self.instance = self.create(
            self.validated_data
        )

    else:

        self.instance = self.update(
            self.instance,
            self.validated_data
        )

    return self.instance
```

এটাই পুরো magic।

---

# Module 10: to_representation()

সবচেয়ে important।

Database

```python
Product

↓

name="iPhone"

price=100
```

↓

JSON

```json
{
    "name":"iPhone",

    "price":100
}
```

এই conversion

কোথায়?

↓

```python
to_representation()
```

---

মানে

```text
Database

↓

JSON
```

---

যখন

```python
serializer.data
```

করো

↓

```python
to_representation()
```

call হয়।

---

# Module 11: Nested Serializer

Example

```python
class CategorySerializer(...):
```

```python
class ProductSerializer(

    serializers.ModelSerializer
):

    category = CategorySerializer()
```

Output

```json
{
    "name":"iPhone",

    "category":{

        "id":1,

        "name":"Phone"
    }
}
```

Nested serializer

---

Production Note

Nested serializer ব্যবহার করলে query optimize করতে হবে:

```python
queryset = Product.objects.select_related("category")
```

নইলে N+1 Query Problem হতে পারে।

---

# Module 12: ListSerializer

ধরো

```python
many=True
```

```python
ProductSerializer(

    products,

    many=True
)
```

Internally

DRF

```text
ListSerializer

↓

ProductSerializer

↓

ProductSerializer

↓

ProductSerializer
```

প্রত্যেক object-এর জন্য child serializer ব্যবহার করে।

---

# Module 13: Bulk Create

Default

```python
for item in data:

    serializer.save()
```

১০০০ query।

---

Better

Custom ListSerializer

```python
class ProductListSerializer(
    serializers.ListSerializer
):

    def create(
        self,
        validated_data
    ):

        objs = [

            Product(**item)

            for item in validated_data
        ]

        return Product.objects.bulk_create(objs)
```

একটা query।

---

# Module 14: Performance

## Use select_related()

Nested serializer

↓

```python
select_related()
```

---

## Use prefetch_related()

ManyToMany

↓

```python
prefetch_related()
```

---

## Avoid SerializerMethodField

যদি

Database hit করে।

Bad

```python
def get_orders(...)
```

ভিতরে query।

---

Better

```python
annotate()
```

---

## Read Serializer

↓

Minimal fields।

---

## Write Serializer

↓

Validation only।

---

# Common Mistakes

### ❌ Business Logic

Serializer-এর ভিতরে payment, email, notification।

না।

ওগুলো Service Layer-এ।

---

### ❌ Calling save()

Without

```python
is_valid()
```

Never।

---

### ❌ Doing DB query

Inside

```python
SerializerMethodField
```

বারবার।

---

### ❌ Overriding create()

কিন্তু

```python
super()
```

logic না বোঝা।

---

### ❌ Returning model instance

Inside validate()

ভুল।

`validate()`-এ সবসময় `attrs` return করবে।

---

# Interview Questions

1. `serializer.is_valid()` internally কী করে?
    
2. `run_validation()`-এর কাজ কী?
    
3. `to_internal_value()` এবং `to_representation()`-এর পার্থক্য কী?
    
4. `validate_<field>()` বনাম `validate()`?
    
5. `serializer.save()` কীভাবে `create()` বা `update()` decide করে?
    
6. `many=True` হলে কোন class ব্যবহার হয়?
    
7. Nested serializer-এর performance issue কী?
    
8. `SerializerMethodField` কখন সমস্যা তৈরি করতে পারে?
    

---

# Senior Developer Patterns

## 1. আলাদা Read ও Write Serializer

```python
class ProductReadSerializer(...):
    ...

class ProductWriteSerializer(...):
    ...
```

তারপর ViewSet-এ:

```python
def get_serializer_class(self):
    if self.action in ["list", "retrieve"]:
        return ProductReadSerializer
    return ProductWriteSerializer
```

---

## 2. Business Logic Serializer-এ নয়

```python
serializer.is_valid(raise_exception=True)
OrderService.create_order(
    serializer.validated_data,
    request.user
)
```

---

## 3. Serializer Context

যদি serializer-এর ভিতরে `request` দরকার হয়:

```python
request = self.context["request"]
```

কারণ `GenericAPIView.get_serializer()` স্বয়ংক্রিয়ভাবে context পাঠায়।

---

# এখন তোমার DRF Knowledge

তুমি এখন শিখেছ:

- ✅ APIView
    
- ✅ GenericAPIView
    
- ✅ Mixins
    
- ✅ Generic Views
    
- ✅ ViewSets
    
- ✅ Routers
    
- ✅ `@action`
    
- ✅ Filtering
    
- ✅ Pagination
    
- ✅ Authentication
    
- ✅ Permissions
    
- ✅ Transactions
    
- ✅ Project Architecture
    
- ✅ Serializer Internals
    

---

# আমার মতে এখন সবচেয়ে গুরুত্বপূর্ণ পরবর্তী লেসন

এখন **Testing** শেখা উচিত।

কারণ একজন Senior Django Developer শুধু feature লেখে না, **feature verify-ও করে**।

পরবর্তী লেসনে আমরা শিখব:

- Unit Test
    
- API Test
    
- Serializer Test
    
- Permission Test
    
- Authentication Test
    
- Factory Boy
    
- Mocking
    
- `APITestCase`
    
- `APIClient`
    
- Coverage
    
- Production testing strategy
    

এটি এমন একটি skill যা internship থেকে senior engineer—সব লেভেলেই খুব মূল্যবান।


----
চমৎকার। এখন আমরা এমন একটি বিষয় শিখব যেটা অনেক Django Developer এড়িয়ে যায়, কিন্তু **Professional Backend Developer**-দের জন্য এটি বাধ্যতামূলক।

> **Lesson 10: Testing in Django REST Framework (Zero → Senior)**

একটি কথা মনে রাখবে:

> **"If it's not tested, you don't really know if it works."**

Google, Netflix, Stripe, GitHub—সব বড় কোম্পানিতে testing ছাড়া code merge হয় না।

---

# Roadmap

```text
Module 1  : Why Testing?
Module 2  : Types of Testing
Module 3  : Django Test Lifecycle
Module 4  : APITestCase
Module 5  : APIClient
Module 6  : Testing CRUD APIs
Module 7  : Authentication Tests
Module 8  : Permission Tests
Module 9  : Serializer Tests
Module 10 : Mocking
Module 11 : Factory Pattern
Module 12 : Coverage
Module 13 : Common Mistakes
Module 14 : Interview Questions
```

---

# Module 1: Why Testing?

ধরো তুমি Product API লিখেছো।

আজ ঠিকভাবে কাজ করছে।

কাল নতুন feature যোগ করলে

হঠাৎ

```text
Product Create ✔

Product Update ❌

Product Delete ✔
```

Update ভেঙে গেল।

Testing থাকলে

৫ সেকেন্ডে বুঝে যাবে।

Testing না থাকলে

Production-এ User report করবে।

---

# Module 2: Testing Pyramid

```text
                E2E Tests
             (Few, Expensive)

            Integration Tests

         Unit Tests (Most, Fast)
```

DRF-এ আমরা সাধারণত

- Unit Test
    
- Integration/API Test
    

বেশি লিখি।

---

# Module 3: Django Test Lifecycle

যখন তুমি

```bash
python manage.py test
```

চালাও

Django

```text
Create Test Database

↓

Run Tests

↓

Rollback/Cleanup

↓

Delete Test Database
```

তাই Test-এর data

Real Database-এ যায় না।

---

# Module 4: APITestCase

DRF-এর সবচেয়ে common test class।

```python
from rest_framework.test import APITestCase

class ProductAPITest(APITestCase):

    def test_product_list(self):
        ...
```

এতে DRF-এর API testing helper পাওয়া যায়।

---

# Module 5: APIClient

সবচেয়ে বেশি ব্যবহৃত object।

```python
response = self.client.get("/api/products/")
```

POST

```python
response = self.client.post(
    "/api/products/",
    {
        "name": "iPhone",
        "price": 1000
    },
    format="json"
)
```

PUT

```python
self.client.put(...)
```

PATCH

```python
self.client.patch(...)
```

DELETE

```python
self.client.delete(...)
```

---

# Module 6: CRUD Test

ধরো

Product Create

```python
class ProductCreateTest(APITestCase):

    def test_create_product(self):

        response = self.client.post(
            "/api/products/",
            {
                "name": "Laptop",
                "price": 1000
            },
            format="json"
        )

        self.assertEqual(
            response.status_code,
            201
        )
```

---

List Test

```python
response = self.client.get("/api/products/")

self.assertEqual(
    response.status_code,
    200
)
```

---

Delete Test

```python
response = self.client.delete(
    "/api/products/1/"
)

self.assertEqual(
    response.status_code,
    204
)
```

---

# শুধু Status Code Test করবে?

না।

Data-ও test করবে।

```python
self.assertEqual(
    response.data["name"],
    "Laptop"
)
```

---

Database

```python
self.assertEqual(
    Product.objects.count(),
    1
)
```

---

# Module 7: Authentication Test

User

```python
user = User.objects.create_user(
    username="atiar",
    password="123"
)
```

Login

```python
self.client.force_authenticate(
    user=user
)
```

এখন সব request

Authenticated।

---

Without Login

```python
response = self.client.get(
    "/api/orders/"
)

self.assertEqual(
    response.status_code,
    401
)
```

---

With Login

```python
self.client.force_authenticate(user)

response = self.client.get(...)

self.assertEqual(
    response.status_code,
    200
)
```

---

# Module 8: Permission Test

ধরো

Owner

```text
Atiar
```

Rahim

Delete করতে চাইলো।

```python
self.client.force_authenticate(
    rahim
)

response = self.client.delete(...)

self.assertEqual(
    response.status_code,
    403
)
```

Owner

```python
self.client.force_authenticate(
    atiar
)

response = self.client.delete(...)

204
```

---

# Module 9: Serializer Test

অনেকে API দিয়ে serializer test করে।

Senior Developer

Serializer আলাদা test করে।

```python
serializer = ProductSerializer(
    data={
        "name":"Phone",

        "price":100
    }
)

self.assertTrue(
    serializer.is_valid()
)
```

Invalid

```python
serializer = ProductSerializer(
    data={
        "price":-5
    }
)

self.assertFalse(
    serializer.is_valid()
)
```

---

Validation Error

```python
self.assertIn(
    "price",
    serializer.errors
)
```

---

# Module 10: Mocking

Suppose

Order create করলে

Email যায়।

Real Email পাঠাবে?

না।

Use

```python
from unittest.mock import patch
```

```python
@patch(
    "orders.services.send_email"
)
def test_create_order(
    self,
    mock_email
):

    ...

    mock_email.assert_called_once()
```

Real Email যাবে না।

---

# Module 11: Factory Pattern

Junior

```python
User.objects.create(...)

Product.objects.create(...)

Category.objects.create(...)
```

প্রতিটি test-এ।

---

Better

Factory

```python
product = ProductFactory()
```

সব data

Automatically।

Production-এ

**Factory Boy** খুব জনপ্রিয়।

---

# Module 12: Coverage

Run

```bash
coverage run manage.py test
```

Report

```bash
coverage report
```

Example

```text
orders/

95%

products/

92%

users/

98%
```

Target

```text
80%+
```

কিন্তু

**Meaningful coverage** বেশি গুরুত্বপূর্ণ।

---

# কী কী Test করবে?

প্রতিটি API-র জন্য কমপক্ষে:

### Happy Path

```text
ঠিক input
```

---

### Invalid Data

```text
Missing field

Negative price

Wrong email
```

---

### Unauthorized

```text
Without Login
```

---

### Forbidden

```text
Wrong User
```

---

### Edge Cases

```text
Empty List

Large Number

Duplicate

Out of Stock
```

---

### Database Effect

```text
Count

Updated Field

Deleted Row
```

---

# Real Project Folder

```text
products/

    tests/

        test_models.py

        test_serializers.py

        test_views.py

        test_permissions.py

        test_services.py
```

এক ফাইলে ২০০টা test রাখো না।

---

# Common Mistakes

### ❌ শুধু Status Code Test করা

ভুল।

Database-ও verify করো।

---

### ❌ API দিয়ে সব Test

Serializer, Service, Permission আলাদা test করো।

---

### ❌ External API Mock না করা

Payment API

Email API

SMS API

সব Mock করো।

---

### ❌ Test-এর মধ্যে Test-এর উপর dependency

প্রতিটি test independent হবে।

---

### ❌ Hardcoded IDs

Bad

```python
/api/products/1/
```

Better

```python
product.id
```

---

# Interview Questions

1. `APITestCase` এবং `TestCase`-এর পার্থক্য কী?
    
2. `force_authenticate()` কেন ব্যবহার করা হয়?
    
3. কেন Mock দরকার?
    
4. Serializer আলাদা test করবে কেন?
    
5. Permission কীভাবে test করবে?
    
6. Coverage 100% হলে কি bug থাকবে না?
    
7. Unit Test এবং Integration Test-এর পার্থক্য কী?
    
8. Happy Path এবং Edge Case-এর মধ্যে পার্থক্য কী?
    

---

# Senior Testing Strategy

আমি সাধারণত একটি feature-এর জন্য এইভাবে test লিখি:

|Layer|কী Test করব|
|---|---|
|Model|Model methods, managers|
|Serializer|Validation, serialization|
|Service|Business logic, transactions|
|Permission|Access rules|
|View/API|HTTP request/response|
|Integration|End-to-end flow (database সহ)|

---

# বাস্তব উদাহরণ: Order API

যদি `OrderService.checkout()` লিখি, তাহলে আমি আলাদা আলাদা test লিখব:

```text
test_checkout_success()

test_checkout_out_of_stock()

test_checkout_unauthorized()

test_checkout_invalid_quantity()

test_checkout_creates_order()

test_checkout_reduces_stock()

test_checkout_rollback_on_payment_error()
```

এভাবে প্রতিটি গুরুত্বপূর্ণ scenario cover হয়।

---

# এখন তোমার DRF Skill Set

এখন তুমি শিখেছ:

- ✅ DRF Architecture
    
- ✅ GenericAPIView
    
- ✅ Mixins
    
- ✅ ViewSets
    
- ✅ Routers
    
- ✅ Serializers (Internals)
    
- ✅ Authentication & Permissions
    
- ✅ Transactions & Concurrency
    
- ✅ Service Layer
    
- ✅ Testing
    

এগুলো একজন **ভালো Django REST Framework Developer**-এর core skills।

---

# এরপর কী?

এখন DRF-এর feature শেখার চেয়ে **Real Production Engineering** শেখা বেশি গুরুত্বপূর্ণ।

আমি পরবর্তী লেসনে শেখাব:

> **Caching + Redis + Celery + Background Tasks + Performance Engineering**

এখানে আমরা শিখব:

- Django Cache Framework
    
- Redis
    
- Celery
    
- Background jobs
    
- Cache invalidation
    
- Rate limiting
    
- Performance optimization
    
- Large-scale API patterns
    

এগুলো ছাড়া high-traffic production backend তৈরি করা কঠিন।

-----------
দারুণ। এখন আমরা Django Backend-এর এমন একটি অংশে যাচ্ছি যা **Mid-level → Senior** transition-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

> **Lesson 11: Caching + Redis + Celery + Background Tasks (Zero → Senior)**

**কিন্তু শুরুতেই একটি গুরুত্বপূর্ণ কথা:**

অনেকেই ভাবে—

> Redis = Cache

এটা **আংশিক সত্য**।

Redis শুধু cache নয়।

Redis ব্যবহার করা যায়—

- Cache
    
- Celery Broker
    
- Celery Result Backend
    
- Rate Limiting
    
- Distributed Lock
    
- Pub/Sub
    
- Session Storage
    

আজ সবগুলো পরিষ্কার হবে।

---

# Roadmap

```text
Module 1  : Why Caching?
Module 2  : Cache Types
Module 3  : Django Cache Framework
Module 4  : Redis
Module 5  : Cache Keys
Module 6  : Cache Invalidation
Module 7  : Celery
Module 8  : Message Broker
Module 9  : Background Tasks
Module 10 : Retry & Failure Handling
Module 11 : Real Project Examples
Module 12 : Common Mistakes
Module 13 : Interview Questions
```

---

# Module 1: Why Caching?

ধরো তোমার Product List API।

```python
GET /api/products/
```

Database-এ

```text
100,000 Products
```

প্রতি request-এ

```text
Client

↓

Database Query

↓

Serializer

↓

JSON

↓

Response
```

১০০০ User

↓

১০০০ Query

Database-এর উপর চাপ।

---

Solution

```text
Client

↓

Cache

↓

Response
```

Database-এ যাওয়ার দরকার নেই।

---

# Module 2: Cache Types

## 1. Per Site Cache

পুরো website cache।

---

## 2. Per View Cache

একটা API cache।

Example

```python
GET /products/
```

---

## 3. Low Level Cache

নিজে cache control করবে।

এটাই সবচেয়ে বেশি ব্যবহার হয়।

---

# Module 3: Django Cache Framework

Example

```python
from django.core.cache import cache
```

Save

```python
cache.set(
    "products",
    products,
    timeout=300
)
```

Read

```python
products = cache.get("products")
```

Delete

```python
cache.delete("products")
```

Clear

```python
cache.clear()
```

---

Flow

```text
Request

↓

cache.get()

↓

Found?

↓

Yes → Return

↓

No

↓

Database

↓

cache.set()

↓

Response
```

---

# Module 4: Redis

Redis

=

Memory Database

Database

↓

Disk

Redis

↓

RAM

RAM অনেক faster।

---

Example

Database

```text
10-50 ms
```

Redis

```text
<1 ms
```

---

Redis Use Cases

```text
Cache

Session

Celery

OTP

Rate Limit

Leaderboard

Queue

Locks
```

---

# Module 5: Cache Keys

Bad

```python
cache.set("products", data)
```

সব User একই cache।

---

Better

```python
cache.set(

    f"user:{user.id}:products",

    data
)
```

---

আরও ভালো

```python
product:list:category:phone
```

Readable।

---

Rule

```text
feature:type:id
```

Example

```text
user:5

product:10

blog:list

order:33
```

---

# Module 6: Cache Invalidation

সবচেয়ে difficult topic।

ধরো

Product Price

```text
100
```

Cache

↓

100

Database

↓

150

User

↓

100 দেখছে।

Wrong।

---

After Update

```python
cache.delete(

    "product:5"
)
```

---

Rule

```text
Update Database

↓

Delete Cache

↓

Next Request

↓

Fresh Cache
```

---

# Module 7: Celery

সব request user-এর জন্য অপেক্ষা করানো উচিত?

Example

```text
Checkout

↓

Create Order

↓

Generate Invoice PDF

↓

Send Email

↓

Send SMS

↓

Notify Admin
```

User অপেক্ষা করছে।

---

Better

```text
Create Order

↓

Response

↓

Celery

↓

Email

↓

SMS

↓

Invoice
```

---

User Fast Response পেল।

---

# Module 8: Celery Architecture

```text
Client

↓

Django

↓

Redis

↓

Celery Worker

↓

Task

↓

Done
```

Redis এখানে

Queue।

---

Task Example

```python
from celery import shared_task

@shared_task
def send_email(order_id):

    ...
```

Call

```python
send_email.delay(order.id)
```

`.delay()`

↓

Queue-তে চলে গেল।

---

# Module 9: Background Tasks

Good Candidates

```text
Email

SMS

Push Notification

Image Resize

PDF Generate

Video Processing

Report Export

Analytics
```

---

Bad Candidates

```text
Login

Payment Validation

Permission Check

Inventory Check
```

এগুলো synchronous হওয়া উচিত।

---

# Module 10: Retry

Email Fail।

কি করবে?

```text
Retry
```

Celery

Automatically

```python
retry()
```

করতে পারে।

---

Production

```text
Try

↓

Fail

↓

Retry

↓

Retry

↓

Dead Letter
```

---

# Module 11: Real Project

Checkout

```text
Request

↓

transaction.atomic()

↓

Create Order

↓

Commit

↓

Response

↓

Celery

↓

Invoice

↓

Email

↓

SMS
```

---

Blog Publish

```text
Publish

↓

Save

↓

Cache Delete

↓

Celery

↓

Notify Followers
```

---

OTP

```text
Generate OTP

↓

Redis

↓

60 Seconds

↓

Expire
```

Redis-এর TTL এখানে কাজে লাগে।

---

# Module 12: Common Mistakes

## ❌ Cache Everything

সব cache করবে না।

যা expensive, সেটা cache করো।

---

## ❌ Never Expire Cache

Stale data হবে।

---

## ❌ Long Celery Tasks

এক Task

```text
20 Minutes
```

খারাপ।

ছোট task বানাও।

---

## ❌ External API

Inside transaction

ভুল।

Transaction commit

↓

Celery

↓

External API

---

## ❌ Cache User Sensitive Data

যদি key design ভুল হয়,

এক User-এর data

অন্য User দেখতে পারে।

---

# Performance Checklist

প্রতিটি API-এর জন্য আমি সাধারণত এই প্রশ্ন করি:

```text
Database Query কি optimize করা হয়েছে?
        ↓
select_related / prefetch_related
        ↓
Need caching?
        ↓
Need pagination?
        ↓
Need background task?
        ↓
Need transaction?
```

---

# Interview Questions

1. Redis কী?
    
2. Redis এবং Database-এর পার্থক্য কী?
    
3. Cache Hit এবং Cache Miss কী?
    
4. Cache Invalidation কেন কঠিন?
    
5. Celery কী?
    
6. Celery Broker কী?
    
7. `.delay()` কী করে?
    
8. কোন কাজগুলো Background Task হওয়া উচিত?
    
9. কেন Email Celery-তে পাঠানো ভালো?
    
10. Redis-এর ৫টি ব্যবহার বলো।
    

---

# Senior Production Pattern

ধরো Product Update API।

আমি সাধারণত এই sequence অনুসরণ করি:

```text
Validate Request
        ↓
transaction.atomic()
        ↓
Update Database
        ↓
Commit
        ↓
Delete Related Cache
        ↓
transaction.on_commit()
        ↓
Celery Task
            ↓
Email
Notification
Search Index Update
Analytics
```

এতে data consistency বজায় থাকে এবং user দ্রুত response পায়।

---

# এখন তোমার Backend Skill Set

তুমি এখন শিখেছ:

- ✅ DRF Core
    
- ✅ Authentication & Permissions
    
- ✅ Transactions
    
- ✅ Concurrency
    
- ✅ Service Layer
    
- ✅ Testing
    
- ✅ Caching
    
- ✅ Redis
    
- ✅ Celery
    
- ✅ Background Tasks
    

এগুলো একজন **Professional Backend Developer**-এর মূল দক্ষতার বড় অংশ।

---

# এখন কী শেখা উচিত?

এখন আমি DRF feature নয়, **Production Deployment & DevOps for Django** শেখাব।

সেখানে আমরা শিখব:

- Gunicorn
    
- Nginx
    
- Docker
    
- Docker Compose
    
- Environment Variables
    
- Static & Media Files
    
- PostgreSQL in Production
    
- CI/CD
    
- Logging & Monitoring
    
- Production Security Checklist
    

এই অংশটি শিখলে তুমি শুধু Django Developer থাকবে না—একজন **Production-ready Backend Engineer** হওয়ার পথে অনেকটাই এগিয়ে যাবে।

--------
দারুণ। এখন আমরা এমন একটি বিষয় শিখব যা **Junior → Professional Backend Engineer** হওয়ার জন্য অপরিহার্য।

অনেকেই Django দিয়ে API বানাতে পারে, কিন্তু Production-এ deploy করতে পারে না।

> **Lesson 12: Production Deployment + DevOps for Django (Zero → Senior)**

---

# এই Lesson-এর Goal

লোকাল মেশিনে API চালানো এক জিনিস।

Production Server-এ

* হাজার User
* HTTPS
* Domain
* Nginx
* Gunicorn
* Docker
* PostgreSQL

এসব নিয়ে API চালানো সম্পূর্ণ অন্য জিনিস।

---

# Roadmap

```text
Module 1  : Development vs Production
Module 2  : WSGI & ASGI
Module 3  : Gunicorn
Module 4  : Nginx
Module 5  : Static & Media Files
Module 6  : Environment Variables
Module 7  : PostgreSQL Production Setup
Module 8  : Docker
Module 9  : Docker Compose
Module 10 : Logging
Module 11 : Security Checklist
Module 12 : CI/CD
Module 13 : Monitoring
Module 14 : Interview Questions
```

---

# Module 1: Development vs Production

লোকাল

```bash
python manage.py runserver
```

এটা শুধু

Development Server।

Production-এর জন্য না।

---

Production

```text
Internet

↓

Nginx

↓

Gunicorn

↓

Django

↓

PostgreSQL
```

---

runserver

↓

Debugging

Gunicorn

↓

Production

---

# Module 2: WSGI vs ASGI

Django

দুইভাবে চলতে পারে।

## WSGI

Traditional

```text
Request

↓

Response
```

Sync।

---

## ASGI

Modern

Supports

```text
WebSocket

Async

Long Connection
```

---

Interview

WSGI

↓

Sync

ASGI

↓

Async

---

# Module 3: Gunicorn

Gunicorn

=

WSGI Server

User

↓

Nginx

↓

Gunicorn

↓

Django

---

Run

```bash
gunicorn config.wsgi:application
```

---

Workers

```bash
gunicorn --workers 4
```

Rule

```text
CPU * 2 + 1
```

Approximation।

---

Gunicorn

↓

Python Process

---

# Module 4: Nginx

Nginx

কী করে?

```text
Internet

↓

HTTPS

↓

Static Files

↓

Load Balancing

↓

Reverse Proxy

↓

Gunicorn
```

---

Static

```text
/css/

/js/

/images/
```

Nginx serve করবে।

---

API

↓

Gunicorn

---

# Module 5: Static vs Media

Static

```text
CSS

JS

Logo

Fonts
```

Deploy-এর সময় collect করা হয়।

```bash
python manage.py collectstatic
```

---

Media

User Upload

```text
Profile Picture

Resume

Invoice PDF
```

এগুলো collectstatic-এর অংশ নয়।

---

Rule

Static

↓

Developer

Media

↓

User

---

# Module 6: Environment Variables

Bad

```python
SECRET_KEY = "123"
```

GitHub-এ push।

Danger।

---

Better

```python
import os

SECRET_KEY = os.getenv("SECRET_KEY")
```

---

Database

```python
DATABASE_URL
```

SMTP

```python
EMAIL_HOST_PASSWORD
```

সব Env Variable।

---

# Module 7: PostgreSQL Production

SQLite

↓

Learning

---

PostgreSQL

↓

Production

---

Need

```text
Backup

Indexes

Connection Pool

Vacuum

Analyze
```

---

Migration

```bash
python manage.py migrate
```

Production-এ

Maintenance Window থাকলে ভালো।

---

# Module 8: Docker

আগে

```text
Works on my machine
```

Problem।

---

Docker

↓

Same Environment

সব জায়গায়।

---

Container

```text
Python

Django

Dependencies
```

একসাথে।

---

Dockerfile

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["gunicorn","config.wsgi"]
```

---

# Module 9: Docker Compose

একটা App

↓

অনেক Service

```text
Django

PostgreSQL

Redis

Celery

Nginx
```

সব একসাথে।

Compose

```yaml
services:

    web:

    db:

    redis:

    celery:

    nginx:
```

---

# Module 10: Logging

Never

```python
print("Error")
```

Production-এ।

---

Use

```python
import logging

logger = logging.getLogger(__name__)
```

```python
logger.error(...)
```

---

Levels

```text
DEBUG

INFO

WARNING

ERROR

CRITICAL
```

---

# Module 11: Production Security Checklist

Never

```python
DEBUG=True
```

Production-এ।

---

Need

```python
DEBUG=False
```

---

ALLOWED_HOSTS

Set করো।

---

HTTPS

Always।

---

CORS

যত কম

তত ভালো।

---

SECRET_KEY

Never commit।

---

Database Password

Never commit।

---

Rotate Secrets

Time to time।

---

# Module 12: CI/CD

Developer

↓

Push GitHub

↓

GitHub Actions

↓

Run Tests

↓

Deploy

↓

Server

---

Pipeline

```text
Push

↓

Lint

↓

Test

↓

Build

↓

Deploy
```

---

Automation।

---

# Module 13: Monitoring

Deploy করলেই কাজ শেষ না।

Need

```text
Logs

CPU

RAM

Disk

Errors

Response Time
```

---

Popular

```text
Sentry

Prometheus

Grafana
```

---

Need Alerts

Server Down?

↓

Email

Slack

SMS

---

# Production Flow

```text
Browser

↓

HTTPS

↓

Nginx

↓

Gunicorn

↓

Django

↓

Redis

↓

PostgreSQL

↓

Celery

↓

Email
```

---

# Common Mistakes

## ❌ DEBUG=True

---

## ❌ SQLite Production

---

## ❌ SECRET_KEY GitHub-এ

---

## ❌ collectstatic না করা

---

## ❌ Gunicorn ছাড়া runserver দিয়ে Production চালানো

---

## ❌ No Logging

---

## ❌ Backup না রাখা

---

## ❌ Health Check না রাখা

---

# Deployment Checklist

```text
✔ DEBUG=False

✔ Env Variables

✔ Gunicorn

✔ Nginx

✔ PostgreSQL

✔ Redis

✔ Celery

✔ HTTPS

✔ Logging

✔ Monitoring

✔ Backup

✔ Tests Passed

✔ Migrations Applied

✔ collectstatic
```

---

# Interview Questions

1. runserver Production-এর জন্য কেন নয়?
2. Gunicorn কী?
3. Nginx কেন দরকার?
4. Static এবং Media-এর পার্থক্য কী?
5. Docker কেন ব্যবহার করা হয়?
6. Docker Compose কী?
7. Environment Variables কেন দরকার?
8. DEBUG=False কেন জরুরি?
9. PostgreSQL কেন SQLite-এর চেয়ে ভালো?
10. CI/CD কী?

---

# Senior Deployment Architecture

Production Django Application

```text
                 Internet
                     │
                HTTPS Request
                     │
                 Cloud Load Balancer
                     │
                   Nginx
                     │
              Gunicorn (4 Workers)
                     │
                  Django App
          ┌──────────┼──────────┐
          │          │          │
     PostgreSQL    Redis     Celery
          │                     │
          │               Background Tasks
          │                     │
          └──────────────┬──────┘
                         │
                Email / SMS / PDFs
```

---

# একটা গুরুত্বপূর্ণ কথা

তুমি এখন যে topics শেষ করেছ, এগুলো একজন **Professional Django Backend Developer**-এর core।

কিন্তু এখনও **সবচেয়ে কঠিন অংশ** বাকি আছে।

---

# এখান থেকে কী শেখা উচিত?

এখন থেকে Framework না, **Software Engineering** শিখতে হবে।

আমার প্রস্তাবিত Advanced সিরিজ:

1. **Design Patterns in Django**

   * Strategy
   * Factory
   * Adapter
   * Observer
   * Dependency Injection

2. **System Design for Backend**

   * URL Shortener
   * Chat System
   * Notification Service
   * Multi-vendor E-commerce
   * Inventory System
   * Payment System

3. **Database Design Masterclass**

   * Normalization
   * Indexing
   * Constraints
   * Partitioning
   * Sharding (conceptual)
   * Read Replica

4. **Performance Engineering**

   * Query Plans
   * `EXPLAIN ANALYZE`
   * Advanced indexing
   * Slow query optimization

---

## আমার মতে এখন তোমার জন্য পরবর্তী সেরা লেসন

তোমার আগের প্রশ্নগুলো (Multi-vendor, Blog DB Design, Architecture, Transactions) দেখে মনে হচ্ছে এখন **System Design with Django** শুরু করা সবচেয়ে বেশি উপকারী হবে।

সেখানে আমরা শুধু "কীভাবে কোড লিখতে হয়" নয়, বরং **কীভাবে বড় প্রজেক্ট ডিজাইন করতে হয়**—সেটা শিখব, যেমন একজন Senior Backend Engineer করে।


-----
এখন থেকে আমরা **Senior Backend Engineer**-দের জগতে প্রবেশ করছি।

এখান থেকে আর শুধু Django শেখা হবে না।

এখন শিখবে **কিভাবে বড় কোম্পানিগুলো Software Design করে।**

---

# Lesson 13: System Design for Django Backend (Zero → Senior)

> **Goal:** এমনভাবে backend design করা যাতে ১০০ user থেকে ১০ লাখ user পর্যন্ত scale করা যায়।

---

# Roadmap

```text
Module 1  : What is System Design?
Module 2  : Functional vs Non-Functional Requirements
Module 3  : Capacity Estimation
Module 4  : High-Level Architecture
Module 5  : Database Design
Module 6  : API Design
Module 7  : Caching Strategy
Module 8  : Scaling Django
Module 9  : Asynchronous Processing
Module 10 : File Storage
Module 11 : Real Example (E-commerce)
Module 12 : Common Mistakes
Module 13 : Interview Approach
```

---

# Module 1: What is System Design?

Junior Developer ভাবে—

> "Feature কীভাবে লিখব?"

Senior Engineer ভাবে—

> "এই Feature ১০ লাখ user ব্যবহার করলে কী হবে?"

---

উদাহরণ

একটি Blog API।

Junior

```text
User

↓

Django

↓

Database
```

Senior

```text
User

↓

Load Balancer

↓

Multiple Django Servers

↓

Redis Cache

↓

PostgreSQL

↓

Celery

↓

Object Storage (Images)

↓

Monitoring
```

এটাই System Design।

---

# Module 2: Functional vs Non-Functional Requirements

ধরো Multi-vendor E-commerce বানাবে।

## Functional Requirements

```text
User Registration

Login

Product

Cart

Order

Payment

Reviews
```

---

## Non-Functional Requirements

```text
Fast Response

High Availability

Security

Scalability

Reliability

Backup
```

Interview-এ **দুটোই** জিজ্ঞেস করা হতে পারে।

---

# Module 3: Capacity Estimation

Interview-এ কেউ বলতে পারে:

> ১ মিলিয়ন User-এর জন্য System Design করো।

প্রথম প্রশ্ন হওয়া উচিত:

```text
Daily Active Users?

Requests Per Second?

Average Image Size?

Storage?

Read vs Write Ratio?
```

ধরো

```text
1,000,000 Users

100,000 Daily Active Users

10 Requests/User

↓

1,000,000 Requests/Day
```

এখন বোঝা যাবে কতটা infrastructure লাগতে পারে।

---

# Module 4: High-Level Architecture

একটি Production Django Architecture

```text
                Users
                  │
             Load Balancer
                  │
      ┌───────────┴───────────┐
      │                       │
 Django App 1           Django App 2
      │                       │
      └───────────┬───────────┘
                  │
             PostgreSQL
                  │
        ┌─────────┴─────────┐
        │                   │
      Redis             Celery
```

কেন একাধিক Django App?

কারণ

```text
One Server Crash

↓

Application Still Running
```

---

# Module 5: Database Design

Database design সবচেয়ে গুরুত্বপূর্ণ।

ভালো Database Design

↓

কম Bug

↓

কম Query

↓

Fast API

---

Rules

## Primary Key

সব Table-এ থাকবে।

---

## Foreign Key

Data Integrity।

---

## Index

যেখানে বেশি Search হয়।

Example

```python
email

username

slug
```

---

Index না থাকলে

```text
10 Million Rows

↓

Full Table Scan
```

---

Index থাকলে

```text
Index Lookup

↓

Milliseconds
```

---

# Module 6: API Design

Bad API

```text
/getProducts

/createProduct

/updateProduct
```

RESTful না।

---

Good

```text
GET    /products/

POST   /products/

GET    /products/{id}/

PATCH  /products/{id}/

DELETE /products/{id}/
```

---

Nested

```text
/orders/{id}/items/
```

---

Search

```text
/products/?search=iphone
```

---

Pagination

```text
/products/?page=2
```

---

# Module 7: Caching Strategy

সব Data Cache করবে?

না।

Cache করো

```text
Popular Products

Categories

Homepage

Settings
```

Cache করো না

```text
Bank Balance

OTP

Payment Status (unless carefully designed)
```

---

Pattern

```text
Request

↓

Cache

↓

Miss?

↓

Database

↓

Update Cache
```

---

# Module 8: Scaling Django

একটি Server

↓

100 Users

---

100,000 Users?

↓

Multiple Servers

```text
Load Balancer

↓

App 1

App 2

App 3
```

---

Database

↓

Read Replica

```text
Write

↓

Primary DB

↓

Read Replica
```

Read-heavy application-এ useful।

---

# Module 9: Asynchronous Processing

সব Request User-এর জন্য অপেক্ষা করাবে না।

Good

```text
Upload Image

↓

Response

↓

Celery Resize
```

---

Good

```text
Order

↓

Response

↓

Email
```

---

Bad

```text
Login

↓

Celery
```

Login synchronous হওয়া উচিত।

---

# Module 10: File Storage

লোকাল Server-এ Image রাখবে?

Small project

↓

হ্যাঁ

Production

↓

Object Storage

যেমন:

* Amazon S3
* Compatible object storage services

কারণ

```text
Server Replace

↓

Images Safe
```

---

# Module 11: Real Example

## Multi-vendor E-commerce

Architecture

```text
Client

↓

Nginx

↓

Load Balancer

↓

Django API

↓

Redis

↓

PostgreSQL

↓

Celery

↓

Object Storage
```

Flow

```text
Checkout

↓

Transaction

↓

Order Save

↓

Stock Update

↓

Commit

↓

Celery

↓

Email

↓

Notification
```

---

# Module 12: Common Mistakes

### ❌ সব Logic View-এ

---

### ❌ Cache ছাড়া সব Query

---

### ❌ Pagination না রাখা

---

### ❌ Database Index না দেওয়া

---

### ❌ Media Local Disk-এ রাখা (যখন একাধিক server)

---

### ❌ Single Django Server-এর উপর নির্ভর করা

---

# Module 13: System Design Interview Approach

যদি Interview-এ বলে:

> Design a Blog System.

এই Flow Follow করবে।

### Step 1

Requirements

```text
Users?

Posts?

Comments?

Likes?

Search?
```

---

### Step 2

High Level Design

```text
Client

↓

API

↓

Database
```

---

### Step 3

Database

```text
User

Post

Comment

Like
```

---

### Step 4

API

```text
GET /posts/

POST /posts/

POST /comments/
```

---

### Step 5

Scaling

```text
Redis

Pagination

Celery

CDN/Object Storage
```

---

### Step 6

Security

```text
Authentication

Permissions

Rate Limiting
```

---

# Senior Engineer Checklist

যখন নতুন Feature Design করি, আমি সাধারণত এই প্রশ্নগুলো করি:

| Question                      | Example              |
| ----------------------------- | -------------------- |
| Data কোথায় থাকবে?            | PostgreSQL           |
| Read বেশি না Write?           | Read-heavy হলে cache |
| Background task লাগবে?        | Email, PDF           |
| Transaction লাগবে?            | Payment, Inventory   |
| Permission কী?                | Owner/Admin          |
| Failure হলে কী হবে?           | Retry, Rollback      |
| Scale করলে bottleneck কোথায়? | DB, Cache, Network   |

---

# Interview Questions

1. Functional vs Non-functional requirements কী?
2. Load Balancer কেন দরকার?
3. Read Replica কী?
4. Cache কোথায় ব্যবহার করবে?
5. Object Storage কেন Local Disk-এর চেয়ে ভালো?
6. RESTful API Design কী?
7. Index কেন দরকার?
8. System Design শুরু করার প্রথম ধাপ কী?

---

# এখন তুমি কোথায় দাঁড়িয়ে?

তুমি এখন শিখেছ:

* ✅ Django
* ✅ Django REST Framework
* ✅ Authentication
* ✅ Permissions
* ✅ Transactions
* ✅ Concurrency
* ✅ Architecture
* ✅ Testing
* ✅ Redis & Celery
* ✅ Deployment
* ✅ Production Concepts
* ✅ System Design Fundamentals

---

# এখন সবচেয়ে গুরুত্বপূর্ণ কী?

এখন থেকে **নতুন topic শেখার চেয়ে Real Project Building বেশি গুরুত্বপূর্ণ।**

তোমার জন্য আমি এই ক্রমে ৫টি Project বানানোর পরামর্শ দেব:

1. **Blog API** (Authentication, Comments, Likes)
2. **E-commerce API** (Products, Cart, Orders, Payments)
3. **Multi-vendor Marketplace** (Vendor Dashboard, Commissions, Permissions)
4. **Learning Management System (LMS)** (Courses, Enrollment, Progress)
5. **Job Portal** (Companies, Applications, Resume Upload)

এই ৫টি প্রজেক্ট শেষ করলে তুমি Django-এর প্রায় সব গুরুত্বপূর্ণ production pattern বাস্তবে ব্যবহার করবে। এগুলো তোমার portfolio, interview এবং বাস্তব backend engineering—তিন ক্ষেত্রেই সবচেয়ে বেশি মূল্য দেবে।
