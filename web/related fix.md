Now we have the exact root cause in your log:

### 🚨 Key error

```
Requested GL implementation (gl=none,angle=none) not found in allowed implementations
(gl=egl-angle,angle=default)

Exiting GPU process due to errors during initialization
GPU process was unable to boot: GPU access is disabled due to frequent crashes
```

---

## 💥 What this actually means

Chrome is **NOT failing because of your AMD driver**.

It is failing because:

> Chrome is trying to use ANGLE/OpenGL backend, but your system/Chrome build is missing or blocked from using EGL-ANGLE.

So Chrome ends up in this broken state:

- GPU process starts ❌
    
- ANGLE backend selection fails ❌
    
- GPU process crashes repeatedly ❌
    
- Chrome permanently blacklists GPU ❌
    
- WebGL disabled completely ❌
    

---

## 🧠 Why this is happening (most likely)

One of these is true:

### 1. Broken/missing ANGLE/EGL support in your Chrome build

Your Chrome package is not correctly linking to EGL/OpenGL backend.

### 2. Missing system EGL libraries (VERY common on Ubuntu)

You likely are missing:

- `libegl1`
    
- `libgl1-mesa-dri`
    
- `mesa-vulkan-drivers`
    

### 3. Chrome GPU crash blacklist got triggered

After repeated startup failures, Chrome permanently disables GPU:

> “GPU access is disabled due to frequent crashes”

---

## ✅ FIX (do this in order)

### 🔧 Step 1 — install missing graphics libraries

Run:

```bash
sudo apt update
sudo apt install --reinstall \
libgl1-mesa-dri \
libegl1 \
mesa-vulkan-drivers \
libgbm1
```

Then reboot:

```bash
sudo reboot
```

---

### 🔧 Step 2 — reset Chrome GPU crash state

After reboot:

```bash
mv ~/.config/google-chrome/Default/GPUCache ~/.config/google-chrome/Default/GPUCache.backup
```

(or just reset full profile if needed later)

---

### 🔧 Step 3 — force correct backend

Run Chrome like this:

```bash
google-chrome --use-gl=egl --ignore-gpu-blocklist
```

---

### 🔧 Step 4 — if still broken (important test)

Try Chromium:

```bash
sudo snap install chromium
```

If Chromium works → Chrome package is broken  
If Chromium also fails → system EGL stack issue

---

## 🎯 What I strongly suspect

Given your logs:

> `gl=none,angle=none`

This usually happens when:

👉 **EGL/OpenGL loader in Chrome is broken or missing system EGL libs**

NOT a GPU problem.

---

## 🧾 Summary

Your AMD GPU is fine.

The real problem is:

> Chrome cannot initialize EGL/OpenGL backend → GPU process crashes → WebGL disabled.

---

If you want, I can give you a **1-command permanent fix** (clean reinstall + correct flags + guaranteed Figma working setup).