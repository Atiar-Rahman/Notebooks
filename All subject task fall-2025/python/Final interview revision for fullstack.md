
### What is the difference between HTML and CSS
HTML (Hyper Text  markup language ) is used to structure content on a web page, such as headings, paragraphs, and images
CSS (Cascading Style Sheets) is used to style and design that structure, such as colors, spacing and layout.

for example, HTML creates a button, CSS controls its color and size.

#### What is the box model in CSS
the CSS box model describes how elements are structured. it consists of 
- content
- padding
- border
- margin

Every element on a web page is treated as a rectangular box with these four parts.

#### what is the difference between `Flexbox and Grid`

Flex-box is mainly used for one dimensional layouts (row or columns) Grid is used for two dimensional layouts (rows and columns)

Flex-box is ideal for aligning items in a `Navbar.`
Grid is better for building complex page layouts.

#### what is the difference between var, let, const in JavaScript
- `Var` is function scoped and can e `redeclared.`
- `let` is block scoped and can not be reassigned.
- `const`  is block scoped and cannot be reassigned

in modern JavaScript, let and const preferred

#### what is the `DOM`
`DOM` (Document Object Model) is a programming interface for html documents.
it allows `Javascript` to access and modify HTML elements dynamically
for example, changing text when a button is clicked.


#### what is an event in JavaScript
An event is an action that occurs in the browser, such as clicking a button or submitting a form. JavaScript can listen for events and executes functions in response.

#### what is asynchronous JavaScript?
Asynchronous JavaScript allows code to run without blocking other operations. it is used when working APIs, timers, or file loading. promises and `async/wait` are used to handle asynchronous operations.


#### what is an API
API (Application Programming Interface) allows communication between different software systems

for example, a fronted application calling a `backend` endpoint to fetch user data.

#### what is `JSON`
`JSON` (JavaScript Object Notation) is a high weight data format used to exchange data between client and server.

it is easy to read and widely used in REST APIs

#### what is `CORS`
`CORS` (`Cors Origins Resource Sharing`) is security mechanism that controls which domains can access resources from a server.
it prevents unauthorized `corss-origin request`


## `Backend (Django/Rest/Server)
#### What is REST
REST (Representational state transfer) is an architectural style for building APIs.
it uses HTTP methods like:
- GET (retrieve)
- POST (create)
- PUT (update)
- `DETELE (delete)`

#### difference between GET and POST
GET retrieves data and does not modify it.
post sends data to the server and creates new resources
GET data appears in the URL, POST data is sent in the request body.

#### what is `django ORM`
Django `ORM` (Object Relational Mapping) allows developers to interact with databases using Python code instead of raw SQL

It converts Python models into database tables

#### what is `Middleware` in  Django
`Middleware `is a layer that processes requests and responses globally.
for example
- Authentication
- logging
- Security checks

#### what is authentication vs authorization
Authentication verifies who the user is. Authorization determines what the user is allowed to do

#### what is `JWT`
`JWT `(`JSON` web token) is a secure way to transmit authentication data between client and server
it is commonly used in REST APIs for stateless authentication

#### what is `MVC`
`MVC` Stands for 
- models (data)
- View(`UI`)
- Controller(Logic)
Django follows a similar pattern called `MVT`(Model view template)


#### what is hashing
Hashing converts data into a fixed length encrypted value. Passwords are stored using hashing for security.


#### what is 404 error
404 means the requested resource was not found the server

#### What is a 500 error
500 is an internal server error. it indicates something went wrong on the `backend`

## Database
#### what is a Primary Key.
A primary key uniquely identifies each record in a table. it can not be null and must be unique

#### what is foreign Key
a foreign key links one table to another table. it creates relationships between tables

#### what is normalization
Normalization is organizing data to redundancy and improve consistency

#### difference between MySQL and PostgreSQL
Both are relational databases. PostgreSQL is more advanced and supports complex queries and `JSON`.  MySQL is widely used and slightly easier to set up.

#### What is indexing
Indexing improves query performance by allowing faster data retrieval.


## Problem solving logic

#### what is time complexity
Time complexity measures how an algorithm's performance changes as input size increases.

for example
- O(1) constant
- O(n) linear
- O(n^2) quadratic
#### What is the difference between  == and === in JavaScript

-  == compares values only
-  ===  compares both value and type.
using === is recommended


#### what is promise
A promise represents  a value that may be available now, later or never.

it has 
- Pending
- Fulfilled
- Rejected states

#### what happens when you type a URL is the browser
Structured
- `DNS` resolves domain name to IP address
- Browser sends HTTP request
- Server Processes request
- server sends response
- Browser renders HTML, CSS, `JS`

#### How would you secure a web application
- Use `HTTPS`
- Hash passwords
- Validate input
- Use authentication & authorization
- Protect against SQL injection and `XSS`
- configure `CORS` properly

##  Reverse String
Write a function to reverse  a string.


```js

function reverseString(str){
	return str.split('').reverse().join('')
}

console.log(reverseString('hellow'))

```
Explain:
- split('') converts string to array
- reverse() reverse array
- join('') converts back to string
## Check Even or Odd
Write a function to check if a number is even or odd.

```js
function isEven(num){
	if (num%2===0){
		return "even"
	}
	return 'odd'
}

console.log(isEven(23)) // odd
```


## find largest Number in array
Return the largest number from an array

```js
function findLargest(arr){
	return Math.max(...arr)
}

console.log(findLargest([1,2,4,6,4,2]))
```

alternative without build in

```js
function findLargest(arr){
	let largest = arr[0]
	for(let i=1;i<arr.length;i++){
		if(largest<arr[i]){
			largest=arr[i]
		}
	}
	return largest;
}

console.log(findLargest([1,5,4,3,6,8]))

```

## count vowels in a string
Count how many vowels are a string
```js
function countVowels(str){
	let count=0;
	let vowels = 'aeiouAEIOU';
	
	for(let char of str){
		if(vowels.includes(char)){
			count++;
		}
	}
	return count;
}

console.log(countVowels('hello world))
```


## Remove Duplicate values from an array

```js
function removeDuplicates(arr){
	return [...new Set(arr)];
}

console.log(removeDuplicates([1,2,3,2,2,2,4,55,5,5])
```


## Simple API fetch Example

```js
async function fetchData(){
	try{
		const response = await fetch('')
		const data = await response.json();
		console.log(data)
		
	}catch(error){
		console.error('ERROR', error)
	}
}

fetchData()
```

Explanation
- await waits for response
- `.json()` converts response
- try/catch handles errors

## palindrome check
check if a string is a Palindrome.

```js
function isPalndrome(str){
	let reversed = str.split('').reverse().json('')
	return str===reversed;
}

console.log(isPalindrome('madam'))
```



# 1️⃣ Prevent Duplicate User Registration

### 🧠 Scenario:

Users are being registered multiple times with the same email.

### ✅ Solution:

- Add `unique=True` in model
    
- Validate in serializer
    

```python
class CustomUser(models.Model):
    email = models.EmailField(unique=True)
```

In serializer:

```python
def validate_email(self, value):
    if CustomUser.objects.filter(email=value).exists():
        raise serializers.ValidationError("Email already exists.")
    return value
```

🎯 Why: Database-level + application-level validation ensures safety.

---

# 2️⃣ Handle High Traffic on API Endpoint

### 🧠 Scenario:

Your API becomes slow when too many users request data.

### ✅ Solution:

- Add caching
    
- Optimize queries
    
- Add indexing
    

Example using Django cache:

```python
from django.core.cache import cache

def get_posts(request):
    data = cache.get("posts")
    if not data:
        posts = Post.objects.all()
        data = PostSerializer(posts, many=True).data
        cache.set("posts", data, timeout=60)
    return Response(data)
```

🎯 Why: Reduces database load.

---

# 3️⃣ Avoid N+1 Query Problem

### 🧠 Scenario:

You fetch posts and their authors, but it causes too many queries.

### ✅ Solution:

Use `select_related()` or `prefetch_related()`.

```python
posts = Post.objects.select_related('author').all()
```

🎯 Why: Fetches related data in a single query.

---

# 4️⃣ Implement Role-Based Access Control

### 🧠 Scenario:

Only admin users should delete posts.

### ✅ Solution:

Check permissions.

```python
@api_view(['DELETE'])
def delete_post(request, pk):
    if not request.user.is_staff:
        return Response({"error": "Unauthorized"}, status=403)
    
    post = get_object_or_404(Post, pk=pk)
    post.delete()
    return Response({"message": "Deleted"})
```

🎯 Why: Protects sensitive actions.

---

# 5️⃣ Prevent SQL Injection

### 🧠 Scenario:

User input is used in query filtering.

### ❌ Bad:

```python
cursor.execute(f"SELECT * FROM users WHERE name = '{name}'")
```

### ✅ Good:

```python
User.objects.filter(name=name)
```

🎯 Why: ORM automatically escapes inputs.

---

# 6️⃣ File Upload with Size Validation

### 🧠 Scenario:

Users upload profile pictures, but some files are too large.

### ✅ Solution:

```python
def validate_profile_picture(self, value):
    if value.size > 2 * 1024 * 1024:
        raise serializers.ValidationError("File too large (max 2MB).")
    return value
```

🎯 Why: Prevents server overload.

---

# 7️⃣ Implement JWT Authentication (Concept)

### 🧠 Scenario:

You need stateless authentication for mobile app.

### ✅ Approach:

- Install simplejwt
    
- Add token authentication
    
- Protect endpoints
    

Protected view:

```python
from rest_framework.permissions import IsAuthenticated

@api_view(['GET'])
@permission_classes([IsAuthenticated])
def secure_data(request):
    return Response({"message": "Secure access"})
```

🎯 Why: JWT removes need for server-side sessions.

---

# 8️⃣ Handle Database Transaction Safely

### 🧠 Scenario:

User payment and order creation must both succeed or fail together.

### ✅ Solution:

```python
from django.db import transaction

@api_view(['POST'])
def create_order(request):
    with transaction.atomic():
        payment = Payment.objects.create(...)
        order = Order.objects.create(payment=payment, ...)
    return Response({"message": "Order created"})
```

🎯 Why: Prevents partial database updates.

---

# 9️⃣ Implement Rate Limiting

### 🧠 Scenario:

Users are spamming login API.

### ✅ Solution (DRF setting):

```python
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.UserRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'user': '5/minute'
    }
}
```

🎯 Why: Prevents brute force attacks.

---

# 🔟 Optimize Slow Query

### 🧠 Scenario:

Filtering by `created_at` is slow.

### ✅ Solution:

Add database index.

```python
created_at = models.DateTimeField(auto_now_add=True, db_index=True)
```

🎯 Why: Index improves search performance.

---

# 🧠 What Interviewers Want in These Questions

They are testing:

✔ Security awareness  
✔ Performance optimization  
✔ Database understanding  
✔ Clean architecture thinking  
✔ Real-world scalability

---

# 🚀 Since This Is YOU

You already:

- Built multi-user systems
    
- Used Django REST
    
- Handled datasets
    
- Built large ML pipelines
    

These advanced questions are completely in your level.

---

If you want next, I can give you:

- 🔥 10 System Design mini-scenarios (very powerful for hiring)
    
- ⚡ 10 debugging-style backend problems
    
- 🎯 10 tricky Django interview traps
    
- ⏱ Full 45-minute advanced backend mock test
    

Which one do you want? 💪











