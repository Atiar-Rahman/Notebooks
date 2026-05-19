Here are the most commonly used features and patterns in TypeScript that developers use daily:

---

# Most Commonly Used TypeScript Features

## 1. Basic Types

```ts
let username: string = "Alex";
let age: number = 18;
let isOnline: boolean = true;
```

Common primitive types:

- `string`
    
- `number`
    
- `boolean`
    
- `null`
    
- `undefined`
    

---

## 2. Arrays

```ts
let scores: number[] = [90, 85, 100];

let names: string[] = ["Ava", "Liam"];
```

Alternative syntax:

```ts
let items: Array<string> = ["a", "b"];
```

---

## 3. Functions

```ts
function greet(name: string): string {
  return `Hello ${name}`;
}
```

Arrow function:

```ts
const add = (a: number, b: number): number => {
  return a + b;
};
```

---

## 4. Interfaces

Used heavily in APIs, React apps, and object structures.

```ts
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "Sara",
  age: 20
};
```

---

## 5. Type Aliases

```ts
type ID = string | number;

let userId: ID = 101;
```

---

## 6. Optional Properties

```ts
interface Product {
  name: string;
  price?: number;
}
```

The `?` means optional.

---

## 7. Union Types

Very common.

```ts
let value: string | number;

value = "hello";
value = 42;
```

---

## 8. Objects

```ts
const car: {
  brand: string;
  year: number;
} = {
  brand: "Toyota",
  year: 2024
};
```

---

## 9. Classes

```ts
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet() {
    console.log(`Hi ${this.name}`);
  }
}
```

---

## 10. Generics

Super common in libraries and React.

```ts
function identity<T>(value: T): T {
  return value;
}

identity<string>("Hello");
```

---

## 11. Enums

```ts
enum Role {
  Admin,
  User,
  Guest
}

let myRole: Role = Role.Admin;
```

---

## 12. Type Assertions

```ts
let input = document.querySelector("input") as HTMLInputElement;
```

---

## 13. Async/Await

Used constantly with APIs.

```ts
async function fetchData(): Promise<void> {
  const response = await fetch("/api/data");
  const data = await response.json();

  console.log(data);
}
```

---

# Most Common Real-World Uses of TypeScript

## Frontend Development

With:

- [React](https://react.dev?utm_source=chatgpt.com)
    
- [Next.js](https://nextjs.org?utm_source=chatgpt.com)
    
- [Angular](https://angular.dev?utm_source=chatgpt.com)
    

Example:

```tsx
type Props = {
  title: string;
};

function Header({ title }: Props) {
  return <h1>{title}</h1>;
}
```

---

## Backend Development

Using:

- [Node.js](https://nodejs.org?utm_source=chatgpt.com)
    
- [Express](https://expressjs.com?utm_source=chatgpt.com)
    
- [NestJS](https://nestjs.com?utm_source=chatgpt.com)
    

---

## API Development

```ts
interface ApiResponse {
  success: boolean;
  data: string[];
}
```

---

## Large Applications

TypeScript is popular because it:

- catches bugs early
    
- improves autocomplete
    
- makes teamwork easier
    
- scales well
    

---

# Most Important Things to Learn First

If you're starting TypeScript, focus on:

1. Types
    
2. Functions
    
3. Interfaces
    
4. Arrays
    
5. Objects
    
6. Union types
    
7. Async/await
    
8. Generics
    

Those cover most real-world TypeScript code.


Yes — this is a very common React + TypeScript pattern: **fetch data from an API and store it in `useState`**.

I’ll show you the standard way step by step.

---

# 1. Basic Idea

You:

1. Call API
    
2. Store result in `useState`
    
3. Show it in UI
    

---

# 2. Example API Fetch with useState (TypeScript)

## Step 1: Define type

```ts
type User = {
  id: number;
  name: string;
  email: string;
};
```

---

## Step 2: Component with API call

```tsx
import { useEffect, useState } from "react";

type User = {
  id: number;
  name: string;
  email: string;
};

function Users() {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState<boolean>(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data: User[]) => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading...</p>;

  return (
    <div>
      {users.map((user) => (
        <div key={user.id}>
          <h3>{user.name}</h3>
          <p>{user.email}</p>
        </div>
      ))}
    </div>
  );
}

export default Users;
```

---

# 3. Same Example Using async/await (Better)

```tsx
import { useEffect, useState } from "react";

type User = {
  id: number;
  name: string;
  email: string;
};

function Users() {
  const [users, setUsers] = useState<User[]>([]);

  useEffect(() => {
    const fetchUsers = async () => {
      const res = await fetch("https://jsonplaceholder.typicode.com/users");
      const data: User[] = await res.json();
      setUsers(data);
    };

    fetchUsers();
  }, []);

  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

---

# 4. Common Pattern Summary

You always use:

### State

```ts
const [data, setData] = useState<Type[]>([]);
```

### Effect

```ts
useEffect(() => {
  fetchData();
}, []);
```

### API

```ts
fetch(url).then(res => res.json())
```

---

# 5. Real-world Upgrade (Axios)

Install:

```bash
npm install axios
```

Example:

```tsx
import axios from "axios";
import { useEffect, useState } from "react";

type User = {
  id: number;
  name: string;
};

function Users() {
  const [users, setUsers] = useState<User[]>([]);

  useEffect(() => {
    axios.get("https://jsonplaceholder.typicode.com/users")
      .then((res) => setUsers(res.data));
  }, []);

  return (
    <div>
      {users.map((u) => (
        <p key={u.id}>{u.name}</p>
      ))}
    </div>
  );
}
```

---

# If you want next step

I can show you:

- React Query (best way)
    
- Loading spinner UI
    
- Error handling pattern
    
- Real project structure (services/api folder)
    

না ✅  
`Props` নামটাই ব্যবহার করতে হবে এমন না।

তুমি যেকোনো valid নাম দিতে পারো।

---

# Example

## Using `Props`

```tsx
type Props = {
  name: string;
};

function User({ name }: Props) {
  return <h1>{name}</h1>;
}
```

---

## Using Another Name

```tsx
type UserProps = {
  name: string;
};

function User({ name }: UserProps) {
  return <h1>{name}</h1>;
}
```

✅ এটাও perfectly correct।

---

# Real Project Best Practice

Developers usually use:

```ts
type ButtonProps
type UserCardProps
type NavbarProps
```

কারণ component-specific name বেশি clear।

---

# Example

```tsx
type ButtonProps = {
  text: string;
};

function Button({ text }: ButtonProps) {
  return <button>{text}</button>;
}
```

---

# Summary

|Name|Valid|
|---|---|
|`Props`|✅|
|`UserProps`|✅|
|`ButtonProps`|✅|
|`MyCustomType`|✅|

শুধু valid TypeScript type name হলেই হবে।

হ্যাঁ ✅  
যদি তুমি `type` দিয়ে custom type বানাও, তাহলে `type` keyword লাগবেই।

Example:

```ts
type UserProps = {
  name: string;
};
```

এখানে:

- `type` = TypeScript keyword
    
- `UserProps` = তোমার type name
    

---

# Alternative আছে: interface

তুমি `interface` ও ব্যবহার করতে পারো।

```ts
interface UserProps {
  name: string;
}
```

এটাও same কাজ করে অনেক ক্ষেত্রে।

---

# Most Common

## Using type

```ts
type Props = {
  title: string;
};
```

---

## Using interface

```ts
interface Props {
  title: string;
}
```

---

# Difference (Simple)

|type|interface|
|---|---|
|বেশি flexible|object এর জন্য popular|
|union support|extend easy|
|modern projects এ বেশি used|older React projects এ common|

---

# React এ দুইটাই use হয়

Most developers use:

- `type` for props
    
- sometimes `interface`
    
