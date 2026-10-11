হ্যাঁ, দুটোই ব্যবহার করা যায়। তবে **`ui` আর `components`-এর মধ্যে পার্থক্যটা naming/organization-এর**, Next.js-এর কোনো বাধ্যতামূলক rule না।

আমি সহজভাবে বলি:

### 1. `ui/` → ছোট, generic, reusable UI

যেগুলো শুধু visual building block:

```text
components/
└── ui/
    ├── Button.jsx
    ├── Input.jsx
    ├── Modal.jsx
    ├── Badge.jsx
    ├── Spinner.jsx
    ├── Dropdown.jsx
    └── Pagination.jsx
```

উদাহরণ:

```jsx
<Button>Save</Button>
<Button>Delete</Button>
<Button>Login</Button>
```

একই `Button` অনেক জায়গায় ব্যবহার করা যায়।

---

### 2. `components/` → বড়/feature-specific components

যেগুলোর মধ্যে কিছু business/UI logic থাকতে পারে:

```text
components/
├── ui/
│   ├── Button.jsx
│   ├── Input.jsx
│   └── Modal.jsx
│
├── navbar/
│   └── Navbar.jsx
│
├── product/
│   ├── ProductCard.jsx
│   ├── ProductList.jsx
│   └── ProductFilter.jsx
│
├── cart/
│   ├── CartItem.jsx
│   └── CartSummary.jsx
│
└── dashboard/
    ├── StatsCard.jsx
    └── SalesChart.jsx
```

যেমন `ProductCard` শুধু button-এর মতো generic না; এটা **Product domain-এর component**।

---

## তাহলে `components` + `ui` একসাথে কীভাবে?

আমার recommendation:

```text
src/
├── app/
│   ├── page.jsx
│   ├── products/
│   ├── cart/
│   └── dashboard/
│
└── components/
    ├── ui/
    │   ├── Button.jsx
    │   ├── Input.jsx
    │   ├── Modal.jsx
    │   └── Table.jsx
    │
    ├── layout/
    │   ├── Navbar.jsx
    │   ├── Sidebar.jsx
    │   └── Footer.jsx
    │
    ├── product/
    │   ├── ProductCard.jsx
    │   └── ProductFilter.jsx
    │
    └── cart/
        ├── CartItem.jsx
        └── CartSummary.jsx
```

### এক লাইনে মনে রাখো

**`ui/` = ছোট reusable building blocks**

**`components/` = application-এর বিভিন্ন বড়/reusable components**

তবে `ui` নিজেও `components`-এর ভিতরে থাকলে সবচেয়ে পরিষ্কার হয়:

```text
components/
└── ui/
```

তোমার **Next.js + DRF e-commerce project** হলে আমি এই structure-টাই recommend করব।


---
`lib` folder-কে সহজভাবে বললে **application-এর reusable logic/service রাখার জায়গা**। এখানে সাধারণত UI component রাখা হয় না।

তোমার **Next.js + Django REST API** project ধরলে `lib`-এ এগুলো রাখতে পারো:

```text
src/
└── lib/
    ├── api.js
    ├── auth.js
    ├── utils.js
    ├── validation.js
    ├── format.js
    ├── constants.js
    └── config.js
```

### 1. API / Data Fetching ⭐

Backend API call:

```js
// lib/api.js

export async function getProducts() {
  const response = await fetch(
    "http://localhost:8000/api/products/"
  );

  if (!response.ok) {
    throw new Error("Failed to fetch products");
  }

  return response.json();
}
```

তারপর:

```js
import { getProducts } from "@/lib/api";
```

---

### 2. Authentication

Login/logout/current-user related logic:

```text
lib/
└── auth.js
```

যেমন:

```js
export async function getCurrentUser() {
  // API থেকে current user আনবে
}
```

---

### 3. Utility Functions

বারবার প্রয়োজন হয় এমন ছোট function:

```js
// lib/utils.js

export function cn(...classes) {
  return classes.filter(Boolean).join(" ");
}
```

অথবা:

```js
export function calculateDiscount(price, discount) {
  return price - (price * discount) / 100;
}
```

---

### 4. Formatting

Date, currency ইত্যাদি format:

```js
// lib/format.js

export function formatPrice(price) {
  return `৳${price.toLocaleString()}`;
}
```

ব্যবহার:

```js
formatPrice(1500);
```

Output:

```text
৳1,500
```

---

### 5. Validation

Form/data validation-এর reusable logic:

```text
lib/
└── validation.js
```

যেমন:

```js
export function isValidEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
```

---

### 6. Constants

বারবার ব্যবহৃত fixed values:

```js
// lib/constants.js

export const API_URL = "http://localhost:8000/api";

export const ORDER_STATUS = {
  PENDING: "pending",
  PAID: "paid",
  SHIPPED: "shipped",
  DELIVERED: "delivered",
};
```

---

### 7. Configuration

Application configuration:

```js
// lib/config.js

export const config = {
  apiUrl: process.env.NEXT_PUBLIC_API_URL,
};
```

---

## সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

ধরো তোমার **Product** page আছে।

```text
ProductPage
    │
    ├── ProductCard
    │       └── UI
    │
    └── getProducts()
            │
            └── lib/api.js
                    │
                    ↓
              Django REST API
```

অর্থাৎ:

| Folder               | কাজ                                            |
| -------------------- | ---------------------------------------------- |
| `components/ui`      | ছোট reusable UI                                |
| `components/product` | Product-related UI                             |
| `lib`                | reusable logic, API, utility, formatting, auth |
| `app`                | routing + pages + layouts                      |

### একটা গুরুত্বপূর্ণ বিষয়

`lib` **Next.js-এর mandatory folder না**।

তুমি চাইলে:

```text
src/lib/
```

অথবা:

```text
src/services/
src/utils/
```

এভাবেও organize করতে পারো।

কিন্তু Next.js project-এ **`lib` নামটি খুব common convention**, তাই beginner হিসেবে এটা ব্যবহার করাই ভালো।

----
হ্যাঁ, **কিছু JSON data `lib`-এ রাখা যায়**, কিন্তু **সব JSON data `lib`-এ রাখা উচিত না**।

মূল বিষয় হলো JSON data-টা **কী ধরনের data**।

### 1. Static application data → রাখা যায়

যেমন তোমার country list:

```text
src/
└── lib/
    └── countries.json
```

```json
[
  {
    "id": 1,
    "name": "Bangladesh",
    "code": "BD"
  },
  {
    "id": 2,
    "name": "India",
    "code": "IN"
  }
]
```

তারপর:

```js
import countries from "@/lib/countries.json";

console.log(countries);
```

এটা ঠিক আছে।

---

### 2. Configuration data → `lib`-এ রাখা যায়

যেমন:

```text
lib/
├── config.js
└── constants.js
```

```js
export const languages = [
  {
    code: "en",
    name: "English",
  },
  {
    code: "bn",
    name: "Bangla",
  },
];
```

---

### 3. API থেকে আসা data → `lib`-এ JSON হিসেবে রাখবে না ❌

ধরো Django API থেকে:

```text
GET /api/products/
```

response:

```json
[
  {
    "id": 1,
    "name": "Laptop",
    "price": 50000
  }
]
```

এই data `lib/products.json` করে রাখা উচিত না।

বরং:

```text
Next.js
   ↓
lib/api.js
   ↓
Django REST API
   ↓
JSON response
```

---

### 4. Large/static public data → `public/` ব্যবহার করা যেতে পারে

যেমন:

```text
public/
├── images/
└── data/
    └── products.json
```

এটা browser থেকে directly access করার প্রয়োজন হলে useful।

---

## সহজ Rule

```text
Static reusable data
        ↓
       lib/

Publicly accessible files
        ↓
      public/

Backend/API data
        ↓
   Django API → fetch()

UI-specific data
        ↓
 component-এর ভিতরে
```

### তোমার Django + Next.js project-এ

আমি সাধারণত এমন রাখব:

```text
src/
├── app/
├── components/
│   └── ui/
├── lib/
│   ├── api.js
│   ├── auth.js
│   ├── utils.js
│   ├── constants.js
│   └── countries.json
│
└── hooks/
```

**তাই উত্তর হলো: হ্যাঁ, static/reusable JSON data `lib`-এ রাখা যায়; কিন্তু API থেকে পাওয়া dynamic data `lib`-এ JSON file হিসেবে রাখা উচিত নয়।**

---
হ্যাঁ—এখানে Next.js tutorial-এর **placeholder data** বলতে আসলে কী বোঝাচ্ছে সেটা খুব গুরুত্বপূর্ণ।

তারা `app/lib/placeholder-data.ts`-এ এমন কিছু **fake/sample data** রেখেছে, যাতে database/API তৈরি না করেও UI বানানো ও test করা যায়।

ধরো:

```text
app/
├── lib/
│   ├── placeholder-data.ts
│   └── ...
├── ui/
└── ...
```

`placeholder-data.ts`:

```ts
export const invoices = [
  {
    id: '1',
    customer_id: 'customer-1',
    amount: 2500,
    status: 'pending',
  },
  {
    id: '2',
    customer_id: 'customer-2',
    amount: 5000,
    status: 'paid',
  },
];
```

এখানে প্রতিটি object একটা invoice record-এর মতো।

```text
invoices
   ↓
[
  { invoice 1 },
  { invoice 2 },
  { invoice 3 }
]
```

### "Each JavaScript object represents a table" কথাটা একটু বুঝে নাও

Tutorial-এর wording-টা আসলে একটু confusing হতে পারে।

ধরো:

```ts
export const customers = [
  {
    id: '1',
    name: 'Rahim',
    email: 'rahim@example.com',
  },
];

export const invoices = [
  {
    id: '1',
    customer_id: '1',
    amount: 5000,
  },
];
```

এখানে:

```text
customers array → customers table-এর sample records
invoices array  → invoices table-এর sample records
```

অর্থাৎ **প্রতিটি object নিজে table নয়**; বরং array/collection-টি একটা table-এর sample data represent করছে।

### কেন placeholder data ব্যবহার করে?

ধরো তুমি একটা dashboard বানাচ্ছো:

```text
Dashboard
 ├── Revenue
 ├── Customers
 ├── Invoices
 └── Recent Transactions
```

কিন্তু Django backend/database এখনো বানাওনি।

তখন:

```text
placeholder-data.ts
        ↓
fake data
        ↓
Next.js UI
        ↓
Dashboard তৈরি/test
```

Backend তৈরি হয়ে গেলে:

```text
Django/PostgreSQL
        ↓
REST API
        ↓
Next.js fetch()
        ↓
Dashboard
```

তখন placeholder data আর প্রয়োজন হবে না।

### তোমার project-এ কীভাবে ব্যবহার করবে?

তুমি যদি **Next.js + DRF** project বানাও, development-এর শুরুতে:

```text
src/
├── app/
├── components/
└── lib/
    ├── api.js
    └── placeholder-data.js
```

`placeholder-data.js`:

```js
export const products = [
  {
    id: 1,
    name: "Laptop",
    price: 75000,
  },
  {
    id: 2,
    name: "Keyboard",
    price: 2500,
  },
];
```

UI তৈরি:

```jsx
import { products } from "@/lib/placeholder-data";

export default function Products() {
  return (
    <div>
      {products.map((product) => (
        <div key={product.id}>
          <h2>{product.name}</h2>
          <p>{product.price}</p>
        </div>
      ))}
    </div>
  );
}
```

পরে Django API ready হলে:

```jsx
const response = await fetch(
  "http://localhost:8000/api/products/"
);

const products = await response.json();
```

তখন `placeholder-data.js` বাদ দিতে পারবে।

**সুতরাং `placeholder-data.ts` হলো temporary/fake data—real database নয়।** UI development দ্রুত করার জন্য এটা ব্যবহার করা হয়।

---
হ্যাঁ, **এই `fetch()` code-টা `lib`-এর মধ্যে রাখা খুব ভালো practice**, বিশেষ করে তুমি যেহেতু Django REST Framework backend ব্যবহার করবে।

তবে একটা জিনিস বুঝতে হবে: **`lib`-এ function বানাবে, আর page/component থেকে সেই function call করবে।**

### 1. `lib/api.js` বানাও

```text
src/
└── lib/
    └── api.js
```

এখানে:

```js
const API_URL = "http://localhost:8000/api";

export async function getProducts() {
  const response = await fetch(`${API_URL}/products/`);

  if (!response.ok) {
    throw new Error("Failed to fetch products");
  }

  const products = await response.json();

  return products;
}
```

এখন তোমার API fetching logic `lib/api.js`-এর মধ্যে আছে।

---

### 2. Page থেকে ব্যবহার করো

ধরো:

```text
src/
└── app/
    └── products/
        └── page.jsx
```

```jsx
import { getProducts } from "@/lib/api";

export default async function ProductsPage() {
  const products = await getProducts();

  return (
    <div>
      {products.map((product) => (
        <div key={product.id}>
          <h2>{product.name}</h2>
          <p>{product.price}</p>
        </div>
      ))}
    </div>
  );
}
```

তখন flow হবে:

```text
ProductsPage
     ↓
getProducts()
     ↓
lib/api.js
     ↓
fetch()
     ↓
Django REST API
     ↓
JSON
     ↓
ProductsPage
     ↓
UI
```

### আরও ভালোভাবে organize করলে

Project বড় হলে আমি একটাই `api.js`-এ সব API রাখতাম না।

```text
src/
├── app/
│   └── products/
│       └── page.jsx
│
├── lib/
│   ├── api/
│   │   ├── products.js
│   │   ├── users.js
│   │   ├── orders.js
│   │   └── auth.js
│   │
│   ├── utils.js
│   └── constants.js
```

`products.js`:

```js
const API_URL = "http://localhost:8000/api";

export async function getProducts() {
  const response = await fetch(`${API_URL}/products/`);

  if (!response.ok) {
    throw new Error("Failed to fetch products");
  }

  return response.json();
}
```

তারপর:

```jsx
import { getProducts } from "@/lib/api/products";

export default async function ProductsPage() {
  const products = await getProducts();

  return (
    <div>
      {products.map((product) => (
        <div key={product.id}>{product.name}</div>
      ))}
    </div>
  );
}
```

**তাই তোমার প্রশ্নের সরাসরি উত্তর:**
`fetch → response.json()` **page-এর মধ্যে না লিখে reusable API function হিসেবে `lib`-এ রাখা ভালো।** Page শুধু `getProducts()` call করবে।

----
হ্যাঁ। Next.js/React-এ **conditionally CSS class apply** করার কয়েকটা common way আছে। CSS Module-এর সাথে সবচেয়ে বেশি এগুলো ব্যবহার করবে।

## 1. Ternary operator — সবচেয়ে সহজ

```jsx
import styles from "./Button.module.css";

export default function Button({ isActive }) {
  return (
    <button className={isActive ? styles.active : styles.inactive}>
      Button
    </button>
  );
}
```

CSS:

```css
.active {
  background: green;
  color: white;
}

.inactive {
  background: gray;
  color: black;
}
```

যদি:

```jsx
<Button isActive={true} />
```

তাহলে:

```text
active
```

আর:

```jsx
<Button isActive={false} />
```

তাহলে:

```text
inactive
```

---

## 2. একটা class সবসময় + একটা conditional class

এটা খুব common।

```jsx
<button
  className={`${styles.button} ${
    isActive ? styles.active : ""
  }`}
>
  Save
</button>
```

এখানে:

```text
সবসময় → button

isActive true → active
```

অর্থাৎ:

```text
button + active
```

---

## 3. Multiple condition

ধরো button-এর তিনটা state:

```jsx
<button
  className={
    isLoading
      ? styles.loading
      : isSuccess
      ? styles.success
      : styles.normal
  }
>
  Save
</button>
```

এখানে:

```text
isLoading → loading
isSuccess → success
otherwise → normal
```

তবে অনেক condition হলে এভাবে লেখা messy হয়ে যায়।

---

## 4. `&&` দিয়ে conditional class

যদি class শুধু condition true হলে লাগাতে চাও:

```jsx
<button
  className={`${styles.button} ${
    isActive && styles.active
  }`}
>
  Save
</button>
```

যদি `isActive = true`:

```text
button active
```

যদি `false`:

```text
button
```

---

## 5. Tailwind-এর সাথে

তুমি যেহেতু Tailwind ব্যবহার করছো, সেখানে:

```jsx
<button
  className={`px-4 py-2 ${
    isActive
      ? "bg-blue-600 text-white"
      : "bg-gray-300 text-black"
  }`}
>
  Save
</button>
```

এটাও খুব common।

---

## 6. `clsx` ব্যবহার ⭐

বড় project-এ আমি `clsx` recommend করব।

Install:

```bash
pnpm add clsx
```

তারপর:

```jsx
import clsx from "clsx";
import styles from "./Button.module.css";

export default function Button({ isActive, isDisabled }) {
  return (
    <button
      className={clsx(
        styles.button,
        isActive && styles.active,
        isDisabled && styles.disabled
      )}
    >
      Save
    </button>
  );
}
```

CSS:

```css
.button {
  padding: 10px 20px;
}

.active {
  background: blue;
  color: white;
}

.disabled {
  opacity: 0.5;
}
```

এটা অনেক clean:

```text
button → সবসময়
active → isActive হলে
disabled → isDisabled হলে
```

### আমার recommendation

ছোট condition:

```jsx
className={isActive ? styles.active : styles.inactive}
```

একাধিক condition:

```jsx
className={clsx(
  styles.button,
  isActive && styles.active,
  isDisabled && styles.disabled
)}
```

**Production React/Next.js project-এ `clsx` শেখা খুব useful।**

---
Next.js-এ **Fonts এবং Images optimize করা** খুব important, কারণ এগুলো website-এর **loading speed, Core Web Vitals এবং user experience**-এ বড় প্রভাব ফেলে।

Next.js-এর `next/font` এবং `next/image` এই কাজগুলো অনেক সহজ করে দেয়।

---

# 1. Font Optimization

সাধারণভাবে আমরা Google Font এভাবে ব্যবহার করতে পারি:

```html
<link
  href="https://fonts.googleapis.com/css2?family=Inter"
  rel="stylesheet"
/>
```

কিন্তু Next.js-এ `next/font` ব্যবহার করা ভালো।

এটা font-কে application-এর build-এর সময় handle করে, তাই runtime-এ আলাদা করে Google Fonts request করার প্রয়োজন কমে।

---

## 2. Google Font ব্যবহার

ধরো `Inter` ব্যবহার করবে।

`app/layout.jsx`:

```jsx
import { Inter } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
});

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className={inter.className}>
        {children}
      </body>
    </html>
  );
}
```

এখন পুরো application-এ `Inter` font ব্যবহার হবে।

---

# 3. Different Font Weight

তুমি আগেও font weight নিয়ে জানতে চেয়েছিলে। এখানে:

```jsx
const inter = Inter({
  subsets: ["latin"],
  weight: ["400", "500", "600", "700"],
});
```

তারপর:

```jsx
<h1 className="font-bold">
  Hello
</h1>
```

Tailwind-এর `font-bold` সেই loaded font weight ব্যবহার করবে।

### আরেকটা example

```jsx
const roboto = Roboto({
  subsets: ["latin"],
  weight: ["400", "500", "700"],
});
```

---

# 4. Variable Font

কিছু font variable weight support করে।

তখন:

```jsx
const inter = Inter({
  subsets: ["latin"],
});
```

অনেক ক্ষেত্রে আলাদা আলাদা weight manually specify করার প্রয়োজন হয় না।

---

# 5. Local Font

তোমার নিজের `.woff2` font থাকলে:

```text
public/
└── fonts/
    └── MyFont.woff2
```

এর পরিবর্তে Next.js-এ সাধারণত:

```text
src/
├── app/
└── fonts/
    └── MyFont.woff2
```

তারপর:

```jsx
import localFont from "next/font/local";

const myFont = localFont({
  src: "../fonts/MyFont.woff2",
});
```

তারপর:

```jsx
<body className={myFont.className}>
```

---
Next.js-এ যেকোনো Google Font ব্যবহার করতে মূলত ৩টা জিনিস change করতে হবে। 😊

## ১. Google Fonts থেকে font বেছে নাও

[Google Fonts](https://fonts.google.com/) থেকে পছন্দের font-এর নাম নাও। যেমন: Roboto, Poppins, Inter।

## ২. `layout.tsx`-এ ৩টি জায়গা পরিবর্তন করো

উদাহরণ হিসেবে Poppins ব্যবহার করি:

```
import { Poppins } from "next/font/google";

const poppins = Poppins({
  weight: ["400", "700"],
  subsets: ["latin"],
});
```

তারপর `<html>`-এ:

```
<html lang="en" className={`${poppins.className} h-full antialiased`}>
```

## ৩. কোন কোন জিনিস change করবে?

|কী পরিবর্তন করবে|উদাহরণ|
|---|---|
|Font import|`Poppins`|
|Font function|`Poppins({...})`|
|Variable name|`poppins`|
|HTML class|`poppins.className`|
|Weight|Font-এর available weight অনুযায়ী|
|Subset|সাধারণত `latin`|

## সম্পূর্ণ উদাহরণ

```

import type { Metadata } from "next";
import { Poppins } from "next/font/google";
import "./globals.css";

const poppins = Poppins({
  weight: ["400", "700"],
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "My Website",
  description: "My Next.js website",
};

export default function RootLayout({
  children,
}: LayoutProps<"/">) {
  return (
    <html
      lang="en"
      className={`${poppins.className} h-full antialiased`}
    >
      <body className="min-h-full flex flex-col">
        {children}
      </body>
    </html>
  );
}
```

## মনে রাখার সহজ নিয়ম

যেমন, Roboto-এর পরিবর্তে Inter ব্যবহার করতে চাইলে:

- `Roboto` → `Inter`
    
- `const roboto` → `const inter`
    
- `roboto.className` → `inter.className`
    

সতর্কতা: শুধু Google Fonts-এ font আছে বলেই যে সেটি তোমার Next.js version-এ supported হবে, এমন নয়। Import name ও weight supported কি না যাচাই করবে।

[https://github.com/vercel/next.js/blob/canary/packages/font/src/google/font-data.json](https://github.com/vercel/next.js/blob/canary/packages/font/src/google/font-data.json)


---
Next.js-এ একটা website-এ multiple font ব্যবহার করতে পারো। সবচেয়ে সহজ উপায় হলো `next/font/google` থেকে একাধিক font import করে প্রয়োজন অনুযায়ী apply করা।

## 1. একাধিক Google Font import করো

ধরো, তুমি `Poppins` আর `Roboto` ব্যবহার করবে।

`app/layout.tsx`

```
import { Poppins, Roboto } from "next/font/google";

const poppins = Poppins({
  subsets: ["latin"],
  weight: ["400", "700"],
  variable: "--font-poppins",
});

const roboto = Roboto({
  subsets: ["latin"],
  weight: ["400", "700"],
  variable: "--font-roboto",
});

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body className={`${poppins.variable} ${roboto.variable}`}>
        {children}
      </body>
    </html>
  );
}
```

এখানে `variable` দিয়ে প্রতিটি font-এর জন্য আলাদা CSS variable তৈরি করেছি।

## 2. CSS দিয়ে আলাদা জায়গায় font ব্যবহার করো

`app/globals.css`

```
.heading {
  font-family: var(--font-poppins);
}

.paragraph {
  font-family: var(--font-roboto);
}
```

তারপর component-এ:

```
export default function Home() {
  return (
    <main>
      <h1 className="heading">
        Welcome to my website
      </h1>

      <p className="paragraph">
        This is a paragraph using another font.
      </p>
    </main>
  );
}
```

এভাবে font ভাগ করতে পারো

## Heading → Poppins

Body text → Roboto

Button → Poppins, অথবা design অনুযায়ী অন্য font

## 3. Tailwind CSS ব্যবহার করলে

যদি Tailwind ব্যবহার করো, তাহলে `className` দিয়েও font apply করতে পারো। যেমন:

```
<h1 className={`${poppins.className} text-3xl`}>
  Welcome
</h1>
```

তবে মনে রেখো, `poppins.className` পুরো element-এর font সেট করে। একই element-এ একাধিক font variable দিয়ে ব্যবহার করতে চাইলে CSS-এর `font-family` বা Tailwind-এর custom font utility ব্যবহার করতে পারো।

আমার পরামর্শ: পুরো website-এর সাধারণ text-এর জন্য একটা font রাখো, আর heading বা বিশেষ section-এর জন্য অন্য font ব্যবহার করো। এতে design consistent থাকবে।






# 6. Image Optimization

Next.js-এর সবচেয়ে গুরুত্বপূর্ণ feature:

```jsx
import Image from "next/image";
```

তারপর:

```jsx
<Image
  src="/profile.jpg"
  alt="Profile"
  width={500}
  height={500}
/>
```

এটা সাধারণ:

```html
<img src="/profile.jpg" />
```

এর চেয়ে Next.js-এর image optimization features ব্যবহার করতে দেয়।

---

# 7. Image কোথায় রাখবে?

Local image হলে:

```text
public/
├── images/
│   ├── laptop.jpg
│   └── phone.jpg
```

তারপর:

```jsx
<Image
  src="/images/laptop.jpg"
  alt="Laptop"
  width={800}
  height={600}
/>
```

---

# 8. Responsive Image

যদি image container-এর পুরো width নেয়:

```jsx
<div className="relative h-64 w-full">
  <Image
    src="/images/laptop.jpg"
    alt="Laptop"
    fill
    className="object-cover"
  />
</div>
```

এখানে:

```jsx
fill
```

image-কে parent container fill করতে দেয়।

Parent সাধারণত:

```css
position: relative;
```

হতে হয়।

Tailwind:

```text
relative
```

---

# 9. `sizes` ব্যবহার

Responsive image হলে:

```jsx
<Image
  src="/images/laptop.jpg"
  alt="Laptop"
  fill
  sizes="(max-width: 768px) 100vw, 50vw"
  className="object-cover"
/>
```

এটা browser-কে বুঝতে সাহায্য করে কোন screen size-এ image কতটা জায়গা নেবে।

---

# 10. Remote Image

ধরো Django API থেকে image URL আসছে:

```json
{
  "id": 1,
  "name": "Laptop",
  "image": "https://example.com/laptop.jpg"
}
```

তখন:

```jsx
<Image
  src={product.image}
  alt={product.name}
  width={500}
  height={500}
/>
```

কিন্তু external domain Next.js configuration-এ allow করতে হবে।

`next.config.js`:

```js
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "example.com",
      },
    ],
  },
};

export default nextConfig;
```

তারপর server restart করতে হবে।

---
```jsx
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
  cacheComponents: true,
  partialPrefetching: true,
  turbopack: {
    rules: {
      "*.css": {
        loaders: ["@tailwindcss/turbopack"],
        as: "*.css",
      },
    },
  },
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "imgs.search.brave.com",
        pathname: "/**",
      },
    ],
  },
};

export default nextConfig;
```


```

---

# 11. `priority`

যে image page-এর সবচেয়ে গুরুত্বপূর্ণ এবং initial viewport-এ দেখা যায়, সেখানে priority ব্যবহার করা যায়:

```jsx
<Image
  src="/images/hero.jpg"
  alt="Hero"
  width={1200}
  height={600}
  priority
/>
```

যেমন:

```text
Homepage
┌─────────────────────────┐
│       HERO IMAGE        │ ← priority
│                         │
└─────────────────────────┘

      ↓ scroll

┌───────┐ ┌───────┐
│Image  │ │Image  │ ← lazy loading
└───────┘ └───────┘
```

সব image-এ `priority` দেওয়া উচিত না।

---

# 12. Image quality

প্রয়োজনে:

```jsx
<Image
  src="/images/product.jpg"
  alt="Product"
  width={500}
  height={500}
  quality={75}
/>
```

সাধারণত default optimization-ই যথেষ্ট।

---

# 13. `loading="lazy"`

সাধারণভাবে Next.js-এর `Image` নিচের দিকের image lazy-load করতে পারে।

তাই সাধারণ image-এর জন্য আলাদা করে:

```jsx
loading="lazy"
```

দেওয়ার প্রয়োজন অনেক সময় হয় না।

---

# 14. Font + Image project structure

তোমার project:

```text
src/
├── app/
│   ├── layout.jsx
│   ├── page.jsx
│   └── globals.css
│
├── components/
│   ├── Navbar.jsx
│   └── ProductCard.jsx
│
├── lib/
│   └── api/
│
└── fonts/
    └── MyFont.woff2

public/
└── images/
    ├── hero.jpg
    └── logo.png
```

---

# 15. তোমার জন্য সবচেয়ে important rule

### Fonts

```text
Google Font
      ↓
next/font/google

Custom Font
      ↓
next/font/local
```

### Images

```text
Local image
      ↓
next/image

External image
      ↓
next/image + remotePatterns
```

### সাধারণভাবে

```jsx
import Image from "next/image";
```

ব্যবহার করবে, আর:

```jsx
<img />
```

শুধু বিশেষ প্রয়োজন হলে ব্যবহার করবে।

---

## Real-world example

তোমার **DRF + Next.js e-commerce** project ধরো:

```text
Django
   ↓
Product API
   ↓
{
  name: "Laptop",
  image: "https://api.example.com/media/laptop.jpg"
}
   ↓
Next.js
   ↓
<Image />
   ↓
Optimized image
   ↓
Browser
```

আর application font:

```text
next/font
   ↓
Font optimized
   ↓
Next.js application
```

**এটাই Next.js-এর Font ও Image Optimization-এর মূল ধারণা।**

---
