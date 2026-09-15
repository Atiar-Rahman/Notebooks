`useEffect` মূলত **কোনো component render হওয়ার পরে কোনো side effect করার জন্য** ব্যবহার করি।

সহজ ভাষায়:

> **React-এর UI render হওয়ার বাইরে কোনো কাজ করতে হলে `useEffect` ব্যবহার করি।**

## ১. API call করার জন্য

সবচেয়ে common example:

```
useEffect(() => {
  fetch("https://api.example.com/users")
    .then(res => res.json())
    .then(data => console.log(data));
}, []);
```

Component প্রথমবার render হওয়ার পরে API call হবে।

---

## ২. Component-এর বাইরে কোনো কাজ করার জন্য

যেমন browser-এর `document.title` পরিবর্তন:

```
useEffect(() => {
  document.title = `Count: ${counter}`;
}, [counter]);
```

এখন `counter` পরিবর্তন হলে page title-ও পরিবর্তন হবে।

```
counter change
      ↓
component re-render
      ↓
useEffect runs
      ↓
document.title changes
```

---

## ৩. Event listener যোগ করার জন্য

যেমন keyboard event:

```
useEffect(() => {
  const handleKeyDown = (event) => {
    console.log(event.key);
  };

  window.addEventListener("keydown", handleKeyDown);

  return () => {
    window.removeEventListener("keydown", handleKeyDown);
  };
}, []);
```

এখানে `return` অংশটা **cleanup**।

Component remove হওয়ার সময় listener-টা remove করবে।

---

# Dependency Array খুব important

`useEffect` সাধারণত এভাবে লিখি:

```
useEffect(() => {
  // কাজ
}, [dependencies]);
```

### `[]` দিলে

```
useEffect(() => {
  console.log("Hello");
}, []);
```

👉 Component **প্রথমবার mount হওয়ার পরে একবার** চলে।

---

### `[counter]` দিলে

```
useEffect(() => {
  console.log(counter);
}, [counter]);
```

👉 প্রথমবার চলবে এবং **`counter` change হলে আবার চলবে**।

---

### Dependency না দিলে

```
useEffect(() => {
  console.log("Hello");
});
```

👉 Component **প্রতিবার render হওয়ার পরে** চলবে।

এটা সাবধানে ব্যবহার করতে হয়।

---

# `useEffect` কখন ব্যবহার করব?

নিজেকে এই প্রশ্নটা করো:

> **"এই কাজটা কি React-এর render-এর বাইরে কোনো external system-এর সাথে interaction করছে?"**

যদি হ্যাঁ হয়, `useEffect` লাগতে পারে।

যেমন:

- API/fetch
- `document.title` পরিবর্তন
- `localStorage` sync
- Event listener
- Timer (`setInterval`, `setTimeout`)
- WebSocket
- Third-party library-এর সাথে interaction

### কিন্তু এগুলোর জন্য সাধারণত `useEffect` দরকার নেই:

```
const total = price * quantity;
```

অথবা:

```
const handleClick = () => {
  setCounter(counter + 1);
};
```

এগুলো normal JavaScript/React logic।

## সবচেয়ে সহজ formula

```
Render → UI তৈরি

useEffect → Render হওয়ার পরে external side effect
```

**`useState` = data/state রাখি**  
**`useContext` / `use` = shared data নিই**  
**`useEffect` = render-এর পরে side effect করি**

---
হ্যাঁ—**dependency array আর component render-এর relationship** বুঝলে `useEffect` অনেক সহজ হয়ে যাবে।

 ধরো:

```
const [count, setCount] = useState(0);

useEffect(() => {
  console.log("Effect runs");
}, [count]);
```

 এখানে `[count]` হলো **dependency**।

 ## মূল ব্যাপার

 প্রথমবার component render হলে `useEffect` **একবার run করবে**।

 তারপর React দেখবে:

 > আগের render-এর `count` আর এখনকার render-এর `count` কি আলাদা?

 ### যদি আলাদা হয় → Effect আবার run করবে

```
Initial render
count = 0
    ↓
useEffect runs

setCount(1)
    ↓
Re-render
count = 1
    ↓
আগের count (0) ≠ নতুন count (1)
    ↓
useEffect runs
```

 আবার:

```
setCount(2)
    ↓
Re-render
count = 2
    ↓
আগের count (1) ≠ নতুন count (2)
    ↓
useEffect runs
```

---

 ## কিন্তু অন্য state change করলে?

 ধরো:

```
const [count, setCount] = useState(0);
const [name, setName] = useState("Rahim");

useEffect(() => {
  console.log("Effect");
}, [count]);
```

 এখন:

```
setName("Karim")
       ↓
Component re-render
       ↓
count কিন্তু একই (0)
       ↓
useEffect run করবে না
```

 কারণ dependency শুধু `count`।

 ### তাই গুরুত্বপূর্ণ কথা:

 **Component re-render হওয়া আর `useEffect` run হওয়া একই জিনিস না।**

```
State/Props change
      ↓
Component re-render
      ↓
React dependency check করে
      ↓
Dependency change হলে → useEffect runs
Dependency change না হলে → useEffect doesn't run
```

---

 # তিনটা case মনে রাখো

 ### ১. `[]`

```
useEffect(() => {
  console.log("Effect");
}, []);
```

 Initial render-এর পরে একবার।

```
Render → Effect ✅

Re-render → Effect ❌
Re-render → Effect ❌
```

---

 ### ২. `[count]`

```
useEffect(() => {
  console.log("Effect");
}, [count]);
```

 `count` change হলে।

```
Initial render → Effect ✅

count change → Re-render → Effect ✅

name change → Re-render → Effect ❌
```

---

 ### ৩. Dependency না দিলে

```
useEffect(() => {
  console.log("Effect");
});
```

 প্রতিবার render-এর পরে।

```
Render → Effect ✅
Re-render → Effect ✅
Re-render → Effect ✅
Re-render → Effect ✅
```

---

 ## একটা real example

```
const Counter = () => {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("Rahim");

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <>
      <h1>{count}</h1>

      <button onClick={() => setCount(prev => prev + 1)}>
        Increase
      </button>

      <button onClick={() => setName("Karim")}>
        Change Name
      </button>
    </>
  );
};
```

 `Increase` চাপলে:

```
count change
 ↓
re-render
 ↓
[count] change detect
 ↓
useEffect runs
 ↓
document.title changes
```

 কিন্তু `Change Name` চাপলে:

```
name change
 ↓
re-render
 ↓
count change হয়নি
 ↓
useEffect runs না
```

 ### ⭐ একদম সহজ করে

 **Render = Component আবার execute করে UI update করা।**

 **Dependency = React-কে বলা, "এই value বদলালে আমার effect আবার চালাবে।"**

 এই concept-টা বুঝে গেলে `useEffect` অনেক সহজ হয়ে যাবে।

---
# `useEffect`-এর **cleanup** প্রথমে একটু confusing লাগে, কিন্তু একটা simple idea মনে রাখলেই হবে:

 > **`useEffect` দিয়ে কোনো কাজ শুরু করলে, সেই কাজটা component থেকে চলে যাওয়ার আগে বা আবার effect চালানোর আগে বন্ধ/পরিষ্কার করার জন্য cleanup ব্যবহার করি।**

 ## ১. Cleanup আসলে কী?

 `useEffect` থেকে একটা function `return` করলে সেটাই cleanup function।

```
useEffect(() => {
  // effect

  return () => {
    // cleanup
  };
}, []);
```

 মানে:

```
useEffect শুরু করল
      ↓
কিছু কাজ চলতে থাকল
      ↓
cleanup দরকার হলে
      ↓
return-এর ভিতরের function চলবে
```

---

 # ২. কেন cleanup দরকার?

 ধরো তুমি `setInterval()` চালালে:

```
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Hello");
  }, 1000);
}, []);
```

 এখানে প্রতি ১ সেকেন্ডে `Hello` চলতে থাকবে।

 কিন্তু component যদি screen থেকে remove হয়ে যায়, interval নিজে নিজে সবসময় পরিষ্কার হবে এমন ধরে নেওয়া ঠিক না।

 তাই cleanup:

```
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Hello");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

 এখন:

```
Component mounted
      ↓
setInterval শুরু
      ↓
1 sec → Hello
1 sec → Hello
1 sec → Hello
      ↓
Component unmounted
      ↓
cleanup
      ↓
clearInterval()
      ↓
Timer বন্ধ
```

---

 # ৩. কখন cleanup ব্যবহার করব?

 যখন `useEffect` কোনো **ongoing/external কাজ শুরু করে**, তখন cleanup সাধারণত দরকার হতে পারে।

 Common examples:

 - `setInterval`
- `setTimeout`
- `addEventListener`
- WebSocket connection
- Subscription
- Third-party library connection
- কিছু ধরনের external resource

---

 # ৪. Event Listener-এর example

 ধরো:

```
useEffect(() => {
  const handleResize = () => {
    console.log(window.innerWidth);
  };

  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

 এখানে আমরা effect-এর মধ্যে listener **add** করছি:

```
window.addEventListener("resize", handleResize);
```

 তাই cleanup-এ সেটা **remove** করছি:

```
window.removeEventListener("resize", handleResize);
```

 ### সহজ rule:

```
add → remove
start → stop
subscribe → unsubscribe
connect → disconnect
```

---

 # ৫. Dependency থাকলে cleanup কখন চলে?

 এটা খুব important।

 ধরো:

```
useEffect(() => {
  console.log("Effect");

  return () => {
    console.log("Cleanup");
  };
}, [count]);
```

 `count` change হলে কী হবে?

 অনেকে ভাবে:

```
count change
↓
effect
```

 কিন্তু আসলে:

```
count change
↓
re-render
↓
আগের effect-এর cleanup
↓
নতুন effect
```

 অর্থাৎ:

```
Old Effect
    ↓
Cleanup
    ↓
New Effect
```

---

 # ৬. Real example

```
useEffect(() => {
  const timer = setInterval(() => {
    console.log(count);
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, [count]);
```

 যখন `count = 0`:

```
Effect
 ↓
Timer-0 starts
```

 তারপর `count = 1` হলে:

```
Re-render
 ↓
Old cleanup
 ↓
Timer-0 stops
 ↓
New effect
 ↓
Timer-1 starts
```

 এটা খুব important কারণ cleanup না করলে একাধিক interval একসাথে চলতে পারে।

---

 # ৭. Component unmount হলে কী হয়?

 ধরো:

```
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

 Component screen-এ আছে:

```
Component mounted
     ↓
Effect
     ↓
Timer চলছে
```

 Component remove হলো:

```
Component unmount
     ↓
Cleanup
     ↓
clearInterval()
```

 অর্থাৎ cleanup **unmount-এর সময়ও চলে**।

---

 # ৮. API call-এ cleanup লাগবে?

 প্রতিটা API call-এর জন্য cleanup লাগবেই—এমন না।

 যেমন:

```
useEffect(() => {
  fetch("/api/users")
    .then(res => res.json())
    .then(data => setUsers(data));
}, []);
```

 এখানে সাধারণভাবে cleanup না থাকলেও হতে পারে।

 তবে request cancel করার দরকার হলে `AbortController` ব্যবহার করতে পারো:

```
useEffect(() => {
  const controller = new AbortController();

  fetch("/api/users", {
    signal: controller.signal,
  })
    .then(res => res.json())
    .then(data => setUsers(data));

  return () => {
    controller.abort();
  };
}, []);
```

 এখানে component চলে গেলে request abort করা হচ্ছে।

---

 # ৯. একটা Golden Rule ⭐

 নিজেকে শুধু এই প্রশ্নটা করো:

 > **"আমি কি `useEffect`-এর ভিতরে এমন কিছু শুরু করছি যেটা পরে বন্ধ/সরাতে হবে?"**

 যদি হ্যাঁ:

```
useEffect(() => {
  // Start

  return () => {
    // Stop / Cleanup
  };
}, []);
```

 ### যেমন:

 | Effect-এ করলাম | Cleanup-এ করব |
| --- | --- |
| `setInterval()` | `clearInterval()` |
| `setTimeout()` | `clearTimeout()` |
| `addEventListener()` | `removeEventListener()` |
| `subscribe()` | `unsubscribe()` |
| `connect()` | `disconnect()` |
| request শুরু | প্রয়োজন হলে abort |

---

 ## সবচেয়ে important concept

 `useEffect` এবং cleanup-কে একটা **room** হিসেবে ভাবো:

```
Component আসে
     ↓
Room setup → useEffect

Component থাকে
     ↓
কাজ চলতে থাকে

Component যায়
     ↓
Room পরিষ্কার → cleanup
```

 আর dependency change হলে:

```
Old setup
   ↓
Old cleanup
   ↓
New setup
```

 **তাই cleanup-এর main কাজ হলো পুরোনো effect-এর কাজ পরিষ্কার করা, যাতে memory leak, duplicate listener, multiple timer বা unwanted subscription-এর মতো সমস্যা না হয়।**

---
