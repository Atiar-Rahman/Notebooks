SPA = Single Page Application
## What is React Router?

**React Router** is a library that allows you to create **multiple pages/views in a React application without reloading the browser**.

Normally React is a **Single Page Application (SPA)**:

```
index.html
     |
     |
 React App
```

React Router changes the displayed component based on the URL.

Example:

```
localhost:5173/

        ↓

Home Component


localhost:5173/about

        ↓

About Component


localhost:5173/products

        ↓

Products Component
```

No full page refresh happens.

---

# Why do we need React Router?

Without Router:

```jsx
function App(){

 return (
   <div>
     <Home/>
     <About/>
     <Contact/>
   </div>
 )

}
```

Everything shows together.

With Router:

```
/        → Home
/about   → About
/contact → Contact
```

---

# Install React Router

For React Vite project:

```bash
npm install react-router-dom
```

---

# Basic Project Structure

Example:

```
src
 |
 ├── App.jsx
 |
 ├── pages
 |     |
 |     ├── Home.jsx
 |     ├── About.jsx
 |     └── Contact.jsx
 |
 └── main.jsx
```

---

# Create Pages

## Home.jsx

```jsx
const Home = ()=>{

 return (
   <h1>
     Home Page
   </h1>
 )

}

export default Home;
```

---

## About.jsx

```jsx
const About = ()=>{

 return (
   <h1>
     About Page
   </h1>
 )

}

export default About;
```

---

## Contact.jsx

```jsx
const Contact = ()=>{

 return (
   <h1>
     Contact Page
   </h1>
 )

}

export default Contact;
```

---

# Setup Router

Usually `main.jsx`:

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

import {
 BrowserRouter
} from "react-router-dom";

import App from "./App";


ReactDOM.createRoot(
 document.getElementById("root")
)
.render(

<BrowserRouter>

 <App/>

</BrowserRouter>

);
```

---

# Create Routes

App.jsx:

```jsx
import {
 Routes,
 Route
} from "react-router-dom";


import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";


function App(){


return (

<Routes>


<Route
 path="/"
 element={<Home/>}
/>


<Route
 path="/about"
 element={<About/>}
/>


<Route
 path="/contact"
 element={<Contact/>}
/>


</Routes>


)

}


export default App;
```

Now:

```
/
```

shows Home

```
/about
```

shows About

```
/contact
```

shows Contact

---

# Link Navigation

Never use normal `<a>` in React Router.

Wrong:

```html
<a href="/about">
 About
</a>
```

It reloads page.

Use:

```jsx
import {
 Link
} from "react-router-dom";


<Link to="/about">
 About
</Link>
```

---

# Navbar Example

```jsx
import {Link} from "react-router-dom";


function Navbar(){

return (

<nav>


<Link to="/">
 Home
</Link>


<Link to="/about">
 About
</Link>


<Link to="/contact">
 Contact
</Link>


</nav>

)

}

export default Navbar;
```

---

# Active Link

Use `NavLink`.

```jsx
import {
NavLink
} from "react-router-dom";


<NavLink
 to="/about"

 className={({isActive})=>
  isActive
  ? "active"
  : ""
 }
>

About

</NavLink>
```

If URL is:

```
/about
```

class:

```
active
```

---

# Nested Routes

Example:

Dashboard:

```
/dashboard

/dashboard/profile

/dashboard/settings
```

Route:

```jsx
<Route 
 path="/dashboard"
 element={<Dashboard/>}
>


<Route
 path="profile"
 element={<Profile/>}
/>


<Route
 path="settings"
 element={<Settings/>}
/>


</Route>
```

---

Dashboard component:

```jsx
import {
Outlet
} from "react-router-dom";


function Dashboard(){


return (

<div>

<h1>
Dashboard
</h1>


<Outlet/>


</div>

)

}

export default Dashboard;
```

`Outlet` displays child routes.

---

# URL Parameters

Example:

```
/user/10
```

10 is id.

Route:

```jsx
<Route

path="/user/:id"

element={<User/>}

/>
```

---

User.jsx:

```jsx
import {
useParams
} from "react-router-dom";


function User(){


const {id}=useParams();


return (

<h1>

User ID: {id}

</h1>

)


}

export default User;
```

URL:

```
/user/25
```

Output:

```
User ID: 25
```

---

# Navigate Programmatically

Example after login:

```jsx
import {
useNavigate
} from "react-router-dom";


function Login(){


const navigate=useNavigate();



function submit(){


 // login success

 navigate("/dashboard");


}


return (

<button onClick={submit}>
Login
</button>

)

}
```

---

# 404 Page

If route does not exist:

```jsx
<Route
 path="*"
 element={<NotFound/>}
/>
```

Example:

```
/abcxyz
```

shows:

```
Page Not Found
```

---

# Layout Route

Common website:

```
Navbar
 |
 ---- Home
 ---- About
 ---- Contact
Footer
```

Layout:

```jsx
function Layout(){

return (

<>

<Navbar/>

<Outlet/>

<Footer/>

</>

)

}
```

Routes:

```jsx
<Route element={<Layout/>}>


<Route
path="/"
element={<Home/>}
/>


<Route
path="/about"
element={<About/>}
/>


</Route>
```

---

# React Router Flow

```
User clicks Link

       ↓

URL changes

       ↓

Router checks Route

       ↓

Matching Component Render

       ↓

UI updates
```

---

# Real Project Example

E-commerce:

```
/
   Home

/products
   ProductList

/products/10
   ProductDetails

/cart
   Cart

/login
   Login

/dashboard
   Admin Dashboard
```

---

# React Router Important APIs

|API|Purpose|
|---|---|
|BrowserRouter|Enable routing|
|Routes|Route container|
|Route|Define URL|
|Link|Navigation|
|NavLink|Active navigation|
|useNavigate|Move using code|
|useParams|Read URL data|
|Outlet|Nested route|

---

React Router is basically the **navigation system of React applications**. It converts a single-page React app into a multi-page experience.


-------
# Understand Nested Routing , Outlet , Link And NavLink

Let's understand **Nested Routing, Outlet, Link, and NavLink** with a real example.

Assume we are building:

```
Dashboard
 ├── Profile
 ├── Settings
 └── Orders
```

URL structure:

```
/dashboard

/dashboard/profile

/dashboard/settings

/dashboard/orders
```

---

# 1. Nested Routing

**Nested route means a route inside another route.**

Parent:

```
/dashboard
```

Children:

```
/dashboard/profile
/dashboard/settings
```

The child pages belong to the parent page.

---

## App.jsx

```jsx
import {
  Routes,
  Route
} from "react-router-dom";


import Dashboard from "./Dashboard";
import Profile from "./Profile";
import Settings from "./Settings";
import Orders from "./Orders";


function App(){


return (

<Routes>


  <Route
    path="/dashboard"
    element={<Dashboard/>}
  >


    <Route
      path="profile"
      element={<Profile/>}
    />


    <Route
      path="settings"
      element={<Settings/>}
    />


    <Route
      path="orders"
      element={<Orders/>}
    />


  </Route>


</Routes>

)

}


export default App;
```

Notice:

```jsx
<Route path="/dashboard">
```

inside:

```jsx
<Route path="profile">
```

This creates:

```
/dashboard/profile
```

---

# 2. Outlet

`Outlet` is where child routes appear.

Think:

```
Dashboard.jsx

+----------------+
| Dashboard      |
|                |
|  <Outlet/>     |
|                |
+----------------+

```

The child component replaces `<Outlet/>`.

---

## Dashboard.jsx

```jsx
import {Outlet} from "react-router-dom";


function Dashboard(){


return (

<div>


<h1>
Dashboard
</h1>


<Outlet/>


</div>

)

}


export default Dashboard;
```

---

When URL:

```
/dashboard/profile
```

React renders:

```
Dashboard

    +
    |
    Profile
```

because:

```jsx
<Outlet/>
```

becomes:

```jsx
<Profile/>
```

---

# 3. Link

`Link` is used for navigation.

Normal HTML:

```html
<a href="/about">
About
</a>
```

causes page reload.

React way:

```jsx
<Link to="/about">
About
</Link>
```

No reload.

---

Example:

```jsx
import {Link} from "react-router-dom";


function Navbar(){

return (

<nav>


<Link to="/">
Home
</Link>


<Link to="/dashboard">
Dashboard
</Link>


</nav>

)

}
```

---

# 4. NavLink

`NavLink` is like Link but it knows:

"Is this link currently active?"

Example:

```jsx
import {NavLink} from "react-router-dom";


<NavLink
to="/dashboard"
>

Dashboard

</NavLink>
```

If URL:

```
/dashboard
```

It becomes active.

---

## Add Active Style

```jsx
<NavLink

to="/dashboard"

className={({isActive})=>

isActive
?
"bg-blue-500 text-white"
:
""

}

>

Dashboard

</NavLink>
```

When active:

```css
background: blue;
color:white;
```

---

# Dashboard Sidebar Example

```jsx
import {
NavLink
} from "react-router-dom";


function Sidebar(){


return (

<div>


<NavLink
to="profile"
>
Profile
</NavLink>


<NavLink
to="settings"
>
Settings
</NavLink>


<NavLink
to="orders"
>
Orders
</NavLink>


</div>

)

}
```

---

Dashboard layout:

```
Dashboard
--------------------------------

Sidebar        Content

Profile  -->   Profile page

Settings -->   Settings page

Orders   -->   Orders page

--------------------------------
```

---

# Complete Flow

User clicks:

```jsx
<NavLink to="profile">
Profile
</NavLink>
```

↓

URL changes:

```
/dashboard/profile
```

↓

Router finds:

```jsx
/dashboard
   |
   profile
```

↓

Render:

```
Dashboard.jsx

<Outlet/>

        ↓

Profile.jsx
```

---

# Difference Summary

|Thing|Purpose|
|---|---|
|Nested Route|Route inside route|
|Outlet|Shows child route component|
|Link|Move between pages|
|NavLink|Link + active state|

Simple memory:

```
Route = path setup

Outlet = child display area

Link = navigation

NavLink = navigation + active style
```

These 4 are used together in almost every React dashboard, admin panel, and e-commerce project.

-------

In React Router (v6.4+), **Loader** and **useLoaderData()** are used to load data **before a route component renders**.

Traditional way:

```jsx
useEffect()
   |
   ↓
API call
   |
   ↓
setState()
   |
   ↓
render
```

Problem:

- Component renders first
    
- Then data loads
    
- Need loading state
    

React Router loader:

```text
Route match
     |
     ↓
Loader runs
     |
     ↓
Data fetched
     |
     ↓
Component renders with data
```

---

## 1. Basic Loader Example

Install:

```bash
npm install react-router-dom
```

---

### Create API

Example:

```javascript
// api.js

export const getUsers = async()=>{

 const res = await fetch(
   "https://jsonplaceholder.typicode.com/users"
 );

 return res.json();

}
```

---

## Route Setup

`main.jsx`

```jsx
import {
 createBrowserRouter,
 RouterProvider
} from "react-router-dom";


import Users from "./Users";
import Home from "./Home";


const router = createBrowserRouter([


{
 path:"/",
 element:<Home/>
},


{
 path:"/users",
 element:<Users/>,

 loader:getUsers

}


]);



ReactDOM.createRoot(
document.getElementById("root")
)
.render(

<RouterProvider router={router}/>

);
```

---

## Component Read Data

`Users.jsx`

```jsx
import {
 useLoaderData
} from "react-router-dom";


function Users(){


const users = useLoaderData();


return (

<div>

{
users.map(user=>

<h2 key={user.id}>
{user.name}
</h2>

)
}

</div>

)

}


export default Users;
```

No `useEffect`, no `useState`.

---

# 2. Loader With Single Data

Example:

URL:

```
/users/5
```

Route:

```jsx
{
 path:"/users/:id",
 element:<UserDetails/>,
 loader:userLoader
}
```

---

Loader:

```javascript
export const userLoader = async({params})=>{


const res = await fetch(
 `https://jsonplaceholder.typicode.com/users/${params.id}`
);


return res.json();


}
```

---

Component:

```jsx
import {
useLoaderData
} from "react-router-dom";


function UserDetails(){


const user = useLoaderData();


return (

<h1>

{user.name}

</h1>

)

}
```

URL:

```
/users/5
```

Output:

```
Leanne Graham
```

---

# 3. Loader With Axios

Loader can use axios too.

Install:

```bash
npm install axios
```

---

```javascript
import axios from "axios";


export const productLoader = async()=>{


const res = await axios.get(
 "http://localhost:5000/products"
);


return res.data;


}
```

---

# 4. Multiple Data Loading

Need users + products.

```javascript
export const dashboardLoader = async()=>{


const users =
fetch("/users")
.then(res=>res.json());


const products =
fetch("/products")
.then(res=>res.json());



return {

users:await users,
products:await products

}


}
```

---

Component:

```jsx
const data = useLoaderData();


return (

<>

<h1>
Users
</h1>


{
data.users.map(user=>

<p>
{user.name}
</p>

)
}



<h1>
Products
</h1>


{
data.products.map(product=>

<p>
{product.title}
</p>

)
}


</>

)
```

---

# 5. Loader With Params + Query

URL:

```
/products?category=phone
```

Loader:

```javascript
export const productLoader = async({request})=>{


const url = new URL(
 request.url
);


const category =
url.searchParams.get("category");



const res = await fetch(
 `/products?category=${category}`
);


return res.json();

}
```

---

# 6. Loader Error Handling

```javascript
export const loader = async()=>{


const res =
await fetch("/users");


if(!res.ok){

 throw new Error(
 "Data load failed"
 );

}


return res.json();


}
```

---

Show error:

```jsx
import {
useRouteError
} from "react-router-dom";


function ErrorPage(){


const error =
useRouteError();


return (

<h1>
{error.message}
</h1>

)

}
```

Route:

```jsx
{
 path:"/users",
 element:<Users/>,
 loader,
 errorElement:<ErrorPage/>
}
```

---

# 7. Loader + Nested Route

Example:

```
Dashboard
 |
 |-- Profile
 |-- Settings
```

Route:

```jsx
{
 path:"dashboard",
 element:<Dashboard/>,

 loader:dashboardLoader,


 children:[

 {
 path:"profile",
 element:<Profile/>
 }

 ]

}
```

Dashboard:

```jsx
import {
Outlet,
useLoaderData
} from "react-router-dom";


function Dashboard(){


const data =
useLoaderData();


return (

<>

<h1>
{data.username}
</h1>


<Outlet/>


</>

)

}
```

---

# Loader vs useEffect

|Loader|useEffect|
|---|---|
|Runs before render|Runs after render|
|Route based|Component based|
|No loading flicker|Need loading state|
|Works with routing|Works anywhere|
|Can handle errors|Manual|

---

Real projects:

```
React Router
      |
      |
   Loader
      |
      |
 API Call
      |
      |
 Backend
      |
      |
 Database
```

Common use:

- Product details page
    
- User profile
    
- Dashboard data
    
- Blog details
    
- E-commerce pages
    

Loader + useLoaderData is the modern React Router data-fetching pattern.

-----------
# In React Router, **params** are used to create **dynamic routes** where the URL value changes.

Example:

```
/users/1
/users/2
/users/3
```

Same component, different data.

---

## 1. What is Dynamic Route?

Normal route:

```jsx
<Route 
 path="/about"
 element={<About/>}
/>
```

Only works:

```
/about
```

Dynamic route:

```jsx
<Route
 path="/users/:id"
 element={<User/>}
/>
```

Works:

```
/users/1
/users/2
/users/100
```

Here:

```
:id
```

is a dynamic parameter.

---

# 2. Create Dynamic Path

Example project:

```
src
 |
 ├── App.jsx
 ├── Users.jsx
 └── UserDetails.jsx
```

---

## App.jsx

```jsx
import {
 Routes,
 Route
} from "react-router-dom";


import Users from "./Users";
import UserDetails from "./UserDetails";


function App(){


return (

<Routes>


<Route
 path="/users"
 element={<Users/>}
/>


<Route
 path="/users/:id"
 element={<UserDetails/>}
/>


</Routes>

)

}


export default App;
```

---

Now URLs:

```
/users/10

/users/20

/users/50
```

all render:

```jsx
<UserDetails/>
```

---

# 3. Read Params Using useParams()

`UserDetails.jsx`

```jsx
import {
 useParams
} from "react-router-dom";


function UserDetails(){


const params = useParams();


return (

<div>

<h1>
User ID:
{params.id}
</h1>


</div>

)

}


export default UserDetails;
```

---

URL:

```
localhost:5173/users/25
```

Output:

```
User ID: 25
```

---

## Short way:

```jsx
const {id}=useParams();
```

instead of:

```jsx
const params=useParams();
```

Example:

```jsx
function UserDetails(){


const {id}=useParams();


return (

<h1>
{id}
</h1>

)

}
```

---

# 4. Create Dynamic Link

Users list:

```jsx
import {
Link
} from "react-router-dom";


function Users(){


const users=[

{
 id:1,
 name:"Atiar"
},

{
 id:2,
 name:"Rahim"
},

{
 id:3,
 name:"Karim"
}

];



return (

<div>


{
users.map(user=>(


<div key={user.id}>


<h2>
{user.name}
</h2>


<Link
to={`/users/${user.id}`}
>

View Details

</Link>


</div>


))

}


</div>

)

}
```

---

Output:

```
Atiar
View Details

Rahim
View Details

Karim
View Details
```

Click Atiar:

```
/users/1
```

Click Rahim:

```
/users/2
```

---

# 5. Fetch Data Using Params

Real example:

URL:

```
/products/5
```

Need product id.

```jsx
import {
useParams
} from "react-router-dom";

import {
useEffect,
useState
} from "react";


function ProductDetails(){


const {id}=useParams();


const [product,setProduct]=useState(null);



useEffect(()=>{


fetch(
`https://api.com/products/${id}`
)

.then(res=>res.json())

.then(data=>

setProduct(data)

)



},[id]);



return (

<>

{
product &&
<h1>
{product.title}
</h1>
}

</>

)

}
```

---

# 6. Multiple Params

Example:

```
/category/electronics/product/5
```

Route:

```jsx
<Route

path="/category/:category/product/:id"

element={<Product/>}

/>
```

URL:

```
/category/mobile/product/20
```

Read:

```jsx
const {
 category,
 id
}=useParams();
```

Result:

```javascript
category = "mobile"

id = "20"
```

---

# 7. Optional Params

```jsx
<Route

path="/profile/:username?"

element={<Profile/>}

/>
```

Works:

```
/profile

/profile/atiar
```

---

# 8. Dynamic Route + Loader

Modern React Router:

```jsx
{
 path:"/users/:id",

 element:<User/>,

 loader:userLoader
}
```

Loader:

```javascript
export const userLoader =
async({params})=>{


const res =
await fetch(
`/users/${params.id}`
);


return res.json();


}
```

---

# Real Project Example

E-commerce:

```
/products
        |
        |
        ↓
/products/101
        |
        |
ProductDetails
```

Blog:

```
/blog/react-router
/blog/javascript
/blog/python
```

Profile:

```
/profile/atiar
/profile/rahim
```

---

## Summary

|Concept|Use|
|---|---|
|`:id`|Create dynamic path|
|useParams()|Read URL value|
|Link|Create dynamic URL|
|map()|Generate multiple routes|
|params + API|Load specific data|

Memory:

```
Route:
 /users/:id

URL:
 /users/50

useParams():
 id = 50
```

Dynamic routes are used everywhere: products, users, blogs, dashboards, profiles.

-----------

# Explore Dynamic Route , Params & Load Data Based On Dynamic Route

Let's explore **Dynamic Route, Params, and Loading Data Based on Dynamic Route** in React Router.

This is one of the most common patterns in real projects:

- E-commerce product details
    
- Blog details
    
- User profile
    
- Job details
    
- Dashboard pages
    

---

# 1. What is Dynamic Route?

A dynamic route is a route where a part of the URL changes.

Example:

Normal route:

```jsx
/about
```

Only one page.

Dynamic route:

```jsx
/products/:id
```

Can create many pages:

```
/products/1
/products/2
/products/3
```

All use the same component.

---

# 2. Create Dynamic Route

Install:

```bash
npm install react-router-dom
```

---

## App.jsx

```jsx
import {
  Routes,
  Route
} from "react-router-dom";


import Products from "./Products";
import ProductDetails from "./ProductDetails";


function App(){

return (

<Routes>


<Route
 path="/products"
 element={<Products/>}
/>


<Route
 path="/products/:id"
 element={<ProductDetails/>}
/>


</Routes>

)

}


export default App;
```

Now:

```
/products/101
```

renders:

```jsx
<ProductDetails/>
```

---

# 3. Create Dynamic Links

Products list:

`Products.jsx`

```jsx
import {
 Link
} from "react-router-dom";


const Products = ()=>{


const products=[

{
 id:1,
 title:"Laptop",
 price:50000
},

{
 id:2,
 title:"Mobile",
 price:30000
},

{
 id:3,
 title:"Headphone",
 price:5000
}

];


return (

<div>


{
products.map(product=>(


<div key={product.id}>


<h2>
{product.title}
</h2>


<p>
{product.price}
</p>


<Link
to={`/products/${product.id}`}
>

Details

</Link>


</div>


))

}


</div>

)

}


export default Products;
```

---

Output:

```
Laptop
Details


Mobile
Details


Headphone
Details
```

Click Laptop:

URL:

```
/products/1
```

---

# 4. Read Params

`ProductDetails.jsx`

```jsx
import {
useParams
} from "react-router-dom";


const ProductDetails = ()=>{


const {id}=useParams();


return (

<h1>

Product ID:
{id}

</h1>

)

}


export default ProductDetails;
```

URL:

```
/products/2
```

Output:

```
Product ID: 2
```

---

# 5. Load Data Based on Dynamic Route

Now use the id to fetch data.

Example API:

```
https://fakestoreapi.com/products/1
```

---

## ProductDetails.jsx

```jsx
import {
useParams
} from "react-router-dom";


import {
useEffect,
useState
} from "react";



const ProductDetails = ()=>{


const {id}=useParams();


const [product,setProduct]=useState(null);



useEffect(()=>{


fetch(
`https://fakestoreapi.com/products/${id}`
)

.then(res=>res.json())

.then(data=>{

 setProduct(data);

})


},[id]);



if(!product){

return <h1>Loading...</h1>

}



return (

<div>


<h1>
{product.title}
</h1>


<img
src={product.image}
width="200"
/>


<h2>
${product.price}
</h2>


<p>
{product.description}
</p>


</div>

)

}


export default ProductDetails;
```

---

Flow:

```
User clicks product
        |
        ↓
URL changes

/products/3

        |
        ↓

useParams()

id = 3

        |
        ↓

API call

/products/3

        |
        ↓

Show product
```

---

# 6. Dynamic Route With Loader (Modern Way)

React Router v6.4+ recommends loaders.

Route:

```jsx
{
 path:"/products/:id",
 element:<ProductDetails/>,
 loader:productLoader
}
```

---

Loader:

```javascript
export const productLoader =
async({params})=>{


const res =
await fetch(
`https://fakestoreapi.com/products/${params.id}`
);


return res.json();


}
```

---

Component:

```jsx
import {
useLoaderData
} from "react-router-dom";


function ProductDetails(){


const product =
useLoaderData();



return (

<>

<h1>
{product.title}
</h1>


<h2>
${product.price}
</h2>

</>

)

}
```

No:

```jsx
useEffect()
useState()
```

needed.

---

# 7. Multiple Dynamic Params

Example:

URL:

```
/category/electronics/product/5
```

Route:

```jsx
<Route

path="/category/:category/product/:id"

element={<Product/>}

/>
```

Read:

```jsx
const {
category,
id
}=useParams();
```

Result:

```
category = electronics

id = 5
```

---

# 8. Real Project Examples

## E-commerce

```
/products
/products/100
```

Product ID loads details.

---

## Blog

```
/blog/react-router
/blog/javascript
```

Slug loads article.

---

## User Profile

```
/profile/atiar
/profile/rahim
```

Username loads profile.

---

## Job Portal

```
/jobs/frontend-developer-1
```

Job details load.

---

# Summary

|Concept|Purpose|
|---|---|
|Dynamic Route|Create changing URLs|
|`:id`|Dynamic value placeholder|
|useParams()|Read URL value|
|Link|Create dynamic URL|
|Loader|Fetch before rendering|
|useEffect|Fetch after rendering|

Simple memory:

```
Route:
 /products/:id


URL:
 /products/10


Params:
 id = 10


API:
 /products/10
```

This pattern is used in almost every professional React application.


----------------

# Explore Hooks UseNavigate And UseNavigator For Router Spinner

You mean **React Router hooks: `useNavigate` and `useNavigation`** (not `useNavigator`). These are used for navigation and loading/spinner handling.

---

# 1. useNavigate()

`useNavigate()` lets you change routes **using JavaScript code**.

Normally:

```jsx
<Link to="/home">
 Home
</Link>
```

User clicks manually.

With `useNavigate`:

```jsx
navigate("/home")
```

React moves automatically.

---

## Basic Example

```jsx
import {
  useNavigate
} from "react-router-dom";


function Login(){


const navigate = useNavigate();



const handleLogin = ()=>{


// login success


navigate("/dashboard");


}



return (

<button onClick={handleLogin}>

Login

</button>

)

}


export default Login;
```

Flow:

```
Click Button
      |
      ↓
navigate()
      |
      ↓
/dashboard
      |
      ↓
Dashboard Component
```

---

# 2. Go Back / Forward

Browser history control:

```jsx
const navigate = useNavigate();
```

Back:

```jsx
navigate(-1);
```

Equivalent:

```
Browser Back Button
```

Forward:

```jsx
navigate(1);
```

---

Example:

```jsx
<button
onClick={()=>navigate(-1)}
>
Back
</button>
```

---

# 3. Replace Current Route

Normally:

```
Login
  |
  ↓
Dashboard
```

User can go back to Login.

Replace:

```jsx
navigate(
"/dashboard",
{
 replace:true
}
)
```

Now history:

```
Dashboard
```

Login removed.

Used for:

- Login redirect
    
- Logout
    
- Protected routes
    

---

# 4. Send State with Navigate

You can pass data:

```jsx
navigate(
"/profile",
{
 state:{
   username:"Atiar"
 }
}
)
```

Receive:

```jsx
import {
useLocation
} from "react-router-dom";


const location =
useLocation();


console.log(
location.state.username
);
```

Output:

```
Atiar
```

---

# 5. useNavigation()

`useNavigation()` is for **router loading state**.

Example:

When you click:

```
Products
    |
    ↓
API loading
    |
    ↓
Show spinner
```

---

## Setup with Loader

Route:

```jsx
{
 path:"/products",
 element:<Products/>,
 loader:productsLoader
}
```

---

Loader:

```javascript
const productsLoader =
async()=>{


const res =
await fetch("/products");


return res.json();


}
```

---

## Add Spinner

App.jsx:

```jsx
import {
Outlet,
useNavigation
} from "react-router-dom";


function Layout(){


const navigation =
useNavigation();



return (

<>


{
navigation.state === "loading"
&&

<div>

Loading...

</div>

}


<Outlet/>


</>

)

}


export default Layout;
```

---

# Navigation States

`useNavigation()` gives:

```javascript
navigation.state
```

Values:

### idle

No loading:

```javascript
"idle"
```

---

### loading

Loader running:

```javascript
"loading"
```

---

### submitting

Form data sending:

```javascript
"submitting"
```

---

# Spinner Example

```jsx
function Spinner(){

return (

<div className="flex justify-center">

<span className="loading loading-spinner">

</span>

</div>

)

}
```

Use:

```jsx
{
navigation.state === "loading"
?
<Spinner/>
:
null
}
```

---

# Full Example

```jsx
import {
Outlet,
useNavigation
} from "react-router-dom";


function MainLayout(){


const navigation =
useNavigation();



return (

<div>


{
navigation.state === "loading"
&&

<div className="text-center">

Loading...

</div>

}



<Navbar/>


<Outlet/>


</div>

)

}
```

---

# Real Project Use

## Login

```javascript
navigate("/dashboard")
```

---

## After Create Product

```javascript
navigate("/products")
```

---

## Show API Loading

```javascript
useNavigation()
```

---

## Form Submit

```javascript
navigation.state==="submitting"
```

---

# Difference

|Hook|Use|
|---|---|
|useNavigate|Change route programmatically|
|useNavigation|Track router loading|
|useLocation|Read current URL/state|
|useParams|Read URL parameter|

Memory:

```
useNavigate()
      ↓
Move page


useNavigation()
      ↓
Know router status
      ↓
Show spinner
```

These two hooks are used heavily in modern React Router apps.


------------

## `useNavigate()` and `useLocation()` in React Router

These are two important React Router hooks.

- **useNavigate()** → change route using JavaScript
    
- **useLocation()** → get current URL information
    

---

# 1. useNavigate()

`useNavigate` is used when you want to move the user to another page by code.

Import:

```jsx
import { useNavigate } from "react-router-dom";
```

---

## Basic Example

```jsx
import { useNavigate } from "react-router-dom";


function Login(){

  const navigate = useNavigate();


  const handleLogin = ()=>{

    // after successful login

    navigate("/dashboard");

  }


  return (
    <button onClick={handleLogin}>
      Login
    </button>
  )

}

export default Login;
```

When button clicked:

```
/login
   |
   ↓
navigate()
   |
   ↓
/dashboard
```

---

# Navigate Back / Forward

Browser history control:

### Back

```jsx
navigate(-1);
```

Example:

```jsx
<button onClick={()=>navigate(-1)}>
 Back
</button>
```

Same as browser back button.

---

### Forward

```jsx
navigate(1);
```

---

# Replace Route

Normally:

```
Login
  ↓
Dashboard
```

User can go back to Login.

Use replace:

```jsx
navigate(
 "/dashboard",
 {
  replace:true
 }
);
```

Now:

```
Dashboard
```

Login removed from history.

Used for:

- login redirect
    
- logout
    
- protected route
    

---

# Send Data With Navigate

You can send state:

```jsx
navigate("/profile",{

 state:{
   name:"Atiar",
   role:"Developer"
 }

})
```

---

Receive data:

Use `useLocation()`:

```jsx
import { useLocation } from "react-router-dom";


function Profile(){

const location = useLocation();


return (

<div>

<h1>
{location.state.name}
</h1>

<p>
{location.state.role}
</p>

</div>

)

}
```

Output:

```
Atiar
Developer
```

---

# 2. useLocation()

`useLocation()` gives the current URL information.

Import:

```jsx
import {
 useLocation
} from "react-router-dom";
```

---

Example:

URL:

```
http://localhost:5173/products?id=10
```

Component:

```jsx
function Page(){


const location = useLocation();


console.log(location);


}
```

Output:

```javascript
{
 pathname:"/products",
 search:"?id=10",
 hash:"",
 state:null
}
```

---

# pathname

Current route:

```jsx
const location = useLocation();


console.log(location.pathname);
```

URL:

```
/about
```

Output:

```
/about
```

---

# search

Query string:

URL:

```
/products?category=phone
```

Code:

```jsx
console.log(location.search);
```

Output:

```
?category=phone
```

---

# Read Query Params

Use `URLSearchParams`

```jsx
import {
useLocation
} from "react-router-dom";


function Products(){


const location = useLocation();


const params =
new URLSearchParams(location.search);


const category =
params.get("category");


return (

<h1>
{category}
</h1>

)

}
```

URL:

```
/products?category=phone
```

Output:

```
phone
```

---

# Difference Between useNavigate and useLocation

|useNavigate|useLocation|
|---|---|
|Changes route|Reads route|
|Moves user|Gets URL info|
|Function|Object|
|`navigate("/home")`|`location.pathname`|

---

## Real Project Example

### After Login

```jsx
navigate("/dashboard");
```

---

### Check Current Page

```jsx
const location = useLocation();


if(location.pathname==="/dashboard"){

}
```

---

### Send Data

```jsx
navigate("/profile",{
 state:user
})
```

Receive:

```jsx
const location = useLocation();

location.state
```

---

Simple memory:

```
useNavigate()
        ↓
"Go there"


useLocation()
        ↓
"Where am I?"
```

Both are used together a lot in React Router projects.