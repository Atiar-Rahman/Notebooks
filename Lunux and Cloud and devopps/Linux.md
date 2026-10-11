
### 🐧 Linux শেখার Roadmap

**Level 1 — Basic**

1. Linux কী এবং কেন ব্যবহার করা হয়
2. Linux distribution কী — Ubuntu, Debian, Fedora ইত্যাদি
3. Linux install ও Virtual Machine
4. File system structure
5. Terminal ও Shell
6. Basic commands:

   * `pwd`
   * `ls`
   * `cd`
   * `mkdir`
   * `touch`
   * `cp`
   * `mv`
   * `rm`
   * `cat`
   * `less`

**Level 2 — Command Line**

* `grep`
* `find`
* `sort`
* `cut`
* `head`
* `tail`
* pipes `|`
* redirection `>`, `>>`, `<`
* wildcards `*`, `?`

**Level 3 — Users & Permissions**

* User এবং Group
* `sudo`
* `chmod`
* `chown`
* `chgrp`
* Read/Write/Execute permissions
* `rwx` এবং permission numbers যেমন `755`, `644`

**Level 4 — Software Management**

* Package কী
* `apt`
* `dnf`
* `pacman`
* Software install/update/remove
* Repository কী

**Level 5 — Processes & System**

* Process কী
* `ps`
* `top`
* `htop`
* `kill`
* `systemctl`
* Services
* Boot process
* Logs

**Level 6 — Networking**

* IP address
* DNS
* Ports
* TCP/UDP
* `ping`
* `ip`
* `ss`
* `curl`
* `wget`
* SSH

**Level 7 — Bash Scripting**

* Variables
* Conditions
* Loops
* Functions
* Arguments
* Shell scripts
* Automation

**Level 8 — Storage**

* Disk ও partition
* Filesystem
* `df`
* `du`
* `mount`
* `umount`
* `lsblk`
* `/etc/fstab`

**Level 9 — Advanced Linux**

* Kernel
* Environment variables
* Cron jobs
* System logs
* Firewall
* SELinux/AppArmor
* Docker
* Virtualization

**Level 10 — Linux Administration**

* Server management
* SSH administration
* Web server
* Database
* Backup
* Monitoring
* Security
* Troubleshooting

### 🎯 শেখার পদ্ধতি

শুধু theory মুখস্থ না করে আমরা এভাবে শিখব:

**Concept → Command → Example → নিজে Practice → ছোট Project**

যেমন প্রথমে:

```bash
pwd
ls
cd
mkdir linux
cd linux
touch hello.txt
ls
```

তারপর আমি প্রতিটি command **কেন ব্যবহার হয়, কীভাবে কাজ করে, output কী বোঝায় এবং common mistakes কী**—সব বুঝিয়ে দেব।

চাইলে আমরা এখনই **Linux Lesson 1: Linux কী, Kernel কী, Distribution কী, Terminal/Shell কী এবং Linux-এর File System** থেকে শুরু করতে পারি।


----
# 🐧 Linux — Level 1: Complete Beginner

## 1. Linux কী?

Linux হলো একটি **Unix-like operating system-এর family**, যার মূল ভিত্তি হলো **Linux kernel**।

সহজ উদাহরণ:

> Windows যেমন একটি operating-system ecosystem, Linux-ও তেমন একটি ecosystem; তবে Linux-এর ক্ষেত্রে বিভিন্ন distribution যেমন Ubuntu, Debian, Fedora ইত্যাদি ব্যবহৃত হয়।

### Linux কোথায় ব্যবহৃত হয়?

* 💻 Desktop/Laptop
* 🖥️ Servers
* ☁️ Cloud
* 📱 Android-এর kernel ভিত্তি
* 🌐 Web servers
* 🔐 Cybersecurity ও networking
* 🐳 Containers/Docker
* ⚙️ Embedded systems

---

# 2. Kernel কী?

এটা Linux শেখার সবচেয়ে গুরুত্বপূর্ণ basic concept।

**Kernel = Operating System-এর core অংশ।**

Kernel hardware এবং software-এর মধ্যে communication করায়।

উদাহরণ:

```text
User
  ↓
Application
  ↓
Shell / GUI
  ↓
Linux Kernel
  ↓
Hardware
```

তুমি যদি একটি file open করো, application সরাসরি hardware-এর সঙ্গে কাজ না করে kernel-এর মাধ্যমে প্রয়োজনীয় resources পায়।

### Kernel-এর প্রধান কাজ

* CPU management
* Memory management
* Process management
* Device management
* File-system management
* Networking

### Kernel version দেখতে

```bash
uname -r
```

Example output:

```text
6.8.0-40-generic
```

---

# 3. Linux Distribution কী?

অনেকে beginner অবস্থায় একটা mistake করে:

> **Linux = Ubuntu**

এটা পুরোপুরি ঠিক নয়।

Linux হলো kernel; আর Linux kernel-এর সঙ্গে বিভিন্ন software, package manager, libraries ইত্যাদি মিলিয়ে তৈরি হয় **Linux distribution (distro)**।

উদাহরণ:

* Ubuntu
* Debian
* Fedora
* Arch Linux
* Linux Mint
* Rocky Linux
* AlmaLinux

ধরো:

```text
Linux Kernel
     +
System utilities
     +
Libraries
     +
Package manager
     +
Applications
     ↓
Linux Distribution
```

### Interview Question

**Q: Is Ubuntu a Linux kernel?**

**Answer:** No. Ubuntu is a Linux distribution that uses the Linux kernel.

---

# 4. GUI এবং CLI

Linux-এ সাধারণত দুইভাবে কাজ করতে পারো।

### GUI

Graphical User Interface।

যেমন:

* Mouse
* Windows
* Icons
* File Manager

### CLI

Command Line Interface।

যেমন:

```bash
ls
cd
pwd
mkdir
```

Linux administration-এ CLI অত্যন্ত গুরুত্বপূর্ণ।

---

# 5. Terminal কী?

**Terminal হলো এমন একটি interface যেখানে তুমি command লিখে system-এর সঙ্গে কাজ করতে পারো।**

Terminal খুলে লিখতে পারো:

```bash
pwd
```

এটি তোমার বর্তমান directory দেখাবে।

---

# 6. Shell কী?

এখানে আরেকটি common beginner confusion:

> Terminal এবং Shell একই জিনিস নয়।

**Terminal** হলো interface।

**Shell** হলো এমন একটি program যা তোমার command বুঝে এবং system-এ execute করে।

Popular shell:

* Bash
* Zsh
* Fish

বর্তমান shell দেখতে:

```bash
echo $SHELL
```

Example:

```text
/bin/bash
```

### সহজ analogy

```text
You
 ↓
Terminal
 ↓
Shell
 ↓
Kernel
 ↓
Hardware
```

---

# 7. `pwd` — কোথায় আছি?

`pwd` = **Print Working Directory**

```bash
pwd
```

Example:

```text
/home/student
```

এর অর্থ তুমি বর্তমানে `/home/student` directory-তে আছো।

### Beginner mistake

❌ শুধু `pwd` দেখে `/home/student`-কে একটি file ভাবা।

এটি একটি **directory path**।

---

# 8. `ls` — ভিতরে কী আছে?

বর্তমান directory-এর files এবং directories দেখতে:

```bash
ls
```

আরও বিস্তারিত:

```bash
ls -l
```

Hidden files সহ:

```bash
ls -la
```

### Example

```bash
ls
```

Output:

```text
Documents
Downloads
file.txt
Pictures
```

### `-l` কী?

Long/list format।

### `-a` কী?

All files, including hidden files।

---

# 9. `cd` — Directory পরিবর্তন

`cd` = **Change Directory**

```bash
cd Documents
```

তারপর:

```bash
pwd
```

হতে পারে:

```text
/home/student/Documents
```

এক directory পিছনে:

```bash
cd ..
```

Home directory-তে:

```bash
cd ~
```

অথবা শুধু:

```bash
cd
```

---

# 10. Absolute Path বনাম Relative Path

এটা interview-এ খুব common।

### Absolute path

Root `/` থেকে সম্পূর্ণ path।

```text
/home/student/Documents/file.txt
```

### Relative path

বর্তমান location-এর relative path।

যদি তুমি `/home/student`-এ থাকো:

```bash
cd Documents
```

এটি relative path।

### Beginner mistake

`/` এবং `~` একই মনে করা।

তারা একই নয়।

```text
/     → Root directory
~     → Current user's home directory
```

---
~ এই symbol-এর নাম tilde (টিল্ড)।
# 11. `mkdir` — Directory তৈরি

```bash
mkdir test
```

এতে `test` নামে directory তৈরি হবে।

একাধিক directory:

```bash
mkdir one two three
```

Nested directory:

```bash
mkdir -p project/src/code
```

`-p` না দিলে parent directory না থাকলে command fail করতে পারে।

---

# 12. `touch` — File তৈরি

```bash
touch hello.txt
```

তারপর:

```bash
ls
```

দেখবে:

```text
hello.txt
```

### গুরুত্বপূর্ণ

`touch` সাধারণভাবে নতুন empty file তৈরি করতে পারে, কিন্তু existing file-এর timestamp-ও পরিবর্তন করতে পারে।

Beginnerরা অনেক সময় ভাবে:

> touch = শুধু file create

এটা সম্পূর্ণ ধারণা নয়।

---

# 13. `cp` — Copy

File copy:

```bash
cp hello.txt backup.txt
```

Directory copy করতে:

```bash
cp -r project project_backup
```

`-r` = recursive।

---

# 14. `mv` — Move / Rename

File move:

```bash
mv hello.txt Documents/
```

Rename:

```bash
mv old.txt new.txt
```

এখানে একটি গুরুত্বপূর্ণ বিষয়:

**Linux-এ আলাদা `rename` command না ব্যবহার করেও `mv` দিয়ে সাধারণ file rename করা যায়।**

---

# 15. `rm` — Delete

File delete:

```bash
rm hello.txt
```

Directory delete করতে:

```bash
rm -r test
```

### ⚠️ Beginner-এর সবচেয়ে গুরুত্বপূর্ণ mistake

`rm` ব্যবহার করার আগে খুব সতর্ক হও।

বিশেষ করে:

```bash
rm -r
```

এটি directory এবং তার contents মুছে দিতে পারে।

আর command blindly copy-paste করা উচিত নয়।

---

# 16. Linux File System

Linux-এ Windows-এর মতো:

```text
C:
D:
E:
```

ধারণাটি ব্যবহার করা হয় না।

Linux-এর filesystem শুরু হয়:

```text
/
```

এটিকে বলা হয় **root directory**।

একটি simplified structure:

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── opt
├── proc
├── root
├── tmp
├── usr
└── var
```

### গুরুত্বপূর্ণ directories

| Directory | সাধারণ উদ্দেশ্য                           |
| --------- | ----------------------------------------- |
| `/`       | Root                                      |
| `/home`   | সাধারণ users-এর home directories          |
| `/root`   | root user's home                          |
| `/etc`    | System configuration                      |
| `/tmp`    | Temporary files                           |
| `/var`    | Variable data/logs                        |
| `/usr`    | User-space programs/data                  |
| `/boot`   | Boot-related files                        |
| `/dev`    | Device files                              |
| `/proc`   | Process/kernel-related virtual filesystem |

---

# 17. `/root` বনাম `/`

এটাও খুব common interview question।

```text
/       = Root of the entire filesystem
/root   = Home directory of the root user
```

দুটো এক জিনিস নয়।

---

# 18. Hidden File

Linux-এ সাধারণত যে file-এর নাম `.` দিয়ে শুরু হয় সেটিকে hidden file হিসেবে দেখা হয়।

Example:

```text
.bashrc
.profile
```

সাধারণ:

```bash
ls
```

এগুলো নাও দেখতে পারো।

ব্যবহার করো:

```bash
ls -a
```

---

# 19. `cat`

File-এর contents দেখতে:

```bash
cat hello.txt
```

Example:

```text
Hello Linux
```

`cat` মূলত file concatenate/display করার command।

---

# 20. `less`

বড় file পড়ার জন্য:

```bash
less logfile.txt
```

এতে page-by-page দেখা যায়।

বের হতে:

```text
q
```

### Beginner mistake

বড় log file-এর জন্য সবসময়:

```bash
cat huge.log
```

ব্যবহার করা ভালো নয়—পুরো output terminal-এ ঢেলে দিতে পারে।

---

# 🧪 তোমার প্রথম Linux Practice

Terminal খুলে একে একে চালাও:

```bash
pwd
ls
mkdir linux_lab
cd linux_lab
touch file1.txt
mkdir documents
ls
mv file1.txt documents/
cd documents
ls
pwd
cd ..
cp -r documents backup
ls
```

শেষে structure এমন হতে পারে:

```text
linux_lab/
├── documents/
│   └── file1.txt
└── backup/
    └── file1.txt
```

---

# 🚨 Level 1-এর Common Beginner Mistakes

### Mistake 1

```bash
cd /home
```

আর

```bash
cd home
```

এক মনে করা।

**না।**

প্রথমটি absolute path, দ্বিতীয়টি relative path।

---

### Mistake 2

```text
/root = /
```

❌ ভুল।

---

### Mistake 3

`Linux = Ubuntu`

❌ Ubuntu হলো Linux distribution।

---

### Mistake 4

`Terminal = Shell`

❌ একই নয়।

---

### Mistake 5

`rm`-কে Windows Recycle Bin-এর মতো ভাবা।

❌ সাধারণ `rm` ব্যবহারে file traditional recycle-bin workflow-এ যায় না।

---

### Mistake 6

Linux case-sensitive নয় ভাবা।

❌ Linux সাধারণত case-sensitive।

```text
file.txt
File.txt
FILE.txt
```

এগুলো আলাদা নাম হতে পারে।

---

# 🎯 Level 1 Interview Questions

### Beginner

**1. What is Linux?**
Linux is a Unix-like operating-system family built around the Linux kernel.

**2. What is a kernel?**
The kernel is the core component that manages hardware resources and provides services to applications.

**3. What is a Linux distribution?**
A distribution combines the Linux kernel with system utilities, libraries, package-management tools, and other software.

**4. Give examples of Linux distributions.**
Ubuntu, Debian, Fedora, Arch Linux, Linux Mint, Rocky Linux.

**5. What is a terminal?**
A terminal provides an interface for interacting with the system, commonly through a command-line shell.

**6. What is a shell?**
A shell interprets commands and interacts with the operating system on the user's behalf.

**7. What is Bash?**
Bash is a widely used Unix/Linux command-line shell.

**8. What does `pwd` do?**
It prints the current working directory.

**9. What does `ls -la` do?**
It lists directory contents in long format, including hidden entries.

**10. What does `cd ..` do?**
It moves to the parent directory.

---

## 🔥 একটু কঠিন Interview Questions

**11. What is the difference between `/` and `/root`?**

`/` is the filesystem root; `/root` is the root user's home directory.

**12. What is the difference between absolute and relative paths?**

Absolute paths start from `/`; relative paths are interpreted from the current working directory.

**13. Is Linux an operating system or a kernel?**

Strictly speaking, **Linux is the kernel**. In everyday usage, "Linux" often refers to complete operating systems/distributions built around that kernel.

**14. Is Ubuntu Linux?**

Ubuntu is a Linux distribution.

**15. Is Linux case-sensitive?**

Yes, Linux filesystems and command-line environments generally treat uppercase and lowercase names as distinct.

**16. What is the difference between `cp` and `mv`?**

`cp` copies; `mv` moves or renames.

**17. What does `-r` mean in commands such as `cp -r`?**

It means recursive operation, allowing the command to process directories and their contents.

---

# 🏆 Level 1 শেষে তোমার যা জানা উচিত

```text
Linux
 ├── Kernel
 ├── Distribution
 ├── Terminal
 ├── Shell
 ├── Filesystem
 │    ├── /
 │    ├── /home
 │    ├── /etc
 │    ├── /var
 │    └── /root
 │
 └── Basic Commands
      ├── pwd
      ├── ls
      ├── cd
      ├── mkdir
      ├── touch
      ├── cp
      ├── mv
      ├── rm
      ├── cat
      └── less
```

**পরের ধাপে Level 2-তে** আমরা `grep`, `find`, pipes `|`, redirection `>`, `>>`, wildcards, `head`, `tail`, `sort`, `cut` ইত্যাদি **real-world example + practice + beginner mistakes + interview questions** সহ শিখব।

---
# 🐧 Linux Level 2 — Command Line Mastery

Level 2-তে আমরা Linux command line-এর সবচেয়ে গুরুত্বপূর্ণ tools শিখব। প্রতিটি command-এর **কাজ, syntax, example, common mistake এবং interview question** থাকবে।

---

## 1. `echo` — Text দেখানো

`echo` terminal-এ text বা variable-এর value দেখায়।

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

Variable:

```bash
name="Rahim"
echo $name
```

Output:

```text
Rahim
```

### Beginner mistake

```bash
echo name
```

এটি `name` text দেখাবে।

Variable-এর value চাইলে:

```bash
echo $name
```

---

# 2. `>` — Output Redirect

Command-এর output terminal-এ না দেখিয়ে file-এ পাঠাতে পারো।

```bash
echo "Hello" > hello.txt
```

তারপর:

```bash
cat hello.txt
```

Output:

```text
Hello
```

### ⚠️ গুরুত্বপূর্ণ

`>` existing file-এর content **overwrite** করে।

```bash
echo "Second" > hello.txt
```

আগের `Hello` চলে যাবে।

---

# 3. `>>` — Append

Existing content রেখে নতুন content যোগ করতে:

```bash
echo "First" > test.txt
echo "Second" >> test.txt
```

তারপর:

```bash
cat test.txt
```

Output:

```text
First
Second
```

### মনে রাখো

```text
>   = overwrite
>>  = append
```

---

# 4. `<` — Input Redirection

File থেকে command-এর input নেওয়া যায়।

উদাহরণ:

```bash
wc -l < test.txt
```

এখানে `test.txt` থেকে input নিয়ে `wc` line count করবে।

---

# 5. Pipe `|`

Linux-এর সবচেয়ে powerful conceptগুলোর একটি।

**এক command-এর output → অন্য command-এর input**

Example:

```bash
ls | grep ".txt"
```

এখানে:

```text
ls
 ↓
output
 ↓
grep
 ↓
শুধু .txt matching result
```

আরেকটি example:

```bash
cat names.txt | sort
```

এটি names sort করবে।

### Beginner mistake

`|` এবং `>` একই মনে করা।

❌ নয়।

```text
|  → output অন্য command-এ পাঠায়
>  → output file-এ পাঠায়
```

---

# 6. `grep` — Search

`grep` text-এর মধ্যে pattern search করে।

ধরো:

```text
names.txt
```

এর content:

```text
Rahim
Karim
Hasan
Rahim
```

Search:

```bash
grep "Rahim" names.txt
```

Output:

```text
Rahim
Rahim
```

### Case-insensitive search

```bash
grep -i "rahim" names.txt
```

### Line number সহ

```bash
grep -n "Rahim" names.txt
```

Example:

```text
1:Rahim
4:Rahim
```

### Multiple files

```bash
grep "error" app.log system.log
```

---

# 7. `grep -r` — Recursive Search

Directory-এর ভিতরের files-এ search করতে:

```bash
grep -r "error" logs/
```

এটি `logs/` এবং তার subdirectories-এর files-এ search করবে।

---

# 8. `find` — File খোঁজা

`find` filesystem-এ files/directories search করার জন্য ব্যবহৃত হয়।

Current directory-তে:

```bash
find .
```

`.txt` files:

```bash
find . -name "*.txt"
```

Directory খুঁজতে:

```bash
find . -type d -name "documents"
```

File খুঁজতে:

```bash
find . -type f -name "test.txt"
```

---

# 9. `find` + Size

বড় files খুঁজতে:

```bash
find . -type f -size +100M
```

অর্থাৎ 100 MB-এর বেশি files খোঁজা হবে।

---

# 10. `find` + Modification Time

গত 1 দিনের মধ্যে modified files:

```bash
find . -type f -mtime -1
```

এটি system administration-এ খুব useful।

---

# 11. `head`

File-এর শুরু থেকে কিছু line দেখতে:

```bash
head file.txt
```

Default-এ সাধারণত প্রথম 10 lines দেখা যায়।

নির্দিষ্ট 5 lines:

```bash
head -n 5 file.txt
```

---

# 12. `tail`

File-এর শেষের lines দেখতে:

```bash
tail file.txt
```

শেষ 5 lines:

```bash
tail -n 5 file.txt
```

---

# 13. `tail -f` — Real-time Log Monitoring

Server administration-এ অত্যন্ত গুরুত্বপূর্ণ।

```bash
tail -f /var/log/app.log
```

নতুন log line আসলে terminal-এ দেখতে থাকবে।

বন্ধ করতে:

```text
Ctrl + C
```

### Real-world example

ধরো website-এর server চলছে এবং application log তৈরি করছে।

তুমি দেখতে চাও নতুন error আসছে কিনা:

```bash
tail -f app.log
```

---

# 14. `wc` — Count

`wc` = Word Count।

```bash
wc file.txt
```

এটি সাধারণত দেখায়:

```text
lines words bytes
```

শুধু lines:

```bash
wc -l file.txt
```

শুধু words:

```bash
wc -w file.txt
```

শুধু bytes:

```bash
wc -c file.txt
```

---

# 15. `sort`

Text sort করতে:

```bash
sort names.txt
```

Reverse:

```bash
sort -r names.txt
```

Numeric sorting:

```bash
sort -n numbers.txt
```

---

# 16. `uniq`

Duplicate consecutive lines remove করার জন্য:

```bash
uniq names.txt
```

⚠️ এখানে beginnerদের একটি গুরুত্বপূর্ণ ভুল হয়।

`uniq` সাধারণত **adjacent/consecutive duplicate** lines নিয়ে কাজ করে।

তাই:

```text
Rahim
Rahim
Karim
Rahim
```

এখানে শেষের `Rahim` remove হবে না।

সব duplicate group করতে সাধারণত:

```bash
sort names.txt | uniq
```

---

# 17. `cut`

Text-এর নির্দিষ্ট অংশ বের করতে `cut` ব্যবহার করা হয়।

ধরো:

```text
Rahim:20:Dhaka
Karim:22:Chittagong
```

Colon delimiter ব্যবহার করে প্রথম field:

```bash
cut -d ':' -f 1 data.txt
```

Output:

```text
Rahim
Karim
```

দ্বিতীয় field:

```bash
cut -d ':' -f 2 data.txt
```

Output:

```text
20
22
```

---

# 18. Wildcards

Linux command line-এ wildcard খুব গুরুত্বপূর্ণ।

### `*`

যেকোনো সংখ্যক characters match করতে পারে।

```bash
ls *.txt
```

সব `.txt` files দেখাবে।

### `?`

একটি character match করে।

```bash
ls file?.txt
```

যেমন:

```text
file1.txt
file2.txt
```

match হতে পারে।

---

# 19. `*` বনাম `?`

ধরো files:

```text
file1.txt
file10.txt
fileABC.txt
```

```bash
ls file*.txt
```

তিনটিই match করতে পারে।

কিন্তু:

```bash
ls file?.txt
```

শুধু এক-character অংশের নাম match করবে, যেমন:

```text
file1.txt
```

---

# 20. Command Combination

এখন আসল Linux skill শুরু।

ধরো `access.log`-এ অনেক line আছে।

শুধু `ERROR` খুঁজতে:

```bash
grep "ERROR" access.log
```

কতগুলো ERROR আছে:

```bash
grep "ERROR" access.log | wc -l
```

এখানে:

```text
grep
 ↓
ERROR lines
 ↓
wc -l
 ↓
number of lines
```

---

# 🔥 Real-World Example

ধরো:

```text
server.log
```

এতে:

```text
INFO User logged in
ERROR Database failed
INFO Request received
ERROR Connection failed
WARNING Disk usage high
ERROR Database failed
```

### সব ERROR:

```bash
grep "ERROR" server.log
```

### ERROR-এর সংখ্যা:

```bash
grep "ERROR" server.log | wc -l
```

### ERROR-গুলো sort:

```bash
grep "ERROR" server.log | sort
```

### Duplicate ERROR count-এর জন্য:

```bash
grep "ERROR" server.log | sort | uniq -c
```

এখানে command chain:

```text
grep
 ↓
sort
 ↓
uniq
```

এটাই Linux command-line-এর আসল শক্তি।

---

# 🚨 Level 2 Common Beginner Mistakes

### Mistake 1 — `>` ব্যবহার করে file overwrite করা

```bash
echo "A" > test.txt
echo "B" > test.txt
```

শেষে থাকবে:

```text
B
```

Append চাইলে:

```bash
echo "B" >> test.txt
```

---

### Mistake 2 — `uniq` সব duplicate remove করবে ভাবা

`uniq` সাধারণত adjacent duplicate lines handle করে।

Better:

```bash
sort file.txt | uniq
```

---

### Mistake 3 — `grep` এবং `find` একই মনে করা

```text
grep → file-এর ভিতরের text/pattern search
find → filesystem-এর file/directory search
```

---

### Mistake 4 — `*` এবং `?` গুলিয়ে ফেলা

```text
* → zero or more characters
? → typically exactly one character
```

---

### Mistake 5 — `tail -f` থেকে বের হতে না পারা

```text
Ctrl + C
```

---

### Mistake 6 — Pipe-এর কাজ ভুল বোঝা

```bash
command1 | command2
```

মানে command1-এর output command2-এর input হিসেবে যাচ্ছে।

---

# 🧠 Level 2 Interview Questions

### 1. What is a pipe in Linux?

A pipe `|` sends the standard output of one command to the standard input of another command.

---

### 2. Difference between `>` and `>>`?

`>` overwrites a file, while `>>` appends output to a file.

---

### 3. What does `grep` do?

It searches input/files for lines matching a specified pattern.

---

### 4. Difference between `find` and `grep`?

`find` searches for files/directories based on filesystem criteria; `grep` searches text for matching patterns.

---

### 5. What does `grep -i` do?

It performs a case-insensitive search.

---

### 6. What does `grep -r` do?

It recursively searches through directories.

---

### 7. What does `tail -f` do?

It continuously displays new data appended to a file, commonly used for monitoring logs.

---

### 8. What does `wc -l` do?

It counts lines.

---

### 9. What is the difference between `head` and `tail`?

`head` displays the beginning of input; `tail` displays the end.

---

### 10. What does `sort | uniq -c` do?

It sorts input and then counts occurrences of identical consecutive lines.

---

# 🔥 Advanced Interview Questions

### Q11. How would you count the number of ERROR lines in a log?

```bash
grep -c "ERROR" app.log
```

অথবা:

```bash
grep "ERROR" app.log | wc -l
```

---

### Q12. How would you find all `.log` files under `/var`?

```bash
find /var -type f -name "*.log"
```

---

### Q13. How would you find the 10 largest files?

এটি একটু advanced; একটি common approach:

```bash
find . -type f -printf '%s %p\n' | sort -nr | head -10
```

এখানে:

```text
find
 ↓
file size + path
 ↓
sort largest first
 ↓
top 10
```

---

### Q14. How can you monitor a log file in real time?

```bash
tail -f application.log
```

---

### Q15. How can you search for "failed" ignoring case?

```bash
grep -i "failed" app.log
```

---

# 🧪 Level 2 Practice Project

নিজে একটি practice environment বানাও:

```bash
mkdir linux_level2
cd linux_level2

touch server.log
```

তারপর:

```bash
echo "INFO User logged in" >> server.log
echo "ERROR Database failed" >> server.log
echo "INFO Request received" >> server.log
echo "ERROR Connection failed" >> server.log
echo "WARNING Disk usage high" >> server.log
echo "ERROR Database failed" >> server.log
```

এখন নিজে বের করার চেষ্টা করো:

**1.** শুধু ERROR lines
**2.** ERROR কতগুলো
**3.** WARNING lines
**4.** সব lines-এর মধ্যে duplicate কোনগুলো
**5.** file-এর প্রথম 3 lines
**6.** শেষ 2 lines

এই ৬টা করতে পারলে **Level 2-এর core command-line concepts ভালোভাবে বুঝে ফেলবে।**

**Level 3**-এ এরপর আসবে Linux-এর অত্যন্ত গুরুত্বপূর্ণ অংশ: **Users, Groups, `sudo`, permissions, `chmod`, `chown`, `rwx`, `755`, `644`, এবং permission-based interview questions**।

---
# 🐧 Linux Level 3 — Users, Groups & Permissions

Level 3 Linux administration-এর জন্য খুব গুরুত্বপূর্ণ। এখানে আমরা শিখব:

**User → Group → Ownership → Permission → `chmod` → `chown` → `sudo` → `rwx` → `755/644` → troubleshooting → interview questions**

---

# 1. Linux-এ User কী?

Linux একটি **multi-user operating system**। একই machine-এ একাধিক user থাকতে পারে।

উদাহরণ:

```text
student
rahim
karim
admin
root
```

প্রতিটি user-এর আলাদা:

* username
* UID
* home directory
* permissions
* groups

বর্তমান user দেখতে:

```bash
whoami
```

Example:

```text
student
```

---

# 2. `id` — User সম্পর্কে তথ্য

```bash
id
```

Example:

```text
uid=1000(student) gid=1000(student) groups=1000(student),27(sudo)
```

এখানে:

```text
uid = User ID
gid = Primary Group ID
groups = User যে groups-এর member
```

অন্য user-এর information:

```bash
id rahim
```

---

# 3. UID কী?

**UID = User ID**

Linux internally username-এর পাশাপাশি numerical ID ব্যবহার করে।

উদাহরণ:

```text
student → UID 1000
```

একজন user-এর name পরিবর্তন হলেও system permission-এর ক্ষেত্রে UID গুরুত্বপূর্ণ।

---

# 4. GID কী?

**GID = Group ID**

প্রতিটি group-এর একটি numerical ID থাকে।

```bash
id
```

থেকে GID দেখা যায়।

---

# 5. `/etc/passwd`

Linux-এর local user account information সাধারণত এখানে থাকে:

```text
/etc/passwd
```

দেখতে:

```bash
cat /etc/passwd
```

একটি entry দেখতে এমন হতে পারে:

```text
student:x:1000:1000:Student:/home/student:/bin/bash
```

এর গুরুত্বপূর্ণ অংশ:

```text
username : password-placeholder : UID : GID : comment : home : shell
```

### ⚠️ গুরুত্বপূর্ণ

`/etc/passwd`-এ সাধারণত actual password রাখা হয় না।

Password hashes সাধারণত:

```text
/etc/shadow
```

এ থাকে এবং সেটি privileged access-এর জন্য protected।

---

# 6. User তৈরি করা

Linux-এ user তৈরি করতে:

```bash
sudo useradd rahim
```

কিন্তু beginner হিসেবে আরও convenient:

```bash
sudo adduser rahim
```

তারপর password এবং কিছু information চাইতে পারে।

---

# 7. User-এর Home Directory

User-এর home:

```text
/home/rahim
```

দেখতে:

```bash
ls /home
```

User create করার সময় home directory তৈরি করার behavior command/options-এর ওপর নির্ভর করতে পারে।

`useradd`-এর ক্ষেত্রে সাধারণত home explicitly দিতে পারো:

```bash
sudo useradd -m rahim
```

`-m` → home directory তৈরি করতে বলে।

---

# 8. User Delete

```bash
sudo userdel rahim
```

Home directory-সহ remove করতে:

```bash
sudo userdel -r rahim
```

### ⚠️ Beginner mistake

`userdel -r` সাবধানে ব্যবহার করতে হবে, কারণ user-এর home data মুছে যেতে পারে।

---

# 9. Group কী?

Group ব্যবহার করে একসঙ্গে একাধিক user-এর permission manage করা যায়।

উদাহরণ:

```text
developers
 ├── rahim
 ├── karim
 └── hasan
```

একটি project-এর files developers group-এর জন্য accessible করা যায়।

---

# 10. Group তৈরি

```bash
sudo groupadd developers
```

দেখতে:

```bash
getent group developers
```

---

# 11. User-কে Group-এ Add

```bash
sudo usermod -aG developers rahim
```

এখানে:

```text
-a = append
-G = supplementary groups
```

### ⚠️ খুব গুরুত্বপূর্ণ Beginner Mistake

অনেকে লেখে:

```bash
sudo usermod -G developers rahim
```

এতে existing supplementary groups replace হয়ে যেতে পারে।

সাধারণত নতুন group যোগ করার জন্য:

```bash
sudo usermod -aG developers rahim
```

ব্যবহার করা নিরাপদ।

---

# 12. User-এর Groups দেখা

```bash
groups rahim
```

অথবা:

```bash
id rahim
```

---

# 13. File Ownership

চলো:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 rahim developers 120 Sep 29 12:00 report.txt
```

এখানে:

```text
rahim       → owner
developers  → group
```

Linux file-এর সঙ্গে owner এবং group associated থাকে।

---

# 14. Linux Permission

এই অংশটি খুব ভালোভাবে বুঝতে হবে।

Example:

```text
-rwxr-xr--
```

এটিকে ভাগ করি:

```text
- | rwx | r-x | r--
    ↓      ↓     ↓
   User   Group Others
```

### প্রথম character

```text
-
```

মানে regular file।

যদি:

```text
d
```

হয়, তাহলে directory।

---

# 15. `rwx` কী?

তিন ধরনের basic permission:

```text
r = read
w = write
x = execute
```

### File-এর ক্ষেত্রে

**r** → file পড়তে পারবে
**w** → file modify করতে পারবে
**x** → executable হিসেবে চালাতে পারবে

---

# 16. Directory-এর ক্ষেত্রে `rwx`

এখানে beginnerদের খুব বেশি confusion হয়।

Directory-তে:

**r** → directory contents list করার ability

**w** → directory-এর entries create/delete/rename করার ability

**x** → directory-তে enter/traverse করার ability

তাই directory-তে `x` খুব গুরুত্বপূর্ণ।

---

# 17. User / Group / Others

Permission তিনটি category-তে দেওয়া হয়:

```text
User/Owner
Group
Others
```

Example:

```text
-rwxr-xr--
```

ভেঙে:

```text
Owner  → rwx
Group  → r-x
Others → r--
```

অর্থাৎ:

```text
Owner  → read + write + execute
Group  → read + execute
Others → read
```

---

# 18. Numeric Permission

Linux-এ permissions numbers দিয়েও লেখা যায়।

```text
r = 4
w = 2
x = 1
```

তাই:

```text
rwx = 4+2+1 = 7
rw- = 4+2   = 6
r-x = 4+1   = 5
r-- = 4     = 4
```

---

# 19. `755` বুঝে ফেলো

```text
755
```

ভাঙলে:

```text
7 → Owner
5 → Group
5 → Others
```

আর:

```text
7 = rwx
5 = r-x
5 = r-x
```

তাই:

```text
755 = rwxr-xr-x
```

---

# 20. `644`

```text
644
```

মানে:

```text
6 → rw-
4 → r--
4 → r--
```

অর্থাৎ:

```text
rw-r--r--
```

সাধারণ regular files-এর জন্য `644` একটি common permission configuration।

---

# 21. `chmod`

`chmod` = **change mode**

Permission পরিবর্তন করতে ব্যবহার করা হয়।

ধরো:

```bash
touch script.sh
```

বর্তমানে executable নয়।

```bash
chmod +x script.sh
```

তারপর:

```bash
ls -l script.sh
```

---

# 22. Numeric `chmod`

```bash
chmod 755 script.sh
```

এতে:

```text
rwxr-xr-x
```

হবে।

File:

```bash
chmod 644 report.txt
```

হবে:

```text
rw-r--r--
```

---

# 23. Symbolic `chmod`

Owner-এর execute permission:

```bash
chmod u+x script.sh
```

Group-এর write permission:

```bash
chmod g+w file.txt
```

Others-এর write permission remove:

```bash
chmod o-w file.txt
```

এখানে:

```text
u = user/owner
g = group
o = others
```

সবাইকে execute:

```bash
chmod a+x script.sh
```

`a` = all।

---

# 24. `chown`

`chown` = **change owner**

```bash
sudo chown rahim report.txt
```

এতে owner হবে `rahim`।

Owner এবং group দুটো:

```bash
sudo chown rahim:developers report.txt
```

---

# 25. `chgrp`

শুধু group পরিবর্তন:

```bash
sudo chgrp developers report.txt
```

---

# 26. `sudo`

`sudo` সাধারণ user-কে নির্দিষ্ট administrative command privilegedভাবে চালাতে দেয়, যদি তার configuration সেই অনুমতি দেয়।

উদাহরণ:

```bash
sudo apt update
```

User create:

```bash
sudo adduser rahim
```

### Beginner mistake

সব command-এর আগে `sudo` দেওয়া।

❌ দরকার নেই।

শুধু privilege দরকার এমন command-এ ব্যবহার করা উচিত।

---

# 27. Root User

Linux-এর একটি বিশেষ privileged account হলো:

```text
root
```

Root-এর অনেক administrative restriction থাকে না।

বর্তমান user:

```bash
whoami
```

যদি:

```text
root
```

দেখায়, তুমি root account হিসেবে কাজ করছ।

### ⚠️ Important

Root privileges নিয়ে ভুল command system-এর গুরুত্বপূর্ণ files পরিবর্তন বা delete করতে পারে। তাই administrative commands সতর্কভাবে চালাতে হয়।

---

# 28. Permission Example

ধরো:

```text
-rwxr-x---
```

ভাঙি:

```text
Owner  = rwx
Group  = r-x
Others = ---
```

Numeric:

```text
rwx = 7
r-x = 5
--- = 0
```

তাই:

```text
750
```

---

# 29. আরেকটি Example

```text
-rw-r-----
```

ভাঙি:

```text
Owner  → rw-
Group  → r--
Others → ---
```

Numeric:

```text
6 4 0
```

তাই:

```text
640
```

---

# 30. `ls -l` Reading Practice

ধরো:

```text
-rwxr-xr-- 1 rahim developers 2048 Sep 29 script.sh
```

তুমি কী বুঝবে?

```text
-              → regular file
rwx            → owner permissions
r-x            → group permissions
r--            → others permissions
rahim          → owner
developers     → group
2048           → size
script.sh      → filename
```

---

# 🔥 Real-world Scenario

ধরো একটি development project:

```text
/opt/project
```

Team:

```text
developers
```

Users:

```text
rahim
karim
hasan
```

প্রথমে:

```bash
sudo groupadd developers
```

Users-কে group-এ:

```bash
sudo usermod -aG developers rahim
sudo usermod -aG developers karim
sudo usermod -aG developers hasan
```

Project directory-এর group:

```bash
sudo chown -R root:developers /opt/project
```

তারপর appropriate permissions set করা যায়, requirements অনুযায়ী।

**এখানে গুরুত্বপূর্ণ concept হলো:**

```text
Users
  ↓
Group
  ↓
Ownership
  ↓
Permissions
```

---

# 🚨 Level 3-এর Common Beginner Mistakes

### Mistake 1

`755` মানে সবাই full permission।

❌ ভুল।

```text
755
Owner  → rwx
Group  → r-x
Others → r-x
```

---

### Mistake 2

`644` মানে owner-এর execute permission আছে।

❌ না।

```text
644 = rw-r--r--
```

Owner-এর `x` নেই।

---

### Mistake 3

File-এর `x` এবং directory-এর `x` একইভাবে ভাবা।

❌ না।

Directory-এর `x` মূলত traversal/access-এর সঙ্গে সম্পর্কিত।

---

### Mistake 4

```bash
chmod 777 file
```

কে default solution ভাবা।

❌ উচিত নয়।

`777` দিলে:

```text
rwxrwxrwx
```

অর্থাৎ owner, group, others—তিন পক্ষেরই read/write/execute permission থাকে।

Permission যতটা দরকার, ততটাই দেওয়া উচিত।

---

### Mistake 5

```bash
usermod -G developers rahim
```

দিয়ে নতুন group যোগ করা।

এতে supplementary group membership replace হওয়ার ঝুঁকি থাকে।

সাধারণভাবে:

```bash
usermod -aG developers rahim
```

ব্যবহার করো।

---

# 🧠 Level 3 Interview Questions

### Q1. What is UID?

UID is the numeric identifier assigned to a Linux user.

### Q2. What is GID?

GID is the numeric identifier assigned to a group.

### Q3. What is the difference between user and group?

A user represents an individual account; a group is a collection of users used to manage access collectively.

### Q4. What are the three basic Linux permissions?

```text
r = read
w = write
x = execute
```

### Q5. What are the three permission classes?

```text
owner
group
others
```

### Q6. What does `chmod 755 file` mean?

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

### Q7. What does `chmod 644 file` mean?

```text
Owner  → rw-
Group  → r--
Others → r--
```

### Q8. What does `chown` do?

It changes the owner of a file or directory.

### Q9. Difference between `chown` and `chmod`?

```text
chown → ownership
chmod → permissions
```

### Q10. What is `sudo`?

It allows an authorized user to execute a command with elevated privileges according to the system's sudo configuration.

---

# 🔥 Advanced Interview Questions

### Q11. What does `rwxr-xr--` mean?

```text
Owner  → rwx
Group  → r-x
Others → r--
```

Numeric:

```text
754
```

---

### Q12. What is the difference between `/root` and `root`?

```text
/root → root user's home directory
root  → privileged user/account
```

---

### Q13. What is the difference between `chmod 755` and `chmod 644`?

```text
755 → owner can read/write/execute; group and others can read/execute

644 → owner can read/write; group and others can only read
```

---

### Q14. Why shouldn't you use `chmod 777` everywhere?

Because it grants read, write, and execute permissions to owner, group, and others, potentially allowing unintended modification or execution.

---

### Q15. What does `chmod u+x file` mean?

Add execute permission for the file owner.

---

### Q16. What does `chmod g-w file` mean?

Remove write permission from the group.

---

### Q17. What does this mean?

```bash
chown rahim:developers project.txt
```

Owner:

```text
rahim
```

Group:

```text
developers
```

---

# 🧪 Level 3 Hands-on Lab

নিজে একটি lab তৈরি করো:

```bash
mkdir linux_level3
cd linux_level3

touch file.txt
mkdir project
```

Permission দেখো:

```bash
ls -l
```

তারপর:

```bash
chmod 640 file.txt
chmod 750 project
```

আবার:

```bash
ls -ld project
ls -l file.txt
```

এখন permission পড়ার চেষ্টা করো।

### Challenge

নিচের permission-এর numeric value বের করো:

```text
rwxr-xr-x
rw-r--r--
rwx------
rw-r-----
r-xr-x---
```

**Answers:**

```text
rwxr-xr-x → 755
rw-r--r-- → 644
rwx------ → 700
rw-r----- → 640
r-xr-x--- → 550
```

---

## 🎯 Level 3 Mastery Checklist

Level 3 শেষ হলে তোমার confidently বলতে পারা উচিত:

```text
✓ User কী
✓ UID কী
✓ Group কী
✓ GID কী
✓ /etc/passwd কী
✓ /etc/shadow কী
✓ root কী
✓ sudo কী
✓ owner কী
✓ group ownership কী
✓ r/w/x কী
✓ directory permissions কীভাবে কাজ করে
✓ chmod
✓ chown
✓ chgrp
✓ 755
✓ 644
✓ 750
✓ 640
✓ symbolic permissions
✓ numeric permissions
```

**এর পর Level 4-এ আমরা Package Management শিখব:** `apt`, `dpkg`, repository, install/update/remove package, dependency, `apt update` বনাম `apt upgrade`, এবং এগুলোর **real-world troubleshooting + interview questions**।

---
# 🐧 Linux Level 4 — Package Management

Level 4-এ আমরা Linux-এ **software/package install, update, remove, search এবং troubleshoot** করা শিখব।

> এখানে মূলত **Debian/Ubuntu-based Linux** দিয়ে example দেব। শেষে Fedora/RHEL-এর `dnf`-এর সঙ্গে comparison-ও থাকবে।

---

# 1. Package কী?

Linux-এ software সাধারণত **package** আকারে distributed হয়।

একটি package-এর মধ্যে থাকতে পারে:

* Program files
* Configuration files
* Libraries
* Metadata
* Dependencies
* Documentation

উদাহরণ:

```text
nginx
python3
curl
git
vim
```

Ubuntu/Debian-এ package file সাধারণত:

```text
something.deb
```

---

# 2. Package Manager কী?

Package manually download করে install করার বদলে **package manager** ব্যবহার করা হয়।

Package manager সাধারণত:

```text
Search
 ↓
Download
 ↓
Dependency resolve
 ↓
Install
 ↓
Update
 ↓
Remove
```

করতে সাহায্য করে।

Debian/Ubuntu-তে:

```text
APT
```

Fedora/RHEL-এর modern systems-এ:

```text
DNF
```

---

# 3. APT কী?

**APT = Advanced Package Tool**

Ubuntu/Debian systems-এ package management-এর জন্য `apt` খুব common।

Version দেখতে:

```bash
apt --version
```

---

# 4. Repository কী?

Repository হলো এমন একটি software source যেখানে packages এবং package metadata রাখা হয়।

সহজভাবে:

```text
Your Computer
      ↓
     APT
      ↓
 Repository
      ↓
 Package
```

তুমি যখন:

```bash
sudo apt install nginx
```

চালাও, APT configured repositories থেকে প্রয়োজনীয় package এবং dependencies সংগ্রহ করতে পারে।

---

# 5. `apt update`

এটি অত্যন্ত গুরুত্বপূর্ণ।

```bash
sudo apt update
```

এর অর্থ **installed software update করা নয়**।

এটি package repository-এর **package information/index refresh** করে।

সহজভাবে:

```text
Repository
   ↓
New package information
   ↓
apt update
   ↓
Local package lists refreshed
```

### Beginner-এর বড় ভুল

```text
apt update = software update
```

❌ পুরোপুরি ঠিক নয়।

---

# 6. `apt upgrade`

Installed packages-এর available newer versions install করতে:

```bash
sudo apt upgrade
```

তাই সাধারণ workflow:

```bash
sudo apt update
sudo apt upgrade
```

### Difference

```text
apt update
→ package lists/information refresh

apt upgrade
→ installed packages-এর available upgrades install
```

---

# 7. Package Install

ধরো `curl` install করতে চাও:

```bash
sudo apt install curl
```

একাধিক package:

```bash
sudo apt install git vim curl
```

---

# 8. Package Remove

Package remove:

```bash
sudo apt remove curl
```

এটি package remove করবে, কিন্তু কিছু configuration file রেখে যেতে পারে।

---

# 9. `apt purge`

Package-এর সঙ্গে associated configuration files-ও remove করতে:

```bash
sudo apt purge curl
```

### Difference

```text
remove
→ package remove

purge
→ package + relevant configuration removal
```

তবে exact files/configuration behavior package-specific হতে পারে।

---

# 10. Package Search

Package-এর নাম বা description search:

```bash
apt search nginx
```

---

# 11. Package Information

কোন package সম্পর্কে information দেখতে:

```bash
apt show nginx
```

এতে package-এর:

* Version
* Description
* Dependencies
* Size
* Repository information

ইত্যাদি দেখা যেতে পারে।

---

# 12. Installed Package Check

Package installed কিনা দেখতে:

```bash
dpkg -l
```

নির্দিষ্ট package:

```bash
dpkg -l nginx
```

অথবা:

```bash
apt list --installed
```

---

# 13. `dpkg` কী?

`dpkg` হলো Debian-based systems-এর **low-level package management tool**।

`.deb` package নিয়ে সরাসরি কাজ করতে পারে।

APT এবং dpkg-এর সম্পর্ক roughly:

```text
APT
 ↓
Dependency/repository management
 ↓
dpkg
 ↓
Install/manage .deb packages
```

---

# 14. `.deb` Package কী?

Debian/Ubuntu package file:

```text
program.deb
```

Install করতে modern systems-এ:

```bash
sudo apt install ./program.deb
```

এটি local `.deb` package install করার পাশাপাশি dependencies resolve করতে পারে।

---

# 15. `dpkg -i`

`.deb` manually install করার traditional method:

```bash
sudo dpkg -i program.deb
```

কিন্তু dependency missing থাকলে problem হতে পারে।

সেক্ষেত্রে:

```bash
sudo apt install -f
```

ব্যবহার করা হতে পারে।

`-f` এখানে broken dependencies ঠিক করার জন্য dependency fixing operation বোঝায়।

---

# 16. Dependency কী?

একটি software অন্য software/library-এর ওপর নির্ভর করতে পারে।

উদাহরণ:

```text
Application
   ↓
Library A
   ↓
Library B
```

Application install করার সময় এগুলো দরকার হতে পারে।

APT dependency resolution-এর বড় সুবিধা হলো এটি প্রয়োজনীয় dependencies automatically handle করতে পারে।

---

# 17. Dependency Problem Example

ধরো তুমি একটি `.deb` manually install করলে:

```bash
sudo dpkg -i app.deb
```

এবং dependency missing।

তখন:

```bash
sudo apt install -f
```

প্রয়োজনীয় dependencies install/fix করতে সাহায্য করতে পারে।

---

# 18. `apt autoremove`

যেসব dependency আর দরকার নেই, সেগুলোর কিছু remove করতে:

```bash
sudo apt autoremove
```

⚠️ Command চালানোর আগে proposed removal list দেখে নেওয়া ভালো।

---

# 19. `apt clean`

APT-এর downloaded package cache পরিষ্কার করতে:

```bash
sudo apt clean
```

এটি disk space ব্যবহারের কিছু অংশ কমাতে সাহায্য করতে পারে।

---

# 20. `apt autoclean`

পুরোনো package files যেগুলো আর repository থেকে পাওয়া যায় না, সেগুলোর cache cleanup করতে:

```bash
sudo apt autoclean
```

---

# 21. Package Version দেখা

```bash
apt policy nginx
```

এতে installed এবং candidate version সম্পর্কিত information দেখা যায়।

---

# 22. কোন Package কোন File Install করেছে?

যদি package installed থাকে:

```bash
dpkg -L nginx
```

এতে package-এর installed files-এর list পাওয়া যায়।

---

# 23. কোন Package একটি File দিয়েছে?

যদি local system-এ fileটি কোন installed package-এর তা জানতে চাও:

```bash
dpkg -S /path/to/file
```

Example:

```bash
dpkg -S /usr/bin/curl
```

---

# 24. Package Installation-এর Basic Workflow

একটি practical workflow:

```bash
sudo apt update
sudo apt install nginx
```

Check:

```bash
nginx -v
```

তারপর package information:

```bash
apt show nginx
```

Remove:

```bash
sudo apt remove nginx
```

---

# 25. `apt update` বনাম `apt upgrade`

এটা interview-এর খুব common question।

| Command          | কাজ                                              |
| ---------------- | ------------------------------------------------ |
| `apt update`     | Repository package information refresh           |
| `apt upgrade`    | Installed packages-এর available upgrades install |
| `apt install`    | Package install                                  |
| `apt remove`     | Package remove                                   |
| `apt purge`      | Package + relevant configuration remove          |
| `apt autoremove` | No-longer-needed dependencies remove             |

---

# 26. `apt` বনাম `apt-get`

দুটোই Debian-based systems-এ package management-এর সঙ্গে সম্পর্কিত।

```bash
apt
```

সাধারণ user-facing interactive usage-এর জন্য convenient।

```bash
apt-get
```

Traditional scripting/automation environments-এ বেশি দেখা যায়।

উদাহরণ:

```bash
sudo apt update
```

এবং:

```bash
sudo apt-get update
```

দুটোই package metadata update করতে পারে।

---

# 27. Ubuntu/Debian Repository Configuration

Repository configuration সাধারণত এখানে পাওয়া যায়:

```text
/etc/apt/sources.list
```

এবং:

```text
/etc/apt/sources.list.d/
```

দেখতে:

```bash
cat /etc/apt/sources.list
```

অথবা:

```bash
ls /etc/apt/sources.list.d/
```

### ⚠️ Beginner Warning

Repository configuration blindly edit করা উচিত নয়। ভুল repository configuration করলে package management সমস্যা হতে পারে।

---

# 28. GPG Signing এবং Repository Security

Package repositories সাধারণত cryptographic signing ব্যবহার করে যাতে package/source authenticity যাচাই করা যায়।

APT trusted repository metadata verify করার mechanisms ব্যবহার করে।

তাই random website থেকে `.deb` download করে install করার বদলে trusted repository ব্যবহার করা সাধারণত safer workflow।

---

# 29. Fedora/RHEL-এ কী ব্যবহার হয়?

Ubuntu/Debian:

```text
apt
dpkg
.deb
```

Fedora/RHEL family:

```text
dnf
.rpm
```

উদাহরণ:

```bash
sudo dnf install nginx
```

Update:

```bash
sudo dnf upgrade
```

Search:

```bash
dnf search nginx
```

---

# 30. APT বনাম DNF

| Ubuntu/Debian | Fedora/RHEL                         |
| ------------- | ----------------------------------- |
| `apt`         | `dnf`                               |
| `dpkg`        | RPM                                 |
| `.deb`        | `.rpm`                              |
| `/etc/apt/`   | `/etc/dnf/` ও related configuration |

Concept কিন্তু একই:

```text
Repository
 ↓
Package Manager
 ↓
Dependencies
 ↓
Install/Update/Remove
```

---

# 🔥 Real-World Scenario 1

ধরো server-এ `curl` install করতে হবে।

প্রথমে:

```bash
sudo apt update
```

তারপর:

```bash
sudo apt install curl
```

Check:

```bash
curl --version
```

---

# 🔥 Real-World Scenario 2 — Package Install হচ্ছে না

ধরো:

```bash
sudo apt install nginx
```

কোনো error পেলাম।

তখন blindly random commands চালানো উচিত নয়।

প্রথমে:

```bash
sudo apt update
```

তারপর error message পড়ো।

Package status:

```bash
apt policy nginx
```

যদি dependency issue থাকে, error-এর details অনুযায়ী troubleshoot করতে হবে।

---

# 🔥 Real-World Scenario 3 — Broken `.deb`

```bash
sudo dpkg -i app.deb
```

যদি dependencies missing হয়:

```bash
sudo apt install -f
```

তারপর package state আবার check করা যায়:

```bash
dpkg -l app-name
```

---

# 🚨 Level 4 Common Beginner Mistakes

### Mistake 1

```bash
sudo apt update
```

চালিয়ে ভাবা software update হয়ে গেছে।

❌ `apt update` package lists refresh করে।

---

### Mistake 2

সব software random website থেকে `.deb` download করা।

এতে:

* security risk
* dependency problem
* incompatible package
* update management সমস্যা

হতে পারে।

---

### Mistake 3

`remove` এবং `purge` একই মনে করা।

```text
remove → package removal
purge  → package + relevant configuration removal
```

---

### Mistake 4

`dpkg -i` সব dependency automatically solve করবে ভাবা।

❌ `dpkg` low-level tool; dependency resolution-এর জন্য APT বেশি suitable।

---

### Mistake 5

`apt autoremove` blindly চালানো।

কী remove হবে আগে review করা উচিত।

---

### Mistake 6

Repository file blindly modify করা।

ভুল repository configuration package management ভেঙে দিতে পারে।

---

# 🧠 Level 4 Interview Questions

### Q1. What is a package?

A package is a bundled unit containing software and associated metadata/files required for installation and management.

---

### Q2. What is a package manager?

A package manager installs, removes, upgrades, searches, and manages software packages and their dependencies.

---

### Q3. What is APT?

APT is the package-management framework commonly used on Debian and Ubuntu systems.

---

### Q4. What does `apt update` do?

It refreshes the local package metadata/indexes from configured repositories.

---

### Q5. What does `apt upgrade` do?

It upgrades installed packages for which newer versions are available, subject to the package manager's dependency and upgrade rules.

---

### Q6. Difference between `apt update` and `apt upgrade`?

```text
apt update
→ refresh package information

apt upgrade
→ install available package upgrades
```

---

### Q7. What is `dpkg`?

`dpkg` is the low-level package management tool used by Debian-based systems to work with `.deb` packages.

---

### Q8. What is a dependency?

A dependency is another software component/package required by a package for it to function correctly.

---

### Q9. What is the difference between `apt remove` and `apt purge`?

`remove` removes the package while potentially leaving configuration files; `purge` also removes associated configuration files managed by the package.

---

### Q10. What is a repository?

A repository is a configured source containing packages and package metadata from which a package manager can retrieve software.

---

# 🔥 Advanced Interview Questions

### Q11. Why use APT instead of manually installing `.deb` files?

APT can retrieve packages from configured repositories and resolve/manage dependencies, while manually installing individual `.deb` files can require dependency handling separately.

---

### Q12. What happens when you run:

```bash
sudo apt install nginx
```

High-level process:

```text
APT
 ↓
Check package metadata
 ↓
Find nginx
 ↓
Resolve dependencies
 ↓
Download packages
 ↓
Install/configure packages
```

---

### Q13. What is the difference between APT and dpkg?

```text
APT
→ higher-level package management
→ repositories
→ dependency resolution

dpkg
→ lower-level Debian package tool
→ directly handles .deb packages
```

---

### Q14. What is the equivalent of APT on Fedora?

Modern Fedora commonly uses:

```text
DNF
```

---

### Q15. What is the difference between `.deb` and `.rpm`?

```text
.deb → Debian/Ubuntu ecosystem
.rpm → Red Hat/Fedora ecosystem
```

---

# 🧪 Level 4 Hands-on Lab

Ubuntu/Debian machine থাকলে নিজে করো:

### Step 1

```bash
apt --version
```

### Step 2

```bash
apt search curl
```

### Step 3

```bash
apt show curl
```

### Step 4

```bash
sudo apt update
```

### Step 5

```bash
sudo apt install curl
```

### Step 6

```bash
curl --version
```

### Step 7

```bash
apt list --installed 2>/dev/null | grep curl
```

### Step 8

```bash
sudo apt remove curl
```

---

# 🎯 Level 4 Mastery Checklist

```text
✓ Package কী
✓ Package Manager কী
✓ Repository কী
✓ APT কী
✓ apt update
✓ apt upgrade
✓ apt install
✓ apt remove
✓ apt purge
✓ apt search
✓ apt show
✓ apt autoremove
✓ apt clean
✓ dpkg
✓ .deb
✓ Dependency
✓ /etc/apt/
✓ apt vs apt-get
✓ Debian/Ubuntu vs Fedora/RHEL
✓ apt vs dnf
```

### 🏆 এখন পর্যন্ত Linux Journey

```text
LEVEL 1
Linux basics
Terminal
Shell
Filesystem
Basic commands

        ↓

LEVEL 2
grep
find
pipe
redirection
sort
uniq
cut
head
tail
wildcards

        ↓

LEVEL 3
Users
Groups
UID/GID
Ownership
rwx
chmod
chown
sudo

        ↓

LEVEL 4
Packages
APT
DPKG
Repositories
Dependencies
Install/Update/Remove
```

**Level 5-এ** আমরা Linux-এর **Process & Service Management** শিখব: `ps`, `top`, `htop`, `kill`, PID, signals, foreground/background process, `jobs`, `bg`, `fg`, `systemctl`, services, `systemd`, logs এবং troubleshooting—এর সঙ্গে interview questions।

---
# 🐧 Linux Level 5 — Processes, Services & Systemd

Level 5 Linux administration-এর একটি **খুব গুরুত্বপূর্ণ অংশ**। এখানে আমরা শিখব:

**Process → PID → PPID → foreground/background → `ps` → `top` → `htop` → `kill` → signals → jobs → `bg` → `fg` → `systemctl` → systemd → service → logs → troubleshooting → interview questions**

---

# 1. Process কী?

Linux-এ যখন কোনো program execute হয়, তখন তার একটি **running instance** তৈরি হয়—এটাকে process বলা হয়।

উদাহরণ:

```bash
firefox
```

Firefox চালু হলে Linux তার জন্য process তৈরি করে।

সহজভাবে:

```text
Program
   ↓
Execute
   ↓
Process
   ↓
CPU + Memory + Other resources
```

একই program-এর একাধিক process-ও থাকতে পারে।

---

# 2. PID কী?

**PID = Process ID**

প্রতিটি running process-এর একটি unique process ID থাকে।

দেখতে:

```bash
ps
```

Example:

```text
PID TTY          TIME CMD
2451 pts/0    00:00:00 bash
3180 pts/0    00:00:00 ps
```

এখানে:

```text
2451 → bash-এর PID
3180 → ps-এর PID
```

---

# 3. PPID কী?

**PPID = Parent Process ID**

একটি process অন্য process থেকে তৈরি হলে parent-child relationship থাকতে পারে।

উদাহরণ:

```text
Parent
  │
  └── Child
```

`ps` দিয়ে:

```bash
ps -o pid,ppid,cmd
```

Example:

```text
PID    PPID   CMD
2451   2300   bash
3500   2451   sleep 100
```

এখানে `sleep` process-এর parent হলো `bash`।

---

# 4. PID 1 — কেন গুরুত্বপূর্ণ?

Linux boot হওয়ার পর একটি বিশেষ প্রথম userspace process চালু হয়।

আধুনিক Linux distributions-এ সাধারণত:

```text
systemd
```

PID:

```text
1
```

চেক:

```bash
ps -p 1 -o pid,comm,args
```

Example:

```text
PID COMMAND  COMMAND
1   systemd  /sbin/init
```

### গুরুত্বপূর্ণ

`systemd` শুধু একটি service manager নয়; এটি modern Linux systems-এর initialization এবং বিভিন্ন system-management কাজের কেন্দ্রীয় component।

---

# 5. Running Processes দেখা — `ps`

Basic:

```bash
ps
```

আরও useful:

```bash
ps aux
```

এখানে:

* `a` → অনেক/all users-এর processes
* `u` → user-oriented format
* `x` → terminal-এর সঙ্গে directly attached নয় এমন processes-ও include করতে সাহায্য করে

---

# 6. `ps -ef`

আরেকটি খুব common command:

```bash
ps -ef
```

Example:

```text
UID       PID   PPID  C STIME TTY      TIME CMD
root        1      0  0 ...   ?        ...  /sbin/init
student  2451   2300  0 ...   pts/0    ...  bash
```

Interview-এ দুটোই দেখতে পাবে:

```bash
ps aux
ps -ef
```

---

# 7. Specific Process Search

ধরো nginx process খুঁজতে চাও:

```bash
ps aux | grep nginx
```

অথবা:

```bash
pgrep nginx
```

`pgrep` process name অনুযায়ী PID খুঁজতে convenient।

---

# 8. `top`

Live process monitoring:

```bash
top
```

এখানে দেখতে পারো:

* CPU usage
* Memory usage
* Load
* PID
* Process owner
* Process state
* Running processes

বের হতে:

```text
q
```

---

# 9. `htop`

`htop` হলো interactive process viewer।

```bash
htop
```

যদি installed না থাকে:

```bash
sudo apt install htop
```

তারপর:

```bash
htop
```

`top` এবং `htop` একই উদ্দেশ্যের হলেও `htop` সাধারণত বেশি interactive এবং user-friendly।

---

# 10. CPU ও Memory

`top`/`htop`-এ process resource usage দেখতে পারো।

উদাহরণ:

```text
PID    CPU%    MEM%    COMMAND
1200   80.0    5.2     python
1300   20.0    2.1     nginx
```

যদি কোনো process অস্বাভাবিকভাবে CPU ব্যবহার করে, সেটি investigate করতে হবে—সরাসরি kill করা সবসময় প্রথম step নয়।

---

# 11. Process State

Linux process-এর বিভিন্ন state থাকতে পারে।

Common states:

```text
R → Running / Runnable
S → Interruptible sleep
D → Uninterruptible sleep
T → Stopped/Traced
Z → Zombie
```

`ps` output-এ এগুলো দেখতে পারো:

```bash
ps -eo pid,stat,cmd
```

---

# 12. Zombie Process কী?

Zombie process হলো এমন একটি terminated child process যার exit status এখনও parent process collect করেনি।

Concept:

```text
Child process
    ↓
terminates
    ↓
Parent hasn't collected status
    ↓
Zombie
```

Zombie সাধারণত CPU execute করে না; কিন্তু process table-এ entry রাখতে পারে।

---

# 13. Process Terminate — `kill`

ধরো PID:

```text
3456
```

সাধারণ termination request:

```bash
kill 3456
```

Default signal হলো:

```text
SIGTERM
```

---

# 14. SIGTERM বনাম SIGKILL

এটা খুব গুরুত্বপূর্ণ।

### SIGTERM

```bash
kill -15 3456
```

অথবা:

```bash
kill 3456
```

Process-কে politely terminate করার request দেয়।

Process cleanup করার সুযোগ পেতে পারে।

### SIGKILL

```bash
kill -9 3456
```

এটি forceful termination signal।

Process এটি catch বা ignore করতে পারে না।

### Golden Rule

```text
SIGTERM → first choice in many cases
SIGKILL → last resort
```

### Beginner mistake

সব process-এর জন্য:

```bash
kill -9
```

ব্যবহার করা।

❌ ভালো practice নয়।

---

# 15. Signals কী?

Linux process-কে বিভিন্ন **signals** পাঠাতে পারে।

কিছু গুরুত্বপূর্ণ signal:

```text
SIGTERM  15 → graceful termination request
SIGKILL   9 → forceful termination
SIGSTOP  19 → stop process
SIGCONT  18 → continue stopped process
SIGHUP    1 → hangup/reload-related use cases
SIGINT    2 → interrupt, commonly Ctrl+C
```

Signals list:

```bash
kill -l
```

---

# 16. `Ctrl + C`

Terminal-এ চলমান foreground command interrupt করতে:

```text
Ctrl + C
```

সাধারণত এটি:

```text
SIGINT
```

signal পাঠায়।

---

# 17. `Ctrl + Z`

Foreground process suspend করতে:

```text
Ctrl + Z
```

সাধারণত এটি:

```text
SIGTSTP
```

দিয়ে process-কে stopped state-এ পাঠায়।

তারপর:

```bash
jobs
```

দিয়ে দেখতে পারো।

---

# 18. Background Process

ধরো:

```bash
sleep 100
```

এটি terminal আটকে রাখবে যতক্ষণ process চলছে।

Background-এ চালাতে:

```bash
sleep 100 &
```

Output হতে পারে:

```text
[1] 4567
```

এখানে:

```text
1    → job number
4567 → PID
```

---

# 19. `jobs`

Current shell-এর background/stopped jobs:

```bash
jobs
```

Example:

```text
[1]+  Running    sleep 100 &
[2]-  Stopped    vim test.txt
```

---

# 20. `fg`

Background job-কে foreground-এ আনতে:

```bash
fg
```

Specific job:

```bash
fg %1
```

---

# 21. `bg`

Stopped job-কে background-এ continue করতে:

```bash
bg %1
```

---

# 22. Process vs Job

এখানে beginnerদের confusion হয়।

**PID** হলো process-এর system-wide process identifier।

**Job number** হলো current shell-এর job-control identifier।

উদাহরণ:

```text
[1] 4567
```

```text
1    → shell job number
4567 → process PID
```

---

# 23. `nohup`

Terminal logout করার পরও কোনো long-running command চালিয়ে রাখতে `nohup` ব্যবহার করা যেতে পারে:

```bash
nohup ./script.sh &
```

এটি সাধারণত SIGHUP-এর প্রভাব থেকে command-কে বিচ্ছিন্নভাবে চালানোর জন্য ব্যবহৃত হয়।

---

# 24. Service কী?

Service হলো background-এ system বা application-এর জন্য কাজ করা long-running process/application।

উদাহরণ:

* SSH server
* Web server
* Database
* Cron-related services

---

# 25. `systemctl`

Modern systemd-based Linux systems-এ service manage করতে:

```bash
systemctl
```

ব্যবহার করা হয়।

---

# 26. Service Status

ধরো SSH service:

```bash
systemctl status ssh
```

কিছু distributions-এ service name হতে পারে:

```text
sshd
```

তাই system অনুযায়ী নাম আলাদা হতে পারে।

---

# 27. Service Start

```bash
sudo systemctl start nginx
```

এতে বর্তমানে service start হবে।

---

# 28. Service Stop

```bash
sudo systemctl stop nginx
```

বর্তমানে service stop হবে।

---

# 29. Service Restart

```bash
sudo systemctl restart nginx
```

Service restart হবে।

---

# 30. Reload বনাম Restart

এটা interview-এ গুরুত্বপূর্ণ।

```bash
sudo systemctl reload nginx
```

Reload সাধারণত configuration re-read করার চেষ্টা করে **service পুরোপুরি stop/start না করেই**।

```bash
sudo systemctl restart nginx
```

Service restart করে।

কোনটি supported তা service-এর ওপর নির্ভর করে।

---

# 31. Enable বনাম Start

এখানে beginnerদের common mistake।

```bash
sudo systemctl start nginx
```

মানে:

> এখন nginx চালু করো।

কিন্তু:

```bash
sudo systemctl enable nginx
```

মানে:

> System boot-এর সময় nginx automatically start করার জন্য enable করো।

দুটো এক জিনিস নয়।

একসঙ্গে:

```bash
sudo systemctl enable --now nginx
```

এতে enable এবং বর্তমানে start—দুটো করার চেষ্টা করা হয়।

---

# 32. Disable

Boot-এর সময় automatic start বন্ধ:

```bash
sudo systemctl disable nginx
```

এটি সাধারণত current running service বন্ধ করে না।

Current service stop করতে:

```bash
sudo systemctl stop nginx
```

---

# 33. `systemctl is-active`

```bash
systemctl is-active nginx
```

Output হতে পারে:

```text
active
```

---

# 34. `systemctl is-enabled`

```bash
systemctl is-enabled nginx
```

Output:

```text
enabled
```

এটি boot-time enablement status সম্পর্কে জানায়।

---

# 35. Service Logs

Service সমস্যা হলে:

```bash
journalctl
```

systemd journal-এর logs দেখতে ব্যবহার করা হয়।

Nginx-এর মতো একটি service:

```bash
journalctl -u nginx
```

শেষের logs:

```bash
journalctl -u nginx -n 50
```

Real-time:

```bash
journalctl -u nginx -f
```

---

# 36. `journalctl -b`

Current boot-এর logs:

```bash
journalctl -b
```

Previous boot-এর logs দেখতে system configuration অনুযায়ী:

```bash
journalctl -b -1
```

---

# 37. Service Troubleshooting

ধরো nginx start হচ্ছে না।

প্রথমে:

```bash
systemctl status nginx
```

তারপর:

```bash
journalctl -u nginx -n 50
```

তারপর error অনুযায়ী investigate।

Concept:

```text
Service failed
     ↓
systemctl status
     ↓
journalctl
     ↓
Identify error
     ↓
Fix cause
     ↓
Restart/reload
     ↓
Verify
```

---

# 38. Example — Port Already in Use

ধরো nginx start করতে গিয়ে error:

```text
Address already in use
```

কোন process port ব্যবহার করছে দেখতে:

```bash
sudo ss -ltnp
```

অথবা নির্দিষ্ট port:

```bash
sudo ss -ltnp | grep :80
```

তারপর process identify করে root cause investigate করবে।

**Blindly process kill করা উচিত নয়।**

---

# 39. `systemctl list-units`

Active systemd units দেখতে:

```bash
systemctl list-units
```

Services:

```bash
systemctl list-units --type=service
```

---

# 40. `systemctl list-unit-files`

Configured unit files এবং enabled/disabled status:

```bash
systemctl list-unit-files --type=service
```

---

# 🔥 Real-World Scenario

ধরো একটি web server কাজ করছে না।

### Step 1 — Service status

```bash
sudo systemctl status nginx
```

### Step 2 — Logs

```bash
sudo journalctl -u nginx -n 50
```

### Step 3 — Port check

```bash
sudo ss -ltnp | grep :80
```

### Step 4 — Configuration test

Nginx হলে:

```bash
sudo nginx -t
```

### Step 5 — Fix configuration

তারপর:

```bash
sudo systemctl reload nginx
```

অথবা প্রয়োজন অনুযায়ী:

```bash
sudo systemctl restart nginx
```

### Step 6 — Verify

```bash
sudo systemctl status nginx
```

---

# 🚨 Level 5 Common Beginner Mistakes

### Mistake 1

সব process-এ:

```bash
kill -9 PID
```

ব্যবহার করা।

❌ প্রথমে সাধারণত graceful termination চেষ্টা করা ভালো।

---

### Mistake 2

`start` আর `enable` একই ভাবা।

```text
start  → এখন চালাও
enable → boot-এ automatically চালানোর configuration
```

---

### Mistake 3

`disable` মানে service এখনই stop হবে ভাবা।

❌ `disable` সাধারণত boot-time automatic start বন্ধ করে।

---

### Mistake 4

`Ctrl+C` এবং `Ctrl+Z` একই ভাবা।

```text
Ctrl+C → interrupt
Ctrl+Z → suspend/stop foreground job
```

---

### Mistake 5

`ps` আর `top` একই ভাবা।

```text
ps  → process-এর snapshot
top → continuously updating process monitor
```

---

### Mistake 6

Service fail করলে সঙ্গে সঙ্গে restart করা।

আগে:

```bash
systemctl status service
journalctl -u service
```

দিয়ে **কারণ** বোঝার চেষ্টা করা উচিত।

---

# 🧠 Level 5 Interview Questions

### Q1. What is a process?

A process is a running instance of a program.

### Q2. What is PID?

PID is the unique process identifier assigned to a process.

### Q3. What is PPID?

PPID is the process ID of a process's parent.

### Q4. How do you list processes?

Common commands:

```bash
ps aux
ps -ef
```

### Q5. What is the difference between `ps` and `top`?

`ps` generally provides a snapshot of processes; `top` provides an interactive, continuously updating view.

### Q6. What is PID 1?

On modern systemd-based Linux systems, PID 1 is normally `systemd`, the initial userspace process and service manager.

### Q7. What is SIGTERM?

SIGTERM is a termination request signal that allows a process an opportunity to perform cleanup.

### Q8. What is SIGKILL?

SIGKILL forcibly terminates a process and cannot be caught, blocked, or ignored by the target process.

### Q9. Difference between SIGTERM and SIGKILL?

```text
SIGTERM → graceful termination request
SIGKILL → forceful termination
```

### Q10. What does `Ctrl+C` send?

Typically `SIGINT`.

---

# 🔥 Advanced Interview Questions

### Q11. Difference between `start` and `enable`?

```text
start
→ start service now

enable
→ configure service to start automatically at boot
```

---

### Q12. Difference between `restart` and `reload`?

```text
restart
→ stop/start the service

reload
→ ask service to reload configuration without a full restart, if supported
```

---

### Q13. How do you check whether a service is running?

```bash
systemctl status nginx
```

or:

```bash
systemctl is-active nginx
```

---

### Q14. How do you find why a service failed?

Common first steps:

```bash
systemctl status nginx
journalctl -u nginx
```

Then investigate the specific error.

---

### Q15. How do you find which process is listening on a port?

```bash
sudo ss -ltnp
```

For port 80:

```bash
sudo ss -ltnp | grep :80
```

---

### Q16. What is a zombie process?

A terminated child process whose parent has not yet collected its exit status, leaving a process-table entry.

---

### Q17. What is a background process?

A process running without occupying the shell's foreground interaction, commonly started using `&` or shell job control.

---

### Q18. What is `systemd`?

`systemd` is a system and service manager used by many modern Linux distributions. It commonly runs as PID 1 and manages services, targets, dependencies, and related system initialization.

---

# 🧪 Level 5 Hands-on Lab

নিজে চালাও:

### Process

```bash
sleep 300 &
```

তারপর:

```bash
jobs
```

PID বের করতে:

```bash
pgrep sleep
```

Process দেখো:

```bash
ps -ef | grep sleep
```

তারপর graceful terminate:

```bash
kill PID
```

`PID`-এর জায়গায় actual PID বসাবে।

---

### Job Control

```bash
sleep 200
```

তারপর:

```text
Ctrl + Z
```

তারপর:

```bash
jobs
```

Background-এ continue:

```bash
bg
```

আবার foreground:

```bash
fg
```

---

### Service Practice

Ubuntu/Debian-এ SSH service-এর status:

```bash
systemctl status ssh
```

কোনো service পরিবর্তন করার আগে তার নাম এবং বর্তমান status বুঝে নাও।

---

# 🎯 Level 5 Mastery Checklist

```text
✓ Process
✓ PID
✓ PPID
✓ PID 1
✓ ps
✓ ps aux
✓ ps -ef
✓ pgrep
✓ top
✓ htop
✓ Process states
✓ Zombie
✓ Signals
✓ SIGTERM
✓ SIGKILL
✓ SIGINT
✓ kill
✓ jobs
✓ bg
✓ fg
✓ Ctrl+C
✓ Ctrl+Z
✓ Background process
✓ systemd
✓ systemctl
✓ start
✓ stop
✓ restart
✓ reload
✓ enable
✓ disable
✓ status
✓ journalctl
✓ Service troubleshooting
✓ Port/process investigation
```

## 🏆 এখন তোমার Linux foundation

```text
LEVEL 1 → Linux Fundamentals
       ↓
LEVEL 2 → Command Line
       ↓
LEVEL 3 → Users & Permissions
       ↓
LEVEL 4 → Package Management
       ↓
LEVEL 5 → Processes & Services
```

**Level 6-এ** আমরা যাব **Linux Networking**-এ: IP address, MAC, DNS, TCP/UDP, ports, routing, `ip`, `ping`, `ss`, `curl`, `wget`, `traceroute`, `/etc/hosts`, `/etc/resolv.conf`, SSH এবং networking troubleshooting—সবকিছু example + common mistakes + interview questionsসহ।

---
# 🐧 Linux A–Z — LEVEL 6

## 🌐 Linux Networking: IP, DNS, Ports, TCP/UDP, Routing & SSH

Level 6-এ আমরা Linux networking-এর foundation থেকে troubleshooting পর্যন্ত শিখব। আগের Level 5-এর মতো এখানেও **concept + command + example + beginner mistake + practical lab + interview questions** থাকবে।

---

# 1. Networking আসলে কী?

Networking হলো একাধিক computer/device-এর মধ্যে data আদান-প্রদান করার ব্যবস্থা।

উদাহরণ:

```text
Your PC
   |
   | Wi-Fi
   ↓
Router
   |
   ↓
Internet
   |
   ↓
Google Server
```

যখন তুমি browser-এ:

```text
https://google.com
```

লিখো, তখন তোমার computer-এর network stack বিভিন্ন ধাপে কাজ করে:

```text
Domain name
    ↓
DNS
    ↓
IP address
    ↓
Routing
    ↓
TCP/UDP
    ↓
Port
    ↓
Server
```

---

# 2. IP Address কী?

IP address হলো network-এ একটি device/interface-কে identify করার address।

IPv4 example:

```text
192.168.1.10
```

আরেকটি:

```text
10.0.0.25
```

IPv4-এর চারটি অংশ থাকে:

```text
192 . 168 . 1 . 10
```

প্রতিটি অংশ 0–255 পর্যন্ত হতে পারে।

---

# 3. Private IP vs Public IP

## Private IP

Local network-এর ভিতরে ব্যবহৃত হয়।

Common private ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Example:

```text
192.168.1.20
```

বাসার Wi-Fi network-এ এমন IP দেখা খুব common।

## Public IP

Internet-এ externally reachable address হিসেবে ব্যবহৃত হতে পারে।

Example:

```text
203.x.x.x
```

একটি important concept:

```text
Private IP
   ↓
Router/NAT
   ↓
Public IP
   ↓
Internet
```

---

# 4. Linux-এ নিজের IP দেখবে কীভাবে?

সবচেয়ে important command:

```bash
ip addr
```

সংক্ষেপে:

```bash
ip a
```

Example output-এর অংশ:

```text
2: eth0:
    inet 192.168.1.20/24
```

এখানে:

```text
192.168.1.20
```

হলো IP address।

আর:

```text
/24
```

হলো CIDR prefix।

---

# 5. Network Interface কী?

Computer-এর network connection-কে interface হিসেবে দেখা যায়।

উদাহরণ:

```text
eth0
ens33
enp0s3
wlan0
```

Modern Linux-এ interface name অনেক সময় এমন হয়:

```text
enp0s3
ens33
```

Wi-Fi interface কখনও:

```text
wlan0
```

হতে পারে, যদিও naming distribution/system অনুযায়ী আলাদা হতে পারে।

দেখতে:

```bash
ip link
```

অথবা:

```bash
ip addr
```

---

# 6. MAC Address কী?

MAC address হলো network interface-এর Layer-2 address।

Example:

```text
52:54:00:12:34:56
```

দেখতে:

```bash
ip link
```

Output-এ:

```text
link/ether 52:54:00:12:34:56
```

দেখতে পারো।

### IP বনাম MAC

| বিষয়               | IP                         | MAC                                                                |
| ------------------ | -------------------------- | ------------------------------------------------------------------ |
| Layer              | Network                    | Data Link                                                          |
| Example            | `192.168.1.20`             | `52:54:00:12:34:56`                                                |
| মূল কাজ            | Network addressing/routing | Local network interface identification                             |
| পরিবর্তন হতে পারে? | হ্যাঁ                      | Interface-level address; software দিয়ে পরিবর্তন/override করা সম্ভব |

Beginner হিসেবে মনে রাখো:

```text
MAC → local network level
IP  → network/routing level
```

---

# 7. CIDR `/24` কী?

এই অংশটা খুব important।

ধরো:

```text
192.168.1.20/24
```

এখানে `/24` বলে IP-এর প্রথম 24 bits network portion-এর জন্য ব্যবহৃত হচ্ছে।

সাধারণভাবে:

```text
/8
/16
/24
/32
```

দেখবে।

### `/24`

সাধারণ IPv4 subnet mask:

```text
255.255.255.0
```

একটি typical `/24` network:

```text
192.168.1.0/24
```

এর address range:

```text
192.168.1.0
       ↓
192.168.1.255
```

Traditional IPv4 subnetting-এ প্রথম address network address এবং শেষটি broadcast address হিসেবে ব্যবহৃত হয়।

---

# 8. Default Gateway কী?

তোমার computer যদি নিজের local network-এর বাইরে কোনো destination-এ যেতে চায়, সাধারণত তাকে একটি router-এর মাধ্যমে যেতে হয়।

এই router-এর address-কে সাধারণত **default gateway** বলা হয়।

Example:

```text
PC
192.168.1.20
      |
      ↓
Gateway
192.168.1.1
      |
      ↓
Internet
```

দেখতে:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

এখানে:

```text
default
```

মানে অন্যান্য matching route না থাকলে এই route ব্যবহার করা হবে।

---

# 9. Routing কী?

Routing হলো packet কোন পথ দিয়ে যাবে সেটা নির্ধারণ করা।

Command:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.20
```

এখানে Linux জানে:

```text
192.168.1.0/24
```

local network।

আর:

```text
default via 192.168.1.1
```

অন্য destination-এর জন্য default gateway।

---

# 10. `ping` কী?

`ping` network connectivity test করতে ব্যবহৃত হয়।

Example:

```bash
ping 8.8.8.8
```

অথবা:

```bash
ping google.com
```

বন্ধ করতে:

```text
Ctrl + C
```

Example:

```text
64 bytes from 8.8.8.8: ...
```

মানে response পাওয়া গেছে।

### Important

`ping` সফল না হলেই যে internet অবশ্যই completely down—এটা বলা যায় না।

কারণ firewall বা network policy ICMP block করতে পারে।

---

# 11. `ping` দিয়ে troubleshooting

এই sequence খুব useful:

```bash
ping 127.0.0.1
```

তারপর:

```bash
ping <gateway-ip>
```

তারপর:

```bash
ping 8.8.8.8
```

তারপর:

```bash
ping google.com
```

ধরো:

```text
127.0.0.1       → কাজ করে
gateway         → কাজ করে
8.8.8.8         → কাজ করে
google.com      → কাজ করে না
```

তাহলে DNS problem-এর সম্ভাবনা আছে।

---

# 12. DNS কী?

DNS = **Domain Name System**

মানুষ মনে রাখতে সহজ:

```text
google.com
```

computer network-এ কাজ করে:

```text
IP address
```

DNS এই নামকে IP address-এ resolve করতে সাহায্য করে।

Conceptually:

```text
google.com
    ↓
DNS
    ↓
IP address
```

---

# 13. DNS check করার commands

### `getent`

```bash
getent hosts google.com
```

### `dig`

```bash
dig google.com
```

### `nslookup`

```bash
nslookup google.com
```

`dig` DNS troubleshooting-এর জন্য বিশেষভাবে useful।

---

# 14. `/etc/hosts`

Linux-এ local hostname mapping-এর জন্য:

```text
/etc/hosts
```

দেখতে:

```bash
cat /etc/hosts
```

Example:

```text
127.0.0.1 localhost
192.168.1.50 myserver
```

তাহলে:

```text
myserver
```

এর জন্য local mapping ব্যবহার করা যেতে পারে।

---

# 15. `/etc/resolv.conf`

DNS resolver configuration-এর সঙ্গে সম্পর্কিত:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 192.168.1.1
```

তবে modern Linux systems-এ `/etc/resolv.conf` অনেক সময় NetworkManager, systemd-resolved বা অন্য network management system দ্বারা managed হতে পারে।

তাই **ইচ্ছেমতো edit করা beginner-এর জন্য ভালো practice নয়।**

---

# 16. TCP কী?

TCP = Transmission Control Protocol

TCP connection-oriented।

Concept:

```text
Client
  |
  | connection establish
  ↓
Server
  |
  | data
  ↓
Client
```

TCP সাধারণত reliability-এর জন্য ব্যবহৃত হয়।

উদাহরণ:

```text
HTTP/HTTPS
SSH
```

---

# 17. UDP কী?

UDP = User Datagram Protocol

UDP connection-oriented TCP-এর মতো handshake/reliability mechanism ব্যবহার করে না।

এটি সাধারণত কম overhead-এর জন্য ব্যবহৃত হয়।

উদাহরণ:

```text
DNS queries
streaming/real-time applications-এর কিছু ক্ষেত্রে
```

তবে কোন application TCP/UDP ব্যবহার করবে সেটা protocol/application-এর design-এর ওপর নির্ভর করে।

---

# 18. TCP vs UDP

| TCP                          | UDP                                                   |
| ---------------------------- | ----------------------------------------------------- |
| Connection-oriented          | Connectionless                                        |
| Reliable delivery mechanisms | Delivery guarantee নেই                                |
| Ordering support             | Ordering guarantee নেই                                |
| বেশি overhead                | কম overhead                                           |
| SSH, HTTPS                   | DNS-এর অনেক query, real-time applications-এর কিছু অংশ |

Interview-এ খুব common:

> TCP reliable, UDP lightweight কিন্তু delivery guarantee দেয় না।

---

# 19. Port কী?

একটি IP address একটি host-কে identify করতে সাহায্য করে।

Port একটি host-এর ভিতরে নির্দিষ্ট network service/application-এর endpoint identify করতে সাহায্য করে।

Example:

```text
192.168.1.20:22
```

এখানে:

```text
192.168.1.20 → IP
22            → Port
```

Common ports:

| Port | সাধারণ ব্যবহার |
| ---: | -------------- |
|   22 | SSH            |
|   53 | DNS            |
|   80 | HTTP           |
|  443 | HTTPS          |
|   25 | SMTP           |
| 3306 | MySQL          |
| 5432 | PostgreSQL     |

**Port number alone কোনো service নিশ্চিত করে না; actual application configuration আলাদা হতে পারে।**

---

# 20. Listening Port কী?

ধরো SSH server চলছে।

তাহলে server কোনো interface-এ port 22-এ listen করতে পারে।

দেখতে:

```bash
ss -ltn
```

Options:

```text
-l → listening
-t → TCP
-n → numeric
```

আর process-সহ দেখতে:

```bash
sudo ss -ltnp
```

Example:

```text
LISTEN 0 128 0.0.0.0:22
```

মানে service IPv4-এর available interfaces-এ port 22-এ listen করছে।

---

# 21. `ss` — খুব গুরুত্বপূর্ণ command

আগের Level 5-এ আমরা `ss` দেখেছি। Networking Level-এ এটাকে আরও গভীরভাবে ব্যবহার করব।

সব TCP listening:

```bash
ss -ltn
```

সব UDP listening:

```bash
ss -lun
```

সব listening socket:

```bash
ss -lntup
```

Established connections:

```bash
ss -tn
```

একটি specific port:

```bash
ss -ltn | grep ':22'
```

---

# 22. `localhost` কী?

```text
localhost
```

সাধারণত নিজের computer-কে refer করে।

IPv4:

```text
127.0.0.1
```

IPv6:

```text
::1
```

Example:

```bash
ping localhost
```

---

# 23. `0.0.0.0` কী?

যখন কোনো server:

```text
0.0.0.0:8080
```

এ listen করে, সাধারণভাবে এর অর্থ হলো IPv4-এর available local interfaces-এ ওই port-এ listen করা।

অন্যদিকে:

```text
127.0.0.1:8080
```

মানে service শুধু local machine-এর loopback interface-এ accessible।

### খুব common troubleshooting problem

Application:

```text
127.0.0.1:8080
```

এ listen করছে।

অন্য computer থেকে access করতে গেলে কাজ করছে না।

কারণ application network-এর অন্য interface-এ listen করছে না।

---

# 24. `curl` কী?

`curl` network requests করার খুব powerful command।

Example:

```bash
curl https://example.com
```

শুধু headers:

```bash
curl -I https://example.com
```

Verbose networking information:

```bash
curl -v https://example.com
```

Specific URL:

```bash
curl https://example.com/api
```

### Real-world use

Web server troubleshooting-এ:

```bash
curl -I http://localhost
```

যদি response আসে:

```text
HTTP/1.1 200 OK
```

তাহলে HTTP service response দিচ্ছে।

---

# 25. `wget`

`wget` file download-এর জন্য widely used।

Example:

```bash
wget https://example.com/file.zip
```

Difference সহজভাবে:

```text
curl → requests/API/testing/output-এর জন্য খুব useful
wget → downloading-এর জন্য খুব convenient
```

দুটোর capability overlap করে।

---

# 26. `traceroute`

Network packet destination-এর দিকে কোন কোন routing hop অতিক্রম করছে তা দেখতে ব্যবহার করা হয়।

```bash
traceroute google.com
```

কিছু Linux system-এ:

```bash
tracepath google.com
```

ব্যবহার করা যায়।

Example conceptual output:

```text
1   router
2   ISP router
3   ...
4   destination
```

সব hop response দেবে এমন নয়; firewall/routing policy-এর কারণে কিছু জায়গায় `*` দেখা যেতে পারে।

---

# 27. Neighbor/ARP information

Local network-এ IP-to-link-layer neighbor information দেখতে:

```bash
ip neigh
```

Example:

```text
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

এখানে দেখা যাচ্ছে:

```text
IP → MAC
```

local network neighbor information হিসেবে।

---

# 28. SSH কী?

SSH = **Secure Shell**

Remote Linux machine-এ securely command-line access করার জন্য ব্যবহৃত হয়।

Concept:

```text
Your PC
   |
   | SSH
   ↓
Remote Linux Server
```

Basic form:

```bash
ssh username@server-ip
```

Example:

```bash
ssh rahim@192.168.1.50
```

Server-এর hostname দিয়েও:

```bash
ssh rahim@server.example.com
```

---

# 29. SSH-এর default port

সাধারণত:

```text
22
```

তাই:

```bash
ssh user@server
```

সাধারণ configuration-এ port 22 ব্যবহার করতে পারে।

Custom port হলে:

```bash
ssh -p 2222 user@server
```

---

# 30. SSH troubleshooting

ধরো:

```bash
ssh user@192.168.1.50
```

কাজ করছে না।

একসাথে random commands চালাবে না।

Step-by-step:

### Step 1 — IP reachable?

```bash
ping 192.168.1.50
```

### Step 2 — Port reachable/listening?

নিজের authorized server-এ:

```bash
ss -ltn
```

Server-এ SSH service status:

```bash
systemctl status ssh
```

কিছু distro-তে service name:

```bash
systemctl status sshd
```

### Step 3 — SSH client verbose mode

```bash
ssh -v user@192.168.1.50
```

এতে connection-এর বিভিন্ন stage সম্পর্কে diagnostic information পাওয়া যায়।

---

# 31. Networking Troubleshooting-এর Golden Flow ⭐

এই flow interview এবং real Linux administration—দুটোর জন্যই খুব useful।

ধরো:

> “Server internet access করতে পারছে না।”

### Step 1 — Interface আছে?

```bash
ip link
```

### Step 2 — IP address আছে?

```bash
ip addr
```

### Step 3 — Route আছে?

```bash
ip route
```

### Step 4 — Gateway reachable?

```bash
ping <gateway>
```

### Step 5 — Internet IP reachable?

```bash
ping 8.8.8.8
```

### Step 6 — DNS কাজ করছে?

```bash
getent hosts google.com
```

অথবা:

```bash
dig google.com
```

### Step 7 — HTTP/HTTPS কাজ করছে?

```bash
curl -I https://example.com
```

এটা troubleshooting-এর একটি logical sequence।

---

# 32. একটি Real Scenario

ধরো:

```bash
ping google.com
```

fail করছে।

প্রথমে:

```bash
ping 8.8.8.8
```

যদি এটা কাজ করে:

```text
Network connectivity → probably okay
DNS → suspicious
```

তারপর:

```bash
getent hosts google.com
```

যদি DNS resolution fail করে, DNS configuration/resolver নিয়ে investigate করবে।

---

# 33. আরেকটি Scenario

Server-এ application চলছে।

```bash
systemctl status myapp
```

বলছে running।

কিন্তু browser থেকে access হচ্ছে না।

Check:

```bash
ss -ltnp
```

ধরো:

```text
127.0.0.1:8080
```

এখন বুঝতে পারো application শুধু localhost-এ listen করছে।

যদি application-এর configuration অনুযায়ী remote access প্রয়োজন হয়, তাহলে তার bind/listen configuration এবং firewall/network policy যাচাই করতে হবে।

---

# 34. Network Configuration নিয়ে Beginner Mistakes 🚨

### Mistake 1

শুধু:

```bash
ping google.com
```

দিয়ে পুরো networking diagnose করা।

❌ ভুল।

কারণ DNS, ICMP, routing, HTTP—সব আলাদা layer/part।

---

### Mistake 2

`127.0.0.1`-কে নিজের LAN IP মনে করা।

❌ ভুল।

```text
127.0.0.1 → loopback
192.168.x.x → typical private LAN address
```

---

### Mistake 3

IP address আছে মানেই Internet আছে ভাবা।

❌ ভুল।

IP থাকতে পারে কিন্তু:

```text
gateway missing
route missing
DNS broken
firewall issue
```

হতে পারে।

---

### Mistake 4

Port আর IP-কে একই জিনিস ভাবা।

```text
IP   → host/network address
Port → service/application endpoint
```

---

### Mistake 5

`ping` fail = server down ধরে নেওয়া।

❌ সবসময় নয়।

ICMP block হতে পারে।

---

### Mistake 6

`/etc/resolv.conf` blindly edit করা।

❌ Modern Linux-এ এটি অন্য service দ্বারা managed হতে পারে।

---

### Mistake 7

`0.0.0.0`-কে একটি real remote IP ভাবা।

❌ এটি সাধারণত listen/bind context-এ special wildcard address।

---

# 35. Level 6-এর Most Important Commands

| Command        | কাজ                           |
| -------------- | ----------------------------- |
| `ip addr`      | IP/interface information      |
| `ip link`      | network interfaces            |
| `ip route`     | routing table                 |
| `ip neigh`     | neighbor information          |
| `ping`         | connectivity test             |
| `ss`           | sockets/connections/listeners |
| `curl`         | HTTP/network requests         |
| `wget`         | downloads                     |
| `dig`          | DNS lookup                    |
| `nslookup`     | DNS lookup                    |
| `getent hosts` | hostname resolution           |
| `traceroute`   | network path                  |
| `tracepath`    | network path                  |
| `hostname`     | hostname information          |
| `ssh`          | remote secure shell           |

---

# 🧪 Level 6 Hands-on Lab

নিজের Linux machine/VM-এ চালাতে পারো:

### Lab 1 — Interface

```bash
ip link
```

খুঁজে বের করো:

* interface name
* UP/DOWN status

---

### Lab 2 — IP

```bash
ip addr
```

খুঁজে বের করো:

```text
IPv4 address
CIDR prefix
```

---

### Lab 3 — Route

```bash
ip route
```

খুঁজে বের করো:

```text
default gateway
```

---

### Lab 4 — Local connectivity

```bash
ping 127.0.0.1
```

তারপর:

```bash
ping 8.8.8.8
```

---

### Lab 5 — DNS

```bash
getent hosts google.com
```

তারপর:

```bash
dig google.com
```

---

### Lab 6 — Listening ports

```bash
ss -lnt
```

তারপর:

```bash
sudo ss -lntp
```

কোন services listen করছে লক্ষ্য করো।

---

### Lab 7 — HTTP

```bash
curl -I https://example.com
```

তারপর:

```bash
curl -v https://example.com
```

Verbose output-এর মধ্যে connection/DNS/TLS/HTTP সম্পর্কিত তথ্য লক্ষ্য করো।

---

# 🎯 Level 6 Interview Questions

## Beginner

### 1. IP address কী?

Network-এ host/interface address করার জন্য ব্যবহৃত logical address।

### 2. Private IP কী?

Local/private networks-এর জন্য reserved address ranges-এর IP।

### 3. MAC address কী?

Local network/data-link level-এ network interface-এর address।

### 4. Default gateway কী?

Local network-এর বাইরে destination-এ যাওয়ার জন্য সাধারণত যে router ব্যবহার করা হয়।

### 5. DNS কী?

Domain/hostname-কে IP address-এর মতো network information-এ resolve করার system।

### 6. Port কী?

একটি host-এর নির্দিষ্ট network service/application endpoint identify করতে ব্যবহৃত number।

### 7. TCP আর UDP-এর difference কী?

TCP connection-oriented এবং reliable delivery mechanisms দেয়; UDP connectionless এবং কম overhead-এর।

---

# 🔥 Intermediate Interview Questions

### 8. `/24` কী বোঝায়?

IPv4 CIDR prefix; প্রথম 24 bits network prefix নির্দেশ করে।

### 9. `127.0.0.1` কী?

IPv4 loopback address।

### 10. `0.0.0.0` কী?

Context অনুযায়ী বিশেষ wildcard/unspecified address; server binding-এর ক্ষেত্রে available IPv4 interfaces-এ listen বোঝাতে ব্যবহৃত হতে পারে।

### 11. `ss` কেন ব্যবহার করি?

Network sockets, listening ports এবং connections inspect করতে।

### 12. `ip route` কী দেখায়?

Kernel-এর routing table।

### 13. DNS কাজ করছে কি না কীভাবে check করবে?

```bash
getent hosts example.com
```

অথবা:

```bash
dig example.com
```

### 14. `curl` কেন useful?

HTTP/API connectivity এবং server response test করতে।

---

# 💀 Advanced Interview Questions

### 15. IP আছে কিন্তু internet নেই—কী কী check করবে?

Logical sequence:

```text
ip link
↓
ip addr
↓
ip route
↓
gateway connectivity
↓
external IP connectivity
↓
DNS
↓
application protocol
```

---

### 16. `ping 8.8.8.8` কাজ করে কিন্তু `ping google.com` কাজ করে না—সম্ভাব্য কারণ?

**DNS resolution problem** একটি strong possibility।

---

### 17. Application running কিন্তু remote client connect করতে পারছে না—কী check করবে?

```bash
systemctl status service
```

তারপর:

```bash
ss -ltnp
```

বিশেষভাবে দেখবে service কোন address/port-এ listen করছে।

তারপর প্রয়োজন অনুযায়ী firewall এবং network path check করবে।

---

### 18. `127.0.0.1:8080` এবং `0.0.0.0:8080`-এর practical difference কী?

```text
127.0.0.1:8080
→ local machine-এর loopback-এ listen

0.0.0.0:8080
→ IPv4 interfaces-এর wildcard bind; সাধারণত multiple interfaces দিয়ে connection গ্রহণ করতে পারে
```

---

### 19. `ss -lntp`-এর প্রতিটি অংশ কী?

```text
-l → listening
-n → numeric
-t → TCP
-p → process information
```

---

### 20. DNS আর routing-এর difference কী?

```text
DNS
→ "এই hostname-এর network address কী?"

Routing
→ "এই destination-এ packet কোন path/interface/gateway দিয়ে যাবে?"
```

---

# 🧠 Level 6 Final Challenge

ধরো interview-এ interviewer বলল:

> **“একটি Linux server-এ application চলছে, কিন্তু user website access করতে পারছে না। তুমি কীভাবে troubleshoot করবে?”**

একজন ভালো Linux administrator এভাবে চিন্তা করবে:

```text
1. Is the interface up?
        ↓
   ip link

2. Does it have an IP?
        ↓
   ip addr

3. Is routing correct?
        ↓
   ip route

4. Is the service running?
        ↓
   systemctl status

5. Is the expected port listening?
        ↓
   ss -lntp

6. Is it listening on the correct address?
        ↓
   127.0.0.1 vs 0.0.0.0 / specific IP

7. Can the server reach the network?
        ↓
   ping / curl

8. Is DNS working?
        ↓
   getent / dig

9. Is firewall/network policy blocking it?
        ↓
   inspect relevant firewall/network configuration

10. Check application/service logs
        ↓
   journalctl / application logs
```

এটাই Level 6-এর সবচেয়ে গুরুত্বপূর্ণ skill:

> **একটা problem দেখে random command না চালিয়ে layer-by-layer troubleshoot করা।**

---

## 🏆 Level 6 শেষে তোমার যে জিনিসগুলো অবশ্যই জানা উচিত

```text
IP
MAC
CIDR
Subnet
Gateway
Routing
DNS
TCP
UDP
Port
Socket
localhost
127.0.0.1
0.0.0.0
ip
ping
ss
curl
wget
dig
getent
traceroute
SSH
Network troubleshooting
```

**Level 7**-এ গেলে আমরা Linux-এর **Storage & Filesystem** শিখব—`disk`, `partition`, `filesystem`, `mount`, `fstab`, `df`, `du`, `lsblk`, `fdisk`, `blkid`, `LVM`, `inode`, এবং disk-full troubleshooting—সবকিছু example, beginner mistakes, practical lab ও interview questionsসহ।

----
# 🐧 Linux A–Z — LEVEL 7

## 💾 Storage, Disk, Partition, Filesystem, Mount, `fstab`, LVM & Inode

Level 7-এ আমরা Linux-এর **storage system** বুঝব। এটা খুব গুরুত্বপূর্ণ, কারণ Linux server manage করতে গেলে disk space, partitions, filesystems, mounts, permissions এবং disk-full সমস্যাগুলো নিয়মিত troubleshoot করতে হয়।

---

# 1. Storage-এর পুরো Picture

একটা সাধারণ Linux system-কে এভাবে ভাবো:

```text
Physical Disk
     ↓
Partition
     ↓
Filesystem
     ↓
Mount Point
     ↓
Files / Directories
```

উদাহরণ:

```text
/dev/sda
   ↓
/dev/sda1
   ↓
ext4
   ↓
/data
   ↓
/data/file.txt
```

এখানে প্রত্যেকটি জিনিসের আলাদা কাজ আছে।

---

# 2. Disk কী?

Disk হলো storage device।

উদাহরণ:

```text
HDD
SSD
NVMe SSD
Virtual Disk
```

Linux-এ disk সাধারণত এমন নাম পেতে পারে:

```text
/dev/sda
/dev/sdb
```

NVMe disk:

```text
/dev/nvme0n1
```

---

# 3. Block Device কী?

Linux-এ storage device সাধারণত `/dev` directory-এর মধ্যে দেখা যায়।

```bash
ls /dev
```

Disk example:

```text
/dev/sda
/dev/sdb
/dev/nvme0n1
```

Partition example:

```text
/dev/sda1
/dev/sda2
```

NVMe:

```text
/dev/nvme0n1p1
/dev/nvme0n1p2
```

### Beginner mistake 🚨

```text
/dev/sda
```

এবং

```text
/dev/sda1
```

এক জিনিস নয়।

```text
/dev/sda
    ↓
whole disk

/dev/sda1
    ↓
partition
```

---

# 4. `lsblk` — সবচেয়ে Important Storage Command ⭐

প্রথমেই শিখবে:

```bash
lsblk
```

আরও useful:

```bash
lsblk -f
```

Example:

```text
NAME   FSTYPE FSVER LABEL UUID                                 MOUNTPOINT
sda
├─sda1 ext4         ...   ...                                  /
└─sda2 ext4         ...   ...                                  /data
```

এখানে দেখতে পারছো:

* disk
* partition
* filesystem
* UUID
* mount point

### Interview tip

যদি interviewer জিজ্ঞেস করে:

> “Linux-এ disk structure quickly কীভাবে দেখবে?”

একটি excellent starting command:

```bash
lsblk
```

---

# 5. Partition কী?

একটি physical/virtual disk-কে logical অংশে ভাগ করাকে partitioning বলা যায়।

ধরো:

```text
1 TB Disk
│
├── 100 GB → /
├── 200 GB → /home
└── 700 GB → /data
```

Linux-এ:

```text
/dev/sda1
/dev/sda2
/dev/sda3
```

হতে পারে।

---

# 6. Filesystem কী?

Partition-এর raw storage-এর ওপর files/directories manage করার জন্য filesystem প্রয়োজন।

Common Linux filesystems:

```text
ext4
XFS
Btrfs
```

Ubuntu-তে `ext4` খুব common।

Filesystem-এর কাজ:

```text
File
Directory
Metadata
Permissions
Timestamps
Storage blocks
```

এসব manage করা।

---

# 7. `ext4`

`ext4` = Extended File System 4।

একটি widely used Linux filesystem।

Example:

```text
/dev/sda1
    ↓
ext4
    ↓
/
```

Check করতে:

```bash
lsblk -f
```

অথবা:

```bash
df -T
```

---

# 8. `df` — Disk Space Check

সবচেয়ে useful command:

```bash
df
```

Human-readable:

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   30G   18G  63% /
```

এখানে:

```text
Size → total
Used → used
Avail → available
Use% → percentage
Mounted on → কোথায় mounted
```

---

# 9. `df -h` কেন `-h`?

`-h` = human-readable

Without:

```text
52428800
```

Human-readable:

```text
50G
```

তাই সাধারণত:

```bash
df -h
```

ব্যবহার করা convenient।

---

# 10. `du` — কোন directory কত space নিচ্ছে?

`df` এবং `du`-এর difference খুব important।

### `df`

Filesystem কতটা full?

```bash
df -h
```

### `du`

কোন file/directory কত storage ব্যবহার করছে?

```bash
du -sh /var/log
```

Current directory:

```bash
du -sh .
```

Subdirectories:

```bash
du -h --max-depth=1
```

---

# 11. `df` vs `du`

| Command         | Purpose                            |
| --------------- | ---------------------------------- |
| `df -h`         | Filesystem free/used space         |
| `du -sh folder` | Folder কত space ব্যবহার করছে       |
| `du -sh *`      | Current directory-এর items-এর size |

Interview-এ খুব common:

> “Disk full হলে প্রথমে কী করবে?”

```bash
df -h
```

তারপর কোন directory বড় সেটা বের করতে:

```bash
du -sh /*
```

তবে `/proc`, `/sys`, `/dev` ইত্যাদি pseudo-filesystems থাকার কারণে blindly পুরো filesystem-এর `du` analysis না করে relevant directories-এ drill down করা ভালো।

---

# 12. Mount কী?

Linux-এ filesystem-কে directory tree-এর একটি জায়গায় attach করাকে **mount** করা বলে।

ধরো:

```text
/dev/sdb1
     ↓
   /data
```

তাহলে:

```text
/data
```

হলো mount point।

---

# 13. Mount Point কী?

Mount point হলো সেই directory যেখানে filesystem attach করা হয়েছে।

Example:

```text
/dev/sdb1 → /data
```

এখানে:

```text
/data
```

হলো mount point।

---

# 14. `mount` Command

Current mounted filesystems দেখতে:

```bash
mount
```

আরও readable:

```bash
findmnt
```

Specific filesystem:

```bash
findmnt /data
```

এটা খুব useful।

---

# 15. Manual Mount

ধরো:

```text
/dev/sdb1
```

কে:

```text
/data
```

এ mount করতে চাও।

প্রথমে mount point:

```bash
sudo mkdir -p /data
```

তারপর:

```bash
sudo mount /dev/sdb1 /data
```

Check:

```bash
df -h
```

অথবা:

```bash
findmnt /data
```

---

# ⚠️ Important Safety

`mount` শেখার সময় **নিজের VM/lab disk** ব্যবহার করো।

কোন device কী সেটা না জেনে partitioning বা formatting command চালানো উচিত নয়।

---

# 16. Unmount

Unmount:

```bash
sudo umount /data
```

অথবা:

```bash
sudo umount /dev/sdb1
```

### Beginner mistake 🚨

`umount`-এ `n` নেই।

সঠিক:

```bash
umount
```

ভুল:

```bash
unmount
```

---

# 17. “Target is busy” কেন?

যদি:

```bash
sudo umount /data
```

করো এবং:

```text
target is busy
```

এরকম message পাও, তার মানে filesystem-টি এখনও কোনো process/current working directory দ্বারা ব্যবহৃত হতে পারে।

প্রথমে:

```bash
findmnt /data
```

তারপর কোন process ব্যবহার করছে তা investigate করা যায়।

নিজের shell যদি `/data`-এর ভিতরে থাকে:

```bash
cd /
```

তারপর আবার unmount try করা যায়।

---

# 18. `/etc/fstab`

Linux boot হওয়ার সময় কোন filesystem কোথায় mount হবে সেটা configure করার traditional জায়গা:

```text
/etc/fstab
```

দেখতে:

```bash
cat /etc/fstab
```

Example concept:

```text
UUID=xxxx-xxxx   /data   ext4   defaults   0 2
```

এখানে:

```text
UUID
   ↓
device/filesystem identification

/data
   ↓
mount point

ext4
   ↓
filesystem type

defaults
   ↓
mount options
```

---

# 19. UUID কী?

UUID = Universally Unique Identifier.

Filesystem-এর জন্য একটি identifier।

দেখতে:

```bash
blkid
```

Example:

```text
/dev/sda1: UUID="abc123..." TYPE="ext4"
```

UUID ব্যবহার করার সুবিধা হলো device name পরিবর্তিত হলেও identifier stable থাকার সম্ভাবনা বেশি।

---

# 20. `blkid`

Filesystem এবং UUID দেখতে:

```bash
sudo blkid
```

Example:

```text
/dev/sda1: UUID="..." TYPE="ext4"
/dev/sdb1: UUID="..." TYPE="xfs"
```

এটা `fstab` troubleshooting-এ useful।

---

# 21. `fstab`-এ Beginner Mistake 🚨

`/etc/fstab` খুব sensitive configuration file।

একটা ভুল entry boot বা mount সমস্যার কারণ হতে পারে।

তাই edit করার পর:

```bash
sudo mount -a
```

দিয়ে configuration validate করার অভ্যাস useful।

যদি error আসে, reboot করার আগে সেটা ঠিক করো।

---

# 22. `mount -a`

`/etc/fstab`-এর applicable entries mount করার জন্য:

```bash
sudo mount -a
```

এটা production machine-এ ব্যবহার করার আগে `fstab` entry বুঝে নেওয়া জরুরি।

---

# 23. Disk Usage Troubleshooting

ধরো:

```bash
df -h
```

দেখাচ্ছে:

```text
Use% = 95%
```

প্রথম question:

> “কোন filesystem full?”

তারপর:

```bash
du -sh /var/*
```

ধরো `/var/log` বড়।

তাহলে:

```bash
du -sh /var/log/*
```

এভাবে gradually narrow down করবে।

---

# 24. Disk Full কিন্তু `du`-তে space দেখা যাচ্ছে না?

এটা একটি classic Linux interview question।

Possible কারণ:

**কোনো deleted file এখনও একটি running process open করে রেখেছে।**

File directory থেকে delete হয়ে গেছে, কিন্তু process file descriptor ধরে রেখেছে।

তখন:

```text
df
```

অনেক usage দেখাতে পারে, কিন্তু:

```text
du
```

তার corresponding file দেখতে নাও পারে।

এই ধরনের case investigate করতে:

```bash
sudo lsof +L1
```

ব্যবহার করা যায়, যদি `lsof` installed থাকে।

---

# 25. Inode কী?

এটা খুব important advanced concept।

Filesystem শুধু file-এর content store করে না।

File-এর metadata-এর জন্য inode ব্যবহৃত হয়।

একটি inode-এর মধ্যে সাধারণত থাকে:

```text
file type
permissions
owner
group
timestamps
size-related metadata
pointers to data blocks
```

সহ বিভিন্ন metadata।

---

# 26. Inode Exhaustion

ধরো disk-এ অনেক ছোট ছোট file তৈরি হয়েছে।

Storage space হয়তো আছে:

```text
20 GB free
```

কিন্তু inode শেষ।

তখন নতুন file তৈরি করা যাবে না।

Check:

```bash
df -i
```

Example:

```text
Filesystem      Inodes   IUsed   IFree IUse%
/dev/sda1       1000000 1000000      0 100%
```

এখানে storage free থাকলেও inode exhausted।

---

# 27. `df -h` vs `df -i`

```text
df -h
↓
storage blocks/space

df -i
↓
inodes
```

Interview question:

> “Disk space free আছে, কিন্তু নতুন file create হচ্ছে না—কী check করবে?”

Answer:

```bash
df -i
```

এবং inode exhaustion-এর possibility investigate করবে।

---

# 28. Hard Link-এর সঙ্গে Inode

Hard link-এর ক্ষেত্রে একাধিক filename একই inode-এর দিকে point করতে পারে।

Concept:

```text
file1
  \
   → inode → data
  /
file2
```

তাই:

```bash
ls -li
```

ব্যবহার করে inode number দেখতে পারো।

Example:

```text
12345 -rw-r--r-- file1
12345 -rw-r--r-- file2
```

দুই filename একই inode number দেখাতে পারে।

---

# 29. Symbolic Link বনাম Hard Link

### Symbolic link

```bash
ln -s original.txt link.txt
```

Concept:

```text
link.txt
   ↓
original.txt
```

### Hard link

```bash
ln original.txt hardlink.txt
```

Concept:

```text
original.txt ─┐
              ├→ same inode → data
hardlink.txt ─┘
```

---

# 30. Symbolic Link-এর Important Difference

যদি original file delete হয়:

```text
original.txt → deleted
```

symbolic link সাধারণত broken হয়ে যায়।

Hard link-এর ক্ষেত্রে data inode-এর মাধ্যমে accessible থাকতে পারে যতক্ষণ অন্তত একটি hard link/reference থাকে।

---

# 31. `ls -li`

Inode number দেখতে:

```bash
ls -li
```

Example:

```text
12345 -rw-r--r-- 2 user user 100 file.txt
```

এখানে:

```text
12345
```

হলো inode number।

---

# 32. LVM কী?

LVM = **Logical Volume Manager**

Linux server-এ flexible storage management-এর জন্য খুব useful।

Traditional partitioning:

```text
Disk
 ↓
Partition
 ↓
Filesystem
```

LVM:

```text
Physical Disk
     ↓
Physical Volume (PV)
     ↓
Volume Group (VG)
     ↓
Logical Volume (LV)
     ↓
Filesystem
     ↓
Mount Point
```

এটা খুব important diagram।

---

# 33. Physical Volume — PV

LVM-এর জন্য disk/partition প্রস্তুত করলে সেটা Physical Volume হতে পারে।

Concept:

```text
/dev/sdb1
    ↓
PV
```

Check:

```bash
pvs
```

---

# 34. Volume Group — VG

এক বা একাধিক PV-কে pool হিসেবে group করা যায়।

```text
PV1 ─┐
     ├──→ VG
PV2 ─┘
```

Check:

```bash
vgs
```

---

# 35. Logical Volume — LV

VG-এর storage থেকে Logical Volume তৈরি করা যায়।

```text
VG
 ↓
LV
 ↓
Filesystem
 ↓
/data
```

Check:

```bash
lvs
```

---

# 36. LVM কেন ব্যবহার করব?

ধরো:

```text
Disk = 1 TB
```

তুমি flexible storage চাইছো।

LVM ব্যবহার করলে logical volumes manage করা সহজ হয় এবং storage pool-এর মধ্যে allocation/resizing করা যায়।

Common server use cases:

```text
/var
/home
/data
```

আলাদা logical volumes হিসেবে রাখা।

---

# 37. LVM-এর তিনটি Command

মনে রাখো:

```bash
pvs
vgs
lvs
```

মানে:

```text
pvs → Physical Volumes
vgs → Volume Groups
lvs → Logical Volumes
```

Interview-এর জন্য অত্যন্ত important।

---

# 38. Storage Troubleshooting Flow ⭐

একজন Linux administrator যদি বলে:

> “Server-এর disk full।”

তুমি:

### Step 1

```bash
df -h
```

### Step 2

কোন filesystem full সেটা identify।

### Step 3

Relevant directory inspect:

```bash
du -sh /var/*
```

### Step 4

আরও গভীরে:

```bash
du -sh /var/log/*
```

### Step 5

Inode check:

```bash
df -i
```

### Step 6

Deleted-open files সন্দেহ হলে:

```bash
sudo lsof +L1
```

এভাবে problem isolate করবে।

---

# 🚨 Level 7 Beginner Mistakes

### Mistake 1 — `df` আর `du` একই মনে করা

না।

```text
df → filesystem usage
du → file/directory usage
```

---

### Mistake 2 — `/dev/sda` আর `/dev/sda1` একই ভাবা

না।

```text
/dev/sda  → disk
/dev/sda1 → partition
```

---

### Mistake 3 — Mount point আর filesystem একই ভাবা

না।

```text
/dev/sdb1 → filesystem/device
/data      → mount point
```

---

### Mistake 4 — `rm` দিয়ে disk space সঙ্গে সঙ্গে ফিরে আসবেই ভাবা

যদি কোনো process deleted file open করে রাখে, `df`-এ space সঙ্গে সঙ্গে ফিরে নাও আসতে পারে।

---

### Mistake 5 — `fstab` না বুঝে edit করা

খুব risky।

প্রথমে backup/validation এবং `mount -a` দিয়ে verify করা উচিত।

---

### Mistake 6 — `df -h`-এ 100% না দেখে disk problem নেই ভাবা

Inode usage 100% হতে পারে।

তাই:

```bash
df -i
```

মনে রাখো।

---

### Mistake 7 — Disk format করার আগে device verify না করা

Storage administration-এ device ভুল নির্বাচন করলে data loss হতে পারে।

তাই unfamiliar disk-এর ওপর destructive operation চালানোর আগে device, partition এবং mount status verify করা জরুরি।

---

# 🧪 Level 7 Practical Lab

নিজের Linux VM বা test environment-এ:

## Lab 1 — Disk structure

```bash
lsblk
```

তারপর:

```bash
lsblk -f
```

খুঁজে বের করো:

* disk
* partition
* filesystem
* mount point

---

## Lab 2 — Disk usage

```bash
df -h
```

তারপর:

```bash
df -i
```

দুই output-এর difference বোঝার চেষ্টা করো।

---

## Lab 3 — Directory usage

নিজের home directory-তে:

```bash
du -sh ~
```

তারপর:

```bash
du -sh ~/*
```

---

## Lab 4 — Mount information

```bash
findmnt
```

Specific:

```bash
findmnt /
```

---

## Lab 5 — UUID

```bash
sudo blkid
```

Filesystem এবং UUID identify করো।

---

## Lab 6 — Inode

```bash
ls -li
```

কিছু file-এর inode number দেখো।

---

## Lab 7 — LVM

যদি তোমার VM-এ LVM থাকে:

```bash
sudo pvs
sudo vgs
sudo lvs
```

এই তিনটার relationship বুঝো:

```text
PV → VG → LV
```

---

# 🎯 Level 7 Interview Questions

## Beginner

### 1. Linux-এ disk কীভাবে দেখবে?

```bash
lsblk
```

### 2. Disk usage কীভাবে দেখবে?

```bash
df -h
```

### 3. Directory কত space নিচ্ছে?

```bash
du -sh directory
```

### 4. Filesystem কী?

Files ও metadata organize/manage করার storage structure।

### 5. Mount point কী?

যে directory-তে filesystem attach করা হয়।

### 6. `/etc/fstab` কী?

Boot-time/persistent filesystem mount configuration-এর জন্য ব্যবহৃত file।

---

# 🔥 Intermediate Interview Questions

### 7. `df` বনাম `du`?

```text
df → filesystem-level usage
du → file/directory-level usage
```

### 8. UUID কেন ব্যবহার করা হয়?

Filesystem identify করার stable identifier হিসেবে ব্যবহার করা যায়, বিশেষ করে persistent mounts-এর configuration-এ।

### 9. `mount` আর `umount` কী?

```text
mount  → filesystem attach
umount → filesystem detach
```

### 10. `df -i` কী দেখায়?

Filesystem inode usage।

### 11. inode কী?

File-এর metadata এবং filesystem-এর data-block references সম্পর্কিত structure।

### 12. Disk space free কিন্তু file create হচ্ছে না—কী করবে?

```bash
df -i
```

চেক করবে inode exhausted কিনা।

---

# 💀 Advanced Interview Questions

### 13. `df` 95% দেখাচ্ছে কিন্তু `du` expected usage দেখাচ্ছে না—কেন?

একটি সম্ভাব্য কারণ:

> Deleted file এখনও কোনো running process open করে রেখেছে।

Check:

```bash
sudo lsof +L1
```

---

### 14. LVM-এর architecture বলো।

```text
Physical Disk/Partition
        ↓
       PV
        ↓
       VG
        ↓
       LV
        ↓
   Filesystem
        ↓
   Mount Point
```

---

### 15. PV, VG এবং LV কী?

```text
PV → physical storage allocated to LVM
VG → pool of storage made from PVs
LV → logical storage carved from a VG
```

---

### 16. `lsblk -f` কেন useful?

একসঙ্গে disk/partition-এর:

```text
filesystem
UUID
mount point
```

সহ structure দেখতে সাহায্য করে।

---

### 17. `/dev/sda1` কী?

সাধারণ naming scheme-এ:

```text
/dev/sda
```

একটি disk এবং:

```text
/dev/sda1
```

তার প্রথম partition।

---

# 🧠 LEVEL 7 FINAL SCENARIO

Interviewer:

> **“Your Linux server says: No space left on device. What will you do?”**

তুমি এভাবে answer করতে পারো:

```text
Step 1:
df -h
```

→ কোন filesystem full?

```text
Step 2:
df -i
```

→ inode full কিনা?

```text
Step 3:
du -sh <relevant-directory>/*
```

→ কোন directory বড়?

```text
Step 4:
Check logs / application data / temporary files
```

→ কোন legitimate data space নিচ্ছে?

```text
Step 5:
sudo lsof +L1
```

→ deleted-but-open files আছে কিনা?

তারপর root cause অনুযায়ী safe cleanup, log rotation, application configuration বা storage expansion-এর মতো corrective action নেওয়া হবে।

**শুধু `rm -rf` চালানো troubleshooting নয়।** আগে জানতে হবে space কেন শেষ হয়েছে।

---

# 🏆 Level 7 Must-Know Cheat Sheet

```text
lsblk
lsblk -f

df -h
df -T
df -i

du -sh .
du -sh *

mount
umount
findmnt

blkid

cat /etc/fstab
mount -a

ls -li

pvs
vgs
lvs

sudo lsof +L1
```

### সবচেয়ে গুরুত্বপূর্ণ mental model:

```text
DISK
 ↓
PARTITION
 ↓
FILESYSTEM
 ↓
MOUNT
 ↓
DIRECTORY
 ↓
FILES
```

আর LVM হলে:

```text
DISK/PARTITION
      ↓
     PV
      ↓
     VG
      ↓
     LV
      ↓
FILESYSTEM
      ↓
MOUNT POINT
```

**Level 8**-এ আমরা Linux-এর **Boot Process + GRUB + Kernel + `initramfs` + systemd boot sequence + recovery/rescue mode + boot troubleshooting** শিখব—মানে power button চাপা থেকে login prompt আসা পর্যন্ত Linux ভিতরে ভিতরে কী করে, সেটা।

---
# 🐧 Linux A–Z — LEVEL 8

## 🚀 Boot Process, GRUB, Kernel, initramfs, systemd & Boot Troubleshooting

Level 8-এ আমরা Linux **boot হওয়া থেকে login screen/terminal prompt আসা পর্যন্ত পুরো process** শিখব।

এটা Linux administration-এর খুব গুরুত্বপূর্ণ অংশ।

---

# 1. Linux Boot হলে আসলে কী হয়?

Computer চালু করলে সরাসরি Linux desktop আসে না।

একটি sequence অনুসরণ হয়:

```text
Power On
   ↓
Firmware (BIOS/UEFI)
   ↓
Bootloader (GRUB)
   ↓
Linux Kernel
   ↓
initramfs
   ↓
systemd (PID 1)
   ↓
Services / Targets
   ↓
Login
```

এটাই Level 8-এর মূল diagram।

---

# 2. Boot Process-এর Big Picture ⭐

আরও বিস্তারিত:

```text
┌──────────────┐
│ Power On     │
└──────┬───────┘
       ↓
┌──────────────┐
│ BIOS / UEFI  │
└──────┬───────┘
       ↓
┌──────────────┐
│ GRUB         │
└──────┬───────┘
       ↓
┌──────────────┐
│ Linux Kernel │
└──────┬───────┘
       ↓
┌──────────────┐
│ initramfs    │
└──────┬───────┘
       ↓
┌──────────────┐
│ systemd      │
│ PID 1        │
└──────┬───────┘
       ↓
┌──────────────┐
│ Services     │
└──────┬───────┘
       ↓
┌──────────────┐
│ Login        │
└──────────────┘
```

---

# 3. BIOS কী?

BIOS = **Basic Input/Output System**

এটি পুরোনো firmware technology।

Computer power-on হলে firmware hardware initialize করে এবং boot করার জন্য suitable boot device খুঁজে।

---

# 4. UEFI কী?

UEFI = **Unified Extensible Firmware Interface**

Modern computers-এ UEFI খুব common।

UEFI BIOS-এর modern replacement হিসেবে কাজ করে এবং boot process-এর আগে hardware/boot environment initialize করে।

### সহজভাবে:

```text
Old systems
→ BIOS

Modern systems
→ UEFI
```

---

# 5. BIOS বনাম UEFI

| BIOS                                           | UEFI                       |
| ---------------------------------------------- | -------------------------- |
| Older firmware approach                        | Modern firmware            |
| Traditional boot mechanism                     | Modern boot mechanism      |
| MBR-based systems-এর সঙ্গে historically common | GPT-এর সঙ্গে commonly used |
| More limited                                   | More flexible              |

**Important:** BIOS/UEFI এবং GPT/MBR একেবারে একই concept নয়।

Firmware:

```text
BIOS / UEFI
```

Partitioning scheme:

```text
MBR / GPT
```

এগুলো আলাদা concepts।

---

# 6. MBR কী?

MBR = **Master Boot Record**

পুরোনো partitioning/boot scheme।

এতে boot information এবং partition table-এর historical structure থাকে।

Modern systems-এ GPT বেশি common।

---

# 7. GPT কী?

GPT = **GUID Partition Table**

Modern partitioning scheme।

GPT-এর সুবিধাগুলোর মধ্যে:

* modern systems-এর জন্য suitable
* বড় disks support
* বেশি partitions-এর flexibility
* UEFI systems-এর সঙ্গে commonly used

---

# 8. GRUB কী?

GRUB = **GRand Unified Bootloader**

Linux systems-এ widely used bootloader।

GRUB-এর কাজ:

```text
Firmware
   ↓
GRUB
   ↓
Kernel
```

GRUB Linux kernel load করতে সাহায্য করে এবং একাধিক operating system/kernel-এর মধ্যে নির্বাচন করার সুযোগ দিতে পারে।

---

# 9. GRUB Menu

Computer boot করার সময় এমন menu দেখতে পারো:

```text
GNU GRUB

Ubuntu
Advanced options for Ubuntu
```

`Advanced options`-এর মধ্যে পুরোনো kernel বা recovery-related entries থাকতে পারে।

---

# 10. GRUB Configuration কোথায়?

Common generated configuration:

```text
/boot/grub/grub.cfg
```

দেখতে:

```bash id="r4w2do"
ls /boot/grub
```

### গুরুত্বপূর্ণ

`grub.cfg` সাধারণত manually edit করা উচিত নয়।

কারণ এটি generated configuration।

---

# 11. `/etc/default/grub`

GRUB-এর configuration preferences সাধারণত:

```text id="d77h4x"
/etc/default/grub
```

এখানে settings থাকতে পারে।

Example:

```bash id="khq7m2"
cat /etc/default/grub
```

তারপর configuration regenerate করতে distribution-এর appropriate tool ব্যবহার করা হয়।

Debian/Ubuntu family-তে সাধারণত:

```bash id="90brv8"
sudo update-grub
```

---

# 12. Kernel কী?

আগের level-এ kernel-এর basic concept দেখেছি।

Boot-এর সময় Linux kernel memory-তে load হয়।

Kernel:

```text id="mcrkdr"
CPU
Memory
Devices
Processes
Networking
Filesystem
```

সহ hardware এবং system resources manage করে।

---

# 13. Kernel File কোথায় থাকে?

সাধারণত:

```text id="e2b7gk"
/boot
```

দেখো:

```bash id="80wqf3"
ls -lh /boot
```

তুমি এমন file দেখতে পারো:

```text id="5pv9fy"
vmlinuz-...
initrd.img-...
```

---

# 14. `vmlinuz` কী?

`vmlinuz` নাম সাধারণত compressed Linux kernel image-এর জন্য ব্যবহৃত হয়।

Example:

```text id="g3vsl1"
/boot/vmlinuz-...
```

এটাই bootloader kernel হিসেবে load করতে পারে।

---

# 15. initramfs কী?

initramfs = **initial RAM filesystem**

এটি boot-এর early stage-এ RAM-এর মধ্যে একটি temporary filesystem environment দেয়।

কেন দরকার?

Kernel boot করার পর root filesystem access করার আগে কিছু drivers/tools/configuration দরকার হতে পারে।

যেমন:

```text id="n9kgd6"
Storage driver
Filesystem driver
LVM support
RAID support
Encryption-related boot support
```

এসব early boot environment-এ প্রয়োজন হতে পারে।

---

# 16. initramfs-এর কাজ

Conceptually:

```text
Kernel
  ↓
initramfs
  ↓
Find/prepare root filesystem
  ↓
Switch to real root filesystem
  ↓
systemd
```

এটা মনে রাখো:

> **initramfs হলো early userspace environment, যা real root filesystem ব্যবহারের আগে boot process-কে সাহায্য করে।**

---

# 17. `initramfs` file কোথায়?

সাধারণত:

```bash id="gkll9w"
ls -lh /boot
```

এমন কিছু দেখতে পারো:

```text id="v8d5gr"
initrd.img-...
```

অনেক Linux distribution-এ `initrd` নামটি initramfs image-এর জন্য ব্যবহৃত হয়।

---

# 18. systemd কখন আসে?

Boot process-এর পরে:

```text id="d5qhr2"
Kernel
  ↓
initramfs
  ↓
systemd
```

Modern systemd-based Linux system-এ systemd সাধারণত:

```text id="kg6e4a"
PID 1
```

হয়।

Check:

```bash id="u4t8l3"
ps -p 1 -o pid,comm,args
```

Example:

```text id="t7k8xq"
PID COMMAND
1   systemd
```

---

# 19. PID 1 কেন Important?

PID 1 system-এর প্রথম userspace process।

systemd অনেক system-level responsibilities handle করে:

```text
Services
Logging integration
Targets
Mounts
Dependencies
Startup
Shutdown
```

---

# 20. systemd Boot Process

systemd অনেক unit manage করে।

Common unit types:

```text
.service
.socket
.target
.mount
.timer
```

আমাদের জন্য সবচেয়ে important:

```text
.service
.target
```

---

# 21. systemd Target কী?

Target হলো system-এর একটি desired state/grouping।

পুরোনো SysV runlevel-এর modern equivalent হিসেবে targets ব্যবহৃত হয়।

দেখতে:

```bash id="o4ib2m"
systemctl get-default
```

Example:

```text id="myr0t8"
graphical.target
```

অথবা:

```text id="8shx4x"
multi-user.target
```

---

# 22. `multi-user.target`

সাধারণ server-oriented system state।

এখানে সাধারণত:

```text
Network
Services
Login
```

চলতে পারে, কিন্তু graphical desktop প্রয়োজনীয় নয়।

---

# 23. `graphical.target`

Desktop environment সহ graphical system state।

Concept:

```text id="23q8r4"
graphical.target
      ↓
multi-user functionality
      +
graphical login
```

---

# 24. Default Target

দেখতে:

```bash id="a7rj5k"
systemctl get-default
```

Change করার প্রয়োজন হলে:

```bash id="l3h0e7"
sudo systemctl set-default multi-user.target
```

অথবা graphical:

```bash id="09oz3c"
sudo systemctl set-default graphical.target
```

**নিজের test VM-এ practice করা ভালো।**

---

# 25. Boot-এর সময় কোন services start হয়েছে?

দেখতে:

```bash id="6qf8r2"
systemctl list-units --type=service
```

Enabled services:

```bash id="3xfl9k"
systemctl list-unit-files --type=service
```

---

# 26. Boot Time Analysis

Linux boot হতে কত সময় লাগছে দেখতে:

```bash id="tdn5xy"
systemd-analyze
```

Example:

```text id="v4yn5x"
Startup finished in 3.2s
```

আর বিস্তারিত:

```bash id="9n8e6g"
systemd-analyze blame
```

এটি কোন units startup-এ কত সময় নিয়েছে সে সম্পর্কে information দিতে পারে।

---

# 27. Boot Critical Chain

আরও useful:

```bash id="c2gr4q"
systemd-analyze critical-chain
```

এটা boot-এর dependency chain দেখাতে সাহায্য করে।

---

# 28. Journal Logs

systemd systems-এ boot এবং service logs-এর জন্য:

```bash id="6e2n4g"
journalctl
```

Current boot:

```bash id="5j4m0w"
journalctl -b
```

Previous boot:

```bash id="yl3qdf"
journalctl -b -1
```

Kernel messages:

```bash id="q15y6k"
journalctl -k
```

---

# 29. `dmesg`

Kernel ring buffer messages দেখতে:

```bash id="ezgplr"
dmesg
```

শেষের কিছু:

```bash id="zzqzj0"
dmesg | tail
```

Human-readable timestamps সহ:

```bash id="uw6zv2"
dmesg -T
```

Storage/driver/boot troubleshooting-এ এটি useful।

---

# 30. Boot Failure Scenario 🚨

ধরো machine boot হচ্ছে না।

প্রথমে problem-এর stage identify করতে হবে।

```text id="9yqv1w"
Power
 ↓
UEFI/BIOS
 ↓
GRUB
 ↓
Kernel
 ↓
initramfs
 ↓
systemd
 ↓
Services
 ↓
Login
```

যে stage-এ fail করছে, troubleshooting সেই stage অনুযায়ী হবে।

---

# 31. Scenario: GRUB আসে না

যদি system GRUB পর্যন্তই পৌঁছাতে না পারে, তাহলে problem হতে পারে:

```text
Boot configuration
EFI/boot files
Bootloader installation
Disk/firmware configuration
```

এখানে system boot mode (UEFI/legacy), boot device এবং bootloader configuration verify করতে হয়।

---

# 32. Scenario: Kernel Load হচ্ছে না

সম্ভাব্য বিষয়:

```text
Kernel image
Boot configuration
/boot filesystem
Bootloader entry
```

এরকম ক্ষেত্রে GRUB-এর available kernel entries এবং `/boot` contents investigate করা হয়।

---

# 33. Scenario: `initramfs` Emergency Shell

একটি common serious boot issue হলো:

```text id="x39t5s"
(initramfs)
```

এরকম prompt পাওয়া।

এটি early boot environment-এ সমস্যা হয়েছে বোঝাতে পারে।

Possible causes:

```text
Root filesystem unavailable
Storage issue
Filesystem problem
Incorrect boot configuration
Missing driver
LVM/RAID/encryption-related issue
```

এখানে blindly filesystem repair command চালানো উচিত নয়।

প্রথমে root device এবং error message identify করতে হবে।

---

# 34. Scenario: Root Filesystem পাওয়া যাচ্ছে না

Boot process যদি root filesystem locate করতে না পারে:

```text id="o8mbr7"
Kernel
 ↓
initramfs
 ↓
❌ root filesystem
```

তখন check করতে হয়:

* expected device exists কি না
* filesystem identifier ঠিক আছে কি না
* storage detected কি না
* LVM available কি না
* boot configuration correct কি না

---

# 35. `fstab` Boot Problem

Level 7-এ আমরা `/etc/fstab` শিখেছি।

ধরো তুমি ভুল mount entry দিলে।

Boot-এর সময় system সেই filesystem mount করার চেষ্টা করতে গিয়ে delay বা failure ঘটাতে পারে।

তাই:

```text id="r9k1eg"
/etc/fstab
```

একটি boot-critical configuration হতে পারে।

---

# 36. Rescue Mode কী?

Rescue mode হলো troubleshooting/recovery-এর জন্য minimal system state।

systemd systems-এ:

```text id="q36x4k"
rescue.target
```

এর concept আছে।

এখানে সাধারণত normal desktop-এর বদলে minimum services নিয়ে recovery work করা যায়।

---

# 37. Emergency Mode কী?

আরও minimal recovery state:

```text id="8xxjbl"
emergency.target
```

Rescue-এর তুলনায় আরও minimal environment হতে পারে।

Conceptually:

```text
normal
  ↓
rescue
  ↓
emergency
```

যত নিচে যাবে, environment তত minimal।

---

# 38. Rescue vs Emergency

| Rescue                   | Emergency             |
| ------------------------ | --------------------- |
| Recovery/troubleshooting | Very minimal recovery |
| More services available  | Very few services     |
| Maintenance work         | Serious boot failures |
| `rescue.target`          | `emergency.target`    |

---

# 39. Single-user Concept

পুরোনো Linux terminology-তে:

```text
single-user mode
```

শব্দটি শুনতে পারো।

Modern systemd systems-এ equivalent concepts হিসেবে rescue/emergency targets বেশি relevant।

---

# 40. Kernel Parameters কী?

GRUB kernel-কে কিছু boot parameters দিতে পারে।

Example:

```text id="x5f4l3"
ro
quiet
```

এগুলো kernel boot behavior-এর বিভিন্ন aspect control করতে পারে।

GRUB menu-তে একটি Linux entry edit করলে kernel command line দেখা যেতে পারে।

### Beginner warning

Unknown kernel parameter blindly change করা উচিত নয়।

---

# 41. `quiet` কী?

অনেক Linux systems-এ:

```text id="wy2u2o"
quiet
```

kernel boot messages কম দেখানোর জন্য ব্যবহৃত হতে পারে।

Troubleshooting-এর সময় graphical splash-এর বদলে actual boot messages দেখতে চাইলে boot configuration অনুযায়ী `quiet` behaviour গুরুত্বপূর্ণ হতে পারে।

---

# 42. `ro` কী?

Kernel command line-এ:

```text id="4h2y2c"
ro
```

সাধারণত root filesystem প্রথমে read-only হিসেবে mount করার নির্দেশের সঙ্গে সম্পর্কিত।

Boot process পরে প্রয়োজন অনুযায়ী filesystem state পরিবর্তন করতে পারে।

---

# 43. Boot Logs

Current boot:

```bash id="h4p1ks"
journalctl -b
```

শুধু errors:

```bash id="8japc6"
journalctl -b -p err
```

Previous boot:

```bash id="z3f7t9"
journalctl -b -1
```

Kernel:

```bash id="4pjr6x"
journalctl -k
```

Service:

```bash id="ymt1ly"
journalctl -u ssh
```

---

# 44. Failed Services

একটি খুব useful command:

```bash id="l1r4do"
systemctl --failed
```

যদি কোনো service boot-এর সময় fail করে থাকে, এখানে দেখা যেতে পারে।

তারপর:

```bash id="8sv3b5"
systemctl status <service>
```

এবং:

```bash id="j0yr2a"
journalctl -u <service>
```

---

# 45. Boot Troubleshooting Golden Flow ⭐

যদি Linux boot সমস্যা হয়:

```text id="6q5u8n"
1. Which stage failed?
        ↓
2. Firmware / GRUB?
        ↓
3. Kernel?
        ↓
4. initramfs?
        ↓
5. systemd?
        ↓
6. Service?
        ↓
7. Check logs
```

Commands:

```bash id="ynk5ks"
systemctl --failed
```

```bash id="j8i7lw"
journalctl -b -p err
```

```bash id="n7c6h0"
journalctl -k
```

```bash id="d9x8zz"
dmesg -T
```

---

# 46. Common Beginner Mistakes 🚨

### Mistake 1

BIOS আর GRUB একই মনে করা।

❌ না।

```text
BIOS/UEFI → firmware
GRUB      → bootloader
```

---

### Mistake 2

Kernel আর operating system একই জিনিস মনে করা।

Linux technically kernel; complete distribution-এর মধ্যে kernel-এর পাশাপাশি userspace tools, libraries, package manager, services ইত্যাদি থাকে।

---

### Mistake 3

GRUB configuration manually edit করা।

```text id="jld6hx"
/boot/grub/grub.cfg
```

সাধারণত generated file।

---

### Mistake 4

`systemctl enable` মানে service এখনই start হবে ভাবা।

না।

```text id="m4ekr4"
start
→ এখন চালাও

enable
→ boot-এর সময় automatically start করার configuration
```

একসাথে:

```bash id="2f9dzn"
sudo systemctl enable --now nginx
```

---

### Mistake 5

Boot problem দেখলেই reinstall করা।

❌ আগে:

```text id="9akqgr"
logs
boot stage
disk
filesystem
fstab
services
```

check করা উচিত।

---

### Mistake 6

`journalctl -b` এবং `journalctl -b -1` একই মনে করা।

```text id="j8v1ht"
-b
→ current boot

-b -1
→ previous boot
```

---

# 🧪 Level 8 Practical Lab

নিজের Linux VM-এ এগুলো safely practice করো।

## Lab 1 — Kernel

```bash id="c4p75q"
uname -r
```

Kernel version দেখো।

আর:

```bash id="w5f9r5"
uname -a
```

---

## Lab 2 — `/boot`

```bash id="uwl1jr"
ls -lh /boot
```

খুঁজে দেখো:

```text
vmlinuz
initrd/initramfs
grub
```

---

## Lab 3 — PID 1

```bash id="f2k48v"
ps -p 1 -o pid,comm,args
```

---

## Lab 4 — Default target

```bash id="m7cz6d"
systemctl get-default
```

---

## Lab 5 — Failed services

```bash id="l8t9jo"
systemctl --failed
```

---

## Lab 6 — Current boot logs

```bash id="c1bq8p"
journalctl -b -n 50
```

---

## Lab 7 — Boot errors

```bash id="m6cqwy"
journalctl -b -p err
```

---

## Lab 8 — Boot performance

```bash id="y2x8nz"
systemd-analyze
```

তারপর:

```bash id="2d0xwq"
systemd-analyze blame
```

---

## Lab 9 — Critical chain

```bash id="07w5y6"
systemd-analyze critical-chain
```

Output দেখে বুঝতে চেষ্টা করো কোন dependency chain boot-এর জন্য important।

---

# 🎯 Level 8 Interview Questions

## Beginner

### 1. Linux boot process-এর basic sequence কী?

```text id="cz4z0u"
UEFI/BIOS
↓
GRUB
↓
Kernel
↓
initramfs
↓
systemd
↓
Services/Targets
↓
Login
```

### 2. GRUB কী?

Linux-এর একটি widely used bootloader।

### 3. Kernel কী?

OS-এর core component যা hardware/resources এবং core system functionality manage করে।

### 4. initramfs কী?

Early boot-এর temporary userspace filesystem/environment, যা real root filesystem ব্যবহারের আগে প্রয়োজনীয় tools/drivers support করতে পারে।

### 5. PID 1 কী?

Modern systemd-based Linux system-এ সাধারণত systemd process।

---

# 🔥 Intermediate Interview Questions

### 6. BIOS এবং UEFI-এর difference কী?

দুটিই firmware technology; UEFI হলো modern firmware interface, BIOS হলো older/traditional approach।

### 7. GRUB-এর কাজ কী?

Kernel এবং boot entries নির্বাচন/load করার জন্য bootloader হিসেবে কাজ করা।

### 8. `systemctl get-default` কী করে?

Default systemd target দেখায়।

### 9. `journalctl -b` কী?

Current boot-এর journal messages দেখায়।

### 10. `journalctl -b -1`?

Previous boot-এর journal messages।

### 11. `systemctl --failed` কী?

Failed systemd units দেখায়।

### 12. `systemd-analyze` কী?

System boot performance/timing-এর summary দেয়।

---

# 💀 Advanced Interview Questions

### 13. Linux boot process বিস্তারিত explain করো।

একটি strong answer:

```text id="f4f7wb"
Firmware
↓
Bootloader
↓
Kernel
↓
initramfs
↓
real root filesystem
↓
systemd/PID 1
↓
targets/services
↓
login
```

প্রতিটি stage-এর আলাদা responsibility আছে।

---

### 14. initramfs কেন দরকার?

Kernel boot হওয়ার পর real root filesystem access করার জন্য প্রয়োজনীয় early userspace tools/drivers/storage support দিতে পারে।

---

### 15. Server boot হয়েছে কিন্তু একটি service নেই। কী করবে?

```bash id="f8y7by"
systemctl --failed
```

তারপর:

```bash id="b6x7bd"
systemctl status <service>
```

তারপর:

```bash id="f7d8r9"
journalctl -u <service>
```

তারপর service configuration/dependencies fix করে আবার verify করবে।

---

### 16. Boot slow হলে কীভাবে investigate করবে?

```bash id="wm5d2g"
systemd-analyze
```

তারপর:

```bash id="7q9s9d"
systemd-analyze blame
```

এবং:

```bash id="1o9l6v"
systemd-analyze critical-chain
```

এরপর relevant service/log investigate করবে।

---

### 17. `rescue.target` এবং `emergency.target` কী?

দুটিই recovery-oriented systemd targets।

```text id="3khrbr"
rescue.target
→ maintenance/recovery environment

emergency.target
→ আরও minimal emergency environment
```

---

# 🧠 LEVEL 8 FINAL INTERVIEW SCENARIO

Interviewer:

> **“A Linux server was working yesterday. Today it doesn't boot normally. How will you troubleshoot?”**

একটি structured answer:

```text id="x4c9fz"
1. Identify where boot stops
        ↓
2. Firmware/UEFI?
        ↓
3. GRUB?
        ↓
4. Kernel?
        ↓
5. initramfs/root filesystem?
        ↓
6. systemd?
        ↓
7. Failed service?
```

যদি system boot করে কিন্তু service missing:

```bash id="1xsp9r"
systemctl --failed
```

তারপর:

```bash id="v7s7vl"
systemctl status <service>
```

তারপর:

```bash id="e2r5aj"
journalctl -u <service>
```

Boot-level logs:

```bash id="9c1q5s"
journalctl -b -p err
```

Kernel-level:

```bash id="2drm4u"
journalctl -k
```

আর boot performance:

```bash id="1r0wsy"
systemd-analyze
```

**মূল skill হলো command মুখস্থ করা নয়—কোন stage-এ failure হয়েছে সেটা isolate করা।**

---

# 🏆 Level 8 Must-Know Cheat Sheet

```text
uname -r
uname -a

ls -lh /boot

ps -p 1 -o pid,comm,args

systemctl get-default
systemctl --failed

journalctl
journalctl -b
journalctl -b -1
journalctl -b -p err
journalctl -k
journalctl -u <service>

dmesg -T

systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain

ls /boot/grub
cat /etc/default/grub
```

### সবচেয়ে important mental model:

```text
POWER
  ↓
BIOS / UEFI
  ↓
GRUB
  ↓
KERNEL
  ↓
INITRAMFS
  ↓
ROOT FILESYSTEM
  ↓
SYSTEMD (PID 1)
  ↓
TARGETS + SERVICES
  ↓
LOGIN
```

**Level 9**-এ আমরা Linux-এর **Security & Hardening** শিখব—`sudo`, SSH security, permissions review, file ownership, `umask`, password policies, firewall concepts, `ufw`, `firewalld`, SELinux/AppArmor basics, logs, least privilege এবং common security mistakes—সবকিছু beginner থেকে interview level পর্যন্ত।


---
# 🐧 Linux A–Z — LEVEL 9

## 🔐 Linux Security & Hardening — `sudo`, SSH, Firewall, `umask`, SELinux/AppArmor

Level 9-এ আমরা Linux system **secure করার fundamentals** শিখব। এখানে লক্ষ্য হলো defensive administration—নিজের Linux machine/server কীভাবে নিরাপদভাবে configure, monitor এবং troubleshoot করতে হয়।

---

# 1. Linux Security-এর মূল ধারণা

Linux security-কে কয়েকটি layer হিসেবে ভাবো:

```text
┌──────────────────────┐
│ Users & Authentication│
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Permissions           │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ sudo / Least Privilege│
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ SSH Security         │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Firewall             │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ MAC: SELinux/AppArmor│
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Logging & Monitoring │
└──────────────────────┘
```

এখানে একটি গুরুত্বপূর্ণ principle:

> **Security = শুধু firewall নয়।**

---

# 2. Authentication বনাম Authorization

এই দুইটা interview-এ খুব common।

### Authentication

> তুমি কে?

উদাহরণ:

```text
username
password
SSH key
```

### Authorization

> তুমি কী করতে পারবে?

উদাহরণ:

```text
read
write
execute
sudo
access specific service
```

সহজভাবে:

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

# 3. User Security

Users দেখো:

```bash
id
```

বর্তমান user:

```bash
whoami
```

সব user-এর information:

```bash
cat /etc/passwd
```

Groups:

```bash
groups
```

কোন user কোন groups-এর member:

```bash
id username
```

---

# 4. Root User

Linux-এর privileged account:

```text
root
UID = 0
```

Root অনেক system-level operation করতে পারে।

এজন্য daily কাজের জন্য root account ব্যবহার না করে সাধারণ user + `sudo` ব্যবহার করা safer practice।

---

# 5. `sudo`

`sudo` মানে সাধারণভাবে:

> একটি authorized user-কে নির্দিষ্ট command elevated privileges-এ চালানোর সুযোগ দেওয়া।

Example:

```bash
sudo systemctl restart nginx
```

অথবা:

```bash
sudo apt update
```

---

# 6. কেন সবসময় root হিসেবে কাজ করা উচিত নয়?

ধরো তুমি সাধারণ user:

```text
rahim
```

যদি কোনো ভুল command চালাও, তার permission সীমিত থাকে।

কিন্তু root হিসেবে একই ভুল command-এর impact অনেক বেশি হতে পারে।

তাই principle:

```text
Least Privilege
```

অর্থাৎ:

> যতটুকু permission প্রয়োজন, ততটুকুই দেওয়া।

---

# 7. `sudo` Configuration

সাধারণত:

```text
/etc/sudoers
```

এবং:

```text
/etc/sudoers.d/
```

configuration-এর সঙ্গে সম্পর্কিত।

### Important warning 🚨

`/etc/sudoers` সরাসরি ভুলভাবে edit করা dangerous হতে পারে।

সাধারণত:

```bash
sudo visudo
```

ব্যবহার করা হয়।

`visudo` syntax validation করতে সাহায্য করে।

---

# 8. SSH Security

SSH remote administration-এর জন্য খুব important।

Basic:

```bash
ssh user@server
```

SSH server configuration সাধারণত:

```text
/etc/ssh/sshd_config
```

দেখতে:

```bash
sudo sshd -T
```

এতে effective SSH configuration-এর অনেক setting দেখা যায়।

---

# 9. SSH Key Authentication

Password-এর পরিবর্তে SSH key authentication ব্যবহার করা যায়।

Concept:

```text
Your Computer
     |
     | private key
     ↓
SSH Server
     |
     | authorized public key
     ↓
Authentication
```

Key pair:

```text
Private Key
Public Key
```

### সবচেয়ে গুরুত্বপূর্ণ rule:

> **Private key গোপন রাখতে হবে।**

Public key server-এ রাখা যায়।

---

# 10. SSH Key Files

সাধারণত user-এর SSH directory:

```text
~/.ssh/
```

দেখতে:

```bash
ls -la ~/.ssh
```

Public key-এর example:

```text
~/.ssh/id_ed25519.pub
```

Private key:

```text
~/.ssh/id_ed25519
```

**Private key অন্যকে দেওয়া উচিত নয়।**

---

# 11. `authorized_keys`

Server-side user-এর SSH public keys সাধারণত:

```text
~/.ssh/authorized_keys
```

এ থাকে।

Concept:

```text
Client private key
        ↓
matches
        ↓
Server authorized public key
```

---

# 12. SSH Key Permissions

SSH key files-এর permission গুরুত্বপূর্ণ।

Private key:

```bash
chmod 600 ~/.ssh/id_ed25519
```

`.ssh` directory:

```bash
chmod 700 ~/.ssh
```

Public key সাধারণত:

```text
.pub
```

file হওয়ায় private key-এর মতো secret নয়।

---

# 13. `umask` কী?

`umask` নতুন file/directory তৈরি হওয়ার সময় default permissions থেকে কিছু permission বাদ দিতে সাহায্য করে।

দেখতে:

```bash
umask
```

Example:

```text
0022
```

এটি security-এর জন্য important।

---

# 14. `umask` Example

ধরো একটি program defaultভাবে file-এর জন্য:

```text
666
```

permissions request করে।

যদি:

```text
umask = 022
```

হয়, তাহলে resulting permission সাধারণভাবে:

```text
644
```

হতে পারে।

Directory-এর base mode সাধারণত:

```text
777
```

থেকে umask apply হয়।

তাই:

```text
777 - 022 → 755
```

ধরনের result দেখা যায়।

### মনে রাখবে

`umask` সাধারণ subtraction-এর মতো সব ক্ষেত্রে blindly ভাবা উচিত নয়; permission bits-এর masking logic কাজ করে।

---

# 15. `chmod 777` কেন Avoid করা হয়?

অনেক beginner ভাবে:

> Permission problem → `chmod 777`

এটা ভালো solution নয়।

`777`:

```text
rwxrwxrwx
```

মানে owner/group/others সবাইকে read, write, execute permission দেওয়া।

Security principle:

```text
Need permission?
→ Give required permission only.
```

---

# 16. File Permission Review

দেখতে:

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 rahim developers 1200 file.txt
```

Breakdown:

```text
-       → regular file
rw-     → owner
r--     → group
r--     → others
```

আগের Level 3-এর knowledge এখানে security-এর অংশ হয়ে যায়।

---

# 17. Sensitive Files

কিছু Linux configuration/security files:

```text
/etc/passwd
/etc/shadow
/etc/sudoers
/etc/ssh/sshd_config
/etc/fstab
```

এর মধ্যে বিশেষভাবে:

```text
/etc/shadow
```

sensitive।

সাধারণ user-এর এটিতে unrestricted access থাকা উচিত নয়।

---

# 18. `/etc/shadow`

Linux systems-এ password-related credential data-এর protected representation এখানে থাকে।

Check:

```bash
sudo ls -l /etc/shadow
```

**এটার contents casually share করা উচিত নয়।**

---

# 19. Password Policy

System security-তে password policy-এর মধ্যে থাকতে পারে:

```text
minimum length
expiration
history
lockout-related policy
```

Distribution/tool অনুযায়ী configuration আলাদা হতে পারে।

একটি গুরুত্বপূর্ণ concept:

> Strong authentication + least privilege + regular updates = basic security foundation.

---

# 20. Firewall কী?

Firewall network traffic-এর rules enforce করে।

Concept:

```text
Internet
   |
   ↓
Firewall
   |
   ↓
Linux Server
```

Firewall decide করতে পারে:

```text
Allow?
Deny?
```

কোন traffic।

---

# 21. Firewall-এর Basic Concept

ধরো server-এ:

```text
SSH → 22
HTTP → 80
HTTPS → 443
```

তুমি চাইছো শুধু প্রয়োজনীয় service accessible হোক।

Conceptually:

```text
22  → allowed
80  → allowed
443 → allowed
other unnecessary ports → not allowed
```

এটাই attack surface কমানোর basic idea।

---

# 22. UFW

Ubuntu/Debian family-তে beginner-friendly firewall interface:

```text
UFW
```

= Uncomplicated Firewall

Status:

```bash
sudo ufw status
```

Detailed:

```bash
sudo ufw status verbose
```

---

# 23. UFW Rules

Conceptually allow SSH:

```bash
sudo ufw allow 22/tcp
```

HTTP:

```bash
sudo ufw allow 80/tcp
```

HTTPS:

```bash
sudo ufw allow 443/tcp
```

Enable:

```bash
sudo ufw enable
```

### ⚠️ SSH Warning

Remote server-এ firewall enable করার আগে SSH access-এর প্রয়োজনীয় rule/configuration নিশ্চিত না করলে নিজের remote access হারাতে পারো।

নিজের local VM-এ practice করা safest।

---

# 24. UFW Rules দেখো

```bash
sudo ufw status numbered
```

এতে rule list দেখা যায়।

---

# 25. Firewalld

Fedora/RHEL-family systems-এ `firewalld` common।

Status:

```bash
sudo firewall-cmd --state
```

Rules/zones সম্পর্কে:

```bash
sudo firewall-cmd --get-active-zones
```

এই ecosystem-এ firewall configuration UFW-এর মতো নয়।

---

# 26. UFW vs firewalld

| Ubuntu/Debian                 | Fedora/RHEL                    |
| ----------------------------- | ------------------------------ |
| UFW commonly used             | firewalld commonly used        |
| `ufw` command                 | `firewall-cmd`                 |
| Beginner-friendly abstraction | Zone-based firewall management |

Underlying Linux networking stack আলাদা কোনো "UFW network" নয়; এগুলো firewall management tools/interfaces।

---

# 27. Firewall vs `ss`

এখানে একটা গুরুত্বপূর্ণ distinction:

```text
ss
↓
কোন service কোন port-এ listen করছে?

firewall
↓
কোন network traffic allow/deny হচ্ছে?
```

উদাহরণ:

```bash
ss -lnt
```

দেখাতে পারে:

```text
:80 LISTEN
```

কিন্তু firewall port 80 block করতে পারে।

অর্থাৎ:

```text
Service listening
≠
Externally reachable
```

---

# 28. SELinux কী?

SELinux = **Security-Enhanced Linux**

এটি একটি Mandatory Access Control (MAC) system।

Traditional Unix permissions:

```text
owner
group
others
```

SELinux এর অতিরিক্ত security policy enforce করতে পারে।

---

# 29. DAC vs MAC

### DAC

Discretionary Access Control:

```text
chmod
chown
owner/group
```

### MAC

Mandatory Access Control:

```text
SELinux
```

Concept:

```text
Linux Security
       |
       ├── DAC
       │    └── permissions
       │
       └── MAC
            └── SELinux
```

---

# 30. SELinux Modes

Check:

```bash
getenforce
```

Possible output:

```text
Enforcing
Permissive
Disabled
```

### Enforcing

Policy violations block করতে পারে।

### Permissive

Violation log করে কিন্তু enforcement করে না।

### Disabled

SELinux disabled।

---

# 31. SELinux Status

```bash
sestatus
```

এতে আরও detailed information পাওয়া যায়।

---

# 32. AppArmor কী?

AppArmor-ও একটি Linux security framework, যা application profiles ব্যবহার করে access control enforce করতে পারে।

Ubuntu-তে AppArmor commonly encountered।

Check:

```bash
sudo aa-status
```

যদি tool installed/configured থাকে।

---

# 33. SELinux বনাম AppArmor

দুটিই security framework।

| SELinux                        | AppArmor                          |
| ------------------------------ | --------------------------------- |
| Label/context based model      | Path/profile-oriented model       |
| Fedora/RHEL ecosystem-এ common | Ubuntu/Debian ecosystem-এ common  |
| Powerful MAC                   | MAC-based application confinement |

একটিকে universally "better" বলা ঠিক নয়; distribution/environment-এর security architecture অনুযায়ী ব্যবহৃত হয়।

---

# 34. Linux Security Logs

Security troubleshooting-এর জন্য logs অত্যন্ত important।

systemd journal:

```bash
journalctl
```

SSH service:

```bash
journalctl -u ssh
```

কিছু distro-তে:

```bash
journalctl -u sshd
```

Authentication-related logs distribution অনুযায়ী:

```text
/var/log/auth.log
```

অথবা:

```text
/var/log/secure
```

---

# 35. Failed Login Investigation

নিজের authorized system-এ authentication events investigate করতে logs ব্যবহার করা যায়।

উদাহরণ:

```bash
sudo journalctl -u ssh
```

অথবা distro-এর relevant authentication log।

লক্ষ্য:

```text
successful login
failed login
authentication errors
configuration errors
```

বোঝা।

---

# 36. Least Privilege

Security-এর সবচেয়ে important principle-গুলোর একটি:

> User/process-কে তার কাজের জন্য যতটুকু permission প্রয়োজন, শুধু ততটুকু দাও।

Example:

Application-এর যদি শুধু:

```text
read /var/www/app
```

দরকার হয়, তাহলে তাকে পুরো filesystem-এর write access দেওয়া উচিত নয়।

---

# 37. Attack Surface

Attack surface মানে broadly:

> System-এর যে জায়গাগুলো attacker-এর জন্য interaction/entry opportunity তৈরি করতে পারে।

উদাহরণ:

```text
Open ports
Running services
Exposed applications
Unnecessary accounts
Weak authentication
Outdated software
```

তাই basic hardening:

```text
Remove unnecessary services
Close unnecessary ports
Use least privilege
Keep software updated
Use secure authentication
Monitor logs
```

---

# 38. Linux Security Hardening Checklist ⭐

একটি নতুন Linux server-এর জন্য high-level checklist:

```text
☑ Update system
☑ Remove unnecessary software/services
☑ Review users
☑ Review sudo access
☑ Use strong authentication
☑ Secure SSH
☑ Use least privilege
☑ Configure firewall
☑ Review listening ports
☑ Protect sensitive files
☑ Monitor logs
☑ Configure appropriate MAC framework
☑ Keep backups
```

---

# 39. Security Troubleshooting Scenario

ধরো:

> “SSH কাজ করছে না।”

Randomly firewall off করবে না।

প্রথমে:

```bash
systemctl status ssh
```

অথবা:

```bash
systemctl status sshd
```

তারপর:

```bash
ss -lntp
```

দেখবে SSH port listen করছে কিনা।

তারপর firewall:

```bash
sudo ufw status
```

অথবা firewalld হলে:

```bash
sudo firewall-cmd --get-active-zones
```

তারপর logs:

```bash
journalctl -u ssh
```

এই flow:

```text
Service
 ↓
Port
 ↓
Firewall
 ↓
Logs
 ↓
Configuration
```

---

# 40. আরেকটি Scenario

Application চলছে কিন্তু permission denied:

```text
Permission denied
```

তখন শুধু:

```bash
chmod 777
```

করবে না।

প্রথমে check:

```bash
ls -l file
```

তারপর:

```bash
id
```

এবং প্রয়োজনে:

```bash
namei -l /path/to/file
```

এটা path-এর প্রতিটি directory-এর permission inspect করতে useful।

তারপর SELinux/AppArmor policy relevant কিনা investigate করবে।

---

# 41. `namei -l` কেন Useful?

ধরো:

```text
/path/to/application/data/file.txt
```

শেষ file-এর permission ঠিক আছে।

তবুও access denied।

কারণ parent directory-এর traversal permission সমস্যা হতে পারে।

```bash
namei -l /path/to/application/data/file.txt
```

প্রতিটি path component-এর permission দেখতে সাহায্য করে।

---

# 42. Security-এর জন্য `777` নয়

যদি application কাজ না করে:

❌

```bash
chmod -R 777 /some/directory
```

এটা security-এর জন্য খারাপ habit।

বরং প্রশ্ন করো:

```text
Who owns the file?
Who runs the application?
What permission is actually needed?
Is the parent directory accessible?
Is SELinux/AppArmor involved?
```

---

# 43. File Ownership Review

```bash
ls -l
```

Change owner:

```bash
sudo chown user:group file
```

Change permission:

```bash
chmod 640 file
```

Difference:

```text
chown → ownership
chmod → permissions
```

---

# 44. Security Updates

Package updates security-এর জন্য important।

Debian/Ubuntu:

```bash
sudo apt update
sudo apt upgrade
```

Fedora/RHEL family:

```bash
sudo dnf upgrade
```

Security hardening-এর অংশ হিসেবে systems updated রাখা গুরুত্বপূর্ণ।

---

# 45. Security Monitoring Mindset

শুধু configure করে শেষ নয়।

Regularly inspect:

```bash
ss -lntup
```

```bash
systemctl --failed
```

```bash
journalctl -p err
```

এবং authentication/security-related logs।

Question:

> “কোন service চলছে?”

> “কোন port open/listening?”

> “কার sudo access আছে?”

> “কোন authentication failures হচ্ছে?”

এই mindset একজন administrator-এর জন্য গুরুত্বপূর্ণ।

---

# 🚨 Level 9 Beginner Mistakes

### Mistake 1

সব permission problem-এ:

```bash
chmod 777
```

❌

---

### Mistake 2

Remote server-এ firewall enable করে SSH rule না দেখে দেওয়া।

❌ নিজের access হারাতে পারো।

---

### Mistake 3

Firewall off করে problem solve করা।

❌ Firewall-এর rule/configuration troubleshoot করাই ভালো।

---

### Mistake 4

`ss` output দেখে port open মানেই Internet থেকে accessible ভাবা।

❌ Firewall/routing/interface binding matter করে।

---

### Mistake 5

Root account দিয়ে সব কাজ করা।

❌ Least privilege principle ভাঙে।

---

### Mistake 6

Private SSH key share করা।

❌ কখনোই নয়।

---

### Mistake 7

SELinux/AppArmor disable করে সব problem solve করার চেষ্টা।

❌ Security control সরিয়ে ফেললে root cause ঠিক হয় না।

---

# 🧪 Level 9 Practical Lab

নিজের Linux VM-এ practice করো।

## Lab 1 — Current identity

```bash
whoami
id
groups
```

---

## Lab 2 — Sudo

```bash
sudo -l
```

এটা তোমার current user-এর sudo permissions সম্পর্কে information দিতে পারে।

---

## Lab 3 — SSH configuration

```bash
ls -la ~/.ssh
```

তারপর server configuration-এর existence:

```bash
sudo ls -l /etc/ssh/sshd_config
```

---

## Lab 4 — Listening services

```bash
sudo ss -lntup
```

প্রতিটি listening port-এর service identify করার চেষ্টা করো।

---

## Lab 5 — Firewall

Ubuntu/Debian + UFW থাকলে:

```bash
sudo ufw status verbose
```

Fedora/RHEL + firewalld থাকলে:

```bash
sudo firewall-cmd --state
```

---

## Lab 6 — SELinux

যদি system-এ SELinux থাকে:

```bash
getenforce
```

তারপর:

```bash
sestatus
```

---

## Lab 7 — AppArmor

যদি AppArmor installed/enabled থাকে:

```bash
sudo aa-status
```

---

## Lab 8 — Security logs

```bash
journalctl -p err -b
```

তারপর SSH-related:

```bash
journalctl -u ssh
```

অথবা system অনুযায়ী:

```bash
journalctl -u sshd
```

---

# 🎯 Level 9 Interview Questions

## Beginner

### 1. Authentication কী?

User কে তা verify করা।

### 2. Authorization কী?

User কী করতে পারবে তা determine করা।

### 3. `sudo` কেন ব্যবহার করা হয়?

Authorized users-কে elevated privileges-এ নির্দিষ্ট command চালানোর সুযোগ দিতে।

### 4. Root-এর UID কত?

```text
0
```

### 5. Firewall কী?

Network traffic-এর allow/deny rules enforce করার security mechanism।

### 6. SSH কী?

Secure remote shell/access protocol।

---

# 🔥 Intermediate Interview Questions

### 7. `chmod` এবং `chown` difference?

```text
chmod → permissions
chown → ownership
```

### 8. `umask` কী?

নতুন file/directory তৈরির default permission-এর ওপর restriction/mask apply করে।

### 9. `ss -lntup` কী দেখায়?

Listening network sockets-এর TCP/UDP information এবং process information।

### 10. UFW কী?

Ubuntu/Debian systems-এ firewall management-এর একটি beginner-friendly interface/tool।

### 11. SELinux কী?

Linux-এর একটি Mandatory Access Control security framework।

### 12. AppArmor কী?

Application profiles-এর মাধ্যমে access restrictions enforce করার Linux security framework।

---

# 💀 Advanced Interview Questions

### 13. DAC এবং MAC-এর difference?

```text
DAC
→ owner/group/permission based access

MAC
→ centrally defined security policies enforce access
```

---

### 14. Service running কিন্তু connection হচ্ছে না—কী check করবে?

```text
systemctl status
      ↓
ss -lntup
      ↓
bind address
      ↓
firewall
      ↓
routing/network
      ↓
logs
```

---

### 15. Permission denied হলে কীভাবে troubleshoot করবে?

```bash
ls -l
```

তারপর:

```bash
id
```

তারপর path permissions:

```bash
namei -l /path/to/file
```

তারপর ownership/ACL/security policy relevant কিনা investigate করবে।

---

### 16. কেন `chmod 777` security best practice নয়?

কারণ owner/group/others সবাইকে broad read/write/execute permission দেয় এবং unnecessary access তৈরি করতে পারে।

---

### 17. SSH hardening-এর basic principles কী?

High-level:

```text
Use strong authentication
Protect private keys
Limit access to authorized users
Use least privilege
Keep SSH software updated
Monitor authentication logs
Avoid unnecessary exposure
```

---

# 🧠 LEVEL 9 FINAL INTERVIEW SCENARIO

Interviewer:

> **“A web server is running, but users cannot connect. How do you troubleshoot it securely?”**

একটি strong answer:

```text
1. Check service
   ↓
systemctl status nginx

2. Check listening port
   ↓
ss -lntp

3. Check bind address
   ↓
127.0.0.1 vs server interface

4. Check firewall
   ↓
ufw / firewalld

5. Check network
   ↓
ip addr
ip route

6. Check logs
   ↓
journalctl
application logs

7. Check security policy
   ↓
SELinux / AppArmor

8. Fix only the required permission/rule
   ↓
Verify
```

এখানে সবচেয়ে important হলো:

> **Security problem solve করতে গিয়ে security control disable করা নয়; root cause identify করে minimum required change করা।**

---

# 🏆 Level 9 Must-Know Cheat Sheet

```text
whoami
id
groups

sudo
sudo -l
visudo

ls -l
chmod
chown
umask
namei -l

ssh
~/.ssh/
authorized_keys
/etc/ssh/sshd_config

ss -lntup

ufw status
ufw status numbered

firewall-cmd --state
firewall-cmd --get-active-zones

getenforce
sestatus
aa-status

journalctl
journalctl -u ssh
journalctl -p err -b

systemctl --failed
```

## 🔐 Level 9-এর Core Mental Model

```text
          Linux Security
                │
      ┌─────────┼─────────┐
      ↓         ↓         ↓
 Authentication Authorization Logging
      │         │         │
      ↓         ↓         ↓
    SSH      sudo/ACL    journal
                │
                ↓
         Least Privilege
                │
       ┌────────┴────────┐
       ↓                 ↓
   Firewall          MAC Security
   UFW/firewalld     SELinux/AppArmor
```

**Level 10**-এ আমরা Linux-এর **Shell Scripting & Automation** শুরু করব—Bash variables, quoting, arguments, `if/else`, loops, functions, exit codes, `$?`, `&&`, `||`, `case`, `read`, command substitution, scripts, debugging, `cron` এবং practical automation—সবকিছু beginner mistakes ও interview questionsসহ।


---
# 🐧 Linux A–Z — LEVEL 10

## ⚙️ Bash Shell Scripting & Automation

Level 10-এ আমরা Linux-এর সবচেয়ে useful skillগুলোর একটি শিখব: **Bash scripting**।

এখন পর্যন্ত তুমি command manually চালিয়েছ। এবার আমরা শিখব কীভাবে অনেকগুলো command একসাথে script বানিয়ে **automate** করা যায়।

---

# 1. Shell Script কী?

Shell script হলো একটি text file যেখানে এক বা একাধিক shell command লেখা থাকে।

উদাহরণ:

```bash
#!/bin/bash

echo "Hello Linux"
pwd
ls
```

ধরো file-এর নাম:

```text
hello.sh
```

Run:

```bash
bash hello.sh
```

অথবা executable করে:

```bash
chmod +x hello.sh
./hello.sh
```

---

# 2. Bash কী?

Bash = **Bourne Again Shell**

এটি Linux-এ বহুল ব্যবহৃত shell।

Check:

```bash
echo $SHELL
```

আর:

```bash
bash --version
```

---

# 3. Shell বনাম Bash

```text
Shell
→ একটি command interpreter-এর category/interface

Bash
→ একটি নির্দিষ্ট shell
```

অন্য shell:

```text
bash
zsh
fish
sh
```

---

# 4. প্রথম Bash Script ⭐

File তৈরি:

```bash
nano hello.sh
```

লিখো:

```bash
#!/bin/bash

echo "Hello from Bash"
echo "Linux is powerful"
```

Save করে:

```bash
bash hello.sh
```

Output:

```text
Hello from Bash
Linux is powerful
```

---

# 5. Shebang কী?

প্রথম line:

```bash
#!/bin/bash
```

এটাকে **shebang** বলা হয়।

এটি system-কে জানায় script কোন interpreter দিয়ে execute করা হবে।

Example:

```bash
#!/bin/bash
```

মানে Bash ব্যবহার করো।

---

# 6. Script Executable করা

প্রথমে:

```bash
chmod +x hello.sh
```

তারপর:

```bash
./hello.sh
```

এখানে:

```text
./
```

মানে current directory।

---

# 7. Variable কী?

Variable-এ value রাখা যায়।

```bash
name="Rahim"
```

তারপর:

```bash
echo "$name"
```

Output:

```text
Rahim
```

### Important

এভাবে লিখবে না:

```bash
name = "Rahim"
```

❌ Bash variable assignment-এ `=`-এর দুই পাশে space দেওয়া যায় না।

সঠিক:

```bash
name="Rahim"
```

---

# 8. Variable Access

Variable ব্যবহার করতে:

```bash
$name
```

Example:

```bash
name="Linux"

echo $name
```

আরও ভালো practice:

```bash
echo "$name"
```

---

# 9. Double Quotes কেন ব্যবহার করব?

ধরো:

```bash
name="Linux User"
```

তাহলে:

```bash
echo "$name"
```

একটি value হিসেবে treat করা সহজ হয়।

Shell scripting-এ quoting খুব গুরুত্বপূর্ণ।

---

# 10. Single vs Double Quotes

### Double quote

```bash
name="Rahim"
echo "$name"
```

Variable expansion হয়।

Output:

```text
Rahim
```

### Single quote

```bash
echo '$name'
```

Output:

```text
$name
```

সহজভাবে:

```text
"$name"
→ variable expand করবে

'$name'
→ literal text হিসেবে রাখবে
```

---

# 11. Command Substitution ⭐

একটি command-এর output variable-এ রাখা যায়:

```bash
current_dir=$(pwd)
```

তারপর:

```bash
echo "$current_dir"
```

আরেকটি example:

```bash
today=$(date)
echo "$today"
```

পুরোনো syntax:

```bash
today=`date`
```

কাজ করতে পারে, কিন্তু modern Bash scripting-এ:

```bash
$(date)
```

বেশি readable।

---

# 12. Environment Variable

কিছু variables shell/environment থেকে আসে।

দেখো:

```bash
echo "$HOME"
```

```bash
echo "$USER"
```

```bash
echo "$PATH"
```

Common variables:

| Variable | Meaning                   |
| -------- | ------------------------- |
| `$HOME`  | User home directory       |
| `$USER`  | Current username          |
| `$SHELL` | Current/default shell     |
| `$PWD`   | Current working directory |
| `$PATH`  | Command search paths      |

---

# 13. `$PATH` কী?

যখন তুমি লিখো:

```bash
ls
```

Shell কোথায় `ls` executable আছে তা খুঁজে।

এই search locations-এর তালিকা:

```bash
echo "$PATH"
```

Example:

```text
/usr/local/bin:/usr/bin:/bin
```

---

# 14. `which` এবং `command -v`

কোন command কোথা থেকে আসছে দেখতে:

```bash
which bash
```

আর Bash-এ:

```bash
command -v bash
```

`command -v` অনেক ক্ষেত্রে আরও useful।

---

# 15. User Input নেওয়া

```bash
read name
echo "Hello $name"
```

আর prompt সহ:

```bash
read -p "Enter your name: " name
echo "Hello $name"
```

Example:

```text
Enter your name: Rahim
Hello Rahim
```

---

# 16. Script Arguments ⭐

Script run করার সময় value দেওয়া যায়:

```bash
./hello.sh Rahim
```

Script:

```bash
#!/bin/bash

echo "Hello $1"
```

Output:

```text
Hello Rahim
```

---

# 17. Important Positional Parameters

```text
$0
$1
$2
$3
...
```

Meaning:

```text
$0 → script name
$1 → first argument
$2 → second argument
```

Example:

```bash
./test.sh Linux Beginner
```

তাহলে:

```text
$0 = ./test.sh
$1 = Linux
$2 = Beginner
```

---

# 18. `$#`

`$#` = number of positional arguments।

Example:

```bash
echo "$#"
```

Run:

```bash
./test.sh one two three
```

Output:

```text
3
```

---

# 19. `$@`

`"$@"` সাধারণত সব positional arguments আলাদাভাবে preserve করে iterate করার জন্য useful।

Example:

```bash
for arg in "$@"
do
    echo "$arg"
done
```

Run:

```bash
./test.sh Linux Bash Docker
```

Output:

```text
Linux
Bash
Docker
```

---

# 20. `$?` — Exit Status ⭐⭐⭐

এটা interview-এর জন্য খুব important।

একটি command শেষ হওয়ার পর:

```bash
echo $?
```

আগের command সফল হলে সাধারণত:

```text
0
```

আর non-zero value হলে failure/error condition indicate করতে পারে।

Example:

```bash
ls /tmp
echo $?
```

সাধারণত:

```text
0
```

---

# 21. Exit Code কেন Important?

Automation-এ script বুঝতে পারে command সফল হয়েছে কি না।

```text
0
→ success

non-zero
→ some failure/error condition
```

---

# 22. `if` Statement

Basic:

```bash
if [ "$name" = "Rahim" ]; then
    echo "Hello Rahim"
fi
```

Structure:

```text
if condition
then
    command
fi
```

---

# 23. `if / else`

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
else
    echo "Under 18"
fi
```

তবে বয়স-related logic বাস্তবে ব্যবহার করলে local laws/policies আলাদা হতে পারে; এখানে এটি শুধু Bash condition শেখানোর example।

---

# 24. Common Comparison Operators

### String

```bash
=
!=
```

### Numbers

```bash
-eq
-ne
-gt
-ge
-lt
-le
```

Meaning:

```text
-eq → equal
-ne → not equal
-gt → greater than
-ge → greater/equal
-lt → less than
-le → less/equal
```

---

# 25. File Tests ⭐

Linux scripting-এ খুব useful:

```bash
-f file
```

Regular file আছে?

```bash
-d directory
```

Directory আছে?

```bash
-e path
```

Path exists?

```bash
-r file
```

Readable?

```bash
-w file
```

Writable?

```bash
-x file
```

Executable?

---

# 26. File Check Example

```bash
if [ -f "/etc/hosts" ]; then
    echo "File exists"
else
    echo "File not found"
fi
```

---

# 27. Directory Check

```bash
if [ -d "$HOME" ]; then
    echo "Home directory exists"
fi
```

---

# 28. `&&`

দুটি command conditionally chain করতে:

```bash
command1 && command2
```

মানে:

> command1 successful হলে command2 চালাও।

Example:

```bash
mkdir backup && echo "Created"
```

---

# 29. `||`

```bash
command1 || command2
```

মানে:

> command1 fail করলে command2 চালাও।

Example:

```bash
cd /wrong/path || echo "Directory not found"
```

---

# 30. `&&` + `||`

Example:

```bash
mkdir backup && echo "Success" || echo "Failed"
```

তবে complex logic-এ `if` ব্যবহার করলে code বেশি readable হতে পারে।

---

# 31. `case` Statement

অনেক option handle করার জন্য useful।

```bash
case "$1" in
    start)
        echo "Starting"
        ;;
    stop)
        echo "Stopping"
        ;;
    restart)
        echo "Restarting"
        ;;
    *)
        echo "Unknown option"
        ;;
esac
```

Run:

```bash
./service.sh start
```

---

# 32. `for` Loop ⭐

একাধিক item-এর উপর একই কাজ:

```bash
for name in Rahim Karim Hasan
do
    echo "Hello $name"
done
```

Output:

```text
Hello Rahim
Hello Karim
Hello Hasan
```

---

# 33. File Loop

```bash
for file in *.txt
do
    echo "$file"
done
```

Current directory-এর `.txt` files iterate করবে।

---

# 34. `while` Loop

Condition true থাকা পর্যন্ত চলবে।

```bash
count=1

while [ "$count" -le 5 ]
do
    echo "$count"
    count=$((count + 1))
done
```

Output:

```text
1
2
3
4
5
```

---

# 35. Arithmetic

Bash-এ:

```bash
a=10
b=5

sum=$((a + b))

echo "$sum"
```

Output:

```text
15
```

আর:

```bash
x=$((x + 1))
```

---

# 36. Function ⭐

Repeated code organize করতে function ব্যবহার করা হয়।

```bash
greet() {
    echo "Hello Linux"
}

greet
```

Output:

```text
Hello Linux
```

---

# 37. Function with Argument

```bash
greet() {
    echo "Hello $1"
}

greet "Rahim"
```

Output:

```text
Hello Rahim
```

Function-এর `$1` function-এর argument হিসেবে কাজ করে।

---

# 38. Return Status

Function:

```bash
check_file() {
    if [ -f "$1" ]; then
        return 0
    else
        return 1
    fi
}
```

তারপর:

```bash
if check_file "/etc/hosts"; then
    echo "File exists"
else
    echo "File missing"
fi
```

---

# 39. `exit`

Script-এর execution stop করতে:

```bash
exit 0
```

Success:

```text
0
```

Failure-এর জন্য appropriate non-zero code ব্যবহার করা যায়:

```bash
exit 1
```

---

# 40. `set -e`

Script-এ:

```bash
set -e
```

ব্যবহার করলে কিছু command failure-এর ক্ষেত্রে script early exit করতে পারে।

কিন্তু এটাকে magic safety switch ভাববে না।

Complex scripts-এ error handling বুঝে ব্যবহার করতে হয়।

---

# 41. `set -u`

```bash
set -u
```

Unset variables-এর accidental use ধরতে সাহায্য করতে পারে।

একসাথে common strict mode:

```bash
set -euo pipefail
```

এটি useful, কিন্তু beginner হিসেবে প্রতিটি অংশ কী করে তা বুঝে ব্যবহার করা উচিত।

---

# 42. `pipefail`

Normal pipeline:

```bash
command1 | command2
```

শেষ command-এর status গুরুত্বপূর্ণ হতে পারে।

`pipefail` pipeline-এর আগের command failure detect করতে সাহায্য করে।

Example:

```bash
set -o pipefail
```

---

# 43. Script Debugging ⭐

একটি script debug করতে:

```bash
bash -x script.sh
```

এতে commands execution trace দেখা যায়।

আর script-এর ভিতরে:

```bash
set -x
```

এবং বন্ধ:

```bash
set +x
```

---

# 44. Syntax Check

Script execute না করে syntax check:

```bash
bash -n script.sh
```

এটা beginnerদের জন্য খুব useful।

---

# 45. ShellCheck

Bash script-এর common problems ধরতে **ShellCheck** খুব জনপ্রিয় static-analysis tool।

যেমন:

```bash
shellcheck script.sh
```

যদি system-এ installed থাকে।

এটি:

* quoting problems
* suspicious constructs
* common Bash mistakes

ধরতে সাহায্য করতে পারে।

---

# 46. Practical Script — Disk Check

একটি simple monitoring script:

```bash
#!/bin/bash

usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

if [ "$usage" -ge 80 ]; then
    echo "Warning: disk usage is ${usage}%"
else
    echo "Disk usage is ${usage}%"
fi
```

এখানে আমরা combine করেছি:

```text
df
awk
tr
variable
if
comparison
```

এটাই scripting-এর real power।

---

# 47. Practical Script — Backup

ধরো নিজের home-এর একটি directory backup করতে চাও।

```bash
#!/bin/bash

SOURCE="$HOME/Documents"
DEST="$HOME/backup"

mkdir -p "$DEST"

cp -r "$SOURCE" "$DEST"

echo "Backup completed"
```

এটা basic example। Real backup system-এ `rsync` এবং proper error handling বেশি appropriate হতে পারে।

---

# 48. `cron` — Automation ⭐⭐⭐

`cron` নির্দিষ্ট সময়/interval-এ command বা script চালাতে সাহায্য করে।

User crontab:

```bash
crontab -e
```

দেখতে:

```bash
crontab -l
```

---

# 49. Cron Format

Basic format:

```text
minute hour day-of-month month day-of-week command
```

Example:

```text
0 2 * * * /home/user/backup.sh
```

মানে সাধারণভাবে:

> প্রতিদিন রাত 2:00-এ script চালানোর schedule।

---

# 50. Cron-এর 5 Fields

```text
* * * * *
│ │ │ │ │
│ │ │ │ └── day of week
│ │ │ └──── month
│ │ └────── day of month
│ └──────── hour
└────────── minute
```

---

# 51. Cron Common Mistakes

### Mistake 1

Script manually কাজ করে, কিন্তু cron-এ কাজ করে না।

কারণ cron-এর environment interactive shell-এর মতো নয়।

বিশেষ করে:

```text
PATH
HOME
working directory
environment variables
```

ভিন্ন হতে পারে।

তাই scripts-এ absolute paths এবং explicit configuration useful।

---

# 52. Cron Output Log

Cron job debug করতে output redirect করতে পারো:

```text
0 2 * * * /home/user/backup.sh >> /home/user/backup.log 2>&1
```

এখানে:

```text
>> 
```

output append করে।

```text
2>&1
```

stderr-কে stdout-এর destination-এ পাঠায়।

---

# 53. Cron vs systemd Timer

Modern Linux systems-এ scheduled tasks-এর জন্য systemd timers-ও ব্যবহৃত হয়।

Conceptually:

```text
cron
→ traditional scheduler

systemd timer
→ systemd-integrated scheduler
```

Level 10-এ cron fundamentals শিখলেই যথেষ্ট; systemd timers পরে deeperভাবে শেখা যাবে।

---

# 🚨 Level 10 Beginner Mistakes

## Mistake 1 — Variable-এর পাশে spaces

❌

```bash
name = "Rahim"
```

সঠিক:

```bash
name="Rahim"
```

---

## Mistake 2 — Unquoted variables

❌

```bash
rm $file
```

যদি filename-এ spaces থাকে, unexpected word splitting হতে পারে।

সাধারণভাবে:

```bash
rm -- "$file"
```

এর মতো quoting safer।

---

## Mistake 3 — `$?` দেরিতে check করা

```bash
command1
command2

echo "$?"
```

এখানে `$?` সাধারণত `command2`-এর status।

যদি command1-এর status দরকার:

```bash
command1
status=$?
command2

echo "$status"
```

---

## Mistake 4 — `rm -rf` blindly script-এ ব্যবহার

Automation-এ destructive commands অত্যন্ত carefully handle করতে হয়।

প্রথমে path validate করো।

---

## Mistake 5 — Relative paths in cron

Cron-এ:

```bash
./backup.sh
```

সমস্যা করতে পারে।

বরং:

```text
/home/user/backup.sh
```

এর মতো absolute path বেশি predictable।

---

## Mistake 6 — Shell script-এ password hard-code করা

❌

```bash
password="mysecret"
```

এটা security risk।

Credentials-এর জন্য appropriate secret-management approach ব্যবহার করতে হয়।

---

## Mistake 7 — Bash script-এ syntax error

Check:

```bash
bash -n script.sh
```

---

# 🧪 LEVEL 10 PRACTICAL LAB

## Lab 1 — Hello Script

```bash
nano hello.sh
```

```bash
#!/bin/bash

echo "Hello Linux"
echo "User: $USER"
echo "Home: $HOME"
```

Run:

```bash
bash hello.sh
```

---

## Lab 2 — Arguments

Script:

```bash
#!/bin/bash

echo "Script: $0"
echo "First: $1"
echo "Second: $2"
echo "Total arguments: $#"
```

Run:

```bash
bash test.sh Linux Bash
```

---

## Lab 3 — File Check

```bash
#!/bin/bash

if [ -f "/etc/hosts" ]; then
    echo "hosts file exists"
else
    echo "hosts file missing"
fi
```

---

## Lab 4 — Loop

```bash
#!/bin/bash

for file in /etc/*.conf
do
    echo "$file"
done
```

---

## Lab 5 — Function

```bash
#!/bin/bash

show_info() {
    echo "User: $USER"
    echo "Home: $HOME"
    echo "Directory: $PWD"
}

show_info
```

---

## Lab 6 — Debugging

```bash
bash -n script.sh
```

তারপর:

```bash
bash -x script.sh
```

দুইটার difference observe করো।

---

# 🎯 Level 10 Interview Questions

## Beginner

### 1. Shell script কী?

একটি text file যেখানে shell commands এবং programming constructs ব্যবহার করে automation করা হয়।

### 2. Bash কী?

একটি Unix/Linux shell এবং scripting language environment।

### 3. Shebang কী?

যেমন:

```bash
#!/bin/bash
```

এটি script-এর interpreter নির্দেশ করে।

### 4. Script executable কীভাবে করবে?

```bash
chmod +x script.sh
```

তারপর:

```bash
./script.sh
```

### 5. `$1` কী?

Script-এর first positional argument।

---

# 🔥 Intermediate Interview

### 6. `$?` কী?

সর্বশেষ executed command-এর exit status।

### 7. `$#` কী?

Positional arguments-এর সংখ্যা।

### 8. `$@` কী?

Positional arguments-এর collection; `"$@"` প্রতিটি argument আলাদাভাবে preserve করে iterate করতে useful।

### 9. `>` এবং `>>` difference?

```text
>  → overwrite
>> → append
```

### 10. `&&` কী?

আগের command successful হলে পরের command চালায়।

### 11. `||` কী?

আগের command fail করলে পরের command চালায়।

### 12. `bash -n` কী?

Script-এর syntax check করতে ব্যবহার করা যায়।

### 13. `bash -x` কী?

Script execution trace/debug output দেখাতে সাহায্য করে।

---

# 💀 Advanced Interview Questions

### 14. কেন shell script-এ quoting গুরুত্বপূর্ণ?

কারণ spaces, globbing, word splitting এবং special characters-এর কারণে unquoted values unexpected behaviour তৈরি করতে পারে।

---

### 15. `$?` কীভাবে ভুলভাবে ব্যবহার হতে পারে?

```bash
command1
command2
echo "$?"
```

এখানে `echo "$?"` সাধারণত `command2`-এর status দেখাবে, `command1`-এর নয়।

---

### 16. Cron script manually কাজ করে কিন্তু cron-এ কাজ করে না কেন?

সম্ভাব্য কারণ:

```text
Different PATH
Different environment
Different working directory
Missing permissions
Relative paths
Missing environment variables
```

---

### 17. `chmod +x` এবং `bash script.sh`-এর difference?

```text
bash script.sh
→ Bash interpreter দিয়ে file execute করা হচ্ছে

./script.sh
→ file executable হতে হবে এবং shebang অনুযায়ী interpreter ব্যবহৃত হবে
```

---

### 18. `set -euo pipefail` কী?

Common Bash scripting pattern:

```bash
set -euo pipefail
```

এতে:

```text
-e → কিছু command failure-এ early exit behaviour
-u → unset variable reference detect করতে সাহায্য
pipefail → pipeline-এর ভেতরের failure propagate করতে সাহায্য
```

তবে complex scripts-এ এগুলোর semantics বুঝে ব্যবহার করতে হয়।

---

# 🧠 LEVEL 10 FINAL INTERVIEW SCENARIO

Interviewer:

> **“You need to automatically check disk usage every day and report if it exceeds a threshold. How would you design it?”**

একটি ভালো approach:

```text
1. Write Bash script
        ↓
2. Get disk usage with df
        ↓
3. Extract percentage
        ↓
4. Compare with threshold
        ↓
5. Print/log result
        ↓
6. Test manually
        ↓
7. bash -n / ShellCheck
        ↓
8. Schedule with cron/systemd timer
        ↓
9. Check logs/output
```

Example core logic:

```bash
#!/bin/bash

usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

if [ "$usage" -ge 80 ]; then
    echo "WARNING: disk usage is ${usage}%"
else
    echo "OK: disk usage is ${usage}%"
fi
```

---

# 🏆 LEVEL 10 MUST-KNOW CHEAT SHEET

```bash
#!/bin/bash

name="Linux"
echo "$name"

read -p "Name: " name

echo "$0"
echo "$1"
echo "$#"
echo "$@"
echo "$?"

result=$(pwd)

if [ -f "$file" ]; then
    echo "exists"
fi

for file in *.txt; do
    echo "$file"
done

while [ condition ]; do
    ...
done

case "$1" in
    start) ... ;;
    stop) ... ;;
esac

function_name() {
    ...
}

command1 && command2
command1 || command2

bash -n script.sh
bash -x script.sh

crontab -e
crontab -l
```

## 🧠 Level 10-এর Core Mental Model

```text
Manual Commands
      ↓
Variables
      ↓
Conditions
      ↓
Loops
      ↓
Functions
      ↓
Exit Codes
      ↓
Error Handling
      ↓
Bash Script
      ↓
Cron / Automation
```

**Level 11**-এ Linux-এর **Storage & Disk Management** শেখা হবে—`lsblk`, `fdisk`, `parted`, partitions, filesystem, `mkfs`, `mount`, `/etc/fstab`, UUID, LVM, `df`, `du`, inode, disk-full troubleshooting এবং interview scenarios।

---
# 🐧 Linux A–Z — LEVEL 11

# 💾 Storage, Disk & Filesystem Management

Level 11-এ আমরা Linux-এর **disk/storage system** শিখব। এটা Linux administrator, DevOps, Cloud এবং System Engineer-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 1. Storage-এর Basic Mental Model

একটা Linux server-এ storage সাধারণত এভাবে ভাবতে পারো:

```text
Physical Disk
     ↓
Partition
     ↓
Filesystem
     ↓
Mount Point
     ↓
Files & Directories
```

আর advanced setup:

```text
Disk
 ↓
Partition
 ↓
LVM Physical Volume
 ↓
Volume Group
 ↓
Logical Volume
 ↓
Filesystem
 ↓
Mount Point
```

---

# 2. Disk কী?

Disk হলো physical বা virtual storage device।

উদাহরণ:

```text
/dev/sda
/dev/sdb
/dev/nvme0n1
```

এগুলো Linux-এর কাছে block devices হিসেবে দেখা যায়।

---

# 3. `/dev` কী?

Linux-এ device files সাধারণত:

```text
/dev/
```

এর মধ্যে থাকে।

Example:

```text
/dev/sda
/dev/sda1
/dev/sda2
/dev/nvme0n1
/dev/nvme0n1p1
```

---

# 4. `lsblk` ⭐

Disk এবং partition দেখার সবচেয়ে useful command:

```bash
lsblk
```

Example:

```text
NAME        SIZE TYPE MOUNTPOINTS
sda         100G disk
├─sda1       96G part /
└─sda2        4G part [SWAP]
```

এখানে:

```text
sda  → disk
sda1 → partition
sda2 → partition
```

---

# 5. `lsblk -f`

Filesystem information দেখতে:

```bash
lsblk -f
```

Example:

```text
NAME   FSTYPE FSVER LABEL UUID                                 MOUNTPOINTS
sda1   ext4         root  1234-ABCD                            /
sda2   swap         ...   ...
```

এখানে গুরুত্বপূর্ণ:

```text
FSTYPE
UUID
MOUNTPOINTS
```

---

# 6. Filesystem কী?

Filesystem হলো disk-এর মধ্যে files/directories কীভাবে organize এবং manage হবে তার structure।

Common Linux filesystems:

```text
ext4
XFS
Btrfs
```

সবচেয়ে common traditional Linux filesystem-এর একটি:

```text
ext4
```

---

# 7. Partition কী?

একটি disk-কে logical অংশে ভাগ করা যায়।

ধরো:

```text
100 GB Disk
│
├── 20 GB → partition 1
└── 80 GB → partition 2
```

Linux-এ:

```text
/dev/sda1
/dev/sda2
```

---

# 8. Partition Table

Disk partitioning-এর জন্য প্রধান দুই ধরনের scheme:

```text
MBR
GPT
```

Modern systems-এ GPT খুব common।

আগের Level-এ আমরা দেখেছি:

```text
BIOS/UEFI
```

আর এখানে:

```text
MBR/GPT
```

এগুলো একই জিনিস নয়।

```text
UEFI → firmware interface
GPT  → partitioning scheme
```

---

# 9. `fdisk`

Partition information/manage করার classic tool:

```bash
sudo fdisk -l
```

এটি disk এবং partition সম্পর্কে তথ্য দেখাতে পারে।

⚠️ Partition modify/delete করার command খুব carefully ব্যবহার করতে হয়।

---

# 10. `parted`

আরেকটি partition management tool:

```bash
sudo parted -l
```

Modern partitioning environments-এ `parted` useful।

---

# 11. ⚠️ Beginner Warning

এই ধরনের command ভুল disk-এ দিলে data loss হতে পারে:

```text
fdisk
parted
mkfs
dd
```

বিশেষ করে:

```bash
mkfs
```

filesystem তৈরি করতে গিয়ে existing data destroy করতে পারে।

তাই production disk-এ command দেওয়ার আগে **device name verify** করা অত্যন্ত জরুরি।

---

# 12. `df` ⭐⭐⭐

Filesystem কতটা full তা দেখার command:

```bash
df
```

Human-readable:

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   28G  42% /
```

---

# 13. `df -h` Output বুঝি

```text
Size
Used
Avail
Use%
Mounted on
```

যেমন:

```text
50G
20G
28G
42%
/
```

মানে root filesystem-এর প্রায় 42% ব্যবহৃত।

---

# 14. `df -T`

Filesystem type দেখতে:

```bash
df -T
```

Example:

```text
Filesystem     Type  1K-blocks     Used Available Use% Mounted on
/dev/sda1      ext4
```

---

# 15. `du` ⭐⭐⭐

`df` এবং `du`-এর difference খুব important।

### `df`

Filesystem কতটা full?

```bash
df -h
```

### `du`

কোন directory/file কত space ব্যবহার করছে?

```bash
du -sh /var/log
```

---

# 16. `du -sh`

```bash
du -sh /home/user
```

Example:

```text
8.4G    /home/user
```

---

# 17. কোন subdirectory বেশি বড়?

```bash
du -h --max-depth=1 /home/user
```

Example:

```text
2.1G /home/user/Documents
5.0G /home/user/Videos
1.3G /home/user/.cache
8.4G /home/user
```

তখন বুঝতে পারবে কোন directory বেশি storage নিচ্ছে।

---

# 18. Large Files খোঁজা

Level 2-এর `find` কাজে লাগবে:

```bash
find /home/user -type f -size +1G
```

মানে 1 GB-এর বেশি files খুঁজবে।

আর:

```bash
find /var -type f -size +100M
```

---

# 19. `sort` দিয়ে সাজানো

যেমন:

```bash
du -h --max-depth=1 /var | sort -h
```

এতে ছোট থেকে বড় size অনুযায়ী output সাজাতে সাহায্য করবে।

---

# 20. Mount কী? ⭐⭐⭐

Linux-এ filesystem ব্যবহার করতে সেটাকে directory-এর সাথে attach করা হয়।

এটাকে **mount** বলা হয়।

উদাহরণ:

```text
Disk
 ↓
Filesystem
 ↓
/data
```

তারপর:

```bash
cd /data
```

করলে সেই mounted filesystem-এর contents দেখতে পারবে।

---

# 21. Mount Point কী?

যে directory-তে filesystem attach করা হয় সেটাই mount point।

Common examples:

```text
/
/home
/boot
/mnt
/media
/data
```

---

# 22. `mount`

Current mounted filesystems:

```bash
mount
```

আর readable output:

```bash
findmnt
```

---

# 23. `findmnt` ⭐

Mount relationship বুঝতে খুব useful:

```bash
findmnt
```

Specific filesystem:

```bash
findmnt /
```

---

# 24. Manual Mount

ধরো `/dev/sdb1`-এ filesystem আছে।

প্রথমে mount point:

```bash
sudo mkdir /data
```

তারপর:

```bash
sudo mount /dev/sdb1 /data
```

Check:

```bash
df -h
```

অথবা:

```bash
findmnt /data
```

---

# 25. Unmount

Unmount:

```bash
sudo umount /data
```

⚠️ Command হলো:

```bash
umount
```

`unmount` নয়।

---

# 26. কেন `umount` fail করতে পারে?

যদি কোনো process ওই filesystem-এর directory ব্যবহার করে থাকে।

Example:

```text
target is busy
```

তখন:

```bash
pwd
```

দেখো তুমি mounted directory-এর ভিতরে আছো কি না।

তারপর:

```bash
cd ~
```

এবং আবার:

```bash
sudo umount /data
```

---

# 27. `/etc/fstab` ⭐⭐⭐

Linux boot-এর সময় কোন filesystem কোথায় mount হবে তা configure করার জন্য:

```text
/etc/fstab
```

ব্যবহার করা হয়।

Example concept:

```text
UUID=xxxx-xxxx  /data  ext4  defaults  0  2
```

---

# 28. `fstab` Fields

সাধারণভাবে:

```text
device
mount point
filesystem type
options
dump
fsck order
```

Example:

```text
UUID=abc123 /data ext4 defaults 0 2
```

---

# 29. UUID কী?

UUID = **Universally Unique Identifier**

Filesystem-এর unique identifier হিসেবে ব্যবহার করা যায়।

দেখতে:

```bash
blkid
```

Example:

```text
/dev/sda1: UUID="abcd-1234" TYPE="ext4"
```

---

# 30. UUID কেন ব্যবহার করা হয়?

Device naming সবসময় একইভাবে ধরে নেওয়া ভালো নয়।

যেমন:

```text
/dev/sda
/dev/sdb
```

এর order পরিবর্তিত হতে পারে।

তাই `/etc/fstab`-এ UUID ব্যবহার করলে system নির্দিষ্ট filesystem identify করতে পারে।

---

# 31. `blkid`

Filesystem এবং UUID দেখতে:

```bash
sudo blkid
```

Example:

```text
/dev/sda1: UUID="1234-ABCD" TYPE="ext4"
```

---

# 32. `mount -a` ⭐

`/etc/fstab`-এর entries test/apply করার জন্য:

```bash
sudo mount -a
```

এটা গুরুত্বপূর্ণ।

### কিন্তু সতর্কতা

`fstab`-এ ভুল entry থাকলে boot problem হতে পারে।

তাই editing-এর পরে:

```bash
sudo mount -a
```

দিয়ে configuration test করা ভালো practice।

---

# 33. Filesystem তৈরি — `mkfs`

ধরো একটি নতুন partition আছে:

```text
/dev/sdb1
```

ext4 filesystem তৈরি করার command:

```bash
sudo mkfs.ext4 /dev/sdb1
```

⚠️ এটি existing filesystem/data destroy করতে পারে।

**Production disk-এ না বুঝে ব্যবহার করবে না।**

---

# 34. Filesystem Check

ext filesystem-এর জন্য:

```bash
fsck
```

এটি filesystem consistency checking-এর জন্য ব্যবহৃত হয়।

⚠️ সাধারণভাবে mounted filesystem-এর উপর filesystem repair/check blindly চালানো উচিত নয়।

Filesystem-specific tools এবং proper maintenance procedure follow করতে হয়।

---

# 35. Inode কী? ⭐⭐⭐

এটি interview-এর খুব common topic।

Linux filesystem-এ inode file সম্পর্কে metadata রাখে।

যেমন:

```text
permissions
owner
group
file size
timestamps
links
data block references
```

সহজভাবে:

```text
Filename
   ↓
inode
   ↓
file data
```

---

# 36. Inode Full Problem

একটি filesystem-এর storage free থাকতে পারে, কিন্তু inode শেষ হয়ে যেতে পারে।

Check:

```bash
df -i
```

Example:

```text
Filesystem     Inodes  IUsed  IFree IUse%
/dev/sda1      1M     1M     0     100%
```

তখন নতুন file তৈরি করতে সমস্যা হতে পারে—even if `df -h`-এ space available থাকে।

---

# 37. `df -h` বনাম `df -i`

```text
df -h
→ disk space

df -i
→ inode usage
```

Interview-এ মনে রাখবে।

---

# 38. LVM কী? ⭐⭐⭐

LVM = **Logical Volume Manager**

এটি storage management আরও flexible করে।

Basic structure:

```text
Physical Disk
      ↓
Physical Volume (PV)
      ↓
Volume Group (VG)
      ↓
Logical Volume (LV)
      ↓
Filesystem
      ↓
Mount Point
```

---

# 39. Physical Volume — PV

LVM-এর জন্য disk/partition prepare করা হলে সেটি Physical Volume হতে পারে।

Conceptual example:

```text
/dev/sdb1
    ↓
PV
```

---

# 40. Volume Group — VG

এক বা একাধিক PV combine করে Volume Group তৈরি করা যায়।

```text
PV1 ─┐
     ├── VG
PV2 ─┘
```

---

# 41. Logical Volume — LV

VG-এর মধ্যে logical volume তৈরি করা যায়।

```text
VG
│
├── LV1 → 20G
├── LV2 → 30G
└── LV3 → 10G
```

এরপর LV-এর উপর filesystem তৈরি করা যায়।

---

# 42. LVM Commands

PV:

```bash
pvs
pvdisplay
```

VG:

```bash
vgs
vgdisplay
```

LV:

```bash
lvs
lvdisplay
```

---

# 43. LVM কেন ব্যবহার করব?

Traditional partitioning:

```text
100G partition
```

পরে size পরিবর্তন করতে inconvenient হতে পারে।

LVM:

```text
VG
 ↓
LV
```

Storage allocation এবং resizing আরও flexible হতে পারে।

---

# 44. LVM Conceptual Example

ধরো:

```text
Disk 1 → 100G
Disk 2 → 100G
```

LVM:

```text
Disk 1 → PV ─┐
             ├── VG → 200G
Disk 2 → PV ─┘
```

তারপর:

```text
LV1 → 80G
LV2 → 50G
LV3 → 30G
```

বাকি space future use-এর জন্য রাখা যেতে পারে।

---

# 45. `lsblk` + `df` + `du`

Storage troubleshooting-এ তিনটি command খুব গুরুত্বপূর্ণ:

```bash
lsblk
df -h
du -sh
```

তাদের কাজ:

```text
lsblk
→ disk/partition structure

df -h
→ filesystem usage

du
→ কোন file/directory space নিচ্ছে
```

---

# 46. Disk Full Troubleshooting ⭐⭐⭐

ধরো application বলছে:

```text
No space left on device
```

প্রথম:

```bash
df -h
```

যদি filesystem full:

```bash
df -h
```

তারপর:

```bash
df -i
```

inode full কি না।

তারপর:

```bash
du -sh /*
```

অথবা নির্দিষ্ট directory:

```bash
du -h --max-depth=1 /var | sort -h
```

তারপর বড় directory identify করো।

---

# 47. Deleted File কিন্তু Space Free হয়নি

এটা interesting Linux scenario।

কোনো process একটি file open করে রেখেছে।

তারপর file delete করা হলো।

Filesystem-এর directory থেকে file disappear করতে পারে, কিন্তু process file descriptor ধরে রাখলে disk space সঙ্গে সঙ্গে ফেরত নাও আসতে পারে।

এটা investigate করতে:

```bash
sudo lsof +L1
```

`lsof` installed থাকলে।

---

# 48. `lsof`

`lsof` = **List Open Files**

Example:

```bash
sudo lsof /var/log
```

Linux-এ "everything is a file" concept-এর কারণে এটি troubleshooting-এ খুব useful।

---

# 49. Disk বনাম Partition বনাম Filesystem

এগুলো confuse করবে না:

```text
Disk
→ physical/virtual storage device

Partition
→ disk-এর logical section

Filesystem
→ data organize করার structure

Mount point
→ filesystem-এর directory attachment location
```

---

# 50. Real-World Example

ধরো server-এ নতুন 100GB disk এসেছে:

```text
/dev/sdb
```

Conceptual workflow:

```text
/dev/sdb
   ↓
partition
   ↓
filesystem
   ↓
mount point
   ↓
/data
```

তারপর:

```bash
df -h
```

দিয়ে verify করবে।

Production environment-এ exact partition/filesystem commands দেওয়ার আগে disk identity এবং backup/change procedure verify করতে হয়।

---

# 🚨 Level 11 Beginner Mistakes

### ❌ 1. `df` আর `du` এক মনে করা

```text
df → filesystem
du → files/directories
```

---

### ❌ 2. Wrong disk-এ `mkfs`

```bash
sudo mkfs.ext4 /dev/sda
```

ভুল device হলে catastrophic data loss হতে পারে।

---

### ❌ 3. `/etc/fstab` blindly edit করা

ভুল entry boot problem তৈরি করতে পারে।

Edit করার পরে:

```bash
sudo mount -a
```

দিয়ে test করা ভালো।

---

### ❌ 4. Mounted filesystem unmount না করে repair করা

Filesystem maintenance-এর আগে mounted/unmounted state এবং appropriate tool বুঝতে হবে।

---

### ❌ 5. `umount`-কে `unmount` লেখা

সঠিক:

```bash
umount
```

---

### ❌ 6. Disk space আছে কিন্তু file তৈরি হচ্ছে না

Check:

```bash
df -h
df -i
```

কারণ inode exhaustion হতে পারে।

---

# 🧪 LEVEL 11 HANDS-ON LAB

এগুলো safe inspection commands:

### Lab 1

```bash
lsblk
```

Disk structure দেখো।

### Lab 2

```bash
lsblk -f
```

Filesystem এবং UUID দেখো।

### Lab 3

```bash
df -h
```

Disk usage দেখো।

### Lab 4

```bash
df -i
```

inode usage দেখো।

### Lab 5

```bash
findmnt
```

কোন filesystem কোথায় mounted দেখো।

### Lab 6

```bash
du -sh "$HOME"
```

নিজের home directory কত space ব্যবহার করছে দেখো।

### Lab 7

```bash
du -h --max-depth=1 "$HOME" | sort -h
```

Home-এর কোন directory বেশি space নিচ্ছে দেখো।

### Lab 8

```bash
blkid
```

UUID এবং filesystem type দেখো।

### Lab 9

```bash
cat /etc/fstab
```

বর্তমান filesystem configuration দেখো।

**এখানে এখনই edit করবে না।**

---

# 🎯 LEVEL 11 INTERVIEW QUESTIONS

### Beginner

**1. Linux filesystem কী?**

Files এবং directories organize/manage করার structure।

**2. Partition কী?**

একটি disk-এর logical section।

**3. Mount point কী?**

যে directory-তে filesystem attach করা হয়।

**4. `df` কী করে?**

Filesystem-এর available/used space দেখায়।

**5. `du` কী করে?**

File/directory কত storage ব্যবহার করছে তা দেখায়।

**6. `lsblk` কী করে?**

Block devices, disks এবং partitions-এর structure দেখায়।

---

# 🔥 Intermediate

**7. `df -h` বনাম `df -i`?**

```text
df -h → disk space
df -i → inode usage
```

**8. UUID কী?**

Filesystem/device identify করার unique identifier।

**9. `/etc/fstab` কী?**

Filesystem mount configuration file।

**10. `mount -a` কী করে?**

`fstab`-এর applicable entries mount করার চেষ্টা করে।

**11. `umount` কখন ব্যবহার করি?**

Filesystem safely detach করার জন্য।

**12. `ext4` কী?**

একটি Linux filesystem।

---

# 💀 Advanced Interview

### 13. Disk 100% full হলে কীভাবে troubleshoot করবে?

```text
df -h
 ↓
কোন filesystem full?
 ↓
df -i
 ↓
inode full?
 ↓
du
 ↓
বড় directory/file identify
 ↓
logs/cache/application data investigate
 ↓
প্রয়োজনীয় cleanup/retention policy
 ↓
verify
```

---

### 14. `df -h` 80% কিন্তু `du` হিসাব মিলছে না কেন?

সম্ভাব্য কারণ:

* deleted-but-open files
* mount points-এর কারণে accounting difference
* filesystem reserved space
* filesystem-specific behaviour
* permissions-এর কারণে incomplete `du` scan

Investigation-এর জন্য:

```bash
sudo lsof +L1
```

সহ অন্যান্য checks করা যায়।

---

### 15. LVM-এর architecture কী?

```text
PV
 ↓
VG
 ↓
LV
 ↓
Filesystem
 ↓
Mount Point
```

---

### 16. Disk এবং filesystem-এর difference কী?

Disk হলো storage device; filesystem হলো সেই storage-এর মধ্যে data organize করার structure।

---

### 17. কেন UUID `fstab`-এ ব্যবহার করা হয়?

Device naming-এর পরিবর্তন/ordering-এর উপর কম নির্ভর করে নির্দিষ্ট filesystem identify করার জন্য।

---

# 🏆 LEVEL 11 FINAL SCENARIO

### Interviewer:

> “একটি Linux server বলছে `No space left on device`. তুমি কী করবে?”

একজন ভালো Linux administrator সরাসরি random file delete করবে না।

প্রথমে:

```bash
df -h
```

তারপর:

```bash
df -i
```

তারপর affected filesystem identify করে:

```bash
du -h --max-depth=1 /var | sort -h
```

প্রয়োজনে:

```bash
sudo lsof +L1
```

তারপর investigate করবে:

```text
Logs?
Application data?
Cache?
Deleted open files?
Inodes?
Unexpected growth?
```

তারপর approved cleanup/retention process অনুযায়ী action নেবে এবং শেষে:

```bash
df -h
```

দিয়ে verify করবে।

---

# 🧠 LEVEL 11 MASTER MAP

```text
                 STORAGE
                    │
        ┌───────────┴───────────┐
        │                       │
      Disk                  Filesystem
        │                       │
   Partition                  ext4/XFS
        │                       │
       LVM                    Mount
        │                       │
    PV → VG → LV              /data
        │
        └──────────────┐
                       ↓
                  Files/Dirs
```

### সবচেয়ে গুরুত্বপূর্ণ commands:

```bash
lsblk
lsblk -f
fdisk -l
parted -l
df -h
df -T
df -i
du -sh
findmnt
mount
umount
blkid
cat /etc/fstab
mount -a
pvs
vgs
lvs
lsof
```

**Level 11-এর মূল কথা:**
`lsblk` দিয়ে **কী storage আছে**, `df` দিয়ে **filesystem কতটা full**, `du` দিয়ে **কোথায় space যাচ্ছে**, আর LVM দিয়ে **storage কীভাবে flexibleভাবে manage করা যায়**—এই চারটি mental model ভালোভাবে আয়ত্ত করো।


---

যদি তুমি **Linux A–Z শেখার পুরো roadmap-এর কত % Level 11 পর্যন্ত cover হবে** জানতে চাও, তাহলে আনুমানিকভাবে:

### 📊 এখন পর্যন্ত Coverage

| Level | Topic                | Status   |
| ----- | -------------------- | -------- |
| 1     | Linux Fundamentals   | ✅        |
| 2     | Command Line         | ✅        |
| 3     | Users & Permissions  | ✅        |
| 4     | Package Management   | ✅        |
| 5     | Processes & Systemd  | ✅        |
| 6     | Networking           | ⚠️ আংশিক |
| 7     | Intermediate Linux   | ⚠️       |
| 8     | Boot Process         | ✅        |
| 9     | Security             | ✅        |
| 10    | Bash Scripting       | ✅        |
| 11    | Storage & Filesystem | ✅        |

**Level 11 পর্যন্ত মোটামুটি 55–65% Linux fundamentals-to-admin knowledge cover হয়েছে।**

তবে **“Linux A–Z” বলতে যদি professional Linux System Administrator/DevOps level** বোঝাও, তাহলে এখনও গুরুত্বপূর্ণ বিষয় বাকি আছে:

* Networking advanced
* DNS
* SSH advanced
* Firewall advanced
* LVM advanced
* RAID
* Kernel/modules
* Logs & monitoring
* Performance tuning
* `systemd` advanced
* NFS/Samba
* Containers/Docker
* Virtualization
* Git
* CI/CD basics
* Ansible/configuration management
* Cloud Linux
* Advanced troubleshooting
* Backup & disaster recovery
* Linux internals
* Advanced security
* Real-world projects

**Level 11-এর পর আমরা যদি Level 20–25 পর্যন্ত যাই, তাহলে তোমার Linux knowledge অনেক বেশি complete হবে।**

### 🎯 সহজভাবে

```text
Level 1–5   → Beginner foundation       ████████░░
Level 6–11  → Core admin skills         ██████░░░░
Level 12–18 → Advanced Linux            ░░░░░░░░░░
Level 19–25 → Professional/DevOps       ░░░░░░░░░░
```

অর্থাৎ **এখন থামলে Linux-এর foundation বেশ ভালো হবে, কিন্তু professional-level A–Z এখনো শেষ হবে না।**


---
