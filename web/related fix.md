
---

## 🔌 USB webcam auto off – next fixes

### 1️⃣ USB power control force করে “on” করো

আগে webcam কোন device সেটা বের করি:

```bash
lsusb
```

এখানে webcam-এর line দেখাবে (যেমন: _USB Camera_, _Logitech_, _HD Webcam_ ইত্যাদি)

এখন USB power status দেখো:

```bash
cat /sys/bus/usb/devices/*/power/control
```

সব জায়গায় `auto` থাকলে, আমরা `on` করে দেব।

👉 Quick fix:

```bash
for i in /sys/bus/usb/devices/*/power/control; do echo on | sudo tee $i; done
```

---

### 2️⃣ USB port change করো (surprisingly effective 😅)

- Front USB → Rear USB (বা উল্টোটা)
    
- USB hub থাকলে **hub বাদ দিয়ে direct laptop/PC-তে** লাগাও
    

---

### 3️⃣ Webcam driver reset (without reboot)

```bash
sudo modprobe -r uvcvideo
sudo modprobe uvcvideo
```

তারপর test:

```bash
cheese
```

---

### 4️⃣ Cable / Power issue check

USB webcam হলে খুব common:

- Cable একটু নড়লে off হয়
    
- Low-quality USB cable  
    👉 অন্য cable থাকলে একবার try করো
    

---

### 5️⃣ Browser হলে (Chrome / Firefox)

Camera off হয়ে গেলে browser-level issue হতে পারে।

Chrome:

```
chrome://settings/content/camera
```

Firefox:

```
about:preferences#privacy
```

একটাই webcam select করা আছে কিনা দেখো।

---

## 🧪 Stress test (best test)

```bash
mpv av://v4l2:/dev/video0
```

৫–১০ মিনিট চালু থাকলে → hardware + driver OK  
এখানেই off হলে → USB power / cable issue almost sure

---

ভালো 👍 এই আউটপুটটাই আসলে প্রমাণ করে 👉 **TLP ইনস্টল আছে**।  
তুমি শুধু option দাওনি বলে usage দেখাচ্ছে।

এখন ঠিকভাবে করি 👇

---

## 🔥 Step 1 (MOST IMPORTANT): TLP এখনই বন্ধ করে test

এটা দাও:

```bash
sudo tlp stop
```

তারপর **সাথে সাথে**:

```bash
cheese
```

বা যেই app-এ webcam off হয়, সেটা চালাও।

⏱️ ৫–১০ মিনিট দেখো —  
👉 **যদি এখন off না হয়** → 100% confirmed: **TLP USB power কাটছে**।

---

## 🔒 Step 2: Permanent fix (TLP থাকলেও webcam safe)

এখন config edit করো:

```bash
sudo nano /etc/tlp.conf
```

এই লাইনগুলো খুঁজে বের করো (থাকলে uncomment করো, না থাকলে add করো):

```
USB_AUTOSUSPEND=0
USB_BLACKLIST=""
```

Save করো → তারপর:

```bash
sudo systemctl restart tlp
```

Reboot-এর পরেও webcam stable থাকবে ✅

---

## 🧪 Extra confirm (optional but useful)

```bash
tlp-stat -u
```

এখানে webcam device-এর পাশে `autosuspend = disabled` দেখা উচিত।

---

## যদি এখনো off হয় 😬

তখন আমরা নিশ্চিত হবো এটা **hardware / cable / USB port** issue।

সেক্ষেত্রে next step:

```bash
dmesg | tail -30
```

(webcam off হওয়ার ঠিক পরেই)

---

### এখন আমাকে শুধু এটা বলো 👇

`sudu tlp stop` দেওয়ার পর **off হওয়া বন্ধ হয়েছে কি না**?

এটা বললেই আমি জানব—  
🔧 **software fix done** নাকি  
🔌 **hardware verdict দিতে হবে**