https://motion.dev/docs/react

https://www.youtube.com/watch?v=OkWWAgLSGkc

In **Motion for React (`motion/react`)**, you can animate almost any CSS-like property. The `animate` prop accepts an object where the keys are the properties you want to change.

Example:

```jsx
import { motion } from "motion/react";

export default function Box() {
  return (
    <motion.div
      animate={{
        x: 100,
        y: 50,
        rotate: 45,
        scale: 1.2,
        opacity: 0.5,
      }}
    />
  );
}
```

Below are the main animation properties and what they do:

---

## 1. Position

### `x`

Moves horizontally

```jsx
animate={{ x: 100 }}
```

Moves right by 100px.

---

### `y`

Moves vertically

```jsx
animate={{ y: 50 }}
```

Moves down by 50px.

---

### `translateX`

CSS-style horizontal movement

```jsx
animate={{ translateX: 100 }}
```

---

### `translateY`

```jsx
animate={{ translateY: 100 }}
```

---

## 2. Rotation

### `rotate`

```jsx
animate={{ rotate: 180 }}
```

Rotates degrees.

---

### `rotateX`

```jsx
animate={{ rotateX: 180 }}
```

3D horizontal rotation.

---

### `rotateY`

```jsx
animate={{ rotateY: 180 }}
```

3D vertical rotation.

---

## 3. Scale

### `scale`

```jsx
animate={{ scale: 2 }}
```

Makes element twice bigger.

---

### `scaleX`

```jsx
animate={{ scaleX: 2 }}
```

Stretches horizontally.

---

### `scaleY`

```jsx
animate={{ scaleY: 2 }}
```

Stretches vertically.

---

## 4. Transparency

### `opacity`

```jsx
animate={{ opacity: 0 }}
```

`0` = invisible  
`1` = visible

---

## 5. Size

### `width`

```jsx
animate={{ width: 300 }}
```

---

### `height`

```jsx
animate={{ height: 300 }}
```

---

Example:

```jsx
<motion.div
  animate={{
    width: 300,
    height: 200
  }}
/>
```

---

## 6. Colors

### `backgroundColor`

```jsx
animate={{
  backgroundColor: "#ff0000"
}}
```

---

### `color`

Text color:

```jsx
animate={{
  color: "blue"
}}
```

---

### `borderColor`

```jsx
animate={{
  borderColor: "red"
}}
```

---

## 7. Border

### `borderRadius`

```jsx
animate={{
  borderRadius: 50
}}
```

Turns square into rounded.

---

### `borderWidth`

```jsx
animate={{
  borderWidth: 5
}}
```

---

## 8. Shadow

### `boxShadow`

```jsx
animate={{
 boxShadow: "0px 10px 20px gray"
}}
```

---

## 9. Skew

### `skewX`

```jsx
animate={{
 skewX: 30
}}
```

Slants horizontally.

---

### `skewY`

```jsx
animate={{
 skewY: 20
}}
```

Slants vertically.

---

## 10. Filters

### `filter`

Blur, brightness, etc.

```jsx
animate={{
 filter: "blur(10px)"
}}
```

Examples:

```jsx
filter:
"brightness(2)"

filter:
"contrast(2)"

filter:
"grayscale(1)"
```

---

## 11. SVG properties

Works with SVG:

### `pathLength`

```jsx
<motion.path
 animate={{
   pathLength: 1
 }}
/>
```

---

### `stroke`

```jsx
animate={{
 stroke: "red"
}}
```

---

### `fill`

```jsx
animate={{
 fill: "blue"
}}
```

---

## 12. CSS variables

```jsx
animate={{
 "--x": "100px"
}}
```

---

## 13. Gesture animations

### Hover

```jsx
whileHover={{
 scale: 1.2
}}
```

---

### Tap

```jsx
whileTap={{
 scale: 0.8
}}
```

---

### Drag

```jsx
drag
animate={{
 x: 200
}}
```

---

## 14. Transition control

Controls how animation happens:

```jsx
<motion.div
 animate={{
   x: 200
 }}
 transition={{
   duration: 2,
   delay: 1,
   ease: "easeInOut"
 }}
/>
```

Properties:

|Property|Meaning|
|---|---|
|duration|animation time|
|delay|wait before start|
|ease|speed curve|
|repeat|repeat count|
|repeatType|loop/yoyo|
|type|spring/tween|

---

## Complete example

```jsx
<motion.div
  initial={{
    opacity:0,
    x:-100,
    rotate:0
  }}

  animate={{
    opacity:1,
    x:100,
    y:50,
    rotate:360,
    scale:1.5,
    backgroundColor:"purple",
    borderRadius:50,
    boxShadow:"0px 20px 30px gray"
  }}

  transition={{
    duration:2,
    type:"spring"
  }}
/>
```

This animates:

- position
    
- rotation
    
- size
    
- color
    
- border
    
- shadow
    
- transparency
    

Most CSS properties that can be interpolated can be animated with `animate`.

----------
# which property apply
`animate`-এ সব CSS property কাজ করে না। তবে যেগুলো সবচেয়ে বেশি ব্যবহার হয়, সেগুলো নিচে category অনুযায়ী দিলাম।

## Transform Properties

```jsx
animate={{
  x: 100,
  y: -50,
  scale: 1.2,
  scaleX: 1.5,
  scaleY: 0.8,
  rotate: 45,
  rotateX: 30,
  rotateY: 30,
  skewX: 10,
  skewY: 10,
}}
```

## Opacity

```jsx
animate={{
  opacity: 0.5,
}}
```

## Size

```jsx
animate={{
  width: 300,
  height: 200,
  maxWidth: 500,
  maxHeight: 400,
}}
```

## Spacing

```jsx
animate={{
  marginTop: 20,
  marginLeft: 30,
  padding: 20,
}}
```

## Position

```jsx
animate={{
  top: 50,
  left: 100,
  right: 20,
  bottom: 10,
}}
```

⚠️ `position: absolute/fixed/relative` animate হয় না, কিন্তু `top`, `left` ইত্যাদি animate হতে পারে।

## Colors

```jsx
animate={{
  backgroundColor: "#3b82f6",
  color: "#ffffff",
  borderColor: "#ef4444",
}}
```

## Border

```jsx
animate={{
  borderRadius: 20,
  borderWidth: 5,
}}
```

## Shadow

```jsx
animate={{
  boxShadow: "0 10px 30px rgba(0,0,0,0.3)",
}}
```

## Filter

```jsx
animate={{
  filter: "blur(5px)",
}}
```

আরও:

```jsx
animate={{
  filter: "brightness(150%)",
}}
```

## Clip Path

```jsx
animate={{
  clipPath: "circle(50%)",
}}
```

## Text

```jsx
animate={{
  letterSpacing: "5px",
  lineHeight: "2",
}}
```

---

## যেগুলো Animate হয় না

```jsx
animate={{
  display: "none",
  position: "absolute",
  overflow: "hidden",
  zIndex: 999,
}}
```

এগুলো state change করতে পারো, কিন্তু smooth animation হবে না।

---

## সবচেয়ে বেশি ব্যবহৃত

```jsx
animate={{
  x: 100,
  y: -20,
  scale: 1.1,
  rotate: 10,
  opacity: 0.8,
  backgroundColor: "#2563eb",
  borderRadius: 20,
  boxShadow: "0 10px 20px rgba(0,0,0,.2)",
}}
```

বাস্তব project-এ ৮০% animation সাধারণত `x`, `y`, `scale`, `rotate`, `opacity`, `backgroundColor`, `borderRadius`, `boxShadow` দিয়েই করা হয়।

----------------

# In **Motion for React (`motion/react`)**, the `transition` prop controls **how an animation moves from one state to another**.

Example:

```jsx
import { motion } from "motion/react";

<motion.div
  animate={{ x: 200 }}
  transition={{
    duration: 2,
    ease: "easeInOut"
  }}
/>
```

Here are the main `transition` properties:

---

# 1. `duration`

Controls animation length (seconds).

```jsx
transition={{
  duration: 2
}}
```

- `0.5` → fast
    
- `2` → slow
    

Example:

```jsx
animate={{ opacity: 1 }}
transition={{ duration: 3 }}
```

Fade takes 3 seconds.

---

# 2. `delay`

Wait before animation starts.

```jsx
transition={{
  delay: 1
}}
```

Example:

```jsx
animate={{ x: 100 }}
transition={{
  delay: 2,
  duration: 1
}}
```

Timeline:

```
0s -------- 2s -------- 3s
wait        animation
```

---

# 3. `ease`

Controls the speed curve.

## Built-in easing

### `linear`

Same speed entire time.

```jsx
transition={{
 ease:"linear"
}}
```

Movement:

```
|----------------|
same speed
```

---

### `easeIn`

Starts slow, ends fast.

```jsx
ease:"easeIn"
```

Good for:

- leaving screen
    
- disappearing
    

---

### `easeOut`

Starts fast, ends slow.

```jsx
ease:"easeOut"
```

Good for:

- appearing
    
- dropping objects
    

---

### `easeInOut`

Slow → fast → slow

```jsx
ease:"easeInOut"
```

Most common.

---

## Custom cubic bezier

```jsx
transition={{
 ease:[0.42,0,0.58,1]
}}
```

Format:

```
[x1,y1,x2,y2]
```

Example:

```jsx
ease:[0,0.71,0.2,1.01]
```

Creates custom motion.

---

# 4. `type`

Defines animation physics.

Options:

```
"tween"
"spring"
"inertia"
```

---

## tween

Normal duration animation.

```jsx
transition={{
 type:"tween"
}}
```

Uses:

- duration
    
- ease
    

Example:

```jsx
transition={{
 type:"tween",
 duration:2
}}
```

---

## spring

Physics-based animation.

```jsx
transition={{
 type:"spring"
}}
```

Example:

```jsx
<motion.div
 animate={{x:300}}
 transition={{
   type:"spring"
 }}
/>
```

Feels like a real object.

---

# Spring properties

## `stiffness`

Spring strength.

Default around:

```
100
```

Higher:

```jsx
stiffness:500
```

= faster, harder spring

Lower:

```jsx
stiffness:50
```

= soft movement

Example:

```jsx
transition={{
 type:"spring",
 stiffness:200
}}
```

---

## `damping`

Controls bouncing.

```jsx
damping:10
```

Low damping:

```
bounce bounce bounce
```

High damping:

```
smooth stop
```

Example:

```jsx
transition={{
 type:"spring",
 damping:20
}}
```

---

## `mass`

Object weight.

```jsx
mass:2
```

Higher mass:

- slower
    
- heavier feeling
    

Lower mass:

- quicker
    

Example:

```jsx
transition={{
 type:"spring",
 mass:0.5
}}
```

---

## `bounce`

Controls overshoot.

```jsx
bounce:0.5
```

Range:

```
0 = no bounce
1 = maximum bounce
```

Example:

```jsx
transition={{
 type:"spring",
 bounce:0.8
}}
```

---

# 5. `repeat`

Repeat animation.

```jsx
transition={{
 repeat:3
}}
```

Runs:

```
1 → 2 → 3 → 4
```

Infinite:

```jsx
repeat:Infinity
```

Example:

```jsx
animate={{rotate:360}}

transition={{
 repeat:Infinity,
 duration:2
}}
```

---

# 6. `repeatType`

How repeating behaves.

## loop

Default

```jsx
repeatType:"loop"
```

```
→→→→→
```

---

## reverse

Forward then backward.

```jsx
repeatType:"reverse"
```

```
→←→←
```

Example:

```jsx
animate={{
 x:200
}}

transition={{
 repeat:Infinity,
 repeatType:"reverse"
}}
```

---

## mirror

Same as reverse but swaps start/end.

```jsx
repeatType:"mirror"
```

---

# 7. `repeatDelay`

Delay between repeats.

```jsx
transition={{
 repeat:Infinity,
 repeatDelay:1
}}
```

Timeline:

```
move
wait
move
wait
```

---

# 8. `when`

Controls parent/child timing.

Used with variants.

## beforeChildren

Parent first:

```jsx
transition={{
 when:"beforeChildren"
}}
```

---

## afterChildren

Children first:

```jsx
transition={{
 when:"afterChildren"
}}
```

---

# 9. `staggerChildren`

Delay children animations.

Example:

```jsx
<motion.ul
 variants={{
  show:{
   transition:{
    staggerChildren:0.2
   }
  }
 }}
/>
```

Children:

```
item 1
   item 2
      item 3
```

---

# 10. `delayChildren`

Delay all children.

```jsx
transition={{
 delayChildren:1
}}
```

---

# 11. `times`

Controls keyframe timing.

Example:

```jsx
animate={{
 x:[0,100,200]
}}

transition={{
 duration:3,
 times:[0,0.5,1]
}}
```

Meaning:

```
0s   x=0
1.5s x=100
3s   x=200
```

---

# 12. `velocity`

Starting speed.

Mostly for drag/inertia.

```jsx
transition={{
 velocity:500
}}
```

---

# 13. `restSpeed`

Spring stop speed.

```jsx
transition={{
 restSpeed:0.1
}}
```

Animation stops when speed is below this.

---

# 14. `restDelta`

Precision for spring ending.

```jsx
transition={{
 restDelta:0.01
}}
```

Smaller = more accurate.

---

# Full transition example

```jsx
<motion.div

animate={{
 x:300,
 rotate:360,
 scale:1.5
}}

transition={{

 type:"spring",

 stiffness:200,
 damping:15,
 mass:0.8,

 delay:0.5,

 repeat:Infinity,
 repeatType:"reverse",
 repeatDelay:1

}}

 />
```

This creates:

- spring physics
    
- delay
    
- infinite animation
    
- reverse motion
    
- rotation + movement + scaling
    

---

A good mental model:

```
transition = {
  HOW FAST?       duration
  WHEN START?     delay
  HOW MOVE?       ease/type
  HOW MANY TIMES? repeat
  HOW PHYSICAL?   stiffness/damping/mass
}
```


------------
# এটাকে একটা **decision rule** হিসেবে শিখলে আর confusion থাকবে না। Motion-এ `initial`, `animate`, `whileInView`, `whileHover`, `whileTap`, `transition`—প্রতিটা আলাদা situation-এর জন্য।

## 1. `initial` → শুরুতে কেমন থাকবে

**Question:** "Animation শুরু হওয়ার আগে element কেমন থাকবে?"

```jsx
<motion.div
  initial={{ opacity: 0, y: 40 }}
>
```

মানে:

```text
শুরু:
opacity = 0
y = 40
```

সাধারণত:

```text
opacity: 0
y: 20/40/50
scale: 0.8
```

দেবে।

### Example

```jsx
<motion.h1
  initial={{ opacity: 0, y: 30 }}
>
  Welcome
</motion.h1>
```

---

# 2. `animate` → সাধারণ target state

**Question:** "Element-টা শেষ পর্যন্ত কোথায়/কী অবস্থায় যাবে?"

```jsx
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
>
```

মানে:

```text
initial
   ↓
invisible

animate
   ↓
visible
```

### কখন?

যখন component render হওয়ার পর **automatically animation** করতে চাও।

```jsx
<motion.div
  initial={{ x: -100 }}
  animate={{ x: 0 }}
>
```

Page load → left থেকে আসবে।

---

# 3. `whileInView` → screen-এ এলে

**Question:** "User scroll করে element-টা দেখতে পেলে কী হবে?"

```jsx
<motion.div
  initial={{ opacity: 0, y: 50 }}
  whileInView={{ opacity: 1, y: 0 }}
>
```

এটা তোমার website-এর:

* About section
* Services
* Product cards
* Testimonials
* Features

এর জন্য খুব useful।

### Mental model

```text
Page load
   ↓
element এখনো দেখা যায়নি
   ↓
scroll
   ↓
element viewport-এ আসলো
   ↓
whileInView
```

---

# 4. `whileHover` → mouse রাখলে

**Question:** "Mouse hover করলে কী হবে?"

```jsx
<motion.div
  whileHover={{ scale: 1.05 }}
>
```

যেমন Product Card:

```jsx
<motion.div
  whileHover={{ y: -8, scale: 1.02 }}
>
  Product
</motion.div>
```

Mouse ঢুকলে:

```text
Card
 ↓
উপরে উঠবে + একটু বড় হবে
```

Mouse বের করলে আবার original অবস্থায় ফিরে যাবে।

---

# 5. `whileTap` → click/press করলে

**Question:** "User button press করলে কী হবে?"

```jsx
<motion.button
  whileTap={{ scale: 0.95 }}
>
  Buy Now
</motion.button>
```

Click করার সময় button একটু ছোট হবে।

এটা button-এর জন্য খুব natural:

```jsx
<motion.button
  whileHover={{ scale: 1.05 }}
  whileTap={{ scale: 0.95 }}
>
  Submit
</motion.button>
```

---

# 6. `transition` → animation কীভাবে হবে

এটা খুব important।

**Question:** "Animation কত দ্রুত/কী ধরনের হবে?"

```jsx
transition={{ duration: 0.5 }}
```

এটা নিজে animation না।

বরং animation-এর **behavior control করে**।

### Example

```jsx
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 1 }}
>
```

এখানে:

```text
initial → opacity 0
animate → opacity 1
transition → 1 second
```

---

# 7. সবগুলো একসাথে

এখন তোমার code-এর মতো একটা real example:

```jsx
<motion.div
  initial={{ opacity: 0, y: 40 }}
  whileInView={{ opacity: 1, y: 0 }}
  whileHover={{ y: -8 }}
  transition={{ duration: 0.5 }}
>
  Hotel Card
</motion.div>
```

এখানে:

```text
initial
   ↓
শুরুতে invisible + নিচে

whileInView
   ↓
screen-এ এলে visible + normal position

whileHover
   ↓
mouse রাখলে 8px উপরে

transition
   ↓
সব animation smooth করে
```

---

# 8. `animate` আর `whileInView`-এর পার্থক্য

এখানেই beginner-দের বেশি confusion হয়।

### `animate`

```jsx
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
>
```

Component render হওয়ার পর animation শুরু হবে।

```text
Page load
 ↓
Animation
```

### `whileInView`

```jsx
<motion.div
  initial={{ opacity: 0 }}
  whileInView={{ opacity: 1 }}
>
```

User scroll করে element দেখার মধ্যে আসার পর animation হবে।

```text
Page load
 ↓
scroll
 ↓
element visible
 ↓
Animation
```

---

# 9. কখন কোনটা ব্যবহার করবে — Cheat Sheet

| তোমার দরকার               | ব্যবহার করবে  |
| ------------------------- | ------------- |
| শুরুতে hidden             | `initial`     |
| Automatically animate     | `animate`     |
| Scroll করে আসলে animate   | `whileInView` |
| Mouse hover               | `whileHover`  |
| Mouse click/press         | `whileTap`    |
| Keyboard focus            | `whileFocus`  |
| Drag করার সময়             | `whileDrag`   |
| Animation-এর speed/effect | `transition`  |

---

# 10. Practical UI অনুযায়ী

### Hero section

```jsx
initial
+
animate
```

```jsx
<motion.h1
  initial={{ opacity: 0, y: 30 }}
  animate={{ opacity: 1, y: 0 }}
>
  Build Better Websites
</motion.h1>
```

---

### Product Card

```jsx
whileHover
```

```jsx
<motion.div
  whileHover={{ y: -8 }}
>
  Product
</motion.div>
```

---

### Scroll Section

```jsx
initial
+
whileInView
```

```jsx
<motion.section
  initial={{ opacity: 0, y: 50 }}
  whileInView={{ opacity: 1, y: 0 }}
>
  About Us
</motion.section>
```

---

### Button

```jsx
whileHover
+
whileTap
```

```jsx
<motion.button
  whileHover={{ scale: 1.05 }}
  whileTap={{ scale: 0.95 }}
>
  Buy Now
</motion.button>
```

---

### Modal

এখানে পরে শিখবে:

```text
AnimatePresence
+
initial
+
animate
+
exit
```

---

## সবচেয়ে সহজে মনে রাখো

```text
initial
↓
"শুরুতে আমি কেমন?"

animate
↓
"নিজে নিজে কোথায় যাব?"

whileInView
↓
"আমাকে দেখলে কী হবে?"

whileHover
↓
"Mouse রাখলে কী হবে?"

whileTap
↓
"Click করলে কী হবে?"

transition
↓
"এই পরিবর্তনটা কীভাবে হবে?"
```

আর একটা গুরুত্বপূর্ণ বিষয়: **সবগুলো একসাথে ব্যবহার করতে হবে এমন নয়।** তোমার UI-এর interaction অনুযায়ী ১–৩টা বেছে নেবে।


----
হ্যাঁ। Motion-এ একটা `div`-কে automatically **উপরে-নিচে ভাসমান** রাখতে `animate` + `transition` ব্যবহার করবে।

```jsx
import { motion } from "motion/react";

const App = () => {
  return (
    <motion.div
      animate={{ y: [0, -20, 0] }}
      transition={{
        duration: 2,
        repeat: Infinity,
        ease: "easeInOut",
      }}
      className="w-40 h-40 bg-blue-500"
    >
      Floating
    </motion.div>
  );
};

export default App;
```

### এখানে কী হচ্ছে?

```jsx
animate={{ y: [0, -20, 0] }}
```

মানে:

```text
নিচের অবস্থান
    ↓
  0px
    ↑
 -20px
    ↓
  0px
```

অর্থাৎ `div` → **উপরে যাবে → আবার নিচে আসবে → আবার উপরে যাবে**।

### `repeat: Infinity`

```jsx
repeat: Infinity
```

মানে animation **শেষ হবে না**, বারবার চলবে।

### আরও smooth করতে

```jsx
transition={{
  duration: 2,
  repeat: Infinity,
  ease: "easeInOut",
}}
```

`duration: 2` → এক cycle-এর সময় ২ সেকেন্ড।

---

### ⭐ Real project-এ যেমন ব্যবহার করতে পারো

```jsx
<motion.div
  animate={{ y: [0, -15, 0] }}
  transition={{
    duration: 3,
    repeat: Infinity,
    ease: "easeInOut",
  }}
  className="absolute top-20 right-20 w-32 h-32 rounded-full bg-purple-500"
>
</motion.div>
```

**মনে রাখার shortcut:**

> `y: [0, -20, 0]` = Up → Down
> `repeat: Infinity` = বারবার
> `duration` = কত দ্রুত
> `ease` = কত smooth


----
হ্যাঁ, একইভাবে **left ↔ right** করতে চাইলে `x` ব্যবহার করবে। `y` হলো up/down, আর `x` হলো left/right।

```jsx
<motion.div
  animate={{ x: [0, 30, 0] }}
  transition={{
    duration: 2,
    repeat: Infinity,
    ease: "easeInOut",
  }}
  className="w-40 h-40 bg-blue-500"
>
  Floating
</motion.div>
```

### বুঝো সহজভাবে

```jsx
x: [0, 30, 0]
```

মানে:

```text
Original
   ↓
  0px
   →
 +30px
   ←
  0px
```

অর্থাৎ **ডানে যাবে → আবার আগের জায়গায় আসবে → আবার ডানে যাবে**।

### ↔️ দুই দিকেই চাইলে

```jsx
<motion.div
  animate={{ x: [-30, 30, -30] }}
  transition={{
    duration: 3,
    repeat: Infinity,
    ease: "easeInOut",
  }}
>
  Floating
</motion.div>
```

এটা হবে:

```text
← Left     Center     Right →
 -30px       0px       +30px
```

**Shortcut মনে রাখো:**

* `x` → ↔️ Left / Right
* `y` → ↕️ Up / Down
* `repeat: Infinity` → 🔄 বারবার চলবে


---
হ্যাঁ। Motion শেখার সময় সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো **কোন property কোথায় দিতে হয় এবং property-এর value কীভাবে লিখতে হয়**। এটা বুঝে গেলে animation অনেক সহজ হয়ে যাবে।

## 1. `animate` এর ভিতরে কী দেওয়া যায়?

`animate`-এর ভিতরে তুমি **কোন অবস্থায় element যাবে** সেটা দাও।

```jsx
<motion.div
  animate={{
    x: 100,
    y: 50,
    opacity: 0.5,
    scale: 1.2,
    rotate: 45,
  }}
/>
```

এখানে:

| Property          | কাজ                       |
| ----------------- | ------------------------- |
| `x`               | left/right                |
| `y`               | up/down                   |
| `opacity`         | transparent/visible       |
| `scale`           | বড়/ছোট                    |
| `rotate`          | ঘোরানো                    |
| `width`           | width পরিবর্তন            |
| `height`          | height পরিবর্তন           |
| `borderRadius`    | corner পরিবর্তন           |
| `backgroundColor` | background color পরিবর্তন |

---

## 2. `x` কীভাবে দিতে হয়?

```jsx
animate={{ x: 100 }}
```

মানে ডানদিকে `100px`।

```jsx
animate={{ x: -100 }}
```

মানে বামদিকে `100px`।

### Automatic left-right

```jsx
animate={{
  x: [-30, 30, -30]
}}
```

মানে:

```text
← 30px     30px →
    \       /
     \     /
      Center
```

---

## 3. `y`

```jsx
animate={{ y: -50 }}
```

উপরে যাবে।

```jsx
animate={{ y: 50 }}
```

নিচে যাবে।

### Floating effect

```jsx
animate={{
  y: [0, -20, 0]
}}
```

---

## 4. `scale`

Element বড়/ছোট করতে:

```jsx
animate={{
  scale: 1.2
}}
```

মানে 20% বড় হবে।

```jsx
animate={{
  scale: 0.8
}}
```

মানে ছোট হবে।

Automatic:

```jsx
animate={{
  scale: [1, 1.2, 1]
}}
```

---

## 5. `rotate`

```jsx
animate={{
  rotate: 360
}}
```

একবার পুরো ঘুরবে।

বারবার:

```jsx
animate={{
  rotate: [0, 360]
}}
transition={{
  duration: 2,
  repeat: Infinity
}}
```

---

## 6. `opacity`

```jsx
animate={{
  opacity: 1
}}
```

পুরো visible।

```jsx
animate={{
  opacity: 0
}}
```

পুরো invisible।

Fade effect:

```jsx
initial={{ opacity: 0 }}
animate={{ opacity: 1 }}
```

---

# 7. সবচেয়ে গুরুত্বপূর্ণ: Array `[]`

তুমি যখন **একাধিক অবস্থার মধ্যে animation করাতে চাও**, তখন array ব্যবহার করতে পারো।

```jsx
animate={{
  x: [0, 100, 0]
}}
```

মানে:

```text
0 → 100 → 0
```

একইভাবে:

```jsx
animate={{
  y: [0, -20, 0]
}}
```

```jsx
animate={{
  scale: [1, 1.2, 1]
}}
```

```jsx
animate={{
  opacity: [1, 0.5, 1]
}}
```

---

# 8. একসাথে অনেক property

তুমি চাইলে একসাথে দিতে পারো:

```jsx
<motion.div
  animate={{
    x: [0, 30, 0],
    y: [0, -20, 0],
    scale: [1, 1.1, 1],
    rotate: [0, 5, 0],
    opacity: [1, 0.8, 1],
  }}
  transition={{
    duration: 3,
    repeat: Infinity,
    ease: "easeInOut",
  }}
>
  Hello
</motion.div>
```

এখন element একই সাথে:

**↔️ left-right + ↕️ up-down + 🔍 scale + 🔄 rotate + opacity**

করবে।

---

# 9. `transition`-এর ভিতরে কী দেওয়া যায়?

`transition` বলে **animation কীভাবে চলবে**।

```jsx
transition={{
  duration: 2,
  delay: 1,
  repeat: Infinity,
  ease: "easeInOut",
}}
```

Common properties:

| Property    | কাজ                      |
| ----------- | ------------------------ |
| `duration`  | কত সময় ধরে animation হবে |
| `delay`     | কতক্ষণ পরে শুরু হবে      |
| `repeat`    | কতবার চলবে               |
| `ease`      | movement-এর smoothness   |
| `type`      | spring/tween ইত্যাদি     |
| `stiffness` | spring-এর শক্তি          |
| `damping`   | spring-এর damping        |

---

# 10. `initial`, `animate`, `whileHover`—এগুলোর মধ্যে কী দেবে?

এটাই খুব important।

### `initial`

**শুরুতে কেমন থাকবে?**

```jsx
initial={{
  opacity: 0,
  y: 50,
  scale: 0.8,
}}
```

### `animate`

**সাধারণভাবে কোন অবস্থায় যাবে?**

```jsx
animate={{
  opacity: 1,
  y: 0,
  scale: 1,
}}
```

### `whileHover`

**Mouse রাখলে কী হবে?**

```jsx
whileHover={{
  scale: 1.1,
  y: -5,
}}
```

### `whileTap`

**Click/press করলে কী হবে?**

```jsx
whileTap={{
  scale: 0.95,
}}
```

---

## একটা complete example

```jsx
<motion.div
  initial={{
    opacity: 0,
    y: 30,
  }}
  animate={{
    opacity: 1,
    y: 0,
  }}
  whileHover={{
    scale: 1.05,
    y: -5,
  }}
  whileTap={{
    scale: 0.95,
  }}
  transition={{
    duration: 0.5,
    ease: "easeInOut",
  }}
  className="w-60 h-40 bg-blue-500 rounded-xl"
>
  Hello
</motion.div>
```

এখানে পুরো flow:

```text
initial
   ↓
শুরুতে নিচে + invisible
   ↓
animate
   ↓
normal position + visible
   ↓
whileHover
   ↓
mouse রাখলে একটু বড় + উপরে
   ↓
whileTap
   ↓
click করলে একটু ছোট
```

### একটা খুব সহজ rule মনে রাখো

```text
initial       → শুরুতে কী হবে?
animate       → সাধারণ animation কী হবে?
whileHover    → hover করলে কী হবে?
whileTap      → click করলে কী হবে?
whileInView   → screen-এ এলে কী হবে?
transition    → animation কীভাবে হবে?
```

আর `x, y, scale, rotate, opacity` হলো **কী জিনিস পরিবর্তন করবে**।

---
# screen scale animation add 


হ্যাঁ, তুমি যেটা চাচ্ছো সেটা হলো **scroll animation**:

* 1st `div` → **left side থেকে আসবে**
* 2nd `div` → **right side থেকে আসবে**
* 3rd → আবার left
* 4th → right
* এভাবে চলবে
* User scroll করলে প্রতিটি `div` screen-এর কাছে এলে animation হবে।

Motion-এ এখানে মূলত `initial` + `whileInView` ব্যবহার করবে।

```jsx
import { motion } from "motion/react";

const App = () => {
  return (
    <div className="overflow-hidden">

      {/* 1 */}
      <motion.div
        initial={{ x: -200, opacity: 0 }}
        whileInView={{ x: 0, opacity: 1 }}
        transition={{ duration: 0.8 }}
        viewport={{ once: true }}
        className="my-10 p-10 border"
      >
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Est,
        accusantium! Voluptate exercitationem atque voluptatibus iusto a,
        qui laboriosam?
      </motion.div>


      {/* 2 */}
      <motion.div
        initial={{ x: 200, opacity: 0 }}
        whileInView={{ x: 0, opacity: 1 }}
        transition={{ duration: 0.8 }}
        viewport={{ once: true }}
        className="my-10 p-10 border"
      >
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Porro
        dignissimos, repellendus recusandae culpa delectus aspernatur
        accusamus perspiciatis quibusdam.
      </motion.div>


      {/* 3 */}
      <motion.div
        initial={{ x: -200, opacity: 0 }}
        whileInView={{ x: 0, opacity: 1 }}
        transition={{ duration: 0.8 }}
        viewport={{ once: true }}
        className="my-10 p-10 border"
      >
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio
        pariatur dolores recusandae minus dolorem repellat.
      </motion.div>


      {/* 4 */}
      <motion.div
        initial={{ x: 200, opacity: 0 }}
        whileInView={{ x: 0, opacity: 1 }}
        transition={{ duration: 0.8 }}
        viewport={{ once: true }}
        className="my-10 p-10 border"
      >
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Cupiditate
        nulla unde perferendis cumque autem in provident delectus.
      </motion.div>

    </div>
  );
};

export default App;
```

### মূল ব্যাপারটা এখানে

**Left থেকে:**

```jsx
initial={{ x: -200, opacity: 0 }}
whileInView={{ x: 0, opacity: 1 }}
```

মানে:

```text
Screen-এর বাইরে
      ←
   -200px
      |
      ↓
     0px
   [ DIV ]
```

**Right থেকে:**

```jsx
initial={{ x: 200, opacity: 0 }}
whileInView={{ x: 0, opacity: 1 }}
```

মানে:

```text
           বাইরে
             →
          +200px
             |
             ↓
          0px
        [ DIV ]
```

### `viewport={{ once: true }}` কেন?

```jsx
viewport={{ once: true }}
```

এর মানে হলো **একবার screen-এ আসার পর animation একবারই হবে।**

যদি এটা না দাও, scroll করে বাইরে → আবার ভিতরে আনলে animation আবার হতে পারে।

---

## তোমার ১০টা `div` হলে

তোমাকে প্রতিটাতে আলাদা করে code লিখতে হবে না। `map()` দিয়ে করতে পারো।

```jsx
const texts = [
  "Lorem ipsum dolor sit amet...",
  "Porro dignissimos repellendus...",
  "Odio pariatur dolores...",
  "Cupiditate nulla unde...",
  "Veniam a laborum architecto...",
  "Quae nam laudantium...",
  "Vero consequatur excepturi...",
  "Molestiae neque est dolor...",
  "Autem delectus saepe...",
  "Rerum rem nisi quod...",
];
```

তারপর:

```jsx
<div className="overflow-hidden">

  {texts.map((text, index) => (
    <motion.div
      key={index}
      initial={{
        x: index % 2 === 0 ? -200 : 200,
        opacity: 0,
      }}
      whileInView={{
        x: 0,
        opacity: 1,
      }}
      transition={{
        duration: 0.8,
        ease: "easeOut",
      }}
      viewport={{
        once: true,
        amount: 0.2,
      }}
      className="my-10 p-10 border"
    >
      {text}
    </motion.div>
  ))}

</div>
```

এখানে এই লাইনটাই সবচেয়ে interesting:

```jsx
x: index % 2 === 0 ? -200 : 200
```

মানে:

```text
index 0 → -200 → Left
index 1 → +200 → Right
index 2 → -200 → Left
index 3 → +200 → Right
index 4 → -200 → Left
...
```

আর `amount: 0.2` মানে element-এর প্রায় **20% viewport-এ ঢোকার পর animation trigger** হবে।

**তোমার এই use-case-এর জন্য মূল combination মনে রাখো:**

```jsx
initial       → কোথা থেকে আসবে
whileInView   → screen-এ এলে কোথায় যাবে
viewport      → কখন trigger হবে
transition    → কত দ্রুত/smooth হবে
```

এটা আসলে Motion-এর খুব common **scroll reveal animation** pattern।

---
হ্যাঁ—**তুমি যদি Motion-এর ৫–৬টা core property ভালোভাবে শিখে ফেলো, তাহলে React project-এর বেশিরভাগ সাধারণ animation করতে পারবে।** সব property মুখস্থ করার দরকার নেই।

### আগে এইগুলো ভালোভাবে শেখো

| Property      | কখন ব্যবহার করবে                      |
| ------------- | ------------------------------------- |
| `initial`     | animation শুরু হওয়ার অবস্থার জন্য     |
| `animate`     | automatic/general animation           |
| `whileInView` | scroll করে element screen-এ এলে       |
| `whileHover`  | mouse hover করলে                      |
| `whileTap`    | click/press করলে                      |
| `transition`  | animation-এর speed, delay, smoothness |

এর সাথে **`exit` + `AnimatePresence`** পরে শিখবে, কারণ modal/menu/page exit animation-এ এগুলো খুব কাজে লাগে।

### এই ৭টা দিয়ে তুমি করতে পারবে

```text
Hero animation          → initial + animate
Scroll reveal           → initial + whileInView
Card hover              → whileHover
Button click            → whileTap
Floating animation      → animate + transition
Modal open/close        → AnimatePresence + exit
Staggered list          → variants + staggerChildren
```

তোমার এখন যেহেতু `x`, `y`, `opacity`, `scale` নিয়েও কাজ করছো, এগুলোও core হিসেবে ধরো।

**Learning priority:**

```text
Phase 1
initial
animate
transition
x / y / opacity / scale

Phase 2
whileHover
whileTap
whileInView
viewport

Phase 3
variants
staggerChildren
AnimatePresence
exit

Phase 4
layout
layoutId
useScroll
useTransform
```

**Phase 1 + 2 ভালোভাবে পারলে তুমি বাস্তব React website-এর অনেক animation নিজেই বানাতে পারবে।** Advanced property পরে প্রয়োজন অনুযায়ী শেখাই বেশি ভালো—সব docs একসাথে মুখস্থ করার দরকার নেই।


-----

একদম সহজভাবে বললে:

```jsx
initial={{ x: 200, opacity: 0 }}
whileInView={{ x: 0, opacity: 1 }}
```

এখানে **`initial` = আগে কী হবে**, আর **`whileInView` = screen-এ আসার পর কী হবে**।

### Step-by-step

ধরো তোমার `div` ডান দিক থেকে আসবে।

#### 1️⃣ শুরুতে — `initial`

```jsx
initial={{ x: 200, opacity: 0 }}
```

মানে:

* `x: 200` → ডানদিকে 200px সরানো
* `opacity: 0` → সম্পূর্ণ invisible

অর্থাৎ শুরুতে:

```text
              [ DIV ]
                 ← 200px
              invisible
```

---

#### 2️⃣ Screen-এ আসলে — `whileInView`

```jsx
whileInView={{ x: 0, opacity: 1 }}
```

Motion তখন animation করে:

```text
x: 200  ─────────→  x: 0
opacity: 0 ───────→ opacity: 1
```

অর্থাৎ:

```text
আগে                         পরে

[ বাইরে ]       ─────→       [ DIV ]
invisible                    visible
x = 200                      x = 0
```

### তাহলে `animate` কোথায়?

এই particular case-এ **`animate` দরকার নেই**।

কারণ তুমি বলছো:

> "যখন আমার div screen-এ আসবে, তখন animation হবে।"

তাই:

```jsx
initial
   ↓
শুরু অবস্থান
   ↓
whileInView
   ↓
screen-এ আসার পরের অবস্থান
```

### `animate` দিলে কী হতো?

যদি তুমি লিখতে:

```jsx
initial={{ x: 200, opacity: 0 }}
animate={{ x: 0, opacity: 1 }}
```

তাহলে element **page render হওয়ার পরই** `x: 200 → x: 0` animation করবে।

কিন্তু:

```jsx
initial={{ x: 200, opacity: 0 }}
whileInView={{ x: 0, opacity: 1 }}
```

মানে **scroll করে element viewport-এ এলে** animation করবে।

**Shortcut:**

```text
initial     = আগে
animate     = সাধারণভাবে পরে
whileInView = screen-এ এলে পরে
```

তাই তোমার scroll animation-এর ক্ষেত্রে `initial → whileInView` একদম ঠিক।

---
`transition={{ duration: 10 }}` দিয়ে তুমি **animation কত সময় ধরে চলবে** সেটা নির্ধারণ করো।

```jsx
transition={{ duration: 10 }}
```

মানে animation শেষ হতে **10 seconds** লাগবে।

### তোমার example দিয়ে দেখি

```jsx
<motion.div
  initial={{ x: 200, opacity: 0 }}
  whileInView={{ x: 0, opacity: 1 }}
  transition={{ duration: 10 }}
>
  Hello
</motion.div>
```

এখানে:

```text
x: 200  ───────────────────→  x: 0
        ←── 10 seconds ───→
```

অর্থাৎ `div` **ধীরে ধীরে 10 seconds ধরে** right থেকে নিজের জায়গায় আসবে এবং একই সাথে opacity `0 → 1` হবে।

### Duration পরিবর্তন করলে

```jsx
duration: 0.3
```

খুব দ্রুত ⚡

```jsx
duration: 1
```

স্বাভাবিক গতির animation।

```jsx
duration: 2
```

আরও ধীরে।

```jsx
duration: 10
```

অনেক ধীরে 🐢

### গুরুত্বপূর্ণ

`duration` **distance নির্ধারণ করে না**।

```jsx
initial={{ x: 200 }}
```

এটা বলে **কত দূর থেকে আসবে**।

```jsx
transition={{ duration: 2 }}
```

এটা বলে **কত সময়ে সেই distance পার করবে**।

তাই:

```jsx
initial={{ x: 500 }}
transition={{ duration: 2 }}
```

= 500px দূর থেকে **2 seconds-এ** আসবে।

```jsx
initial={{ x: 100 }}
transition={{ duration: 5 }}
```

= 100px দূর থেকে **5 seconds-এ** আসবে।

**Shortcut:**

> `x/y/scale` → **কী পরিবর্তন হবে**
> `initial/animate/whileInView` → **কখন/কোন state হবে**
> `duration` → **কত সময় লাগবে**


----
