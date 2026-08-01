নিচে একটা complete example — নাম আর ইমেইল নেওয়ার form, validation সহ, API-তে POST করবে।

**Setup (প্রথমে install করতে হবে):**

```bash
npm install react-hook-form zod @hookform/resolvers
```

**Component code:**

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

// 1. Schema define — kon field e ki rule lagbe
const schema = z.object({
  name: z.string().min(2, "নাম কমপক্ষে ২ অক্ষরের হতে হবে"),
  email: z.string().email("সঠিক ইমেইল দিন"),
});

export default function ContactForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(schema), // zod schema দিয়ে validation
  });

  // 2. Submit হলে এই function চলবে (validation pass হলেই তবে)
  const onSubmit = async (data) => {
    try {
      const res = await fetch("/api/contact", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data),
      });

      if (!res.ok) throw new Error("Something went wrong");

      const result = await res.json();
      console.log("Success:", result);
      reset(); // form clear
    } catch (err) {
      console.error(err);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <input {...register("name")} placeholder="Name" />
        {errors.name && <p style={{ color: "red" }}>{errors.name.message}</p>}
      </div>

      <div>
        <input {...register("email")} placeholder="Email" />
        {errors.email && <p style={{ color: "red" }}>{errors.email.message}</p>}
      </div>

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Submitting..." : "Submit"}
      </button>
    </form>
  );
}
```

**API route (`app/api/contact/route.js`):**

```js
export async function POST(request) {
  const data = await request.json();

  // এখানে database save বা অন্য কিছু করতে পারো
  console.log("Received:", data);

  return Response.json({ message: "Received successfully", data });
}
```

**যা যা হচ্ছে:**

- `register("name")` → input-টাকে RHF-এর সাথে connect করে দেয়
- `zodResolver(schema)` → submit করার আগে zod schema দিয়ে check করে, ভুল থাকলে `errors` object-এ message চলে আসে
- `handleSubmit(onSubmit)` → validation pass করলেই `onSubmit` চলবে, নাহলে চলবে না
- `isSubmitting` → বারবার click ঠেকাতে button disable করে

এটা কি তোমার use case-এর সাথে মিলে, নাকি field গুলো আলাদা (যেমন file upload, dropdown, ইত্যাদি)?


ভালো practice হলো schema, component, আর api route আলাদা ফাইলে রাখা। App Router ধরে একটা structure দিচ্ছি:

```
src/
├── app/
│   ├── api/
│   │   └── contact/
│   │       └── route.js          # POST handler
│   │
│   ├── contact/
│   │   └── page.js               # ContactForm component ব্যবহার হবে এখানে
│   │
│   └── layout.js
│
├── components/
│   └── ContactForm.jsx           # form UI + submit logic
│
└── lib/
    └── schemas/
        └── contact.schema.js     # zod schema আলাদা ফাইলে
```

**`lib/schemas/contact.schema.js`:**

```js
import { z } from "zod";

export const contactSchema = z.object({
  name: z.string().min(2, "নাম কমপক্ষে ২ অক্ষরের হতে হবে"),
  email: z.string().email("সঠিক ইমেইল দিন"),
});
```

**`components/ContactForm.jsx`:**

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { contactSchema } from "@/lib/schemas/contact.schema";

export default function ContactForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(contactSchema),
  });

  const onSubmit = async (data) => {
    const res = await fetch("/api/contact", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });
    if (res.ok) reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Name" />
      {errors.name && <p>{errors.name.message}</p>}

      <input {...register("email")} placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}

      <button disabled={isSubmitting}>Submit</button>
    </form>
  );
}
```

**`app/api/contact/route.js`:**

```js
import { contactSchema } from "@/lib/schemas/contact.schema";

export async function POST(request) {
  const body = await request.json();

  // server-side এও validate করা ভালো practice (client-side skip করা যায় বলে)
  const result = contactSchema.safeParse(body);
  if (!result.success) {
    return Response.json({ error: result.error.flatten() }, { status: 400 });
  }

  // এখানে DB save ইত্যাদি
  return Response.json({ message: "Success", data: result.data });
}
```

**`app/contact/page.js`:**

```jsx
import ContactForm from "@/components/ContactForm";

export default function ContactPage() {
  return <ContactForm />;
}
```

**কেন এভাবে ভাগ করলাম:**

- `schema` আলাদা রাখলে client আর server (API route) দুই জায়গাতেই একই schema reuse করতে পারবে — duplicate validation লিখতে হবে না
- `components/` এ UI আলাদা থাকলে অন্য page-এও এই form দরকার হলে সহজে import করে ব্যবহার করা যায়
- `@/` alias (jsconfig.json বা tsconfig.json এ configured থাকে by default create-next-app এ) দিয়ে path সহজ হয়

Project বড় হলে `lib/schemas/`-এর মতো আরও folder লাগবে যেমন `lib/actions/`, `lib/db/` ইত্যাদি — চাইলে সেটাও দেখাতে পারি।

হ্যাঁ, সাধারণত different endpoint মানে different data shape, তাই আলাদা schema লাগে। যেমন contact form আর signup form-এর field আলাদা, তাই schema-ও আলাদা হবে।

**Structure এভাবে হতে পারে:**

```
lib/
└── schemas/
    ├── contact.schema.js
    ├── signup.schema.js
    └── login.schema.js
```

**তবে কিছু case-এ schema share/reuse করা যায়:**

১. **যদি দুই endpoint-এর data shape একই হয়** (যেমন "create user" আর "update user" প্রায় same field নেয়), তাহলে একই schema বা schema extend করে ব্যবহার করা যায়:

```js
// user.schema.js
import { z } from "zod";

export const baseUserSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
});

// signup এ password লাগবে extra
export const signupSchema = baseUserSchema.extend({
  password: z.string().min(6),
});

// update এ সব field optional হতে পারে
export const updateUserSchema = baseUserSchema.partial();
```

২. **Common validation rule আলাদা করে রাখা যায়** যাতে বারবার না লিখতে হয়:

```js
// common.schema.js
export const emailField = z.string().email("সঠিক ইমেইল দিন");
export const passwordField = z.string().min(6, "কমপক্ষে ৬ অক্ষর লাগবে");
```

```js
// signup.schema.js
import { emailField, passwordField } from "./common.schema";

export const signupSchema = z.object({
  email: emailField,
  password: passwordField,
});
```

**সংক্ষেপে:**

- Endpoint আলাদা হলে সাধারণত schema-ও আলাদা ফাইলে রাখো
- কিন্তু field গুলো overlap করলে base schema বানিয়ে `.extend()` বা `.partial()` দিয়ে reuse করো — duplicate লেখা লাগবে না

তোমার কি একাধিক form/endpoint আছে এখন যেগুলোর মধ্যে field overlap আছে? থাকলে বলো, exact structure সাজিয়ে দিতে পারি।


সোজা কথায়, schema লাগে কারণ **user যা ইচ্ছা তাই পাঠাতে পারে**, আর তুমি সেটা trust করতে পারো না। Schema হলো একটা "চেকপয়েন্ট" — data ভিতরে ঢোকার আগে যাচাই করে নেয়।

**Schema ছাড়া কী সমস্যা হয়, উদাহরণ দিয়ে দেখি:**

ধরো তোমার signup form-এ email নেওয়ার কথা, কিন্তু কেউ পাঠালো:

```json
{ "email": "" }
```

বা

```json
{ "email": 12345 }
```

বা email field-ই পাঠালো না।

Schema ছাড়া তোমাকে হাতে হাতে চেক লিখতে হবে:

```js
if (!data.email) return error;
if (typeof data.email !== "string") return error;
if (!data.email.includes("@")) return error;
if (data.email.length < 5) return error;
// আরও fields থাকলে এরকম আরো অনেক if
```

ফিল্ড বাড়লে এই if-else গুলো messy আর error-prone হয়ে যায়।

**Schema দিয়ে একই জিনিস:**

```js
const schema = z.object({
  email: z.string().email(),
});
```

এক লাইনে সব rule বলা হয়ে গেলো — type check, required check, format check সব একসাথে।

**দুইটা মূল কারণ:**

1. **Client-side এ** — user ভুল data দিলে সাথে সাথে error message দেখানো (submit করার আগেই), ভালো UX-এর জন্য।
    
2. **Server-side এ (এটা বেশি জরুরি)** — কেউ browser-এর form skip করে সরাসরি API-তে (Postman দিয়ে বা script দিয়ে) garbage data পাঠাতে পারে। Client-side validation তখন কোনো কাজে আসে না, কারণ সেটা bypass করা যায়। তাই server-এও schema দিয়ে check করতে হয় — নাহলে database-এ ভুল/harmful data ঢুকে যেতে পারে।
    

**সংক্ষেপে:** Schema হলো data-এর জন্য একটা contract/rule বই — "এই shape-এর বাইরে কিছু আসলে reject করো।" এটা security আর data integrity দুটোর জন্যই দরকার।


আচ্ছা, তাহলে Next.js শুধু **frontend**, আর backend আলাদা Django REST Framework (DRF)-এ আছে। এটা জানা থাকলে পুরো ছবিটা একটু বদলে যায়।

**তাহলে কী পরিবর্তন হবে:**

১. **Next.js-এর নিজের `api/route.js` লাগবে না** (যদি না তুমি একটা middle-layer proxy বানাতে চাও)। সরাসরি DRF endpoint-এ POST করবে:

```jsx
const onSubmit = async (data) => {
  try {
    const res = await fetch("https://your-drf-backend.com/api/contact/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });

    if (!res.ok) {
      const errorData = await res.json();
      console.log("Server validation error:", errorData);
      return;
    }

    const result = await res.json();
    reset();
  } catch (err) {
    console.error(err);
  }
};
```

২. **Server-side validation DRF-ই করবে** — তোমার Django serializer-এ। যেমন:

```python
# serializers.py
class ContactSerializer(serializers.Serializer):
    name = serializers.CharField(min_length=2)
    email = serializers.EmailField()
```

এটা DRF-এর নিজস্ব "schema validation" — অনেকটা zod-এর মতোই কাজ করে, কিন্তু Python side এ।

৩. **তাহলে zod কি লাগবেই না?** লাগবে — কিন্তু শুধু **client-side (Next.js)** এর জন্য। কারণ:

- User submit করার আগেই form-এ error দেখানো (ভালো UX, backend call করা লাগবে না ভুল data দিয়ে)
- কিন্তু আসল/final validation তো DRF serializer-ই করবে, কারণ backend কখনো frontend-কে trust করে না

**সংক্ষেপে দুই স্তর validation:**

|জায়গা|Tool|কাজ|
|---|---|---|
|Next.js (client)|zod + RHF|তাড়াতাড়ি feedback, ভালো UX|
|DRF (server)|Serializer|আসল security/data integrity check|

দুটোই দরকার, একটা আরেকটার replacement না। DRF-এর serializer error response তুমি কীভাবে ফেরত পাও (field-wise error format), সেটা জানলে Next.js form-এ ওই error গুলো map করে দেখানোর কোড দেখাতে পারি — চাইলে বলো।


ভালো প্রশ্ন — schema নিজে কোথাও data পাঠায় না, এটা শুধু data-কে **check/filter** করে। আসল flow বুঝি:

**পুরো journey টা এরকম:**

```
User form-এ টাইপ করে
      ↓
handleSubmit() call হয়
      ↓
zod schema data check করে (client-side)
      ↓
   ভুল থাকলে → error দেখায়, আর কিছু হয় না (থেমে যায়)
   ঠিক থাকলে → onSubmit(data) function চলে
      ↓
fetch() দিয়ে DRF backend-এ POST request যায়
      ↓
DRF-এর serializer আবার validate করে (server-side)
      ↓
   ভুল থাকলে → error response ফেরত আসে
   ঠিক থাকলে → Django database-এ save করে
      ↓
Response ফেরত আসে Next.js-এ
      ↓
তুমি সেটা দেখাও (success message/redirect ইত্যাদি)
```

**মূল কথা: schema নিজে data পাঠায় না, এটা একটা gatekeeper।**

```jsx
const onSubmit = async (data) => {
  // এখানে "data" মানে zod validate করে দেওয়া clean data
  // schema শুধু চেক করে দিয়েছে এই data ঠিক আছে কিনা
  
  const res = await fetch("https://backend.com/api/contact/", {
    method: "POST",
    body: JSON.stringify(data), // এখানে data actual পাঠানো হচ্ছে
  });
};
```

তাহলে:

- **zod schema** → শুধু data-কে check করে, pass করলে `onSubmit` function-কে data হাতে তুলে দেয়
- **`fetch`/`onSubmit`** → আসল data backend-এ পাঠায়
- **DRF serializer** → backend-এ আবার সেই data check করে, তারপর database-এ save করে

Schema হলো just একটা "quality check" ধাপ — data-এর journey-তে এটা একটা checkpoint, destination না।


----
Schema শেখার সহজ উপায় হলো এটাকে একটা **language** হিসেবে দেখা — কিছু building block শিখে নিলে যেকোনো shape বানানো যায়। ধাপে ধাপে দেখি।

**১. Basic types (এগুলো দিয়েই শুরু)**

```js
z.string()      // text
z.number()      // সংখ্যা
z.boolean()     // true/false
z.date()        // date
```

**২. String-এর common rules**

```js
z.string().min(2, "কমপক্ষে ২ অক্ষর")
z.string().max(50, "সর্বোচ্চ ৫০ অক্ষর")
z.string().email("সঠিক ইমেইল দিন")
z.string().url("সঠিক URL দিন")
z.string().regex(/^[0-9]+$/, "শুধু সংখ্যা")
```

**৩. Optional / required / default**

```js
z.string().optional()        // না দিলেও চলবে
z.string().nullable()        // null দেওয়া যাবে
z.string().default("N/A")    // না দিলে default value
```

**৪. Number-এর rules**

```js
z.number().min(1)
z.number().max(100)
z.number().int("পূর্ণসংখ্যা হতে হবে")
z.number().positive()
```

**৫. Object বানানো (form-এর মূল ব্যবহার এটাই)**

```js
const schema = z.object({
  name: z.string().min(2),
  age: z.number().min(18, "১৮+ হতে হবে"),
  email: z.string().email(),
});
```

**৬. Array**

```js
z.array(z.string())              // string-এর array
z.array(z.string()).min(1, "কমপক্ষে ১টা item লাগবে")

// object-এর array (যেমন multiple items)
z.array(z.object({
  productName: z.string(),
  quantity: z.number(),
}))
```

**৭. Enum (fixed options)**

```js
z.enum(["male", "female", "other"])
```

**৮. Custom validation (নিজের rule)**

```js
z.string().refine((val) => val.includes("@gmail.com"), {
  message: "শুধু gmail address দিন",
})
```

**৯. দুইটা field-এর মধ্যে match check (যেমন password confirm)**

```js
const schema = z.object({
  password: z.string().min(6),
  confirmPassword: z.string(),
}).refine((data) => data.password === data.confirmPassword, {
  message: "Password মিলছে না",
  path: ["confirmPassword"], // কোন field-এ error দেখাবে
});
```

**১০. Nested object**

```js
const schema = z.object({
  name: z.string(),
  address: z.object({
    city: z.string(),
    zip: z.string(),
  }),
});
```

---

**শেখার practical পদ্ধতি:**

1. প্রথমে তোমার form-এর প্রতিটা field আর তার data type লিস্ট করো (string/number/boolean ইত্যাদি)
2. প্রতিটা field-এ কী rule লাগবে ভাবো (required? min length? format?)
3. উপরের building block গুলো জোড়া দিয়ে schema লিখে ফেলো
4. `schema.safeParse(testData)` দিয়ে console-এ test করো ঠিকমতো কাজ করছে কিনা

**Test করার উদাহরণ:**

```js
const result = schema.safeParse({ name: "A", email: "wrong" });
console.log(result.success);  // false
console.log(result.error.flatten()); // কোন field এ কী error
```

তোমার একটা real form (যেমন signup বা product form) এর field list দাও, আমি সেটার জন্য schema লিখে দেখাই — practice-এর জন্য এটাই সবচেয়ে ভালো উপায়।

------
Schema তুমি নিজে কোথাও explicitly "call" করছো না — এটা **RHF-এর ভিতরে automatically call হয়**, `resolver` এর মাধ্যমে।

**এই লাইনটাই আসল connection:**

```jsx
const { register, handleSubmit } = useForm({
  resolver: zodResolver(schema), // 👈 এখানে schema resolver-কে দেওয়া হলো
});
```

**ভিতরে কী হয় (flow):**

```
User submit বাটনে ক্লিক করে
      ↓
handleSubmit(onSubmit) trigger হয়
      ↓
RHF নিজে থেকেই resolver (zodResolver) কে call করে
      ↓
zodResolver ভিতরে schema.safeParse(formData) চালায়   ← schema এখানে call হয়
      ↓
   Valid হলে → onSubmit(data) function চলে
   Invalid হলে → errors object populate হয়, onSubmit চলে না
```

তুমি নিজে হাতে `schema.parse()` বা `schema.safeParse()` লেখো না RHF দিয়ে কাজ করলে — `zodResolver(schema)` এটা RHF-কে বলে দেয় "submit করার আগে এই schema দিয়ে check করো।"

---

**যদি RHF ছাড়া শুধু zod ব্যবহার করতে চাও (manual call):**

```js
const result = schema.safeParse(data);

if (!result.success) {
  console.log(result.error.flatten());
} else {
  // result.data নিয়ে কাজ করো
}
```

এখানে তুমি নিজে হাতে schema call করছো।

---

**সংক্ষেপে:**

- RHF + zodResolver ব্যবহার করলে → schema **automatically** call হয় submit-এর সময়, RHF নিজে ভিতরে করে দেয়
- RHF ছাড়া (backend API route-এ, যেমন DRF-এর বদলে Next.js API নিজে হ্যান্ডেল করলে) → তোমাকে নিজে হাতে `safeParse()` call করতে হবে

DRF backend ব্যবহার করছো বলে, zod তোমার শুধু **client-side form-এই** কাজ করবে RHF-এর মাধ্যমে — backend-এ zod লাগবে না, ওখানে DRF serializer নিজেই এই কাজ করবে।

-----
E-commerce-এর Category আর Product দুটোর জন্য complete example দিচ্ছি।

**Folder structure:**

```
src/
├── lib/
│   └── schemas/
│       ├── category.schema.js
│       └── product.schema.js
├── components/
│   ├── CategoryForm.jsx
│   └── ProductForm.jsx
```

---

## ১. Category Schema

```js
// lib/schemas/category.schema.js
import { z } from "zod";

export const categorySchema = z.object({
  name: z.string().min(2, "Category name কমপক্ষে ২ অক্ষরের হতে হবে"),
  slug: z.string()
    .min(2, "Slug দিতে হবে")
    .regex(/^[a-z0-9-]+$/, "Slug এ শুধু lowercase, সংখ্যা, আর - থাকতে পারবে"),
  description: z.string().max(500, "সর্বোচ্চ ৫০০ অক্ষর").optional(),
  isActive: z.boolean().default(true),
});
```

## Category Form Component

```jsx
// components/CategoryForm.jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { categorySchema } from "@/lib/schemas/category.schema";

export default function CategoryForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(categorySchema),
    defaultValues: { isActive: true },
  });

  const onSubmit = async (data) => {
    try {
      const res = await fetch("http://localhost:8000/api/categories/", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data),
      });

      if (!res.ok) {
        const err = await res.json();
        console.log("Backend error:", err);
        return;
      }

      const result = await res.json();
      console.log("Created:", result);
      reset();
    } catch (err) {
      console.error(err);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <div>
        <input {...register("name")} placeholder="Category Name" className="border p-2 w-full" />
        {errors.name && <p className="text-red-500 text-sm">{errors.name.message}</p>}
      </div>

      <div>
        <input {...register("slug")} placeholder="category-slug" className="border p-2 w-full" />
        {errors.slug && <p className="text-red-500 text-sm">{errors.slug.message}</p>}
      </div>

      <div>
        <textarea {...register("description")} placeholder="Description" className="border p-2 w-full" />
        {errors.description && <p className="text-red-500 text-sm">{errors.description.message}</p>}
      </div>

      <label className="flex items-center gap-2">
        <input type="checkbox" {...register("isActive")} />
        Active
      </label>

      <button type="submit" disabled={isSubmitting} className="bg-blue-500 text-white px-4 py-2 rounded">
        {isSubmitting ? "Saving..." : "Create Category"}
      </button>
    </form>
  );
}
```

---

## ২. Product Schema (একটু বেশি complex — category select, image, price)

```js
// lib/schemas/product.schema.js
import { z } from "zod";

export const productSchema = z.object({
  name: z.string().min(2, "Product name দিতে হবে"),
  slug: z.string().regex(/^[a-z0-9-]+$/, "Valid slug দিন"),
  description: z.string().min(10, "কমপক্ষে ১০ অক্ষরের description দিন"),

  price: z.coerce.number({ invalid_type_error: "Price সংখ্যা হতে হবে" })
    .positive("Price ০ এর বেশি হতে হবে"),

  stock: z.coerce.number()
    .int("Stock পূর্ণসংখ্যা হতে হবে")
    .nonnegative("Stock ঋণাত্মক হতে পারবে না"),

  categoryId: z.string().min(1, "Category select করুন"), // dropdown থেকে category id

  images: z
    .array(z.string().url("Valid image URL দিন"))
    .min(1, "কমপক্ষে ১টা image লাগবে"),

  isFeatured: z.boolean().default(false),
});
```

**কেন `z.coerce.number()` ব্যবহার করলাম:** HTML input থেকে সবসময় string আসে (`"500"`), even number type input হলেও। `z.coerce.number()` সেটাকে automatically number-এ convert করে দেয়।

## Product Form Component

```jsx
// components/ProductForm.jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { productSchema } from "@/lib/schemas/product.schema";
import { useEffect, useState } from "react";

export default function ProductForm() {
  const [categories, setCategories] = useState([]);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(productSchema),
    defaultValues: { images: [""], isFeatured: false },
  });

  // Category dropdown-এর জন্য data লোড করা
  useEffect(() => {
    fetch("http://localhost:8000/api/categories/")
      .then((res) => res.json())
      .then((data) => setCategories(data));
  }, []);

  const onSubmit = async (data) => {
    // images field text input থেকে string আসলে array বানানো লাগতে পারে
    const payload = {
      ...data,
      images: Array.isArray(data.images) ? data.images : [data.images],
    };

    const res = await fetch("http://localhost:8000/api/products/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload),
    });

    if (!res.ok) {
      const err = await res.json();
      console.log("Backend validation error:", err);
      return;
    }

    reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <div>
        <input {...register("name")} placeholder="Product Name" className="border p-2 w-full" />
        {errors.name && <p className="text-red-500 text-sm">{errors.name.message}</p>}
      </div>

      <div>
        <input {...register("slug")} placeholder="product-slug" className="border p-2 w-full" />
        {errors.slug && <p className="text-red-500 text-sm">{errors.slug.message}</p>}
      </div>

      <div>
        <textarea {...register("description")} placeholder="Description" className="border p-2 w-full" />
        {errors.description && <p className="text-red-500 text-sm">{errors.description.message}</p>}
      </div>

      <div>
        <input {...register("price")} placeholder="Price" className="border p-2 w-full" />
        {errors.price && <p className="text-red-500 text-sm">{errors.price.message}</p>}
      </div>

      <div>
        <input {...register("stock")} placeholder="Stock" className="border p-2 w-full" />
        {errors.stock && <p className="text-red-500 text-sm">{errors.stock.message}</p>}
      </div>

      <div>
        <select {...register("categoryId")} className="border p-2 w-full">
          <option value="">Select Category</option>
          {categories.map((cat) => (
            <option key={cat.id} value={cat.id}>{cat.name}</option>
          ))}
        </select>
        {errors.categoryId && <p className="text-red-500 text-sm">{errors.categoryId.message}</p>}
      </div>

      <div>
        <input {...register("images.0")} placeholder="Image URL" className="border p-2 w-full" />
        {errors.images && <p className="text-red-500 text-sm">{errors.images.message}</p>}
      </div>

      <label className="flex items-center gap-2">
        <input type="checkbox" {...register("isFeatured")} />
        Featured Product
      </label>

      <button type="submit" disabled={isSubmitting} className="bg-green-500 text-white px-4 py-2 rounded">
        {isSubmitting ? "Saving..." : "Create Product"}
      </button>
    </form>
  );
}
```

---

## Django DRF-এর corresponding serializer (মিলিয়ে দেখার জন্য)

```python
# serializers.py
from rest_framework import serializers
from .models import Category, Product

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = ["id", "name", "slug", "description", "isActive"]

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ["id", "name", "slug", "description", "price", "stock", "categoryId", "images", "isFeatured"]

    def validate_price(self, value):
        if value <= 0:
            raise serializers.ValidationError("Price must be positive")
        return value
```

**লক্ষ্য করো:** Zod schema-র rule আর DRF serializer-এর validation প্রায় একই জিনিস বলছে — দুই জায়গায়। এটাই normal practice, duplicate না, বরং **defense in depth** (দুই স্তরে সুরক্ষা)।

তোমার actual Product model-এ কি আরও field আছে (যেমন variants, discount, category nested object)? থাকলে বলো, সেই অনুযায়ী schema adjust করে দিই।



হ্যাঁ, **প্রায় প্রতিটা form-এর জন্যই schema বানানো ভালো practice** — তবে এটা "must" না সবসময়, নির্ভর করে form কেমন সেটার উপর।

**কখন schema অবশ্যই বানাবে:**

- Data backend-এ save হচ্ছে (create/update form) — যেমন Category, Product, Signup ইত্যাদি
- Multiple field আছে যেগুলোর validation দরকার (email format, min length, required check)
- Field-এর মধ্যে relation আছে (password === confirmPassword)

**কখন লাগবে না / simple রাখলেই চলে:**

- খুবই ছোট form, ১টা field (যেমন শুধু search box, newsletter email input)
- কোনো validation দরকার নেই এমন form (যেমন শুধু একটা button click করে action ট্রিগার করা)

এসব ক্ষেত্রে `useState` দিয়েই যথেষ্ট, RHF+zod লাগানো overkill।

---

**Practical approach যেটা বেশিরভাগ project follow করে:**

```
lib/schemas/
├── category.schema.js
├── product.schema.js
├── login.schema.js
├── signup.schema.js
└── ...
```

প্রতিটা **major form/entity**-এর জন্য একটা schema ফাইল — এটাই standard পদ্ধতি। কারণ:

1. Reusable (client + সম্ভব হলে elsewhere)
2. এক জায়গায় সব validation rule, খুঁজে পাওয়া সহজ
3. Form বড় হলে বা পরে নতুন field add করলে শুধু schema ফাইল edit করলেই হয়

---

**একটা জিনিস মাথায় রাখা ভালো:** Schema ফাইল বানানো মানে এই না যে সব field-এর জন্য অনেক জটিল rule লিখতে হবে। ছোট schema ও ঠিক আছে:

```js
export const newsletterSchema = z.object({
  email: z.string().email("সঠিক ইমেইল দিন"),
});
```

এক লাইনের schema হলেও আলাদা ফাইলে রাখলে consistency থাকে প্রজেক্টে।

**সংক্ষেপে:** যেকোনো form যেখানে data backend-এ যাচ্ছে এবং validation দরকার — সেখানে schema বানানোই better practice, যদিও ছোট form-এ inline-ও লেখা যায় (আলাদা ফাইল ছাড়া)।



Depend করে data shape same কিনা তার উপর — বেশিরভাগ ক্ষেত্রে **কাছাকাছি same হয় কিন্তু পুরোপুরি same থাকে না**। কারণ বুঝি:

**সাধারণ পার্থক্য:**

||Create|Update|
|---|---|---|
|সব field|Required|সাধারণত Optional (যেটা change করবে শুধু সেটাই পাঠাবে)|
|id/slug|সাধারণত থাকে না|থাকে (কোনটা update হবে বোঝাতে)|
|Password|Required (signup-এ)|Optional (change না করলে না দিলেও চলবে)|

---

## Best practice: Base schema বানিয়ে reuse করা

```js
// lib/schemas/product.schema.js
import { z } from "zod";

// এইটা common/base — create আর update দুটোতেই কাজ করবে
const baseProductSchema = z.object({
  name: z.string().min(2, "Product name দিতে হবে"),
  slug: z.string().regex(/^[a-z0-9-]+$/, "Valid slug দিন"),
  description: z.string().min(10, "কমপক্ষে ১০ অক্ষরের description দিন"),
  price: z.coerce.number().positive("Price ০ এর বেশি হতে হবে"),
  stock: z.coerce.number().int().nonnegative(),
  categoryId: z.string().min(1, "Category select করুন"),
  images: z.array(z.string().url()).min(1, "কমপক্ষে ১টা image লাগবে"),
  isFeatured: z.boolean().default(false),
});

// CREATE — সব field required (base schema-ই যথেষ্ট)
export const createProductSchema = baseProductSchema;

// UPDATE — সব field optional করে দিলাম (.partial())
export const updateProductSchema = baseProductSchema.partial();
```

**ব্যবহার:**

```jsx
// Create form
const { register } = useForm({
  resolver: zodResolver(createProductSchema),
});

// Edit/Update form
const { register } = useForm({
  resolver: zodResolver(updateProductSchema),
});
```

---

## Password-এর মতো special case (signup vs profile update)

```js
// lib/schemas/user.schema.js
import { z } from "zod";

const baseUserSchema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
});

// Signup — password required
export const signupSchema = baseUserSchema.extend({
  password: z.string().min(6, "কমপক্ষে ৬ অক্ষর লাগবে"),
});

// Profile update — password optional (change করতে চাইলে দিবে)
export const updateUserSchema = baseUserSchema.extend({
  password: z.string().min(6).optional(),
});
```

---

**সংক্ষেপে:**

- পুরোপুরি duplicate schema লেখার দরকার নেই
- একটা **base schema** বানাও, তারপর:
    - Create-এর জন্য যেভাবে আছে সেভাবেই ব্যবহার করো
    - Update-এর জন্য `.partial()` দিয়ে সব field optional করে দাও (বা `.extend()` দিয়ে আলাদা rule দাও যেখানে দরকার)

এতে duplicate code কম হয়, আর একটা field-এর rule change করলে দুই জায়গায় (create + update) manually আপডেট করতে হয় না।


------
Next.js-এ data POST করতে হলে পুরো process-টা এই ধাপগুলোতে ভাগ করা যায়:

## ধাপ ১: Package install করো

```bash
npm install react-hook-form zod @hookform/resolvers
```

## ধাপ ২: Schema বানাও (validation rule)

```js
// lib/schemas/product.schema.js
import { z } from "zod";

export const productSchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),
  price: z.coerce.number().positive("Price ঠিক দিন"),
});
```

## ধাপ ৩: Form component বানাও (RHF দিয়ে)

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { productSchema } from "@/lib/schemas/product.schema";

export default function ProductForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(productSchema),
  });

  // ধাপ ৪ এখানে যাবে (নিচে)

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Name" />
      {errors.name && <p>{errors.name.message}</p>}

      <input {...register("price")} placeholder="Price" />
      {errors.price && <p>{errors.price.message}</p>}

      <button disabled={isSubmitting}>Submit</button>
    </form>
  );
}
```

## ধাপ ৪: Submit function লেখো (API-তে POST)

```jsx
const onSubmit = async (data) => {
  try {
    const res = await fetch("https://your-backend.com/api/products/", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });

    if (!res.ok) {
      const errData = await res.json();
      console.log("Error:", errData);
      return;
    }

    const result = await res.json();
    console.log("Success:", result);
    reset();
  } catch (err) {
    console.error("Network error:", err);
  }
};
```

## ধাপ ৫: Component-টা page-এ ব্যবহার করো

```jsx
// app/products/create/page.js
import ProductForm from "@/components/ProductForm";

export default function CreateProductPage() {
  return <ProductForm />;
}
```

## ধাপ ৬: Loading এবং error state handle করো (UX ভালো করার জন্য)

- `isSubmitting` দিয়ে button disable করা (উপরের code-এ আছে)
- Backend থেকে আসা field-wise error দেখানো (optional, চাইলে দেখাতে পারি)
- Success হলে toast/message দেখানো বা redirect করা

---

**সংক্ষেপে ৬টা ধাপ:**

1. Package install
2. Zod schema বানানো
3. RHF দিয়ে form বানানো
4. `onSubmit`-এ fetch/axios দিয়ে API call
5. Component page-এ ব্যবহার
6. Loading/error/success state handle

কোনো step নিয়ে confusion থাকলে বা backend error response field-wise form-এ দেখাতে চাইলে বলো, সেটাও দেখিয়ে দিই।


----------
নিচে generic template — যেকোনো project-এ copy-paste করে apply করতে পারবে।

## সম্পূর্ণ Folder Structure

```
src/
├── app/
│   └── products/
│       └── create/
│           └── page.js          ← Step 5
│
├── components/
│   └── forms/
│       └── ProductForm.jsx      ← Step 3 + 4
│
├── lib/
│   ├── schemas/
│   │   └── product.schema.js    ← Step 2
│   │
│   └── api/
│       └── product.api.js       ← Step 4 (API call আলাদা ফাইলে, cleaner)
│
package.json                     ← Step 1
```

---

### Step 1 — Package install (`package.json` এ যোগ হবে)

```bash
npm install react-hook-form zod @hookform/resolvers
```

---

### Step 2 — Schema (`lib/schemas/product.schema.js`)

```js
import { z } from "zod";

export const productSchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),
  price: z.coerce.number().positive("Price ঠিক দিন"),
});
```

---

### Step 4 (আলাদা করে) — API call function (`lib/api/product.api.js`)

```js
export async function createProduct(data) {
  const res = await fetch("https://your-backend.com/api/products/", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });

  if (!res.ok) {
    const errData = await res.json();
    throw new Error(errData.message || "Something went wrong");
  }

  return res.json();
}
```

**কেন API call আলাদা ফাইলে রাখলাম:** এই `createProduct` function অন্য কোথাও থেকেও call করা যাবে (যেমন admin panel বা অন্য component থেকে), duplicate fetch code লিখতে হবে না।

---

### Step 3 + 4 — Form Component (`components/forms/ProductForm.jsx`)

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { productSchema } from "@/lib/schemas/product.schema";
import { createProduct } from "@/lib/api/product.api";

export default function ProductForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(productSchema),
  });

  // Step 4 — submit logic
  const onSubmit = async (data) => {
    try {
      const result = await createProduct(data);
      console.log("Success:", result);
      reset();
    } catch (err) {
      console.error(err.message);
    }
  };

  // Step 3 — UI
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Name" />
      {errors.name && <p>{errors.name.message}</p>}

      <input {...register("price")} placeholder="Price" />
      {errors.price && <p>{errors.price.message}</p>}

      <button disabled={isSubmitting}>
        {isSubmitting ? "Saving..." : "Submit"}
      </button>
    </form>
  );
}
```

---

### Step 5 — Page-এ ব্যবহার (`app/products/create/page.js`)

```jsx
import ProductForm from "@/components/forms/ProductForm";

export default function CreateProductPage() {
  return <ProductForm />;
}
```

---

### Step 6 — Loading/Error/Success (উপরে already আছে, শুধু enhance):

```jsx
const onSubmit = async (data) => {
  try {
    const result = await createProduct(data);
    alert("Product created!"); // বা toast library ব্যবহার করো
    reset();
  } catch (err) {
    alert(err.message); // বা error state এ রেখে UI-তে দেখাও
  }
};
```

---

## সংক্ষেপে mapping টেবিল

|Step|কাজ|ফাইল|
|---|---|---|
|1|Package install|`package.json`|
|2|Schema বানানো|`lib/schemas/[name].schema.js`|
|3|Form UI|`components/forms/[Name]Form.jsx`|
|4|API call + submit logic|`lib/api/[name].api.js` + component-এর `onSubmit`|
|5|Page-এ বসানো|`app/[route]/page.js`|
|6|Loading/error/success|Component-এর ভিতরেই (`isSubmitting`, try-catch)|

---

**যেকোনো নতুন entity (Category, User, Order...) এর জন্য শুধু এই ৩টা ফাইল বানালেই হবে:**

```
lib/schemas/[entity].schema.js
lib/api/[entity].api.js
components/forms/[Entity]Form.jsx
```

এই pattern একবার মুখস্থ হয়ে গেলে, যেকোনো নতুন form ৫-১০ মিনিটে বানিয়ে ফেলতে পারবে — শুধু field আর validation rule বদলাবে।



------
# 📝 Final Summary — Next.js Form Handling (RHF + Zod + API)

## কেন এগুলো লাগে

- **react-hook-form (RHF)** → form state, input tracking, submit handle করা সহজ করে
- **zod** → data validation-এর জন্য schema/rule বানানো (type check, required, format check)
- **@hookform/resolvers** → RHF আর zod-কে connect করে

## Validation-এর দুই স্তর

|জায়গা|Tool|কাজ|
|---|---|---|
|Client (Next.js)|zod + RHF|দ্রুত feedback, ভালো UX|
|Server (DRF/backend)|Serializer|আসল security check — কারণ client bypass করা যায়|

দুটোই দরকার — একটা আরেকটার replacement না।

## Schema সম্পর্কে মূল পয়েন্ট

- Schema নিজে data পাঠায় না — শুধু data validate করে (gatekeeper)
- RHF-এ `resolver: zodResolver(schema)` দিলে submit-এর সময় automatically call হয়
- প্রতিটা major form/entity-এর জন্য আলাদা schema ফাইল রাখা ভালো practice
- **Create vs Update** schema আলাদা করার দরকার নেই পুরোপুরি — base schema বানিয়ে `.partial()` বা `.extend()` দিয়ে reuse করা যায়

## Data POST করার ৬টা ধাপ + Folder Structure

```
src/
├── app/
│   └── [entity]/create/page.js     ← Step 5: page-এ বসানো
├── components/
│   └── forms/
│       └── [Entity]Form.jsx        ← Step 3+4: UI + submit logic
├── lib/
│   ├── schemas/
│   │   └── [entity].schema.js      ← Step 2: validation rule
│   └── api/
│       └── [entity].api.js         ← Step 4: API call function
```

1. Package install (`react-hook-form`, `zod`, `@hookform/resolvers`)
2. Schema বানানো (validation rule define)
3. RHF দিয়ে form component বানানো
4. `onSubmit`-এ fetch দিয়ে API call (আলাদা `api.js` ফাইলে রাখা ভালো)
5. Component page-এ ব্যবহার
6. Loading (`isSubmitting`), error, success state handle

## এই pattern reuse করার নিয়ম

নতুন যেকোনো entity (Category, Product, User...) এর জন্য শুধু ৩টা ফাইল বানালেই হয়:

```
lib/schemas/[entity].schema.js
lib/api/[entity].api.js
components/forms/[Entity]Form.jsx
```

এই workflow একবার abhyash হয়ে গেলে, নতুন form বানানো অনেক দ্রুত আর consistent হয়ে যাবে।


File/media upload একটু আলাদাভাবে handle করতে হয় কারণ JSON-এর বদলে **FormData** ব্যবহার করতে হবে। ধাপে ধাপে দেখি।

## মূল পার্থক্য: JSON vs FormData

```js
// সাধারণ data → JSON
body: JSON.stringify({ name: "Product A" })

// File থাকলে → FormData লাগবে (JSON.stringify file নিতে পারে না)
const formData = new FormData();
formData.append("name", "Product A");
formData.append("image", fileObject);
```

---

## Step 2 — Schema (file validation সহ)

```js
// lib/schemas/product.schema.js
import { z } from "zod";

const MAX_IMAGE_SIZE = 5 * 1024 * 1024; // 5MB
const MAX_VIDEO_SIZE = 50 * 1024 * 1024; // 50MB
const ACCEPTED_IMAGE_TYPES = ["image/jpeg", "image/png", "image/webp"];
const ACCEPTED_VIDEO_TYPES = ["video/mp4", "video/webm"];
const ACCEPTED_AUDIO_TYPES = ["audio/mpeg", "audio/wav"];

export const productSchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),

  image: z
    .instanceof(File, { message: "Image select করুন" })
    .refine((file) => file.size <= MAX_IMAGE_SIZE, "ছবি ৫MB এর কম হতে হবে")
    .refine((file) => ACCEPTED_IMAGE_TYPES.includes(file.type), "শুধু jpg/png/webp"),

  video: z
    .instanceof(File)
    .refine((file) => file.size <= MAX_VIDEO_SIZE, "ভিডিও ৫০MB এর কম হতে হবে")
    .refine((file) => ACCEPTED_VIDEO_TYPES.includes(file.type), "শুধু mp4/webm")
    .optional(),

  audio: z
    .instanceof(File)
    .refine((file) => ACCEPTED_AUDIO_TYPES.includes(file.type), "শুধু mp3/wav")
    .optional(),
});
```

---

## Step 4 — API call function (`lib/api/product.api.js`)

```js
export async function createProduct(formData) {
  const res = await fetch("https://your-backend.com/api/products/", {
    method: "POST",
    // ⚠️ Content-Type header দেওয়া লাগবে না — browser নিজেই বসিয়ে দেয় FormData এর জন্য
    body: formData,
  });

  if (!res.ok) {
    const errData = await res.json();
    throw new Error(errData.message || "Upload failed");
  }

  return res.json();
}
```

**⚠️ গুরুত্বপূর্ণ:** FormData পাঠানোর সময় `"Content-Type": "application/json"` header **দিও না** — browser নিজেই সঠিক `multipart/form-data` boundary সহ header বসিয়ে দেয়। manually দিলে ভেঙে যাবে।

---

## Step 3+4 — Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { productSchema } from "@/lib/schemas/product.schema";
import { createProduct } from "@/lib/api/product.api";

export default function ProductForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(productSchema),
  });

  const onSubmit = async (data) => {
    try {
      // ধাপ ১: FormData বানানো
      const formData = new FormData();
      formData.append("name", data.name);
      formData.append("image", data.image); // File object
      if (data.video) formData.append("video", data.video);
      if (data.audio) formData.append("audio", data.audio);

      // ধাপ ২: পাঠানো
      const result = await createProduct(formData);
      console.log("Success:", result);
      reset();
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Name" />
      {errors.name && <p>{errors.name.message}</p>}

      <div>
        <label>Image</label>
        <input type="file" accept="image/*" {...register("image")} />
        {errors.image && <p>{errors.image.message}</p>}
      </div>

      <div>
        <label>Video (optional)</label>
        <input type="file" accept="video/*" {...register("video")} />
        {errors.video && <p>{errors.video.message}</p>}
      </div>

      <div>
        <label>Audio (optional)</label>
        <input type="file" accept="audio/*" {...register("audio")} />
        {errors.audio && <p>{errors.audio.message}</p>}
      </div>

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

**⚠️ Note:** `register("image")` দিয়ে file input register করলে RHF ভিতরে `FileList` রাখে, single value না। তাই zod schema-তে ঠিকমতো কাজ করানোর জন্য একটু adjustment লাগে — নিচে সেটা fix করে দিচ্ছি (আসল working version):

```jsx
import { z } from "zod";

export const productSchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),
  image: z
    .any()
    .refine((files) => files?.length === 1, "Image select করুন")
    .refine((files) => files?.[0]?.size <= 5 * 1024 * 1024, "৫MB এর কম হতে হবে"),
});
```

আর submit-এ:

```jsx
const onSubmit = async (data) => {
  const formData = new FormData();
  formData.append("name", data.name);
  formData.append("image", data.image[0]); // FileList থেকে actual file নাও
  await createProduct(formData);
};
```

---

## Image preview দেখানো (optional, ভালো UX)

```jsx
import { useState } from "react";

const [preview, setPreview] = useState(null);

<input
  type="file"
  accept="image/*"
  {...register("image")}
  onChange={(e) => {
    const file = e.target.files[0];
    if (file) setPreview(URL.createObjectURL(file));
  }}
/>

{preview && <img src={preview} alt="preview" width={150} />}
```

---

## Django DRF-এর দিক থেকে (মিলিয়ে দেখার জন্য)

```python
# serializers.py
class ProductSerializer(serializers.ModelSerializer):
    image = serializers.ImageField()
    video = serializers.FileField(required=False)
    audio = serializers.FileField(required=False)

    class Meta:
        model = Product
        fields = ["name", "image", "video", "audio"]
```

DRF নিজে থেকেই `multipart/form-data` পার্স করে file গুলো `request.FILES` হিসেবে পায়, আলাদা কিছু করতে হয় না।

---

## সংক্ষেপে মূল পয়েন্ট

|জিনিস|Normal form|File upload form|
|---|---|---|
|Data format|JSON|FormData|
|Content-Type header|manually দাও|manually দিও **না**|
|Schema validation|value check|file size/type check|
|Submit data build|direct `data` পাঠাও|FormData বানিয়ে append করো|

তোমার এক্ষেত্রে multiple images (gallery) upload লাগবে কিনা, বা single image/video/audio যথেষ্ট — বললে সেই অনুযায়ী multiple file handling দেখিয়ে দিতে পারি।
দুটোই দেখাচ্ছি — single আর multiple file upload।

## ১️⃣ Single File Upload

### Schema

```js
// lib/schemas/product.schema.js
import { z } from "zod";

export const productSchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),

  image: z
    .any()
    .refine((files) => files?.length === 1, "Image select করুন")
    .refine((files) => files?.[0]?.size <= 5 * 1024 * 1024, "৫MB এর কম হতে হবে")
    .refine(
      (files) => ["image/jpeg", "image/png", "image/webp"].includes(files?.[0]?.type),
      "শুধু jpg/png/webp"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { productSchema } from "@/lib/schemas/product.schema";
import { useState } from "react";

export default function SingleImageForm() {
  const [preview, setPreview] = useState(null);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(productSchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("name", data.name);
    formData.append("image", data.image[0]); // FileList থেকে single file

    try {
      const res = await fetch("https://your-backend.com/api/products/", {
        method: "POST",
        body: formData, // Content-Type header দিও না
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreview(null);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Product Name" />
      {errors.name && <p style={{ color: "red" }}>{errors.name.message}</p>}

      <input
        type="file"
        accept="image/*"
        {...register("image")}
        onChange={(e) => {
          const file = e.target.files[0];
          if (file) setPreview(URL.createObjectURL(file));
        }}
      />
      {errors.image && <p style={{ color: "red" }}>{errors.image.message}</p>}

      {preview && <img src={preview} alt="preview" width={150} />}

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## ২️⃣ Multiple File Upload (যেমন Product Gallery — একাধিক image)

### Schema

```js
// lib/schemas/gallery.schema.js
import { z } from "zod";

const MAX_SIZE = 5 * 1024 * 1024; // 5MB per file
const ACCEPTED_TYPES = ["image/jpeg", "image/png", "image/webp"];

export const gallerySchema = z.object({
  name: z.string().min(2, "নাম দিতে হবে"),

  images: z
    .any()
    .refine((files) => files?.length >= 1, "কমপক্ষে ১টা image দিন")
    .refine((files) => files?.length <= 5, "সর্বোচ্চ ৫টা image দেওয়া যাবে")
    .refine(
      (files) => Array.from(files || []).every((file) => file.size <= MAX_SIZE),
      "প্রতিটা image ৫MB এর কম হতে হবে"
    )
    .refine(
      (files) => Array.from(files || []).every((file) => ACCEPTED_TYPES.includes(file.type)),
      "শুধু jpg/png/webp"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { gallerySchema } from "@/lib/schemas/gallery.schema";
import { useState } from "react";

export default function MultipleImageForm() {
  const [previews, setPreviews] = useState([]);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(gallerySchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("name", data.name);

    // multiple files হলে loop করে append করো
    Array.from(data.images).forEach((file) => {
      formData.append("images", file); // same key "images" বারবার — backend list হিসেবে পাবে
    });

    try {
      const res = await fetch("https://your-backend.com/api/products/gallery/", {
        method: "POST",
        body: formData,
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreviews([]);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Product Name" />
      {errors.name && <p style={{ color: "red" }}>{errors.name.message}</p>}

      <input
        type="file"
        accept="image/*"
        multiple                       // 👈 এইটাই মূল পার্থক্য single থেকে
        {...register("images")}
        onChange={(e) => {
          const files = Array.from(e.target.files);
          setPreviews(files.map((file) => URL.createObjectURL(file)));
        }}
      />
      {errors.images && <p style={{ color: "red" }}>{errors.images.message}</p>}

      <div style={{ display: "flex", gap: "8px", flexWrap: "wrap" }}>
        {previews.map((src, i) => (
          <img key={i} src={src} alt={`preview-${i}`} width={100} />
        ))}
      </div>

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## Single vs Multiple — মূল পার্থক্য টেবিল

||Single|Multiple|
|---|---|---|
|Input attribute|শুধু `type="file"`|`type="file" multiple`|
|Schema check|`files.length === 1`|`files.length >= 1 && <= max`|
|FormData append|`formData.append("image", data.image[0])`|loop দিয়ে `formData.append("images", file)` বারবার|
|Backend field|`ImageField()`|`ListField` বা custom handling|

---

## Django DRF সাইড (Multiple file handle করার জন্য)

DRF সরাসরি multiple file একটা field-এ নেয় না, view-তে হাতে handle করতে হয়:

```python
# views.py
from rest_framework.views import APIView
from rest_framework.response import Response

class ProductGalleryView(APIView):
    def post(self, request):
        name = request.data.get("name")
        images = request.FILES.getlist("images")  # 👈 getlist দিয়ে multiple file নাও

        # প্রতিটা image save করো (loop করে)
        for img in images:
            # ProductImage.objects.create(product=product, image=img)
            pass

        return Response({"message": "Uploaded", "count": len(images)})
```

**গুরুত্বপূর্ণ:** `request.FILES.get()` না, `request.FILES.getlist("images")` ব্যবহার করতে হবে multiple file পেতে।

---

## Video/Audio-এর জন্যও same pattern

Video আর audio single/multiple upload একইভাবে কাজ করবে — শুধু `accept="video/*"` বা `accept="audio/*"` আর schema-তে size/type limit বদলাবে। চাইলে video/audio-এর জন্য আলাদা করে multiple upload example ও দেখিয়ে দিতে পারি।

Video আর Audio-এর জন্য একই pattern, শুধু file type আর size limit বদলে দিলাম।

## ৩️⃣ Single Video Upload

### Schema

```js
// lib/schemas/video.schema.js
import { z } from "zod";

const MAX_VIDEO_SIZE = 50 * 1024 * 1024; // 50MB
const ACCEPTED_VIDEO_TYPES = ["video/mp4", "video/webm", "video/quicktime"];

export const videoSchema = z.object({
  title: z.string().min(2, "Title দিতে হবে"),

  video: z
    .any()
    .refine((files) => files?.length === 1, "Video select করুন")
    .refine((files) => files?.[0]?.size <= MAX_VIDEO_SIZE, "Video ৫০MB এর কম হতে হবে")
    .refine(
      (files) => ACCEPTED_VIDEO_TYPES.includes(files?.[0]?.type),
      "শুধু mp4/webm/mov"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { videoSchema } from "@/lib/schemas/video.schema";
import { useState } from "react";

export default function SingleVideoForm() {
  const [preview, setPreview] = useState(null);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(videoSchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("title", data.title);
    formData.append("video", data.video[0]);

    try {
      const res = await fetch("https://your-backend.com/api/videos/", {
        method: "POST",
        body: formData,
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreview(null);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("title")} placeholder="Video Title" />
      {errors.title && <p style={{ color: "red" }}>{errors.title.message}</p>}

      <input
        type="file"
        accept="video/*"
        {...register("video")}
        onChange={(e) => {
          const file = e.target.files[0];
          if (file) setPreview(URL.createObjectURL(file));
        }}
      />
      {errors.video && <p style={{ color: "red" }}>{errors.video.message}</p>}

      {preview && (
        <video src={preview} width={300} controls />
      )}

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## ৪️⃣ Multiple Video Upload

### Schema

```js
// lib/schemas/videoGallery.schema.js
import { z } from "zod";

const MAX_VIDEO_SIZE = 50 * 1024 * 1024;
const ACCEPTED_VIDEO_TYPES = ["video/mp4", "video/webm"];

export const videoGallerySchema = z.object({
  title: z.string().min(2, "Title দিতে হবে"),

  videos: z
    .any()
    .refine((files) => files?.length >= 1, "কমপক্ষে ১টা video দিন")
    .refine((files) => files?.length <= 3, "সর্বোচ্চ ৩টা video দেওয়া যাবে")
    .refine(
      (files) => Array.from(files || []).every((f) => f.size <= MAX_VIDEO_SIZE),
      "প্রতিটা video ৫০MB এর কম হতে হবে"
    )
    .refine(
      (files) => Array.from(files || []).every((f) => ACCEPTED_VIDEO_TYPES.includes(f.type)),
      "শুধু mp4/webm"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { videoGallerySchema } from "@/lib/schemas/videoGallery.schema";
import { useState } from "react";

export default function MultipleVideoForm() {
  const [previews, setPreviews] = useState([]);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(videoGallerySchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("title", data.title);

    Array.from(data.videos).forEach((file) => {
      formData.append("videos", file);
    });

    try {
      const res = await fetch("https://your-backend.com/api/videos/gallery/", {
        method: "POST",
        body: formData,
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreviews([]);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("title")} placeholder="Title" />
      {errors.title && <p style={{ color: "red" }}>{errors.title.message}</p>}

      <input
        type="file"
        accept="video/*"
        multiple
        {...register("videos")}
        onChange={(e) => {
          const files = Array.from(e.target.files);
          setPreviews(files.map((f) => URL.createObjectURL(f)));
        }}
      />
      {errors.videos && <p style={{ color: "red" }}>{errors.videos.message}</p>}

      <div style={{ display: "flex", gap: "8px", flexWrap: "wrap" }}>
        {previews.map((src, i) => (
          <video key={i} src={src} width={150} controls />
        ))}
      </div>

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## ৫️⃣ Single Audio Upload

### Schema

```js
// lib/schemas/audio.schema.js
import { z } from "zod";

const MAX_AUDIO_SIZE = 10 * 1024 * 1024; // 10MB
const ACCEPTED_AUDIO_TYPES = ["audio/mpeg", "audio/wav", "audio/mp3"];

export const audioSchema = z.object({
  title: z.string().min(2, "Title দিতে হবে"),

  audio: z
    .any()
    .refine((files) => files?.length === 1, "Audio select করুন")
    .refine((files) => files?.[0]?.size <= MAX_AUDIO_SIZE, "Audio ১০MB এর কম হতে হবে")
    .refine(
      (files) => ACCEPTED_AUDIO_TYPES.includes(files?.[0]?.type),
      "শুধু mp3/wav"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { audioSchema } from "@/lib/schemas/audio.schema";
import { useState } from "react";

export default function SingleAudioForm() {
  const [preview, setPreview] = useState(null);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(audioSchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("title", data.title);
    formData.append("audio", data.audio[0]);

    try {
      const res = await fetch("https://your-backend.com/api/audios/", {
        method: "POST",
        body: formData,
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreview(null);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("title")} placeholder="Audio Title" />
      {errors.title && <p style={{ color: "red" }}>{errors.title.message}</p>}

      <input
        type="file"
        accept="audio/*"
        {...register("audio")}
        onChange={(e) => {
          const file = e.target.files[0];
          if (file) setPreview(URL.createObjectURL(file));
        }}
      />
      {errors.audio && <p style={{ color: "red" }}>{errors.audio.message}</p>}

      {preview && <audio src={preview} controls />}

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## ৬️⃣ Multiple Audio Upload

### Schema

```js
// lib/schemas/audioGallery.schema.js
import { z } from "zod";

const MAX_AUDIO_SIZE = 10 * 1024 * 1024;
const ACCEPTED_AUDIO_TYPES = ["audio/mpeg", "audio/wav"];

export const audioGallerySchema = z.object({
  title: z.string().min(2, "Title দিতে হবে"),

  audios: z
    .any()
    .refine((files) => files?.length >= 1, "কমপক্ষে ১টা audio দিন")
    .refine((files) => files?.length <= 5, "সর্বোচ্চ ৫টা audio দেওয়া যাবে")
    .refine(
      (files) => Array.from(files || []).every((f) => f.size <= MAX_AUDIO_SIZE),
      "প্রতিটা audio ১০MB এর কম হতে হবে"
    )
    .refine(
      (files) => Array.from(files || []).every((f) => ACCEPTED_AUDIO_TYPES.includes(f.type)),
      "শুধু mp3/wav"
    ),
});
```

### Form Component

```jsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { audioGallerySchema } from "@/lib/schemas/audioGallery.schema";
import { useState } from "react";

export default function MultipleAudioForm() {
  const [previews, setPreviews] = useState([]);

  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({ resolver: zodResolver(audioGallerySchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("title", data.title);

    Array.from(data.audios).forEach((file) => {
      formData.append("audios", file);
    });

    try {
      const res = await fetch("https://your-backend.com/api/audios/gallery/", {
        method: "POST",
        body: formData,
      });

      if (!res.ok) throw new Error("Upload failed");

      const result = await res.json();
      console.log("Success:", result);
      reset();
      setPreviews([]);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("title")} placeholder="Title" />
      {errors.title && <p style={{ color: "red" }}>{errors.title.message}</p>}

      <input
        type="file"
        accept="audio/*"
        multiple
        {...register("audios")}
        onChange={(e) => {
          const files = Array.from(e.target.files);
          setPreviews(files.map((f) => URL.createObjectURL(f)));
        }}
      />
      {errors.audios && <p style={{ color: "red" }}>{errors.audios.message}</p>}

      <div>
        {previews.map((src, i) => (
          <audio key={i} src={src} controls style={{ display: "block", marginBottom: "8px" }} />
        ))}
      </div>

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## Django DRF সাইড — Multiple video/audio handle

```python
# views.py
class VideoGalleryView(APIView):
    def post(self, request):
        title = request.data.get("title")
        videos = request.FILES.getlist("videos")  # multiple video পাওয়ার জন্য getlist

        for video in videos:
            # VideoModel.objects.create(title=title, video=video)
            pass

        return Response({"message": "Uploaded", "count": len(videos)})
```

Audio-এর জন্যও একই pattern, শুধু field name বদলাবে (`request.FILES.getlist("audios")`)।

---

## সব মিলিয়ে প্যাটার্ন (মনে রাখার জন্য)

|Media|Single field check|Multiple field check|Preview tag|
|---|---|---|---|
|Image|`files.length === 1`|`files.length >= 1 && <= max`|`<img>`|
|Video|same|same|`<video controls>`|
|Audio|same|same|`<audio controls>`|

**সবার জন্য একই ৪টা জিনিস বদলায় শুধু:**

1. `accept="image/*"` → `video/*` → `audio/*`
2. Accepted MIME types list
3. Max size limit
4. Preview-এ কোন HTML tag ব্যবহার হবে (`img`/`video`/`audio`)

বাকি pattern (FormData বানানো, `getlist()` ব্যবহার, register/refine) সব একই থাকে। এই একটা template মুখস্থ থাকলে যেকোনো file-upload form ৫ মিনিটে বানানো যাবে।

# 📁 File Upload Form — Universal Template

## Folder Structure (যেকোনো project-এ apply করার জন্য)

```
src/
├── app/
│   └── [route]/page.js              ← Page-এ component বসানো
├── components/
│   └── forms/
│       └── [Name]UploadForm.jsx     ← Form UI + submit logic
└── lib/
    └── schemas/
        └── [name].schema.js         ← Validation rule
```

---

## 🔑 Universal Rule (সব media-তে same থাকে)

|জিনিস|Normal Form|File Upload Form|
|---|---|---|
|Data format|JSON|**FormData**|
|Header|`Content-Type: application/json`|**কিছু দিও না** (browser নিজে বসায়)|
|Submit body|`JSON.stringify(data)`|`formData` (append করা)|

---

## Step-by-Step Template (Copy-Paste Ready)

### 1️⃣ Schema (media type অনুযায়ী শুধু এই ৩টা জিনিস বদলাও)

```js
import { z } from "zod";

const MAX_SIZE = 5 * 1024 * 1024;              // ⚙️ সাইজ লিমিট বদলাও
const ACCEPTED_TYPES = ["image/jpeg", "image/png"]; // ⚙️ MIME type বদলাও

export const uploadSchema = z.object({
  title: z.string().min(2, "Title দিতে হবে"),

  // ✅ SINGLE FILE
  file: z
    .any()
    .refine((f) => f?.length === 1, "File select করুন")
    .refine((f) => f?.[0]?.size <= MAX_SIZE, "সাইজ বেশি বড়")
    .refine((f) => ACCEPTED_TYPES.includes(f?.[0]?.type), "Type সঠিক না"),

  // ✅ MULTIPLE FILE (দরকার হলে এইটা ব্যবহার করো)
  // files: z
  //   .any()
  //   .refine((f) => f?.length >= 1, "কমপক্ষে ১টা দিন")
  //   .refine((f) => f?.length <= 5, "সর্বোচ্চ ৫টা")
  //   .refine((f) => Array.from(f||[]).every(x=>x.size<=MAX_SIZE), "সাইজ বড়")
  //   .refine((f) => Array.from(f||[]).every(x=>ACCEPTED_TYPES.includes(x.type)), "Type ভুল"),
});
```

### 2️⃣ Form Component

```jsx
"use client";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { uploadSchema } from "@/lib/schemas/[name].schema";
import { useState } from "react";

export default function UploadForm() {
  const [preview, setPreview] = useState(null);
  const { register, handleSubmit, formState: { errors, isSubmitting }, reset } =
    useForm({ resolver: zodResolver(uploadSchema) });

  const onSubmit = async (data) => {
    const formData = new FormData();
    formData.append("title", data.title);
    formData.append("file", data.file[0]);          // single
    // Array.from(data.files).forEach(f => formData.append("files", f)); // multiple হলে

    try {
      const res = await fetch("https://your-backend.com/api/upload/", {
        method: "POST",
        body: formData,
      });
      if (!res.ok) throw new Error("Upload failed");
      reset();
      setPreview(null);
    } catch (err) {
      console.error(err.message);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("title")} placeholder="Title" />
      {errors.title && <p>{errors.title.message}</p>}

      <input
        type="file"
        accept="image/*"                              // ⚙️ image/*, video/*, audio/*
        // multiple                                    // ⚙️ multiple হলে uncomment
        {...register("file")}
        onChange={(e) => setPreview(URL.createObjectURL(e.target.files[0]))}
      />
      {errors.file && <p>{errors.file.message}</p>}

      {preview && <img src={preview} width={150} />}   {/* ⚙️ img/video/audio */}

      <button disabled={isSubmitting}>
        {isSubmitting ? "Uploading..." : "Submit"}
      </button>
    </form>
  );
}
```

---

## 🎛️ Media Type অনুযায়ী শুধু এই ৪টা জিনিস বদলাও

||Image|Video|Audio|
|---|---|---|---|
|`MAX_SIZE`|5MB|50MB|10MB|
|`ACCEPTED_TYPES`|jpeg, png, webp|mp4, webm|mpeg, wav|
|`accept=""`|`image/*`|`video/*`|`audio/*`|
|Preview tag|`<img>`|`<video controls>`|`<audio controls>`|

---

## 🐍 Django DRF সাইড (Backend reminder)

```python
# Single file
request.FILES.get("file")

# Multiple file — অবশ্যই getlist() ব্যবহার করবে
request.FILES.getlist("files")
```

---

## ✅ চেকলিস্ট (নতুন form বানানোর সময় মনে রাখার জন্য)

- [ ] Schema-তে `MAX_SIZE` আর `ACCEPTED_TYPES` সেট করেছি
- [ ] Single হলে `files.length === 1`, multiple হলে `>= 1 && <= max`
- [ ] Input-এ সঠিক `accept` আর দরকার হলে `multiple` attribute
- [ ] `FormData` ব্যবহার করেছি, JSON না
- [ ] `Content-Type` header **manually দিইনি**
- [ ] Single হলে `data.file[0]`, multiple হলে loop করে `append`
- [ ] Backend-এ multiple file হলে `getlist()` ব্যবহার করছি

এই একটা টেমপ্লেট save রাখলে যেকোনো image/video/audio, single/multiple upload form এই কয়েকটা জায়গা বদলিয়ে ৫ মিনিটে বানানো যাবে।


