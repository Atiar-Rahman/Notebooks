
## **What is `Supabase`?**

`Supabase` provides a set of tools to help developers manage a` backend`, including:

1. **Database** – A hosted PostgreSQL database.
    
2. **Authentication** – Pre-built user management (signup, login, OAuth).
    
3. **Realtime** – Listen to database changes in real time.
    
4. **Storage** – File storage for images, videos, and other assets.
    
5. **APIs** – Auto-generated RESTful and GraphQL APIs for your database.
    

In short, it’s a way to quickly have a **fully functional backend** without manually setting up servers, APIs, or databases.

---

## **Why use Supabase?**

- **Fast development** – Get a backend running in minutes.
    
- **SQL-based** – Full power of PostgreSQL for queries.
    
- **Open source** – You can self-host if you want.
    
- **Realtime features** – Build live apps like chat, dashboards, or notifications.
    
- **Authentication ready** – Handles users, sessions, and OAuth easily.
    
- **File storage** – Store and serve media without separate servers.
    

It’s especially useful for **web apps, mobile apps, and prototypes**, or when you want a **serverless-like setup with a real database**.

---

## **How to use Supabase**

1. **Create a project**
    
    - Go to [supabase.com](https://supabase.com/) and create a free account.
        
    - Start a new project (you get a PostgreSQL database automatically).
        
2. **Set up tables**
    
    - Use the Supabase dashboard to create tables for your data.
        
    - Example: a `users` table or a `messages` table.
        
3. **Connect your app**
    
    - Install the Supabase client in your frontend or backend:
        
        ```bash
        npm install @supabase/supabase-js
        ```
        
    - Initialize the client in your code:
        
        ```javascript
        import { createClient } from '@supabase/supabase-js'
        
        const supabaseUrl = 'https://xyzcompany.supabase.co'
        const supabaseKey = 'public-anon-key'
        const supabase = createClient(supabaseUrl, supabaseKey)
        ```
        
4. **Use APIs**
    
    - **CRUD operations**:
        
        ```javascript
        // Get all users
        const { data, error } = await supabase.from('users').select('*')
        
        // Insert a new user
        const { data, error } = await supabase.from('users').insert([{ name: 'Atiar' }])
        ```
        
    - **Authentication**:
        
        ```javascript
        const { data, error } = await supabase.auth.signUp({
          email: 'test@example.com',
          password: 'password123'
        })
        ```
        
    - **Realtime subscription**:
        
        ```javascript
        supabase
          .from('messages')
          .on('INSERT', payload => console.log('New message:', payload))
          .subscribe()
        ```
        
5. **Optional features**
    
    - File storage: `supabase.storage.from('avatars').upload(...)`
        
    - GraphQL: Automatically available for your database.
        

---

### **When to use Supabase**

- You want a **backend quickly** without server setup.
    
- You like **SQL** over NoSQL.
    
- You need **authentication, storage, or realtime features** out-of-the-box.
    
- You’re building **MVPs, dashboards, or web/mobile apps**.
    

---

1. supabase sign up
2. 