

নিচে **Express.js backend এ production-level Swagger setup** দেখানো হলো। Industry backend projects সাধারণত **Express.js** এর সাথে **swagger-ui-express** এবং **swagger-jsdoc** ব্যবহার করে।

এটা এমনভাবে করা হয় যাতে:

* documentation auto generate হয়
* JWT auth support থাকে
* versioned API থাকে
* modular route structure থাকে

---

# 1️⃣ Production Folder Structure

Industry level Express backend সাধারণত এমন হয়:

```text
project
│
├── src
│   ├── controllers
│   │      auth.controller.js
│   │      user.controller.js
│   │
│   ├── routes
│   │      auth.routes.js
│   │      user.routes.js
│   │
│   ├── middlewares
│   │      auth.middleware.js
│   │
│   ├── docs
│   │      swagger.js
│   │
│   ├── app.js
│   └── server.js
│
├── package.json
```

Swagger config সাধারণত `docs/swagger.js` এ থাকে।

---

# 2️⃣ Required Packages Install

```bash
npm install swagger-ui-express swagger-jsdoc
```

Optional but useful:

```bash
npm install yamljs
```

---

# 3️⃣ Swagger Configuration (docs/swagger.js)

```javascript
const swaggerJsdoc = require("swagger-jsdoc");

const options = {
  definition: {
    openapi: "3.0.0",
    info: {
      title: "AI CCTV API",
      version: "1.0.0",
      description: "API documentation for AI CCTV surveillance system",
    },
    servers: [
      {
        url: "http://localhost:5000/api/v1",
      },
    ],
    components: {
      securitySchemes: {
        BearerAuth: {
          type: "http",
          scheme: "bearer",
          bearerFormat: "JWT",
        },
      },
    },
    security: [
      {
        BearerAuth: [],
      },
    ],
  },

  apis: ["./src/routes/*.js"],
};

const swaggerSpec = swaggerJsdoc(options);

module.exports = swaggerSpec;
```

### Important fields

| field                      | meaning                    |
| -------------------------- | -------------------------- |
| openapi                    | OpenAPI version            |
| info                       | API information            |
| servers                    | base API url               |
| components.securitySchemes | authentication             |
| apis                       | documentation source files |

---

# 4️⃣ Swagger UI Setup (app.js)

```javascript
const express = require("express");
const swaggerUi = require("swagger-ui-express");
const swaggerSpec = require("./docs/swagger");

const app = express();

app.use("/api-docs", swaggerUi.serve, swaggerUi.setup(swaggerSpec));

module.exports = app;
```

Server run করলে documentation পাওয়া যাবে:

```
http://localhost:5000/api-docs
```

---

# 5️⃣ Route Documentation Example

`routes/auth.routes.js`

```javascript
const express = require("express");
const router = express.Router();

/**
 * @swagger
 * /auth/login:
 *   post:
 *     summary: User login
 *     tags: [Authentication]
 *     description: Login user and return JWT token
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             properties:
 *               email:
 *                 type: string
 *               password:
 *                 type: string
 *     responses:
 *       200:
 *         description: Login successful
 *       401:
 *         description: Invalid credentials
 */

router.post("/login", (req, res) => {
  res.json({ message: "login success" });
});

module.exports = router;
```

Swagger UI তে দেখাবে:

```
POST /auth/login
```

---

# 6️⃣ Model Schema Documentation

Example user schema:

```javascript
/**
 * @swagger
 * components:
 *   schemas:
 *     User:
 *       type: object
 *       properties:
 *         id:
 *           type: integer
 *         name:
 *           type: string
 *         email:
 *           type: string
 */
```

এটা reusable schema।

---

# 7️⃣ Using Schema in Response

```javascript
/**
 * @swagger
 * /users:
 *   get:
 *     summary: Get all users
 *     tags: [Users]
 *     responses:
 *       200:
 *         description: Users list
 *         content:
 *           application/json:
 *             schema:
 *               $ref: '#/components/schemas/User'
 */
```

---

# 8️⃣ JWT Authentication Button

Swagger UI তে automatically দেখাবে:

```
Authorize 🔒
```

User token দিয়ে API test করতে পারবে।

Example header:

```
Authorization: Bearer <token>
```

---

# 9️⃣ Versioned API (Industry Practice)

Production APIs সাধারণত versioned হয়:

```
/api/v1/users
/api/v1/auth/login
/api/v2/users
```

Swagger config:

```javascript
servers: [
  {
    url: "http://localhost:5000/api/v1"
  }
]
```

---

# 🔟 Tags for Grouping

```javascript
tags:
  - name: Authentication
  - name: Users
  - name: Cameras
  - name: Alerts
```

Swagger UI:

```
Authentication
Users
Cameras
Alerts
```

---

# 1️⃣1️⃣ Example Request

Professional API docs এ example দেওয়া হয়:

```javascript
example:
{
 "email": "admin@example.com",
 "password": "123456"
}
```

---

# 1️⃣2️⃣ Production Result

Swagger UI দেখাবে:

```
Authentication
   POST /auth/login

Users
   GET /users
   GET /users/{id}

Cameras
   GET /cameras
   POST /cameras
```

এখান থেকে frontend developer directly API test করতে পারবে।

---

# 🚀 Pro Industry Tips

Production Express Swagger docs এ সাধারণত থাকে:

* OpenAPI 3.0 specification
* reusable schemas
* JWT authentication
* versioned API
* modular route documentation
* examples
* error responses

---

💡 যেহেতু তুমি **Django + AI CCTV system backend বানাচ্ছো**, একটা interesting জিনিস বলি — অনেক AI startup architecture হয়:

```
React frontend
↓
Express API Gateway
↓
Python AI microservice
```

এজন্য **Express + Swagger জানা future এ খুব useful হবে।**

---

যদি চাও, আমি তোমাকে আরও দেখাতে পারি:

**“Express.js + Swagger + JWT + Role based API documentation (enterprise pattern)”**
যেটা normally **large SaaS backend systems** এ ব্যবহার হয়।
