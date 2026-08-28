**Flowbite** হলো Tailwind CSS-এর উপর তৈরি একটি **UI component library**। সহজভাবে বললে, Tailwind দিয়ে নিজে নিজে button, navbar, modal, dropdown ইত্যাদি বানানোর বদলে Flowbite-এর ready-made components ব্যবহার করতে পারো।

### 🔹 উদাহরণ

Flowbite-এ আগে থেকেই এমন component থাকে:

- 🔘 Buttons
    
- 🧭 Navbar
    
- 📋 Dropdown
    
- 🪟 Modal
    
- 📝 Forms / Input
    
- 🃏 Cards
    
- 🔔 Alerts
    
- 📑 Tables
    
- 📱 Drawer
    
- 🌓 Dark mode components
    

তাই:

```text
Tailwind CSS
     ↓
Flowbite
     ↓
Ready-made UI Components
     ↓
React / Next.js Website
```

### Tailwind বনাম Flowbite

**Tailwind:**

```jsx
<button className="px-4 py-2 rounded-lg bg-blue-600 text-white">
  Login
</button>
```

তুমি নিজে styling করবে।

**Flowbite:**

Flowbite-এর component structure ব্যবহার করে দ্রুত professional UI বানাতে পারো।

### React/Next.js-এ

Flowbite-এর React package আছে:

```bash
npm install flowbite-react
```

তারপর component ব্যবহার করা যায়:

```jsx
import { Button } from "flowbite-react";

export default function App() {
  return (
    <Button>
      Login
    </Button>
  );
}
```

### ⭐ কখন Flowbite ব্যবহার করবে?

যদি তুমি **Next.js + Tailwind** দিয়ে দ্রুত dashboard, admin panel, SaaS বা business website বানাতে চাও → **Flowbite বেশ useful**।

আর যদি Tailwind-এর class নিজে লিখে **পুরো design নিজের মতো control** করতে চাও → সরাসরি Tailwind ব্যবহার করো।

**এক লাইনে:**

> **Tailwind = styling framework**  
> **Flowbite = Tailwind-এর উপর তৈরি ready-made UI components**


