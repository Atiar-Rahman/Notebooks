`Bujhte perechi — **apni jodi nijekei webcam ta off na koren, tahole eta chalte thake**. Kintu jodi **automatically off hoy 2–3 minute por**, tokhon ta bujhte hobe je kichu system-level feature (like USB autosuspend) eta kortese kina.

`Apni ager command diye je **USB autosuspend off** korechilen:

```bash
for d in /sys/bus/usb/devices/*/power/control; do echo on | sudo tee "$d"; done
```

`Eta jodi kaaj kore (mane, webcam ar off hocche na), tahole bujhte hobe je:

>` **System-i webcam ke idle dhore off kore ditchhilo.**

---

## ✅ Shortcut `Bujhte:

|Apni ki koren|Webcam er obostha|
|---|---|
|Nijeke off koren|Off hoy (expected) ✅|
|Off na korle|Chalte thake (bhalo) ✅|
|2–3 min idle thakle off hoy|Power management problem ❌ (solved if autosuspend off)|

---

## 🔧 `Ki Korben Next

`Apni jodi dekhen je **webcam ar auto off hocche na**:

-` Tahole udev rule diye eta **permanently fix** kore felun.
    

###  `Udev rule baniye permanent solution:

```bash
sudo nano /etc/udev/rules.d/99-usb-camera.rules
```

`Likhen:

```
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="1224", ATTR{idProduct}=="2a25", TEST=="power/control", ATTR{power/control}="on"
```

`Save` `kore ber berun:

- `Ctrl + O` → `Enter` → `Ctrl + X`
    

Then run:

```bash
sudo udevadm control --reload
sudo udevadm trigger
```

`Tarpor **reboot** din.

---

### 🔁  `Ekhon theke:

- `Webcam ar auto-off hobe na
    
- `Apni jodi manually off na koren, chalte thakbe
    

---

`Jodi ar kono issue thake (ba apnar specific app-e eita hoy), taile app-er name ta bolun, ami check kore dekhi config lagche kina.

`Apni great vabe troubleshoot korchen 👌 — ekhon just permanent solution apply korlei hobe.

-------
Got it ✅ — you want to **increase the USB autosuspend delay** from `2000 ms` (2 seconds) to **4 hours**, so the webcam won’t auto-suspend for a long time. Let’s calculate and set it properly.

---

## 🧩 Step 1: Convert 4 hours to milliseconds

1 hour = 60 minutes = 3600 seconds  
4 hours = 4 × 3600 = 14400 seconds

Milliseconds = seconds × 1000

```
14400 × 1000 = 14,400,000 ms
```

So **4 hours = 14,400,000 ms** ✅

---

## 🧩 Step 2: Temporarily change autosuspend_delay_ms

```bash
echo 14400000 | sudo tee /sys/bus/usb/devices/1-1/power/autosuspend_delay_ms
```

- This will take effect **immediately**, but **resets on reboot**.
    
- Check the new value:
    

```bash
cat /sys/bus/usb/devices/1-1/power/autosuspend_delay_ms
```

→ Should print `14400000`

---

## 🧩 Step 3: Make it permanent (optional)

1. Create a **udev rule**:
    

```bash
sudo nano /etc/udev/rules.d/99-webcam-autosuspend-delay.rules
```

2. Add this line:
    

```
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="1224", ATTR{idProduct}=="2a25", TEST=="power/autosuspend_delay_ms", ATTR{power/autosuspend_delay_ms}="14400000"
```

3. Reload udev rules:
    

```bash
sudo udevadm control --reload-rules && sudo udevadm trigger
```

Now your webcam’s autosuspend delay is **4 hours permanently**.

---

### 🧩 Step 4: Optional — ensure it stays on

If you want to completely **disable autosuspend** (so it never suspends), you can also do:

```bash
echo on | sudo tee /sys/bus/usb/devices/1-1/power/control
```

---

If you want, I can give you a **single command/script** that **sets autosuspend to 4 hours AND keeps the webcam always on** permanently, so you don’t have to worry about it turning off.

Do you want me to do that?