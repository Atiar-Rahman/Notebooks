অবশ্যই। `nmap` মূলত **network/host discovery, port scanning, service/version detection এবং কিছু ক্ষেত্রে OS detection** করার জন্য ব্যবহৃত হয়। নিজের lab, নিজের server, বা অনুমতি থাকা network-এ ব্যবহার করাই নিরাপদ ও বৈধ।

নিচে তোমার দেখানো Nmap 7.99 help-এর গুরুত্বপূর্ণ অংশগুলো সহজভাবে দিলাম।

### 1. Basic scan

```bash
nmap 192.168.1.1
```

একটি host-এর common TCP ports scan করবে।

```bash
nmap example.com
```

Hostname দিয়েও scan করা যায়।

---

### 2. Host জীবিত আছে কি না দেখা — `-sn`

```bash
nmap -sn 192.168.1.0/24
```

এটি মূলত **host discovery** করে; সাধারণ port scan করে না।

উদাহরণস্বরূপ, নিজের Wi-Fi network-এ কোন কোন device বর্তমানে reachable তা বোঝার জন্য কাজে লাগে।

---

### 3. নির্দিষ্ট port scan — `-p`

```bash
nmap -p 22 192.168.1.10
```

শুধু port `22` পরীক্ষা করবে।

একাধিক:

```bash
nmap -p 22,80,443 192.168.1.10
```

Range:

```bash
nmap -p 1-1000 192.168.1.10
```

সব TCP port:

```bash
nmap -p- 192.168.1.10
```

---

### 4. Service ও version বের করা — `-sV`

```bash
nmap -sV 192.168.1.10
```

যেমন কোনো open port-এ SSH/HTTP ইত্যাদি চলছে কিনা এবং সম্ভব হলে service-এর version শনাক্ত করে।

উদাহরণ:

```text
22/tcp   open  ssh    OpenSSH ...
80/tcp   open  http   Apache ...
```

এটি network administration ও security assessment-এ খুব গুরুত্বপূর্ণ।

---

### 5. Default NSE scripts — `-sC`

```bash
nmap -sC 192.168.1.10
```

Nmap-এর default **NSE (Nmap Scripting Engine)** scripts চালায়।

Service detection-এর সঙ্গে:

```bash
nmap -sC -sV 192.168.1.10
```

নিজের lab/server-এর basic security assessment-এর জন্য এটি বহুল ব্যবহৃত combination।

---

### 6. OS detection — `-O`

```bash
sudo nmap -O 192.168.1.10
```

Network behavior দেখে target-এর operating system সম্পর্কে অনুমান করার চেষ্টা করে।

`sudo` অনেক ক্ষেত্রে দরকার হয় কারণ কিছু scan-এর জন্য raw packets ব্যবহৃত হয়।

---

### 7. `-A` — অনেক কিছু একসাথে

```bash
sudo nmap -A 192.168.1.10
```

`-A` সাধারণত একসাথে চালায়:

* OS detection
* Version detection
* Default scripts
* Traceroute

অর্থাৎ এটি তুলনামূলকভাবে **বেশি intrusive/noisy** scan হতে পারে। অনুমতি থাকা target-এ ব্যবহার করা উচিত।

---

### 8. Fast scan — `-F`

```bash
nmap -F 192.168.1.10
```

Nmap-এর ছোট common-port set ব্যবহার করে দ্রুত scan করে।

---

### 9. Top ports

```bash
nmap --top-ports 100 192.168.1.10
```

সব port না দেখে সবচেয়ে common 100টি port পরীক্ষা করবে।

---

### 10. UDP scan — `-sU`

```bash
sudo nmap -sU 192.168.1.10
```

TCP-এর বদলে UDP ports পরীক্ষা করে।

যেমন DNS, DHCP ইত্যাদি UDP-based service খুঁজতে কাজে লাগতে পারে। UDP scan সাধারণত TCP scan-এর চেয়ে ধীর।

---

### 11. TCP SYN scan — `-sS`

```bash
sudo nmap -sS 192.168.1.10
```

এটি Nmap-এর বহুল ব্যবহৃত TCP scanning technique।

সহজভাবে:

```text
Nmap → SYN
       ↓
Target
       ↓
SYN/ACK → port সম্ভবত open
RST     → port closed
```

---

### 12. শুধু open port দেখানো — `--open`

```bash
nmap --open 192.168.1.10
```

Output-এ মূলত open/possibly-open ports-এ focus করে।

---

### 13. DNS resolution বন্ধ — `-n`

```bash
nmap -n 192.168.1.0/24
```

DNS lookup না করায় কিছু ক্ষেত্রে scan দ্রুত হতে পারে।

---

### 14. Verbose output — `-v`

```bash
nmap -v 192.168.1.10
```

আরও বিস্তারিত progress/output দেখায়।

আরও বেশি:

```bash
nmap -vv 192.168.1.10
```

---

### 15. Output save করা

Normal:

```bash
nmap -oN scan.txt 192.168.1.10
```

XML:

```bash
nmap -oX scan.xml 192.168.1.10
```

একসাথে বিভিন্ন format:

```bash
nmap -oA myscan 192.168.1.10
```

এতে `myscan.nmap`, `myscan.xml`, `myscan.gnmap` ধরনের output পাওয়া যায়।

---

## Nmap-এর একটি practical learning sequence

নিজের Kali/Linux lab-এ এভাবে practice করতে পারো:

```bash
# 1. নিজের machine
nmap localhost

# 2. নিজের LAN-এর live hosts
nmap -sn 192.168.1.0/24

# 3. একটি নিজের lab host-এর common ports
nmap 192.168.1.10

# 4. নির্দিষ্ট ports
nmap -p 22,80,443 192.168.1.10

# 5. Service/version
nmap -sV 192.168.1.10

# 6. Default NSE scripts
nmap -sC -sV 192.168.1.10

# 7. নিজের authorized lab-এ OS detection
sudo nmap -O 192.168.1.10
```

### Nmap-এর বড় picture

```text
Target
  │
  ├── Host discovery (-sn)
  │       ↓
  ├── Port discovery (-p / -F / --top-ports)
  │       ↓
  ├── Service detection (-sV)
  │       ↓
  ├── NSE scripts (-sC / --script)
  │       ↓
  ├── OS detection (-O)
  │       ↓
  └── Report (-oN / -oX / -oA)
```

**বিশেষ করে `-sS`, `-sU`, `-sV`, `-sC`, `-O`, `-A`, `-p`, `-sn`, `--script`—এইগুলো আগে ভালোভাবে শিখলে Nmap-এর মূল ধারণাটা পরিষ্কার হয়ে যাবে।**

চাইলে আমি তোমাকে **Kali Linux-এ Nmap-এর beginner → intermediate → advanced একটি hands-on lab course** বানিয়ে দিতে পারি, যেখানে প্রতিটি command-এর output কীভাবে পড়তে হয় সেটাও দেখাব।

For learning Nmap

* Read Nmap output line by line
* Practice in a safe lab


----
অবশ্যই। নিচে **Kali Linux-এ Nmap Beginner → Intermediate → Advanced Hands-on Lab Course** দিলাম। পুরো course-টি এমনভাবে সাজানো যে আগে basic networking বুঝবে, তারপর scanning, service enumeration, NSE, output analysis এবং শেষে একটি controlled security-assessment workflow করবে।

> **Lab rule:** শুধু নিজের machine, নিজের VM, অথবা স্পষ্ট অনুমতি থাকা target-এ scan করবে। Internet-এর random IP/domain scan করে practice করার দরকার নেই।

# 🛡️ Nmap Hands-on Lab Course

## Lab setup

সবচেয়ে ভালো setup:

```text
┌──────────────┐        ┌────────────────┐
│ Kali Linux   │        │ Target VM      │
│ Nmap         │ ────── │ Linux/Windows  │
│ Scanner      │        │ Your lab       │
└──────────────┘        └────────────────┘
```

Target হিসেবে নিজের একটি Linux VM ব্যবহার করতে পারো। Kali এবং target-কে একই **Host-only/Internal Network**-এ রাখলে Internet-এর অন্য system accidentally scan হওয়ার সম্ভাবনা কমে।

প্রথমে Kali-তে:

```bash
nmap --version
```

তারপর:

```bash
ip addr
```

এবং:

```bash
ip route
```

নিজের lab subnet চিনে নাও।

---

# 🟢 Level 1 — Beginner

## Lab 1 — নিজের machine scan

```bash
nmap localhost
```

অথবা:

```bash
nmap 127.0.0.1
```

### লক্ষ্য

Nmap কী ধরনের information দেখায় সেটা বোঝা।

Output সাধারণত এরকম:

```text
PORT     STATE    SERVICE
22/tcp   open     ssh
80/tcp   open     http
```

এখানে:

* `22` → port number
* `tcp` → protocol
* `open` → সেখানে service listening করছে
* `ssh` → Nmap-এর service identification

---

# Lab 2 — Target discovery

নিজের lab network ধরো:

```text
192.168.56.0/24
```

তারপর:

```bash
nmap -sn 192.168.56.0/24
```

### শেখার বিষয়

`-sn` সাধারণত **host discovery** করে; এটি traditional port scan নয়।

তোমার লক্ষ্য:

```text
কতগুলো host alive?
কোন IP কোন machine?
```

---

# Lab 3 — Basic port scan

নিজের target VM:

```bash
nmap 192.168.56.20
```

তারপর output লিখে রাখো।

উদাহরণ:

```text
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
```

### Exercise

নিজেকে জিজ্ঞেস করো:

1. কোন port open?
2. TCP না UDP?
3. কোন service শনাক্ত হয়েছে?
4. কোন port closed?
5. কোন port filtered হতে পারে?

---

# Lab 4 — Specific ports

```bash
nmap -p 22,80,443 192.168.56.20
```

Port range:

```bash
nmap -p 1-1000 192.168.56.20
```

সব TCP port:

```bash
nmap -p- 192.168.56.20
```

### গুরুত্বপূর্ণ ধারণা

```text
-p 22
```

= একটি port

```text
-p 22,80,443
```

= নির্দিষ্ট ports

```text
-p 1-1000
```

= range

```text
-p-
```

= সব TCP port

---

# Lab 5 — Fast scan

```bash
nmap -F 192.168.56.20
```

তারপর compare করো:

```bash
nmap 192.168.56.20
```

এবং:

```bash
nmap -F 192.168.56.20
```

### Question

দুই scan-এ port-এর সংখ্যা/ফলাফল কেন আলাদা হতে পারে?

---

# 🟡 Level 2 — Intermediate

## Lab 6 — Service Version Detection

এখন:

```bash
nmap -sV 192.168.56.20
```

এতে Nmap open ports-এর service এবং সম্ভাব্য version শনাক্ত করার চেষ্টা করবে।

উদাহরণ:

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH ...
80/tcp open  http    Apache ...
```

### লক্ষ্য

শুধু:

> "port 80 open"

না বলে বুঝতে শেখা:

> "port 80-এ HTTP service চলছে এবং Nmap একটি সম্ভাব্য server/version শনাক্ত করেছে।"

---

# Lab 7 — Default NSE scripts

```bash
nmap -sC 192.168.56.20
```

তারপর:

```bash
nmap -sC -sV 192.168.56.20
```

এখানে `-sC` default NSE scripts চালায়।

### NSE কী?

NSE = **Nmap Scripting Engine**

এটি Nmap-কে শুধু port scanner না রেখে বিভিন্ন ধরনের network/service information সংগ্রহ করতে সাহায্য করে।

---

# Lab 8 — OS Detection

নিজের lab target-এ:

```bash
sudo nmap -O 192.168.56.20
```

আরও aggressive OS guessing:

```bash
sudo nmap --osscan-guess 192.168.56.20
```

### মনে রাখবে

OS detection সবসময় 100% accurate নয়।

Output-কে:

> "Nmap অনুমান করছে..."

হিসেবে দেখবে, absolute fact হিসেবে নয়।

---

# Lab 9 — `-A` বোঝা

```bash
sudo nmap -A 192.168.56.20
```

`-A` একসাথে বেশ কিছু detection capability চালায়, যেমন:

```text
OS detection
Service/version detection
Default NSE scripts
Traceroute
```

এটি beginner-এর প্রথম command হওয়া উচিত নয়। আগে আলাদা আলাদা option বুঝে তারপর `-A` ব্যবহার করাই ভালো।

---

# Lab 10 — UDP

নিজের lab target:

```bash
sudo nmap -sU --top-ports 20 192.168.56.20
```

তারপর নির্দিষ্ট UDP port:

```bash
sudo nmap -sU -p 53 192.168.56.20
```

### কেন UDP আলাদা?

TCP এবং UDP-এর behavior আলাদা। তাই TCP scan-এ কোনো service না পাওয়া মানেই UDP-তে service নেই—এমন নয়।

---

# Lab 11 — TCP বনাম UDP

একটি lab target নিয়ে:

```bash
nmap -p 1-1000 192.168.56.20
```

তারপর:

```bash
sudo nmap -sU --top-ports 100 192.168.56.20
```

একটি table বানাও:

| Protocol | Open ports | Services |
| -------- | ---------- | -------- |
| TCP      | ?          | ?        |
| UDP      | ?          | ?        |

এটা network enumeration-এর একটি গুরুত্বপূর্ণ skill।

---

# 🟠 Level 3 — Advanced

## Lab 12 — NSE script categories

NSE script-এর help দেখতে:

```bash
nmap --script-help=default
```

Script database সম্পর্কে:

```bash
ls /usr/share/nmap/scripts/
```

নির্দিষ্ট script-এর help:

```bash
nmap --script-help=http-title
```

তারপর নিজের HTTP-enabled lab target-এ:

```bash
nmap --script=http-title -p 80 192.168.56.20
```

### লক্ষ্য

Script কী করে সেটা **আগে বুঝবে**, তারপর lab target-এ চালাবে।

---

# Lab 13 — HTTP enumeration

যদি নিজের lab VM-এ HTTP server থাকে:

```bash
nmap -sV -p 80,443 192.168.56.20
```

তারপর:

```bash
nmap --script=http-title -p 80 192.168.56.20
```

এখানে লক্ষ্য হচ্ছে:

```text
Port
 ↓
Service
 ↓
Application protocol
 ↓
Additional metadata
```

এই methodology বোঝা।

---

# Lab 14 — Scan timing

নিজের lab target-এ timing template compare করতে পারো:

```bash
nmap -T2 192.168.56.20
```

```bash
nmap -T3 192.168.56.20
```

```bash
nmap -T4 192.168.56.20
```

সাধারণ ধারণা:

```text
T0/T1 → very slow
T2    → polite/slower
T3    → normal
T4    → faster
T5    → very aggressive
```

Lab-এর বাইরে শুধু speed-এর জন্য aggressive timing ব্যবহার করার দরকার নেই।

---

# Lab 15 — Output save

একটি assessment-এর output সংরক্ষণ করো:

```bash
nmap -sV -oN scan.txt 192.168.56.20
```

একসাথে major formats:

```bash
nmap -sV -oA lab-scan 192.168.56.20
```

তারপর:

```bash
ls lab-scan*
```

তুমি দেখতে পাবে বিভিন্ন output format।

---

# Lab 16 — `--reason`

```bash
nmap --reason 192.168.56.20
```

এটি Nmap কেন কোনো port-কে নির্দিষ্ট state হিসেবে দেখছে তার indication দিতে পারে।

এটা বিশেষভাবে useful যখন তুমি Nmap output **interpret** করতে শিখছ।

---

# Lab 17 — Filtered বনাম Closed

এই তিনটি state ভালোভাবে বুঝো:

```text
OPEN
CLOSED
FILTERED
```

### Open

কোনো application/service connection গ্রহণ করছে।

### Closed

Host reachable, কিন্তু ওই port-এ service listening করছে না।

### Filtered

Firewall/filtering-এর কারণে Nmap নিশ্চিতভাবে বলতে পারছে না port open নাকি closed।

এটি Nmap শেখার সবচেয়ে গুরুত্বপূর্ণ concepts-এর একটি।

---

# 🔴 Level 4 — Professional-style lab workflow

এখন সব knowledge একসাথে ব্যবহার করো।

ধরো:

```text
Target = 192.168.56.20
```

### Step 1 — Host discovery

```bash
nmap -sn 192.168.56.20
```

### Step 2 — Basic TCP scan

```bash
nmap 192.168.56.20
```

### Step 3 — Full TCP ports

```bash
nmap -p- 192.168.56.20
```

### Step 4 — Service detection

ধরা যাক open ports পেলে:

```text
22,80,8080
```

তারপর:

```bash
nmap -sV -p 22,80,8080 192.168.56.20
```

### Step 5 — Default scripts

```bash
nmap -sC -sV -p 22,80,8080 192.168.56.20
```

### Step 6 — OS detection

```bash
sudo nmap -O 192.168.56.20
```

### Step 7 — Results save

```bash
nmap -sC -sV -p 22,80,8080 \
-oA target-assessment \
192.168.56.20
```

---

# 🧠 Final Assessment

এখন এই প্রশ্নগুলোর উত্তর নিজে বের করার চেষ্টা করো:

### Q1

```bash
nmap -sn 192.168.56.0/24
```

কী জানতে পারবে?

### Q2

```bash
nmap -p- 192.168.56.20
```

`-p-` কী বোঝায়?

### Q3

```bash
nmap -sV 192.168.56.20
```

`-sV` কেন ব্যবহার করব?

### Q4

```bash
sudo nmap -O 192.168.56.20
```

এটি কী ধরনের information দিতে পারে?

### Q5

```bash
nmap -sC -sV 192.168.56.20
```

এখানে `-sC` এবং `-sV`-এর কাজ আলাদা কীভাবে?

### Q6

একটি port যদি:

```text
filtered
```

দেখায়, তার অর্থ কী?

---

# 🏆 Course শেষে যে skillগুলো থাকা উচিত

```text
Nmap
│
├── Host Discovery
│   └── -sn
│
├── Port Scanning
│   ├── -p
│   ├── -p-
│   ├── -F
│   └── --top-ports
│
├── Service Enumeration
│   └── -sV
│
├── NSE
│   ├── -sC
│   └── --script
│
├── OS Detection
│   └── -O
│
├── UDP
│   └── -sU
│
├── Performance
│   └── -T
│
└── Reporting
    ├── -oN
    ├── -oX
    └── -oA
```

**পরের ধাপে চাইলে আমি তোমার জন্য একটি সম্পূর্ণ `Kali + Metasploitable 2` Nmap practice lab বানাতে পারি—প্রতিটি lab-এ target setup, exact command, expected output, এবং শেষে প্রশ্ন/quiz সহ।**


----
অবশ্যই। নিচে **Nmap-এর একটি complete practical tutorial** দিলাম—একদম beginner থেকে শুরু করে বাস্তব lab workflow পর্যন্ত। প্রতিটি command-এর **কী কাজ, কেন ব্যবহার করবে, example, output কীভাবে বুঝবে, এবং beginner-রা কোথায় ভুল করে**—সব একসাথে থাকবে।

> **Safety:** উদাহরণগুলো `127.0.0.1`, নিজের VM, বা অনুমোদিত lab target-এ চালাবে। Random public IP/domain scan করে practice করো না।

# Nmap Complete Practical Tutorial

## 0. Nmap আসলে কী?

**Nmap = Network Mapper**

এর সাহায্যে মূলত জানা যায়:

* কোন host online/reachable
* কোন TCP/UDP port open
* কোন service চলছে
* service-এর সম্ভাব্য version
* কিছু ক্ষেত্রে OS-এর সম্ভাব্য ধরন
* NSE script দিয়ে অতিরিক্ত service/network information
* scan result report হিসেবে save করা

একটি সাধারণ security/network assessment flow:

```text
Target
  ↓
Host Discovery
  ↓
Port Discovery
  ↓
Service Detection
  ↓
NSE Enumeration
  ↓
OS Detection
  ↓
Result Analysis
  ↓
Report
```

---

# 1. প্রথমে Nmap install/verify

Kali-তে:

```bash
nmap --version
```

তোমার version দেখাবে।

Help:

```bash
nmap -h
```

আরও বিস্তারিত manual:

```bash
man nmap
```

শুধু option খুঁজতে:

```bash
nmap --help
```

---

# 2. প্রথম Nmap scan

প্রথমে নিজের computer:

```bash
nmap 127.0.0.1
```

অথবা:

```bash
nmap localhost
```

একটি সাধারণ result:

```text
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
```

এখানে:

| অংশ    | অর্থ                                |
| ------ | ----------------------------------- |
| `22`   | port number                         |
| `tcp`  | protocol                            |
| `open` | service connection গ্রহণ করছে       |
| `ssh`  | Nmap যে service হিসেবে শনাক্ত করেছে |

### Beginner mistake #1

অনেকে মনে করে:

> `22 open` মানে machine-এ vulnerability আছে।

**ভুল।**

Open port শুধু বোঝায় সেখানে কোনো service listening করছে। Vulnerability আছে কি না সেটা আলাদা বিষয়।

---

# 3. নিজের IP এবং network বোঝা

Kali-তে:

```bash
ip addr
```

এবং:

```bash
ip route
```

ধরো তুমি দেখতে পেলে:

```text
192.168.56.10/24
```

তাহলে lab network হতে পারে:

```text
192.168.56.0/24
```

এখন নিজের authorized lab network-এ host discovery:

```bash
nmap -sn 192.168.56.0/24
```

---

# 4. `-sn` — Host Discovery

```bash
nmap -sn 192.168.56.0/24
```

এটি মূলত:

> "এই network-এ কোন host reachable?"

এটা জানতে ব্যবহৃত হয়।

উদাহরণ:

```text
Nmap scan report for 192.168.56.1
Host is up

Nmap scan report for 192.168.56.10
Host is up

Nmap scan report for 192.168.56.20
Host is up
```

তাহলে তুমি জানতে পারলে:

```text
192.168.56.1
192.168.56.10
192.168.56.20
```

reachable।

### Beginner mistake #2

```bash
nmap -sn target
```

দিয়ে যদি host না পাও, তার মানে **নিশ্চয়ই machine বন্ধ**—এটা ধরে নিও না।

Firewall বা filtering-এর কারণে discovery probe-এর response নাও আসতে পারে।

---

# 5. Basic Port Scan

এখন নিজের lab target:

```bash
nmap 192.168.56.20
```

ধরো output:

```text
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
```

তাহলে প্রথম ধারণা:

```text
22  → SSH
80  → HTTP
443 → HTTPS
```

কিন্তু মনে রাখবে, port number দেখে service নিশ্চিত করা যায় না।

---

# 6. Port State বুঝে নাও

Nmap-এ গুরুত্বপূর্ণ state:

### `open`

Service listening করছে।

```text
80/tcp open http
```

### `closed`

Host reachable, কিন্তু সেখানে ওই port-এ service listening করছে না।

```text
23/tcp closed telnet
```

### `filtered`

Firewall/filtering-এর কারণে Nmap নিশ্চিতভাবে বলতে পারছে না।

```text
25/tcp filtered smtp
```

এগুলো খুব গুরুত্বপূর্ণ।

---

# 7. নির্দিষ্ট Port Scan

শুধু SSH:

```bash
nmap -p 22 192.168.56.20
```

একাধিক:

```bash
nmap -p 22,80,443 192.168.56.20
```

Range:

```bash
nmap -p 1-1000 192.168.56.20
```

সব TCP port:

```bash
nmap -p- 192.168.56.20
```

### `-p-` কী?

এটি shorthand হিসেবে সব TCP port range scan করতে ব্যবহৃত হয়।

### Beginner mistake #3

```bash
nmap 192.168.56.20
```

চালিয়ে মনে করা:

> "আমি সব port scan করেছি।"

সাধারণ default scan **সব 65,535 TCP ports scan করে না**।

যদি সব TCP port দেখতে চাও:

```bash
nmap -p- 192.168.56.20
```

---

# 8. Fast Scan

```bash
nmap -F 192.168.56.20
```

`-F` কম সংখ্যক common ports scan করে।

তাই:

```bash
nmap target
```

এবং:

```bash
nmap -F target
```

এর result একই হওয়া বাধ্যতামূলক নয়।

---

# 9. Top Ports

যেমন:

```bash
nmap --top-ports 20 192.168.56.20
```

Top 100:

```bash
nmap --top-ports 100 192.168.56.20
```

এটি quick assessment-এ useful।

---

# 10. Service Version Detection — `-sV`

এখন সবচেয়ে গুরুত্বপূর্ণ command:

```bash
nmap -sV 192.168.56.20
```

ধরো:

```text
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.x
80/tcp   open  http    Apache httpd 2.x
```

এখন শুধু:

> "80 open"

জানার বদলে তুমি জানতে পারছ:

> "80-এ HTTP service আছে এবং Nmap একটি Apache version শনাক্ত করার চেষ্টা করেছে।"

### Beginner mistake #4

শুধু port number দেখে service ধরে নেওয়া।

যেমন:

```text
8080 = অবশ্যই HTTP
```

এটা নিশ্চিত নয়।

তাই:

```bash
nmap -sV target
```

দিয়ে verify করা ভালো।

---

# 11. `-sC` — Default NSE Scripts

```bash
nmap -sC 192.168.56.20
```

এটি Nmap-এর default NSE scripts চালায়।

আর service detection-এর সঙ্গে:

```bash
nmap -sC -sV 192.168.56.20
```

এটি খুব useful lab command।

---

# 12. NSE কী?

NSE:

**Nmap Scripting Engine**

Nmap-এর scripting system।

Script list দেখতে:

```bash
ls /usr/share/nmap/scripts/
```

কোনো script-এর help:

```bash
nmap --script-help=http-title
```

তারপর নিজের lab HTTP service:

```bash
nmap --script=http-title -p 80 192.168.56.20
```

### গুরুত্বপূর্ণ

সব NSE script একই ধরনের নয়। কিছু discovery/enumeration করে, কিছু configuration/security checks করতে পারে।

তাই আগে:

```bash
nmap --script-help=<script>
```

দেখে নেওয়া ভালো।

---

# 13. OS Detection — `-O`

নিজের lab target:

```bash
sudo nmap -O 192.168.56.20
```

Nmap network behavior দেখে OS সম্পর্কে অনুমান করার চেষ্টা করে।

### Beginner mistake #5

OS detection result-কে 100% নিশ্চিত ধরে নেওয়া।

Nmap-এর OS detection হলো **fingerprinting/guessing**, guarantee নয়।

---

# 14. `-A` কী?

```bash
sudo nmap -A 192.168.56.20
```

`-A` একসাথে বিভিন্ন advanced detection capability চালায়, যেমন:

```text
OS detection
Version detection
Default NSE scripts
Traceroute
```

তাই beginner হিসেবে প্রথম command হিসেবে `-A` না চালিয়ে আগে:

```bash
nmap target
nmap -sV target
nmap -sC -sV target
sudo nmap -O target
```

আলাদা আলাদা বুঝে নেওয়া ভালো।

---

# 15. TCP SYN Scan — `-sS`

```bash
sudo nmap -sS 192.168.56.20
```

এটি TCP SYN scanning technique।

সহজভাবে:

```text
Nmap ── SYN ──> Target

Target ── SYN/ACK ──> Nmap
       অথবা
Target ── RST ─────> Nmap
```

Nmap এই ধরনের responses ব্যবহার করে port state নির্ণয় করতে পারে।

---

# 16. TCP Connect Scan — `-sT`

```bash
nmap -sT 192.168.56.20
```

এটি normal TCP connection ব্যবহার করে।

অনেক ক্ষেত্রে raw packet privileges না থাকলে Nmap এই ধরনের scan ব্যবহার করতে পারে।

---

# 17. UDP Scan — `-sU`

TCP এবং UDP এক জিনিস নয়।

নিজের lab:

```bash
sudo nmap -sU --top-ports 20 192.168.56.20
```

নির্দিষ্ট UDP port:

```bash
sudo nmap -sU -p 53 192.168.56.20
```

### Beginner mistake #6

```bash
nmap target
```

দিয়ে মনে করা:

> "TCP এবং UDP দুটোই scan হয়ে গেছে।"

না।

UDP-এর জন্য:

```bash
-sU
```

ব্যবহার করতে হয়।

---

# 18. TCP + UDP

নিজের lab-এ:

```bash
sudo nmap -sS -sU --top-ports 100 192.168.56.20
```

এটি TCP এবং UDP—দুই ধরনের common ports সম্পর্কে information সংগ্রহ করতে পারে।

UDP scan সাধারণত TCP-এর তুলনায় ধীর হতে পারে।

---

# 19. `-n` — DNS Resolution বন্ধ

```bash
nmap -n 192.168.56.20
```

DNS lookup না করার কারণে কিছু পরিস্থিতিতে scan দ্রুত হতে পারে।

এটি particularly useful যখন reverse DNS resolution-এর দরকার নেই।

---

# 20. Verbose Mode

```bash
nmap -v 192.168.56.20
```

আরও verbose:

```bash
nmap -vv 192.168.56.20
```

এটি scan-এর progress এবং অতিরিক্ত details দেখতে সাহায্য করে।

---

# 21. `--reason`

```bash
nmap --reason 192.168.56.20
```

এতে port state-এর পেছনে Nmap কী ধরনের response পেয়েছে তার indication দেখতে পারো।

Beginnerদের জন্য output interpretation শেখার ক্ষেত্রে এটি খুব useful।

---

# 22. Timing

```bash
nmap -T3 192.168.56.20
```

আরও দ্রুত:

```bash
nmap -T4 192.168.56.20
```

Timing templates সাধারণভাবে:

```text
T0 → very slow
T1 → slow
T2 → polite
T3 → normal
T4 → aggressive/faster
T5 → very aggressive
```

### Beginner mistake #7

সবসময়:

```bash
-T5
```

ব্যবহার করা।

দ্রুত মানেই ভালো নয়। Network condition, IDS/firewall, reliability ইত্যাদি বিবেচনা করতে হয়।

Lab-এ সাধারণত `T3`/`T4` নিয়ে experiment করাই যথেষ্ট।

---

# 23. Scan Result Save

Normal output:

```bash
nmap -sV -oN scan.txt 192.168.56.20
```

তারপর:

```bash
cat scan.txt
```

XML:

```bash
nmap -sV -oX scan.xml 192.168.56.20
```

সব major format:

```bash
nmap -sV -oA labscan 192.168.56.20
```

এতে বিভিন্ন output file তৈরি হবে।

---

# 24. একটি Complete Lab Workflow

এখন ধরো:

```text
Kali      = 192.168.56.10
Target VM = 192.168.56.20
```

### Step 1 — Host discovery

```bash
nmap -sn 192.168.56.20
```

### Step 2 — Basic scan

```bash
nmap 192.168.56.20
```

### Step 3 — Full TCP ports

```bash
nmap -p- 192.168.56.20
```

ধরো পেলাম:

```text
22
80
443
8080
```

### Step 4 — Version detection

```bash
nmap -sV -p 22,80,443,8080 192.168.56.20
```

### Step 5 — Default scripts

```bash
nmap -sC -sV -p 22,80,443,8080 192.168.56.20
```

### Step 6 — OS detection

```bash
sudo nmap -O 192.168.56.20
```

### Step 7 — Save report

```bash
nmap -sC -sV \
-p 22,80,443,8080 \
-oA target-report \
192.168.56.20
```

এটাই একটি basic authorized network-enumeration workflow।

---

# 25. Output কীভাবে পড়বে?

ধরো:

```text
PORT     STATE    SERVICE  VERSION
22/tcp   open     ssh      OpenSSH 9.2
80/tcp   open     http     Apache httpd 2.4
443/tcp  closed   https
8080/tcp filtered http-proxy
```

তাহলে:

### 22

```text
open
ssh
```

SSH service reachable।

### 80

```text
open
http
Apache
```

HTTP service শনাক্ত হয়েছে।

### 443

```text
closed
```

Host reachable হলেও সেখানে ওই port-এ service listening করছে না।

### 8080

```text
filtered
```

Network filtering-এর কারণে Nmap নিশ্চিতভাবে state নির্ধারণ করতে পারছে না।

---

# 26. Beginner-এর সবচেয়ে common mistakes

## Mistake 1 — Permission ছাড়া scanning

এটা করো না:

```bash
nmap random-public-ip
```

Practice করার জন্য:

```text
127.0.0.1
নিজের VM
নিজের lab network
অনুমোদিত test environment
```

ব্যবহার করো।

---

## Mistake 2 — Open port = vulnerability

ভুল:

```text
80 open
↓
Vulnerable!
```

সঠিক:

```text
80 open
↓
HTTP service identified
↓
Service/version/configuration investigate
↓
তারপর security assessment
```

---

## Mistake 3 — Default scan = সব port

ভুল:

```bash
nmap target
```

মানে সব 65,535 TCP port নয়।

Full TCP:

```bash
nmap -p- target
```

---

## Mistake 4 — TCP/UDP গুলিয়ে ফেলা

TCP:

```bash
nmap target
```

UDP:

```bash
sudo nmap -sU target
```

দুটো আলাদা protocol।

---

## Mistake 5 — `-A` সব সমস্যার সমাধান মনে করা

```bash
nmap -A target
```

অনেক information দেয়, কিন্তু এটা কোনো magic vulnerability scanner নয়।

---

## Mistake 6 — Version দেখে vulnerability নিশ্চিত করা

ধরো:

```text
Apache 2.4.x
```

শুধু version দেখে vulnerability আছে বলে সিদ্ধান্ত নিও না।

Version identification-এর পরে proper validation দরকার।

---

## Mistake 7 — `filtered` মানে closed ধরে নেওয়া

না।

```text
closed ≠ filtered
```

`filtered` সাধারণত filtering/firewall-এর কারণে uncertainty বোঝায়।

---

## Mistake 8 — খুব aggressive timing

```bash
-T5
```

সব সময় দরকার নেই।

প্রথমে:

```bash
-T3
```

বা lab-এ:

```bash
-T4
```

নিয়ে কাজ শেখো।

---

# 27. Beginner থেকে Advanced যাওয়ার Practice Order

এই order-এ practice করলে ভালো হবে:

```text
1. nmap localhost
        ↓
2. nmap -sn LAB_NETWORK
        ↓
3. nmap TARGET
        ↓
4. nmap -p 22,80,443 TARGET
        ↓
5. nmap -p- TARGET
        ↓
6. nmap -sV TARGET
        ↓
7. nmap -sC -sV TARGET
        ↓
8. sudo nmap -O TARGET
        ↓
9. sudo nmap -sU TARGET
        ↓
10. NSE scripts
        ↓
11. Timing
        ↓
12. Output/reporting
        ↓
13. Complete assessment workflow
```

# 🧪 Final Challenge

নিজের lab target-এর জন্য এই sequence চালাও:

```bash
nmap -sn TARGET
```

```bash
nmap TARGET
```

```bash
nmap -p- TARGET
```

```bash
nmap -sV TARGET
```

```bash
nmap -sC -sV TARGET
```

```bash
sudo nmap -O TARGET
```

তারপর একটি report বানাও:

```text
Target:
Host status:

Open TCP ports:
- Port:
- Service:
- Version:

Open UDP ports:
- Port:
- Service:

OS guess:

Interesting findings:

Questions/uncertainties:
```

**সবচেয়ে গুরুত্বপূর্ণ skill হলো command মুখস্থ করা নয়—Nmap-এর output থেকে `host → port → service → version → evidence → conclusion` এই chain তৈরি করতে শেখা।**

For your Nmap practice

* Show how to read Nmap output as evidence
* Explain why full TCP scans can miss UDP services


---
Exactly. The key is to treat Nmap as **evidence collection**, not as a vulnerability verdict.

## 1. Start with the observation

Suppose Nmap returns:

```text
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.2
80/tcp   open  http    Apache httpd 2.4.57
443/tcp  closed https
```

Don't immediately write:

> "The server is vulnerable."

Instead separate **what Nmap observed** from **what you infer**.

### Observation

> TCP port 22 was reported open, and Nmap identified an SSH service with a reported version of OpenSSH 9.2.

That's a defensible statement.

### Not justified yet

> "OpenSSH 9.2 is vulnerable."

The Nmap result alone doesn't establish that.

---

# 2. Use the Evidence → Interpretation → Conclusion model

A useful workflow is:

```text
Nmap output
    ↓
What exactly was observed?
    ↓
What does that observation reasonably indicate?
    ↓
What remains unknown?
    ↓
What additional evidence is needed?
    ↓
Careful conclusion
```

For example:

| Nmap evidence  | Reasonable interpretation                              | Not established                               |
| -------------- | ------------------------------------------------------ | --------------------------------------------- |
| `22/tcp open`  | Something is accepting TCP connections on 22           | That SSH is vulnerable                        |
| `80/tcp open`  | An HTTP service appears reachable                      | The web application is vulnerable             |
| `OpenSSH 9.2`  | Nmap identified/reported an SSH implementation/version | That the version is exploitable               |
| `Apache 2.4.x` | Nmap fingerprinted an Apache HTTP service              | That Apache itself has a usable vulnerability |
| `filtered`     | Filtering prevented a definitive determination         | That the port is closed                       |
| OS fingerprint | Nmap's fingerprint suggests an OS                      | That the identification is certain            |

---

# 3. Example: Open port

Suppose:

```bash
nmap 192.168.56.20
```

returns:

```text
22/tcp open ssh
```

### Bad conclusion

> "SSH vulnerability found."

### Careful conclusion

> "TCP/22 is reachable and Nmap reports an SSH service. This establishes service exposure, but does not by itself establish a vulnerability."

That's the distinction you want to develop.

---

# 4. Example: Version detection

Now:

```bash
nmap -sV 192.168.56.20
```

returns:

```text
22/tcp open ssh OpenSSH 9.2
```

### Bad reasoning

```text
OpenSSH 9.2
      ↓
Old version
      ↓
Vulnerable
```

There are several unsupported assumptions there.

### Better reasoning

```text
Nmap reports OpenSSH 9.2
        ↓
Confirm the service/version independently if important
        ↓
Determine the exact product/build/package
        ↓
Check applicable security advisories
        ↓
Determine whether the affected condition actually applies
        ↓
Only then assess vulnerability
```

A reported version is a **clue**, not proof.

---

# 5. Example: HTTP

Suppose:

```bash
nmap -sV -p 80 192.168.56.20
```

returns:

```text
80/tcp open http Apache httpd 2.4.57
```

You can safely conclude:

> "An HTTP service is reachable on TCP/80, and Nmap identifies it as Apache HTTP Server 2.4.57."

You **cannot** conclude from that alone:

> "The website is vulnerable."

Why?

Because application security can depend on things such as:

* configuration
* enabled modules
* application code
* authentication
* deployment architecture
* operating-system packages/backports
* patches
* request handling
* actual exposure of the affected component

---

# 6. Version numbers need context

One particularly important beginner mistake is assuming:

```text
Detected version = exact installed software state
```

Nmap performs **service fingerprinting**. Its result can be incomplete or inaccurate.

Also, package maintainers may backport security fixes without changing the upstream-looking version in the way you might expect.

So instead of:

> "Version X means vulnerable."

use:

> "Nmap reports version X. The applicability of any vulnerability associated with that product/version needs to be verified against the actual package/build, configuration, and relevant security advisory."

---

# 7. NSE results need the same discipline

Suppose:

```bash
nmap -sC -sV 192.168.56.20
```

produces some interesting NSE output.

Don't automatically translate:

```text
NSE finding
↓
confirmed vulnerability
```

Instead ask:

1. What exactly did the script test?
2. What evidence did it obtain?
3. Is the result informational, a configuration finding, or an actual vulnerability indication?
4. Does the script have limitations or false-positive possibilities?
5. Can the finding be independently validated?

---

# 8. `filtered` is also evidence

Suppose:

```text
8080/tcp filtered
```

A beginner might say:

> "Port 8080 is closed."

That's incorrect.

A better conclusion:

> "Nmap could not determine whether TCP/8080 is open because filtering prevented a definitive response."

The distinction:

```text
closed
  ↓
Nmap has evidence that the port is not accepting connections

filtered
  ↓
Nmap cannot determine the state because filtering interferes
```

---

# 9. OS detection is an estimate

Suppose:

```bash
sudo nmap -O 192.168.56.20
```

reports a Linux fingerprint.

Don't write:

> "The target definitely runs Linux."

Write:

> "Nmap's OS fingerprint is consistent with Linux."

The word **consistent** is useful because it accurately reflects the nature of fingerprinting.

---

# 10. Build a confidence hierarchy

When writing an assessment, distinguish between:

### Direct observation

> TCP/22 responded as an open port.

**High confidence** in what Nmap directly observed.

### Tool identification

> Nmap identified OpenSSH 9.2.

**Moderate confidence**, because fingerprinting has limitations.

### Interpretation

> The host exposes an SSH service.

A reasonable interpretation of the evidence.

### Security hypothesis

> The service may warrant review for known vulnerabilities or configuration weaknesses.

Reasonable, but not a vulnerability finding.

### Confirmed vulnerability

> A specific vulnerability is present and the affected condition has been independently verified.

This requires **additional evidence** beyond simply seeing an open port.

---

# 11. A practical report format

Instead of writing:

```text
Port 80 is vulnerable.
```

write:

```text
Finding: HTTP service exposed

Evidence:
Nmap reported TCP/80 as open and identified an HTTP service.

Interpretation:
An HTTP service is reachable from the scanning host.

Security significance:
The service expands the externally/reachable attack surface and
should be reviewed according to the intended network exposure.

Limitation:
The Nmap result alone does not establish a vulnerability.

Next validation:
Confirm the deployed software/package version and review applicable
security advisories and configuration.
```

That's much stronger technically because every claim is tied to evidence.

---

# 12. A complete example

Imagine your scan gives:

```text
PORT     STATE    SERVICE VERSION
22/tcp   open     ssh     OpenSSH 9.2
80/tcp   open     http    Apache httpd 2.4.57
443/tcp  filtered https
3306/tcp open     mysql   MySQL 8.0.x
```

### Weak report

> The server has SSH, Apache and MySQL vulnerabilities.

There is **not enough evidence** for that conclusion.

### Better report

> Nmap identified four notable TCP states. TCP/22 is reported open with an SSH service identified as OpenSSH 9.2. TCP/80 is reported open with Apache HTTP Server 2.4.57. TCP/3306 is reported open with a MySQL service identified as 8.0.x. TCP/443 is reported as filtered, so its state could not be definitively determined by this scan. These results establish reachable services and provide candidates for further assessment; they do not, by themselves, establish the presence of vulnerabilities.

That's a professional conclusion.

---

# 13. The golden rule

Whenever you see an Nmap result, ask:

> **"What does this prove, and what does it merely suggest?"**

For example:

```text
OPEN PORT
   │
   ├── Proves/strongly indicates:
   │      A service is reachable
   │
   └── Does NOT prove:
          Vulnerability
          Exploitability
          Compromise
          Weak authentication
          Outdated patch status
```

And:

```text
VERSION DETECTED
   │
   ├── Indicates:
   │      Nmap fingerprinted a probable product/version
   │
   └── Does NOT prove:
          Vulnerability
          Applicable CVE
          Exploitability
          Missing patch
```

## A useful sentence template

For almost any Nmap finding, you can use:

> **"Nmap observed X. This indicates Y. However, the scan alone does not establish Z. Additional validation of A and B would be required to determine Z."**

That single pattern will prevent a lot of overclaiming in security reports.

For your Nmap reports

* Compare scan evidence types
* Separate exposure from exploitability



---
হ্যাঁ, **তোমার নিজের mobile আর PC ব্যবহার করে Nmap practice করা যাবে**—এটা beginner lab হিসেবে ভালো setup। শুধু দুটো device যেন **একই local network/Wi-Fi-তে থাকে** এবং দুটোই তোমার নিজের/অনুমোদিত device হয়।

### সহজ setup

```text
        একই Wi-Fi
           │
    ┌──────┴──────┐
    │             │
  Kali PC       Mobile
  Scanner       Target
```

### 1. Mobile-এর local IP বের করো

Android হলে সাধারণত:

**Settings → Wi-Fi → Connected network → IP address**

ধরো mobile-এর IP:

```text
192.168.1.25
```

PC/Kali থেকে প্রথমে connectivity পরীক্ষা:

```bash
ping 192.168.1.25
```

তারপর basic scan:

```bash
nmap 192.168.1.25
```

আর service detection:

```bash
nmap -sV 192.168.1.25
```

### 2. Mobile-এ একটি test service চালানো

Mobile-এ যদি তোমার নিজের কোনো HTTP server/app থাকে এবং সেটি LAN থেকে connections গ্রহণ করে, তাহলে তার port Nmap দিয়ে দেখা যায়।

উদাহরণস্বরূপ, mobile-এ কোনো test web server যদি `8080` port-এ চলে:

```bash
nmap -p 8080 192.168.1.25
```

তারপর:

```bash
nmap -sV -p 8080 192.168.1.25
```

এতে তুমি খুব সুন্দরভাবে শিখতে পারবে:

```text
IP
 ↓
Port
 ↓
Open/closed/filtered
 ↓
Service detection
 ↓
Nmap result interpretation
```

### ⚠️ একটি গুরুত্বপূর্ণ ব্যাপার

Mobile-এ কোনো port open না পেলেও সেটা সমস্যা নয়। Android/iOS সাধারণত অনেক incoming connection block করে, এবং mobile carrier/Wi-Fi isolation-ও থাকতে পারে।

আর **mobile data/Internet IP scan করার দরকার নেই**—নিজের Wi-Fi LAN-এর private IP ব্যবহার করো।

তোমার যদি **Kali PC + Android mobile** থাকে, আমি চাইলে একদম **`Kali → Android` ৩০ মিনিটের practical Nmap lab** দিতে পারি—mobile-এ কী install করবে, কোন test server চালাবে, কোন `nmap` command দেবে, এবং প্রতিটি output কীভাবে বুঝবে।

For your mobile-to-PC lab

* Set up a safe test service
* Check why no ports appear


-----
অবশ্যই। নিচে **Kali Linux PC → নিজের Android Mobile** ধরে একটি সম্পূর্ণ beginner-friendly Nmap practical lab দিলাম। সবগুলো ধাপ নিজের ফোন ও নিজের LAN/Wi-Fi-তে করো।

## 🧪 Lab Topology

```text
        Same Wi-Fi / LAN
┌───────────────────────────────┐
│                               │
│ Kali Linux PC                 │
│ Scanner                       │
│ 192.168.1.10                  │
│                               │
│          ↕                    │
│                               │
│ Android Phone                 │
│ Target                        │
│ 192.168.1.25                  │
│                               │
└───────────────────────────────┘
```

---

# Part 1 — Android-এর IP বের করো

Android-এ:

**Settings → Wi-Fi → Connected Network → Network details**

এখানে `IP address` দেখবে।

ধরা যাক:

```text
Android IP = 192.168.1.25
```

Kali-তে নিজের IP দেখতে:

```bash
ip addr
```

অথবা:

```bash
ip route
```

---

# Part 2 — Connectivity Test

প্রথমে Kali থেকে Android-কে ping করো:

```bash
ping -c 4 192.168.1.25
```

যদি এমন response পাও:

```text
64 bytes from 192.168.1.25
64 bytes from 192.168.1.25
```

তাহলে basic network connectivity আছে।

যদি ping না আসে, **তার মানে ফোন offline—এমনটা নিশ্চিত নয়**। Android বা Wi-Fi network ICMP/ping block করতে পারে।

---

# Part 3 — প্রথম Nmap Scan

```bash
nmap 192.168.1.25
```

Possible output:

```text
PORT     STATE    SERVICE
...
```

অনেক Android ফোনে এখানে **কোনো open port নাও দেখা যেতে পারে**। এটা স্বাভাবিক।

### মনে রাখবে

```text
open     → ওই port-এ reachable service থাকার evidence
closed   → host reachable, কিন্তু ওই port-এ service listening নেই
filtered → firewall/filtering-এর কারণে Nmap নিশ্চিত হতে পারছে না
```

**Open port = vulnerability নয়।**

---

# Part 4 — Specific Ports Scan

উদাহরণ:

```bash
nmap -p 80,443,8080 192.168.1.25
```

অথবা port range:

```bash
nmap -p 1-1000 192.168.1.25
```

সব TCP ports:

```bash
nmap -p- 192.168.1.25
```

⚠️ `-p-` অনেক বেশি ports পরীক্ষা করে, তাই lab-এ শেখার জন্য ঠিক আছে কিন্তু unnecessary scans এড়ানো ভালো।

---

# Part 5 — Service Detection

যদি কোনো open port পাও:

```bash
nmap -sV 192.168.1.25
```

Specific port:

```bash
nmap -sV -p 8080 192.168.1.25
```

ধরা যাক:

```text
8080/tcp open  http
```

তাহলে conclusion হবে:

> Nmap observed TCP/8080 as open and identified an HTTP service.

কিন্তু **এটা বলা যাবে না**:

> “8080 vulnerable.”

কারণ vulnerability প্রমাণ করার জন্য আরও evidence দরকার।

---

# Part 6 — Android-এ একটি Test Server চালানো

এটা lab-টাকে অনেক বেশি interesting করবে।

Android-এ একটি terminal environment যেমন **Termux** ব্যবহার করে নিজের test directory বানাতে পারো।

ধরা যাক test file:

```text
hello.html
```

তারপর একটি local HTTP server চালানো যায়:

```bash
python -m http.server 8080
```

এখন Android-এর IP যদি হয়:

```text
192.168.1.25
```

তাহলে Kali থেকে:

```bash
nmap -p 8080 192.168.1.25
```

Expected:

```text
PORT     STATE SERVICE
8080/tcp open  http-proxy
```

Service detection:

```bash
nmap -sV -p 8080 192.168.1.25
```

---

# Part 7 — Browser দিয়ে Verify

Kali browser থেকে:

```text
http://192.168.1.25:8080
```

যদি Android-এর directory listing/test page আসে, তাহলে তোমার evidence chain অনেক পরিষ্কার:

```text
Nmap
 ↓
8080/tcp open
 ↓
HTTP service detected
 ↓
Browser connection successful
 ↓
Test server confirmed
```

এখানে Nmap-এর result independently verify করা হলো।

---

# Part 8 — `-sC`

নিজের lab target-এ:

```bash
nmap -sC -p 8080 192.168.1.25
```

এটা default NSE scripts ব্যবহার করে কিছু additional information সংগ্রহ করবে।

Service + default scripts:

```bash
nmap -sC -sV -p 8080 192.168.1.25
```

---

# Part 9 — OS Detection

নিজের lab-এ চেষ্টা করতে পারো:

```bash
sudo nmap -O 192.168.1.25
```

কখনো output আসতে পারে:

```text
OS details: Android ...
```

কিন্তু এটাকে absolute fact হিসেবে লিখবে না।

Professional wording:

> Nmap fingerprinting suggests an Android/Linux-based operating environment.

না যে:

> “The phone definitely runs Android version X.”

---

# Part 10 — Aggressive Detection

Lab-এ:

```bash
sudo nmap -A -p 8080 192.168.1.25
```

`-A` একসাথে several detection techniques চালায়, যেমন service/version detection, OS-related detection এবং NSE-based enumeration।

শেখার জন্য useful, কিন্তু বাস্তব network-এ blindly ব্যবহার করা উচিত নয়।

---

# Part 11 — UDP Scan

TCP আর UDP আলাদা।

নিজের Android lab-এ:

```bash
sudo nmap -sU --top-ports 20 192.168.1.25
```

একটি নির্দিষ্ট UDP port:

```bash
sudo nmap -sU -p 5353 192.168.1.25
```

UDP result interpretation একটু আলাদা:

```text
open
closed
open|filtered
```

`open|filtered` মানে Nmap নিশ্চিতভাবে বলতে পারছে না port open নাকি filtering হচ্ছে।

---

# Part 12 — Host Discovery

একই Wi-Fi network-এ নিজের devices খুঁজে দেখতে:

```bash
nmap -sn 192.168.1.0/24
```

তোমার network যদি অন্য subnet হয়, সেটা ব্যবহার করবে।

যেমন:

```text
192.168.1.0/24
```

মানে roughly:

```text
192.168.1.1
192.168.1.2
...
192.168.1.254
```

এর মধ্যে কোন hosts responding করছে তা দেখা যাবে।

---

# Part 13 — শুধু Android Target

ধরা যাক Android:

```text
192.168.1.25
```

একটি ছোট practical workflow:

```bash
ping -c 4 192.168.1.25
```

তারপর:

```bash
nmap 192.168.1.25
```

তারপর:

```bash
nmap -sV 192.168.1.25
```

তারপর যদি 8080 open থাকে:

```bash
nmap -sC -sV -p 8080 192.168.1.25
```

আরও information:

```bash
sudo nmap -O 192.168.1.25
```

শেষে combined lab scan:

```bash
sudo nmap -A -p 8080 192.168.1.25
```

---

# Part 14 — Result কীভাবে লিখবে

ধরা যাক result:

```text
8080/tcp open http
```

### ❌ ভুল conclusion

> Android-এর 8080 port vulnerable.

### ✅ ভালো conclusion

> Nmap identified TCP/8080 as open and detected an HTTP service. This confirms that an HTTP service was reachable from the Kali host. The scan alone does not establish that the service is vulnerable. Further validation of the application, configuration, authentication controls, and applicable software versions would be required.

---

# Part 15 — Evidence Table

প্রতিটি scan-এর result এভাবে লিখতে পারো:

| Evidence                  | Interpretation                             | What it does NOT prove        |
| ------------------------- | ------------------------------------------ | ----------------------------- |
| `80/tcp open`             | HTTP-related service reachable             | Vulnerability                 |
| `8080/tcp open`           | Service reachable on 8080                  | RCE/exploitability            |
| `-sV` identifies software | Nmap fingerprint suggests software/version | That version is vulnerable    |
| `-O` suggests Android     | OS fingerprint suggests Android            | 100% OS certainty             |
| `filtered`                | Filtering prevents determination           | Port is definitely closed     |
| NSE reports information   | Script observed a condition                | Automatic vulnerability proof |

---

# 🎯 Final 30-Minute Challenge

এখন পুরো lab নিজে করো।

### Task 1

Android IP বের করো।

```bash
ip route
```

তারপর:

```bash
ping -c 4 ANDROID_IP
```

### Task 2

Basic scan:

```bash
nmap ANDROID_IP
```

### Task 3

Top ports:

```bash
nmap --top-ports 100 ANDROID_IP
```

### Task 4

Service detection:

```bash
nmap -sV ANDROID_IP
```

### Task 5

Android-এ নিজের test HTTP server চালাও:

```bash
python -m http.server 8080
```

তারপর Kali:

```bash
nmap -sV -p 8080 ANDROID_IP
```

### Task 6

Verify:

```text
http://ANDROID_IP:8080
```

### Task 7

NSE:

```bash
nmap -sC -sV -p 8080 ANDROID_IP
```

### Task 8

OS fingerprint:

```bash
sudo nmap -O ANDROID_IP
```

### Task 9

Final lab scan:

```bash
sudo nmap -A -p 8080 ANDROID_IP
```

---

## 🧠 তোমার শেখার মূল flow

```text
Android
   ↓
IP address
   ↓
Host discovery
   ↓
Port discovery
   ↓
Port state
   ↓
Service detection
   ↓
Version/fingerprint
   ↓
Manual verification
   ↓
Evidence
   ↓
Careful conclusion
```

সবচেয়ে গুরুত্বপূর্ণ rule:

> **Nmap যা observe করেছে সেটা আলাদা, আর তুমি তার security meaning হিসেবে যা conclude করছ সেটা আলাদা।**

এই Android + Kali setup দিয়ে তুমি **Beginner → Intermediate Nmap** শেখার জন্য যথেষ্ট বাস্তব hands-on practice করতে পারবে।

For your Kali–Android lab

* Add a second practice service
* Troubleshoot missing open ports



---
হ্যাঁ। একই Android ফোনে **দুটি harmless local test service** চালিয়ে Kali থেকে পাশাপাশি scan করলে Nmap-এর result comparison খুব ভালোভাবে শেখা যাবে।

ধরি:

```text
Android IP = 192.168.1.25
Service 1  = HTTP on TCP/8080
Service 2  = HTTP on TCP/8000
```

## 1. Android-এ প্রথম service

প্রথম terminal session-এ:

```bash
mkdir -p ~/nmap-lab/service1
cd ~/nmap-lab/service1
echo "This is test service 1" > index.html
python -m http.server 8080
```

এটি `8080/tcp`-এ একটি harmless HTTP server চালাবে।

Kali থেকে test:

```bash
nmap -p 8080 192.168.1.25
```

তারপর:

```bash
nmap -sV -p 8080 192.168.1.25
```

---

## 2. Android-এ দ্বিতীয় service

**নতুন terminal session** খুলে:

```bash
mkdir -p ~/nmap-lab/service2
cd ~/nmap-lab/service2
echo "This is test service 2" > index.html
python -m http.server 8000
```

এখন Android-এ দুটি service চলছে:

```text
TCP/8080 → HTTP test service 1
TCP/8000 → HTTP test service 2
```

দুটি server-ই চালু রাখতে হবে।

---

## 3. Kali থেকে দুটো একসাথে scan

```bash
nmap -p 8000,8080 192.168.1.25
```

সম্ভাব্য output:

```text
PORT     STATE SERVICE
8000/tcp open  http-alt
8080/tcp open  http-proxy
```

এখানে গুরুত্বপূর্ণ বিষয়:

**Nmap-এর `SERVICE` column হলো port-number/service fingerprint-এর interpretation; এটাকে application-এর security verdict হিসেবে দেখবে না।**

---

## 4. Version detection দিয়ে compare

```bash
nmap -sV -p 8000,8080 192.168.1.25
```

সম্ভাব্যভাবে Python HTTP server সম্পর্কিত information দেখতে পারো।

তখন comparison:

| Port      | Nmap observation       | Interpretation                      |
| --------- | ---------------------- | ----------------------------------- |
| 8000/tcp  | `open`                 | একটি reachable service আছে          |
| 8080/tcp  | `open`                 | একটি reachable service আছে          |
| 8000/8080 | HTTP-related detection | Nmap HTTP service fingerprint করেছে |

এখানে **কোনোটাকেই vulnerability বলা হচ্ছে না**।

---

## 5. আলাদাভাবে verify করো

Kali browser থেকে:

```text
http://192.168.1.25:8000
```

এবং:

```text
http://192.168.1.25:8080
```

অথবা Kali terminal থেকে:

```bash
curl http://192.168.1.25:8000
```

```bash
curl http://192.168.1.25:8080
```

তাহলে তোমার evidence chain হবে:

```text
Nmap
 ↓
8000/tcp open
 ↓
HTTP detected
 ↓
curl/browser connection succeeds
 ↓
Test service confirmed
```

এবং একইভাবে `8080`-এর জন্য।

---

## 6. NSE দিয়েও compare

নিজের lab target-এ:

```bash
nmap -sC -sV -p 8000,8080 192.168.1.25
```

এতে Nmap আরও information সংগ্রহ করার চেষ্টা করবে।

তবে এখানেও rule একই:

> **NSE output-ও evidence; automatic vulnerability verdict নয়।**

---

## 7. Professional conclusion লিখে practice করো

ধরা যাক তোমার actual result:

```text
8000/tcp open http
8080/tcp open http
```

### ❌ এভাবে লিখবে না

> Android-এর দুইটা vulnerable service আছে।

### ✅ এভাবে লিখবে

> Nmap identified TCP ports 8000 and 8080 as open and detected HTTP services on both ports. Manual HTTP requests to both ports successfully reached the corresponding test servers. These observations confirm that two HTTP services are reachable from the Kali host. The scan does not, by itself, establish that either service contains a vulnerability.

---

## 8. সবচেয়ে useful comparison

একই machine-এ service দুটো intentionally একই ধরনের হওয়ায় তুমি বুঝতে পারবে:

```text
Port
 ↓
State
 ↓
Service fingerprint
 ↓
Version information
 ↓
Manual verification
 ↓
Security interpretation
```

**Port 8000 open** এবং **port 8080 open**—দুটোর security meaning একই নয় শুধু port number আলাদা বলে; actual application/configuration কী, সেটাই গুরুত্বপূর্ণ।

### ছোট challenge

এখন এই তিনটি command-এর output compare করো:

```bash
nmap -p 8000,8080 192.168.1.25
```

```bash
nmap -sV -p 8000,8080 192.168.1.25
```

```bash
nmap -sC -sV -p 8000,8080 192.168.1.25
```

তারপর প্রতিটি output-এর জন্য আলাদা করে লিখবে:

**Evidence → Interpretation → What is still unknown → Conclusion**

এটাই Nmap result থেকে **careful security assessment** লেখার সবচেয়ে গুরুত্বপূর্ণ অভ্যাস।

For your Kali–Android lab

* Save and diff scan results
* Compare one service with a closed port


---
অবশ্যই। নিজের Android target `192.168.1.25` ধরে আমরা **8000 ও 8080** scan-এর result Kali-তে **normal text** এবং **XML**—দুই format-এ save করব, তারপর শুধু observable change compare করব।

## 1. Normal output save

দুই port একসাথে:

```bash
nmap -sV -p 8000,8080 192.168.1.25 -oN android-services.txt
```

ফাইল দেখো:

```bash
cat android-services.txt
```

আরও সহজে:

```bash
less android-services.txt
```

---

## 2. XML output save

```bash
nmap -sV -p 8000,8080 192.168.1.25 -oX android-services.xml
```

দেখতে:

```bash
less android-services.xml
```

XML সাধারণত machine-readable structured data রাখে—যেমন host, port, state, service ইত্যাদি।

---

## 3. একই scan-এর দুই format রাখা

তুমি চাইলে `-oA` দিয়ে একবারেই তিন ধরনের output তৈরি করতে পারো:

```bash
nmap -sV -p 8000,8080 192.168.1.25 -oA android-services
```

এতে সাধারণত:

```text
android-services.nmap
android-services.xml
android-services.gnmap
```

তৈরি হবে।

তোমার প্রশ্নের জন্য মূল দুটো হলো:

```text
android-services.nmap
android-services.xml
```

---

# 4. Observable result compare

ধরো প্রথম scan-এর output:

```text
PORT     STATE SERVICE VERSION
8000/tcp open  http    Python ...
8080/tcp open  http    Python ...
```

এখন দুই format-এর content **একই scan-এর representation**—normal output human-readable, XML structured।

তাই comparison-এর সময় খেয়াল করবে:

```text
Port
State
Protocol
Service
Version/fingerprint reported by Nmap
```

---

# 5. পরে service পরিবর্তন করে আবার scan

ধরো তুমি Android-এর `8000` service বন্ধ করলে কিন্তু `8080` চালু রাখলে।

তারপর নতুন scan:

```bash
nmap -sV -p 8000,8080 192.168.1.25 -oN android-services-after.txt
```

এবং:

```bash
nmap -sV -p 8000,8080 192.168.1.25 -oX android-services-after.xml
```

এখন normal outputs-এর difference দেখতে:

```bash
diff -u android-services.txt android-services-after.txt
```

যদি `8000` বন্ধ হয়ে যায়, observable change হতে পারে:

```diff
-8000/tcp open  http
+8000/tcp closed
```

অন্যদিকে `8080` unchanged থাকলে তার corresponding line unchanged থাকবে।

---

## 6. XML comparison

XML সরাসরি `diff` করা যায়:

```bash
diff -u android-services.xml android-services-after.xml
```

তবে XML-এর formatting/metadata-এর কারণে raw diff অনেক noisy হতে পারে।

তাই শেখার সময় **normal output দিয়ে human comparison** এবং **XML দিয়ে structured record রাখা**—এই workflow-টা বেশি পরিষ্কার।

---

# 7. Comparison table বানাও

ধরা যাক first scan:

| Port | Before | After  | Observable change        |
| ---- | ------ | ------ | ------------------------ |
| 8000 | open   | closed | Port state changed       |
| 8080 | open   | open   | No observed state change |

এখানে conclusion হবে:

> The scan results show that TCP/8000 changed from `open` to `closed`, while TCP/8080 remained `open`. These are observable changes in Nmap's scan results. The scans alone do not establish why the change occurred or whether either service is vulnerable.

এটাই গুরুত্বপূর্ণ distinction:

**Observed:** `open → closed`
**Not established:** *why* it changed, or whether anything is vulnerable.

---

## 8. Lab-এর জন্য clean directory

সব scan আলাদা করে রাখতে পারো:

```bash
mkdir -p ~/nmap-lab/scans
cd ~/nmap-lab/scans
```

Before:

```bash
nmap -sV -p 8000,8080 192.168.1.25 \
  -oN before.nmap \
  -oX before.xml
```

After:

```bash
nmap -sV -p 8000,8080 192.168.1.25 \
  -oN after.nmap \
  -oX after.xml
```

তারপর:

```bash
diff -u before.nmap after.nmap
```

এতে তোমার lab-এ একটি পরিষ্কার **Before → Change → After** Nmap record তৈরি হবে।

For your Kali–Android scan comparison

* Record scan timing changes
* Compare XML fields directly


---
