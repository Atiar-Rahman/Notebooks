If you want to **block YouTube on Ubuntu**, here are some good apps and methods you can use 👇

---

## 1️⃣ 🛡️ **Cold Turkey**

**Best for:** Strong website blocking (hard to bypass)

### Features:

* Block specific websites (like youtube.com)
* Set timer (focus mode)
* Very hard to disable while active

### Install on Ubuntu:

Download Linux version from their website and install `.deb` file:

```bash
sudo dpkg -i filename.deb
```

✔ Good for students
✔ Focus mode
❌ Paid version required for full features

---

## 2️⃣ 🔒 **Focus To-Do**

**Best for:** Pomodoro + light website blocking

* Timer-based study system
* Helps reduce distraction
* Works with browser extensions

✔ Good for productivity
❌ Not very strong blocking

---

## 3️⃣ 🌐 Browser Extension (Easy Method)

If you use Chrome or Firefox:

### 🔹 **BlockSite**

* Add to Chrome/Firefox
* Add youtube.com to block list
* Set password protection

✔ Easy
✔ Free
❌ Can be removed easily

---

## 4️⃣ 💻 Hosts File Method (Free & Powerful)

This is the strongest **free method**.

Edit hosts file:

```bash
sudo nano /etc/hosts
```

Add this line at bottom:

```
127.0.0.1 youtube.com
127.0.0.1 www.youtube.com
```

Save → Restart browser

✔ Completely free
✔ System-level block
❌ Easy to undo if you know Linux

---

## 5️⃣ 🛜 Router-Level Blocking (Advanced)

If you want to block YouTube for entire WiFi:

* Login to router admin panel
* Use parental control / URL filtering
* Add youtube.com

✔ Works for all devices
✔ Hard to bypass
❌ Requires router access

---

# 🔥 My Recommendation (For You)

Since you are a CSE student and use Ubuntu for projects:

👉 Use **hosts file method + BlockSite extension together**
This gives double protection.

---

If you want, tell me:

* Do you want temporary blocking?
* Or permanent blocking?
* Only browser or whole system?

I’ll give you exact step-by-step setup.
