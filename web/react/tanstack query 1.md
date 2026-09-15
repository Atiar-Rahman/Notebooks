অবশ্যই। আমি **TanStack Query + React.js** একদম beginner থেকে advanced পর্যন্ত এমনভাবে শেখাবো যেন তুমি শুধু API call করা না, বরং **real-world production app-এ TanStack Query কেন/কখন/কীভাবে ব্যবহার করতে হয়** সেটাও বুঝতে পারো।

---

# TanStack Query — Beginner → Advanced Roadmap

প্রথমে পুরো ধারণাটা বুঝে নিই:

> **TanStack Query হলো server state manage করার library।**

React-এর `useState` মূলত UI/local state-এর জন্য।

যেমন:

```js
const [isModalOpen, setIsModalOpen] = useState(false);
const [name, setName] = useState("");
```

এগুলো **client state**।

অন্যদিকে:

```text
Users
Products
Orders
Posts
Comments
Notifications
```

যেগুলো backend/API/database থেকে আসে, এগুলো **server state**।

TanStack Query এই server state-এর:

- fetching
    
- caching
    
- loading
    
- error
    
- refetching
    
- updating
    
- synchronization
    
- pagination
    
- infinite scrolling
    
- optimistic updates
    

ইত্যাদি অনেক কিছু handle করে।

---

# 1. কেন TanStack Query দরকার?

ধরো তুমি সাধারণ React দিয়ে API call করলে:

```jsx
function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err);
        setLoading(false);
      });
  }, []);

  // ...
}
```

শুরুতে ঠিক আছে।

কিন্তু app বড় হলে সমস্যা শুরু হয়।

তোমাকে manually handle করতে হবে:

```text
Loading
Error
Caching
Refetching
Retry
Duplicate requests
Stale data
Pagination
Infinite scroll
Mutation
Cache invalidation
Optimistic update
Background fetching
```

TanStack Query এগুলোর অনেকটাই করে দেয়।

---

# 2. TanStack Query কীভাবে চিন্তা করবে?

একটা খুব গুরুত্বপূর্ণ concept:

```text
React Component
       ↓
TanStack Query
       ↓
Cache
       ↓
API
       ↓
Backend / Database
```

ধরো:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});
```

TanStack Query প্রথমে cache দেখবে।

```text
["users"]
```

এই key-এর data cache-এ আছে কি না।

না থাকলে:

```text
API request
   ↓
data
   ↓
cache
   ↓
component
```

পরের component একই query চাইলে:

```text
Component A ──┐
              ├── TanStack Query Cache
Component B ──┘
```

একই data reuse করতে পারে।

---

# 3. Installation

React project-এ:

```bash
npm install @tanstack/react-query
```

তারপর:

```jsx
import {
  QueryClient,
  QueryClientProvider
} from "@tanstack/react-query";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <YourApp />
    </QueryClientProvider>
  );
}
```

এটাই foundation।

---

# 4. প্রথম `useQuery`

ধরো API:

```text
GET /api/users
```

API function:

```js
async function fetchUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed to fetch users");
  }

  return response.json();
}
```

Component:

```jsx
import { useQuery } from "@tanstack/react-query";

function Users() {
  const {
    data,
    isPending,
    isError,
    error
  } = useQuery({
    queryKey: ["users"],
    queryFn: fetchUsers
  });

  if (isPending) {
    return <p>Loading...</p>;
  }

  if (isError) {
    return <p>{error.message}</p>;
  }

  return (
    <div>
      {data.map(user => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </div>
  );
}
```

এখানে সবচেয়ে important দুটি জিনিস:

```js
queryKey
queryFn
```

---

# 5. `queryKey` কী?

এটা TanStack Query-এর কাছে data-এর **identity**।

```js
queryKey: ["users"]
```

মানে:

> এই query-এর data হলো `users`।

আর:

```js
queryKey: ["products"]
```

মানে:

> এইটা products-এর data।

---

## Dynamic query key

ধরো user ID:

```text
/api/users/10
```

তাহলে:

```jsx
const { data } = useQuery({
  queryKey: ["user", 10],
  queryFn: () => fetchUser(10)
});
```

User 20:

```jsx
queryKey: ["user", 20]
```

দুটো আলাদা cache:

```text
["user", 10] → User 10

["user", 20] → User 20
```

এটা অত্যন্ত গুরুত্বপূর্ণ।

---

# 6. Query Key কেন এত গুরুত্বপূর্ণ?

ধরো:

```jsx
useQuery({
  queryKey: ["products", category],
  queryFn: () => fetchProducts(category)
});
```

যদি:

```js
category = "laptop"
```

তাহলে:

```text
["products", "laptop"]
```

আর:

```js
category = "phone"
```

তাহলে:

```text
["products", "phone"]
```

TanStack Query বুঝতে পারে:

> category পরিবর্তন হয়েছে → নতুন query।

---

# 7. `queryFn`

এটা হলো actual API request function।

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});
```

এখানে:

```js
fetchUsers
```

API call করে।

একটা ভালো pattern:

```text
src/
├── api/
│   └── users.js
├── hooks/
│   └── useUsers.js
├── components/
│   └── Users.jsx
```

---

# 8. API function আলাদা রাখা

```js
// api/users.js

export async function fetchUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed to fetch users");
  }

  return response.json();
}
```

তারপর:

```js
// hooks/useUsers.js

import { useQuery } from "@tanstack/react-query";
import { fetchUsers } from "../api/users";

export function useUsers() {
  return useQuery({
    queryKey: ["users"],
    queryFn: fetchUsers
  });
}
```

Component:

```jsx
function Users() {
  const {
    data,
    isPending,
    isError
  } = useUsers();

  // ...
}
```

এটা production code-এ অনেক cleaner।

---

# 9. Important Query States

TanStack Query-তে সাধারণত এই states দেখবে:

```js
isPending
isError
isSuccess
isFetching
```

### `isPending`

প্রথমবার data এখনো পাওয়া যায়নি।

```jsx
if (isPending) {
  return <Loading />;
}
```

### `isError`

request failed:

```jsx
if (isError) {
  return <Error />;
}
```

### `isSuccess`

data successfully পাওয়া গেছে।

### `isFetching`

background-এ request চলছে।

এটা `isPending` থেকে আলাদা।

---

# 10. `isPending` বনাম `isFetching`

এটা beginner-রা প্রায়ই confuse করে।

ধরো প্রথমবার:

```text
No data
   ↓
Fetching
   ↓
Data
```

তখন:

```js
isPending = true
isFetching = true
```

কিন্তু data already আছে এবং background refetch হচ্ছে:

```text
Existing data
     ↓
Background fetch
     ↓
New data
```

তখন:

```js
isPending = false
isFetching = true
```

তাই:

```jsx
if (isFetching) {
  return <small>Refreshing...</small>;
}
```

দারুণ UX দিতে পারো।

---

# 11. Caching

এটাই TanStack Query-এর সবচেয়ে powerful concepts-এর একটা।

ধরো:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});
```

API থেকে data এলো:

```text
users data
     ↓
TanStack Query Cache
```

তারপর তুমি অন্য page-এ গেলে এবং আবার users চাইলে:

```text
Cache
 ↓
Existing users
```

সবসময় নতুন API request করতে হবে না।

---

# 12. `staleTime`

ধরো:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
  staleTime: 1000 * 60 * 5
});
```

মানে:

```text
5 minutes
```

data fresh হিসেবে বিবেচিত হবে।

সহজভাবে:

```text
0 min ───────── 5 min
       fresh

5 min-এর পরে
       stale
```

---

# 13. `gcTime`

আরেকটি important option:

```js
gcTime
```

এটা cache-এর unused data কতক্ষণ memory-তে থাকবে সেটা control করে।

Beginner হিসেবে আপাতত মনে রাখো:

```text
staleTime → data কতক্ষণ fresh

gcTime → unused cache কতক্ষণ রাখা হবে
```

এই দুইটা এক জিনিস নয়।

---

# 14. Automatic Refetch

TanStack Query বিভিন্ন situation-এ refetch করতে পারে।

যেমন:

```text
Window focus
Network reconnect
Component mount
```

এটা configure করা যায়।

উদাহরণ:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
  refetchOnWindowFocus: false
});
```

---

# 15. Query Devtools

Development-এর সময় Devtools ব্যবহার করলে Query-এর ভিতরের অবস্থা দেখতে পারবে।

Install:

```bash
npm install @tanstack/react-query-devtools
```

তারপর:

```jsx
import { ReactQueryDevtools } from "@tanstack/react-query-devtools";
```

Provider-এর ভিতরে:

```jsx
<QueryClientProvider client={queryClient}>
  <App />

  <ReactQueryDevtools initialIsOpen={false} />
</QueryClientProvider>
```

এখানে দেখতে পারবে:

```text
Queries
Status
Data
Query Keys
Stale/Fresh
Fetching
Cache
```

TanStack Query শেখার জন্য এটা খুব useful।

---

# 16. Query Variables

ধরো:

```text
GET /api/products?category=shoes
```

```jsx
function Products({ category }) {
  const query = useQuery({
    queryKey: ["products", category],
    queryFn: () => fetchProducts(category)
  });

  // ...
}
```

API:

```js
async function fetchProducts(category) {
  const response = await fetch(
    `/api/products?category=${category}`
  );

  if (!response.ok) {
    throw new Error("Failed");
  }

  return response.json();
}
```

Key-এর মধ্যে variable রাখা খুব important:

```js
["products", category]
```

---

# 17. Search

ধরো search:

```jsx
const [search, setSearch] = useState("");

const query = useQuery({
  queryKey: ["products", search],
  queryFn: () => searchProducts(search)
});
```

Search পরিবর্তন হলে:

```text
["products", "phone"]

        ↓

["products", "iphone"]
```

নতুন query।

Production app-এ এখানে **debouncing** যোগ করা খুব common।

---

# 18. Dependent Query

ধরো প্রথমে user:

```text
GET /users/10
```

তারপর সেই user-এর projects:

```text
GET /users/10/projects
```

তখন:

```jsx
const userQuery = useQuery({
  queryKey: ["user", userId],
  queryFn: () => fetchUser(userId)
});

const projectsQuery = useQuery({
  queryKey: ["projects", userId],
  queryFn: () => fetchProjects(userId),
  enabled: !!userId
});
```

`enabled` query কখন run করবে সেটা control করতে পারে।

---

# 19. `enabled`

উদাহরণ:

```jsx
useQuery({
  queryKey: ["user", userId],
  queryFn: () => fetchUser(userId),
  enabled: !!userId
});
```

যদি:

```js
userId = undefined
```

তাহলে query চলবে না।

এটা dependent queries-এর জন্য খুব useful।

---

# 20. Mutation কী?

`useQuery` মূলত **data read/fetch** করার জন্য।

কিন্তু:

```text
POST
PUT
PATCH
DELETE
```

এসবের জন্য:

```js
useMutation
```

ব্যবহার করবে।

---

# 21. POST Example

ধরো:

```js
async function createUser(user) {
  const response = await fetch("/api/users", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(user)
  });

  if (!response.ok) {
    throw new Error("Failed to create user");
  }

  return response.json();
}
```

Component:

```jsx
const mutation = useMutation({
  mutationFn: createUser
});
```

তারপর:

```js
mutation.mutate({
  name: "Rahim",
  email: "rahim@example.com"
});
```

---

# 22. Mutation States

```js
mutation.isPending
mutation.isError
mutation.isSuccess
mutation.data
mutation.error
```

যেমন:

```jsx
<button
  disabled={mutation.isPending}
  onClick={() => mutation.mutate(formData)}
>
  {mutation.isPending ? "Creating..." : "Create"}
</button>
```

---

# 23. সবচেয়ে গুরুত্বপূর্ণ: Query Invalidation

ধরো:

```text
GET /users
```

দিয়ে users দেখাচ্ছো।

তারপর:

```text
POST /users
```

দিয়ে নতুন user create করলে cache-এর old data থাকবে।

তখন:

```js
queryClient.invalidateQueries({
  queryKey: ["users"]
});
```

মানে:

> Users query-টা stale করে দাও এবং প্রয়োজন অনুযায়ী আবার fetch করো।

---

# 24. Complete Mutation Example

```jsx
import {
  useMutation,
  useQueryClient
} from "@tanstack/react-query";

function CreateUser() {
  const queryClient = useQueryClient();

  const mutation = useMutation({
    mutationFn: createUser,

    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: ["users"]
      });
    }
  });

  return (
    <button
      onClick={() =>
        mutation.mutate({
          name: "Rahim"
        })
      }
    >
      Create User
    </button>
  );
}
```

Flow:

```text
Create user
    ↓
POST API
    ↓
Success
    ↓
Invalidate ["users"]
    ↓
Users refetch
    ↓
UI updated
```

এটা real-world development-এ খুব গুরুত্বপূর্ণ pattern।

---

# 25. `setQueryData`

সবসময় API refetch করতে হবে এমন নয়।

তুমি সরাসরি cache update করতে পারো:

```js
queryClient.setQueryData(
  ["user", userId],
  updatedUser
);
```

এটা useful যখন API response-এর মধ্যে updated data already পাওয়া গেছে।

---

# 26. Optimistic Update

Advanced concept।

ধরো:

```text
Like button
```

User click করল।

Server response আসতে 500ms লাগবে।

তুমি চাইলে server response-এর আগেই UI update করতে পারো:

```text
Click Like
   ↓
UI immediately changes ❤️
   ↓
API request
   ↓
Success → keep
Failure → rollback
```

এটাই optimistic update।

TanStack Query-তে `onMutate`, `onError`, `onSettled` দিয়ে সাধারণত implement করা হয়।

Conceptually:

```jsx
useMutation({
  mutationFn: updateTodo,

  onMutate: async (newTodo) => {
    // cancel existing fetch
    // save previous data
    // update cache optimistically

    return {
      previousTodo
    };
  },

  onError: (error, newTodo, context) => {
    // rollback
  },

  onSettled: () => {
    // refetch / invalidate
  }
});
```

---

# 27. Pagination

ধরো API:

```text
/api/products?page=1
/api/products?page=2
/api/products?page=3
```

তখন:

```jsx
const [page, setPage] = useState(1);

const query = useQuery({
  queryKey: ["products", page],
  queryFn: () => fetchProducts(page)
});
```

Page পরিবর্তন করলে:

```text
["products", 1]

       ↓

["products", 2]
```

নতুন query/cache entry তৈরি হবে।

Modern TanStack Query-তে pagination UX smooth করার জন্য placeholder data-এর pattern ব্যবহার করা যায়।

---

# 28. Infinite Query

Facebook/Instagram-type feed:

```text
Page 1
 ↓
Page 2
 ↓
Page 3
 ↓
Page 4
```

এক্ষেত্রে:

```js
useInfiniteQuery
```

ব্যবহার করবে।

Concept:

```jsx
const query = useInfiniteQuery({
  queryKey: ["posts"],
  queryFn: fetchPosts,
  initialPageParam: 1,
  getNextPageParam: (lastPage) => {
    return lastPage.nextPage;
  }
});
```

তারপর:

```js
query.fetchNextPage();
```

---

# 29. Infinite Query Data Structure

এখানে data সাধারণত pages আকারে থাকে:

```js
data.pages
```

ধরো:

```text
pages
 ├── page 1
 ├── page 2
 ├── page 3
```

Render:

```jsx
data.pages.map(page =>
  page.items.map(item => (
    <div key={item.id}>
      {item.name}
    </div>
  ))
)
```

---

# 30. Prefetching

ধরো products list আছে।

User কোনো product-এর উপর hover করলে তুমি আগেই details fetch করতে পারো।

```js
queryClient.prefetchQuery({
  queryKey: ["product", productId],
  queryFn: () => fetchProduct(productId)
});
```

তারপর user details page-এ গেলে:

```text
User clicks
   ↓
Cache already has data
   ↓
Details page feels instant
```

এটা advanced UX technique।

---

# 31. Query Cancellation

কখনো request cancel করতে হয়।

TanStack Query `AbortSignal` ব্যবহার করতে পারে।

```js
async function fetchUsers({ signal }) {
  const response = await fetch("/api/users", {
    signal
  });

  return response.json();
}
```

Query:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});
```

Query inactive/unmounted হলে cancellation দরকার হলে এটি useful হতে পারে।

---

# 32. Error Handling

Basic:

```jsx
const query = useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});

if (query.isError) {
  return <p>{query.error.message}</p>;
}
```

আর production application-এ global error handling-ও configure করা যায়।

---

# 33. Retry

Network request failure হলে TanStack Query retry করতে পারে।

Configure:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
  retry: 2
});
```

মানে failure হলে আবার চেষ্টা করবে।

কিন্তু সব error retry করা উচিত নয়।

যেমন:

```text
500 → retry reasonable
Network error → retry reasonable

401/403 → সাধারণত blindly retry করার দরকার নেই
404 → সাধারণত retry করার দরকার নেই
```

API architecture অনুযায়ী strategy ঠিক করবে।

---

# 34. Authentication

ধরো JWT token আছে।

একটা API client বানানো ভালো:

```js
async function apiFetch(url, options = {}) {
  const token = localStorage.getItem("token");

  return fetch(url, {
    ...options,
    headers: {
      ...options.headers,
      Authorization: `Bearer ${token}`
    }
  });
}
```

তারপর:

```js
async function fetchUsers() {
  const response = await apiFetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed");
  }

  return response.json();
}
```

Real production application-এ token storage/security architecture backend-এর authentication strategy অনুযায়ী design করা উচিত।

---

# 35. Axios + TanStack Query

TanStack Query Axios-এর replacement নয়।

এরা আলাদা কাজ করে।

```text
Axios
 ↓
HTTP request

TanStack Query
 ↓
Server-state management
```

তাই:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: async () => {
    const response = await axios.get("/api/users");

    return response.data;
  }
});
```

দুটো একসাথে ব্যবহার করা যায়।

---

# 36. React Query Architecture

একটা বড় project-এ আমি এভাবে organize করতে বলব:

```text
src/
│
├── api/
│   ├── users.api.js
│   ├── products.api.js
│   └── orders.api.js
│
├── hooks/
│   ├── useUsers.js
│   ├── useProducts.js
│   └── useOrders.js
│
├── components/
│
├── pages/
│
├── lib/
│   └── queryClient.js
│
└── App.jsx
```

---

# 37. Query Options আলাদা করা

Advanced application-এ query configuration reuse করা যায়।

Concept:

```js
function usersQueryOptions() {
  return {
    queryKey: ["users"],
    queryFn: fetchUsers
  };
}
```

তারপর:

```jsx
useQuery(usersQueryOptions());
```

এতে একই query configuration বিভিন্ন জায়গায় reuse করা সহজ হয়।

---

# 38. Query Key Factory

Large project-এ এটা খুব useful।

```js
export const userKeys = {
  all: ["users"],

  lists: () => [...userKeys.all, "list"],

  list: (filters) => [
    ...userKeys.lists(),
    filters
  ],

  details: () => [
    ...userKeys.all,
    "detail"
  ],

  detail: (id) => [
    ...userKeys.details(),
    id
  ]
};
```

তারপর:

```js
useQuery({
  queryKey: userKeys.detail(userId),
  queryFn: () => fetchUser(userId)
});
```

Invalidation:

```js
queryClient.invalidateQueries({
  queryKey: userKeys.all
});
```

Large application-এ query keys consistent রাখার জন্য এটা খুব helpful।

---

# 39. Server State বনাম Client State

এই distinction ভালোভাবে বুঝো।

### Client state

```text
Modal open?
Sidebar open?
Selected tab?
Input value?
Theme?
```

Use:

```js
useState
useReducer
Context
Zustand
Redux
```

### Server state

```text
Users
Products
Orders
Posts
Comments
```

Use:

```text
TanStack Query
```

সব state TanStack Query-তে রাখার চেষ্টা করা উচিত নয়।

---

# 40. TanStack Query + Zustand

দুটো একসাথে ব্যবহার করা perfectly fine।

Example:

```text
Zustand
 ├── theme
 ├── sidebar
 ├── selected filters
 └── UI state

TanStack Query
 ├── users
 ├── products
 ├── orders
 └── server data
```

এটা অনেক application-এর clean architecture।

---

# 41. Cache Manipulation

তোমার toolbox-এ এই methodsগুলো থাকা উচিত:

```js
queryClient.invalidateQueries()
```

→ query stale/refetch strategy trigger

```js
queryClient.refetchQueries()
```

→ actively refetch

```js
queryClient.setQueryData()
```

→ cache manually update

```js
queryClient.getQueryData()
```

→ cache থেকে data পড়া

```js
queryClient.removeQueries()
```

→ queries remove করা

```js
queryClient.prefetchQuery()
```

→ আগেই data fetch করা

এগুলো advanced TanStack Query-এর core tools।

---

# 42. Real-world CRUD Architecture

ধরো তুমি একটা Todo app বানাচ্ছো।

```text
GET     /todos
GET     /todos/:id

POST    /todos
PATCH   /todos/:id
DELETE  /todos/:id
```

তাহলে architecture:

```text
              TanStack Query
                    │
       ┌────────────┴────────────┐
       ↓                         ↓
    Queries                   Mutations
       │                         │
   GET /todos            POST/PATCH/DELETE
       │                         │
       └────────────┬────────────┘
                    ↓
                 API
                    ↓
                Backend
```

Mutation success:

```text
Mutation
   ↓
invalidateQueries(["todos"])
   ↓
refetch
   ↓
UI updated
```

---

# 43. সবচেয়ে গুরুত্বপূর্ণ mental model

TanStack Query-কে শুধু:

> "API call করার library"

হিসেবে চিন্তা করলে পুরো power বুঝবে না।

এভাবে চিন্তা করো:

> **TanStack Query হলো server data-এর cache + synchronization + fetching lifecycle manager।**

এটাই আসল concept।

---

# 44. Beginner → Advanced Learning Order

আমি হলে এই order-এ শিখতাম:

### Level 1 — Foundation

```text
1. Server state কী
2. QueryClient
3. QueryClientProvider
4. useQuery
5. queryKey
6. queryFn
7. isPending
8. isError
9. isFetching
```

### Level 2 — Caching

```text
10. Cache
11. staleTime
12. gcTime
13. refetch
14. background refetch
15. window focus
16. retry
```

### Level 3 — Mutations

```text
17. useMutation
18. POST
19. PATCH
20. DELETE
21. onSuccess
22. invalidateQueries
23. setQueryData
```

### Level 4 — Real-world

```text
24. Dynamic query keys
25. enabled
26. Dependent queries
27. Search
28. Filtering
29. Pagination
30. Prefetching
```

### Level 5 — Advanced

```text
31. useInfiniteQuery
32. Optimistic updates
33. Rollback
34. Query cancellation
35. Query key factories
36. Query options
37. Cache manipulation
38. Error strategies
```

### Level 6 — Production

```text
39. Axios/fetch architecture
40. Authentication
41. Token refresh
42. Global error handling
43. TypeScript
44. Testing
45. SSR
46. Next.js
47. Hydration
48. Prefetching
49. Performance
50. Devtools
```

---

# 45. একটা Full Example

একটা simple users application:

```jsx
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
  useMutation,
  useQueryClient
} from "@tanstack/react-query";

const queryClient = new QueryClient();

async function getUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed to fetch users");
  }

  return response.json();
}

async function createUser(user) {
  const response = await fetch("/api/users", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(user)
  });

  if (!response.ok) {
    throw new Error("Failed to create user");
  }

  return response.json();
}

function Users() {
  const query = useQuery({
    queryKey: ["users"],
    queryFn: getUsers,
    staleTime: 1000 * 60 * 5
  });

  if (query.isPending) {
    return <p>Loading...</p>;
  }

  if (query.isError) {
    return <p>Error: {query.error.message}</p>;
  }

  return (
    <div>
      {query.data.map(user => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </div>
  );
}

function CreateUser() {
  const queryClient = useQueryClient();

  const mutation = useMutation({
    mutationFn: createUser,

    onSuccess: () => {
      queryClient.invalidateQueries({
        queryKey: ["users"]
      });
    }
  });

  return (
    <button
      disabled={mutation.isPending}
      onClick={() =>
        mutation.mutate({
          name: "Rahim"
        })
      }
    >
      {mutation.isPending
        ? "Creating..."
        : "Create User"}
    </button>
  );
}

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <CreateUser />
      <Users />
    </QueryClientProvider>
  );
}
```

এখানে তুমি ইতিমধ্যে শিখে ফেলেছ:

```text
QueryClient
Provider
useQuery
queryKey
queryFn
Loading
Error
Caching
staleTime
useMutation
Mutation
invalidateQueries
```

---

# 46. একদম মনে রাখার মতো Cheat Sheet

```text
useQuery
    ↓
GET / READ data
```

```text
useMutation
    ↓
POST / PUT / PATCH / DELETE
```

```text
queryKey
    ↓
Data-এর unique identity
```

```text
queryFn
    ↓
Actual API request
```

```text
staleTime
    ↓
কতক্ষণ data fresh
```

```text
gcTime
    ↓
Unused cache কতক্ষণ রাখা হবে
```

```text
enabled
    ↓
কখন query run করবে
```

```text
invalidateQueries
    ↓
পুরনো query-কে stale করে update/refetch করানো
```

```text
setQueryData
    ↓
Cache manually update
```

```text
prefetchQuery
    ↓
আগে থেকেই data এনে রাখা
```

```text
useInfiniteQuery
    ↓
Infinite scroll / load more
```

```text
onMutate
    ↓
Optimistic update শুরু
```

```text
onError
    ↓
Failure / rollback
```

```text
onSettled
    ↓
শেষে synchronization
```

---

## শেষ পর্যন্ত যে mental modelটা মাথায় রাখবে

```text
                 ┌──────────────────┐
                 │   React UI       │
                 └────────┬─────────┘
                          │
                    useQuery /
                   useMutation
                          │
                 ┌────────▼─────────┐
                 │ TanStack Query   │
                 │                  │
                 │ Cache            │
                 │ Fetching         │
                 │ Refetching       │
                 │ Retry            │
                 │ Synchronization  │
                 └────────┬─────────┘
                          │
                       HTTP
                          │
                 ┌────────▼─────────┐
                 │ Backend / API    │
                 └────────┬─────────┘
                          │
                     Database
```

**সবচেয়ে গুরুত্বপূর্ণ:** TanStack Query শেখার সময় শুধু syntax মুখস্থ কোরো না। প্রতিটি concept-এর ক্ষেত্রে নিজেকে জিজ্ঞেস করো—**"এই data কি server state? এই data-এর cache identity কী? কখন stale হবে? mutation-এর পরে cache কীভাবে synchronize হবে?"** এই চারটা প্রশ্ন বুঝে গেলে TanStack Query অনেক সহজ হয়ে যাবে।

----
হ্যাঁ 😄 শুরুতে **`fetch` vs `axios` vs `TanStack Query`** নিয়ে মাথা ঘুরে যাওয়াটা একদম normal। আসলে সবচেয়ে important ব্যাপার হলো:

> **Fetch আর Axios এক ধরনের জিনিস। TanStack Query অন্য ধরনের জিনিস।**

এই distinction বুঝলেই ৮০% confusion শেষ।

---

# 🧠 প্রথমে এক লাইনে বুঝো

```text
FETCH / AXIOS
     ↓
"API-তে request কীভাবে পাঠাব?"

TANSTACK QUERY
     ↓
"API-এর data কীভাবে manage করব?"
```

অর্থাৎ:

|Tool|কাজ|
|---|---|
|`fetch`|HTTP request|
|`axios`|HTTP request|
|`TanStack Query`|Server data management|

---

# 1. Fetch কী?

`fetch` browser-এর built-in API।

উদাহরণ:

```js
const response = await fetch("/api/users");

const data = await response.json();

console.log(data);
```

এখানে তুমি নিজে request করছো।

### Fetch-এর কাজ:

```text
Browser
   ↓
fetch()
   ↓
API
   ↓
Response
```

Fetch তোমার জন্য automatically:

- cache management
    
- query state
    
- background refetch
    
- mutation management
    
- retry strategy
    

এসব manage করে না।

---

# 2. Axios কী?

Axios-ও HTTP request করার জন্য।

```js
import axios from "axios";

const response = await axios.get("/api/users");

console.log(response.data);
```

মানে:

```text
fetch ─────┐
           ├── HTTP Client
axios ─────┘
```

তাই সাধারণত:

> **Fetch অথবা Axios**

দুটো একসাথে ব্যবহার করার প্রয়োজন নেই।

---

# 3. তাহলে TanStack Query কোথায়?

TanStack Query API request নিজে করার বদলে সাধারণত তোমার দেওয়া function ব্যবহার করে।

যেমন:

```js
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers
});
```

এখানে `fetchUsers` হতে পারে:

### Fetch দিয়ে

```js
async function fetchUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed");
  }

  return response.json();
}
```

অথবা Axios দিয়ে:

```js
async function fetchUsers() {
  const response = await axios.get("/api/users");

  return response.data;
}
```

অর্থাৎ:

```text
              TanStack Query
                    │
             ┌──────┴──────┐
             ↓             ↓
           fetch          axios
             │             │
             └──────┬──────┘
                    ↓
                   API
```

---

# 🔥 এখন সবচেয়ে important example

ধরো তোমার `/users` API আছে।

## Option A — শুধু Fetch

```jsx
function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("/api/users")
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  // ...
}
```

এখানে তুমি manually manage করছো:

```text
loading
error
data
refetch
cache
```

---

# Option B — শুধু Axios

```jsx
useEffect(() => {
  axios.get("/api/users")
    .then(response => {
      setUsers(response.data);
    });
}, []);
```

Axios শুধু request সহজ করেছে।

কিন্তু এখনও তোমাকে manage করতে হবে:

```text
loading
error
cache
refetch
duplicate requests
```

---

# Option C — TanStack Query + Fetch ⭐

```jsx
const usersQuery = useQuery({
  queryKey: ["users"],
  queryFn: async () => {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("Failed");
    }

    return response.json();
  }
});
```

এখন TanStack Query manage করবে:

```text
          TanStack Query

              │
      ┌───────┼────────┐
      ↓       ↓        ↓
    Cache   Loading   Error
      ↓
  Refetch
      ↓
 Background update
```

---

# Option D — TanStack Query + Axios ⭐

এটাও খুব common:

```jsx
const usersQuery = useQuery({
  queryKey: ["users"],
  queryFn: async () => {
    const response = await axios.get("/api/users");

    return response.data;
  }
});
```

এখানে:

```text
Axios
 ↓
API request

TanStack Query
 ↓
Cache
Loading
Error
Refetch
Synchronization
```

---

# 🤯 তাহলে কোনটা কখন?

এই rule-টা মনে রাখো:

## Rule #1

### API request করতে হলে:

```text
fetch OR axios
```

---

## Rule #2

### Server data manage করতে হলে:

```text
TanStack Query
```

---

# বাস্তবে আমি কোনটা নেব?

তোমার project-এর size অনুযায়ী:

### ছোট project

```text
React
 +
fetch
```

যথেষ্ট হতে পারে।

যেমন:

```text
Portfolio
Small landing page
Simple contact form
Tiny CRUD
```

---

### Medium/large project

আমি সাধারণত:

```text
React
+
TanStack Query
+
fetch/axios
```

নেব।

---

# Fetch নাকি Axios?

এখানে দুটোই valid।

### Fetch নাও যদি:

```text
Simple API
Few endpoints
No special HTTP abstraction needed
```

Example:

```js
async function getUsers() {
  const res = await fetch("/api/users");

  if (!res.ok) {
    throw new Error("Request failed");
  }

  return res.json();
}
```

---

### Axios নাও যদি:

তোমার application-এ API layer একটু complex হয়।

যেমন:

```text
Base URL
Request interceptors
Response interceptors
Authentication headers
Centralized error handling
Multiple API configuration
```

তখন Axios convenient হতে পারে।

Example:

```js
const api = axios.create({
  baseURL: "https://api.example.com"
});
```

তারপর:

```js
api.get("/users");
api.post("/users");
api.patch("/users/1");
api.delete("/users/1");
```

---

# 🔥 Production Architecture

একটা বড় React application ধরো।

আমি architecture-টা এমনভাবে ভাবব:

```text
                 React
                   │
                   ↓
            TanStack Query
                   │
             ┌─────┴─────┐
             ↓           ↓
           Query      Mutation
             │           │
             └─────┬─────┘
                   ↓
                API Client
                   │
                 Axios
                   │
                   ↓
                Backend
```

তখন code হতে পারে:

### API layer

```js
// api/users.js

import api from "./client";

export async function getUsers() {
  const response = await api.get("/users");

  return response.data;
}

export async function createUser(user) {
  const response = await api.post("/users", user);

  return response.data;
}
```

### Query layer

```js
// hooks/useUsers.js

import { useQuery } from "@tanstack/react-query";
import { getUsers } from "../api/users";

export function useUsers() {
  return useQuery({
    queryKey: ["users"],
    queryFn: getUsers
  });
}
```

### Component

```jsx
function Users() {
  const {
    data: users,
    isPending,
    isError
  } = useUsers();

  if (isPending) {
    return <p>Loading...</p>;
  }

  if (isError) {
    return <p>Something went wrong</p>;
  }

  return (
    <>
      {users.map(user => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </>
  );
}
```

এখানে প্রত্যেকটার দায়িত্ব আলাদা:

```text
Axios
  ↓
"কীভাবে HTTP request করব?"

TanStack Query
  ↓
"এই server data কীভাবে manage করব?"

React
  ↓
"UI কীভাবে দেখাব?"
```

---

# 🧩 আরেকটা সহজ analogy

ভাবো তুমি একটা restaurant চালাচ্ছো।

### Fetch / Axios = Delivery person 🚚

তারা:

```text
Order নিয়ে যাবে
Food নিয়ে আসবে
```

### TanStack Query = Restaurant Manager 🧑‍💼

Manager দেখে:

```text
কোন order pending?
কোন order complete?
আগের order-এর তথ্য আছে?
আবার order করা দরকার?
কোনটা update করতে হবে?
```

### React = Customer-facing screen 🖥️

সে শুধু দেখাচ্ছে:

```text
Loading...
Users...
Error...
Updated data...
```

---

# ⚠️ সবচেয়ে common ভুল

অনেকে ভাবে:

```text
Axios vs TanStack Query
```

এটা comparison।

আসলে পুরোপুরি comparison না।

কারণ:

```text
Axios ≈ Fetch
```

কিন্তু:

```text
TanStack Query
```

একটা আলাদা layer।

তাই:

```text
❌ Axios OR TanStack Query
```

এভাবে ভাববে না।

বরং:

```text
✅ Axios + TanStack Query
```

অথবা:

```text
✅ Fetch + TanStack Query
```

---

# 🎯 আমার recommendation

তুমি যদি এখন **React শিখছো এবং TanStack Query শিখতে চাও**, তাহলে প্রথমে:

```text
React
 ↓
fetch
 ↓
TanStack Query
```

এই combination দিয়ে concept বোঝো।

যেমন:

```jsx
useQuery({
  queryKey: ["users"],
  queryFn: async () => {
    const res = await fetch("/api/users");

    if (!res.ok) {
      throw new Error("Failed");
    }

    return res.json();
  }
});
```

এরপর যখন TanStack Query বুঝে যাবে, তখন:

```text
fetch
   ↓
Axios
```

শিখে API layer আরও clean করতে পারো।

---

# 🧠 শেষবারের মতো এইটা মুখস্থ করো

```text
┌─────────────────────────────┐
│          React              │
│           UI                │
└──────────────┬──────────────┘
               │
               ↓
┌─────────────────────────────┐
│     TanStack Query          │
│                             │
│ Cache                       │
│ Loading                     │
│ Error                       │
│ Refetch                     │
│ Background Sync             │
│ Pagination                  │
│ Mutations                   │
└──────────────┬──────────────┘
               │
               ↓
┌─────────────────────────────┐
│      Fetch / Axios          │
│      HTTP Request           │
└──────────────┬──────────────┘
               │
               ↓
┌─────────────────────────────┐
│          Backend            │
└─────────────────────────────┘
```

**এক লাইনের rule:**

> 🟢 **Fetch/Axios = API-তে কথা বলার মাধ্যম**  
> 🔵 **TanStack Query = API থেকে পাওয়া data manage করার system**

তুমি চাইলে এরপর আমি তোমাকে **একটা বাস্তব React CRUD project দিয়ে `Axios + TanStack Query` একদম zero → production level** শেখাতে পারি—`GET → POST → PATCH → DELETE → loading → error → cache → invalidate → optimistic update → pagination` সব এক project-এ।

---
