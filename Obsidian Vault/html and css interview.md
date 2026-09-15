

# HTML Interview — Top 20 Questions & Answers
##### HTML কী?

Answer:
HTML-এর পূর্ণরূপ HyperText Markup Language। এটি web page-এর structure তৈরি করতে ব্যবহার করা হয়। যেমন heading, paragraph, image, link, form ইত্যাদি।

##### HTML কি Programming Language?

Answer:
না। HTML একটি markup language, programming language নয়। কারণ HTML-এ programming logic বা condition, loop ইত্যাদি থাকে না।

##### HTML5 কী?

Answer:
HTML5 হলো HTML-এর modern version। এতে semantic elements, audio, video, canvas, form improvements এবং আরও অনেক নতুন feature এসেছে।

উদাহরণ:

<header></header>
<nav></nav>
<main></main>
<section></section>
<footer></footer>

 ##### Semantic HTML কী?

Answer:
যে HTML elements তাদের content-এর meaning পরিষ্কারভাবে প্রকাশ করে, সেগুলোকে semantic elements বলে।

যেমন:

```
<header>
<nav>
<main>
<section>
<article>
<footer>
```


এগুলো SEO, accessibility এবং code readability-এর জন্য ভালো।

##### <div> এবং <span> এর মধ্যে পার্থক্য কী?

Answer:


<div> সাধারণত block-level container, আর <span> সাধারণত inline container।
<div>Hello</div>
<span>Hello</span>




div বড় section/group তৈরি করতে বেশি ব্যবহার হয়, আর span text-এর ছোট অংশ style করতে ব্যবহার করা হয়।

6. Block-level এবং Inline element কী?

Answer:

Block-level element সাধারণত নতুন line থেকে শুরু হয় এবং available width নেয়।

উদাহরণ:

<div>
<p>
<h1>
<section>


Inline element নতুন line থেকে শুরু হয় না এবং content যতটুকু জায়গা নেয় ততটুকুই নেয়।

উদাহরণ:

<span>
<a>
<strong>
<em>

7. id এবং class এর মধ্যে পার্থক্য কী?

Answer:

id সাধারণত একটি unique element identify করতে ব্যবহার করা হয়।

<div id="header"></div>


class একাধিক element-এর মধ্যে একইভাবে ব্যবহার করা যায়।

<div class="card"></div>
<div class="card"></div>


সহজভাবে:

id = unique identity
class = reusable group

8. <a> tag কী কাজে ব্যবহার করা হয়?

Answer:
<a> tag hyperlink তৈরি করতে ব্যবহার করা হয়।

<a href="https://example.com">Visit Website</a>


href attribute বলে দেয় link কোথায় যাবে।

9. <img> tag-এ alt attribute কেন ব্যবহার করা হয়?

Answer:
alt image-এর alternative text দেয়।

<img src="profile.jpg" alt="User profile picture">


Image load না হলে বা screen reader ব্যবহার করলে alt text গুরুত্বপূর্ণ।

এটি accessibility এবং SEO-এর জন্যও গুরুত্বপূর্ণ।

10. <strong> এবং <b> এর মধ্যে পার্থক্য কী?

Answer:

<b> শুধু text-কে visually bold করে।

<b>Hello</b>


<strong> text-কে strong importance হিসেবে বোঝায় এবং সাধারণত bold দেখায়।

<strong>Important</strong>


Semantic meaning-এর জন্য <strong> বেশি appropriate।

11. <em> এবং <i> এর মধ্যে পার্থক্য কী?

Answer:

<i> সাধারণত text-কে italic style দেওয়ার জন্য ব্যবহার করা হয়।

<em> text-এ emphasis বোঝায়।

Semantic meaning প্রয়োজন হলে <em> ব্যবহার করা ভালো।

12. HTML Form কী?

Answer:
User-এর কাছ থেকে data নেওয়ার জন্য HTML form ব্যবহার করা হয়।

<form>
  <input type="text">
  <input type="email">
  <button type="submit">Submit</button>
</form>


Login, registration, search ইত্যাদিতে form ব্যবহার করা হয়।

13. GET এবং POST form method-এর মধ্যে পার্থক্য কী?

Answer:

GET:

Data URL-এর মধ্যে পাঠায়
সাধারণত data retrieve করার জন্য ব্যবহার করা হয়
Sensitive data-এর জন্য উপযুক্ত নয়

POST:

Data request body-এর মধ্যে পাঠায়
সাধারণত data create/submit করার জন্য ব্যবহার করা হয়

উদাহরণ:

<form method="GET">

<form method="POST">


তবে মনে রাখতে হবে, POST নিজে থেকে data encrypted করে না। Sensitive data নিরাপদে পাঠানোর জন্য HTTPS দরকার।

14. <label> tag কেন ব্যবহার করা হয়?

Answer:
Form input-এর জন্য label দেওয়ার জন্য <label> ব্যবহার করা হয়।

<label for="email">Email</label>
<input id="email" type="email">


এটি accessibility improve করে এবং label-এ click করলে associated input focus হতে পারে।

15. HTML Attribute কী?

Answer:
Attribute element সম্পর্কে অতিরিক্ত information দেয়।

<img src="image.jpg" alt="Profile">


এখানে:

src → attribute
alt → attribute

আরও উদাহরণ:

id
class
href
src
type
disabled

16. HTML-এর meta viewport কেন ব্যবহার করা হয়?

Answer:
Responsive website-এর জন্য viewport meta tag গুরুত্বপূর্ণ।

<meta name="viewport" content="width=device-width, initial-scale=1.0">


এটি mobile device-এ webpage-এর width এবং scaling সঠিকভাবে handle করতে সাহায্য করে।

17. HTML এ Accessibility কী?

Answer:
Accessibility মানে হলো website যেন সব ধরনের user, বিশেষ করে disability থাকা user-রাও সহজে ব্যবহার করতে পারে।

উদাহরণ:

Proper <label> ব্যবহার করা
Image-এ meaningful alt দেওয়া
Semantic HTML ব্যবহার করা
Keyboard navigation support করা
প্রয়োজন অনুযায়ী ARIA ব্যবহার করা
18. HTML Entity কী?

Answer:
HTML-এ কিছু special character সরাসরি লেখা যায় না বা reserved meaning থাকতে পারে। সেগুলো লেখার জন্য HTML entities ব্যবহার করা হয়।

উদাহরণ:

&lt;   → <
&gt;   → >
&amp;  → &
&nbsp; → space

19. <script> এবং defer কী?

Answer:
<script> দিয়ে JavaScript file HTML-এর সাথে যুক্ত করা হয়।

<script src="app.js"></script>


defer দিলে browser HTML parsing চালিয়ে যেতে পারে এবং script পরে execute হয়।

<script src="app.js" defer></script>


সাধারণভাবে external script-এর ক্ষেত্রে defer page loading-এর জন্য useful।

20. SEO-এর জন্য HTML কীভাবে optimize করবে?

Answer:
SEO-এর জন্য semantic এবং meaningful HTML ব্যবহার করব।

যেমন:

Proper <title> ব্যবহার
Useful meta description
Proper heading hierarchy (h1, h2, h3)
Semantic elements ব্যবহার
Images-এ meaningful alt
Descriptive links ব্যবহার
Proper HTML structure রাখা

উদাহরণ:

<h1>Frontend Development Course</h1>

<p>Learn HTML, CSS and JavaScript.</p>

🔥 Interview-এর জন্য সবচেয়ে বেশি গুরুত্ব দাও

প্রথমে এইগুলো ভালোভাবে শিখো:

Semantic HTML
div vs span
id vs class
Block vs Inline
Forms + GET vs POST
alt attribute
Accessibility
HTML5
script + defer
SEO-friendly HTML

Tip: Interview-তে শুধু definition মুখস্থ না করে একটা ছোট example দিয়ে explain করতে পারলে answer অনেক বেশি strong হবে।

অবশ্যই। নিচে CSS-এর সবচেয়ে important 20টি interview question + সহজ Bangla answer দিলাম। এগুলো Junior/Frontend Developer interview-এর জন্য খুব গুরুত্বপূর্ণ।

CSS Interview — Top 20 Questions & Answers
1. CSS কী?

Answer:
CSS-এর পূর্ণরূপ Cascading Style Sheets। HTML-এর structure-কে style এবং layout দেওয়ার জন্য CSS ব্যবহার করা হয়।

যেমন:

h1 {
  color: blue;
  font-size: 32px;
}

2. CSS কতভাবে HTML-এ ব্যবহার করা যায়?

Answer:
৩ভাবে:

Inline CSS
Internal CSS
External CSS

External CSS সাধারণত সবচেয়ে ভালো approach।

<link rel="stylesheet" href="style.css">

3. CSS Selector কী?

Answer:
Selector দিয়ে আমরা HTML-এর কোন element-এ style apply করব সেটা select করি।

p {
  color: red;
}

.title {
  color: blue;
}

#header {
  background: black;
}


এখানে p, .title, এবং #header হলো selector।

4. class এবং id selector-এর মধ্যে পার্থক্য কী?

Answer:

class একাধিক element-এ ব্যবহার করা যায়:

.card {
  color: red;
}


id সাধারণত একটি unique element-এর জন্য:

#header {
  color: blue;
}


CSS-এ class বেশি reusable।

5. CSS Box Model কী?

Answer:
প্রতিটি HTML element-কে CSS একটি box হিসেবে বিবেচনা করে। Box Model-এর চারটি অংশ:

Content
Padding
Border
Margin

.box {
  width: 200px;
  padding: 20px;
  border: 2px solid black;
  margin: 10px;
}


Interview-এ অবশ্যই Content → Padding → Border → Margin মনে রাখবে।

6. margin এবং padding এর মধ্যে পার্থক্য কী?

Answer:

Padding হলো content এবং border-এর মধ্যকার space।

Margin হলো element-এর border-এর বাইরের space।

Margin
  ↓
┌───────────────┐
│    Border     │
│  ┌─────────┐  │
│  │ Padding │  │
│  │ Content │  │
│  └─────────┘  │
└───────────────┘


সহজভাবে:

Padding = ভিতরের space
Margin = বাইরের space

7. box-sizing: border-box কী?

Answer:
Default box-sizing হলো content-box।

border-box ব্যবহার করলে element-এর declared width এবং height-এর মধ্যে padding এবং border-ও include হয়।

* {
  box-sizing: border-box;
}


এটি responsive layout তৈরি করতে খুব useful।

8. CSS Specificity কী?

Answer:
একই element-এ একাধিক CSS rule apply হলে কোন rule বেশি priority পাবে, সেটি নির্ধারণ করতে specificity কাজ করে।

সাধারণভাবে priority:

!important
    ↓
Inline style
    ↓
ID
    ↓
Class / Attribute / Pseudo-class
    ↓
Element


যেমন:

#title {
  color: red;
}

.title {
  color: blue;
}


এখানে #title বেশি specific, তাই red হবে।

9. CSS Cascade কী?

Answer:
একই element-এর জন্য একাধিক CSS rule থাকলে browser বিভিন্ন factor দেখে final style নির্ধারণ করে। এই process-কে cascade বলা হয়।

মূল বিষয়গুলোর মধ্যে আছে:

Importance
Origin
Specificity
Source order

তাই CSS-এর নামের মধ্যে Cascading এসেছে।

10. display: block, inline, এবং inline-block কী?

Answer:

Block:

নতুন line থেকে শুরু হয়
সাধারণত available width নেয়

Inline:

নতুন line থেকে শুরু হয় না
সাধারণত width/height সরাসরি কাজ করে না

Inline-block:

একই line-এ থাকতে পারে
width এবং height দেওয়া যায়
.block {
  display: block;
}

.inline {
  display: inline;
}

.inline-block {
  display: inline-block;
}

11. Flexbox কী?

Answer:
Flexbox হলো CSS-এর একটি one-dimensional layout system। এটি row অথবা column বরাবর element arrange করতে ব্যবহার করা হয়।

.container {
  display: flex;
  justify-content: center;
  align-items: center;
}


Flexbox দিয়ে সহজে:

Horizontal alignment
Vertical alignment
Spacing
Responsive layout

করা যায়।

12. justify-content এবং align-items এর পার্থক্য কী?

Answer:
Flexbox-এ default flex-direction: row হলে:

justify-content → main axis
align-items → cross axis
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}


সহজভাবে row layout-এ মনে রাখতে পারো:

justify-content = horizontal
align-items = vertical

তবে flex-direction: column করলে axis বদলে যায়।

13. CSS Grid কী?

Answer:
CSS Grid হলো two-dimensional layout system। অর্থাৎ একইসাথে rows এবং columns নিয়ে কাজ করতে পারে।

.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}


Complex page layout-এর জন্য Grid খুব useful।

14. Flexbox এবং Grid-এর মধ্যে পার্থক্য কী?

Answer:

Flexbox:

One-dimensional
Row অথবা column
Component-level layout-এর জন্য খুব useful

Grid:

Two-dimensional
Row এবং column দুটো একসাথে
Page-level/complex layout-এর জন্য useful

সহজভাবে:

Flexbox = 1D
Grid = 2D

15. position property-এর বিভিন্ন value কী?

Answer:
প্রধান values:

position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;

static → default
relative → নিজের normal position থেকে offset করা যায়
absolute → positioned ancestor-এর relative-এ position হয়
fixed → viewport-এর relative-এ fixed থাকে
sticky → scroll করার সময় নির্দিষ্ট অবস্থানে আটকে থাকতে পারে
16. relative এবং absolute এর মধ্যে পার্থক্য কী?

Answer:

position: relative দিলে element normal document flow-এ থাকে।

.parent {
  position: relative;
}


position: absolute দিলে element normal flow থেকে বের হয়ে যায় এবং nearest positioned ancestor-এর relative-এ position হয়।

.child {
  position: absolute;
  top: 0;
  right: 0;
}


একটি common pattern:

.parent {
  position: relative;
}

.child {
  position: absolute;
}

17. Pseudo-class এবং Pseudo-element কী?

Answer:

Pseudo-class element-এর একটি state বোঝায়।

button:hover {
  background: blue;
}


এখানে :hover হলো pseudo-class।

Pseudo-element element-এর নির্দিষ্ট অংশ বা generated content style করতে পারে।

p::first-letter {
  font-size: 30px;
}


এখানে ::first-letter হলো pseudo-element।

মনে রাখবে:

: → Pseudo-class
:: → Pseudo-element

18. Responsive Web Design কী?

Answer:
যে website বিভিন্ন screen size—যেমন mobile, tablet এবং desktop—অনুযায়ী layout adjust করে, তাকে responsive website বলা হয়।

সাধারণত ব্যবহার করা হয়:

Flexible layouts
Flexbox/Grid
Media queries
Relative units

উদাহরণ:

@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}

19. px, %, em, rem, vh, vw কী?

Answer:

px → fixed CSS pixel unit
% → parent/context-এর relative
em → current element-এর font-size/context-এর relative
rem → root (html) font-size-এর relative
vh → viewport height-এর 1%
vw → viewport width-এর 1%

উদাহরণ:

.container {
  width: 80%;
  font-size: 1rem;
  min-height: 100vh;
}

20. display: none এবং visibility: hidden এর পার্থক্য কী?

Answer:

display: none করলে element layout থেকে সম্পূর্ণ remove হয়ে যায়।

.box {
  display: none;
}


visibility: hidden করলে element দেখা যায় না, কিন্তু তার জায়গা layout-এ থাকে।

.box {
  visibility: hidden;
}


সহজভাবে:

display: none → element + space দুটোই চলে যায়
visibility: hidden → element hidden, কিন্তু space থাকে

🔥 Interview-এর আগে এগুলো অবশ্যই ভালোভাবে শিখো

সবচেয়ে বেশি গুরুত্ব দাও:

Box Model
Specificity
Flexbox
Grid
Position
Responsive Design
Media Query
display
Pseudo-class / Pseudo-element
px vs % vs em vs rem
margin vs padding
relative vs absolute
Flexbox-এর justify-content vs align-items

এগুলো শুধু মুখস্থ না করে নিজে code করে practice করলে interview-এ follow-up question এলেও answer দিতে পারবে।


অবশ্যই। নিচে JavaScript-এর সবচেয়ে গুরুত্বপূর্ণ 40টি interview question + সহজ Bangla answer দিলাম। এগুলো বিশেষ করে Junior/Frontend/React Developer interview-এর জন্য গুরুত্বপূর্ণ।

JavaScript Interview — Top 40
1. JavaScript কী?

Answer:
JavaScript হলো একটি high-level, dynamically typed programming language, যা মূলত web page-এ interactivity এবং logic যোগ করতে ব্যবহার করা হয়। Browser ছাড়াও Node.js-এর মাধ্যমে server-side-এও JavaScript ব্যবহার করা যায়।

2. var, let, এবং const এর মধ্যে পার্থক্য কী?

Answer:

var → function-scoped
let → block-scoped
const → block-scoped এবং reassign করা যায় না
var a = 10;
let b = 20;
const c = 30;


Modern JavaScript-এ সাধারণত let এবং const ব্যবহার করা হয়।

3. let এবং const এর মধ্যে পার্থক্য কী?

Answer:
let variable পরে reassign করা যায়:

let age = 20;
age = 25;


const reassign করা যায় না:

const age = 20;
// age = 25; ❌


তবে const দিয়ে object/array declare করলে তার ভিতরের data পরিবর্তন করা যায়।

4. JavaScript-এর primitive data types কী কী?

Answer:
প্রধান primitive types:

String
Number
Boolean
Undefined
Null
BigInt
Symbol


Example:

let name = "Rahim";       // String
let age = 25;             // Number
let active = true;        // Boolean
let x;                    // Undefined
let y = null;             // Null

5. == এবং === এর মধ্যে পার্থক্য কী?

Answer:

== শুধু value compare করার আগে type conversion করতে পারে।

5 == "5"   // true


=== value এবং type দুটোই check করে।

5 === "5"  // false


সাধারণত === ব্যবহার করা বেশি নিরাপদ।

6. null এবং undefined এর মধ্যে পার্থক্য কী?

Answer:

undefined সাধারণত বোঝায় variable-এর value assign করা হয়নি।

let x;
console.log(x); // undefined


null সাধারণত developer ইচ্ছাকৃতভাবে "কোনো value নেই" বোঝাতে ব্যবহার করে।

let user = null;

7. Truthy এবং Falsy কী?

Answer:
JavaScript-এ কিছু value condition-এর ক্ষেত্রে false হিসেবে behave করে। এগুলো falsy।

প্রধান falsy values:

false
0
""
null
undefined
NaN


এগুলো ছাড়া বেশিরভাগ value truthy।

8. Function কী?

Answer:
Function হলো reusable code block, যা নির্দিষ্ট কাজ সম্পাদন করে।

function add(a, b) {
  return a + b;
}

console.log(add(2, 3));

9. Function declaration এবং function expression-এর পার্থক্য কী?

Answer:

Function declaration:

function greet() {
  console.log("Hello");
}


Function expression:

const greet = function () {
  console.log("Hello");
};


Function declaration সাধারণত hoisted হয়, তাই declaration-এর আগে call করা সম্ভব।

10. Arrow function কী?

Answer:
Arrow function হলো function লেখার একটি shorter syntax।

const add = (a, b) => {
  return a + b;
};


Short form:

const add = (a, b) => a + b;


Arrow function-এর নিজের this binding থাকে না।

11. Scope কী?

Answer:
Scope নির্ধারণ করে কোন জায়গা থেকে একটি variable access করা যাবে।

প্রধান scope:

Global scope
Function scope
Block scope
{
  let x = 10;
}

console.log(x); // Error


কারণ x block-এর বাইরে accessible নয়।

12. Hoisting কী?

Answer:
JavaScript execution-এর আগে কিছু declaration-এর information environment-এ প্রস্তুত করে। এই behavior-কে সাধারণভাবে hoisting বলা হয়।

console.log(x); // undefined
var x = 10;


let এবং const declaration hoisted হলেও initialization-এর আগে access করলে ReferenceError হয়, কারণ তারা Temporal Dead Zone (TDZ)-এ থাকে।

13. Temporal Dead Zone (TDZ) কী?

Answer:
let বা const variable declare হওয়ার আগে থেকে initialization পর্যন্ত যে সময়টাতে variable access করা যায় না, সেটাই Temporal Dead Zone।

console.log(name); // ReferenceError

let name = "Rahim";

14. Closure কী?

Answer:
যখন একটি inner function তার outer function-এর variables-কে মনে রাখতে এবং access করতে পারে, তখন তাকে closure বলা হয়।

function outer() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = outer();

console.log(counter()); // 1
console.log(counter()); // 2


এখানে inner function count variable-কে মনে রাখছে।

15. Callback function কী?

Answer:
যে function-কে অন্য function-এর argument হিসেবে পাঠানো হয় এবং পরে execute করা হয়, তাকে callback function বলে।

function greet(name, callback) {
  callback(name);
}

greet("Rahim", function (name) {
  console.log("Hello", name);
});

16. Higher-order function কী?

Answer:
যে function: অন্য function-কে argument হিসেবে নেয়, অথবা function return করে তাকে Higher-Order Function বলে।

map(), filter(), reduce() এর common examples।

17. map() কী?

Answer:
map() array-এর প্রতিটি element-এর উপর operation চালিয়ে নতুন array return করে।

const numbers = [1, 2, 3];

const result = numbers.map(num => num * 2);

console.log(result);
// [2, 4, 6]

18. filter() কী?

Answer:
filter() condition অনুযায়ী elements select করে এবং নতুন array return করে।

const numbers = [1, 2, 3, 4];

const result = numbers.filter(num => num > 2);

console.log(result);
// [3, 4]

19. map() এবং forEach() এর পার্থক্য কী?

Answer:

map() একটি নতুন array return করে।

const result = numbers.map(x => x * 2);


forEach() সাধারণত শুধু প্রতিটি item-এর উপর কাজ চালায় এবং নতুন array return করে না।

numbers.forEach(x => {
  console.log(x);
});

20. reduce() কী?

Answer:
reduce() array-এর অনেকগুলো value থেকে একটি final value তৈরি করতে ব্যবহার করা হয়।

const numbers = [1, 2, 3, 4];

const sum = numbers.reduce(
  (total, num) => total + num,
  0
);

console.log(sum); // 10

21. Spread operator (...) কী?

Answer:
Spread operator array/object-এর values expand বা copy করতে ব্যবহার করা হয়।

const a = [1, 2];
const b = [...a, 3, 4];

console.log(b);
// [1, 2, 3, 4]


Object-এর ক্ষেত্রেও:

const user = { name: "Rahim" };

const newUser = {
  ...user,
  age: 25
};

22. Rest operator (...) কী?

Answer:
Rest operator multiple values-কে একটি array বা parameter collection হিসেবে collect করে।

function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}

sum(1, 2, 3, 4);


Spread = expand
Rest = collect

23. Destructuring কী?

Answer:
Array বা object থেকে সহজে value বের করার syntax হলো destructuring।

Object:

const user = {
  name: "Rahim",
  age: 25
};

const { name, age } = user;


Array:

const numbers = [10, 20];

const [a, b] = numbers;

24. Synchronous এবং Asynchronous JavaScript কী?

Answer:

Synchronous: Code একটার পর একটা execute হয়।

Asynchronous: কিছু কাজ background-এ অপেক্ষা করতে পারে, আর JavaScript meanwhile অন্য কাজ চালাতে পারে।

যেমন:

setTimeout(() => {
  console.log("Done");
}, 2000);

console.log("Hello");


Output:

Hello
Done

25. Promise কী?

Answer:
Promise হলো asynchronous operation-এর eventual result represent করার একটি object।

Promise-এর তিনটি state:

Pending
Fulfilled
Rejected


Example:

const promise = fetch("/api/users");

promise
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.log(error));

26. async/await কী?

Answer:
async/await Promise-based asynchronous code সহজ এবং readableভাবে লেখার syntax।

async function getUsers() {
  try {
    const response = await fetch("/api/users");
    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.log(error);
  }
}

27. try...catch কী কাজে ব্যবহার করা হয়?

Answer:
Runtime error handle করার জন্য try...catch ব্যবহার করা হয়।

try {
  const result = riskyFunction();
} catch (error) {
  console.log(error);
}

28. Event bubbling কী?

Answer:
যখন কোনো child element-এ event ঘটে এবং event তার parent elements-এর দিকে propagate করে, তাকে event bubbling বলে।

Child
  ↑
Parent
  ↑
Grandparent

29. Event delegation কী?

Answer:
অনেকগুলো child element-এ আলাদা event listener না দিয়ে parent element-এ একটি listener ব্যবহার করে event handle করাকে event delegation বলে।

এটি event bubbling-এর সুবিধা নেয়।

list.addEventListener("click", (event) => {
  if (event.target.matches("button")) {
    console.log("Button clicked");
  }
});

30. this keyword কী?

Answer:
this সাধারণভাবে current execution context-এর object-কে refer করে। এর value কীভাবে function call করা হয়েছে তার উপর নির্ভর করে।

Object method:

const user = {
  name: "Rahim",

  greet() {
    console.log(this.name);
  }
};

user.greet();


এখানে this হলো user object।

Arrow function-এর নিজের this নেই; এটি surrounding lexical this ব্যবহার করে।

31. call(), apply(), এবং bind() কী?

Answer:
এগুলো দিয়ে function-এর this context control করা যায়।

function greet(city) {
  console.log(this.name, city);
}

const user = { name: "Rahim" };

greet.call(user, "Dhaka");
greet.apply(user, ["Dhaka"]);

const fn = greet.bind(user);
fn("Dhaka");


পার্থক্য:

call() → arguments আলাদাভাবে নেয়
apply() → arguments array হিসেবে নেয়
bind() → নতুন function return করে
32. Shallow copy এবং Deep copy কী?

Answer:

Shallow copy করলে nested object-এর reference shared থাকতে পারে।

const copy = { ...user };


Deep copy করলে nested data-ও আলাদাভাবে copy করা হয়।

Modern JavaScript-এ:

const copy = structuredClone(user);

33. JavaScript-এ object এবং reference কীভাবে কাজ করে?

Answer:
Object variable-এ object-এর reference থাকে। তাই দুইটি variable একই object reference করতে পারে।

const user1 = { name: "Rahim" };
const user2 = user1;

user2.name = "Karim";

console.log(user1.name);
// Karim


কারণ user1 এবং user2 একই object-এর reference ধরে রেখেছে।

34. DOM কী?

Answer:
DOM-এর পূর্ণরূপ Document Object Model। Browser HTML document-কে একটি object/tree structure হিসেবে তৈরি করে, যাতে JavaScript দিয়ে HTML elements access এবং modify করা যায়।

document.getElementById("title").textContent = "Hello";

35. localStorage এবং sessionStorage এর পার্থক্য কী?

Answer:

localStorage:

Browser-এ data store করে
সাধারণত browser বন্ধ করলেও data থাকে

sessionStorage:

Current browser tab/session-এর জন্য data রাখে
Tab বন্ধ হলে সাধারণত data চলে যায়
localStorage.setItem("name", "Rahim");

const name = localStorage.getItem("name");


দুটোতেই data সাধারণত string হিসেবে store হয়।

36. JSON.stringify() এবং JSON.parse() কী?

Answer:

JSON.stringify() → JavaScript object-কে JSON string-এ convert করে।

const user = { name: "Rahim" };

const json = JSON.stringify(user);


JSON.parse() → JSON string-কে JavaScript object-এ convert করে।

const user = JSON.parse(json);

37. Debouncing কী?

Answer:
কোনো function বারবার খুব দ্রুত call হলে, কিছু সময় অপেক্ষা করে শেষ call-টি execute করাকে debouncing বলে।

যেমন search input:

User types:
H → He → Hel → Hell → Hello

API call শুধু "Hello" লেখার পর হবে।


Search box, autocomplete ইত্যাদিতে debounce useful।

38. Throttling কী?

Answer:
কোনো function বারবার call হলেও নির্দিষ্ট সময়ের মধ্যে সীমিত সংখ্যকবার execute করাকে throttling বলে।

যেমন:

Scroll event
Mouse movement
Window resize

সহজভাবে:

Debounce → শেষের call-এর পর execute
Throttle → নির্দিষ্ট interval-এ execute

39. Event loop কী?

Answer:
JavaScript-এর asynchronous কাজগুলো কীভাবে execute হবে, সেটা manage করার mechanism-এর গুরুত্বপূর্ণ অংশ হলো event loop।

সহজভাবে:

Call Stack
    ↓
Web APIs / Async tasks
    ↓
Callback / Microtask Queue
    ↓
Event Loop
    ↓
Call Stack


JavaScript মূলত single-threaded হলেও event loop-এর মাধ্যমে asynchronous operations handle করতে পারে।

40. Promise.all() কী?

Answer:
একাধিক Promise একসাথে চালিয়ে সবগুলো complete হওয়ার জন্য অপেক্ষা করতে Promise.all() ব্যবহার করা হয়।

const [users, posts] = await Promise.all([
  fetch("/api/users"),
  fetch("/api/posts")
]);


যদি সব Promise fulfill হয়, result পাওয়া যাবে। কিন্তু কোনো একটি Promise reject করলে Promise.all() reject করবে।

🔥 সবচেয়ে বেশি গুরুত্ব দিয়ে এগুলো পড়ো

যদি interview-এর আগে সময় কম থাকে, এই 15টা অবশ্যই ভালোভাবে শিখবে:

var vs let vs const
== vs ===
Scope
Hoisting
Closure
this
Arrow function
Callback
map vs forEach
filter এবং reduce
Promise
async/await
Event bubbling/delegation
Spread/Rest + Destructuring
Event loop

React interview-এর জন্য বিশেষভাবে: closure, this, array methods, destructuring, spread operator, promise, async/await, event loop এবং immutability ভালোভাবে বুঝে রাখো। এগুলো থেকে React-এর follow-up question আসার সম্ভাবনা বেশি।



অবশ্যই। নিচে React-এর সবচেয়ে important 20টি interview question + সহজ Bangla answer দিলাম। এগুলো বিশেষ করে Junior/Frontend React Developer interview-এর জন্য খুব গুরুত্বপূর্ণ।

React Interview — Top 20
1. React কী?

Answer:
React হলো একটি JavaScript library যা user interface তৈরি করার জন্য ব্যবহার করা হয়। এটি component-based architecture ব্যবহার করে এবং UI efficiently update করার জন্য virtual DOM-এর মতো mechanisms ব্যবহার করে।

2. React-এর প্রধান সুবিধাগুলো কী?

Answer:

React-এর গুরুত্বপূর্ণ সুবিধা:

Component-based architecture
Reusable components
Declarative UI
Efficient UI updates
Large ecosystem
State management-এর সুবিধা
SPA তৈরি করা সহজ
3. Component কী?

Answer:
Component হলো UI-এর একটি reusable এবং independent অংশ।

উদাহরণ:

function Button() {
  return <button>Click Me</button>;
}


এখানে Button একটি component।

Component-এর মাধ্যমে বড় UI-কে ছোট ছোট reusable অংশে ভাগ করা যায়।

4. Props কী?

Answer:
Props হলো parent component থেকে child component-এ data পাঠানোর উপায়।

function User({ name }) {
  return <h2>{name}</h2>;
}

function App() {
  return <User name="Rahim" />;
}


এখানে name হলো prop।

মনে রাখবে: Props সাধারণত read-only।

5. State কী?

Answer:
State হলো component-এর নিজস্ব data, যার পরিবর্তনের সাথে UI update হতে পারে।

const [count, setCount] = useState(0);


এখানে count হলো state এবং setCount দিয়ে state update করা হয়।

6. Props এবং State-এর মধ্যে পার্থক্য কী?

Answer:

Props	State
Parent থেকে আসে	Component-এর নিজস্ব
Read-only হিসেবে ব্যবহার করা হয়	Setter দিয়ে update করা যায়
Component-এর বাইরে থেকে data আসে	Component-এর ভিতরে manage হয়
Child component-কে data পাঠাতে ব্যবহৃত হয়	Dynamic data manage করতে ব্যবহৃত হয়

সহজভাবে:

Props = বাইরে থেকে পাওয়া data
State = component-এর নিজের managed data

7. useState কী?

Answer:
useState হলো একটি React Hook, যা functional component-এ state manage করতে ব্যবহার করা হয়।

const [count, setCount] = useState(0);

function increment() {
  setCount(count + 1);
}


State update হলে React প্রয়োজন অনুযায়ী component re-render করে।

8. useEffect কী?

Answer:
useEffect component-এর side effects handle করতে ব্যবহার করা হয়।

যেমন:

API call
Event listener
Timer
Subscription
External system-এর সাথে synchronization
useEffect(() => {
  fetch("/api/users");
}, []);

9. useEffect-এর dependency array কী?

Answer:
Dependency array বলে দেয় কোন value পরিবর্তন হলে effect আবার run করবে।

useEffect(() => {
  console.log("Effect runs");
}, [count]);


এখানে count পরিবর্তন হলে effect run করবে।

আর:

useEffect(() => {
  console.log("Runs after initial mount");
}, []);


Empty dependency array থাকলে সাধারণভাবে effect initial mount-এর পরে একবার run করে।

10. Virtual DOM কী?

Answer:
Virtual DOM হলো UI-এর একটি in-memory representation। React state/props পরিবর্তনের পর নতুন UI representation তৈরি করে এবং আগেরটার সাথে তুলনা করে প্রয়োজনীয় DOM updates করে।

এর ফলে পুরো page নতুন করে manually update না করেও UI efficiently update করা যায়।

11. React-এ key কেন ব্যবহার করা হয়?

Answer:
List render করার সময় React-কে প্রতিটি item identify এবং track করতে key ব্যবহার করা হয়।

users.map(user => (
  <div key={user.id}>
    {user.name}
  </div>
))


key ideally unique এবং stable হওয়া উচিত।

যেমন user.id ভালো key।

12. Controlled এবং Uncontrolled component কী?

Answer:

Controlled: Input-এর value React state দ্বারা control হয়।

const [name, setName] = useState("");

<input
  value={name}
  onChange={e => setName(e.target.value)}
/>


Uncontrolled: Input-এর value DOM নিজে manage করে এবং সাধারণত ref দিয়ে access করা হয়।

const inputRef = useRef();

<input ref={inputRef} />

13. React Hooks কী?

Answer:
Hooks হলো React-এর functions, যেগুলো functional component-এর মধ্যে state, effects, context ইত্যাদি React features ব্যবহার করতে দেয়।

Common Hooks:

useState
useEffect
useContext
useRef
useMemo
useCallback

14. Rules of Hooks কী?

Answer:
দুটি প্রধান rule:

Hooks top level-এ call করতে হবে।
Hooks শুধুমাত্র React function component বা custom Hook-এর ভিতরে call করতে হবে।

এভাবে করা উচিত নয়:

if (condition) {
  useState(0); // ❌
}

15. useRef কী?

Answer:
useRef এমন একটি mutable value রাখতে পারে যার পরিবর্তনে সাধারণত component re-render হয় না।

DOM element access করতেও এটি ব্যবহার করা হয়।

const inputRef = useRef(null);

<input ref={inputRef} />

inputRef.current.focus();


Common uses:

DOM access
Timer ID রাখা
Previous value/reference রাখা
16. Context API কী?

Answer:
Context API parent থেকে অনেক level নিচের component-এ data পাঠাতে সাহায্য করে বারবার props pass না করেই।

const ThemeContext = createContext();


Common use cases:

Theme
Current user
Language
App-level settings

তবে সব state-এর জন্য Context ব্যবহার করা উচিত নয়।

17. Prop drilling কী?

Answer:
যখন কোনো data দরকার না থাকা intermediate components-এর মধ্য দিয়ে বারবার props হিসেবে pass করতে হয়, তাকে prop drilling বলে।

App
 ↓ props
A
 ↓ props
B
 ↓ props
C


Context বা appropriate state management ব্যবহার করে কিছু ক্ষেত্রে এটি কমানো যায়।

18. React-এ Conditional Rendering কী?

Answer:
Condition অনুযায়ী আলাদা UI render করাকে conditional rendering বলে।

{isLoggedIn ? (
  <Dashboard />
) : (
  <Login />
)}


আরও একটি example:

{isAdmin && <AdminPanel />}

19. React-এ API call কীভাবে করা যায়?

Answer:
fetch() বা Axios-এর মতো HTTP client ব্যবহার করে API call করা যায়। React-এ সাধারণত component lifecycle-এর সাথে synchronize করার জন্য useEffect ব্যবহার করা হয়।

useEffect(() => {
  async function getUsers() {
    const response = await fetch("/api/users");
    const data = await response.json();

    setUsers(data);
  }

  getUsers();
}, []);


Real application-এ loading এবং error state-ও handle করা উচিত।

20. React-এ performance optimize কীভাবে করবে?

Answer:
প্রয়োজন অনুযায়ী কয়েকটি technique ব্যবহার করা যায়:

React.memo
useMemo
useCallback
Lazy loading
Code splitting
Unnecessary re-render কমানো
বড় list-এর ক্ষেত্রে virtualization
Proper key ব্যবহার

তবে সব জায়গায় useMemo বা useCallback ব্যবহার করা উচিত নয়। Actual performance problem থাকলে বা computation/reference stability-এর প্রয়োজন হলে ব্যবহার করা ভালো।

🔥 Interview-এর আগে এই 10টা অবশ্যই পারো

যদি সময় কম থাকে, এগুলো সবচেয়ে আগে ভালোভাবে শিখো:

Component
Props vs State
useState
useEffect
useRef
Controlled vs Uncontrolled
Context API
Key
Conditional Rendering
API Call

আর যেহেতু তুমি HTML → CSS → JavaScript → React ধারাবাহিকভাবে interview preparation করছ, JavaScript-এর closure, array methods, async/await, promise, this, এবং React-এর useState/useEffect একসাথে practice করো—এগুলো থেকে interviewer প্রায়ই একটার পর একটা follow-up question করে।


অবশ্যই। যদি Next.js interview preparation করো, তাহলে নিচের 20টা most important question + সহজ Bangla answer আগে ভালোভাবে শিখে রাখো।

Next.js Interview — Top 20
1. Next.js কী?

Answer:
Next.js হলো React-এর উপর তৈরি একটি full-stack web framework। এটি React application তৈরি করার পাশাপাশি routing, rendering, data fetching, optimization এবং backend functionality-এর জন্য built-in features দেয়।

2. React এবং Next.js-এর মধ্যে পার্থক্য কী?

Answer:

React মূলত UI তৈরি করার library।

Next.js React-এর উপর framework হিসেবে কাজ করে এবং অতিরিক্ত features দেয়:

File-based routing
Server-side rendering
Static generation
Server Components
API/Route Handlers
Image optimization
Metadata/SEO support
Code splitting

সহজভাবে:

React = UI library
Next.js = React-based framework

3. Next.js-এ routing কীভাবে কাজ করে?

Answer:
Next.js-এ সাধারণত file-system based routing ব্যবহার করা হয়।

App Router-এ:

app/
 ├── page.jsx
 ├── about/
 │    └── page.jsx
 └── contact/
      └── page.jsx


এখানে:

/        → app/page.jsx
/about   → app/about/page.jsx
/contact → app/contact/page.jsx

4. App Router এবং Pages Router কী?

Answer:
Next.js-এ দুটি routing architecture রয়েছে:

App Router → app/ directory ব্যবহার করে
Pages Router → pages/ directory ব্যবহার করে

Modern Next.js application-এর ক্ষেত্রে App Router সাধারণত preferred approach।

5. Server Component এবং Client Component কী?

Answer:
App Router-এ component defaultভাবে Server Component হতে পারে।

Server Component server-এ render হয় এবং client-side JavaScript কম পাঠাতে সাহায্য করতে পারে।

Client Component প্রয়োজন হয় যখন browser-side interactivity বা client-only features দরকার হয়।

"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}


"use client" directive component-টিকে Client Component boundary-এর মধ্যে রাখে।

6. "use client" কেন ব্যবহার করা হয়?

Answer:
যখন কোনো component-এ client-side features দরকার হয়, তখন "use client" ব্যবহার করা হয়।

যেমন:

useState
useEffect
Event handlers
Browser APIs
Client-side interactivity
"use client";

import { useState } from "react";

7. SSR কী?

Answer:
SSR-এর পূর্ণরূপ Server-Side Rendering।

এখানে request-এর সময় server HTML তৈরি করে client-এ পাঠায়।

Browser
   ↓ request
Server
   ↓
HTML
   ↓
Browser


Dynamic এবং request-dependent content-এর ক্ষেত্রে SSR useful হতে পারে।

8. SSG কী?

Answer:
SSG-এর পূর্ণরূপ Static Site Generation।

এখানে page-এর output আগে থেকেই generate করা হয় এবং পরে serve করা যায়।

Static content-এর জন্য এটি খুব fast এবং scalable হতে পারে।

উদাহরণ:

Blog
Documentation
Marketing pages
9. SSR এবং SSG-এর পার্থক্য কী?

Answer:

SSR:

Request → Server renders → Response


SSG:

Build/Pre-generation → Static output → User request


সহজভাবে:

SSR = request-এর সময় render
SSG = আগে থেকেই generate

10. ISR কী?

Answer:
ISR-এর পূর্ণরূপ Incremental Static Regeneration।

এটি static page-কে নির্দিষ্ট সময় পর revalidate করে নতুন data দিয়ে update করার সুবিধা দেয়।

fetch("https://api.example.com/posts", {
  next: {
    revalidate: 60
  }
});


এখানে data-এর cache/revalidation behavior framework-এর মাধ্যমে control করা হচ্ছে।

11. Next.js-এ dynamic route কী?

Answer:
Dynamic route ব্যবহার করে URL-এর কোনো অংশ dynamic করা যায়।

app/
 └── products/
      └── [id]/
           └── page.jsx


তাহলে:

/products/1
/products/2
/products/100


সব route একই dynamic page structure ব্যবহার করতে পারে।

12. Link component কেন ব্যবহার করা হয়?

Answer:
Next.js-এর Link component internal navigation-এর জন্য ব্যবহার করা হয়।

import Link from "next/link";

<Link href="/about">
  About
</Link>


এটি client-side navigation-এর সুবিধা দেয় এবং full page reload এড়াতে সাহায্য করতে পারে।

13. Next.js-এর Image component কী?

Answer:
next/image image optimization-এর জন্য ব্যবহার করা হয়।

import Image from "next/image";

<Image
  src="/profile.jpg"
  alt="Profile"
  width={500}
  height={500}
/>


এটি responsive sizing, optimization এবং efficient image delivery-এর মতো সুবিধা দিতে পারে।

14. Next.js-এ API কীভাবে তৈরি করা যায়?

Answer:
App Router-এ Route Handlers ব্যবহার করে backend endpoint তৈরি করা যায়।

app/
 └── api/
      └── users/
           └── route.js

export async function GET() {
  return Response.json({
    message: "Hello"
  });
}


তাহলে /api/users endpoint পাওয়া যাবে।

15. Next.js Middleware কী?

Answer:
Middleware request process হওয়ার আগে নির্দিষ্ট logic চালাতে ব্যবহার করা যায়।

Common use cases:

Authentication checks
Redirect
Request-based logic
কিছু ক্ষেত্রে authorization-related checks

উদাহরণ:

Request
   ↓
Middleware
   ↓
Page / Route

16. Next.js-এ Environment Variables কীভাবে ব্যবহার করা হয়?

Answer:
.env.local file-এ environment variables রাখা যায়।

DATABASE_URL=your_database_url
NEXT_PUBLIC_API_URL=https://example.com


Client-side-এ expose করতে হলে সাধারণত NEXT_PUBLIC_ prefix লাগে।

process.env.NEXT_PUBLIC_API_URL


Important: Secret key কখনো NEXT_PUBLIC_ variable-এ রাখা উচিত নয়।

17. Next.js-এ SEO কীভাবে improve করবে?

Answer:
Next.js metadata features ব্যবহার করে page-এর title, description, Open Graph information ইত্যাদি define করা যায়।

App Router-এ:

export const metadata = {
  title: "My Website",
  description: "My website description"
};


এছাড়া semantic HTML এবং proper content structure গুরুত্বপূর্ণ।

18. Next.js-এ data fetching কীভাবে করা হয়?

Answer:
Server-side code-এ সাধারণত fetch() ব্যবহার করে data fetch করা যায়।

async function getUsers() {
  const response = await fetch(
    "https://api.example.com/users"
  );

  return response.json();
}

export default async function Page() {
  const users = await getUsers();

  return <div>{users.length} users</div>;
}


App Router-এ server-side data fetching-এর সুবিধা ভালোভাবে বুঝে রাখা গুরুত্বপূর্ণ।

19. Hydration কী?

Answer:
Server থেকে HTML আসার পর React client-side JavaScript-এর সাথে সেই HTML-কে interactive করার process-কে hydration বলা হয়।

সহজভাবে:

Server-rendered HTML
        ↓
Browser receives HTML
        ↓
React hydrates
        ↓
Interactive UI


Server এবং client-এর rendered output mismatch হলে hydration error/warning হতে পারে।

20. Next.js কেন ব্যবহার করব?

Answer:
Next.js ব্যবহার করলে React application-এর জন্য অনেক গুরুত্বপূর্ণ feature built-in পাওয়া যায়:

Routing
Server/Client rendering model
Data fetching
SEO support
Image optimization
Code splitting
Backend Route Handlers
Caching/revalidation
ভালো production tooling

তাই production-grade React application তৈরি করা সহজ হয়।

🔥 Interview-এর আগে Next.js-এর এই 10টা অবশ্যই পারো
React vs Next.js
App Router
Server Component vs Client Component
"use client"
SSR
SSG
ISR
Dynamic Routing
Middleware
Data Fetching + Caching/Revalidation
⭐ একটা গুরুত্বপূর্ণ interview pattern

Interviewer যদি জিজ্ঞেস করে:

"Next.js কেন ব্যবহার করবেন?"

তখন শুধু "SEO ভালো" বলবে না। ভালো answer হবে:

"Next.js React-এর উপর built একটি framework, যেখানে routing, server/client rendering, data fetching, caching, image optimization এবং backend route handling-এর মতো অনেক feature built-in থাকে। তাই production application তৈরি করা এবং optimize করা তুলনামূলক সহজ হয়।"

এটা Junior React/Next.js interview-এর জন্য বেশ strong answer।

অবশ্যই। নিচে Git এবং GitHub-এর সবচেয়ে important 20টি interview question + সহজ Bangla answer দিলাম। Junior/Frontend Developer interview-এর জন্য এগুলো খুব গুরুত্বপূর্ণ।

Git & GitHub Interview — Top 20
1. Git কী?

Answer:
Git হলো একটি Distributed Version Control System (DVCS)। এটি code-এর changes track করতে এবং team-এর সাথে code manage করতে ব্যবহার করা হয়।

সহজভাবে:

Git = Code-এর version/history manage করার tool।

2. GitHub কী?

Answer:
GitHub হলো একটি cloud-based platform যেখানে Git repositories host করা যায়।

GitHub ব্যবহার করে:

Code online রাখা যায়
Team-এর সাথে collaborate করা যায়
Pull Request করা যায়
Code review করা যায়
Issues manage করা যায়

সহজভাবে:

Git = Version control tool
GitHub = Git repository host এবং collaboration platform

3. Git এবং GitHub-এর মধ্যে পার্থক্য কী?

Answer:

Git	GitHub
Version control system	Online platform
Local machine-এ কাজ করে	Cloud-based hosting/collaboration
Code history track করে	Repository host করে
GitHub ছাড়াও Git ব্যবহার করা যায়	Git ছাড়া GitHub-এর মূল Git workflow অসম্পূর্ণ
4. Repository কী?

Answer:
Repository বা repo হলো এমন একটি জায়গা যেখানে project-এর files এবং তাদের Git version history রাখা হয়।

Local repository এবং remote repository—দুটোই থাকতে পারে।

5. git init কী করে?

Answer:
git init current project directory-কে Git repository হিসেবে initialize করে।

git init


এর ফলে .git directory তৈরি হয়, যেখানে Git-এর metadata/history রাখা হয়।

6. git clone কী?

Answer:
Remote repository-এর একটি copy local computer-এ নিয়ে আসতে git clone ব্যবহার করা হয়।

git clone https://github.com/user/project.git


Clone করলে repository-এর files এবং Git history local machine-এ আসে।

7. git status কী?

Answer:
বর্তমান repository-এর অবস্থান দেখতে git status ব্যবহার করা হয়।

git status


এটি দেখাতে পারে:

Modified files
Untracked files
Staged files
Current branch
8. git add কী?

Answer:
Commit করার জন্য changes-কে staging area-তে রাখতে git add ব্যবহার করা হয়।

git add file.js


সব changed files stage করতে:

git add .

9. git commit কী?

Answer:
Staged changes-এর একটি snapshot Git history-তে save করতে git commit ব্যবহার করা হয়।

git commit -m "Add login form"


ভালো commit message হওয়া উচিত ছোট এবং meaningful।

10. Git-এর তিনটি গুরুত্বপূর্ণ area কী?

Answer:

Working Directory
       ↓ git add
Staging Area
       ↓ git commit
Repository


Working Directory: যেখানে তুমি code modify করছ।

Staging Area: যেসব changes পরবর্তী commit-এ রাখতে চাও।

Repository: যেখানে committed history থাকে।

11. git push কী?

Answer:
Local repository-এর commits remote repository-তে পাঠাতে git push ব্যবহার করা হয়।

git push origin main

12. git pull কী?

Answer:
Remote repository থেকে changes নিয়ে local branch update করতে git pull ব্যবহার করা হয়।

git pull origin main


Conceptually, git pull সাধারণত fetch + integrate operation করে।

13. git fetch এবং git pull এর পার্থক্য কী?

Answer:

git fetch remote-এর নতুন commits/refs local repository-তে আনে, কিন্তু current branch-এ automatically integrate করে না।

git fetch origin


git pull fetch করার পর changes integrate করার চেষ্টা করে।

git pull origin main


সহজভাবে:

fetch = আগে changes দেখো/নিয়ে আসো
pull = নিয়ে এসে integrate করো

14. Branch কী?

Answer:
Branch হলো codebase-এর একটি আলাদা line of development।

যেমন:

git branch feature-login
git switch feature-login


এতে main code সরাসরি affect না করে নতুন feature নিয়ে কাজ করা যায়।

15. git merge কী?

Answer:
একটি branch-এর changes অন্য branch-এ combine করতে git merge ব্যবহার করা হয়।

git switch main
git merge feature-login


এতে feature-login branch-এর changes main-এ integrate হবে।

16. Merge conflict কী?

Answer:
দুই branch-এর একই অংশের code-এ incompatible changes থাকলে Git automatically decide করতে না পারলে merge conflict হয়।

উদাহরণ:

<<<<<<< HEAD
Hello
=======
Hi
>>>>>>> feature


Developer-কে manually ঠিক করতে হবে, তারপর:

git add .
git commit

17. Pull Request (PR) কী?

Answer:
Pull Request হলো GitHub-এর একটি feature, যার মাধ্যমে নিজের branch-এর changes অন্য branch-এ merge করার জন্য review/request করা হয়।

Typical workflow:

Create branch
      ↓
Write code
      ↓
Commit
      ↓
Push
      ↓
Create Pull Request
      ↓
Code Review
      ↓
Merge

18. .gitignore কী?

Answer:
যেসব files/folders Git repository-তে track করতে চাই না, সেগুলো .gitignore-এ specify করা হয়।

Example:

node_modules/
.env
dist/


যেমন node_modules এবং secret-containing .env সাধারণত repository-তে commit করা উচিত নয়।

19. git reset এবং git revert এর মধ্যে পার্থক্য কী?

Answer:

git reset branch-এর history/HEAD সরাতে ব্যবহার করা যায় এবং mode অনুযায়ী working/staging changes-এর উপরও প্রভাব ফেলতে পারে।

git reset --soft HEAD~1


git revert পুরনো commit-এর বিপরীত একটি নতুন commit তৈরি করে।

git revert abc123


Shared/public branch-এর history rewrite করার চেয়ে git revert সাধারণত safer।

20. git stash কী?

Answer:
বর্তমান uncommitted changes temporarily সরিয়ে রাখতে git stash ব্যবহার করা হয়।

git stash


পরে changes ফিরিয়ে আনতে:

git stash pop


যেমন তুমি feature নিয়ে কাজ করছ, কিন্তু হঠাৎ অন্য branch-এর জরুরি কাজ করতে হবে—তখন stash useful।

🔥 Interview-এর জন্য Must Know Commands

এগুলো অবশ্যই হাতে-কলমে practice করবে:

git init
git clone
git status
git add
git commit
git push
git pull
git fetch
git branch
git switch
git merge
git stash
git log
git diff
git revert

⭐ সবচেয়ে important 10টা

যদি interviewer খুব basic Git question করে, এগুলো সবচেয়ে বেশি আসতে পারে:

Git কী?
Git vs GitHub
Repository কী?
git add
git commit
git push vs git pull
git fetch vs git pull
Branch কী?
Merge conflict কী?
Pull Request কী?
🎯 একটা common interview question

Interviewer: "একটা feature নিয়ে কাজ করার সময় তুমি কীভাবে Git workflow follow করবে?"

তুমি বলতে পারো:

"প্রথমে latest main branch থেকে নতুন feature branch তৈরি করব। তারপর feature-এর code লিখে git add এবং git commit করব। এরপর branch-টা remote-এ git push করব এবং GitHub-এ Pull Request তৈরি করব। Code review এবং required changes শেষ হলে PR merge করব।"

এই answer-টা practical এবং interview-friendly।

হ্যাঁ—Git/GitHub-এর basic 20টার বাইরে আরও কিছু important interview question আছে, যেগুলো একটু experienced interviewer জিজ্ঞেস করতে পারে।

Git & GitHub — Advanced/Practical Questions
21. git log কী?

Answer:
Repository-এর commit history দেখতে git log ব্যবহার করা হয়।

git log


Short version:

git log --oneline

22. git diff কী?

Answer:
বর্তমান changes এবং previous/staged version-এর মধ্যে কী পরিবর্তন হয়েছে সেটা দেখতে git diff ব্যবহার করা হয়।

git diff

23. origin কী?

Answer:
origin হলো remote repository-এর একটি সাধারণ/default নাম।

git push origin main


এখানে:

origin → remote repository
main → branch
24. HEAD কী?

Answer:
HEAD সাধারণত current checked-out commit/branch position-কে নির্দেশ করে।

git log --oneline


HEAD কোথায় আছে সেটা বোঝা Git history নিয়ে কাজ করার সময় গুরুত্বপূর্ণ।

25. git switch কী?

Answer:
Branch change বা নতুন branch তৈরি করার জন্য git switch ব্যবহার করা যায়।

git switch main


নতুন branch:

git switch -c feature-login

26. git checkout কী?

Answer:
git checkout পুরনো Git command, যা branch switch করার পাশাপাশি আরও কিছু কাজ করতে পারে।

git checkout main


Modern Git-এ branch switching-এর জন্য git switch এবং file restore-এর জন্য git restore বেশি পরিষ্কার approach।

27. git cherry-pick কী?

Answer:
একটি নির্দিষ্ট commit-এর changes অন্য branch-এ apply করতে git cherry-pick ব্যবহার করা হয়।

git cherry-pick abc123


যখন পুরো branch merge না করে শুধু একটি নির্দিষ্ট commit দরকার হয়, তখন useful।

28. git rebase কী?

Answer:
এক branch-এর commits-কে অন্য branch-এর latest base-এর উপর replay করতে git rebase ব্যবহার করা হয়।

git switch feature
git rebase main


এটি history-কে অনেক ক্ষেত্রে linear রাখতে সাহায্য করে।

Important: Shared/public history rebase করে rewrite করার ক্ষেত্রে সতর্ক থাকতে হয়।

29. Merge এবং Rebase-এর পার্থক্য কী?

Answer:

Merge:

A---B---C main
     \
      D---E feature

A---B---C-------M
     \         /
      D---E---


Merge সাধারণত existing history preserve করে এবং প্রয়োজনে merge commit তৈরি করে।

Rebase:

A---B---C main
         \
          D'---E' feature


Rebase feature commits-কে নতুন base-এর উপর replay করে এবং history linear করতে পারে।

সহজভাবে:

Merge = history combine করে
Rebase = history নতুন base-এর উপর replay করে

30. git remote কী?

Answer:
Remote repository-এর information manage/view করতে git remote ব্যবহার করা হয়।

git remote -v


এতে remote URL দেখা যায়।

31. git tag কী?

Answer:
কোনো নির্দিষ্ট commit-কে একটি meaningful version/name দিয়ে mark করতে tag ব্যবহার করা হয়।

git tag v1.0.0


Software release versioning-এ tag খুব common।

32. git revert কখন ব্যবহার করবে?

Answer:
যদি কোনো ভুল commit already shared branch-এ push করা হয়ে থাকে এবং সেটার effect undo করতে হয়, git revert useful।

git revert abc123


এটি একটি নতুন commit তৈরি করে পুরনো change-এর বিপরীত change apply করে।

33. ভুল করে commit করে ফেললে কী করবে?

Answer:
Situation-এর উপর depend করে।

যদি commit local এবং undo করতে চাই:

git reset --soft HEAD~1


এতে commit সরবে, কিন্তু changes staging area-তে থাকবে।

যদি commit already shared/pushed হয়, সাধারণত history rewrite না করে:

git revert <commit>


ব্যবহার করা safer।

34. git reset --soft, --mixed, --hard এর পার্থক্য কী?

Answer:

--soft → commit সরায়, changes staged থাকে
--mixed → commit সরায়, changes unstaged থাকে
--hard → commit এবং working tree changes discard করতে পারে
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1


⚠️ --hard ব্যবহার করার আগে খুব সতর্ক হতে হবে, কারণ uncommitted work হারাতে পারে।

35. GitHub-এ Fork কী?

Answer:
অন্য কারও repository-এর নিজের GitHub account-এ একটি copy তৈরি করাকে Fork বলে।

এটি open-source project-এ contribution করার সময় খুব common।

Original Repository
        ↓
      Fork
        ↓
Your Repository
        ↓
Changes
        ↓
Pull Request

36. Pull Request এবং git pull কি একই?

Answer:
না।

Pull Request (PR): GitHub-এর collaboration/review mechanism।

git pull: Remote repository-এর changes local branch-এ আনার Git command।

37. GitHub Issues কী?

Answer:
Project-এর:

Bug
Feature request
Task
Improvement

track এবং discuss করার জন্য GitHub Issues ব্যবহার করা হয়।

38. GitHub Actions কী?

Answer:
GitHub Actions হলো GitHub-এর CI/CD এবং automation platform।

যেমন code push করার পর automatically:

Push Code
   ↓
Run Tests
   ↓
Build
   ↓
Deploy


automate করা যায়।

39. .gitignore-এ .env কেন রাখা হয়?

Answer:
.env file-এ API key, database URL, secret বা অন্য sensitive configuration থাকতে পারে।

তাই সাধারণত:

.env
.env.local


রাখা হয়।

তবে .gitignore security boundary নয়। কোনো secret ভুল করে commit/push হয়ে গেলে শুধু .gitignore যোগ করলেই history থেকে secret নিরাপদে মুছে যায় না—secret rotate/revoke করাও প্রয়োজন।

40. একজন Frontend Developer-এর সাধারণ Git workflow কী?

Answer:

main
 ↓
Create feature branch
 ↓
Write code
 ↓
git add
 ↓
git commit
 ↓
git push
 ↓
Create Pull Request
 ↓
Code Review
 ↓
Fix issues if needed
 ↓
Merge


Interview-এ এভাবে বলতে পারো:

"আমি সাধারণত main branch থেকে feature branch তৈরি করি। Feature complete হলে changes commit করে remote-এ push করি, তারপর Pull Request তৈরি করি। Code review এবং required changes শেষ হলে PR merge করি।"

⭐ এখন Git-এর জন্য যেগুলো সবচেয়ে ভালোভাবে practice করবে
git clone
git status
git add
git commit
git push
git pull
git fetch
git branch
git switch
git merge
Merge conflict
Pull Request
git stash
git revert
git reset
rebase
cherry-pick
.gitignore

এগুলো জানলে Junior Frontend/React/Next.js interview-এর Git অংশের জন্য বেশ ভালো foundation তৈরি হয়ে যাবে।




