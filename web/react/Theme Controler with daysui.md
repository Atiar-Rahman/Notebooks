অবশ্যই। তুমি যদি React + DaisyUI ব্যবহার করো, তাহলে useState দিয়ে খুব সহজেই Light/Dark theme controller বানাতে পারো।

1. useState দিয়ে theme state রাখো
import { useState } from "react";

function App() {
  const [theme, setTheme] = useState("light");

  return (
    <div data-theme={theme} className="min-h-screen">
      <div className="navbar bg-base-200">
        <div className="flex-1">
          <a className="btn btn-ghost text-xl">My App</a>
        </div>

        <div>
          <button
            className="btn btn-primary"
            onClick={() =>
              setTheme(theme === "light" ? "dark" : "light")
            }
          >
            {theme === "light" ? "🌙 Dark" : "☀️ Light"}
          </button>
        </div>
      </div>

      <div className="p-10">
        <h1 className="text-3xl font-bold">
          Hello DaisyUI!
        </h1>

        <p className="mt-4">
          Current theme: {theme}
        </p>
      </div>
    </div>
  );
}

export default App;

2. এখানে মূল ব্যাপারটা কী?

এই লাইনটি theme-এর বর্তমান value রাখছে:

const [theme, setTheme] = useState("light");


শুরুতে:

theme = "light"


Button click করলে:

setTheme(theme === "light" ? "dark" : "light")


মানে:

light → dark
dark  → light


তারপর DaisyUI-কে theme জানানোর জন্য:

<div data-theme={theme}>


ব্যবহার করছি।

অর্থাৎ theme যদি dark হয়, DOM হবে:

<div data-theme="dark">


আর light হলে:

<div data-theme="light">


DaisyUI-এর bg-base-200, text-base-content, btn-primary ইত্যাদি semantic class তখন theme অনুযায়ী color পরিবর্তন করবে।

আরেকটা গুরুত্বপূর্ণ বিষয়

যদি তুমি DaisyUI-এর নির্দিষ্ট theme, যেমন cupcake, synthwave, forest, dracula ইত্যাদি ব্যবহার করতে চাও, একই পদ্ধতিতে করতে পারো:

const [theme, setTheme] = useState("cupcake");

return (
  <div data-theme={theme}>
    <button onClick={() => setTheme("cupcake")}>
      Cupcake
    </button>

    <button onClick={() => setTheme("synthwave")}>
      Synthwave
    </button>

    <button onClick={() => setTheme("dracula")}>
      Dracula
    </button>
  </div>
);


তবে পুরো app-এর theme controller বানাতে চাইলে data-theme-টা সাধারণত root-level element-এ রাখা ভালো। চাইলে আমি তোমাকে React + Tailwind + DaisyUI দিয়ে navbar-এর মধ্যে সুন্দর Light/Dark toggle সহ পুরো working example দেখাতে পারি।

---
হ্যাঁ, একদম একটা component-এর মধ্যেই ১০+ DaisyUI theme রাখতে পারো। useState-এ শুধু theme-এর নাম রাখবে, আর data-theme={theme} দিয়ে component-এ apply করবে।

ThemeController.jsx
import { useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "dracula",
];

const ThemeController = () => {
  const [theme, setTheme] = useState("light");

  return (
    <div data-theme={theme} className="min-h-screen bg-base-100 text-base-content">
      
      {/* Theme Selector */}
      <div className="flex flex-wrap gap-2 p-5">
        {themes.map((item) => (
          <button
            key={item}
            onClick={() => setTheme(item)}
            className={`btn ${
              theme === item ? "btn-primary" : "btn-outline"
            }`}
          >
            {item}
          </button>
        ))}
      </div>

      {/* Demo Content */}
      <div className="p-5">
        <div className="card bg-base-200 shadow-xl">
          <div className="card-body">
            <h2 className="card-title">
              Current Theme: {theme}
            </h2>

            <p>
              This content changes according to the selected DaisyUI theme.
            </p>

            <div className="card-actions">
              <button className="btn btn-primary">
                Primary
              </button>

              <button className="btn btn-secondary">
                Secondary
              </button>
            </div>
          </div>
        </div>
      </div>

    </div>
  );
};

export default ThemeController;

DaisyUI config

তোমার DaisyUI version অনুযায়ী themes enable করতে হবে। যদি DaisyUI 5 + Tailwind CSS 4 ব্যবহার করো, CSS-এ themes declare করতে পারো:

@import "tailwindcss";

@plugin "daisyui" {
  themes: light, dark, cupcake, bumblebee, emerald, corporate,
    synthwave, retro, cyberpunk, valentine, aqua, dracula;
}


তারপর:

<ThemeController />


ব্যস। 🎨

মূল concept: themes array-তে যত theme রাখবে, map() ততগুলো button তৈরি করবে এবং setTheme(item) দিয়ে data-theme পরিবর্তন করবে।

চাইলে এটাকে আরও সুন্দর করে dropdown/select + theme preview + localStorage, যাতে page refresh করলেও selected theme থাকে—এভাবেও করা যায়।

---
হ্যাঁ। একটা component-এর মধ্যেই Dropdown + Theme Preview + localStorage করা যায়। নিচেরটা সরাসরি ব্যবহার করতে পারো।

Writing
ThemeController.jsx
import { useEffect, useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "dracula",
];

const ThemeController = () => {
  // localStorage থেকে theme নেওয়া
  const [theme, setTheme] = useState(
    () => localStorage.getItem("theme") || "light"
  );

  // Theme change হলে localStorage + DOM update
  useEffect(() => {
    localStorage.setItem("theme", theme);
    document.documentElement.setAttribute("data-theme", theme);
  }, [theme]);

  return (
    <div className="min-h-screen bg-base-100 text-base-content p-6">
      
      {/* Theme Dropdown */}
      <div className="flex justify-center mb-8">
        <select
          value={theme}
          onChange={(e) => setTheme(e.target.value)}
          className="select select-bordered w-full max-w-xs"
        >
          {themes.map((item) => (
            <option key={item} value={item}>
              {item}
            </option>
          ))}
        </select>
      </div>

      {/* Theme Preview */}
      <div className="max-w-xl mx-auto">
        <div className="card bg-base-200 shadow-xl">
          <div className="card-body">
            <h2 className="card-title">
              Theme Preview
            </h2>

            <p>
              Current theme:{" "}
              <span className="font-bold">{theme}</span>
            </p>

            <div className="flex flex-wrap gap-2 mt-4">
              <button className="btn btn-primary">
                Primary
              </button>

              <button className="btn btn-secondary">
                Secondary
              </button>

              <button className="btn btn-accent">
                Accent
              </button>

              <button className="btn btn-outline">
                Outline
              </button>
            </div>

            {/* Color Preview */}
            <div className="grid grid-cols-3 gap-3 mt-5">
              <div className="bg-primary text-primary-content p-4 rounded-lg">
                Primary
              </div>

              <div className="bg-secondary text-secondary-content p-4 rounded-lg">
                Secondary
              </div>

              <div className="bg-accent text-accent-content p-4 rounded-lg">
                Accent
              </div>
            </div>
          </div>
        </div>
      </div>

      {/* All Theme Preview */}
      <div className="mt-10">
        <h2 className="text-2xl font-bold mb-4">
          Available Themes
        </h2>

        <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
          {themes.map((item) => (
            <button
              key={item}
              onClick={() => setTheme(item)}
              data-theme={item}
              className={`p-4 rounded-xl border-2 text-left bg-base-100 ${
                theme === item
                  ? "border-primary"
                  : "border-base-300"
              }`}
            >
              <div className="font-bold mb-2">
                {item}
              </div>

              <div className="flex gap-1">
                <div className="w-6 h-6 rounded bg-primary" />
                <div className="w-6 h-6 rounded bg-secondary" />
                <div className="w-6 h-6 rounded bg-accent" />
                <div className="w-6 h-6 rounded bg-neutral" />
              </div>
            </button>
          ))}
        </div>
      </div>

    </div>
  );
};

export default ThemeController;

DaisyUI config

DaisyUI 5 + Tailwind CSS 4 হলে CSS-এ themes enable করো:

@import "tailwindcss";

@plugin "daisyui" {
  themes: light, dark, cupcake, bumblebee, emerald, corporate,
    synthwave, retro, cyberpunk, valentine, aqua, dracula;
}

কীভাবে কাজ করছে
useState() → বর্তমানে কোন theme selected সেটা রাখছে।
select → dropdown থেকে theme select করা যাচ্ছে।
useEffect() → theme পরিবর্তন হলে localStorage-এ save করছে।
document.documentElement.setAttribute() → পুরো website-এ theme apply করছে।
data-theme={item} → প্রতিটা theme-এর ছোট preview তৈরি করছে।
Page refresh করলে:
localStorage.getItem("theme")


থেকে আগের theme automatically চলে আসবে।

উদাহরণ:

User selects → cyberpunk
        ↓
setTheme("cyberpunk")
        ↓
localStorage = "cyberpunk"
        ↓
<html data-theme="cyberpunk">
        ↓
পুরো website cyberpunk theme
        ↓
Refresh
        ↓
আবার cyberpunk


একটা গুরুত্বপূর্ণ পার্থক্য: এখানে আমি data-theme পুরো <html>-এ দিয়েছি। তাই ThemeController component-এর বাইরের navbar, sidebar, footer—সব জায়গাতেই DaisyUI theme কাজ করবে।

চাইলে আমি এর আরও সুন্দর version দিতে পারি যেখানে dropdown-এর ভেতরেই প্রতিটি theme-এর color preview দেখা যাবে এবং Dark/Light toggle + 12 themes + localStorage একসাথে থাকবে।


---
হ্যাঁ, বুঝেছি। তুমি চাচ্ছো ThemeController component-টা যেখানে call করবে, সেখানেই শুধু একটা button/dropdown দেখাবে। Button-এ click করলে ১০+ theme-এর option এবং preview দেখাবে।

এটার জন্য ThemeController-কে reusable component বানানো ভালো।

ThemeController.jsx
import { useEffect, useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "dracula",
];

const ThemeController = () => {
  const [theme, setTheme] = useState(
    () => localStorage.getItem("theme") || "light"
  );

  const [open, setOpen] = useState(false);

  useEffect(() => {
    localStorage.setItem("theme", theme);
    document.documentElement.setAttribute("data-theme", theme);
  }, [theme]);

  const handleThemeChange = (newTheme) => {
    setTheme(newTheme);
    setOpen(false);
  };

  return (
    <div className="relative">
      {/* Controller Button */}
      <button
        onClick={() => setOpen(!open)}
        className="btn btn-primary"
      >
        🎨 {theme}
      </button>

      {/* Theme Menu */}
      {open && (
        <div className="absolute right-0 top-12 z-50 w-72 rounded-xl bg-base-100 p-4 shadow-2xl border border-base-300">
          
          <h3 className="font-bold text-lg mb-3">
            Choose Theme
          </h3>

          <div className="grid grid-cols-2 gap-2 max-h-80 overflow-y-auto">
            {themes.map((item) => (
              <button
                key={item}
                onClick={() => handleThemeChange(item)}
                data-theme={item}
                className={`rounded-lg border p-3 text-left bg-base-100 hover:border-primary transition ${
                  theme === item
                    ? "border-primary ring-2 ring-primary"
                    : "border-base-300"
                }`}
              >
                <div className="text-sm font-semibold mb-2">
                  {item}
                </div>

                {/* Color Preview */}
                <div className="flex gap-1">
                  <span className="h-4 w-4 rounded bg-primary" />
                  <span className="h-4 w-4 rounded bg-secondary" />
                  <span className="h-4 w-4 rounded bg-accent" />
                  <span className="h-4 w-4 rounded bg-neutral" />
                </div>
              </button>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default ThemeController;

যেখানে ব্যবহার করবে

ধরো তোমার Navbar.jsx আছে:

import ThemeController from "./ThemeController";

const Navbar = () => {
  return (
    <div className="navbar bg-base-200">
      <div className="flex-1">
        <h1 className="text-xl font-bold">
          My Website
        </h1>
      </div>

      <div>
        <ThemeController />
      </div>
    </div>
  );
};

export default Navbar;


তাহলে navbar-এ শুধু:

┌─────────────────────────────────────────┐
│ My Website                    🎨 light   │
└─────────────────────────────────────────┘


🎨 light button-এ click করলে:

             ┌──────────────────────┐
             │ Choose Theme          │
             │                      │
             │ light     dark       │
             │ 🟦🟪⬛      🟦🟪⬛      │
             │                      │
             │ cupcake   bumblebee   │
             │ 🟦🟪⬛      🟦🟪⬛      │
             │                      │
             │ emerald   corporate   │
             │ 🟦🟪⬛      🟦🟪⬛      │
             │                      │
             │ ...আরও themes        │
             └──────────────────────┘


অর্থাৎ ThemeController যেখানে বসাবে, controller-এর UI সেখানেই থাকবে। Theme change করলে পুরো website-এর DaisyUI theme change হবে, আর localStorage থাকার কারণে refresh করলেও selected theme থাকবে।

আর ThemeController-এর নিজের কোনো বড় layout নেই—তাই Navbar, Sidebar, Settings page, বা যেকোনো জায়গায় <ThemeController /> বসাতে পারবে।

---
হ্যাঁ, তোমার এই index.html-এ:

<html lang="en" data-theme="night">


এখন DaisyUI-এর default theme night সেট করা আছে।

তুমি যদি React-এর ThemeController দিয়ে theme change করো, তাহলে index.html আলাদা করে modify করতে হবে না। React থেকে সরাসরি <html>-এর data-theme পরিবর্তন করা যাবে।

1. তোমার index.html

এভাবে রাখতে পারো:

<!doctype html>
<html lang="en" data-theme="night">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>tailwind_dasyui</title>
  </head>

  <body>
    <div id="root"></div>

    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>


data-theme="night" শুধু initial/default theme হিসেবে থাকবে।

2. ThemeController.tsx

তোমার ক্ষেত্রে আমি এভাবে করার পরামর্শ দেব:

import { useEffect, useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "night",
];

const ThemeController = () => {
  const [theme, setTheme] = useState(() => {
    return localStorage.getItem("theme") || "night";
  });

  const [open, setOpen] = useState(false);

  useEffect(() => {
    // html element select
    const html = document.documentElement;

    // DaisyUI theme change
    html.setAttribute("data-theme", theme);

    // localStorage save
    localStorage.setItem("theme", theme);
  }, [theme]);

  const changeTheme = (newTheme: string) => {
    setTheme(newTheme);
    setOpen(false);
  };

  return (
    <div className="relative">
      {/* Controller Button */}
      <button
        onClick={() => setOpen(!open)}
        className="btn btn-primary"
      >
        🎨 {theme}
      </button>

      {/* Theme Dropdown */}
      {open && (
        <div className="absolute right-0 top-12 z-50 w-80 rounded-xl border border-base-300 bg-base-100 p-4 shadow-2xl">
          <h3 className="mb-3 text-lg font-bold">
            Choose Theme
          </h3>

          <div className="grid max-h-80 grid-cols-2 gap-2 overflow-y-auto">
            {themes.map((item) => (
              <button
                key={item}
                onClick={() => changeTheme(item)}
                data-theme={item}
                className={`rounded-lg border bg-base-100 p-3 text-left ${
                  theme === item
                    ? "border-primary ring-2 ring-primary"
                    : "border-base-300"
                }`}
              >
                <p className="mb-2 text-sm font-semibold">
                  {item}
                </p>

                {/* Theme Preview */}
                <div className="flex gap-1">
                  <span className="h-4 w-4 rounded bg-primary" />
                  <span className="h-4 w-4 rounded bg-secondary" />
                  <span className="h-4 w-4 rounded bg-accent" />
                  <span className="h-4 w-4 rounded bg-neutral" />
                </div>
              </button>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default ThemeController;

3. সবচেয়ে গুরুত্বপূর্ণ অংশ

এই অংশটাই তোমার index.html-এর:

<html data-theme="night">


কে React থেকে control করছে:

const html = document.documentElement;

html.setAttribute("data-theme", theme);


ধরো user cyberpunk select করল।

তখন React automatically করবে:

<html lang="en" data-theme="cyberpunk">


আবার dracula select করলে:

<html lang="en" data-theme="dracula">


আর night select করলে:

<html lang="en" data-theme="night">


তাই index.html manually পরিবর্তন করার দরকার নেই।

4. যেখানে controller দেখাতে চাও

যেমন Navbar.tsx:

import ThemeController from "./ThemeController";

const Navbar = () => {
  return (
    <div className="navbar bg-base-200">
      <div className="flex-1">
        <h1 className="text-xl font-bold">
          My Website
        </h1>
      </div>

      <div>
        <ThemeController />
      </div>
    </div>
  );
};

export default Navbar;


এখন ThemeController শুধু navbar-এর ওই জায়গাতেই button দেখাবে।

5. DaisyUI themes অবশ্যই enable করতে হবে

যদি Tailwind CSS 4 + DaisyUI 5 ব্যবহার করো, CSS-এ:

@import "tailwindcss";

@plugin "daisyui" {
  themes: light, dark, cupcake, bumblebee, emerald, corporate,
    synthwave, retro, cyberpunk, valentine, aqua, night;
}

পুরো flow
index.html
    ↓
data-theme="night"
    ↓
React App
    ↓
<ThemeController />
    ↓
User selects "cyberpunk"
    ↓
setTheme("cyberpunk")
    ↓
useEffect()
    ↓
<html data-theme="cyberpunk">
    ↓
পুরো website cyberpunk 🎨
    ↓
localStorage-এ "cyberpunk" save
    ↓
Refresh করলেও cyberpunk থাকবে


একটা জিনিস খেয়াল রাখবে: data-theme যদি <html>-এ থাকে, তাহলে পুরো React app-এর সব DaisyUI component theme change করবে। তোমার case-এ এটাই সবচেয়ে clean approach।

---
হ্যাঁ, .tsx হলে মূল logic একই। শুধু TypeScript-এর জন্য themes array-কে type দিতে পারো এবং newTheme-এর type string হবে।

তোমার ক্ষেত্রে আমি এই version-টাই recommend করব:

ThemeController.tsx
Writing
import { useEffect, useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "night",
] as const;

type Theme = (typeof themes)[number];

const ThemeController = () => {
  const [theme, setTheme] = useState<Theme>(() => {
    const savedTheme = localStorage.getItem("theme");

    // saved theme valid কিনা check
    if (themes.includes(savedTheme as Theme)) {
      return savedTheme as Theme;
    }

    return "night";
  });

  const [open, setOpen] = useState(false);

  useEffect(() => {
    // <html> element
    const html = document.documentElement;

    // DaisyUI theme apply
    html.setAttribute("data-theme", theme);

    // localStorage save
    localStorage.setItem("theme", theme);
  }, [theme]);

  const changeTheme = (newTheme: Theme) => {
    setTheme(newTheme);
    setOpen(false);
  };

  return (
    <div className="relative">
      {/* Main Button */}
      <button
        onClick={() => setOpen((prev) => !prev)}
        className="btn btn-primary"
      >
        🎨 {theme}
      </button>

      {/* Dropdown */}
      {open && (
        <div className="absolute right-0 top-12 z-50 w-80 rounded-xl border border-base-300 bg-base-100 p-4 shadow-2xl">
          <h3 className="mb-3 text-lg font-bold">
            Choose Theme
          </h3>

          <div className="grid max-h-80 grid-cols-2 gap-2 overflow-y-auto">
            {themes.map((item) => (
              <button
                key={item}
                onClick={() => changeTheme(item)}
                data-theme={item}
                className={`rounded-lg border bg-base-100 p-3 text-left transition ${
                  theme === item
                    ? "border-primary ring-2 ring-primary"
                    : "border-base-300 hover:border-primary"
                }`}
              >
                <p className="mb-2 text-sm font-semibold">
                  {item}
                </p>

                {/* Theme Preview */}
                <div className="flex gap-1">
                  <span className="h-4 w-4 rounded bg-primary" />
                  <span className="h-4 w-4 rounded bg-secondary" />
                  <span className="h-4 w-4 rounded bg-accent" />
                  <span className="h-4 w-4 rounded bg-neutral" />
                </div>
              </button>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default ThemeController;

index.html

এটা একই থাকবে:

<html lang="en" data-theme="night">


React থেকে এই লাইন:

document.documentElement.setAttribute("data-theme", theme);


<html>-এর theme পরিবর্তন করবে।

Navbar.tsx
import ThemeController from "./ThemeController";

const Navbar = () => {
  return (
    <div className="navbar bg-base-200">
      <div className="flex-1">
        <h1 className="text-xl font-bold">
          My Website
        </h1>
      </div>

      <ThemeController />
    </div>
  );
};

export default Navbar;

TypeScript-এ as const কেন?
const themes = [
  "light",
  "dark",
  "night",
  "cyberpunk",
] as const;


এর ফলে TypeScript বুঝবে theme যেকোনো random string না, বরং এই নির্দিষ্ট theme-গুলোর একটা।

তাই:

setTheme("cyberpunk"); // ✅
setTheme("night");     // ✅
setTheme("hello");     // ❌ TypeScript error


এটা .tsx project-এর জন্য বেশ clean এবং type-safe approach।

---

# Next js apply for themecontrol
হ্যাঁ, Next.js + TypeScript (.tsx) + Tailwind + DaisyUI-তেও একইভাবে করা যাবে। তবে Next.js-এ একটা গুরুত্বপূর্ণ বিষয় আছে: localStorage, useState, useEffect browser-only, তাই ThemeController-এ "use client" দিতে হবে।

তোমার setup যদি App Router (app/) হয়, তাহলে এভাবে করো।

1. ThemeController.tsx
"use client";

import { useEffect, useState } from "react";

const themes = [
  "light",
  "dark",
  "cupcake",
  "bumblebee",
  "emerald",
  "corporate",
  "synthwave",
  "retro",
  "cyberpunk",
  "valentine",
  "aqua",
  "night",
] as const;

type Theme = (typeof themes)[number];

const ThemeController = () => {
  const [theme, setTheme] = useState<Theme>("night");
  const [open, setOpen] = useState(false);

  // Browser থেকে saved theme নেওয়া
  useEffect(() => {
    const savedTheme = localStorage.getItem("theme");

    if (savedTheme && themes.includes(savedTheme as Theme)) {
      setTheme(savedTheme as Theme);
    }
  }, []);

  // Theme apply + localStorage
  useEffect(() => {
    document.documentElement.setAttribute("data-theme", theme);
    localStorage.setItem("theme", theme);
  }, [theme]);

  const changeTheme = (newTheme: Theme) => {
    setTheme(newTheme);
    setOpen(false);
  };

  return (
    <div className="relative">
      {/* Theme Button */}
      <button
        onClick={() => setOpen((prev) => !prev)}
        className="btn btn-primary"
      >
        🎨 {theme}
      </button>

      {/* Dropdown */}
      {open && (
        <div className="absolute right-0 top-12 z-50 w-80 rounded-xl border border-base-300 bg-base-100 p-4 shadow-xl">
          <h3 className="mb-3 text-lg font-bold">
            Choose Theme
          </h3>

          <div className="grid max-h-80 grid-cols-2 gap-2 overflow-y-auto">
            {themes.map((item) => (
              <button
                key={item}
                onClick={() => changeTheme(item)}
                data-theme={item}
                className={`rounded-lg border bg-base-100 p-3 text-left ${
                  theme === item
                    ? "border-primary ring-2 ring-primary"
                    : "border-base-300 hover:border-primary"
                }`}
              >
                <p className="mb-2 text-sm font-semibold">
                  {item}
                </p>

                <div className="flex gap-1">
                  <span className="h-4 w-4 rounded bg-primary" />
                  <span className="h-4 w-4 rounded bg-secondary" />
                  <span className="h-4 w-4 rounded bg-accent" />
                  <span className="h-4 w-4 rounded bg-neutral" />
                </div>
              </button>
            ))}
          </div>
        </div>
      )}
    </div>
  );
};

export default ThemeController;

2. layout.tsx

Next.js-এ <html> এখানেই থাকবে।

import type { Metadata } from "next";
import "./globals.css";

export const metadata: Metadata = {
  title: "My Website",
  description: "My website",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en" data-theme="night">
      <body>{children}</body>
    </html>
  );
}


এখানে:

data-theme="night"


মানে initial theme হবে night।

তারপর ThemeController যখন user theme select করবে, এটা:

document.documentElement.setAttribute("data-theme", theme);


<html>-এর theme পরিবর্তন করবে।

3. Navbar-এ ব্যবহার

ধরো:

app/
├── layout.tsx
├── page.tsx
└── components/
    ├── Navbar.tsx
    └── ThemeController.tsx


Navbar.tsx:

import ThemeController from "./ThemeController";

const Navbar = () => {
  return (
    <div className="navbar bg-base-200 px-6">
      <div className="flex-1">
        <h1 className="text-xl font-bold">
          My Website
        </h1>
      </div>

      <ThemeController />
    </div>
  );
};

export default Navbar;


তারপর page.tsx:

import Navbar from "./components/Navbar";

export default function Home() {
  return (
    <>
      <Navbar />

      <main className="p-10">
        <h1 className="text-4xl font-bold">
          Hello Next.js
        </h1>

        <button className="btn btn-primary mt-5">
          Click Me
        </button>
      </main>
    </>
  );
}

4. DaisyUI configuration

তুমি যদি Tailwind CSS 4 + DaisyUI 5 ব্যবহার করো, globals.css:

@import "tailwindcss";

@plugin "daisyui" {
  themes: light, dark, cupcake, bumblebee, emerald, corporate,
    synthwave, retro, cyberpunk, valentine, aqua, night;
}

একটা বিষয় খেয়াল রাখো

Next.js-এ প্রথম render-এর সময়:

<html data-theme="night">


থাকবে।

তারপর browser-side useEffect() চলে এবং:

localStorage
     ↓
saved theme
     ↓
setTheme()
     ↓
data-theme পরিবর্তন


হবে।

অর্থাৎ user একবার cyberpunk select করলে:

প্রথমবার:
night → cyberpunk

Refresh:
localStorage → cyberpunk
             ↓
        cyberpunk


তাই Next.js-এও তোমার আগের approach কাজ করবে, শুধু ThemeController.tsx-এ "use client" অবশ্যই দিতে হবে।

আর যদি তুমি Next.js-এ একদম production-level solution চাও, তাহলে localStorage + useEffect-এর বদলে DaisyUI + next-themes ব্যবহার করা আরও ভালো—বিশেষ করে refresh-এর সময় theme flash (আগে light, পরে dark) এড়ানোর জন্য।

---

