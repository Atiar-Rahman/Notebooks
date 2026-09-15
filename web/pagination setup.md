হ্যাঁ। Django REST Framework (DRF)-এ pagination add করলে React থেকে সাধারণত API-এর `next`, `previous`, `count`, `results` ব্যবহার করে pagination control করা যায়।

ধরো API response এমন:

```json
{
  "count": 50,
  "next": "http://localhost:8000/api/products/?page=2",
  "previous": null,
  "results": [
    {
      "id": 1,
      "name": "Product 1"
    }
  ]
}
```

### 1. DRF-এ pagination setup

`settings.py`:

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 10,
}
```

চাইলে custom pagination:

```python
from rest_framework.pagination import PageNumberPagination

class CustomPagination(PageNumberPagination):
    page_size = 10
    page_query_param = "page"
    page_size_query_param = "page_size"
    max_page_size = 100
```

তারপর view-তে:

```python
from rest_framework.viewsets import ModelViewSet

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = CustomPagination
```

---

### 2. React-এ data fetch

`fetch` দিয়ে খুব সহজেই করা যায়:

```jsx
import { useEffect, useState } from "react";

function Products() {
  const [products, setProducts] = useState([]);
  const [page, setPage] = useState(1);
  const [total, setTotal] = useState(0);

  useEffect(() => {
    fetch(`http://localhost:8000/api/products/?page=${page}`)
      .then(res => res.json())
      .then(data => {
        setProducts(data.results);
        setTotal(data.count);
      });
  }, [page]);

  return (
    <div>
      <h2>Products</h2>

      {products.map(product => (
        <div key={product.id}>
          {product.name}
        </div>
      ))}

      <div>
        <button
          disabled={page === 1}
          onClick={() => setPage(page - 1)}
        >
          Previous
        </button>

        <span> Page {page} </span>

        <button
          disabled={page * 10 >= total}
          onClick={() => setPage(page + 1)}
        >
          Next
        </button>
      </div>
    </div>
  );
}

export default Products;
```

এখানে মূল ব্যাপার হলো:

```js
?page=1
?page=2
?page=3
```

প্রতিবার `page` change হলে `useEffect` আবার API call করবে।

### আরও ভালো approach

DRF-এর `next` এবং `previous` URL সরাসরি ব্যবহার করলে page size hardcode করতে হবে না:

```jsx
const [data, setData] = useState(null);

const fetchProducts = async (url) => {
  const response = await fetch(url);
  const result = await response.json();
  setData(result);
};

useEffect(() => {
  fetchProducts(
    "http://localhost:8000/api/products/"
  );
}, []);

return (
  <>
    {data?.results.map(product => (
      <div key={product.id}>{product.name}</div>
    ))}

    <button
      disabled={!data?.previous}
      onClick={() => fetchProducts(data.previous)}
    >
      Previous
    </button>

    <button
      disabled={!data?.next}
      onClick={() => fetchProducts(data.next)}
    >
      Next
    </button>
  </>
);
```

**আমি দ্বিতীয় approach-টাই recommend করব**, কারণ backend pagination configuration পরিবর্তন হলেও React-এর pagination logic তুলনামূলকভাবে সহজ থাকে।


---


হ্যাঁ, **Next.js-এও প্রায় একই process**। কারণ Next.js-এ frontend থেকে Django REST API call করার সময় pagination-এর logic React-এর মতোই থাকে।

ধরো DRF থেকে response:

```json
{
  "count": 50,
  "next": "http://localhost:8000/api/products/?page=2",
  "previous": null,
  "results": [
    {
      "id": 1,
      "name": "Product 1"
    }
  ]
}
```

### Next.js Client Component

যদি Next.js App Router ব্যবহার করো:

```jsx
"use client";

import { useEffect, useState } from "react";

export default function Products() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);

  const fetchProducts = async (url) => {
    setLoading(true);

    try {
      const res = await fetch(url);
      const result = await res.json();

      setData(result);
    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchProducts(
      "http://localhost:8000/api/products/"
    );
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      <h1>Products</h1>

      {data?.results?.map((product) => (
        <div key={product.id}>
          {product.name}
        </div>
      ))}

      <div>
        <button
          disabled={!data?.previous}
          onClick={() => fetchProducts(data.previous)}
        >
          Previous
        </button>

        <button
          disabled={!data?.next}
          onClick={() => fetchProducts(data.next)}
        >
          Next
        </button>
      </div>
    </div>
  );
}
```

### তবে Next.js-এ একটা আরও ভালো approach আছে

URL-এর মধ্যে page number রাখলে:

```text
/products?page=1
/products?page=2
/products?page=3
```

তখন Next.js-এর `searchParams` ব্যবহার করতে পারো।

যেমন:

```jsx
const res = await fetch(
  `http://localhost:8000/api/products/?page=${page}`
);

const data = await res.json();
```

আর pagination:

```jsx
<Link href={`/products?page=${page - 1}`}>
  Previous
</Link>

<Link href={`/products?page=${page + 1}`}>
  Next
</Link>
```

এটার সুবিধা হলো:

- Browser URL-এ current page দেখা যাবে
    
- Refresh করলে একই page থাকবে
    
- Back/Forward browser navigation কাজ করবে
    
- Page share করা যাবে
    
- Next.js-এর routing-এর সাথে সুন্দরভাবে integrate হবে
    

**তাই React SPA হলে `useState + useEffect`, আর Next.js App Router হলে `searchParams` দিয়ে URL-based pagination করা বেশ ভালো pattern।**

চাইলে আমি তোমাকে **Django REST Framework + Next.js App Router দিয়ে একদম production-style pagination (page number + search + loading + error handling)** এর complete example দেখাতে পারি।



---
হ্যাঁ, **dynamic ভাবে pagination করা যায়**—এবং আসলে এটাই সবচেয়ে ভালো approach। তুমি চাইলে backend থেকে `page_size`-ও dynamic করতে পারো।

### 1. Django DRF

```python
from rest_framework.pagination import PageNumberPagination

class CustomPagination(PageNumberPagination):
    page_size = 10
    page_size_query_param = "page_size"
    max_page_size = 100
```

এখন API-তে তুমি চাইলে:

```text
/api/products/?page=1
```

অথবা:

```text
/api/products/?page=2&page_size=20
```

অর্থাৎ frontend থেকেই প্রতি page-এ কয়টা item থাকবে সেটা control করা যাবে।

---

### 2. Next.js-এ dynamic page

ধরো URL:

```text
/products?page=2&page_size=20
```

Next.js থেকে:

```jsx
const res = await fetch(
  `http://localhost:8000/api/products/?page=${page}&page_size=${pageSize}`
);

const data = await res.json();
```

DRF response:

```json
{
  "count": 100,
  "next": "...?page=3&page_size=20",
  "previous": "...?page=1&page_size=20",
  "results": [...]
}
```

এখানে **`count` দেখে total page dynamically বের করা যায়**:

```js
const totalPages = Math.ceil(data.count / pageSize);
```

যেমন:

```text
count = 100
pageSize = 20

totalPages = 100 / 20 = 5
```

---

### 3. Dynamic pagination buttons

```jsx
{Array.from({ length: totalPages }, (_, index) => (
  <button
    key={index}
    onClick={() => setPage(index + 1)}
  >
    {index + 1}
  </button>
))}
```

তাহলে backend-এ যদি 100টা data থাকে এবং `page_size=20` হয়:

```text
[1] [2] [3] [4] [5]
```

আর data 250টা হলে:

```text
[1] [2] [3] ... [13]
```

কোনো কিছু hardcode করতে হবে না।

### আরও ভালোভাবে

Next.js-এ আমি সাধারণত এই structure রাখব:

```text
/products?page=2&page_size=20
```

তারপর:

```text
              Django API
                  ↓
        count / next / previous
                  ↓
              Next.js
                  ↓
       ┌────────────────────┐
       │ 1  2  3  4  5 ... │
       └────────────────────┘
```

এতে **total data যতই হোক pagination automatically generate হবে**।

আর চাইলে `page_size`-ও user select করতে পারবে:

```text
Items per page:
[ 10 ▼ ]

[Previous] 1 2 3 4 5 [Next]
```

`10 → 20 → 50` করলে pagination-ও automatically পরিবর্তন হবে।

---
হ্যাঁ, **React-এ pagination implement করতে শুরুতে একটু বেশি ঝামেলা মনে হতে পারে**, বিশেষ করে dynamic page number, loading, search/filter, `next/previous` এগুলো একসাথে থাকলে।

কিন্তু মূল logic আসলে খুব ছোট:

```text
page state
   ↓
API call → ?page=2
   ↓
results দেখাও
   ↓
next/previous click
   ↓
page change
   ↓
আবার API call
```

তুমি যদি **Next.js ব্যবহার করো**, তাহলে তোমার জন্য URL-based pagination বেশ clean হবে:

```text
/products?page=1
/products?page=2
/products?page=3
```

আর Django শুধু:

```json
{
  "count": 100,
  "next": "...?page=2",
  "previous": null,
  "results": [...]
}
```

দেবে।

**আমার recommendation:**  
যদি তোমার project এখনো শুরু/early stage-এ থাকে, **Django REST Framework + Next.js + URL `searchParams` pagination** ব্যবহার করো। পরে search, filter, sorting যোগ করাও সহজ হবে।

চাইলে আমি তোমাকে **একটা complete CRUD example** দেখাতে পারি যেখানে DRF pagination + Next.js pagination একসাথে থাকবে, যাতে copy করে project-এ বসাতে পারো।

---
হ্যাঁ। তোমার `count` যদি DRF থেকে আসে, তাহলে `totalPages` বের করে `.map()` দিয়ে button generate করলেই হবে।

ধরো API response:

```js
const data = {
  count: 40,
  results: [...]
};
```

আর প্রতি page-এ 10টা করে data:

```js
const pageSize = 10;
const totalPages = Math.ceil(data.count / pageSize);
```

তারপর তোমার JSX:

```jsx
<div className="join">
  {Array.from({ length: totalPages }, (_, index) => (
    <button
      key={index + 1}
      onClick={() => setPage(index + 1)}
      className={`join-item btn btn-xs ${
        page === index + 1 ? "btn-active" : ""
      }`}
    >
      {index + 1}
    </button>
  ))}
</div>
```

### পুরোটা একসাথে

```jsx
const [page, setPage] = useState(1);
const pageSize = 10;

// API response থেকে
const totalPages = Math.ceil(data.count / pageSize);
```

তারপর:

```jsx
<div className="join">
  {Array.from({ length: totalPages }, (_, index) => {
    const pageNumber = index + 1;

    return (
      <button
        key={pageNumber}
        onClick={() => setPage(pageNumber)}
        className={`join-item btn btn-xs ${
          page === pageNumber ? "btn-active" : ""
        }`}
      >
        {pageNumber}
      </button>
    );
  })}
</div>
```

যদি `count = 40` এবং `pageSize = 10` হয়:

```text
[ 1 ] [ 2 ] [ 3 ] [ 4 ]
```

আর `count = 100` হলে automatically:

```text
[ 1 ] [ 2 ] [ 3 ] [ 4 ] [ 5 ] [ 6 ] [ 7 ] [ 8 ] [ 9 ] [ 10 ]
```

আর button click করলে API call:

```jsx
useEffect(() => {
  fetch(`http://localhost:8000/api/products/?page=${page}`)
    .then(res => res.json())
    .then(data => setData(data));
}, [page]);
```

**মূল trick হলো `Array.from()` + `data.count`।** `1, 2, 3, 4` manually লিখতে হবে না।


---
অবশ্যই। একদম **শূন্য থেকে complete example** দিচ্ছি। তুমি শুধু এই flow-টা বুঝো:

**Django → `count`, `results`, `next`, `previous` পাঠাবে → React page number বানাবে → button click করলে নতুন page-এর API call হবে।**

ধরি তোমার `Product` API আছে।

---

## 1. Django REST Framework

প্রথমে pagination setup করো।

### `pagination.py`

```python
from rest_framework.pagination import PageNumberPagination


class ProductPagination(PageNumberPagination):
    page_size = 5
    page_size_query_param = "page_size"
    max_page_size = 100
```

এখানে:

```python
page_size = 5
```

মানে প্রতি page-এ ৫টা product আসবে।

### View

```python
from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer
from .pagination import ProductPagination


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = ProductPagination
```

ধরো তোমার database-এ **23টা product** আছে।

তাহলে:

```text
page 1 → 5 products
page 2 → 5 products
page 3 → 5 products
page 4 → 5 products
page 5 → 3 products
```

অর্থাৎ মোট:

```text
23 / 5 = 4.6
```

তাই মোট **5 pages**।

---

# 2. Django API কী return করবে?

তুমি যদি যাও:

```text
/api/products/?page=1
```

তাহলে DRF এমন response দেবে:

```json
{
    "count": 23,
    "next": "http://localhost:8000/api/products/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "name": "Product 1"
        },
        {
            "id": 2,
            "name": "Product 2"
        },
        {
            "id": 3,
            "name": "Product 3"
        },
        {
            "id": 4,
            "name": "Product 4"
        },
        {
            "id": 5,
            "name": "Product 5"
        }
    ]
}
```

এখানে সবচেয়ে important:

```text
count = 23
```

এটা দিয়ে আমরা বুঝব database-এ মোট 23টা product আছে।

আর:

```text
results
```

এর মধ্যে current page-এর product থাকবে।

---

# 3. এবার React

এখন আসল জিনিস।

ধরি `Products.jsx`:

```jsx
import { useEffect, useState } from "react";

function Products() {
  const [products, setProducts] = useState([]);
  const [page, setPage] = useState(1);
  const [totalProducts, setTotalProducts] = useState(0);

  const pageSize = 5;

  useEffect(() => {
    fetch(`http://localhost:8000/api/products/?page=${page}`)
      .then((response) => response.json())
      .then((data) => {
        console.log(data);

        setProducts(data.results);
        setTotalProducts(data.count);
      });
  }, [page]);

  const totalPages = Math.ceil(totalProducts / pageSize);

  return (
    <div>

      <h1>Products</h1>

      {/* Products */}
      <div>
        {products.map((product) => (
          <div key={product.id}>
            <h3>{product.name}</h3>
          </div>
        ))}
      </div>


      {/* Pagination */}
      <div className="join">

        {Array.from(
          { length: totalPages },
          (_, index) => {

            const pageNumber = index + 1;

            return (
              <button
                key={pageNumber}
                onClick={() => setPage(pageNumber)}
                className={`join-item btn btn-xs ${
                  page === pageNumber
                    ? "btn-active"
                    : ""
                }`}
              >
                {pageNumber}
              </button>
            );

          }
        )}

      </div>

    </div>
  );
}

export default Products;
```

এখন **লাইন বাই লাইন বুঝি**।

---

# 4. প্রথমে `page`

```jsx
const [page, setPage] = useState(1);
```

এর মানে:

```text
বর্তমানে আমি page 1-এ আছি।
```

শুরুতে:

```text
page = 1
```

---

# 5. API call

এই অংশটা দেখো:

```jsx
useEffect(() => {
  fetch(`http://localhost:8000/api/products/?page=${page}`)
    .then((response) => response.json())
    .then((data) => {
      setProducts(data.results);
      setTotalProducts(data.count);
    });
}, [page]);
```

শুরুতে `page = 1`।

তাই API হবে:

```text
/api/products/?page=1
```

তারপর তুমি **2** button click করলে:

```jsx
setPage(2)
```

তখন `page` হয়ে যাবে:

```text
page = 2
```

এবং যেহেতু:

```jsx
}, [page]);
```

আছে, `useEffect` আবার চলবে।

API হবে:

```text
/api/products/?page=2
```

এটাই pagination-এর মূল concept।

---

# 6. এবার আসল magic 😄

Django থেকে আমরা পাচ্ছি:

```json
{
    "count": 23
}
```

React-এ:

```jsx
setTotalProducts(data.count);
```

তাই:

```text
totalProducts = 23
```

আমরা জানি প্রতি page-এ 5টা product:

```jsx
const pageSize = 5;
```

তাহলে:

```jsx
const totalPages = Math.ceil(totalProducts / pageSize);
```

মানে:

```text
Math.ceil(23 / 5)

= Math.ceil(4.6)

= 5
```

তাই:

```text
totalPages = 5
```

---

# 7. এখন 1 2 3 4 5 কীভাবে তৈরি হচ্ছে?

এই অংশ:

```jsx
Array.from(
  { length: totalPages },
  (_, index) => {
```

যেহেতু:

```text
totalPages = 5
```

তাই এটা basically 5টা item তৈরি করবে।

```text
0
1
2
3
4
```

কিন্তু আমরা চাই:

```text
1
2
3
4
5
```

তাই:

```jsx
const pageNumber = index + 1;
```

ফলে:

```text
index       pageNumber

0              1
1              2
2              3
3              4
4              5
```

---

# 8. Button তৈরি হচ্ছে

তারপর:

```jsx
<button
  onClick={() => setPage(pageNumber)}
>
  {pageNumber}
</button>
```

তাই automatically তৈরি হবে:

```html
<button>1</button>
<button>2</button>
<button>3</button>
<button>4</button>
<button>5</button>
```

তোমাকে manually লিখতে হবে না।

---

# 9. Active button

তোমার original code ছিল:

```jsx
<button className="join-item btn btn-xs">
  1
</button>

<button className="join-item btn btn-xs btn-active">
  2
</button>
```

এখানে তুমি manually `btn-active` দিয়েছো।

আমরা সেটা dynamic করব:

```jsx
className={`join-item btn btn-xs ${
  page === pageNumber
    ? "btn-active"
    : ""
}`}
```

ধরো:

```text
page = 2
```

তাহলে:

```text
pageNumber = 1
2 === 1 → false

pageNumber = 2
2 === 2 → true

pageNumber = 3
2 === 3 → false
```

তাই শুধু **2** active হবে।

```text
[ 1 ] [ 2 ] [ 3 ] [ 4 ] [ 5 ]
        ↑
      active
```

---

# 10. পুরো flow

এখন পুরো ব্যাপারটা মাথায় রাখো:

```text
Database
   ↓
23 Products
   ↓
Django Pagination
   ↓
প্রতি page = 5
   ↓
count = 23
   ↓
React
   ↓
23 / 5
   ↓
5 Pages
   ↓
[1] [2] [3] [4] [5]
```

তুমি **3** click করলে:

```text
setPage(3)
      ↓
page = 3
      ↓
useEffect আবার চলে
      ↓
/api/products/?page=3
      ↓
Django page 3-এর data দেয়
      ↓
React products update করে
```

---

## 11. এবার তোমার code-এর সাথে মিলিয়ে দেখো

তোমার ছিল:

```jsx
<div className="join">
  <button className="join-item btn btn-xs">1</button>
  <button className="join-item btn btn-xs btn-active">2</button>
  <button className="join-item btn btn-xs">3</button>
  <button className="join-item btn btn-xs">4</button>
</div>
```

এটা dynamic করলে মূলত শুধু এটা:

```jsx
<div className="join">

  {Array.from(
    { length: totalPages },
    (_, index) => {

      const pageNumber = index + 1;

      return (
        <button
          key={pageNumber}
          onClick={() => setPage(pageNumber)}
          className={`join-item btn btn-xs ${
            page === pageNumber
              ? "btn-active"
              : ""
          }`}
        >
          {pageNumber}
        </button>
      );

    }
  )}

</div>
```

**এইটুকুই pagination button-এর dynamic অংশ।**

তোমার সবচেয়ে গুরুত্বপূর্ণ ৩টা জিনিস মনে রাখলেই হবে:

```jsx
const [page, setPage] = useState(1);
```

```jsx
fetch(`/api/products/?page=${page}`)
```

```jsx
const totalPages = Math.ceil(data.count / pageSize);
```

এই তিনটার connection বুঝে গেলে DRF + React pagination অনেক সহজ হয়ে যাবে।

---
