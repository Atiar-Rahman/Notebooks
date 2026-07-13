Git commit message লেখার skill আসলে **English জানার বিষয় না**, এটা হলো **কী change করলাম সেটা এক লাইনে চিন্তা করার skill**।

Senior developerরা commit লেখার আগে এই ৩টা প্রশ্ন করে:

```
1. আমি কী করেছি?
2. কেন করেছি?
3. এটা কোন category এর change?
```

তারপর message বানায়।

---

## 1. Commit message এর basic structure

সবচেয়ে common format:

```
<type>(scope): <short description>
```

Example:

```
feat(auth): add google oauth login
```

ভাঙলে:

```
feat        → কী ধরনের change
(auth)      → কোন part এ change
add google oauth login → কী করেছি
```

---

# Step 1: Change type চিন্তা করুন

## 1. Feature add করলে

নতুন কিছু যোগ করলে:

```
feat
```

Example:

তুমি GitHub OAuth add করলে:

❌ Bad:

```
github done
```

❌ Bad:

```
update code
```

✅ Good:

```
feat(oauth): add github oauth provider
```

কারণ:

```
feat = নতুন feature
oauth = কোন module
add github oauth provider = কী add করেছ
```

---

## 2. Bug fix করলে

Use:

```
fix
```

Example:

Problem:

```
JWT refresh token কাজ করছিল না
```

Commit:

```
fix(auth): handle expired refresh token
```

---

## 3. Code improve/refactor করলে

Use:

```
refactor
```

মানে functionality change হয়নি, শুধু code better হয়েছে।

Example:

আগে:

```
GoogleLoginView
GithubLoginView
FacebookLoginView
```

তিনটা আলাদা ছিল।

তুমি করলা:

```
OAuthCallbackView
```

Commit:

```
refactor(oauth): create generic oauth callback handler
```

---

## 4. Documentation change

Use:

```
docs
```

Example:

README update:

```
docs(readme): add authentication setup guide
```

---

## 5. Testing add করলে

Use:

```
test
```

Example:

```
test(auth): add oauth login test cases
```

---

## 6. Configuration change

Use:

```
chore
```

Example:

package install:

```
chore(deps): add django-allauth dependency
```

---

# Step 2: Scope কী হবে?

Scope মানে:

"কোন area পরিবর্তন করেছি?"

Example:

তোমার Django project:

```
apps
 |
 |-- authentication
 |-- users
 |-- products
 |-- orders
 |-- payments
```

তাহলে:

Authentication:

```
feat(auth): add email verification
```

Product:

```
feat(product): add product filtering
```

Order:

```
fix(order): prevent duplicate order creation
```

---

# Step 3: Description কেমন হবে?

Rule:

### Verb দিয়ে শুরু করবেন

Good:

```
add
create
update
remove
fix
handle
implement
refactor
```

---

Bad:

```
changes
updates
code update
work done
finished
```

কারণ এগুলো বলে না কী হয়েছে।

---

# Real project examples

## User registration

Change:

```
Custom user model তৈরি করেছি
```

Commit:

```
feat(users): create custom user model
```

---

## JWT Authentication

Change:

```
JWT login add করেছি
```

Commit:

```
feat(auth): implement jwt authentication
```

---

## Serializer validation

Change:

```
password match validation add করেছি
```

Commit:

```
feat(auth): add password validation
```

---

## Database migration

Change:

```
new fields add
```

Commit:

```
feat(users): add profile fields
```

---

## API optimization

Change:

```
select_related ব্যবহার করেছি
```

Commit:

```
perf(api): optimize product queries
```

---

# Beginnerরা যে ভুল করে

## Mistake 1

```
git commit -m "done"
```

Problem:

৬ মাস পরে দেখলে বুঝবে না।

---

## Mistake 2

```
git commit -m "update files"
```

কোন files? কী update?

---

## Mistake 3

এক commit এ অনেক কাজ:

```
feat: add login, fix product, update css
```

Wrong.

কারণ commit এর purpose একটাই হওয়া উচিত।

---

# Professional workflow

ধরো তুমি OAuth project করছো:

### Commit 1

Custom User Model:

```
feat(users): create custom user model
```

---

### Commit 2

Base model:

```
feat(core): add reusable base model
```

---

### Commit 3

JWT:

```
feat(auth): implement jwt authentication
```

---

### Commit 4

Google provider:

```
feat(oauth): add google oauth provider
```

---

### Commit 5

Google callback:

```
feat(oauth): handle google oauth callback
```

---

### Commit 6

Error handling:

```
fix(oauth): handle oauth provider errors
```

---

# তোমার জন্য একটা চিন্তার framework

কাজ শেষ করার পর নিজেকে জিজ্ঞেস করো:

```
আমি নতুন কিছু বানিয়েছি?
        |
        yes
        |
       feat


আগের কিছু broken ছিল?
        |
        yes
        |
       fix


শুধু code clean করেছি?
        |
        yes
        |
       refactor


শুধু dependency/config?
        |
        yes
        |
       chore
```

---

তুমি যেহেতু Django + DRF বড় project build করছো, এই style follow করলে GitHub repository অনেক বেশি **senior developer level** দেখাবে। OAuth guide-এও এই ধরনের commit sequence রাখা হয়েছে, যেমন `feat(oauth): add github oauth provider`। 

পরের level এ শেখা উচিত: **"একটা বড় feature কে কীভাবে 5-10টা meaningful commit এ ভাগ করতে হয়"** — এটা senior developerদের খুব গুরুত্বপূর্ণ skill।

