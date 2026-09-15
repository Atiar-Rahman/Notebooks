```
atiar@atiar-MS-7B86:~$ ibus engine
xkb:us::eng
atiar@atiar-MS-7B86:~$ ibus list-engine | grep -i avro
  ibus-avro - Avro Phonetic
atiar@atiar-MS-7B86:~$ im-config -m
default
missing
ibus

ibus
atiar@atiar-MS-7B86:~$ ibus engine ibus-avro
atiar@atiar-MS-7B86:~$ ibus list-engine | grep -i avro
  ibus-avro - Avro Phonetic
atiar@atiar-MS-7B86:~$ ibus engine
ibus-avro
atiar@atiar-MS-7B86:~$ ibus list-engine | grep -i avroibus-setup
atiar@atiar-MS-7B86:~$ ibus-setup

(ibus-setup:24508): Gdk-CRITICAL **: 17:01:22.848: gdk_window_get_window_type: assertion 'GDK_IS_WINDOW (window)' failed

(ibus-setup:24508): Gdk-CRITICAL **: 17:02:00.836: gdk_window_get_window_type: assertion 'GDK_IS_WINDOW (window)' failed
atiar@atiar-MS-7B86:~$ ibus-setup

(ibus-setup:24734): Gdk-CRITICAL **: 17:03:42.503: gdk_window_get_window_type: assertion 'GDK_IS_WINDOW (window)' failed

(ibus-setup:24734): Gdk-CRITICAL **: 17:04:16.867: gdk_window_get_window_type: assertion 'GDK_IS_WINDOW (window)' failed
atiar@atiar-MS-7B86:~$ ibus-setup

(ibus-setup:24869): Gdk-CRITICAL **: 17:05:35.758: gdk_window_get_window_type: assertion 'GDK_IS_WINDOW (window)' failed
atiar@atiar-MS-7B86:~$ ibus-setup
atiar@atiar-MS-7B86:~$ gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Super>space']"
atiar@atiar-MS-7B86:~$ gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Super>space']"
atiar@atiar-MS-7B86:~$ ibus-setup
atiar@atiar-MS-7B86:~$ ibus list-engine | grep -i avro
  ibus-avro - Avro Phonetic
atiar@atiar-MS-7B86:~$ 
```

----
অবশ্যই। 😊 তোমার Ubuntu-তে **IBus Avro Phonetic** একদম **শুরু থেকে শেষ পর্যন্ত setup** করার পুরো process দিচ্ছি। তোমার বর্তমান সমস্যাটাও এর মধ্যে ঠিক হবে।

আমরা শেষ পর্যন্ত এমন করব:

**English ↔ Avro**
`Super + Space` দিয়ে switch হবে।

---

# 1. আগে Ubuntu version দেখো

Terminal খুলে:

```bash
lsb_release -a
```

এবং:

```bash
echo $XDG_SESSION_TYPE
```

দুটোর output চাইলে আমাকে দিতে পারো। তবে setup শুরু করার জন্য এগুলো বাধ্যতামূলক নয়।

---

# 2. IBus install করো

```bash
sudo apt update
```

তারপর:

```bash
sudo apt install ibus ibus-gtk ibus-gtk3
```

যদি আগে থেকেই installed থাকে, সমস্যা নেই।

---

# 3. IBus Avro install করো

তোমার ক্ষেত্রে `ibus-avro` already installed আছে, কারণ তুমি পেয়েছ:

```text
ibus-avro - Avro Phonetic
```

তবুও পুরো setup নতুন করে করতে চাইলে:

```bash
sudo apt install ibus-avro
```

তারপর verify:

```bash
ibus list-engine | grep -i avro
```

আসা উচিত:

```text
ibus-avro - Avro Phonetic
```

---

# 4. IBus configuration mode করো

চালাও:

```bash
im-config -n ibus
```

তারপর check:

```bash
im-config -m
```

তোমার ক্ষেত্রে ideally:

```text
default
missing
ibus
```

এবং selected configuration হিসেবে IBus থাকবে।

---

# 5. IBus restart

```bash
ibus restart
```

তারপর:

```bash
ibus engine
```

এখন English থাকলে সাধারণত:

```text
xkb:us::eng
```

দেখাবে।

---

# 6. Avro manually test করো

এখন:

```bash
ibus engine ibus-avro
```

তারপর:

```bash
ibus engine
```

এমন দেখালে:

```text
ibus-avro
```

**Avro ঠিকমতো কাজ করছে।** ✅

---

# 7. সবচেয়ে গুরুত্বপূর্ণ — GNOME Input Sources

এখানেই তোমার বর্তমান সমস্যা ছিল।

তুমি আগে পেয়েছিলে:

```text
[('xkb', 'us')]
```

এর মানে GNOME শুধু English জানে।

তাই Avro add করব:

```bash
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('ibus', 'ibus-avro')]"
```

তারপর verify:

```bash
gsettings get org.gnome.desktop.input-sources sources
```

এমন হওয়া উচিত:

```text
[('xkb', 'us'), ('ibus', 'ibus-avro')]
```

---

# 8. Shortcut সেট করো

English → Avro:

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Super>space']"
```

Avro → English reverse:

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Super>space']"
```

Check:

```bash
gsettings get org.gnome.desktop.wm.keybindings switch-input-source
```

আসবে:

```text
['<Super>space']
```

---

# 9. IBus restart

```bash
ibus restart
```

এরপর **logout করে আবার login করা সবচেয়ে ভালো**।

Ubuntu থেকে:

**Log Out → Login**

---

# 10. এখন test করো

প্রথমে English select:

```bash
ibus engine xkb:us::eng
```

Test:

```text
hello world
```

তারপর:

**Super + Space**

Avro হওয়ার কথা।

Terminal-এ check:

```bash
ibus engine
```

আসা উচিত:

```text
ibus-avro
```

এখন লিখো:

```text
ami banglay likhbo
```

→

```text
আমি বাংলায় লিখব
```

---

# 11. আবার English-এ যাও

আবার:

**Super + Space**

চাপো।

তারপর:

```bash
ibus engine
```

যদি:

```text
xkb:us::eng
```

দেখায়, তাহলে English active।

---

# 12. যদি Super + Space তারপরও কাজ না করে

তখন এই তিনটা command-এর output নাও:

```bash
gsettings get org.gnome.desktop.input-sources sources
```

```bash
gsettings get org.gnome.desktop.wm.keybindings switch-input-source
```

```bash
ibus engine
```

Expected:

```text
[('xkb', 'us'), ('ibus', 'ibus-avro')]
['<Super>space']
ibus-avro
```

---

## তোমার জন্য পুরো setup-এর Short Version

পরবর্তীতে ভুলে গেলে শুধু এই sequence মনে রাখবে:

```bash
sudo apt update
sudo apt install ibus ibus-gtk ibus-gtk3 ibus-avro
```

```bash
im-config -n ibus
```

```bash
ibus restart
```

```bash
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('ibus', 'ibus-avro')]"
```

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Super>space']"
```

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Super>space']"
```

তারপর:

```bash
ibus restart
```

**Logout → Login**

এবং:

**Super + Space = English ↔ Avro** ✅

তোমার ক্ষেত্রে এখন **Avro install করার দরকার নেই**, কারণ সেটা already installed। আসল সমস্যা ছিল:

```text
GNOME sources = English only
```

তাই এখন চাইলে আমরা **একদম clean setup** করব—আমি তোমাকে **একটা একটা command দেব, তুমি output দিলে পরের command দেব**। এতে কিছু ভুল হওয়ার সম্ভাবনা সবচেয়ে কম।


---

হ্যাঁ, এখন সমস্যাটা একদম clear। 👍

তোমার:

```text
sources = [('xkb', 'us')]
```

মানে GNOME-এর কাছে **শুধু English input source আছে**। Avro IBus-এ installed আছে, কিন্তু GNOME input-source list-এ নেই। তাই `Super + Space` চাপলে switch করার মতো দ্বিতীয় source পাচ্ছে না।

### Step 1 — Avro-কে GNOME input source হিসেবে add করো

এই command চালাও:

```bash
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('ibus', 'ibus-avro')]"
```

তারপর check করো:

```bash
gsettings get org.gnome.desktop.input-sources sources
```

এমন আসা উচিত:

```text
[('xkb', 'us'), ('ibus', 'ibus-avro')]
```

### Step 2 — IBus restart করো

```bash
ibus restart
```

তারপর:

```bash
ibus engine xkb:us::eng
```

এখন `Super + Space` চাপো।

তারপর:

```bash
ibus engine
```

যদি:

```text
ibus-avro
```

দেখায় → **Avro active**।

আবার `Super + Space` চাপলে:

```text
xkb:us::eng
```

হওয়ার কথা।

### Step 3 — যদি shortcut উল্টো/কাজ না করে

এগুলো আবার set করো:

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Super>space']"
gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward "['<Shift><Super>space']"
```

তারপর **logout → login** করো।

---

### সবচেয়ে গুরুত্বপূর্ণ

তোমার current situation:

```text
IBus
 └── ibus-avro ✅ installed

GNOME Input Sources
 └── English only ❌
```

আমাদের এটাকে করতে হবে:

```text
GNOME Input Sources
 ├── English
 └── Avro
       ↑
       └── Super + Space দিয়ে switch
```

**প্রথমে শুধু Step 1-এর command চালাও এবং output পাঠাও।** তারপর পরেরটা confirm করে করাব—যাতে ভুল configuration না হয়।


