For Django REST API, a clean naming convention usually follows **resource-based URLs** (REST style).

### Recommended API naming

Use:

- lowercase
    
- plural nouns
    
- hyphen (`-`) for multiple words
    
- no verbs in URL
    

### Good examples

```
GET     /api/products/
POST    /api/products/

GET     /api/products/1/
PUT     /api/products/1/
PATCH   /api/products/1/
DELETE  /api/products/1/
```

---

## Users

```
GET     /api/users/
POST    /api/users/

GET     /api/users/1/
PATCH   /api/users/1/
DELETE  /api/users/1/
```

---

## Categories

```
GET  /api/categories/

POST /api/categories/

GET  /api/categories/1/products/
```

---

## Product images

Nested resource:

```
GET  /api/products/1/images/

POST /api/products/1/images/
```

Example:

```
/api/products/15/images/
```

returns:

```json
[
  {
    "id":1,
    "image":"phone1.jpg"
  },
  {
    "id":2,
    "image":"phone2.jpg"
  }
]
```

---

## Cart

Since cart belongs to user:

```
GET   /api/cart/

POST  /api/cart/items/

PATCH /api/cart/items/1/

DELETE /api/cart/items/1/
```

Example:

```
POST /api/cart/items/

{
 "product":5,
 "quantity":2
}
```

---

## Orders

```
GET  /api/orders/

POST /api/orders/

GET /api/orders/10/
```

Order items:

```
GET /api/orders/10/items/
```

---

## Authentication

Common pattern:

```
POST /api/auth/register/

POST /api/auth/login/

POST /api/auth/logout/

POST /api/auth/refresh-token/
```

---

## Search / Filter

Query params:

```
GET /api/products/?category=electronics

GET /api/products/?min_price=100&max_price=1000

GET /api/products/?search=phone
```

---

## Versioning (large project)

Use:

```
/api/v1/products/

/api/v1/orders/
```

Example:

```
GET /api/v1/products/
```

---

### Avoid ❌

```
/getProducts
/createProduct
/deleteProduct
/product-list
/allUsers
```

Prefer ✅

```
/products/
/users/
/orders/
```

A typical e-commerce API structure:

```
api/
 ├── v1/
 │    ├── users/
 │    ├── products/
 │    ├── categories/
 │    ├── cart/
 │    ├── orders/
 │    └── payments/
```


----

