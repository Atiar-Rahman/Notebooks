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
