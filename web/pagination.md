```js
const Pagination = ({ totalPages, currentPage, handlePageChange }) => {
  return (
    <div className="flex justify-center mb-6">
      {Array.from({ length: totalPages }, (_, i) => (
        <button
          key={i}
          onClick={() => handlePageChange(i + 1)}
          className={`mx-1 px-3 py-1 rounded ${
            currentPage === i + 1 ? "bg-secondary text-white" : "bg-gray-200"
          }`}
        >
          {i + 1}
        </button>
      ))}
    </div>
  );
};

export default Pagination;
```



অবশ্যই। তোমার বর্তমান component-টা basic। যদি **যেকোনো Django/DRF + React project-এ reusable pagination component** বানাতে চাও, তাহলে আমি এটাকে একটু production-ready করতাম।

এতে থাকবে:

* Previous / Next button
* First / Last page
* Active page
* অনেক page হলে `...`
* Disabled state
* Responsive design
* Tailwind CSS
* Reusable props
* `totalPages = 1` হলে unnecessary pagination hide
* `aria` accessibility

### Reusable `Pagination.jsx`

```jsx
import {
  ChevronLeft,
  ChevronRight,
  ChevronsLeft,
  ChevronsRight,
} from "lucide-react";

const Pagination = ({
  totalPages = 1,
  currentPage = 1,
  handlePageChange,
  siblingCount = 1,
}) => {
  // Nothing to paginate
  if (totalPages <= 1) {
    return null;
  }

  // Prevent invalid page numbers
  const safeCurrentPage = Math.min(
    Math.max(currentPage, 1),
    totalPages
  );

  const createPageNumbers = () => {
    const totalPageNumbers = siblingCount * 2 + 5;

    // If total pages are small, show all pages
    if (totalPages <= totalPageNumbers) {
      return Array.from(
        { length: totalPages },
        (_, index) => index + 1
      );
    }

    const leftSibling = Math.max(
      safeCurrentPage - siblingCount,
      1
    );

    const rightSibling = Math.min(
      safeCurrentPage + siblingCount,
      totalPages
    );

    const showLeftDots = leftSibling > 2;
    const showRightDots = rightSibling < totalPages - 1;

    // Example:
    // 1 2 3 ... 10
    if (!showLeftDots && showRightDots) {
      const leftItemCount = 3 + siblingCount * 2;

      return [
        ...Array.from(
          { length: leftItemCount },
          (_, index) => index + 1
        ),
        "...",
        totalPages,
      ];
    }

    // Example:
    // 1 ... 8 9 10
    if (showLeftDots && !showRightDots) {
      const rightItemCount = 3 + siblingCount * 2;

      return [
        1,
        "...",
        ...Array.from(
          { length: rightItemCount },
          (_, index) =>
            totalPages - rightItemCount + index + 1
        ),
      ];
    }

    // Example:
    // 1 ... 5 6 7 ... 20
    return [
      1,
      "...",
      ...Array.from(
        { length: rightSibling - leftSibling + 1 },
        (_, index) => leftSibling + index
      ),
      "...",
      totalPages,
    ];
  };

  const pages = createPageNumbers();

  const goToPage = (page) => {
    if (
      page >= 1 &&
      page <= totalPages &&
      page !== safeCurrentPage
    ) {
      handlePageChange(page);
    }
  };

  const baseButton =
    "inline-flex items-center justify-center rounded-lg border text-sm font-medium transition-all duration-200";

  const normalButton =
    "border-gray-200 bg-white text-gray-700 hover:border-secondary hover:bg-secondary/10";

  const activeButton =
    "border-secondary bg-secondary text-white shadow-md";

  const disabledButton =
    "cursor-not-allowed border-gray-100 bg-gray-100 text-gray-400";

  return (
    <nav
      className="flex items-center justify-center py-6"
      aria-label="Pagination"
    >
      <div className="flex items-center gap-1 sm:gap-2">

        {/* First Page */}
        <button
          type="button"
          onClick={() => goToPage(1)}
          disabled={safeCurrentPage === 1}
          aria-label="Go to first page"
          className={`
            ${baseButton}
            hidden h-9 w-9 sm:flex
            ${
              safeCurrentPage === 1
                ? disabledButton
                : normalButton
            }
          `}
        >
          <ChevronsLeft size={17} />
        </button>

        {/* Previous */}
        <button
          type="button"
          onClick={() => goToPage(safeCurrentPage - 1)}
          disabled={safeCurrentPage === 1}
          aria-label="Go to previous page"
          className={`
            ${baseButton}
            h-9 w-9
            ${
              safeCurrentPage === 1
                ? disabledButton
                : normalButton
            }
          `}
        >
          <ChevronLeft size={17} />
        </button>

        {/* Page Numbers */}
        {pages.map((page, index) => {
          if (page === "...") {
            return (
              <span
                key={`dots-${index}`}
                className="flex h-9 w-9 items-center justify-center text-gray-500"
              >
                ...
              </span>
            );
          }

          return (
            <button
              key={page}
              type="button"
              onClick={() => goToPage(page)}
              aria-label={`Go to page ${page}`}
              aria-current={
                safeCurrentPage === page
                  ? "page"
                  : undefined
              }
              className={`
                ${baseButton}
                h-9 min-w-9 px-3
                ${
                  safeCurrentPage === page
                    ? activeButton
                    : normalButton
                }
              `}
            >
              {page}
            </button>
          );
        })}

        {/* Next */}
        <button
          type="button"
          onClick={() => goToPage(safeCurrentPage + 1)}
          disabled={safeCurrentPage === totalPages}
          aria-label="Go to next page"
          className={`
            ${baseButton}
            h-9 w-9
            ${
              safeCurrentPage === totalPages
                ? disabledButton
                : normalButton
            }
          `}
        >
          <ChevronRight size={17} />
        </button>

        {/* Last Page */}
        <button
          type="button"
          onClick={() => goToPage(totalPages)}
          disabled={safeCurrentPage === totalPages}
          aria-label="Go to last page"
          className={`
            ${baseButton}
            hidden h-9 w-9 sm:flex
            ${
              safeCurrentPage === totalPages
                ? disabledButton
                : normalButton
            }
          `}
        >
          <ChevronsRight size={17} />
        </button>

      </div>
    </nav>
  );
};

export default Pagination;
```

### ব্যবহার

প্রথমে icon package লাগবে:

```bash
npm install lucide-react
```

তারপর:

```jsx
import Pagination from "./components/Pagination";
```

Parent component:

```jsx
const [currentPage, setCurrentPage] = useState(1);

const handlePageChange = (page) => {
  setCurrentPage(page);
};
```

তারপর:

```jsx
<Pagination
  totalPages={20}
  currentPage={currentPage}
  handlePageChange={handlePageChange}
/>
```

তখন শুরুতে দেখতে পারে:

```text
«  ‹  1  2  3  4  5  ...  20  ›  »
```

ধরো তুমি page 10-এ গেলে:

```text
«  ‹  1  ...  9  10  11  ...  20  ›  »
```

আর শেষ page-এ গেলে:

```text
«  ‹  1  ...  16  17  18  19  20  ›  »
```

### DRF-এর সাথে ব্যবহার

এখানেই এই component-টা সবচেয়ে useful হবে।

ধরো Django API response:

```json
{
  "count": 200,
  "next": "...?page=2",
  "previous": null,
  "results": []
}
```

যদি প্রতি page-এ 10টা item থাকে:

```js
const totalPages = Math.ceil(data.count / 10);
```

তারপর:

```jsx
<Pagination
  totalPages={totalPages}
  currentPage={currentPage}
  handlePageChange={handlePageChange}
/>
```

এবং:

```jsx
const handlePageChange = (page) => {
  setCurrentPage(page);
};
```

API request:

```js
axios.get(`/api/products/?page=${currentPage}`);
```

তাহলে পুরো flow হবে:

```text
User clicks page 3
        ↓
handlePageChange(3)
        ↓
setCurrentPage(3)
        ↓
React re-render
        ↓
API request
        ↓
/api/products/?page=3
        ↓
Django DRF
        ↓
page 3 products
        ↓
UI update
```

**একটা গুরুত্বপূর্ণ design principle:** Pagination component-কে API-aware না রাখাই ভালো। অর্থাৎ component-এর ভিতরে `axios`, `fetch`, Django URL ইত্যাদি রাখবে না। শুধু `currentPage → handlePageChange(page)` রাখবে। তাহলে একই component **e-commerce, hotel, job portal, news portal, admin dashboard—সব জায়গায়** ব্যবহার করতে পারবে।




----
# fech product by hook make

```js
import { useEffect, useState } from "react";
import apiClient from "../services/api-client";

const useFetchProduct = (
  currentPage,
  priceRange,
  selectedCategory,
  searchQuery,
  sortOrder
) => {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(false);
  const [totalPages, setTotalPages] = useState(0);

  useEffect(() => {
    const fetchProducts = async () => {
      setLoading(true);
      const url = `/products/?price__gt=${priceRange[0]}&price__lt=${priceRange[1]}&page=${currentPage}&category_id=${selectedCategory}&search=${searchQuery}&ordering=${sortOrder}`;
      try {
        const response = await apiClient.get(url);
        const data = await response.data;

        setProducts(data.results);
        setTotalPages(Math.ceil(data.count / data.results.length));
      } catch (error) {
        console.log(error);
      } finally {
        setLoading(false);
      }
    };
    fetchProducts();
  }, [currentPage, priceRange, selectedCategory, searchQuery, sortOrder]);

  return { products, loading, totalPages };
};

export default useFetchProduct;
```


#  fetch categories

```js
import { useEffect, useState } from "react";
import apiClient from "../services/api-client";

const useFetchCategories = () => {
  const [categories, setCategories] = useState([]);
  useEffect(() => {
    apiClient.get("/categories").then((res) => setCategories(res.data));
  }, []);

  return categories;
};

export default useFetchCategories;
```


# shop page where call hook and pagination

```js
import { useState } from "react";
import ProductList from "./ProductList";
import Pagination from "./Pagination";
import useFetchProduct from "../../hooks/useFetchProducts";
import FilterSection from "./FilterSection";
import useFetchCategories from "../../hooks/useFetchCategories";

const ShopPage = () => {
  const [currentPage, setCurrentPage] = useState(1);
  const [priceRange, setPriceRange] = useState([0, 1000]);
  const [selectedCategory, setSelecetedCategory] = useState("");
  const [searchQuery, setSearchQuery] = useState("");
  const [sortOrder, setSortOrder] = useState("");

  const { products, loading, totalPages } = useFetchProduct(
    currentPage,
    priceRange,
    selectedCategory,
    searchQuery,
    sortOrder
  );

  const categories = useFetchCategories();

  const handlePriceChange = (index, value) => {
    setPriceRange((prev) => {
      const newRange = [...prev];
      newRange[index] = value;
      return newRange;
    });
    setCurrentPage(1);
  };

  return (
    <div className="max-w-7xl mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold mb-8">Shop Our Products</h1>
      <FilterSection
        priceRange={priceRange}
        handlePriceChange={handlePriceChange}
        categories={categories}
        selectedCategory={selectedCategory}
        handleCategoryChange={setSelecetedCategory}
        searchQuery={searchQuery}
        handleSearchQuery={setSearchQuery}
        sortOrder={sortOrder}
        handleSorting={setSortOrder}
      />
      <ProductList products={products} loading={loading} />
      <Pagination
        totalPages={totalPages}
        currentPage={currentPage}
        handlePageChange={setCurrentPage}
      />
    </div>
  );
};

export default ShopPage;
```


# product show

```js
import ProductItem from "../Products/ProductItem";

const ProductList = ({ products, loading }) => {
  if (loading)
    return (
      <div className="flex justify-center items-center py-10 min-h-screen">
        <span className="loading loading-spinner loading-xl text-secondary"></span>
      </div>
    );

  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {products.map((product) => (
        <ProductItem product={product} key={product.id} />
      ))}
    </div>
  );
};

export default ProductList;
```

# filter ui 
```js
const FilterSection = ({
  priceRange,
  handlePriceChange,
  categories,
  selectedCategory,
  handleCategoryChange,
  searchQuery,
  handleSearchQuery,
  sortOrder,
  handleSorting,
}) => {
  return (
    <div className="mb-8 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
      {/* Price Range */}
      <div className="bg-white p-4 rounded-lg shadow">
        <label className="block text-sm font-medium text-gray-700 mb-2">
          Price Range
        </label>
        {/* Min Range  */}
        <div className="flex items-center space-x-4">
          <input
            type="number"
            min="0"
            max={priceRange[1]}
            value={priceRange[0]}
            onChange={(e) => handlePriceChange(0, Number(e.target.value))}
            className="w-20 p-2 border rounded-md"
          />
          <input
            type="range"
            min="0"
            max={priceRange[1]}
            step="10"
            value={priceRange[0]}
            onChange={(e) => handlePriceChange(0, Number(e.target.value))}
            className="w-full"
          />
        </div>
        {/* Max Range  */}
        <div className="flex items-center space-x-4">
          <input
            type="number"
            min={priceRange[0]}
            max="1000"
            value={priceRange[1]}
            onChange={(e) => handlePriceChange(1, Number(e.target.value))}
            className="w-20 p-2 border rounded-md"
          />
          <input
            type="range"
            min={priceRange[0]}
            max="1000"
            step="10"
            value={priceRange[1]}
            onChange={(e) => handlePriceChange(1, Number(e.target.value))}
            className="w-full"
          />
        </div>

        <div className="flex justify-between text-sm text-gray-600 mt-2">
          <span>${priceRange[0]}</span>
          <span>${priceRange[1]}</span>
        </div>
      </div>

      {/* Category Filter */}
      <div className="bg-white p-4 rounded-lg shadow">
        <label className="block text-sm font-medium text-gray-700 mb-2">
          Category
        </label>
        <select
          className="w-full p-2 border rounded-md"
          value={selectedCategory}
          onChange={(e) => handleCategoryChange(e.target.value)}
        >
          <option value="">All Categories</option>
          {categories.map((category) => (
            <option key={category.id} value={category.id}>
              {category.name}
            </option>
          ))}
        </select>
      </div>

      {/* Search */}
      <div className="bg-white p-4 rounded-lg shadow">
        <label className="block text-sm font-medium text-gray-700 mb-2">
          Search
        </label>
        <input
          type="text"
          value={searchQuery}
          onChange={(e) => handleSearchQuery(e.target.value)}
          placeholder="Search books..."
          className="w-full p-2 border rounded-md"
        />
      </div>

      {/* Sorting  */}
      <div className="bg-white p-4 rounded-lg shadow">
        <label className="block text-sm font-medium text-gray-700 mb-2">
          Sort By Price
        </label>
        <select
          className="w-full p-2 border rounded-md"
          value={sortOrder}
          onChange={(e) => handleSorting(e.target.value)}
        >
          <option value="">Default</option>
          <option value="price">Price: Low to High</option>
          <option value="-price">Price: High to Low</option>
        </select>
      </div>
    </div>
  );
};

export default FilterSection;
```

হ্যাঁ—এখানে আসল সমস্যা **Tailwind class মুখস্থ করা না**, বরং **UI দেখলে কীভাবে ভেঙে চিন্তা করবে** সেটা শেখা। এটা practice করলে মাথায় আসবে।

তুমি যে `FilterSection` বানিয়েছো, সেটা আমি সাধারণত **৪ ধাপে চিন্তা** করতাম।

## 1. প্রথমে code না, UI-কে অংশে ভাঙো

ধরো requirement:

> Product filter করার একটা section বানাতে হবে।

সাথে সাথে JSX লিখবে না।

আগে কাগজে লিখবে:

```text
Product Filter
│
├── Price
│   ├── Min price
│   ├── Max price
│   └── Slider
│
├── Category
│   └── Select
│
├── Search
│   └── Input
│
└── Sort
    └── Select
```

ব্যস। এখন তোমার UI-এর structure পরিষ্কার।

---

# 2. তারপর প্রতিটা অংশের জন্য HTML element চিনবে

নিজেকে জিজ্ঞেস করবে:

> এই জিনিসটার জন্য কোন HTML element দরকার?

যেমন:

```text
Price       → input type number + range
Category    → select
Search      → input text
Sort        → select
```

তাহলে basic HTML দাঁড়াবে:

```jsx
<div>
  <div>
    <label>Price</label>
    <input type="number" />
    <input type="range" />
  </div>

  <div>
    <label>Category</label>
    <select />
  </div>

  <div>
    <label>Search</label>
    <input type="text" />
  </div>

  <div>
    <label>Sort</label>
    <select />
  </div>
</div>
```

**এখনও Tailwind লিখবে না।**

---

# 3. এরপর layout চিন্তা করবে

এখন প্রশ্ন:

> চারটা filter পাশাপাশি থাকবে নাকি নিচে নিচে?

Desktop-এ তুমি চাও:

```text
┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
│   Price    │ │  Category  │ │   Search   │ │    Sort    │
│            │ │            │ │            │ │            │
└────────────┘ └────────────┘ └────────────┘ └────────────┘
```

Mobile-এ:

```text
┌────────────────────────┐
│         Price          │
└────────────────────────┘

┌────────────────────────┐
│       Category         │
└────────────────────────┘

┌────────────────────────┐
│        Search          │
└────────────────────────┘

┌────────────────────────┐
│         Sort           │
└────────────────────────┘
```

তখন তোমার মাথায় আসবে:

```text
grid
```

তারপর:

```jsx
grid-cols-1
md:grid-cols-2
lg:grid-cols-4
```

এইভাবেই Tailwind class **মুখস্থ থেকে নয়, design requirement থেকে** আসবে।

---

# 4. তারপর styling

প্রতিটা filter একটা card।

তাহলে card-এর বৈশিষ্ট্য:

```text
white background
padding
rounded corner
shadow
```

Tailwind:

```jsx
bg-white p-4 rounded-lg shadow
```

এখন পুরো container:

```jsx
<div className="mb-8 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
```

এখানে প্রত্যেকটা class-এর কারণ আছে:

```text
mb-8          → নিচে space

grid          → grid layout

grid-cols-1   → mobile-এ 1 column

md:grid-cols-2
              → medium screen-এ 2 column

lg:grid-cols-4
              → large screen-এ 4 column

gap-6         → card-এর মধ্যে gap
```

এভাবে চিন্তা করলে class মনে রাখার দরকার অনেক কমে যায়।

---

# সবচেয়ে গুরুত্বপূর্ণ: UI design করার একটা formula রাখো

যেকোনো UI দেখলে এই sequence follow করো:

```text
1. What?
   ↓
2. Sections কী কী?
   ↓
3. প্রতিটা section-এর HTML element কী?
   ↓
4. Layout কী?
   ↓
5. Spacing কী?
   ↓
6. Color কী?
   ↓
7. Border / Radius?
   ↓
8. Interaction কী?
   ↓
9. Responsive কীভাবে হবে?
```

---

# ধরো তোমাকে নতুন একটা UI বানাতে দিল

Requirement:

> E-commerce product page বানাও।

সাথে সাথে code না।

প্রথমে:

```text
Product Page
│
├── Header
│
├── Filter
│   ├── Search
│   ├── Category
│   ├── Price
│   └── Sort
│
├── Products
│   └── Product Card
│       ├── Image
│       ├── Name
│       ├── Price
│       ├── Rating
│       └── Button
│
└── Pagination
```

তারপর layout:

```text
Desktop

┌──────────────────────────────────────────┐
│                  Header                  │
├───────────────┬──────────────────────────┤
│               │                          │
│    Filters    │       Products           │
│               │                          │
│               │   ┌───┐ ┌───┐ ┌───┐    │
│               │   │   │ │   │ │   │    │
│               │   └───┘ └───┘ └───┘    │
│               │                          │
├───────────────┴──────────────────────────┤
│               Pagination                 │
└──────────────────────────────────────────┘
```

এখন তোমার মাথায় automatically আসবে:

```text
main container → max-width

layout → grid/flex

sidebar → width

products → grid

cards → rounded/shadow

pagination → flex
```

---

# একটা খুব গুরুত্বপূর্ণ skill: Reference দেখে copy না, analyze করো

ধরো তুমি কোনো website দেখলে:

```text
┌──────────────────────────────┐
│ Search                       │
├──────────────────────────────┤
│ Category ▼                   │
├──────────────────────────────┤
│ Price                        │
│ ─────●────────               │
├──────────────────────────────┤
│ Sort ▼                       │
└──────────────────────────────┘
```

নিজেকে জিজ্ঞেস করবে:

**১. Outer structure কী?**

```jsx
<div>
```

**২. Layout কী?**

```text
vertical → flex-col
```

**৩. প্রত্যেকটা section কী?**

```text
Search → input
Category → select
Price → range
Sort → select
```

**৪. প্রত্যেকটা section-এর visual container আছে?**

হ্যাঁ:

```jsx
bg-white rounded-lg shadow
```

**৫. Spacing?**

```jsx
p-4
gap-4
```

এই analysis করতে করতে তুমি নিজে UI বানাতে পারবে।

---

# তোমার জন্য সবচেয়ে ভালো practice

তুমি এখন থেকে **"UI বানাবো"** বলে বসবে না।

বরং একটা UI দেখে এই ৫টা প্রশ্নের উত্তর লিখবে:

```text
1. Structure কী?
2. Layout কী?
3. Components কী কী?
4. State কী কী?
5. User interaction কী?
```

উদাহরণ:

### Filter UI

```text
Structure:
FilterSection
 ├── Price
 ├── Category
 ├── Search
 └── Sort

Layout:
Grid

State:
priceRange
selectedCategory
searchQuery
sortOrder

Interaction:
price change
category change
search
sorting

API:
GET /products/
```

তারপর code।

---

## আর একটা জিনিস তোমার ক্ষেত্রে খুব গুরুত্বপূর্ণ

তুমি যেহেতু React + Django/DRF শিখছো, **UI এবং logic একসাথে চিন্তা করবে না।**

এইভাবে চিন্তা করো:

```text
             UI
              │
       ┌──────┴──────┐
       │             │
   Presentation    Interaction
       │             │
   Tailwind       Handler
                     │
                     ↓
                  State
                     │
                     ↓
                Custom Hook
                     │
                     ↓
                  API
                     │
                     ↓
                  Django
```

তাহলে `FilterSection`, `useFetchProduct`, `Pagination`—এগুলো কেন আলাদা component/hook হয়েছে সেটা পরিষ্কার হয়ে যাবে।

**UI design skill = component breakdown + layout thinking + spacing + responsive thinking + repeated practice.**

Tailwind মুখস্থ করা দ্বিতীয় বিষয়। তুমি চাইলে আমি তোমাকে **"একদম zero থেকে UI দেখে কীভাবে React + Tailwind component বানাতে হয়" — 10টা practical class-এর মতো করে** শেখাতে পারি।


হ্যাঁ, এখন বুঝতে পারছি তোমার আসল সমস্যা। **UI বানাতে পারো, কিন্তু বড় UI-কে কোন কোন component-এ ভাঙবে, কোনটা parent হবে, কোনটা child হবে, কোন logic কোথায় থাকবে—এই architecture thinking-টাই missing।**

এটা খুব common। এর জন্য একটা fixed method follow করো।

## ১. প্রথমে একটা rule মাথায় রাখো

React component বানানোর সময় **"কোন HTML আলাদা করব?"** এটা ভাববে না।

ভাববে:

> **"এই অংশটার কি আলাদা একটা responsibility আছে?"**

যদি থাকে → component বানাও।

যেমন তোমার Product Page:

```text
Product Page
│
├── FilterSection
├── ProductList
│   └── ProductCard
└── Pagination
```

কেন?

কারণ প্রত্যেকটার আলাদা responsibility:

```text
FilterSection → filter input নেওয়া
ProductList   → products-এর list দেখানো
ProductCard   → একটি product দেখানো
Pagination    → page পরিবর্তন
```

এটাই componentization।

---

# ২. একটা বড় page দেখলে প্রথমে ৩ level-এ ভাঙবে

ধরো Product Listing Page।

প্রথমে:

```text
ProductPage
│
├── Header
├── Filters
├── Products
└── Pagination
```

তারপর Products-কে ভাঙবে:

```text
Products
│
├── ProductCard
├── ProductCard
├── ProductCard
└── ProductCard
```

তারপর ProductCard:

```text
ProductCard
│
├── ProductImage
├── ProductInfo
│   ├── ProductName
│   ├── Price
│   └── Rating
└── AddToCartButton
```

কিন্তু এখানে একটা গুরুত্বপূর্ণ ব্যাপার:

**প্রতিটা ছোট জিনিস component বানাতে হবে না।**

---

# ৩. কখন component বানাবে?

এই ৫টা প্রশ্ন করো।

### প্রশ্ন ১ — এটা কি নিজস্ব responsibility?

```text
Pagination
```

হ্যাঁ → component।

---

### প্রশ্ন ২ — এটা কি বারবার ব্যবহার হবে?

```text
ProductCard
```

এক page-এ ২০টা product থাকলেও একই structure repeat হচ্ছে।

তাই:

```jsx
<ProductCard />
```

---

### প্রশ্ন ৩ — এটা কি বড় হয়ে যাচ্ছে?

ধরো:

```jsx
ProductPage.jsx
```

এর ভিতরে 500 lines হয়ে গেছে।

তখন ভাগ করো।

---

### প্রশ্ন ৪ — এই অংশটা independently change হতে পারে?

যেমন:

```text
FilterSection
```

আগামীকাল filter design পরিবর্তন হতে পারে।

তাই আলাদা component ভালো।

---

### প্রশ্ন ৫ — component আলাদা করলে parent সহজ হয়?

এটা সবচেয়ে important।

যদি:

```text
ProductPage.jsx
```

অনেক complicated হয়ে যায়:

```jsx
// 300 lines
// filter
// product
// pagination
// modal
// loading
// error
```

তাহলে ভাগ করো।

---

# ৪. কিন্তু তোমার সবচেয়ে বড় confusion: "কোথায় রাখব?"

এখানে একটা practical structure follow করতে পারো।

```text
src/
│
├── components/
│   │
│   ├── common/
│   │   ├── Button.jsx
│   │   ├── Modal.jsx
│   │   ├── Spinner.jsx
│   │   └── Pagination.jsx
│   │
│   ├── products/
│   │   ├── ProductCard.jsx
│   │   ├── ProductList.jsx
│   │   ├── ProductFilter.jsx
│   │   └── ProductSort.jsx
│   │
│   └── layout/
│       ├── Navbar.jsx
│       ├── Footer.jsx
│       └── Sidebar.jsx
│
├── pages/
│   ├── ProductPage.jsx
│   ├── ProductDetailsPage.jsx
│   └── HomePage.jsx
│
├── hooks/
│   ├── useFetchProducts.js
│   └── useDebounce.js
│
├── services/
│   └── api-client.js
│
├── context/
│   └── AuthContext.jsx
│
└── utils/
    └── formatPrice.js
```

তবে **এটাই একমাত্র correct structure না**। Project বড় হলে feature-based structure আরও ভালো হতে পারে।

---

# ৫. তোমার Product project-এ আমি feature-based structure ব্যবহার করতাম

যেহেতু তুমি e-commerce project করছো:

```text
src/
│
├── features/
│   │
│   └── products/
│       │
│       ├── components/
│       │   ├── ProductCard.jsx
│       │   ├── ProductList.jsx
│       │   ├── FilterSection.jsx
│       │   └── ProductPagination.jsx
│       │
│       ├── hooks/
│       │   └── useFetchProducts.js
│       │
│       ├── services/
│       │   └── product-api.js
│       │
│       └── pages/
│           ├── ProductListPage.jsx
│           └── ProductDetailPage.jsx
│
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   └── Button.jsx
│
├── hooks/
│   └── useDebounce.js
│
├── services/
│   └── api-client.js
│
└── App.jsx
```

এখানে একটা সুন্দর rule:

> **যে code শুধু Product feature-এর জন্য, সেটা Product-এর folder-এর ভিতরে।**

যেমন:

```text
useFetchProducts.js
```

শুধু product-এর জন্য।

তাই:

```text
features/products/hooks/
```

এর মধ্যে।

কিন্তু:

```text
useDebounce.js
```

Product ছাড়াও অন্য জায়গায় ব্যবহার হতে পারে।

তাই:

```text
hooks/
```

এ থাকবে।

---

# ৬. এখন তোমার বর্তমান code-গুলো কোথায় যাবে?

তুমি যেগুলো আমাকে দেখিয়েছো:

### `FilterSection`

```text
features/
└── products/
    └── components/
        └── FilterSection.jsx
```

### `Pagination`

যদি শুধু product-এর pagination হয়:

```text
features/
└── products/
    └── components/
        └── ProductPagination.jsx
```

কিন্তু যদি hotel, user, order, product—সব জায়গায় ব্যবহার করো:

```text
components/
└── common/
    └── Pagination.jsx
```

### `useFetchProduct`

```text
features/
└── products/
    └── hooks/
        └── useFetchProducts.js
```

### `apiClient`

```text
services/
└── api-client.js
```

---

# ৭. Parent কে হবে?

এটাও একটা সহজ rule দিয়ে মনে রাখো:

> **যে component পুরো section-এর state/control জানে, সেটা parent।**

তোমার ক্ষেত্রে:

```text
ProductListPage
```

হবে parent।

এর মধ্যে:

```text
ProductListPage
│
├── FilterSection
├── ProductList
│   └── ProductCard
└── Pagination
```

Parent-এর কাছে থাকবে:

```js
currentPage
priceRange
selectedCategory
searchQuery
sortOrder
```

এবং:

```js
handlePriceChange
handleCategoryChange
handleSearchQuery
handleSorting
handlePageChange
```

---

# ৮. Data কোন দিকে যাবে?

React-এ সাধারণত:

```text
Parent
   ↓
Child
```

data যায়।

আর child event পাঠায়:

```text
Child
   ↑
   │
handler
   │
Parent
```

তোমার ক্ষেত্রে:

```text
ProductPage
│
│ props
├──────────────→ FilterSection
│
│ products
├──────────────→ ProductList
│
│ pagination data
└──────────────→ Pagination
```

FilterSection:

```text
User changes category
        ↓
handleCategoryChange()
        ↓
ProductPage
        ↓
setSelectedCategory()
        ↓
useFetchProducts()
        ↓
API
```

---

# ৯. সবচেয়ে গুরুত্বপূর্ণ architecture rule

একটা component-এর মধ্যে এই সব একসাথে ঢুকাবে না:

```jsx
ProductPage.jsx

// API call
// filter
// search
// sorting
// product card
// pagination
// modal
// cart
// authentication
// UI
```

এটা শুরুতে সহজ মনে হবে।

কিন্তু ২-৩ সপ্তাহ পরে:

```text
ProductPage.jsx
→ 700 lines
→ বুঝতে কষ্ট
→ change করলে অন্য জায়গা break
```

তার বদলে:

```text
ProductPage
│
├── FilterSection
├── ProductList
│   └── ProductCard
├── Pagination
│
└── useFetchProducts
```

---

# ১০. কিন্তু আবার অতিরিক্ত component-ও বানাবে না

এটা beginner-এর আরেকটা mistake।

এমন করা দরকার নেই:

```text
ProductCard
│
├── ProductImage
├── ProductTitle
├── ProductPrice
├── ProductRating
├── ProductButton
├── ProductButtonIcon
├── ProductButtonText
└── ProductPriceSymbol
```

যদি এগুলোর আলাদা responsibility না থাকে।

বরং:

```jsx
<ProductCard />
```

এর ভিতরেই:

```jsx
<img />
<h3 />
<p />
<button />
```

থাকতে পারে।

**Componentization-এর উদ্দেশ্য code ছোট করা না; responsibility আলাদা করা।**

---

# ১১. এই mental model-টা মনে রাখো

যেকোনো project শুরু করার সময়:

```text
                PAGE
                 │
        ┌────────┼────────┐
        ↓        ↓        ↓
      Section  Section  Section
        │
        ↓
    Component
        │
        ↓
     Small UI
```

আর logic:

```text
Component
    │
    ├── UI
    │
    └── Event
          │
          ↓
        State
          │
          ↓
        Hook
          │
          ↓
        Service
          │
          ↓
         API
```

---

## তোমার জন্য একটা golden rule

আগামীতে কোনো নতুন page বানানোর সময় **সরাসরি VS Code খুলে coding শুরু করবে না।**

প্রথমে ৫ মিনিট:

```text
1. Page-এর নাম কী?
2. বড় section কয়টা?
3. কোন section reusable?
4. কোন state লাগবে?
5. কোন logic API-related?
```

তারপর একটা tree আঁকবে:

```text
ProductPage
│
├── FilterSection
├── ProductList
│   └── ProductCard
└── Pagination
```

তারপর decide করবে:

```text
UI      → components
State   → parent
API     → hook/service
Reusable → common/components
Feature-specific → features/products/
```

**এই tree আঁকার অভ্যাসটাই তোমার "মাথায় architecture আসছে না" সমস্যাটা সবচেয়ে বেশি ঠিক করবে।** প্রথমে ১০–১৫টা project এ ইচ্ছা করে এভাবে breakdown করলে পরে নতুন UI দেখলেই component structure মাথায় আসতে শুরু করবে।


এটাই React component architecture-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটা। **কোন জিনিস props হিসেবে যাবে—এটা মুখস্থ করার বিষয় না; একটা decision process আছে।**

তোমার `ProductPage → FilterSection → useFetchProduct` example দিয়েই বুঝাই।

---

# 1. প্রথম rule: Child-এর যে জিনিস জানা দরকার, সেটাই props

ধরো:

```text
ProductPage
    │
    └── FilterSection
```

`FilterSection`-কে যদি Category দেখাতে হয়, তাহলে Category data তার দরকার।

তাই:

```jsx
<FilterSection categories={categories} />
```

এখানে:

```text
Parent-এর data
      ↓
    props
      ↓
Child
```

**সহজ প্রশ্ন:**

> "এই child component ঠিকমতো কাজ করতে parent-এর কোন information দরকার?"

সেটাই প্রথমে props candidate।

---

# 2. Props শুধু data না, function-ও হতে পারে

এটা beginner-দের সবচেয়ে বেশি confusing হয়।

ধরো `FilterSection`-এর ভিতরে user category select করল।

Child জানে user কী select করেছে।

কিন্তু `selectedCategory` state আছে Parent-এ।

তাহলে child কী করবে?

Parent-এর function child-কে দেবে:

```jsx
<FilterSection
  selectedCategory={selectedCategory}
  handleCategoryChange={handleCategoryChange}
/>
```

Child:

```jsx
<select
  value={selectedCategory}
  onChange={(e) =>
    handleCategoryChange(e.target.value)
  }
/>
```

এখানে:

```text
selectedCategory
     ↓
Parent → Child

handleCategoryChange
     ↓
Parent → Child

user action
     ↓
Child → function → Parent
```

এটাই React-এর খুব common pattern।

---

# 3. একটা golden question

প্রতিটা component বানানোর পর নিজেকে জিজ্ঞেস করো:

### প্রশ্ন ১:

> **Child-এর UI render করতে কী data দরকার?**

সেগুলো props।

### প্রশ্ন ২:

> **Child user interaction-এর পরে parent-কে কিছু জানাবে?**

তাহলে callback function props।

---

# 4. তোমার `FilterSection`-এর props কীভাবে বের হলো?

তোমার component:

```jsx
<FilterSection
  priceRange={priceRange}
  handlePriceChange={handlePriceChange}
  categories={categories}
  selectedCategory={selectedCategory}
  handleCategoryChange={handleCategoryChange}
  searchQuery={searchQuery}
  handleSearchQuery={handleSearchQuery}
  sortOrder={sortOrder}
  handleSorting={handleSorting}
/>
```

এখন এক এক করে চিন্তা করি।

---

### Price

FilterSection-এ price দেখাতে হবে।

তাই:

```jsx
priceRange
```

দরকার।

User price change করতে পারে।

তাই:

```jsx
handlePriceChange
```

দরকার।

---

### Category

Category dropdown দেখাতে category list দরকার:

```jsx
categories
```

বর্তমান selected category দেখাতে:

```jsx
selectedCategory
```

User category change করলে parent-কে জানাতে:

```jsx
handleCategoryChange
```

---

### Search

Input-এর বর্তমান value:

```jsx
searchQuery
```

User কিছু লিখলে parent-কে জানাতে:

```jsx
handleSearchQuery
```

---

### Sorting

বর্তমান sorting:

```jsx
sortOrder
```

নতুন sorting select করলে:

```jsx
handleSorting
```

---

# 5. কিন্তু সবসময় state props করতে হবে না

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```jsx
const [isOpen, setIsOpen] = useState(false);
```

যদি শুধু `FilterSection`-এর ভিতরের কোনো dropdown open/close করার জন্য লাগে, তাহলে parent-এ নেওয়ার দরকার নেই।

Child-এর ভিতরেই:

```jsx
const [isOpen, setIsOpen] = useState(false);
```

রাখতে পারো।

তাহলে প্রশ্ন হবে:

> **এই state কি অন্য component-এর দরকার?**

### না:

```text
Child-এর ভিতরে রাখো
```

### হ্যাঁ:

```text
Common parent-এ রাখো
↓
props দিয়ে child-কে দাও
```

এটাকে বলে **state lifting**।

---

# 6. খুব সহজ একটা example

ধরো:

```text
ProductPage
│
├── FilterSection
└── ProductList
```

`FilterSection` category change করে।

`ProductList` filtered products দেখায়।

তাহলে:

```text
selectedCategory
```

কার দরকার?

শুধু FilterSection-এর না।

ProductList/API fetching-এরও দরকার।

তাই state থাকবে common parent:

```jsx
const [selectedCategory, setSelectedCategory] =
  useState("");
```

তারপর:

```text
ProductPage
│
├── selectedCategory
│
├── FilterSection
│     ↑
│     └── selectedCategory
│         handleCategoryChange
│
└── ProductList
      ↑
      └── filtered products
```

---

# 7. Data কোন level-এ থাকবে সেটা কীভাবে বুঝবে?

এই প্রশ্ন করো:

> **এই data কে কে ব্যবহার করছে?**

ধরো `categories`:

```text
FilterSection → ব্যবহার করছে
ProductList   → ব্যবহার করছে না
```

তাহলে:

```text
ProductPage
   ↓
FilterSection
```

এখানেই যথেষ্ট।

কিন্তু `products`:

```text
ProductList → ব্যবহার করছে
Pagination  → pagination-related info ব্যবহার করছে
```

তাহলে parent-এ থাকবে।

---

# 8. Props decide করার সবচেয়ে useful diagram

যেকোনো page-এর জন্য এটা আঁকো:

```text
                  Parent
                    │
           ┌────────┴────────┐
           ↓                 ↓
        Child A            Child B
           │
           │ needs:
           ├── data
           ├── state
           └── actions
```

তারপর লিখো:

```text
Child A needs:
    categories
    selectedCategory
    handleCategoryChange
```

তাহলে props হয়ে যাবে:

```jsx
<ChildA
  categories={categories}
  selectedCategory={selectedCategory}
  handleCategoryChange={handleCategoryChange}
/>
```

---

# 9. একটা আরও powerful rule

React-এ **props-এর মাধ্যমে information নিচে যায়**:

```text
Parent
   ↓
Child
   ↓
Grandchild
```

কিন্তু event/notification সাধারণত callback-এর মাধ্যমে উপরে যায়:

```text
Parent
   ↓ function
Child
   │
   │ user clicks
   ↓
callback()
   ↓
Parent state update
```

অর্থাৎ:

```text
DATA
Parent ───────────→ Child

EVENT
Child ───────────→ Parent
       callback
```

এই দুইটা মাথায় থাকলে ৮০% props decision সহজ হয়ে যায়।

---

# 10. কখন props বেশি হয়ে যাচ্ছে?

তোমার current:

```jsx
<FilterSection
  priceRange={}
  handlePriceChange={}
  categories={}
  selectedCategory={}
  handleCategoryChange={}
  searchQuery={}
  handleSearchQuery={}
  sortOrder={}
  handleSorting={}
/>
```

এখানে 8টা props আছে।

এটা **এখনও acceptable**, কারণ সবগুলোই FilterSection-এর responsibility-এর সাথে directly related।

কিন্তু যদি এমন হয়:

```jsx
<ProductPage
  user={}
  products={}
  categories={}
  orders={}
  cart={}
  theme={}
  notifications={}
  priceRange={}
  searchQuery={}
  ...
/>
```

তাহলে architecture problem শুরু হচ্ছে।

তখন ভাববে:

> কেন এত information এক component-এর মধ্যে ঢুকছে?

---

# 11. তোমার project-এর জন্য final mental model

Product page বানানোর সময় এইভাবে চিন্তা করবে:

```text
ProductPage
│
├── কী জানে?
│   ├── products
│   ├── filters
│   ├── currentPage
│   └── categories
│
├── FilterSection
│   ├── needs categories
│   ├── needs selected filters
│   └── needs callbacks
│
├── ProductList
│   └── needs products
│
└── Pagination
    ├── needs currentPage
    ├── needs totalPages
    └── needs handlePageChange
```

তারপর props automatically বের হয়ে যাবে:

```jsx
<FilterSection
  categories={categories}
  priceRange={priceRange}
  selectedCategory={selectedCategory}
  searchQuery={searchQuery}
  sortOrder={sortOrder}
  handlePriceChange={handlePriceChange}
  handleCategoryChange={handleCategoryChange}
  handleSearchQuery={handleSearchQuery}
  handleSorting={handleSorting}
/>

<ProductList
  products={products}
/>

<Pagination
  currentPage={currentPage}
  totalPages={totalPages}
  handlePageChange={handlePageChange}
/>
```

### এক লাইনে মনে রাখো:

> **"Child কী জানবে?" → data props.  
> "Child কী করলে parent-কে জানাতে হবে?" → function props.  
> "এই state কে ব্যবহার করছে?" → যাদের common দরকার তাদের closest common parent-এ state রাখো।**

এই ৩টা প্রশ্নের অভ্যাস হয়ে গেলে **props নিজে থেকেই মাথায় আসবে**—আলাদা করে props মুখস্থ করতে হবে না।


অবশ্যই। তুমি যেহেতু **যেকোনো project-এ reuse করতে চাও**, তাই আমি `Category` আর `Product`-এর জন্য আলাদা hook না বানিয়ে এমনভাবে বানাবো যাতে পরে **API endpoint, query params, pagination, search, filter, sorting** সহজে reuse করা যায়।

### 1. `useFetch.js` — Generic reusable hook

```jsx
import { useEffect, useState } from "react";
import apiClient from "../services/api-client";

const useFetch = (url, params = {}) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      setLoading(true);
      setError(null);

      try {
        const response = await apiClient.get(url, {
          params,
        });

        setData(response.data);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url, JSON.stringify(params)]);

  return {
    data,
    loading,
    error,
  };
};

export default useFetch;
```

এটা **Category/Product specific না**। যেকোনো GET API-তে ব্যবহার করতে পারবে।

---

### 2. `useFetchCategories.js`

এখন generic hook-এর উপর category-specific hook বানাবো।

```jsx
import useFetch from "./useFetch";

const useFetchCategories = () => {
  const { data, loading, error } = useFetch("/categories/");

  return {
    categories: data?.results || [],
    loading,
    error,
  };
};

export default useFetchCategories;
```

ব্যবহার:

```jsx
const {
  categories,
  loading,
  error,
} = useFetchCategories();
```

---

### 3. `useFetchProducts.js`

Product-এর ক্ষেত্রে filter, search, sorting, pagination রাখি:

```jsx
import useFetch from "./useFetch";

const useFetchProducts = ({
  page = 1,
  category = "",
  search = "",
  ordering = "",
  priceMin = "",
  priceMax = "",
} = {}) => {
  const params = {
    page,
    category,
    search,
    ordering,
    price__gte: priceMin,
    price__lte: priceMax,
  };

  const { data, loading, error } = useFetch(
    "/products/",
    params
  );

  return {
    products: data?.results || [],
    totalCount: data?.count || 0,
    next: data?.next || null,
    previous: data?.previous || null,
    loading,
    error,
  };
};

export default useFetchProducts;
```

তখন Product page-এ:

```jsx
const {
  products,
  totalCount,
  loading,
  error,
} = useFetchProducts({
  page: currentPage,
  category: selectedCategory,
  search: searchQuery,
  ordering: sortOrder,
  priceMin: priceRange[0],
  priceMax: priceRange[1],
});
```

### পুরো architecture

```text
ProductPage
│
├── useFetchCategories()
│       │
│       └── useFetch()
│
├── useFetchProducts()
│       │
│       └── useFetch()
│
├── FilterSection
│
├── ProductList
│     └── ProductCard
│
└── Pagination
```

এখানে সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো:

```text
useFetch()
   ↓
Generic API fetching

useFetchCategories()
   ↓
Category-specific logic

useFetchProducts()
   ↓
Product-specific logic
```

তাই অন্য project-এ শুধু:

```jsx
useFetch("/users/")
```

বা

```jsx
useFetch("/orders/")
```

করেও একই generic hook ব্যবহার করতে পারবে।

**একটা জিনিস আরও improve করা দরকার:** `JSON.stringify(params)` dependency হিসেবে কাজ করবে, কিন্তু production-level reusable hook হলে আমরা এটাকে আরও clean করে **stable params + debounce + AbortController/request cancellation** সহ বানাতে পারি।


হ্যাঁ। Production-level করার সময় ৩টা জিনিস আলাদা করে ভাববে:

```text
params unstable
      ↓
useMemo → stable params
      ↓
search typing
      ↓
debounce → API call কমাবে
      ↓
API request
      ↓
AbortController → পুরনো request cancel করবে
```

তবে একটা গুরুত্বপূর্ণ বিষয়: **debounce আর AbortController একই কাজ করে না।**

* **Debounce** = user typing শেষ করার আগে API call না করা
* **AbortController** = আগের API request এখনও চললে সেটাকে cancel করা

## 1. প্রথমে `useDebounce`

```jsx
import { useEffect, useState } from "react";

const useDebounce = (value, delay = 500) => {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(timer);
    };
  }, [value, delay]);

  return debouncedValue;
};

export default useDebounce;
```

ধরো user লিখছে:

```text
l
la
lap
lapt
lapto
laptop
```

Debounce ছাড়া:

```text
6 API requests
```

Debounce `500ms` হলে user typing থামানোর **500ms পরে** request যাবে:

```text
laptop
  ↓
500ms অপেক্ষা
  ↓
1 API request
```

---

# 2. `useFetch`-এ AbortController

এখন generic fetch hook:

```jsx
import { useEffect, useState } from "react";
import apiClient from "../services/api-client";

const useFetch = (url, params = {}) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    const fetchData = async () => {
      setLoading(true);
      setError(null);

      try {
        const response = await apiClient.get(url, {
          params,
          signal: controller.signal,
        });

        setData(response.data);
      } catch (error) {
        if (error.name === "CanceledError") {
          return;
        }

        setError(error);
      } finally {
        if (!controller.signal.aborted) {
          setLoading(false);
        }
      }
    };

    fetchData();

    return () => {
      controller.abort();
    };
  }, [url, params]);

  return {
    data,
    loading,
    error,
  };
};

export default useFetch;
```

এখানে:

```jsx
const controller = new AbortController();
```

request-এর জন্য controller তৈরি করছে।

তারপর:

```jsx
signal: controller.signal
```

request-এর সাথে controller attach করছে।

আর যখন dependency change হবে:

```jsx
return () => {
  controller.abort();
};
```

আগের request cancel হবে।

---

# 3. কিন্তু `params`-এর সমস্যা আছে

ধরো:

```jsx
const params = {
  page: 1,
  category: 5,
};
```

Component প্রতিবার render হলে নতুন object তৈরি হতে পারে।

অর্থাৎ:

```text
render 1 → params object #1
render 2 → params object #2
render 3 → params object #3
```

Data একই হলেও reference আলাদা।

তাই:

```jsx
[params]
```

dependency দিলে unnecessary effect চালু হতে পারে।

এখানে `useMemo` ব্যবহার করা যায়।

---

# 4. `useFetchProducts`

এখন সবকিছু একসাথে:

```jsx
import { useMemo } from "react";
import useFetch from "./useFetch";
import useDebounce from "./useDebounce";

const useFetchProducts = ({
  page = 1,
  category = "",
  search = "",
  ordering = "",
  priceMin = "",
  priceMax = "",
} = {}) => {
  // Search-এর জন্য debounce
  const debouncedSearch = useDebounce(search, 500);

  // Stable params
  const params = useMemo(
    () => ({
      page,
      category,
      search: debouncedSearch,
      ordering,
      price__gte: priceMin,
      price__lte: priceMax,
    }),
    [
      page,
      category,
      debouncedSearch,
      ordering,
      priceMin,
      priceMax,
    ]
  );

  const { data, loading, error } = useFetch(
    "/products/",
    params
  );

  return {
    products: data?.results || [],
    totalCount: data?.count || 0,
    next: data?.next || null,
    previous: data?.previous || null,
    loading,
    error,
  };
};

export default useFetchProducts;
```

এখন architecture অনেক পরিষ্কার:

```text
ProductPage
     │
     │ search = "laptop"
     ↓
useFetchProducts()
     │
     ├── useDebounce()
     │       │
     │       └── 500ms wait
     │
     ├── useMemo()
     │       │
     │       └── stable params
     │
     ↓
useFetch()
     │
     ├── Axios
     │
     └── AbortController
             │
             └── old request cancel
```

---

# 5. বাস্তবে কী ঘটবে?

ধরো user search করছে:

```text
l
```

`useDebounce` এখনো wait করছে।

তারপর:

```text
la
```

আগের timer cancel।

তারপর:

```text
lap
```

আগের timer cancel।

শেষে:

```text
laptop
```

user আর কিছু লিখল না।

```text
500ms
 ↓
debouncedSearch = "laptop"
 ↓
params change
 ↓
useFetch()
 ↓
GET /products/?search=laptop
```

---

# 6. এবার user নতুন search করলে

ধরো আগে request চলছে:

```text
GET /products/?search=laptop
       ↓
      loading...
```

এর মধ্যে user লিখল:

```text
phone
```

তখন:

```text
old request
GET /products/?search=laptop
        ↓
controller.abort()
        ↓
CANCELLED
```

তারপর:

```text
GET /products/?search=phone
```

চলবে।

এটা খুব গুরুত্বপূর্ণ কারণ network-এ কখনও এমন হতে পারে:

```text
Request A = laptop
Request B = phone

B আগে response দিল
A পরে response দিল
```

তাহলে পুরনো `laptop` result এসে নতুন `phone` result-কে overwrite করতে পারে।

**AbortController এই ধরনের stale request problem কমাতে সাহায্য করে।**

---

## 7. Category-এর ক্ষেত্রে debounce লাগবে না

Category select করলে user সাধারণত একবারেই নির্বাচন করে:

```jsx
const {
  categories,
  loading,
  error,
} = useFetchCategories();
```

Category hook:

```jsx
import useFetch from "./useFetch";

const useFetchCategories = () => {
  const { data, loading, error } = useFetch(
    "/categories/"
  );

  return {
    categories: data?.results || [],
    loading,
    error,
  };
};

export default useFetchCategories;
```

এখানে:

```text
Category
   ↓
useFetchCategories
   ↓
useFetch
   ↓
AbortController
   ↓
API
```

Debounce দরকার নেই।

---

# 8. সবচেয়ে গুরুত্বপূর্ণ design principle

তুমি এখন এই pattern-টা মাথায় রাখো:

```text
                 ┌──────────────────┐
                 │    useFetch      │
                 │                  │
                 │ Generic API      │
                 │ Loading          │
                 │ Error            │
                 │ AbortController  │
                 └────────┬─────────┘
                          │
              ┌───────────┴───────────┐
              │                       │
       useFetchProducts       useFetchCategories
              │                       │
       Product logic            Category logic
              │
       ┌──────┴───────┐
       │              │
    debounce       filters
    search         sorting
    pagination
```

এটাই আমি তোমার জন্য recommend করব।

**Generic hook-এর কাজ:** API request manage করা।

**Resource-specific hook-এর কাজ:** Product/Category-এর business/query logic manage করা।

**Component-এর কাজ:** UI দেখানো এবং user interaction নেওয়া।

এই separation করলে পরবর্তীতে একই pattern দিয়ে `useFetchOrders`, `useFetchUsers`, `useFetchReviews`, `useFetchBookings` বানাতে পারবে।


---
