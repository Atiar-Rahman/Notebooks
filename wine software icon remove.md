ভালো 👍 এখন পরিষ্কার বোঝা যাচ্ছে সমস্যা কোথায়।

তোমার output বলছে:

```bash
ls ~/.local/share/applications | grep wine
wine
```

মানে এখানে `wine-xxx.desktop` না, বরং **wine নামে একটা folder** আছে।

তাই `wine-*.desktop` delete হচ্ছে না।

---

# ✅ ঠিক করার সঠিক উপায়

## 🔍 Step 1: ভিতরে কী আছে দেখো

```bash
ls ~/.local/share/applications/wine
```

এখানে তোমার uninstall করা software এর shortcut থাকবে।

---

## 🧹 Step 2: পুরো wine menu folder delete করো

যদি সব Wine shortcut remove করতে চাও:

```bash
rm -rf ~/.local/share/applications/wine
```

---

## 🔄 Step 3: Desktop refresh

```bash
update-desktop-database ~/.local/share/applications
```

তারপর:

```bash
killall gnome-shell
```

(যদি Ubuntu X11 ব্যবহার করো)

না হলে simple logout/login করলেই হবে।

---

# 🎯 এতে কী হবে?

✅ Menu থেকে Wine installed app icon চলে যাবে  
✅ Broken shortcut remove হবে  
❌ Wine uninstall হবে না

---

Nice 😄🔥

মানে এখন icon চলে গেছে — problem solved 👍

Wine অনেক সময় uninstall করলে shortcut রেখে দেয়, তাই manual folder delete করাটাই ছিল আসল fix।

---

যদি ভবিষ্যতে এমন হয়:

📁 এই path মনে রাখবে

```
~/.local/share/applications/wine
```

ওখানেই Wine এর menu shortcut থাকে।

---

আর যদি কখনো Wine একদম clean reset করতে চাও:

```
rm -rf ~/.wine
```

---

