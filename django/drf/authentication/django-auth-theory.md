দারুণ। আমরা এই কোর্সটা এমনভাবে করব যেন শেষে আপনি **Google, GitHub, Microsoft, Facebook—যেকোনো OAuth provider** Django + DRF project-এ নিজে integrate করতে পারেন।

---

# Lesson 1: Authentication-এর Foundation (OAuth শেখার আগে যা অবশ্যই জানতে হবে)

> **Goal:** OAuth শেখার আগে Authentication-এর পুরো picture মাথায় বসানো।

---

# একটি প্রশ্ন

ধরুন আপনার Django API আছে।

```
POST /api/login
```

User login করল

```
Email:
admin@gmail.com

Password:
123456
```

এখন প্রশ্ন হলো—

> **পরের request-এ server কীভাবে বুঝবে এই user আগে login করেছে?**

যেমন

```
GET /api/profile
```

এখানে password তো আবার পাঠাচ্ছে না।

তাহলে?

---

## Answer

Login করার পরে server user-কে একটা **proof** দেয়।

যেমন—

```
You are authenticated.

Here is your proof.

ABCDEFG123456
```

এরপর user প্রতিটি request-এ সেই proof পাঠায়।

```
Authorization:

Bearer ABCDEFG123456
```

Server proof verify করে।

ঠিক থাকলে

```
Authenticated
```

---

# Authentication কী?

Authentication =

> **তুমি কে?**

Example

```
User:

I am Atiar.
```

Server

```
Proof?
```

User

```
Password
```

Server

```
Correct.

You are Atiar.
```

এটাই Authentication।

---

# Authorization কী?

Authentication-এর পরে আসে Authorization।

Example

```
User login করেছে।

এখন

DELETE /products/1
```

Server

```
You are authenticated.

But...

Are you admin?
```

যদি না হয়

```
403 Forbidden
```

---

## তাই

Authentication

```
Who are you?
```

Authorization

```
What can you do?
```

---

# Real Life Example

Airport

Authentication

```
Passport দেখাও।
```

Authorization

```
Business Lounge-এ ঢুকতে পারবে?
```

---

# Django Login Flow

```
Browser

↓

POST /login

↓

Django

↓

Check email

↓

Check password

↓

Correct?

↓

YES

↓

Create authentication proof

↓

Return proof

↓

Browser stores proof

↓

Every request sends proof

↓

Server verifies proof
```

এটাই সব Authentication system-এর ভিত্তি।

---

# এখন Proof কী হতে পারে?

এখান থেকেই বিভিন্ন Authentication system শুরু।

---

## 1. Session Authentication

```
User Login

↓

Server creates Session

↓

Database

↓

Session ID

↓

Cookie

↓

Browser stores Cookie
```

প্রতিবার browser cookie পাঠায়।

Django-এর default login এটাই।

---

## 2. Token Authentication

```
User Login

↓

Server

↓

Token

↓

Client stores token

↓

Every request

↓

Authorization

Token xxxxxxxxx
```

---

## 3. JWT

```
User Login

↓

JWT

↓

Client stores JWT

↓

Authorization

Bearer JWT
```

আজকাল DRF-এ সবচেয়ে popular।

---

## 4. OAuth

OAuth একটু আলাদা।

এখানে password আপনার server দেখে না।

```
User

↓

Google Login

↓

Google verifies password

↓

Google tells your app

Yes.

This user is genuine.
```

এটাই OAuth-এর magic।

---

# চারটি Authentication-এর তুলনা

| Method  | Password কে verify করে? | Server password জানে? |
| ------- | ----------------------- | --------------------- |
| Session | Your Server             | ✅ হ্যাঁ               |
| Token   | Your Server             | ✅ হ্যাঁ               |
| JWT     | Your Server             | ✅ হ্যাঁ               |
| OAuth   | Google/GitHub ইত্যাদি   | ❌ না                  |

---

# একটা বাস্তব উদাহরণ

### Normal Login

```
You

↓

My Website

↓

Password

↓

Database

↓

Login
```

Website আপনার password জানে।

---

### Google Login

```
You

↓

Google

↓

Password

↓

Google verifies

↓

Google says

This user is valid.

↓

My Website
```

Website কখনো আপনার Google password দেখে না।

---

# Beginner Mistake #1

অনেকে ভাবে

> OAuth = JWT

❌ ভুল।

OAuth login করার **উপায়**।

JWT হলো **login-এর পরে authentication token**।

অনেক project-এ flow এমন হয়:

```
Google OAuth

↓

User verified

↓

Create User

↓

Issue JWT

↓

Frontend stores JWT

↓

DRF Authentication
```

অর্থাৎ OAuth + JWT একসাথে ব্যবহার করা খুবই সাধারণ।

---

# Beginner Mistake #2

অনেকে ভাবে

```
Google Login
```

মানে

```
JWT নেই।
```

❌ ভুল।

বাস্তবে বেশিরভাগ Django API-তে:

```
Google OAuth

↓

Backend

↓

SimpleJWT

↓

Access Token

↓

Refresh Token
```

---

# Real Project Flow (আপনি যা ব্যবহার করবেন)

```
React

↓

Login with Google

↓

Google

↓

Returns authorization code

↓

Django Backend

↓

Google API

↓

User information

↓

Create/Login User

↓

SimpleJWT

↓

Access Token

↓

Refresh Token

↓

React stores JWT

↓

Every API request uses JWT
```

এটি modern Django + DRF architecture-এর একটি খুব সাধারণ pattern।

---

# Senior Tips

OAuth শিখতে গেলে আগে এই ৫টি জিনিস পরিষ্কার থাকতে হবে:

1. Authentication কী?
2. Authorization কী?
3. Session কীভাবে কাজ করে?
4. Token/JWT কীভাবে কাজ করে?
5. Browser এবং Server কীভাবে একে অপরকে বিশ্বাস করে?

এই ভিত্তি পরিষ্কার থাকলে OAuth-এর flow অনেক সহজ লাগবে।

---

# Lesson 1 Summary

আপনি আজ শিখলেন:

* ✅ Authentication = "তুমি কে?"
* ✅ Authorization = "তুমি কী করতে পারো?"
* ✅ Session, Token, JWT, OAuth-এর মৌলিক পার্থক্য
* ✅ OAuth-এ আপনার server user-এর password দেখে না
* ✅ OAuth-এর পরে JWT ব্যবহার করা খুবই সাধারণ

---

## Homework (অবশ্যই করুন)

নিজের ভাষায় নিচের প্রশ্নগুলোর উত্তর লিখুন:

1. Authentication এবং Authorization-এর মধ্যে পার্থক্য কী?
2. Session Authentication কীভাবে কাজ করে?
3. JWT Authentication কীভাবে কাজ করে?
4. OAuth-এ কেন আমাদের server user-এর password পায় না?
5. কেন OAuth-এর পরে JWT ব্যবহার করা হয়?

**Lesson 2**-এ আমরা শুরু করব **OAuth-এর core concept**: *OAuth আসলে কী, কেন তৈরি হয়েছে, এবং Authorization Code Flow কীভাবে কাজ করে।* এখান থেকেই আসল OAuth যাত্রা শুরু হবে।


--------
চমৎকার। আজ থেকে আসল OAuth শুরু।

আগের Lesson-এর ভিত্তি মনে রাখুন:

* Authentication = আমি কে?
* OAuth = **অন্য একটি trusted service আমার পরিচয় verify করবে।**

---

# Lesson 2 — OAuth আসলে কী? (The Big Picture)

## আজকের Goal

আজ code লিখব না।

আজ এমনভাবে OAuth বুঝব, যাতে Google, GitHub, Facebook—সব OAuth একই মনে হয়।

---

# একটি সমস্যা দিয়ে শুরু করি

ধরুন আপনার একটি Django Website আছে।

```text
shop.com
```

আপনি login page বানিয়েছেন।

```text
Email

Password

[Login]
```

এখন user password দিল।

```text
atiar@gmail.com

123456
```

আপনার server password verify করল।

সব ঠিক।

---

## কিন্তু সমস্যা কোথায়?

এখন user-কে আরও ১০০টা website-এ account করতে হবে।

```text
Amazon

Facebook

Netflix

Spotify

GitHub

Medium
```

প্রত্যেকটায়

```text
Email

Password
```

নতুন password।

এতে সমস্যা কী?

* User অনেক password মনে রাখতে পারে না।
* একই password বারবার ব্যবহার করে।
* Password leak হলে অনেক account ঝুঁকিতে পড়ে।

---

# তখন Google বলল...

Google বলল,

> "Password আমাদের কাছেই থাকুক। অন্য website-কে password দেবেন না।"

তখন OAuth-এর ধারণা আসে।

---

# OAuth-এর মূল ধারণা

OAuth-এর অর্থ:

> **আমি তোমাকে আমার password দেব না, কিন্তু আমি Google-কে বলব যে তুমি আমাকে বিশ্বাস করতে পারো।**

---

# Normal Login বনাম OAuth Login

## Normal Login

```text
User
    │
    │ Email + Password
    ▼
Your Django Server
    │
    ▼
Database
```

এখানে আপনার server password জানে।

---

## OAuth Login

```text
User
    │
    ▼
Google
    │
Password only here
    │
    ▼
Google verifies user
    │
    ▼
Your Django Server
```

এখানে

**Password কখনো Django-তে আসে না।**

এটাই OAuth-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়।

---

# Real Life Example

ধরুন আপনি একটি অফিসে ঢুকবেন।

Security Guard বলল

```text
ID Card?
```

আপনি বললেন

```text
আমি Google Company-র employee.
```

Guard বলল

```text
Proof?
```

আপনি Google-issued ID Card দেখালেন।

Guard বলল

```text
ঠিক আছে।

Google already verified you.

Come in.
```

Guard আপনার জন্মসনদ দেখেনি।

Google-এর verification-কে trust করেছে।

OAuth-ও ঠিক এভাবেই কাজ করে।

---

# OAuth-এর Actors (সবচেয়ে গুরুত্বপূর্ণ)

OAuth-এ ৪টি Actor থাকে।

---

## 1. Resource Owner

এটা কে?

User।

```text
Atiar
```

OAuth specification-এ একে বলে

> Resource Owner

কারণ user-এর data user-এরই।

---

## 2. Client

এটা কে?

আপনার Django Application।

```text
shop.com
```

এটাই Google-এর কাছে permission চাইবে।

---

## 3. Authorization Server

এটা কে?

Google।

অথবা

GitHub

Microsoft

Facebook

এরা login verify করে।

---

## 4. Resource Server

Google-এর API।

যেখানে user information থাকে।

যেমন

```text
Name

Email

Picture
```

---

# পুরো Flow

```text
User

↓

Your Django App

↓

Google Login

↓

Google asks

"Allow this app?"

↓

User clicks YES

↓

Google returns permission

↓

Django gets user info

↓

Create/Login User

↓

Issue JWT
```

এই flow-টাই OAuth-এর heart।

---

# OAuth কি Login System?

**এখানেই সবচেয়ে বড় confusion।**

অনেকে বলে

```text
OAuth = Login
```

আসলে

**পুরোপুরি না।**

OAuth মূলত

> **Authorization Framework**

মানে

একটি application আরেকটি application-এর resource access করার permission পায়।

Login পরে জনপ্রিয় use case হয়ে গেছে।

---

# তাহলে Google Login কেন?

Google Login-এ

Google বলে

```text
এই user verified.
```

তারপর

আপনার app user-এর email নিয়ে নিজের database-এ user create করে।

অর্থাৎ

Google আপনার হয়ে login করে দেয় না।

Google শুধু identity verify করে।

---

# একটি Example

ধরুন

আপনি Canva-তে

```text
Continue with Google
```

চাপলেন।

Canva কী করে?

না।

Canva Google database use করে না।

Canva নিজের database-এ

```text
Name

Email

User ID
```

save করে।

---

# Django-এর কাজ কী?

Google verify করবে।

কিন্তু

আপনার Django করবে

```text
Create User

OR

Existing User Login
```

অর্থাৎ

শেষ সিদ্ধান্ত আপনার server-এর।

---

# Beginner Mistake #1

অনেকে ভাবে

```text
Google login করলে

Google আমার website-এ user store করে।
```

❌ ভুল।

Google user store করে না।

আপনার Django database-এই user থাকবে।

---

# Beginner Mistake #2

অনেকে ভাবে

```text
OAuth = Google API
```

❌ ভুল।

Google OAuth support করে।

GitHub-ও করে।

Microsoft-ও করে।

Facebook-ও করে।

এমনকি আপনার নিজের company-ও OAuth Provider হতে পারে।

---

# Beginner Mistake #3

অনেকে ভাবে

```text
OAuth মানেই Google।
```

না।

Google শুধু একটি OAuth Provider।

---

# OAuth-এর সবচেয়ে গুরুত্বপূর্ণ শব্দ

আজ শুধু এই ৫টি শব্দ মুখস্থ করবেন না, **বুঝবেন**।

| Term                 | Meaning              |
| -------------------- | -------------------- |
| Resource Owner       | User                 |
| Client               | Your Django App      |
| Authorization Server | Google               |
| Resource Server      | Google API           |
| Access Token         | Permission-এর প্রমাণ |

---

# Senior Developer Perspective

Senior Developer OAuth implement করার সময় প্রথমে code লেখে না।

সে আগে নিজেকে জিজ্ঞাসা করে—

> User কে?

↓

> কে verify করবে?

↓

> কে data-এর owner?

↓

> কোন server token issue করবে?

↓

> আমার backend-এর responsibility কোথায় শুরু হবে?

এই thinking-টাই আপনাকে senior level-এ নিয়ে যাবে।

---

# Lesson 2 Summary

আজ আপনি শিখলেন:

* ✅ OAuth কেন তৈরি হয়েছে।
* ✅ Password কেন আপনার Django server-এ আসে না।
* ✅ OAuth-এর ৪টি প্রধান Actor।
* ✅ Google শুধু identity verify করে।
* ✅ User শেষ পর্যন্ত আপনার Django database-এই থাকে।
* ✅ OAuth একটি Authorization Framework; login তার একটি জনপ্রিয় ব্যবহার।

---

# Homework

নিচের প্রশ্নগুলোর উত্তর নিজের ভাষায় লিখুন:

1. OAuth কেন তৈরি হয়েছে?
2. Normal Login এবং OAuth Login-এর মধ্যে সবচেয়ে বড় পার্থক্য কী?
3. Resource Owner কে?
4. Client কে?
5. Authorization Server কে?
6. Resource Server কে?
7. Google Login করার পরে কেন Django-তে user create করতে হয়?

---

## পরের Lesson (Lesson 3)

এখন আমরা **OAuth-এর সবচেয়ে গুরুত্বপূর্ণ Flow** শিখব:

* Authorization Code কী?
* Redirect URI কী?
* Client ID কী?
* Client Secret কী?
* State Parameter কী?
* Browser কীভাবে Google-এর কাছে যায় এবং আবার Django-তে ফিরে আসে?

এই Lesson-এর পর OAuth-এর পুরো request/response flow আপনার কাছে পরিষ্কার হয়ে যাবে।


-----------
দারুণ। আজকের Lesson-টা পুরো OAuth-এর **heart**। এই lesson বুঝতে পারলে Google, GitHub, Microsoft—সব OAuth provider একই pattern মনে হবে।

> **Goal:** Authorization Code Flow সম্পূর্ণ বুঝে ফেলা।

---

# Lesson 3 — Authorization Code Flow (The Heart of OAuth)

## প্রথমে একটি বাস্তব উদাহরণ

ধরুন আপনি একটি conference-এ গেছেন।

Registration Desk আপনাকে একটি **Token Number** দিল।

```text
Token: A-102
```

এই Token দিয়ে আপনি পরে ID Card সংগ্রহ করবেন।

খেয়াল করুন—

**Token Number ≠ ID Card**

এটা শুধু একটা temporary proof।

OAuth-এ **Authorization Code** ঠিক এমনই।

---

# পুরো Flow (Bird's Eye View)

```text
+--------+         +----------------+         +----------------------+
|  User  |         | Django Backend |         | Google OAuth Server  |
+--------+         +----------------+         +----------------------+
     |                     |                          |
     | Login with Google   |                          |
     |-------------------->|                          |
     |                     | Redirect user           |
     |<--------------------|                          |
     |===============================================>|
     |        Google Login + Consent                 |
     |<===============================================|
     |                     |                          |
     |  Redirect with Code |                          |
     |-------------------->|                          |
     |                     | Exchange Code           |
     |                     |------------------------->|
     |                     | Access Token            |
     |                     |<-------------------------|
     |                     | Get User Info           |
     |                     |------------------------->|
     |                     | Email, Name            |
     |                     |<-------------------------|
     |                     | Create/Login User       |
     |                     | Issue JWT               |
     |<--------------------|                          |
```

এখন আমরা প্রতিটি step বুঝব।

---

# Step 1 — User Clicks Login

Frontend-এ button:

```text
[ Continue with Google ]
```

User click করল।

এখনও Google-এর সাথে কোনো authentication হয়নি।

---

# Step 2 — Redirect to Google

Browser Google-এ যায়।

উদাহরণ (সহজ করে):

```text
https://accounts.google.com/o/oauth2/auth
```

সাথে কিছু information যায়।

যেমন—

```text
client_id=abc123

redirect_uri=https://myapp.com/auth/google/callback

scope=email profile

response_type=code

state=random123
```

এখন প্রতিটা বুঝি।

---

# Client ID

Google জানতে চায়—

> "কে permission চাইছে?"

তাই প্রতিটি application-এর একটি public ID থাকে।

```text
Client ID

abc123xyz
```

এটা secret না।

Frontend-এ থাকলেও সমস্যা নেই।

---

# Redirect URI

Google login শেষ হলে কোথায় ফিরে যাবে?

উদাহরণ

```text
https://myapp.com/auth/google/callback
```

Google এই URL-এই user-কে ফেরত পাঠাবে।

---

# Scope

User-এর কোন data লাগবে?

উদাহরণ

```text
email

profile
```

অর্থাৎ

```text
Need email

Need profile picture

Need name
```

Google তখন user-কে সেটাই দেখাবে।

---

# Response Type

Google-কে বলা হচ্ছে

```text
response_type=code
```

মানে

> "Access Token এখন দিও না। আগে Authorization Code দাও।"

এটাই Authorization Code Flow।

---

# State Parameter

এটা security-এর জন্য।

একটা random value।

যেমন

```text
9fa83x7kLm12
```

পরে Google একই value ফেরত পাঠাবে।

যদি না মেলে

→ Request reject।

এটা CSRF attack প্রতিরোধে ব্যবহৃত হয়।

---

# Step 3 — Google Login Screen

Google user-কে দেখায়

```text
Login with Gmail
```

Password user Google-কেই দেয়।

আপনার Django কখনো password দেখে না।

---

# Step 4 — Consent Screen

Google জিজ্ঞাসা করে

```text
MyApp wants access to:

✓ Email

✓ Profile

Allow?

[Allow]

[Deny]
```

User Allow চাপল।

---

# Step 5 — Google Returns Authorization Code

Google redirect করল

```text
https://myapp.com/auth/google/callback
```

সাথে

```text
code=4ab93cd....

state=9fa83x7kLm12
```

খেয়াল করুন

Google এখনও Access Token দেয়নি।

শুধু

Authorization Code।

---

# Authorization Code কী?

এটা একটি

**temporary one-time code**

উদাহরণ

```text
code=x7Yp91LkQ
```

এর বৈশিষ্ট্য

* অল্প সময় valid
* একবার ব্যবহার করা যায়
* Access Token পাওয়ার জন্য ব্যবহার হয়

---

# কেন সরাসরি Access Token দেয় না?

কারণ Browser নিরাপদ জায়গা নয়।

যদি Browser-এই Access Token দিত

তাহলে malicious JavaScript

বা

Browser extension

বা

Attacker

Token চুরি করতে পারত।

তাই Google বলে

```text
Browser

↓

Only Authorization Code
```

এরপর

```text
Backend

↓

Access Token
```

---

# Step 6 — Backend Exchanges the Code

এখন Django Backend Google-কে বলে

```text
Hi Google,

Here is the code.

Please give me an Access Token.
```

সাথে পাঠায়

```text
Client ID

Client Secret

Authorization Code
```

---

# Client Secret

এটা password-এর মতো।

```text
Client Secret

sdf83h2jks82...
```

এটা কখনো Frontend-এ যাবে না।

শুধু Backend জানবে।

---

# Google Verification

Google check করে

* Client ID ঠিক?
* Client Secret ঠিক?
* Code valid?
* Code expire হয়নি?
* Redirect URI match করছে?

সব ঠিক হলে

```text
Access Token
```

ফেরত দেয়।

---

# Step 7 — Access Token

Google দেয়

```text
access_token

ya29.a0....
```

এটা দিয়ে Google API call করা যায়।

---

# Step 8 — Get User Information

Django Backend

```text
GET User Info
```

Google বলে

```json
{
  "email": "atiar@gmail.com",
  "name": "Md Atiar Rahman",
  "picture": "...",
  "verified_email": true
}
```

---

# Step 9 — Django Creates or Finds User

Backend

```python
user = User.objects.filter(email=email).first()

if not user:
    create_user(...)
```

এখানেই আপনার database update হয়।

---

# Step 10 — Issue JWT

এখন Google-এর কাজ শেষ।

আপনার Backend

SimpleJWT দিয়ে

```text
Access Token

Refresh Token
```

generate করে React-এ পাঠায়।

এরপর আর Google দরকার হয় না।

---

# পুরো Flow একসাথে

```text
React

↓

Google Login

↓

Google Authentication

↓

Authorization Code

↓

Django Backend

↓

Access Token

↓

User Info

↓

Create/Login User

↓

SimpleJWT

↓

Frontend
```

---

# OAuth-এ সবচেয়ে গুরুত্বপূর্ণ ৫টি জিনিস

| Term               | কাজ                                |
| ------------------ | ---------------------------------- |
| Client ID          | Application-এর Public Identity     |
| Client Secret      | Application-এর Secret              |
| Redirect URI       | Login শেষে কোথায় ফিরবে            |
| Authorization Code | Temporary Code                     |
| Access Token       | Google API ব্যবহার করার Permission |

---

# Beginner Mistakes

### ❌ Mistake 1

Authorization Code = Access Token

না।

Code দিয়ে Token আনা হয়।

---

### ❌ Mistake 2

Client Secret React-এ রাখা।

এটা খুব বড় Security Risk।

Client Secret শুধুমাত্র Backend-এ থাকবে।

---

### ❌ Mistake 3

Redirect URI change করা।

Google Console-এ যেটা register করেছেন, request-এ ঠিক সেটাই ব্যবহার করতে হবে।

---

### ❌ Mistake 4

State parameter ignore করা।

এটা CSRF protection-এর গুরুত্বপূর্ণ অংশ।

---

# Senior Thinking

Senior Developer OAuth implement করার সময় এই প্রশ্নগুলো মাথায় রাখে:

1. Browser কোন data দেখতে পারবে?
2. Backend কোন secret রাখবে?
3. কোন step-এ user identity verify হলো?
4. কোন step-এ আমার database update হবে?
5. Google-এর role কোথায় শেষ, আমার backend-এর role কোথায় শুরু?

---

# Lesson 3 Summary

আজ আপনি শিখলেন:

* ✅ Authorization Code Flow-এর সম্পূর্ণ lifecycle
* ✅ Client ID-এর কাজ
* ✅ Client Secret-এর কাজ
* ✅ Redirect URI কেন লাগে
* ✅ Scope কী
* ✅ State Parameter কেন গুরুত্বপূর্ণ
* ✅ Authorization Code ও Access Token-এর পার্থক্য
* ✅ Django Backend কীভাবে User তৈরি করে এবং JWT issue করে

---

## Homework

নিজের ভাষায় নিচের প্রশ্নগুলোর উত্তর লিখুন:

1. কেন Google প্রথমেই Access Token দেয় না?
2. Authorization Code-এর কাজ কী?
3. Client ID এবং Client Secret-এর মধ্যে পার্থক্য কী?
4. Redirect URI ভুল হলে কী হতে পারে?
5. State Parameter কেন ব্যবহার করা হয়?
6. Google-এর কাজ কোথায় শেষ হয় এবং Django Backend-এর কাজ কোথা থেকে শুরু হয়?

### পরের Lesson (Lesson 4)

এবার আমরা **Google OAuth Console Setup**-এ যাব। আপনি শিখবেন:

* Google Cloud Console-এ OAuth App তৈরি
* OAuth Consent Screen
* Client ID ও Client Secret তৈরি
* Redirect URI configure করা
* Localhost এবং Production-এর configuration

এরপর থেকেই আমরা Django + DRF-এ বাস্তব implementation শুরু করব।

----------
দারুণ। আজ থেকে আমরা **real implementation** শুরু করছি।

এখন পর্যন্ত আপনি flow বুঝেছেন। এবার Google Console-এ OAuth App তৈরি শিখবেন। একজন Senior Django Developer-এর প্রথম কাজই হলো OAuth Provider (Google) configure করা।

---

# Lesson 4 — Google OAuth Console Setup

## আজকের Goal

আজ আপনি শিখবেন—

* Google Cloud Project কী
* OAuth App কী
* OAuth Consent Screen
* Client ID
* Client Secret
* Redirect URI
* Development vs Production

> **আজ কোনো Django code লিখব না।** প্রথমে infrastructure ঠিক করব।

---

# Step 1 — Google Cloud Project কী?

আপনি যখন Google OAuth ব্যবহার করবেন, Google আগে জানতে চাইবে—

> "এই application কে বানিয়েছে?"

তাই Google Cloud-এ একটি Project তৈরি করতে হয়।

ভাবুন এটা আপনার application's identity।

```
Google Cloud

└── My Ecommerce API
      ├── OAuth
      ├── Maps API
      ├── Gmail API
      └── Billing
```

একটি Project-এর ভিতরে অনেক Google Service থাকতে পারে।

---

# Step 2 — OAuth App Registration

আপনি Google-কে বলছেন—

```
আমার Application-এর নাম:

Shop API

এটা Google Login ব্যবহার করবে।
```

Google তখন আপনার App-কে register করে।

এরপর Google দুইটি জিনিস দেয়।

```
Client ID

Client Secret
```

---

# Client ID

এটা আপনার App-এর Public Identity।

উদাহরণ

```
123456789-abcdef.apps.googleusercontent.com
```

এটা secret নয়।

Google যখন request পায়

```
client_id=123456...
```

তখন Google বুঝে

> "এই request Shop API থেকে এসেছে।"

---

# Client Secret

এটা Application-এর Password।

উদাহরণ

```
GOCSPX-xxxxxxxxxxxxxxxx
```

এটা কখনো

* React-এ যাবে না
* JavaScript-এ যাবে না
* GitHub-এ push করা যাবে না

শুধু Backend জানবে।

---

# OAuth Consent Screen

এটাই সেই screen যেটা user দেখে।

উদাহরণ

```
Shop API

This app wants to access

✓ Email

✓ Profile

Allow?

[Allow]

[Deny]
```

এই screen Google নিজে generate করে।

আপনি শুধু information দেন।

---

# Consent Screen-এ কী কী থাকে?

```
Application Name

Logo

Support Email

Developer Contact

Scopes

Privacy Policy URL

Terms of Service URL
```

Production App-এ এগুলো গুরুত্বপূর্ণ।

---

# Scope কী?

Google-কে বলতে হবে

```
আমার কী দরকার?
```

Example

```
email
profile
```

মানে

```
Name

Email

Profile Picture
```

---

আরও Scope হতে পারে

```
Google Drive

Calendar

Gmail

Contacts
```

আপনি যত scope চাইবেন,

Google তত permission user-এর কাছে চাইবে।

---

# Principle of Least Privilege

Senior Developer সবসময়

**Minimum Scope**

ব্যবহার করে।

যদি শুধু email লাগে

তাহলে

```
email
```

চাইবেন।

Drive Access চাইবেন না।

---

# Redirect URI

এটা সবচেয়ে গুরুত্বপূর্ণ।

Google Login শেষ হলে

Google কোথায় ফিরে আসবে?

উদাহরণ

```
http://localhost:8000/auth/google/callback/
```

Production

```
https://api.shop.com/auth/google/callback/
```

Google শুধু Registered Redirect URI-তেই redirect করবে।

---

# যদি Redirect URI Match না করে?

ধরুন

Google Console-এ আছে

```
http://localhost:8000/auth/google/callback/
```

কিন্তু request গেল

```
http://localhost:8000/google/callback/
```

Google সঙ্গে সঙ্গে reject করবে।

কারণ

```
Redirect URI Mismatch
```

---

# Authorized JavaScript Origin

এটা Frontend-এর Domain।

উদাহরণ

Development

```
http://localhost:3000
```

Production

```
https://shop.com
```

---

# Redirect URI vs JavaScript Origin

অনেক Beginner confuse হয়।

JavaScript Origin

```
React কোথায় চলছে?
```

Redirect URI

```
Google Login শেষে কোথায় redirect করবে?
```

দুইটা আলাদা।

---

# Development Environment

ধরুন

React

```
localhost:5173
```

Django

```
localhost:8000
```

তাহলে

```
Origin

http://localhost:5173

Redirect URI

http://localhost:8000/auth/google/callback/
```

---

# Production Environment

```
React

https://shop.com

Backend

https://api.shop.com

Redirect URI

https://api.shop.com/auth/google/callback/
```

---

# Environment Variables

কখনো

এভাবে লিখবেন না।

```python
CLIENT_SECRET = "GOCSPX-XXXXXXXXXXXX"
```

সবসময়

```
.env
```

```
GOOGLE_CLIENT_ID=....

GOOGLE_CLIENT_SECRET=....
```

তারপর

```python
settings.py
```

```
GOOGLE_CLIENT_ID

GOOGLE_CLIENT_SECRET
```

---

# Project Structure

একটি Professional Django Project

```
backend/

    settings.py

    .env

apps/

    authentication/

        views.py

        services.py

        urls.py
```

OAuth Secret

```
.env
```

---

# Production Security

Never

```
GitHub Push
```

```
.env
```

Never

```
Expose Client Secret
```

Never

```
Send Client Secret to React
```

---

# Real Project Architecture

```
React

↓

Google Login

↓

Google

↓

Redirect

↓

Django

↓

Google API

↓

User Info

↓

Create User

↓

JWT

↓

React
```

Google Console-এর Configuration এই Flow-এর শুরু।

---

# Beginner Mistakes

## ❌ Mistake 1

Client Secret React-এ রাখা।

এটা মারাত্মক ভুল।

---

## ❌ Mistake 2

Development Redirect URI

Production-এ ব্যবহার করা।

---

## ❌ Mistake 3

সব Google Scope add করা।

যেটা দরকার শুধু সেটাই নিন।

---

## ❌ Mistake 4

.env GitHub-এ Push করা।

এটা করলে Secret leak হয়ে যাবে।

---

# Senior Best Practices

✅ আলাদা Google Project ব্যবহার করুন Development এবং Production-এর জন্য।

উদাহরণ:

```
Shop API Dev

Shop API Production
```

কারণ:

* আলাদা Client ID
* আলাদা Client Secret
* আলাদা Redirect URI
* Production Secret নিরাপদ থাকে

---

# Lesson 4 Summary

আজ আপনি শিখলেন:

* ✅ Google Cloud Project কী
* ✅ OAuth App Registration
* ✅ Client ID-এর ভূমিকা
* ✅ Client Secret-এর গুরুত্ব
* ✅ OAuth Consent Screen
* ✅ Scope কীভাবে নির্বাচন করবেন
* ✅ Redirect URI কী এবং কেন গুরুত্বপূর্ণ
* ✅ Authorized JavaScript Origin কী
* ✅ `.env`-এ Secret রাখা
* ✅ Development বনাম Production configuration

---

# Homework

উত্তর দিন:

1. Client ID public কেন হতে পারে, কিন্তু Client Secret কেন গোপন রাখতে হয়?
2. Redirect URI mismatch হলে কী হবে?
3. যদি শুধু email দরকার হয়, তাহলে কেন Google Drive scope চাওয়া উচিত নয়?
4. Authorized JavaScript Origin এবং Redirect URI-এর মধ্যে পার্থক্য কী?
5. কেন Development এবং Production-এর জন্য আলাদা Google Project ব্যবহার করা ভালো?

---

# Lesson 5 (সবচেয়ে Exciting)

এখন থেকে **Django + DRF coding** শুরু হবে।

আমরা শিখব:

* Django-তে কোন package ব্যবহার করব এবং কেন
* `django-allauth`, `dj-rest-auth`, `social-auth-app-django`—এদের পার্থক্য
* **কখন package ব্যবহার করবেন, আর কখন নিজে OAuth implement করবেন**
* Professional project-এর জন্য কোন approach সবচেয়ে ভালো

এর পরের lesson থেকেই আমরা Google OAuth-এর endpoint, callback, JWT integration এবং সম্পূর্ণ working implementation তৈরি করব।

--------
দারুণ। এখন থেকে আমরা **coding architecture**-এ ঢুকব।

অনেক beginner এখানেই ভুল করে। তারা YouTube দেখে package install করে, কিন্তু **কেন সেই package ব্যবহার করছে** তা জানে না।

একজন Senior Developer-এর প্রথম প্রশ্ন হয়:

> **"আমি কি package ব্যবহার করব, নাকি নিজে implement করব?"**

---

# Lesson 5 — Django OAuth Packages এবং Architecture

## আজকের Goal

আজ আপনি শিখবেন:

* Django ecosystem-এর OAuth packages
* কোন package কখন ব্যবহার করবেন
* Professional architecture
* কেন অনেক কোম্পানি custom OAuth লেখে

---

# Django-তে OAuth করার ৩টি প্রধান উপায়

## Option 1 — django-allauth

এটি সবচেয়ে জনপ্রিয় package।

এটি handle করে:

* Registration
* Login
* Email Verification
* Password Reset
* Social Login

Supported Providers:

* Google
* GitHub
* Facebook
* Microsoft
* Apple
* Twitter
* আরও অনেক

---

### Architecture

```text
React

↓

Django

↓

django-allauth

↓

Google
```

আপনি package configure করেন, package অনেক কাজ করে দেয়।

---

### সুবিধা

* খুব mature
* অনেক provider support
* Community বড়
* Documentation ভালো

---

### অসুবিধা

* ভিতরে অনেক abstraction
* Debug করা কঠিন হতে পারে
* Custom flow করতে গেলে জটিল লাগে

---

# Option 2 — dj-rest-auth

এটি মূলত DRF-এর জন্য।

এটি REST API দেয়।

উদাহরণ

```text
POST /login

POST /logout

POST /password/reset

POST /google/login
```

এটি প্রায়ই `django-allauth`-এর উপর নির্ভর করে।

---

Architecture

```text
React

↓

DRF API

↓

dj-rest-auth

↓

django-allauth

↓

Google
```

---

### সুবিধা

React + DRF project-এর জন্য খুব সুবিধাজনক।

---

### অসুবিধা

Flow না বুঝে ব্যবহার করলে সমস্যা হলে debug করা কঠিন।

---

# Option 3 — Custom OAuth (Pure Django)

এখানে package ব্যবহার না করে আপনি নিজেই OAuth Flow implement করেন।

Flow:

```text
React

↓

Google

↓

Authorization Code

↓

Django

↓

Google Token API

↓

User Info API

↓

JWT
```

সব HTTP request আপনি নিজেই করবেন।

---

### সুবিধা

* Flow পুরো বুঝবেন
* সম্পূর্ণ control
* যেকোনো OAuth provider integrate করতে পারবেন

---

### অসুবিধা

* শুরুতে বেশি code
* Security নিজেকেই ঠিক রাখতে হবে

---

# কোনটা কখন ব্যবহার করবেন?

## ছোট Project

```text
django-allauth

+

dj-rest-auth
```

দ্রুত development।

---

## Medium Project

```text
django-allauth

+

Custom Service Layer
```

Business logic আলাদা রাখবেন।

---

## Enterprise Project

অনেক কোম্পানি Custom OAuth implementation করে।

কারণ:

* Custom business rules
* Audit logging
* Multi-provider support
* Fine-grained control

---

# Package-এর ভিতরে কী হয়?

ধরুন

```text
POST /google/login
```

আপনি ভাবছেন magic হচ্ছে।

আসলে ভিতরে প্রায় এই কাজগুলোই হয়:

```python
Receive authorization code

↓

Exchange code

↓

Get access token

↓

Get user info

↓

Find/Create user

↓

Return JWT
```

Package শুধু এই repetitive কাজগুলো করে দেয়।

---

# Professional Project Structure

আমি OAuth logic কখনো `views.py`-তে লিখি না।

ভালো structure:

```text
apps/

    authentication/

        views.py

        serializers.py

        services.py

        providers.py

        utils.py

        urls.py
```

---

# Responsibility

## views.py

শুধু Request/Response।

```python
POST

↓

Serializer

↓

Service
```

Business logic নয়।

---

## services.py

এখানে থাকবে

```python
Exchange Code

↓

Get Token

↓

Get User Info

↓

Create User

↓

Issue JWT
```

---

## providers.py

Provider-specific logic।

```python
GoogleOAuthProvider

GithubOAuthProvider

MicrosoftOAuthProvider
```

---

# কেন Provider আলাদা?

Google-এর endpoint একরকম।

GitHub-এর endpoint আলাদা।

কিন্তু Interface একই রাখা যায়।

উদাহরণ:

```python
provider.authenticate(code)
```

Google-এর implementation ভিন্ন হবে, GitHub-এর implementation ভিন্ন হবে—কিন্তু `authenticate()` method একই ধারণা অনুসরণ করবে।

---

# Senior Design Pattern

একটি interface কল্পনা করুন:

```text
OAuthProvider

↓

GoogleProvider

GithubProvider

FacebookProvider
```

তখন View জানেই না Google নাকি GitHub ব্যবহার হচ্ছে।

সে শুধু বলে:

```text
provider.authenticate()
```

এটাকে Strategy Pattern-এর একটি ব্যবহার হিসেবে ভাবতে পারেন।

---

# Beginner Mistakes

## ❌ সব logic View-তে লেখা

```python
views.py

500 lines
```

এটা maintain করা কঠিন।

---

## ❌ Google API call Serializer-এ করা

Serializer-এর কাজ:

* Validation
* Data transformation

OAuth business logic নয়।

---

## ❌ User create করার code বিভিন্ন জায়গায় লেখা

এক জায়গায় রাখুন।

উদাহরণ:

```python
AuthenticationService
```

---

## ❌ Package-এর উপর পুরোপুরি নির্ভর করা

Package ব্যবহার করুন।

কিন্তু Flow বুঝে ব্যবহার করুন।

---

# বাস্তব Interview Question

**প্রশ্ন:**

> আপনি কেন django-allauth ব্যবহার করবেন?

ভালো উত্তর:

> "এটি বহু OAuth provider support করে এবং authentication-related common কাজগুলো সহজ করে। তবে business logic আমি service layer-এ রাখব, যাতে প্রয়োজনে package পরিবর্তন করলেও application architecture খুব বেশি বদলাতে না হয়।"

---

# আমি আপনাকে কী শেখাব?

আমরা **শুরুতে package ব্যবহার করব না।**

কারণ:

যদি আপনি আগে package শিখেন,

তাহলে শুধু configuration শিখবেন।

কিন্তু যদি আগে **OAuth Flow** নিজে implement করেন,

তাহলে পরে যে কোনো package ৩০ মিনিটেই বুঝতে পারবেন।

আমাদের শেখার ক্রম হবে:

1. ✅ Pure OAuth (নিজে implement)
2. ✅ Google OAuth
3. ✅ JWT Integration
4. ✅ GitHub OAuth
5. ✅ Multi Provider
6. ✅ তারপর django-allauth ও dj-rest-auth

এভাবে শেখার পর package আপনার কাছে "black box" মনে হবে না।

---

# Lesson 5 Summary

আজ আপনি শিখলেন:

* ✅ `django-allauth` কী
* ✅ `dj-rest-auth` কী
* ✅ Custom OAuth implementation কী
* ✅ Service Layer কেন গুরুত্বপূর্ণ
* ✅ Provider abstraction কী
* ✅ কেন View-তে business logic রাখা উচিত নয়
* ✅ কেন আগে flow শেখা, পরে package শেখা ভালো

---

# Homework

এই প্রশ্নগুলোর উত্তর নিজের ভাষায় লিখুন:

1. `django-allauth` এবং `dj-rest-auth`-এর মধ্যে সম্পর্ক কী?
2. কেন `views.py`-তে OAuth-এর পুরো logic রাখা উচিত নয়?
3. `services.py`-এর দায়িত্ব কী?
4. `providers.py` আলাদা রাখার সুবিধা কী?
5. কেন আগে Custom OAuth শেখা, পরে package শেখা ভালো?

---

## Lesson 6 Preview — প্রথম Code

এখন আমরা প্রথমবারের মতো Django + DRF-এ বাস্তব OAuth implementation শুরু করব।

আপনি শিখবেন:

* Authentication app তৈরি
* URL structure
* Google OAuth callback endpoint
* কেন frontend `code` backend-এ পাঠায়
* প্রথম working DRF endpoint তৈরি

এখান থেকেই প্রকৃত implementation শুরু হবে।

------------
চমৎকার। এখন থেকে আমরা **বাস্তব implementation** শুরু করছি।

এখান থেকে আমি আপনাকে **Senior Developer**-এর মতো শেখাব। শুধু "কোড লিখুন" না, বরং **কেন এই architecture** ব্যবহার করছি সেটাও বুঝব।

---

# Lesson 6 — প্রথম OAuth Endpoint (Authorization Code গ্রহণ করা)

## আজকের Goal

আজ আমরা শুধুমাত্র এই অংশ implement করব।

```text
React

↓

Continue with Google

↓

Google Login

↓

Google Redirect

↓

Frontend receives authorization code

↓

POST /api/v1/auth/google/

↓

Django Backend receives code
```

**আজ Google API call করব না।**

প্রথমে backend-এ code receive করার architecture তৈরি করব।

---

# Step 1 — Project Structure

আমি authentication app এভাবে organize করি।

```text
apps/
└── authentication/
    ├── serializers.py
    ├── views.py
    ├── services.py
    ├── urls.py
    ├── providers.py
    └── exceptions.py
```

### কেন?

* `views.py` → Request/Response
* `serializers.py` → Validation
* `services.py` → Business Logic
* `providers.py` → Google/GitHub specific code
* `exceptions.py` → Custom errors

এটা scalable।

---

# Step 2 — URL Design

```python
# apps/authentication/urls.py

from django.urls import path
from .views import GoogleLoginView

urlpatterns = [
    path(
        "google/",
        GoogleLoginView.as_view(),
        name="google-login",
    ),
]
```

API হবে

```text
POST /api/v1/auth/google/
```

---

# কেন `/callback/` না?

অনেক tutorial বানায়

```text
/auth/google/callback/
```

আমরা কেন করছি না?

কারণ React frontend Google থেকে `code` নিয়ে backend-এ পাঠাবে।

Flow হবে

```text
Google

↓

React

↓

POST /api/v1/auth/google/

↓

Backend
```

এতে frontend-এর উপর control বেশি থাকে।

> **নোট:** এটিই একমাত্র উপায় নয়। Backend callback URI ব্যবহার করাও খুবই প্রচলিত। আমরা এখানে SPA (React) + DRF architecture বোঝার জন্য এই flow ব্যবহার করছি।

---

# Step 3 — Serializer

Backend কী receive করবে?

মাত্র একটি জিনিস।

```json
{
    "code": "4/0AVMB..."
}
```

Serializer

```python
from rest_framework import serializers


class GoogleLoginSerializer(serializers.Serializer):
    code = serializers.CharField()
```

---

## কেন Serializer?

অনেকে করে

```python
request.data["code"]
```

এটা beginner style।

Professional way

```python
serializer.is_valid(raise_exception=True)
```

সব validation serializer করবে।

---

# Step 4 — View

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .serializers import GoogleLoginSerializer


class GoogleLoginView(APIView):

    def post(self, request):

        serializer = GoogleLoginSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        code = serializer.validated_data["code"]

        return Response(
            {
                "message": "Authorization code received.",
                "code": code,
            }
        )
```

---

# Flow

```text
POST

↓

Serializer

↓

Validation

↓

Extract code

↓

Return response
```

---

# কেন View-তে Google API call করছি না?

কারণ View-এর responsibility:

```text
Receive Request

↓

Validate

↓

Call Service

↓

Return Response
```

Google-এর সাথে কথা বলা Business Logic।

ওটা `services.py`-তে যাবে।

---

# Step 5 — Service Layer

এখন শুধু structure বানাই।

```python
# services.py

class GoogleOAuthService:

    def authenticate(self, code):
        pass
```

এখনও কিছু লিখছি না।

---

# কেন?

কারণ পরে এই method করবে

```text
Authorization Code

↓

Exchange Token

↓

Get User Info

↓

Create User

↓

Generate JWT

↓

Return Tokens
```

সব এক জায়গায় থাকবে।

---

# View এখন এমন হবে

```python
service = GoogleOAuthService()

result = service.authenticate(code)
```

আজ method empty।

আগামী lesson-এ implementation হবে।

---

# কেন Class?

অনেকে লিখে

```python
def google_login():
```

আমি prefer করি

```python
GoogleOAuthService()
```

কারণ পরে

```python
GoogleOAuthService

GithubOAuthService

MicrosoftOAuthService
```

একই pattern follow করবে।

---

# Response

আজ response হবে

```json
{
    "message": "Authorization code received.",
    "code": "4/0AX..."
}
```

এতে নিশ্চিত হব

Frontend → Backend communication ঠিক আছে।

---

# Architecture Diagram

```text
React

↓

POST

↓

GoogleLoginView

↓

GoogleLoginSerializer

↓

GoogleOAuthService

↓

Response
```

এটাই clean architecture।

---

# Beginner Mistakes

## ❌ Mistake 1

সব logic View-তে।

```python
class GoogleLoginView(APIView):

    def post():

        # 200 lines
```

না।

---

## ❌ Mistake 2

Serializer skip করা।

```python
code = request.data.get("code")
```

Validation হারিয়ে যায়।

---

## ❌ Mistake 3

Google API call View-তে।

না।

Service Layer।

---

## ❌ Mistake 4

User create View-তে।

না।

Service।

---

# Senior Thinking

একজন Senior Developer View লিখে এইভাবে ভাবেন:

```text
Request এসেছে

↓

Serializer validate করবে

↓

Service business logic করবে

↓

View শুধু response দিবে
```

এই pattern শুধু OAuth নয়, আপনার পুরো Django project-এ ব্যবহার করতে পারবেন।

---

# আজ আমরা কেন Google API call করলাম না?

কারণ implementation-কে ছোট ছোট ধাপে ভাগ করলে debugging সহজ হয়।

আজ আমরা নিশ্চিত হলাম:

* ✅ Route কাজ করছে
* ✅ Serializer কাজ করছে
* ✅ View কাজ করছে
* ✅ Code backend-এ আসছে

আগামী lesson-এ একটাই নতুন কাজ যোগ হবে:

```text
Authorization Code

↓

Google Token Endpoint

↓

Access Token
```

এভাবে প্রতিটি lesson-এ একটি করে layer যোগ করব।

---

# Lesson 6 Summary

আজ আপনি শিখলেন:

* ✅ OAuth endpoint design
* ✅ Serializer দিয়ে authorization code validate করা
* ✅ Clean View structure
* ✅ Service Layer introduce করা
* ✅ কেন View-তে business logic রাখা উচিত নয়
* ✅ React → DRF communication flow

---

# Homework

নিচের প্রশ্নগুলোর উত্তর নিজের ভাষায় লিখুন:

1. কেন `GoogleLoginSerializer` ব্যবহার করলাম?
2. কেন View-তে Google API call করিনি?
3. `GoogleOAuthService`-এর ভবিষ্যৎ দায়িত্ব কী হবে?
4. কেন Class-based Service ব্যবহার করা ভালো?
5. আজকের implementation-এ Google-এর সাথে কোনো communication হয়েছে কি? যদি না হয়ে থাকে, কেন?

---

## Lesson 7 Preview (খুব গুরুত্বপূর্ণ)

পরের lesson-এ আমরা প্রথমবার Google-এর সাথে কথা বলব।

আপনি শিখবেন:

* Authorization Code → Access Token exchange
* Google Token Endpoint
* `requests` বা `httpx` দিয়ে POST request
* Client ID ও Client Secret কোথায় ব্যবহার হয়
* Error handling (invalid code, expired code)

এখান থেকেই আপনার OAuth implementation বাস্তবে Google-এর সাথে যুক্ত হবে।

------
চমৎকার। আজকের Lesson-টা OAuth-এর সবচেয়ে গুরুত্বপূর্ণ coding lesson।

এখানেই প্রথমবার আপনার Django Backend **Google-এর সাথে যোগাযোগ করবে**।

> **Goal:** Authorization Code → Access Token Exchange

---

# Lesson 7 — Authorization Code Exchange

## আজ আমরা কোথায় আছি?

আগের lesson পর্যন্ত Flow ছিল

```text
React
    │
    ▼
POST /api/v1/auth/google/
    │
    ▼
GoogleLoginView
    │
    ▼
GoogleOAuthService.authenticate(code)
```

আজ আমরা `authenticate()` method implement করব।

---

# পুরো Flow

```text
Authorization Code

↓

Django Backend

↓

Google Token Endpoint

↓

Access Token

↓

Next Lesson → User Info
```

---

# Google Token Endpoint

Google একটি endpoint দেয়।

```
https://oauth2.googleapis.com/token
```

Backend এখানে POST request পাঠাবে।

---

## কী পাঠাতে হবে?

Google বলবে

> "তোমার authorization code দাও, আমি access token দেব।"

Request body হবে

```text
code=xxxxxxxx

client_id=xxxxxxxx

client_secret=xxxxxxxx

redirect_uri=http://localhost:8000/auth/google/callback/

grant_type=authorization_code
```

---

# প্রতিটি field বুঝি

## code

React থেকে এসেছে।

```text
4/0AXxxxx
```

---

## client_id

Google Cloud Console থেকে পাওয়া।

Public।

---

## client_secret

Google Cloud Console থেকে পাওয়া।

Secret।

শুধু Backend জানবে।

---

## redirect_uri

একদম সেই URI

যেটা Google Console-এ register করা আছে।

এক অক্ষরও আলাদা হলে

Google reject করবে।

---

## grant_type

সবসময়

```text
authorization_code
```

কারণ আমরা Authorization Code Flow ব্যবহার করছি।

---

# Service Layer

এখন `GoogleOAuthService`

```python
class GoogleOAuthService:

    def authenticate(self, code):

        # Exchange Code

        pass
```

এখানেই Google call হবে।

---

# HTTP Library

Django-তে সাধারণত দুইটা জনপ্রিয় option:

* `requests`
* `httpx`

**আমি `httpx` recommend করি**, কারণ এটি modern এবং async support করে। তবে `requests`-ও এখনও ব্যাপকভাবে ব্যবহৃত হয়।

উদাহরণ (ধারণাগত):

```python
import httpx
```

---

# POST Request

Conceptually

```python
response = httpx.post(
    TOKEN_URL,
    data={
        ...
    }
)
```

---

# Response

Google যদি successful হয়

Response

```json
{
    "access_token": "...",
    "expires_in": 3599,
    "scope": "...",
    "token_type": "Bearer",
    "id_token": "..."
}
```

আজ আমাদের দরকার

```text
access_token
```

---

# তাহলে authenticate() Flow

```text
Receive Code

↓

POST Google

↓

Receive Access Token

↓

Return Access Token
```

---

# Service Responsibility

এখন Service

```text
Input

Authorization Code

↓

Output

Access Token
```

এখনও User create করবে না।

একটা কাজ।

একটা method।

---

# কেন ছোট ছোট Step?

অনেকে লিখে

```python
authenticate()

↓

Exchange

↓

User Info

↓

Create User

↓

JWT

↓

Response
```

সব এক method।

৬০০ line।

Maintain করা কঠিন।

---

Professional way

```text
exchange_code()

↓

get_user_info()

↓

get_or_create_user()

↓

generate_tokens()
```

ছোট method।

একটা method = একটা কাজ।

এটি **Single Responsibility Principle (SRP)**-এর একটি ভালো উদাহরণ।

---

# আমার Design

আমি সাধারণত

```python
class GoogleOAuthService:

    def exchange_code(self):
        ...

    def get_user_info(self):
        ...

    def get_or_create_user(self):
        ...

    def generate_jwt(self):
        ...

    def authenticate(self):
        ...
```

`authenticate()`

শুধু orchestrate করবে।

---

# Orchestrate মানে?

```text
authenticate()

↓

exchange_code()

↓

get_user_info()

↓

get_or_create_user()

↓

generate_jwt()
```

সব step call করবে।

Business logic ভাগ করা থাকবে।

---

# Error Handling

Google সবসময় success দিবে না।

ধরুন

Code expire।

Response

```json
{
  "error": "invalid_grant"
}
```

তখন?

Exception raise করবেন।

যেমন

```text
OAuthAuthenticationError

↓

400 Bad Request
```

---

# আরেকটি Error

ভুল Client Secret

Google বলবে

```text
invalid_client
```

---

# আরেকটি

Redirect URI ভুল।

```text
redirect_uri_mismatch
```

---

# তাই Service-এর কাজ

```text
Request

↓

Google

↓

Success?

↓

Yes

↓

Return Token

──────────────

No

↓

Raise Exception
```

---

# Environment Variables

কখনো

```python
CLIENT_SECRET = "abcd"
```

না।

সবসময়

```text
.env
```

```text
GOOGLE_CLIENT_ID

GOOGLE_CLIENT_SECRET
```

তারপর

`settings.py`

সেখান থেকে পড়বেন।

---

# Architecture

```text
React

↓

Authorization Code

↓

GoogleLoginView

↓

GoogleOAuthService

↓

Google Token Endpoint

↓

Access Token

↓

Return Service
```

---

# Beginner Mistakes

## ❌ Client Secret React-এ পাঠানো

কখনো না।

---

## ❌ View-এর ভিতরে HTTP request

না।

Service Layer।

---

## ❌ Token exchange এবং User create একই method-এ

ছোট method লিখুন।

---

## ❌ Google error ignore করা

সব error handle করুন।

---

# Senior Best Practices

Service method-এর নাম এমন রাখুন যাতে পড়েই বোঝা যায় কী করছে।

ভালো:

```python
exchange_code_for_access_token()
```

অথবা

```python
exchange_code()
```

খারাপ:

```python
login()
```

কারণ `login()` নাম দেখে বোঝা যায় না ভেতরে কী হচ্ছে।

---

# আজ পর্যন্ত Complete Flow

```text
React

↓

Google Login

↓

Authorization Code

↓

Django

↓

Exchange Code

↓

Access Token
```

এখনও

* User নেই
* JWT নেই
* Database নেই

শুধু Access Token।

এটাই আজকের Goal।

---

# Lesson 7 Summary

আজ আপনি শিখলেন:

* ✅ Google Token Endpoint কী
* ✅ Authorization Code Exchange কীভাবে হয়
* ✅ কোন data Google-কে পাঠাতে হয়
* ✅ Access Token কীভাবে পাওয়া যায়
* ✅ কেন `exchange_code()` আলাদা method হওয়া উচিত
* ✅ Service orchestration ধারণা
* ✅ Error handling-এর ভিত্তি

---

# Homework

উত্তর দিন:

1. Google Token Endpoint-এর কাজ কী?
2. `grant_type=authorization_code` কেন দিতে হয়?
3. `Client Secret` কেন Backend-এ রাখতে হয়?
4. কেন `exchange_code()` method আলাদা রাখা ভালো?
5. যদি Google `invalid_grant` return করে, তাহলে আপনার Service কী করা উচিত?

---

# Lesson 8 (খুব গুরুত্বপূর্ণ)

এখন আমাদের কাছে **Access Token** আছে।

পরের lesson-এ আমরা শিখব:

* Access Token দিয়ে Google User Info API call
* Email, Name, Picture আনা
* `verified_email` কেন check করা উচিত
* কোন fields database-এ save করবেন
* Fake email এবং security considerations

> **একটি গুরুত্বপূর্ণ সংশোধন:** বাস্তব Google OAuth-এ অনেক ক্ষেত্রে `id_token` (OpenID Connect) ব্যবহার করাও একটি প্রচলিত ও নিরাপদ পদ্ধতি, বিশেষ করে user identity verify করার জন্য। আমরা প্রথমে Access Token দিয়ে flow বুঝব, তারপর পরের lessons-এ `id_token` এবং OpenID Connect-ও বিস্তারিত শিখব, যাতে আপনি modern Google Sign-In implementation-ও বুঝতে পারেন।


----------
দারুণ। আপনি এখন এমন জায়গায় এসেছেন যেখানে **OAuth শুধু "login" না, বরং user identity নিয়ে কাজ শুরু করছে।**

আজকের lesson খুবই গুরুত্বপূর্ণ, কারণ এখানেই **Google-এর user → আপনার Django User**-এ রূপান্তর হবে।

---

# Lesson 8 — Access Token দিয়ে User Information আনা

## Goal

আজ আমরা শিখব

```text
Authorization Code

↓

Access Token

↓

Google UserInfo API

↓

User Information

↓

Next Lesson → Create Django User
```

---

# এখন পর্যন্ত Flow

আমাদের Service

```text
exchange_code()

↓

Access Token
```

return করছে।

এখন প্রশ্ন—

**Access Token দিয়ে কী করব?**

---

# Access Token কী?

Access Token কোনো User Information না।

এটা শুধু একটা Permission।

ধরুন

```text
Access Token

ya29.a0AfH6SM...
```

এটা দেখে আপনি বুঝতে পারবেন না

* User কে?
* Email কী?
* Name কী?

কিছুই না।

---

# তাহলে User Information কোথায়?

Google-এর আরেকটি API আছে।

```text
Google UserInfo Endpoint
```

এখানে Access Token পাঠালে

Google User-এর profile return করবে।

---

# Flow

```text
Access Token

↓

Google UserInfo API

↓

Name

↓

Email

↓

Picture

↓

Verified Email
```

---

# Request

Conceptually

```http
GET UserInfo

Authorization:

Bearer ACCESS_TOKEN
```

খেয়াল করুন

এবার আর

```text
Client Secret
```

লাগছে না।

কারণ

Access Token-ই Permission।

---

# Response

Google সাধারণত এরকম data দেয়

```json
{
    "id": "103847593847593",
    "email": "atiar@gmail.com",
    "verified_email": true,
    "name": "Md Atiar Rahman",
    "given_name": "Md",
    "family_name": "Rahman",
    "picture": "https://...."
}
```

---

# কোন Field সবচেয়ে গুরুত্বপূর্ণ?

অনেক Beginner ভাবে

```text
Name
```

সবচেয়ে important।

না।

Senior Developer প্রথমে দেখে

```text
email
```

কারণ

আমাদের User Model

```python
email = models.EmailField(unique=True)
```

Email-ই identity।

---

# দ্বিতীয় গুরুত্বপূর্ণ Field

```text
verified_email
```

---

## verified_email কেন?

ধরুন

Google বলল

```json
{
    "email": "abc@gmail.com",
    "verified_email": false
}
```

আপনি কি Login allow করবেন?

বেশিরভাগ production system

**না।**

কারণ Email verify হয়নি।

---

# Production Rule

```python
if not verified_email:
    raise AuthenticationError()
```

এটা খুব common।

---

# picture Field

```text
https://lh3.googleusercontent...
```

এটা optional।

অনেক Project

User Avatar হিসেবে save করে।

---

# id Field

Google-এর নিজস্ব User ID।

উদাহরণ

```text
103847593847593
```

এটা

আপনার Django User ID না।

Google User ID।

---

# Service Design

এখন Service-এ নতুন method।

```python
class GoogleOAuthService:

    def exchange_code():
        ...

    def get_user_info():
        ...
```

---

# get_user_info()

Input

```text
Access Token
```

Output

```python
{
    "email": "...",
    "name": "...",
    "picture": "...",
    "verified_email": True,
}
```

খেয়াল করুন

Raw Google Response

না।

Clean Data।

---

# কেন Clean Data?

Google অনেক field পাঠায়।

আপনার দরকার

```text
Email

Name

Picture
```

শুধু।

তাই

Service normalize করবে।

---

# Normalize মানে?

Google

```json
{
    "given_name": "...",

    "family_name": "...",

    "locale": "...",

    "picture": "...",

    "hd": "...",

    "sub": "..."
}
```

↓

আপনার Application

```python
{
    "email": "...",
    "name": "...",
    "picture": "...",
}
```

---

# কেন?

কারণ

আগামীকাল

GitHub add করবেন।

GitHub Response

আলাদা।

Microsoft Response

আলাদা।

Facebook

আলাদা।

কিন্তু

Application

একই data পাবে।

---

# Provider Layer

এই জন্য

```text
Google Provider

↓

Normalize

↓

Application
```

---

# Senior Thinking

Provider-এর responsibility

```text
Google Response

↓

Application Response
```

Application যেন Google-এর format না জানে।

---

# Error Handling

যদি

Access Token expire হয়।

Google

```text
401 Unauthorized
```

দেবে।

Service

Exception raise করবে।

---

যদি

Access Token invalid হয়।

Google

```text
Invalid Token
```

দেবে।

Service

Reject করবে।

---

# Architecture

এখন পর্যন্ত

```text
React

↓

Authorization Code

↓

exchange_code()

↓

Access Token

↓

get_user_info()

↓

Clean User Data
```

---

# এখন প্রশ্ন

আমরা কি User create করলাম?

**না।**

আজ পর্যন্ত

Database touch করিনি।

---

# কেন?

কারণ

একটা Step

একটা Responsibility।

আজ শুধু

Google থেকে

User Information

আনলাম।

---

# OpenID Connect (OIDC) সম্পর্কে গুরুত্বপূর্ণ কথা

আগের lesson-এ বলেছিলাম আমরা পরে `id_token` শিখব।

এখন একটি ধারণা রাখুন:

Google OAuth-এর সাথে অনেক সময় **OpenID Connect (OIDC)** ব্যবহার করা হয়।

তখন Google একটি **`id_token`** দেয়, যেখানে user identity সম্পর্কিত signed information থাকে।

Production-এ অনেক application:

```text
Authorization Code

↓

Token Endpoint

↓

Access Token + ID Token

↓

ID Token verify

↓

User Identity
```

ব্যবহার করে।

আমরা আগে UserInfo API দিয়ে concept পরিষ্কার করছি। এরপর OIDC এবং `id_token` verification আলাদা lesson-এ বিস্তারিত শিখব।

---

# Beginner Mistakes

## ❌ Mistake 1

Access Token database-এ save করা।

সাধারণ login flow-তে সাধারণত এর দরকার হয় না।

---

## ❌ Mistake 2

Google Response সরাসরি Frontend-এ পাঠানো।

আগে normalize করুন।

---

## ❌ Mistake 3

`verified_email` ignore করা।

Production system-এ এটি গুরুত্বপূর্ণ।

---

## ❌ Mistake 4

Google User ID-কে Django Primary Key ভাবা।

দুটো সম্পূর্ণ আলাদা।

---

# Senior Best Practices

Service methods

```python
exchange_code()

↓

get_user_info()

↓

get_or_create_user()

↓

generate_tokens()
```

প্রতিটি method

একটি কাজ।

এটাই maintainable architecture।

---

# Lesson 8 Summary

আজ আপনি শিখলেন

* ✅ Access Token দিয়ে UserInfo API call করা
* ✅ UserInfo Response-এর গুরুত্বপূর্ণ fields
* ✅ `verified_email` কেন check করা উচিত
* ✅ Response normalize করা
* ✅ Google User ID বনাম Django User ID
* ✅ Provider Layer-এর দায়িত্ব
* ✅ OpenID Connect (`id_token`) সম্পর্কে প্রাথমিক ধারণা

---

# Homework

উত্তর দিন:

1. Access Token দিয়ে কী করা হয়?
2. কেন UserInfo API call করতে হয়?
3. `verified_email` কেন গুরুত্বপূর্ণ?
4. Response normalize করার সুবিধা কী?
5. Google User ID এবং Django User ID-এর মধ্যে পার্থক্য কী?

---

# Lesson 9 (সবচেয়ে গুরুত্বপূর্ণ)

এবার আমরা **Database**-এ যাব।

আপনি শিখবেন:

* `get_or_create_user()` method
* Existing User বনাম New User
* Email conflict কীভাবে handle করবেন
* Custom User Model-এর সাথে OAuth integrate করা
* শেষে JWT generate করে login সম্পূর্ণ করা

এই lesson-এর পর আপনার OAuth flow প্রথমবারের মতো **end-to-end** সম্পূর্ণ হবে।


-----
দারুণ। আজকের Lesson-এর পর আপনি বুঝতে পারবেন **Google user কীভাবে আপনার Django User-এ পরিণত হয়**।

এখানেই OAuth-এর সবচেয়ে গুরুত্বপূর্ণ business logic থাকে।

---

# Lesson 9 — get_or_create_user() (Google User → Django User)

## আজকের Goal

আজ পর্যন্ত আমাদের Flow ছিল

```text
Authorization Code

↓

Access Token

↓

Google UserInfo

↓

{
    "email": "atiar@gmail.com",
    "name": "Md Atiar Rahman",
    "picture": "..."
}
```

এখন এই data দিয়ে

**Django User** create বা login করব।

---

# প্রথম প্রশ্ন

Google বলল

```json
{
    "email": "atiar@gmail.com",
    "name": "Md Atiar Rahman"
}
```

এখন কি সবসময়

```python
User.objects.create(...)
```

করব?

❌ না।

---

# কেন?

ধরুন

আজ user প্রথমবার login করল।

```text
Google

↓

atiar@gmail.com
```

Database

```text
Empty
```

তখন

```python
User.objects.create(...)
```

ঠিক।

---

কিন্তু

আগামীকাল আবার login করল।

Database

```text
atiar@gmail.com
```

আছে।

আবার

```python
User.objects.create(...)
```

করলে?

```text
IntegrityError

Duplicate Email
```

---

# Solution

প্রথমে

User আছে কিনা দেখুন।

```text
Email

↓

Exists?

↓

Yes → Login

↓

No → Create
```

---

# Service Method

```python
class GoogleOAuthService:

    def get_or_create_user(self, user_data):
        ...
```

Input

```python
{
    "email": "...",
    "name": "...",
    "picture": "..."
}
```

Output

```python
User instance
```

---

# Step 1

Email বের করুন।

```python
email = user_data["email"]
```

---

# Step 2

User খুঁজুন।

Conceptually

```python
user = User.objects.filter(
    email=email
).first()
```

---

# যদি User থাকে

```python
return user
```

Create করার দরকার নেই।

---

# যদি User না থাকে

তখন

```python
User.objects.create(...)
```

---

# কোন Field Save করবেন?

Minimum

```python
email

full_name
```

Optional

```python
profile_picture
```

Production-এ অনেক Project

Google Picture save করে।

---

# Password কী হবে?

সবচেয়ে Common Question।

Google Login User-এর

Password থাকে?

উত্তর

**না।**

---

কারণ

User

Password

Google-কে দিয়েছে।

আপনার Django-কে না।

---

তাই

অনেক Project

```python
user.set_unusable_password()
```

ব্যবহার করে।

এর মানে

```text
Google Login Only
```

User password দিয়ে login করতে পারবে না, যতক্ষণ না আলাদাভাবে password সেট করা হয়।

---

# কেন set_unusable_password()?

ধরুন

User

Google দিয়ে account বানিয়েছে।

আপনি

Random password

```text
123456
```

দিয়ে দিলেন।

এটা বড় Security Risk।

তাই

```python
set_unusable_password()
```

ব্যবহার করা হয়।

---

# Profile Picture

Google

```text
picture
```

পাঠায়।

আপনি চাইলে

```python
profile_image
```

Field-এ save করতে পারেন।

---

# Name Update করবেন?

ধরুন

আজ

Google

```text
Md Atiar Rahman
```

আগামী বছর

User Google-এ Name change করল।

আবার Login করল।

আপনি কি Update করবেন?

Production-এ দুইটা Approach আছে।

---

## Option 1

কখনো Update করবেন না।

প্রথমবার যা এসেছে

সেটাই থাকবে।

---

## Option 2

প্রতিবার Login-এ

Sync করবেন।

```python
user.full_name = google_name
```

অনেক SaaS Project এই approach ব্যবহার করে।

---

# Email Change

ধরুন

Google Email

Change হয়েছে।

তখন?

এটা Business Rule-এর উপর নির্ভর করে।

অনেক system

Email-কে immutable identity ধরে।

অনেকে update allow করে।

---

# Transaction দরকার?

ধরুন

```python
Create User

↓

Create Profile

↓

Create Wallet

↓

Create Notification Settings
```

এখন

Wallet Create Failed।

User already create হয়ে গেছে।

Database inconsistent।

---

Solution

```python
transaction.atomic()
```

আপনি DRF নিয়ে আগেই `transaction.atomic()` শিখেছেন। এখানেও একই চিন্তা প্রযোজ্য—একাধিক database write যদি একসাথে সফল বা ব্যর্থ হওয়া দরকার হয়, তাহলে transaction ব্যবহার করবেন।

---

# Service Design

এখন পর্যন্ত

```python
authenticate()

↓

exchange_code()

↓

get_user_info()

↓

get_or_create_user()
```

---

# authenticate()

Conceptually

```python
def authenticate(code):

    token = exchange_code(code)

    user_data = get_user_info(token)

    user = get_or_create_user(user_data)

    return user
```

খেয়াল করুন

JWT এখনও নেই।

---

# Architecture

```text
Google

↓

User Info

↓

GoogleOAuthService

↓

get_or_create_user()

↓

Django User
```

---

# Custom User Model

আপনার Custom User Model যদি হয়

```python
email

full_name

avatar
```

তাহলে

Google Data

সেই অনুযায়ী map করবেন।

---

যদি User Model হয়

```python
first_name

last_name
```

তাহলে

Google

```text
given_name

family_name
```

Map করবেন।

---

# Normalize করার সুবিধা

আগের lesson-এ

আমরা

```python
{
    "email": "...",

    "name": "...",

    "picture": "..."
}
```

Return করেছিলাম।

এখন

Google Field

নিয়ে ভাবতেই হচ্ছে না।

এটাই

Provider Layer-এর লাভ।

---

# Beginner Mistakes

## ❌ Mistake 1

সবসময়

```python
User.objects.create()
```

করা।

Duplicate হবে।

---

## ❌ Mistake 2

Random Password set করা।

না।

```python
set_unusable_password()
```

---

## ❌ Mistake 3

Email Unique না রাখা।

OAuth Login-এর জন্য Email সাধারণত identity হিসেবে ব্যবহৃত হয়। (আপনার application-এর business rule ভিন্ন হলে অন্য identity-ও ব্যবহার করা যেতে পারে।)

---

## ❌ Mistake 4

Google Response

সরাসরি save করা।

আগে normalize করুন।

---

# Senior Best Practices

আমি সাধারণত

`get_or_create_user()`

শুধু User create করি।

Profile

Wallet

Settings

অন্য Service handle করে।

কারণ

একটা Method

একটা Responsibility।

---

# Complete Flow (এখন পর্যন্ত)

```text
Authorization Code

↓

Access Token

↓

Google UserInfo

↓

Normalize

↓

get_or_create_user()

↓

Django User
```

এখন শুধু

JWT বাকি।

---

# Lesson 9 Summary

আজ আপনি শিখলেন

* ✅ Existing User বনাম New User
* ✅ `get_or_create_user()` pattern
* ✅ `set_unusable_password()` কেন ব্যবহার করা হয়
* ✅ Profile picture mapping
* ✅ Name synchronization strategy
* ✅ Transaction-এর প্রয়োজনীয়তা
* ✅ Normalize data-এর সুবিধা

---

# Homework

উত্তর দিন:

1. কেন `get_or_create_user()` দরকার?
2. `set_unusable_password()` কী করে?
3. User-এর নাম প্রতিবার Google থেকে update করা উচিত কি? আপনার মতামত কী?
4. `transaction.atomic()` কখন ব্যবহার করবেন?
5. Provider থেকে normalize করা data ব্যবহার করার সুবিধা কী?

---

# একটি গুরুত্বপূর্ণ বাস্তব বিষয়

এখন পর্যন্ত আমরা Google OAuth-এর মূল flow শিখেছি। তবে আধুনিক Google Sign-In-এ **OpenID Connect (OIDC)** এবং `id_token` verification-ও গুরুত্বপূর্ণ অংশ। বাস্তব production implementation-এ আমরা সেটাও শিখব, যাতে শুধু OAuth নয়, identity verification-ও সঠিকভাবে করতে পারেন।

## Lesson 10 (End-to-End Completion)

পরের lesson-এ আমরা শিখব:

* Django User থেকে JWT তৈরি
* `Access Token` এবং `Refresh Token` issue করা
* Login response design
* Complete Google OAuth → JWT flow
* React কীভাবে token store করবে
* এরপর authenticated API call কীভাবে কাজ করবে

Lesson 10-এর পর আপনার প্রথম **সম্পূর্ণ Google OAuth Login System** ধারণাগতভাবে সম্পূর্ণ হয়ে যাবে।


দারুণ। আজকের Lesson-এর পর আমাদের প্রথম **Google OAuth → Django → JWT** flow সম্পূর্ণ হবে।

এখন পর্যন্ত আমরা শিখেছি:

```
Authorization Code
        ↓
Exchange Code
        ↓
Access Token
        ↓
Get User Info
        ↓
Get or Create User
```

আজ শেষ Step:

```
Django User

↓

JWT

↓

Frontend

↓

Authenticated API
```

---

# Lesson 10 — JWT Generate করা

## Goal

আজ আমরা শিখব

* Django User থেকে JWT generate করা
* Access Token vs Refresh Token
* Login Response Design
* React কী store করবে
* এরপর API authentication কীভাবে হবে

---

# Step 1 — Google-এর কাজ শেষ

এখন আমাদের কাছে

```python
user = User(...)
```

আছে।

Google-এর role এখানেই শেষ।

এখন Google আর দরকার নেই।

এখন Authentication করবে

**আমাদের Django Backend।**

---

# পুরো Flow

```
Google

↓

Verify User

↓

Django User

↓

SimpleJWT

↓

Access Token

↓

Refresh Token

↓

Frontend
```

---

# JWT Generate

DRF-এ সাধারণত SimpleJWT ব্যবহার করা হয়।

Conceptually

```python
refresh = RefreshToken.for_user(user)

access_token = str(refresh.access_token)

refresh_token = str(refresh)
```

এখানে

Input

```
Django User
```

Output

```
JWT Tokens
```

---

# Access Token

এটা Frontend

প্রতিটি request-এ পাঠাবে।

```
Authorization:

Bearer ACCESS_TOKEN
```

---

# Refresh Token

এটা

নতুন Access Token বানানোর জন্য।

Frontend

প্রতিটি request-এ এটা পাঠায় না।

শুধু

Access Token expire হলে।

---

# কেন দুইটা Token?

ধরুন

Access Token

```
15 মিনিট
```

valid।

Refresh Token

```
7 দিন
```

valid।

১৫ মিনিট পরে

User-কে আবার Google Login করাতে হবে?

না।

Refresh Token

নতুন Access Token বানিয়ে দেবে।

---

# Login Response

আমি সাধারণত

এভাবে Response design করি।

```json
{
    "user": {
        "id": 1,
        "email": "atiar@gmail.com",
        "full_name": "Md Atiar Rahman"
    },
    "tokens": {
        "access": "...",
        "refresh": "..."
    }
}
```

---

# কেন User Data Return করি?

React Login করার পরে

Navbar-এ দেখাবে

```
Hello Atiar
```

তাই

আবার

```
GET /me
```

call না করেও

basic information পেয়ে যায়।

---

# React কী Store করবে?

সাধারণভাবে

```
Access Token

Refresh Token
```

Store করবে।

তারপর

```
Authorization

Bearer TOKEN
```

দিয়ে API call করবে।

> **Security Note:** বাস্তব production application-এ token কোথায় store করবেন (memory, secure HttpOnly cookie ইত্যাদি) সেটা application-এর architecture ও security requirements-এর উপর নির্ভর করে। এটা আমরা পরের security lessons-এ বিস্তারিত আলোচনা করব।

---

# পরের Request

Login

```
POST

/api/auth/google/
```

↓

Response

```
Access Token
```

↓

তারপর

```
GET

/api/profile/
```

Header

```
Authorization:

Bearer ACCESS_TOKEN
```

↓

Django

```
IsAuthenticated
```

↓

User

```
request.user
```

---

# request.user কোথা থেকে আসে?

SimpleJWT

Access Token verify করে।

তারপর

```
request.user
```

set করে।

আপনার View শুধু লিখবে

```python
request.user
```

JWT Backend verify করবে।

---

# authenticate()

এখন

আমাদের Service

Conceptually

```python
def authenticate(code):

    access_token = exchange_code(code)

    user_info = get_user_info(access_token)

    user = get_or_create_user(user_info)

    tokens = generate_tokens(user)

    return {
        "user": user,
        "tokens": tokens
    }
```

এটাই Complete Flow।

---

# Architecture

```
React

↓

Google

↓

Authorization Code

↓

GoogleOAuthService

↓

exchange_code()

↓

get_user_info()

↓

get_or_create_user()

↓

generate_tokens()

↓

Response
```

---

# View এখন কী করবে?

View-এর কাজ

```
Receive Request

↓

Serializer

↓

Service.authenticate()

↓

Return Response
```

এতটুকুই।

---

# Service-এর Responsibility

Service

```
OAuth Flow

↓

Business Logic

↓

User

↓

JWT
```

View

Business Logic জানে না।

---

# Access Token Expire হলে?

Flow

```
Access Token

↓

Expired

↓

Frontend

↓

POST /refresh/

↓

Refresh Token

↓

New Access Token
```

User বুঝতেও পারবে না।

---

# Logout

Google Logout?

না।

আপনার JWT invalidate করবেন।

Google Account Logout আলাদা বিষয়।

অনেক application

Google থেকে logout-ই করে না।

শুধু

নিজের JWT revoke/blacklist করে (যদি blacklist ব্যবহার করা হয়) বা client-side token remove করে।

---

# Beginner Mistakes

## ❌ Google Access Token Frontend-এ ব্যবহার করা

না।

Frontend

আপনার

JWT ব্যবহার করবে।

Google Token

না।

---

## ❌ Google User ID

JWT-তে রাখা

প্রয়োজন নেই।

Django User

ব্যবহার করুন।

---

## ❌ প্রতিটি Request-এ Google API call

না।

একবার Login।

তারপর

JWT।

---

## ❌ প্রতি Request-এ UserInfo API call

না।

Login-এর সময়

একবার।

---

# Senior Best Practices

আমি OAuth Login-এর পরে

Google Access Token

Database-এ save করি না।

যদি

Google Drive

Calendar

Gmail API

Use না করি।

কারণ

আমার দরকার

শুধু Identity।

Google Identity পেলেই

JWT যথেষ্ট।

> যদি আপনার application পরে Google API (যেমন Calendar, Drive, Gmail) ব্যবহার করে, তখন Google Access Token (এবং প্রয়োজনে Refresh Token) নিরাপদভাবে সংরক্ষণ করার প্রয়োজন হতে পারে।

---

# End-to-End Flow

```
React

↓

Google Login

↓

Authorization Code

↓

Backend

↓

Exchange Code

↓

Access Token

↓

UserInfo

↓

User

↓

JWT

↓

React

↓

Authenticated APIs
```

এটাই Modern Django + DRF OAuth Login-এর মূল ধারণা।

---

# Production Architecture

```
authentication/

    views.py

    serializers.py

    services.py

    providers.py

    exceptions.py

    urls.py
```

Business Logic

সব

Service-এ।

---

# Lesson 10 Summary

আজ আপনি শিখলেন

* ✅ JWT generate করা
* ✅ Access Token vs Refresh Token
* ✅ Login response design
* ✅ React কী ব্যবহার করবে
* ✅ `request.user` কীভাবে আসে
* ✅ OAuth → JWT → Authenticated API Flow
* ✅ Google-এর role কোথায় শেষ হয়

---

# Homework

উত্তর দিন:

1. Google Login-এর পরে কেন JWT generate করি?
2. Access Token এবং Refresh Token-এর পার্থক্য কী?
3. Frontend কেন Google Access Token-এর বদলে Django JWT ব্যবহার করবে?
4. `request.user` কীভাবে populate হয়?
5. কোন পরিস্থিতিতে Google Access Token সংরক্ষণ করা দরকার হতে পারে?

---

# 🎉 প্রথম Milestone Complete

Lesson 1–10 শেষে আপনি বুঝেছেন:

* OAuth কী
* Authorization Code Flow
* Google OAuth-এর architecture
* Service Layer design
* User creation
* JWT integration

এখনও কিছু **গুরুত্বপূর্ণ advanced topic** বাকি আছে, যেগুলো একজন Senior Django Developer-এর জন্য খুব দরকার।

## Lesson 11 থেকে আমরা শিখব

* বাস্তব Google OAuth implementation (`httpx` দিয়ে actual requests)
* OpenID Connect (OIDC)
* `id_token` verification (signature, audience, issuer)
* PKCE
* Security best practices
* Multiple providers (Google, GitHub, Microsoft)
* Reusable OAuth architecture
* Testing এবং debugging

এই অংশগুলো শেখার পর আপনি বাস্তবে production-ready OAuth system confidently implement করতে পারবেন।

-------
চমৎকার। এখন থেকে আমরা **Advanced OAuth**-এ প্রবেশ করছি।

**Lesson 1–10**-এ আমরা OAuth-এর architecture শিখেছি। কিন্তু একটি গুরুত্বপূর্ণ বিষয় আমরা ইচ্ছা করে সরল করেছি।

> **বাস্তব Google Login-এ শুধু Access Token-এর উপর নির্ভর করা সবসময় যথেষ্ট নয়।**

এখন আমরা Production Level implementation শিখব।

---

# Lesson 11 — OpenID Connect (OIDC) এবং ID Token

## Goal

আজ আপনি শিখবেন

* OAuth vs OpenID Connect (OIDC)
* `id_token` কী
* Access Token এবং ID Token-এর পার্থক্য
* কেন আধুনিক Google Sign-In-এ OIDC ব্যবহার করা হয়

---

# OAuth কি Login-এর জন্য তৈরি হয়েছিল?

এটা অনেকেরই ভুল ধারণা।

আসলে OAuth তৈরি হয়েছিল

```text
Permission দেওয়ার জন্য।
```

উদাহরণ

```text
Google Drive

↓

My App

↓

Permission
```

OAuth-এর মূল উদ্দেশ্য ছিল **authorization**।

---

# তাহলে Login কোথা থেকে এল?

Google, Microsoft ইত্যাদি পরে **OpenID Connect (OIDC)** যোগ করে।

OIDC =

```text
OAuth

+

Identity Layer
```

এখন Google শুধু permission দেয় না,

সে user-এর identity-ও securely জানায়।

---

# OAuth vs OpenID Connect

| OAuth           | OpenID Connect          |
| --------------- | ----------------------- |
| Permission      | Identity + Permission   |
| Access Token    | Access Token + ID Token |
| Resource Access | User Authentication     |

---

# ID Token কী?

Google Token Endpoint থেকে অনেক সময় response হয়

```json
{
    "access_token": "...",
    "id_token": "...",
    "expires_in": 3599
}
```

এখানে

```text
id_token
```

সবচেয়ে গুরুত্বপূর্ণ।

---

# ID Token-এর ভিতরে কী থাকে?

এটা সাধারণ text না।

এটা একটি **JWT**।

Conceptually

```text
Header

↓

Payload

↓

Signature
```

---

# Payload

Conceptually

```json
{
  "sub": "103847593847593",
  "email": "atiar@gmail.com",
  "email_verified": true,
  "name": "Md Atiar Rahman",
  "picture": "...",
  "aud": "YOUR_CLIENT_ID",
  "iss": "https://accounts.google.com"
}
```

খেয়াল করুন

Google নিজেই User Information দিয়েছে।

---

# তাহলে UserInfo API লাগবে না?

এটা নির্ভর করে।

অনেক Application

```text
ID Token

↓

Verify

↓

Extract User Info
```

এটাই করে।

আবার অনেক Application

```text
Access Token

↓

UserInfo API
```

call করে।

দুই approach-ই ব্যবহার হয়।

---

# তাহলে কোনটা ভালো?

Production-এ

**Google Identity verify করার জন্য**

ID Token verify করা খুব common এবং recommended।

কারণ

Google Token-এ

Signature থাকে।

---

# কেন Verify করতে হবে?

ধরুন

কেউ নিজে একটা JWT বানাল।

```text
email = admin@gmail.com
```

আপনি verify না করেই trust করলেন।

বড় Security Problem।

তাই

ID Token verify করতে হয়।

---

# Verify করার সময় কী কী check করবেন?

কমপক্ষে

## 1. Signature

Google সত্যিই token issue করেছে?

---

## 2. Audience (`aud`)

Token কি

**আপনার Client ID**-এর জন্য issue হয়েছে?

যদি

```text
aud = another_app_client_id
```

তাহলে reject।

---

## 3. Issuer (`iss`)

Issuer

Google কি?

Expected

```text
accounts.google.com
```

অথবা

```text
https://accounts.google.com
```

---

## 4. Expiration (`exp`)

Token expire হয়েছে?

---

## 5. Email Verified

```json
{
  "email_verified": true
}
```

---

# Access Token vs ID Token

| Access Token            | ID Token                   |
| ----------------------- | -------------------------- |
| Google API access       | User identity              |
| Resource Server-এর জন্য | Client Application-এর জন্য |
| Opaque বা JWT হতে পারে  | JWT                        |
| UserInfo API call       | User authenticate          |

---

# Production Flow

```text
React

↓

Google Login

↓

Authorization Code

↓

Backend

↓

Token Endpoint

↓

Access Token

+

ID Token

↓

Verify ID Token

↓

Extract User

↓

Create/Login User

↓

JWT
```

---

# Django Service Design

আগে

```python
authenticate()
```

এখন

Conceptually

```text
exchange_code()

↓

verify_id_token()

↓

extract_user()

↓

get_or_create_user()

↓

generate_tokens()
```

দেখুন,

**UserInfo API**-এর জায়গায়

অনেক ক্ষেত্রে

`verify_id_token()`

এসে গেছে।

---

# Beginner Mistakes

## ❌ ID Token decode করেই trust করা

JWT decode করা আর verify করা এক জিনিস নয়।

---

## ❌ Signature verify না করা

Production-এ বড় Security Risk।

---

## ❌ Audience check না করা

Token অন্য App-এরও হতে পারে।

---

## ❌ Expiration check না করা

Expired token accept করা যাবে না।

---

# Senior Best Practices

একজন Senior Developer সবসময় নিজেকে প্রশ্ন করে:

> "আমি কীভাবে নিশ্চিত হব যে এই identity সত্যিই Google issue করেছে?"

উত্তর:

* Signature verify
* Audience verify
* Issuer verify
* Expiration verify

তারপরই User create/login।

---

# Lesson 11 Summary

আজ আপনি শিখলেন:

* ✅ OAuth এবং OpenID Connect-এর পার্থক্য
* ✅ `id_token` কী
* ✅ Access Token বনাম ID Token
* ✅ কেন ID Token verify করতে হয়
* ✅ কোন claims (`aud`, `iss`, `exp`, `email_verified`) গুরুত্বপূর্ণ
* ✅ Modern Google Sign-In flow

---

# Homework

উত্তর দিন:

1. OAuth এবং OpenID Connect-এর মধ্যে পার্থক্য কী?
2. `id_token`-এর প্রধান উদ্দেশ্য কী?
3. কেন শুধু JWT decode করলেই হবে না?
4. `aud` claim কেন verify করতে হয়?
5. Access Token এবং ID Token-এর কাজ আলাদা কেন?

---

## 🔥 এরপর কী?

এখন আপনার সামনে দুটি পথ আছে:

1. **Lesson 12: Production Code** — Django + DRF-এ `httpx`, Google token exchange, `google-auth` library দিয়ে `id_token` verification-এর বাস্তব code।
2. **Lesson 12: PKCE** — Public client (React, Mobile)-এর জন্য Authorization Code Flow with PKCE, যা আধুনিক OAuth-এর অত্যন্ত গুরুত্বপূর্ণ security feature।

আমি **Production Code** আগে শেখানোর পর PKCE শেখাব। এতে আপনি আগে একটি সম্পূর্ণ working implementation বুঝবেন, তারপর সেটাকে আরও নিরাপদ করবেন।

-------------
চমৎকার। এখন থেকে আমরা **Production Code** লিখব।

এখন পর্যন্ত আমরা concept শিখেছি। এবার এমন code লিখব যা বাস্তব project-এ ব্যবহার করা যায়।

> **Goal:** Google OAuth-এর Production Service Layer তৈরি করা।

---

# Lesson 12 — Production Implementation (Google OAuth Service)

## আজকের Architecture

```text
React
    │
    ▼
POST /api/v1/auth/google/
    │
    ▼
GoogleLoginView
    │
    ▼
GoogleOAuthService.authenticate()
    │
    ├──────────────► exchange_code()
    │
    ├──────────────► verify_id_token()
    │
    ├──────────────► get_or_create_user()
    │
    └──────────────► generate_tokens()
```

এখন এই structure implement করব।

---

# Step 1 — Required Packages

দুইটি package ব্যবহার করব।

```bash
pip install httpx
pip install google-auth
```

কেন?

### httpx

Google API-তে HTTP request পাঠানোর জন্য।

### google-auth

Google-এর `id_token` verify করার জন্য।

---

# Step 2 — Settings

```python
GOOGLE_CLIENT_ID = env("GOOGLE_CLIENT_ID")
GOOGLE_CLIENT_SECRET = env("GOOGLE_CLIENT_SECRET")
GOOGLE_REDIRECT_URI = env("GOOGLE_REDIRECT_URI")
```

`.env`

```text
GOOGLE_CLIENT_ID=xxxxxxxx

GOOGLE_CLIENT_SECRET=xxxxxxxx

GOOGLE_REDIRECT_URI=http://localhost:8000/auth/google/callback/
```

---

# Step 3 — Service Structure

```python
class GoogleOAuthService:

    TOKEN_URL = "https://oauth2.googleapis.com/token"

    def authenticate(self, code):
        pass

    def exchange_code(self, code):
        pass

    def verify_id_token(self, id_token):
        pass

    def get_or_create_user(self, user_data):
        pass

    def generate_tokens(self, user):
        pass
```

খেয়াল করুন।

প্রতিটি method

একটি কাজ করছে।

---

# Step 4 — exchange_code()

এখানেই Google-এর Token API call হবে।

Conceptually

```python
response = httpx.post(
    TOKEN_URL,
    data={
        "code": code,
        "client_id": settings.GOOGLE_CLIENT_ID,
        "client_secret": settings.GOOGLE_CLIENT_SECRET,
        "redirect_uri": settings.GOOGLE_REDIRECT_URI,
        "grant_type": "authorization_code",
    },
)
```

---

Google Success হলে

```json
{
    "access_token": "...",
    "id_token": "...",
    "expires_in": 3599
}
```

Return করবে।

---

# Production Check

Success ধরে নিবেন না।

সবসময়

```python
if response.status_code != 200:
    ...
```

check করবেন।

---

# Response Parsing

```python
data = response.json()
```

তারপর

```python
id_token = data["id_token"]
```

---

# Step 5 — verify_id_token()

এটাই সবচেয়ে গুরুত্বপূর্ণ।

Conceptually

```python
from google.oauth2 import id_token

from google.auth.transport import requests
```

তারপর

```python
id_info = id_token.verify_oauth2_token(...)
```

এখানে

Google

* Signature verify করবে
* Audience verify করবে
* Expiration verify করবে

---

তারপর

আমরা

```python
email = id_info["email"]
```

পাব।

---

# Step 6 — verified_email

Production-এ

```python
if not id_info["email_verified"]:
    raise AuthenticationError()
```

---

# Step 7 — Normalize

আমি কখনো

Google Response

Application-এ পাঠাই না।

বরং

```python
return {
    "email": ...,
    "name": ...,
    "picture": ...
}
```

---

# Step 8 — get_or_create_user()

এটা আমরা আগের lesson-এ design করেছি।

এখন

verify করা

User data

ব্যবহার করবে।

---

# Step 9 — generate_tokens()

SimpleJWT

```python
RefreshToken.for_user(user)
```

↓

Return

```python
{
    "access": "...",
    "refresh": "..."
}
```

---

# authenticate()

এটাই orchestration method।

Conceptually

```python
def authenticate(code):

    token_data = exchange_code(code)

    user_data = verify_id_token(
        token_data["id_token"]
    )

    user = get_or_create_user(user_data)

    tokens = generate_tokens(user)

    return {
        "user": user,
        "tokens": tokens
    }
```

দেখুন।

Method-এর ভিতরে

Business Logic নেই।

শুধু

Step Call করছে।

---

# View

View

এখনও

Simple।

```python
serializer

↓

service.authenticate()

↓

Response
```

এটাই Professional Django।

---

# Error Handling

আমি সাধারণত

Google Error

সরাসরি Frontend-এ পাঠাই না।

বরং

নিজের Exception।

যেমন

```python
OAuthAuthenticationError
```

---

তারপর

Global Exception Handler

↓

Response

```json
{
    "detail": "Google authentication failed."
}
```

---

# Logging

Production-এ

```python
logger.exception(...)
```

করবেন।

কিন্তু

কখনো

```python
Client Secret
```

Log করবেন না।

---

# Retry?

Google Server

৫০০ Error দিল।

Retry?

কিছু ক্ষেত্রে করা যায়।

কিন্তু

```text
invalid_grant
```

Retry করে লাভ নেই।

Error type বুঝে সিদ্ধান্ত নিতে হবে।

---

# Final Architecture

```text
GoogleLoginView

↓

GoogleOAuthService

↓

exchange_code()

↓

verify_id_token()

↓

normalize()

↓

get_or_create_user()

↓

generate_tokens()

↓

Response
```

---

# Production Folder

```text
authentication/

    views.py

    serializers.py

    services.py

    providers.py

    exceptions.py

    selectors.py

    urls.py
```

খেয়াল করেছেন?

আমি

এখন

`selectors.py`

যোগ করেছি।

---

# কেন selectors.py?

ধরুন

```python
User.objects.filter(...)
```

অনেক জায়গায় লাগছে।

তখন

```python
get_user_by_email()
```

selector

বানাতে পারেন।

এতে query logic এক জায়গায় থাকে।

---

# Beginner Mistakes

## ❌ Google Response

সরাসরি Database-এ save।

আগে normalize করুন।

---

## ❌ View-তে

Token Exchange।

না।

---

## ❌ Exception ignore করা।

Google Fail

↓

Return 500

এটা ভালো UX নয়।

---

## ❌ Settings

Hardcode করা।

সব

`.env`

---

# Senior Best Practices

আমি OAuth Service

Test করি

Google ছাড়া।

কিভাবে?

`exchange_code()`

Mock করি।

তাহলে

Business Logic

Unit Test করা সহজ হয়।

এটাই Testable Architecture।

---

# Lesson 12 Summary

আজ আপনি শিখলেন:

* ✅ Production Service Structure
* ✅ `httpx` দিয়ে Token Exchange
* ✅ `google-auth` দিয়ে `id_token` verification
* ✅ Normalize response
* ✅ Exception Handling
* ✅ Logging
* ✅ `selectors.py` ব্যবহার করার ধারণা
* ✅ Testable Service Design

---

# এখন পর্যন্ত আপনি যা শিখেছেন

আপনি এখন conceptually একটি production-ready Google OAuth system design করতে পারেন।

কিন্তু এখনও ৩টি বড় বিষয় বাকি:

1. **PKCE (Proof Key for Code Exchange)** — আধুনিক React, SPA এবং Mobile App-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
2. **Multi Provider Architecture** — একই codebase-এ Google, GitHub, Microsoft, Facebook।
3. **Testing & Security** — Mocking, Integration Test, Rate Limiting, Replay Attack, Secret Rotation।

## Lesson 13

আমরা **PKCE** শিখব।

এটি OAuth-এর সবচেয়ে গুরুত্বপূর্ণ security feature-গুলোর একটি, এবং আধুনিক SPA ও Mobile application-এ Authorization Code Flow-এর সাথে প্রায় সবসময় ব্যবহার করা হয়।

------
দারুণ। আমরা Lesson 14 করে ফেলেছিলাম, এখন ধারাবাহিকতার জন্য **Lesson 13 (PKCE)** বিস্তারিতভাবে করি। এটি এমন একটি বিষয় যা অনেক Django Developer জানেন না, কিন্তু Production OAuth-এ এটি অত্যন্ত গুরুত্বপূর্ণ।

---

# Lesson 13 — PKCE (Proof Key for Code Exchange)

## Goal

এই lesson শেষে আপনি বুঝবেন:

* PKCE কেন দরকার
* এটি কোন attack প্রতিরোধ করে
* React + Django + Google OAuth-এ এটি কীভাবে কাজ করে
* Django Backend-এর কী responsibility
* Google কীভাবে PKCE verify করে

---

# প্রথমে Problem বুঝি

আগের Flow ছিল

```text
React

↓

Google Login

↓

Authorization Code

↓

Django

↓

Access Token
```

ধরুন একজন attacker কোনোভাবে

```text
Authorization Code
```

চুরি করে ফেলল।

যদি শুধু Code থাকলেই Token পাওয়া যেত,

তাহলে attacker-ও Google থেকে Access Token নিয়ে নিতে পারত।

এটাই PKCE solve করে।

---

# PKCE কী?

PKCE = **Proof Key for Code Exchange**

সহজ ভাষায়

Google বলে—

> "Code আছে, ঠিক আছে। কিন্তু প্রমাণ করো যে Code যিনি request করেছিলেন, Token-ও তিনিই চাইছেন।"

এই proof-এর জন্য দুটি জিনিস ব্যবহার হয়।

```text
Code Verifier

↓

Code Challenge
```

---

# Code Verifier

এটি একটি

High Random String।

উদাহরণ

```text
X9eLk8K8mPq2zWQ...
```

এটি Secret।

Frontend এটি নিজের কাছে রাখে।

---

# Code Challenge

Code Verifier থেকে

SHA-256 hash করা হয়।

```text
Code Verifier

↓

SHA256

↓

Base64URL Encode

↓

Code Challenge
```

এটি আর Secret নয়।

এটি Google-কে পাঠানো হয়।

---

# Login Flow

React

প্রথমে

```text
Random Verifier

↓

Challenge তৈরি
```

তারপর

Google-কে পাঠায়

```text
challenge
```

Google

Challenge Save করে।

---

# User Login

User Login Complete করলে

Google

Authorization Code দেয়।

---

# Backend

Backend

Authorization Code দিয়ে

Token চাইবে।

কিন্তু এবার

আরও একটি Field পাঠাবে।

```text
code_verifier
```

---

# Google কী করবে?

Google

নিজেই

```text
Verifier

↓

SHA256

↓

Challenge
```

বানাবে।

তারপর compare করবে

```text
Saved Challenge

==

New Challenge ?
```

যদি Match করে

Token দিবে।

---

# যদি Attacker Code চুরি করে?

তার কাছে

Authorization Code আছে।

কিন্তু

Verifier নেই।

Google

Reject করবে।

---

# Flow Diagram

```text
React

↓

Generate Verifier

↓

Generate Challenge

↓

Google Login

↓

Google stores Challenge

↓

Authorization Code

↓

Backend sends

Code + Verifier

↓

Google verifies

↓

Access Token
```

---

# Django-এর Role

একটি গুরুত্বপূর্ণ বিষয়।

অনেকে ভাবে

"Django PKCE generate করবে।"

সবসময় না।

SPA (React)-এ সাধারণত

React

```text
Verifier

↓

Challenge
```

generate করে।

Django শুধু

Token Exchange-এর সময়

Verifier পাঠায়।

---

# Mobile App

Android

iOS

React Native

Flutter

সবখানেই

PKCE ব্যবহার করা হয়।

---

# কেন Client Secret যথেষ্ট না?

ধরুন

React App

Client Secret রাখল।

User

Browser থেকে দেখে ফেলতে পারবে।

তাই

SPA-তে

Client Secret Secret থাকে না।

PKCE

এই Problem solve করে।

---

# OAuth Flow Without PKCE

```text
Code

↓

Token
```

---

# OAuth Flow With PKCE

```text
Code

+

Verifier

↓

Token
```

---

# Google কী Save করে?

Google

Verifier Save করে না।

শুধু

Challenge।

কারণ

Challenge থেকে

Verifier বের করা যায় না।

---

# SHA256 কেন?

কারণ

One-way Hash।

```text
Verifier

↓

Hash

↓

Challenge
```

Reverse করা সম্ভব নয়।

---

# Production Flow

```text
React

↓

Verifier

↓

Challenge

↓

Google

↓

Authorization Code

↓

Django

↓

Verifier

↓

Google

↓

Access Token
```

---

# Service Layer

আগে

```text
exchange_code(code)
```

এখন

Conceptually

```text
exchange_code(

code,

code_verifier

)
```

দুইটি Input।

---

# React কী পাঠাবে?

```json
{
    "code": "...",
    "code_verifier": "..."
}
```

---

# Django Serializer

আগে

```python
code
```

ছিল।

এখন

Conceptually

```python
code

code_verifier
```

দুটো Validate করবে।

---

# Google Token Request

আগে

```text
code

client_id

client_secret
```

এখন

আরও

```text
code_verifier
```

যোগ হবে।

> **নোট:** Public client (SPA, Mobile)-এর ক্ষেত্রে PKCE-এর সাথে অনেক সময় `client_secret` ব্যবহার করা হয় না। আবার আপনার architecture যদি Backend (confidential client) দিয়ে token exchange করে, তাহলে Google configuration অনুযায়ী `client_secret` থাকতে পারে। এটি OAuth client type-এর উপর নির্ভর করে।

---

# Beginner Mistakes

## ❌ PKCE মানে Encryption

না।

এটি Encryption নয়।

এটি Proof Mechanism।

---

## ❌ Challenge Save করা

Backend-এ দরকার নেই।

Google Handle করে।

---

## ❌ Verifier Hardcode করা

প্রতিটি Login-এর জন্য

নতুন Random Verifier।

---

## ❌ SHA256 Skip করা

Google

Plain Verifier

Challenge হিসেবে Accept করবে না (S256 method ব্যবহারই বর্তমানে standard)।

---

# Senior Best Practices

Production SPA-তে

```text
Authorization Code Flow

+

PKCE
```

এটাই Standard।

Implicit Flow

আজকাল নতুন Project-এ ব্যবহার করা হয় না।

---

# Architecture

```text
React

↓

Generate Verifier

↓

Generate Challenge

↓

Google Login

↓

Authorization Code

↓

Django

↓

Exchange Code + Verifier

↓

Google

↓

Access Token

↓

ID Token

↓

JWT
```

---

# Lesson 13 Summary

আজ আপনি শিখলেন:

* ✅ PKCE কী
* ✅ Code Verifier
* ✅ Code Challenge
* ✅ SHA256-এর ভূমিকা
* ✅ PKCE কোন attack প্রতিরোধ করে
* ✅ React ও Django-এর আলাদা responsibility
* ✅ কেন PKCE আধুনিক OAuth-এর standard

---

# Homework

উত্তর দিন:

1. PKCE কেন দরকার?
2. Code Verifier এবং Code Challenge-এর মধ্যে পার্থক্য কী?
3. Google কেন Verifier-এর বদলে Challenge store করে?
4. PKCE কোন ধরনের attack প্রতিরোধ করে?
5. React + Django architecture-এ Verifier কে generate করে এবং Token Exchange-এর সময় কে Google-কে পাঠায়?

---

## এরপর কী?

এখন OAuth roadmap-এর সবচেয়ে গুরুত্বপূর্ণ conceptগুলো আপনি শিখে ফেলেছেন।

পরবর্তী advanced module-এ আমরা শিখব:

* **Lesson 15:** Production-grade Testing (Unit Test, Integration Test, Mocking `httpx`, OAuth flow testing)
* Security hardening (CSRF, state parameter, replay attack prevention)
* Account linking (একই email দিয়ে Google + GitHub login)
* Refresh token rotation
* Enterprise authentication architecture

এই module শেষ হলে আপনি বাস্তবে যেকোনো Django + DRF project-এ OAuth confidently implement করতে পারবেন।


---------
চমৎকার। এখন আমরা এমন একটি বিষয় শিখব যা **Senior Backend Developer**-দের OAuth implementation-এ সবচেয়ে বেশি কাজে লাগে।

এখন পর্যন্ত আমরা শুধুমাত্র **Google OAuth** করেছি।

কিন্তু বাস্তবে Project-এ requirement আসে:

* Continue with Google
* Continue with GitHub
* Continue with Microsoft
* Continue with Facebook
* Continue with Apple

আপনি কি প্রতিটি Provider-এর জন্য আলাদা ৫০০ লাইনের Service লিখবেন?

**না।**

এখানেই Software Design Pattern কাজে আসে।

---

# Lesson 14 — Multi Provider OAuth Architecture

## Goal

আজ শিখবেন

* একই Architecture-তে Multiple OAuth Provider support করা
* Strategy Pattern
* Provider Interface
* Factory Pattern
* Reusable Design

---

# Beginner Architecture ❌

অনেকে এভাবে শুরু করে

```text
GoogleLoginView

↓

GoogleService



GithubLoginView

↓

GithubService



FacebookLoginView

↓

FacebookService
```

প্রথমে ভালো লাগে।

৬ মাস পরে

```text
Google

Github

Facebook

Microsoft

Apple

LinkedIn
```

সবগুলোর code duplicate হতে শুরু করে।

---

# Senior Architecture

একটা Common Interface

```text
OAuthProvider

↓

GoogleProvider

GithubProvider

MicrosoftProvider

FacebookProvider
```

সব Provider

একই Method implement করবে।

---

# OAuthProvider Interface

Conceptually

```python
class OAuthProvider:

    def authenticate(self, code):
        raise NotImplementedError
```

এখানে

Google Provider

```python
class GoogleProvider(OAuthProvider):
    ...
```

GitHub Provider

```python
class GithubProvider(OAuthProvider):
    ...
```

---

# কেন Interface?

কারণ View জানবে না

Google নাকি GitHub।

সে শুধু জানবে

```python
provider.authenticate(code)
```

এটাই Abstraction।

---

# Google Provider

Conceptually

```text
exchange_code()

↓

verify_identity()

↓

normalize()

↓

return user_data
```

---

# GitHub Provider

Conceptually

```text
exchange_code()

↓

get_user()

↓

normalize()

↓

return user_data
```

---

# খেয়াল করুন

Google

UserInfo

একভাবে দেয়।

GitHub

আরেকভাবে।

কিন্তু

Application

সবসময় একই data পায়।

```python
{
    "email": "...",
    "name": "...",
    "avatar": "..."
}
```

---

# Normalize কেন এত গুরুত্বপূর্ণ?

Google Response

```json
{
    "picture": "...",
    "name": "..."
}
```

GitHub

```json
{
    "avatar_url": "...",
    "login": "...",
    "name": "..."
}
```

Microsoft

```json
{
    "displayName": "...",
    "mail": "..."
}
```

Application কি এগুলো জানবে?

না।

সব Provider

একই Format return করবে।

```python
{
    "email": "...",
    "name": "...",
    "avatar": "..."
}
```

---

# Factory Pattern

এখন প্রশ্ন

কোন Provider create হবে?

আমি সাধারণত

Factory ব্যবহার করি।

Conceptually

```text
Provider Name

↓

Factory

↓

GoogleProvider
```

অথবা

```text
github

↓

Factory

↓

GithubProvider
```

---

# Factory-এর কাজ

Input

```text
google
```

Output

```text
GoogleProvider()
```

---

Input

```text
github
```

Output

```text
GithubProvider()
```

---

# Flow

```text
React

↓

provider=google

↓

Factory

↓

GoogleProvider

↓

authenticate()
```

---

আর

```text
provider=github

↓

Factory

↓

GithubProvider

↓

authenticate()
```

---

# View এখন

Google-specific হবে?

না।

একটাই View

Conceptually

```text
POST

/api/auth/{provider}/
```

উদাহরণ

```text
/api/auth/google/

/api/auth/github/

/api/auth/microsoft/
```

সব

একই View।

---

# Service

একটাই

```text
OAuthAuthenticationService
```

---

Flow

```text
Factory

↓

Provider

↓

User Data

↓

get_or_create_user()

↓

JWT
```

---

# Folder Structure

```text
authentication/

    providers/

        base.py

        google.py

        github.py

        microsoft.py

        facebook.py

    factory.py

    services.py

    views.py
```

এটা Enterprise Project-এ খুব common।

---

# Responsibility

## Google Provider

Google API জানে।

---

## GitHub Provider

GitHub API জানে।

---

## Authentication Service

User Create জানে।

JWT জানে।

---

## View

Request জানে।

---

দেখুন

সব Responsibility আলাদা।

---

# Senior Thinking

আমি সবসময় প্রশ্ন করি

> আগামী বছরে যদি Apple Login add করতে হয়?

যদি উত্তর হয়

> ২০টা File modify করতে হবে।

তাহলে Design ভালো না।

ভালো Design হলে

শুধু

```text
AppleProvider
```

add করবেন।

বাকি Code পরিবর্তন করতে হবে না।

এটাই **Open/Closed Principle**:

* **Open for extension** (নতুন provider যোগ করা সহজ)
* **Closed for modification** (পুরনো code কম পরিবর্তন করতে হবে)

---

# Error Handling

সব Provider

নিজস্ব Error

দেবে।

Google

```text
invalid_grant
```

GitHub

```text
bad_verification_code
```

কিন্তু

Application

একটাই Exception পাবে।

```text
OAuthAuthenticationError
```

এটাও Normalize করা।

---

# Testing

Google Provider

Mock

↓

Test

GitHub Provider

Mock

↓

Test

Authentication Service

আলাদা Test

সব Independent।

---

# Beginner Mistakes

## ❌ Google Logic Service-এ Hardcode করা

তাহলে GitHub add করা কঠিন হবে।

---

## ❌ Response Normalize না করা

Application

Provider-specific হয়ে যাবে।

---

## ❌ প্রতিটি Provider-এর জন্য আলাদা View

Code duplication হবে।

---

## ❌ সব Provider-এর Logic একই File-এ

Maintain করা কঠিন।

---

# Professional Architecture

```text
                OAuthAuthenticationService
                           │
                           ▼
                     Provider Factory
          ┌────────────┼────────────┐
          ▼            ▼            ▼
   GoogleProvider GithubProvider MicrosoftProvider
          │            │            │
          └────────────┼────────────┘
                       ▼
             Normalized User Data
                       ▼
              get_or_create_user()
                       ▼
                  Generate JWT
```

---

# Lesson 14 Summary

আজ আপনি শিখলেন:

* ✅ Multi Provider Architecture
* ✅ Provider Interface
* ✅ Strategy Pattern-এর ব্যবহার
* ✅ Factory Pattern-এর ব্যবহার
* ✅ Response Normalization
* ✅ Open/Closed Principle
* ✅ Enterprise Folder Structure
* ✅ Scalable OAuth Design

---

# Homework

উত্তর দিন:


-------
অভিনন্দন! 🎉

আজ **OAuth Mastery Module**-এর শেষ lesson। এই lesson-এর পর আপনি শুধু OAuth implement করাই নয়, **production-quality OAuth code** লিখতে পারবেন।

---

# Lesson 15 — Testing, Security & Production Best Practices

## Goal

আজ শিখবেন

* OAuth Testing
* Mocking Google API
* Security Checklist
* State Parameter
* Account Linking
* Refresh Token Rotation
* Production Checklist

---

# Part 1 — OAuth Testing

## Beginner Mistake

অনেকে OAuth test করে এভাবে:

```text
Run Server

↓

Google Login

↓

Manually Click

↓

Works
```

এটা Testing না।

এটা Manual Verification।

---

## Professional Testing

Production-এ ৩ ধরনের Test থাকে।

```text
Unit Test

↓

Integration Test

↓

End-to-End Test
```

---

# Unit Test

শুধু Service Test করবেন।

Google-কে Call করবেন না।

```text
exchange_code()

↓

Mock Response
```

---

উদাহরণ

```text
Google

↓

{
    "id_token": "fake-token"
}
```

Return করিয়ে

Business Logic Test করুন।

---

# কেন Mock?

কারণ

```text
Google Server Down
```

হলেও

আপনার Test Fail হওয়া উচিত না।

---

# Part 2 — Integration Test

এখানে

Google Mock Server

বা Test Double ব্যবহার করা যায়।

Flow Test করবেন।

```text
Serializer

↓

Service

↓

JWT
```

---

# Part 3 — End-to-End Test

এটাই আসল Login।

```text
Browser

↓

Google

↓

Backend

↓

JWT
```

সব কিছু Real।

---

# Mock কোথায় করবেন?

সবচেয়ে Common

```text
httpx.post()
```

Mock করবেন।

যাতে

Google-এর বদলে

নিজের Fake Response আসে।

---

# Security Checklist

Production-এ

সবসময় Check করবেন।

---

## 1. State Parameter

এটা আমরা আগে বিস্তারিত করিনি।

আজ শিখি।

---

User

Google Login শুরু করল।

Backend

একটা Random String বানায়।

```text
state

↓

XKJ829AJK92
```

Google-কে পাঠায়।

---

Google

Login শেষে

একই

```text
state
```

ফিরিয়ে দেয়।

---

Backend

Compare করে।

```text
Sent State

==

Received State
```

Match?

Login Continue।

---

কেন?

CSRF Protection।

---

# 2. Nonce

OIDC-এ

আরও একটি Field আছে।

```text
nonce
```

এটি

Replay Attack কমাতে সাহায্য করে।

বিশেষ করে `id_token` validate করার সময়।

---

# 3. HTTPS

Production-এ

কখনো

```text
http://
```

না।

সবসময়

```text
https://
```

---

# 4. Secret

কখনো

```python
CLIENT_SECRET="abc"
```

Hardcode করবেন না।

সব

`.env`

---

# 5. Logging

Log করুন

```text
User Login Success
```

Log করবেন না

```text
Access Token

Refresh Token

Client Secret
```

---

# 6. Rate Limiting

ধরুন

একজন

১০০০০ বার

OAuth Endpoint

Hit করছে।

Rate Limit করুন।

---

# 7. Exception Message

Google বলল

```text
invalid_client
```

Frontend-এ

সরাসরি পাঠাবেন?

না।

Return করুন

```text
Authentication Failed
```

Detailed Error

শুধু Log।

---

# Account Linking

ধরুন

User

আগে

Email Password

দিয়ে Account করেছে।

আজ

Google Login করল।

Email একই।

কি করবেন?

---

Professional Rule

```text
Same Email

↓

Same User
```

নতুন User না।

---

# Multi Provider

```text
atiar@gmail.com

↓

Google Login

↓

User #10
```

পরে

```text
atiar@gmail.com

↓

GitHub Login

↓

User #10
```

একই User।

---

# Refresh Token Rotation

SimpleJWT

Default

Refresh Token

একই থাকতে পারে।

Production Security

Rotate করুন।

```text
Old Refresh Token

↓

New Refresh Token
```

চুরি হয়ে গেলে Risk কমে।

---

# Logout

Production Logout

```text
Blacklist Refresh Token
```

তারপর

Access Token

Expire হবে।

---

# Folder Structure

```text
authentication/

    providers/

    services/

    selectors/

    exceptions/

    tests/

        test_google.py

        test_service.py

        test_views.py

        test_tokens.py
```

Testing আলাদা Folder।

---

# CI/CD

Production-এ

Deploy-এর আগে

```text
pytest
```

Run হবে।

সব Pass?

তাহলে Deploy।

---

# Monitoring

Google OAuth Fail করলে

Alert আসবে।

Sentry

বা অন্য Monitoring Tool

ব্যবহার করতে পারেন।

---

# Production Checklist

✅ HTTPS

✅ PKCE

✅ State Parameter

✅ Verify ID Token

✅ Verify Audience

✅ Verify Issuer

✅ Verify Expiration

✅ Email Verified

✅ Normalize Response

✅ get_or_create_user()

✅ JWT

✅ Logging

✅ Rate Limiting

✅ Tests

---

# Complete OAuth Architecture

```text
React

↓

Generate PKCE

↓

Google Login

↓

Authorization Code

↓

Django View

↓

Serializer

↓

OAuth Service

↓

Exchange Code

↓

Verify ID Token

↓

Normalize User

↓

Get/Create User

↓

Generate JWT

↓

Frontend

↓

Authenticated APIs
```

---

# Senior Thinking

একজন Senior Developer OAuth implement করার সময় শুধু ভাবেন না:

> "Login হচ্ছে?"

তিনি আরও ভাবেন:

* যদি Google API Fail করে?
* যদি Token Expire হয়?
* যদি User একই Email দিয়ে অন্য Provider ব্যবহার করে?
* যদি কেউ Authorization Code চুরি করে?
* যদি ১০,০০০ Request আসে?
* যদি Google-এর Response Format পরিবর্তন হয়?
* যদি Tests Fail করে?

এটাই Senior Mindset।

---

# Beginner vs Senior

| Beginner        | Senior                                    |
| --------------- | ----------------------------------------- |
| Login হলেই খুশি | Security, Scalability, Testing চিন্তা করে |
| সব Code View-তে | Service + Provider + Factory              |
| Manual Test     | Automated Test                            |
| Hardcode        | Environment Variables                     |
| Google Only     | Multi Provider Ready                      |

---

# 🎓 OAuth Mastery Complete

আপনি এখন শিখেছেন:

### Foundation

* ✅ OAuth Basics
* ✅ Authorization Code Flow
* ✅ Access Token
* ✅ Refresh Token

### Google OAuth

* ✅ Token Exchange
* ✅ UserInfo
* ✅ ID Token
* ✅ OIDC

### Django Architecture

* ✅ Service Layer
* ✅ Provider Layer
* ✅ Factory Pattern
* ✅ Selectors

### Security

* ✅ PKCE
* ✅ State Parameter
* ✅ Nonce
* ✅ HTTPS
* ✅ Token Verification

### Production

* ✅ Testing
* ✅ Logging
* ✅ Error Handling
* ✅ Multi Provider
* ✅ JWT
* ✅ Account Linking

---

# একটি গুরুত্বপূর্ণ বাস্তবতা

এই ১৫টি lesson আপনাকে **OAuth-এর architecture, flow এবং production design** শিখিয়েছে।

কিন্তু **Mastery** তখনই হবে যখন আপনি নিজে অন্তত ২–৩ বার OAuth implement করবেন।

আমি আপনাকে এই Practice Projectগুলো করার পরামর্শ দিচ্ছি:

### Project 1 (Easy)

* Google Login
* SimpleJWT
* Custom User

### Project 2 (Intermediate)

* Google + GitHub Login
* Common Provider Architecture
* Account Linking

### Project 3 (Advanced)

* Multi-tenant SaaS
* Google + Microsoft + GitHub
* PKCE
* Refresh Token Rotation
* Comprehensive Test Suite
* Rate Limiting
* Audit Logs

এই তিনটি project শেষ করতে পারলে আপনি শুধু OAuth "জানবেন" না, **যেকোনো Django + DRF project-এ confidently implement করতে পারবেন।**

----------
