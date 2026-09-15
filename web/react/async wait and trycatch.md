# `async/await` আর `try/catch/finally` একসাথে বুঝলে API call করা অনেক সহজ হয়ে যাবে।

## 1. `async/await` কেন ব্যবহার করি?

ধরো API থেকে data আনতে হবে:

```
const response = fetch("/api/users");
```

`fetch()` সঙ্গে সঙ্গে data দেয় না। এটা একটা **Promise** দেয়।

`await` ব্যবহার করে আমরা Promise-এর result আসা পর্যন্ত অপেক্ষা করতে পারি:

```
const response = await fetch("/api/users");
```

তবে `await` ব্যবহার করতে হলে function-কে `async` করতে হয়:

```
const getUsers = async () => {
  const response = await fetch("/api/users");
};
```

সহজভাবে:

```
async → এই function-এর ভিতরে await ব্যবহার করতে পারব

await → Promise-এর result আসা পর্যন্ত অপেক্ষা করো
```

---

# 2. `try/catch` কেন?

API call fail করতে পারে।

যেমন:

- Internet নেই
- Server error
- Wrong URL
- Request fail
- JSON parsing error

তাই error handle করার জন্য:

```
try {
  // যেটা fail করতে পারে
} catch (error) {
  // error হলে এখানে আসবে
}
```

Example:

```
const getUsers = async () => {
  try {
    const response = await fetch("/api/users");

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.log(error);
  }
};
```

Flow:

```
try
 ↓
API call
 ↓
Success? ──→ data
 ↓
Error?
 ↓
catch
```

---

# 3. `finally` কেন?

`finally` **success হোক বা error হোক—দুই ক্ষেত্রেই চলবে।**

```
try {
  // কাজ
} catch (error) {
  // error
} finally {
  // সবসময় চলবে
}
```

Example:

```
const getUsers = async () => {
  try {
    const response = await fetch("/api/users");
    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.log(error);
  } finally {
    console.log("Request finished");
  }
};
```

### Success হলে:

```
try
 ↓
success
 ↓
finally
```

### Error হলে:

```
try
 ↓
error
 ↓
catch
 ↓
finally
```

---

# 4. কোথায় `finally` সবচেয়ে বেশি ব্যবহার হয়?

Loading state-এর ক্ষেত্রে খুব common।

React example:

```
const [loading, setLoading] = useState(false);
const [users, setUsers] = useState([]);
const [error, setError] = useState(null);
```

তারপর:

```
const getUsers = async () => {
  setLoading(true);

  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }

    const data = await response.json();

    setUsers(data);
  } catch (error) {
    setError(error.message);
  } finally {
    setLoading(false);
  }
};
```

এখানে `finally` খুব useful।

কারণ API success হলেও loading বন্ধ করতে হবে:

```
Success
 ↓
loading = false
```

আবার API fail হলেও loading বন্ধ করতে হবে:

```
Error
 ↓
loading = false
```

তাই:

```
finally {
  setLoading(false);
}
```

এক জায়গাতেই লিখে ফেললাম।

---

# 5. `response.ok` কেন check করি?

একটা গুরুত্বপূর্ণ ব্যাপার:

```
const response = await fetch("/api/users");
```

`fetch()` সাধারণত HTTP `404`, `500` পেলেও নিজে থেকে `catch`-এ যাবে না।

তাই:

```
if (!response.ok) {
  throw new Error("Something went wrong");
}
```

এটা করলে আমরা নিজেরাই error তৈরি করে `catch`-এ পাঠাতে পারি।

Complete pattern:

```
const getUsers = async () => {
  setLoading(true);

  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("Failed to fetch users");
    }

    const data = await response.json();

    setUsers(data);
  } catch (error) {
    setError(error.message);
  } finally {
    setLoading(false);
  }
};
```

---

# 6. `async/await` কোথায় ব্যবহার করব?

যখন কোনো কাজ **Promise-based** হয়।

Common examples:

- API request
- Database operation
- File operation
- Authentication request
- কোনো asynchronous function

যেমন:

```
const login = async () => {
  const response = await fetch("/api/login");
};
```

---

# 7. `try/catch` কোথায় ব্যবহার করব?

যেখানে error হওয়ার possibility আছে এবং তুমি error handle করতে চাও।

```
try {
  const data = await getData();
} catch (error) {
  console.log("Something went wrong");
}
```

---

# 8. `finally` কোথায় ব্যবহার করব?

যে কাজটা **success/error দুই ক্ষেত্রেই করতে হবে**, সেখানে।

সবচেয়ে common:

```
finally {
  setLoading(false);
}
```

আরও উদাহরণ:

```
try     → loading শুরু
catch   → error দেখাও
finally → loading বন্ধ
```

---

# 9. React + `useEffect`-এ খুব common pattern

API call করলে:

```
useEffect(() => {
  const getUsers = async () => {
    setLoading(true);

    try {
      const response = await fetch("/api/users");

      if (!response.ok) {
        throw new Error("Failed to fetch users");
      }

      const data = await response.json();
      setUsers(data);
    } catch (error) {
      setError(error.message);
    } finally {
      setLoading(false);
    }
  };

  getUsers();
}, []);
```

খেয়াল করো, আমরা সরাসরি এভাবে সাধারণত লিখি না:

```
useEffect(async () => {
  // ...
}, []);
```

কারণ `useEffect` callback-কে সরাসরি `async` করা উচিত নয়। বরং ভিতরে `async` function বানিয়ে call করি।

---

# সবশেষে এই pattern মুখস্থ করো

```
const someFunction = async () => {
  try {
    // 1. কাজ করো
    const response = await fetch("API");

    // 2. Error check
    if (!response.ok) {
      throw new Error("Something went wrong");
    }

    // 3. Data নাও
    const data = await response.json();

  } catch (error) {
    // 4. Error handle
    console.log(error);

  } finally {
    // 5. সবসময় চলবে
    console.log("Finished");
  }
};
```

### ⭐ এক লাইনে মনে রাখো

**`async` → function-কে asynchronous বানায়**  
**`await` → Promise-এর result-এর জন্য অপেক্ষা করে**  
**`try` → risky কাজ রাখি**  
**`catch` → error handle করি**  
**`finally` → success/error যাই হোক, শেষে যা করতেই হবে সেটা করি**



----
