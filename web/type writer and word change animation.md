
Tailwind CSS-এ **word animation** করার কয়েকটি উপায় আছে। Tailwind নিজে শুধু কিছু built-in animation দেয় (`animate-bounce`, `animate-pulse`, `animate-spin`, `animate-ping`)। **Typing effect**, **word change**, **text reveal** ইত্যাদির জন্য সাধারণত CSS, React state, অথবা animation library ব্যবহার করা হয়।

## 1. Bounce Animation

```jsx
<h1 className="text-4xl font-bold animate-bounce">
  Hello World
</h1>
```

---

## 2. Pulse Animation

```jsx
<h1 className="text-4xl font-bold animate-pulse">
  Welcome
</h1>
```

---

## 3. Fade In Animation (Tailwind + Custom CSS)

```jsx
<h1 className="animate-fade text-4xl font-bold">
  Hello
</h1>
```

```css
@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animate-fade {
  animation: fade 2s ease-in-out;
}
```

---

## 4. Typing Animation

```jsx
<h1 className="typing text-4xl font-bold">
  Welcome to My Website
</h1>
```

```css
.typing {
  width: 0;
  overflow: hidden;
  white-space: nowrap;
  border-right: 3px solid black;
  animation: typing 4s steps(22) infinite,
             blink .7s infinite;
}

@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}

@keyframes blink {
  50% {
    border-color: transparent;
  }
}
```

---

## 5. Word Change Animation (React)

```jsx
import { useEffect, useState } from "react";

const words = ["Developer", "Designer", "Freelancer"];

export default function App() {
  const [index, setIndex] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setIndex((prev) => (prev + 1) % words.length);
    }, 2000);

    return () => clearInterval(timer);
  }, []);

  return (
    <h1 className="text-4xl font-bold">
      I am a{" "}
      <span className="text-blue-600 transition-all duration-500">
        {words[index]}
      </span>
    </h1>
  );
}
```

Output:

```text
I am a Developer
↓
I am a Designer
↓
I am a Freelancer
```

---

## 6. Hover Animation

```jsx
<h1 className="text-4xl font-bold transition duration-300 hover:scale-110 hover:text-blue-500">
  Hover Me
</h1>
```

---

## Interview Tip

যদি React + Tailwind দিয়ে **typing animation**, **changing words**, বা **hero section text animation** করতে চান, তাহলে অনেক developer **Framer Motion** ব্যবহার করেন। এটি smooth এবং powerful animation দেয়।

উদাহরণ:

```jsx
import { motion } from "framer-motion";

<motion.h1
  initial={{ opacity: 0, y: -20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 1 }}
>
  Welcome
</motion.h1>
```

### কোন animation কখন ব্যবহার করবেন?

- **`animate-bounce`** → Button, icon বা call-to-action highlight করতে।
    
- **`animate-pulse`** → Loading বা attention আকর্ষণ করতে।
    
- **Typing animation** → Hero section-এর headline।
    
- **Word changing animation** → Portfolio বা landing page-এ role দেখাতে (যেমন: _Developer → Designer → Freelancer_)।
    
- **Framer Motion** → Professional React project-এ complex text animation-এর জন্য।

---------
আপনি যে animation-এর কথা বলছেন সেটাকে সাধারণত **Typing Animation** বা **Typewriter Effect** বলা হয়।

এতে:

1. Sentence-এর অক্ষর **একটা একটা করে আসে**।
    
2. পুরো sentence লেখা হলে কিছুক্ষণ থাকে।
    
3. তারপর **একটা একটা করে delete হয়**।
    
4. এরপর নতুন sentence আবার **একটা একটা করে আসে**।
    

### React Example

```jsx
import { useEffect, useState } from "react";

const words = [
  "Web Developer",
  "React Developer",
  "MERN Stack Developer",
];

export default function App() {
  const [text, setText] = useState("");
  const [wordIndex, setWordIndex] = useState(0);
  const [isDeleting, setIsDeleting] = useState(false);

  useEffect(() => {
    const currentWord = words[wordIndex];

    const timer = setTimeout(() => {
      if (!isDeleting) {
        setText(currentWord.substring(0, text.length + 1));

        if (text === currentWord) {
          setTimeout(() => setIsDeleting(true), 1000);
        }
      } else {
        setText(currentWord.substring(0, text.length - 1));

        if (text === "") {
          setIsDeleting(false);
          setWordIndex((prev) => (prev + 1) % words.length);
        }
      }
    }, isDeleting ? 80 : 120);

    return () => clearTimeout(timer);
  }, [text, isDeleting, wordIndex]);

  return (
    <h1 className="text-5xl font-bold">
      I am a{" "}
      <span className="text-blue-600 border-r-2 border-blue-600 pr-1">
        {text}
      </span>
    </h1>
  );
}
```

### Output

```text
I am a Web Developer
↓
I am a Web Develope
↓
I am a Web Develop
↓
...
I am a
↓
I am a React Developer
↓
I am a MERN Stack Developer
↓
(repeat)
```

---

## সহজ উপায় (লাইব্রেরি ব্যবহার করে)

অনেক React developer এই effect-এর জন্য **react-type-animation** বা **react-typed** ব্যবহার করেন।

উদাহরণ:

```jsx
import { TypeAnimation } from "react-type-animation";

<TypeAnimation
  sequence={[
    "Web Developer",
    1500,
    "React Developer",
    1500,
    "MERN Stack Developer",
    1500,
  ]}
  speed={50}
  repeat={Infinity}
/>
```

### কোনটা ব্যবহার করবেন?

- **ইন্টারভিউ বা শেখার জন্য** → নিজে `useState` + `useEffect` দিয়ে বানানো ভালো।
    
- **বাস্তব React project-এর জন্য** → `react-type-animation` বা `react-typed` ব্যবহার করলে কম কোডে সুন্দর animation পাওয়া যায়।

React/Next.js-এর জন্য অনেক ভালো animation library আছে। UI দ্রুত এবং professional দেখানোর জন্য নিচেরগুলো সবচেয়ে জনপ্রিয়।

## 1. Framer Motion (বর্তমানে Motion) ⭐⭐⭐⭐⭐ (সেরা)

**সবচেয়ে জনপ্রিয় React animation library।**

এতে পাবেন:

* Page Transition
* Fade In / Fade Out
* Slide Animation
* Scale
* Hover Effect
* Scroll Animation
* Drag & Drop
* Shared Layout Animation

```jsx
<motion.div
  initial={{ opacity: 0, y: 50 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.5 }}
>
  Hello
</motion.div>
```

**ব্যবহার করুন যখন:**

* Portfolio
* Dashboard
* Landing Page
* SaaS Website

---

## 2. GSAP ⭐⭐⭐⭐⭐

সবচেয়ে powerful animation library।

এতে করতে পারবেন:

* SVG Animation
* Complex Timeline
* Text Animation
* Scroll Animation
* Loader Animation

```jsx
gsap.to(".box", {
  x: 300,
  duration: 2,
});
```

**ব্যবহার করুন যখন:**

* Creative Website
* Agency Website
* Premium UI

---

## 3. AOS (Animate On Scroll) ⭐⭐⭐⭐☆

Scroll করলে animation হবে।

```html
<div data-aos="fade-up">
```

Animation:

* Fade
* Zoom
* Flip
* Slide

**এক লাইনে animation দিতে পারবেন।**

---

## 4. React Awesome Reveal ⭐⭐⭐⭐☆

React-এর জন্য সহজ scroll animation।

```jsx
<Fade>
  <h1>Hello</h1>
</Fade>
```

---

## 5. React Typed / Type Animation ⭐⭐⭐⭐☆

Typing Effect

```
Developer |
Designer |
Freelancer |
```

একটা একটা করে লেখা আসবে।

---

## 6. React CountUp ⭐⭐⭐⭐☆

Number Counter

```
0
100
500
1000
```

Portfolio-তে ব্যবহার হয়।

---

## 7. React Fast Marquee ⭐⭐⭐⭐☆

Logo Slider

```
Google Microsoft Amazon Meta
```

Automatically চলবে।

---

## 8. Lottie React ⭐⭐⭐⭐⭐

JSON animation play করতে পারবেন।

Loading animation

Robot

Success animation

Error animation

---

## 9. Swiper.js ⭐⭐⭐⭐⭐

Carousel

Slider

Testimonial

Hero Slider

Mobile Friendly

---

## 10. Lenis ⭐⭐⭐⭐⭐

Smooth Scroll

Apple website-এর মতো smooth scrolling।

---

## 11. React Bits ⭐⭐⭐⭐⭐

অনেক ready-made animation components।

যেমন:

* Text Reveal
* Magnetic Button
* Glowing Card
* Cursor Effect
* Background Animation

---

## 12. Magic UI ⭐⭐⭐⭐⭐

Ready-made animated UI components।

* Dock
* Bento Grid
* Animated Border
* Gradient Text
* Hero Section
* Beam Effect

---

## 13. Aceternity UI ⭐⭐⭐⭐⭐

Beautiful premium-looking components।

* Lamp Effect
* Spotlight
* Background Beams
* Hero Parallax
* Infinite Moving Cards

---

## 14. Shadcn/ui + Motion ⭐⭐⭐⭐⭐

Professional SaaS UI

Animation + Components

---

## 15. Three.js + React Three Fiber ⭐⭐⭐⭐⭐

3D Website

3D Model

Particles

Galaxy

Earth

---

# আমার সাজেশন (React/Next.js-এর জন্য)

| Purpose                 | Library                      |
| ----------------------- | ---------------------------- |
| General UI Animation    | **Motion (Framer Motion)** ⭐ |
| Scroll Animation        | **AOS** বা **Motion**        |
| Typing Text             | **react-type-animation**     |
| Counter                 | **react-countup**            |
| Slider                  | **Swiper.js**                |
| Lottie Animation        | **lottie-react**             |
| Smooth Scroll           | **Lenis**                    |
| Premium UI Components   | **Magic UI**                 |
| Beautiful Hero Sections | **Aceternity UI**            |
| Complex Animation       | **GSAP**                     |

### যদি আপনি ২০২৬ সালে Modern React/Next.js UI বানাতে চান, তাহলে এই combination খুবই শক্তিশালী:

* **Tailwind CSS** → Styling
* **Motion (Framer Motion)** → Animation
* **Shadcn/ui** → UI Components
* **Magic UI** → Animated Components
* **Aceternity UI** → Hero Sections & Visual Effects
* **Swiper.js** → Sliders
* **Lottie React** → Loading & Icon Animations
* **Lenis** → Smooth Scrolling

এই stack দিয়ে খুব কম কোডে modern, interactive, এবং professional-looking UI তৈরি করা যায়।
