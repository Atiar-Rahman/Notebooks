হ্যাঁ, পারবেন। তবে **different e-commerce website থেকে data collect** করতে গেলে প্রথমে ঠিক করতে হবে আপনি কোন ধরনের data চান এবং কীভাবে legally/technically collect করবেন।

আপনার Data Analyst/ML learning-এর জন্য আমি হলে **একটা reusable E-commerce Data Collection Pipeline** বানাতাম।

### 1. কী কী data collect করতে পারেন

প্রতিটি product-এর জন্য:

```text
product_name
category
subcategory
brand
price
original_price
discount
rating
review_count
availability
product_url
image_url
seller
description
specifications
scraped_at
```

উদাহরণ:

```text
Product: Samsung Galaxy A56
Category: Smartphone
Brand: Samsung
Price: 49,999
Original Price: 54,999
Discount: 9%
Rating: 4.6
Reviews: 1250
Availability: In Stock
```

### 2. Data collection-এর প্রধান পদ্ধতি

#### Method 1 — Official API

সবচেয়ে ভালো পদ্ধতি।

```text
Website
   ↓
Official API
   ↓
JSON
   ↓
Python
   ↓
Pandas
   ↓
PostgreSQL
```

API থাকলে সেটাই প্রথম পছন্দ।

---

#### Method 2 — HTML Scraping

Python দিয়ে:

```text
Website
   ↓
requests
   ↓
HTML
   ↓
BeautifulSoup
   ↓
Extract data
   ↓
CSV / Database
```

Basic example:

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com/products"

response = requests.get(
    url,
    headers={
        "User-Agent": "Mozilla/5.0"
    }
)

soup = BeautifulSoup(response.text, "html.parser")

products = soup.select(".product")

for product in products:
    name = product.select_one(".product-name")
    price = product.select_one(".price")

    print(name.get_text(strip=True))
    print(price.get_text(strip=True))
```

তবে প্রতিটি website-এর HTML structure আলাদা হবে।

---

### 3. Dynamic website হলে

অনেক modern e-commerce site JavaScript দিয়ে product load করে।

তখন:

```text
Playwright
     ↓
Open browser
     ↓
Load JavaScript
     ↓
Wait
     ↓
Extract products
```

যেমন:

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)

    page = browser.new_page()

    page.goto("https://example.com/products")

    page.wait_for_load_state("networkidle")

    products = page.locator(".product")

    for i in range(products.count()):
        product = products.nth(i)

        print(product.inner_text())

    browser.close()
```

### 4. Multiple website নিয়ে architecture

আপনি যদি 10–20টা e-commerce website থেকে data নিতে চান, তাহলে **প্রতিটি website-এর জন্য আলাদা scraper adapter** বানানো ভালো।

```text
ecommerce-data-collector/
│
├── scrapers/
│   ├── site_a.py
│   ├── site_b.py
│   ├── site_c.py
│   ├── site_d.py
│   └── base_scraper.py
│
├── models/
│   └── product.py
│
├── pipelines/
│   ├── cleaner.py
│   ├── normalizer.py
│   └── exporter.py
│
├── database/
│   └── postgres.py
│
├── config/
│   └── settings.py
│
├── scheduler/
│   └── jobs.py
│
└── main.py
```

এখানে সবচেয়ে important হবে **common schema**।

কারণ Website A হয়তো বলে:

```text
product_title
selling_price
```

Website B:

```text
name
current_price
```

আপনার database-এ দুটোকেই convert করবেন:

```text
product_name
price
```

---

### 5. Database design

আপনি PostgreSQL ব্যবহার করতে পারেন।

```text
websites
---------
id
name
url


categories
----------
id
name


products
--------
id
website_id
category_id
name
brand
price
original_price
discount
rating
review_count
availability
url
image_url
created_at
updated_at


price_history
-------------
id
product_id
price
recorded_at
```

`price_history` খুব গুরুত্বপূর্ণ।

তাহলে আপনি পরে analysis করতে পারবেন:

```text
Product Price
     ↓
Day 1 → 50,000
Day 7 → 48,500
Day 14 → 46,999
Day 30 → 45,999
```

এর মাধ্যমে **price trend analysis** করা যাবে।

---

## 6. আপনার জন্য আমি যে project recommend করব

আপনি যেহেতু Pandas, NumPy, Matplotlib, Seaborn এবং SQL শিখছেন, একটা বাস্তব project বানাতে পারেন:

### 🛒 Multi-Ecommerce Product Analytics System

```text
        E-commerce Websites
        /       |       \
       /        |        \
   Site A    Site B    Site C
      ↓         ↓         ↓
        Data Collection
              ↓
       Data Cleaning
              ↓
       Data Normalization
              ↓
           PostgreSQL
              ↓
            Pandas
              ↓
      ┌───────┼────────┐
      ↓       ↓        ↓
   Analysis Visualization ML
```

তারপর প্রশ্নের উত্তর বের করবেন:

- কোন website-এ product সবচেয়ে সস্তা?
    
- কোন category-তে discount বেশি?
    
- কোন brand-এর average price বেশি?
    
- কোন product-এর rating বেশি?
    
- rating বনাম price-এর relationship কী?
    
- কোন product-এর review সবচেয়ে বেশি?
    
- কোন category সবচেয়ে popular?
    
- price কীভাবে সময়ের সাথে পরিবর্তন হচ্ছে?
    

---

### ⚠️ গুরুত্বপূর্ণ

সব website থেকে নির্বিচারে scraping করা উচিত নয়। আগে website-এর **Terms of Service, robots.txt, rate limits এবং applicable laws** দেখবেন। Login-protected/private data, CAPTCHA bypass, anti-bot/security controls bypass করা উচিত নয়। সম্ভব হলে official API বা publicly available data ব্যবহার করুন।

**আপনার জন্য সবচেয়ে ভালো learning sequence হবে:**

```text
M01 → requests
M02 → BeautifulSoup
M03 → CSS selectors
M04 → Pagination
M05 → Dynamic website + Playwright
M06 → Data cleaning
M07 → Multi-site scraper architecture
M08 → PostgreSQL
M09 → Pandas analysis
M10 → Automation / scheduler
M11 → Visualization dashboard
M12 → Complete Ecommerce Data Analytics Project
```

চাইলে আমি **M01 থেকে শুরু করে “Multi-Ecommerce Web Scraping & Data Collection” complete course** milestone-by-milestone সাজিয়ে দিতে পারি—প্রতিটি module-এ theory + real website-style example + Python code + project task থাকবে।


---
# M01 — Python `requests` দিয়ে Web Data Collection

এই module-এ আমরা **একদম basic থেকে** শিখব কীভাবে Python দিয়ে একটি e-commerce website-এর public webpage request করে HTML data collect করা যায়।

> **Goal:** M01 শেষে আপনি বুঝবেন `requests` কীভাবে কাজ করে এবং website থেকে HTML এনে Python দিয়ে inspect করতে পারবেন।

---

## 1. পুরো Data Collection Pipeline

আমাদের target হবে:

```text
E-commerce Website
       ↓
   HTTP Request
       ↓
 Python requests
       ↓
    HTML Page
       ↓
 HTML inspect
       ↓
 পরের Module-এ BeautifulSoup
```

আজকে মূলত:

```text
Website → requests → HTML
```

---

# 2. HTTP কী?

আপনি browser-এ যখন লিখেন:

```text
https://example.com
```

তখন browser server-এর কাছে একটি **HTTP request** পাঠায়।

```text
Browser
   │
   │ HTTP Request
   ↓
Server
   │
   │ HTTP Response
   ↓
Browser
```

Python দিয়েও একই কাজ করা যায়।

```python
import requests

response = requests.get("https://example.com")
```

এখানে:

```python
requests.get()
```

server-এর কাছে GET request পাঠাচ্ছে।

---

# 3. `requests` install

Terminal:

```bash
pip install requests
```

Check:

```bash
pip show requests
```

Jupyter হলে:

```python
!pip install requests
```

---

# 4. প্রথম Request

```python
import requests

url = "https://example.com"

response = requests.get(url)

print(response)
```

Output সাধারণত:

```text
<Response [200]>
```

এখানে `200` খুব গুরুত্বপূর্ণ।

---

# 5. HTTP Status Code

Common status codes:

| Code | Meaning            |
| ---- | ------------------ |
| 200  | Success            |
| 301  | Permanent redirect |
| 302  | Temporary redirect |
| 400  | Bad request        |
| 401  | Unauthorized       |
| 403  | Forbidden          |
| 404  | Not found          |
| 429  | Too many requests  |
| 500  | Server error       |

সবচেয়ে common:

```python
response.status_code
```

Example:

```python
import requests

url = "https://example.com"

response = requests.get(url)

print(response.status_code)
```

Output:

```text
200
```

---

# 6. HTML পাওয়ার জন্য `.text`

Website server response-এর HTML দেখতে:

```python
print(response.text)
```

Complete example:

```python
import requests

url = "https://example.com"

response = requests.get(url)

print(response.status_code)
print(response.text)
```

আপনি অনেক HTML দেখতে পাবেন:

```html
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
</head>

<body>

<h1>Example Domain</h1>

<p>This domain is for use in illustrative examples...</p>

</body>
</html>
```

এটাই আমাদের **raw webpage data**।

---

# 7. Response Object

`response` একটি object।

এর মধ্যে অনেক useful information থাকে।

```python
import requests

response = requests.get("https://example.com")

print(response.status_code)
print(response.url)
print(response.headers)
print(response.text)
```

---

## 8. `response.url`

Request করার পর actual URL দেখতে:

```python
print(response.url)
```

---

# 9. Response Headers

```python
print(response.headers)
```

Output-এর মতো হতে পারে:

```text
{
    'content-type': 'text/html',
    'content-length': '1256',
    ...
}
```

Specific header:

```python
print(response.headers.get("Content-Type"))
```

---

# 10. খুব গুরুত্বপূর্ণ — `timeout`

Production scraper-এ request কখনো indefiniteভাবে আটকে রাখা উচিত নয়।

তাই:

```python
response = requests.get(
    url,
    timeout=10
)
```

মানে সর্বোচ্চ প্রায় 10 seconds অপেক্ষা করবে।

---

# 11. Error Handling

এটা খুব important।

শুধু:

```python
requests.get(url)
```

লিখে রাখা ভালো practice না।

বরং:

```python
import requests

url = "https://example.com"

try:
    response = requests.get(url, timeout=10)

    response.raise_for_status()

    print("Success!")
    print(response.status_code)

except requests.RequestException as e:
    print("Request failed:", e)
```

### `raise_for_status()`

যদি:

```text
200 → কিছু করবে না
404 → error
403 → error
500 → error
```

তাহলে exception তৈরি করবে।

---

# 12. User-Agent

অনেক website request-এর সঙ্গে browser-এর মতো headers দেখতে চায়।

Example:

```python
import requests

url = "https://example.com"

headers = {
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(
    url,
    headers=headers,
    timeout=10
)

print(response.status_code)
```

আরও realisticভাবে:

```python
headers = {
    "User-Agent": (
        "Mozilla/5.0 (X11; Linux x86_64) "
        "AppleWebKit/537.36 "
        "(KHTML, like Gecko) "
        "Chrome/140.0 Safari/537.36"
    )
}
```

**Note:** User-Agent দেওয়া anti-bot protection bypass করার উপায় নয়। Website-এর rules মেনে request করবেন।

---

# 13. একটি reusable function বানাই

এখন আমরা code সুন্দর করি।

```python
import requests


def fetch_page(url):

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    try:
        response = requests.get(
            url,
            headers=headers,
            timeout=10
        )

        response.raise_for_status()

        return response.text

    except requests.RequestException as e:

        print("Error:", e)

        return None
```

তারপর:

```python
html = fetch_page("https://example.com")

if html:
    print(html[:1000])
```

এখানে:

```python
html[:1000]
```

মানে প্রথম 1000 characters।

---

# 14. কেন Function ব্যবহার করছি?

ধরুন 20টা website আছে:

```text
site1.com
site2.com
site3.com
...
site20.com
```

প্রতিবার একই code লিখতে হবে না।

```python
html1 = fetch_page(url1)
html2 = fetch_page(url2)
html3 = fetch_page(url3)
```

এটাই reusable programming।

---

# 15. Multiple URLs

```python
import requests

urls = [
    "https://example.com",
    "https://example.org",
    "https://example.net"
]

for url in urls:

    try:
        response = requests.get(
            url,
            headers={"User-Agent": "Mozilla/5.0"},
            timeout=10
        )

        print(url)
        print(response.status_code)

    except requests.RequestException as e:

        print(url, "FAILED")
        print(e)
```

Output:

```text
https://example.com
200

https://example.org
200

https://example.net
200
```

---

# 16. HTML file হিসেবে save করা

Data collection-এর সময় raw HTML save করা অনেক useful।

```python
import requests

url = "https://example.com"

response = requests.get(
    url,
    headers={"User-Agent": "Mozilla/5.0"},
    timeout=10
)

response.raise_for_status()

with open("page.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Saved successfully!")
```

আপনার folder-এ:

```text
project/
│
├── page.html
└── scraper.py
```

তৈরি হবে।

---

# 17. HTML থেকে title বের করার চেষ্টা

এখানে একটা সমস্যা আছে।

আমরা raw HTML পেয়েছি:

```python
html = response.text
```

কিন্তু এখনো structured data পাইনি।

যেমন:

```text
Product Name
Price
Rating
Review Count
```

এগুলো আলাদা করতে হবে।

এখানেই আসবে **BeautifulSoup**।

```text
requests
   ↓
HTML
   ↓
BeautifulSoup
   ↓
Product data
```

এটা আমাদের **M02**-এর main topic হবে।

---

# 18. Query Parameters

কিছু website URL-এর সঙ্গে parameters ব্যবহার করে।

Example:

```text
https://example.com/search?q=laptop
```

Python:

```python
import requests

url = "https://example.com/search"

params = {
    "q": "laptop"
}

response = requests.get(
    url,
    params=params,
    timeout=10
)

print(response.url)
```

Python automatically URL তৈরি করবে:

```text
https://example.com/search?q=laptop
```

---

# 19. Multiple Parameters

```python
params = {
    "q": "laptop",
    "page": 2,
    "sort": "price"
}

response = requests.get(
    "https://example.com/search",
    params=params,
    timeout=10
)

print(response.url)
```

এটা e-commerce scraping-এ অনেক কাজে লাগে।

যেমন:

```text
search
page
category
sort
brand
price
```

---

# 20. Cookies

Response-এর cookies দেখতে:

```python
print(response.cookies)
```

Request-এর সময় cookies দিতে:

```python
cookies = {
    "example_cookie": "value"
}

response = requests.get(
    url,
    cookies=cookies,
    timeout=10
)
```

তবে login/session-related data নিয়ে কাজ করার আগে website-এর authorization এবং terms মেনে চলতে হবে।

---

# 21. Session ব্যবহার

Multiple request করলে `Session` useful।

```python
import requests

session = requests.Session()

session.headers.update({
    "User-Agent": "Mozilla/5.0"
})

response1 = session.get(
    "https://example.com",
    timeout=10
)

response2 = session.get(
    "https://example.org",
    timeout=10
)

print(response1.status_code)
print(response2.status_code)
```

Session connection/settings reuse করতে পারে।

---

# 22. E-commerce-এর জন্য আমাদের প্রথম mini scraper

এখন একটি realistic structure:

```python
import requests


def fetch_page(url):

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    try:

        response = requests.get(
            url,
            headers=headers,
            timeout=10
        )

        response.raise_for_status()

        print("Status:", response.status_code)
        print("URL:", response.url)

        return response.text

    except requests.RequestException as e:

        print("Error:", e)

        return None


url = "https://example.com"

html = fetch_page(url)

if html:

    print("HTML length:", len(html))
    print(html[:500])
```

Output:

```text
Status: 200
URL: https://example.com
HTML length: 1256
<!doctype html>
<html>
...
```

---

# 23. এখন আমাদের Architecture

M01 শেষে আপনি এই অংশটি বুঝবেন:

```text
                 Website
                    │
                    ▼
             requests.get()
                    │
                    ▼
              HTTP Response
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
      status      headers    text
        200                   │
                              ▼
                           HTML
```

পরবর্তী ধাপে:

```text
HTML
 │
 ▼
BeautifulSoup
 │
 ├── Product Name
 ├── Price
 ├── Rating
 ├── Discount
 └── Product URL
```

---

# 24. M01 Practice Project

এখন নিজে এই project করুন:

### Project: Website Collector

একটি Python file বানান:

```text
m01_web_collector/
│
├── scraper.py
├── data/
│   └── pages/
└── requirements.txt
```

`requirements.txt`:

```text
requests
```

`scraper.py`:

```python
import requests


def fetch_page(url):

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    try:

        response = requests.get(
            url,
            headers=headers,
            timeout=10
        )

        response.raise_for_status()

        return response

    except requests.RequestException as e:

        print("Request failed:", e)

        return None


url = "https://example.com"

response = fetch_page(url)

if response:

    print("Status Code:", response.status_code)
    print("Final URL:", response.url)
    print("Content Type:",
          response.headers.get("Content-Type"))

    with open(
        "data/pages/page.html",
        "w",
        encoding="utf-8"
    ) as file:

        file.write(response.text)

    print("HTML saved successfully!")
```

Run:

```bash
python scraper.py
```

---

# 25. M01-এ যা অবশ্যই শিখবেন

এইগুলো ভালোভাবে practice করবেন:

```text
✅ HTTP Request
✅ GET request
✅ requests.get()
✅ Response object
✅ status_code
✅ response.text
✅ response.url
✅ response.headers
✅ timeout
✅ raise_for_status()
✅ RequestException
✅ headers
✅ User-Agent
✅ params
✅ cookies
✅ Session
✅ Save HTML
✅ reusable function
```

### সবচেয়ে গুরুত্বপূর্ণ mental model

```text
requests
   ↓
website-এ request পাঠায়

response
   ↓
server কী ফেরত দিয়েছে

response.status_code
   ↓
request successful কিনা

response.text
   ↓
website-এর HTML

BeautifulSoup
   ↓
HTML থেকে প্রয়োজনীয় data বের করবে
```

**M01-এর মূল লক্ষ্য product data বের করা নয়।** প্রথমে `requests` দিয়ে website থেকে reliableভাবে HTML response আনা শিখবেন। তারপর **M02 — BeautifulSoup + HTML/CSS Selector Deep Dive**-তে সেই HTML থেকে `product_name`, `price`, `rating`, `discount`, `URL` ইত্যাদি বের করা শুরু করব।

----
# M02 — BeautifulSoup + HTML/CSS Selector Deep Dive

M01-এ আমরা শিখেছি:

```text
Website
   ↓
requests.get()
   ↓
HTML
```

এখন M02-এ সবচেয়ে গুরুত্বপূর্ণ কাজ:

```text
HTML
 ↓
BeautifulSoup
 ↓
Find elements
 ↓
Extract data
```

অর্থাৎ এখন থেকে আমরা **Product Name, Price, Rating, Link, Image URL** ইত্যাদি বের করা শুরু করব।

---

# 1. BeautifulSoup কী?

`BeautifulSoup` হলো Python-এর একটি HTML parser।

ধরুন website থেকে আমরা পেলাম:

```html
<div class="product">
    <h2 class="product-name">Samsung Galaxy A56</h2>
    <span class="price">49999</span>
    <span class="rating">4.6</span>
</div>
```

BeautifulSoup দিয়ে আমরা করতে পারব:

```text
Product Name → Samsung Galaxy A56
Price        → 49999
Rating       → 4.6
```

---

# 2. Install

```bash
pip install beautifulsoup4
```

M01-এর সাথে:

```bash
pip install requests beautifulsoup4
```

Check:

```bash
pip show beautifulsoup4
```

---

# 3. First BeautifulSoup Program

```python
from bs4 import BeautifulSoup

html = """
<html>
    <body>
        <h1>Hello World</h1>
    </body>
</html>
"""

soup = BeautifulSoup(html, "html.parser")

print(soup)
```

Output:

```html
<html>
<body>
<h1>Hello World</h1>
</body>
</html>
```

---

# 4. `find()` দিয়ে element খোঁজা

```python
h1 = soup.find("h1")

print(h1)
```

Output:

```html
<h1>Hello World</h1>
```

শুধু text:

```python
print(h1.text)
```

Output:

```text
Hello World
```

আরও ভালো:

```python
print(h1.get_text(strip=True))
```

---

# 5. HTML Tag কী?

এই HTML:

```html
<h1>Samsung Galaxy A56</h1>
```

এখানে:

```text
<h1>        → opening tag
Samsung...  → content
</h1>       → closing tag
```

BeautifulSoup-এ:

```python
soup.find("h1")
```

মানে:

> প্রথম `<h1>` element খুঁজে দাও।

---

# 6. Realistic Product HTML

এখন আমরা একটি ছোট e-commerce page ধরে practice করি:

```python
html = """
<div class="product">

    <h2 class="product-name">
        Samsung Galaxy A56
    </h2>

    <span class="price">
        49999
    </span>

    <span class="rating">
        4.6
    </span>

</div>
"""
```

Parse:

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(html, "html.parser")
```

---

# 7. Product Name বের করা

```python
product_name = soup.find(
    "h2",
    class_="product-name"
)

print(product_name)
```

Output:

```html
<h2 class="product-name">
Samsung Galaxy A56
</h2>
```

শুধু text:

```python
print(product_name.get_text(strip=True))
```

Output:

```text
Samsung Galaxy A56
```

---

# 8. Price বের করা

```python
price = soup.find(
    "span",
    class_="price"
)

print(price.get_text(strip=True))
```

Output:

```text
49999
```

---

# 9. Rating

```python
rating = soup.find(
    "span",
    class_="rating"
)

print(rating.get_text(strip=True))
```

Output:

```text
4.6
```

---

# 10. পুরো Product Scraper

এখন:

```python
from bs4 import BeautifulSoup

html = """
<div class="product">

    <h2 class="product-name">
        Samsung Galaxy A56
    </h2>

    <span class="price">
        49999
    </span>

    <span class="rating">
        4.6
    </span>

</div>
"""

soup = BeautifulSoup(
    html,
    "html.parser"
)

name = soup.find(
    "h2",
    class_="product-name"
).get_text(strip=True)

price = soup.find(
    "span",
    class_="price"
).get_text(strip=True)

rating = soup.find(
    "span",
    class_="rating"
).get_text(strip=True)

print("Name:", name)
print("Price:", price)
print("Rating:", rating)
```

Output:

```text
Name: Samsung Galaxy A56
Price: 49999
Rating: 4.6
```

---

# 11. `find()` বনাম `find_all()`

এটা খুব গুরুত্বপূর্ণ।

ধরুন:

```html
<div class="product">
    <h2>Samsung A56</h2>
</div>

<div class="product">
    <h2>iPhone 17</h2>
</div>

<div class="product">
    <h2>Google Pixel</h2>
</div>
```

### `find()`

```python
product = soup.find("h2")
```

শুধু প্রথমটা:

```text
Samsung A56
```

### `find_all()`

```python
products = soup.find_all("h2")
```

সবগুলো:

```text
Samsung A56
iPhone 17
Google Pixel
```

---

# 12. Multiple Products Scrape

এখন realistic example:

```python
from bs4 import BeautifulSoup

html = """
<div class="product">
    <h2 class="name">Samsung A56</h2>
    <span class="price">49999</span>
</div>

<div class="product">
    <h2 class="name">iPhone 17</h2>
    <span class="price">129999</span>
</div>

<div class="product">
    <h2 class="name">Google Pixel</h2>
    <span class="price">89999</span>
</div>
"""

soup = BeautifulSoup(
    html,
    "html.parser"
)

products = soup.find_all(
    "div",
    class_="product"
)

for product in products:

    name = product.find(
        "h2",
        class_="name"
    ).get_text(strip=True)

    price = product.find(
        "span",
        class_="price"
    ).get_text(strip=True)

    print(name, price)
```

Output:

```text
Samsung A56 49999
iPhone 17 129999
Google Pixel 89999
```

এটাই আসলে আমাদের e-commerce scraping-এর basic pattern।

---

# 13. CSS Selector

BeautifulSoup-এর সবচেয়ে powerful feature হলো:

```python
select()
```

Example:

```python
products = soup.select(".product")
```

এখানে:

```text
.product
```

মানে:

```text
class="product"
```

---

# 14. CSS Selector বুঝুন

HTML:

```html
<div class="product">
```

Selector:

```css
.product
```

---

HTML:

```html
<div id="products">
```

Selector:

```css
#products
```

---

HTML:

```html
<h2>
```

Selector:

```css
h2
```

---

HTML:

```html
<div class="product">
    <h2 class="name">
```

Selector:

```css
.product .name
```

মানে:

> `.product` এর ভিতরে থাকা `.name`

---

# 15. `select()`

```python
products = soup.select(".product")

for product in products:
    print(product.get_text(" ", strip=True))
```

---

# 16. Specific Element

```python
names = soup.select(".product .name")

for name in names:
    print(name.get_text(strip=True))
```

Output:

```text
Samsung A56
iPhone 17
Google Pixel
```

---

# 17. `select_one()`

`find()`-এর মতো first matching element:

```python
name = soup.select_one(".product .name")

print(name.get_text(strip=True))
```

---

# 18. CSS Selector vs `find()`

দুটোই শিখবেন।

### `find()`

```python
soup.find(
    "h2",
    class_="name"
)
```

### CSS selector

```python
soup.select_one(
    "h2.name"
)
```

দুটোর result প্রায় একই।

আমি scraping project-এ অনেক সময় CSS selector ব্যবহার করার পরামর্শ দেব কারণ complex HTML-এ এটা খুব flexible।

---

# 19. Nested Elements

ধরুন:

```html
<div class="product">

    <div class="info">

        <h2 class="name">
            Samsung A56
        </h2>

        <div class="price-box">
            <span class="price">
                49999
            </span>
        </div>

    </div>

</div>
```

Selector:

```python
name = soup.select_one(
    ".product .info .name"
)
```

Price:

```python
price = soup.select_one(
    ".product .price-box .price"
)
```

---

# 20. Attribute Extract করা

এটা e-commerce scraping-এ **অত্যন্ত গুরুত্বপূর্ণ**।

HTML:

```html
<a
    class="product-link"
    href="/product/samsung-a56"
>
    Samsung A56
</a>
```

Text:

```python
link = soup.select_one(
    ".product-link"
)

print(link.get_text(strip=True))
```

Output:

```text
Samsung A56
```

কিন্তু URL চাইলে:

```python
print(link["href"])
```

Output:

```text
/product/samsung-a56
```

---

# 21. `.get("href")`

Better practice:

```python
url = link.get("href")

print(url)
```

কারণ attribute না থাকলে error না দিয়ে `None` দিতে পারে।

---

# 22. Image URL

HTML:

```html
<img
    class="product-image"
    src="/images/samsung-a56.jpg"
>
```

Python:

```python
image = soup.select_one(
    ".product-image"
)

image_url = image.get("src")

print(image_url)
```

Output:

```text
/images/samsung-a56.jpg
```

---

# 23. `data-*` Attributes

অনেক website এভাবে data রাখে:

```html
<div
    class="product"
    data-product-id="12345"
>
```

Python:

```python
product = soup.select_one(".product")

product_id = product.get(
    "data-product-id"
)

print(product_id)
```

Output:

```text
12345
```

---

# 24. Real Product Structure

এখন একটু বড় example:

```python
html = """
<div class="product">

    <a
        class="product-link"
        href="/product/samsung-a56"
    >
        <img
            class="product-image"
            src="/images/a56.jpg"
        >

        <h2 class="product-name">
            Samsung Galaxy A56
        </h2>
    </a>

    <div class="price-box">

        <span class="original-price">
            54999
        </span>

        <span class="price">
            49999
        </span>

        <span class="discount">
            9%
        </span>

    </div>

    <div class="rating">
        4.6
    </div>

    <div class="reviews">
        1250 Reviews
    </div>

</div>
"""
```

এখন parse:

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(
    html,
    "html.parser"
)

product = soup.select_one(".product")
```

---

# 25. সব Data Extract

```python
name = product.select_one(
    ".product-name"
).get_text(strip=True)

price = product.select_one(
    ".price"
).get_text(strip=True)

original_price = product.select_one(
    ".original-price"
).get_text(strip=True)

discount = product.select_one(
    ".discount"
).get_text(strip=True)

rating = product.select_one(
    ".rating"
).get_text(strip=True)

reviews = product.select_one(
    ".reviews"
).get_text(strip=True)

link = product.select_one(
    ".product-link"
).get("href")

image = product.select_one(
    ".product-image"
).get("src")
```

তারপর:

```python
print(name)
print(price)
print(original_price)
print(discount)
print(rating)
print(reviews)
print(link)
print(image)
```

---

# 26. কিন্তু এখানে একটা Problem আছে

যদি কোনো product-এ rating না থাকে:

```html
<div class="product">
    ...
</div>
```

তাহলে:

```python
product.select_one(".rating")
```

ফিরিয়ে দিতে পারে:

```python
None
```

তারপর:

```python
None.get_text()
```

করলে error হবে।

---

# 27. Safe Extraction

এভাবে লিখবেন:

```python
rating_element = product.select_one(
    ".rating"
)

if rating_element:
    rating = rating_element.get_text(
        strip=True
    )
else:
    rating = None
```

আরও clean:

```python
rating_element = product.select_one(".rating")

rating = (
    rating_element.get_text(strip=True)
    if rating_element
    else None
)
```

---

# 28. Reusable `get_text()` Function

আমরা একটা helper বানাতে পারি:

```python
def get_text(element):

    if element:
        return element.get_text(
            strip=True
        )

    return None
```

তারপর:

```python
name = get_text(
    product.select_one(".product-name")
)

price = get_text(
    product.select_one(".price")
)

rating = get_text(
    product.select_one(".rating")
)
```

এটা বড় scraper-এ অনেক useful হবে।

---

# 29. Complete Product Parser

```python
from bs4 import BeautifulSoup


def get_text(element):

    if element:
        return element.get_text(
            strip=True
        )

    return None


def parse_product(product):

    data = {

        "name": get_text(
            product.select_one(".product-name")
        ),

        "price": get_text(
            product.select_one(".price")
        ),

        "original_price": get_text(
            product.select_one(".original-price")
        ),

        "discount": get_text(
            product.select_one(".discount")
        ),

        "rating": get_text(
            product.select_one(".rating")
        ),

        "reviews": get_text(
            product.select_one(".reviews")
        ),

        "url": (
            product.select_one(
                ".product-link"
            ).get("href")
            if product.select_one(".product-link")
            else None
        ),

        "image_url": (
            product.select_one(
                ".product-image"
            ).get("src")
            if product.select_one(".product-image")
            else None
        )
    }

    return data
```

এখন:

```python
products = soup.select(".product")

for product in products:

    data = parse_product(product)

    print(data)
```

Result:

```python
{
    "name": "Samsung Galaxy A56",
    "price": "49999",
    "original_price": "54999",
    "discount": "9%",
    "rating": "4.6",
    "reviews": "1250 Reviews",
    "url": "/product/samsung-a56",
    "image_url": "/images/a56.jpg"
}
```

---

# 30. Relative URL → Absolute URL

এটা real scraping-এ খুব গুরুত্বপূর্ণ।

আমরা পেলাম:

```text
/product/samsung-a56
```

কিন্তু database-এ আমরা চাই:

```text
https://example.com/product/samsung-a56
```

Python-এর `urljoin()`:

```python
from urllib.parse import urljoin

base_url = "https://example.com"

relative_url = "/product/samsung-a56"

full_url = urljoin(
    base_url,
    relative_url
)

print(full_url)
```

Output:

```text
https://example.com/product/samsung-a56
```

Image-এর ক্ষেত্রেও:

```python
image_url = urljoin(
    base_url,
    "/images/a56.jpg"
)
```

---

# 31. M01 + M02 একসাথে

এখন আমরা প্রথমবার **actual web scraping pipeline** তৈরি করছি।

```python
import requests

from bs4 import BeautifulSoup
from urllib.parse import urljoin


def fetch_page(url):

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    response = requests.get(
        url,
        headers=headers,
        timeout=10
    )

    response.raise_for_status()

    return response.text


def get_text(element):

    if element:
        return element.get_text(
            strip=True
        )

    return None


def parse_products(html, base_url):

    soup = BeautifulSoup(
        html,
        "html.parser"
    )

    products = []

    for product in soup.select(".product"):

        link = product.select_one(
            ".product-link"
        )

        image = product.select_one(
            ".product-image"
        )

        data = {

            "name": get_text(
                product.select_one(
                    ".product-name"
                )
            ),

            "price": get_text(
                product.select_one(
                    ".price"
                )
            ),

            "rating": get_text(
                product.select_one(
                    ".rating"
                )
            ),

            "url": (
                urljoin(
                    base_url,
                    link.get("href")
                )
                if link
                else None
            ),

            "image_url": (
                urljoin(
                    base_url,
                    image.get("src")
                )
                if image
                else None
            )
        }

        products.append(data)

    return products
```

এখানে architecture:

```text
                 URL
                  ↓
            fetch_page()
                  ↓
                HTML
                  ↓
          BeautifulSoup
                  ↓
          parse_products()
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      Name      Price     Rating
        ↓         ↓         ↓
              Dictionary
                  ↓
                List
```

---

# 32. Browser থেকে Selector বের করা

এটা আপনার জন্য অত্যন্ত গুরুত্বপূর্ণ skill।

Chrome/Chromium-এ website খুলুন।

তারপর:

```text
Right Click
   ↓
Inspect
   ↓
Element select
   ↓
HTML দেখুন
```

ধরুন দেখলেন:

```html
<div class="product-card">
    <h2 class="product-title">
        Laptop XYZ
    </h2>

    <span class="current-price">
        ৳75,000
    </span>
</div>
```

তাহলে selector:

```css
.product-card
.product-title
.current-price
```

Python:

```python
product = soup.select_one(
    ".product-card"
)

name = product.select_one(
    ".product-title"
)

price = product.select_one(
    ".current-price"
)
```

---

# 33. CSS Selector-এর আরও গুরুত্বপূর্ণ অংশ

### Class

```css
.product
```

### ID

```css
#products
```

### Tag

```css
h2
```

### Tag + class

```css
h2.product-title
```

### Parent → child

```css
.product .price
```

### Direct child

```css
.product > .price
```

### Attribute

```css
a[href]
```

### Specific attribute

```css
a[href="/product/test"]
```

### Attribute contains

```css
a[href*="/product/"]
```

এগুলো scraping-এ বারবার ব্যবহার করবেন।

---

# 34. সবচেয়ে বড় ভুল

অনেকে শুধু:

```python
soup.find("div")
```

দিয়ে scraping করতে যায়।

এটা dangerous।

কারণ website-এ শত শত `<div>` থাকতে পারে।

বরং:

```python
soup.select(".product-card")
```

এর মতো **specific selector** ব্যবহার করবেন।

---

# 35. `text` vs `get_text()`

আপনি দেখতে পারেন:

```python
element.text
```

এবং:

```python
element.get_text(strip=True)
```

আমি সাধারণত দ্বিতীয়টি recommend করব:

```python
name = element.get_text(
    strip=True
)
```

কারণ HTML-এর whitespace/newline clean হয়ে যায়।

---

# 36. `attrs`

Element-এর সব attributes:

```python
print(element.attrs)
```

যেমন:

```python
{
    "class": ["product"],
    "data-id": "123"
}
```

Specific:

```python
print(element.get("data-id"))
```

---

# 37. M02 Mini Project

এখন আপনার task:

একটা HTML page ধরে **10টি product** বানান।

প্রতিটি product-এ রাখুন:

```text
name
price
original_price
discount
rating
review_count
product_url
image_url
```

তারপর BeautifulSoup দিয়ে output করুন:

```text
Product 1
Name: Samsung A56
Price: 49999
Discount: 9%
Rating: 4.6
Reviews: 1250
URL: ...
Image: ...

Product 2
Name: iPhone 17
Price: 129999
...
```

---

# 38. M02 Challenge

নিজে এমন HTML তৈরি করুন:

```html
<div class="product-card">

    <a class="product-link"
       href="/products/laptop-1">

        <img
            class="product-image"
            src="/images/laptop-1.jpg"
        >

        <h2 class="product-title">
            Lenovo IdeaPad
        </h2>

    </a>

    <span class="old-price">
        85000
    </span>

    <span class="current-price">
        75000
    </span>

    <span class="discount">
        12%
    </span>

    <span class="rating">
        4.5
    </span>

    <span class="review-count">
        450
    </span>

</div>
```

এবং Python দিয়ে output করুন:

```text
Name: Lenovo IdeaPad
Old Price: 85000
Current Price: 75000
Discount: 12%
Rating: 4.5
Reviews: 450
Product URL: https://example.com/products/laptop-1
Image URL: https://example.com/images/laptop-1.jpg
```

---

# 39. M02 শেষে আপনার Skill

এখন আপনার mental model হওয়া উচিত:

```text
                  WEBSITE
                     ↓
                 requests
                     ↓
                    HTML
                     ↓
              BeautifulSoup
                     ↓
             ┌───────┴────────┐
             ↓                ↓
          Selector           Parser
             ↓                ↓
       Product Element     Attributes
             ↓                ↓
       ┌─────┼─────┐      href/src
       ↓     ↓     ↓
      Name Price Rating
             ↓
          Dictionary
             ↓
             List
```

আর সবচেয়ে গুরুত্বপূর্ণ reusable pattern:

```python
response = requests.get(url)

soup = BeautifulSoup(
    response.text,
    "html.parser"
)

products = soup.select(
    ".product-card"
)

for product in products:

    name = product.select_one(
        ".product-title"
    )

    price = product.select_one(
        ".current-price"
    )

    print(
        name.get_text(strip=True)
    )

    print(
        price.get_text(strip=True)
    )
```

**M01 = website থেকে HTML আনা।**
**M02 = HTML-এর ভিতর থেকে structured product data বের করা।**

পরের ধাপে **M03 — Pagination + Multiple Product Pages + URL Traversal** শিখলে আমরা একটি category page-এর **page 1 → page 2 → page 3 → ...** ঘুরে শত/হাজার product collect করার real scraper architecture-এ ঢুকব।

---
# M03 — Pagination + Multiple Product Pages + URL Traversal

M02-এ আমরা শিখেছি:

```text id="6p3v5f"
HTML
 ↓
BeautifulSoup
 ↓
CSS Selector
 ↓
Product data
```

কিন্তু বাস্তব e-commerce website-এ সাধারণত এক page-এ সব product থাকে না।

যেমন:

```text id="4hpl0q"
Page 1 → 20 products
Page 2 → 20 products
Page 3 → 20 products
Page 4 → 20 products
...
Page 50 → 20 products
```

তাই M03-এর লক্ষ্য:

> **একাধিক page automatically visit করে সব product collect করা।**

---

# 1. M03-এর Complete Flow

```text id="0yd4q1"
Category Page
     ↓
Page 1
     ↓
Extract products
     ↓
Find next page
     ↓
Page 2
     ↓
Extract products
     ↓
Find next page
     ↓
Page 3
     ↓
...
     ↓
No next page
     ↓
Stop
```

---

# 2. Pagination কী?

ধরুন URL:

```text id="z6g0a4"
https://example.com/products?page=1
https://example.com/products?page=2
https://example.com/products?page=3
```

এখানে:

```text id="w0n1sk"
?page=1
?page=2
?page=3
```

হলো pagination parameter।

---

# 3. Simple Pagination

Python:

```python id="m8i1l4"
import requests
from bs4 import BeautifulSoup

base_url = "https://example.com/products"

for page in range(1, 6):

    params = {
        "page": page
    }

    response = requests.get(
        base_url,
        params=params,
        headers={
            "User-Agent": "Mozilla/5.0"
        },
        timeout=10
    )

    response.raise_for_status()

    print(
        "Page:",
        page,
        "URL:",
        response.url
    )
```

Output:

```text id="x9b0as"
Page: 1 URL: https://example.com/products?page=1
Page: 2 URL: https://example.com/products?page=2
Page: 3 URL: https://example.com/products?page=3
Page: 4 URL: https://example.com/products?page=4
Page: 5 URL: https://example.com/products?page=5
```

---

# 4. Pagination থেকে Product Extract

ধরুন প্রতিটি page:

```html id="g6r5zy"
<div class="product-card">
    <h2 class="product-title">
        Samsung A56
    </h2>

    <span class="price">
        49999
    </span>
</div>
```

তাহলে:

```python id="caj4l4"
import requests
from bs4 import BeautifulSoup

base_url = "https://example.com/products"

for page in range(1, 6):

    response = requests.get(
        base_url,
        params={"page": page},
        headers={"User-Agent": "Mozilla/5.0"},
        timeout=10
    )

    response.raise_for_status()

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    products = soup.select(
        ".product-card"
    )

    print(
        f"Page {page}: "
        f"{len(products)} products"
    )
```

Output:

```text id="dy9e6g"
Page 1: 20 products
Page 2: 20 products
Page 3: 20 products
Page 4: 20 products
Page 5: 20 products
```

---

# 5. Product Data Collect

এখন M02-এর parsing logic যোগ করি।

```python id="sv5fkm"
import requests

from bs4 import BeautifulSoup


def get_text(element):

    if element:
        return element.get_text(
            strip=True
        )

    return None


def parse_product(product):

    return {

        "name": get_text(
            product.select_one(
                ".product-title"
            )
        ),

        "price": get_text(
            product.select_one(
                ".price"
            )
        ),

        "rating": get_text(
            product.select_one(
                ".rating"
            )
        )
    }
```

---

# 6. Multiple Pages + Parser

```python id="32m24x"
import requests

from bs4 import BeautifulSoup


def get_text(element):

    if element:
        return element.get_text(
            strip=True
        )

    return None


def parse_product(product):

    return {

        "name": get_text(
            product.select_one(
                ".product-title"
            )
        ),

        "price": get_text(
            product.select_one(
                ".price"
            )
        ),

        "rating": get_text(
            product.select_one(
                ".rating"
            )
        )
    }


all_products = []

base_url = "https://example.com/products"


for page in range(1, 6):

    response = requests.get(
        base_url,
        params={"page": page},
        headers={
            "User-Agent": "Mozilla/5.0"
        },
        timeout=10
    )

    response.raise_for_status()

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    products = soup.select(
        ".product-card"
    )

    for product in products:

        data = parse_product(
            product
        )

        all_products.append(data)


print(
    "Total products:",
    len(all_products)
)
```

এখন:

```text id="1cm8f4"
Page 1 → 20
Page 2 → 20
Page 3 → 20
Page 4 → 20
Page 5 → 20

Total = 100 products
```

---

# 7. `while` Loop দিয়ে Pagination

কিন্তু একটা সমস্যা আছে।

আমরা যদি না জানি কত page আছে?

```text id="hknx9t"
Page 1
Page 2
Page 3
...
Page ?
```

তাহলে `for range()` ideal নয়।

আমরা `while` ব্যবহার করতে পারি।

```python id="4drw8d"
page = 1

while True:

    print("Scraping page:", page)

    page += 1
```

কিন্তু কখন stop করব?

---

# 8. Product না পাওয়া গেলে Stop

```python id="73t7q4"
page = 1

while True:

    response = requests.get(
        base_url,
        params={"page": page},
        headers={
            "User-Agent": "Mozilla/5.0"
        },
        timeout=10
    )

    response.raise_for_status()

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    products = soup.select(
        ".product-card"
    )

    if not products:
        print("No more products.")
        break

    print(
        f"Page {page}: "
        f"{len(products)} products"
    )

    page += 1
```

এখানে:

```text id="6l25fl"
products = []
```

হলে:

```python id="9e3xpr"
break
```

করবে।

---

# 9. কিন্তু এই method-এর সমস্যা

কিছু website-এর invalid page-এও একই page-এর product দেখাতে পারে।

তাই শুধু:

```python id="2tq5c8"
if not products:
```

সবসময় reliable নয়।

আরেকটি method:

**Next button detect করা।**

---

# 10. Next Button

HTML:

```html id="n8t4w4"
<a class="next-page"
   href="/products?page=2">
    Next
</a>
```

BeautifulSoup:

```python id="rxskx2"
next_button = soup.select_one(
    ".next-page"
)
```

তারপর:

```python id="r7sp4n"
if next_button:

    next_url = next_button.get(
        "href"
    )

else:

    next_url = None
```

---

# 11. `urljoin()`

ধরুন:

```text id="zzqgj0"
/products?page=2
```

আমাদের দরকার:

```text id="y4x2w7"
https://example.com/products?page=2
```

```python id="69jyhh"
from urllib.parse import urljoin

next_url = urljoin(
    current_url,
    next_button.get("href")
)
```

---

# 12. Next Button Based Scraper

এটাই বাস্তব scraping-এর একটি গুরুত্বপূর্ণ pattern:

```python id="8e9b6x"
import requests

from bs4 import BeautifulSoup
from urllib.parse import urljoin


url = "https://example.com/products"

all_products = []


while url:

    print(
        "Scraping:",
        url
    )

    response = requests.get(
        url,
        headers={
            "User-Agent": "Mozilla/5.0"
        },
        timeout=10
    )

    response.raise_for_status()

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    products = soup.select(
        ".product-card"
    )

    for product in products:

        name = product.select_one(
            ".product-title"
        )

        price = product.select_one(
            ".price"
        )

        data = {

            "name": (
                name.get_text(strip=True)
                if name
                else None
            ),

            "price": (
                price.get_text(strip=True)
                if price
                else None
            )
        }

        all_products.append(data)


    next_button = soup.select_one(
        ".next-page"
    )


    if next_button:

        next_href = next_button.get(
            "href"
        )

        url = urljoin(
            url,
            next_href
        )

    else:

        url = None


print(
    "Total:",
    len(all_products)
)
```

---

# 13. এটা কীভাবে কাজ করছে?

```text id="x6y9kp"
url = Page 1
      ↓
request
      ↓
HTML
      ↓
products extract
      ↓
Next button?
      ↓
YES
      ↓
Page 2
      ↓
request
      ↓
HTML
      ↓
products extract
      ↓
Next button?
      ↓
YES
      ↓
Page 3
      ↓
...
      ↓
Next button নেই
      ↓
STOP
```

---

# 14. URL Traversal কী?

ধরুন category page:

```text id="sq7u0v"
https://example.com/category/laptops
```

সেখানে products-এর link:

```text id="v5s2c7"
/product/lenovo-ideapad
/product/hp-pavilion
/product/dell-inspiron
```

আমরা category page থেকে product URL collect করে **প্রতিটি product page-এ ঢুকতে পারি।**

এটিই URL traversal-এর basic idea।

---

# 15. Category → Product Page

```text id="e4qv9m"
Category Page
     │
     ├── Product 1 URL
     ├── Product 2 URL
     ├── Product 3 URL
     └── Product 4 URL
              │
              ↓
        Product Details
```

---

# 16. Product Link Collect

HTML:

```html id="0thjra"
<div class="product-card">

    <a
        class="product-link"
        href="/product/laptop-1"
    >
        Laptop 1
    </a>

</div>
```

Python:

```python id="q8jjl2"
links = soup.select(
    ".product-link"
)

for link in links:

    href = link.get("href")

    print(href)
```

Output:

```text id="qj8mli"
/product/laptop-1
/product/laptop-2
/product/laptop-3
```

---

# 17. Full Product URLs

```python id="g7o4iu"
from urllib.parse import urljoin

base_url = "https://example.com"

for link in links:

    href = link.get("href")

    full_url = urljoin(
        base_url,
        href
    )

    print(full_url)
```

Output:

```text id="2ctuw9"
https://example.com/product/laptop-1
https://example.com/product/laptop-2
https://example.com/product/laptop-3
```

---

# 18. Product Details Page Scrape

ধরুন product detail page:

```html id="s1g9hk"
<h1 class="product-name">
    Lenovo IdeaPad
</h1>

<span class="price">
    75000
</span>

<div class="description">
    Powerful laptop...
</div>
```

Function:

```python id="e6id1s"
def scrape_product_page(url):

    response = requests.get(
        url,
        headers={
            "User-Agent": "Mozilla/5.0"
        },
        timeout=10
    )

    response.raise_for_status()

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    name = soup.select_one(
        ".product-name"
    )

    price = soup.select_one(
        ".price"
    )

    description = soup.select_one(
        ".description"
    )

    return {

        "name": (
            name.get_text(strip=True)
            if name
            else None
        ),

        "price": (
            price.get_text(strip=True)
            if price
            else None
        ),

        "description": (
            description.get_text(
                " ",
                strip=True
            )
            if description
            else None
        )
    }
```

---

# 19. Category → Product Detail Pipeline

এখন পুরো process:

```python id="t0hmne"
import requests

from bs4 import BeautifulSoup
from urllib.parse import urljoin


category_url = (
    "https://example.com/products"
)


response = requests.get(
    category_url,
    headers={
        "User-Agent": "Mozilla/5.0"
    },
    timeout=10
)

response.raise_for_status()


soup = BeautifulSoup(
    response.text,
    "html.parser"
)


product_links = soup.select(
    ".product-link"
)


for link in product_links:

    href = link.get("href")

    product_url = urljoin(
        category_url,
        href
    )

    print(product_url)
```

---

# 20. তারপর প্রতিটি URL Scrape

```python id="ec7dx7"
for link in product_links:

    href = link.get("href")

    product_url = urljoin(
        category_url,
        href
    )

    data = scrape_product_page(
        product_url
    )

    print(data)
```

Output:

```python id="t2t6a5"
{
    "name": "Lenovo IdeaPad",
    "price": "75000",
    "description": "Powerful laptop..."
}
```

---

# 21. Pagination + Product Details

এখন আসল architecture:

```text id="5bpx3g"
                 Category
                    │
              ┌─────┴─────┐
              ↓             ↓
           Page 1         Page 2
              ↓             ↓
         Product URLs  Product URLs
              ↓             ↓
       ┌──────┼─────────────┐
       ↓      ↓             ↓
    Product Product      Product
      Page     Page         Page
       ↓        ↓            ↓
     Name     Price       Rating
       │        │            │
       └────────┼────────────┘
                ↓
           All Products
```

এটাই multi-page e-commerce scraper-এর foundation।

---

# 22. Duplicate URL Problem

Pagination-এ একই product কখনো একাধিক জায়গায় আসতে পারে।

তাই:

```python id="q10w6q"
product_urls = set()
```

`set()` duplicate remove করে।

```python id="0g8y3b"
product_urls.add(
    product_url
)
```

তারপর:

```python id="9r5q66"
for url in product_urls:
    print(url)
```

---

# 23. URL Deduplication

```python id="npr4gj"
product_urls = set()

for link in soup.select(
    ".product-link"
):

    href = link.get("href")

    if href:

        full_url = urljoin(
            category_url,
            href
        )

        product_urls.add(
            full_url
        )

print(
    "Unique URLs:",
    len(product_urls)
)
```

---

# 24. Request Delay

একসাথে অনেক request পাঠানো উচিত নয়।

Basic delay:

```python id="m1fv5r"
import time

time.sleep(1)
```

যেমন:

```python id="qjv3km"
for url in product_urls:

    data = scrape_product_page(url)

    time.sleep(1)
```

এতে server-এর ওপর unnecessary load কমে।

Website-এর stated rate limits/robots rules থাকলে সেগুলো follow করবেন।

---

# 25. Retry Logic

Network error হতে পারে।

```python id="x6t7s4"
import requests
import time


def fetch_page(url, retries=3):

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    for attempt in range(retries):

        try:

            response = requests.get(
                url,
                headers=headers,
                timeout=10
            )

            response.raise_for_status()

            return response.text

        except requests.RequestException as e:

            print(
                f"Attempt {attempt + 1} failed:",
                e
            )

            time.sleep(2)

    return None
```

এখন:

```python id="k40t6q"
html = fetch_page(url)

if html:
    print("Success")
else:
    print("Failed")
```

---

# 26. গুরুত্বপূর্ণ: 429

যদি server দেয়:

```text id="2svj9p"
429 Too Many Requests
```

এর অর্থ সাধারণত আপনি খুব দ্রুত বা বেশি request করছেন।

এক্ষেত্রে:

```text id="i5fhsc"
❌ request speed বাড়াবেন না
❌ anti-bot bypass করার চেষ্টা করবেন না

✅ request কমান
✅ delay দিন
✅ documented rate limit মানুন
✅ API থাকলে API ব্যবহার করুন
```

---

# 27. `robots.txt`

অনেক website:

```text id="b5bqzw"
https://example.com/robots.txt
```

দিয়ে crawler-related rules প্রকাশ করে।

Python:

```python id="5e7yrw"
import requests

url = "https://example.com/robots.txt"

response = requests.get(
    url,
    timeout=10
)

print(response.text)
```

এটা technical permission-এর একমাত্র source নয়—website-এর Terms of Service এবং applicable law-ও বিবেচনা করবেন।

---

# 28. M03 Complete Mini Scraper Structure

এখন project:

```text id="8nq4cu"
m03_ecommerce_scraper/
│
├── scraper.py
│
├── data/
│   └── products.json
│
└── requirements.txt
```

`requirements.txt`:

```text id="p4z86v"
requests
beautifulsoup4
```

---

# 29. M03 Final Code Pattern

একটা clean version:

```python id="7kg9dp"
import time
import requests

from bs4 import BeautifulSoup
from urllib.parse import urljoin


HEADERS = {
    "User-Agent": "Mozilla/5.0"
}


def fetch_page(url):

    try:

        response = requests.get(
            url,
            headers=HEADERS,
            timeout=10
        )

        response.raise_for_status()

        return response.text

    except requests.RequestException as e:

        print("Request error:", e)

        return None


def get_text(element):

    if element:

        return element.get_text(
            strip=True
        )

    return None


def scrape_category_page(url):

    html = fetch_page(url)

    if not html:
        return [], None

    soup = BeautifulSoup(
        html,
        "html.parser"
    )

    product_urls = set()


    for link in soup.select(
        ".product-link"
    ):

        href = link.get("href")

        if href:

            full_url = urljoin(
                url,
                href
            )

            product_urls.add(
                full_url
            )


    next_button = soup.select_one(
        ".next-page"
    )


    if next_button:

        next_href = next_button.get(
            "href"
        )

        next_url = urljoin(
            url,
            next_href
        )

    else:

        next_url = None


    return (
        list(product_urls),
        next_url
    )


def scrape_product_page(url):

    html = fetch_page(url)

    if not html:
        return None

    soup = BeautifulSoup(
        html,
        "html.parser"
    )


    return {

        "name": get_text(
            soup.select_one(
                ".product-name"
            )
        ),

        "price": get_text(
            soup.select_one(
                ".price"
            )
        ),

        "rating": get_text(
            soup.select_one(
                ".rating"
            )
        ),

        "description": get_text(
            soup.select_one(
                ".description"
            )
        ),

        "url": url
    }


category_url = (
    "https://example.com/products"
)


all_product_urls = set()

current_url = category_url


while current_url:

    print(
        "Category:",
        current_url
    )

    urls, next_url = (
        scrape_category_page(
            current_url
        )
    )

    all_product_urls.update(
        urls
    )

    current_url = next_url

    time.sleep(1)


print(
    "Unique products:",
    len(all_product_urls)
)


all_products = []


for product_url in all_product_urls:

    print(
        "Product:",
        product_url
    )

    product = scrape_product_page(
        product_url
    )

    if product:

        all_products.append(
            product
        )

    time.sleep(1)


print(
    "Collected:",
    len(all_products)
)
```

**এই code-টা সরাসরি কোনো নির্দিষ্ট e-commerce site-এ paste করলেই কাজ করবে না**, কারণ `.product-link`, `.next-page`, `.product-name`, `.price` ইত্যাদি selector website অনুযায়ী পরিবর্তন করতে হবে।

---

# 30. M03-এ সবচেয়ে গুরুত্বপূর্ণ Concept

### Concept 1

```text
Pagination
```

```text
Page 1
 ↓
Page 2
 ↓
Page 3
```

### Concept 2

```text
URL Traversal
```

```text
Category
 ↓
Product URL
 ↓
Product detail
```

### Concept 3

```text
Deduplication
```

```python id="1w7l6p"
set()
```

### Concept 4

```text
Rate control
```

```python id="q9o5ut"
time.sleep()
```

### Concept 5

```text
Error handling
```

```python id="1uvt1w"
try:
    ...
except requests.RequestException:
    ...
```

---

# 31. M01 → M03 এখন পর্যন্ত

```text id="cm0dne"
M01
Requests
  │
  └── Website → HTML


M02
BeautifulSoup
  │
  └── HTML → Product Data


M03
Pagination + URL Traversal
  │
  ├── Page 1
  ├── Page 2
  ├── Page 3
  │
  └── Product Detail Pages
          ↓
       All Products
```

এর পরের logical step হলো **M04 — Data Cleaning & Normalization**: scraped price যেমন `৳75,000`, `75,000 Tk`, `$999`, rating `4.5/5`, reviews `1.2K`—এসবকে clean করে একই database schema-তে রাখা। এটা না শিখলে different e-commerce website-এর data একসাথে analysis করা কঠিন হবে।

----
# M04 — Data Cleaning & Normalization Deep Dive

M01–M03-এ আমরা শিখেছি:

```text
M01 → Website থেকে HTML collect
M02 → HTML থেকে product data extract
M03 → Pagination + Product URL traversal
```

এখন সবচেয়ে গুরুত্বপূর্ণ একটা সমস্যা সামনে আসবে।

Different e-commerce website একই information **different format-এ** দেয়।

উদাহরণ:

```text
Website A → ৳75,000
Website B → 75000 Tk
Website C → BDT 75,000
Website D → ৳ 75,000
```

কিন্তু database-এ আমরা চাই:

```text
75000
```

এটাই **Data Cleaning + Normalization**।

---

# 1. M04-এর Goal

M04 শেষে raw scraped data:

```text
৳75,000
4.5/5
1.2K Reviews
In Stock
Samsung Electronics
```

কে convert করব:

```python
{
    "price": 75000.0,
    "rating": 4.5,
    "review_count": 1200,
    "availability": "in_stock",
    "brand": "Samsung"
}
```

অর্থাৎ:

```text
RAW DATA
   ↓
Cleaning
   ↓
Normalization
   ↓
Structured Data
   ↓
Database / Pandas
```

---

# 2. কেন Data Cleaning এত গুরুত্বপূর্ণ?

ধরুন 3টা website থেকে price পেলাম:

```python
prices = [
    "৳75,000",
    "75000 Tk",
    "BDT 75,000"
]
```

Pandas-এ সরাসরি average করলে সমস্যা হবে।

আমাদের convert করতে হবে:

```python
[
    75000,
    75000,
    75000
]
```

তারপর:

```python
average = 75000
```

---

# 3. Raw Data সাধারণত কেমন হয়?

Scraper থেকে:

```python
product = {
    "name": " Samsung Galaxy A56 ",
    "price": "৳ 49,999",
    "old_price": "৳54,999",
    "discount": "9% OFF",
    "rating": "4.6/5",
    "reviews": "1.2K Reviews",
    "availability": "In Stock"
}
```

এগুলো database-ready নয়।

---

# 4. String Cleaning

প্রথমে whitespace remove:

```python
name = " Samsung Galaxy A56 "

print(name.strip())
```

Output:

```text
Samsung Galaxy A56
```

---

## `.strip()`

```python
text = "   Hello World   "

clean = text.strip()

print(clean)
```

---

# 5. `.lower()`

Comparison-এর জন্য:

```python
status = "In Stock"

print(status.lower())
```

Output:

```text
in stock
```

---

# 6. `.upper()`

```python
brand = "samsung"

print(brand.upper())
```

Output:

```text
SAMSUNG
```

---

# 7. `.replace()`

```python
price = "৳75,000"

price = price.replace(
    "৳",
    ""
)

print(price)
```

Output:

```text
75,000
```

Comma:

```python
price = price.replace(
    ",",
    ""
)

print(price)
```

Output:

```text
75000
```

---

# 8. Basic Price Cleaning

```python
price = "৳75,000"

price = price.replace("৳", "")
price = price.replace(",", "")
price = price.strip()

price = float(price)

print(price)
```

Output:

```text
75000.0
```

---

# 9. কিন্তু Different Format?

ধরুন:

```text
৳75,000
75000 Tk
BDT 75,000
Tk. 75,000
৳ 75,000
75,000 BDT
```

প্রতিটা আলাদা করে replace করা cumbersome।

এখানে **Regex** ব্যবহার করব।

---

# 10. Regex কী?

Regex = Regular Expression

এটা text-এর মধ্যে pattern খুঁজতে ব্যবহার হয়।

Python:

```python
import re
```

ধরুন:

```python
text = "৳75,000"
```

শুধু digits চাই:

```python
numbers = re.findall(
    r"\d+",
    text
)

print(numbers)
```

Output:

```text
['75', '000']
```

Comma থাকার কারণে দুই অংশ হয়েছে।

---

# 11. Price থেকে Number Extract

Better:

```python
text = "৳75,000"

clean = re.sub(
    r"[^\d.]",
    "",
    text
)

print(clean)
```

Output:

```text
75000
```

তারপর:

```python
price = float(clean)

print(price)
```

Output:

```text
75000.0
```

---

# 12. Reusable Price Function

এটা খুব গুরুত্বপূর্ণ।

```python
import re


def clean_price(value):

    if value is None:
        return None

    value = str(value)

    value = re.sub(
        r"[^\d.]",
        "",
        value
    )

    if not value:
        return None

    return float(value)
```

Test:

```python
prices = [
    "৳75,000",
    "75000 Tk",
    "BDT 75,000",
    "৳ 75,000"
]

for price in prices:

    print(
        clean_price(price)
    )
```

Output:

```text
75000.0
75000.0
75000.0
75000.0
```

---

# 13. Price Range Problem

ধরুন:

```text
৳50,000 - ৳60,000
```

আমাদের function:

```python
clean_price(
    "৳50,000 - ৳60,000"
)
```

দিলে:

```text
5000060000
```

ভুল হবে।

তাই বুঝতে হবে **price field কী ধরনের data represent করছে**।

যদি single product price হয়, তাহলে range থাকার কথা নয়।

Data cleaning-এর সময় invalid format detect করা দরকার।

---

# 14. Rating Cleaning

Raw:

```text
"4.6/5"
```

আমাদের চাই:

```text
4.6
```

Simple:

```python
rating = "4.6/5"

rating = rating.split("/")[0]

rating = float(rating)

print(rating)
```

Output:

```text
4.6
```

---

# 15. Rating Function

```python
import re


def clean_rating(value):

    if value is None:
        return None

    match = re.search(
        r"\d+(\.\d+)?",
        str(value)
    )

    if not match:
        return None

    return float(match.group())
```

Test:

```python
ratings = [
    "4.6/5",
    "4.8",
    "Rating: 4.2",
    "4.5 stars"
]

for rating in ratings:

    print(
        clean_rating(rating)
    )
```

Output:

```text
4.6
4.8
4.2
4.5
```

---

# 16. Rating Validation

ধরুন:

```text
"8.9/5"
```

এটা mathematically invalid।

তাই:

```python
def clean_rating(value):

    if value is None:
        return None

    match = re.search(
        r"\d+(\.\d+)?",
        str(value)
    )

    if not match:
        return None

    rating = float(match.group())

    if 0 <= rating <= 5:
        return rating

    return None
```

এখন:

```python
print(clean_rating("8.9/5"))
```

Output:

```text
None
```

---

# 17. Review Count Cleaning

Raw data:

```text
1,250 Reviews
```

আমাদের চাই:

```text
1250
```

```python
import re


def clean_review_count(value):

    if value is None:
        return None

    value = str(value)

    value = re.sub(
        r"[^\d]",
        "",
        value
    )

    if not value:
        return None

    return int(value)
```

Test:

```python
print(
    clean_review_count(
        "1,250 Reviews"
    )
)
```

Output:

```text
1250
```

---

# 18. কিন্তু `1.2K`?

E-commerce website-এ প্রায়ই:

```text
1.2K Reviews
```

থাকে।

আমাদের চাই:

```text
1200
```

Function:

```python
import re


def clean_review_count(value):

    if value is None:
        return None

    text = str(value).strip().upper()

    match = re.search(
        r"(\d+(?:\.\d+)?)\s*([KMB]?)",
        text
    )

    if not match:
        return None

    number = float(match.group(1))
    suffix = match.group(2)

    if suffix == "K":
        number *= 1_000

    elif suffix == "M":
        number *= 1_000_000

    elif suffix == "B":
        number *= 1_000_000_000

    return int(number)
```

Test:

```python
tests = [
    "1.2K Reviews",
    "5K Reviews",
    "1.5M Reviews",
    "1250 Reviews"
]

for value in tests:

    print(
        value,
        "→",
        clean_review_count(value)
    )
```

Output:

```text
1.2K Reviews → 1200
5K Reviews → 5000
1.5M Reviews → 1500000
1250 Reviews → 1250
```

---

# 19. Discount Cleaning

Raw:

```text
"20% OFF"
```

আমাদের:

```text
20
```

```python
import re


def clean_discount(value):

    if value is None:
        return None

    match = re.search(
        r"\d+(?:\.\d+)?",
        str(value)
    )

    if not match:
        return None

    return float(match.group())
```

Test:

```python
print(
    clean_discount("20% OFF")
)
```

Output:

```text
20.0
```

---

# 20. Availability Normalization

Different websites:

```text
In Stock
Available
Available Now
Out of Stock
Unavailable
Sold Out
```

আমরা চাই:

```text
in_stock
out_of_stock
```

Function:

```python
def normalize_availability(value):

    if value is None:
        return None

    text = value.strip().lower()

    if text in [
        "in stock",
        "available",
        "available now"
    ]:
        return "in_stock"

    if text in [
        "out of stock",
        "unavailable",
        "sold out"
    ]:
        return "out_of_stock"

    return "unknown"
```

Test:

```python
tests = [
    "In Stock",
    "Available",
    "Sold Out",
    "Out of Stock"
]

for value in tests:

    print(
        value,
        "→",
        normalize_availability(value)
    )
```

---

# 21. Brand Normalization

Different websites:

```text
Samsung
SAMSUNG
samsung
Samsung Electronics
```

আপনি standard করতে পারেন:

```python
def normalize_brand(value):

    if not value:
        return None

    text = value.strip().lower()

    mapping = {
        "samsung": "Samsung",
        "samsung electronics":
            "Samsung"
    }

    return mapping.get(
        text,
        value.strip()
    )
```

---

# 22. Category Normalization

এক website:

```text
Mobile
```

অন্যটি:

```text
Smartphone
```

আরেকটি:

```text
Mobile Phones
```

আপনার common schema:

```text
Smartphone
```

Function:

```python
def normalize_category(value):

    if not value:
        return None

    text = value.strip().lower()

    mapping = {

        "mobile": "Smartphone",

        "mobile phone":
            "Smartphone",

        "mobile phones":
            "Smartphone",

        "smartphone":
            "Smartphone"
    }

    return mapping.get(
        text,
        value.strip()
    )
```

---

# 23. Product Name Cleaning

Product name-এ extra whitespace থাকতে পারে:

```text
"  Samsung   Galaxy   A56  "
```

Simple:

```python
def clean_text(value):

    if value is None:
        return None

    return " ".join(
        value.split()
    )
```

Test:

```python
name = "  Samsung   Galaxy   A56  "

print(
    clean_text(name)
)
```

Output:

```text
Samsung Galaxy A56
```

---

# 24. URL Cleaning

Raw:

```text
/product/samsung-a56
```

আমাদের:

```text
https://example.com/product/samsung-a56
```

M03-এ শিখেছিলাম:

```python
from urllib.parse import urljoin

full_url = urljoin(
    base_url,
    relative_url
)
```

---

# 25. Image URL

Same:

```python
image_url = urljoin(
    base_url,
    image_url
)
```

তাই database-এ সবসময় absolute URL রাখা convenient।

---

# 26. Date/Time

প্রতিটি scraped product-এর সঙ্গে:

```text
scraped_at
```

রাখা খুব useful।

```python
from datetime import datetime

scraped_at = datetime.now()

print(scraped_at)
```

Output-এর মতো:

```text
2026-09-07 00:42:10
```

Timezone-aware application হলে production project-এ UTC timestamp ব্যবহার করা ভালো।

---

# 27. Complete Cleaning Pipeline

এখন একটা raw product:

```python
raw_product = {

    "name":
        "  Samsung   Galaxy A56  ",

    "price":
        "৳ 49,999",

    "old_price":
        "৳54,999",

    "discount":
        "9% OFF",

    "rating":
        "4.6/5",

    "reviews":
        "1.2K Reviews",

    "availability":
        "In Stock",

    "brand":
        "SAMSUNG",

    "category":
        "Mobile Phones"
}
```

আমরা clean করব।

---

# 28. Complete Normalizer

```python
def normalize_product(product):

    return {

        "name": clean_text(
            product.get("name")
        ),

        "price": clean_price(
            product.get("price")
        ),

        "old_price": clean_price(
            product.get("old_price")
        ),

        "discount": clean_discount(
            product.get("discount")
        ),

        "rating": clean_rating(
            product.get("rating")
        ),

        "review_count": clean_review_count(
            product.get("reviews")
        ),

        "availability":
            normalize_availability(
                product.get("availability")
            ),

        "brand":
            normalize_brand(
                product.get("brand")
            ),

        "category":
            normalize_category(
                product.get("category")
            )
    }
```

---

# 29. Test

```python
cleaned = normalize_product(
    raw_product
)

print(cleaned)
```

Result:

```python
{
    "name": "Samsung Galaxy A56",
    "price": 49999.0,
    "old_price": 54999.0,
    "discount": 9.0,
    "rating": 4.6,
    "review_count": 1200,
    "availability": "in_stock",
    "brand": "Samsung",
    "category": "Smartphone"
}
```

এখন এটা database/Pandas-এর জন্য অনেক বেশি useful।

---

# 30. Data Validation

Cleaning-এর পর validation করতে হবে।

ধরুন:

```python
product = {
    "price": -5000,
    "rating": 9.5,
    "discount": 150
}
```

এগুলো invalid।

---

# 31. Price Validation

```python
def validate_price(price):

    if price is None:
        return False

    return price >= 0
```

---

# 32. Rating Validation

```python
def validate_rating(rating):

    if rating is None:
        return True

    return 0 <= rating <= 5
```

---

# 33. Discount Validation

```python
def validate_discount(discount):

    if discount is None:
        return True

    return 0 <= discount <= 100
```

---

# 34. Product Validation

```python
def validate_product(product):

    if not product.get("name"):
        return False

    if not validate_price(
        product.get("price")
    ):
        return False

    if not validate_rating(
        product.get("rating")
    ):
        return False

    if not validate_discount(
        product.get("discount")
    ):
        return False

    return True
```

---

# 35. Cleaning + Validation

Ideal pipeline:

```text
Raw Product
     ↓
Clean
     ↓
Normalize
     ↓
Validate
     ↓
Valid?
  /     \
YES      NO
 ↓        ↓
Store   Reject/Log
```

---

# 36. Missing Data

সব product-এর সব information পাওয়া যাবে না।

Example:

```python
{
    "name": "Laptop XYZ",
    "price": "75000",
    "rating": None,
    "reviews": None
}
```

এটা necessarily bad data নয়।

Rating না থাকলে:

```text
rating = NULL
```

রাখতে পারেন।

**Fake value দেবেন না।**

যেমন:

```python
rating = 0
```

দেওয়া ভুল হতে পারে।

কারণ:

```text
0 rating
```

এবং:

```text
rating unavailable
```

এক জিনিস নয়।

---

# 37. Duplicate Products

Different websites একই product sell করতে পারে।

Example:

```text
Website A:
Samsung Galaxy A56 8GB 256GB

Website B:
Samsung A56 8/256 GB

Website C:
Samsung Galaxy A56 Smartphone
```

এগুলো potentially একই product।

এই problem:

> **Entity Resolution / Product Matching**

এটা M04-এর advanced অংশ, এবং পরে আলাদা module-এ আমরা fuzzy matching, SKU/model extraction ইত্যাদি শিখব।

---

# 38. Price History-এর জন্য Cleaning

আজ:

```text
৳50,000
```

কাল:

```text
৳48,999
```

Database:

```text
product_id | price | scraped_at
-----------|-------|------------
101        | 50000 | 2026-09-07
101        | 48999 | 2026-09-08
```

এখন আমরা পরে graph করতে পারব:

```text
Price
  │
50k│ ●
   │  \
49k│   ●
   │
   └────────── Time
```

---

# 39. M04 Final Project

এখন আমরা M01–M04 একসাথে ভাবব:

```text
                 Website
                    ↓
              requests.get()
                    ↓
                  HTML
                    ↓
              BeautifulSoup
                    ↓
             Extract Product
                    ↓
              Raw Dictionary
                    ↓
             Data Cleaning
                    ↓
            Data Normalization
                    ↓
              Data Validation
                    ↓
              Clean Dictionary
                    ↓
          CSV / PostgreSQL
```

---

# 40. Production-style Folder Structure

এখন থেকে project structure এমন করতে পারেন:

```text
ecommerce_data_collector/
│
├── scrapers/
│   ├── site_a.py
│   ├── site_b.py
│   └── site_c.py
│
├── parsers/
│   └── product_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── data/
│   ├── raw/
│   └── cleaned/
│
├── config/
│   └── settings.py
│
├── main.py
│
└── requirements.txt
```

এটা বড় project-এর জন্য অনেক better than সব code এক file-এ রাখা।

---

# 41. `product_cleaner.py`

আপনার cleaner file:

```python
import re


def clean_text(value):

    if value is None:
        return None

    return " ".join(
        str(value).split()
    )


def clean_price(value):

    if value is None:
        return None

    value = re.sub(
        r"[^\d.]",
        "",
        str(value)
    )

    if not value:
        return None

    return float(value)


def clean_rating(value):

    if value is None:
        return None

    match = re.search(
        r"\d+(?:\.\d+)?",
        str(value)
    )

    if not match:
        return None

    rating = float(
        match.group()
    )

    if 0 <= rating <= 5:
        return rating

    return None


def clean_review_count(value):

    if value is None:
        return None

    text = str(value).strip().upper()

    match = re.search(
        r"(\d+(?:\.\d+)?)\s*([KMB]?)",
        text
    )

    if not match:
        return None

    number = float(
        match.group(1)
    )

    suffix = match.group(2)

    multipliers = {
        "K": 1_000,
        "M": 1_000_000,
        "B": 1_000_000_000
    }

    number *= multipliers.get(
        suffix,
        1
    )

    return int(number)


def clean_discount(value):

    if value is None:
        return None

    match = re.search(
        r"\d+(?:\.\d+)?",
        str(value)
    )

    if not match:
        return None

    discount = float(
        match.group()
    )

    if 0 <= discount <= 100:
        return discount

    return None
```

---

# 42. M04 Practice Task

নিজে এই raw data নিন:

```python
products = [

    {
        "name":
            "  Samsung   Galaxy A56  ",

        "price":
            "৳ 49,999",

        "rating":
            "4.6/5",

        "reviews":
            "1.2K Reviews",

        "discount":
            "9% OFF"
    },

    {
        "name":
            " iPhone 17 ",

        "price":
            "BDT 129,999",

        "rating":
            "4.8",

        "reviews":
            "5K Reviews",

        "discount":
            "10% OFF"
    },

    {
        "name":
            "  Google Pixel 10 ",

        "price":
            "৳89,999",

        "rating":
            "4.5/5",

        "reviews":
            "850 Reviews",

        "discount":
            "5%"
    }
]
```

Target:

```python
[
    {
        "name": "Samsung Galaxy A56",
        "price": 49999.0,
        "rating": 4.6,
        "review_count": 1200,
        "discount": 9.0
    },

    {
        "name": "iPhone 17",
        "price": 129999.0,
        "rating": 4.8,
        "review_count": 5000,
        "discount": 10.0
    },

    {
        "name": "Google Pixel 10",
        "price": 89999.0,
        "rating": 4.5,
        "review_count": 850,
        "discount": 5.0
    }
]
```

---

# 43. M04-এর Core Skills

এই module থেকে এগুলো অবশ্যই mastery করবেন:

```text
✅ strip()
✅ split()
✅ replace()
✅ lower()
✅ upper()

✅ Regex
✅ re.search()
✅ re.sub()

✅ Price cleaning
✅ Rating cleaning
✅ Review count cleaning
✅ Discount cleaning

✅ Category normalization
✅ Brand normalization
✅ Availability normalization

✅ Missing data
✅ Validation
✅ Duplicate concept
✅ URL normalization
```

সবচেয়ে গুরুত্বপূর্ণ ধারণাটা হলো:

```text
Different Websites
       ↓
Different Raw Formats
       ↓
       CLEAN
       ↓
      NORMALIZE
       ↓
      VALIDATE
       ↓
 SAME STANDARD SCHEMA
       ↓
    PostgreSQL
       ↓
 Pandas / SQL Analysis
```

**M01 = Data আনা → M02 = Data বের করা → M03 = অনেক page/product collect করা → M04 = Data-কে analysis/database-ready করা।**

এরপর **M05 — Dynamic E-commerce Websites + JavaScript + Playwright**-এ গেলে `requests` দিয়ে HTML-এ product না পাওয়া গেলে কেন হয়, browser-rendered data কীভাবে কাজ করে, এবং কখন Playwright ব্যবহার করতে হবে—এসব শিখব।


----
# M05 — Dynamic E-commerce Website + JavaScript + Playwright

এখন আমরা এমন website নিয়ে কাজ করব যেখানে **`requests + BeautifulSoup` দিয়ে product পাওয়া যায় না**, কারণ product data JavaScript দিয়ে browser-এর ভিতরে load হয়।

M05-এর মূল লক্ষ্য:

> **Browser automation ব্যবহার করে JavaScript-rendered e-commerce website থেকে structured product data collect করা।**

---

# 1. Static বনাম Dynamic Website

আগের M01–M04-এ আমাদের pipeline ছিল:

```text
Website
   ↓
requests.get()
   ↓
HTML
   ↓
BeautifulSoup
   ↓
Product Data
```

Static website হলে এটা যথেষ্ট।

কিন্তু dynamic website-এ:

```text
Website
   ↓
Initial HTML
   ↓
JavaScript executes
   ↓
API/Data loads
   ↓
DOM changes
   ↓
Products appear
```

তাই:

```python
requests.get(url)
```

করলে হয়তো product HTML-ই পাওয়া যাবে না।

---

# 2. কেন requests কাজ করে না?

ধরো browser-এ তুমি দেখতে পাচ্ছ:

```text
Samsung Galaxy S25
৳89,999

iPhone 16
৳119,999

Google Pixel 9
৳79,999
```

কিন্তু `requests` দিয়ে HTML download করলে:

```html
<div id="app"></div>

<script src="app.js"></script>
```

এরকম পাওয়া যেতে পারে।

Product নেই।

কারণ:

```text
requests
   ↓
HTML download
   ↓
JavaScript execute করে না
   ↓
Product নেই
```

Browser:

```text
Browser
   ↓
HTML
   ↓
JavaScript
   ↓
API request
   ↓
Product data
   ↓
DOM
   ↓
Product visible
```

---

# 3. Playwright কী?

**Playwright** হলো browser automation framework।

Python দিয়ে browser control করতে পারবে।

যেমন:

```python
from playwright.sync_api import sync_playwright
```

তারপর:

```text
Python
   ↓
Playwright
   ↓
Chromium
   ↓
Website
```

Browser automatically:

* open করতে পারবে
* URL visit করতে পারবে
* click করতে পারবে
* scroll করতে পারবে
* JavaScript execute করতে পারবে
* rendered HTML পড়তে পারবে
* product data extract করতে পারবে
* screenshot নিতে পারবে

---

# 4. Installation

Virtual environment activate করো:

```bash
python -m venv venv
```

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

তারপর:

```bash
pip install playwright
```

Browser install:

```bash
playwright install chromium
```

Check:

```bash
playwright --version
```

---

# 5. প্রথম Playwright Program

`test.py`

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:

    browser = p.chromium.launch(headless=False)

    page = browser.new_page()

    page.goto("https://example.com")

    print(page.title())

    browser.close()
```

Run:

```bash
python test.py
```

Browser open হবে।

---

# 6. `headless=False` কী?

```python
browser = p.chromium.launch(headless=False)
```

এর অর্থ browser দেখতে পারবে।

Development-এর সময়:

```python
headless=False
```

ভালো।

Production/server-এ:

```python
headless=True
```

ব্যবহার করা যায়।

---

# 7. Page Object

```python
page = browser.new_page()
```

এখানে `page` হচ্ছে browser-এর একটি tab।

তুমি:

```python
page.goto()
```

দিয়ে URL visit করতে পারবে।

```python
page.title()
```

দিয়ে title নিতে পারবে।

```python
page.content()
```

দিয়ে rendered HTML নিতে পারবে।

---

# 8. `page.goto()`

```python
page.goto("https://example.com")
```

আরও ভালো:

```python
page.goto(
    "https://example.com",
    wait_until="domcontentloaded"
)
```

অথবা:

```python
page.goto(
    "https://example.com",
    timeout=30000
)
```

এখানে timeout:

```text
30000 milliseconds
=
30 seconds
```

---

# 9. Rendered HTML নেওয়া

এটা খুব গুরুত্বপূর্ণ।

```python
html = page.content()

print(html)
```

BeautifulSoup-এর মতো করে parse করতে পারো:

```python
from bs4 import BeautifulSoup

html = page.content()

soup = BeautifulSoup(html, "html.parser")

print(soup.title.text)
```

অর্থাৎ:

```text
Playwright
    ↓
JavaScript execute
    ↓
Rendered HTML
    ↓
BeautifulSoup
    ↓
Data extraction
```

এটা খুব powerful combination।

---

# 10. Playwright + BeautifulSoup

Complete example:

```python
from playwright.sync_api import sync_playwright
from bs4 import BeautifulSoup

URL = "https://example.com"

with sync_playwright() as p:

    browser = p.chromium.launch(headless=False)

    page = browser.new_page()

    page.goto(URL)

    html = page.content()

    soup = BeautifulSoup(html, "html.parser")

    print(soup.get_text(strip=True))

    browser.close()
```

---

# 11. Locator কী?

Playwright-এ element খুঁজতে সবচেয়ে important concept হলো **Locator**।

Example:

```python
page.locator(".product")
```

অথবা:

```python
page.locator("h2")
```

অথবা:

```python
page.locator("#products")
```

---

# 12. `locator()` বনাম BeautifulSoup

BeautifulSoup:

```python
soup.select(".product")
```

Playwright:

```python
page.locator(".product")
```

দুটো দেখতে similar।

কিন্তু Playwright-এর advantage:

```text
Browser DOM
+
JavaScript
+
Interaction
+
Waiting
```

সব করতে পারে।

---

# 13. Product Card Find করা

ধরো website-এর HTML:

```html
<div class="product-card">

    <h2 class="product-name">
        Samsung Galaxy S25
    </h2>

    <span class="price">
        ৳89,999
    </span>

</div>
```

Playwright:

```python
products = page.locator(".product-card")

print(products.count())
```

ধরো:

```text
20
```

product পাওয়া গেল।

---

# 14. প্রতিটি Product Loop করা

```python
products = page.locator(".product-card")

for i in range(products.count()):

    product = products.nth(i)

    name = product.locator(".product-name").text_content()

    price = product.locator(".price").text_content()

    print(name)
    print(price)
```

Output:

```text
Samsung Galaxy S25
৳89,999

iPhone 16
৳119,999

Google Pixel 9
৳79,999
```

---

# 15. `.text_content()`

```python
name = product.locator(".product-name").text_content()
```

এটা element-এর text দেয়।

যেমন:

```html
<h2 class="product-name">
    Samsung Galaxy S25
</h2>
```

Result:

```text
Samsung Galaxy S25
```

---

# 16. Text Clean করা

কখনো:

```text
"\n   Samsung Galaxy S25   "
```

পেতে পারো।

তখন:

```python
name = product.locator(".product-name").text_content()

if name:
    name = name.strip()
```

অথবা:

```python
name = product.locator(".product-name").inner_text().strip()
```

---

# 17. Attribute Extract করা

ধরো:

```html
<a
    class="product-link"
    href="/products/samsung-s25"
>
    Samsung Galaxy S25
</a>
```

Playwright:

```python
url = product.locator(".product-link").get_attribute("href")
```

Result:

```text
/products/samsung-s25
```

---

# 18. Absolute URL বানানো

আগের M03-এর মতো:

```python
from urllib.parse import urljoin

base_url = "https://example.com"

url = urljoin(
    base_url,
    "/products/samsung-s25"
)

print(url)
```

Result:

```text
https://example.com/products/samsung-s25
```

---

# 19. Image URL

HTML:

```html
<img
    class="product-image"
    src="/images/s25.jpg"
>
```

Code:

```python
image_url = product.locator(
    ".product-image"
).get_attribute("src")
```

তারপর:

```python
image_url = urljoin(base_url, image_url)
```

---

# 20. Safe Extraction

Problem:

সব product-এর rating নাও থাকতে পারে।

যদি সরাসরি:

```python
rating = product.locator(".rating").text_content()
```

করো, error বা empty result পেতে পারো।

Better:

```python
rating_element = product.locator(".rating")

if rating_element.count() > 0:
    rating = rating_element.first.text_content()
else:
    rating = None
```

---

# 21. অপেক্ষা করা — সবচেয়ে গুরুত্বপূর্ণ

Dynamic website-এ:

```python
page.goto(url)
```

করেই সঙ্গে সঙ্গে product পাওয়া যাবে—এমন guarantee নেই।

কারণ:

```text
Page loaded
     ↓
JavaScript starts
     ↓
API request
     ↓
Data arrives
     ↓
Product rendered
```

তাই অপেক্ষা করতে হবে।

---

# 22. `wait_for_selector()`

ধরো product card:

```css
.product-card
```

তাহলে:

```python
page.wait_for_selector(".product-card")
```

এটা খুব useful।

Complete:

```python
page.goto(URL)

page.wait_for_selector(".product-card")

products = page.locator(".product-card")

print(products.count())
```

---

# 23. Timeout

যদি product না আসে:

```python
page.wait_for_selector(
    ".product-card",
    timeout=10000
)
```

মানে:

```text
maximum 10 seconds
```

---

# 24. Timeout Handle করা

```python
from playwright.sync_api import TimeoutError

try:

    page.wait_for_selector(
        ".product-card",
        timeout=10000
    )

except TimeoutError:

    print("Product did not load")
```

Production scraper-এ এই ধরনের error handling খুব important।

---

# 25. `page.wait_for_load_state()`

Example:

```python
page.goto(URL)

page.wait_for_load_state("domcontentloaded")
```

কিন্তু শুধু page load হওয়া মানেই product load হয়েছে—এটা সবসময় ঠিক না।

তাই product-এর selector-এর জন্য অপেক্ষা করা সাধারণত বেশি নির্ভরযোগ্য:

```python
page.wait_for_selector(".product-card")
```

---

# 26. `networkidle` সম্পর্কে

তুমি দেখতে পারো:

```python
page.goto(
    URL,
    wait_until="networkidle"
)
```

কিন্তু dynamic e-commerce site-এ সবসময় এটা ideal নয়।

কারণ কিছু website continuously:

* analytics
* tracking
* ads
* websocket
* background requests

চালাতে পারে।

তাই practical approach:

```python
page.goto(URL)

page.wait_for_selector(".product-card")
```

---

# 27. Complete Dynamic Product Scraper

এখন M01–M05 combine করি।

```python
from playwright.sync_api import sync_playwright, TimeoutError
from urllib.parse import urljoin


URL = "https://example.com/products"


def scrape_products(page, url):

    page.goto(
        url,
        wait_until="domcontentloaded",
        timeout=30000
    )

    try:
        page.wait_for_selector(
            ".product-card",
            timeout=10000
        )

    except TimeoutError:

        print("Products not loaded")

        return []

    products = page.locator(".product-card")

    results = []

    for i in range(products.count()):

        product = products.nth(i)

        name_element = product.locator(".product-name")

        price_element = product.locator(".price")

        link_element = product.locator("a")

        image_element = product.locator("img")

        name = (
            name_element.inner_text().strip()
            if name_element.count()
            else None
        )

        price = (
            price_element.inner_text().strip()
            if price_element.count()
            else None
        )

        href = (
            link_element.get_attribute("href")
            if link_element.count()
            else None
        )

        image = (
            image_element.get_attribute("src")
            if image_element.count()
            else None
        )

        product_url = (
            urljoin(url, href)
            if href
            else None
        )

        image_url = (
            urljoin(url, image)
            if image
            else None
        )

        results.append({
            "name": name,
            "price": price,
            "product_url": product_url,
            "image_url": image_url,
        })

    return results


with sync_playwright() as p:

    browser = p.chromium.launch(
        headless=False
    )

    page = browser.new_page()

    data = scrape_products(page, URL)

    for product in data:

        print(product)

    browser.close()
```

---

# 28. Browser Context

Real project-এ সরাসরি:

```python
browser.new_page()
```

এর বদলে context ব্যবহার করা useful।

```python
context = browser.new_context()

page = context.new_page()
```

Structure:

```text
Browser
   │
   ├── Context 1
   │      ├── Page 1
   │      └── Page 2
   │
   └── Context 2
          └── Page 1
```

---

# 29. Viewport Set করা

```python
context = browser.new_context(
    viewport={
        "width": 1366,
        "height": 768
    }
)
```

তারপর:

```python
page = context.new_page()
```

---

# 30. Screenshot নেওয়া

Debugging-এর জন্য খুব useful।

```python
page.screenshot(
    path="debug.png",
    full_page=True
)
```

তখন website-এর screenshot save হবে।

---

# 31. HTML Save করা

Debugging-এর জন্য:

```python
html = page.content()

with open(
    "debug.html",
    "w",
    encoding="utf-8"
) as f:

    f.write(html)
```

এখন তুমি পরে HTML inspect করতে পারবে।

---

# 32. Browser DevTools দিয়ে Selector বের করা

ধরো website-এ product card আছে।

Chrome:

```text
Right Click
     ↓
Inspect
     ↓
Element
```

ধরো দেখলে:

```html
<div class="product-card">
```

তাহলে selector:

```css
.product-card
```

Product name:

```html
<h2 class="product-name">
```

Selector:

```css
.product-name
```

Price:

```html
<span class="price">
```

Selector:

```css
.price
```

---

# 33. CSS Selector Hierarchy

ধরো:

```html
<div class="product-card">

    <div class="info">

        <h2 class="name">
            iPhone 16
        </h2>

        <span class="price">
            ৳120000
        </span>

    </div>

</div>
```

তুমি করতে পারো:

```python
product.locator(".name")
```

অথবা:

```python
product.locator(".info .name")
```

অথবা:

```python
product.locator("h2.name")
```

---

# 34. `locator()` কেন গুরুত্বপূর্ণ?

ধরো 50টি product আছে:

```python
products = page.locator(".product-card")
```

এখন:

```python
products.nth(0)
```

প্রথম product।

```python
products.nth(1)
```

দ্বিতীয় product।

```python
products.nth(49)
```

50তম product।

---

# 35. Dynamic Pagination

আগের M03-এ URL pagination দেখেছিলাম:

```text
?page=1
?page=2
?page=3
```

Dynamic website-এ অনেক সময়:

```text
Load More
```

button থাকে।

Example:

```html
<button class="load-more">
    Load More
</button>
```

Playwright:

```python
page.locator(".load-more").click()
```

---

# 36. Load More Loop

```python
while True:

    button = page.locator(".load-more")

    if button.count() == 0:
        break

    try:

        button.click()

        page.wait_for_timeout(2000)

    except:
        break
```

তারপর:

```python
products = page.locator(".product-card")

print(products.count())
```

---

# 37. Better Load More Approach

Blind:

```python
page.wait_for_timeout(2000)
```

এর বদলে possible হলে DOM change-এর জন্য wait করা ভালো।

ধরো product count:

```python
old_count = page.locator(
    ".product-card"
).count()

button.click()
```

তারপর নতুন count আসার জন্য অপেক্ষা করা যায়।

Concept:

```text
Old products = 20

Click Load More

       ↓

New products loading

       ↓

Products = 40
```

এতে scraper বেশি reliable হয়।

---

# 38. Infinite Scroll

কিছু e-commerce website-এ:

```text
Page
 ↓
Products
 ↓
Scroll
 ↓
More products
 ↓
Scroll
 ↓
More products
```

তখন:

```python
page.mouse.wheel(0, 5000)
```

ব্যবহার করা যায়।

তারপর নতুন content আসার জন্য অপেক্ষা:

```python
page.wait_for_timeout(2000)
```

---

# 39. Infinite Scroll Loop

Concept:

```python
previous_count = 0

while True:

    products = page.locator(".product-card")

    current_count = products.count()

    if current_count == previous_count:
        break

    previous_count = current_count

    page.mouse.wheel(0, 5000)

    page.wait_for_timeout(2000)
```

বাস্তব website অনুযায়ী stopping condition আরও ভালোভাবে design করতে হবে।

---

# 40. Product Detail Page

M03-এ আমরা শিখেছি:

```text
Category
   ↓
Product URLs
   ↓
Product Detail
```

এখন Playwright দিয়ে detail page scrape করতে পারি।

Example:

```python
def scrape_product_detail(page, url):

    page.goto(
        url,
        wait_until="domcontentloaded"
    )

    page.wait_for_selector(
        ".product-title"
    )

    name = page.locator(
        ".product-title"
    ).inner_text()

    price = page.locator(
        ".product-price"
    ).inner_text()

    rating = page.locator(
        ".rating"
    ).inner_text()

    return {
        "name": name.strip(),
        "price": price.strip(),
        "rating": rating.strip()
    }
```

---

# 41. M05 Complete Architecture

এখন আমাদের scraper আরও powerful:

```text
                  E-commerce Website
                          │
              ┌───────────┴───────────┐
              │                       │
          Static HTML             Dynamic JS
              │                       │
          Requests                Playwright
              │                       │
       BeautifulSoup            Browser DOM
              │                       │
              └───────────┬───────────┘
                          ↓
                    Raw Product Data
                          ↓
                       Cleaner
                          ↓
                      Validator
                          ↓
                  Standard Schema
                          ↓
                     PostgreSQL
                          ↓
                    Pandas / SQL
                          ↓
                    Visualization
```

এটাই আমাদের পুরো project-এর foundation।

---

# 42. Requests নাকি Playwright?

এটা খুব গুরুত্বপূর্ণ decision।

| Situation            | Tool                  |
| -------------------- | --------------------- |
| Static HTML          | `requests`            |
| HTML parsing         | `BeautifulSoup`       |
| JavaScript rendered  | `Playwright`          |
| Click করতে হবে       | `Playwright`          |
| Infinite scroll      | `Playwright`          |
| Load More            | `Playwright`          |
| Public API available | API preferred         |
| অনেক দ্রুত scraping  | `requests` preferable |
| Browser interaction  | `Playwright`          |

সব website-এ Playwright ব্যবহার করা উচিত না।

যদি:

```text
Public API
```

থাকে → **API first**

যদি:

```text
Static HTML
```

হয় → **requests + BeautifulSoup**

যদি:

```text
JavaScript rendering
```

প্রয়োজন হয় → **Playwright**

---

# 43. API থাকলে Playwright-এর চেয়েও ভালো

ধরো website browser-এ product দেখাচ্ছে।

Browser:

```text
JavaScript
   ↓
GET /api/products
   ↓
JSON
```

তাহলে browser automate করার দরকার নেই।

সরাসরি API:

```python
import requests

response = requests.get(
    "https://example.com/api/products"
)

data = response.json()
```

এটা সাধারণত:

```text
faster
+
lighter
+
easier
+
more stable
```

তাই পরের গুরুত্বপূর্ণ skill হবে **Network/API inspection**।

---

# 44. Security / Anti-bot সম্পর্কে

Professional data collection করার সময়:

* website-এর Terms of Service দেখবে
* `robots.txt`-কে একটি signal হিসেবে দেখবে
* reasonable rate limit রাখবে
* unnecessary request করবে না
* public data-তেই কাজ করবে
* login-protected/private data সংগ্রহ করবে না
* CAPTCHA বা anti-bot system bypass করার চেষ্টা করবে না
* security control evade করার technique ব্যবহার করবে না

আমাদের লক্ষ্য:

> **Legitimate public e-commerce data collection pipeline তৈরি করা।**

---

# 45. M05 Mini Project

এখন তোমার নিজের একটা project বানাও:

```text
m05_dynamic_scraper/
│
├── scraper.py
├── requirements.txt
│
├── data/
│   ├── raw/
│   └── screenshots/
│
└── debug/
    └── page.html
```

`requirements.txt`:

```text
playwright
beautifulsoup4
requests
```

---

# 46. Mini Project Requirements

তোমার scraper:

### Step 1

Website open করবে:

```python
page.goto(URL)
```

### Step 2

Product loading-এর জন্য wait করবে:

```python
page.wait_for_selector(
    ".product-card"
)
```

### Step 3

সব product count করবে:

```python
products.count()
```

### Step 4

প্রতিটি product থেকে collect করবে:

```text
name
price
rating
review_count
product_url
image_url
```

### Step 5

Relative URL convert করবে:

```python
urljoin()
```

### Step 6

Rendered HTML save করবে:

```python
page.content()
```

### Step 7

Screenshot save করবে:

```python
page.screenshot()
```

### Step 8

শেষে list/dictionary বানাবে:

```python
[
    {
        "name": "...",
        "price": "...",
        "rating": "...",
        "review_count": "...",
        "product_url": "...",
        "image_url": "..."
    }
]
```

---

# 47. M05-এর সবচেয়ে গুরুত্বপূর্ণ শেখার বিষয়

এই module শেষে তোমার মাথায় এই flow পরিষ্কার থাকতে হবে:

```text
                    Website
                       ↓
              Is HTML sufficient?
                 /           \
               YES            NO
                ↓              ↓
            Requests       Playwright
                ↓              ↓
        BeautifulSoup      Browser
                ↓              ↓
              Parse       JS Rendering
                ↓              ↓
                └──────┬───────┘
                       ↓
                 Product Data
                       ↓
                    Cleaning
                       ↓
                  Normalization
                       ↓
                    Validation
                       ↓
                  Database
```

### M05 Mastery Checklist

* [ ] Playwright install
* [ ] Chromium install
* [ ] Browser launch
* [ ] `page.goto()`
* [ ] `page.content()`
* [ ] `locator()`
* [ ] `count()`
* [ ] `nth()`
* [ ] `inner_text()`
* [ ] `text_content()`
* [ ] `get_attribute()`
* [ ] `wait_for_selector()`
* [ ] Timeout handling
* [ ] Screenshot
* [ ] Save rendered HTML
* [ ] Load More
* [ ] Infinite scroll concept
* [ ] Dynamic pagination
* [ ] Product detail scraping
* [ ] Requests vs Playwright decision
* [ ] API-first mindset

---

## 🔥 M01 → M05 পর্যন্ত তোমার অবস্থান

এখন পর্যন্ত তুমি শিখেছ:

```text
M01
Requests
   ↓
Website থেকে HTML আনা

M02
BeautifulSoup
   ↓
HTML থেকে product বের করা

M03
Pagination
   ↓
অনেক page/product collect করা

M04
Cleaning + Normalization
   ↓
Different website-এর data একই format করা

M05
Playwright
   ↓
JavaScript-rendered website থেকে data collect করা
```

অর্থাৎ এখন তুমি **basic scraper থেকে real-world e-commerce collector-এর দিকে** চলে এসেছ।

**পরের logical module হবে M06 — Network/API Data Extraction Deep Dive**, যেখানে browser-এর Network tab দেখে website আসলে কোন API/JSON endpoint থেকে product data নিচ্ছে সেটা বুঝব। এটা শিখলে অনেক ক্ষেত্রে Playwright বাদ দিয়ে সরাসরি API থেকে হাজার হাজার product data collect করতে পারবে।

-----
# M06 — Network/API Data Extraction Deep Dive

M05-এ আমরা শিখেছি **Playwright দিয়ে browser control করে dynamic website থেকে data নেওয়া**।

এখন আরও important একটা skill শিখব:

> **Website-এর browser আসলে কোন API থেকে product data নিচ্ছে সেটা খুঁজে বের করে সরাসরি JSON/API থেকে data collect করা।**

এটা real-world e-commerce data collection-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 1. কেন API খুঁজব?

ধরো একটি e-commerce website-এ 10,000 products আছে।

Playwright দিয়ে:

```text
Browser
   ↓
Load page
   ↓
JavaScript
   ↓
API
   ↓
Render HTML
   ↓
Extract product
```

অনেক কাজ।

কিন্তু আমরা যদি API খুঁজে পাই:

```text
API
 ↓
JSON
 ↓
Python
 ↓
Data
```

তাহলে অনেক সহজ।

---

# 2. Example

Browser-এ তুমি দেখতে পাচ্ছ:

```text
Samsung Galaxy S25
৳89,999

iPhone 16
৳119,999

Pixel 9
৳79,999
```

কিন্তু background-এ website হয়তো request করছে:

```text
GET /api/products?page=1
```

Response:

```json
{
    "products": [
        {
            "name": "Samsung Galaxy S25",
            "price": 89999
        },
        {
            "name": "iPhone 16",
            "price": 119999
        }
    ]
}
```

আমাদের কাজ:

```text
Browser
   ↓
Network request identify
   ↓
API endpoint
   ↓
requests
   ↓
JSON
   ↓
Product data
```

---

# 3. API কী?

API = **Application Programming Interface**

সহজভাবে:

```text
Client
   ↓
Request
   ↓
API
   ↓
Server
   ↓
Response
```

Example:

```text
GET /api/products
```

Response:

```json
[
    {
        "id": 1,
        "name": "Laptop",
        "price": 80000
    }
]
```

---

# 4. JSON কী?

API response সাধারণত JSON format-এ আসে।

Example:

```json
{
    "name": "iPhone 16",
    "price": 120000,
    "rating": 4.8
}
```

Python-এ:

```python
import requests

response = requests.get(url)

data = response.json()

print(data)
```

---

# 5. Browser-এর Network Tab

এখন সবচেয়ে important practical skill।

Chrome খুলবে।

তারপর:

```text
Right Click
    ↓
Inspect
    ↓
Network
```

তারপর website reload:

```text
Ctrl + R
```

Network tab-এ অনেক request দেখতে পাবে।

যেমন:

```text
document
stylesheet
javascript
image
font
fetch
xhr
```

আমাদের সবচেয়ে বেশি interest:

```text
Fetch
XHR
```

---

# 6. Fetch/XHR কেন গুরুত্বপূর্ণ?

Modern website-এর JavaScript যখন server থেকে data আনে, তখন সাধারণত:

```text
Fetch
```

অথবা:

```text
XHR
```

request দেখা যায়।

Example:

```text
GET
/api/products?page=1
```

এটাই আমাদের target হতে পারে।

---

# 7. Network Request Inspect

ধরো Network tab-এ:

```text
products?page=1
```

দেখলে সেটাতে click করো।

তারপর দেখতে পারো:

```text
Headers
Payload
Preview
Response
Timing
```

সবচেয়ে important:

### Headers

### Payload

### Response

---

# 8. Response দেখো

Response tab-এ যদি এমন কিছু পাও:

```json
{
    "products": [
        {
            "id": 101,
            "title": "Samsung Galaxy S25",
            "price": 89999
        }
    ]
}
```

তাহলে jackpot! 😄

কারণ browser HTML generate করার আগে server থেকেই structured data এসেছে।

---

# 9. Request URL

Headers-এর মধ্যে দেখতে পারো:

```text
Request URL:
https://example.com/api/products?page=1
```

এটা copy করতে পারো।

Python:

```python
import requests

url = "https://example.com/api/products?page=1"

response = requests.get(url)

print(response.status_code)

data = response.json()

print(data)
```

---

# 10. প্রথম API Scraper

Basic:

```python
import requests


url = "https://example.com/api/products"

response = requests.get(
    url,
    timeout=20
)

response.raise_for_status()

data = response.json()

print(data)
```

---

# 11. JSON থেকে Products বের করা

ধরো response:

```json
{
    "products": [
        {
            "name": "Laptop",
            "price": 85000
        },
        {
            "name": "Phone",
            "price": 50000
        }
    ]
}
```

Python:

```python
products = data["products"]

for product in products:

    print(product["name"])
    print(product["price"])
```

Output:

```text
Laptop
85000

Phone
50000
```

---

# 12. Nested JSON

বাস্তবে response অনেক সময় nested হয়।

Example:

```json
{
    "data": {
        "products": [
            {
                "id": 1,
                "name": "Laptop",
                "price": 85000
            }
        ]
    }
}
```

তখন:

```python
products = data["data"]["products"]
```

---

# 13. Safe JSON Extraction

Production code-এ সরাসরি:

```python
products = data["data"]["products"]
```

সবসময় করা উচিত না।

কারণ key missing হতে পারে।

Better:

```python
products = (
    data
    .get("data", {})
    .get("products", [])
)
```

এখন missing হলে:

```python
[]
```

পাবে।

---

# 14. API Query Parameters

ধরো API:

```text
/api/products?page=1&limit=20
```

Python-এ manually URL বানানোর দরকার নেই।

```python
import requests

url = "https://example.com/api/products"

params = {
    "page": 1,
    "limit": 20
}

response = requests.get(
    url,
    params=params
)

print(response.url)
```

Output:

```text
https://example.com/api/products?page=1&limit=20
```

---

# 15. Pagination API

এখন আসল কাজ।

ধরো:

```text
page=1
page=2
page=3
...
```

তাহলে:

```python
import requests


url = "https://example.com/api/products"

all_products = []

for page in range(1, 6):

    params = {
        "page": page,
        "limit": 20
    }

    response = requests.get(
        url,
        params=params,
        timeout=20
    )

    response.raise_for_status()

    data = response.json()

    products = (
        data
        .get("data", {})
        .get("products", [])
    )

    if not products:
        break

    all_products.extend(products)

print("Total:", len(all_products))
```

---

# 16. API Pagination বুঝবে কীভাবে?

Network response দেখো।

অনেক API response-এ থাকতে পারে:

```json
{
    "data": {
        "products": []
    },
    "pagination": {
        "page": 1,
        "limit": 20,
        "total": 1000
    }
}
```

তাহলে আমরা জানি:

```text
total = 1000
limit = 20
```

অর্থাৎ প্রায়:

```text
1000 / 20
= 50 pages
```

---

# 17. Pagination Metadata

Example:

```python
pagination = data.get(
    "pagination",
    {}
)

current_page = pagination.get(
    "page"
)

total = pagination.get(
    "total"
)

limit = pagination.get(
    "limit"
)

print(current_page)
print(total)
print(limit)
```

---

# 18. API Filtering

E-commerce API-তে filter থাকতে পারে:

```text
category
brand
min_price
max_price
rating
search
sort
```

Example:

```python
params = {
    "category": "laptop",
    "brand": "samsung",
    "min_price": 50000,
    "max_price": 150000
}

response = requests.get(
    url,
    params=params
)
```

এতে server filtered data দিতে পারে।

---

# 19. Search API

ধরো website-এ search করলে:

```text
iphone
```

Network-এ দেখতে পারো:

```text
/api/products/search?q=iphone
```

Python:

```python
params = {
    "q": "iphone"
}

response = requests.get(
    url,
    params=params
)

data = response.json()
```

---

# 20. Sort

API-তে থাকতে পারে:

```text
sort=price_asc
```

Python:

```python
params = {
    "sort": "price_asc"
}
```

অথবা:

```python
params = {
    "sort": "rating_desc"
}
```

এগুলো website-এর actual API contract অনুযায়ী হবে।

---

# 21. POST API

সব API GET হয় না।

কখনো:

```text
POST /api/products/search
```

হতে পারে।

Payload:

```json
{
    "query": "iphone",
    "page": 1
}
```

Python:

```python
payload = {
    "query": "iphone",
    "page": 1
}

response = requests.post(
    url,
    json=payload,
    timeout=20
)

response.raise_for_status()

data = response.json()
```

---

# 22. Headers

Network request-এর Headers-এ দেখতে পারো:

```text
Accept
Content-Type
Referer
User-Agent
```

Public endpoint হলে সাধারণ request যথেষ্ট হতে পারে।

Example:

```python
headers = {
    "Accept": "application/json",
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(
    url,
    headers=headers
)
```

তবে গুরুত্বপূর্ণ:

> Header ব্যবহার করা legitimate compatibility-এর জন্য; authentication, CAPTCHA বা anti-bot/security control bypass করার জন্য নয়।

---

# 23. `Accept`

API যদি JSON response দেয়:

```python
headers = {
    "Accept": "application/json"
}
```

এটা server-কে জানায়:

> আমি JSON response expect করছি।

---

# 24. Content-Type

POST request হলে:

```python
headers = {
    "Content-Type": "application/json"
}
```

তবে `requests.post(..., json=payload)` ব্যবহার করলে `requests` সাধারণত JSON content type সেট করে দেয়।

---

# 25. Cookies

কিছু public website session cookie ব্যবহার করতে পারে।

Playwright-এ browser context-এর session থাকতে পারে।

কিন্তু protected/private data access করার জন্য cookie/session ব্যবহার করা উচিত নয়।

Public API-এর ক্ষেত্রে প্রয়োজনীয় normal session handling হলে:

```python
session = requests.Session()
```

ব্যবহার করতে পারো।

---

# 26. `requests.Session()`

Repeated API calls-এর জন্য:

```python
import requests

session = requests.Session()

response = session.get(url)

print(response.status_code)
```

তারপর:

```python
response = session.get(
    url,
    params={"page": 2}
)
```

Session connection reuse করতে পারে এবং shared settings রাখতে সাহায্য করে।

---

# 27. API Scraper Class

এখন একটু professional code লিখি।

```python
import requests


class EcommerceAPI:

    def __init__(self, base_url):

        self.base_url = base_url

        self.session = requests.Session()

        self.session.headers.update({
            "Accept": "application/json",
            "User-Agent": "Mozilla/5.0"
        })

    def get_products(
        self,
        page=1,
        limit=20
    ):

        params = {
            "page": page,
            "limit": limit
        }

        response = self.session.get(
            self.base_url,
            params=params,
            timeout=20
        )

        response.raise_for_status()

        return response.json()
```

---

# 28. Class ব্যবহার

```python
api = EcommerceAPI(
    "https://example.com/api/products"
)

data = api.get_products(
    page=1,
    limit=20
)

print(data)
```

---

# 29. API → Standard Schema

আমাদের project-এর সবচেয়ে important concept।

Different API:

### Site A

```json
{
    "title": "iPhone 16",
    "sale_price": 120000
}
```

### Site B

```json
{
    "product_name": "iPhone 16",
    "currentPrice": 119000
}
```

### Site C

```json
{
    "name": "iPhone 16",
    "price": 118500
}
```

আমাদের database-এ চাই:

```text
name
price
brand
category
rating
review_count
product_url
image_url
source
```

তাই API-specific parser দরকার।

---

# 30. Site A Parser

```python
def parse_site_a(item):

    return {
        "name": item.get("title"),
        "price": item.get("sale_price"),
        "brand": item.get("brand"),
        "category": item.get("category"),
    }
```

---

# 31. Site B Parser

```python
def parse_site_b(item):

    return {
        "name": item.get("product_name"),
        "price": item.get("currentPrice"),
        "brand": item.get("brandName"),
        "category": item.get("categoryName"),
    }
```

শেষে দুই site-এর output:

```python
{
    "name": "...",
    "price": 120000,
    "brand": "Apple",
    "category": "Smartphone"
}
```

একই schema।

---

# 32. API + M04 Cleaner

আমরা আগে M04-এ শিখেছি cleaning।

এখন pipeline:

```text
API
 ↓
JSON
 ↓
API Parser
 ↓
Raw Standard Schema
 ↓
Cleaner
 ↓
Normalizer
 ↓
Validator
 ↓
Database
```

এটা real project architecture-এর দিকে যাচ্ছে।

---

# 33. Duplicate Data

API pagination-এ কখনো একই product দুইবার আসতে পারে।

তাই:

```python
seen = set()

unique_products = []

for product in products:

    product_id = product.get("id")

    if product_id in seen:
        continue

    seen.add(product_id)

    unique_products.append(product)
```

---

# 34. যদি Product ID না থাকে?

তাহলে URL ব্যবহার করতে পারো:

```python
key = product.get("product_url")
```

অথবা combination:

```python
key = (
    product.get("name"),
    product.get("brand")
)
```

তবে name-based deduplication perfect নয়।

Production project-এ stable product identifier সবচেয়ে ভালো।

---

# 35. API Error Handling

```python
import requests


try:

    response = requests.get(
        url,
        timeout=20
    )

    response.raise_for_status()

    data = response.json()

except requests.Timeout:

    print("Request timed out")

except requests.HTTPError as e:

    print("HTTP error:", e)

except requests.RequestException as e:

    print("Request failed:", e)

except ValueError:

    print("Invalid JSON")
```

---

# 36. Status Code

API debugging-এ:

```python
print(response.status_code)
```

Common:

```text
200 → Success
400 → Bad Request
401 → Authentication required
403 → Forbidden
404 → Not Found
429 → Too Many Requests
500 → Server Error
```

বিশেষ করে:

```text
429
```

দেখলে request rate কমাতে হবে।

Anti-bot bypass করার চেষ্টা করা উচিত নয়।

---

# 37. Network Tab থেকে "Copy as cURL"

Chrome DevTools-এর Network request-এর উপর right-click করলে অনেক ক্ষেত্রে:

```text
Copy
   ↓
Copy as cURL
```

পাওয়া যায়।

এটা debugging/understanding-এর জন্য useful।

তখন request-এর:

* URL
* method
* headers
* query parameters
* body

বোঝা যায়।

তারপর Python-এ প্রয়োজনীয় legitimate অংশগুলো reproduce করতে পারো।

---

# 38. API Discovery Workflow

এখন পুরো process:

```text
Open Website
     ↓
Inspect
     ↓
Network
     ↓
Reload
     ↓
Fetch / XHR
     ↓
Find product request
     ↓
Open request
     ↓
Inspect URL
     ↓
Inspect Method
     ↓
Inspect Params
     ↓
Inspect Response
     ↓
Understand JSON structure
     ↓
Test with Python requests
     ↓
Build parser
```

---

# 39. API আছে কিনা বুঝবে কীভাবে?

Network tab-এ search করতে পারো:

```text
product
products
search
catalog
items
category
listing
```

আর response-এ খুঁজবে:

```text
name
title
price
product
items
results
data
```

---

# 40. API বনাম Playwright

| Feature                | API                  | Playwright     |
| ---------------------- | -------------------- | -------------- |
| Speed                  | ⭐⭐⭐⭐⭐                | ⭐⭐⭐            |
| Resource usage         | Low                  | High           |
| JSON data              | Excellent            | Indirect       |
| JavaScript interaction | No                   | Yes            |
| Click                  | No                   | Yes            |
| Infinite scroll        | Usually unnecessary  | Yes            |
| Dynamic DOM            | No                   | Yes            |
| Pagination             | Easy if API supports | More complex   |
| Stability              | Usually high         | Can be fragile |
| Best for bulk data     | ✅                    | Sometimes      |

---

# 41. আমাদের E-commerce Project-এ এখন Architecture

```text
                    E-commerce Sites
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       Public API      Static HTML       Dynamic JS
          │                │                │
      requests         requests          Playwright
          │                │                │
          ↓                ↓                ↓
       JSON          BeautifulSoup     Browser DOM
          │                │                │
          └────────────────┼────────────────┘
                           ↓
                     Site Parsers
                           ↓
                    Common Schema
                           ↓
                    Data Cleaning
                           ↓
                    Normalization
                           ↓
                      Validation
                           ↓
                     Deduplication
                           ↓
                      PostgreSQL
                           ↓
                    Pandas / SQL
```

---

# 42. M06 Project Structure

এখন project structure একটু upgrade করি:

```text
ecommerce-data-collector/
│
├── scrapers/
│   ├── base_scraper.py
│   ├── site_a_api.py
│   ├── site_b_api.py
│   └── site_c_playwright.py
│
├── parsers/
│   ├── site_a_parser.py
│   ├── site_b_parser.py
│   └── site_c_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── data/
│   ├── raw/
│   └── cleaned/
│
├── config/
│   └── settings.py
│
├── main.py
│
└── requirements.txt
```

---

# 43. M06 Mini Project

এখন তুমি একটা **API Product Collector** বানাবে।

Goal:

```text
API
 ↓
Collect 100+ products
 ↓
Parse JSON
 ↓
Standardize
 ↓
Save JSON
 ↓
Save CSV
```

Basic collector:

```python
import requests
import json


URL = "https://example.com/api/products"

all_products = []

for page in range(1, 6):

    params = {
        "page": page,
        "limit": 20
    }

    response = requests.get(
        URL,
        params=params,
        timeout=20
    )

    response.raise_for_status()

    data = response.json()

    products = (
        data
        .get("data", {})
        .get("products", [])
    )

    if not products:
        break

    all_products.extend(products)


with open(
    "data/raw/products.json",
    "w",
    encoding="utf-8"
) as f:

    json.dump(
        all_products,
        f,
        ensure_ascii=False,
        indent=4
    )


print(
    "Collected:",
    len(all_products)
)
```

**নোট:** এখানে `example.com` শুধু structure বোঝানোর জন্য। বাস্তবে public/authorized API endpoint ব্যবহার করবে।

---

# 44. এরপর CSV

M06-এর শেষে JSON থেকে CSV করতে পারো:

```python
import pandas as pd

df = pd.DataFrame(all_products)

df.to_csv(
    "data/raw/products.csv",
    index=False,
    encoding="utf-8-sig"
)

print(df.head())
```

এখন:

```text
API
 ↓
JSON
 ↓
Python
 ↓
Pandas
 ↓
CSV
```

---

# 45. M06 Practice Tasks

### Task 1

একটি public API খুঁজে:

```text
GET request
```

করো।

### Task 2

Response inspect করো।

### Task 3

এই fields খুঁজে বের করো:

```text
id
name/title
price
category
image
```

### Task 4

Pagination implement করো।

### Task 5

100+ records collect করো।

### Task 6

Duplicate remove করো।

### Task 7

CSV তৈরি করো।

### Task 8

M04 cleaner apply করো।

---

# 46. M06 Mastery Checklist

তোমার এগুলো জানা উচিত:

* [ ] API কী
* [ ] REST API concept
* [ ] GET
* [ ] POST
* [ ] JSON
* [ ] Request URL
* [ ] Query parameters
* [ ] Headers
* [ ] Payload
* [ ] Response
* [ ] Chrome Network tab
* [ ] Fetch/XHR
* [ ] API endpoint identify
* [ ] `response.json()`
* [ ] Nested JSON
* [ ] Pagination
* [ ] Filtering
* [ ] Search API
* [ ] Sorting
* [ ] `requests.Session()`
* [ ] Error handling
* [ ] HTTP status codes
* [ ] Deduplication
* [ ] API parser
* [ ] Standard schema
* [ ] API → Pandas → CSV

---

# 🔥 M01 → M06 এখন কী দাঁড়াল?

```text
M01
Requests
   ↓
Web থেকে data আনা

M02
BeautifulSoup
   ↓
HTML parse করা

M03
Pagination
   ↓
Multiple pages/products

M04
Cleaning & Normalization
   ↓
Data standardize করা

M05
Playwright
   ↓
Dynamic JavaScript website

M06
Network + API
   ↓
Browser-এর actual data source বের করা
   ↓
Direct JSON collection
```

এখন তোমার জন্য একটা **খুব গুরুত্বপূর্ণ transition** হয়েছে:

```text
আগে:
Website → Browser → HTML → Scrape

এখন:
Website → API → JSON → Direct Data Collection
```

আর এটাই bulk e-commerce data collection-এর জন্য অনেক বেশি practical approach।

**পরের M07-এ আমরা `Multi-Ecommerce Scraper Architecture` বানাব — একসাথে 3–5টা আলাদা e-commerce website, প্রত্যেকটার আলাদা HTML/API structure থাকলেও কীভাবে একই Python project-এর মধ্যে plug-in style scraper হিসেবে manage করা যায়।**

---
# M07 — Multi-Ecommerce Scraper Architecture

M01–M06 পর্যন্ত আমরা আলাদা আলাদা skill শিখেছি। এখন এগুলোকে **একটা professional project architecture-এর মধ্যে combine** করব।

M07-এর মূল লক্ষ্য:

> **একই Python project দিয়ে একাধিক e-commerce website-এর data collect করা, যদিও প্রতিটি website-এর HTML/API structure আলাদা।**

---

# 1. Problemটা কী?

ধরো তোমার 3টা website আছে:

```text
Website A → API
Website B → Static HTML
Website C → JavaScript
```

তিনটার data structure আলাদা।

### Website A

```json
{
    "title": "Samsung S25",
    "sale_price": 89999
}
```

### Website B

```html
<div class="product">
    <h2>Samsung S25</h2>
    <span class="price">৳89,999</span>
</div>
```

### Website C

JavaScript দিয়ে product load করে।

তাহলে যদি সব code `main.py`-এর মধ্যে লিখো:

```python
if site == "A":
    ...

elif site == "B":
    ...

elif site == "C":
    ...
```

কিছুদিন পর code বিশাল হয়ে যাবে।

তাই দরকার:

```text
Common Interface
       ↓
Site-specific Scrapers
```

---

# 2. Professional Architecture

আমাদের project:

```text
ecommerce-data-collector/
│
├── scrapers/
│   ├── base.py
│   ├── site_a.py
│   ├── site_b.py
│   └── site_c.py
│
├── parsers/
│   ├── site_a_parser.py
│   ├── site_b_parser.py
│   └── site_c_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── models/
│   └── product.py
│
├── pipelines/
│   ├── normalize.py
│   └── exporter.py
│
├── data/
│   ├── raw/
│   └── cleaned/
│
├── config/
│   └── settings.py
│
├── main.py
│
└── requirements.txt
```

এখানে প্রতিটি component-এর আলাদা responsibility থাকবে।

---

# 3. Single Responsibility

সবচেয়ে important concept:

> **একটা file/function/class-এর একটাই primary responsibility থাকবে।**

যেমন:

```text
Scraper
   ↓
Data collect করবে

Parser
   ↓
Raw response বুঝবে

Cleaner
   ↓
Data clean করবে

Validator
   ↓
Data valid কিনা দেখবে

Exporter
   ↓
CSV/JSON save করবে
```

এটাকে বলা যায় separation of concerns।

---

# 4. আমাদের Standard Product Schema

সব website থেকে শেষ পর্যন্ত একই structure চাই:

```python
{
    "source": "",
    "product_id": "",
    "name": "",
    "brand": "",
    "category": "",
    "price": None,
    "original_price": None,
    "discount": None,
    "rating": None,
    "review_count": None,
    "availability": "",
    "product_url": "",
    "image_url": "",
    "description": "",
    "scraped_at": ""
}
```

এটাই আমাদের **common schema**।

---

# 5. কেন Common Schema?

Website A:

```text
title
sale_price
ratingScore
```

Website B:

```text
product_name
current_price
stars
```

Website C:

```text
name
price
rating
```

কিন্তু আমাদের database-এ:

```text
name
price
rating
```

থাকবে।

তাই:

```text
Site A ──┐
Site B ──┼──> Common Product Schema
Site C ──┘
```

---

# 6. Base Scraper

`scrapers/base.py`

```python
from abc import ABC, abstractmethod


class BaseScraper(ABC):

    @abstractmethod
    def scrape(self):
        pass
```

এটা আমাদের common contract।

প্রতিটি scraper-এর `scrape()` method থাকবে।

---

# 7. Site A API Scraper

`scrapers/site_a.py`

```python
import requests

from .base import BaseScraper


class SiteAScraper(BaseScraper):

    def __init__(self, api_url):

        self.api_url = api_url

        self.session = requests.Session()

    def scrape(self):

        response = self.session.get(
            self.api_url,
            timeout=20
        )

        response.raise_for_status()

        return response.json()
```

---

# 8. Site B HTML Scraper

ধরো Site B static HTML।

```python
import requests

from bs4 import BeautifulSoup

from .base import BaseScraper


class SiteBScraper(BaseScraper):

    def __init__(self, url):

        self.url = url

    def scrape(self):

        response = requests.get(
            self.url,
            timeout=20
        )

        response.raise_for_status()

        soup = BeautifulSoup(
            response.text,
            "html.parser"
        )

        products = []

        for item in soup.select(
            ".product-card"
        ):

            products.append(item)

        return products
```

---

# 9. Site C Playwright Scraper

Dynamic website হলে:

```python
from playwright.sync_api import sync_playwright

from .base import BaseScraper


class SiteCScraper(BaseScraper):

    def __init__(self, url):

        self.url = url

    def scrape(self):

        with sync_playwright() as p:

            browser = p.chromium.launch(
                headless=True
            )

            page = browser.new_page()

            page.goto(
                self.url,
                wait_until="domcontentloaded"
            )

            page.wait_for_selector(
                ".product-card"
            )

            products = []

            cards = page.locator(
                ".product-card"
            )

            for i in range(cards.count()):

                card = cards.nth(i)

                products.append({
                    "name": card.locator(
                        ".name"
                    ).inner_text(),

                    "price": card.locator(
                        ".price"
                    ).inner_text()
                })

            browser.close()

            return products
```

---

# 10. তিনটা Scraper-এর Common Interface

এখন:

```python
site_a = SiteAScraper(api_url)
site_b = SiteBScraper(url)
site_c = SiteCScraper(url)
```

তিনটাকেই:

```python
.scrape()
```

দিয়ে চালানো যাবে।

এটাই abstraction-এর power।

---

# 11. Main.py

```python
from scrapers.site_a import SiteAScraper
from scrapers.site_b import SiteBScraper
from scrapers.site_c import SiteCScraper


scrapers = [

    SiteAScraper(
        "https://example.com/api/products"
    ),

    SiteBScraper(
        "https://example.com/products"
    ),

    SiteCScraper(
        "https://example.com/catalog"
    )
]


for scraper in scrapers:

    data = scraper.scrape()

    print(data)
```

এখন main code জানে না:

```text
API?
HTML?
Playwright?
```

সে শুধু জানে:

```python
scraper.scrape()
```

---

# 12. এটিই Polymorphism

Python-এ:

```python
for scraper in scrapers:

    scraper.scrape()
```

প্রতিটি object নিজের implementation অনুযায়ী কাজ করছে।

```text
SiteAScraper
     ↓
API

SiteBScraper
     ↓
HTML

SiteCScraper
     ↓
Playwright
```

কিন্তু interface:

```python
scrape()
```

একই।

---

# 13. Parser আলাদা কেন?

এখন একটা বড় design improvement।

Scraper-এর কাজ:

> Data collect করা।

Parser-এর কাজ:

> Collected data থেকে relevant fields বের করা।

যেমন Site A API response:

```json
{
    "title": "iPhone 16",
    "sale_price": 120000,
    "ratingScore": 4.8
}
```

Parser:

```python
def parse_product(item):

    return {
        "name": item.get("title"),
        "price": item.get("sale_price"),
        "rating": item.get("ratingScore")
    }
```

---

# 14. Site A Parser

`parsers/site_a_parser.py`

```python
def parse_product(item):

    return {
        "source": "site_a",

        "product_id": item.get("id"),

        "name": item.get("title"),

        "brand": item.get("brand"),

        "category": item.get("category"),

        "price": item.get("sale_price"),

        "original_price": item.get(
            "original_price"
        ),

        "rating": item.get(
            "ratingScore"
        ),

        "review_count": item.get(
            "reviewCount"
        ),

        "product_url": item.get(
            "url"
        ),

        "image_url": item.get(
            "image"
        )
    }
```

---

# 15. Site B Parser

Site B-এর fields আলাদা:

```python
def parse_product(item):

    return {
        "source": "site_b",

        "product_id": item.get(
            "data-id"
        ),

        "name": item.get(
            "product_name"
        ),

        "brand": item.get(
            "brand_name"
        ),

        "category": item.get(
            "category_name"
        ),

        "price": item.get(
            "current_price"
        ),

        "original_price": item.get(
            "regular_price"
        ),

        "rating": item.get(
            "stars"
        ),

        "review_count": item.get(
            "reviews"
        ),

        "product_url": item.get(
            "url"
        ),

        "image_url": item.get(
            "image_url"
        )
    }
```

দেখো—input আলাদা হলেও output একই।

---

# 16. Normalized Product

Site A:

```text
title → name
sale_price → price
ratingScore → rating
```

Site B:

```text
product_name → name
current_price → price
stars → rating
```

Final:

```python
{
    "name": "iPhone 16",
    "price": 120000,
    "rating": 4.8
}
```

---

# 17. Cleaner কোথায়?

M04-এর cleaner এখন এখানে আসবে:

```text
Scraper
   ↓
Parser
   ↓
Cleaner
   ↓
Validator
   ↓
Exporter
```

Example:

```python
raw = parser.parse(item)

cleaned = clean_product(raw)

valid = validate_product(cleaned)
```

---

# 18. Cleaner

`cleaners/product_cleaner.py`

```python
def clean_text(value):

    if value is None:
        return None

    return " ".join(
        str(value).split()
    )


def clean_product(product):

    product["name"] = clean_text(
        product.get("name")
    )

    product["brand"] = clean_text(
        product.get("brand")
    )

    return product
```

M04-এ আমরা price/rating/discount-এর আরও detailed cleaner তৈরি করেছি। সেগুলো এখানেই ব্যবহার করবে।

---

# 19. Validator

`validators/product_validator.py`

```python
def validate_product(product):

    if not product.get("name"):
        return False

    price = product.get("price")

    if price is not None and price < 0:
        return False

    rating = product.get("rating")

    if rating is not None:

        if rating < 0 or rating > 5:
            return False

    return True
```

---

# 20. Pipeline

এখন আমাদের actual pipeline:

```python
def process_product(
    raw_product,
    parser,
    cleaner,
    validator
):

    product = parser(raw_product)

    product = cleaner(product)

    if not validator(product):
        return None

    return product
```

---

# 21. Full Data Flow

একটা product:

```text
Website
   ↓
Scraper
   ↓
Raw Response
   ↓
Parser
   ↓
Common Schema
   ↓
Cleaner
   ↓
Normalizer
   ↓
Validator
   ↓
Deduplication
   ↓
Exporter
```

এটা খুব important architecture।

---

# 22. Scraper Registry

এখন আরও professional approach।

`main.py`:

```python
SCRAPERS = {
    "site_a": SiteAScraper(
        "https://example.com/api/products"
    ),

    "site_b": SiteBScraper(
        "https://example.com/products"
    ),

    "site_c": SiteCScraper(
        "https://example.com/catalog"
    )
}
```

তারপর:

```python
for name, scraper in SCRAPERS.items():

    print(
        f"Scraping {name}..."
    )

    data = scraper.scrape()
```

---

# 23. শুধু একটি Site Run করা

Command-line argument ব্যবহার করতে পারো।

```python
import sys

site_name = sys.argv[1]
```

Run:

```bash
python main.py site_a
```

তারপর:

```python
scraper = SCRAPERS[site_name]

data = scraper.scrape()
```

---

# 24. Multiple Sites

```bash
python main.py site_a
```

অথবা:

```bash
python main.py site_b
```

অথবা:

```bash
python main.py site_c
```

এতে debugging অনেক সহজ হবে।

---

# 25. Configuration আলাদা রাখা

`config/settings.py`

```python
SITES = {

    "site_a": {
        "type": "api",
        "url": "https://example.com/api/products"
    },

    "site_b": {
        "type": "html",
        "url": "https://example.com/products"
    },

    "site_c": {
        "type": "playwright",
        "url": "https://example.com/catalog"
    }
}
```

Production project-এ URL/config code-এর ভিতরে hard-code না করাই ভালো।

---

# 26. Environment Variables

Sensitive configuration থাকলে `.env` ব্যবহার করা যায়।

```text
API_BASE_URL=...
```

Python:

```python
import os

url = os.getenv(
    "API_BASE_URL"
)
```

Public API হলেও secrets থাকলে source code-এ রাখা উচিত নয়।

---

# 27. Logging

`print()` দিয়ে production scraper চালানো ঠিক নয়।

Python-এর `logging` ব্যবহার করো:

```python
import logging


logging.basicConfig(
    level=logging.INFO
)

logger = logging.getLogger(__name__)
```

তারপর:

```python
logger.info(
    "Starting scraper"
)
```

Error:

```python
logger.error(
    "Failed to fetch products"
)
```

---

# 28. Scraping Log

Example:

```text
2026-09-07 10:00:01 INFO Starting site_a
2026-09-07 10:00:02 INFO Page 1
2026-09-07 10:00:03 INFO Page 2
2026-09-07 10:00:04 INFO Collected 40 products
2026-09-07 10:00:04 INFO Finished site_a
```

এতে debugging অনেক সহজ।

---

# 29. Failure Isolation

ধরো:

```text
Site A → Success
Site B → Success
Site C → Failed
```

তবুও A/B-এর data save হওয়া উচিত।

খারাপ design:

```python
scrape_all()
```

এক জায়গায় error → পুরো program crash।

Better:

```python
for name, scraper in SCRAPERS.items():

    try:

        data = scraper.scrape()

    except Exception as e:

        logger.error(
            f"{name} failed: {e}"
        )

        continue
```

---

# 30. Retry

Network failure হলে retry করা যায়।

```python
import time
import requests


for attempt in range(3):

    try:

        response = requests.get(
            url,
            timeout=20
        )

        response.raise_for_status()

        break

    except requests.RequestException:

        if attempt == 2:
            raise

        time.sleep(2)
```

কিন্তু rate limiting বা server errors-এর ক্ষেত্রে responsible backoff ব্যবহার করবে।

---

# 31. Rate Limiting

Multiple website scrape করলে:

```python
import time

time.sleep(1)
```

ব্যবহার করতে পারো।

যেমন:

```python
for page in pages:

    scrape(page)

    time.sleep(1)
```

উদ্দেশ্য:

> Server-এর উপর unnecessary load না দেওয়া।

---

# 32. Raw Data Save করা

খুব গুরুত্বপূর্ণ।

Scrape করার পর সরাসরি cleaned data overwrite না করে:

```text
data/
├── raw/
└── cleaned/
```

রাখো।

Example:

```text
data/raw/site_a_2026-09-07.json
```

তারপর:

```text
data/cleaned/site_a_2026-09-07.csv
```

কেন?

কারণ parser/cleaner bug হলে raw data থেকে আবার process করা যাবে।

---

# 33. Raw vs Cleaned

```text
RAW
{
    "price": "৳89,999",
    "rating": "4.8 Stars"
}
```

↓

```text
CLEANED
{
    "price": 89999,
    "rating": 4.8
}
```

Raw data কখনো ফেলে দেবে না—বিশেষ করে development/testing phase-এ।

---

# 34. Exporter

`pipelines/exporter.py`

```python
import json
import pandas as pd


def save_json(data, path):

    with open(
        path,
        "w",
        encoding="utf-8"
    ) as f:

        json.dump(
            data,
            f,
            ensure_ascii=False,
            indent=4
        )


def save_csv(data, path):

    df = pd.DataFrame(data)

    df.to_csv(
        path,
        index=False,
        encoding="utf-8-sig"
    )
```

---

# 35. Final Pipeline Code

Conceptually:

```python
def run_scraper(
    scraper,
    parser,
    cleaner,
    validator
):

    raw_data = scraper.scrape()

    results = []

    for item in raw_data:

        product = parser(item)

        product = cleaner(product)

        if validator(product):

            results.append(product)

    return results
```

এখন:

```text
Scraper
  ↓
Parser
  ↓
Cleaner
  ↓
Validator
  ↓
Results
```

---

# 36. Factory Pattern

যখন site বাড়বে:

```text
site_a
site_b
site_c
site_d
site_e
site_f
```

তখন factory useful হতে পারে।

```python
def create_scraper(site_name):

    if site_name == "site_a":
        return SiteAScraper(...)

    if site_name == "site_b":
        return SiteBScraper(...)

    if site_name == "site_c":
        return SiteCScraper(...)

    raise ValueError(
        "Unknown site"
    )
```

---

# 37. আরও ভালো Registry

Conditional code কমাতে:

```python
SCRAPER_CLASSES = {

    "site_a": SiteAScraper,

    "site_b": SiteBScraper,

    "site_c": SiteCScraper
}
```

তারপর:

```python
scraper_class = SCRAPER_CLASSES[
    "site_a"
]

scraper = scraper_class(...)
```

---

# 38. Site Adapter Concept

প্রতিটি website-কে একটা **adapter** হিসেবে ভাবো।

```text
             Common Interface
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
    Site A       Site B       Site C
     Adapter      Adapter      Adapter
        ↓           ↓           ↓
      API          HTML       Playwright
        │           │           │
        └───────────┼───────────┘
                    ↓
             Common Product
```

এতে নতুন site যোগ করা সহজ।

---

# 39. নতুন Website যোগ করা

ধরো Site D যোগ করতে হবে।

তাহলে পুরো project পরিবর্তন করার দরকার নেই।

শুধু:

```text
scrapers/site_d.py
parsers/site_d_parser.py
```

তৈরি করবে।

তারপর registry-তে:

```python
SCRAPER_CLASSES[
    "site_d"
] = SiteDScraper
```

ব্যস।

---

# 40. M07-এর সবচেয়ে গুরুত্বপূর্ণ Design Principle

এখন তোমাকে এই distinction পরিষ্কারভাবে বুঝতে হবে:

### Scraper

```text
"কোথা থেকে data আনব?"
```

### Parser

```text
"Response-এর কোন field কী?"
```

### Cleaner

```text
"Data কীভাবে পরিষ্কার করব?"
```

### Normalizer

```text
"সব website-এর format কীভাবে এক করব?"
```

### Validator

```text
"Data valid কিনা?"
```

### Deduplicator

```text
"Duplicate কিনা?"
```

### Exporter

```text
"কোথায় save করব?"
```

---

# 41. M07 Final Architecture

এখন তোমার পুরো project:

```text
                     ┌──────────────┐
                     │  E-Commerce  │
                     │   Websites   │
                     └──────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
           API           HTML          JavaScript
             ↓              ↓              ↓
        API Scraper    HTML Scraper   Playwright
             ↓              ↓              ↓
             └──────────────┼──────────────┘
                            ↓
                         Parser
                            ↓
                    Common Schema
                            ↓
                         Cleaner
                            ↓
                       Normalizer
                            ↓
                        Validator
                            ↓
                      Deduplication
                            ↓
                      Raw Data Save
                            ↓
                     Clean Data Save
                            ↓
                       PostgreSQL
                            ↓
                    Pandas / SQL
                            ↓
                     Visualization
```

---

# 42. M07 Mini Project

এখন একটা ছোট multi-site framework বানাও:

```text
multi_ecommerce_scraper/
│
├── main.py
│
├── scrapers/
│   ├── __init__.py
│   ├── base.py
│   ├── site_a.py
│   └── site_b.py
│
├── parsers/
│   ├── site_a_parser.py
│   └── site_b_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── pipelines/
│   └── exporter.py
│
├── data/
│   ├── raw/
│   └── cleaned/
│
└── requirements.txt
```

---

# 43. তোমার Assignment

একটা **minimum 2-site collector** তৈরি করো।

### Site 1

API-based:

```text
API
 ↓
requests
 ↓
JSON
```

### Site 2

HTML-based অথবা dynamic:

```text
HTML
 ↓
BeautifulSoup
```

অথবা:

```text
JavaScript
 ↓
Playwright
```

তারপর দুটোর output একই:

```python
{
    "source": "...",
    "name": "...",
    "brand": "...",
    "category": "...",
    "price": 0,
    "original_price": 0,
    "discount": 0,
    "rating": 0,
    "review_count": 0,
    "availability": "...",
    "product_url": "...",
    "image_url": "..."
}
```

শেষে:

```text
Site A → 50 products
Site B → 50 products
          ↓
       100 products
          ↓
      Clean + Validate
          ↓
        CSV
```

---

# 44. M07 Mastery Checklist

* [ ] Base scraper
* [ ] Abstract method
* [ ] Multiple scraper classes
* [ ] API scraper
* [ ] HTML scraper
* [ ] Playwright scraper
* [ ] Common product schema
* [ ] Site-specific parser
* [ ] Cleaner integration
* [ ] Validator
* [ ] Deduplication
* [ ] Raw data storage
* [ ] Cleaned data storage
* [ ] CSV exporter
* [ ] JSON exporter
* [ ] Logging
* [ ] Error isolation
* [ ] Retry
* [ ] Rate limiting
* [ ] Configuration
* [ ] Scraper registry
* [ ] Factory concept
* [ ] Adapter concept

---

## 🔥 M01 → M07: এখন তোমার Data Collection Pipeline

```text
M01
Requests
     ↓
HTTP data collection

M02
BeautifulSoup
     ↓
HTML parsing

M03
Pagination
     ↓
Multiple pages

M04
Cleaning + Normalization
     ↓
Standard data

M05
Playwright
     ↓
Dynamic websites

M06
Network + API
     ↓
Direct JSON extraction

M07
Multi-Site Architecture
     ↓
API + HTML + Playwright
     ↓
Common Schema
     ↓
Cleaning
     ↓
Validation
     ↓
Export
```

**এখন পর্যন্ত তুমি মূলত Data Collection Layer তৈরি করেছ।**

পরবর্তী বড় ধাপ **M08 — PostgreSQL Database Integration**: scraped product data কীভাবে database-এ এমনভাবে store করবে যাতে **product, category, website, seller এবং price history** আলাদা relational tables-এ থাকে এবং পরে SQL/Pandas দিয়ে price comparison, discount analysis, brand analysis ইত্যাদি করা যায়।

----
# M08 — PostgreSQL Database Integration

এখন আমরা Data Collection pipeline-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটিতে ঢুকব:

> **Scraped e-commerce data কীভাবে PostgreSQL-এ professional relational database structure-এ store করা যায়।**

M01–M07 পর্যন্ত:

```text
Website
   ↓
API / HTML / Playwright
   ↓
Scraper
   ↓
Parser
   ↓
Cleaner
   ↓
Validator
   ↓
Common Schema
```

M08-এ হবে:

```text
Common Product Data
        ↓
    PostgreSQL
        ↓
  SQL Queries
        ↓
Price Comparison
Discount Analysis
Brand Analysis
Price History
```

---

# 1. কেন CSV যথেষ্ট নয়?

ধরো তোমার কাছে:

```csv
source,product_name,brand,category,price
site_a,iPhone 16,Apple,Smartphone,120000
site_b,iPhone 16,Apple,Smartphone,118000
site_c,iPhone 16,Apple,Smartphone,119000
```

শুরুতে CSV ভালো।

কিন্তু পরে যদি:

```text
10 websites
100 categories
100,000 products
1,000,000 price records
```

হয়?

তখন database দরকার।

বিশেষ করে আমাদের দরকার:

```text
Product
Website
Category
Brand
Seller
Price History
```

আলাদা করে manage করা।

---

# 2. PostgreSQL কেন?

PostgreSQL হলো relational database।

এখানে আমরা:

```text
Tables
Rows
Columns
Primary Keys
Foreign Keys
Indexes
Constraints
Relationships
```

ব্যবহার করতে পারি।

আমাদের project-এর জন্য PostgreSQL খুব ভালো fit।

---

# 3. Database Architecture

আমাদের initial design:

```text
                    PostgreSQL
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
     websites       categories         brands
        │               │                │
        └───────────────┼────────────────┘
                        ↓
                    products
                        │
                        ↓
                  price_history
```

আর seller দরকার হলে:

```text
                    products
                        │
                     sellers
```

---

# 4. Database তৈরি

Ubuntu-তে PostgreSQL install করা থাকলে:

```bash
sudo -u postgres psql
```

তারপর:

```sql
CREATE DATABASE ecommerce_db;
```

User তৈরি:

```sql
CREATE USER ecommerce_user
WITH PASSWORD 'your_password';
```

Permission:

```sql
GRANT ALL PRIVILEGES
ON DATABASE ecommerce_db
TO ecommerce_user;
```

তারপর:

```sql
\q
```

Database connect:

```bash
psql -U ecommerce_user -d ecommerce_db
```

---

# 5. Database-এর প্রথম Table — Websites

আমরা প্রথমে website রাখব।

```sql
CREATE TABLE websites (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    base_url TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Data:

```sql
INSERT INTO websites
(name, base_url)
VALUES
('Site A', 'https://example-a.com'),
('Site B', 'https://example-b.com');
```

দেখতে:

```sql
SELECT * FROM websites;
```

---

# 6. Website Table কেন আলাদা?

Product table-এ যদি লিখি:

```text
Site A
Site A
Site A
Site A
Site B
Site B
```

তাহলে repeated data হবে।

বরং:

```text
websites
---------
1 | Site A
2 | Site B
```

Product:

```text
website_id
----------
1
1
1
2
2
```

এটা database normalization-এর দিকে যায়।

---

# 7. Categories Table

```sql
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
```

Data:

```sql
INSERT INTO categories (name)
VALUES
('Smartphone'),
('Laptop'),
('Tablet'),
('Headphone');
```

---

# 8. Brands Table

```sql
CREATE TABLE brands (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
```

Example:

```sql
INSERT INTO brands (name)
VALUES
('Apple'),
('Samsung'),
('Xiaomi'),
('Dell');
```

---

# 9. Products Table

এখন main table।

```sql
CREATE TABLE products (
    id BIGSERIAL PRIMARY KEY,

    website_id INTEGER
        REFERENCES websites(id),

    category_id INTEGER
        REFERENCES categories(id),

    brand_id INTEGER
        REFERENCES brands(id),

    external_product_id VARCHAR(255),

    name TEXT NOT NULL,

    product_url TEXT,

    image_url TEXT,

    description TEXT,

    availability VARCHAR(50),

    created_at TIMESTAMP
        DEFAULT CURRENT_TIMESTAMP,

    updated_at TIMESTAMP
        DEFAULT CURRENT_TIMESTAMP
);
```

---

# 10. Product ID বনাম External Product ID

এটা খুব important।

আমাদের database:

```text
id = 1
```

এটা আমাদের internal ID।

Website-এর:

```text
product_id = 938472
```

হতে পারে।

তাই:

```text
id
external_product_id
```

আলাদা রাখব।

Example:

```text
Database ID → 1

Site A Product ID → 938472
```

---

# 11. Price আলাদা Table-এ কেন?

ধরো:

আজ:

```text
iPhone 16 → 120000
```

কাল:

```text
iPhone 16 → 118000
```

পরশু:

```text
iPhone 16 → 115000
```

যদি product table-এ শুধু:

```text
price = 115000
```

রাখো, তাহলে আগের দাম হারিয়ে যাবে।

আমরা চাই:

```text
Price History
----------------------
Date        Price
Sep 7       120000
Sep 8       118000
Sep 9       115000
```

তাই price আলাদা table।

---

# 12. Price History Table

```sql
CREATE TABLE price_history (
    id BIGSERIAL PRIMARY KEY,

    product_id BIGINT NOT NULL
        REFERENCES products(id)
        ON DELETE CASCADE,

    price NUMERIC(12, 2) NOT NULL,

    original_price NUMERIC(12, 2),

    discount NUMERIC(5, 2),

    rating NUMERIC(3, 2),

    review_count INTEGER,

    scraped_at TIMESTAMP
        DEFAULT CURRENT_TIMESTAMP
);
```

---

# 13. কেন Rating-ও Price History-তে?

কারণ rating/review count সময়ের সাথে পরিবর্তিত হতে পারে।

আজ:

```text
Rating = 4.5
Reviews = 120
```

এক মাস পরে:

```text
Rating = 4.7
Reviews = 350
```

তাই historical analytics করতে চাইলে snapshot হিসেবে price observation-এর সঙ্গে রাখা useful।

তবে project-এর প্রয়োজন অনুযায়ী rating/reviews-এর জন্য আলাদা history table-ও করা যায়।

---

# 14. Final Database Relationship

```text
websites
   │
   │ 1
   │
   │ N
products
   │
   │ 1
   │
   │ N
price_history
```

আর:

```text
categories
     │
     │ 1
     │
     │ N
  products
```

```text
brands
   │
   │ 1
   │
   │ N
products
```

---

# 15. ERD Concept

```text
┌──────────────┐
│   websites   │
├──────────────┤
│ id PK        │
│ name         │
│ base_url     │
└──────┬───────┘
       │
       │ 1:N
       ↓
┌──────────────┐
│   products   │
├──────────────┤
│ id PK        │
│ website_id FK│
│ category_id FK
│ brand_id FK  │
│ external_id  │
│ name         │
│ product_url  │
└──────┬───────┘
       │
       │ 1:N
       ↓
┌─────────────────┐
│ price_history   │
├─────────────────┤
│ id PK           │
│ product_id FK   │
│ price           │
│ original_price  │
│ discount        │
│ rating          │
│ review_count    │
│ scraped_at      │
└─────────────────┘
```

---

# 16. PostgreSQL Python-এর সঙ্গে connect করা

আমরা `psycopg` ব্যবহার করতে পারি।

Install:

```bash
pip install psycopg[binary]
```

---

# 17. Basic Connection

```python
import psycopg


connection = psycopg.connect(
    host="localhost",
    port=5432,
    dbname="ecommerce_db",
    user="ecommerce_user",
    password="your_password"
)

print("Database connected!")
```

---

# 18. Cursor

Database query execute করার জন্য cursor ব্যবহার করতে পারো:

```python
with connection.cursor() as cursor:

    cursor.execute(
        "SELECT * FROM websites"
    )

    rows = cursor.fetchall()

    for row in rows:
        print(row)
```

শেষে:

```python
connection.close()
```

---

# 19. Better Connection Pattern

```python
import psycopg


with psycopg.connect(
    host="localhost",
    port=5432,
    dbname="ecommerce_db",
    user="ecommerce_user",
    password="your_password"
) as connection:

    with connection.cursor() as cursor:

        cursor.execute(
            "SELECT * FROM websites"
        )

        rows = cursor.fetchall()

        for row in rows:
            print(row)
```

Context manager ব্যবহার করলে transaction/connection handling সহজ হয়।

---

# 20. Insert Website

```python
with connection.cursor() as cursor:

    cursor.execute(
        """
        INSERT INTO websites
        (name, base_url)
        VALUES (%s, %s)
        """,
        (
            "Site A",
            "https://example-a.com"
        )
    )

connection.commit()
```

---

# 21. SQL Injection Avoid করা

এভাবে লিখবে না:

```python
query = f"""
INSERT INTO products (name)
VALUES ('{name}')
"""
```

কারণ user/data input-এর কারণে SQL injection risk তৈরি হতে পারে।

তার বদলে parameterized query:

```python
cursor.execute(
    """
    INSERT INTO products (name)
    VALUES (%s)
    """,
    (name,)
)
```

এটাই correct approach।

---

# 22. Product Insert

```python
product = {
    "website_id": 1,
    "category_id": 1,
    "brand_id": 1,
    "external_product_id": "A-1001",
    "name": "iPhone 16",
    "product_url": "https://example.com/iphone16",
    "image_url": "https://example.com/image.jpg",
    "availability": "in_stock"
}
```

Insert:

```python
cursor.execute(
    """
    INSERT INTO products (
        website_id,
        category_id,
        brand_id,
        external_product_id,
        name,
        product_url,
        image_url,
        availability
    )
    VALUES (%s, %s, %s, %s, %s, %s, %s, %s)
    """,
    (
        product["website_id"],
        product["category_id"],
        product["brand_id"],
        product["external_product_id"],
        product["name"],
        product["product_url"],
        product["image_url"],
        product["availability"]
    )
)
```

---

# 23. Insert করার পর Product ID পাওয়া

এটা খুব useful।

```python
cursor.execute(
    """
    INSERT INTO products (
        website_id,
        name
    )
    VALUES (%s, %s)
    RETURNING id
    """,
    (1, "iPhone 16")
)

product_id = cursor.fetchone()[0]

print(product_id)
```

ধরো:

```text
product_id = 42
```

এখন price history-তে:

```python
cursor.execute(
    """
    INSERT INTO price_history (
        product_id,
        price
    )
    VALUES (%s, %s)
    """,
    (
        product_id,
        120000
    )
)
```

---

# 24. Transaction

ধরো:

```text
Product insert
     ↓
Price insert
```

দ্বিতীয়টা fail করলে প্রথমটাও rollback করা ভালো।

```python
try:

    with connection.cursor() as cursor:

        # Product insert
        ...

        # Price insert
        ...

    connection.commit()

except Exception:

    connection.rollback()

    raise
```

এতে database inconsistent হওয়ার chance কমে।

---

# 25. `ON CONFLICT`

একই website-এর একই product বারবার insert করতে চাই না।

ধরো:

```text
website_id = 1
external_product_id = "A100"
```

এটাকে unique করতে পারি।

```sql
ALTER TABLE products
ADD CONSTRAINT unique_site_product
UNIQUE (
    website_id,
    external_product_id
);
```

এখন duplicate insert আটকানো যাবে।

---

# 26. Upsert

ধরো product already exists।

আমরা update করতে চাই।

PostgreSQL:

```sql
INSERT INTO products (
    website_id,
    external_product_id,
    name,
    product_url
)
VALUES (
    %s, %s, %s, %s
)
ON CONFLICT (
    website_id,
    external_product_id
)
DO UPDATE SET
    name = EXCLUDED.name,
    product_url = EXCLUDED.product_url,
    updated_at = CURRENT_TIMESTAMP;
```

এটাকে **upsert** বলা হয়।

---

# 27. কেন Upsert আমাদের Project-এ দরকার?

Scraper প্রতিদিন চলবে:

```text
Monday
 ↓
Product A exists

Tuesday
 ↓
Same Product A

Wednesday
 ↓
Same Product A
```

আমরা চাই:

```text
products
→ one product record
```

কিন্তু:

```text
price_history
→ every scraping observation
```

অর্থাৎ:

```text
products
   ↓
same product

price_history
   ↓
many price records
```

---

# 28. Example

Product:

```text
id = 1
name = iPhone 16
```

Price history:

```text
id | product_id | price
------------------------
1  | 1          | 120000
2  | 1          | 118000
3  | 1          | 115000
```

এখন আমরা price trend দেখতে পারব।

---

# 29. Insert Price Snapshot

```python
from datetime import datetime


cursor.execute(
    """
    INSERT INTO price_history (
        product_id,
        price,
        original_price,
        discount,
        rating,
        review_count,
        scraped_at
    )
    VALUES (
        %s, %s, %s, %s, %s, %s, %s
    )
    """,
    (
        product_id,
        115000,
        130000,
        11.54,
        4.7,
        350,
        datetime.now()
    )
)
```

---

# 30. Database থেকে Data পড়া

```python
cursor.execute(
    """
    SELECT
        name,
        product_url
    FROM products
    """
)

rows = cursor.fetchall()

for row in rows:

    print(row[0])
    print(row[1])
```

---

# 31. JOIN

এখন আসল SQL power।

আমরা চাই:

```text
Product
+
Website
+
Brand
+
Category
```

Query:

```sql
SELECT
    p.name,
    w.name AS website,
    b.name AS brand,
    c.name AS category
FROM products p
JOIN websites w
    ON p.website_id = w.id
JOIN brands b
    ON p.brand_id = b.id
JOIN categories c
    ON p.category_id = c.id;
```

Result:

```text
iPhone 16 | Site A | Apple | Smartphone
```

---

# 32. Product + Current Price

ধরো latest price বের করতে চাই।

একটি approach:

```sql
SELECT
    p.name,
    ph.price,
    ph.scraped_at
FROM products p
JOIN price_history ph
    ON p.id = ph.product_id;
```

এতে সব historical price আসবে।

Latest price দরকার হলে আরও precise query লাগবে।

---

# 33. Latest Price with PostgreSQL

PostgreSQL-এর `DISTINCT ON` ব্যবহার করা যায়:

```sql
SELECT DISTINCT ON (product_id)
    product_id,
    price,
    scraped_at
FROM price_history
ORDER BY
    product_id,
    scraped_at DESC;
```

এটা প্রতিটি product-এর latest record দেবে।

---

# 34. Price Comparison

ধরো একই product বিভিন্ন website-এ আছে।

Query concept:

```sql
SELECT
    p.name,
    w.name AS website,
    ph.price
FROM products p
JOIN websites w
    ON p.website_id = w.id
JOIN price_history ph
    ON p.id = ph.product_id;
```

তারপর:

```text
iPhone 16

Site A → 120000
Site B → 118000
Site C → 119000
```

আমাদের future analytics system এখান থেকেই তৈরি হবে।

---

# 35. Cheapest Product

Latest price ধরে cheapest বের করতে:

```sql
SELECT
    p.name,
    w.name AS website,
    ph.price
FROM products p
JOIN websites w
    ON p.website_id = w.id
JOIN price_history ph
    ON p.id = ph.product_id
ORDER BY ph.price ASC
LIMIT 10;
```

Production version-এ অবশ্যই latest-price filtering যোগ করবে, যাতে পুরোনো price-এর সঙ্গে comparison না হয়।

---

# 36. Index

Data বড় হলে query slow হতে পারে।

তাই indexes:

```sql
CREATE INDEX idx_products_website
ON products(website_id);
```

Price history:

```sql
CREATE INDEX idx_price_product
ON price_history(product_id);
```

Time-based query:

```sql
CREATE INDEX idx_price_scraped_at
ON price_history(scraped_at);
```

---

# 37. কেন Index?

ধরো:

```text
10 rows
```

search দ্রুত।

কিন্তু:

```text
10 million rows
```

হলে database-কে efficient search structure দরকার।

Index অনেক query দ্রুত করতে পারে।

তবে:

> সব column-এ index দেওয়া উচিত নয়।

কারণ index-এরও storage ও write/update cost আছে।

---

# 38. Data Types

Price-এর জন্য:

```sql
NUMERIC(12, 2)
```

ভালো choice।

Avoid:

```sql
FLOAT
```

যখন exact monetary value গুরুত্বপূর্ণ।

Example:

```text
120000.00
```

---

# 39. Rating

```sql
NUMERIC(3, 2)
```

যেমন:

```text
4.80
```

---

# 40. Review Count

```sql
INTEGER
```

Example:

```text
1250
```

M04-এ:

```text
1.2K
```

কে:

```text
1200
```

এ convert করেছিলাম।

Database-এ clean integer রাখব।

---

# 41. Scraper → PostgreSQL

এখন পুরো pipeline:

```text
Website
   ↓
Scraper
   ↓
Raw Data
   ↓
Parser
   ↓
Common Schema
   ↓
Cleaner
   ↓
Validator
   ↓
Deduplication
   ↓
PostgreSQL
   │
   ├── websites
   ├── categories
   ├── brands
   ├── products
   └── price_history
```

---

# 42. Database Layer আলাদা করো

Project:

```text
ecommerce-data-collector/
│
├── database/
│   ├── connection.py
│   ├── websites.py
│   ├── products.py
│   └── prices.py
│
├── scrapers/
├── parsers/
├── cleaners/
├── validators/
├── pipelines/
│
├── data/
│
└── main.py
```

---

# 43. `connection.py`

```python
import psycopg


def get_connection():

    return psycopg.connect(
        host="localhost",
        port=5432,
        dbname="ecommerce_db",
        user="ecommerce_user",
        password="your_password"
    )
```

---

# 44. Product Repository

`database/products.py`

```python
from .connection import get_connection


def insert_product(product):

    with get_connection() as connection:

        with connection.cursor() as cursor:

            cursor.execute(
                """
                INSERT INTO products (
                    website_id,
                    external_product_id,
                    name,
                    product_url,
                    image_url
                )
                VALUES (%s, %s, %s, %s, %s)
                RETURNING id
                """,
                (
                    product["website_id"],
                    product["product_id"],
                    product["name"],
                    product["product_url"],
                    product["image_url"]
                )
            )

            return cursor.fetchone()[0]
```

---

# 45. Price Repository

`database/prices.py`

```python
from .connection import get_connection


def insert_price(
    product_id,
    price,
    original_price,
    discount,
    rating,
    review_count
):

    with get_connection() as connection:

        with connection.cursor() as cursor:

            cursor.execute(
                """
                INSERT INTO price_history (
                    product_id,
                    price,
                    original_price,
                    discount,
                    rating,
                    review_count
                )
                VALUES (
                    %s, %s, %s, %s, %s, %s
                )
                """,
                (
                    product_id,
                    price,
                    original_price,
                    discount,
                    rating,
                    review_count
                )
            )
```

---

# 46. Professional Flow

এখন একটি scraped product:

```python
product = {
    "source": "site_a",
    "product_id": "A100",
    "name": "iPhone 16",
    "brand": "Apple",
    "category": "Smartphone",
    "price": 120000,
    "original_price": 130000,
    "discount": 7.69,
    "rating": 4.8,
    "review_count": 250,
    "availability": "in_stock",
    "product_url": "...",
    "image_url": "..."
}
```

Pipeline:

```text
product
   ↓
Find website
   ↓
Find category
   ↓
Find brand
   ↓
Upsert product
   ↓
Get product_id
   ↓
Insert price snapshot
```

---

# 47. Important Concept — Product Identity

এখানে একটা বড় challenge আছে।

ধরো:

```text
Site A:
Apple iPhone 16 128GB Black

Site B:
iPhone 16 - Black - 128 GB

Site C:
Apple iPhone 16 128 GB
```

এগুলো কি একই product?

Human বুঝতে পারে।

Database automatically বুঝবে না।

এটা হলো:

> **Entity Resolution / Product Matching**

এটা আমাদের later advanced module-এ আসবে।

---

# 48. M08 Mini Project

এখন তোমার project:

```text
ecommerce_db
│
├── websites
├── categories
├── brands
├── products
└── price_history
```

তারপর:

```text
2 websites
   ↓
100 products
   ↓
PostgreSQL
```

প্রথম scraping:

```text
iPhone 16 → 120000
```

দ্বিতীয় scraping:

```text
iPhone 16 → 118000
```

Database:

```text
products
---------
iPhone 16

price_history
-------------
120000
118000
```

---

# 49. M08 Practice Tasks

### Task 1

PostgreSQL install/setup করো।

### Task 2

Database তৈরি করো:

```text
ecommerce_db
```

### Task 3

এই tables তৈরি করো:

```text
websites
categories
brands
products
price_history
```

### Task 4

Foreign key relationship তৈরি করো।

### Task 5

একটি product insert করো।

### Task 6

একই product-এর 3টি price snapshot insert করো।

### Task 7

JOIN দিয়ে:

```text
product
website
brand
category
price
```

দেখাও।

### Task 8

latest price বের করো।

### Task 9

সবচেয়ে কম price বের করো।

### Task 10

M07 scraper-এর output PostgreSQL-এ save করো।

---

# 50. M08 Mastery Checklist

* [ ] PostgreSQL basics
* [ ] Database create
* [ ] Table create
* [ ] Primary Key
* [ ] Foreign Key
* [ ] UNIQUE constraint
* [ ] NOT NULL
* [ ] `SERIAL`
* [ ] `BIGSERIAL`
* [ ] `NUMERIC`
* [ ] Relationships
* [ ] One-to-many
* [ ] INSERT
* [ ] SELECT
* [ ] UPDATE
* [ ] DELETE
* [ ] JOIN
* [ ] Index
* [ ] Transaction
* [ ] Rollback
* [ ] Upsert
* [ ] `ON CONFLICT`
* [ ] Psycopg
* [ ] Python → PostgreSQL
* [ ] Product table
* [ ] Price history
* [ ] Database repository layer

---

# 🔥 M01 → M08 Complete Pipeline

এখন তুমি যে system বানাচ্ছ সেটা আর simple scraper নয়।

```text
                   E-COMMERCE WEBSITES
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
        API             HTML              JS
          ↓                ↓                ↓
     Requests         BeautifulSoup     Playwright
          └────────────────┼────────────────┘
                           ↓
                      Site Parsers
                           ↓
                    Common Schema
                           ↓
                 Cleaning / Normalize
                           ↓
                      Validation
                           ↓
                     Deduplication
                           ↓
                     PostgreSQL
                           │
         ┌─────────────────┼─────────────────┐
         ↓                 ↓                 ↓
     Websites          Products        Price History
         │                 │                 │
         └─────────────────┼─────────────────┘
                           ↓
                       SQL Analysis
                           ↓
                    Pandas Analysis
                           ↓
                       Dashboard
```

## 🎯 M08-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা

একটা **product** আর একটা **price observation** একই জিনিস নয়।

```text
PRODUCT
------
iPhone 16
Apple
Smartphone
Site A

        ↓

PRICE HISTORY
-------------
Sep 1 → 120,000
Sep 2 → 119,000
Sep 3 → 117,500
Sep 4 → 115,000
```

এই separation-টাই তোমার future project-এর সবচেয়ে গুরুত্বপূর্ণ database design decisionগুলোর একটি।

**পরের M09-এ আমরা PostgreSQL-এর এই collected data নিয়ে `Pandas + SQL` দিয়ে actual e-commerce analytics শুরু করব—price comparison, discount analysis, brand performance, category analysis, rating/review analysis, cheapest seller এবং statistical analysis।**

----
# M09 — PostgreSQL + Pandas E-commerce Analytics Deep Dive

M08-এ আমরা **scraped e-commerce data PostgreSQL-এ store** করা শিখেছি।
এখন M09-এ সেই database-এর data নিয়ে **real-world analytics** করব।

আমাদের complete flow হবে:

```text
E-commerce Websites
        ↓
     Scraper
        ↓
   PostgreSQL
        ↓
       SQL
        ↓
     Pandas
        ↓
   Data Cleaning
        ↓
     Analysis
        ↓
   CSV / Excel / Reports
```

---

# 🎯 M09-এর Main Goal

এই module শেষে তুমি PostgreSQL থেকে data নিয়ে জানতে পারবে:

* কোন website-এ product সবচেয়ে cheap?
* কোন website-এর average price কম?
* কোন product-এর discount বেশি?
* কোন brand সবচেয়ে বেশি products sell করছে?
* কোন category-তে price বেশি?
* কোন category-তে discount বেশি?
* rating বনাম review count কেমন?
* কোন product-এর price সবচেয়ে বেশি?
* কোন product-এর price সবচেয়ে কম?
* একই product-এর বিভিন্ন website-এর price difference কত?
* price history থেকে price কতটা পরিবর্তন হয়েছে?

---

# M09.01 — PostgreSQL থেকে Pandas-এ Data নেওয়া

আমাদের দরকার হবে:

```bash
pip install pandas sqlalchemy psycopg
```

Project structure:

```text
ecommerce-data-collector/
│
├── database/
│   ├── connection.py
│   ├── products.py
│   └── prices.py
│
├── analytics/
│   ├── load_data.py
│   ├── price_analysis.py
│   ├── discount_analysis.py
│   └── product_analysis.py
│
├── data/
│   ├── exports/
│   └── reports/
│
└── main.py
```

---

# M09.02 — Database Connection

SQLAlchemy ব্যবহার করলে Pandas-এর সাথে কাজ করা সহজ হয়।

```python
from sqlalchemy import create_engine

DATABASE_URL = (
    "postgresql+psycopg://"
    "ecommerce_user:your_password@localhost:5432/ecommerce_db"
)

engine = create_engine(DATABASE_URL)
```

Test:

```python
with engine.connect() as connection:
    print("Database connected!")
```

---

# M09.03 — PostgreSQL → Pandas DataFrame

ধরো আমরা products দেখতে চাই।

```python
import pandas as pd

query = """
SELECT *
FROM products;
"""

df = pd.read_sql(query, engine)

print(df.head())
```

এখন:

```text
PostgreSQL Table
       ↓
   SQL Query
       ↓
Pandas DataFrame
```

---

# M09.04 — Product + Website + Category + Brand

শুধু `products` table আমাদের জন্য যথেষ্ট নয়।

কারণ:

```text
products
    ↓
website_id
category_id
brand_id
```

তাই `JOIN` ব্যবহার করব।

```sql
SELECT
    p.id,
    w.name AS website,
    c.name AS category,
    b.name AS brand,
    p.external_product_id,
    p.name,
    p.product_url,
    p.availability
FROM products p
LEFT JOIN websites w
    ON p.website_id = w.id
LEFT JOIN categories c
    ON p.category_id = c.id
LEFT JOIN brands b
    ON p.brand_id = b.id;
```

Python:

```python
query = """
SELECT
    p.id,
    w.name AS website,
    c.name AS category,
    b.name AS brand,
    p.external_product_id,
    p.name,
    p.product_url,
    p.availability
FROM products p
LEFT JOIN websites w
    ON p.website_id = w.id
LEFT JOIN categories c
    ON p.category_id = c.id
LEFT JOIN brands b
    ON p.brand_id = b.id;
"""

df_products = pd.read_sql(query, engine)

print(df_products.head())
```

---

# M09.05 — Latest Price বের করা

M08-এ আমাদের `price_history` ছিল:

```text
price_history
------------------------
product_id
price
original_price
discount
rating
review_count
scraped_at
```

এক product-এর অনেক price record থাকতে পারে।

Example:

```text
iPhone 16

2026-09-01 → 95,000
2026-09-02 → 94,500
2026-09-03 → 93,999
2026-09-04 → 92,999
```

আমাদের অনেক সময় শুধু **latest price** দরকার।

PostgreSQL-এ:

```sql
SELECT DISTINCT ON (product_id)
    product_id,
    price,
    original_price,
    discount,
    rating,
    review_count,
    scraped_at
FROM price_history
ORDER BY product_id, scraped_at DESC;
```

এখানে:

```sql
ORDER BY product_id, scraped_at DESC
```

এর কারণে প্রতিটি product-এর সবচেয়ে recent record প্রথমে আসবে।

---

# M09.06 — Product + Latest Price একসাথে

এখন সবচেয়ে useful query:

```sql
SELECT
    p.id,
    w.name AS website,
    c.name AS category,
    b.name AS brand,
    p.name,
    ph.price,
    ph.original_price,
    ph.discount,
    ph.rating,
    ph.review_count,
    ph.scraped_at
FROM products p

LEFT JOIN websites w
    ON p.website_id = w.id

LEFT JOIN categories c
    ON p.category_id = c.id

LEFT JOIN brands b
    ON p.brand_id = b.id

LEFT JOIN (
    SELECT DISTINCT ON (product_id)
        product_id,
        price,
        original_price,
        discount,
        rating,
        review_count,
        scraped_at
    FROM price_history
    ORDER BY product_id, scraped_at DESC
) ph
    ON p.id = ph.product_id;
```

Pandas:

```python
df = pd.read_sql(query, engine)

print(df.head())
```

এখন আমাদের DataFrame হতে পারে:

| website   | category   | brand  | name      | price | discount | rating |
| --------- | ---------- | ------ | --------- | ----: | -------: | -----: |
| Daraz     | Smartphone | Apple  | iPhone 16 | 92000 |        8 |    4.7 |
| Pickaboo  | Smartphone | Apple  | iPhone 16 | 93500 |        5 |    4.6 |
| Star Tech | Laptop     | Lenovo | IdeaPad   | 65000 |       10 |    4.5 |

---

# M09.07 — DataFrame Inspect করা

প্রথমে data বুঝতে হবে।

```python
print(df.head())
```

শেষের data:

```python
print(df.tail())
```

Shape:

```python
print(df.shape)
```

Example:

```text
(5000, 12)
```

মানে:

```text
5000 rows
12 columns
```

---

# M09.08 — Column দেখা

```python
print(df.columns)
```

Output:

```text
Index([
    'id',
    'website',
    'category',
    'brand',
    'name',
    'price',
    'original_price',
    'discount',
    'rating',
    'review_count',
    'scraped_at'
], dtype='object')
```

---

# M09.09 — Data Types

```python
print(df.dtypes)
```

Example:

```text
price            float64
discount         float64
rating           float64
review_count       int64
scraped_at        object
```

---

# M09.10 — `info()`

```python
df.info()
```

এটা খুব important।

এতে দেখতে পারবে:

* কত rows
* কোন column-এর datatype
* কতগুলো non-null value
* memory usage

---

# M09.11 — Statistical Summary

```python
print(df.describe())
```

Price:

```python
print(df["price"].describe())
```

Output conceptually:

```text
count       4500
mean       48500
std        32000
min         1500
25%        12000
50%        38000
75%        70000
max       250000
```

এখান থেকে আমরা বুঝতে পারি:

```text
Average price = 48,500
Minimum       = 1,500
Maximum       = 250,000
```

---

# M09.12 — Missing Values

প্রথমে:

```python
print(df.isnull().sum())
```

Example:

```text
price              10
discount           50
rating            120
review_count       80
brand               5
```

Percentage:

```python
missing_percentage = (
    df.isnull().mean() * 100
)

print(missing_percentage)
```

---

# M09.13 — Missing Price Handle

Price missing হলে সাধারণত fake value দেওয়া উচিত নয়।

Bad:

```python
df["price"] = df["price"].fillna(0)
```

কারণ:

```text
0 টাকা
```

মানে actual price zero—যা ভুল হতে পারে।

Better:

```python
df = df.dropna(subset=["price"])
```

---

# M09.14 — Duplicate Data

```python
print(df.duplicated().sum())
```

Duplicate remove:

```python
df = df.drop_duplicates()
```

Product-level duplicate যদি website + external ID দিয়ে detect করতে চাই:

```python
df = df.drop_duplicates(
    subset=["website", "name"]
)
```

তবে বাস্তব project-এ শুধু `name` দিয়ে duplicate detect করা সবসময় নিরাপদ নয়।

---

# M09.15 — Price Filtering

Price > 50,000:

```python
expensive = df[df["price"] > 50000]

print(expensive)
```

Price < 10,000:

```python
cheap = df[df["price"] < 10000]
```

Range:

```python
mid_range = df[
    (df["price"] >= 10000) &
    (df["price"] <= 50000)
]
```

---

# M09.16 — Sorting

সবচেয়ে expensive products:

```python
df.sort_values(
    by="price",
    ascending=False
).head(10)
```

সবচেয়ে cheap:

```python
df.sort_values(
    by="price",
    ascending=True
).head(10)
```

---

# M09.17 — Cheapest Product

```python
cheapest = df.loc[df["price"].idxmin()]

print(cheapest)
```

Most expensive:

```python
expensive = df.loc[df["price"].idxmax()]

print(expensive)
```

---

# M09.18 — Website-wise Average Price

এটা e-commerce analytics-এর খুব important analysis।

```python
website_price = (
    df.groupby("website")["price"]
      .mean()
      .sort_values()
)

print(website_price)
```

Example:

```text
Website A    42,500
Website B    46,800
Website C    51,200
```

তাহলে:

```text
Website A
```

এর average product price সবচেয়ে কম।

---

# M09.19 — Website-wise Price Statistics

শুধু average না।

```python
website_stats = (
    df.groupby("website")["price"]
      .agg([
          "count",
          "mean",
          "min",
          "max",
          "median"
      ])
)

print(website_stats)
```

আমরা পাব:

| website | count |  mean | min |    max | median |
| ------- | ----: | ----: | --: | -----: | -----: |
| Site A  |  1200 | 45000 | 500 | 250000 |  38000 |
| Site B  |   900 | 47000 | 800 | 220000 |  40000 |

---

# M09.20 — Category-wise Price Analysis

```python
category_price = (
    df.groupby("category")["price"]
      .agg(["count", "mean", "min", "max"])
      .sort_values("mean", ascending=False)
)

print(category_price)
```

এতে বুঝতে পারবে:

```text
Laptop       → expensive
Smartphone   → medium
Accessories  → cheap
```

---

# M09.21 — Brand-wise Analysis

```python
brand_analysis = (
    df.groupby("brand")
      .agg(
          product_count=("name", "count"),
          average_price=("price", "mean"),
          minimum_price=("price", "min"),
          maximum_price=("price", "max"),
          average_rating=("rating", "mean")
      )
      .sort_values(
          "product_count",
          ascending=False
      )
)

print(brand_analysis.head(20))
```

এটা খুব powerful।

---

# M09.22 — কোন Brand-এর Product সবচেয়ে বেশি?

```python
brand_counts = (
    df["brand"]
      .value_counts()
)

print(brand_counts.head(10))
```

Example:

```text
Samsung      520
Xiaomi       410
Apple        350
Realme       300
```

---

# M09.23 — Discount Analysis

Average discount:

```python
average_discount = df["discount"].mean()

print(average_discount)
```

Website-wise:

```python
discount_by_website = (
    df.groupby("website")["discount"]
      .mean()
      .sort_values(ascending=False)
)

print(discount_by_website)
```

---

# M09.24 — Category-wise Discount

```python
discount_by_category = (
    df.groupby("category")["discount"]
      .agg([
          "count",
          "mean",
          "max"
      ])
      .sort_values(
          "mean",
          ascending=False
      )
)

print(discount_by_category)
```

এখান থেকে জানা যাবে:

> কোন category-তে average discount সবচেয়ে বেশি?

---

# M09.25 — Highest Discount Products

```python
top_discount = (
    df.sort_values(
        by="discount",
        ascending=False
    )
    .head(20)
)

print(
    top_discount[
        [
            "website",
            "name",
            "price",
            "original_price",
            "discount"
        ]
    ]
)
```

---

# M09.26 — Rating Analysis

Average rating:

```python
print(df["rating"].mean())
```

Website-wise:

```python
rating_by_website = (
    df.groupby("website")["rating"]
      .mean()
      .sort_values(ascending=False)
)

print(rating_by_website)
```

Brand-wise:

```python
rating_by_brand = (
    df.groupby("brand")["rating"]
      .mean()
      .sort_values(ascending=False)
)

print(rating_by_brand.head(10))
```

---

# M09.27 — Review Count Analysis

সবচেয়ে বেশি reviewed products:

```python
top_reviewed = (
    df.sort_values(
        by="review_count",
        ascending=False
    )
    .head(20)
)

print(
    top_reviewed[
        ["name", "brand", "rating", "review_count"]
    ]
)
```

---

# M09.28 — Rating + Review Count

ধরো:

```text
Product A
rating = 5.0
reviews = 2
```

এটা সবসময় খুব trustworthy signal নয়।

অন্যদিকে:

```text
Product B
rating = 4.7
reviews = 20,000
```

এটার rating অনেক বেশি meaningful হতে পারে।

তাই দুইটা metric একসাথে দেখতে হবে।

```python
df[
    ["name", "rating", "review_count"]
].sort_values(
    "review_count",
    ascending=False
).head(20)
```

---

# M09.29 — Price vs Rating

আমরা জানতে চাই:

> expensive product কি বেশি rating পায়?

```python
price_rating = df[
    ["price", "rating"]
].dropna()

print(
    price_rating.corr()
)
```

শুধু correlation coefficient:

```python
correlation = (
    df["price"]
      .corr(df["rating"])
)

print(correlation)
```

Interpretation:

```text
+1   → strong positive relationship
 0   → little/no linear relationship
-1   → strong negative relationship
```

কিন্তু correlation মানেই causation নয়।

---

# M09.30 — Price Comparison

এখন আসি আমাদের সবচেয়ে important e-commerce analysis-এ।

ধরো:

```text
Product: iPhone 16

Site A → 92,000
Site B → 95,000
Site C → 89,500
```

আমরা জানতে চাই:

```text
Cheapest seller = Site C
```

যদি product identity ঠিকভাবে normalized থাকে:

```python
comparison = (
    df.groupby("name")
      .agg(
          cheapest_price=("price", "min"),
          expensive_price=("price", "max"),
          average_price=("price", "mean")
      )
)

print(comparison)
```

---

# M09.31 — Price Spread

Price spread:

```python
comparison["price_spread"] = (
    comparison["expensive_price"]
    - comparison["cheapest_price"]
)
```

এখন:

```python
print(
    comparison.sort_values(
        "price_spread",
        ascending=False
    ).head(20)
)
```

এতে বুঝতে পারবে কোন product-এর seller-to-seller price difference বেশি।

---

# M09.32 — Cheapest Website per Product

```python
idx = df.groupby("name")["price"].idxmin()

cheapest_sellers = df.loc[
    idx,
    [
        "name",
        "website",
        "price"
    ]
]

print(cheapest_sellers)
```

Example:

| Product    | Website |  Price |
| ---------- | ------- | -----: |
| iPhone 16  | Site C  | 89,500 |
| Galaxy S25 | Site A  | 91,000 |
| Redmi Note | Site B  | 22,500 |

---

# M09.33 — Most Expensive Website

```python
idx = df.groupby("name")["price"].idxmax()

most_expensive = df.loc[
    idx,
    [
        "name",
        "website",
        "price"
    ]
]

print(most_expensive)
```

---

# M09.34 — Price Difference Percentage

ধরো:

```text
minimum = 90,000
maximum = 100,000
```

Difference:

```text
10,000
```

Percentage:

```python
comparison["price_difference_percent"] = (
    comparison["price_spread"]
    / comparison["cheapest_price"]
) * 100
```

---

# M09.35 — Real Product Comparison Table

```python
product_comparison = (
    df.pivot_table(
        index="name",
        columns="website",
        values="price",
        aggfunc="min"
    )
)

print(product_comparison)
```

Output:

```text
website              Site A    Site B    Site C

iPhone 16             92000     95000     89500
Galaxy S25            91000     93000     90000
Redmi Note             22000     21500     23000
```

এটা e-commerce price comparison system-এর foundation।

---

# M09.36 — Price History Analysis

এখন আমরা latest price না নিয়ে পুরো `price_history` load করব।

```python
query = """
SELECT
    p.name,
    w.name AS website,
    ph.price,
    ph.discount,
    ph.rating,
    ph.review_count,
    ph.scraped_at
FROM price_history ph
JOIN products p
    ON ph.product_id = p.id
JOIN websites w
    ON p.website_id = w.id;
"""

price_history_df = pd.read_sql(
    query,
    engine
)
```

---

# M09.37 — DateTime Conversion

```python
price_history_df["scraped_at"] = pd.to_datetime(
    price_history_df["scraped_at"]
)
```

তারপর:

```python
print(
    price_history_df["scraped_at"].dtype
)
```

হওয়া উচিত:

```text
datetime64[ns]
```

---

# M09.38 — Daily Price

```python
price_history_df["date"] = (
    price_history_df["scraped_at"]
    .dt.date
)
```

এখন daily average:

```python
daily_price = (
    price_history_df
    .groupby(["name", "date"])["price"]
    .mean()
    .reset_index()
)

print(daily_price.head())
```

---

# M09.39 — Price Change

একটি product-এর historical price:

```text
100000
98000
95000
92000
```

Pandas-এর `diff()`:

```python
price_history_df["price_change"] = (
    price_history_df
    .sort_values("scraped_at")
    .groupby(["name", "website"])["price"]
    .diff()
)
```

Interpretation:

```text
-2000 → price decreased
+1500 → price increased
0     → no change
```

---

# M09.40 — Percentage Price Change

```python
grouped = (
    price_history_df
    .sort_values("scraped_at")
    .groupby(["name", "website"])
)

price_history_df["previous_price"] = (
    grouped["price"].shift(1)
)
```

তারপর:

```python
price_history_df["price_change_percent"] = (
    (
        price_history_df["price"]
        - price_history_df["previous_price"]
    )
    / price_history_df["previous_price"]
) * 100
```

---

# M09.41 — Biggest Price Drop

```python
biggest_drop = (
    price_history_df
    .sort_values(
        "price_change_percent"
    )
    .head(20)
)

print(biggest_drop)
```

Negative value যত বেশি:

```text
-2%
-5%
-12%
-20%
```

তত বড় price drop।

---

# M09.42 — SQL বনাম Pandas: কোনটা কোথায়?

এটা খুব important concept।

### SQL ভালো যখন:

```text
Filtering
JOIN
Aggregation
Database-level processing
Large datasets
```

Example:

```sql
SELECT
    website_id,
    AVG(price)
FROM price_history
GROUP BY website_id;
```

### Pandas ভালো যখন:

```text
Exploratory Data Analysis
Data cleaning
Statistical analysis
Transformation
Visualization
Machine Learning preparation
```

Example:

```python
df.groupby("website")["price"].mean()
```

---

# M09.43 — SQL + Pandas Together

Professional workflow:

```text
PostgreSQL
     ↓
SQL filtering
     ↓
Relevant dataset
     ↓
Pandas
     ↓
EDA
     ↓
Statistics
     ↓
Visualization
```

❌ পুরো database blindly Pandas-এ load করা ভালো না।

Instead:

```sql
SELECT only_needed_columns
FROM ...
WHERE ...
```

তারপর Pandas।

---

# M09.44 — SQL দিয়ে Filter

ধরো শুধু smartphone:

```python
query = """
SELECT
    p.name,
    w.name AS website,
    c.name AS category,
    ph.price,
    ph.rating
FROM products p
JOIN websites w
    ON p.website_id = w.id
JOIN categories c
    ON p.category_id = c.id
JOIN price_history ph
    ON p.id = ph.product_id
WHERE c.name = 'Smartphone';
"""

df_smartphones = pd.read_sql(
    query,
    engine
)
```

---

# M09.45 — Pandas দিয়ে এরপর Analysis

```python
print(
    df_smartphones
    .groupby("website")["price"]
    .mean()
)
```

অর্থাৎ:

```text
SQL
 ↓
Filter
 ↓
Pandas
 ↓
Analyze
```

---

# M09.46 — Export CSV

```python
df.to_csv(
    "data/exports/products_analysis.csv",
    index=False
)
```

---

# M09.47 — Export Excel

```bash
pip install openpyxl
```

তারপর:

```python
df.to_excel(
    "data/exports/products_analysis.xlsx",
    index=False
)
```

---

# M09.48 — Multiple Sheets Excel Report

এটা real-world analytics project-এ খুব useful।

```python
with pd.ExcelWriter(
    "data/reports/ecommerce_report.xlsx"
) as writer:

    df.to_excel(
        writer,
        sheet_name="Products",
        index=False
    )

    website_price.to_excel(
        writer,
        sheet_name="Website Price"
    )

    category_price.to_excel(
        writer,
        sheet_name="Category Price"
    )

    brand_analysis.to_excel(
        writer,
        sheet_name="Brand Analysis"
    )
```

তাহলে Excel file:

```text
ecommerce_report.xlsx

├── Products
├── Website Price
├── Category Price
└── Brand Analysis
```

---

# M09.49 — Complete Analytics Pipeline

এখন পুরো system:

```text
                 PostgreSQL
                     │
                     ▼
              SQL Query / JOIN
                     │
                     ▼
               Pandas DataFrame
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Cleaning    Filtering   Validation
          │          │          │
          └──────────┼──────────┘
                     ▼
                  Analysis
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   Price Analysis Discount     Rating
        │            │            │
        └────────────┼────────────┘
                     ▼
               Excel / CSV
```

---

# M09.50 — Professional Analytics Script

`analytics/main.py`

```python
import pandas as pd
from sqlalchemy import create_engine


DATABASE_URL = (
    "postgresql+psycopg://"
    "ecommerce_user:your_password@localhost:5432/ecommerce_db"
)

engine = create_engine(DATABASE_URL)


query = """
SELECT
    p.id,
    w.name AS website,
    c.name AS category,
    b.name AS brand,
    p.name,
    ph.price,
    ph.original_price,
    ph.discount,
    ph.rating,
    ph.review_count,
    ph.scraped_at

FROM products p

LEFT JOIN websites w
    ON p.website_id = w.id

LEFT JOIN categories c
    ON p.category_id = c.id

LEFT JOIN brands b
    ON p.brand_id = b.id

LEFT JOIN (
    SELECT DISTINCT ON (product_id)
        product_id,
        price,
        original_price,
        discount,
        rating,
        review_count,
        scraped_at
    FROM price_history
    ORDER BY product_id, scraped_at DESC
) ph
    ON p.id = ph.product_id;
"""


df = pd.read_sql(query, engine)


# -------------------------
# Basic Cleaning
# -------------------------

df = df.drop_duplicates()

df = df.dropna(
    subset=["price"]
)


# -------------------------
# Basic Information
# -------------------------

print("\nDATASET SHAPE")
print(df.shape)

print("\nDATASET INFO")
print(df.info())

print("\nSTATISTICS")
print(df["price"].describe())


# -------------------------
# Website Analysis
# -------------------------

website_analysis = (
    df.groupby("website")
      .agg(
          products=("name", "count"),
          average_price=("price", "mean"),
          minimum_price=("price", "min"),
          maximum_price=("price", "max"),
          average_discount=("discount", "mean"),
          average_rating=("rating", "mean")
      )
      .sort_values(
          "average_price"
      )
)

print("\nWEBSITE ANALYSIS")
print(website_analysis)


# -------------------------
# Category Analysis
# -------------------------

category_analysis = (
    df.groupby("category")
      .agg(
          products=("name", "count"),
          average_price=("price", "mean"),
          average_discount=("discount", "mean"),
          average_rating=("rating", "mean")
      )
      .sort_values(
          "products",
          ascending=False
      )
)

print("\nCATEGORY ANALYSIS")
print(category_analysis)


# -------------------------
# Brand Analysis
# -------------------------

brand_analysis = (
    df.groupby("brand")
      .agg(
          products=("name", "count"),
          average_price=("price", "mean"),
          average_rating=("rating", "mean")
      )
      .sort_values(
          "products",
          ascending=False
      )
)

print("\nBRAND ANALYSIS")
print(brand_analysis.head(20))


# -------------------------
# Cheapest Products
# -------------------------

cheapest = (
    df.sort_values(
        "price"
    )
    .head(20)
)

print("\nCHEAPEST PRODUCTS")
print(
    cheapest[
        ["name", "website", "price"]
    ]
)


# -------------------------
# Highest Discount
# -------------------------

highest_discount = (
    df.sort_values(
        "discount",
        ascending=False
    )
    .head(20)
)

print("\nHIGHEST DISCOUNT")
print(
    highest_discount[
        [
            "name",
            "website",
            "price",
            "discount"
        ]
    ]
)


# -------------------------
# Export
# -------------------------

df.to_csv(
    "data/exports/products.csv",
    index=False
)

with pd.ExcelWriter(
    "data/reports/ecommerce_report.xlsx"
) as writer:

    df.to_excel(
        writer,
        sheet_name="Products",
        index=False
    )

    website_analysis.to_excel(
        writer,
        sheet_name="Websites"
    )

    category_analysis.to_excel(
        writer,
        sheet_name="Categories"
    )

    brand_analysis.to_excel(
        writer,
        sheet_name="Brands"
    )


print("\nAnalysis completed!")
```

---

# 🔥 M09 Mini Project

এখন তোমার practical assignment:

## Project: E-commerce Price Analytics System

তোমার database-এ minimum:

```text
2 Websites
5 Categories
10 Brands
100 Products
```

এবং প্রতিটি product-এর:

```text
price
original_price
discount
rating
review_count
```

থাকবে।

---

## Task 1 — Website Analysis

Calculate:

```text
Total products
Average price
Minimum price
Maximum price
Average discount
Average rating
```

---

## Task 2 — Category Analysis

Find:

```text
Most popular category
Most expensive category
Highest discount category
Highest rated category
```

---

## Task 3 — Brand Analysis

Find:

```text
Top 10 brands by product count
Top 10 brands by rating
Top 10 expensive brands
```

---

## Task 4 — Price Comparison

Find:

```text
Cheapest product
Most expensive product
Average product price
Price spread
Cheapest website
Most expensive website
```

---

## Task 5 — Discount Analysis

Find:

```text
Highest discount
Average discount
Website with highest discount
Category with highest discount
```

---

## Task 6 — Review Analysis

Find:

```text
Most reviewed product
Highest rated product
Average rating
Average review count
```

---

## Task 7 — Historical Analysis

For products having multiple price snapshots:

```text
Initial price
Latest price
Price change
Price change %
Highest price
Lowest price
```

---

# 🧠 M09-এ যে Pandas Concepts অবশ্যই Master করবে

```text
pd.read_sql()
DataFrame
head()
tail()
shape
columns
info()
describe()

isnull()
dropna()
fillna()

drop_duplicates()

loc[]
iloc[]

sort_values()

value_counts()

groupby()

agg()

min()
max()
mean()
median()
sum()
count()

pivot_table()

corr()

pd.to_datetime()

dt.date
dt.year
dt.month

diff()
shift()

to_csv()
to_excel()
ExcelWriter
```

---

# 🏗️ M08 → M09 Architecture

এখন তোমার project অনেক বেশি powerful হয়েছে:

```text
                 E-COMMERCE WEBSITES
                         │
                         ▼
                  SCRAPER SYSTEM
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
          HTML/API             Playwright
              │                     │
              └──────────┬──────────┘
                         ▼
                    CLEANER
                         │
                         ▼
                    VALIDATOR
                         │
                         ▼
                    POSTGRESQL
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
           SQL                    Pandas
             │                       │
             └───────────┬───────────┘
                         ▼
                    ANALYTICS
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Pricing        Discount       Rating
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                    CSV / Excel
```

---

# 🎯 M09 Mastery Checklist

M09 শেষ করার আগে তুমি যেন নিজে করতে পারো:

* [ ] PostgreSQL → Pandas connection
* [ ] `pd.read_sql()`
* [ ] SQL JOIN
* [ ] Latest price extraction
* [ ] DataFrame inspection
* [ ] Missing-value handling
* [ ] Duplicate handling
* [ ] Filtering
* [ ] Sorting
* [ ] GroupBy
* [ ] Aggregation
* [ ] Website analysis
* [ ] Category analysis
* [ ] Brand analysis
* [ ] Discount analysis
* [ ] Rating analysis
* [ ] Review analysis
* [ ] Cheapest seller
* [ ] Price spread
* [ ] Price comparison
* [ ] Price history
* [ ] `diff()`
* [ ] `shift()`
* [ ] Correlation
* [ ] CSV export
* [ ] Excel report generation

### M09-এর core skill

সবচেয়ে গুরুত্বপূর্ণ mental model:

```text
SQL = Data থেকে প্রয়োজনীয় অংশ বের করা

Pandas = Data নিয়ে গভীরভাবে analyze করা

Excel/CSV = Result/report বের করা
```

**M09 শেষ হলে তুমি শুধু scraper না—একজন e-commerce data analyst-এর মতো collected data analyze করতে পারবে।**

পরের ধাপ হবে **M10 — Advanced E-commerce Data Modeling & Product Matching (Entity Resolution)**: একই product বিভিন্ন website-এ আলাদা নাম/brand/model দিয়ে থাকলে কীভাবে identify করে এক product হিসেবে match করা যায়—এটাই price-comparison system-এর সবচেয়ে গুরুত্বপূর্ণ সমস্যাগুলোর একটি।

---
# M10 — Product Matching & Entity Resolution Deep Dive

M09-এ আমরা price analysis, discount analysis, brand/category analysis করেছি। কিন্তু সেখানে একটি **খুব বড় problem** আছে:

ধরো তিনটি website-এ একই product আছে:

```text
Website A:
Apple iPhone 16 128GB Black

Website B:
iPhone 16 - Black - 128 GB

Website C:
Apple iPhone 16 128 GB
```

Pandas যদি শুধু `name` দেখে, তাহলে এগুলোকে **৩টি আলাদা product** মনে করবে।

কিন্তু বাস্তবে:

```text
                SAME PRODUCT
                     │
       ┌─────────────┼─────────────┐
       ▼             ▼             ▼
    Site A         Site B        Site C
    92,000         94,000        89,500
```

তাই একটি professional e-commerce price comparison system-এর জন্য **Product Matching / Entity Resolution** অত্যন্ত গুরুত্বপূর্ণ।

---

# 🎯 M10-এর Main Goal

এই module শেষে তুমি বুঝবে:

* Product identity কী
* Exact matching
* Normalized matching
* Brand + model matching
* SKU/MPN matching
* Fuzzy matching
* Similarity score
* Candidate generation
* Rule-based matching
* Confidence score
* False positive / false negative
* Product master table
* Product variant
* Cross-site product matching
* PostgreSQL-এ matched product store করা

---

# M10.01 — Product Matching আসলে কী?

আমাদের raw data:

```text
Site A
"Apple iPhone 16 128GB Black"

Site B
"iPhone 16 Black 128 GB"

Site C
"APPLE IPHONE 16 128 GB"
```

আমাদের goal:

```text
master_product_id = 101

Site A → 101
Site B → 101
Site C → 101
```

তারপর price comparison করা যাবে:

```text
Master Product 101

Site A → ৳92,000
Site B → ৳94,000
Site C → ৳89,500
```

---

# M10.02 — কেন শুধু Product Name ব্যবহার করা যাবে না?

ধরো:

```text
iPhone 16
iPhone 16 128GB
iPhone 16 256GB
iPhone 16 Pro
iPhone 16 Pro Max
```

এগুলো দেখতে similar হলেও একই product নয়।

আর:

```text
Apple iPhone 16 128GB Black
Apple iPhone 16 128 GB Black
```

দুটো প্রায় একই।

তাই:

```text
String similarity ≠ Product identity
```

এটা M10-এর সবচেয়ে important concept।

---

# M10.03 — Product Identity

একটি product identify করার জন্য আমরা বিভিন্ন attributes ব্যবহার করতে পারি।

```text
Brand
Model
Model Number
SKU
MPN
GTIN / EAN / UPC
Storage
RAM
Color
Size
Variant
```

Example:

```text
Brand       = Apple
Model       = iPhone 16
Storage     = 128GB
Color       = Black
```

এগুলো মিলে একটি variant identity তৈরি হতে পারে।

---

# M10.04 — Strong Identifier বনাম Weak Identifier

সব field-এর গুরুত্ব সমান নয়।

### Strong identifiers

```text
GTIN
EAN
UPC
MPN
Manufacturer Model Number
SKU
```

যদি একই manufacturer product identifier পাওয়া যায়:

```text
MPN = A3287
```

তাহলে matching অনেক সহজ।

---

### Weak identifiers

```text
name
description
price
rating
image
```

এগুলো alone ব্যবহার করে matching করা risky।

---

# M10.05 — Exact Matching

সবচেয়ে সহজ method।

```python
product_a = "Apple iPhone 16 128GB Black"
product_b = "Apple iPhone 16 128GB Black"

if product_a == product_b:
    print("Match")
```

Output:

```text
Match
```

কিন্তু:

```text
Apple iPhone 16 128GB Black
Apple iPhone 16 128 GB Black
```

এখানে:

```python
product_a == product_b
```

হবে:

```text
False
```

যদিও একই product হতে পারে।

---

# M10.06 — Normalization

Matching-এর আগে text normalize করা দরকার।

```python
import re


def normalize_text(text):
    if not text:
        return ""

    text = text.lower()

    text = text.replace("-", " ")
    text = text.replace("_", " ")

    text = re.sub(r"\s+", " ", text)

    return text.strip()
```

Test:

```python
a = "Apple iPhone 16 - 128GB Black"
b = "APPLE IPHONE 16 128GB BLACK"

print(normalize_text(a))
print(normalize_text(b))
```

দুটো হবে:

```text
apple iphone 16 128gb black
apple iphone 16 128gb black
```

এখন:

```python
print(
    normalize_text(a) ==
    normalize_text(b)
)
```

Output:

```text
True
```

---

# M10.07 — Punctuation Remove

আরও robust normalization:

```python
def normalize_text(text):
    if not text:
        return ""

    text = text.lower()

    text = re.sub(
        r"[^a-z0-9]+",
        " ",
        text
    )

    text = re.sub(
        r"\s+",
        " ",
        text
    )

    return text.strip()
```

Example:

```text
"Apple iPhone 16 (128GB) - Black!"
```

→

```text
apple iphone 16 128gb black
```

---

# M10.08 — Unit Normalization

এখানে আরেকটি common problem।

```text
128GB
128 GB
128-gb
128 gb
```

সব একই।

আমরা normalize করতে পারি:

```python
def normalize_storage(text):
    text = text.lower()

    text = re.sub(
        r"(\d+)\s*gb",
        r"\1gb",
        text
    )

    return text
```

Example:

```python
print(
    normalize_storage("128 GB")
)
```

Output:

```text
128gb
```

---

# M10.09 — Color Normalization

Different websites:

```text
Black
black
Midnight Black
Black Color
```

এখানে simple dictionary ব্যবহার করা যায়।

```python
COLOR_MAP = {
    "black color": "black",
    "midnight black": "black",
    "blk": "black",

    "white color": "white",
    "wh": "white",

    "blue color": "blue"
}
```

Function:

```python
def normalize_color(color):
    if not color:
        return None

    color = color.lower().strip()

    return COLOR_MAP.get(
        color,
        color
    )
```

---

# M10.10 — Brand Normalization

ধরো:

```text
Apple
APPLE
apple inc
Apple Inc.
```

একই brand হতে পারে।

```python
BRAND_MAP = {
    "apple inc": "apple",
    "apple inc.": "apple",
    "samsung electronics": "samsung",
    "xiaomi corporation": "xiaomi"
}
```

```python
def normalize_brand(brand):
    if not brand:
        return None

    brand = normalize_text(brand)

    return BRAND_MAP.get(
        brand,
        brand
    )
```

---

# M10.11 — Product Name Normalization

```python
def normalize_product_name(name):
    if not name:
        return ""

    name = name.lower()

    name = re.sub(
        r"[^a-z0-9]+",
        " ",
        name
    )

    name = re.sub(
        r"\s+",
        " ",
        name
    )

    return name.strip()
```

Example:

```text
Apple iPhone 16 - 128 GB Black
```

→

```text
apple iphone 16 128 gb black
```

---

# M10.12 — Tokenization

Product name:

```text
apple iphone 16 128gb black
```

Tokens:

```python
text = "apple iphone 16 128gb black"

tokens = text.split()

print(tokens)
```

Output:

```text
[
    "apple",
    "iphone",
    "16",
    "128gb",
    "black"
]
```

---

# M10.13 — Set-based Matching

দুটি product:

```text
A:
apple iphone 16 128gb black

B:
iphone 16 black 128gb apple
```

Order different হলেও tokens same।

```python
a = set(
    "apple iphone 16 128gb black".split()
)

b = set(
    "iphone 16 black 128gb apple".split()
)

print(a == b)
```

Output:

```text
True
```

---

# M10.14 — Jaccard Similarity

Set similarity-এর জন্য Jaccard similarity useful।

Formula:

```text
J(A,B) = |A ∩ B| / |A ∪ B|
```

Python:

```python
def jaccard_similarity(text_a, text_b):

    a = set(
        normalize_product_name(text_a).split()
    )

    b = set(
        normalize_product_name(text_b).split()
    )

    if not a or not b:
        return 0

    return len(a & b) / len(a | b)
```

Test:

```python
score = jaccard_similarity(
    "Apple iPhone 16 128GB Black",
    "iPhone 16 Black 128GB"
)

print(score)
```

Score 0 থেকে 1-এর মধ্যে হবে।

```text
1.0 → identical token sets
0.0 → no common tokens
```

---

# M10.15 — Fuzzy Matching

এখন যদি:

```text
Apple iPhone 16 128GB Black
Apple Iphone 16 128 GB Blak
```

হয়?

এখানে spelling difference আছে।

Fuzzy matching useful হতে পারে।

Python package:

```bash
pip install rapidfuzz
```

তারপর:

```python
from rapidfuzz.fuzz import ratio
```

```python
score = ratio(
    "apple iphone 16 128gb black",
    "apple iphone 16 128gb blak"
)

print(score)
```

Score:

```text
0 → completely different
100 → identical
```

---

# M10.16 — `token_sort_ratio`

Product title-এর word order আলাদা হলে:

```python
from rapidfuzz.fuzz import token_sort_ratio

score = token_sort_ratio(
    "Apple iPhone 16 128GB Black",
    "Black Apple iPhone 16 128GB"
)

print(score)
```

এটি token order-এর impact কমায়।

---

# M10.17 — `token_set_ratio`

আরও useful:

```python
from rapidfuzz.fuzz import token_set_ratio

score = token_set_ratio(
    "Apple iPhone 16 128GB Black",
    "Apple iPhone 16 Black"
)

print(score)
```

কিন্তু এখানেও একটা danger আছে।

```text
iPhone 16 128GB
iPhone 16 256GB
```

দুটোর similarity অনেক high হতে পারে।

তাই fuzzy score alone দিয়ে product match করা যাবে না।

---

# 🚨 M10.18 — সবচেয়ে গুরুত্বপূর্ণ Rule

**Never do this:**

```python
if similarity > 80:
    match = True
```

কারণ:

```text
iPhone 16 128GB
iPhone 16 256GB
```

similarity খুব বেশি হতে পারে।

কিন্তু এগুলো different variants।

তাই আমাদের **multi-field matching** করতে হবে।

---

# M10.19 — Multi-field Matching

আমরা match score বানাব:

```text
Brand        → 20 points
Model        → 30 points
Storage      → 20 points
RAM          → 10 points
Color        → 10 points
Name          → 10 points

Total        → 100
```

Example:

```text
Brand match       = 20
Model match       = 30
Storage match     = 20
RAM match         = 10
Color match       = 10
Name similarity   = 9

Total = 99
```

তাহলে strong match।

---

# M10.20 — Simple Rule-Based Matcher

```python
def compare_products(a, b):

    score = 0

    if a["brand"] == b["brand"]:
        score += 20

    if a["model"] == b["model"]:
        score += 30

    if a["storage"] == b["storage"]:
        score += 20

    if a["ram"] == b["ram"]:
        score += 10

    if a["color"] == b["color"]:
        score += 10

    name_score = ratio(
        a["name"],
        b["name"]
    )

    score += (
        name_score / 100
    ) * 10

    return score
```

---

# M10.21 — Match Decision

```python
def match_decision(score):

    if score >= 90:
        return "strong_match"

    elif score >= 75:
        return "possible_match"

    else:
        return "no_match"
```

Example:

```python
score = 94

print(
    match_decision(score)
)
```

Output:

```text
strong_match
```

---

# M10.22 — Confidence Score

আমরা শুধু:

```text
match / no match
```

রাখব না।

বরং:

```text
0.00 → 1.00
```

confidence রাখতে পারি।

Example:

```text
0.98 → Very strong
0.91 → Strong
0.82 → Possible
0.65 → Weak
0.30 → No match
```

---

# M10.23 — Three-way Decision

Professional system-এ manual review রাখা ভালো।

```python
def classify_match(score):

    if score >= 90:
        return "MATCH"

    if score >= 75:
        return "REVIEW"

    return "NO_MATCH"
```

Flow:

```text
             Candidate Pair
                   │
                   ▼
             Matching Score
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
      >=90      75–89        <75
        │          │           │
        ▼          ▼           ▼
      MATCH      REVIEW     NO_MATCH
```

এটি অনেক safer।

---

# M10.24 — Candidate Generation

এখানে একটা বড় performance problem আসে।

ধরো:

```text
Site A = 100,000 products
Site B = 100,000 products
```

সব pair compare করলে:

```text
100,000 × 100,000
=
10,000,000,000
```

অর্থাৎ 10 billion comparisons।

এটা inefficient।

তাই আগে **candidate generation / blocking** করতে হবে।

---

# M10.25 — Blocking

ধরো product-এর brand জানা আছে।

আমরা শুধু same brand-এর products compare করব।

```text
Apple ↔ Apple
Samsung ↔ Samsung
Xiaomi ↔ Xiaomi
```

কিন্তু:

```text
Apple ↔ Samsung
```

compare করার দরকার নেই।

এতে candidate count dramatically কমে যায়।

---

# M10.26 — Model-based Blocking

আরও strong blocking:

```text
brand + model
```

Example:

```text
apple + iphone 16
```

তারপর candidate:

```text
Apple iPhone 16 128GB
Apple iPhone 16 256GB
Apple iPhone 16 Black
```

এদের মধ্যে detailed comparison করব।

---

# M10.27 — Variant Matching

এখানে খুব careful হতে হবে।

```text
iPhone 16 128GB Black
iPhone 16 256GB Black
```

Same model হলেও:

```text
Same product family
Different variant
```

আমাদের database-এ আলাদা variant রাখা উচিত।

---

# M10.28 — Product Family বনাম Product Variant

Structure:

```text
Product Family
      │
      └── iPhone 16
             │
       ┌─────┼─────┐
       ▼     ▼     ▼
    128GB  256GB  512GB
```

তারপর color:

```text
128GB
 ├── Black
 ├── White
 └── Blue
```

এটা professional product catalog architecture-এর দিকে নিয়ে যায়।

---

# M10.29 — Database Design

M08-এর `products` table-এর সাথে আমরা একটি master product concept যোগ করতে পারি।

### `master_products`

```sql
CREATE TABLE master_products (
    id BIGSERIAL PRIMARY KEY,

    brand VARCHAR(100),

    model VARCHAR(255),

    canonical_name TEXT,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

তারপর existing product:

```sql
ALTER TABLE products
ADD COLUMN master_product_id BIGINT
REFERENCES master_products(id);
```

এখন:

```text
master_products
       │
       │ 1:N
       ▼
   products
       │
       ▼
 price_history
```

---

# M10.30 — Cross-site Mapping

ধরো:

```text
master_products

id = 101
canonical_name = Apple iPhone 16 128GB Black
```

তার নিচে:

```text
products

Site A → product id 5001 → master 101
Site B → product id 7204 → master 101
Site C → product id 9312 → master 101
```

এখন price comparison সহজ:

```sql
SELECT
    mp.canonical_name,
    w.name AS website,
    ph.price
FROM products p

JOIN master_products mp
    ON p.master_product_id = mp.id

JOIN websites w
    ON p.website_id = w.id

JOIN price_history ph
    ON ph.product_id = p.id;
```

---

# M10.31 — Matching Table আলাদাও রাখা যায়

আরও flexible design:

```sql
CREATE TABLE product_matches (
    id BIGSERIAL PRIMARY KEY,

    product_id_a BIGINT NOT NULL
        REFERENCES products(id),

    product_id_b BIGINT NOT NULL
        REFERENCES products(id),

    similarity_score NUMERIC(5,2),

    match_status VARCHAR(30),

    matching_method VARCHAR(50),

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Example:

```text
product A
product B
score = 96.5
status = MATCH
method = brand_model_variant
```

---

# M10.32 — Matching Pipeline

Professional architecture:

```text
Raw Products
     │
     ▼
Normalize Text
     │
     ▼
Extract Attributes
     │
     ▼
Generate Candidates
     │
     ▼
Compare Fields
     │
     ▼
Calculate Score
     │
     ▼
Decision
     │
 ┌───┼────────┐
 ▼   ▼        ▼
Match Review No Match
```

---

# M10.33 — Attribute Extraction

Product name:

```text
Apple iPhone 16 128GB Black
```

আমরা extract করতে চাই:

```python
{
    "brand": "apple",
    "model": "iphone 16",
    "storage": "128gb",
    "color": "black"
}
```

Simple storage extractor:

```python
import re


def extract_storage(text):

    match = re.search(
        r"(\d+)\s*(gb|tb)",
        text.lower()
    )

    if match:
        return (
            match.group(1)
            + match.group(2)
        )

    return None
```

Test:

```python
print(
    extract_storage(
        "Apple iPhone 16 128 GB Black"
    )
)
```

Output:

```text
128gb
```

---

# M10.34 — RAM Extractor

```python
def extract_ram(text):

    match = re.search(
        r"(\d+)\s*gb\s*ram",
        text.lower()
    )

    if match:
        return match.group(1) + "gb"

    return None
```

Example:

```text
Samsung Galaxy S25 12GB RAM
```

→

```text
12gb
```

---

# M10.35 — Model Number

ধরো:

```text
Samsung Galaxy S25 SM-S931B
```

`SM-S931B` হচ্ছে useful identifier।

যদি দুই website-এ:

```text
SM-S931B
```

same পাওয়া যায়, তাহলে strong evidence।

---

# M10.36 — Exact Identifier Priority

Matching priority হতে পারে:

```text
1. GTIN/EAN/UPC
        ↓
2. MPN / Model Number
        ↓
3. SKU
        ↓
4. Brand + Model + Variant
        ↓
5. Fuzzy Text Matching
```

অর্থাৎ fuzzy matching আমাদের **শেষের দিকে** ব্যবহার করা উচিত।

---

# M10.37 — Match Rules

Example:

### Rule 1

```text
EAN same
```

→ Strong Match

### Rule 2

```text
Brand same
Model Number same
```

→ Strong Match

### Rule 3

```text
Brand same
Model same
Storage same
Color same
```

→ Strong Match

### Rule 4

```text
Brand same
Model similar
Storage unknown
```

→ Review

### Rule 5

```text
Only name similarity high
```

→ Don't automatically match

---

# M10.38 — False Positive

False positive:

```text
System says MATCH
but actually different products.
```

Example:

```text
iPhone 16 128GB
iPhone 16 256GB
```

যদি system incorrectly match করে:

```text
FALSE POSITIVE
```

E-commerce price comparison-এর জন্য এটা dangerous।

---

# M10.39 — False Negative

False negative:

```text
System says NO_MATCH
but actually same product.
```

Example:

```text
Apple iPhone 16 128GB Black

Apple Iphone16 128 Gb Midnight Black
```

System আলাদা করে দিল।

এটা:

```text
FALSE NEGATIVE
```

---

# M10.40 — Precision বনাম Recall

Matching system evaluate করতে:

### Precision

আমরা যেগুলো match বলেছি:

```text
কতগুলো সত্যিই correct?
```

Formula:

```text
Precision =
True Positive /
(True Positive + False Positive)
```

### Recall

যেসব সত্যিকারের match ছিল:

```text
তার কতগুলো আমরা খুঁজে পেয়েছি?
```

Formula:

```text
Recall =
True Positive /
(True Positive + False Negative)
```

---

# M10.41 — কেন Precision Important?

Price comparison system-এ ভুল product merge করলে:

```text
Product A = 128GB
Product B = 256GB
```

এক করে ফেললে user ভুল price comparison দেখতে পারে।

তাই automatic matching-এ:

```text
High precision
```

খুব important।

---

# M10.42 — Pandas Matching Example

ধরো:

```python
import pandas as pd

data = {
    "website": [
        "Site A",
        "Site B",
        "Site C"
    ],

    "name": [
        "Apple iPhone 16 128GB Black",
        "iPhone 16 Black 128 GB",
        "Apple iPhone 16 256GB Black"
    ]
}

df = pd.DataFrame(data)

print(df)
```

Normalize:

```python
df["normalized_name"] = (
    df["name"]
    .apply(normalize_product_name)
)
```

---

# M10.43 — Grouping Candidate Products

```python
df["brand"] = "apple"
```

তারপর:

```python
groups = df.groupby("brand")
```

এখন একই brand-এর মধ্যে matching করা যাবে।

---

# M10.44 — Pairwise Comparison

```python
from itertools import combinations

for a, b in combinations(
    df.to_dict("records"),
    2
):

    score = ratio(
        a["normalized_name"],
        b["normalized_name"]
    )

    print(
        a["name"],
        "<->",
        b["name"],
        score
    )
```

এখানে প্রতিটি pair compare হচ্ছে।

---

# M10.45 — Practical Matcher

```python
from rapidfuzz.fuzz import token_set_ratio


def product_similarity(name_a, name_b):

    a = normalize_product_name(name_a)
    b = normalize_product_name(name_b)

    return token_set_ratio(a, b)
```

Decision:

```python
def match_products(name_a, name_b):

    score = product_similarity(
        name_a,
        name_b
    )

    if score >= 95:
        return score, "MATCH"

    elif score >= 80:
        return score, "REVIEW"

    else:
        return score, "NO_MATCH"
```

**Note:** 95/80 এখানে universal threshold নয়। নিজের labelled dataset দিয়ে threshold validate করতে হবে।

---

# M10.46 — Better Matcher

শুধু name না:

```python
def compare_products(a, b):

    score = 0

    if a["brand"] and b["brand"]:
        if a["brand"] == b["brand"]:
            score += 20

    if a["model"] and b["model"]:
        if a["model"] == b["model"]:
            score += 30

    if a["storage"] and b["storage"]:
        if a["storage"] == b["storage"]:
            score += 20
        else:
            return 0, "NO_MATCH"

    if a["color"] and b["color"]:
        if a["color"] == b["color"]:
            score += 10

    name_score = token_set_ratio(
        a["name"],
        b["name"]
    )

    score += (
        name_score * 0.20
    )

    if score >= 90:
        status = "MATCH"

    elif score >= 70:
        status = "REVIEW"

    else:
        status = "NO_MATCH"

    return score, status
```

এখানে একটা important design:

```python
if storage_a != storage_b:
    return 0, "NO_MATCH"
```

কারণ variant mismatch অনেক সময় hard conflict।

---

# M10.47 — Missing Attribute Problem

ধরো:

```text
Product A:
iPhone 16 128GB

Product B:
iPhone 16
```

Product B-তে storage missing।

তাহলে:

```text
Unknown ≠ Different
```

এটা খুব important।

আমরা বলতে পারি না:

```text
B = 256GB
```

তাই:

```python
if storage_a is None or storage_b is None:
    # uncertain
```

এক্ষেত্রে:

```text
REVIEW
```

হতে পারে।

---

# M10.48 — Product Matching-এর Golden Rule

মনে রাখবে:

```text
Same name
      ≠
Same product
```

এবং:

```text
Different name
      ≠
Different product
```

Product matching হচ্ছে:

```text
Identity + Attributes + Evidence
```

---

# M10.49 — Canonical Product

Matching হওয়ার পরে আমরা একটি canonical name রাখতে পারি।

Example:

```text
Canonical:
Apple iPhone 16 128GB Black
```

Website-specific:

```text
Site A:
Apple iPhone 16 128GB Black Smartphone

Site B:
iPhone 16 Black 128 GB

Site C:
Apple iPhone 16 128 GB Black
```

সবগুলো:

```text
master_product_id = 101
```

---

# M10.50 — Final Database Architecture

M08 + M09 + M10 মিলিয়ে:

```text
                 websites
                    │
                    ▼
                 products
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
 master_product          product attributes
          │
          ▼
   price_history
```

আর matching:

```text
Site A Product ─┐
                │
Site B Product ─┼──→ Master Product
                │
Site C Product ─┘
```

---

# 🔥 M10 Mini Project

এখন তোমার practical project:

## Dataset

কমপক্ষে:

```text
Site A → 100 products
Site B → 100 products
Site C → 100 products
```

এর মধ্যে intentionally কিছু duplicate রাখবে:

```text
Apple iPhone 16 128GB Black
iPhone 16 Black 128 GB
APPLE IPHONE 16 128GB BLACK
```

এবং কিছু variants:

```text
iPhone 16 128GB
iPhone 16 256GB
```

---

## Step 1 — Normalize

প্রতিটি product-এর:

```text
name
brand
model
storage
RAM
color
```

normalize করবে।

---

## Step 2 — Candidate Generation

প্রথমে:

```text
same brand
```

তারপর:

```text
same/similar model
```

তারপর detailed matching।

---

## Step 3 — Similarity

Calculate:

```text
Name similarity
Brand match
Model match
Storage match
RAM match
Color match
```

---

## Step 4 — Match Score

Output:

```text
product_a
product_b
score
status
```

Example:

| Product A        | Product B           | Score | Status   |
| ---------------- | ------------------- | ----: | -------- |
| iPhone 16 128GB  | iPhone 16 128 GB    |    98 | MATCH    |
| iPhone 16 128GB  | iPhone 16 256GB     |    20 | NO_MATCH |
| Galaxy S25 Black | Galaxy S25 Midnight |    82 | REVIEW   |

---

## Step 5 — PostgreSQL

Matched products:

```text
master_products
```

এবং:

```text
products.master_product_id
```

update করবে।

---

# 🧠 M10 Mastery Checklist

M10 শেষ করার আগে তুমি যেন বুঝতে পারো:

* [ ] Product identity
* [ ] Exact matching
* [ ] Text normalization
* [ ] Tokenization
* [ ] Brand normalization
* [ ] Unit normalization
* [ ] Variant handling
* [ ] Jaccard similarity
* [ ] Fuzzy matching
* [ ] RapidFuzz
* [ ] Token similarity
* [ ] Multi-field matching
* [ ] Weighted score
* [ ] Confidence score
* [ ] Candidate generation
* [ ] Blocking
* [ ] False positive
* [ ] False negative
* [ ] Precision
* [ ] Recall
* [ ] Manual review
* [ ] Canonical product
* [ ] Master product
* [ ] Product variant
* [ ] PostgreSQL mapping

---

# 🚀 M08 → M10 পর্যন্ত তোমার System

```text
                    E-COMMERCE
                        │
                        ▼
                    SCRAPING
                        │
             ┌──────────┼──────────┐
             ▼          ▼          ▼
          Requests   API       Playwright
             │          │          │
             └──────────┼──────────┘
                        ▼
                     PARSER
                        │
                        ▼
                    CLEANER
                        │
                        ▼
                   PostgreSQL
                        │
                        ▼
                      SQL
                        │
                        ▼
                     Pandas
                        │
                        ▼
                  EDA / ANALYSIS
                        │
                        ▼
              PRODUCT MATCHING
                        │
             ┌──────────┼──────────┐
             ▼          ▼          ▼
           MATCH      REVIEW    NO MATCH
             │
             ▼
        MASTER PRODUCT
             │
             ▼
        PRICE COMPARISON
```

### M10-এর সবচেয়ে গুরুত্বপূর্ণ takeaway

**M09 আমাদের শিখিয়েছে “data কীভাবে analyze করতে হয়।”**

**M10 শেখাচ্ছে “different websites-এর data কীভাবে একই real-world product-এর সাথে connect করতে হয়।”**

এই দুইটি skill একসাথে হলে তুমি একটি basic scraper-এর বদলে **real e-commerce price intelligence / price comparison data pipeline** তৈরি করার পর্যায়ে চলে যাচ্ছ।

পরের logical step হবে **M11 — Advanced E-commerce Data Cleaning & Feature Engineering**, যেখানে এই matched product data থেকে `price_difference`, `discount_percentage`, `price_rank`, `rating_score`, `review_score`, `deal_score`, `competitiveness_score` ইত্যাদি তৈরি করে analytics/ML-ready dataset বানানো হবে।


----
# M11 — Advanced E-commerce Data Cleaning & Feature Engineering

M10-এ আমরা **Product Matching / Entity Resolution** করেছি। এখন matched product data থেকে এমন **useful numerical features** তৈরি করব যেগুলো দিয়ে:

* Price comparison
* Deal detection
* Seller ranking
* Product ranking
* Business analytics
* Dashboard
* Machine Learning

সব করা যাবে।

আমাদের flow:

```text
PostgreSQL
    ↓
Matched Products
    ↓
Data Cleaning
    ↓
Feature Engineering
    ↓
Business Metrics
    ↓
Analytics Dataset
    ↓
Dashboard / ML
```

---

# 🎯 M11-এর Main Goal

এই module শেষে একটি product-এর জন্য আমরা এমন dataset তৈরি করতে পারব:

```text
product
brand
category
website
price
original_price
discount
rating
review_count

        ↓ Feature Engineering

discount_amount
discount_percent
price_rank
website_avg_price
price_difference
price_difference_percent
cheapest_price
highest_price
seller_count
rating_score
review_score
deal_score
competitiveness_score
```

---

# M11.01 — Feature Engineering কী?

Feature engineering হলো raw data থেকে **analysis বা ML-এর জন্য useful নতুন variables/features তৈরি করা**।

ধরো raw data:

```text
price = 90,000
original_price = 100,000
rating = 4.7
review_count = 5000
```

আমরা বের করতে পারি:

```text
discount_amount = 10,000
discount_percent = 10%
```

আর যদি একই product অন্য website-এ:

```text
Site A = 90,000
Site B = 95,000
Site C = 85,000
```

তাহলে:

```text
cheapest_price = 85,000
highest_price = 95,000
price_spread = 10,000
```

এগুলোই engineered features।

---

# M11.02 — Raw Dataset Load

M10-এর matched dataset ধরে নিচ্ছি।

```python
import pandas as pd
from sqlalchemy import create_engine


DATABASE_URL = (
    "postgresql+psycopg://"
    "ecommerce_user:your_password@localhost:5432/ecommerce_db"
)

engine = create_engine(DATABASE_URL)
```

Query:

```python
query = """
SELECT
    p.id,
    p.master_product_id,
    w.name AS website,
    c.name AS category,
    b.name AS brand,
    p.name,
    ph.price,
    ph.original_price,
    ph.discount,
    ph.rating,
    ph.review_count,
    ph.scraped_at
FROM products p

LEFT JOIN websites w
    ON p.website_id = w.id

LEFT JOIN categories c
    ON p.category_id = c.id

LEFT JOIN brands b
    ON p.brand_id = b.id

LEFT JOIN (
    SELECT DISTINCT ON (product_id)
        product_id,
        price,
        original_price,
        discount,
        rating,
        review_count,
        scraped_at
    FROM price_history
    ORDER BY product_id, scraped_at DESC
) ph
    ON p.id = ph.product_id;
"""

df = pd.read_sql(query, engine)
```

---

# M11.03 — Basic Cleaning

প্রথমে column names:

```python
df.columns = (
    df.columns
      .str.lower()
      .str.strip()
      .str.replace(" ", "_")
)
```

Numeric columns:

```python
numeric_columns = [
    "price",
    "original_price",
    "discount",
    "rating",
    "review_count"
]

for column in numeric_columns:
    df[column] = pd.to_numeric(
        df[column],
        errors="coerce"
    )
```

---

# M11.04 — Remove Impossible Values

Price:

```python
df.loc[
    df["price"] <= 0,
    "price"
] = pd.NA
```

Rating:

```python
df.loc[
    (df["rating"] < 0) |
    (df["rating"] > 5),
    "rating"
] = pd.NA
```

Discount:

```python
df.loc[
    (df["discount"] < 0) |
    (df["discount"] > 100),
    "discount"
] = pd.NA
```

Review count:

```python
df.loc[
    df["review_count"] < 0,
    "review_count"
] = pd.NA
```

---

# M11.05 — Price vs Original Price Validation

ধরো:

```text
price = 90,000
original_price = 100,000
```

ঠিক।

কিন্তু:

```text
price = 100,000
original_price = 90,000
```

এখানে সমস্যা।

```python
invalid_price = (
    df["original_price"].notna() &
    (df["price"] > df["original_price"])
)

print(
    df[invalid_price]
)
```

এই ধরনের records investigate করতে হবে।

---

# M11.06 — Discount Amount

Formula:

```text
discount_amount
=
original_price - price
```

Python:

```python
df["discount_amount"] = (
    df["original_price"]
    - df["price"]
)
```

Example:

```text
Original = 100,000
Price    = 90,000

Discount amount = 10,000
```

---

# M11.07 — Discount Percentage

Formula:

```text
Discount %
=
(original_price - price)
/
original_price
× 100
```

Python:

```python
df["discount_percent"] = (
    (
        df["original_price"]
        - df["price"]
    )
    / df["original_price"]
) * 100
```

---

# M11.08 — Avoid Division by Zero

Always protect the denominator.

```python
df["discount_percent"] = (
    (
        df["original_price"] - df["price"]
    )
    / df["original_price"].replace(0, pd.NA)
) * 100
```

তারপর:

```python
df["discount_percent"] = (
    df["discount_percent"]
    .clip(0, 100)
)
```

---

# M11.09 — Existing Discount vs Calculated Discount

ধরো website বলছে:

```text
discount = 15%
```

কিন্তু calculation:

```text
original = 100,000
price = 90,000

calculated = 10%
```

দুটো conflict করছে।

আমরা দুটো column রাখব:

```python
df["reported_discount"] = df["discount"]

df["calculated_discount"] = (
    (
        df["original_price"]
        - df["price"]
    )
    / df["original_price"].replace(0, pd.NA)
) * 100
```

তারপর difference:

```python
df["discount_difference"] = (
    df["reported_discount"]
    - df["calculated_discount"]
)
```

এতে data quality issue detect করা যায়।

---

# M11.10 — Price Rank

প্রতিটি master product-এর seller price rank করতে চাই।

```python
df["price_rank"] = (
    df.groupby("master_product_id")["price"]
      .rank(
          method="dense",
          ascending=True
      )
)
```

Example:

```text
Product X

Site A → 90,000 → Rank 2
Site B → 85,000 → Rank 1
Site C → 95,000 → Rank 3
```

---

# M11.11 — Cheapest Price

```python
df["cheapest_price"] = (
    df.groupby("master_product_id")["price"]
      .transform("min")
)
```

এখন প্রতিটি row জানবে:

```text
এই product-এর cheapest available price কত?
```

---

# M11.12 — Highest Price

```python
df["highest_price"] = (
    df.groupby("master_product_id")["price"]
      .transform("max")
)
```

---

# M11.13 — Average Market Price

```python
df["average_market_price"] = (
    df.groupby("master_product_id")["price"]
      .transform("mean")
)
```

Example:

```text
Site A = 90,000
Site B = 95,000
Site C = 85,000

Average = 90,000
```

---

# M11.14 — Price Spread

Formula:

```text
highest_price - cheapest_price
```

```python
df["price_spread"] = (
    df["highest_price"]
    - df["cheapest_price"]
)
```

---

# M11.15 — Price Difference from Cheapest

```python
df["difference_from_cheapest"] = (
    df["price"]
    - df["cheapest_price"]
)
```

Example:

```text
Site A = 90,000
Cheapest = 85,000

Difference = 5,000
```

---

# M11.16 — Difference Percentage

```python
df["difference_from_cheapest_percent"] = (
    (
        df["price"]
        - df["cheapest_price"]
    )
    / df["cheapest_price"]
) * 100
```

Example:

```text
Cheapest = 85,000
Current = 90,000

Difference = 5,000

Percentage ≈ 5.88%
```

---

# M11.17 — Cheapest Seller Flag

```python
df["is_cheapest"] = (
    df["price"] ==
    df["cheapest_price"]
)
```

Output:

```text
True
False
False
```

আরও useful:

```python
df["is_cheapest"] = (
    df["price"] ==
    df["cheapest_price"]
).astype(int)
```

তাহলে:

```text
1 = cheapest
0 = not cheapest
```

---

# M11.18 — Seller Count

একটি product কত website-এ available?

```python
df["seller_count"] = (
    df.groupby("master_product_id")["website"]
      .transform("nunique")
)
```

Example:

```text
iPhone 16

Site A
Site B
Site C

seller_count = 3
```

---

# M11.19 — Market Competition

Seller count থেকে simple competition level:

```python
def competition_level(count):

    if count >= 5:
        return "high"

    elif count >= 3:
        return "medium"

    return "low"
```

Apply:

```python
df["competition_level"] = (
    df["seller_count"]
    .apply(competition_level)
)
```

---

# M11.20 — Price Position

একটি seller market-এর কোথায় আছে সেটা বের করতে পারি।

```python
df["price_position"] = (
    (
        df["price"]
        - df["cheapest_price"]
    )
    / (
        df["highest_price"]
        - df["cheapest_price"]
    )
)
```

Interpretation:

```text
0 → cheapest
1 → most expensive
```

কিন্তু cheapest = highest হলে division by zero হতে পারে। তাই robust version:

```python
spread = (
    df["highest_price"]
    - df["cheapest_price"]
)

df["price_position"] = (
    (df["price"] - df["cheapest_price"])
    / spread.replace(0, pd.NA)
)
```

---

# M11.21 — Rating Score

Raw rating:

```text
4.8
```

কে 0–1 scale-এ আনতে পারি:

```python
df["rating_score"] = (
    df["rating"] / 5
)
```

Example:

```text
5.0 → 1.00
4.5 → 0.90
4.0 → 0.80
```

---

# M11.22 — Review Count Transformation

Review count অনেক skewed হতে পারে।

Example:

```text
2
10
100
1,000
100,000
```

তাই log transformation useful:

```python
import numpy as np

df["review_score_raw"] = np.log1p(
    df["review_count"].fillna(0)
)
```

`log1p(x)` ব্যবহার করছি যাতে:

```text
log1p(0)
```

valid থাকে।

---

# M11.23 — Review Score Normalize

Min-Max normalization:

```python
min_review = df["review_score_raw"].min()
max_review = df["review_score_raw"].max()

df["review_score"] = (
    (
        df["review_score_raw"]
        - min_review
    )
    / (
        max_review
        - min_review
    )
)
```

Result:

```text
0 → lowest review signal
1 → highest review signal
```

---

# M11.24 — Weighted Rating Score

শুধু rating দেখে product quality বিচার করা risky।

ধরো:

```text
Product A
rating = 5.0
reviews = 2
```

এবং:

```text
Product B
rating = 4.8
reviews = 20,000
```

তাই rating + review volume combine করা যায়।

Simple weighted score:

```python
df["quality_score"] = (
    0.7 * df["rating_score"].fillna(0)
    +
    0.3 * df["review_score"].fillna(0)
)
```

এটি একটি **business-defined heuristic**, universal formula নয়।

---

# M11.25 — Discount Score

Discount percentage normalize করতে পারি:

```python
df["discount_score"] = (
    df["discount_percent"]
    .clip(0, 100)
    / 100
)
```

Example:

```text
10% → 0.10
25% → 0.25
50% → 0.50
```

---

# M11.26 — Price Score

যেহেতু lower price সাধারণত better deal:

```python
df["price_score"] = (
    1 -
    df["price_position"]
)
```

Example:

```text
cheapest → 1.0
middle   → 0.5
highest  → 0.0
```

---

# M11.27 — Deal Score

এখন আমরা একটি simple deal score তৈরি করতে পারি।

ধরি:

```text
Price Score       = 50%
Discount Score    = 25%
Quality Score     = 25%
```

```python
df["deal_score"] = (
    0.50 * df["price_score"].fillna(0)
    +
    0.25 * df["discount_score"].fillna(0)
    +
    0.25 * df["quality_score"].fillna(0)
)
```

তারপর:

```python
df = df.sort_values(
    "deal_score",
    ascending=False
)
```

---

# M11.28 — কেন Deal Score দরকার?

ধরো:

### Product A

```text
Price       = 90,000
Discount    = 20%
Rating      = 4.8
Reviews     = 10,000
```

### Product B

```text
Price       = 85,000
Discount    = 5%
Rating      = 4.2
Reviews     = 200
```

শুধু:

```text
lowest price
```

দেখলে B winner।

শুধু:

```text
highest discount
```

দেখলে A winner।

কিন্তু:

```text
Price
+
Discount
+
Quality
+
Reviews
```

combine করলে more useful ranking পাওয়া যায়।

---

# M11.29 — Competitiveness Score

এটা seller-এর জন্য useful।

ধরো seller-এর price:

```text
cheapest = 90,000
current = 92,000
highest = 100,000
```

Seller market-এর relatively competitive।

আমরা:

```python
df["competitiveness_score"] = (
    1 -
    df["price_position"]
)
```

এর সাথে rating যোগ করতে পারি:

```python
df["competitiveness_score"] = (
    0.7 * df["price_score"].fillna(0)
    +
    0.3 * df["rating_score"].fillna(0)
)
```

---

# M11.30 — Price Bucket

Analytics-এর জন্য price range বানানো useful।

```python
bins = [
    0,
    1000,
    5000,
    10000,
    25000,
    50000,
    100000,
    float("inf")
]

labels = [
    "<1K",
    "1K-5K",
    "5K-10K",
    "10K-25K",
    "25K-50K",
    "50K-100K",
    "100K+"
]

df["price_bucket"] = pd.cut(
    df["price"],
    bins=bins,
    labels=labels,
    right=False
)
```

তারপর:

```python
print(
    df["price_bucket"]
    .value_counts()
    .sort_index()
)
```

---

# M11.31 — Discount Bucket

```python
discount_bins = [
    -1,
    0,
    10,
    20,
    30,
    50,
    100
]

discount_labels = [
    "No Discount",
    "1-10%",
    "10-20%",
    "20-30%",
    "30-50%",
    "50%+"
]

df["discount_bucket"] = pd.cut(
    df["discount_percent"],
    bins=discount_bins,
    labels=discount_labels
)
```

---

# M11.32 — Rating Bucket

```python
rating_bins = [
    0,
    2,
    3,
    4,
    4.5,
    5.01
]

rating_labels = [
    "Poor",
    "Below Average",
    "Average",
    "Good",
    "Excellent"
]

df["rating_bucket"] = pd.cut(
    df["rating"],
    bins=rating_bins,
    labels=rating_labels
)
```

---

# M11.33 — Availability Feature

ধরো:

```text
in_stock
out_of_stock
unknown
```

One-hot encoding:

```python
availability_encoded = pd.get_dummies(
    df["availability"],
    prefix="availability"
)
```

Result:

```text
availability_in_stock
availability_out_of_stock
availability_unknown
```

---

# M11.34 — Website Encoding

Machine Learning-এর জন্য categorical data encode করতে হয়।

```python
website_encoded = pd.get_dummies(
    df["website"],
    prefix="website"
)
```

কিন্তু analytics-এর জন্য সবসময় encoding দরকার নেই।

এটা মনে রাখবে:

```text
Analytics ≠ Machine Learning
```

---

# M11.35 — Category Encoding

ML-এর জন্য:

```python
category_encoded = pd.get_dummies(
    df["category"],
    prefix="category"
)
```

কিন্তু category analysis করতে:

```python
df.groupby("category")
```

যথেষ্ট।

---

# M11.36 — Log Price

Price distribution অনেক সময় right-skewed হয়।

```python
df["log_price"] = np.log1p(
    df["price"]
)
```

এটা পরে:

* ML
* statistical modeling
* visualization

এ কাজে লাগতে পারে।

---

# M11.37 — Price Change Feature

M09-এর historical data থেকে:

```python
history = price_history_df.copy()

history["scraped_at"] = pd.to_datetime(
    history["scraped_at"]
)

history = history.sort_values(
    ["name", "website", "scraped_at"]
)
```

Previous price:

```python
history["previous_price"] = (
    history
    .groupby(["name", "website"])["price"]
    .shift(1)
)
```

Price change:

```python
history["price_change"] = (
    history["price"]
    - history["previous_price"]
)
```

---

# M11.38 — Price Change Percentage

```python
history["price_change_percent"] = (
    (
        history["price"]
        - history["previous_price"]
    )
    /
    history["previous_price"]
        .replace(0, pd.NA)
) * 100
```

এখন:

```text
+5% → price increased
-10% → price decreased
0% → unchanged
```

---

# M11.39 — Price Trend Feature

শেষ কয়েকটি observations দেখে simple trend তৈরি করা যায়।

```python
def price_trend(value):

    if pd.isna(value):
        return "unknown"

    if value > 0:
        return "increasing"

    if value < 0:
        return "decreasing"

    return "stable"
```

```python
history["price_trend"] = (
    history["price_change_percent"]
    .apply(price_trend)
)
```

---

# M11.40 — Data Quality Features

Feature engineering শুধু business features নয়।

আমরা data quality features-ও রাখতে পারি।

```python
df["has_rating"] = (
    df["rating"].notna()
).astype(int)

df["has_discount"] = (
    df["discount_percent"].notna()
).astype(int)

df["has_original_price"] = (
    df["original_price"].notna()
).astype(int)

df["has_reviews"] = (
    df["review_count"].notna()
).astype(int)
```

---

# M11.41 — Data Completeness Score

```python
quality_columns = [
    "price",
    "original_price",
    "discount_percent",
    "rating",
    "review_count"
]

df["data_completeness"] = (
    df[quality_columns]
    .notna()
    .mean(axis=1)
)
```

Example:

```text
1.0 → all fields available
0.8 → 80% fields available
0.4 → poor completeness
```

---

# M11.42 — Outlier Detection

Price:

```python
Q1 = df["price"].quantile(0.25)
Q3 = df["price"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

Outliers:

```python
outliers = df[
    (df["price"] < lower) |
    (df["price"] > upper)
]

print(outliers)
```

---

# M11.43 — কিন্তু Outlier মানেই ভুল নয়

এটা খুব important।

ধরো:

```text
iPhone = 100,000
MacBook = 250,000
```

MacBook-এর price অনেক বেশি।

কিন্তু সেটা ভুল data নাও হতে পারে।

তাই:

```text
Outlier ≠ Error
```

Outlier হলো:

> Data point that is unusual compared with the distribution.

তারপর investigate করতে হবে।

---

# M11.44 — Product-level Feature Dataset

আমাদের seller-level dataset:

```text
master_product_id
website
price
rating
discount
```

থেকে product-level summary বানাতে পারি।

```python
product_features = (
    df.groupby("master_product_id")
      .agg(
          cheapest_price=("price", "min"),
          highest_price=("price", "max"),
          average_price=("price", "mean"),
          seller_count=("website", "nunique"),
          average_rating=("rating", "mean"),
          average_discount=("discount_percent", "mean"),
          max_discount=("discount_percent", "max"),
          total_reviews=("review_count", "sum")
      )
      .reset_index()
)
```

এটা অনেক powerful dataset।

---

# M11.45 — Seller-level Dataset

Seller perspective:

```python
seller_features = (
    df.groupby("website")
      .agg(
          product_count=("master_product_id", "nunique"),
          average_price=("price", "mean"),
          average_discount=("discount_percent", "mean"),
          average_rating=("rating", "mean"),
          cheapest_products=("is_cheapest", "sum")
      )
      .reset_index()
)
```

এখন seller comparison:

```text
Website
Product count
Average price
Average discount
Average rating
Number of cheapest products
```

---

# M11.46 — Category-level Features

```python
category_features = (
    df.groupby("category")
      .agg(
          product_count=("master_product_id", "nunique"),
          average_price=("price", "mean"),
          average_discount=("discount_percent", "mean"),
          average_rating=("rating", "mean"),
          average_reviews=("review_count", "mean")
      )
      .reset_index()
)
```

এটা dashboard-এর জন্য useful।

---

# M11.47 — Brand-level Features

```python
brand_features = (
    df.groupby("brand")
      .agg(
          product_count=("master_product_id", "nunique"),
          average_price=("price", "mean"),
          average_discount=("discount_percent", "mean"),
          average_rating=("rating", "mean"),
          total_reviews=("review_count", "sum")
      )
      .reset_index()
)
```

---

# M11.48 — Final Feature Dataset

আমাদের final row হতে পারে:

```text
master_product_id
website
brand
category
price
original_price
discount_percent
discount_amount
rating
review_count

cheapest_price
highest_price
average_market_price
price_spread
difference_from_cheapest
difference_from_cheapest_percent

seller_count
price_rank
is_cheapest
price_position

rating_score
review_score
quality_score
discount_score
price_score
deal_score
competitiveness_score

price_bucket
discount_bucket
rating_bucket

data_completeness
```

এটা এখন অনেকটা **analytics-ready dataset**।

---

# M11.49 — Complete Feature Engineering Function

একটি reusable function বানাই:

```python
def create_features(df):

    df = df.copy()

    # -----------------
    # Discount
    # -----------------

    df["discount_amount"] = (
        df["original_price"]
        - df["price"]
    )

    df["discount_percent"] = (
        (
            df["original_price"]
            - df["price"]
        )
        /
        df["original_price"]
            .replace(0, pd.NA)
    ) * 100

    df["discount_percent"] = (
        df["discount_percent"]
        .clip(0, 100)
    )

    # -----------------
    # Market Prices
    # -----------------

    df["cheapest_price"] = (
        df.groupby("master_product_id")["price"]
          .transform("min")
    )

    df["highest_price"] = (
        df.groupby("master_product_id")["price"]
          .transform("max")
    )

    df["average_market_price"] = (
        df.groupby("master_product_id")["price"]
          .transform("mean")
    )

    # -----------------
    # Price Features
    # -----------------

    df["price_spread"] = (
        df["highest_price"]
        - df["cheapest_price"]
    )

    df["difference_from_cheapest"] = (
        df["price"]
        - df["cheapest_price"]
    )

    df["price_rank"] = (
        df.groupby("master_product_id")["price"]
          .rank(
              method="dense",
              ascending=True
          )
    )

    df["is_cheapest"] = (
        df["price"] ==
        df["cheapest_price"]
    ).astype(int)

    spread = (
        df["highest_price"]
        - df["cheapest_price"]
    )

    df["price_position"] = (
        (
            df["price"]
            - df["cheapest_price"]
        )
        /
        spread.replace(0, pd.NA)
    )

    # -----------------
    # Rating
    # -----------------

    df["rating_score"] = (
        df["rating"] / 5
    )

    # -----------------
    # Review
    # -----------------

    df["review_score_raw"] = np.log1p(
        df["review_count"].fillna(0)
    )

    min_review = (
        df["review_score_raw"].min()
    )

    max_review = (
        df["review_score_raw"].max()
    )

    df["review_score"] = (
        (
            df["review_score_raw"]
            - min_review
        )
        /
        (
            max_review
            - min_review
        )
        if max_review != min_review
        else 0
    )

    # -----------------
    # Quality
    # -----------------

    df["quality_score"] = (
        0.7 * df["rating_score"].fillna(0)
        +
        0.3 * df["review_score"].fillna(0)
    )

    # -----------------
    # Discount Score
    # -----------------

    df["discount_score"] = (
        df["discount_percent"]
        .fillna(0)
        .clip(0, 100)
        / 100
    )

    # -----------------
    # Price Score
    # -----------------

    df["price_score"] = (
        1 -
        df["price_position"].fillna(0)
    )

    # -----------------
    # Deal Score
    # -----------------

    df["deal_score"] = (
        0.50 * df["price_score"]
        +
        0.25 * df["discount_score"]
        +
        0.25 * df["quality_score"]
    )

    # -----------------
    # Seller Count
    # -----------------

    df["seller_count"] = (
        df.groupby("master_product_id")["website"]
          .transform("nunique")
    )

    return df
```

Run:

```python
df_features = create_features(df)
```

---

# M11.50 — Top Deals

```python
top_deals = (
    df_features
    .sort_values(
        "deal_score",
        ascending=False
    )
    .head(20)
)

print(
    top_deals[
        [
            "name",
            "website",
            "price",
            "discount_percent",
            "rating",
            "review_count",
            "deal_score"
        ]
    ]
)
```

এখন আমরা বলতে পারি:

> কোন seller-এর কোন product আমাদের defined scoring rules অনুযায়ী সবচেয়ে attractive deal?

---

# M11.51 — Top Competitive Sellers

```python
seller_summary = (
    df_features
    .groupby("website")
    .agg(
        products=(
            "master_product_id",
            "nunique"
        ),

        avg_price=(
            "price",
            "mean"
        ),

        avg_discount=(
            "discount_percent",
            "mean"
        ),

        avg_rating=(
            "rating",
            "mean"
        ),

        cheapest_count=(
            "is_cheapest",
            "sum"
        ),

        avg_deal_score=(
            "deal_score",
            "mean"
        )
    )
    .sort_values(
        "avg_deal_score",
        ascending=False
    )
)

print(seller_summary)
```

---

# M11.52 — Export Feature Dataset

```python
df_features.to_csv(
    "data/exports/ecommerce_features.csv",
    index=False
)
```

Excel:

```python
df_features.to_excel(
    "data/exports/ecommerce_features.xlsx",
    index=False
)
```

---

# 🏗️ M11 Architecture

এখন পুরো pipeline:

```text
                     WEB DATA
                        │
                        ▼
                    SCRAPERS
                        │
                        ▼
                     PARSER
                        │
                        ▼
                    CLEANING
                        │
                        ▼
                   POSTGRESQL
                        │
                        ▼
                PRODUCT MATCHING
                        │
                        ▼
                MASTER PRODUCTS
                        │
                        ▼
                      SQL
                        │
                        ▼
                    PANDAS
                        │
                        ▼
              FEATURE ENGINEERING
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
   Price Features   Quality Features   Market Features
        │               │                │
        └───────────────┼────────────────┘
                        ▼
                  DEAL SCORE
                        │
                        ▼
             ANALYTICS / DASHBOARD
                        │
                        ▼
                    ML DATASET
```

---

# 🔥 M11 Mini Project

তোমার project-এ এখন এই ৩টি dataset তৈরি করবে।

## 1. `product_features.csv`

প্রতি master product:

```text
master_product_id
cheapest_price
highest_price
average_price
price_spread
seller_count
average_rating
average_discount
total_reviews
```

---

## 2. `seller_features.csv`

প্রতি website:

```text
website
product_count
average_price
average_discount
average_rating
cheapest_products
average_deal_score
```

---

## 3. `seller_product_features.csv`

প্রতি product + website:

```text
master_product_id
website
price
discount_percent
rating
review_count

price_rank
is_cheapest
price_position
difference_from_cheapest
difference_from_cheapest_percent

rating_score
review_score
quality_score
discount_score
price_score
deal_score
competitiveness_score
```

---

# ⚠️ M11-এ কয়েকটি Important সতর্কতা

### 1. Score মানেই truth নয়

যেমন:

```text
deal_score = 0.87
```

এর মানে product objectively "best" নয়।

এর মানে:

> তোমার defined scoring formula অনুযায়ী product-এর score 0.87।

---

### 2. Weight business অনুযায়ী বদলাবে

আমি example হিসেবে দিয়েছি:

```text
Price       50%
Discount    25%
Quality     25%
```

কিন্তু luxury products-এর ক্ষেত্রে হতে পারে:

```text
Price       30%
Quality     50%
Reviews     20%
```

---

### 3. Missing data-কে zero ভাবা risky

বিশেষ করে:

```text
rating
discount
review_count
```

Missing মানেই:

```text
0
```

নয়।

---

# 🧠 M11 Mastery Checklist

তুমি যদি এগুলো নিজে করতে পারো, তাহলে M11 complete:

* [ ] Data validation
* [ ] Missing value handling
* [ ] Invalid value detection
* [ ] Price validation
* [ ] Discount calculation
* [ ] Discount percentage
* [ ] Price rank
* [ ] Cheapest price
* [ ] Highest price
* [ ] Average market price
* [ ] Price spread
* [ ] Price difference
* [ ] Seller count
* [ ] Cheapest seller flag
* [ ] Price position
* [ ] Rating score
* [ ] Review score
* [ ] Log transformation
* [ ] Quality score
* [ ] Discount score
* [ ] Price score
* [ ] Deal score
* [ ] Competitiveness score
* [ ] Price buckets
* [ ] Discount buckets
* [ ] Rating buckets
* [ ] Data completeness
* [ ] Outlier detection
* [ ] Product-level features
* [ ] Seller-level features
* [ ] Category-level features
* [ ] Feature dataset export

---

# 🚀 M08 → M11 Progress

```text
M08
PostgreSQL
   ↓
Database Storage

M09
SQL + Pandas
   ↓
Analytics

M10
Product Matching
   ↓
Same Product Identification

M11
Feature Engineering
   ↓
Business Intelligence Features
```

এখন তোমার data শুধু scraped data নয়:

```text
Raw Data
   ↓
Clean Data
   ↓
Matched Data
   ↓
Feature Data
   ↓
Analytics-ready Data
```

**M11-এর সবচেয়ে গুরুত্বপূর্ণ concept হলো:**

```text
Raw data tells you what happened.

Features help you understand
why it matters and how products/sellers compare.
```

পরবর্তী ধাপে **M12 — Advanced Price Intelligence & Time-Series Analysis**-এ আমরা historical price data নিয়ে `price trend`, `price drop detection`, `moving average`, `volatility`, `price forecasting-এর জন্য dataset preparation`, এবং **কখন product সত্যিই “good deal” হয়েছে**—এসব deeply করব।


---
# M12 — Advanced Price Intelligence & Time-Series Analysis

এই Module-এ আমরা M11-এর feature engineering-এর পরের level-এ যাব।

এখন আমাদের লক্ষ্য হবে:

> **একটি product-এর price কীভাবে সময়ের সাথে পরিবর্তন করছে, কখন price drop হয়েছে, trend কী, volatility কত, এবং কোন সময় product-টি সত্যিকারের good deal—তা programmatically বের করা।**

---

# 🎯 M12 Learning Goals

এই module শেষে তুমি পারবে:

1. Historical price data analyze করতে
2. Daily/weekly price trend বের করতে
3. Price change detect করতে
4. Price drop detect করতে
5. Moving Average calculate করতে
6. Rolling statistics বুঝতে
7. Price volatility calculate করতে
8. Lowest/highest historical price বের করতে
9. Current price বনাম historical price compare করতে
10. Good Deal detection করতে
11. Discount আসলেই ভালো কিনা বুঝতে
12. Forecasting-এর জন্য dataset তৈরি করতে
13. Time-series feature engineering করতে
14. Product-level price intelligence system বানাতে

---

# M12 Architecture

আমাদের pipeline এখন হবে:

```text
E-commerce Websites
        ↓
Scraper / API
        ↓
Raw Product Data
        ↓
Cleaning
        ↓
Product Matching
        ↓
PostgreSQL
        ↓
Historical Price Data
        ↓
Pandas
        ↓
Time-Series Analysis
        ↓
Price Intelligence
        ↓
Good Deal Detection
        ↓
Forecasting Dataset
```

---

# 1. Historical Price Data কী?

ধরো একটি product:

```text
iPhone 16 128GB
```

তার price প্রতিদিন পরিবর্তন হচ্ছে:

| Date  |  Price |
| ----- | -----: |
| Jan 1 | 85,000 |
| Jan 2 | 84,500 |
| Jan 3 | 84,500 |
| Jan 4 | 82,000 |
| Jan 5 | 82,000 |
| Jan 6 | 80,000 |
| Jan 7 | 81,000 |

এটাই হলো:

> **Price History**

এখানে শুধু current price রাখলে আমরা বুঝতে পারব না product-এর price কীভাবে পরিবর্তিত হয়েছে।

তাই M08-এ আমরা `price_history` table তৈরি করেছিলাম।

---

# 2. Price History Table

আমাদের table:

```sql
CREATE TABLE price_history (
    id BIGSERIAL PRIMARY KEY,

    product_id BIGINT NOT NULL
        REFERENCES products(id)
        ON DELETE CASCADE,

    price NUMERIC(12, 2) NOT NULL,

    original_price NUMERIC(12, 2),

    discount NUMERIC(5, 2),

    rating NUMERIC(3, 2),

    review_count INTEGER,

    scraped_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

একটি product-এর জন্য:

```text
product_id = 101
```

এর অনেকগুলো price snapshot থাকতে পারে।

```text
101 → 85000 → Jan 1
101 → 84500 → Jan 2
101 → 82000 → Jan 4
101 → 80000 → Jan 6
```

অর্থাৎ:

```text
Product 1:N Price History
```

---

# 3. PostgreSQL থেকে Historical Data Load

প্রথমে:

```python
import pandas as pd
from sqlalchemy import create_engine
```

Connection:

```python
DATABASE_URL = (
    "postgresql+psycopg://"
    "ecommerce_user:your_password@localhost:5432/ecommerce_db"
)

engine = create_engine(DATABASE_URL)
```

তারপর:

```python
query = """
SELECT
    ph.product_id,
    p.name,
    ph.price,
    ph.original_price,
    ph.discount,
    ph.rating,
    ph.review_count,
    ph.scraped_at
FROM price_history ph
JOIN products p
    ON ph.product_id = p.id
ORDER BY ph.product_id, ph.scraped_at;
"""

df = pd.read_sql(query, engine)
```

দেখি:

```python
print(df.head())
```

---

# 4. Datetime Conversion

`scraped_at` এখন string হতে পারে।

তাই:

```python
df["scraped_at"] = pd.to_datetime(
    df["scraped_at"]
)
```

Check:

```python
print(df.dtypes)
```

Expected:

```text
product_id                 int64
name                      object
price                    float64
original_price           float64
discount                 float64
rating                   float64
review_count               int64
scraped_at        datetime64[ns]
```

---

# 5. Sort করা খুব গুরুত্বপূর্ণ

Time-series analysis-এর আগে অবশ্যই sort করতে হবে।

```python
df = df.sort_values(
    ["product_id", "scraped_at"]
)
```

কারণ আমাদের দরকার:

```text
Product
   ↓
oldest → newest
```

---

# 6. Price Change

ধরো:

```text
85000
84000
82000
80000
```

Price change বের করতে:

```python
df["price_change"] = (
    df.groupby("product_id")["price"]
      .diff()
)
```

Result:

| Price | Price Change |
| ----: | -----------: |
| 85000 |          NaN |
| 84000 |        -1000 |
| 82000 |        -2000 |
| 80000 |        -2000 |

### Interpretation

```text
Negative → price decreased
Positive → price increased
0        → unchanged
```

---

# 7. Price Change Percentage

শুধু টাকা দিয়ে change জানা যথেষ্ট নয়।

আমরা percentage চাই।

Formula:

```text
Price Change %
=
(Current - Previous)
/
Previous
× 100
```

Pandas:

```python
df["previous_price"] = (
    df.groupby("product_id")["price"]
      .shift(1)
)
```

তারপর:

```python
df["price_change_percent"] = (
    (df["price"] - df["previous_price"])
    / df["previous_price"]
) * 100
```

Example:

```text
Previous = 10000
Current  = 9000
```

তাহলে:

```text
(9000 - 10000) / 10000 × 100
= -10%
```

অর্থাৎ:

> Price 10% কমেছে।

---

# 8. Price Drop Detection

এখন আমরা জানতে চাই:

> কোন observation-এ price drop হয়েছে?

```python
df["price_drop"] = (
    df["price_change"] < 0
)
```

Example:

| Price | Change | Drop  |
| ----: | -----: | ----- |
| 10000 |    NaN | False |
|  9500 |   -500 | True  |
|  9500 |      0 | False |
|  9000 |   -500 | True  |

---

# 9. Significant Price Drop

প্রতিটি ছোট drop important নয়।

ধরো:

```text
10,000 → 9,950
```

এটা মাত্র:

```text
-0.5%
```

কিন্তু:

```text
10,000 → 8,000
```

হলো:

```text
-20%
```

আমরা significant drop define করতে পারি:

```python
df["significant_drop"] = (
    df["price_change_percent"] <= -10
)
```

এখানে:

```text
<= -10%
```

মানে অন্তত 10% price drop।

---

# 10. Price Increase Detection

একইভাবে:

```python
df["price_increase"] = (
    df["price_change"] > 0
)
```

Significant increase:

```python
df["significant_increase"] = (
    df["price_change_percent"] >= 10
)
```

---

# 11. Historical Minimum Price

একটি product-এর ইতিহাসে সবচেয়ে কম price:

```python
df["historical_min"] = (
    df.groupby("product_id")["price"]
      .transform("min")
)
```

Example:

```text
Current = 82,000
Historical Min = 75,000
```

এখন বুঝতে পারব current price historical lowest নয়।

---

# 12. Historical Maximum Price

```python
df["historical_max"] = (
    df.groupby("product_id")["price"]
      .transform("max")
)
```

---

# 13. Historical Average Price

```python
df["historical_avg"] = (
    df.groupby("product_id")["price"]
      .transform("mean")
)
```

---

# 14. Current Price বনাম Historical Average

```python
df["difference_from_avg"] = (
    df["price"] - df["historical_avg"]
)
```

Percentage:

```python
df["difference_from_avg_percent"] = (
    (df["price"] - df["historical_avg"])
    / df["historical_avg"]
) * 100
```

যদি:

```text
Current = 80,000
Average = 90,000
```

তাহলে:

```text
-11.11%
```

অর্থাৎ current price historical average-এর চেয়ে প্রায় 11% কম।

---

# 15. Historical Low Distance

Current price historical minimum-এর কত উপরে?

```python
df["distance_from_historical_low"] = (
    df["price"] - df["historical_min"]
)
```

Percentage:

```python
df["distance_from_historical_low_percent"] = (
    (df["price"] - df["historical_min"])
    / df["historical_min"]
) * 100
```

Example:

```text
Historical Low = 75,000
Current = 80,000
```

তাহলে:

```text
(80000 - 75000) / 75000 × 100
= 6.67%
```

Current price historical low থেকে মাত্র 6.67% বেশি।

---

# 16. Is Historical Low?

```python
df["is_historical_low"] = (
    df["price"] == df["historical_min"]
)
```

Result:

```text
True
False
False
```

এটি খুব useful feature।

---

# 17. Rolling Average / Moving Average

এখন আসি খুব important topic-এ।

ধরো price:

```text
100
110
105
120
115
130
```

Price অনেক ওঠানামা করছে।

Trend বুঝতে আমরা **Moving Average** ব্যবহার করতে পারি।

---

# 18. 3-Day Moving Average

Formula:

```text
Day 1 → 100
Day 2 → 110
Day 3 → 105

3-day average
= (100 + 110 + 105) / 3
= 105
```

Pandas:

```python
df["ma_3"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(3).mean()
      )
)
```

---

# 19. 7-Day Moving Average

```python
df["ma_7"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(7).mean()
      )
)
```

---

# 20. 30-Day Moving Average

যদি daily data থাকে:

```python
df["ma_30"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(30).mean()
      )
)
```

---

# 21. Moving Average কেন ব্যবহার করব?

Raw price:

```text
100
102
98
110
105
115
108
```

এখানে noise বেশি।

Moving average:

```text
100
101
100
103
105
110
111
```

এতে overall trend পরিষ্কার হয়।

---

# 22. Rolling Minimum

শেষ 7 observations-এর মধ্যে lowest price:

```python
df["rolling_min_7"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(7).min()
      )
)
```

---

# 23. Rolling Maximum

```python
df["rolling_max_7"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(7).max()
      )
)
```

---

# 24. Rolling Standard Deviation

Price কতটা fluctuate করছে সেটা বুঝতে:

```python
df["rolling_std_7"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(7).std()
      )
)
```

এটি volatility analysis-এর ভিত্তি।

---

# 25. Price Volatility

Simple volatility:

```python
volatility = (
    df.groupby("product_id")["price"]
      .std()
)
```

কিন্তু price scale আলাদা হলে standard deviation compare করা কঠিন।

Better:

```text
Coefficient of Variation

CV = Standard Deviation / Mean
```

Pandas:

```python
volatility_df = (
    df.groupby("product_id")["price"]
      .agg(
          mean_price="mean",
          std_price="std"
      )
      .reset_index()
)

volatility_df["cv"] = (
    volatility_df["std_price"]
    / volatility_df["mean_price"]
)
```

---

# 26. Volatility Interpretation

ধরো:

```text
Product A
Mean = 100,000
Std = 2,000

CV = 0.02
```

অর্থাৎ:

```text
2% volatility
```

আর:

```text
Product B
Mean = 100,000
Std = 15,000

CV = 0.15
```

অর্থাৎ:

```text
15% volatility
```

Product B-এর price অনেক বেশি unstable।

---

# 27. Price Trend

আমরা জানতে চাই:

> Product-এর price overall কমছে নাকি বাড়ছে?

Simple approach:

```python
df["price_change_percent"]
```

তার average:

```python
trend = (
    df.groupby("product_id")["price_change_percent"]
      .mean()
)
```

কিন্তু আরও ভালোভাবে trend analysis করা যায়।

---

# 28. First Price vs Current Price

```python
first_price = (
    df.groupby("product_id")["price"]
      .transform("first")
)

df["change_from_first"] = (
    df["price"] - first_price
)
```

Percentage:

```python
df["change_from_first_percent"] = (
    (df["price"] - first_price)
    / first_price
) * 100
```

যদি:

```text
First = 100,000
Current = 85,000
```

তাহলে:

```text
-15%
```

অর্থাৎ historical period-এ price overall 15% কমেছে।

---

# 29. Price Trend Classification

আমরা category তৈরি করতে পারি:

```python
def classify_trend(value):

    if value < -5:
        return "falling"

    elif value > 5:
        return "rising"

    else:
        return "stable"
```

তারপর:

```python
df["trend"] = (
    df["change_from_first_percent"]
    .apply(classify_trend)
)
```

Output:

```text
falling
stable
rising
```

---

# 30. Better Trend — Linear Regression

আরও advanced approach হলো price বনাম time-এর উপর linear regression।

ধরো:

```text
Day 1 → 100
Day 2 → 98
Day 3 → 97
Day 4 → 95
Day 5 → 94
```

Regression:

```text
Price = a × Time + b
```

এখানে `a` হলো slope।

```text
slope < 0 → price falling
slope > 0 → price rising
slope ≈ 0 → stable
```

Python:

```python
import numpy as np

def price_trend_slope(group):

    group = group.sort_values("scraped_at")

    x = np.arange(len(group))
    y = group["price"].values

    if len(group) < 2:
        return np.nan

    slope = np.polyfit(x, y, 1)[0]

    return slope
```

তারপর:

```python
trend_df = (
    df.groupby("product_id")
      .apply(price_trend_slope)
      .reset_index(name="trend_slope")
)
```

---

# 31. Why Slope Useful?

ধরো:

### Product A

```text
100000
99000
98000
97000
96000
```

Slope:

```text
negative
```

### Product B

```text
90000
92000
94000
96000
98000
```

Slope:

```text
positive
```

### Product C

```text
90000
90200
89800
90100
90000
```

Slope:

```text
near zero
```

---

# 32. Detect Price Crash

ধরো:

```text
100,000
99,000
98,500
75,000
```

শেষ observation-এ:

```text
-23.86%
```

আমরা detect করতে পারি:

```python
df["price_crash"] = (
    df["price_change_percent"] <= -20
)
```

---

# 33. Price Recovery

ধরো:

```text
100,000
80,000
82,000
90,000
95,000
```

Price আবার বাড়ছে।

Previous minimum:

```python
df["historical_min"]
```

Current price historical low থেকে recovery percentage:

```python
df["recovery_from_low_percent"] = (
    (df["price"] - df["historical_min"])
    / df["historical_min"]
) * 100
```

---

# 34. Detect Good Deal

এখন সবচেয়ে interesting অংশ।

ধরো website দেখাচ্ছে:

```text
Original Price = 100,000
Current Price = 80,000
Discount = 20%
```

দেখে মনে হচ্ছে excellent deal।

কিন্তু historical data বলছে:

```text
Last month:
75,000
78,000
80,000
82,000
```

তাহলে 80,000 আসলে extraordinary deal নয়।

এখানে আমরা বুঝি:

> **Advertised discount ≠ Real deal**

---

# 35. Real Deal Concept

একটি product-এর current price যদি:

```text
historical average-এর নিচে
```

এবং:

```text
historical low-এর কাছাকাছি
```

তাহলে deal quality বেশি।

---

# 36. Historical Discount

Feature:

```python
df["historical_discount_percent"] = (
    (df["historical_avg"] - df["price"])
    / df["historical_avg"]
) * 100
```

Example:

```text
Historical Avg = 100,000
Current = 80,000
```

তাহলে:

```text
20%
```

---

# 37. Deal Score

আমরা একটি simple business heuristic বানাতে পারি।

```python
df["historical_deal_score"] = (
    df["historical_discount_percent"]
    .clip(lower=0)
)
```

কিন্তু আরও useful করতে পারি।

---

# 38. Multi-Factor Deal Score

ধরো:

```text
30% → historical price advantage
25% → current discount
20% → rating
15% → review strength
10% → distance from historical low
```

Concept:

```python
df["price_advantage_score"] = (
    df["historical_discount_percent"]
    .clip(0, 50)
    / 50
)
```

Discount:

```python
df["discount_score"] = (
    df["discount_percent"]
    .clip(0, 100)
    / 100
)
```

Rating:

```python
df["rating_score"] = (
    df["rating"] / 5
)
```

তারপর:

```python
df["deal_score"] = (
    0.30 * df["price_advantage_score"].fillna(0)
    + 0.25 * df["discount_score"].fillna(0)
    + 0.20 * df["rating_score"].fillna(0)
)
```

এখানে আরও features যোগ করা যাবে।

**Important:** এই weights universal truth নয়। Business/domain অনুযায়ী validate করতে হবে।

---

# 39. Historical Low Proximity

Current price historical low-এর কত কাছাকাছি?

```python
df["low_proximity"] = (
    1 -
    (
        (df["price"] - df["historical_min"])
        /
        (df["historical_max"] - df["historical_min"])
    )
)
```

Interpretation:

```text
≈ 1 → historical low-এর খুব কাছে
≈ 0 → historical high-এর কাছে
```

Division by zero avoid করতে:

```python
price_range = (
    df["historical_max"] -
    df["historical_min"]
)

df["low_proximity"] = np.where(
    price_range > 0,
    1 - (
        (df["price"] - df["historical_min"])
        / price_range
    ),
    1
)
```

---

# 40. Final Deal Classification

```python
def classify_deal(row):

    if (
        row["is_historical_low"]
        and row["rating"] >= 4
    ):
        return "excellent_deal"

    elif (
        row["historical_discount_percent"] >= 15
        and row["rating"] >= 4
    ):
        return "good_deal"

    elif row["historical_discount_percent"] >= 5:
        return "moderate_deal"

    return "normal"
```

Apply:

```python
df["deal_category"] = (
    df.apply(classify_deal, axis=1)
)
```

---

# 41. Important Problem — Sampling Frequency

এখানে একটি খুব important issue আছে।

ধরো তুমি দিনে একবার scrape করো:

```text
10 AM → 100,000
```

কিন্তু website দুপুর 2 PM-এ price কমিয়ে:

```text
80,000
```

এবং সন্ধ্যায় আবার:

```text
100,000
```

করল।

তুমি যদি শুধু 10 AM-এ scrape করো, তাহলে এই price drop কখনো দেখবে না।

তাই:

> **Time-series quality depends on sampling frequency.**

---

# 42. Daily vs Hourly Data

### Daily

```text
2026-09-01 → 100000
2026-09-02 → 98000
2026-09-03 → 97000
```

### Hourly

```text
09:00 → 100000
10:00 → 100000
11:00 → 95000
12:00 → 90000
13:00 → 92000
```

Hourly data বেশি detailed কিন্তু storage এবং scraping cost বেশি।

---

# 43. Resampling

ধরো data irregular:

```text
09:15
11:40
14:20
17:05
```

আমরা daily data বানাতে পারি।

```python
df = df.set_index("scraped_at")
```

তারপর:

```python
daily_price = (
    df.groupby("product_id")["price"]
      .resample("D")
      .mean()
      .reset_index()
)
```

---

# 44. Daily Minimum Price

অনেক ক্ষেত্রে average-এর চেয়ে minimum useful:

```python
daily_min = (
    df.groupby("product_id")["price"]
      .resample("D")
      .min()
      .reset_index()
)
```

কারণ:

> "আজ product-এর সবচেয়ে কম price কত ছিল?"

এই question-এর answer পাওয়া যাবে।

---

# 45. Daily Maximum Price

```python
daily_max = (
    df.groupby("product_id")["price"]
      .resample("D")
      .max()
      .reset_index()
)
```

---

# 46. Weekly Analysis

Weekly average:

```python
weekly_price = (
    df.groupby("product_id")["price"]
      .resample("W")
      .mean()
      .reset_index()
)
```

এতে weekly trend সহজে দেখা যায়।

---

# 47. Price Change Events

আমরা event table-এর মতো dataset বানাতে পারি।

```python
events = df[
    df["price_change_percent"].notna()
].copy()
```

Significant drops:

```python
price_drop_events = events[
    events["price_change_percent"] <= -10
]
```

এখন:

```python
print(
    price_drop_events[
        [
            "product_id",
            "name",
            "price",
            "previous_price",
            "price_change_percent",
            "scraped_at"
        ]
    ]
)
```

এটি আমাদের **Price Alert System**-এর foundation।

---

# 48. Price Alert Logic

ধরো:

```text
Previous price = 100,000
Current price = 85,000
```

Change:

```text
-15%
```

তাহলে:

```python
if price_change_percent <= -10:
    print("PRICE DROP ALERT")
```

Real system-এ:

```text
Database
    ↓
New price
    ↓
Compare previous
    ↓
Price drop?
    ↓
YES
    ↓
Alert
```

---

# 49. Price Intelligence Dataset

শেষে আমরা এমন dataset তৈরি করতে পারি:

| Feature              | Meaning                      |
| -------------------- | ---------------------------- |
| current_price        | Current price                |
| historical_min       | Lowest historical price      |
| historical_max       | Highest historical price     |
| historical_avg       | Average price                |
| price_change         | Last change                  |
| price_change_percent | Last change %                |
| ma_7                 | 7-day average                |
| ma_30                | 30-day average               |
| volatility           | Price volatility             |
| trend_slope          | Trend                        |
| historical_discount  | Discount vs historical avg   |
| low_proximity        | Distance from historical low |
| is_historical_low    | Lowest price?                |
| deal_score           | Deal quality                 |

এটাই **Price Intelligence Feature Dataset**।

---

# 50. Forecasting Dataset Preparation

এখন আমরা future prediction-এর দিকে যেতে পারি।

ধরো:

```text
Date        Price
Sep 1       100000
Sep 2       99000
Sep 3       98000
Sep 4       97000
Sep 5       95000
```

আমরা future price predict করতে চাই।

প্রথমে lag features বানাতে হবে।

---

# 51. Lag Feature

Lag 1:

```python
df["lag_1"] = (
    df.groupby("product_id")["price"]
      .shift(1)
)
```

Lag 2:

```python
df["lag_2"] = (
    df.groupby("product_id")["price"]
      .shift(2)
)
```

Lag 7:

```python
df["lag_7"] = (
    df.groupby("product_id")["price"]
      .shift(7)
)
```

---

# 52. কেন Lag Feature?

ধরো:

```text
Today price = ?
```

Model-কে আমরা বলছি:

```text
Yesterday price
7 days ago price
30 days ago price
```

এগুলো দিয়ে future price predict করতে।

---

# 53. Rolling Features for Forecasting

```python
df["rolling_mean_7"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(7).mean()
      )
)
```

30-day:

```python
df["rolling_mean_30"] = (
    df.groupby("product_id")["price"]
      .transform(
          lambda x: x.rolling(30).mean()
      )
)
```

---

# 54. Forecasting Feature Set

একটি basic dataset:

```text
lag_1
lag_2
lag_3
lag_7
lag_14
rolling_mean_7
rolling_mean_30
rolling_std_7
discount
rating
review_count
day_of_week
month
```

Target:

```text
future_price
```

---

# 55. Target তৈরি

ধরো next day's price predict করব:

```python
df["target_price"] = (
    df.groupby("product_id")["price"]
      .shift(-1)
)
```

এখানে:

```text
Current row → Tomorrow's price
```

---

# 56. Time Features

Date থেকে:

```python
df["day"] = df["scraped_at"].dt.day
df["month"] = df["scraped_at"].dt.month
df["year"] = df["scraped_at"].dt.year
df["day_of_week"] = df["scraped_at"].dt.dayofweek
```

Hour data থাকলে:

```python
df["hour"] = df["scraped_at"].dt.hour
```

---

# 57. Time-Series Dataset

Final:

```python
features = [
    "lag_1",
    "lag_2",
    "lag_7",
    "rolling_mean_7",
    "rolling_mean_30",
    "rolling_std_7",
    "discount",
    "rating",
    "review_count",
    "day_of_week",
    "month"
]

target = "target_price"
```

---

# 58. Critical Concept — Data Leakage

Time-series ML-এ এটা খুব important।

ভুল:

```text
Future information
        ↓
Current prediction
```

Example:

```python
rolling_mean = df["price"].rolling(7).mean()
```

যদি accidentally future observations include হয়, তাহলে model future দেখে ফেলবে।

আমাদের features অবশ্যই:

> **Prediction time-এর আগে available information দিয়ে তৈরি হতে হবে।**

---

# 59. Random Train-Test Split Avoid করা

Normal ML:

```python
train_test_split(...)
```

কিন্তু time-series-এর ক্ষেত্রে random split problematic হতে পারে।

কারণ:

```text
2026 data
```

training-এ চলে যেতে পারে এবং:

```text
2025 data
```

test-এ চলে যেতে পারে।

এটা বাস্তব forecasting scenario নয়।

Better:

```text
Past
 ↓
TRAIN

Future
 ↓
TEST
```

Example:

```text
Jan → May     TRAIN
Jun → Jul     TEST
```

---

# 60. M12 Complete Feature Pipeline

আমাদের final pipeline:

```text
Historical Price
        ↓
Sort by Product + Time
        ↓
Previous Price
        ↓
Price Change
        ↓
Price Change %
        ↓
Price Drop Detection
        ↓
Historical Min/Max/Avg
        ↓
Moving Average
        ↓
Rolling Min/Max
        ↓
Volatility
        ↓
Trend
        ↓
Historical Deal Analysis
        ↓
Deal Score
        ↓
Lag Features
        ↓
Rolling Features
        ↓
Time Features
        ↓
Forecasting Dataset
```

---

# 61. Complete M12 Example

একসাথে basic pipeline:

```python
import pandas as pd
import numpy as np


def create_price_intelligence(df):

    df = df.copy()

    # -------------------------
    # 1. Datetime
    # -------------------------
    df["scraped_at"] = pd.to_datetime(
        df["scraped_at"]
    )

    # -------------------------
    # 2. Sort
    # -------------------------
    df = df.sort_values(
        ["product_id", "scraped_at"]
    )

    # -------------------------
    # 3. Previous price
    # -------------------------
    df["previous_price"] = (
        df.groupby("product_id")["price"]
          .shift(1)
    )

    # -------------------------
    # 4. Price change
    # -------------------------
    df["price_change"] = (
        df["price"] -
        df["previous_price"]
    )

    # -------------------------
    # 5. Price change %
    # -------------------------
    df["price_change_percent"] = (
        df["price_change"]
        / df["previous_price"]
    ) * 100

    # -------------------------
    # 6. Price drop
    # -------------------------
    df["price_drop"] = (
        df["price_change"] < 0
    )

    # -------------------------
    # 7. Historical min
    # -------------------------
    df["historical_min"] = (
        df.groupby("product_id")["price"]
          .transform("min")
    )

    # -------------------------
    # 8. Historical max
    # -------------------------
    df["historical_max"] = (
        df.groupby("product_id")["price"]
          .transform("max")
    )

    # -------------------------
    # 9. Historical average
    # -------------------------
    df["historical_avg"] = (
        df.groupby("product_id")["price"]
          .transform("mean")
    )

    # -------------------------
    # 10. Historical discount
    # -------------------------
    df["historical_discount_percent"] = (
        (
            df["historical_avg"] -
            df["price"]
        )
        / df["historical_avg"]
    ) * 100

    # -------------------------
    # 11. Historical low
    # -------------------------
    df["is_historical_low"] = (
        df["price"] ==
        df["historical_min"]
    )

    # -------------------------
    # 12. Moving Average
    # -------------------------
    df["ma_7"] = (
        df.groupby("product_id")["price"]
          .transform(
              lambda x:
              x.rolling(7).mean()
          )
    )

    # -------------------------
    # 13. Rolling Std
    # -------------------------
    df["rolling_std_7"] = (
        df.groupby("product_id")["price"]
          .transform(
              lambda x:
              x.rolling(7).std()
          )
    )

    # -------------------------
    # 14. Lag features
    # -------------------------
    df["lag_1"] = (
        df.groupby("product_id")["price"]
          .shift(1)
    )

    df["lag_7"] = (
        df.groupby("product_id")["price"]
          .shift(7)
    )

    # -------------------------
    # 15. Time features
    # -------------------------
    df["day_of_week"] = (
        df["scraped_at"].dt.dayofweek
    )

    df["month"] = (
        df["scraped_at"].dt.month
    )

    # -------------------------
    # 16. Target
    # -------------------------
    df["target_price"] = (
        df.groupby("product_id")["price"]
          .shift(-1)
    )

    return df
```

Run:

```python
result = create_price_intelligence(df)

print(result.head())
```

---

# 62. Product-Level Intelligence Summary

আমরা প্রতিটি product-এর জন্য summary বানাতে পারি:

```python
product_intelligence = (
    df.groupby("product_id")
      .agg(
          current_price=("price", "last"),
          historical_min=("price", "min"),
          historical_max=("price", "max"),
          historical_avg=("price", "mean"),
          price_std=("price", "std"),
          observations=("price", "count"),
          avg_rating=("rating", "mean"),
          avg_discount=("discount", "mean")
      )
      .reset_index()
)
```

---

# 63. Volatility Add করা

```python
product_intelligence["volatility"] = (
    product_intelligence["price_std"]
    /
    product_intelligence["historical_avg"]
)
```

---

# 64. Current Price Position

```python
price_range = (
    product_intelligence["historical_max"]
    -
    product_intelligence["historical_min"]
)

product_intelligence["price_position"] = np.where(
    price_range > 0,
    (
        product_intelligence["current_price"]
        -
        product_intelligence["historical_min"]
    ) / price_range,
    0
)
```

Interpretation:

```text
0   → historical low
0.5 → middle
1   → historical high
```

---

# 65. Final Product Intelligence Table

তখন dataset দেখতে পারে:

| Product    | Current | Min |  Max |  Avg | Volatility | Position |
| ---------- | ------: | --: | ---: | ---: | ---------: | -------: |
| iPhone 16  |     80K | 75K | 100K |  88K |       0.08 |     0.20 |
| Galaxy S25 |     95K | 90K | 110K | 102K |       0.05 |     0.25 |
| Pixel 9    |     70K | 65K |  95K |  80K |       0.12 |     0.20 |

এখন আমরা শুধু "price" দেখছি না।

আমরা product-এর **market behavior** দেখছি।

---

# 66. M12 Mini Project 🚀

এখন তোমার project হবে:

## Project: E-commerce Price Intelligence System

Dataset:

```text
3 Websites
×
100 Products
×
30 Days
```

অর্থাৎ প্রায়:

```text
9,000 price observations
```

যদি প্রতিটি product-এর 30 দিনের data থাকে:

```text
300 products × 30 days
= 9,000 observations
```

---

## Step 1 — PostgreSQL

Collect:

```text
product_id
master_product_id
website
price
discount
rating
review_count
scraped_at
```

---

## Step 2 — Pandas

Load:

```python
pd.read_sql(...)
```

---

## Step 3 — Historical Analysis

Calculate:

```text
previous_price
price_change
price_change_percent
historical_min
historical_max
historical_avg
```

---

## Step 4 — Moving Average

Create:

```text
MA_3
MA_7
MA_14
MA_30
```

---

## Step 5 — Volatility

Calculate:

```text
standard deviation
coefficient of variation
rolling volatility
```

---

## Step 6 — Trend

Create:

```text
trend_slope
trend_category
```

---

## Step 7 — Price Drop

Detect:

```text
>5%
>10%
>20%
```

price drops.

---

## Step 8 — Deal Detection

Create:

```text
historical_discount
low_proximity
deal_score
deal_category
```

---

## Step 9 — Forecasting Dataset

Create:

```text
lag_1
lag_2
lag_3
lag_7
rolling_mean_7
rolling_mean_30
rolling_std_7
day_of_week
month
target_price
```

---

# 67. Recommended Project Structure

M12-এর পরে project structure:

```text
ecommerce_data_collector/
│
├── scrapers/
│   ├── base.py
│   ├── site_a.py
│   ├── site_b.py
│   └── site_c.py
│
├── parsers/
│   ├── site_a_parser.py
│   ├── site_b_parser.py
│   └── site_c_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── matching/
│   ├── normalize.py
│   ├── attributes.py
│   ├── candidates.py
│   └── matcher.py
│
├── database/
│   ├── connection.py
│   ├── products.py
│   └── prices.py
│
├── analytics/
│   ├── price_history.py
│   ├── price_trend.py
│   ├── volatility.py
│   ├── deal_detection.py
│   └── forecasting_features.py
│
├── data/
│   ├── raw/
│   ├── cleaned/
│   └── features/
│
├── main.py
└── requirements.txt
```

---

# 🧠 M12-এর সবচেয়ে Important Concepts

এইগুলো অবশ্যই ভালোভাবে বুঝবে:

```text
1. Historical Price
2. Price Change
3. Price Change %
4. Price Drop
5. Significant Price Drop
6. Historical Min
7. Historical Max
8. Historical Average
9. Moving Average
10. Rolling Statistics
11. Volatility
12. Coefficient of Variation
13. Trend
14. Trend Slope
15. Price Position
16. Historical Low
17. Good Deal
18. Deal Score
19. Lag Features
20. Forecasting Dataset
21. Time Features
22. Data Leakage
23. Time-Based Train/Test Split
```

---

# ✅ M12 Mastery Checklist

নিজেকে test করো:

### Basic

* [ ] Historical price কী?
* [ ] `groupby().shift()` বুঝি?
* [ ] `groupby().diff()` বুঝি?
* [ ] Price change বের করতে পারি?
* [ ] Percentage change বের করতে পারি?

### Intermediate

* [ ] Historical min/max/average বের করতে পারি?
* [ ] Moving average বুঝি?
* [ ] Rolling statistics বুঝি?
* [ ] Volatility বুঝি?
* [ ] CV calculate করতে পারি?
* [ ] Price trend detect করতে পারি?

### Advanced

* [ ] Trend slope calculate করতে পারি?
* [ ] Price drop event detect করতে পারি?
* [ ] Historical low detect করতে পারি?
* [ ] Real deal বনাম advertised discount বুঝি?
* [ ] Deal score বানাতে পারি?
* [ ] Lag features তৈরি করতে পারি?
* [ ] Forecasting dataset তৈরি করতে পারি?
* [ ] Data leakage বুঝি?
* [ ] Time-based train/test split করতে পারি?

---

# 🔥 M08 → M12 পর্যন্ত তোমার পুরো Data Pipeline

এখন পর্যন্ত তুমি একটি খুব শক্তিশালী e-commerce data system-এর foundation তৈরি করেছ:

```text
M01
Requests
  ↓
M02
BeautifulSoup
  ↓
M03
Pagination + URL Traversal
  ↓
M04
Cleaning + Normalization
  ↓
M05
Playwright
  ↓
M06
API Extraction
  ↓
M07
Multi-Site Architecture
  ↓
M08
PostgreSQL
  ↓
M09
PostgreSQL + Pandas Analytics
  ↓
M10
Product Matching
  ↓
M11
Feature Engineering
  ↓
M12
PRICE INTELLIGENCE
  ↓
Historical Analysis
  ↓
Trend + Volatility
  ↓
Deal Detection
  ↓
Forecasting Dataset
```

### M12-এর মূল transformation:

```text
"Product price কত?"
          ↓
"Price কত ছিল?"
          ↓
"Price কীভাবে পরিবর্তন হচ্ছে?"
          ↓
"Price কেন/কতটা fluctuate করছে?"
          ↓
"এখন price historically ভালো অবস্থানে আছে?"
          ↓
"এটা কি সত্যিকারের good deal?"
          ↓
"আগামীতে price কোথায় যেতে পারে?"
```

**এখান থেকেই e-commerce data collection project একটি সাধারণ scraper না থেকে একটি real-world Data Analytics / Data Intelligence project-এ পরিণত হচ্ছে।**


---
হ্যাঁ, **অনেক ধরনের website থেকে data collect করতে পারবে**, কিন্তু **যেকোনো website থেকে যেকোনোভাবে data collect করা যাবে—এটা ঠিক নয়।**

তুমি যেহেতু Data Analytics + E-commerce Data Collection শিখছো, একটা practical rule মনে রাখো:

> **Publicly accessible data + website/API-এর rules মেনে collection = সাধারণত safe approach.**

### কোন website থেকে কীভাবে?

| Website type           | Technique                             |
| ---------------------- | ------------------------------------- |
| Static HTML            | `Requests + BeautifulSoup`            |
| Pagination website     | `Requests + BeautifulSoup`            |
| JavaScript website     | `Playwright`                          |
| Public API             | `Requests + JSON`                     |
| Infinite scroll        | Playwright / available API            |
| E-commerce             | API → Requests → Playwright fallback  |
| নিজের website          | যেকোনো appropriate method             |
| Authorized/private API | API credentials + official rules মেনে |

### Example

ধরো একটি public product page:

```text
https://example.com/products
```

তুমি collect করতে পারো:

```text
Product Name
Price
Original Price
Discount
Rating
Review Count
Category
Brand
Product URL
Image URL
Availability
```

তারপর:

```text
Website
   ↓
Requests / API / Playwright
   ↓
Raw Data
   ↓
BeautifulSoup / JSON Parser
   ↓
Cleaning
   ↓
PostgreSQL
   ↓
Pandas
   ↓
Analytics
   ↓
Price Intelligence
```

### কিন্তু কিছু জিনিস করা উচিত নয়

যেমন:

* Login/authentication bypass করা
* CAPTCHA bypass করা
* Anti-bot/security system bypass করা
* Private/non-public data সংগ্রহ করা
* Website-এর Terms of Service নিষেধ করলে সেই restriction উপেক্ষা করা
* Excessive requests দিয়ে website overload করা

`robots.txt` এবং Terms of Service-কে আগে দেখে নেওয়া ভালো; `robots.txt` নিজে আইন নয়, তবে site owner's crawling preferences-এর গুরুত্বপূর্ণ signal।

### তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ skill

তোমার এখন লক্ষ্য হওয়া উচিত **"আমি যেকোনো website scrape করব"** না।

বরং:

```text
Website
   ↓
Inspect
   ↓
Data কোথায় আছে?
   ├── HTML → BeautifulSoup
   ├── API → Requests
   ├── JavaScript DOM → Playwright
   └── Embedded JSON → JSON extraction
   ↓
Parser
   ↓
Cleaner
   ↓
Database
```

এটা master করতে পারলে **নতুন website দেখেই কোন technique ব্যবহার করতে হবে সেটা নিজে সিদ্ধান্ত নিতে পারবে।**

চাইলে **M13 — Any Website Data Collection Mastery**-তে আমরা একটি website দেখে **কীভাবে HTML/API/JavaScript identify করে সঠিক scraping method নির্বাচন করতে হয়**, সেটা একদম বাস্তব workflow দিয়ে শিখতে পারি।


----
# M13 — Any Website Data Collection Mastery 🌐

M12 পর্যন্ত আমরা **E-commerce Price Intelligence** তৈরি করেছি। এখন M13-এ আমরা একটি বড় skill শিখব:

> **নতুন কোনো website দেখার পর কীভাবে বুঝবে data কোথায় আছে, কোন extraction method ব্যবহার করবে, কোন selector/API খুঁজবে, এবং পুরো collection pipeline তৈরি করবে।**

এটা তোমার জন্য খুব গুরুত্বপূর্ণ, কারণ বাস্তবে **প্রতিটি website-এর HTML structure আলাদা**।

---

# 🎯 M13 শেষে তুমি পারবে

* যেকোনো website inspect করতে
* Static vs Dynamic website identify করতে
* HTML থেকে data খুঁজে বের করতে
* CSS selector তৈরি করতে
* API endpoint identify করতে
* JSON response বুঝতে
* Embedded JSON খুঁজে বের করতে
* Pagination detect করতে
* Product/list/detail structure বুঝতে
* `Requests`, `BeautifulSoup`, `Playwright`, API-এর মধ্যে সঠিক method নির্বাচন করতে
* একটি নতুন website-এর জন্য scraper architecture তৈরি করতে
* scraper failure debug করতে
* common website patterns handle করতে

---

# 1. প্রথম Rule — Website দেখেই Code লিখবে না

অনেকে scraper বানানোর সময় সরাসরি:

```python
requests.get(url)
```

দিয়ে শুরু করে।

এটা সবসময় best approach নয়।

প্রথমে প্রশ্ন:

```text
Website
   ↓
Data কোথায়?
   ├── HTML?
   ├── API?
   ├── Embedded JSON?
   ├── JavaScript generated?
   └── অন্য কোনো public data source?
```

তারপর method নির্বাচন করবে।

---

# 2. Website Inspection Workflow

একটি নতুন website পেলে এই workflow follow করবে:

```text
STEP 1
Open Website
      ↓
STEP 2
Inspect Page
      ↓
STEP 3
Search Target Data
      ↓
STEP 4
Check HTML
      ↓
STEP 5
Check Network
      ↓
STEP 6
Identify Data Source
      ↓
STEP 7
Choose Extraction Method
      ↓
STEP 8
Build Parser
      ↓
STEP 9
Test
      ↓
STEP 10
Pagination / Detail Pages
      ↓
STEP 11
Cleaning
      ↓
STEP 12
Database
```

এটাই তোমার **universal scraping workflow**।

---

# 3. Website-এর Data কোথায় থাকতে পারে?

ধরো তুমি দেখতে পাচ্ছ:

```text
iPhone 16
৳80,000
4.7 ⭐
125 Reviews
```

এই data browser-এ দেখা যাচ্ছে।

কিন্তু data আসতে পারে:

### Method 1 — HTML

```html
<div class="product">
    <h2>iPhone 16</h2>
    <span class="price">৳80,000</span>
</div>
```

### Method 2 — API

```json
{
    "name": "iPhone 16",
    "price": 80000
}
```

### Method 3 — Embedded JSON

```html
<script type="application/json">
{
    "name": "iPhone 16",
    "price": 80000
}
</script>
```

### Method 4 — JavaScript generated DOM

Initial HTML:

```html
<div id="products"></div>
```

JavaScript পরে:

```text
API → JSON → JavaScript → DOM
```

---

# 4. Static Website Identify

প্রথমে simple test:

```python
import requests

url = "https://example.com"

response = requests.get(
    url,
    timeout=20,
    headers={
        "User-Agent": "Mozilla/5.0"
    }
)

print(response.status_code)
print(len(response.text))
```

তারপর:

```python
print(response.text[:1000])
```

যদি target data HTML-এর মধ্যে পাওয়া যায়:

```text
Requests
   ↓
HTML
   ↓
BeautifulSoup
```

তাহলে Playwright দরকার নাও হতে পারে।

---

# 5. BeautifulSoup দিয়ে Search

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(
    response.text,
    "html.parser"
)

print(soup.get_text(" ", strip=True)[:2000])
```

তারপর browser-এর visible content-এর সাথে compare করবে।

যদি browser-এ:

```text
iPhone 16
```

দেখায় কিন্তু:

```python
"iPhone 16" in response.text
```

হয়:

```text
False
```

তাহলে সম্ভবত JavaScript/API involved।

---

# 6. Quick Diagnostic

```python
target = "iPhone 16"

if target in response.text:
    print("Data exists in raw HTML")
else:
    print("Data not found in raw HTML")
```

এটা খুব basic কিন্তু useful diagnostic।

---

# 7. DevTools দিয়ে HTML Inspect

Browser-এ:

```text
Right Click
    ↓
Inspect
```

তারপর:

```text
Elements
```

Target product-এর উপর click করো।

ধরো:

```html
<div class="product-card">
```

তার ভিতরে:

```html
<h2 class="product-title">
    iPhone 16
</h2>

<span class="price">
    ৳80,000
</span>
```

তাহলে:

```python
card = soup.select_one(".product-card")

name = card.select_one(".product-title").get_text(
    strip=True
)

price = card.select_one(".price").get_text(
    strip=True
)
```

---

# 8. CSS Selector Skill

এটা M13-এর অন্যতম important skill।

### Class

```css
.product-card
```

### ID

```css
#product-list
```

### Tag

```css
h2
```

### Nested

```css
.product-card .product-title
```

### Attribute

```css
a[href]
```

### Specific attribute

```css
img[data-src]
```

---

# 9. Multiple Products

ধরো:

```html
<div class="product-card">
...
</div>

<div class="product-card">
...
</div>
```

Python:

```python
products = soup.select(".product-card")
```

তারপর:

```python
for product in products:

    name = product.select_one(
        ".product-title"
    )

    price = product.select_one(
        ".price"
    )

    print(
        name.get_text(strip=True)
        if name else None
    )

    print(
        price.get_text(strip=True)
        if price else None
    )
```

---

# 10. Robust Selector

এইটা খুব important।

ধরো:

```css
div.container div.row div.col-md-4 div.product-card
```

এটা খুব long selector।

Website সামান্য পরিবর্তন করলে scraper break করতে পারে।

Better:

```css
.product-card
```

অথবা:

```css
.product-card .product-title
```

### Rule

> **যতটা সম্ভব stable selector ব্যবহার করবে।**

---

# 11. Dynamic Website Detect

ধরো:

```python
response = requests.get(url)

print("iPhone 16" in response.text)
```

Output:

```text
False
```

কিন্তু browser-এ product দেখা যাচ্ছে।

এখন সম্ভাবনা:

```text
JavaScript
```

তখন:

```text
Browser
   ↓
JavaScript
   ↓
Data
```

---

# 12. Playwright দিয়ে Test

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:

    browser = p.chromium.launch(
        headless=True
    )

    page = browser.new_page()

    page.goto(
        url,
        wait_until="domcontentloaded"
    )

    page.wait_for_selector(
        ".product-card"
    )

    html = page.content()

    browser.close()
```

তারপর:

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(
    html,
    "html.parser"
)
```

এখন আবার:

```python
print(
    "iPhone 16" in soup.get_text(
        " ",
        strip=True
    )
)
```

---

# 13. Requests বনাম Playwright

এই decision tree মনে রাখবে:

```text
Can Requests get target data?
          │
       YES
          ↓
Requests + BeautifulSoup
          
       NO
          ↓
Is data loaded by JavaScript?
          │
       YES
          ↓
Check Network/API first
          │
          ├── Public/authorized API → Requests
          │
          └── No suitable API → Playwright
```

### Priority

আমি সাধারণত এই order recommend করব:

```text
1. Public/authorized API
2. Static HTML
3. Embedded JSON
4. Playwright
```

কারণ browser automation তুলনামূলকভাবে expensive।

---

# 14. Network Tab — সবচেয়ে Powerful Skill

Chrome:

```text
Inspect
   ↓
Network
   ↓
Fetch/XHR
   ↓
Reload
```

এখন website-এর background requests দেখতে পারবে।

ধরো দেখতে পেলে:

```text
GET /api/products?page=1
```

Response:

```json
{
    "products": [
        {
            "id": 101,
            "name": "iPhone 16",
            "price": 80000
        }
    ]
}
```

এখন HTML scrape করার দরকার নাও হতে পারে।

---

# 15. API Extraction

```python
import requests

api_url = "https://example.com/api/products"

response = requests.get(
    api_url,
    timeout=20
)

response.raise_for_status()

data = response.json()

print(data)
```

---

# 16. JSON Structure বুঝতে হবে

ধরো:

```json
{
    "data": {
        "products": [
            {
                "id": 101,
                "name": "iPhone 16",
                "price": 80000
            }
        ]
    }
}
```

Python:

```python
products = data["data"]["products"]
```

তারপর:

```python
for product in products:

    print(product["name"])
    print(product["price"])
```

---

# 17. Safe JSON Extraction

সবসময় ধরে নেবে না যে key থাকবে।

খারাপ:

```python
name = product["name"]
```

Better:

```python
name = product.get("name")
```

Nested:

```python
price = (
    product
    .get("pricing", {})
    .get("current")
)
```

---

# 18. API Pagination

API হতে পারে:

```text
/api/products?page=1
/api/products?page=2
/api/products?page=3
```

Python:

```python
all_products = []

for page_number in range(1, 11):

    params = {
        "page": page_number
    }

    response = requests.get(
        api_url,
        params=params,
        timeout=20
    )

    response.raise_for_status()

    data = response.json()

    products = data.get(
        "products",
        []
    )

    if not products:
        break

    all_products.extend(products)
```

---

# 19. API Pagination আরও ভালোভাবে

অনেক API response দেয়:

```json
{
    "products": [...],
    "page": 1,
    "total_pages": 25
}
```

তাহলে:

```python
data = response.json()

total_pages = data.get(
    "total_pages",
    1
)
```

তারপর:

```python
for page_number in range(
    1,
    total_pages + 1
):
    ...
```

---

# 20. Cursor Pagination

সব API page number ব্যবহার করে না।

Example:

```json
{
    "data": [...],
    "next_cursor": "abc123"
}
```

পরের request:

```python
params = {
    "cursor": "abc123"
}
```

Flow:

```text
Request
 ↓
Data
 ↓
next_cursor
 ↓
Request
 ↓
Data
 ↓
next_cursor
 ↓
...
```

এটাকে **cursor-based pagination** বলে।

---

# 21. Embedded JSON

অনেক modern website initial HTML-এর মধ্যে JSON রেখে দেয়।

Example:

```html
<script type="application/json" id="product-data">
{
    "name": "Laptop",
    "price": 75000
}
</script>
```

BeautifulSoup:

```python
script = soup.select_one(
    "#product-data"
)
```

তারপর:

```python
import json

data = json.loads(
    script.string
)
```

---

# 22. JSON-LD

Product websites-এ খুব useful।

অনেক website এ:

```html
<script type="application/ld+json">
{
    "@type": "Product",
    "name": "Example Product",
    "offers": {
        "price": "80000"
    }
}
</script>
```

Extract:

```python
scripts = soup.select(
    'script[type="application/ld+json"]'
)
```

তারপর:

```python
import json

for script in scripts:

    try:
        data = json.loads(
            script.get_text()
        )

        print(data)

    except json.JSONDecodeError:
        continue
```

এটা product metadata-এর জন্য useful source হতে পারে।

---

# 23. Product Detail Page Discovery

Category page:

```text
/category/phones
```

এর মধ্যে:

```html
<a href="/product/iphone-16">
```

Extract:

```python
from urllib.parse import urljoin

links = soup.select(
    ".product-card a"
)

product_urls = []

for link in links:

    href = link.get("href")

    if href:
        product_urls.append(
            urljoin(
                url,
                href
            )
        )
```

---

# 24. URL Deduplication

```python
product_urls = list(
    set(product_urls)
)
```

Better deterministic approach:

```python
product_urls = list(
    dict.fromkeys(product_urls)
)
```

এতে order preserve হয়।

---

# 25. Category → Product → Detail

Real-world structure:

```text
Homepage
   ↓
Category
   ↓
Pagination
   ↓
Product URLs
   ↓
Product Detail
   ↓
Product Data
```

Code architecture:

```python
for category_url in category_urls:

    product_urls = scrape_category(
        category_url
    )

    for product_url in product_urls:

        product = scrape_product(
            product_url
        )

        save_product(product)
```

---

# 26. Website-এর Data Model আগে বুঝবে

ধরো website-এ:

```text
Category
 ├── Phones
 ├── Laptops
 └── Tablets
```

Product:

```text
Product
 ├── Name
 ├── Brand
 ├── Price
 ├── Rating
 ├── Reviews
 ├── Availability
 └── Variants
```

Variant:

```text
Storage
Color
RAM
```

তাহলে scraper-এ সবকিছু flat করা সবসময় ভালো design নয়।

---

# 27. Product Variant

Example:

```text
iPhone 16

128GB Black
128GB Blue
256GB Black
256GB Blue
```

এগুলো potentially different sellable variants।

তাই:

```text
Master Product
      ↓
Variants
      ↓
Offers/Sellers
      ↓
Price History
```

এই data model M10-এর product matching-এর সাথে directly related।

---

# 28. Price Selector Problem

ধরো HTML:

```html
<span class="price">
    ৳80,000
</span>
```

তুমি:

```python
price = soup.select_one(
    ".price"
)
```

করলে কাজ করছে।

কিন্তু website redesign করে:

```html
<div class="current-price">
    ৳80,000
</div>
```

করল।

তখন scraper break করবে।

এজন্য:

> **Selectors are website-specific and must be tested/maintained.**

---

# 29. Fallback Selectors

কিছু ক্ষেত্রে:

```python
def extract_price(product):

    selectors = [
        ".current-price",
        ".sale-price",
        ".price",
        "[data-price]"
    ]

    for selector in selectors:

        element = product.select_one(
            selector
        )

        if element:

            value = (
                element.get_text(
                    " ",
                    strip=True
                )
            )

            if value:
                return value

    return None
```

এটা scraper robustness বাড়ায়।

---

# 30. Extraction Function Design

Bad:

```python
def scrape():
    # 300 lines
```

Better:

```text
fetch_page()
extract_products()
extract_name()
extract_price()
extract_rating()
extract_url()
clean_product()
validate_product()
save_product()
```

---

# 31. Universal Product Parser

```python
def parse_product(card):

    return {
        "name": extract_name(card),
        "price": extract_price(card),
        "rating": extract_rating(card),
        "review_count": extract_reviews(card),
        "url": extract_url(card),
        "image_url": extract_image(card)
    }
```

এতে code maintain করা সহজ হয়।

---

# 32. Error Handling

একটি product-এ rating missing হতে পারে।

তাই:

```python
try:

    rating = extract_rating(card)

except Exception:
    rating = None
```

কিন্তু আরও ভালো:

```python
def safe_text(element):

    if not element:
        return None

    return element.get_text(
        " ",
        strip=True
    )
```

---

# 33. Logging

`print()` দিয়ে production scraper চালানো ঠিক নয়।

Use:

```python
import logging

logging.basicConfig(
    level=logging.INFO
)

logger = logging.getLogger(
    __name__
)
```

তারপর:

```python
logger.info(
    "Scraping started"
)
```

Error:

```python
logger.error(
    "Failed to parse product"
)
```

---

# 34. Request Retry

Temporary error হলে retry করতে পারো।

Concept:

```text
Request
 ↓
Failed?
 ↓ YES
Wait
 ↓
Retry
 ↓
Failed?
 ↓
Retry
```

Simple:

```python
import time
import requests


def fetch_page(url, retries=3):

    for attempt in range(retries):

        try:

            response = requests.get(
                url,
                timeout=20,
                headers={
                    "User-Agent": "Mozilla/5.0"
                }
            )

            response.raise_for_status()

            return response.text

        except requests.RequestException:

            if attempt == retries - 1:
                raise

            time.sleep(
                2 ** attempt
            )
```

---

# 35. Rate Limiting

ধরো:

```python
for url in urls:

    scrape(url)
```

এভাবে হাজার হাজার request দ্রুত পাঠানো উচিত নয়।

Better:

```python
import time

for url in urls:

    scrape(url)

    time.sleep(1)
```

Real interval site-এর rules, load, and allowed crawling behavior অনুযায়ী রাখতে হবে।

---

# 36. 429 Error

```text
HTTP 429
Too Many Requests
```

মানে server বলছে:

> Requests too frequent.

তখন:

```text
STOP / SLOW DOWN
```

করতে হবে।

Response header-এ `Retry-After` থাকলে সেটার নির্দেশনা follow করা ভালো।

---

# 37. HTTP Status Handling

```python
if response.status_code == 200:
    print("Success")

elif response.status_code == 404:
    print("Not Found")

elif response.status_code == 429:
    print("Rate Limited")

elif response.status_code >= 500:
    print("Server Error")
```

---

# 38. Website Failure Classification

Scraper debugging-এর জন্য:

```text
Request Failure
     ↓
HTML Failure
     ↓
Selector Failure
     ↓
Parsing Failure
     ↓
Cleaning Failure
     ↓
Validation Failure
     ↓
Database Failure
```

প্রতিটি layer আলাদা করে debug করবে।

---

# 39. Data Validation

Scrape করার পর immediately validate:

```python
def validate_product(product):

    if not product.get("name"):
        return False

    if product.get("price") is not None:

        if product["price"] <= 0:
            return False

    return True
```

---

# 40. Raw Data Save করা

খুব important।

Scraping-এর পরে শুধু cleaned data save করবে না।

```text
data/
├── raw/
│   └── site_a_2026_09_07.json
│
└── cleaned/
    └── products.csv
```

কারণ parser bug হলে raw data থেকে আবার process করতে পারবে।

---

# 41. Raw JSON Example

```python
import json

with open(
    "data/raw/products.json",
    "w",
    encoding="utf-8"
) as f:

    json.dump(
        products,
        f,
        ensure_ascii=False,
        indent=2
    )
```

---

# 42. Pandas Export

```python
import pandas as pd

df = pd.DataFrame(products)

df.to_csv(
    "data/cleaned/products.csv",
    index=False
)
```

---

# 43. Website → PostgreSQL

Final pipeline:

```text
Website
   ↓
Fetcher
   ↓
Parser
   ↓
Cleaner
   ↓
Validator
   ↓
Product Matching
   ↓
PostgreSQL
```

এটাই M01–M13-এর combined architecture।

---

# 44. Universal Scraper Decision Tree

এটা মুখস্থ করার মতো:

```text
                 WEBSITE
                    │
                    ↓
             Inspect Website
                    │
                    ↓
        Is data in HTML source?
              /           \
            YES            NO
             │              │
             ↓              ↓
       BeautifulSoup    Check Network
                            │
                            ↓
                     Public/authorized
                       data endpoint?
                       /          \
                     YES          NO
                      │            │
                      ↓            ↓
                  Requests      Playwright
                   + JSON
```

আর embedded JSON থাকলে:

```text
HTML
 ↓
Embedded JSON?
 ↓ YES
JSON Parser
```

---

# 45. Example — Complete Static Website Scraper

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin


def fetch(url):

    response = requests.get(
        url,
        timeout=20,
        headers={
            "User-Agent": "Mozilla/5.0"
        }
    )

    response.raise_for_status()

    return response.text


def parse_products(html, base_url):

    soup = BeautifulSoup(
        html,
        "html.parser"
    )

    cards = soup.select(
        ".product-card"
    )

    products = []

    for card in cards:

        name_el = card.select_one(
            ".product-title"
        )

        price_el = card.select_one(
            ".price"
        )

        link_el = card.select_one(
            "a"
        )

        product = {
            "name": (
                name_el.get_text(
                    strip=True
                )
                if name_el else None
            ),

            "price": (
                price_el.get_text(
                    strip=True
                )
                if price_el else None
            ),

            "url": (
                urljoin(
                    base_url,
                    link_el.get("href")
                )
                if link_el and link_el.get("href")
                else None
            )
        }

        products.append(product)

    return products
```

---

# 46. Complete Website Collector

```python
def scrape_category(url):

    html = fetch(url)

    products = parse_products(
        html,
        url
    )

    return products
```

Run:

```python
products = scrape_category(
    "https://example.com/products"
)

for product in products:
    print(product)
```

---

# 47. Multiple Pages

```python
all_products = []

for page_number in range(1, 11):

    url = (
        f"https://example.com/products"
        f"?page={page_number}"
    )

    products = scrape_category(url)

    if not products:
        break

    all_products.extend(products)
```

---

# 48. M13-এর Real Skill

তোমাকে এখন আর শুধু:

> "BeautifulSoup কী?"

শিখলে হবে না।

তোমাকে চিনতে হবে:

```text
Website A
→ HTML

Website B
→ API

Website C
→ JavaScript

Website D
→ Embedded JSON

Website E
→ API + HTML

Website F
→ Category → Product → Detail
```

এটাই professional-level scraping skill।

---

# 49. Scraper Method Comparison

| Method        | Speed | Complexity | Best Use          |
| ------------- | ----- | ---------- | ----------------- |
| Requests      | ⭐⭐⭐⭐⭐ | Low        | Static HTML/API   |
| BeautifulSoup | ⭐⭐⭐⭐⭐ | Low        | HTML parsing      |
| API           | ⭐⭐⭐⭐⭐ | Medium     | Structured data   |
| Playwright    | ⭐⭐    | High       | JS-rendered pages |
| Pandas        | —     | Low        | Data analysis     |
| PostgreSQL    | —     | Medium     | Storage/history   |

---

# 50. M13 Mini Project 🚀

এখন একটি **Universal E-commerce Collector** বানাবে।

Target:

```text
3 Websites
```

প্রতিটির method আলাদা:

```text
Site A → HTML
Site B → API
Site C → JavaScript
```

Architecture:

```text
                    main.py
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       Site A        Site B       Site C
          ↓            ↓            ↓
    BeautifulSoup     API       Playwright
          ↓            ↓            ↓
          └────────────┼────────────┘
                       ↓
                Common Schema
                       ↓
                    Cleaner
                       ↓
                   Validator
                       ↓
              Product Matching
                       ↓
                  PostgreSQL
                       ↓
                    Pandas
                       ↓
                  Analytics
```

---

# 51. Common Schema

সব website-এর data শেষ পর্যন্ত:

```python
{
    "source": "",
    "product_id": "",
    "master_product_id": None,
    "name": "",
    "brand": "",
    "category": "",
    "price": None,
    "original_price": None,
    "discount": None,
    "rating": None,
    "review_count": None,
    "availability": "",
    "product_url": "",
    "image_url": "",
    "description": "",
    "scraped_at": ""
}
```

এখানেই M07 architecture-এর power দেখা যাচ্ছে।

---

# 52. Folder Structure

M13-এর পরে তোমার project:

```text
ecommerce_data_collector/
│
├── scrapers/
│   ├── base.py
│   ├── site_a.py
│   ├── site_b.py
│   └── site_c.py
│
├── parsers/
│   ├── site_a_parser.py
│   ├── site_b_parser.py
│   └── site_c_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── matching/
│   ├── normalize.py
│   ├── attributes.py
│   ├── candidates.py
│   └── matcher.py
│
├── database/
│   ├── connection.py
│   ├── products.py
│   └── prices.py
│
├── analytics/
│   ├── price_history.py
│   ├── price_trend.py
│   ├── volatility.py
│   └── deal_detection.py
│
├── data/
│   ├── raw/
│   ├── cleaned/
│   └── features/
│
├── logs/
│
├── config/
│   └── settings.py
│
├── main.py
└── requirements.txt
```

---

# 53. M13 Mastery Checklist ✅

### Website Inspection

* [ ] DevTools ব্যবহার করতে পারি
* [ ] Elements inspect করতে পারি
* [ ] HTML source বুঝতে পারি
* [ ] Static vs Dynamic identify করতে পারি
* [ ] Network tab ব্যবহার করতে পারি

### Extraction

* [ ] Requests
* [ ] BeautifulSoup
* [ ] CSS selectors
* [ ] Attribute extraction
* [ ] Embedded JSON
* [ ] JSON-LD
* [ ] API
* [ ] Pagination
* [ ] Cursor pagination
* [ ] Playwright

### Engineering

* [ ] Retry
* [ ] Timeout
* [ ] Logging
* [ ] Rate limiting
* [ ] Error handling
* [ ] Validation
* [ ] Raw data storage
* [ ] Common schema
* [ ] Modular scraper architecture

### Architecture

* [ ] Category → Product URLs
* [ ] Product → Detail page
* [ ] API → JSON → Parser
* [ ] Website-specific parser
* [ ] Common product model
* [ ] PostgreSQL storage

---

# 🔥 এখন পর্যন্ত তোমার Learning Journey

```text
M01  Requests
 ↓
M02  BeautifulSoup
 ↓
M03  Pagination
 ↓
M04  Cleaning
 ↓
M05  Playwright
 ↓
M06  API Extraction
 ↓
M07  Multi-Website Architecture
 ↓
M08  PostgreSQL
 ↓
M09  Pandas Analytics
 ↓
M10  Product Matching
 ↓
M11  Feature Engineering
 ↓
M12  Price Intelligence
 ↓
M13  Any Website Collection
```

### M13-এর সবচেয়ে বড় takeaway:

```text
Don't ask:

"How do I scrape this website?"

Ask:

"Where does this website get its data from?"
                    ↓
              HTML / API / JSON / JS
                    ↓
             Choose the right tool
```

এই mindset তৈরি হয়ে গেলে নতুন website-এর scraper বানানো অনেক সহজ হয়ে যাবে।

**পরের logical step M14 — Scraping at Scale: Automation, Scheduling, Incremental Crawling & Data Pipeline**। সেখানে আমরা দেখব কীভাবে ১টা website একবার scrape করা থেকে **প্রতিদিন/প্রতি ঘণ্টায় automatically data collect করে PostgreSQL-এ historical records maintain** করা যায়।


---
# M14 — Scraping at Scale: Automation, Scheduling & Incremental Data Pipeline 🚀

M13-এ আমরা শিখেছি **একটি নতুন website দেখে কীভাবে extraction method নির্বাচন করতে হয়**।

এখন M14-এ আমরা সেই scraper-কে production-style system বানাব।

আমাদের লক্ষ্য:

> **একবার scraper চালানো নয়; বরং automatically নির্দিষ্ট interval-এ data collect করা, শুধু নতুন/পরিবর্তিত data process করা, PostgreSQL-এ history রাখা, failure handle করা এবং পুরো pipeline monitor করা।**

---

# 🎯 M14 Learning Goals

এই module শেষে তুমি পারবে:

* Automated scraping pipeline বানাতে
* Scheduled scraping করতে
* Cron ব্যবহার করতে
* Incremental crawling বুঝতে
* Full scrape বনাম incremental scrape বুঝতে
* `last_seen` / `last_scraped` tracking করতে
* নতুন product detect করতে
* Price change detect করতে
* Historical snapshots রাখতে
* Duplicate data prevent করতে
* Retry + backoff implement করতে
* Logging করতে
* Failed jobs track করতে
* Multiple website sequential/parallel collection বুঝতে
* ETL pipeline তৈরি করতে
* Scraper → PostgreSQL automation তৈরি করতে

---

# 1. Manual Scraping বনাম Automated Scraping

এখন পর্যন্ত:

```text
তুমি command চালালে
      ↓
scraper চলল
      ↓
data collect হলো
```

এটা manual scraping।

কিন্তু real-world system:

```text
Scheduler
   ↓
Scraper
   ↓
Parser
   ↓
Cleaner
   ↓
Validator
   ↓
Database
   ↓
Analytics
```

Scheduler নিজে scraper চালাবে।

---

# 2. Real-world Example

ধরো তুমি 3টি e-commerce website monitor করছ:

```text
Site A
Site B
Site C
```

তুমি চাও:

```text
প্রতি 6 ঘণ্টায়
      ↓
সব website scrape
      ↓
price update
      ↓
new products detect
      ↓
price history save
```

তাহলে:

```text
00:00 → Scrape
06:00 → Scrape
12:00 → Scrape
18:00 → Scrape
```

একদিনে:

```text
4 scraping jobs
```

---

# 3. Full Scrape বনাম Incremental Scrape

এটা M14-এর সবচেয়ে গুরুত্বপূর্ণ concept।

## Full Scrape

প্রতিবার:

```text
Website
 ↓
সব product
 ↓
সব data
 ↓
Database
```

যদি 100,000 products থাকে:

```text
100,000 products
```

প্রতিবার process করতে হবে।

---

# 4. Incremental Scrape

ধরো database-এ already আছে:

```text
100,000 products
```

আজ website-এ:

```text
500 নতুন products
2,000 price changes
```

তাহলে পুরো 100,000 আবার process করার দরকার নেই।

আমরা শুধু:

```text
New
+
Changed
```

data process করতে পারি।

এটাই:

> **Incremental Crawling / Incremental Data Collection**

---

# 5. কেন Incremental Scraping দরকার?

ধরো:

```text
Products = 1,000,000
```

প্রতিদিন full scrape করলে:

```text
1,000,000 × 30
=
30,000,000 product observations
```

কিন্তু যদি daily changed products মাত্র:

```text
20,000
```

তাহলে incremental approach অনেক efficient হতে পারে।

---

# 6. Database-এ Tracking

আমাদের `products` table-এ কিছু metadata যোগ করতে পারি:

```sql
ALTER TABLE products
ADD COLUMN first_seen_at TIMESTAMP,
ADD COLUMN last_seen_at TIMESTAMP,
ADD COLUMN last_scraped_at TIMESTAMP,
ADD COLUMN is_active BOOLEAN DEFAULT TRUE;
```

এখন আমরা বুঝতে পারব:

```text
first_seen_at
→ product প্রথম কখন দেখেছি

last_seen_at
→ সর্বশেষ কখন website-এ পেয়েছি

last_scraped_at
→ সর্বশেষ কখন process করেছি
```

---

# 7. Product Lifecycle

একটি product:

```text
Website
   ↓
First discovered
   ↓
Database
   ↓
Seen again
   ↓
Price changed?
   ├── YES → price_history
   └── NO
   ↓
Still available?
```

---

# 8. New Product Detection

ধরো website থেকে:

```python
external_product_id = "ABC123"
```

Database-এ নেই।

তাহলে:

```text
NEW PRODUCT
```

SQL:

```sql
SELECT id
FROM products
WHERE website_id = 1
AND external_product_id = 'ABC123';
```

যদি result না আসে:

```text
INSERT
```

---

# 9. Existing Product Detection

যদি পাওয়া যায়:

```text
ABC123 → product_id 5001
```

তাহলে নতুন product insert করবে না।

বরং:

```text
UPDATE product metadata
+
INSERT price snapshot
```

---

# 10. Unique Identity

M08-এ আমরা শিখেছিলাম:

```sql
UNIQUE (
    website_id,
    external_product_id
)
```

এটা incremental pipeline-এর জন্য অত্যন্ত important।

```text
Website A + ABC123
```

একবারই product record হবে।

---

# 11. Upsert

PostgreSQL:

```sql
INSERT INTO products (
    website_id,
    external_product_id,
    name,
    product_url,
    last_seen_at
)
VALUES (
    %s,
    %s,
    %s,
    %s,
    CURRENT_TIMESTAMP
)
ON CONFLICT (
    website_id,
    external_product_id
)
DO UPDATE SET
    name = EXCLUDED.name,
    product_url = EXCLUDED.product_url,
    last_seen_at = CURRENT_TIMESTAMP;
```

এটাই:

> **Upsert = Insert if new, Update if existing**

---

# 12. Price History আলাদা রাখবে

এটা খুব important architecture decision।

`products` table:

```text
Current product identity
```

`price_history`:

```text
Historical observations
```

Example:

```text
products
--------
id = 101
name = iPhone 16
```

Price history:

```text
product_id | price | scraped_at
-----------|-------|------------
101        | 85000 | Sep 1
101        | 84000 | Sep 2
101        | 82000 | Sep 3
101        | 80000 | Sep 4
```

---

# 13. প্রতিবার Price Snapshot Save করা

ধরো:

```python
product_id = 101
price = 80000
```

SQL:

```sql
INSERT INTO price_history (
    product_id,
    price,
    original_price,
    discount,
    rating,
    review_count,
    scraped_at
)
VALUES (
    %s,
    %s,
    %s,
    %s,
    %s,
    %s,
    CURRENT_TIMESTAMP
);
```

এতে historical timeline তৈরি হবে।

---

# 14. কিন্তু একই Price বারবার?

ধরো:

```text
Sep 1 → 80,000
Sep 2 → 80,000
Sep 3 → 80,000
Sep 4 → 80,000
```

তুমি কি চারটি snapshot রাখবে?

এটা business requirement-এর উপর নির্ভর করে।

### Option A — Every observation

```text
Every scrape → snapshot
```

Useful for:

* exact monitoring
* hourly data
* price availability analysis

### Option B — Only changed price

```text
Save only when price changes
```

Useful for:

* storage efficiency
* long-term historical trends

---

# 15. Only Price Changes Store

আগের price:

```sql
SELECT price
FROM price_history
WHERE product_id = %s
ORDER BY scraped_at DESC
LIMIT 1;
```

Python:

```python
previous_price = cursor.fetchone()
```

তারপর:

```python
if previous_price is None:
    save_price()

elif previous_price[0] != current_price:
    save_price()
```

---

# 16. Better Approach — Snapshot Policy

তুমি system-এ policy define করতে পারো:

```text
Every scrape
      ↓
Price changed?
 ├── YES → Save
 └── NO
      ↓
24 hours passed?
 ├── YES → Save snapshot
 └── NO → Skip
```

এতে:

* changes capture হবে
* long-term state-ও থাকবে

---

# 17. Scraping Job Table

Production system-এ scraping job track করা useful।

```sql
CREATE TABLE scrape_jobs (
    id BIGSERIAL PRIMARY KEY,

    website_id INTEGER
        REFERENCES websites(id),

    started_at TIMESTAMP,

    finished_at TIMESTAMP,

    status VARCHAR(30),

    products_found INTEGER DEFAULT 0,

    products_created INTEGER DEFAULT 0,

    products_updated INTEGER DEFAULT 0,

    errors_count INTEGER DEFAULT 0,

    error_message TEXT
);
```

---

# 18. Job Lifecycle

```text
PENDING
   ↓
RUNNING
   ↓
SUCCESS
```

Failure হলে:

```text
RUNNING
   ↓
FAILED
```

তাহলে database থেকে জানতে পারবে:

```text
কোন website?
কখন?
কত product?
কত error?
কেন failed?
```

---

# 19. Python Job Start

```python
def start_job(website_id):

    cursor.execute(
        """
        INSERT INTO scrape_jobs (
            website_id,
            started_at,
            status
        )
        VALUES (
            %s,
            CURRENT_TIMESTAMP,
            'RUNNING'
        )
        RETURNING id
        """,
        (website_id,)
    )

    return cursor.fetchone()[0]
```

---

# 20. Job Success

```python
def finish_job(
    job_id,
    products_found,
    products_created,
    products_updated,
    errors_count
):

    cursor.execute(
        """
        UPDATE scrape_jobs
        SET
            finished_at = CURRENT_TIMESTAMP,
            status = 'SUCCESS',
            products_found = %s,
            products_created = %s,
            products_updated = %s,
            errors_count = %s
        WHERE id = %s
        """,
        (
            products_found,
            products_created,
            products_updated,
            errors_count,
            job_id
        )
    )
```

---

# 21. Job Failure

```python
def fail_job(job_id, error_message):

    cursor.execute(
        """
        UPDATE scrape_jobs
        SET
            finished_at = CURRENT_TIMESTAMP,
            status = 'FAILED',
            error_message = %s
        WHERE id = %s
        """,
        (
            str(error_message),
            job_id
        )
    )
```

---

# 22. Main Pipeline

এখন পুরো system:

```python
def run_scraper():

    job_id = start_job(website_id)

    try:

        products = scraper.scrape()

        cleaned_products = []

        for product in products:

            cleaned = clean_product(
                product
            )

            if validate_product(cleaned):

                cleaned_products.append(
                    cleaned
                )

        save_products(
            cleaned_products
        )

        finish_job(
            job_id=job_id,
            products_found=len(products),
            products_created=created_count,
            products_updated=updated_count,
            errors_count=error_count
        )

    except Exception as e:

        fail_job(
            job_id,
            e
        )

        raise
```

---

# 23. Scheduling — Cron

Linux/Ubuntu-তে সবচেয়ে simple scheduler:

> **Cron**

Check:

```bash
crontab -e
```

---

# 24. প্রতি 6 ঘণ্টায় Run

```cron
0 */6 * * * /path/to/venv/bin/python /path/to/project/main.py
```

Meaning:

```text
0       → minute
*/6     → every 6 hours
*       → every day
*       → every month
*       → every weekday
```

---

# 25. প্রতিদিন রাত 2টায়

```cron
0 2 * * * /path/to/venv/bin/python /path/to/project/main.py
```

Meaning:

```text
02:00 AM
Every day
```

---

# 26. প্রতি ঘণ্টায়

```cron
0 * * * * /path/to/venv/bin/python /path/to/project/main.py
```

---

# 27. প্রতি 30 মিনিটে

```cron
*/30 * * * * /path/to/venv/bin/python /path/to/project/main.py
```

তবে scraping frequency website-এর rules, server load এবং permitted crawling behavior অনুযায়ী নির্ধারণ করবে।

---

# 28. Cron Log

Output file:

```cron
0 */6 * * * /path/to/venv/bin/python /path/to/project/main.py >> /path/to/project/logs/cron.log 2>&1
```

এতে:

```text
stdout
+
stderr
```

log file-এ যাবে।

---

# 29. Python Logging

```python
import logging

logging.basicConfig(
    filename="logs/scraper.log",
    level=logging.INFO,
    format=(
        "%(asctime)s "
        "%(levelname)s "
        "%(message)s"
    )
)

logger = logging.getLogger(__name__)
```

তারপর:

```python
logger.info(
    "Scraping started"
)
```

---

# 30. Useful Logging

```python
logger.info(
    f"Found {len(products)} products"
)
```

Product error:

```python
logger.error(
    f"Failed product: {url}"
)
```

Completion:

```python
logger.info(
    "Scraping completed successfully"
)
```

---

# 31. Retry with Exponential Backoff

M13-এ basic retry দেখেছিলাম।

এবার একটু better:

```python
import time
import requests


def fetch_with_retry(
    url,
    retries=3
):

    for attempt in range(retries):

        try:

            response = requests.get(
                url,
                timeout=20,
                headers={
                    "User-Agent": "Mozilla/5.0"
                }
            )

            response.raise_for_status()

            return response

        except requests.RequestException:

            if attempt == retries - 1:
                raise

            wait_time = 2 ** attempt

            time.sleep(
                wait_time
            )
```

Wait:

```text
Attempt 1 → 1 sec
Attempt 2 → 2 sec
Attempt 3 → 4 sec
```

---

# 32. Why Backoff?

Server temporary problem হলে:

```text
Request
 ↓
Failure
 ↓
Immediately request
 ↓
Failure
 ↓
Immediately request
 ↓
...
```

এটা ভালো আচরণ নয়।

Better:

```text
Failure
 ↓
Wait
 ↓
Retry
 ↓
Wait longer
 ↓
Retry
```

---

# 33. Website-Level Failure Isolation

ধরো:

```text
Site A → Success
Site B → Failed
Site C → Success
```

তাহলে পুরো pipeline বন্ধ করা উচিত নয়।

Bad:

```python
for site in sites:
    scrape(site)
```

একটি unhandled exception পুরো loop থামিয়ে দিতে পারে।

Better:

```python
for site in sites:

    try:

        scrape(site)

    except Exception as e:

        logger.error(
            f"{site} failed: {e}"
        )

        continue
```

---

# 34. Site-Level Architecture

```text
Main Scheduler
      ↓
┌─────┼─────┐
↓     ↓     ↓
A     B     C
↓     ↓     ↓
OK   FAIL   OK
      ↓
   Continue
```

এটা production system-এর জন্য খুব useful।

---

# 35. Scrape Configuration

Hardcode না করে configuration ব্যবহার করো।

```python
SITES = [
    {
        "name": "site_a",
        "enabled": True,
        "method": "html"
    },
    {
        "name": "site_b",
        "enabled": True,
        "method": "api"
    },
    {
        "name": "site_c",
        "enabled": False,
        "method": "playwright"
    }
]
```

তারপর:

```python
for site in SITES:

    if not site["enabled"]:
        continue

    run_site(site)
```

---

# 36. Environment Variables

Database password code-এ hardcode করা উচিত নয়।

`.env`:

```text
DATABASE_URL=postgresql+psycopg://...
```

Python:

```python
import os

DATABASE_URL = os.getenv(
    "DATABASE_URL"
)
```

Production system-এ secrets securely manage করবে।

---

# 37. Incremental Crawl Strategy

ধরো category page-এ 1000 products।

Database-এ:

```text
900 already known
100 new
```

তাহলে:

```text
Category page
      ↓
Extract URLs
      ↓
Compare known URLs/IDs
      ↓
New URLs
      ↓
Detail scraping
```

---

# 38. URL-Based Incremental Detection

```python
known_urls = {
    row["product_url"]
    for row in existing_products
}
```

তারপর:

```python
new_urls = [
    url
    for url in scraped_urls
    if url not in known_urls
]
```

এখন শুধু:

```text
new_urls
```

scrape করতে পারো।

---

# 39. কিন্তু শুধু URL ব্যবহার সবসময় যথেষ্ট নয়

একটি website URL পরিবর্তন করতে পারে:

```text
/product/iphone-16
```

থেকে:

```text
/product/apple-iphone-16
```

তখন URL আলাদা হলেও product একই।

তাই stronger identifier:

```text
GTIN
MPN
SKU
External Product ID
```

ব্যবহার করা ভালো।

এটা M10-এর entity resolution-এর সাথে directly connected।

---

# 40. Sitemap ব্যবহার

অনেক website public sitemap দেয়:

```text
/sitemap.xml
```

যদি allowed/publicly accessible হয়, সেখানে product URLs পাওয়া যেতে পারে।

Concept:

```text
Sitemap
 ↓
Product URLs
 ↓
Compare database
 ↓
New URLs
 ↓
Scrape
```

এটা category pagination-এর alternative হতে পারে।

---

# 41. Last Seen Logic

ধরো:

```text
Sep 1 → product seen
Sep 2 → product seen
Sep 3 → product missing
```

Missing মানেই immediately deleted নয়।

কারণ:

* temporary page failure
* pagination change
* product temporarily unavailable
* scraper bug

তাই:

```text
Missing once
    ↓
Don't immediately deactivate
```

---

# 42. Consecutive Missing Count

Products table-এ:

```sql
ALTER TABLE products
ADD COLUMN missing_count INTEGER DEFAULT 0;
```

যখন পাওয়া যায়:

```sql
UPDATE products
SET
    missing_count = 0,
    last_seen_at = CURRENT_TIMESTAMP,
    is_active = TRUE
WHERE id = %s;
```

না পাওয়া গেলে:

```sql
UPDATE products
SET missing_count = missing_count + 1
WHERE id = %s;
```

তারপর threshold:

```text
missing_count >= 3
```

হলে inactive করা যেতে পারে।

Business logic অনুযায়ী threshold নির্ধারণ করবে।

---

# 43. Product Availability Lifecycle

```text
ACTIVE
  ↓
Missing once
  ↓
ACTIVE
  ↓
Missing twice
  ↓
ACTIVE
  ↓
Missing 3 times
  ↓
INACTIVE
```

এতে false deactivation কমবে।

---

# 44. Price Monitoring Pipeline

এখন ধরো product:

```text
iPhone 16
```

প্রতিদিন:

```text
85K
84K
83K
80K
78K
```

Pipeline:

```text
New scrape
   ↓
Current price
   ↓
Previous price
   ↓
Compare
   ↓
Price changed?
   ↓
YES
   ↓
price_history INSERT
   ↓
Calculate drop %
   ↓
Significant?
   ↓
YES
   ↓
Alert/Analytics
```

---

# 45. M12 + M14 Integration

M12-তে আমরা পেয়েছিলাম:

```text
price_change_percent
historical_min
historical_avg
moving_average
volatility
deal_score
```

M14-এ এগুলো automatic হবে।

```text
Scheduler
 ↓
New Price
 ↓
Historical DB
 ↓
M12 Analytics
 ↓
Deal Score
 ↓
Price Alert
```

এটাই একটি real **Price Intelligence Pipeline**।

---

# 46. ETL Concept

M14 থেকে তোমার ETL concept শুরু হচ্ছে।

### E — Extract

```text
Website/API
```

### T — Transform

```text
Clean
Normalize
Validate
Match
Feature Engineering
```

### L — Load

```text
PostgreSQL
```

Full:

```text
Extract
   ↓
Transform
   ↓
Load
```

---

# 47. ELT-ও বুঝবে

কিছু system:

```text
Extract
 ↓
Load
 ↓
Transform
```

এটা:

> **ELT**

Modern data platforms-এ এই pattern খুব common।

তোমার current project-এ:

```text
Website
 ↓
Raw data
 ↓
PostgreSQL
 ↓
Pandas/SQL
 ↓
Analytics
```

এই pattern-ও ব্যবহার করতে পারো।

---

# 48. Data Pipeline Layers

তোমার project এখন:

```text
                SOURCE
                  ↓
        ┌──────────────────┐
        │ Website / API    │
        └──────────────────┘
                  ↓
              EXTRACT
                  ↓
        ┌──────────────────┐
        │ Raw Data         │
        └──────────────────┘
                  ↓
             TRANSFORM
                  ↓
        ┌──────────────────┐
        │ Clean + Match    │
        └──────────────────┘
                  ↓
                LOAD
                  ↓
        ┌──────────────────┐
        │ PostgreSQL       │
        └──────────────────┘
                  ↓
              ANALYTICS
                  ↓
        ┌──────────────────┐
        │ Pandas / SQL     │
        └──────────────────┘
```

---

# 49. Batch Processing

Cron-based scraping:

```text
02:00
 ↓
Job
 ↓
Finish
```

এটা:

> **Batch Processing**

তুমি নির্দিষ্ট interval-এ data process করছ।

---

# 50. Near Real-Time Concept

যদি প্রতি:

```text
5 minutes
```

data collect করো:

```text
Scheduler
 ↓
Every 5 minutes
 ↓
Scrape
 ↓
Database
```

এটা near-real-time monitoring-এর দিকে যাবে।

কিন্তু scraping frequency অবশ্যই source-এর permitted usage ও practical server load অনুযায়ী রাখতে হবে।

---

# 51. Parallel Scraping

ধরো:

```text
Site A → 10 min
Site B → 10 min
Site C → 10 min
```

Sequential:

```text
A → 10
B → 10
C → 10

Total ≈ 30 min
```

Parallel করলে potentially:

```text
A ─┐
B ─┼→ ≈ 10 min
C ─┘
```

কিন্তু concurrency website-এর rules, network limits এবং resource usage অনুযায়ী সীমিত রাখতে হবে।

---

# 52. ThreadPoolExecutor Example

I/O-bound requests-এর জন্য:

```python
from concurrent.futures import ThreadPoolExecutor


def scrape_site(site):

    return site.scrape()


with ThreadPoolExecutor(
    max_workers=3
) as executor:

    results = executor.map(
        scrape_site,
        sites
    )
```

এটা advanced optimization।

---

# 53. Parallel ≠ Always Better

ধরো:

```text
max_workers=100
```

এটা সবসময় ভালো নয়।

Problems:

```text
Too many requests
        ↓
Server load
        ↓
429
        ↓
Failures
```

তাই:

> **Controlled concurrency**

ব্যবহার করবে।

---

# 54. Database Transaction

একটি scrape job-এ:

```text
100 products
```

এর মধ্যে 50 save হওয়ার পর error হলো।

Transaction ব্যবহার করলে:

```text
BEGIN
 ↓
Insert/Update
 ↓
Error?
 ├── NO → COMMIT
 └── YES → ROLLBACK
```

Python:

```python
try:

    with connection.transaction():

        save_products(products)

except Exception as e:

    logger.error(e)
```

---

# 55. Idempotency

এটা professional data engineering-এর খুব গুরুত্বপূর্ণ concept।

ধরো একই job দুইবার run হলো।

```text
Job A
Job A আবার
```

তবুও database corrupt হওয়া উচিত নয়।

Example:

```sql
UNIQUE (
    website_id,
    external_product_id
)
```

এবং upsert ব্যবহার করে:

```text
Same input
+
Same state
=
Safe repeated execution
```

এটাই idempotent behavior-এর একটি practical example।

---

# 56. Scrape Run ID

আরও advancedভাবে:

```sql
ALTER TABLE price_history
ADD COLUMN scrape_job_id BIGINT
REFERENCES scrape_jobs(id);
```

তাহলে প্রতিটি observation জানতে পারবে:

```text
কোন scrape job থেকে এসেছে?
```

Example:

```text
price_history
--------------------------------
product_id
price
scraped_at
scrape_job_id
```

---

# 57. Data Lineage

এখন তোমার data-এর lineage:

```text
Website
 ↓
Scrape Job #105
 ↓
Raw Data
 ↓
Parser
 ↓
Cleaner
 ↓
Product #501
 ↓
Price History
```

এটা future debugging-এর জন্য অত্যন্ত useful।

---

# 58. M14 Complete Architecture

```text
                    SCHEDULER
                       │
                       ↓
                  SCRAPE JOB
                       │
             ┌─────────┼─────────┐
             ↓         ↓         ↓
          Site A     Site B    Site C
             ↓         ↓         ↓
          Fetch      Fetch     Fetch
             ↓         ↓         ↓
          Parse      Parse     Parse
             └─────────┼─────────┘
                       ↓
                  CLEAN / VALIDATE
                       ↓
                 PRODUCT MATCHING
                       ↓
                 INCREMENTAL CHECK
                       ↓
              ┌────────┴────────┐
              ↓                 ↓
          NEW PRODUCT       EXISTING
              ↓                 ↓
           INSERT          UPDATE
                                ↓
                       PRICE COMPARISON
                                ↓
                         PRICE HISTORY
                                ↓
                        M12 ANALYTICS
                                ↓
                    DEAL / TREND / ALERT
                                ↓
                           REPORTING
```

---

# 59. Recommended Project Structure

M14-এর পরে structure আরও mature হবে:

```text
ecommerce_data_collector/
│
├── scrapers/
│   ├── base.py
│   ├── site_a.py
│   ├── site_b.py
│   └── site_c.py
│
├── parsers/
│   ├── site_a_parser.py
│   ├── site_b_parser.py
│   └── site_c_parser.py
│
├── cleaners/
│   └── product_cleaner.py
│
├── validators/
│   └── product_validator.py
│
├── matching/
│   ├── normalize.py
│   ├── attributes.py
│   ├── candidates.py
│   └── matcher.py
│
├── database/
│   ├── connection.py
│   ├── products.py
│   ├── prices.py
│   └── jobs.py
│
├── analytics/
│   ├── price_history.py
│   ├── price_trend.py
│   ├── volatility.py
│   └── deal_detection.py
│
├── pipeline/
│   ├── extract.py
│   ├── transform.py
│   ├── load.py
│   └── incremental.py
│
├── scheduler/
│   └── jobs.py
│
├── data/
│   ├── raw/
│   ├── cleaned/
│   └── features/
│
├── logs/
│
├── config/
│   └── settings.py
│
├── main.py
├── requirements.txt
└── .env
```

---

# 60. M14 Mini Project 🚀

এখন তোমার practical project:

## **Automated E-commerce Price Monitoring System**

### Target

```text
3 Websites
100 Products/site
প্রতি 6 ঘণ্টায় collection
```

Database:

```text
300+ products
+
historical price observations
```

---

## Phase 1 — Initial Collection

```text
Website
 ↓
300 products
 ↓
PostgreSQL
```

---

## Phase 2 — Scheduler

Cron:

```text
Every 6 hours
```

---

## Phase 3 — Incremental

প্রতিবার:

```text
Known Product
    ↓
Update

New Product
    ↓
Insert
```

---

## Phase 4 — Price History

```text
Current price
 ↓
Previous price
 ↓
Changed?
 ↓ YES
price_history
```

---

## Phase 5 — Analytics

Calculate:

```text
price_change_percent
historical_min
historical_avg
MA_7
MA_30
volatility
trend
deal_score
```

---

## Phase 6 — Job Monitoring

প্রতিটি run-এর:

```text
status
started_at
finished_at
products_found
products_created
products_updated
errors_count
```

save করবে।

---

# 61. M14 Mastery Checklist ✅

### Automation

* [ ] Cron কী বুঝি?
* [ ] Scheduled scraping করতে পারি?
* [ ] Batch processing বুঝি?
* [ ] Job tracking করতে পারি?

### Incremental Collection

* [ ] Full scrape বনাম incremental scrape বুঝি?
* [ ] New product detect করতে পারি?
* [ ] Existing product update করতে পারি?
* [ ] `last_seen_at` ব্যবহার করতে পারি?
* [ ] Missing product lifecycle বুঝি?

### Database

* [ ] Upsert করতে পারি?
* [ ] Unique constraint বুঝি?
* [ ] Transaction বুঝি?
* [ ] Rollback বুঝি?
* [ ] Idempotency বুঝি?
* [ ] Scrape job track করতে পারি?

### Reliability

* [ ] Retry
* [ ] Exponential backoff
* [ ] Logging
* [ ] Error isolation
* [ ] Rate limiting
* [ ] Controlled concurrency

### Data Engineering

* [ ] ETL বুঝি?
* [ ] ELT বুঝি?
* [ ] Batch processing বুঝি?
* [ ] Data lineage বুঝি?
* [ ] Incremental pipeline বুঝি?

---

# 🔥 M01 → M14 এখন কোথায় দাঁড়িয়েছে?

```text
M01 Requests
        ↓
M02 BeautifulSoup
        ↓
M03 Pagination
        ↓
M04 Data Cleaning
        ↓
M05 Playwright
        ↓
M06 API Extraction
        ↓
M07 Multi-Site Architecture
        ↓
M08 PostgreSQL
        ↓
M09 Pandas Analytics
        ↓
M10 Product Matching
        ↓
M11 Feature Engineering
        ↓
M12 Price Intelligence
        ↓
M13 Any Website Collection
        ↓
M14 Automation + Incremental Pipeline
```

এখন তোমার project আর শুধু **"web scraper"** নয়।

এটা হচ্ছে:

```text
                    E-COMMERCE
                 DATA PLATFORM
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
   COLLECTION       DATABASE        ANALYTICS
       ↓               ↓               ↓
   Requests          PostgreSQL      Pandas
   API               History         Features
   BeautifulSoup     Products        Trends
   Playwright        Prices          Deals
       ↓               ↓               ↓
       └───────────────┼───────────────┘
                       ↓
                  PRICE INTELLIGENCE
```

### M14-এর সবচেয়ে গুরুত্বপূর্ণ concept

> **Scraping once is easy. Building a reliable system that keeps collecting correct historical data is the real skill.**

এর পরের logical step হবে **M15 — Data Quality Engineering & Validation at Scale**: হাজার/লাখ record-এর মধ্যে ভুল price, duplicate, missing data, corrupted records, schema changes, scraper breakage এবং data-quality monitoring কীভাবে automatically detect ও handle করতে হয়।


----
# M15 — Data Quality Engineering & Validation at Scale

M14 পর্যন্ত আমরা **automated scraping + incremental pipeline + PostgreSQL + historical data** তৈরি করেছি।

এখন সবচেয়ে গুরুত্বপূর্ণ প্রশ্ন:

> **আমরা যে 10,000 / 100,000 / 1,000,000 records collect করছি—সেগুলো আসলেই reliable কি না?**

এটাই M15-এর মূল বিষয়।

---

# 🎯 M15-এর Goal

একটি production-level system বানানো যেখানে automatically detect করা যাবে:

* ❌ Invalid price
* ❌ Negative price
* ❌ Impossible rating
* ❌ Wrong discount
* ❌ Duplicate product
* ❌ Missing data
* ❌ Corrupted records
* ❌ Broken scraper
* ❌ Website schema পরিবর্তন
* ❌ Unexpectedly কম data
* ❌ Unexpectedly বেশি data
* ❌ Price anomaly
* ❌ Data type problem
* ❌ Historical data inconsistency

Final pipeline:

```text
Scraper
   ↓
Raw Data
   ↓
Schema Validation
   ↓
Field Validation
   ↓
Business Rule Validation
   ↓
Duplicate Detection
   ↓
Anomaly Detection
   ↓
Quality Score
   ↓
Valid Data ─────→ PostgreSQL
   ↓
Invalid Data
   ↓
Quarantine / Error Table
   ↓
Quality Report
```

---

# M15 Roadmap

আমরা M15-কে 10টি অংশে ভাগ করব:

```text
M15.01 → Data Quality Fundamentals
M15.02 → Schema Validation
M15.03 → Field Validation
M15.04 → Business Rule Validation
M15.05 → Missing Data Quality
M15.06 → Duplicate & Consistency Checks
M15.07 → Anomaly Detection
M15.08 → Automated Data Quality Framework
M15.09 → Quality Score & Monitoring
M15.10 → Production Data Quality Pipeline
```

---

# M15.01 — Data Quality Fundamentals

Data quality মানে শুধু:

```text
data আছে কি না
```

এটা অনেক বড় concept।

একটি ভালো dataset-এর কয়েকটি dimension আছে।

## 1. Accuracy

Data বাস্তবতার সাথে correct কি না।

Example:

```text
Product price = 15000
Actual website price = 15000
```

Good.

কিন্তু:

```text
Database price = 150000
Website price = 15000
```

Bad.

---

# 2. Completeness

Required data missing কি না।

Example:

```text
name = iPhone 16
price = 85000
brand = Apple
rating = NULL
```

সব field না থাকলেও record usable হতে পারে।

কিন্তু:

```text
name = NULL
price = NULL
product_url = NULL
```

এটা serious problem।

---

# 3. Consistency

একাধিক field একে অপরের সাথে consistent কি না।

Example:

```text
price = 80000
original_price = 100000
discount = 20%
```

Correct.

কিন্তু:

```text
price = 80000
original_price = 100000
discount = 50%
```

Inconsistent.

---

# 4. Validity

Value allowed range/type-এর মধ্যে আছে কি না।

Example:

```text
rating = 4.5
```

Valid.

```text
rating = 8.7
```

Invalid.

কারণ:

```text
0 <= rating <= 5
```

---

# 5. Uniqueness

একই product accidentally multiple times এসেছে কি না।

Example:

```text
website_id = 1
external_product_id = ABC123
```

একবার থাকা উচিত।

যদি:

```text
ABC123
ABC123
ABC123
```

তাহলে duplicate।

---

# 6. Timeliness

Data কতটা recent?

Example:

```text
last_scraped_at = 2026-09-07
```

Good.

কিন্তু:

```text
last_scraped_at = 2026-01-01
```

বর্তমান price monitoring system-এর জন্য stale data।

---

# 7. Integrity

Relationship ঠিক আছে কি না।

Example:

```text
product_id = 100
website_id = 5
```

কিন্তু database-এ website 5 exist করে না।

এটা referential integrity problem।

---

# Data Quality-এর 7 Dimension

মনে রাখবে:

```text
Accuracy
Completeness
Consistency
Validity
Uniqueness
Timeliness
Integrity
```

---

# M15.02 — Schema Validation

প্রথমে আমরা check করব:

> Data structure ঠিক আছে কি না?

ধরি scraper expected করছে:

```python
required_columns = [
    "source",
    "product_id",
    "name",
    "brand",
    "category",
    "price",
    "original_price",
    "discount",
    "rating",
    "review_count",
    "availability",
    "product_url",
    "image_url",
    "scraped_at"
]
```

DataFrame:

```python
import pandas as pd

df = pd.read_csv("products.csv")

print(df.columns.tolist())
```

---

## Required columns check

```python
missing_columns = [
    col
    for col in required_columns
    if col not in df.columns
]

if missing_columns:
    print("Missing columns:", missing_columns)
else:
    print("Schema OK")
```

যদি website structure পরিবর্তন করে:

```text
price
```

এর পরিবর্তে:

```text
current_price
```

তাহলে scraper/parser fail করতে পারে।

Schema validation সেটা ধরবে।

---

# Extra Columns

ধরি:

```text
expected:
name
price
rating
```

কিন্তু পেলাম:

```text
name
price
rating
seller_name
shipping_fee
```

এটা সবসময় error না।

তাই সাধারণত:

```python
missing = set(required_columns) - set(df.columns)
extra = set(df.columns) - set(required_columns)

print("Missing:", missing)
print("Extra:", extra)
```

---

# Schema Contract

Production system-এ আমরা schema contract define করতে পারি।

Example:

```python
SCHEMA = {
    "name": "string",
    "price": "float",
    "rating": "float",
    "review_count": "integer",
}
```

এর মানে:

```text
name → string
price → numeric
rating → numeric
review_count → integer
```

---

# M15.03 — Field Validation

এখন প্রতিটি column-এর value check করব।

---

## Price Validation

Price:

```python
df["price"] = pd.to_numeric(
    df["price"],
    errors="coerce"
)
```

তারপর:

```python
invalid_price = df[
    df["price"].isna() |
    (df["price"] <= 0)
]

print(invalid_price)
```

---

## Example

```text
10000       ✓
5000        ✓
0           ❌
-500        ❌
"abc"       ❌
NULL        ❌
```

---

# Rating Validation

```python
df["rating"] = pd.to_numeric(
    df["rating"],
    errors="coerce"
)

invalid_rating = df[
    df["rating"].notna() &
    (
        (df["rating"] < 0) |
        (df["rating"] > 5)
    )
]
```

এখানে একটা important বিষয়:

```text
NULL
```

সবসময় invalid নয়।

যদি website rating না দেয়:

```text
rating = NULL
```

এটা **missing**, necessarily invalid নয়।

---

# Review Count

```python
df["review_count"] = pd.to_numeric(
    df["review_count"],
    errors="coerce"
)
```

Check:

```python
invalid_reviews = df[
    df["review_count"].notna() &
    (df["review_count"] < 0)
]
```

কারণ:

```text
review_count = -10
```

বাস্তবে impossible।

---

# Discount

```python
df["discount"] = pd.to_numeric(
    df["discount"],
    errors="coerce"
)
```

Validation:

```python
invalid_discount = df[
    df["discount"].notna() &
    (
        (df["discount"] < 0) |
        (df["discount"] > 100)
    )
]
```

কারণ:

```text
0% → valid
20% → valid
80% → valid
100% → possible
150% → invalid
-20% → invalid
```

---

# M15.04 — Business Rule Validation

এটা খুব গুরুত্বপূর্ণ।

Simple datatype validation যথেষ্ট নয়।

ধরি:

```text
price = 80000
original_price = 100000
discount = 20
```

সবগুলো datatype correct।

কিন্তু আমাদের check করতে হবে:

```text
discount ≈ (original_price - price) / original_price × 100
```

---

# Calculated Discount

```python
df["calculated_discount"] = (
    (
        df["original_price"] - df["price"]
    )
    / df["original_price"]
) * 100
```

তারপর:

```python
df["discount_difference"] = (
    df["discount"]
    - df["calculated_discount"]
).abs()
```

ধরি tolerance:

```python
tolerance = 2
```

Check:

```python
discount_errors = df[
    df["discount_difference"] > tolerance
]
```

---

# Price Relationship

Normally:

```text
price <= original_price
```

Check:

```python
invalid_price_relation = df[
    df["original_price"].notna() &
    df["price"].notna() &
    (df["price"] > df["original_price"])
]
```

Example:

```text
price = 120000
original_price = 100000
```

এটা suspicious।

তবে business context অনুযায়ী exceptions থাকতে পারে।

---

# Rating + Review Consistency

ধরি:

```text
rating = 4.8
review_count = 0
```

এটা necessarily impossible নয়, কিন্তু suspicious।

আর:

```text
rating = NULL
review_count = 10000
```

এটাও necessarily error নয়।

তাই quality system-এ আমরা তিন ধরনের result রাখতে পারি:

```text
VALID
INVALID
SUSPICIOUS
```

---

# M15.05 — Missing Data Quality

Missing data তিনভাবে দেখা যায়:

```text
NULL
empty string
"unknown"
"N/A"
"not available"
```

এগুলো normalize করতে হবে।

---

## Normalize Missing Values

```python
missing_values = [
    "",
    " ",
    "N/A",
    "NA",
    "null",
    "NULL",
    "unknown",
    "Unknown",
    "-"
]

df = df.replace(
    missing_values,
    pd.NA
)
```

---

# Missing Percentage

```python
missing_percentage = (
    df.isna().mean() * 100
)

print(missing_percentage)
```

Example:

```text
name             0.0%
price            1.2%
rating          18.5%
review_count     5.4%
brand            3.1%
```

এতে বুঝতে পারব কোন field problematic।

---

# Critical vs Optional Fields

সব missing value equally important নয়।

### Critical

```text
product_id
name
price
product_url
website_id
```

### Optional

```text
rating
review_count
image_url
description
discount
```

---

# Completeness Score

ধরি required fields:

```python
required_fields = [
    "name",
    "price",
    "product_url",
    "brand",
    "category"
]
```

Calculate:

```python
df["completeness_score"] = (
    df[required_fields].notna().mean(axis=1)
    * 100
)
```

Example:

```text
Product A → 100%
Product B → 80%
Product C → 40%
```

---

# M15.06 — Duplicate Detection

Duplicate দুই ধরনের হতে পারে।

## Exact Duplicate

```python
duplicates = df[
    df.duplicated()
]
```

Remove:

```python
df = df.drop_duplicates()
```

---

# Product Identity Duplicate

Better approach:

```python
df.duplicated(
    subset=[
        "source",
        "product_id"
    ]
)
```

কারণ একই product-এর:

```text
name
price
rating
```

পরিবর্তন হতে পারে।

কিন্তু:

```text
source + product_id
```

একই হলে identity একই হতে পারে।

---

# Database Level Protection

PostgreSQL-এ:

```sql
UNIQUE (
    website_id,
    external_product_id
)
```

এটা খুব গুরুত্বপূর্ণ।

কারণ:

```text
Python validation
+
Database constraint
```

দুটো layer থাকলে reliability বাড়ে।

---

# Duplicate Product Names

এখানে সাবধান।

```text
iPhone 16
iPhone 16
```

মানে duplicate **হতেই হবে** এমন নয়।

দুই seller একই product sell করতে পারে।

তাই:

```text
name
```

দিয়ে identity determine করা উচিত নয়।

M10-এর entity resolution এখানে ব্যবহার হবে।

---

# M15.07 — Anomaly Detection

এখন আমরা এমন data খুঁজব যেটা technically valid কিন্তু suspicious।

Example:

```text
iPhone 16
Normal price: 85,000

Collected:
850,000
```

এটা:

```text
> 0
```

তাই field validation pass করবে।

কিন্তু anomaly হতে পারে।

---

# IQR Method

M11-এ আমরা IQR দেখেছিলাম।

Formula:

```text
IQR = Q3 - Q1
```

Bounds:

```text
Lower = Q1 - 1.5 × IQR
Upper = Q3 + 1.5 × IQR
```

Python:

```python
Q1 = df["price"].quantile(0.25)
Q3 = df["price"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

তারপর:

```python
outliers = df[
    (df["price"] < lower) |
    (df["price"] > upper)
]
```

---

# কিন্তু গুরুত্বপূর্ণ বিষয়

**Outlier ≠ Error**

Example:

```text
Laptop prices:
50k
55k
60k
65k
500k
```

500k সত্যিই premium workstation হতে পারে।

তাই:

```text
Outlier
```

মানে:

> "Investigate this record"

না যে:

> "Delete this record"

---

# Price Change Anomaly

Historical data-তে আরও powerful।

ধরি:

```text
Yesterday = 80,000
Today = 8,000
```

Price drop:

```text
90%
```

এটা real sale হতে পারে।

আবার scraper bug-ও হতে পারে।

---

## Calculate

```python
df = df.sort_values(
    ["master_product_id", "scraped_at"]
)

df["previous_price"] = (
    df.groupby("master_product_id")["price"]
      .shift(1)
)
```

Price change:

```python
df["price_change_percent"] = (
    (
        df["price"] - df["previous_price"]
    )
    / df["previous_price"]
) * 100
```

---

# Suspicious Price Change

```python
suspicious = df[
    df["price_change_percent"].abs() > 50
]
```

এখানেও:

```text
50% change
```

মানে automatic error নয়।

বরং:

```text
SUSPICIOUS
```

---

# M15.08 — Automated Data Quality Framework

এখন আলাদা আলাদা validation function বানাব।

Project structure:

```text
ecommerce_data_collector/
│
├── validators/
│   ├── __init__.py
│   ├── schema.py
│   ├── fields.py
│   ├── business_rules.py
│   ├── duplicates.py
│   ├── anomalies.py
│   └── quality.py
│
├── scrapers/
├── parsers/
├── cleaners/
├── database/
├── analytics/
├── pipeline/
│
├── reports/
│
├── logs/
│
├── main.py
└── requirements.txt
```

---

# Schema Validator

```python
def validate_schema(df, required_columns):

    missing = [
        col
        for col in required_columns
        if col not in df.columns
    ]

    return {
        "valid": len(missing) == 0,
        "missing_columns": missing
    }
```

Use:

```python
result = validate_schema(
    df,
    required_columns
)

print(result)
```

---

# Price Validator

```python
def validate_price(df):

    invalid = (
        df["price"].isna() |
        (df["price"] <= 0)
    )

    return df[invalid]
```

---

# Rating Validator

```python
def validate_rating(df):

    invalid = (
        df["rating"].notna() &
        (
            (df["rating"] < 0) |
            (df["rating"] > 5)
        )
    )

    return df[invalid]
```

---

# Business Rule Validator

```python
def validate_price_relationship(df):

    invalid = (
        df["original_price"].notna() &
        df["price"].notna() &
        (df["price"] > df["original_price"])
    )

    return df[invalid]
```

---

# Master Validation Function

```python
def validate_products(df):

    errors = {}

    errors["invalid_price"] = validate_price(df)
    errors["invalid_rating"] = validate_rating(df)
    errors["invalid_price_relation"] = (
        validate_price_relationship(df)
    )

    return errors
```

---

# M15.09 — Quality Score

এখন প্রতিটি record-এর quality score বানাতে পারি।

Example:

```text
Completeness       30%
Validity           25%
Consistency        20%
Uniqueness         15%
Timeliness         10%
```

---

## Example

```python
df["quality_score"] = (
    0.30 * df["completeness_score"]
    + 0.25 * df["validity_score"]
    + 0.20 * df["consistency_score"]
    + 0.15 * df["uniqueness_score"]
    + 0.10 * df["timeliness_score"]
)
```

এটা একটি **business-specific heuristic**।

সব project-এ একই weight ব্যবহার করতে হবে না।

---

# Quality Categories

```python
def quality_category(score):

    if score >= 90:
        return "EXCELLENT"

    elif score >= 75:
        return "GOOD"

    elif score >= 50:
        return "WARNING"

    else:
        return "BAD"
```

Apply:

```python
df["quality_category"] = (
    df["quality_score"]
    .apply(quality_category)
)
```

---

# Example Result

| Product    | Quality Score | Status    |
| ---------- | ------------: | --------- |
| iPhone 16  |            98 | EXCELLENT |
| Galaxy S25 |            91 | EXCELLENT |
| Redmi Note |            82 | GOOD      |
| Laptop X   |            68 | WARNING   |
| Product Y  |            35 | BAD       |

---

# M15.10 — Production Data Quality Pipeline

এখন পুরো pipeline তৈরি করি।

```text
                    WEBSITE
                       │
                       ▼
                  SCRAPER/API
                       │
                       ▼
                    RAW DATA
                       │
                       ▼
              ┌─────────────────┐
              │ Schema Validation│
              └────────┬────────┘
                       ▼
               Field Validation
                       │
                       ▼
              Business Validation
                       │
                       ▼
              Duplicate Detection
                       │
                       ▼
              Anomaly Detection
                       │
              ┌────────┴─────────┐
              ▼                  ▼
           VALID              INVALID
              │                  │
              ▼                  ▼
        CLEAN DATA          QUARANTINE
              │                  │
              ▼                  ▼
        PostgreSQL          Error Table
              │
              ▼
       Feature Engineering
              │
              ▼
          Analytics
```

---

# Quarantine System

Invalid data সরাসরি delete না করে আলাদা রাখতে পারি।

PostgreSQL:

```sql
CREATE TABLE data_quality_errors (
    id BIGSERIAL PRIMARY KEY,

    scrape_job_id BIGINT,

    website_id INTEGER,

    external_product_id VARCHAR(255),

    error_type VARCHAR(100),

    error_message TEXT,

    raw_data JSONB,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

এটা production system-এ অনেক useful।

---

# Example

Suppose scraper পেল:

```json
{
    "product_id": "ABC123",
    "name": "iPhone 16",
    "price": -5000,
    "rating": 4.8
}
```

Pipeline:

```text
Scraper
   ↓
Raw record
   ↓
price validation
   ↓
INVALID
   ↓
data_quality_errors
```

Database-এর clean products table-এ যাবে না।

---

# Data Quality Report

প্রতিটি scraping job শেষে report generate করতে পারি।

Example:

```text
================================
DATA QUALITY REPORT
================================

Website: Site A

Records collected:       10,000

Valid records:            9,420
Invalid records:            580

Missing price:               120
Invalid price:                35
Invalid rating:               18
Invalid discount:             27
Duplicates:                  210
Suspicious prices:           170

Average quality score:      91.4%

Schema status:              PASS
================================
```

---

# সবচেয়ে গুরুত্বপূর্ণ — Scraper Health Monitoring

এখানে M15-এর সবচেয়ে practical অংশ।

ধরি প্রতিদিন সাধারণত:

```text
10,000 products
```

আজ scraper collect করল:

```text
73 products
```

সব records technically valid হতে পারে।

কিন্তু:

> **Scraper সম্ভবত broken.**

---

# Volume Anomaly

```python
today_count = len(df)

expected_count = 10000

ratio = today_count / expected_count
```

যদি:

```python
ratio < 0.5:
    print("WARNING: unusually low product count")
```

---

# Historical Baseline

আরও ভালো:

```text
Last 7 days:

10,100
9,980
10,230
9,870
10,050
10,120
10,010
```

আজ:

```text
2,000
```

তাহলে automatic alert:

```text
🚨 SCRAPER HEALTH ALERT

Expected: ~10,000
Collected: 2,000
Drop: 80%
```

---

# Schema Drift Detection

Website HTML/API structure পরিবর্তন করলে:

```text
Before:
price
rating
review_count

After:
current_price
stars
reviews
```

Scraper পুরনো selector ব্যবহার করলে:

```text
price = NULL
rating = NULL
review_count = NULL
```

আমাদের data-quality monitoring বলবে:

```text
🚨 price missing rate increased from 1% → 94%
```

এটাই scraper breakage detection-এর powerful technique।

---

# Quality Monitoring Metrics

প্রতিটি job-এর জন্য track করো:

```text
records_collected
records_valid
records_invalid
missing_rate
duplicate_rate
schema_status
average_quality_score
price_anomaly_count
rating_anomaly_count
```

---

# PostgreSQL Quality Job Table

M14-এর `scrape_jobs` আরও extend করা যায়:

```sql
ALTER TABLE scrape_jobs
ADD COLUMN valid_records INTEGER DEFAULT 0,
ADD COLUMN invalid_records INTEGER DEFAULT 0,
ADD COLUMN duplicate_records INTEGER DEFAULT 0,
ADD COLUMN quality_score NUMERIC(5,2),
ADD COLUMN schema_status VARCHAR(20);
```

---

# Full Production Architecture

এখন তোমার e-commerce collector অনেক mature হয়ে যাচ্ছে:

```text
                         ┌───────────────┐
                         │   Scheduler   │
                         └───────┬───────┘
                                 │
                                 ▼
                         ┌───────────────┐
                         │  Scrape Job   │
                         └───────┬───────┘
                                 │
                  ┌──────────────┼──────────────┐
                  ▼              ▼              ▼
               Site A          Site B         Site C
                  │              │              │
                  └──────────────┼──────────────┘
                                 ▼
                           Raw Data
                                 │
                                 ▼
                        Schema Validation
                                 │
                                 ▼
                         Data Cleaning
                                 │
                                 ▼
                       Field Validation
                                 │
                                 ▼
                      Business Validation
                                 │
                                 ▼
                      Duplicate Detection
                                 │
                                 ▼
                       Anomaly Detection
                                 │
                   ┌─────────────┴─────────────┐
                   ▼                           ▼
                Valid                       Invalid
                   │                           │
                   ▼                           ▼
             Product Matching            Quarantine
                   │
                   ▼
             PostgreSQL
                   │
                   ▼
             Price History
                   │
                   ▼
          Feature Engineering
                   │
                   ▼
            Price Analytics
                   │
                   ▼
            Deal Detection
                   │
                   ▼
             Dashboard/API
```

---

# 🔥 M15 Mini Project

এখন তোমার জন্য একটা practical project:

## Project: E-commerce Data Quality Monitoring System

### Input

3 websites:

```text
Site A
Site B
Site C
```

প্রতিটি:

```text
1,000 products
```

Total:

```text
3,000 records
```

---

## Inject Data Problems

নিজে intentionally কিছু error তৈরি করো:

```text
50 invalid prices
30 invalid ratings
40 invalid discounts
100 missing brands
80 duplicates
20 corrupted product IDs
30 suspicious prices
```

---

# Pipeline

```text
CSV/API
  ↓
Pandas
  ↓
Schema Validation
  ↓
Field Validation
  ↓
Business Rules
  ↓
Duplicate Detection
  ↓
Anomaly Detection
  ↓
Quality Score
  ↓
Valid Dataset
  ↓
PostgreSQL
```

Invalid:

```text
Invalid Data
    ↓
data_quality_errors
```

---

# Final Output Files

তোমার project শেষে:

```text
data/
│
├── raw_products.csv
│
├── valid_products.csv
│
├── invalid_products.csv
│
└── quality_report.csv
```

Quality report:

```text
website
total_records
valid_records
invalid_records
duplicate_records
missing_price
invalid_price
invalid_rating
invalid_discount
suspicious_price
average_quality_score
```

---

# 🧠 M15-এর Core Concepts

এইগুলো অবশ্যই strong করতে হবে:

### Data Quality

```text
Accuracy
Completeness
Consistency
Validity
Uniqueness
Timeliness
Integrity
```

### Validation

```text
Schema validation
Type validation
Range validation
Business rule validation
Cross-field validation
```

### Data Problems

```text
Missing data
Duplicate data
Invalid data
Corrupted data
Inconsistent data
Outlier
Anomaly
Schema drift
```

### Production

```text
Quality score
Quality report
Quarantine
Monitoring
Alerting
Scraper health
Data lineage
```

---

# M14 → M15 Connection

এখন তোমার system-এর evolution:

```text
M01
Requests
  ↓
M02
BeautifulSoup
  ↓
M03
Pagination
  ↓
M04
Cleaning
  ↓
M05
Playwright
  ↓
M06
API
  ↓
M07
Multi-site architecture
  ↓
M08
PostgreSQL
  ↓
M09
Pandas Analytics
  ↓
M10
Product Matching
  ↓
M11
Feature Engineering
  ↓
M12
Price Intelligence
  ↓
M13
Any Website Collection
  ↓
M14
Automation + Incremental Pipeline
  ↓
M15
⭐ Data Quality Engineering
```

এখন তুমি শুধু **data collect** করছো না—তুমি এমন একটি system তৈরি করছো যেটা বুঝতে পারে **“এই collected data বিশ্বাসযোগ্য কি না।”**

### পরবর্তী ধাপ

**M16 — Data Monitoring, Alerting & Observability** এ আমরা শিখব কীভাবে system নিজে detect করবে:

```text
Scraper broken
↓
Data suddenly কমে গেছে
↓
Price suddenly পরিবর্তন হয়েছে
↓
API response structure পরিবর্তন হয়েছে
↓
Missing data বেড়ে গেছে
↓
Duplicate বেড়ে গেছে
↓
Quality score কমে গেছে
↓
🚨 Automatic Alert
```

এটা M14 + M15-এর ওপর দাঁড়িয়ে production-level monitoring system তৈরি করবে।


---
