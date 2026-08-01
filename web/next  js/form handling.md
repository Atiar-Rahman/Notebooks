Since you're already comfortable with **React + Django REST Framework**, the most practical way to learn **Next.js form handling** is in this order:

> **HTML Form → React State → React Hook Form (RHF) → Zod Validation → API Call → Loading/Error Handling → Reusable Form Components**

I'll teach it like a production course.

---

# Lesson 1: The Complete Flow

```
User
  │
  ▼
Input Fields
  │
  ▼
React Hook Form
(register, handleSubmit)
  │
  ▼
Zod Validation
  │
  ▼
If Valid
  │
  ▼
API Call (fetch/axios)
  │
  ▼
Backend (DRF)
  │
  ▼
Success / Error
  │
  ▼
Toast + Redirect
```

Think like this

```
User Input

↓

Collect Data (RHF)

↓

Validate (Zod)

↓

Send API

↓

Receive Response

↓

Show Message
```

---

# Lesson 2: Why React Hook Form?

Without RHF

```jsx
const [email, setEmail] = useState("")
const [password, setPassword] = useState("")
```

Every input needs

```
value
onChange
state
```

For 20 fields

```
20 states

20 onChange

Huge code
```

RHF manages all of that automatically.

---

# Lesson 3: Install

```
npm install react-hook-form

npm install zod

npm install @hookform/resolvers
```

If using axios

```
npm install axios
```

---

# Folder Structure

```
app/

login/
    page.tsx

components/
    LoginForm.tsx

lib/
    api.ts

schemas/
    loginSchema.ts

types/
    auth.ts
```

---

# Lesson 4: Login Schema (Zod)

```
schemas/loginSchema.ts
```

```ts
import { z } from "zod"

export const loginSchema = z.object({
    email: z
        .string()
        .email("Invalid email"),

    password: z
        .string()
        .min(6, "Minimum 6 characters")
})

export type LoginType = z.infer<typeof loginSchema>
```

Why?

```
One file

↓

Validation Rule

↓

TypeScript Type

↓

Reusable
```

---

# Lesson 5: Create Form

```tsx
"use client"

import { useForm } from "react-hook-form"

export default function LoginForm(){

const {register,handleSubmit}=useForm()

return(

<form>

<input {...register("email")} />

<input {...register("password")} />

</form>

)

}
```

What register does?

```
register("email")

↓

Create State

↓

Track Changes

↓

Collect Data

↓

Validate
```

No useState required.

---

# Lesson 6: Add Zod

```tsx
import { zodResolver } from "@hookform/resolvers/zod"

import { loginSchema, LoginType } from "@/schemas/loginSchema"

const {

register,

handleSubmit,

formState:{errors}

}=useForm<LoginType>({

resolver:zodResolver(loginSchema)

})
```

Now validation is automatic.

---

# Lesson 7: Show Errors

```tsx
<input

type="email"

{...register("email")}

/>

<p>{errors.email?.message}</p>
```

Password

```tsx
<input

type="password"

{...register("password")}

/>

<p>{errors.password?.message}</p>
```

If

```
abc
```

Then

```
Invalid email
```

appears automatically.

---

# Lesson 8: Submit Form

```tsx
const onSubmit = (data: LoginType) => {

console.log(data)

}
```

Then

```tsx
<form onSubmit={handleSubmit(onSubmit)}>

...
</form>
```

Flow

```
Click Submit

↓

Zod Validation

↓

Success

↓

onSubmit()

↓

data received
```

---

# Lesson 9: API Layer

Create

```
lib/api.ts
```

```ts
import axios from "axios"

export const api = axios.create({

baseURL:"http://localhost:8000/api"

})
```

Now

```
api.post()

api.get()

api.patch()

api.delete()
```

No repeated URL.

---

# Lesson 10: Login API

```tsx
const onSubmit = async (data: LoginType) => {

try{

const response = await api.post(

"/login/",

data

)

console.log(response.data)

}

catch(error){

console.log(error)

}

}
```

Flow

```
Form

↓

JSON

↓

Axios

↓

Django

↓

Response

↓

Console
```

---

# Lesson 11: Loading State

```tsx
const {

register,

handleSubmit,

formState:{isSubmitting}

}=useForm<LoginType>()
```

Button

```tsx
<button disabled={isSubmitting}>

{

isSubmitting

?

"Loading..."

:

"Login"

}

</button>
```

No extra loading state needed.

---

# Lesson 12: Complete Login Component

```tsx
"use client"

import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import { loginSchema, LoginType } from "@/schemas/loginSchema"
import { api } from "@/lib/api"

export default function LoginForm() {

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting }
  } = useForm<LoginType>({
    resolver: zodResolver(loginSchema),
  })

  const onSubmit = async (data: LoginType) => {
    try {
      const res = await api.post("/login/", data)

      console.log(res.data)

    } catch (err) {
      console.error(err)
    }
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>

      <input
        type="email"
        placeholder="Email"
        {...register("email")}
      />

      <p>{errors.email?.message}</p>

      <input
        type="password"
        placeholder="Password"
        {...register("password")}
      />

      <p>{errors.password?.message}</p>

      <button disabled={isSubmitting}>
        {isSubmitting ? "Loading..." : "Login"}
      </button>

    </form>
  )
}
```

---

# Lesson 13: How Django Receives the Data

The submitted JSON looks like:

```json
{
    "email":"john@gmail.com",
    "password":"123456"
}
```

Your DRF view can access it as:

```python
class LoginView(APIView):
    def post(self, request):
        print(request.data)
```

Output:

```python
{
    "email":"john@gmail.com",
    "password":"123456"
}
```

---

# Lesson 14: Production Flow

```
User Input
        │
        ▼
React Hook Form
        │
        ▼
Zod Validation
        │
        ▼
API Service (Axios)
        │
        ▼
JWT Login API (DRF)
        │
        ▼
Access Token + Refresh Token
        │
        ▼
Store Token (HTTP-only cookie or another secure strategy)
        │
        ▼
Redirect
```

---

# Lesson 15: Common RHF APIs

|Method|Purpose|Example|
|---|---|---|
|`register()`|Connect an input to the form|`register("email")`|
|`handleSubmit()`|Validate and submit|`handleSubmit(onSubmit)`|
|`watch()`|Read field values live|`watch("email")`|
|`setValue()`|Update a field programmatically|`setValue("name", "Atiar")`|
|`getValues()`|Get current values|`getValues()`|
|`reset()`|Reset the form|`reset()`|
|`trigger()`|Validate manually|`trigger("email")`|
|`setError()`|Set server-side errors|`setError("email", { type: "server", message: "Email already exists" })`|
|`clearErrors()`|Remove validation errors|`clearErrors("email")`|

---

# Production Best Practices

For a Next.js + Django REST Framework application, a common structure is:

```
src/
├── app/
│   ├── login/
│   ├── register/
│   └── profile/
├── components/
│   ├── forms/
│   │   ├── LoginForm.tsx
│   │   ├── RegisterForm.tsx
│   │   └── UserForm.tsx
│   └── ui/
├── schemas/
│   ├── auth.ts
│   ├── user.ts
│   └── product.ts
├── lib/
│   ├── api.ts
│   └── auth.ts
├── services/
│   ├── authService.ts
│   └── userService.ts
└── types/
```

This separation keeps validation, API logic, UI, and business logic independent and easier to maintain.

## What's next?

After mastering basic RHF + Zod + API integration, the next topics to learn are:

1. Default values and editing forms (`defaultValues`, `reset`)
    
2. Server-side error handling with `setError`
    
3. Dynamic forms using `useFieldArray`
    
4. File uploads (`multipart/form-data`)
    
5. Multi-step forms
    
6. Integration with authentication (JWT, cookies, protected routes)
    
7. Optimistic UI updates and data synchronization with libraries like TanStack Query
    

These are the patterns you'll encounter in production-grade Next.js applications.

Great. Now let's move to **Part 2: Production-Level Form Handling**. Since you already know the basics, this lesson focuses on patterns you'll use in real Next.js applications.

---

# Lesson 16: `defaultValues`

Suppose you're editing a user profile.

Without `defaultValues`, the form starts empty.

```tsx
const {
  register,
} = useForm()
```

Instead:

```tsx
const {
  register,
} = useForm({
  defaultValues: {
    firstName: "Atiar",
    email: "atiar@gmail.com"
  }
})
```

Result:

```
Input
↓

Automatically Filled
```

---

# Dynamic Default Values

Usually, data comes from an API.

```tsx
const {
    register,
    reset
} = useForm<UserForm>()
```

Fetch user data:

```tsx
useEffect(() => {
    async function getUser() {
        const res = await api.get("/profile/")

        reset(res.data)
    }

    getUser()
}, [reset])
```

Why `reset()`?

Because `defaultValues` only works on the first render.

```
Component Mount

↓

defaultValues

↓

Later API Response

↓

reset()

↓

Update Form
```

---

# Lesson 17: `watch()`

Sometimes you need live values.

Example:

```tsx
const {
    register,
    watch
} = useForm()

const password = watch("password")
```

Now

```tsx
<p>Password length: {password?.length}</p>
```

Every keystroke updates automatically.

---

## Watch Multiple Fields

```tsx
const email = watch("email")
const age = watch("age")
```

or

```tsx
const values = watch()
```

returns

```ts
{
   email: "...",
   password: "...",
   age: 20
}
```

---

# Lesson 18: `getValues()`

Difference:

```
watch()

↓

Re-renders
```

```
getValues()

↓

No Re-render
```

Example

```tsx
const {
    getValues
} = useForm()
```

Button

```tsx
<button
onClick={()=>{
    console.log(getValues())
}}
>
Show Values
</button>
```

Output

```ts
{
email:"abc@gmail.com",
password:"123456"
}
```

---

# Lesson 19: `setValue()`

Programmatically update fields.

Example

```tsx
const {
    setValue
} = useForm()
```

Button

```tsx
<button
onClick={()=>{
setValue("name","Atiar")
}}
>
Auto Fill
</button>
```

The input changes immediately.

---

## Multiple Values

```tsx
setValue("email","abc@gmail.com")

setValue("age",25)
```

---

# Lesson 20: `reset()`

Reset after successful submit.

```tsx
const {
    reset
} = useForm()
```

Submit

```tsx
const onSubmit = async(data)=>{

await api.post("/register/",data)

reset()

}
```

Everything clears.

---

## Reset With Values

```tsx
reset({
    name:"Guest",
    email:""
})
```

---

# Lesson 21: Server Validation Errors

Suppose Django returns

```json
{
    "email":[
        "Email already exists."
    ]
}
```

Don't use `alert()`.

Instead

```tsx
const {
    setError
}=useForm()
```

Catch

```tsx
catch(error){

setError("email",{

type:"server",

message:error.response.data.email[0]

})

}
```

Input

```tsx
<p>{errors.email?.message}</p>
```

Now users see the server error under the field.

---

# Lesson 22: Clear Errors

```tsx
clearErrors("email")
```

or

```tsx
clearErrors()
```

Useful when switching tabs or after fixing an error.

---

# Lesson 23: Manual Validation

Normally validation happens on submit.

But sometimes you want:

```
Next Button

↓

Validate

↓

Go Next
```

```tsx
const valid = await trigger()
```

or

```tsx
await trigger("email")
```

Example

```tsx
const next = async()=>{

const valid = await trigger()

if(valid){

console.log("Next Step")

}

}
```

---

# Lesson 24: Validation Modes

Default

```tsx
useForm({
mode:"onSubmit"
})
```

Only validates when submitting.

---

## onChange

```tsx
mode:"onChange"
```

Every keypress validates.

```
A

↓

Validate

↓

B

↓

Validate
```

---

## onBlur

```tsx
mode:"onBlur"
```

Validates after leaving the input.

---

## all

```tsx
mode:"all"
```

Both

```
Typing

+

Blur
```

---

# Lesson 25: Form State

```tsx
const {

formState

}=useForm()
```

Useful properties

```tsx
formState.errors

formState.isDirty

formState.isValid

formState.isSubmitting

formState.submitCount
```

---

## Example

```tsx
<button

disabled={!formState.isValid}

>

Submit

</button>
```

Button stays disabled until the form is valid.

---

# Lesson 26: Disable Entire Form

```tsx
<form>

<fieldset disabled={isSubmitting}>

<input />

<input />

<button>

Submit

</button>

</fieldset>

</form>
```

Everything becomes disabled while the request is in progress.

---

# Lesson 27: API Folder Structure

Instead of calling Axios directly inside components:

❌

```tsx
const res = await api.post("/login/",data)
```

Create

```
services/authService.ts
```

```ts
import { api } from "@/lib/api"

export async function login(data){

const res = await api.post("/login/",data)

return res.data

}
```

Component

```tsx
const result = await login(data)
```

Benefits:

```
UI

↓

Service Layer

↓

Axios

↓

Backend
```

If the API changes later, you update only the service.

---

# Lesson 28: Typed API Response

```ts
interface LoginResponse{

access:string

refresh:string

user:{
id:number
email:string
}

}
```

Usage

```tsx
const res = await api.post<LoginResponse>(
"/login/",
data
)

console.log(res.data.user.email)
```

TypeScript now provides autocomplete and compile-time checks.

---

# Lesson 29: Complete Production Flow

```
User

↓

Input

↓

React Hook Form

↓

Zod

↓

handleSubmit()

↓

Service Layer

↓

Axios

↓

DRF

↓

JSON Response

↓

Store Token

↓

Toast

↓

Redirect
```

---

# Lesson 30: Mini Project — Login Form

**Folder Structure**

```
src/
├── app/
│   └── login/
│       └── page.tsx
├── components/
│   └── LoginForm.tsx
├── schemas/
│   └── auth.ts
├── services/
│   └── authService.ts
├── lib/
│   └── api.ts
└── types/
    └── auth.ts
```

### Workflow

1. User enters email and password.
    
2. Zod validates the input.
    
3. `handleSubmit()` gathers the data.
    
4. `authService.login()` sends a request to the Django API.
    
5. The server returns JWT tokens.
    
6. Store the tokens securely (prefer HTTP-only cookies if your architecture supports them).
    
7. Redirect the user to the dashboard.
    

---

## Next Part (Part 3)

We'll cover advanced, production-ready topics:

- `Controller` (for custom UI libraries like Shadcn UI, MUI, React Select)
    
- `useFieldArray()` (dynamic forms such as adding multiple addresses or phone numbers)
    
- File upload (`multipart/form-data`)
    
- Drag & drop image uploads
    
- Multi-step forms (wizard)
    
- Nested objects and arrays with Zod
    
- Async validation (e.g., check if an email or username is already taken)
    
- Integrating RHF with TanStack Query for mutations and cache updates
    

These are the patterns commonly used in large-scale Next.js applications.

# Next.js Form Mastery (Part 3)

## Advanced React Hook Form + Zod

This part covers the features you'll use in **real production applications**.

---

# Lesson 31: Why Controller?

Until now we've used

```tsx
<input {...register("email")} />
```

This only works for **native HTML inputs**.

But libraries like:

- Shadcn UI
    
- MUI
    
- Ant Design
    
- React Select
    
- DatePicker
    

don't expose refs the same way.

So RHF provides **Controller**.

```
HTML Input
        │
 register()
        │
──────────────

Custom Component
        │
 Controller
```

---

# Example

Without Controller ❌

```tsx
<Select
    {...register("country")}
/>
```

May not work correctly.

Instead

```tsx
import { Controller } from "react-hook-form"

<Controller
    name="country"
    control={control}
    render={({ field }) => (
        <Select
            {...field}
        />
    )}
/>
```

Notice

```
register()

↓

Controller

↓

field

↓

Custom Component
```

---

# Lesson 32: Understanding field

Inside Controller

```tsx
render={({ field }) => ...)
```

field contains

```tsx
field.onChange

field.onBlur

field.value

field.name

field.ref
```

Equivalent to

```tsx
<input

value={field.value}

onChange={field.onChange}

onBlur={field.onBlur}

ref={field.ref}

/>
```

---

# Lesson 33: Shadcn Select Example

```tsx
<Controller
    control={control}
    name="role"
    render={({ field }) => (
        <Select
            value={field.value}
            onValueChange={field.onChange}
        >
            <SelectItem value="admin">
                Admin
            </SelectItem>

            <SelectItem value="user">
                User
            </SelectItem>

        </Select>
    )}
/>
```

This is how most production apps connect RHF to Shadcn components.

---

# Lesson 34: useFieldArray()

Imagine

```
User

↓

Add Phone Number

↓

+ Add Another

↓

+ Add Another
```

Impossible with fixed inputs.

Need

```
Dynamic Inputs
```

---

## Example

```tsx
const {

control

}=useForm({

defaultValues:{

phones:[

{number:""}

]

}

})
```

Then

```tsx
const {

fields,

append,

remove

}=useFieldArray({

control,

name:"phones"

})
```

---

Render

```tsx
{
fields.map((field,index)=>(

<input

key={field.id}

{...register(`phones.${index}.number`)}

/>

))
}
```

Add button

```tsx
<button

onClick={()=>append({

number:""

})}

>

Add

</button>
```

Remove

```tsx
<button

onClick={()=>remove(index)}

>

Delete

</button>
```

---

Data becomes

```json
{
  "phones":[
      {
          "number":"11111"
      },
      {
          "number":"22222"
      }
  ]
}
```

Perfect for DRF Nested Serializers.

---

# Lesson 35: Nested Objects

Instead of

```json
{
"name":"Atiar"
}
```

You can submit

```json
{
"name":"Atiar",

"address":{

"city":"Dhaka",

"country":"Bangladesh"

}

}
```

Register

```tsx
register("address.city")
```

or

```tsx
register("address.country")
```

Simple.

---

# Lesson 36: Nested Zod

```tsx
const schema = z.object({

name:z.string(),

address:z.object({

city:z.string(),

country:z.string()

})

})
```

Works automatically.

---

# Lesson 37: File Upload

Most beginners do

```tsx
register("image")
```

Wrong.

Need

```tsx
<input

type="file"

{...register("image")}

/>
```

Submitted value

```
FileList
```

Not

```
string
```

---

Access

```tsx
const onSubmit=(data)=>{

console.log(data.image)

}
```

Output

```
FileList(1)
```

---

# Lesson 38: Send Image

Need FormData

```tsx
const formData = new FormData()

formData.append(

"title",

data.title

)

formData.append(

"image",

data.image[0]

)
```

Axios

```tsx
await api.post(

"/products/",

formData,

{

headers:{

"Content-Type":"multipart/form-data"

}

}

)
```

DRF receives

```
request.FILES
```

---

# Lesson 39: Image Preview

```tsx
const file = watch("image")
```

Preview

```tsx
const preview =

file?.length

?

URL.createObjectURL(file[0])

:

null
```

Render

```tsx
<img

src={preview}

/>
```

Production apps usually revoke object URLs when no longer needed:

```tsx
useEffect(() => {
  if (!file?.length) return;

  const url = URL.createObjectURL(file[0]);
  setPreview(url);

  return () => URL.revokeObjectURL(url);
}, [file]);
```

This avoids small memory leaks.

---

# Lesson 40: Multiple Images

Input

```tsx
<input

multiple

type="file"

{...register("images")}

/>
```

Submit

```tsx
const formData = new FormData()

Array.from(data.images).forEach(

(image)=>{

formData.append(

"images",

image

)

}

)
```

---

# Lesson 41: Async Validation

Example

```
User types email

↓

Check Database

↓

Already Exists?

↓

Show Error
```

Example

```tsx
const email = watch("email")
```

API

```tsx
const res = await api.get(

"/check-email/",

{

params:{

email

}

})
```

If exists

```tsx
setError(

"email",

{

type:"manual",

message:"Email already exists"

}

)
```

Clear

```tsx
clearErrors("email")
```

A production tip: avoid calling the API on every keystroke. Debounce the request (for example, wait 300–500 ms after typing stops) to reduce unnecessary traffic.

---

# Lesson 42: Password Confirmation

Schema

```tsx
const schema = z

.object({

password:z.string(),

confirmPassword:z.string()

})

.refine(

(data)=>

data.password===

data.confirmPassword,

{

message:

"Password mismatch",

path:["confirmPassword"]

}

)
```

Very common interview question.

---

# Lesson 43: Multi-Step Form

```
Step 1

↓

Name

↓

Next

↓

Step 2

↓

Address

↓

Next

↓

Step 3

↓

Payment

↓

Submit
```

Don't create three forms.

Use

```
One RHF

+

Conditional Rendering
```

Example

```tsx
{

step===1

&&

<StepOne/>

}

{

step===2

&&

<StepTwo/>

}
```

All share the same `useForm()` instance, often through `FormProvider`.

---

# Lesson 44: FormProvider

Instead of

```
Parent

↓

Props

↓

Child

↓

Props

↓

Grandchild

↓

Props
```

Use

```tsx
<FormProvider

{...methods}

>

<StepOne/>

<StepTwo/>

</FormProvider>
```

Child

```tsx
const {

register

}=useFormContext()
```

No prop drilling.

---

# Lesson 45: TanStack Query Mutation

Instead of

```tsx
await api.post(...)
```

Use Mutation.

```tsx
const mutation = useMutation({

mutationFn:login

})
```

Submit

```tsx
mutation.mutate(data)
```

Benefits

- Loading state
    
- Retry
    
- Error handling
    
- Success callback
    
- Cache invalidation
    

---

# Lesson 46: Optimistic Update

User

```
Clicks Like

↓

UI Updates Immediately

↓

API Running

↓

Success

↓

Keep

↓

Fail

↓

Rollback
```

TanStack Query makes this pattern much easier for mutations.

---

# Lesson 47: Reusable Input Component

Instead of

```tsx
<input />

<input />

<input />
```

Create

```tsx
<TextInput

name="email"

label="Email"

/>
```

Inside

```tsx
const {

register

}=useFormContext()
```

Reusable.

---

# Lesson 48: Large Project Folder Structure

```
src/
│
├── app/
│
├── components/
│      ├── forms/
│      │      LoginForm.tsx
│      │      RegisterForm.tsx
│      │
│      ├── fields/
│      │      TextInput.tsx
│      │      SelectField.tsx
│      │      ImageUpload.tsx
│      │
│      └── ui/
│
├── hooks/
│      useLogin.ts
│      useRegister.ts
│
├── services/
│      auth.service.ts
│      user.service.ts
│
├── schemas/
│      auth.schema.ts
│      user.schema.ts
│
├── lib/
│      api.ts
│
├── types/
│
└── utils/
```

---

# Lesson 49: Complete Production Flow

```
User

↓

RHF

↓

Zod

↓

Controller

↓

FieldArray

↓

Service

↓

Axios

↓

DRF API

↓

JWT

↓

TanStack Query

↓

Toast

↓

Redirect
```

---

# Lesson 50: Real-World Example (E-commerce Product Form)

Imagine you're building a product creation page with a Django REST Framework backend.

**Fields**

- Product name
    
- Description
    
- Price
    
- Category (custom Select → `Controller`)
    
- Multiple product images (`FormData`)
    
- Dynamic specifications (`useFieldArray`)
    
    - Color
        
    - Size
        
    - Weight
        
- Stock quantity
    
- Tags
    
- Submit
    

**Workflow**

```
Product Form
        │
        ▼
React Hook Form
        │
        ▼
Zod Validation
        │
        ▼
Dynamic Specifications
(useFieldArray)
        │
        ▼
Image Upload
(FormData)
        │
        ▼
Axios Service
        │
        ▼
DRF View
        │
        ▼
ProductSerializer
        │
        ▼
Database
        │
        ▼
Success Response
```

This combines nearly every advanced concept from Parts 1–3 into a single production-ready feature.

---

## What to Learn Next (Part 4)

The next step is integrating these forms into a **complete authentication system** with Next.js and Django REST Framework:

1. Login with JWT
    
2. Register
    
3. Refresh token handling
    
4. Protected routes
    
5. HTTP-only cookie authentication
    
6. Axios interceptors for automatic token refresh
    
7. Role-based authorization (Admin/User)
    
8. Logout
    
9. Password reset
    
10. Email verification
    

These topics connect advanced form handling with a secure, production-grade authentication flow.

# Next.js Authentication Mastery (Part 4)

## React Hook Form + Next.js + Django REST Framework (JWT)

This part focuses on **production authentication architecture**.

---

# Lesson 51: Authentication Flow

A login system is more than just sending an email and password.

```text
User
   │
   ▼
Login Form (RHF)
   │
   ▼
Zod Validation
   │
   ▼
Auth Service
   │
   ▼
Axios
   │
   ▼
Django REST Framework
   │
   ▼
JWT Token
   │
   ▼
Store Token
   │
   ▼
Protected Pages
```

---

# Lesson 52: Project Structure

A scalable authentication structure might look like:

```text
src/
│
├── app/
│     login/
│     register/
│     dashboard/
│
├── services/
│     auth.service.ts
│
├── hooks/
│     useLogin.ts
│     useRegister.ts
│
├── context/
│     AuthProvider.tsx
│
├── lib/
│     api.ts
│
├── middleware.ts
│
├── types/
│     auth.ts
│
└── schemas/
      auth.schema.ts
```

Notice that:

- UI lives in `components/`
    
- API logic lives in `services/`
    
- Auth state lives in `context/`
    
- Axios configuration lives in `lib/`
    

---

# Lesson 53: Login API

Suppose DRF exposes

```http
POST /api/auth/login/
```

Request

```json
{
    "email":"john@gmail.com",
    "password":"123456"
}
```

Response

```json
{
    "access":"xxxxx",
    "refresh":"yyyyy",
    "user":{
        "id":1,
        "email":"john@gmail.com",
        "name":"John"
    }
}
```

---

# Lesson 54: Define Types

```ts
export interface LoginRequest{
    email:string
    password:string
}

export interface User{
    id:number
    email:string
    name:string
}

export interface LoginResponse{
    access:string
    refresh:string
    user:User
}
```

Everything becomes type-safe.

---

# Lesson 55: Auth Service

Instead of placing Axios inside the component:

```tsx
await api.post(...)
```

Create

```ts
services/auth.service.ts
```

```ts
import { api } from "@/lib/api"

export async function login(data:LoginRequest){

    const response =
        await api.post<LoginResponse>(
            "/auth/login/",
            data
        )

    return response.data
}
```

Component

```tsx
const result = await login(data)
```

Cleaner architecture.

---

# Lesson 56: Custom Hook

Create

```text
hooks/useLogin.ts
```

```tsx
export function useLogin(){

    const mutation = useMutation({
        mutationFn:login
    })

    return mutation
}
```

Component

```tsx
const loginMutation = useLogin()
```

Submit

```tsx
loginMutation.mutate(data)
```

---

# Lesson 57: Auth Context

Authentication state should be global.

```text
Navbar

Dashboard

Profile

Settings
```

All need the current user.

Create

```text
AuthContext
```

```tsx
const AuthContext =
createContext(null)
```

Provider

```tsx
<AuthProvider>

<App/>

</AuthProvider>
```

Now every page can access the authenticated user.

---

# Lesson 58: Store User

```tsx
const [user,setUser] =
useState<User|null>(null)
```

Login

```tsx
setUser(result.user)
```

Anywhere

```tsx
const {user}=useAuth()
```

Display

```tsx
Hello {user.name}
```

---

# Lesson 59: Where Should Tokens Be Stored?

Many beginners use

```text
localStorage
```

It works, but if malicious JavaScript runs in your page (for example through an XSS vulnerability), it can potentially read tokens stored there.

A common production approach is:

```text
Access Token

↓

HTTP-only Cookie

↓

Browser sends automatically

↓

JavaScript cannot read it
```

If you use HTTP-only cookies, the backend usually sets the cookie and the frontend doesn't manually store the token.

---

# Lesson 60: Axios Configuration

```ts
import axios from "axios"

export const api =
axios.create({

baseURL:"http://localhost:8000/api",

withCredentials:true

})
```

`withCredentials: true` allows the browser to send cookies to the backend when your backend is configured for cookie-based authentication and CORS.

---

# Lesson 61: Axios Request Interceptor

Sometimes you do use bearer tokens.

```text
Request

↓

Interceptor

↓

Add Authorization Header

↓

Backend
```

Example

```ts
api.interceptors.request.use(config=>{

    config.headers.Authorization=
    `Bearer ${token}`

    return config

})
```

Now every request includes

```http
Authorization: Bearer xxxxx
```

automatically.

---

# Lesson 62: Refresh Token

Access tokens expire.

Example

```text
Access Token

↓

15 minutes

↓

Expired

↓

Refresh Token

↓

New Access Token
```

No login screen appears.

The refresh token silently generates a new access token.

---

# Lesson 63: Response Interceptor

When the server returns

```http
401 Unauthorized
```

Flow

```text
API Request

↓

401

↓

Refresh Token

↓

Retry Original Request

↓

Success
```

This creates a smooth user experience.

---

# Lesson 64: Protected Route

Public

```text
/

About

Login
```

Protected

```text
/dashboard

/profile

/orders
```

Before rendering

```text
Check Login

↓

Not Logged In

↓

Redirect Login
```

---

# Lesson 65: Middleware

Next.js middleware runs before a page loads.

```text
Request

↓

Middleware

↓

Authenticated?

↓

Dashboard

or

↓

Redirect Login
```

Example

```ts
export function middleware(request){

}
```

Middleware is ideal for route protection.

---

# Lesson 66: Logout

User clicks

```text
Logout
```

Flow

```text
Clear Session

↓

Clear User State

↓

Navigate Login
```

If using cookies, call the backend logout endpoint so it can invalidate or clear the cookie, then clear any client-side auth state.

---

# Lesson 67: Auto Login

User refreshes page.

Don't immediately assume they're logged out.

Instead

```text
Refresh

↓

GET /me

↓

Authenticated?

↓

Restore User
```

Most production apps do this.

---

# Lesson 68: Current User Endpoint

DRF

```http
GET /api/auth/me/
```

Response

```json
{
"id":1,
"name":"John",
"email":"john@gmail.com"
}
```

Your `AuthProvider` can call this endpoint on app startup to restore the session.

---

# Lesson 69: Login Page Flow

```text
User

↓

Email

↓

Password

↓

Zod

↓

React Hook Form

↓

Mutation

↓

API

↓

JWT

↓

Fetch Current User

↓

Dashboard
```

---

# Lesson 70: Registration Flow

```text
Register

↓

Validation

↓

Create User

↓

Email Verification (optional)

↓

Login

↓

Dashboard
```

---

# Lesson 71: Email Verification

```text
Register

↓

Verification Email

↓

Click Link

↓

Verify

↓

Account Activated
```

Many applications require verification before allowing login.

---

# Lesson 72: Forgot Password

```text
Forgot Password

↓

Enter Email

↓

Send Reset Link

↓

Open Email

↓

Reset Password

↓

Login
```

---

# Lesson 73: Reset Password

```text
Reset Link

↓

New Password

↓

Confirm Password

↓

Submit

↓

Success
```

Use the same RHF + Zod validation patterns you've already learned.

---

# Lesson 74: Role-Based Authorization

Suppose the API returns

```json
{
    "role":"admin"
}
```

Now

```text
Admin

↓

Dashboard

Users

Products

Orders
```

User

```text
Dashboard

Orders
```

Role checks can be performed both on the backend (required) and the frontend (for UI visibility). Frontend checks improve the user experience but should never replace backend authorization.

---

# Lesson 75: Production Authentication Architecture

```text
Login Form (RHF)
        │
        ▼
Zod Validation
        │
        ▼
Auth Service
        │
        ▼
Axios
        │
        ▼
DRF JWT
        │
        ▼
HTTP-only Cookie
        │
        ▼
AuthProvider
        │
        ▼
Current User (/me)
        │
        ▼
Protected Routes
        │
        ▼
Dashboard
```

---

# Common Interview Questions

|Question|Expected Answer|
|---|---|
|Why React Hook Form?|Better performance with fewer re-renders than fully controlled forms.|
|Why Zod?|Schema validation with TypeScript type inference.|
|Why a service layer?|Keeps API logic separate from UI components.|
|Why Auth Context?|Shares authentication state across the app.|
|Why middleware?|Protects routes before rendering.|
|Why refresh tokens?|Maintains user sessions without frequent logins.|
|Why `/me` endpoint?|Restores the authenticated user's information after page refresh.|
|Why HTTP-only cookies?|They help protect tokens from JavaScript access, reducing XSS risk.|

---

# Final Authentication Workflow

```text
User Opens Login
        │
        ▼
Fill Form
        │
        ▼
React Hook Form
        │
        ▼
Zod Validation
        │
        ▼
TanStack Query Mutation
        │
        ▼
Auth Service
        │
        ▼
Axios
        │
        ▼
Django REST Framework
        │
        ▼
Issue Tokens / Set Cookie
        │
        ▼
Fetch Current User (/me)
        │
        ▼
Save User in Auth Context
        │
        ▼
Redirect to Dashboard
        │
        ▼
Protected Routes + Middleware
```

## Part 5 Preview: Building a Complete Authentication System

In the next part, we'll build a **complete production-ready Next.js + Django REST Framework authentication project** from scratch, including:

1. Login page (RHF + Zod)
    
2. Registration page
    
3. Email verification
    
4. Forgot/reset password
    
5. AuthProvider
    
6. Axios interceptors
    
7. Middleware route protection
    
8. Refresh token flow
    
9. Protected dashboard
    
10. User profile management
    
11. Logout
    
12. Role-based authorization (Admin/User)
    

The result will be a reusable authentication module suitable for most Next.js + DRF applications.

# Next.js + Django REST Framework Authentication Mastery (Part 5)

## Build a Production-Ready Authentication System

Now we'll build a **real project architecture** similar to what you'd see in production.

---

# Project Architecture

```text
Frontend (Next.js)
│
├── Login
├── Register
├── Forgot Password
├── Reset Password
├── Dashboard
├── Profile
└── Middleware

            │

            ▼

Axios Service

            │

            ▼

Django REST Framework

            │

            ▼

JWT Authentication

            │

            ▼

PostgreSQL
```

---

# Lesson 76: Backend API Design

A clean DRF authentication API might look like this:

|Method|Endpoint|Purpose|
|---|---|---|
|POST|`/api/auth/register/`|Create account|
|POST|`/api/auth/login/`|Login|
|POST|`/api/auth/logout/`|Logout|
|POST|`/api/auth/refresh/`|Refresh access token|
|GET|`/api/auth/me/`|Current user|
|POST|`/api/auth/forgot-password/`|Send reset email|
|POST|`/api/auth/reset-password/`|Reset password|
|GET|`/api/auth/verify-email/`|Verify email|

---

# Lesson 77: Frontend Folder Structure

```
src/

app/
    login/
    register/
    forgot-password/
    reset-password/
    dashboard/
    profile/

components/
    auth/
        LoginForm.tsx
        RegisterForm.tsx
        ForgotPasswordForm.tsx

context/
    AuthProvider.tsx

hooks/
    useLogin.ts
    useRegister.ts

services/
    auth.service.ts

schemas/
    auth.schema.ts

lib/
    api.ts

middleware.ts
```

Everything has one responsibility.

---

# Lesson 78: API Layer

```
lib/

api.ts
```

```ts
import axios from "axios"

export const api = axios.create({
    baseURL: process.env.NEXT_PUBLIC_API_URL,
    withCredentials: true
})
```

Never hardcode URLs throughout your app.

---

# Lesson 79: Auth Service

```
services/

auth.service.ts
```

```ts
export const AuthService = {

    login,

    register,

    logout,

    refresh,

    me,

    forgotPassword,

    resetPassword

}
```

Every authentication request stays in one place.

---

# Lesson 80: Login Flow

```
Login Page

↓

RHF

↓

Zod

↓

handleSubmit

↓

AuthService.login()

↓

API

↓

Success

↓

Fetch User

↓

Dashboard
```

---

# Lesson 81: Register Flow

```
Register

↓

Validate

↓

POST Register

↓

Account Created

↓

Email Verification

↓

Login
```

---

# Lesson 82: AuthProvider

This is the heart of authentication.

```
<AuthProvider>

Entire Application

</AuthProvider>
```

Provider stores

```
User

Loading

Login

Logout

Refresh Session
```

Example

```ts
const value = {

user,

login,

logout,

loading

}
```

Every component can access it.

---

# Lesson 83: Initial App Loading

Never immediately render your app.

Instead

```
Application Starts

↓

Loading...

↓

GET /me

↓

Authenticated?

↓

Yes

↓

Dashboard

No

↓

Login
```

This prevents UI flicker.

---

# Lesson 84: Loading Screen

```tsx
if(loading){

return <LoadingSpinner/>

}
```

Instead of

```
Dashboard

↓

Redirect

↓

Login

↓

Flash Screen
```

---

# Lesson 85: Login Mutation

Instead of

```ts
await login()
```

Use

```ts
const mutation =
useMutation({

mutationFn:

AuthService.login

})
```

Benefits

```
Loading

Success

Error

Retry

Callbacks
```

---

# Lesson 86: Success Callback

```ts
const mutation = useMutation({

mutationFn:login,

onSuccess:()=>{

router.push("/dashboard")

}

})
```

No manual state management.

---

# Lesson 87: Error Handling

Suppose DRF returns

```json
{
"detail":"Invalid credentials"
}
```

Display

```
Email

Password

Invalid credentials
```

Don't use

```
alert()
```

Instead use RHF's `setError()` or display a form-level error state.

---

# Lesson 88: Fetch Current User

After login

```
POST Login

↓

Access Token

↓

GET /me

↓

User Information

↓

Save Context
```

Don't rely solely on the login response if your API provides a dedicated `/me` endpoint.

---

# Lesson 89: Navbar

Navbar should use

```
const {

user

}=useAuth()
```

Display

```
Hello Atiar
```

or

```
Login
```

Automatically.

---

# Lesson 90: Middleware

Protect

```
/dashboard

/profile

/orders
```

Middleware

```
Not Logged In

↓

Redirect Login
```

---

# Lesson 91: Dashboard Layout

Instead of protecting every page

```
dashboard/

layout.tsx
```

Inside

```
Authentication Check

↓

Children
```

Cleaner.

---

# Lesson 92: Protected Route Component

```
<Protected>

Dashboard

</Protected>
```

Logic

```
User?

↓

Yes

↓

Render

↓

No

↓

Redirect
```

---

# Lesson 93: Refresh Flow

```
Access Token

↓

Expired

↓

401

↓

Refresh

↓

Retry

↓

Success
```

Invisible to the user.

---

# Lesson 94: Axios Response Interceptor

```
Request

↓

401

↓

Refresh Token

↓

Retry Original Request
```

This is one of the most common production patterns.

---

# Lesson 95: Logout Flow

```
Logout Button

↓

POST Logout

↓

Clear Session

↓

Clear Context

↓

Redirect Login
```

---

# Lesson 96: Profile Page

```
GET /me

↓

Form

↓

Update Profile

↓

PATCH /profile/

↓

Success
```

Reuse the same RHF + Zod patterns you learned earlier.

---

# Lesson 97: Forgot Password

```
Email

↓

POST

↓

Reset Link

↓

Email
```

---

# Lesson 98: Reset Password

```
Token

↓

New Password

↓

Confirm Password

↓

POST

↓

Login
```

---

# Lesson 99: Production Authentication Lifecycle

```
Application Starts

↓

AuthProvider

↓

GET /me

↓

Authenticated?

↓

Yes

↓

Render App

↓

API Requests

↓

401

↓

Refresh Token

↓

Retry

↓

Continue
```

---

# Lesson 100: Complete Production Architecture

```
                  Next.js

                     │

          React Hook Form

                     │

                  Zod

                     │

               TanStack Query

                     │

             AuthService

                     │

                  Axios

                     │

        Request Interceptor

                     │

        Django REST Framework

                     │

            JWT Authentication

                     │

             PostgreSQL Database

                     │

       Response Interceptor (401)

                     │

             Refresh Token

                     │

              AuthProvider

                     │

            Protected Routes

                     │

               Dashboard
```

# Production Folder Structure

```
src/
│
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   ├── register/
│   │   ├── forgot-password/
│   │   └── reset-password/
│   │
│   ├── (dashboard)/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── profile/
│   │   └── settings/
│   │
│   └── layout.tsx
│
├── components/
│   ├── auth/
│   ├── forms/
│   ├── ui/
│   └── layout/
│
├── context/
│   └── AuthProvider.tsx
│
├── hooks/
│   ├── useAuth.ts
│   ├── useLogin.ts
│   ├── useRegister.ts
│   └── useLogout.ts
│
├── services/
│   └── auth.service.ts
│
├── lib/
│   ├── api.ts
│   └── query-client.ts
│
├── schemas/
│   └── auth.schema.ts
│
├── types/
│   └── auth.ts
│
├── middleware.ts
│
└── utils/
```

---

# Capstone Project

To truly master this topic, build the following project from scratch:

### Frontend

- ✅ Next.js App Router
    
- ✅ TypeScript
    
- ✅ React Hook Form
    
- ✅ Zod
    
- ✅ TanStack Query
    
- ✅ Axios
    
- ✅ Tailwind CSS + Shadcn UI
    

### Backend

- ✅ Django
    
- ✅ Django REST Framework
    
- ✅ SimpleJWT (or your preferred JWT solution)
    
- ✅ PostgreSQL
    
- ✅ Email verification
    
- ✅ Password reset
    
- ✅ Role-based permissions
    

### Features

- User registration
    
- Email verification
    
- Login/logout
    
- Auto session restoration
    
- Token refresh
    
- Protected dashboard
    
- Profile update
    
- Change password
    
- Forgot/reset password
    
- Admin vs User permissions
    
- Responsive UI
    
- Error handling and loading states
    

---

## Part 6 Preview

In Part 6, we'll build this project **step by step**, starting from an empty repository and implementing each feature with complete code, explaining every file and architectural decision rather than just the overall design. This will result in a reusable authentication starter that you can use in future Next.js + Django REST Framework projects.

