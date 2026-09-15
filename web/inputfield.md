
অবশ্যই। তুমি যদি **React-এ form-এর সব common input type থেকে value কীভাবে নিতে হয়** শিখতে চাও, তাহলে একটা complete component দিয়ে দেখাই।

এখানে থাকবে:

- `text`
    
- `email`
    
- `password`
    
- `number`
    
- `date`
    
- `time`
    
- `url`
    
- `tel`
    
- `search`
    
- `checkbox`
    
- multiple checkbox
    
- `radio`
    
- `select`
    
- multiple select
    
- `textarea`
    
- `range`
    
- `file`
    
- `color`
    
- `hidden`
    

সবগুলো **ES6 + React** দিয়ে।

---

# Complete React Form

```jsx
import { useState } from "react";

function AllInputsForm() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    password: "",
    age: "",
    date: "",
    time: "",
    website: "",
    phone: "",
    search: "",
    gender: "",
    country: "",
    skills: [],
    message: "",
    range: 50,
    color: "#000000",
    file: null,
  });

  // সব input-এর জন্য common handler
  const handleChange = (e) => {
    const { name, value } = e.target;

    setFormData((prev) => ({
      ...prev,
      [name]: value,
    }));
  };

  // Checkbox-এর জন্য
  const handleCheckbox = (e) => {
    const { name, value, checked } = e.target;

    setFormData((prev) => {
      if (checked) {
        return {
          ...prev,
          [name]: [...prev[name], value],
        };
      }

      return {
        ...prev,
        [name]: prev[name].filter((item) => item !== value),
      };
    });
  };

  // File input-এর জন্য
  const handleFileChange = (e) => {
    setFormData((prev) => ({
      ...prev,
      file: e.target.files[0],
    }));
  };

  // Submit
  const handleSubmit = (e) => {
    e.preventDefault();

    console.log(formData);
  };

  return (
    <div className="max-w-xl mx-auto p-5">

      <h1 className="text-2xl font-bold mb-5">
        All Input Types
      </h1>

      <form onSubmit={handleSubmit}>

        {/* Text */}
        <div className="mb-4">
          <label>Name</label>

          <input
            type="text"
            name="name"
            value={formData.name}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Email */}
        <div className="mb-4">
          <label>Email</label>

          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Password */}
        <div className="mb-4">
          <label>Password</label>

          <input
            type="password"
            name="password"
            value={formData.password}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Number */}
        <div className="mb-4">
          <label>Age</label>

          <input
            type="number"
            name="age"
            value={formData.age}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Date */}
        <div className="mb-4">
          <label>Date</label>

          <input
            type="date"
            name="date"
            value={formData.date}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Time */}
        <div className="mb-4">
          <label>Time</label>

          <input
            type="time"
            name="time"
            value={formData.time}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* URL */}
        <div className="mb-4">
          <label>Website</label>

          <input
            type="url"
            name="website"
            value={formData.website}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Telephone */}
        <div className="mb-4">
          <label>Phone</label>

          <input
            type="tel"
            name="phone"
            value={formData.phone}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Search */}
        <div className="mb-4">
          <label>Search</label>

          <input
            type="search"
            name="search"
            value={formData.search}
            onChange={handleChange}
            className="input input-bordered w-full"
          />
        </div>


        {/* Radio */}
        <div className="mb-4">

          <label>Gender</label>

          <div>
            <label>
              <input
                type="radio"
                name="gender"
                value="male"
                checked={formData.gender === "male"}
                onChange={handleChange}
              />

              Male
            </label>
          </div>

          <div>
            <label>
              <input
                type="radio"
                name="gender"
                value="female"
                checked={formData.gender === "female"}
                onChange={handleChange}
              />

              Female
            </label>
          </div>

        </div>


        {/* Multiple Checkbox */}
        <div className="mb-4">

          <label>Skills</label>

          <div>
            <label>
              <input
                type="checkbox"
                name="skills"
                value="javascript"
                checked={formData.skills.includes("javascript")}
                onChange={handleCheckbox}
              />

              JavaScript
            </label>
          </div>

          <div>
            <label>
              <input
                type="checkbox"
                name="skills"
                value="react"
                checked={formData.skills.includes("react")}
                onChange={handleCheckbox}
              />

              React
            </label>
          </div>

          <div>
            <label>
              <input
                type="checkbox"
                name="skills"
                value="nextjs"
                checked={formData.skills.includes("nextjs")}
                onChange={handleCheckbox}
              />

              Next.js
            </label>
          </div>

        </div>


        {/* Select */}
        <div className="mb-4">

          <label>Country</label>

          <select
            name="country"
            value={formData.country}
            onChange={handleChange}
            className="select select-bordered w-full"
          >
            <option value="">Select Country</option>
            <option value="bangladesh">Bangladesh</option>
            <option value="india">India</option>
            <option value="usa">USA</option>
          </select>

        </div>


        {/* Textarea */}
        <div className="mb-4">

          <label>Message</label>

          <textarea
            name="message"
            value={formData.message}
            onChange={handleChange}
            className="textarea textarea-bordered w-full"
          />

        </div>


        {/* Range */}
        <div className="mb-4">

          <label>
            Range: {formData.range}
          </label>

          <input
            type="range"
            name="range"
            min="0"
            max="100"
            value={formData.range}
            onChange={handleChange}
            className="range"
          />

        </div>


        {/* Color */}
        <div className="mb-4">

          <label>Color</label>

          <input
            type="color"
            name="color"
            value={formData.color}
            onChange={handleChange}
          />

        </div>


        {/* File */}
        <div className="mb-4">

          <label>File</label>

          <input
            type="file"
            name="file"
            onChange={handleFileChange}
          />

        </div>


        {/* Hidden */}
        <input
          type="hidden"
          name="userId"
          value="123"
        />


        {/* Submit */}
        <button
          type="submit"
          className="btn btn-primary"
        >
          Submit
        </button>

      </form>

    </div>
  );
}

export default AllInputsForm;
```

---

# এখন সবচেয়ে important অংশ

তুমি যদি এই form submit করো:

```jsx
const handleSubmit = (e) => {
  e.preventDefault();

  console.log(formData);
};
```

তাহলে এমন object পাবে:

```js
{
  name: "Rahim",
  email: "rahim@gmail.com",
  password: "123456",
  age: "20",
  date: "2026-09-05",
  time: "10:30",
  website: "https://example.com",
  phone: "01700000000",
  search: "react",
  gender: "male",
  country: "bangladesh",
  skills: ["javascript", "react"],
  message: "Hello",
  range: "70",
  color: "#ff0000",
  file: File
}
```

---

# আসলে সব input-এর মূল নিয়ম

React form-এর ক্ষেত্রে **90% input** তুমি এই একইভাবে handle করতে পারবে:

```jsx
const handleChange = (e) => {
  const { name, value } = e.target;

  setFormData((prev) => ({
    ...prev,
    [name]: value,
  }));
};
```

তারপর input:

```jsx
<input
  type="text"
  name="name"
  value={formData.name}
  onChange={handleChange}
/>
```

আর email:

```jsx
<input
  type="email"
  name="email"
  value={formData.email}
  onChange={handleChange}
/>
```

আর number:

```jsx
<input
  type="number"
  name="age"
  value={formData.age}
  onChange={handleChange}
/>
```

**একই `handleChange`!**

কারণ এখানে:

```jsx
const { name, value } = e.target;
```

`name` বলে দেয় কোন field পরিবর্তন হয়েছে।

যেমন:

```text
name="email"
      ↓
name = "email"
      ↓
formData.email update
```

আর:

```text
name="age"
      ↓
name = "age"
      ↓
formData.age update
```

---

## কিন্তু Checkbox একটু আলাদা

Checkbox-এ:

```jsx
e.target.value
```

এর পাশাপাশি:

```jsx
e.target.checked
```

দরকার হয়।

তাই:

```jsx
const { name, value, checked } = e.target;
```

---

## Radio-ও সহজ

Radio:

```jsx
<input
  type="radio"
  name="gender"
  value="male"
  checked={formData.gender === "male"}
  onChange={handleChange}
/>
```

আর:

```jsx
<input
  type="radio"
  name="gender"
  value="female"
  checked={formData.gender === "female"}
  onChange={handleChange}
/>
```

এখানে একই `name="gender"` হওয়ায় একটাই select হবে।

---

## File আলাদা

File-এর জন্য:

```jsx
const handleFileChange = (e) => {
  setFormData((prev) => ({
    ...prev,
    file: e.target.files[0],
  }));
};
```

কারণ file পাওয়া যায়:

```js
e.target.files
```

থেকে, `e.target.value` থেকে নয়।

---

### এক লাইনে পুরো বিষয়টা মনে রাখো

```text
text/email/password/number/date/select/textarea
                    ↓
              e.target.value

checkbox
                    ↓
              e.target.checked

file
                    ↓
              e.target.files[0]
```

আর **React-এ সবচেয়ে useful pattern হলো controlled form + one common `handleChange`**। এটা ভালোভাবে বুঝে ফেললে Django API-তে form data পাঠানোও অনেক সহজ হয়ে যাবে।

---
অবশ্যই। এই ৫টা জিনিস আসলে **একই concept-এর বিভিন্ন version**। আমি একদম basic থেকে বুঝাই।

প্রথমে শুধু এই পার্থক্যটা মনে রাখো:

|Input|কতগুলো select করা যায়?|Example|
|---|--:|---|
|Checkbox|১টা বা অনেকগুলো|I agree|
|Multiple checkbox|অনেকগুলো|Skills: JS, React, Python|
|Radio|শুধু ১টা|Gender: Male/Female|
|Select|সাধারণত ১টা|Country|
|Multiple select|অনেকগুলো|Select multiple skills|

---

# 1. Checkbox কী?

Checkbox মানে একটা option **on/off** করা।

যেমন:

```text
☐ I agree to the terms
```

User click করলো:

```text
☑ I agree to the terms
```

React:

```jsx
const [agree, setAgree] = useState(false);
```

তারপর:

```jsx
<input
  type="checkbox"
  checked={agree}
  onChange={(e) => setAgree(e.target.checked)}
/>
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

```js
e.target.checked
```

এটা `true` অথবা `false` দেয়।

যেমন:

```text
unchecked → false
checked   → true
```

### Complete example

```jsx
function App() {
  const [agree, setAgree] = useState(false);

  return (
    <div>
      <label>
        <input
          type="checkbox"
          checked={agree}
          onChange={(e) => setAgree(e.target.checked)}
        />

        I agree
      </label>

      <p>
        Value: {agree.toString()}
      </p>
    </div>
  );
}
```

---

# 2. Multiple Checkbox কী?

এখন ধরো registration form-এ:

```text
Skills

☐ JavaScript
☐ React
☐ Next.js
☐ Python
```

এখানে user একাধিক select করতে পারবে।

যেমন:

```text
☑ JavaScript
☑ React
☐ Next.js
☑ Python
```

তাহলে value হবে:

```js
[
  "javascript",
  "react",
  "python"
]
```

তাই এখানে state হবে **array**:

```jsx
const [skills, setSkills] = useState([]);
```

Checkbox:

```jsx
<input
  type="checkbox"
  value="javascript"
  onChange={handleSkillChange}
/>
```

Handler:

```jsx
const handleSkillChange = (e) => {
  const { value, checked } = e.target;

  if (checked) {
    setSkills((prev) => [...prev, value]);
  } else {
    setSkills((prev) =>
      prev.filter((skill) => skill !== value)
    );
  }
};
```

### পুরো example

```jsx
import { useState } from "react";

function App() {
  const [skills, setSkills] = useState([]);

  const handleSkillChange = (e) => {
    const { value, checked } = e.target;

    if (checked) {
      setSkills((prev) => [...prev, value]);
    } else {
      setSkills((prev) =>
        prev.filter((skill) => skill !== value)
      );
    }
  };

  return (
    <div>
      <h2>Skills</h2>

      <label>
        <input
          type="checkbox"
          value="javascript"
          onChange={handleSkillChange}
        />
        JavaScript
      </label>

      <br />

      <label>
        <input
          type="checkbox"
          value="react"
          onChange={handleSkillChange}
        />
        React
      </label>

      <br />

      <label>
        <input
          type="checkbox"
          value="nextjs"
          onChange={handleSkillChange}
        />
        Next.js
      </label>

      <br />

      <label>
        <input
          type="checkbox"
          value="python"
          onChange={handleSkillChange}
        />
        Python
      </label>

      <h3>Selected:</h3>

      <pre>
        {JSON.stringify(skills, null, 2)}
      </pre>
    </div>
  );
}

export default App;
```

ধরো React + Python select করলাম:

```js
[
  "react",
  "python"
]
```

React-এ multiple checkbox-এর **মূল কথা**:

```text
Checkbox → checked?
     ↓
yes → array-তে add
no  → array থেকে remove
```

---

# 3. Radio কী?

Radio একটু আলাদা।

ধরো:

```text
Gender

○ Male
○ Female
○ Other
```

এখানে **একসাথে শুধু একটি** select করা যাবে।

React state:

```jsx
const [gender, setGender] = useState("");
```

তারপর:

```jsx
<input
  type="radio"
  name="gender"
  value="male"
  onChange={(e) => setGender(e.target.value)}
/>

<input
  type="radio"
  name="gender"
  value="female"
  onChange={(e) => setGender(e.target.value)}
/>
```

এখানে:

```js
e.target.value
```

ব্যবহার করছি।

যদি Male select করি:

```js
gender = "male"
```

Female select করলে:

```js
gender = "female"
```

### সবচেয়ে গুরুত্বপূর্ণ বিষয়

Radio button-এর `name` একই হতে হবে:

```jsx
name="gender"
```

কারণ একই `name` বলেই browser বুঝে:

> এইগুলো একই group-এর option।

তাই:

```text
○ Male
○ Female
○ Other
```

একসাথে একটাই select হবে।

---

# 4. Select কী?

Select হলো dropdown।

যেমন:

```text
Country

[ Select Country ▼ ]
```

click করলে:

```text
Bangladesh
India
Pakistan
USA
```

দেখাবে।

React:

```jsx
const [country, setCountry] = useState("");
```

তারপর:

```jsx
<select
  value={country}
  onChange={(e) => setCountry(e.target.value)}
>
  <option value="">Select Country</option>

  <option value="bangladesh">
    Bangladesh
  </option>

  <option value="india">
    India
  </option>

  <option value="usa">
    USA
  </option>
</select>
```

যদি Bangladesh select করো:

```js
country = "bangladesh"
```

এখানে আবার:

```js
e.target.value
```

ব্যবহার করছি।

---

# 5. Multiple Select কী?

এখন ধরো তুমি dropdown থেকে **একাধিক option** select করতে চাও।

যেমন:

```text
Skills

[ JavaScript     ▼ ]

☑ JavaScript
☑ React
☐ Vue
☑ Python
```

HTML-এ:

```jsx
<select multiple>
```

ব্যবহার করতে হয়।

React state হবে array:

```jsx
const [skills, setSkills] = useState([]);
```

তারপর:

```jsx
<select
  multiple
  value={skills}
  onChange={handleSkillsChange}
>
  <option value="javascript">
    JavaScript
  </option>

  <option value="react">
    React
  </option>

  <option value="vue">
    Vue
  </option>

  <option value="python">
    Python
  </option>
</select>
```

এখানে একটু difference আছে।

Multiple select-এর জন্য:

```js
e.target.value
```

দিয়ে সব selected value পাওয়া যায় না।

আমাদের `selectedOptions` ব্যবহার করতে হবে:

```jsx
const handleSkillsChange = (e) => {
  const values = Array.from(
    e.target.selectedOptions,
    (option) => option.value
  );

  setSkills(values);
};
```

এখন যদি JavaScript, React এবং Python select করো:

```js
skills = [
  "javascript",
  "react",
  "python"
];
```

---

# সবগুলো একসাথে তুলনা করো

### Checkbox

```jsx
const [agree, setAgree] = useState(false);
```

Value:

```js
true / false
```

ব্যবহার:

```text
☐ I agree
```

---

### Multiple Checkbox

```jsx
const [skills, setSkills] = useState([]);
```

Value:

```js
["react", "javascript"]
```

ব্যবহার:

```text
☑ React
☑ JavaScript
☐ Python
```

---

### Radio

```jsx
const [gender, setGender] = useState("");
```

Value:

```js
"male"
```

ব্যবহার:

```text
○ Male
○ Female
○ Other
```

**একটাই select।**

---

### Select

```jsx
const [country, setCountry] = useState("");
```

Value:

```js
"bangladesh"
```

ব্যবহার:

```text
[ Bangladesh ▼ ]
```

**একটাই select।**

---

### Multiple Select

```jsx
const [skills, setSkills] = useState([]);
```

Value:

```js
["react", "python"]
```

ব্যবহার:

```text
[ React, Python ▼ ]
```

**একাধিক select।**

---

# সবচেয়ে সহজভাবে মনে রাখো 🧠

```text
Checkbox
    ↓
true / false


Multiple Checkbox
    ↓
Array
["react", "python"]


Radio
    ↓
একটা value
"male"


Select
    ↓
একটা value
"bangladesh"


Multiple Select
    ↓
Array
["react", "python"]
```

আর value নেওয়ার নিয়ম:

```text
Checkbox
    → e.target.checked

Radio
    → e.target.value

Select
    → e.target.value

Multiple Select
    → e.target.selectedOptions
```

**এই distinction-টাই ভালোভাবে বুঝে ফেলো।** এরপর Django REST API-তে এগুলো পাঠানোর সময় কোনটা string, কোনটা boolean, কোনটা array হবে—সেটাও অনেক সহজ লাগবে।


---
হ্যাঁ, একদম **কোন input থেকে কী ধরনের value পাবে**—এটাই যদি জানতে চাও, তাহলে এই table-টা মনে রাখো:

|Input|কী value পাবে|Example|
|---|---|---|
|`text`|**string**|`"Rahim"`|
|`email`|**string**|`"rahim@gmail.com"`|
|`password`|**string**|`"123456"`|
|`number`|⚠️ **string**|`"25"`|
|`date`|**string**|`"2026-09-05"`|
|`time`|**string**|`"14:30"`|
|`url`|**string**|`"https://example.com"`|
|`tel`|**string**|`"01700000000"`|
|`search`|**string**|`"react"`|
|`textarea`|**string**|`"Hello world"`|
|`select`|**string**|`"bangladesh"`|
|`radio`|**string**|`"male"`|
|`checkbox`|**boolean**|`true` / `false`|
|multiple checkbox|**array**|`["react", "python"]`|
|multiple select|**array**|`["react", "python"]`|
|`range`|⚠️ **string**|`"50"`|
|`color`|**string**|`"#ff0000"`|
|`file`|**File object**|`File {...}`|

### সবচেয়ে important ৫টা

**1. Normal input → string**

```jsx
<input type="text" />
```

পাবে:

```js
"Rahim"
```

---

**2. Number → দেখতে number হলেও string**

```jsx
<input type="number" />
```

পাবে:

```js
"25"
```

Number দরকার হলে:

```js
Number(e.target.value)
```

তাহলে:

```js
25
```

---

**3. Checkbox → boolean**

```jsx
<input type="checkbox" />
```

পাবে:

```js
true
```

অথবা:

```js
false
```

এখানে:

```js
e.target.checked
```

---

**4. Radio → string**

```jsx
<input type="radio" name="gender" value="male" />
```

পাবে:

```js
"male"
```

---

**5. Multiple checkbox → array**

```text
☑ React
☑ Python
☐ Vue
```

পাবে:

```js
["react", "python"]
```

---

### একদম shortcut 🧠

```text
Normal input     → "value"
Number           → "25"       ← string
Radio            → "male"     ← string
Select           → "bd"       ← string

Checkbox         → true       ← boolean

Multiple checkbox
                 → ["react", "python"]

Multiple select
                 → ["react", "python"]

File             → File object
```

**একটা জিনিস বিশেষভাবে মনে রেখো:** HTML form-এর `number` input থেকে `e.target.value` নিলে JavaScript-এ সেটা **string** হয়, number না।

----
হ্যাঁ, **checkbox-এ দুটোই পাওয়া যায়**, কিন্তু দুটোর কাজ আলাদা।

### 1. `e.target.value`

Checkbox-এর `value` attribute-এর value দিবে।

```jsx
<input
  type="checkbox"
  value="react"
  onChange={(e) => console.log(e.target.value)}
/>
```

Checkbox click করলে:

```text
"react"
```

পাবে।

### 2. `e.target.checked`

Checkbox **checked আছে কিনা** সেটা দিবে।

```jsx
<input
  type="checkbox"
  value="react"
  onChange={(e) => console.log(e.target.checked)}
/>
```

Click করলে:

```text
true   // checked
false  // unchecked
```

### সহজভাবে মনে রাখো

```text
e.target.value   → checkbox-এর value কী?
e.target.checked → checkbox select করা হয়েছে কিনা?
```

যেমন:

```jsx
const handleChange = (e) => {
  console.log(e.target.value);   // "react"
  console.log(e.target.checked); // true / false
};
```

**Single checkbox** হলে সাধারণত `checked` বেশি important।

আর **multiple checkbox** হলে `value` + `checked` দুটোই লাগে:

```text
value   → কোন option? ("react")
checked → select হয়েছে? (true/false)
```

এই কারণেই multiple checkbox-এর ক্ষেত্রে `checked` দিয়ে array-তে value add/remove করি।

---
Radio button-এও `e.target.value` পাবা। এখানে **`checked` সাধারণত শুধু বোঝায় কোন radio select হয়েছে**, আর আসল selected data নিতে `value` ব্যবহার করি।

```jsx
const handleChange = (e) => {
  console.log(e.target.value);
  console.log(e.target.checked);
};

return (
  <div>
    <label>
      <input
        type="radio"
        name="gender"
        value="male"
        onChange={handleChange}
      />
      Male
    </label>

    <label>
      <input
        type="radio"
        name="gender"
        value="female"
        onChange={handleChange}
      />
      Female
    </label>
  </div>
);
```

Male select করলে:

```text
e.target.value   → "male"
e.target.checked → true
```

Female select করলে:

```text
e.target.value   → "female"
e.target.checked → true
```

### সবচেয়ে important

Radio button-এর ক্ষেত্রে:

```text
value   → কোন option select হয়েছে
checked → এই particular radio-টা selected কিনা
```

তাই React state-এ সাধারণত এভাবে রাখি:

```jsx
const [gender, setGender] = useState("");

const handleChange = (e) => {
  setGender(e.target.value);
};
```

তখন `gender` হবে:

```text
"male"
```

অথবা

```text
"female"
```

**Checkbox:** `checked` বেশি important  
**Radio:** `value` দিয়ে selected option নেওয়া হয়।

---
`select option`-এর ক্ষেত্রে মূলত **`e.target.value`** ব্যবহার করবে। এখানে `checked` লাগে না।

### Example

```jsx
const handleChange = (e) => {
  console.log(e.target.value);
};

return (
  <select name="country" onChange={handleChange}>
    <option value="">Select Country</option>
    <option value="bd">Bangladesh</option>
    <option value="in">India</option>
    <option value="us">USA</option>
  </select>
);
```

তুমি যদি **Bangladesh** select করো:

```text
e.target.value → "bd"
```

India select করলে:

```text
e.target.value → "in"
```

USA select করলে:

```text
e.target.value → "us"
```

### React state-এ

```jsx
const [country, setCountry] = useState("");

const handleChange = (e) => {
  setCountry(e.target.value);
};
```

তাহলে:

```text
country = "bd"
```

### মনে রাখার shortcut

```text
Text input       → e.target.value
Radio            → e.target.value
Select           → e.target.value
Checkbox         → e.target.checked
Multiple select  → selectedOptions থেকে array
File             → e.target.files
```

অর্থাৎ **Select → `e.target.value`** ✅

---
প্রায় ঠিক 👍 তবে React/JSX-এ এই অংশটা:

```jsx
checked="checked"
```

এভাবে না দিয়ে **boolean** হিসেবে লিখবে:

```jsx
checked={true}
```

অথবা সবসময় checked রাখতে চাইলে আরও সহজ:

```jsx
<input
  type="checkbox"
  checked
  className="checkbox border-indigo-600 bg-indigo-500 checked:border-orange-500 checked:bg-orange-400 checked:text-orange-800"
/>
```

### কিন্তু একটা গুরুত্বপূর্ণ বিষয় ⚠️

যদি তুমি checkbox-টা **user যেন click করে check/uncheck করতে পারে** এমন করতে চাও, তাহলে শুধু `checked` দিলে সমস্যা হবে। React-এ তখন `onChange` দিয়ে state control করতে হবে।

```jsx
const [checked, setChecked] = useState(false);

<input
  type="checkbox"
  checked={checked}
  onChange={(e) => setChecked(e.target.checked)}
  className="checkbox border-indigo-600 bg-indigo-500 checked:border-orange-500 checked:bg-orange-400 checked:text-orange-800"
/>
```

এখানে:

```text
checked={checked}
        ↓
true / false

onChange
   ↓
e.target.checked
   ↓
setChecked(...)
```

আর যদি **React Hook Form** ব্যবহার করো, তাহলে `checked` নিজে দেওয়ার দরকার নেই:

```jsx
<input
  type="checkbox"
  {...register("terms")}
  className="checkbox border-indigo-600 bg-indigo-500 checked:border-orange-500 checked:bg-orange-400 checked:text-orange-800"
/>
```

এটাই সবচেয়ে clean approach।

---
হ্যাঁ, **MCQ question-এর option select করার জন্য checkbox ব্যবহার করা যায়**, যদি **একাধিক answer select করা allowed** থাকে।

### Multiple correct answer হলে → Checkbox ✅

```jsx
<input
  type="checkbox"
  value="A"
/>
<span>Option A</span>

<input
  type="checkbox"
  value="B"
/>
<span>Option B</span>

<input
  type="checkbox"
  value="C"
/>
<span>Option C</span>

<input
  type="checkbox"
  value="D"
/>
<span>Option D</span>
```

ধরো user **A এবং C** select করলো:

```js
["A", "C"]
```

এখানে:

```text
value   → কোন option ("A", "B", "C"...)
checked → option select করা হয়েছে কিনা (true/false)
```

### কিন্তু Single answer MCQ হলে → Radio ✅

```jsx
<input type="radio" name="answer" value="A" />
<input type="radio" name="answer" value="B" />
<input type="radio" name="answer" value="C" />
<input type="radio" name="answer" value="D" />
```

Result:

```js
"A"
```

### তাই সহজ rule:

```text
একটাই answer        → Radio
একাধিক answer       → Checkbox
```

আর **React Hook Form দিয়ে MCQ** বানালে multiple checkbox-এর selected answers কীভাবে array হিসেবে পাবা, সেটাও খুব সহজে করা যায়।

---
হ্যাঁ, **MCQ question-এর option select করার জন্য checkbox ব্যবহার করা যায়**, যদি **একাধিক answer select করা allowed** থাকে।

### Multiple correct answer হলে → Checkbox ✅

```jsx
<input
  type="checkbox"
  value="A"
/>
<span>Option A</span>

<input
  type="checkbox"
  value="B"
/>
<span>Option B</span>

<input
  type="checkbox"
  value="C"
/>
<span>Option C</span>

<input
  type="checkbox"
  value="D"
/>
<span>Option D</span>
```

ধরো user **A এবং C** select করলো:

```js
["A", "C"]
```

এখানে:

```text
value   → কোন option ("A", "B", "C"...)
checked → option select করা হয়েছে কিনা (true/false)
```

### কিন্তু Single answer MCQ হলে → Radio ✅

```jsx
<input type="radio" name="answer" value="A" />
<input type="radio" name="answer" value="B" />
<input type="radio" name="answer" value="C" />
<input type="radio" name="answer" value="D" />
```

Result:

```js
"A"
```

### তাই সহজ rule:

```text
একটাই answer        → Radio
একাধিক answer       → Checkbox
```

আর **React Hook Form দিয়ে MCQ** বানালে multiple checkbox-এর selected answers কীভাবে array হিসেবে পাবা, সেটাও খুব সহজে করা যায়।

---
