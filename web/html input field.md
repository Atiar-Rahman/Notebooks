অবশ্যই। HTML5-এর **সব গুরুত্বপূর্ণ `<input>` field/type** নিচে example সহ দিলাম—কোনটা কী কাজে লাগে সেটাও সহজভাবে।

 ## HTML5 Input Types

 ### 1\. `text`

 সাধারণ text লেখার জন্য।

```
<label>Name:</label>
<input type="text" name="name" placeholder="Enter your name">
```

 ➡️ যেমন: `Rahim`

---

 ### 2\. `password`

 Password input নেওয়ার জন্য। লেখা `●●●●` আকারে দেখা যায়।

```
<label>Password:</label>
<input type="password" name="password" placeholder="Enter password">
```

---

 ### 3\. `email`

 Email address নেওয়ার জন্য। Browser basic email validation করতে পারে।

```
<label>Email:</label>
<input type="email" name="email" placeholder="you@example.com">
```

---

 ### 4\. `number`

 শুধু numeric value নেওয়ার জন্য।

```
<label>Age:</label>
<input type="number" name="age" min="1" max="100">
```

 `min`, `max`, `step` ব্যবহার করা যায়:

```
<input type="number" min="0" max="100" step="5">
```

---

 ### 5\. `tel`

 Phone/mobile number নেওয়ার জন্য।

```
<label>Phone:</label>
<input type="tel" name="phone" placeholder="01712345678">
```

 ⚠️ এটি নিজে থেকে phone number validate করে না; `pattern` ব্যবহার করা যায়।

---

 ### 6\. `url`

 Website URL নেওয়ার জন্য।

```
<label>Website:</label>
<input type="url" name="website" placeholder="https://example.com">
```

---

 ### 7\. `search`

 Search box তৈরির জন্য।

```
<label>Search:</label>
<input type="search" name="search" placeholder="Search here...">
```

---

 ### 8\. `date`

 শুধু date নির্বাচন করার জন্য।

```
<label>Date of Birth:</label>
<input type="date" name="dob">
```

 Browser সাধারণত calendar picker দেখায়।

---

 ### 9\. `time`

 Time নির্বাচন করার জন্য।

```
<label>Time:</label>
<input type="time" name="time">
```

 যেমন: `10:30`

---

 ### 10. `datetime-local`

 Date এবং time একসাথে নেওয়ার জন্য।

```
<label>Meeting:</label>
<input type="datetime-local" name="meeting">
```

---

 ### 11\. `month`

 Year + month নির্বাচন করার জন্য।

```
<label>Month:</label>
<input type="month" name="month">
```

 যেমন: `September 2026`

---

 ### 12. `week`

 Year-এর নির্দিষ্ট week নির্বাচন করার জন্য।

```
<label>Week:</label>
<input type="week" name="week">
```

---

 ### 13\. `color`

 Color নির্বাচন করার জন্য।

```
<label>Choose Color:</label>
<input type="color" name="color">
```

 ➡️ Browser color picker দেখাবে।

---

 ### 14\. `range`

 Slider তৈরি করার জন্য।

```
<label>Volume:</label>
<input type="range" name="volume" min="0" max="100" value="50">
```

 এখানে user slider টেনে value পরিবর্তন করতে পারে।

---

 ### 15\. `checkbox`

 এক বা একাধিক option select করার জন্য।

```
<label>
    <input type="checkbox" name="skills" value="html">
    HTML
</label>

<label>
    <input type="checkbox" name="skills" value="css">
    CSS
</label>

<label>
    <input type="checkbox" name="skills" value="javascript">
    JavaScript
</label>
```

 ➡️ একাধিক option একসাথে select করা যায়।
চেকবক্সে (Checkbox) মূল পার্থক্য হলো এটি **বুলিয়ান (Boolean)** বা **`true`/`false`** ভ্যালু ধারণ করে। এখানে মূলত একটি নির্দিষ্ট ভ্যালু (যেমন "male") এর সাথে মেলানোর দরকার হয় না, শুধুই চেক করা লাগে যে এটি সিলেক্ট করা হয়েছে কিনা।

---
হ্যাঁ, checkbox-এর **কোন value checked হয়েছে** সেটা পেতে `e.target.value` ব্যবহার করবে।

তোমার code:

```
<input
  type="checkbox"
  name="name"
  id="JS"
  value="JS"
  onChange={(e) => {
    console.log(e.target.value);
    console.log(e.target.checked);
  }}
/>

<label htmlFor="JS">JS</label>
```

এখানে:

- `e.target.value` → **কোন value** (`"JS"`)
    
- `e.target.checked` → **checked কিনা** (`true` / `false`)
    

### Example

```
function App() {
  const handleChange = (e) => {
    console.log("Value:", e.target.value);
    console.log("Checked:", e.target.checked);
  };

  return (
    <>
      <input
        type="checkbox"
        value="JS"
        onChange={handleChange}
      />
      <label>JS</label>

      <br />

      <input
        type="checkbox"
        value="React"
        onChange={handleChange}
      />
      <label>React</label>
    </>
  );
}
```

JS checkbox click করলে:

```
Value: JS
Checked: true
```

আবার uncheck করলে:

```
Value: JS
Checked: false
```

**তাই মনে রাখো:**

```
e.target.value    // কোন checkbox
e.target.checked  // checked নাকি unchecked
```

তোমার `"JS"` value পেতে অবশ্যই input-এ `value="JS"` দিতে হবে।


### ১. স্টেটের ধরন ভিন্ন
রেডিওতে তোমরা `gender` স্টেটের ভ্যালু (যেমন "male") ট্র্যাক করছ। কিন্তু চেকবক্সে সাধারণত শুধু `isChecked` নামে একটা বুলিয়ান ভ্যালু (`true` বা `false`) রাখা হয়।

### ২. `checked` প্রপার্টি ব্যবহারের নিয়ম
চেকবক্সের জন্য `checked` প্রপার্টিতে সরাসরি স্টেটের ভ্যালু (যেমন `gender === "male"`) পাশ করানোর দরকার নেই। বরং **স্টেট ভেরিয়েবলটিকেই** সরাসরি `checked` প্যাস করতে হয়।

```jsx
import { useState } from "react";

export default function CheckboxExample() {
  // চেকবক্সের জন্য সাধারণত বুলিয়ান স্টেট ব্যবহার করা হয়
  const [isAgreed, setIsAgreed] = useState(false); 

  return (
    <div>
      <h1>Terms & Conditions</h1>
      
      <div>
        {/* 
          এখানে 'checked' প্রপার্টিতে সরাসরি 'isAgreed' ভ্যালু বসাচ্ছে।
          React জানে:
          - isAgreed === true হলে বক্সে টিক থাকবে।
          - isAgreed === false হলে বক্স খালি থাকবে।
        */}
        <input
          type="checkbox"
          id="terms"
          checked={isAgreed} // এখানে তুলনা (===) লাগে না, সরাসরি স্টেট দাও
          onChange={(e) => setIsAgreed(e.target.checked)}
        />
        <label htmlFor="terms">আমি টার্মস ও কন্ডিশন পড়েছি এবং রাজি আছি</label>
      </div>

      <p>Status: {isAgreed ? "Accepted" : "Not Accepted"}</p>
    </div>
  );
}
```

### মূল পার্থক্য (রেডিও বনাম চেকবক্স)

| বৈশিষ্ট্য | রেডিও (Radio) | চেকবক্স (Checkbox) |
| :--- | :--- | :--- |
| **স্টেটের ধরন** | স্ট্রিং (যেমন: `"male"`) | বুলিয়ান (`true` / `false`) |
| **`checked` প্রপার্টি** | `checked={gender === "male"}` <br> (তুলনা করতে হয়) | `checked={isAgreed}` <br> (সরাসরি স্টেট দিলেই চলবে) |
| **ইনপুট ভ্যালু** | `e.target.value` (যেমন "male") | `e.target.checked` (`true` বা `false`) |
| **লজিক** | কোনটা সিলেক্টড তা খুঁজতে হয় | শুধুই সিলেক্টড কিনা তা দেখতে হয় |

### সারসংক্ষেপ
চেকবক্সে সিলেক্ট আছে কিনা বুঝতে হলে:
1.  স্টেটটি যেমন `true` বা `false` থাকে, সেটাই **সরাসরি** `checked` প্রপার্টিতে দাও।
2.  `onChange` এর মধ্যে `e.target.checked` ব্যবহার করো, যা তোমাকে `true` বা `false` রিটার্ন করবে।
3.  এখানে `===` দিয়ে তুলনা করার প্রয়োজন নেই।
---

 ### 16\. `radio`

 একাধিক option থেকে **একটি** নির্বাচন করার জন্য।

```
<p>Gender:</p>

<label>
    <input type="radio" name="gender" value="male">
    Male
</label>

<label>
    <input type="radio" name="gender" value="female">
    Female
</label>
```

 এখানে একই `name="gender"` দেওয়ার কারণে সাধারণত একটি option select করা যাবে।
হ্যাঁ, সঠিক। `checked` প্রপার্টি ব্যবহার করলেও শুধু `checked={true}` বা `checked={false}` দিলে সবসময় ঠিকমতো কাজ করে না। কারণ রুটিও বাক্সের মধ্যে একটার সাথে অন্যটার মান ভিন্ন (একটা `male`, অন্যটা `female`)।

সুতরাং, **যেই রুটিওটি সিলেক্ট করা আছে সেটার মান `gender` স্টেটের সাথে মিলে যাচ্ছে কিনা তা চেক (compare) করে `checked` প্রপার্টি সেট করতে হয়।**

### কেন তুলনা (Compare) করতে হয়?
আমাদের কাছে দুটি অপশন আছে:
1.  `value="male"`
2.  `value="female"`

আমাদের স্টেটে আছে `gender`।
*   যদি `gender === "male"` হয়, তবে শুধু **প্রথম** ইনপুটটিতে `checked={true}` থাকবে।
*   যদি `gender === "female"` হয়, তবে শুধু **দ্বিতীয়** ইনপুটটিতে `checked={true}` থাকবে।

তাই কোডে আমরা তুলনা করি:
*   `checked={gender === "male"}` (এটা `true` দিবে যদি `gender` এর মান "male" হয়।)
*   `checked={gender === "female"}` (এটা `true` দিবে যদি `gender` এর মান "female" হয়।)

### উদাহরণ:

```jsx
// স্টেট: "male"
const [gender, setGender] = useState("male");

// Male ইনপুট
<input 
  type="radio" 
  value="male" 
  // এখানে তুলনা: "male" === "male" -> TRUE
  checked={gender === "male"} 
  ... 
/>

// Female ইনপুট
<input 
  type="radio" 
  value="female" 
  // এখানে তুলনা: "female" === "male" -> FALSE
  checked={gender === "female"} 
  ... 
/>
```

**ফলাফল:**
*   `Male` ইনপুটটিতে `checked={true}` থাকবে (সিলেক্টড দেখাবে)।
*   `Female` ইনপুটটিতে `checked={false}` থাকবে (আনসিলেক্টড দেখাবে)।

**সারাংশ:**
হ্যাঁ, `checked` ব্যবহারের মূল উদ্দেশ্যই হলো **মান তুলনা (compare)** করা। যখন ইউজার ক্লিক করে, তখন `gender` স্টেট পরিবর্তন হয়। রি-রেন্ডার হওয়ার সময় React প্রতিটি ইনপুটের `checked` প্রপার্টি আবার তুলনা করে দেখে কোনটি `true` হওয়া উচিত।

---

 ### 17\. `file`

 Computer/device থেকে file upload করার জন্য।

```
<label>Upload CV:</label>
<input type="file" name="cv">
```

 একাধিক file:

```
<input type="file" name="files" multiple>
```

 শুধু image:

```
<input type="file" accept="image/*">
```

 শুধু PDF:

```
<input type="file" accept=".pdf">
```

---

 ### 18\. `hidden`

 User-এর কাছ থেকে hide করে কোনো value form-এর সাথে পাঠানোর জন্য।

```
<input type="hidden" name="user_id" value="12345">
```

 ➡️ Page-এ দেখা যাবে না, কিন্তু form submit হলে value পাঠানো হবে।

---

 ### 19\. `button`

 সাধারণ button তৈরি করে।

```
<input type="button" value="Click Me">
```

 JavaScript-এর সাথে:

```
<input type="button" value="Click Me" onclick="alert('Hello!')">
```

---

 ### 20\. `submit`

 Form submit করার button।

```
<input type="submit" value="Submit">
```

---

 ### 21\. `reset`

 Form-এর inputগুলো initial/default value-তে ফিরিয়ে দেয়।

```
<input type="reset" value="Reset">
```

---

 ## একসাথে একটি Complete Example

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTML5 Input Example</title>
</head>
<body>

<form>

    <label>Name:</label>
    <input type="text" name="name">

    <br><br>

    <label>Password:</label>
    <input type="password" name="password">

    <br><br>

    <label>Email:</label>
    <input type="email" name="email">

    <br><br>

    <label>Age:</label>
    <input type="number" name="age" min="1" max="100">

    <br><br>

    <label>Phone:</label>
    <input type="tel" name="phone">

    <br><br>

    <label>Website:</label>
    <input type="url" name="website">

    <br><br>

    <label>Date of Birth:</label>
    <input type="date" name="dob">

    <br><br>

    <label>Appointment Time:</label>
    <input type="time" name="time">

    <br><br>

    <label>Favorite Color:</label>
    <input type="color" name="color">

    <br><br>

    <label>Experience:</label>
    <input type="range" name="experience" min="0" max="10">

    <br><br>

    <p>Gender:</p>
    <label>
        <input type="radio" name="gender" value="male">
        Male
    </label>

    <label>
        <input type="radio" name="gender" value="female">
        Female
    </label>

    <br><br>

    <p>Skills:</p>
    <label>
        <input type="checkbox" name="skills" value="html">
        HTML
    </label>

    <label>
        <input type="checkbox" name="skills" value="css">
        CSS
    </label>

    <label>
        <input type="checkbox" name="skills" value="js">
        JavaScript
    </label>

    <br><br>

    <label>Upload Photo:</label>
    <input type="file" name="photo" accept="image/*">

    <br><br>

    <input type="submit" value="Submit">
    <input type="reset" value="Reset">

</form>

</body>
</html>
```

 ## সবচেয়ে বেশি ব্যবহৃতগুলো মনে রাখো

 | Input type | কাজ |
| --- | --- |
| `text` | সাধারণ লেখা |
| `password` | Password |
| `email` | Email |
| `number` | Number |
| `tel` | Phone |
| `url` | Website URL |
| `search` | Search box |
| `date` | Date |
| `time` | Time |
| `datetime-local` | Date + Time |
| `month` | Month |
| `week` | Week |
| `color` | Color picker |
| `range` | Slider |
| `checkbox` | Multiple selection |
| `radio` | Single selection |
| `file` | File upload |
| `hidden` | Hidden value |
| `submit` | Form submit |
| `reset` | Form reset |
| `button` | Normal button |

**একটা গুরুত্বপূর্ণ বিষয়:** `<input>`-এর `type` ছাড়াও `required`, `placeholder`, `value`, `name`, `readonly`, `disabled`, `min`, `max`, `step`, `minlength`, `maxlength`, `pattern`, `autocomplete`, `multiple`—এগুলো খুব গুরুত্বপূর্ণ **attributes**। এগুলো শিখলে HTML form অনেক ভালোভাবে বানাতে পারবে।


