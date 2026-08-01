আপনি যদি **Framer Motion + React + Next.js** ভালোভাবে শিখতে চান, তাহলে আমি একটি **complete roadmap/tutorial path** দিচ্ছি যেটা beginner থেকে advanced পর্যন্ত যাবে। এইটা follow করলে production-level animation বানাতে পারবেন।

# Framer Motion Complete Tutorial Roadmap (React + Next.js)

## 0. Prerequisite (আগে যা জানা দরকার)

Framer Motion শেখার আগে এগুলো জানা ভালো:

✅ React:

- Components
    
- Props
    
- State
    
- Hooks (`useState`, `useEffect`)
    
- Conditional rendering
    
- Mapping arrays
    

✅ Next.js:

- App Router
    
- Client Component (`"use client"`)
    
- Layout
    
- Routing
    

✅ CSS:

- Flexbox
    
- Grid
    
- Transform
    
- Transition
    

---

# 1. Framer Motion Setup

Install:

```bash
npm install framer-motion
```

Import:

```javascript
import { motion } from "framer-motion";
```

Framer Motion-এর মূল idea:

Normal:

```jsx
<div>Hello</div>
```

Motion:

```jsx
<motion.div>
Hello
</motion.div>
```

`motion.div` হচ্ছে animated div.

---

# 2. Basic Animation Concepts

Framer Motion-এর ৩টি main property:

## initial

Animation শুরু কোথা থেকে হবে:

```jsx
initial={{
 opacity:0
}}
```

## animate

শেষ অবস্থান:

```jsx
animate={{
 opacity:1
}}
```

## transition

কিভাবে animation হবে:

```jsx
transition={{
 duration:1
}}
```

Example:

```jsx
"use client"

import {motion} from "framer-motion"

export default function Page(){

return (

<motion.div

initial={{
opacity:0,
x:-100
}}

animate={{
opacity:1,
x:0
}}

transition={{
duration:1
}}

>
Hello World

</motion.div>

)

}
```

---

# 3. Transform Animation

## Move

```jsx
<motion.div
animate={{
x:100
}}
/>
```

## Vertical move

```jsx
animate={{
y:50
}}
```

## Scale

```jsx
animate={{
scale:1.5
}}
```

## Rotate

```jsx
animate={{
rotate:180
}}
```

## Multiple

```jsx
animate={{
x:100,
y:50,
scale:1.2,
rotate:90
}}
```

---

# 4. Transition Deep Dive

## Duration

```javascript
transition={{
duration:2
}}
```

---

## Delay

```javascript
transition={{
delay:1
}}
```

---

## Ease

```javascript
transition={{
ease:"easeInOut"
}}
```

Available:

```
easeIn
easeOut
easeInOut
linear
```

---

## Spring Animation

Realistic animation:

```jsx
transition={{
type:"spring",
stiffness:100
}}
```

Control:

```jsx
transition={{
type:"spring",
mass:1,
stiffness:80,
damping:10
}}
```

---

# 5. Hover Animation

Button/card hover:

```jsx
<motion.div

whileHover={{
scale:1.1
}}

>
Card

</motion.div>
```

Example:

```jsx
<motion.button

whileHover={{
scale:1.05,
backgroundColor:"#000"
}}

whileTap={{
scale:0.9
}}

>
Click

</motion.button>
```

---

# 6. While Tap Animation

Mobile click effect:

```jsx
<motion.div

whileTap={{
scale:0.8
}}

>
Button

</motion.div>
```

---

# 7. Drag Animation

Element drag:

```jsx
<motion.div

drag

>
Drag Me

</motion.div>
```

Limit:

```jsx
<motion.div

drag
dragConstraints={{
left:0,
right:200
}}

>
Drag

</motion.div>
```

---

# 8. Variants (সবচেয়ে গুরুত্বপূর্ণ)

Professional animation এ variants ব্যবহার করা হয়।

Example:

```jsx
const box={
hidden:{
opacity:0,
y:50
},

show:{
opacity:1,
y:0
}

}


<motion.div

variants={box}

initial="hidden"

animate="show"

>

Hello

</motion.div>
```

Advantages:

- Clean code
    
- Reusable animation
    
- Complex animation সহজ হয়
    

---

# 9. Stagger Animation

একটার পর একটা element আসা:

Example:

```jsx
const container={

hidden:{},

show:{
transition:{
staggerChildren:0.3
}
}

}


const item={

hidden:{
opacity:0,
y:20
},

show:{
opacity:1,
y:0
}

}
```

Result:

```
Card 1
↓
Card 2
↓
Card 3
```

---

# 10. Scroll Animation

## whileInView

```jsx
<motion.div

initial={{
opacity:0
}}

whileInView={{
opacity:1
}}

>

Content

</motion.div>
```

---

Only once:

```jsx
viewport={{
once:true
}}
```

---

# 11. Text Animation

Example:

Letter animation:

```
H
He
Hel
Hell
Hello
```

Technique:

- Split text
    
- Map letters
    
- Animate each letter
    

---

# 12. AnimatePresence

Component enter/exit animation:

Install নেই, built-in.

Example:

```jsx
import {AnimatePresence,motion}
from "framer-motion"


<AnimatePresence>

{
show &&
<motion.div

initial={{
opacity:0
}}

animate={{
opacity:1
}}

exit={{
opacity:0
}}

>

Modal

</motion.div>

}

</AnimatePresence>
```

Use:

- Modal
    
- Dropdown
    
- Menu
    
- Toast
    

---

# 13. Next.js Page Animation

App Router:

Structure:

```
app
 |
 layout.jsx
 |
 template.jsx
```

template:

```jsx
"use client"

import {motion} from "framer-motion"


export default function Template({children}){

return (

<motion.div

initial={{
opacity:0
}}

animate={{
opacity:1
}}

>

{children}

</motion.div>

)

}
```

---

# 14. useAnimation Hook

Manual control:

```jsx
const controls=useAnimation()


controls.start({
x:100
})
```

Example:

Button click করলে animation:

```jsx
<button
onClick={()=>controls.start({
rotate:360
})}
>
Animate
</button>
```

---

# 15. Motion Values

Advanced animation:

```javascript
useMotionValue()
```

Use:

- Mouse tracking
    
- Parallax
    
- Scroll effects
    

---

# 16. Scroll Based Advanced Animation

Hooks:

```javascript
useScroll()

useTransform()
```

Example:

```javascript
const {scrollY}=useScroll()

const scale=useTransform(
scrollY,
[0,500],
[1,2]
)
```

---

# 17. Layout Animation

Automatic position change:

```jsx
<motion.div
layout
>
Content
</motion.div>
```

Use:

- Tabs
    
- Filter
    
- Sorting
    
- Cards
    

---

# 18. Shared Layout Animation

এক component থেকে অন্য component এ move:

Example:

- Product image
    
- Gallery
    
- Modal
    

---

# 19. Gesture Animation

Framer Motion supports:

- Hover
    
- Tap
    
- Drag
    
- Pan
    

Example:

```jsx
<motion.div

whileDrag={{
scale:1.2
}}

drag

/>
```

---

# 20. Production Level Projects Practice

এই order এ project বানান:

### Beginner

1. Animated Button
    
2. Loading Spinner
    
3. Fade Landing Page
    
4. Card Hover Animation
    

### Intermediate

5. Portfolio Website
    
6. Animated Navbar
    
7. Modal System
    
8. Image Gallery
    

### Advanced

9. Apple style landing page
    
10. Dashboard animation
    
11. E-commerce product page
    
12. Awwwards style website
    

---

# Recommended Learning Order

```
Day 1:
Basic motion

Day 2:
Transition + Spring

Day 3:
Hover + Tap + Drag

Day 4:
Variants

Day 5:
Stagger Animation

Day 6:
Scroll Animation

Day 7:
AnimatePresence

Day 8:
Next.js Page Transition

Day 9:
useScroll + useTransform

Day 10:
Build Full Website
```

---

# Must Know Framer Motion API

এগুলো মুখস্থ না হলেও ব্যবহার জানতে হবে:

```
motion
initial
animate
exit
transition
variants
whileHover
whileTap
whileInView
AnimatePresence
layout
drag
useAnimation
useMotionValue
useScroll
useTransform
```

এইগুলো জানলে React/Next.js-এ প্রায় সব ধরনের modern UI animation তৈরি করতে পারবেন।

--------

আমি প্রতিটা Framer Motion API **কী, কেন ব্যবহার হয়, কখন ব্যবহার করবেন, এবং complete React/Next.js example** দিয়ে explain করছি।

একসাথে অনেক বড় হয়ে যাবে, তাই আমি এটাকে কয়েকটি part-এ ভাগ করছি। প্রথমে সবচেয়ে গুরুত্বপূর্ণ core API:

1. `motion`
    
2. `initial`
    
3. `animate`
    
4. `exit`
    
5. `transition`
    
6. `variants`
    
7. `whileHover`
    
8. `whileTap`
    

এরপর পরের অংশে:

9. `whileInView`
    
10. `AnimatePresence`
    
11. `layout`
    
12. `drag`
    
13. `useAnimation`
    
14. `useMotionValue`
    
15. `useScroll`
    
16. `useTransform`
    

---

# 1. motion

## motion কী?

Normal HTML element কে animated element বানানোর জন্য `motion` ব্যবহার হয়।

Normal:

```jsx
<div>
Hello
</div>
```

Animation:

```jsx
<motion.div>
Hello
</motion.div>
```

---

## Example

```jsx
"use client"

import { motion } from "framer-motion"


export default function Home(){

return (

<motion.div>

Hello Motion

</motion.div>

)

}
```

এখন এই div animation properties নিতে পারবে।

যেমন:

```jsx
<motion.div

animate={{
x:200
}}

>
Move Me

</motion.div>
```

Result:

```
Start
|
|
|---------> Move 200px
```

---

# 2. initial

## initial কী?

Animation শুরু হওয়ার আগের অবস্থাকে define করে।

Syntax:

```jsx
initial={{
property:value
}}
```

Example:

```jsx
<motion.div

initial={{
opacity:0
}}

animate={{
opacity:1
}}

>

Hello

</motion.div>
```

Flow:

```
Page load

opacity:0
(hidden)

↓

opacity:1
(visible)
```

---

## Multiple initial values

```jsx
<motion.div

initial={{
opacity:0,
x:-100,
scale:0.5
}}

animate={{
opacity:1,
x:0,
scale:1
}}

>
Card

</motion.div>
```

Result:

```
Left side থেকে আসবে
+
fade হবে
+
normal size হবে
```

---

# 3. animate

## animate কী?

Final state define করে।

Example:

```jsx
<motion.div

animate={{
x:100
}}

>
Box

</motion.div>
```

মানে:

```
0px

↓

100px
```

---

## Continuous animation

```jsx
<motion.div

animate={{
rotate:360
}}

transition={{
duration:2,
repeat:Infinity
}}

>

Loading

</motion.div>
```

Result:

```
↻ ↻ ↻
```

---

# 4. exit

## exit কী?

Component remove হওয়ার সময় animation।

এটার জন্য `AnimatePresence` লাগবে।

Example:

```jsx
"use client"

import {
motion,
AnimatePresence
}
from "framer-motion"

import {useState} from "react"


export default function App(){

const [show,setShow]=useState(true)


return (

<div>


<button
onClick={()=>setShow(!show)}
>
Toggle
</button>


<AnimatePresence>

{
show &&

<motion.div

initial={{
opacity:0
}}

animate={{
opacity:1
}}

exit={{
opacity:0
}}

>

Box

</motion.div>

}

</AnimatePresence>


</div>

)

}
```

---

Flow:

Open:

```
opacity 0

↓

opacity 1
```

Close:

```
opacity 1

↓

opacity 0
(remove)
```

---

# 5. transition

## transition কী?

Animation কিভাবে হবে সেটা control করে।

---

Basic:

```jsx
transition={{
duration:1
}}
```

মানে:

১ second ধরে animation হবে।

---

## Delay

```jsx
transition={{
delay:2
}}
```

২ second পরে শুরু হবে।

---

## Ease

```jsx
transition={{
ease:"easeInOut"
}}
```

Animation smooth হবে।

---

## Spring

```jsx
transition={{

type:"spring",
stiffness:100,
damping:10

}}
```

Real object এর মতো feel দেয়।

Example:

```jsx
<motion.div

animate={{
x:200
}}

transition={{

type:"spring"

}}

>
Ball

</motion.div>
```

---

# 6. variants

## variants কী?

Reusable animation object।

Large project এ সবচেয়ে বেশি ব্যবহার হয়।

Without variants:

```jsx
<motion.div

initial={{
opacity:0,
y:50
}}

animate={{
opacity:1,
y:0
}}

>
Card

</motion.div>
```

Problem:

অনেক জায়গায় repeat হবে।

---

Variants:

```jsx
const cardAnimation={


hidden:{

opacity:0,
y:50

},


show:{

opacity:1,
y:0

}


}
```

Use:

```jsx
<motion.div

variants={cardAnimation}

initial="hidden"

animate="show"

>

Card

</motion.div>
```

---

## Real example

```jsx
const box={

hidden:{
scale:0
},

visible:{
scale:1
}

}


function App(){


return (

<motion.div

variants={box}

initial="hidden"

animate="visible"

>

Hello

</motion.div>

)

}
```

---

# 7. whileHover

## কী?

Mouse hover করলে animation।

Example:

```jsx
<motion.div

whileHover={{

scale:1.2

}}

>

Hover Me

</motion.div>
```

Result:

Before:

```
[ Box ]
```

Hover:

```
[ BIG BOX ]
```

---

## Card hover example

```jsx
<motion.div

whileHover={{

y:-10,
boxShadow:"0px 10px 20px gray"

}}

className="card"

>

Product Card

</motion.div>
```

Use:

- Card
    
- Button
    
- Navbar item
    

---

# 8. whileTap

## কী?

Click/touch করলে animation।

Example:

```jsx
<motion.button

whileTap={{

scale:0.8

}}

>

Click Me

</motion.button>
```

Result:

Normal:

```
BUTTON
```

Click:

```
small BUTTON
```

Release:

```
normal
```

---

## Professional Button

```jsx
<motion.button


whileHover={{

scale:1.1

}}


whileTap={{

scale:0.9

}}


>

Buy Now

</motion.button>
```

এটা প্রায় সব modern website এ থাকে।

---

## এখন পর্যন্ত Summary

|API|কাজ|
|---|---|
|motion|element animate করা|
|initial|শুরু অবস্থা|
|animate|শেষ অবস্থা|
|exit|remove animation|
|transition|animation timing/control|
|variants|reusable animation|
|whileHover|mouse hover|
|whileTap|click effect|

পরের part-এ আমি explain করব:

- `whileInView` (scroll animation)
    
- `AnimatePresence` (modal/menu animation)
    
- `layout` (automatic movement)
    
- `drag`
    
- `useAnimation`
    
- `useMotionValue`
    
- `useScroll`
    
- `useTransform`
    

সাথে real Next.js project examples দেব।


---

চলুন **Framer Motion Advanced Part** শুরু করি। এবার আমরা শিখব:

9. `whileInView`
10. `AnimatePresence`
11. `layout`
12. `drag`
13. `useAnimation`
14. `useMotionValue`
15. `useScroll`
16. `useTransform`

এগুলো জানলে আপনি production-level animation বানাতে পারবেন।

---

# 9. whileInView

## whileInView কী?

যখন কোনো element viewport (screen)-এ আসবে তখন animation চালাবে।

এটা ব্যবহার হয়:

* Scroll reveal
* Landing page section
* Portfolio
* Product section

---

## Basic Example

```jsx
"use client"

import {motion} from "framer-motion"


export default function Page(){

return (

<motion.div

initial={{
opacity:0,
y:100
}}

whileInView={{
opacity:1,
y:0
}}

>

Scroll Me

</motion.div>

)

}
```

---

## কী হচ্ছে?

Page load:

```
opacity:0
y:100

(hidden নিচে)
```

Scroll করলে:

```
opacity:1
y:0

(visible)
```

---

## once ব্যবহার

Default:

প্রতিবার scroll করলে animation হবে।

একবার করার জন্য:

```jsx
viewport={{
once:true
}}
```

Example:

```jsx
<motion.div

initial={{
opacity:0
}}

whileInView={{
opacity:1
}}

viewport={{
once:true
}}

>
Content
</motion.div>
```

---

## Amount control

কতটুকু visible হলে animation হবে:

```jsx
viewport={{

amount:0.5

}}
```

মানে:

৫০% element দেখা গেলে animation শুরু হবে।

---

# Real Section Animation

```jsx
const fadeUp={

hidden:{
opacity:0,
y:50
},

show:{
opacity:1,
y:0
}

}


<motion.section

variants={fadeUp}

initial="hidden"

whileInView="show"

viewport={{
once:true
}}

>

<h1>
About Us
</h1>

</motion.section>
```

---

# 10. AnimatePresence

## AnimatePresence কী?

Component চলে যাওয়ার সময় animation করার জন্য।

যেমন:

* Modal
* Dropdown
* Mobile menu
* Toast notification

---

## Without AnimatePresence

```jsx
{
show &&
<motion.div>

Modal

</motion.div>
}
```

এখানে exit animation হবে না।

---

## With AnimatePresence

```jsx
"use client"

import {
motion,
AnimatePresence
}
from "framer-motion"


import {useState} from "react"


export default function App(){


const [open,setOpen]=useState(false)


return (

<>


<button
onClick={()=>setOpen(!open)}
>
Open
</button>


<AnimatePresence>


{
open &&

<motion.div


initial={{
opacity:0,
scale:0.8
}}


animate={{
opacity:1,
scale:1
}}


exit={{
opacity:0,
scale:0.8
}}


>

Modal Content


</motion.div>

}


</AnimatePresence>


</>

)

}
```

---

Flow:

Open:

```
scale 0.8
opacity 0

↓

scale 1
opacity 1
```

Close:

```
scale 1

↓

scale 0.8
(remove)
```

---

# 11. layout

## layout কী?

Framer Motion নিজে থেকে position change animate করে।

Normal CSS:

```
Box A

Box B
```

change:

```
Box B
Box A
```

হঠাৎ jump করবে।

`layout` দিলে:

```
Box A

↓ smooth move

Box B
```

---

## Example

```jsx
<motion.div

layout

>

Content

</motion.div>
```

---

## Real Example: Tabs

```jsx
"use client"

import {
motion
}
from "framer-motion"

import {
useState
}
from "react"


export default function Tabs(){


const [active,setActive]=useState(1)


return (

<div>


{
["Home","About"].map((item,index)=>(


<button

onClick={()=>setActive(index)}

>


{item}


{
active===index &&

<motion.div

layoutId="underline"

className="line"

/>

}


</button>


))

}


</div>

)


}
```

---

Result:

Underline এক button থেকে অন্য button এ smooth যাবে।

---

# 12. drag

## drag কী?

Element drag করার ক্ষমতা দেয়।

Basic:

```jsx
<motion.div

drag

>

Drag Me

</motion.div>
```

---

Result:

Mouse দিয়ে টেনে নেওয়া যাবে।

---

## Direction control

Only X:

```jsx
drag="x"
```

Only Y:

```jsx
drag="y"
```

Example:

```jsx
<motion.div

drag="x"

>

Slider

</motion.div>
```

---

# Drag Constraint

Limit করতে:

```jsx
<motion.div


drag


dragConstraints={{

left:0,
right:300

}}


>

Drag Box


</motion.div>
```

এখন:

```
0 -------- 300px

Box move করবে
```

---

# Drag Elastic

```jsx
<motion.div

drag

dragElastic={0.2}

>

Box

</motion.div>
```

কম bounce করবে।

---

# 13. useAnimation

## useAnimation কী?

নিজে manually animation control করা।

যখন:

Button click করলে animation

API call শেষ হলে animation

Loading শেষ হলে animation

---

Example:

```jsx
"use client"


import {
motion,
useAnimation
}
from "framer-motion"



export default function App(){


const controls=useAnimation()



return (

<>


<button

onClick={()=>{

controls.start({

x:200

})

}}

>

Move


</button>



<motion.div

animate={controls}

>

Box

</motion.div>


</>


)

}
```

---

Flow:

Button click:

```
controls.start()

↓

x:200

↓

Box move
```

---

## Multiple animation

```javascript
controls.start({

scale:2,
rotate:360

})
```

---

# 14. useMotionValue

## useMotionValue কী?

Animation value track করার জন্য।

Normal React state:

```
change হলে re-render
```

MotionValue:

```
without re-render
```

---

Example:

```jsx
"use client"


import {
motion,
useMotionValue
}
from "framer-motion"


export default function App(){


const x=useMotionValue(0)


return (

<motion.div

style={{

x

}}

drag

>

Drag


</motion.div>

)

}
```

---

এখানে:

Drag করলে:

```
x value update
```

কিন্তু React re-render হয় না।

---

Use:

* Mouse tracking
* Parallax
* Advanced animation

---

# 15. useScroll

## useScroll কী?

Page scroll value পাওয়ার জন্য।

Example:

```jsx
"use client"


import {
useScroll,
motion
}
from "framer-motion"



export default function App(){


const {scrollY}=useScroll()



return (

<motion.div

style={{

scale:scrollY

}}

>

Hello

</motion.div>

)

}
```

---

Practical use:

* Progress bar
* Parallax
* Header animation

---

## Scroll Progress Bar

```jsx
const {scrollYProgress}=useScroll()


<motion.div

style={{

scaleX:scrollYProgress

}}

className="progress"

/>
```

Result:

```
0%

|

|

100%

```

Scroll করলে bar বাড়বে।

---

# 16. useTransform

## useTransform কী?

এক value কে অন্য value তে convert করে।

Example:

Scroll:

```
0 -------- 500
```

Convert:

```
1 -------- 2
```

---

Example:

```jsx
"use client"


import {

useScroll,
useTransform,
motion

}

from "framer-motion"



export default function App(){


const {scrollY}=useScroll()



const scale=useTransform(

scrollY,

[0,500],

[1,2]

)



return (

<motion.div

style={{

scale

}}

>

Zoom


</motion.div>

)


}
```

---

Result:

Top:

```
scale 1
```

Scroll:

```
scale 2
```

---

# Real World Example: Parallax Hero

```jsx
const {scrollY}=useScroll()


const y=useTransform(

scrollY,

[0,500],

[0,-200]

)


<motion.img

style={{

y

}}

/>
```

Image:

```
scroll down

image slowly moves up
```

---

# Complete API Summary

| API             | কাজ                       |
| --------------- | ------------------------- |
| whileInView     | Scroll animation          |
| AnimatePresence | Enter/Exit animation      |
| layout          | Automatic layout movement |
| drag            | Drag interaction          |
| useAnimation    | Manual animation control  |
| useMotionValue  | Track animation value     |
| useScroll       | Scroll value              |
| useTransform    | Value convert             |

---

এখন Framer Motion-এর প্রায় সব core API cover হলো।

পরের ধাপে শেখা উচিত:

1. **Advanced Variants + Stagger Children**
2. **Text Animation (letter by letter)**
3. **3D Card Hover Effect**
4. **Mouse Follow Animation**
5. **Apple / Awwwards style Landing Page Animation**
6. **Complete Next.js + Framer Motion project structure**

এগুলো শিখলে আপনি professional animation developer level-এ যেতে পারবেন।
চলুন **Framer Motion Advanced Professional Part** শুরু করি।

এখন আমরা শিখব:

17. Advanced Variants
18. Stagger Children
19. Text Animation (letter by letter)
20. 3D Card Hover Effect
21. Mouse Follow Animation
22. Gradient / Blob Animation
23. Apple-style Hero Animation
24. Complete Next.js project structure

---

# 17. Advanced Variants

আগে আমরা basic variants দেখেছি।

এখন দেখব parent-child animation।

ধরুন:

একটা container আছে:

```
Container
 |
 |-- Card 1
 |-- Card 2
 |-- Card 3
```

আপনি চান:

```
Container আসবে

↓

Card 1 আসবে

↓

Card 2 আসবে

↓

Card 3 আসবে
```

এটার জন্য `staggerChildren` ব্যবহার হয়।

---

## Parent Variant

```jsx
const container = {

hidden:{
opacity:0
},


show:{
opacity:1,

transition:{

staggerChildren:0.3

}

}

}
```

---

## Child Variant

```jsx
const item = {


hidden:{

opacity:0,
y:50

},


show:{

opacity:1,
y:0

}

}
```

---

## Full Example

```jsx
"use client"

import {motion} from "framer-motion"


const container={

hidden:{
opacity:0
},

show:{

opacity:1,

transition:{
staggerChildren:0.3
}

}

}



const item={

hidden:{
opacity:0,
y:50
},

show:{
opacity:1,
y:0
}

}



export default function App(){


return (

<motion.div

variants={container}

initial="hidden"

animate="show"

>


{
[1,2,3].map((i)=>(


<motion.div

key={i}

variants={item}

>

Card {i}


</motion.div>


))

}


</motion.div>

)


}
```

---

Result:

```
Card 1
   ↓
Card 2
   ↓
Card 3
```

---

# 18. Stagger Children Advanced

## Delay children

```javascript
transition:{


delayChildren:1,


staggerChildren:0.2


}
```

Meaning:

```
Wait 1 sec

Card 1

0.2 sec

Card 2

0.2 sec

Card 3
```

---

## Reverse Animation

```javascript
transition:{

staggerDirection:-1

}
```

Result:

```
Card 3

Card 2

Card 1
```

---

# 19. Text Animation (Letter by Letter)

এটা modern website-এ অনেক ব্যবহার হয়।

Example:

```
HELLO

H
HE
HEL
HELL
HELLO
```

---

## Step 1: Text split

```javascript
const text="HELLO"

const letters=text.split("")
```

Result:

```javascript
[
"H",
"E",
"L",
"L",
"O"
]
```

---

## Step 2: Animation

```jsx
"use client"


import {motion} from "framer-motion"



const container={

hidden:{},

show:{

transition:{

staggerChildren:0.1

}

}

}



const letter={


hidden:{

opacity:0,
y:50

},


show:{

opacity:1,
y:0

}


}



export default function TextAnimation(){


const text="HELLO"


return (


<motion.h1

variants={container}

initial="hidden"

animate="show"

>


{

text.split("").map((char,index)=>(


<motion.span

key={index}

variants={letter}

>

{char}


</motion.span>


))

}



</motion.h1>


)

}
```

---

Result:

```
H
 E
  L
   L
    O
```

এক এক করে আসবে।

---

# 20. 3D Card Hover Effect

Professional card animation:

Features:

* Rotate
* Scale
* Shadow
* Perspective

---

CSS:

```css
.card{

perspective:1000px;

}
```

---

React:

```jsx
<motion.div


whileHover={{

scale:1.05,

rotateX:10,

rotateY:-10


}}


transition={{

type:"spring"

}}


>


Card


</motion.div>
```

---

Effect:

Before:

```
---------
| Card |
---------
```

Hover:

```
   /
  /
 -------
| Card |
 -------
```

---

# 21. Mouse Follow Animation

Cursor যেখানে যাবে element সেখানে যাবে।

এটার জন্য:

* useMotionValue
* useSpring

ব্যবহার হয়।

---

Example:

```jsx
"use client"


import {

motion,

useMotionValue,

useSpring

}

from "framer-motion"



export default function App(){


const mouseX=useMotionValue(0)

const mouseY=useMotionValue(0)



const x=useSpring(mouseX)

const y=useSpring(mouseY)



return (

<div


onMouseMove={(e)=>{


mouseX.set(e.clientX)

mouseY.set(e.clientY)


}}


>


<motion.div


style={{

x,
y

}}


className="circle"


/>



</div>

)


}
```

---

Result:

```
Mouse move

↓

Circle follows
```

---

# 22. Blob Animation

Modern hero background:

```
   🔵
  moving
 blob
```

---

Example:

```jsx
<motion.div


animate={{

x:[0,100,0],

y:[0,-50,0],

scale:[1,1.2,1]


}}


transition={{

duration:5,

repeat:Infinity

}}


/>
```

---

Animation:

```
0s

○


2s

   ○


5s

○
```

---

# 23. Apple Style Hero Animation

Common structure:

```
Hero

Title
 |
Subtitle
 |
Button
 |
Image
```

---

Variants:

```javascript
const hero={


hidden:{

opacity:0,
y:100

},


show:{

opacity:1,
y:0,


transition:{

duration:1

}

}


}
```

---

Usage:

```jsx
<motion.h1

variants={hero}

initial="hidden"

animate="show"

>

Future Technology

</motion.h1>
```

---

Image:

```jsx
<motion.img


initial={{

scale:0.8,

opacity:0

}}


animate={{

scale:1,

opacity:1

}}


transition={{

delay:0.5

}}


/>
```

---

Result:

```
Title
  ↓
Subtitle
  ↓
Image
```

Premium landing page feel।

---

# 24. Complete Next.js Structure

Professional project:

```
src

app

 |
 layout.jsx

 |
 page.jsx


components


 |
 MotionWrapper.jsx

 |
 Hero.jsx

 |
 Card.jsx

 |
 Navbar.jsx


animations


 |
 variants.js


utils

 |
 motion.js

```

---

## variants.js

```javascript
export const fadeUp={


hidden:{

opacity:0,

y:50

},


show:{

opacity:1,

y:0

}


}
```

---

## Component

```jsx
import {fadeUp} from "@/animations/variants"


<motion.div

variants={fadeUp}

initial="hidden"

animate="show"

>

Content

</motion.div>
```

---

# Professional Framer Motion Checklist

এগুলো পারলে আপনি advanced level:

✅ motion
✅ variants
✅ staggerChildren
✅ AnimatePresence
✅ layout animation
✅ shared layout
✅ drag
✅ gestures
✅ scroll animation
✅ parallax
✅ text animation
✅ mouse interaction
✅ spring physics
✅ reusable animation system

---

পরের এবং শেষ বড় অংশে আমরা করব:

**Real Project Build:**

🔥 Next.js + Tailwind + Framer Motion দিয়ে

* Animated Navbar
* Hero Section
* Scroll Reveal Sections
* 3D Cards
* Modal
* Page Transition
* Smooth Scrolling
* Awwwards style portfolio website

একদম production structure সহ।
চলুন **Framer Motion Real Project Part** শুরু করি।

এবার আমরা একটি **Production-level Next.js + Tailwind + Framer Motion Portfolio/Landing Page** বানানোর structure দেখব।

Project features:

✅ Animated Navbar  
✅ Hero Section Animation  
✅ Text Reveal  
✅ Floating Image Animation  
✅ Scroll Reveal Sections  
✅ Stagger Cards  
✅ 3D Hover Cards  
✅ Modal Animation  
✅ Page Transition  
✅ Smooth UX Pattern

---

# Project Setup

## 1. Create Next.js Project

```bash
npx create-next-app@latest motion-project
```

Options:

```
✔ TypeScript → Yes
✔ Tailwind → Yes
✔ App Router → Yes
```

---

## Install Framer Motion

```bash
npm install framer-motion
```

---

# Folder Structure

Professional structure:

```
src
│
├── app
│   ├── layout.jsx
│   ├── page.jsx
│   └── globals.css
│
├── components
│   ├── Navbar.jsx
│   ├── Hero.jsx
│   ├── Card.jsx
│   ├── Modal.jsx
│   └── Section.jsx
│
├── animations
│   └── variants.js
│
└── utils
    └── motion.js
```

---

# 1. Animation System তৈরি

`animations/variants.js`

```javascript
export const fadeUp = {

hidden:{
opacity:0,
y:50
},

show:{

opacity:1,
y:0,

transition:{
duration:0.8
}

}

}
```

এখন এটা সব component-এ reuse করতে পারবেন।

---

# 2. Navbar Animation

`Navbar.jsx`

```jsx
"use client"

import {motion} from "framer-motion"


export default function Navbar(){


return (

<motion.nav

initial={{
y:-100,
opacity:0
}}

animate={{

y:0,
opacity:1

}}

transition={{

duration:0.7

}}

className="p-5 flex justify-between"

>


<h1>
Logo
</h1>


<div>

Home

About

Contact

</div>


</motion.nav>

)

}
```

---

Animation:

Page load:

```
Navbar

↓

top থেকে নিচে আসবে
```

---

# 3. Hero Section

Structure:

```
Hero

Title
Subtitle
Button
Image
```

---

`Hero.jsx`

```jsx
"use client"


import {motion} from "framer-motion"



const container={


hidden:{},


show:{


transition:{

staggerChildren:0.2

}


}


}



const item={


hidden:{


opacity:0,

y:50


},


show:{


opacity:1,

y:0


}


}




export default function Hero(){


return (

<section className="min-h-screen">


<motion.div

variants={container}

initial="hidden"

animate="show"


>


<motion.h1

variants={item}

className="text-6xl font-bold"

>

Build Amazing UI


</motion.h1>



<motion.p

variants={item}

>

Next.js + Framer Motion


</motion.p>



<motion.button

variants={item}

whileHover={{

scale:1.1

}}

whileTap={{

scale:0.9

}}

>

Start


</motion.button>



</motion.div>



</section>

)


}
```

---

Result:

```
Title
 ↓
Subtitle
 ↓
Button
```

একটার পর একটা আসবে।

---

# 4. Floating Image Animation

Hero image অনেক website-এ floating থাকে।

Example:

```jsx
<motion.img


animate={{

y:[0,-20,0]

}}


transition={{

duration:3,

repeat:Infinity,

ease:"easeInOut"

}}


/>
```

---

Result:

```
   Image

 ↑
 ↓

Floating effect
```

---

# 5. Scroll Reveal Section

Reusable Component:

`Section.jsx`

```jsx
"use client"


import {motion} from "framer-motion"


export default function Section({children}){


return (

<motion.section


initial={{

opacity:0,

y:80

}}


whileInView={{

opacity:1,

y:0

}}


viewport={{

once:true

}}


transition={{

duration:0.8

}}


>


{children}


</motion.section>

)

}
```

---

Use:

```jsx
<Section>

<h2>
About Me
</h2>

</Section>
```

---

এখন section scroll করলে animate হবে।

---

# 6. Animated Cards

Example:

```
Card 1
Card 2
Card 3
```

একটার পর একটা আসবে।

---

```jsx
const cards={


hidden:{


opacity:0,

y:40


},


show:{


opacity:1,

y:0


}


}
```

---

Component:

```jsx
<motion.div

variants={cards}

>

Card

</motion.div>
```

Parent:

```jsx
<motion.div

initial="hidden"

whileInView="show"


viewport={{

once:true

}}


transition={{

staggerChildren:0.3

}}

>
```

---

Result:

```
Card 1
   ↓
Card 2
   ↓
Card 3
```

---

# 7. 3D Hover Card

Card:

```jsx
<motion.div


whileHover={{

scale:1.05,

rotateX:10,

rotateY:-10

}}


transition={{

type:"spring"

}}


className="card"


>

Project

</motion.div>
```

---

Effect:

Normal:

```
---------
| Card |
---------
```

Hover:

```
  ______
 / Card/
--------
```

---

# 8. Modal Animation

Common pattern:

```jsx
<AnimatePresence>

{

open &&

<motion.div


initial={{

opacity:0,

scale:.8

}}


animate={{

opacity:1,

scale:1

}}


exit={{

opacity:0,

scale:.8

}}


>

Modal


</motion.div>

}


</AnimatePresence>
```

---

Use:

- Login popup
    
- Image preview
    
- Menu
    

---

# 9. Page Transition

`template.jsx`

App Router এ:

```
app

template.jsx
```

Create করুন:

```jsx
"use client"


import {motion} from "framer-motion"



export default function Template({children}){


return (


<motion.div


initial={{

opacity:0

}}


animate={{

opacity:1

}}


transition={{

duration:.5

}}


>


{children}


</motion.div>


)


}
```

---

এখন page change হলে fade animation হবে।

---

# 10. Scroll Progress Bar

Top progress indicator:

```jsx
"use client"


import {

useScroll,

motion

}

from "framer-motion"



export default function Progress(){


const {

scrollYProgress

}=useScroll()



return (

<motion.div


style={{

scaleX:scrollYProgress

}}


className="fixed top-0 h-1 bg-blue-500 w-full"


/>

)


}
```

---

Result:

```
Scroll ↓

███████------


100%
```

---

# 11. Parallax Hero

Image:

```jsx
const {

scrollY

}=useScroll()



const y=useTransform(

scrollY,

[0,500],

[0,-200]

)
```

---

Use:

```jsx
<motion.img

style={{

y

}}

/>
```

Result:

Background slow move করবে।

---

# Production Tips

## Animation বেশি করবেন না

Bad:

```
সব element animate
```

Good:

```
Important elements animate
```

---

## Use variants

Bad:

```jsx
initial={}
animate={}
```

সব জায়গায় repeat করা।

Good:

```jsx
variants={fadeUp}
```

---

## Mobile performance

Avoid:

❌ heavy blur animation  
❌ huge shadows  
❌ too many particles

Prefer:

✅ opacity  
✅ transform  
✅ scale  
✅ translate

---

# এখন পর্যন্ত আপনি শিখেছেন:

```
Basic Motion
        ↓
Variants
        ↓
Stagger
        ↓
Scroll Animation
        ↓
Gestures
        ↓
Advanced Hooks
        ↓
Production Architecture
```

পরের অংশে আমরা করব:

**Framer Motion + Tailwind দিয়ে Awwwards style Website Animation**

যেখানে থাকবে:

🔥 Magnetic Button  
🔥 Cursor Follow  
🔥 Image Reveal Animation  
🔥 Smooth Page Transition  
🔥 SVG Animation  
🔥 Loading Screen  
🔥 Luxury Landing Page Effect (Apple / Stripe style)

চলুন **Framer Motion Awwwards / Apple Style Advanced Animation Part** শুরু করি।

এই অংশে আমরা শিখব:

1. Magnetic Button
2. Custom Cursor Follow
3. Image Reveal Animation
4. SVG Animation
5. Loading Screen Animation
6. Smooth Page Transition Advanced
7. Luxury Hero Section Pattern
8. Performance Optimization

---

# 25. Magnetic Button Animation

## Magnetic Button কী?

Button-এর কাছে mouse গেলে button cursor-এর দিকে একটু টেনে আসে।

এটা ব্যবহার হয়:

* Premium portfolio
* Agency website
* Creative landing page

Example:

```
Normal:

      🖱️

   [ Button ]


Mouse কাছে:

      🖱️

    [Button]
       ↗
```

---

## Implementation

```jsx
"use client"

import {
motion,
useMotionValue,
useSpring
}
from "framer-motion"

import {useRef} from "react"


export default function MagneticButton(){


const ref=useRef(null)


const x=useMotionValue(0)
const y=useMotionValue(0)


const springX=useSpring(x,{
stiffness:150,
damping:10
})


const springY=useSpring(y,{
stiffness:150,
damping:10
})


function move(e){

const box=ref.current.getBoundingClientRect()


const centerX=box.left + box.width/2
const centerY=box.top + box.height/2


x.set((e.clientX-centerX)*0.3)

y.set((e.clientY-centerY)*0.3)

}


function leave(){

x.set(0)
y.set(0)

}


return (

<motion.button

ref={ref}

style={{

x:springX,
y:springY

}}

onMouseMove={move}

onMouseLeave={leave}

className="
bg-black
text-white
px-8
py-4
rounded-full
"

>

Hover Me

</motion.button>

)

}
```

---

এখানে ব্যবহার হয়েছে:

```
useMotionValue
        +
useSpring
        +
motion style
```

---

# 26. Custom Cursor Follow Animation

Modern website-এ cursor replace করা হয়।

Example:

```
Normal cursor:

  ▲


Custom:

     ●
```

---

## Cursor Component

```jsx
"use client"


import {

motion,

useMotionValue,

useSpring

}

from "framer-motion"



export default function Cursor(){


const mouseX=useMotionValue(0)

const mouseY=useMotionValue(0)



const x=useSpring(mouseX)

const y=useSpring(mouseY)



return (

<div

onMouseMove={(e)=>{

mouseX.set(e.clientX)
mouseY.set(e.clientY)

}}

>


<motion.div

style={{

x,
y

}}

className="
fixed
w-5
h-5
rounded-full
bg-black
pointer-events-none
"


/>


</div>

)

}
```

---

Result:

Mouse move করলে:

```
Cursor
   |
   |
   ↓

● follow করবে
```

---

# 27. Image Reveal Animation

এটা খুব popular।

Example:

Image আসবে cover সরিয়ে:

Before:

```
████████
████████
```

After:

```
IMAGE
IMAGE
```

---

## Technique

একটা black overlay থাকবে।

Structure:

```
Container

Image

Overlay
```

---

Code:

```jsx
"use client"


import {motion} from "framer-motion"


export default function ImageReveal(){


return (

<div
className="
relative
overflow-hidden
"
>


<motion.img

initial={{

scale:1.3

}}

animate={{

scale:1

}}

transition={{

duration:1.2

}}

src="/image.jpg"

/>



<motion.div


initial={{

x:"0%"

}}


animate={{

x:"100%"

}}


transition={{

duration:1

}}


className="
absolute
inset-0
bg-black
"


/>


</div>

)

}
```

---

Effect:

```
Black cover

↓

slide away

↓

Image reveal
```

---

# 28. Text Reveal Animation

Premium heading:

Example:

```
BUILD
YOUR
DREAM
```

এক লাইন করে আসবে।

---

Code:

```jsx
const words=[
"BUILD",
"YOUR",
"DREAM"
]


<motion.div>


{
words.map((word,i)=>(


<motion.h1

key={word}

initial={{

y:100

}}

animate={{

y:0

}}

transition={{

delay:i*0.2

}}

>

{word}

</motion.h1>


))

}


</motion.div>
```

---

Result:

```
BUILD
 ↓
YOUR
 ↓
DREAM
```

---

# 29. SVG Animation

Framer Motion SVG animate করতে পারে।

Use:

* Logo animation
* Icons
* Drawing effect

Example:

```jsx
<motion.svg

width="200"

height="200"

>


<motion.circle

cx="100"

cy="100"

r="50"

stroke="black"

fill="transparent"


initial={{

pathLength:0

}}


animate={{

pathLength:1

}}


transition={{

duration:2

}}


/>


</motion.svg>
```

---

Result:

```
Circle draw হবে

○ → ◯ → ●
```

---

# 30. Loading Screen Animation

Website load হওয়ার আগে:

```
Loading...

100%

Website
```

---

Component:

```jsx
"use client"


import {

motion

}

from "framer-motion"



export default function Loader(){


return (

<motion.div


initial={{

y:0

}}


animate={{

y:"-100%"

}}


transition={{

delay:2,

duration:1

}}


className="
fixed
inset-0
bg-black
"

>


<h1 className="text-white">

Loading

</h1>


</motion.div>

)

}
```

---

Flow:

```
0 sec

Black screen


2 sec

slide up


Website visible
```

---

# 31. Advanced Page Transition

Professional transition:

```
Page A

████████

↓

Page B

████████
```

---

`template.jsx`

```jsx
"use client"


import {

motion

}

from "framer-motion"



const variants={


hidden:{

opacity:0,
y:20

},


enter:{

opacity:1,
y:0

},


exit:{

opacity:0,
y:-20

}


}



export default function Template({children}){


return (

<motion.main


variants={variants}

initial="hidden"

animate="enter"

exit="exit"


>

{children}


</motion.main>

)

}
```

---

# 32. Luxury Hero Section Pattern

Professional landing page structure:

```
Navbar

        Title
        Subtitle
        Button


        3D Image


Scroll ↓


Features


Cards


Footer
```

---

Animation sequence:

```
Navbar
   |
   ↓
Title
   |
   ↓
Subtitle
   |
   ↓
Button
   |
   ↓
Image
```

---

Implementation:

```jsx
const heroContainer={


hidden:{},


show:{


transition:{

staggerChildren:0.25

}

}

}


const heroItem={


hidden:{

opacity:0,
y:40

},


show:{

opacity:1,
y:0

}

}
```

---

# 33. Performance Optimization

Framer Motion powerful, কিন্তু optimize করতে হবে।

---

## Prefer transform

Good:

```jsx
x
y
scale
rotate
```

কারণ GPU use করে।

---

Avoid:

```jsx
width
height
top
left
```

বারবার animate করা।

---

## Use LazyMotion

Large apps:

```jsx
import {
LazyMotion,
domAnimation,
m
}
from "framer-motion"
```

এতে bundle size কমে।

---

## Reduce animation on mobile

```javascript
const prefersReducedMotion =
window.matchMedia(
"(prefers-reduced-motion)"
)
```

---

# 34. Final Professional Skill Map

এখন আপনি জানেন:

## Basic

✅ motion
✅ initial
✅ animate
✅ transition
✅ hover
✅ tap

## Intermediate

✅ variants
✅ stagger
✅ AnimatePresence
✅ layout
✅ drag
✅ scroll

## Advanced

✅ useMotionValue
✅ useTransform
✅ magnetic effect
✅ cursor effect
✅ SVG animation
✅ image reveal
✅ page transition

## Professional

✅ Animation architecture
✅ Reusable variants
✅ Performance optimization
✅ Awwwards style effects

---

পরের অংশ হবে:

**Framer Motion Master Project Build**

আমরা বানাবো:

🔥 Complete Awwwards Portfolio Website
🔥 Next.js App Router
🔥 Tailwind CSS
🔥 Framer Motion
🔥 Smooth Scroll
🔥 Animated Navbar
🔥 Hero
🔥 Projects Gallery
🔥 Contact Section
🔥 Page Transition

একদম real client project structure-এর মতো।
চলুন **Framer Motion Master Project Build (Part 1)** শুরু করি।

আমরা এবার একটি **Awwwards-style Portfolio Website** বানানোর architecture দেখব।

Tech Stack:

```
Next.js 15
+
Tailwind CSS
+
Framer Motion
+
TypeScript (optional)
```

Project features:

✅ Smooth Navbar
✅ Hero Animation
✅ Magnetic Button
✅ Text Reveal
✅ Scroll Animation
✅ Project Gallery
✅ 3D Cards
✅ Image Reveal
✅ Contact Animation
✅ Page Transition

---

# Project Structure

Professional structure:

```
src
│
├── app
│   ├── layout.tsx
│   ├── page.tsx
│   ├── template.tsx
│
├── components
│   │
│   ├── Navbar.tsx
│   ├── Hero.tsx
│   ├── Button.tsx
│   ├── ProjectCard.tsx
│   ├── Projects.tsx
│   ├── Contact.tsx
│
├── animations
│   ├── variants.ts
│
├── hooks
│   ├── useMousePosition.ts
│
└── data
    └── projects.ts
```

---

# 1. Global Animation Setup

`animations/variants.ts`

```ts
export const fadeUp = {

hidden:{
opacity:0,
y:80
},

show:{

opacity:1,

y:0,

transition:{
duration:0.8,
ease:"easeOut"
}

}

}


export const staggerContainer = {

hidden:{},


show:{

transition:{

staggerChildren:0.15

}

}

}
```

---

এখন আমরা বারবার একই animation লিখব না।

Use:

```tsx
variants={fadeUp}
```

---

# 2. Layout Setup

`app/layout.tsx`

```tsx
import "./globals.css"


export default function RootLayout({

children

}:{

children:React.ReactNode

}){


return (

<html lang="en">

<body>

{children}

</body>

</html>

)

}
```

---

# 3. Page Transition

`app/template.tsx`

```tsx
"use client"


import {motion} from "framer-motion"



export default function Template({

children

}:{

children:React.ReactNode

}){


return (

<motion.main


initial={{

opacity:0

}}


animate={{

opacity:1

}}


transition={{

duration:.6

}}


>

{children}


</motion.main>

)

}
```

---

এখন প্রতিটি page change smooth হবে।

---

# 4. Animated Navbar

`components/Navbar.tsx`

```tsx
"use client"


import {motion} from "framer-motion"



export default function Navbar(){


return (

<motion.nav


initial={{

y:-100

}}


animate={{

y:0

}}


transition={{

duration:.8

}}


className="
fixed
top-0
w-full
flex
justify-between
p-6
"


>


<h1 className="text-2xl font-bold">

LOGO

</h1>



<div className="flex gap-8">


<a>
Home
</a>


<a>
Work
</a>


<a>
Contact
</a>


</div>


</motion.nav>


)

}
```

---

Animation:

```
Page load

Navbar

⬇

Top থেকে আসবে
```

---

# 5. Hero Section

Structure:

```
Small Text

BIG TITLE

Description

Button

Image
```

---

`Hero.tsx`

```tsx
"use client"


import {

motion

}

from "framer-motion"



import {

staggerContainer,
fadeUp

}

from "@/animations/variants"



export default function Hero(){


return (

<section

className="
min-h-screen
flex
items-center
"

>


<motion.div


variants={staggerContainer}

initial="hidden"

animate="show"


>


<motion.p

variants={fadeUp}

>

Creative Developer

</motion.p>



<motion.h1

variants={fadeUp}

className="
text-7xl
font-bold
"

>

Build Digital Experiences


</motion.h1>




<motion.p

variants={fadeUp}

>

I create modern web applications

with beautiful animations.

</motion.p>



<motion.button


variants={fadeUp}


whileHover={{

scale:1.1

}}


whileTap={{

scale:.9

}}


className="
bg-black
text-white
px-8
py-4
rounded-full
"

>

View Work

</motion.button>



</motion.div>


</section>

)

}
```

---

Result:

```
Creative Developer
        ↓
BIG TITLE
        ↓
Description
        ↓
Button
```

একটার পর একটা আসবে।

---

# 6. Magnetic Button Component

Reusable button:

`Button.tsx`

```tsx
"use client"


import {

motion,
useMotionValue,
useSpring

}

from "framer-motion"



import {useRef} from "react"



export default function Button(){


const ref=useRef<HTMLButtonElement>(null)



const x=useMotionValue(0)

const y=useMotionValue(0)



const springX=useSpring(x)

const springY=useSpring(y)



function move(e:React.MouseEvent){


const box=

ref.current?.getBoundingClientRect()


if(!box)return



x.set(

(e.clientX-box.left-box.width/2)*0.3

)


y.set(

(e.clientY-box.top-box.height/2)*0.3

)


}



return (

<motion.button


ref={ref}


style={{

x:springX,

y:springY

}}



onMouseMove={move}



onMouseLeave={()=>{

x.set(0)

y.set(0)

}}



>

Explore

</motion.button>

)

}
```

---

Effect:

Mouse কাছে:

```
Cursor

 ↗

[ Explore ]
```

Button একটু move করবে।

---

# 7. Main Page

`app/page.tsx`

```tsx
import Navbar from "@/components/Navbar"

import Hero from "@/components/Hero"



export default function Home(){


return (

<main>


<Navbar/>


<Hero/>


</main>

)

}
```

---

এখন আপনার প্রথম Awwwards style foundation তৈরি।

---

পরের Part-এ আমরা বানাব:

### Master Project Part 2

🔥 Project Gallery Section
🔥 Scroll Reveal Cards
🔥 Stagger Grid Animation
🔥 3D Hover Project Card
🔥 Image Parallax
🔥 Modal Project Preview
🔥 Shared Layout Animation (`layoutId`)

এগুলো শিখলে portfolio, agency, SaaS landing page-এর animation নিজে বানাতে পারবেন।
