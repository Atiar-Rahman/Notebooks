# Lesson 1: Linux (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই লেসন শেষ করলে আপনি Linux-এর মৌলিক ধারণা, কমান্ড, ফাইল সিস্টেম, পারমিশন এবং Cloud/DevOps-এ Linux-এর ভূমিকা বুঝতে পারবেন।

---

# 1. Linux কী?

Linux একটি **Open Source Operating System Kernel**।

সহজ ভাষায়, Windows যেমন একটি Operating System, Linux-ও তেমন একটি Operating System (বা Linux kernel-এর উপর ভিত্তি করে তৈরি OS)।

Linux সবচেয়ে বেশি ব্যবহৃত হয়:

- Cloud Server
    
- AWS EC2
    
- Azure VM
    
- Google Cloud VM
    
- Docker
    
- Kubernetes
    
- Web Server
    

**বাস্তব উদাহরণ:**  
আপনি যদি AWS-এ একটি EC2 Server তৈরি করেন, বেশিরভাগ সময় Ubuntu বা Amazon Linux ব্যবহার করবেন।

---

# 2. Linux Distribution (Distro)

Linux-এর অনেক সংস্করণ আছে।

|Distribution|ব্যবহার|
|---|---|
|Ubuntu|Beginner ও Server|
|Debian|Stable Server|
|CentOS|Enterprise|
|Red Hat (RHEL)|Corporate|
|Kali Linux|Cyber Security|
|Amazon Linux|AWS|

**Interview Question**

> Ubuntu কি Linux?

**Answer:** Ubuntu হলো Linux Distribution।

---

# 3. Linux Architecture

```text
Application
      ↓
Shell (Bash)
      ↓
Kernel
      ↓
Hardware
```

### Kernel

Kernel Operating System-এর মূল অংশ।

কাজ:

- Memory Management
    
- Process Management
    
- Device Control
    
- CPU Scheduling
    

---

# 4. Shell কী?

Shell হলো User এবং Kernel-এর মধ্যে Interface।

যখন আপনি লিখেন

```bash
ls
```

Shell এই command Kernel-এ পাঠায়।

সবচেয়ে জনপ্রিয় Shell

- Bash
    
- Zsh
    
- Fish
    

---

# 5. Linux File System

Linux-এ সবকিছু File হিসেবে ধরা হয়।

Root Directory

```text
/
```

এর নিচে সব থাকে।

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── opt
├── root
├── tmp
├── usr
├── var
```

---

## গুরুত্বপূর্ণ Folder

### /home

User-এর personal files

Example

```
/home/atiar
```

---

### /root

Root User-এর Home

```
/root
```

---

### /etc

Configuration Files

Example

```
/etc/passwd
```

---

### /var

Logs

Example

```
/var/log
```

---

### /tmp

Temporary Files

Server restart হলে অনেক ক্ষেত্রে delete হয়ে যায়।

---

### /bin

Basic Commands

Example

```
ls
cp
mv
rm
```

---

# 6. Absolute vs Relative Path

Absolute

```
/home/atiar/Documents/file.txt
```

Root থেকে শুরু।

Relative

```
Documents/file.txt
```

Current directory থেকে শুরু।

---

# 7. Linux Commands

## pwd

Print Working Directory

```bash
pwd
```

Output

```
/home/atiar
```

---

## ls

List files

```bash
ls
```

Example

```
Desktop

Downloads

Documents
```

---

### ls -l

Details

```bash
ls -l
```

Output

```
-rw-r--r--

file.txt
```

---

### ls -a

Hidden Files

```bash
ls -a
```

Output

```
.

..

.bashrc

.profile
```

---

# cd

Directory change

```bash
cd Documents
```

Back

```bash
cd ..
```

Home

```bash
cd ~
```

Root

```bash
cd /
```

---

# mkdir

Folder create

```bash
mkdir project
```

---

# rmdir

Delete Empty Folder

```bash
rmdir project
```

---

# touch

Create File

```bash
touch test.txt
```

---

# cat

Read File

```bash
cat test.txt
```

---

# echo

Write Text

```bash
echo "Hello Linux"
```

Save to file

```bash
echo "Hello" > file.txt
```

Append

```bash
echo "World" >> file.txt
```

Difference

```
>
Overwrite

>>

Append
```

---

# cp

Copy

```bash
cp file.txt backup.txt
```

Folder

```bash
cp -r folder backup
```

---

# mv

Move

```bash
mv file.txt Documents/
```

Rename

```bash
mv old.txt new.txt
```

---

# rm

Delete

```bash
rm file.txt
```

Folder

```bash
rm -r folder
```

Force

```bash
rm -rf folder
```

⚠️ `rm -rf` খুব শক্তিশালী কমান্ড। ভুল জায়গায় চালালে গুরুত্বপূর্ণ ফাইল মুছে যেতে পারে।

---

# find

Search File

```bash
find . -name "*.txt"
```

---

# grep

Search Text

```bash
grep "error" log.txt
```

---

# head

First 10 lines

```bash
head log.txt
```

---

# tail

Last 10 lines

```bash
tail log.txt
```

Live log

```bash
tail -f log.txt
```

---

# 8. File Permission

Example

```
-rwxr-xr--
```

Break it

```
-

File

d

Directory
```

Then

```
rwx

Owner

r-x

Group

r--

Others
```

Meaning

```
r = Read

w = Write

x = Execute
```

Numeric

```
r = 4

w = 2

x = 1
```

Examples

```
755

Owner = 7

rwx

Group = 5

r-x

Others = 5

r-x
```

```
644

Owner

rw-

Group

r--

Others

r--
```

Command

```bash
chmod 755 script.sh
```

---

# 9. Users

Current User

```bash
whoami
```

Current ID

```bash
id
```

Become root (if permitted)

```bash
sudo su
```

---

# 10. Processes

See Running Processes

```bash
ps
```

Live

```bash
top
```

Kill Process

```bash
kill PID
```

Force Kill

```bash
kill -9 PID
```

---

# 11. Package Management (Ubuntu)

Update package list:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install Git:

```bash
sudo apt install git
```

---

# 12. Environment Variables

See all:

```bash
env
```

Show PATH:

```bash
echo $PATH
```

`PATH` বলে দেয় কোন কোন ডিরেক্টরিতে executable command খুঁজতে হবে।

---

# 13. Linux in Cloud & DevOps

ধরুন AWS EC2-তে Ubuntu Server চালু করলেন।

আপনি:

1. SSH দিয়ে লগইন করবেন।
    
2. `sudo apt update` চালাবেন।
    
3. `sudo apt install nginx` দিয়ে web server ইনস্টল করবেন।
    
4. `systemctl status nginx` দিয়ে সার্ভিস চলছে কি না দেখবেন।
    

এটাই বাস্তব DevOps কাজের একটি সাধারণ উদাহরণ।

---

# Interview Questions

1. Linux কী?
    
2. Kernel কী?
    
3. Shell কী?
    
4. `pwd` কী করে?
    
5. `ls -la` কেন ব্যবহার করা হয়?
    
6. `>` এবং `>>`-এর পার্থক্য কী?
    
7. Absolute Path ও Relative Path-এর পার্থক্য কী?
    
8. `chmod 755` এর অর্থ কী?
    
9. `grep` কী কাজে লাগে?
    
10. `rm -rf` চালানোর সময় কেন সতর্ক থাকতে হয়?
    

---

# Practice MCQs

**1. Current directory দেখার command কোনটি?**

- A. ls
    
- B. pwd ✅
    
- C. cd
    
- D. dir
    

**2. Hidden file দেখার জন্য কোন option ব্যবহার হয়?**

- A. `-h`
    
- B. `-a` ✅
    
- C. `-d`
    
- D. `-s`
    

**3. `chmod 755 file.sh`-এ Owner-এর permission কী?**

- A. rw-
    
- B. r-x
    
- C. rwx ✅
    
- D. r--
    

**4. `grep` কী কাজে ব্যবহৃত হয়?**

- A. Copy file
    
- B. Search text ✅
    
- C. Delete file
    
- D. Rename file
    

**5. `/etc` ডিরেক্টরি সাধারণত কী রাখে?**

- A. User documents
    
- B. Configuration files ✅
    
- C. Temporary files
    
- D. Logs
    

---

### Homework

একটি Ubuntu VM (VirtualBox, WSL, বা AWS EC2) ব্যবহার করে নিচের কমান্ডগুলো নিজে চালিয়ে দেখুন:

```bash
pwd
ls -la
mkdir demo
cd demo
touch notes.txt
echo "Linux Practice" > notes.txt
cat notes.txt
cp notes.txt backup.txt
mv backup.txt backup2.txt
find . -name "*.txt"
grep "Linux" notes.txt
chmod 755 notes.txt
```

এভাবে হাতে-কলমে অনুশীলন করলে কমান্ডগুলো অনেক সহজে মনে থাকবে।

পরের লেসনে আমরা **Networking (Basic → Advanced)** বিস্তারিত শিখব, কারণ এটি Cloud ও DevOps-এর অন্যতম গুরুত্বপূর্ণ ভিত্তি।

----

# Lesson 2: Computer Networking (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই লেসন শেষ করলে আপনি Networking-এর মৌলিক ধারণা, IP, DNS, TCP/UDP, HTTP/HTTPS, OSI Model, Ports, Routing, Firewall এবং Cloud Networking বুঝতে পারবেন।

---

# 1. Networking কী?

Networking হলো দুই বা ততোধিক কম্পিউটারকে যুক্ত করে তথ্য আদান-প্রদান করার ব্যবস্থা।

### উদাহরণ

```text
Laptop ─── WiFi Router ─── Internet ─── Google Server
```

যখন আপনি `google.com` ওপেন করেন, আপনার কম্পিউটার Google-এর সার্ভারের সাথে যোগাযোগ করে।

---

# 2. Network Types

|Type|Full Form|Range|
|---|---|---|
|PAN|Personal Area Network|১–১০ মিটার|
|LAN|Local Area Network|Office/Home|
|MAN|Metropolitan Area Network|City|
|WAN|Wide Area Network|Country/World|

### উদাহরণ

- Bluetooth → PAN
    
- বাসার WiFi → LAN
    
- Internet → WAN
    

---

# 3. IP Address

IP Address হলো প্রতিটি ডিভাইসের একটি ইউনিক ঠিকানা।

Example

```text
192.168.1.10
```

এটি চারটি অংশে বিভক্ত।

---

## IPv4

```text
192.168.10.20
```

32-bit

Maximum

```text
255.255.255.255
```

---

## IPv6

Example

```text
2001:db8:85a3::8a2e:370:7334
```

128-bit

IPv4-এর তুলনায় অনেক বেশি Address।

---

# 4. Public vs Private IP

### Private IP

শুধু Local Network-এ ব্যবহৃত হয়।

Ranges

```text
10.0.0.0 - 10.255.255.255

172.16.0.0 - 172.31.255.255

192.168.0.0 - 192.168.255.255
```

---

### Public IP

ISP দেয়।

Internet থেকে Access করা যায়।

---

### Example

```text
Internet

↓

Public IP

↓

Router

↓

Private IP

↓

Laptop
```

---

# 5. Static vs Dynamic IP

### Static

Same থাকে।

Server-এর জন্য ব্যবহার হয়।

---

### Dynamic

Change হয়।

বাসার WiFi সাধারণত Dynamic IP।

---

# 6. MAC Address

প্রত্যেক Network Card-এর Unique Physical Address।

Example

```text
00:1A:2B:3C:4D:5E
```

MAC Layer-2 এ কাজ করে।

IP Layer-3 এ কাজ করে।

---

# 7. DNS

DNS = Domain Name System

DNS Domain কে IP-তে Convert করে।

Example

```text
google.com

↓

142.250.xxx.xxx
```

DNS না থাকলে সব Website IP দিয়ে খুলতে হতো।

---

# 8. DHCP

DHCP = Dynamic Host Configuration Protocol

Automatically দেয়

- IP Address
    
- Gateway
    
- DNS
    

Example

আপনি WiFi Connect করলেন।

Router Automatically IP দিল।

---

# 9. Gateway

Gateway হলো Internet-এর দরজা।

Example

```text
Laptop

↓

Router

↓

Internet
```

Router-ই Gateway।

---

# 10. Subnet Mask

Determines

Network অংশ

Host অংশ

Example

```text
255.255.255.0
```

মানে

```text
192.168.1.xxx
```

একই Network।

---

# 11. Port

একটি IP-এর ভিতরে বিভিন্ন Service চালানোর জন্য Port ব্যবহার হয়।

Example

```text
192.168.1.10
```

Website

↓

Port 80

SSH

↓

Port 22

---

# Important Ports

|Port|Service|
|---|---|
|20|FTP Data|
|21|FTP|
|22|SSH|
|23|Telnet|
|25|SMTP|
|53|DNS|
|67|DHCP|
|68|DHCP Client|
|80|HTTP|
|110|POP3|
|143|IMAP|
|443|HTTPS|
|3306|MySQL|
|5432|PostgreSQL|
|6379|Redis|
|8080|Alternative HTTP|

**মনে রাখার মতো:** 22, 53, 80, 443, 3306

---

# 12. Protocol

Protocol মানে Rules।

Example

HTTP

FTP

SSH

SMTP

DNS

---

# 13. HTTP

Hyper Text Transfer Protocol

Port

```text
80
```

Not Secure

---

# 14. HTTPS

Secure HTTP

Port

```text
443
```

Uses

```text
SSL/TLS
```

Data Encrypt করে।

---

# 15. FTP

File Transfer

Port

```text
21
```

---

# 16. SSH

Secure Shell

Port

```text
22
```

Linux Server Login

```bash
ssh ubuntu@IP
```

Cloud Engineer প্রতিদিন SSH ব্যবহার করে।

---

# 17. SMTP

Email Send

Port

25

---

# 18. TCP vs UDP

## TCP

Features

✔ Reliable

✔ Ordered

✔ Error Checking

✔ Slow

Examples

- HTTP
    
- HTTPS
    
- SSH
    
- FTP
    

---

## UDP

✔ Fast

✔ No Guarantee

✔ No Order

Examples

- Video Streaming
    
- Online Games
    
- Voice Call (VoIP)
    
- DNS queries (often use UDP)
    

---

Comparison

|TCP|UDP|
|---|---|
|Reliable|Fast|
|Connection Oriented|Connectionless|
|Slow|Faster|
|Error Check|Minimal|

---

# 19. OSI Model

সবচেয়ে Common Interview Question

```text
7 Application

6 Presentation

5 Session

4 Transport

3 Network

2 Data Link

1 Physical
```

Shortcut

```text
All

People

Seem

To

Need

Data

Processing
```

---

## Layer 7

Application

Examples

Browser

HTTP

FTP

SMTP

---

## Layer 4

Transport

TCP

UDP

---

## Layer 3

Network

IP

Router

---

## Layer 2

Data Link

MAC

Switch

---

## Layer 1

Physical

Cable

Fiber

---

# 20. TCP/IP Model

```text
Application

Transport

Internet

Network Access
```

বাস্তবে Internet-এ এটি বেশি ব্যবহৃত হয়।

---

# 21. Router vs Switch

Switch

LAN-এর মধ্যে Device Connect করে।

Router

Different Network Connect করে।

---

# 22. Firewall

Firewall Traffic Control করে।

Example

Allow

```text
80

443
```

Block

```text
23
```

---

# 23. NAT

Network Address Translation

Private IP

↓

Public IP

Example

```text
192.168.1.5

↓

103.xx.xx.xx
```

---

# 24. VPN

Virtual Private Network

Encrypted Connection।

Example

বাসা থেকে Office Server-এ Secure Connection।

---

# 25. Load Balancer

একাধিক Server-এ Request ভাগ করে।

```text
User

↓

Load Balancer

↓

Server 1

↓

Server 2

↓

Server 3
```

Benefits

- High Availability
    
- Scalability
    

---

# 26. CDN

Content Delivery Network

Example

Cloudflare

User-এর কাছাকাছি Server থেকে Content দেয়।

Website Fast হয়।

---

# 27. Cloud Networking

AWS Example

```text
Internet

↓

Internet Gateway

↓

VPC

↓

Subnet

↓

EC2
```

Terms

- VPC
    
- Subnet
    
- Route Table
    
- Security Group
    
- Internet Gateway
    

---

# Real-Life Example

আপনি Browser-এ লিখলেন:

```text
https://google.com
```

কি হয়?

1. DNS IP খুঁজে বের করে।
    
2. Browser TCP Connection তৈরি করে।
    
3. HTTPS Handshake হয়।
    
4. Data Encrypt হয়।
    
5. Server Response পাঠায়।
    
6. Browser Page দেখায়।
    

---

# Interview Questions

### What is IP Address?

Unique Address।

---

### Difference between Public and Private IP?

Private

LAN

Public

Internet

---

### DNS কী?

Domain → IP

---

### DHCP কী?

Automatic IP দেয়।

---

### TCP vs UDP?

TCP Reliable

UDP Fast

---

### HTTP vs HTTPS?

HTTPS

Encrypted

HTTP

Not Secure

---

### Router vs Switch?

Router

Network Connect

Switch

Devices Connect

---

### SSH Port?

22

---

### HTTPS Port?

443

---

### DNS Port?

53

---

# Most Important Ports

|Service|Port|
|---|---|
|SSH|22|
|FTP|21|
|DNS|53|
|HTTP|80|
|HTTPS|443|
|MySQL|3306|

---

# MCQ Practice

### 1. SSH Port?

A) 80

B) 21

C) 22 ✅

D) 53

---

### 2. DNS-এর কাজ কী?

A) File Transfer

B) Domain → IP ✅

C) Email

D) SSH

---

### 3. HTTPS Port?

A) 80

B) 443 ✅

C) 22

D) 53

---

### 4. TCP হলো—

A) Fast but unreliable

B) Reliable connection ✅

C) Wireless protocol

D) IP Address

---

### 5. Router কী কাজ করে?

A) Store Files

B) Connect Different Networks ✅

C) Edit Database

D) Compile Code

---

## BJIT Assessment-এর জন্য Networking থেকে সবচেয়ে গুরুত্বপূর্ণ বিষয়

- IP Address
    
- Public vs Private IP
    
- DNS
    
- DHCP
    
- Gateway
    
- TCP vs UDP
    
- HTTP vs HTTPS
    
- SSH
    
- Common Ports (22, 53, 80, 443, 3306)
    
- OSI Model (বিশেষ করে Layer 2, 3, 4, 7)
    
- Router vs Switch
    
- Firewall
    
- Load Balancer
    

এই টপিকগুলো Cloud ও DevOps-এর ভিত্তি। এগুলো ভালোভাবে বুঝলে AWS, Docker, Kubernetes এবং CI/CD শেখাও অনেক সহজ হবে।


----
# Lesson 3: Git & GitHub (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই লেসন শেষ করলে Git, GitHub, Branching, Merge, Conflict, Pull Request এবং DevOps-এ Git-এর ব্যবহার বুঝতে পারবেন।

---

# 1. Git কী?

**Git** হলো একটি **Distributed Version Control System (DVCS)**।

এটি দিয়ে আপনি:

- Code Track করতে পারেন
    
- Previous Version-এ ফিরে যেতে পারেন
    
- Team-এর সাথে কাজ করতে পারেন
    
- Multiple Branch নিয়ে কাজ করতে পারেন
    

### Real Life Example

ধরুন আপনি একটি Website বানাচ্ছেন।

Day 1

```text
Homepage
```

Day 2

```text
Homepage
Login Page
```

Day 3

```text
Homepage
Login
Payment
```

Day 4

আপনি ভুল করে সব Delete করে ফেললেন।

Git থাকলে

```text
Rollback
```

করে আগের Version ফিরে পাবেন।

---

# 2. Git vs GitHub

অনেকেই এই প্রশ্ন করে।

|Git|GitHub|
|---|---|
|Software|Website|
|Local Machine|Cloud|
|Version Control|Code Hosting|
|Offline|Online|

GitHub হলো Git Repository রাখার Website।

---

# 3. Install Git

Ubuntu

```bash
sudo apt install git
```

Windows

Git Download করুন।

---

# 4. Check Version

```bash
git --version
```

Output

```text
git version 2.42
```

---

# 5. Configure Git

প্রথমবার

```bash
git config --global user.name "Atiar"
```

Email

```bash
git config --global user.email "atiar@gmail.com"
```

Check

```bash
git config --list
```

---

# 6. Initialize Repository

Folder তৈরি

```bash
mkdir project
```

Inside

```bash
cd project
```

Initialize

```bash
git init
```

Output

```text
Initialized empty Git repository
```

---

# 7. Git Workflow

```text
Working Directory

↓

Staging Area

↓

Repository
```

---

# 8. Git Status

সবচেয়ে বেশি ব্যবহৃত Command

```bash
git status
```

Output

```text
modified

new file

deleted
```

---

# 9. Create File

```bash
touch app.py
```

Check

```bash
git status
```

Output

```text
Untracked File
```

---

# 10. Add File

Single

```bash
git add app.py
```

All

```bash
git add .
```

Meaning

Working Directory

↓

Staging Area

---

# 11. Commit

Commit মানে Snapshot নেওয়া।

```bash
git commit -m "Initial Commit"
```

Good Messages

```text
Add Login Page

Fix Payment Bug

Update README
```

Bad Message

```text
update
```

---

# 12. Git Log

History

```bash
git log
```

Short

```bash
git log --oneline
```

Example

```text
a3c45 Add Login

ff653 Initial Commit
```

---

# 13. Difference

```bash
git diff
```

Shows

কি Change হয়েছে।

---

# 14. Branch

Default

```text
main
```

Create

```bash
git branch login
```

See Branch

```bash
git branch
```

Output

```text
main

login
```

---

# 15. Switch Branch

Old

```bash
git checkout login
```

New

```bash
git switch login
```

---

# 16. Create + Switch

```bash
git checkout -b payment
```

or

```bash
git switch -c payment
```

---

# 17. Merge

Suppose

```text
main

↓

login
```

Work Finished

Merge

```bash
git checkout main

git merge login
```

---

# 18. Merge Conflict

Example

Main

```text
Hello
```

Branch

```text
Hi
```

Git doesn't know which one to keep.

Conflict

You must resolve manually.

---

# 19. Delete Branch

```bash
git branch -d login
```

Force

```bash
git branch -D login
```

---

# 20. GitHub

Create Repository

Example

```text
Cloud-DevOps
```

Copy URL

```text
https://github.com/user/project.git
```

---

# 21. Clone

Download Repository

```bash
git clone URL
```

Example

```bash
git clone https://github.com/user/project.git
```

---

# 22. Remote

See Remote

```bash
git remote -v
```

Add Remote

```bash
git remote add origin URL
```

---

# 23. Push

Upload Code

```bash
git push origin main
```

---

# 24. Pull

Download Latest Code

```bash
git pull origin main
```

---

# 25. Fetch

Download

But Don't Merge

```bash
git fetch
```

Difference

Fetch

↓

Download only

Pull

↓

Download + Merge

---

# 26. Reset

Undo Commit

```bash
git reset
```

Soft

```bash
git reset --soft
```

Hard

```bash
git reset --hard
```

⚠️ Hard Reset deletes local changes permanently.

---

# 27. Restore

Undo File

```bash
git restore app.py
```

---

# 28. Stash

Temporary Save

```bash
git stash
```

Restore

```bash
git stash pop
```

Useful when you need to switch branches without committing unfinished work.

---

# 29. .gitignore

Don't Upload

```text
node_modules/

.env

*.log
```

Example

```text
.env
```

Contains

Password

API Keys

Never upload.

---

# 30. Pull Request (PR)

Developer

↓

Create Branch

↓

Commit

↓

Push

↓

Open PR

↓

Review

↓

Merge

This is the standard workflow in many software teams.

---

# 31. Git in DevOps

Developer

↓

Git Commit

↓

GitHub

↓

Jenkins

↓

Build

↓

Docker

↓

Deploy

↓

Server

Git is usually the trigger that starts an automated CI/CD pipeline.

---

# Common Interview Questions

### What is Git?

Version Control System.

---

### Difference between Git and GitHub?

Git = Tool

GitHub = Cloud Repository.

---

### Difference between Pull and Fetch?

Fetch

Only Downloads.

Pull

Downloads + Merge.

---

### Difference between Merge and Rebase?

Merge creates a merge commit and preserves branch history.

Rebase rewrites history to create a cleaner linear sequence of commits. For beginners, understanding merge is usually enough.

---

### Difference between Clone and Fork?

Clone

Copies a repository to your local machine.

Fork

Creates your own copy of someone else's repository on GitHub.

---

# Important Commands (Remember)

```bash
git init

git status

git add .

git commit -m "message"

git log

git branch

git checkout

git switch

git merge

git clone

git remote -v

git push

git pull

git fetch

git restore

git stash
```

---

# MCQ Practice

### 1. Git is

A) Database

B) Version Control System ✅

C) Programming Language

D) Operating System

---

### 2. Upload code to GitHub

A) git pull

B) git push ✅

C) git clone

D) git fetch

---

### 3. Download latest code and merge

A) git fetch

B) git pull ✅

C) git clone

D) git status

---

### 4. Create a new branch and switch to it (older syntax)

A) `git branch`

B) `git checkout -b feature` ✅

C) `git merge`

D) `git log`

---

### 5. Which file is commonly used to exclude files from Git tracking?

A) `.ignore`

B) `.gitconfig`

C) `.gitignore` ✅

D) `.github`

---

# Assessment Tips (BJIT)

Git থেকে যেসব প্রশ্ন আসার সম্ভাবনা বেশি:

- Git vs GitHub
    
- `git add`, `git commit`, `git push`, `git pull`
    
- Branch কী?
    
- Merge কী?
    
- Pull vs Fetch
    
- Clone কী?
    
- `.gitignore` কেন ব্যবহার করা হয়?
    
- Version Control-এর সুবিধা কী?
    

এই বিষয়গুলো ভালোভাবে বুঝে রাখলে Cloud & DevOps Trainee assessment-এর Git অংশের অধিকাংশ প্রশ্নের উত্তর দিতে পারবেন।

------
# Lesson 4: Cloud Computing (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই লেসন শেষ করলে আপনি Cloud Computing, AWS, Azure, GCP-এর ভিত্তি, Service Models, Deployment Models এবং Cloud Architecture বুঝতে পারবেন।

---

# 1. What is Cloud Computing?

Cloud Computing হলো **ইন্টারনেটের মাধ্যমে Computing Resources (Server, Storage, Database, Networking, Software) ভাড়া নেওয়ার পদ্ধতি।**

আগে কোম্পানিগুলো নিজেদের Data Center বানাতো।

```text
Company

↓

Own Server

↓

Own Network

↓

Own Storage
```

এখন

```text
Company

↓

AWS / Azure / Google Cloud

↓

Pay as you use
```

---

## Real Life Example

আপনি Netflix দেখছেন।

ভিডিও আপনার ফোনে নেই।

Netflix Cloud Server থেকে ভিডিও পাঠাচ্ছে।

এটাই Cloud।

---

# 2. Why Cloud?

আগে

```text
নিজের Server কিনতে হতো

↓

Setup করতে হতো

↓

Maintenance করতে হতো
```

Cloud এ

```text
৫ মিনিটে Server তৈরি

↓

যত ব্যবহার

↓

তত টাকা
```

Advantages

- Low Cost
    
- High Availability
    
- Fast Deployment
    
- Scalability
    
- Security
    
- Backup
    

---

# 3. Cloud Providers

সবচেয়ে জনপ্রিয়

|Provider|Market|
|---|---|
|AWS|#1|
|Microsoft Azure|#2|
|Google Cloud (GCP)|#3|
|Oracle Cloud|Enterprise|
|Alibaba Cloud|Asia|

BJIT-এ AWS-এর বেসিক জানা থাকলে সুবিধা হবে।

---

# 4. Traditional IT vs Cloud

Traditional

```text
Buy Server

↓

Install

↓

Configure

↓

Maintain
```

Cloud

```text
Login

↓

Create Server

↓

Done
```

---

# 5. Cloud Characteristics

### On Demand

যখন দরকার

তখন Server।

---

### Self Service

নিজেই Server Create।

---

### Pay As You Go

যত ব্যবহার

তত টাকা।

---

### Elasticity

Automatically Scale।

---

### Resource Pooling

একই Hardware অনেক Customer ব্যবহার করে।

---

# 6. Service Models

Interview-এর সবচেয়ে Common Question

---

## IaaS

Infrastructure as a Service

Cloud Provider দেয়

- Server
    
- Storage
    
- Network
    

আপনি Manage করবেন

- Operating System
    
- Software
    
- Security (আংশিক)
    
- Applications
    

Example

- AWS EC2
    
- Azure VM
    

---

## PaaS

Platform as a Service

Provider Manage করে

- OS
    
- Runtime
    
- Middleware
    

আপনি শুধু Code লিখবেন।

Example

- Google App Engine
    
- Azure App Service
    

---

## SaaS

Software as a Service

সবকিছু Provider Manage করে।

আপনি শুধু ব্যবহার করবেন।

Examples

- Gmail
    
- Google Drive
    
- Microsoft 365
    
- Zoom
    

---

### সহজে মনে রাখুন

|Model|আপনি কী Manage করবেন|
|---|---|
|IaaS|OS + App|
|PaaS|শুধু App|
|SaaS|কিছুই না|

---

# 7. Deployment Models

---

## Public Cloud

Example

AWS

Azure

Google Cloud

সবাই ব্যবহার করতে পারে।

---

## Private Cloud

একটি কোম্পানির নিজস্ব Cloud।

---

## Hybrid Cloud

Private + Public

সবচেয়ে বেশি ব্যবহার হয়।

---

## Multi Cloud

AWS + Azure + GCP

---

# 8. Virtualization

আগে

এক Server

↓

এক OS

↓

এক Application

---

Virtualization

এক Physical Server

↓

Hypervisor

↓

অনেক Virtual Machine

↓

Ubuntu

↓

Windows

↓

CentOS

---

Benefits

- Cost Saving
    
- Isolation
    
- Better Utilization
    

---

# 9. Hypervisor

Virtual Machine তৈরি করে।

Types

### Type-1

Bare Metal

Examples

- VMware ESXi
    
- Hyper-V
    

---

### Type-2

Host OS-এর উপর চলে।

Examples

- VirtualBox
    
- VMware Workstation
    

---

# 10. Virtual Machine (VM)

VM হলো Software Computer।

একটি VM-এর থাকে

- CPU
    
- RAM
    
- Disk
    
- Network
    

AWS EC2 হলো VM।

---

# 11. Containers

VM-এর মতো

কিন্তু Lightweight।

Example

Docker Container

---

Difference

|VM|Container|
|---|---|
|Heavy|Lightweight|
|Full OS|Share Kernel|
|Slow|Fast|

---

# 12. Scalability

### Vertical Scaling

Increase RAM

Example

```text
4GB RAM

↓

8GB RAM
```

---

### Horizontal Scaling

More Servers

```text
Server1

+

Server2

+

Server3
```

Cloud-এ Horizontal বেশি ব্যবহৃত হয়।

---

# 13. High Availability

একটি Server Down

↓

অন্য Server চলবে।

Example

```text
Load Balancer

↓

Server1

↓

Server2

↓

Server3
```

---

# 14. Fault Tolerance

এক Server Crash

↓

Automatic অন্য Server

↓

User কিছু বুঝবে না।

---

# 15. Load Balancer

User

↓

Load Balancer

↓

Server A

↓

Server B

↓

Server C

Benefits

- Faster
    
- Highly Available
    
- Balanced Traffic
    

---

# 16. Auto Scaling

Traffic বেড়েছে

↓

New Server

Traffic কমেছে

↓

Server Remove

AWS Auto Scaling

এটাই করে।

---

# 17. Regions

AWS-এর অনেক Region আছে।

Example

```text
Singapore

Tokyo

Mumbai

London
```

---

# 18. Availability Zone (AZ)

একটি Region-এর ভিতরে

একাধিক Data Center।

Example

```text
Singapore Region

↓

AZ A

↓

AZ B

↓

AZ C
```

---

# 19. Data Center

Physical Building

Inside

- Server
    
- Network
    
- Cooling
    
- Power
    

---

# 20. Cloud Storage

Types

---

## Object Storage

Example

AWS S3

Stores

- Image
    
- Video
    
- Backup
    

---

## Block Storage

Example

EBS

Virtual Hard Disk

---

## File Storage

Shared Folder

Example

Amazon EFS

---

# 21. Cloud Security

Concept

CIA

Confidentiality

Integrity

Availability

---

Authentication

Who are you?

Authorization

What can you do?

---

Encryption

Protect Data

---

# 22. Shared Responsibility Model

Cloud Provider

Responsible

- Hardware
    
- Physical Security
    
- Data Center
    

Customer

Responsible

- Password
    
- Data
    
- Applications
    
- IAM Permissions
    

---

# 23. Cloud Monitoring

AWS CloudWatch

Monitors

- CPU
    
- RAM (custom metrics)
    
- Disk
    
- Network
    

---

# 24. Backup

Always Keep Backup

Cloud Supports

- Snapshot
    
- Backup
    
- Replication
    

---

# 25. Disaster Recovery

Server Crash

↓

Backup

↓

Restore

---

# 26. Cloud Architecture

```text
Users

↓

DNS

↓

Load Balancer

↓

Web Server

↓

Application Server

↓

Database

↓

Storage
```

---

# 27. Real Example

Facebook

Millions of Users

↓

Load Balancer

↓

Hundreds of Servers

↓

Database

↓

Cloud Storage

---

# Interview Questions

### What is Cloud Computing?

Internet-এর মাধ্যমে Computing Resources ব্যবহার।

---

### What are Cloud Models?

IaaS

PaaS

SaaS

---

### Difference between VM and Container?

VM

Full OS

Container

Shared Kernel

---

### Horizontal vs Vertical Scaling?

Vertical

Increase RAM/CPU

Horizontal

Increase Servers

---

### Load Balancer কী?

Traffic ভাগ করে।

---

### Auto Scaling কী?

Traffic অনুযায়ী Server Increase/Decrease।

---

### Region vs Availability Zone?

Region = Geographic Area

AZ = Multiple Data Centers inside Region

---

### What is High Availability?

Service যেন একটি Server নষ্ট হলেও চালু থাকে।

---

# Most Important MCQs

### 1. EC2 কী?

A Database

A Storage

✅ Virtual Machine

Email Service

---

### 2. S3 কী?

Compute

Database

✅ Object Storage

DNS

---

### 3. SaaS Example?

AWS EC2

Azure VM

✅ Gmail

Docker

---

### 4. Horizontal Scaling মানে

RAM Increase

CPU Increase

✅ More Servers

Disk Increase

---

### 5. Load Balancer-এর কাজ?

Delete Server

Backup

Distribute Traffic ✅

Install Software

---

# BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ

- Cloud Computing কী
    
- Traditional vs Cloud
    
- IaaS, PaaS, SaaS
    
- Public, Private, Hybrid Cloud
    
- Virtual Machine vs Container
    
- Vertical vs Horizontal Scaling
    
- Load Balancer
    
- Auto Scaling
    
- Region vs Availability Zone
    
- Object Storage vs Block Storage
    
- Shared Responsibility Model
    

---

## 📝 Quick Revision (১ মিনিটে)

- **Cloud =** Internet-এর মাধ্যমে Server/Storage ভাড়া নেওয়া।
    
- **IaaS =** Provider Infrastructure দেয়, আপনি OS ও App ম্যানেজ করেন।
    
- **PaaS =** Provider Platform ম্যানেজ করে, আপনি শুধু Code দেন।
    
- **SaaS =** Ready-made Software (যেমন Gmail)।
    
- **EC2 =** Virtual Machine।
    
- **S3 =** Object Storage।
    
- **EBS =** Block Storage।
    
- **Load Balancer =** Traffic ভাগ করে।
    
- **Auto Scaling =** চাহিদা অনুযায়ী Server বাড়ায়/কমায়।
    
- **Region =** Geographic location, **Availability Zone =** Region-এর ভিতরের Data Center।
    

এই Lesson 4 শেষ হলে পরবর্তী ধাপ হবে **Lesson 5: AWS (EC2, S3, IAM, VPC, Security Groups, Route Tables, Internet Gateway, EBS, ELB, Auto Scaling)**—যেটি BJIT Cloud & DevOps assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

----
# Lesson 5: AWS (Amazon Web Services) Basic → Advanced for Cloud & DevOps

> **Goal:** এই লেসন শেষে আপনি AWS-এর সবচেয়ে গুরুত্বপূর্ণ সার্ভিসগুলো (EC2, S3, IAM, VPC, Security Groups, EBS, ELB, Auto Scaling) বুঝতে পারবেন। এগুলো Cloud & DevOps Trainee assessment-এ খুবই গুরুত্বপূর্ণ।

---

# 1. What is AWS?

AWS (Amazon Web Services) হলো বিশ্বের সবচেয়ে বড় Cloud Platform।

এটি আপনাকে দেয়:

- Virtual Server
    
- Storage
    
- Database
    
- Networking
    
- AI Services
    
- Monitoring
    
- Security
    

---

## Real Life Example

আগে Website চালাতে

```text
নিজের Server কিনতে হতো
```

AWS-এ

```text
Login

↓

Create EC2

↓

Deploy Website
```

মাত্র কয়েক মিনিটে Server Ready।

---

# 2. AWS Global Infrastructure

AWS

↓

Regions

↓

Availability Zones

↓

Data Centers

Example

```text
Asia Pacific (Singapore)

↓

AZ-a

↓

AZ-b

↓

AZ-c
```

---

# 3. AWS Services Overview

| Service      | Purpose           |
| ------------ | ----------------- |
| EC2          | Virtual Machine   |
| S3           | Object Storage    |
| EBS          | Virtual Hard Disk |
| IAM          | User & Permission |
| VPC          | Private Network   |
| ELB          | Load Balancer     |
| Auto Scaling | Automatic Scaling |
| RDS          | Managed Database  |
| CloudWatch   | Monitoring        |
| Route53      | DNS               |

---

# 4. EC2 (Elastic Compute Cloud)

সবচেয়ে গুরুত্বপূর্ণ Service।

EC2 = Virtual Machine

Example

```text
Ubuntu Server

2 CPU

4GB RAM

50GB Disk
```

---

## EC2 Launch Steps

1. Choose AMI
    

↓

2. Choose Instance Type
    

↓

3. Configure Network
    

↓

4. Attach Storage
    

↓

5. Create Key Pair
    

↓

6. Launch
    

---

# 5. AMI

AMI = Amazon Machine Image

Operating System Template।

Examples

- Ubuntu
    
- Amazon Linux
    
- Windows Server
    

---

# 6. Instance Types

Examples

```text
t2.micro

t3.micro

t3.small

m5.large
```

Interview

t2.micro Free Tier.

---

# 7. Key Pair

EC2 Password-এর পরিবর্তে SSH Key ব্যবহার করে।

Files

```text
mykey.pem
```

Linux Login

```bash
ssh -i mykey.pem ubuntu@IP
```

---

# 8. Security Group

সবচেয়ে Common Question।

Security Group = Virtual Firewall

Inbound Rules

↓

Who can enter

Outbound Rules

↓

Who can leave

Example

Allow

```text
22

80

443
```

Block

Everything Else

---

# 9. EC2 State

Running

Stopped

Reboot

Terminate

Difference

Stop

↓

Can Start Again

Terminate

↓

Deleted Permanently

---

# 10. Elastic IP

Normally

EC2 Public IP Changes

Elastic IP

↓

Static Public IP

---

# 11. EBS (Elastic Block Store)

Virtual Hard Disk

Attach হয় EC2-এর সাথে।

Example

```text
EC2

↓

100GB EBS
```

---

## Snapshot

Backup

```text
EBS

↓

Snapshot

↓

S3
```

---

# 12. S3 (Simple Storage Service)

সবচেয়ে Popular Storage।

Stores

- Image
    
- Video
    
- Backup
    
- PDF
    
- Logs
    

---

## Object Storage

File

↓

Object

↓

Bucket

---

# 13. Bucket

Container

Example

```text
company-backup
```

Inside

```text
photo.jpg

resume.pdf

video.mp4
```

---

# 14. Storage Classes

### Standard

Frequently Used

---

### IA

Infrequent Access

---

### Glacier

Archive

Very Cheap

---

### Deep Archive

Old Backup

---

# 15. Versioning

Old Version Save করে।

Delete করলে Restore করা যায়।

---

# 16. IAM (Identity Access Management)

AWS Security-এর Heart।

Controls

- User
    
- Group
    
- Role
    
- Permission
    
- Policy
    

---

## IAM User

Example

```text
Atiar
```

---

## IAM Group

```text
Developers
```

সব Developer একই Permission।

---

## IAM Policy

JSON Permission

Example

```json
{
 "Effect":"Allow",
 "Action":"s3:*"
}
```

---

## IAM Role

Temporary Permission

Example

EC2

↓

IAM Role

↓

Access S3

No Password Needed

---

# 17. VPC (Virtual Private Cloud)

নিজের Private Network।

Example

```text
Internet

↓

VPC

↓

EC2

↓

Database
```

---

# 18. Subnet

VPC-এর ছোট অংশ।

Types

Public

Private

---

## Public Subnet

Internet Access

Web Server

---

## Private Subnet

No Internet

Database

---

# 19. Internet Gateway

Internet

↓

IGW

↓

VPC

Internet Connection দেয়।

---

# 20. Route Table

Controls Traffic।

Example

```text
0.0.0.0/0

↓

Internet Gateway
```

---

# 21. NAT Gateway

Private Server

↓

Internet Access

↓

Cannot Receive Public Traffic

Used for Updates.

---

# 22. Load Balancer (ELB)

Traffic ভাগ করে।

```text
Users

↓

ELB

↓

EC2

↓

EC2

↓

EC2
```

Types

- Application Load Balancer (ALB)
    
- Network Load Balancer (NLB)
    

---

# 23. Auto Scaling

Traffic বেড়েছে

↓

New EC2

Traffic কমেছে

↓

Terminate Extra EC2

---

# 24. RDS

Managed Database

Supports

- MySQL
    
- PostgreSQL
    
- MariaDB
    

Benefits

No Manual Backup

---

# 25. CloudWatch

Monitoring

CPU

Memory (custom metrics)

Network

Disk

Alarm

---

# 26. Route53

AWS DNS Service

Example

```text
google.com

↓

IP Address
```

---

# 27. SQS

Queue Service

Application Decoupling

---

# 28. SNS

Notification Service

Email

SMS

Lambda Trigger

---

# 29. Lambda

Serverless

Upload Code

↓

Run Automatically

Pay only when code runs.

---

# 30. Shared Responsibility Model

AWS

Responsible

- Data Center
    
- Hardware
    
- Physical Security
    

Customer

Responsible

- Password
    
- IAM
    
- Data
    
- Applications
    
- Security Group Rules
    

---

# Real Architecture

```text
User

↓

Route53

↓

Load Balancer

↓

EC2

↓

RDS

↓

S3

↓

CloudWatch
```

---

# Real DevOps Example

Developer

↓

Git Push

↓

Jenkins

↓

Build

↓

Docker

↓

EC2

↓

CloudWatch Monitor

---

# Interview Questions

### EC2 কী?

Virtual Machine।

---

### S3 কী?

Object Storage।

---

### EBS কী?

Block Storage।

---

### IAM কী?

Identity & Access Management।

---

### Security Group কী?

Virtual Firewall।

---

### VPC কী?

Private Network।

---

### Public Subnet কোথায় ব্যবহার হয়?

Web Server।

---

### Private Subnet কোথায়?

Database।

---

### Auto Scaling কী?

Automatically Increase/Decrease EC2।

---

### Route53 কী?

DNS Service।

---

### CloudWatch কী?

Monitoring Service।

---

# AWS Architecture Interview

```text
Internet

↓

Route53

↓

Load Balancer

↓

EC2 (Web Server)

↓

RDS (Database)

↓

S3 (Images)

↓

CloudWatch
```

প্রতিটি কম্পোনেন্টের কাজ:

- **Route53:** Domain name-কে IP-তে রূপান্তর করে।
    
- **Load Balancer:** ট্রাফিক একাধিক EC2-তে ভাগ করে।
    
- **EC2:** আপনার অ্যাপ্লিকেশন চালায়।
    
- **RDS:** ডেটাবেস পরিচালনা করে।
    
- **S3:** ছবি, ভিডিও, ব্যাকআপ সংরক্ষণ করে।
    
- **CloudWatch:** সার্ভারের স্বাস্থ্য ও পারফরম্যান্স পর্যবেক্ষণ করে।
    

---

# BJIT Assessment-এর জন্য Most Important MCQs

### 1. EC2 হলো—

A. Database

B. Virtual Machine ✅

C. DNS

D. Firewall

---

### 2. S3 হলো—

A. Block Storage

B. Object Storage ✅

C. Database

D. Cache

---

### 3. Security Group কী?

A. Antivirus

B. Virtual Firewall ✅

C. Database

D. Backup

---

### 4. IAM-এর কাজ কী?

A. Storage

B. User & Permission Management ✅

C. VM

D. Monitoring

---

### 5. কোন Service Traffic Distribute করে?

A. Route53

B. ELB ✅

C. IAM

D. CloudWatch

---

### 6. কোন Service Monitoring-এর জন্য?

A. EC2

B. CloudWatch ✅

C. Lambda

D. S3

---

# ⭐ BJIT পরীক্ষার জন্য Top 20 AWS Concepts (মুখস্থ ও বুঝে রাখুন)

1. AWS কী?
    
2. Region
    
3. Availability Zone
    
4. EC2
    
5. AMI
    
6. Instance Type
    
7. Key Pair
    
8. Security Group
    
9. Elastic IP
    
10. EBS
    
11. Snapshot
    
12. S3
    
13. Bucket
    
14. IAM
    
15. IAM User vs Role
    
16. VPC
    
17. Public vs Private Subnet
    
18. Internet Gateway
    
19. Load Balancer
    
20. Auto Scaling
    

এই ২০টি বিষয় ভালোভাবে বুঝে গেলে Cloud & DevOps Trainee assessment-এ AWS অংশের বেশিরভাগ মৌলিক প্রশ্নের উত্তর দিতে পারবেন।


---

# Lesson 6: Docker (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি Docker কী, কেন ব্যবহার করা হয়, Image, Container, Dockerfile, Volume, Network, Docker Hub এবং Docker Compose সম্পর্কে পরিষ্কার ধারণা পাবেন।

---

# 1. Docker কী?

Docker হলো একটি **Containerization Platform**।

এটি Application-কে তার সব Dependencies (Library, Runtime, Configuration) সহ Package করে একটি **Container**-এ চালায়।

### Real Life Example

ধরুন আপনি একটি Python App লিখেছেন।

Without Docker

```text
Your Laptop
├── Python 3.10
├── Flask
├── MySQL Driver
└── Other Libraries
```

অন্য কম্পিউটারে একই App চালাতে সবকিছু আবার Install করতে হবে।

With Docker

```text
Docker Image
├── Python
├── Flask
├── Libraries
└── Your App
```

যে কোনো Docker থাকা Machine-এ একইভাবে চলবে।

---

# 2. Why Docker?

Without Docker

```
Developer PC
↓
Works Fine
↓
Production Server
↓
Error
```

এই সমস্যাকে বলে

> **"Works on my machine"**

Docker এই সমস্যা দূর করে।

---

# 3. Traditional Deployment

```
Application

↓

Install Java

↓

Install Python

↓

Install Libraries

↓

Run
```

---

# Docker Deployment

```
Application

↓

Docker Image

↓

Docker Container

↓

Run Anywhere
```

---

# 4. Virtual Machine vs Docker

## Virtual Machine

```
Hardware

↓

Hypervisor

↓

VM

↓

Guest OS

↓

Application
```

---

## Docker

```
Hardware

↓

Host OS

↓

Docker Engine

↓

Container

↓

Application
```

---

### Comparison

|VM|Docker|
|---|---|
|Full OS|Shared OS Kernel|
|Heavy|Lightweight|
|Slow Boot|Fast Boot|
|GB Size|MB Size|
|High RAM|Low RAM|

---

# 5. Docker Architecture

```
Docker Client

↓

Docker Daemon

↓

Images

↓

Containers
```

---

# 6. Docker Components

### Docker Engine

Docker-এর Core Service।

---

### Docker Image

Image হলো Template।

Example

```
Ubuntu Image

Python Image

Nginx Image
```

Image = Blueprint

---

### Docker Container

Container হলো Running Image।

```
Image

↓

Run

↓

Container
```

একটি Image থেকে অনেক Container তৈরি করা যায়।

---

# 7. Image vs Container

Image

- Read Only
    
- Template
    

Container

- Running Process
    
- Writable
    

Example

```
Ubuntu Image

↓

Container1

Container2

Container3
```

---

# 8. Docker Installation

Ubuntu

```bash
sudo apt update

sudo apt install docker.io
```

Start Docker

```bash
sudo systemctl start docker
```

Enable Docker

```bash
sudo systemctl enable docker
```

Check Version

```bash
docker --version
```

---

# 9. Docker Commands

### Download Image

```bash
docker pull ubuntu
```

---

### List Images

```bash
docker images
```

---

### Run Container

```bash
docker run ubuntu
```

---

### Interactive Mode

```bash
docker run -it ubuntu bash
```

---

### Running Containers

```bash
docker ps
```

---

### All Containers

```bash
docker ps -a
```

---

### Stop Container

```bash
docker stop containerID
```

---

### Start Container

```bash
docker start containerID
```

---

### Remove Container

```bash
docker rm containerID
```

---

### Remove Image

```bash
docker rmi imageID
```

---

# 10. Dockerfile

Dockerfile হলো Docker Image তৈরির Recipe।

Example

```dockerfile
FROM ubuntu

RUN apt update

RUN apt install -y nginx

CMD ["nginx","-g","daemon off;"]
```

---

### Build Image

```bash
docker build -t myapp .
```

---

### Run

```bash
docker run myapp
```

---

# 11. Docker Hub

Docker-এর GitHub।

এখানে Image রাখা হয়।

Examples

```
ubuntu

nginx

mysql

redis

python
```

Pull

```bash
docker pull nginx
```

---

# 12. Docker Network

Container একে অপরের সাথে Network-এর মাধ্যমে যোগাযোগ করে।

Types

- Bridge
    
- Host
    
- None
    

Default

Bridge

---

# 13. Docker Volume

Container Delete হলে Data Delete হতে পারে।

Volume Data Save রাখে।

Example

```
Container

↓

Volume

↓

Data
```

Command

```bash
docker volume create myvolume
```

---

# 14. Port Mapping

Suppose

Container

```
80
```

Host

```
8080
```

Command

```bash
docker run -p 8080:80 nginx
```

Meaning

```
Host 8080

↓

Container 80
```

---

# 15. Environment Variables

```bash
docker run -e MYSQL_ROOT_PASSWORD=123456 mysql
```

---

# 16. Docker Logs

```bash
docker logs containerID
```

---

# 17. Execute Command

```bash
docker exec -it containerID bash
```

---

# 18. Docker Compose

একাধিক Container একসাথে Run করার Tool।

Example

```
Web

↓

Database

↓

Redis
```

Compose File

```yaml
version: "3"

services:

  web:

    image: nginx

  db:

    image: mysql
```

Run

```bash
docker compose up
```

Stop

```bash
docker compose down
```

---

# 19. Real DevOps Example

Developer

↓

Git Push

↓

Jenkins

↓

Build Docker Image

↓

Push Docker Hub

↓

Deploy Kubernetes

---

# 20. Docker in AWS

```
Developer

↓

GitHub

↓

Jenkins

↓

Docker Build

↓

Push Image

↓

AWS EC2

↓

Run Container
```

---

# 21. Advantages

- Portable
    
- Lightweight
    
- Fast
    
- Easy Deployment
    
- Isolation
    
- Same Environment Everywhere
    

---

# 22. Disadvantages

- Shared Kernel
    
- Less Isolation than VM
    
- Requires Container Runtime
    

---

# Interview Questions

### Docker কী?

Container Platform।

---

### Docker Image কী?

Template।

---

### Docker Container কী?

Running Image।

---

### Dockerfile কী?

Image তৈরির Script।

---

### Docker Hub কী?

Image Repository।

---

### Docker Volume কেন ব্যবহার হয়?

Data Persist করার জন্য।

---

### Port Mapping কী?

Host Port কে Container Port-এর সাথে যুক্ত করা।

Example

```bash
docker run -p 8080:80 nginx
```

---

### VM vs Docker?

VM

Full OS

Docker

Shared Kernel

---

# Docker Workflow

```
Dockerfile

↓

docker build

↓

Image

↓

docker run

↓

Container
```

---

# Common Docker Commands

```bash
docker pull

docker images

docker run

docker ps

docker ps -a

docker stop

docker start

docker rm

docker rmi

docker logs

docker exec

docker build

docker volume

docker network

docker compose up
```

---

# MCQ Practice

### 1. Docker কী?

A. Database

B. Container Platform ✅

C. Operating System

D. Programming Language

---

### 2. Docker Image হলো—

A. Running Application

B. Template ✅

C. Network

D. Volume

---

### 3. Running Image-কে কী বলা হয়?

A. Repository

B. Volume

C. Container ✅

D. Layer

---

### 4. কোন Command Image Download করে?

A. `docker images`

B. `docker pull` ✅

C. `docker ps`

D. `docker stop`

---

### 5. `docker ps` কী দেখায়?

A. Images

B. Running Containers ✅

C. Networks

D. Volumes

---

### 6. কোন Command Host Port 8080-কে Container Port 80-এর সাথে Map করে?

A.

```bash
docker run nginx
```

B.

```bash
docker run -p 8080:80 nginx
```

✅

C.

```bash
docker pull nginx
```

D.

```bash
docker stop nginx
```

---

### 7. Dockerfile-এর কাজ কী?

A. Database তৈরি

B. Image Build করার নির্দেশনা দেওয়া ✅

C. Container Delete করা

D. Network তৈরি করা

---

# 🎯 BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ Docker Topics

1. Docker কী?
    
2. Docker vs Virtual Machine
    
3. Image vs Container
    
4. Docker Engine
    
5. Docker Hub
    
6. Dockerfile
    
7. `docker pull`
    
8. `docker run`
    
9. `docker ps`
    
10. `docker stop`
    
11. `docker exec`
    
12. `docker logs`
    
13. Docker Volume
    
14. Docker Network
    
15. Port Mapping (`-p host:container`)
    
16. Docker Compose
    

---

## 🚀 Quick Revision (১ মিনিটে)

- **Docker =** Container Platform
    
- **Image =** Template
    
- **Container =** Running Image
    
- **Docker Hub =** Image Repository
    
- **Dockerfile =** Image তৈরির Recipe
    
- **`docker pull` =** Image Download
    
- **`docker run` =** Container Start
    
- **`docker ps` =** Running Containers দেখায়
    
- **Volume =** Container-এর Data স্থায়ীভাবে সংরক্ষণ করে
    
- **`-p 8080:80` =** Host Port 8080 → Container Port 80
    

এই Lesson-এর পর **Lesson 7: Kubernetes** শুরু করলে Docker-এর পর Container Orchestration কীভাবে কাজ করে তা পরিষ্কার হয়ে যাবে।

---
# Lesson 7: Kubernetes (K8s) Basic → Advanced for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি Kubernetes কী, কেন ব্যবহার করা হয়, Pod, Node, Cluster, Deployment, Service, ReplicaSet, ConfigMap, Secret, Namespace এবং Ingress সম্পর্কে পরিষ্কার ধারণা পাবেন।

---

# 1. Kubernetes কী?

Kubernetes (K8s) হলো একটি **Container Orchestration Platform**।

এটি Docker Container-কে Manage করে।

Google এটি তৈরি করেছে।

---

## Real Life Example

Suppose

আপনার

```text
1000 Docker Containers
```

আছে।

সব Manual ভাবে Manage করা অসম্ভব।

তখন Kubernetes ব্যবহার করা হয়।

---

# 2. Why Kubernetes?

Without Kubernetes

```text
Developer

↓

Docker

↓

Run Container
```

যদি Container Crash করে?

Manual Restart করতে হবে।

---

With Kubernetes

```text
Container Crash

↓

Automatically Restart
```

---

# 3. Docker vs Kubernetes

Docker

- Container তৈরি করে
    

Kubernetes

- অনেক Container Manage করে
    

সহজে মনে রাখুন

> Docker builds Containers.

> Kubernetes manages Containers.

---

# 4. Kubernetes Architecture

```text
                Cluster
          ┌────────────────┐
          │                │
 Master    │ Control Plane │
          │                │
          └──────┬─────────┘
                 │
      ┌──────────┴─────────┐
      │                    │
   Worker Node         Worker Node
      │                    │
    Pods                Pods
```

---

# 5. Cluster

সব Nodes-এর Collection।

Example

```text
Cluster

↓

Node1

↓

Node2

↓

Node3
```

---

# 6. Node

Node = Computer

হতে পারে

- Physical
    
- Virtual Machine
    

প্রতিটি Node-এর মধ্যে অনেক Pod থাকে।

---

# 7. Master Node (Control Plane)

এটি পুরো Cluster Control করে।

কাজ

- Scheduling
    
- API
    
- Monitoring
    
- Scaling
    

---

# 8. Worker Node

Application Run করে।

এর ভিতরে থাকে

- Pods
    
- kubelet
    
- Container Runtime
    

---

# 9. Pod

সবচেয়ে গুরুত্বপূর্ণ Concept।

Pod হলো

> Kubernetes-এর Smallest Deployable Unit।

Pod-এর ভিতরে

একটি বা একাধিক Container থাকে।

Example

```text
Pod

↓

Nginx Container
```

---

# 10. One Pod = One Application

Example

```text
Pod

↓

Python App
```

---

# 11. ReplicaSet

Suppose

আপনার

১টি Pod

Crash করলো।

ReplicaSet

Automatically

New Pod Create করবে।

Example

```text
Desired = 3

Running = 2

↓

Create New Pod
```

---

# 12. Deployment

Deployment

ReplicaSet Manage করে।

Example

```text
Deployment

↓

ReplicaSet

↓

Pods
```

Deployment দিয়ে

- Update
    
- Rollback
    
- Scale
    

করা যায়।

---

# 13. Scaling

Current

```text
2 Pods
```

Need

```text
5 Pods
```

Deployment

↓

Automatically

5 Pods

---

# 14. Rolling Update

Old Version

↓

New Version

↓

One by One Update

No Downtime

---

# 15. Rollback

New Version

↓

Bug

↓

Rollback

↓

Old Version

---

# 16. Service

Pod-এর IP বারবার Change হয়।

Service

Stable IP দেয়।

Example

```text
User

↓

Service

↓

Pod

↓

Pod

↓

Pod
```

---

# 17. Service Types

### ClusterIP

Internal Communication

(Default)

---

### NodePort

Outside Access

Example

```text
30000
```

---

### LoadBalancer

Cloud Provider

AWS

Azure

Google Cloud

---

# 18. Ingress

Suppose

```text
app.com

shop.com

blog.com
```

সব

এক Load Balancer

থেকে Access।

এটাই

Ingress।

---

# 19. Namespace

Different Teams

```text
Development

Testing

Production
```

সব আলাদা Namespace।

---

# 20. ConfigMap

Application Configuration রাখে।

Example

```text
Database URL

Environment

Port
```

---

# 21. Secret

Sensitive Information

Stores

- Password
    
- API Key
    
- Token
    

⚠ Password কখনো ConfigMap-এ রাখবেন না।

---

# 22. Persistent Volume (PV)

Container Delete

↓

Data থাকবে।

---

# 23. Persistent Volume Claim (PVC)

Application

↓

Requests Storage

---

# 24. Labels

Suppose

```text
App=Web

App=Database
```

Labels দিয়ে Filter করা হয়।

---

# 25. Selectors

Select

Matching Labels

---

# 26. kubectl

সবচেয়ে Important Command

See Nodes

```bash
kubectl get nodes
```

Pods

```bash
kubectl get pods
```

Deployments

```bash
kubectl get deployments
```

Services

```bash
kubectl get svc
```

---

# 27. YAML

Kubernetes

YAML File ব্যবহার করে।

Example

```yaml
apiVersion: apps/v1

kind: Deployment

metadata:

  name: nginx

spec:

  replicas: 3
```

---

# 28. Kubernetes Workflow

```text
Developer

↓

Docker Image

↓

Push Docker Hub

↓

Deployment YAML

↓

kubectl apply

↓

Pods Created
```

---

# 29. Kubernetes in AWS

```text
GitHub

↓

Jenkins

↓

Docker Build

↓

Docker Hub

↓

Amazon EKS

↓

Pods Running
```

Amazon EKS = Managed Kubernetes

---

# 30. Kubernetes vs Docker Swarm

|Kubernetes|Docker Swarm|
|---|---|
|Complex|Easy|
|Powerful|Less Powerful|
|Industry Standard|Small Projects|

---

# 31. Real DevOps Pipeline

```text
Developer

↓

Git Push

↓

GitHub

↓

Jenkins

↓

Docker Build

↓

Docker Hub

↓

Kubernetes

↓

Pods

↓

Users
```

---

# Interview Questions

### Kubernetes কী?

Container Orchestration Platform।

---

### Pod কী?

Smallest Deployable Unit।

---

### Node কী?

Machine।

---

### Cluster কী?

Collection of Nodes।

---

### Deployment কী?

Manage Pods।

---

### ReplicaSet কী?

Maintains Desired Number of Pods।

---

### Service কী?

Stable Network Access।

---

### ConfigMap কী?

Configuration Store।

---

### Secret কী?

Sensitive Data।

---

### Ingress কী?

HTTP Routing।

---

### kubectl কী?

CLI Tool।

---

# Important kubectl Commands

```bash
kubectl get nodes

kubectl get pods

kubectl get deployments

kubectl get svc

kubectl apply -f app.yaml

kubectl delete pod podname

kubectl describe pod podname

kubectl logs podname
```

---

# Kubernetes Architecture

```text
User

↓

Ingress

↓

Service

↓

Deployment

↓

ReplicaSet

↓

Pods

↓

Containers
```

---

# Kubernetes MCQ

### 1. Kubernetes কী?

A Database

Programming Language

Container Orchestration Platform ✅

Operating System

---

### 2. Smallest Deployable Unit?

Container

Pod ✅

Deployment

Service

---

### 3. ReplicaSet কী করে?

Backup

Monitoring

Maintain Pod Count ✅

Storage

---

### 4. Stable Network দেয়?

Deployment

Service ✅

Pod

Volume

---

### 5. Sensitive Data কোথায় রাখবেন?

ConfigMap

Secret ✅

Deployment

Service

---

### 6. Kubernetes CLI Tool?

docker

kubectl ✅

aws

git

---

# Docker vs Kubernetes (Interview Favorite)

|Docker|Kubernetes|
|---|---|
|Container তৈরি করে|Container Manage করে|
|Single Host|Multi-node Cluster|
|Lightweight|Orchestration Platform|
|docker run|kubectl apply|

---

# BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ Kubernetes Topics

1. Kubernetes কী
    
2. Docker vs Kubernetes
    
3. Pod
    
4. Node
    
5. Cluster
    
6. Deployment
    
7. ReplicaSet
    
8. Service
    
9. ConfigMap
    
10. Secret
    
11. Ingress
    
12. Namespace
    
13. kubectl
    
14. YAML
    
15. Amazon EKS
    

---

# 🔥 Quick Revision (১ মিনিটে)

- **Kubernetes =** Container Orchestration Platform
    
- **Cluster =** Nodes-এর Collection
    
- **Node =** একটি Machine (VM বা Physical)
    
- **Pod =** Smallest Deployable Unit
    
- **Deployment =** Pods Manage করে
    
- **ReplicaSet =** নির্দিষ্ট সংখ্যক Pod চালু রাখে
    
- **Service =** Pod-কে Stable IP/Access দেয়
    
- **ConfigMap =** Configuration সংরক্ষণ করে
    
- **Secret =** Password/API Key সংরক্ষণ করে
    
- **Ingress =** HTTP/HTTPS Routing
    
- **kubectl =** Kubernetes Command Line Tool
    

---

## 🎯 BJIT Trainee Assessment Tip

যেহেতু এটি **Trainee** পদের পরীক্ষা, তাই Kubernetes থেকে সাধারণত **Basic Concept**-ই বেশি আসে। YAML syntax মুখস্থ করার চেয়ে **Pod, Deployment, ReplicaSet, Service, Node, Cluster**—এই ধারণাগুলো পরিষ্কার রাখুন।

### বাকি গুরুত্বপূর্ণ Lesson

এখন শুধু **Lesson 8: CI/CD & Jenkins** বাকি, যা DevOps-এর সবচেয়ে বেশি জিজ্ঞাসিত বিষয়গুলোর একটি। এরপর চাইলে আমি **২০০+ সম্ভাব্য BJIT MCQ (উত্তর ও ব্যাখ্যাসহ)** দিতে পারি, যাতে পরীক্ষার আগে সম্পূর্ণ রিভিশন হয়ে যায়।

---
# Lesson 8: CI/CD & Jenkins (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি DevOps, CI/CD, Jenkins, Pipeline, Build, Test, Deploy এবং Git + Docker + Kubernetes-এর সম্পূর্ণ Workflow বুঝতে পারবেন।

---

# 1. What is DevOps?

DevOps = **Development + Operations**

আগে

```text
Developer

↓

Code Complete

↓

Operations Team

↓

Deploy
```

এতে সময় বেশি লাগত।

DevOps-এ

```text
Developer

↓

Git

↓

CI/CD

↓

Deploy

↓

Monitor
```

Automation-এর মাধ্যমে দ্রুত Software Release করা যায়।

---

# 2. Why DevOps?

আগে

- Manual Deployment
    
- বেশি Error
    
- Slow Release
    

DevOps

- Automation
    
- Faster Deployment
    
- Better Quality
    
- Less Human Error
    

---

# 3. DevOps Lifecycle

```text
Plan

↓

Code

↓

Build

↓

Test

↓

Release

↓

Deploy

↓

Operate

↓

Monitor
```

Interview-এ এটি খুবই জনপ্রিয় প্রশ্ন।

---

# 4. What is CI?

CI = **Continuous Integration**

Developer-রা বারবার Code Push করে।

GitHub

↓

Automatically Build

↓

Automatically Test

Example

```text
Developer A

↓

Git Push

↓

Jenkins Build

↓

Tests Pass
```

---

# 5. What is CD?

CD = দুইভাবে বলা হয়

- Continuous Delivery
    
- Continuous Deployment
    

### Continuous Delivery

Build Ready থাকে।

Human Approval-এর পর Deploy।

---

### Continuous Deployment

Build Finished

↓

Automatically Production Deploy

No Human Approval.

---

# 6. CI vs CD

|CI|CD|
|---|---|
|Build + Test|Deploy|
|Code Integration|Application Release|
|Early Error Detection|Fast Delivery|

---

# 7. CI/CD Pipeline

```text
Git Push

↓

Build

↓

Test

↓

Docker Build

↓

Deploy

↓

Monitor
```

এটাই CI/CD Pipeline।

---

# 8. Jenkins

Jenkins হলো

**Automation Server**

সবচেয়ে Popular CI/CD Tool।

---

# 9. Jenkins Features

- Build Automation
    
- Test Automation
    
- Deploy Automation
    
- Plugins
    
- Pipeline
    

---

# 10. Jenkins Architecture

```text
Developer

↓

GitHub

↓

Jenkins

↓

Docker

↓

AWS

↓

Users
```

---

# 11. Jenkins Job

একটি Automation Task।

Example

```text
Build Website
```

---

# 12. Jenkins Pipeline

একাধিক Step-এর Automation।

Example

```text
Git Pull

↓

Build

↓

Test

↓

Deploy
```

---

# 13. Jenkinsfile

Pipeline Code।

Example

```groovy
pipeline {
    agent any

    stages {

        stage('Build'){
            steps{
                echo "Building..."
            }
        }

        stage('Test'){
            steps{
                echo "Testing..."
            }
        }

        stage('Deploy'){
            steps{
                echo "Deploying..."
            }
        }

    }
}
```

Interview-এ শুধু Jenkinsfile কী জানলেই যথেষ্ট।

---

# 14. Build

Source Code

↓

Compile

↓

Package

↓

Executable

Java

↓

JAR

Python

↓

Requirements Install

---

# 15. Test

Types

- Unit Test
    
- Integration Test
    
- Functional Test
    

CI-তে Automatically হয়।

---

# 16. Deploy

Application

↓

Server

Example

AWS EC2

Docker

Kubernetes

---

# 17. Git + Jenkins

Workflow

```text
Developer

↓

git push

↓

GitHub

↓

Webhook

↓

Jenkins

↓

Pipeline Start
```

Webhook = GitHub Jenkins-কে Notify করে।

---

# 18. Docker + Jenkins

```text
GitHub

↓

Jenkins

↓

docker build

↓

Docker Image

↓

Docker Hub
```

---

# 19. Kubernetes + Jenkins

```text
GitHub

↓

Jenkins

↓

Docker Image

↓

Docker Hub

↓

Kubernetes Deployment
```

---

# 20. Complete DevOps Pipeline

```text
Developer

↓

Git

↓

GitHub

↓

Jenkins

↓

Build

↓

Test

↓

Docker

↓

Docker Hub

↓

Kubernetes

↓

AWS

↓

Users
```

এটি Interview-এর Favorite Diagram।

---

# 21. Monitoring

Deploy-এর পর

Monitor

Tools

- CloudWatch
    
- Prometheus
    
- Grafana
    

---

# 22. Rollback

New Version

↓

Problem

↓

Rollback

↓

Old Version

---

# 23. Benefits of CI/CD

- Fast Delivery
    
- Less Error
    
- Better Quality
    
- Automation
    
- Faster Testing
    
- Frequent Release
    

---

# 24. Popular CI/CD Tools

|Tool|Purpose|
|---|---|
|Jenkins|CI/CD|
|GitHub Actions|CI/CD|
|GitLab CI|CI/CD|
|CircleCI|CI/CD|
|Azure DevOps|CI/CD|

---

# 25. DevOps Tools

|Tool|Use|
|---|---|
|Git|Version Control|
|GitHub|Code Hosting|
|Jenkins|CI/CD|
|Docker|Container|
|Kubernetes|Orchestration|
|AWS|Cloud|
|Linux|Server|
|Ansible|Automation|
|Terraform|Infrastructure as Code|

---

# Real Example

Suppose

আপনি Website Update করলেন।

```text
Developer

↓

Git Push

↓

GitHub

↓

Jenkins Detect

↓

Build

↓

Run Tests

↓

Docker Build

↓

Push Docker Hub

↓

Deploy Kubernetes

↓

Users See New Website
```

সব Automatic।

---

# Interview Questions

### DevOps কী?

Development + Operations.

---

### CI Full Form?

Continuous Integration.

---

### CD Full Form?

Continuous Delivery / Continuous Deployment.

---

### Jenkins কী?

Automation Server.

---

### Jenkins-এর কাজ?

Build

Test

Deploy

Automation.

---

### Pipeline কী?

Automation Steps.

---

### Jenkinsfile কী?

Pipeline-এর Script।

---

### Build কী?

Compile Application.

---

### Deploy কী?

Application Server-এ Publish করা।

---

### Rollback কী?

Previous Version-এ ফিরে যাওয়া।

---

# Complete DevOps Workflow

```text
Code

↓

Git

↓

GitHub

↓

Jenkins

↓

Build

↓

Test

↓

Docker

↓

Docker Hub

↓

Kubernetes

↓

AWS

↓

Monitoring
```

---

# MCQ Practice

### 1. CI-এর Full Form?

A. Continuous Internet

B. Continuous Integration ✅

C. Continuous Install

D. Continuous Instance

---

### 2. Jenkins কী?

A. Database

B. CI/CD Tool ✅

C. Programming Language

D. Operating System

---

### 3. Pipeline কী?

A. Database

B. Automation Workflow ✅

C. Container

D. Network

---

### 4. কোন Tool Container তৈরি করে?

A. Jenkins

B. Docker ✅

C. Git

D. Linux

---

### 5. Kubernetes-এর কাজ?

A. Database

B. Container Orchestration ✅

C. DNS

D. Firewall

---

### 6. CI/CD-এর সবচেয়ে বড় সুবিধা?

A. More Manual Work

B. Automation & Faster Delivery ✅

C. Slow Deployment

D. More Errors

---

# BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ CI/CD Topics

- DevOps কী?
    
- DevOps Lifecycle
    
- CI vs CD
    
- Jenkins
    
- Jenkins Pipeline
    
- Jenkinsfile
    
- Build
    
- Test
    
- Deploy
    
- Git → Jenkins → Docker → Kubernetes → AWS Workflow
    
- Rollback
    
- Monitoring
    

---

# 🔥 Complete DevOps Roadmap (সব Lesson একসাথে)

```text
Linux
↓

Networking
↓

Git & GitHub
↓

Cloud Computing
↓

AWS
↓

Docker
↓

Kubernetes
↓

Jenkins (CI/CD)
↓

Monitoring
```

---

# 🚀 5 মিনিটের Quick Revision (পরীক্ষার আগে)

### Linux

- `ls`, `cd`, `pwd`, `mkdir`, `rm`, `cp`, `mv`
    
- File Permission: `chmod`
    
- Process: `ps`, `top`, `kill`
    

### Networking

- IP Address
    
- DNS
    
- HTTP (80)
    
- HTTPS (443)
    
- SSH (22)
    
- TCP vs UDP
    

### Git

- `git init`
    
- `git add`
    
- `git commit`
    
- `git push`
    
- `git pull`
    
- Branch
    

### AWS

- EC2 = Virtual Machine
    
- S3 = Object Storage
    
- IAM = User & Permission
    
- VPC = Private Network
    
- Security Group = Virtual Firewall
    

### Docker

- Image = Template
    
- Container = Running Image
    
- `docker pull`
    
- `docker run`
    
- Dockerfile
    

### Kubernetes

- Pod
    
- Deployment
    
- Service
    
- ReplicaSet
    
- Cluster
    

### Jenkins

- CI = Continuous Integration
    
- CD = Continuous Delivery/Deployment
    
- Pipeline
    
- Build → Test → Deploy
    

---

## 🎯 আমার ধারণা অনুযায়ী BJIT Trainee Cloud & DevOps Assessment-এ সবচেয়ে বেশি জিজ্ঞাসিত ১০টি প্রশ্ন

1. Linux Command (`ls`, `pwd`, `cd`)
    
2. Git vs GitHub
    
3. HTTP vs HTTPS
    
4. TCP vs UDP
    
5. EC2 কী?
    
6. S3 কী?
    
7. Docker Image vs Container
    
8. Pod কী?
    
9. CI/CD-এর Full Form
    
10. Jenkins-এর কাজ কী?
    

এই ৮টি Lesson শেষ করলে Cloud & DevOps Trainee পদের জন্য একটি শক্ত ভিত্তি তৈরি হবে। এখন সবচেয়ে ভালো প্রস্তুতি হবে **MCQ Practice**, কারণ ৩০ মিনিটের পরীক্ষায় সাধারণত দ্রুত উত্তর দেওয়ার মতো প্রশ্নই বেশি থাকে। 

---
# Lesson 9: Shell Scripting (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি Linux Shell Script লিখতে, Automation করতে এবং BJIT Cloud & DevOps Trainee assessment-এর Shell Scripting অংশের Basic Questions-এর উত্তর দিতে পারবেন।

---

# 1. Shell কী?

Shell হলো User এবং Linux Kernel-এর মধ্যে Interface।

```text
User

↓

Shell (Bash)

↓

Linux Kernel

↓

Hardware
```

সবচেয়ে জনপ্রিয় Shell

- Bash (Most Common)
    
- Zsh
    
- Sh
    
- Ksh
    

---

# 2. Shell Script কী?

অনেক Linux Command একসাথে লিখে একটি File-এ Save করলে সেটাকে Shell Script বলে।

Example

```bash
#!/bin/bash

echo "Hello World"
```

Save করুন

```text
hello.sh
```

Run করুন

```bash
bash hello.sh
```

অথবা

```bash
chmod +x hello.sh

./hello.sh
```

---

# 3. Shebang

প্রথম Line

```bash
#!/bin/bash
```

মানে

এই Script Bash দিয়ে Execute হবে।

---

# 4. Comments

Single Line

```bash
# This is comment
```

---

# 5. Print Output

```bash
echo "Hello"
```

Output

```text
Hello
```

---

# 6. Variables

```bash
name="Atiar"

echo $name
```

Output

```text
Atiar
```

---

## Number Variable

```bash
age=25

echo $age
```

---

# 7. User Input

```bash
echo "Enter Name"

read name

echo "Welcome $name"
```

Example

```
Enter Name
Atiar

Welcome Atiar
```

---

# 8. Arithmetic

```bash
a=10

b=5

echo $((a+b))
```

Output

```
15
```

More

```bash
echo $((a-b))

echo $((a*b))

echo $((a/b))
```

---

# 9. If Statement

```bash
age=20

if [ $age -ge 18 ]

then

echo "Adult"

fi
```

Output

```
Adult
```

---

# 10. If Else

```bash
marks=40

if [ $marks -ge 50 ]

then

echo "Pass"

else

echo "Fail"

fi
```

---

# 11. Comparison Operators

|Operator|Meaning|
|---|---|
|-eq|Equal|
|-ne|Not Equal|
|-gt|Greater Than|
|-lt|Less Than|
|-ge|Greater or Equal|
|-le|Less or Equal|

Example

```bash
if [ $a -gt $b ]
```

---

# 12. String Comparison

```bash
name="Atiar"

if [ "$name" = "Atiar" ]

then

echo "Correct"

fi
```

---

# 13. For Loop

```bash
for i in 1 2 3 4 5

do

echo $i

done
```

Output

```
1

2

3

4

5
```

---

# 14. While Loop

```bash
i=1

while [ $i -le 5 ]

do

echo $i

i=$((i+1))

done
```

---

# 15. Functions

```bash
hello(){

echo "Hello"

}

hello
```

Output

```
Hello
```

---

# 16. Command Line Arguments

Script

```bash
echo $1

echo $2
```

Run

```bash
bash test.sh Atiar Linux
```

Output

```
Atiar

Linux
```

---

# 17. Exit Status

Linux Command Success

```
0
```

Failure

```
Non-zero
```

Check

```bash
echo $?
```

---

# 18. File Check

```bash
if [ -f file.txt ]

then

echo "Exists"

fi
```

Useful Options

|Option|Meaning|
|---|---|
|-f|File Exists|
|-d|Directory Exists|
|-r|Readable|
|-w|Writable|
|-x|Executable|

---

# 19. Case Statement

```bash
read choice

case $choice in

1)

echo "Linux"

;;

2)

echo "Docker"

;;

*)

echo "Invalid"

;;

esac
```

---

# 20. Automation Example

Backup Script

```bash
#!/bin/bash

cp data.txt backup.txt

echo "Backup Complete"
```

---

# 21. Real DevOps Example

```text
Every Night

↓

Shell Script

↓

Backup Database

↓

Upload AWS S3

↓

Send Email
```

---

# 22. Cron Job

Automatically Run Script

Open

```bash
crontab -e
```

Run Every Day

12 AM

```bash
0 0 * * * /home/user/backup.sh
```

---

# 23. Environment Variables

Show

```bash
echo $HOME
```

Current User

```bash
echo $USER
```

Current Directory

```bash
echo $PWD
```

---

# 24. Useful Commands

```bash
date

whoami

hostname

pwd

ls

df -h

free -m

uptime
```

---

# 25. Script Example

```bash
#!/bin/bash

echo "System Information"

echo "User: $USER"

echo "Home: $HOME"

echo "Date:"

date

echo "Disk"

df -h
```

---

# Interview Questions

### Shell কী?

Linux Command Interpreter।

---

### Shell Script কী?

Collection of Linux Commands।

---

### Shebang কী?

```bash
#!/bin/bash
```

---

### Variable কীভাবে Declare করবেন?

```bash
name="Atiar"
```

---

### User Input?

```bash
read name
```

---

### If Statement?

```bash
if

then

fi
```

---

### For Loop?

```bash
for
```

---

### Exit Status Success?

```
0
```

---

### Cron Job কী?

Scheduled Task।

---

### Environment Variable Example?

```
HOME

USER

PATH
```

---

# Common Shell Commands

```bash
echo

read

if

for

while

case

cp

mv

rm

mkdir

chmod

crontab

date

pwd

ls
```

---

# MCQ Practice

### 1. Bash Script-এর প্রথম Line?

A)

```bash
echo Hello
```

B)

```bash
#!/bin/bash
```

✅

C)

```bash
read
```

D)

```bash
pwd
```

---

### 2. Output Print করতে কোন Command?

A)

```bash
ls
```

B)

```bash
echo
```

✅

C)

```bash
pwd
```

D)

```bash
cat
```

---

### 3. User Input?

A)

```bash
echo
```

B)

```bash
read
```

✅

C)

```bash
pwd
```

D)

```bash
mkdir
```

---

### 4. Success Exit Code?

A)

1

B)

2

C)

0

✅

D)

100

---

### 5. Cron Job কী?

A)

Compiler

B)

Scheduler

✅

C)

Database

D)

Firewall

---

# 🎯 BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ Shell Scripting Topics

- Shell কী?
    
- Shell Script কী?
    
- `#!/bin/bash`
    
- `echo`
    
- `read`
    
- Variables
    
- `if-else`
    
- `for` Loop
    
- `while` Loop
    
- Functions
    
- Command Line Arguments (`$1`, `$2`)
    
- Exit Status (`$?`)
    
- File Test (`-f`, `-d`)
    
- `crontab`
    
- Environment Variables (`HOME`, `USER`, `PATH`)
    

---

# 🔥 Quick Revision (১ মিনিটে)

- **Shell =** Linux Command Interpreter
    
- **Shell Script =** অনেক Command-এর Automation
    
- `#!/bin/bash` = Bash Script-এর শুরু
    
- `echo` = Output দেখায়
    
- `read` = User Input নেয়
    
- `if` = Condition
    
- `for` = নির্দিষ্ট সংখ্যক বার Loop
    
- `while` = Condition সত্য থাকলে Loop
    
- `chmod +x` = Script Executable করে
    
- `crontab` = নির্দিষ্ট সময়ে Script চালায়
    
- `$HOME`, `$USER`, `$PWD` = গুরুত্বপূর্ণ Environment Variables
    

## পরীক্ষার জন্য একটি গুরুত্বপূর্ণ পরামর্শ

BJIT-এর **Cloud & DevOps Trainee** পদের ৩০ মিনিটের assessment-এ Shell Scripting থেকে সাধারণত **Conceptual MCQ** আসার সম্ভাবনা বেশি, যেমন:

- Shebang (`#!/bin/bash`)
    
- `echo` ও `read`
    
- Variable
    
- `if-else`
    
- `for` loop
    
- `crontab`
    
- Exit status (`0 = success`)
    

জটিল Script লেখার প্রশ্ন আসার সম্ভাবনা তুলনামূলকভাবে কম।

---
# Lesson 10: SQL (Basic → Advanced) for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি Database, SQL, CRUD Operations, JOIN, GROUP BY, Aggregate Functions এবং Interview-এর Common SQL Questions বুঝতে পারবেন।

---

# 1. SQL কী?

**SQL = Structured Query Language**

Database-এর Data Store, Retrieve, Update এবং Delete করার Language।

Example

```text
Student Database

ID    Name      Department

1     Atiar     CSE

2     Rahim     EEE

3     Karim     CSE
```

---

# 2. Database কী?

Database হলো Data Store করার জায়গা।

Example

```text
College Database

↓

Student Table

↓

Teacher Table

↓

Course Table
```

---

# 3. DBMS

Database Management System

Examples

- MySQL
    
- PostgreSQL
    
- Oracle
    
- SQL Server
    
- SQLite
    

Cloud & DevOps-এ সবচেয়ে বেশি ব্যবহৃত

- MySQL
    
- PostgreSQL
    

---

# 4. Table

Database-এর ভিতরে Table থাকে।

Example

Student Table

|ID|Name|Age|
|---|---|---|
|1|Atiar|24|
|2|Rahim|22|

---

# 5. Row & Column

```text
Column

ID Name Age

↓

Row

1 Atiar 24
```

Column = Field

Row = Record

---

# 6. Primary Key

Unique Value

Example

```text
ID

1

2

3
```

Primary Key

- Unique
    
- Cannot be NULL
    

---

# 7. Foreign Key

এক Table-এর Primary Key অন্য Table-এ Reference হিসেবে ব্যবহার করা হয়।

Example

Student

```text
StudentID
```

Course

```text
StudentID
```

Relation তৈরি হয়।

---

# 8. CRUD

সবচেয়ে গুরুত্বপূর্ণ Concept

|Operation|SQL|
|---|---|
|Create|INSERT|
|Read|SELECT|
|Update|UPDATE|
|Delete|DELETE|

---

# 9. SELECT

সব Data

```sql
SELECT * FROM students;
```

Specific Column

```sql
SELECT name, age FROM students;
```

---

# 10. WHERE

Filter করার জন্য।

```sql
SELECT * FROM students
WHERE age > 20;
```

---

# 11. INSERT

নতুন Data যোগ করা।

```sql
INSERT INTO students
VALUES (1,'Atiar',24);
```

---

# 12. UPDATE

Data পরিবর্তন করা।

```sql
UPDATE students

SET age=25

WHERE id=1;
```

---

# 13. DELETE

Data Remove করা।

```sql
DELETE FROM students

WHERE id=1;
```

---

# 14. ORDER BY

Sort

Ascending

```sql
SELECT *

FROM students

ORDER BY age ASC;
```

Descending

```sql
ORDER BY age DESC;
```

---

# 15. LIMIT

Top Records

```sql
SELECT *

FROM students

LIMIT 5;
```

---

# 16. Aggregate Functions

COUNT

```sql
SELECT COUNT(*)

FROM students;
```

SUM

```sql
SELECT SUM(salary)

FROM employee;
```

AVG

```sql
SELECT AVG(age)

FROM students;
```

MAX

```sql
SELECT MAX(age)

FROM students;
```

MIN

```sql
SELECT MIN(age)

FROM students;
```

---

# 17. GROUP BY

Department অনুযায়ী Group

```sql
SELECT department,

COUNT(*)

FROM students

GROUP BY department;
```

---

# 18. HAVING

GROUP-এর উপর Condition।

```sql
SELECT department,

COUNT(*)

FROM students

GROUP BY department

HAVING COUNT(*)>2;
```

---

# 19. LIKE

Search

Starts With

```sql
SELECT *

FROM students

WHERE name LIKE 'A%';
```

Ends With

```sql
LIKE '%r'
```

Contains

```sql
LIKE '%ti%'
```

---

# 20. IN

```sql
SELECT *

FROM students

WHERE department IN

('CSE','EEE');
```

---

# 21. BETWEEN

```sql
SELECT *

FROM students

WHERE age

BETWEEN 20 AND 30;
```

---

# 22. JOIN

Interview-এর Favorite

---

## INNER JOIN

Common Records

```sql
SELECT *

FROM student

INNER JOIN course

ON student.id=course.sid;
```

---

## LEFT JOIN

Left Table-এর সব Record।

---

## RIGHT JOIN

Right Table-এর সব Record।

---

## FULL JOIN

সব Record।

---

### JOIN সহজে মনে রাখুন

|JOIN|Result|
|---|---|
|INNER|Common Data|
|LEFT|Left-এর সব|
|RIGHT|Right-এর সব|
|FULL|দুই Table-এর সব|

---

# 23. DISTINCT

Duplicate Remove

```sql
SELECT DISTINCT department

FROM students;
```

---

# 24. CREATE TABLE

```sql
CREATE TABLE student(

id INT,

name VARCHAR(50),

age INT

);
```

---

# 25. DROP TABLE

Delete Table

```sql
DROP TABLE student;
```

---

# 26. ALTER TABLE

New Column

```sql
ALTER TABLE student

ADD email VARCHAR(50);
```

---

# 27. TRUNCATE

Delete সব Row

Table থাকবে।

```sql
TRUNCATE TABLE student;
```

---

# 28. DELETE vs TRUNCATE vs DROP

|DELETE|TRUNCATE|DROP|
|---|---|---|
|Delete Rows|Delete All Rows|Delete Table|
|WHERE ব্যবহার করা যায়|WHERE নেই|Table Remove|

---

# 29. Index

Fast Search

Example

Book-এর Index-এর মতো।

---

# 30. SQL in DevOps

Application

↓

Database

↓

SQL Query

↓

Result

Cloud-এ

- Amazon RDS
    
- Aurora
    
- PostgreSQL
    
- MySQL
    

---

# Interview Questions

### SQL কী?

Database Query Language।

---

### Primary Key কী?

Unique Identifier।

---

### Foreign Key কী?

Relationship।

---

### CRUD কী?

Create

Read

Update

Delete

---

### SELECT কী?

Read Data।

---

### WHERE কী?

Filter।

---

### ORDER BY কী?

Sort।

---

### GROUP BY কী?

Grouping।

---

### HAVING কী?

Group Filter।

---

### JOIN কী?

Multiple Table Connect।

---

### COUNT() কী?

Total Row Count।

---

# Common SQL Queries

সব Data

```sql
SELECT * FROM students;
```

Specific Column

```sql
SELECT name FROM students;
```

Condition

```sql
SELECT * FROM students

WHERE age>20;
```

Insert

```sql
INSERT INTO students

VALUES(1,'Atiar',24);
```

Update

```sql
UPDATE students

SET age=25

WHERE id=1;
```

Delete

```sql
DELETE FROM students

WHERE id=1;
```

---

# MCQ Practice

### 1. SQL-এর Full Form?

A) Structured Query Language ✅

B) Simple Query Language

C) Standard Question Language

D) System Query Language

---

### 2. Data Read করার Command?

A) INSERT

B) UPDATE

C) SELECT ✅

D) DELETE

---

### 3. Duplicate Remove?

A) GROUP

B) DISTINCT ✅

C) LIMIT

D) ORDER

---

### 4. JOIN কী?

A) Table Delete

B) Multiple Table Connect ✅

C) Sort

D) Filter

---

### 5. COUNT() কী করে?

A) Average

B) Count Rows ✅

C) Maximum

D) Minimum

---

### 6. Primary Key কেমন?

A) Duplicate হতে পারে

B) NULL হতে পারে

C) Unique ✅

D) Text Only

---

# BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ SQL Topics

- SQL কী?
    
- Database
    
- Table
    
- Row vs Column
    
- Primary Key
    
- Foreign Key
    
- CRUD
    
- SELECT
    
- WHERE
    
- INSERT
    
- UPDATE
    
- DELETE
    
- ORDER BY
    
- GROUP BY
    
- HAVING
    
- COUNT
    
- JOIN (INNER, LEFT)
    
- DISTINCT
    
- LIMIT
    

---

# 🔥 Quick Revision (১ মিনিটে)

- **SQL =** Structured Query Language
    
- **SELECT =** Data পড়া
    
- **INSERT =** নতুন Data যোগ
    
- **UPDATE =** Data পরিবর্তন
    
- **DELETE =** Data মুছে ফেলা
    
- **WHERE =** Filter
    
- **ORDER BY =** Sort
    
- **GROUP BY =** Group করা
    
- **COUNT() =** Row গণনা
    
- **PRIMARY KEY =** Unique ID
    
- **FOREIGN KEY =** দুই Table-এর সম্পর্ক
    
- **INNER JOIN =** Common Records
    
- **LEFT JOIN =** Left Table-এর সব Record
    
- **DISTINCT =** Duplicate বাদ দেয়
    

## 🎯 BJIT Trainee Assessment Tip

Cloud & DevOps Trainee assessment-এ SQL থেকে সাধারণত **Basic MCQ** আসে। বিশেষ করে:

- `SELECT`
    
- `WHERE`
    
- `INSERT`
    
- `UPDATE`
    
- `DELETE`
    
- `JOIN`
    
- `PRIMARY KEY`
    
- `GROUP BY`
    
- `COUNT()`
    

জটিল Query লেখার চেয়ে **Concept ও Query-এর Output বোঝা** বেশি গুরুত্বপূর্ণ।

---

# Lesson 11: Operating System (OS) Basic → Advanced for Cloud & DevOps

> **Goal:** এই Lesson শেষে আপনি Operating System-এর সবচেয়ে গুরুত্বপূর্ণ Concepts বুঝতে পারবেন। BJIT Cloud & DevOps Trainee assessment-এ এগুলো থেকে MCQ আসতে পারে।

---

# 1. Operating System (OS) কী?

Operating System হলো এমন একটি Software যা **User** এবং **Hardware**-এর মধ্যে Interface হিসেবে কাজ করে।

### Example

```text
User

↓

Operating System

↓

CPU
RAM
Disk
Keyboard
```

Examples

- Linux ✅
    
- Windows
    
- macOS
    
- Ubuntu
    
- CentOS
    

---

# 2. OS-এর কাজ

- Process Management
    
- Memory Management
    
- File Management
    
- Device Management
    
- Security
    
- User Management
    

---

# 3. Kernel

Kernel হলো Operating System-এর Core Part।

এটি সরাসরি Hardware-এর সাথে যোগাযোগ করে।

```text
User

↓

Shell

↓

Kernel

↓

Hardware
```

---

# 4. Shell

Shell User-এর Command নিয়ে Kernel-এ পাঠায়।

Example

```bash
ls
```

↓

Shell

↓

Kernel

↓

Output

---

# 5. Process

Process = Running Program

Example

```text
Chrome

VS Code

Firefox
```

সবই Process।

---

# 6. Program vs Process

|Program|Process|
|---|---|
|Stored File|Running Program|
|Static|Dynamic|

Example

```text
chrome.exe

↓

Run

↓

Process
```

---

# 7. Thread

Thread হলো Process-এর ছোট অংশ।

Example

Chrome Browser

```text
Chrome

↓

Tab 1

↓

Tab 2

↓

Tab 3
```

প্রতিটি Tab একটি Thread হতে পারে।

---

# 8. Process vs Thread

|Process|Thread|
|---|---|
|Independent|Process-এর অংশ|
|More Memory|Less Memory|
|Slow|Faster|

---

# 9. CPU Scheduling

OS সিদ্ধান্ত নেয় কোন Process আগে চলবে।

Types

- FCFS
    
- SJF
    
- Priority
    
- Round Robin
    

---

## FCFS

First Come First Serve

যে আগে আসে

সে আগে Execute হয়।

---

## Round Robin

সব Process নির্দিষ্ট Time Slice পায়।

Linux-এ এর ধারণা ব্যবহৃত হয়।

---

# 10. Context Switch

CPU

Process A

↓

Process B

↓

Process C

Switch করার Process-কে Context Switching বলে।

---

# 11. Deadlock

সবচেয়ে Common Interview Question।

Example

Person A

↓

Printer চাইছে

Person B

↓

Scanner চাইছে

দুজনই অপেক্ষা করছে।

কেউ এগোতে পারছে না।

এটাই Deadlock।

---

## Deadlock-এর 4 Conditions

- Mutual Exclusion
    
- Hold and Wait
    
- No Preemption
    
- Circular Wait
    

---

# 12. Memory

Memory Types

```text
CPU Register

↓

Cache

↓

RAM

↓

Disk
```

Speed

Register > Cache > RAM > SSD/HDD

---

# 13. RAM

Temporary Memory।

Power Off

↓

Data Lost।

---

# 14. ROM

Permanent Memory।

Power Off

↓

Data থাকে।

---

# 15. Virtual Memory

RAM কম হলে

Disk-এর কিছু অংশ RAM হিসেবে ব্যবহার করা হয়।

Benefits

- More Programs
    
- Large Applications
    

---

# 16. Paging

Memory-কে ছোট Block-এ ভাগ করা।

---

# 17. Swapping

RAM

↓

Disk

↓

RAM

Memory Management Technique।

---

# 18. File System

Linux

- ext4
    
- xfs
    

Windows

- NTFS
    
- FAT32
    

---

# 19. Boot Process

Computer ON

↓

BIOS/UEFI

↓

Bootloader

↓

Kernel

↓

Operating System

↓

Login

---

# 20. User Types

Linux

Root User

↓

Normal User

Root-এর সব Permission থাকে।

---

# 21. File Permission

```text
r = Read

w = Write

x = Execute
```

Example

```text
rwxr-xr--
```

---

# 22. chmod

Permission Change

```bash
chmod 755 file.sh
```

Meaning

Owner

↓

Read Write Execute

Group

↓

Read Execute

Others

↓

Read Execute

---

# 23. chmod Numbers

|Number|Permission|
|---|---|
|7|rwx|
|6|rw-|
|5|r-x|
|4|r--|
|0|---|

---

# 24. Disk Management

Check Disk

```bash
df -h
```

Check Folder Size

```bash
du -sh
```

---

# 25. Memory Check

```bash
free -m
```

---

# 26. Running Processes

```bash
ps
```

Live

```bash
top
```

---

# 27. Kill Process

```bash
kill PID
```

Force

```bash
kill -9 PID
```

---

# 28. Background Process

```bash
command &
```

Example

```bash
sleep 100 &
```

---

# 29. Foreground Process

```bash
fg
```

---

# 30. Zombie Process

Process শেষ হয়েছে

কিন্তু Entry এখনও Process Table-এ আছে।

---

# 31. Orphan Process

Parent Process শেষ

Child Process এখনও চলছে।

---

# 32. Linux Boot Levels (Runlevels)

পুরনো ধারণা

Modern Linux

Systemd Target ব্যবহার করে।

---

# 33. Systemctl

Start Service

```bash
sudo systemctl start nginx
```

Stop

```bash
sudo systemctl stop nginx
```

Status

```bash
systemctl status nginx
```

---

# 34. Interview Questions

### OS কী?

Hardware ও User-এর মধ্যে Interface।

---

### Kernel কী?

OS-এর Core।

---

### Shell কী?

Command Interpreter।

---

### Process কী?

Running Program।

---

### Thread কী?

Smallest Execution Unit।

---

### Process vs Thread?

Process

Heavy

Thread

Lightweight

---

### Deadlock কী?

Two or More Processes Wait Forever।

---

### Virtual Memory কী?

Disk as RAM।

---

### chmod 755 মানে?

Owner

rwx

Group

r-x

Others

r-x

---

### kill -9 কী?

Force Kill।

---

# Important Linux Commands

```bash
ps

top

kill

kill -9

free -m

df -h

du -sh

chmod

systemctl

whoami

uptime
```

---

# MCQ Practice

### 1. Kernel কী?

A) Browser

B) OS-এর Core ✅

C) Database

D) Compiler

---

### 2. Running Program-কে কী বলে?

A) Thread

B) Process ✅

C) Program

D) Script

---

### 3. Virtual Memory কোথায় থাকে?

A) CPU

B) Disk ✅

C) Cache

D) Register

---

### 4. chmod 755 কী পরিবর্তন করে?

A) Memory

B) Permission ✅

C) Process

D) User

---

### 5. কোন Command Running Process দেখায়?

A) mkdir

B) ps ✅

C) rm

D) ls

---

### 6. কোন Command Disk Usage দেখায়?

A) free -m

B) df -h ✅

C) pwd

D) whoami

---

### 7. কোন Command Memory দেখায়?

A) ps

B) free -m ✅

C) du

D) top

---

### 8. Deadlock কী?

A) Memory Error

B) Process waits forever ✅

C) Network Error

D) File Error

---

# BJIT Assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ OS Topics

- Operating System
    
- Kernel
    
- Shell
    
- Process
    
- Thread
    
- Process vs Thread
    
- CPU Scheduling
    
- Deadlock
    
- Virtual Memory
    
- RAM vs ROM
    
- File Permission (`rwx`)
    
- `chmod`
    
- `ps`
    
- `top`
    
- `kill`
    
- `df -h`
    
- `free -m`
    
- `systemctl`
    

---

# 🔥 Quick Revision (১ মিনিটে)

- **OS =** User ও Hardware-এর মধ্যে Interface
    
- **Kernel =** OS-এর Core
    
- **Shell =** Command Interpreter
    
- **Process =** Running Program
    
- **Thread =** Process-এর ছোট অংশ
    
- **RAM =** Temporary Memory
    
- **Virtual Memory =** Disk-এর অংশ RAM হিসেবে ব্যবহার
    
- **Deadlock =** Process একে অপরের জন্য অপেক্ষা করে আটকে যায়
    
- **`chmod 755` =** Permission Change
    
- **`ps` =** Running Process
    
- **`top` =** Live Process Monitoring
    
- **`kill -9` =** Force Kill
    
- **`df -h` =** Disk Usage
    
- **`free -m` =** Memory Usage
    

---

## 🎯 BJIT Cloud & DevOps Trainee-এর জন্য সবচেয়ে গুরুত্বপূর্ণ Lessons (Priority)

1. ✅ Linux
    
2. ✅ Networking
    
3. ✅ Git
    
4. ✅ Cloud Computing
    
5. ✅ AWS
    
6. ✅ Docker
    
7. ✅ Kubernetes
    
8. ✅ CI/CD & Jenkins
    
9. ✅ Shell Scripting
    
10. ✅ SQL
    
11. ✅ Operating System
    

**এখন আপনার পড়ার অংশ প্রায় সম্পূর্ণ।** এরপর পরীক্ষার জন্য সবচেয়ে কার্যকর হবে **১০০–২০০টি সম্ভাব্য MCQ** প্র্যাকটিস করা, কারণ ৩০ মিনিটের অনলাইন assessment-এ সাধারণত দ্রুত উত্তর দেওয়ার মতো MCQ-ই বেশি থাকে।

---
# Lesson 12: Aptitude & English (BJIT Cloud & DevOps Trainee)

> **Goal:** এই Lesson শেষে আপনি Aptitude, Logical Reasoning এবং English-এর সবচেয়ে Common প্রশ্নগুলো সমাধান করতে পারবেন।

---

# Part A: Aptitude

## 1. Percentage

### Formula

[  
\text{Percentage}=\frac{\text{Part}}{\text{Total}}\times100  
]

### Example

80-এর 25% কত?

```
25/100 × 80 = 20
```

✅ উত্তর = **20**

---

## 2. Profit & Loss

### Formula

Profit

```
Selling Price > Cost Price
```

Profit %

```
Profit/Cost Price ×100
```

### Example

CP = 100

SP = 120

Profit = 20

Profit %

```
20%
```

---

## 3. Ratio

Example

Boys : Girls

```
2 : 3
```

Total = 25

Boy কত?

```
2+3=5

25÷5=5

2×5=10
```

Answer = **10**

---

## 4. Average

Formula

```
Sum ÷ Number
```

Example

```
10 20 30
```

Average

```
60÷3

20
```

---

## 5. Time & Work

Formula

```
1/A +1/B
```

Example

A = 10 Days

B = 15 Days

```
1/10+1/15

=5/30

=1/6
```

Answer

```
6 Days
```

---

## 6. Speed

Formula

```
Distance = Speed × Time
```

Example

```
60 km/h

2 Hour
```

Distance

```
120 km
```

---

## 7. Probability

Formula

```
Favourable

÷

Total
```

Example

Dice

Probability of 4

```
1/6
```

---

## 8. Number Series

Example

```
2

4

8

16

?
```

Answer

```
32
```

---

## 9. Odd One Out

```
Apple

Banana

Mango

Car
```

Answer

```
Car
```

---

## 10. Blood Relation

Example

Father's Brother

=

Uncle

---

# Part B: Logical Reasoning

## Analogy

```
Cat : Kitten

Dog : ?
```

Answer

```
Puppy
```

---

## Coding

Example

```
CAT

DBU
```

Meaning

Each Letter +1

---

## Direction

North

South

East

West

Basic প্রশ্ন আসে।

---

## Calendar

Example

Leap Year

```
366 Days
```

---

## Clock

Hour Hand

Minute Hand

Angle প্রশ্ন।

---

# Part C: English

## 1. Synonym

Happy

=

Joyful

---

Big

=

Large

---

## 2. Antonym

Hot

=

Cold

---

Fast

=

Slow

---

## 3. Fill in the Blank

I ____ a student.

A)

is

B)

am ✅

C)

are

D)

be

---

## 4. Articles

```
A

An

The
```

Example

```
An Apple

A Book
```

---

## 5. Preposition

```
At

On

In
```

Example

```
At 5 PM

On Monday

In January
```

---

## 6. Tense

Present

Past

Future

Example

```
I go.

I went.

I will go.
```

---

## 7. Voice

Active

```
He writes a letter.
```

Passive

```
A letter is written by him.
```

---

## 8. Error Detection

Wrong

```
She don't know.
```

Correct

```
She doesn't know.
```

---

## 9. Vocabulary

Important Words

- Deploy
    
- Server
    
- Network
    
- Secure
    
- Maintain
    
- Configure
    
- Upgrade
    
- Install
    
- Monitor
    
- Access
    

---

## 10. Reading Comprehension

একটি ছোট Passage

↓

MCQ

---

# HR Questions (কখনও কখনও আসে)

### Tell me about yourself.

**Sample Answer:**

> "My name is Md Atiar Rahman. I recently completed my Bachelor's degree in Computer Science and Engineering. I have a strong interest in Cloud Computing, Linux, AWS, Docker, and DevOps. I enjoy learning new technologies and solving technical problems. I am eager to start my career as a Cloud & DevOps Engineer and contribute to BJIT."

---

### Why BJIT?

> "BJIT is a well-known software company with strong training and career development opportunities. I believe the trainee program will help me build practical skills in Cloud and DevOps."

---

### Strength

- Quick Learner
    
- Team Player
    
- Problem Solver
    

---

### Weakness

> "I sometimes spend extra time making sure my work is accurate, but I'm learning to balance quality with efficiency."

---

# 20 Most Common MCQs

### 1. Linux command to list files?

A) pwd

B) ls ✅

C) cd

D) mkdir

---

### 2. Git command to upload code?

A) commit

B) push ✅

C) pull

D) clone

---

### 3. AWS VM Service?

A) S3

B) EC2 ✅

C) IAM

D) VPC

---

### 4. Docker Template?

A) Container

B) Image ✅

C) Volume

D) Pod

---

### 5. Kubernetes Smallest Unit?

A) Node

B) Pod ✅

C) Cluster

D) Deployment

---

### 6. CI Full Form?

A) Continuous Integration ✅

---

### 7. HTTP Port?

A) 22

B) 80 ✅

C) 443

D) 21

---

### 8. HTTPS Port?

A) 80

B) 443 ✅

---

### 9. SSH Port?

A) 22 ✅

---

### 10. SQL Read Command?

A) INSERT

B) SELECT ✅

---

### 11. Primary Key?

A) Duplicate

B) Unique ✅

---

### 12. Shell Script starts with?

A)

```bash
#!/bin/bash
```

✅

---

### 13. Linux Permission 755?

Owner

```
rwx
```

---

### 14. Running Program?

Process ✅

---

### 15. RAM is?

Temporary Memory ✅

---

### 16. EC2 is?

Virtual Machine ✅

---

### 17. Docker Registry?

Docker Hub ✅

---

### 18. Jenkins is?

CI/CD Tool ✅

---

### 19. GitHub is?

Code Repository ✅

---

### 20. Cloud Computing means?

Using computing resources over the Internet. ✅

---

# 🎯 BJIT Cloud & DevOps Assessment-এর শেষ মুহূর্তের Revision

## Linux

- `ls`, `pwd`, `cd`, `mkdir`, `rm`, `chmod`
    

## Networking

- IP
    
- DNS
    
- HTTP (80)
    
- HTTPS (443)
    
- SSH (22)
    
- TCP vs UDP
    

## Git

- `git add`
    
- `git commit`
    
- `git push`
    
- `git pull`
    

## AWS

- EC2
    
- S3
    
- IAM
    
- VPC
    
- Security Group
    

## Docker

- Image
    
- Container
    
- Dockerfile
    
- Docker Hub
    

## Kubernetes

- Pod
    
- Node
    
- Cluster
    
- Deployment
    
- Service
    

## Jenkins

- CI
    
- CD
    
- Pipeline
    

## SQL

- SELECT
    
- INSERT
    
- UPDATE
    
- DELETE
    
- JOIN
    

## Shell

- `echo`
    
- `read`
    
- `if`
    
- `for`
    
- `chmod`
    

## Operating System

- Process
    
- Thread
    
- Kernel
    
- Deadlock
    
- Virtual Memory
    

---

## 🚀 পরীক্ষার আগে কিছু টিপস

- প্রশ্ন ভালো করে পড়ে তারপর উত্তর দিন।
    
- সহজ প্রশ্ন আগে করুন, কঠিনগুলো পরে।
    
- সময়ের দিকে খেয়াল রাখুন—৩০ মিনিটে প্রতি প্রশ্নে গড়ে ৩০–৪৫ সেকেন্ডের বেশি না।
    
- যদি Webcam Monitoring থাকে, তাহলে অন্য ট্যাব বা অন্য ডিভাইসে উত্তর খোঁজার চেষ্টা করবেন না।
    
- পরীক্ষার ১০–১৫ মিনিট আগে লগইন করে Webcam, Microphone এবং Internet Connection ঠিক আছে কিনা দেখে নিন।
    

এই ১২টি Lesson শেষ করলে **BJIT Trainee – Cloud & DevOps** assessment-এর জন্য একটি শক্ত ভিত্তি তৈরি হবে। শুভকামনা!

---

অবশ্যই। **BJIT Trainee - Cloud & DevOps** পরীক্ষার জন্য আমি **২০০টি Most Expected MCQ** দিতে পারি। তবে একবারে ২০০টি দিলে উত্তর খুব বড় হয়ে যাবে এবং ChatGPT-এর সীমা অতিক্রম করবে।

আমি এগুলো নিচের ভাগে দেব:

- ✅ Part 1: MCQ 1–50 (Linux + Networking)
    
- ✅ Part 2: MCQ 51–100 (Git + Cloud + AWS)
    
- ✅ Part 3: MCQ 101–150 (Docker + Kubernetes + Jenkins)
    
- ✅ Part 4: MCQ 151–200 (Shell + SQL + OS + Aptitude + English)
    

প্রতিটি প্রশ্নে থাকবে:

- ✔️ ৪টি অপশন
    
- ✔️ সঠিক উত্তর
    
- ✔️ সংক্ষিপ্ত ব্যাখ্যা
    

এভাবে পড়লে পরীক্ষার জন্য অনেক বেশি কার্যকর হবে।

## Sample (প্রথম ১০টি)

### 1. Which command shows the current working directory?

A. ls  
B. pwd ✅  
C. cd  
D. mkdir

**Answer:** B (`pwd`)

---

### 2. Which command lists files in Linux?

A. dir  
B. ls ✅  
C. pwd  
D. rm

**Answer:** B

---

### 3. Which command changes the current directory?

A. pwd  
B. ls  
C. cd ✅  
D. mv

**Answer:** C

---

### 4. Which Linux command removes a file?

A. cp  
B. rm ✅  
C. mv  
D. cat

**Answer:** B

---

### 5. SSH uses which default port?

A. 21  
B. 22 ✅  
C. 80  
D. 443

**Answer:** B

---

### 6. HTTP uses which port?

A. 21  
B. 22  
C. 80 ✅  
D. 443

**Answer:** C

---

### 7. HTTPS uses which port?

A. 22  
B. 25  
C. 80  
D. 443 ✅

**Answer:** D

---

### 8. DNS stands for?

A. Domain Name System ✅  
B. Data Network Service  
C. Dynamic Node Server  
D. Domain Network Security

**Answer:** A

---

### 9. Which protocol is connection-oriented?

A. UDP  
B. TCP ✅  
C. ICMP  
D. ARP

**Answer:** B

---

### 10. Which protocol is faster but less reliable?

A. TCP  
B. UDP ✅  
C. HTTP  
D. SSH

**Answer:** B

---

# আমার পরামর্শ

আমি এগুলো শুধু চ্যাটে না দিয়ে **একটি সুন্দর PDF** আকারে তৈরি করতে পারি:

- 📘 **200 BJIT Cloud & DevOps MCQs**
    
- ✅ উত্তরসহ
    
- ✅ ব্যাখ্যাসহ
    
- ✅ Interview Tips
    
- ✅ Last-Minute Revision Notes
    

এটি প্রায় **৩০–৪০ পৃষ্ঠার PDF** হবে, যা পরীক্ষার আগে একবার পড়লেই দ্রুত রিভিশন করা যাবে।


---
দারুণ। আমরা **BJIT Trainee - Cloud & DevOps 200 Most Expected MCQ** শুরু করছি।

# Part 1 (MCQ 1–50): Linux + Networking

---

## Linux (1–25)

### 1. Linux is a:

A. Programming Language  
B. Operating System ✅  
C. Database  
D. Browser

**Answer:** B

---

### 2. Which command shows the current directory?

A. ls  
B. pwd ✅  
C. cd  
D. mkdir

**Answer:** B

---

### 3. Which command lists files and folders?

A. ls ✅  
B. pwd  
C. cd  
D. whoami

**Answer:** A

---

### 4. Which command changes directory?

A. cd ✅  
B. ls  
C. pwd  
D. mv

**Answer:** A

---

### 5. Which command creates a new directory?

A. touch  
B. mkdir ✅  
C. rm  
D. cp

**Answer:** B

---

### 6. Which command creates an empty file?

A. touch ✅  
B. mkdir  
C. cp  
D. cat

**Answer:** A

---

### 7. Which command deletes a file?

A. mv  
B. rm ✅  
C. cp  
D. cat

**Answer:** B

---

### 8. Which command copies files?

A. mv  
B. cp ✅  
C. rm  
D. pwd

**Answer:** B

---

### 9. Which command moves or renames files?

A. mv ✅  
B. cp  
C. ls  
D. pwd

**Answer:** A

---

### 10. Which command displays file contents?

A. cat ✅  
B. ls  
C. mkdir  
D. pwd

**Answer:** A

---

### 11. Root user ID is:

A. 1000  
B. 500  
C. 0 ✅  
D. 1

**Answer:** C

---

### 12. Which command shows the current user?

A. whoami ✅  
B. pwd  
C. ls  
D. id

**Answer:** A

---

### 13. Which command changes file permissions?

A. chmod ✅  
B. chown  
C. ls  
D. pwd

**Answer:** A

---

### 14. chmod 755 gives owner:

A. rw-  
B. r-x  
C. rwx ✅  
D. ---

**Answer:** C

---

### 15. Which command shows running processes?

A. ps ✅  
B. ls  
C. mkdir  
D. pwd

**Answer:** A

---

### 16. Which command monitors processes in real time?

A. ps  
B. top ✅  
C. ls  
D. cat

**Answer:** B

---

### 17. Which command forcefully kills a process?

A. stop  
B. kill -9 ✅  
C. exit  
D. remove

**Answer:** B

---

### 18. Which command shows memory usage?

A. df -h  
B. free -m ✅  
C. ls  
D. ps

**Answer:** B

---

### 19. Which command shows disk usage?

A. free -m  
B. df -h ✅  
C. top  
D. ps

**Answer:** B

---

### 20. Which command prints the current date?

A. date ✅  
B. time  
C. cal  
D. today

**Answer:** A

---

### 21. Which file stores environment variables?

A. ~/.bashrc ✅  
B. passwd  
C. shadow  
D. hosts

**Answer:** A

---

### 22. Which shell is most common in Linux?

A. CMD  
B. Bash ✅  
C. PowerShell  
D. Perl

**Answer:** B

---

### 23. Which command downloads a file from the internet?

A. wget ✅  
B. pwd  
C. chmod  
D. ps

**Answer:** A

---

### 24. Which command finds a file?

A. locate  
B. find ✅  
C. ls  
D. pwd

**Answer:** B

---

### 25. Which command shows Linux version?

A. uname -a ✅  
B. pwd  
C. ps  
D. cd

**Answer:** A

---

# Networking (26–50)

### 26. IP stands for:

A. Internet Protocol ✅  
B. Internal Process  
C. Internet Process  
D. Internal Protocol

**Answer:** A

---

### 27. DNS stands for:

A. Domain Name System ✅  
B. Data Network Service  
C. Domain Network Server  
D. Digital Name System

**Answer:** A

---

### 28. HTTP default port:

A. 21  
B. 22  
C. 80 ✅  
D. 443

**Answer:** C

---

### 29. HTTPS default port:

A. 80  
B. 22  
C. 25  
D. 443 ✅

**Answer:** D

---

### 30. SSH default port:

A. 20  
B. 21  
C. 22 ✅  
D. 23

**Answer:** C

---

### 31. FTP default port:

A. 21 ✅  
B. 22  
C. 80  
D. 110

**Answer:** A

---

### 32. SMTP is used for:

A. Receiving Email  
B. Sending Email ✅  
C. Browsing  
D. File Sharing

**Answer:** B

---

### 33. POP3 default port:

A. 25  
B. 110 ✅  
C. 143  
D. 53

**Answer:** B

---

### 34. IMAP default port:

A. 80  
B. 143 ✅  
C. 110  
D. 22

**Answer:** B

---

### 35. Which protocol is secure?

A. HTTP  
B. HTTPS ✅  
C. FTP  
D. Telnet

**Answer:** B

---

### 36. Which protocol is connection-oriented?

A. UDP  
B. TCP ✅  
C. IP  
D. ICMP

**Answer:** B

---

### 37. Which protocol is faster?

A. TCP  
B. UDP ✅  
C. HTTPS  
D. SSH

**Answer:** B

---

### 38. Which device connects different networks?

A. Switch  
B. Router ✅  
C. Hub  
D. Repeater

**Answer:** B

---

### 39. Which device works at Layer 2?

A. Router  
B. Switch ✅  
C. Gateway  
D. Firewall

**Answer:** B

---

### 40. Which command checks connectivity?

A. ping ✅  
B. mkdir  
C. rm  
D. ps

**Answer:** A

---

### 41. Which command traces network path?

A. ping  
B. traceroute ✅  
C. ls  
D. cat

**Answer:** B

---

### 42. Which command shows IP configuration (Linux)?

A. ifconfig ✅  
B. ipconfig  
C. ping  
D. netstat

**Answer:** A

---

### 43. Which command shows open ports?

A. netstat ✅  
B. pwd  
C. ls  
D. cp

**Answer:** A

---

### 44. What does LAN stand for?

A. Local Area Network ✅  
B. Large Area Network  
C. Logical Area Network  
D. Long Area Network

**Answer:** A

---

### 45. What does WAN stand for?

A. Wide Area Network ✅  
B. Wireless Area Network  
C. Web Area Network  
D. World Access Network

**Answer:** A

---

### 46. Which protocol resolves domain names?

A. DNS ✅  
B. FTP  
C. SMTP  
D. SSH

**Answer:** A

---

### 47. Which protocol transfers web pages?

A. HTTP ✅  
B. FTP  
C. SMTP  
D. SSH

**Answer:** A

---

### 48. Which IP version has 128-bit addresses?

A. IPv4  
B. IPv6 ✅  
C. IPv3  
D. IPv5

**Answer:** B

---

### 49. Which command displays hostname?

A. hostname ✅  
B. pwd  
C. whoami  
D. top

**Answer:** A

---

### 50. Which network device filters traffic?

A. Switch  
B. Firewall ✅  
C. Hub  
D. Modem

**Answer:** B

---

## ✅ Part 1 Complete (1–50)

পরবর্তী অংশ **MCQ 51–100**-এ থাকবে:

- Git & GitHub
    
- Cloud Computing
    
- AWS (EC2, S3, IAM, VPC, Security Group)
    
- DevOps Basics
    

এগুলো BJIT Cloud & DevOps Trainee পরীক্ষার সবচেয়ে গুরুত্বপূর্ণ টপিকগুলোর মধ্যে রয়েছে।

----

# BJIT Cloud & DevOps – 200 Most Expected MCQs

## Part 2 (MCQ 51–100): Git + Cloud Computing + AWS

---

# Git & GitHub (51–70)

### 51. Git is a:

A. Database  
B. Version Control System ✅  
C. Operating System  
D. Cloud Service

**Answer:** B

---

### 52. GitHub is:

A. Programming Language  
B. Cloud Storage  
C. Code Hosting Platform ✅  
D. Database

**Answer:** C

---

### 53. Which command initializes a Git repository?

A. git start  
B. git init ✅  
C. git create  
D. git new

**Answer:** B

---

### 54. Which command checks Git status?

A. git check  
B. git status ✅  
C. git info  
D. git show

**Answer:** B

---

### 55. Which command stages files?

A. git add ✅  
B. git commit  
C. git push  
D. git pull

**Answer:** A

---

### 56. Which command saves changes locally?

A. git push  
B. git commit ✅  
C. git clone  
D. git pull

**Answer:** B

---

### 57. Which command uploads code to GitHub?

A. git upload  
B. git push ✅  
C. git send  
D. git commit

**Answer:** B

---

### 58. Which command downloads the latest code?

A. git clone  
B. git pull ✅  
C. git push  
D. git fetch

**Answer:** B

---

### 59. Which command copies an existing repository?

A. git init  
B. git clone ✅  
C. git add  
D. git merge

**Answer:** B

---

### 60. A Git branch is used for:

A. Backup  
B. Parallel Development ✅  
C. Database  
D. Deployment

**Answer:** B

---

### 61. Which command creates a new branch?

A. git branch feature ✅  
B. git add branch  
C. git checkout main  
D. git clone

**Answer:** A

---

### 62. Which command switches branches?

A. git switch ✅  
B. git merge  
C. git push  
D. git status

**Answer:** A

---

### 63. Which command merges branches?

A. git merge ✅  
B. git clone  
C. git pull  
D. git add

**Answer:** A

---

### 64. HEAD in Git points to:

A. First Commit  
B. Current Commit ✅  
C. Last Branch  
D. Remote Repository

**Answer:** B

---

### 65. Git stores project history in:

A. .git folder ✅  
B. bin folder  
C. src folder  
D. temp folder

**Answer:** A

---

### 66. Which command shows commit history?

A. git log ✅  
B. git history  
C. git show  
D. git list

**Answer:** A

---

### 67. Which command removes staged changes?

A. git restore --staged ✅  
B. git remove  
C. git delete  
D. git clean

**Answer:** A

---

### 68. Git was created by:

A. Bill Gates  
B. Linus Torvalds ✅  
C. Elon Musk  
D. James Gosling

**Answer:** B

---

### 69. GitHub is mainly used for:

A. Version Control Collaboration ✅  
B. Email  
C. Networking  
D. Database

**Answer:** A

---

### 70. Which command checks remote repositories?

A. git remote -v ✅  
B. git status  
C. git info  
D. git clone

**Answer:** A

---

# Cloud Computing (71–80)

### 71. Cloud Computing means:

A. Using Internet-based Computing Resources ✅  
B. Programming  
C. Networking  
D. Database

**Answer:** A

---

### 72. Which is NOT a Cloud Provider?

A. AWS  
B. Azure  
C. Google Cloud  
D. Microsoft Word ✅

**Answer:** D

---

### 73. IaaS stands for:

A. Infrastructure as a Service ✅  
B. Internet as a Service  
C. Integration as a Service  
D. Internal as a Service

**Answer:** A

---

### 74. PaaS stands for:

A. Platform as a Service ✅  
B. Program as a Service  
C. Public as a Service  
D. Process as a Service

**Answer:** A

---

### 75. SaaS stands for:

A. Software as a Service ✅  
B. Storage as a Service  
C. Server as a Service  
D. Security as a Service

**Answer:** A

---

### 76. Which is an example of SaaS?

A. Gmail ✅  
B. EC2  
C. Docker  
D. Linux

**Answer:** A

---

### 77. Which deployment model is accessible to everyone?

A. Private Cloud  
B. Public Cloud ✅  
C. Hybrid Cloud  
D. Community Cloud

**Answer:** B

---

### 78. Hybrid Cloud combines:

A. Public + Private Cloud ✅  
B. Linux + Windows  
C. AWS + Azure  
D. Git + Docker

**Answer:** A

---

### 79. Main benefit of Cloud Computing:

A. Scalability ✅  
B. Slow Performance  
C. High Maintenance  
D. Manual Deployment

**Answer:** A

---

### 80. Which service provides virtual servers?

A. IaaS ✅  
B. SaaS  
C. PaaS  
D. DNS

**Answer:** A

---

# AWS (81–100)

### 81. AWS stands for:

A. Amazon Web Services ✅  
B. Advanced Web System  
C. Automated Web Server  
D. Amazon World Service

**Answer:** A

---

### 82. EC2 is:

A. Storage  
B. Virtual Machine ✅  
C. Database  
D. Firewall

**Answer:** B

---

### 83. S3 is used for:

A. Object Storage ✅  
B. Compute  
C. Networking  
D. Database

**Answer:** A

---

### 84. IAM stands for:

A. Identity and Access Management ✅  
B. Internet Access Management  
C. Internal Account Manager  
D. Identity Application Manager

**Answer:** A

---

### 85. VPC stands for:

A. Virtual Private Cloud ✅  
B. Virtual Public Cloud  
C. Virtual Process Center  
D. Variable Private Connection

**Answer:** A

---

### 86. Security Group acts as:

A. Database  
B. Virtual Firewall ✅  
C. Router  
D. Switch

**Answer:** B

---

### 87. Which AWS service stores objects?

A. EC2  
B. S3 ✅  
C. IAM  
D. Lambda

**Answer:** B

---

### 88. Which AWS service runs serverless code?

A. EC2  
B. Lambda ✅  
C. S3  
D. RDS

**Answer:** B

---

### 89. Amazon RDS is used for:

A. Managed Database ✅  
B. Email  
C. Networking  
D. Monitoring

**Answer:** A

---

### 90. Which service monitors AWS resources?

A. CloudWatch ✅  
B. S3  
C. IAM  
D. EC2

**Answer:** A

---

### 91. Which service provides DNS?

A. Route 53 ✅  
B. EC2  
C. S3  
D. IAM

**Answer:** A

---

### 92. Which AWS service is used for Content Delivery?

A. CloudFront ✅  
B. Route 53  
C. S3  
D. IAM

**Answer:** A

---

### 93. Which service provides Auto Scaling?

A. Auto Scaling Group ✅  
B. IAM  
C. S3  
D. Lambda

**Answer:** A

---

### 94. Which service stores secrets securely?

A. Secrets Manager ✅  
B. EC2  
C. Route 53  
D. CloudFront

**Answer:** A

---

### 95. Which AWS service manages containers?

A. ECS/EKS ✅  
B. IAM  
C. S3  
D. Route 53

**Answer:** A

---

### 96. Which AWS service is Kubernetes?

A. ECS  
B. EKS ✅  
C. S3  
D. Lambda

**Answer:** B

---

### 97. Which AWS service provides NoSQL database?

A. RDS  
B. DynamoDB ✅  
C. S3  
D. EC2

**Answer:** B

---

### 98. Which service manages permissions?

A. IAM ✅  
B. S3  
C. Lambda  
D. Route 53

**Answer:** A

---

### 99. Which AWS service is best for file backup?

A. S3 ✅  
B. EC2  
C. IAM  
D. Lambda

**Answer:** A

---

### 100. Which AWS service creates isolated cloud networks?

A. VPC ✅  
B. EC2  
C. S3  
D. CloudWatch

**Answer:** A

---

# ⭐ Most Important Questions (High Probability)

পরীক্ষার আগে এগুলো অবশ্যই দেখে নিন:

- Git vs GitHub
    
- `git add`, `git commit`, `git push`, `git pull`
    
- IaaS, PaaS, SaaS
    
- Public vs Private vs Hybrid Cloud
    
- EC2
    
- S3
    
- IAM
    
- VPC
    
- Security Group
    
- CloudWatch
    
- Route 53
    
- RDS
    
- Lambda
    
- ECS vs EKS
    

➡️ **পরবর্তী Part 3 (MCQ 101–150)**-এ থাকবে:

- Docker
    
- Kubernetes
    
- Jenkins
    
- CI/CD
    
- DevOps (সবচেয়ে গুরুত্বপূর্ণ অংশ)

----
# BJIT Cloud & DevOps – 200 Most Expected MCQs

# Part 3 (MCQ 101–150): Docker + Kubernetes + Jenkins + CI/CD

---

# Docker (101–120)

### 101. Docker is a:

A. Database  
B. Containerization Platform ✅  
C. Programming Language  
D. Operating System

**Answer:** B

---

### 102. Docker packages applications into:

A. VM  
B. Container ✅  
C. Folder  
D. ZIP File

**Answer:** B

---

### 103. Docker Image is:

A. Running Container  
B. Template for Container ✅  
C. Volume  
D. Network

**Answer:** B

---

### 104. Docker Container is:

A. Running Instance of an Image ✅  
B. Database  
C. Script  
D. Repository

**Answer:** A

---

### 105. Which command downloads an image?

A. docker run  
B. docker pull ✅  
C. docker ps  
D. docker exec

**Answer:** B

---

### 106. Which command starts a container?

A. docker run ✅  
B. docker stop  
C. docker ps  
D. docker rm

**Answer:** A

---

### 107. Which command lists running containers?

A. docker images  
B. docker ps ✅  
C. docker ls  
D. docker list

**Answer:** B

---

### 108. Which command lists Docker images?

A. docker ps  
B. docker images ✅  
C. docker run  
D. docker info

**Answer:** B

---

### 109. Dockerfile is used to:

A. Build Docker Images ✅  
B. Delete Containers  
C. Manage Networks  
D. Create Databases

**Answer:** A

---

### 110. Which command builds an image?

A. docker build ✅  
B. docker create  
C. docker image  
D. docker pull

**Answer:** A

---

### 111. Docker Hub is:

A. Database  
B. Image Repository ✅  
C. VM  
D. Cloud Provider

**Answer:** B

---

### 112. Which command stops a container?

A. docker stop ✅  
B. docker killall  
C. docker rm  
D. docker images

**Answer:** A

---

### 113. Which command removes a container?

A. docker delete  
B. docker rm ✅  
C. docker remove  
D. docker stop

**Answer:** B

---

### 114. Which command removes an image?

A. docker rmi ✅  
B. docker rm  
C. docker delete  
D. docker stop

**Answer:** A

---

### 115. Docker Volume is used for:

A. Networking  
B. Persistent Storage ✅  
C. CPU Allocation  
D. Image Building

**Answer:** B

---

### 116. Which option maps ports?

A. -v  
B. -p ✅  
C. -d  
D. -i

**Answer:** B

---

### 117. `docker run -p 8080:80 nginx` means:

A. Host 8080 → Container 80 ✅  
B. Host 80 → Container 8080  
C. Port Block  
D. Network Creation

**Answer:** A

---

### 118. Docker Compose manages:

A. Multiple Containers ✅  
B. Database  
C. Network Only  
D. VM

**Answer:** A

---

### 119. Default Docker network is:

A. Host  
B. Bridge ✅  
C. None  
D. Overlay

**Answer:** B

---

### 120. Docker is lighter than:

A. Browser  
B. Virtual Machine ✅  
C. Database  
D. Network

**Answer:** B

---

# Kubernetes (121–135)

### 121. Kubernetes is:

A. Database  
B. Container Orchestration Platform ✅  
C. Programming Language  
D. Web Server

**Answer:** B

---

### 122. Smallest Deployable Unit:

A. Node  
B. Pod ✅  
C. Deployment  
D. Cluster

**Answer:** B

---

### 123. A Pod contains:

A. Containers ✅  
B. Databases  
C. Routers  
D. Networks

**Answer:** A

---

### 124. Collection of Nodes is called:

A. Pod  
B. Cluster ✅  
C. Service  
D. Namespace

**Answer:** B

---

### 125. Deployment manages:

A. Nodes  
B. Pods ✅  
C. Images  
D. Networks

**Answer:** B

---

### 126. ReplicaSet ensures:

A. Desired Number of Pods ✅  
B. Database Backup  
C. Networking  
D. Security

**Answer:** A

---

### 127. Service provides:

A. Stable Network Access ✅  
B. Storage  
C. Images  
D. CPU

**Answer:** A

---

### 128. ConfigMap stores:

A. Passwords  
B. Configuration Data ✅  
C. Images  
D. Secrets

**Answer:** B

---

### 129. Secret stores:

A. Logs  
B. Passwords/API Keys ✅  
C. Images  
D. Pods

**Answer:** B

---

### 130. Kubernetes CLI is:

A. docker  
B. kubectl ✅  
C. aws  
D. git

**Answer:** B

---

### 131. Which command lists pods?

A. kubectl get pods ✅  
B. docker ps  
C. git log  
D. aws ec2

**Answer:** A

---

### 132. Amazon Kubernetes service:

A. ECS  
B. EKS ✅  
C. EC2  
D. S3

**Answer:** B

---

### 133. Namespace is used for:

A. Organizing Resources ✅  
B. Building Images  
C. Monitoring  
D. Networking

**Answer:** A

---

### 134. Ingress is used for:

A. HTTP Routing ✅  
B. Storage  
C. Database  
D. CPU

**Answer:** A

---

### 135. Persistent Volume (PV) is used for:

A. Permanent Storage ✅  
B. Networking  
C. Monitoring  
D. Security

**Answer:** A

---

# Jenkins & CI/CD (136–150)

### 136. Jenkins is:

A. Database  
B. CI/CD Tool ✅  
C. Web Server  
D. Operating System

**Answer:** B

---

### 137. CI stands for:

A. Continuous Integration ✅  
B. Continuous Internet  
C. Central Integration  
D. Continuous Installation

**Answer:** A

---

### 138. CD stands for:

A. Continuous Delivery/Deployment ✅  
B. Central Deployment  
C. Code Delivery  
D. Continuous Download

**Answer:** A

---

### 139. CI mainly performs:

A. Build & Test ✅  
B. Networking  
C. Monitoring  
D. Database

**Answer:** A

---

### 140. CD mainly performs:

A. Deployment ✅  
B. Coding  
C. Database  
D. Networking

**Answer:** A

---

### 141. Jenkins Pipeline is:

A. Automation Workflow ✅  
B. Storage  
C. Programming Language  
D. Network

**Answer:** A

---

### 142. Jenkinsfile is written in:

A. YAML  
B. Groovy ✅  
C. Python  
D. Java

**Answer:** B

---

### 143. Which comes first in CI/CD?

A. Deploy  
B. Build ✅  
C. Monitor  
D. Scale

**Answer:** B

---

### 144. Typical pipeline order:

A. Test → Build → Deploy  
B. Build → Test → Deploy ✅  
C. Deploy → Build → Test  
D. Monitor → Build

**Answer:** B

---

### 145. Rollback means:

A. Delete Application  
B. Return to Previous Version ✅  
C. Restart Server  
D. Shutdown

**Answer:** B

---

### 146. Which tool stores source code?

A. GitHub ✅  
B. Jenkins  
C. Docker  
D. Kubernetes

**Answer:** A

---

### 147. Which tool creates containers?

A. Jenkins  
B. Docker ✅  
C. Kubernetes  
D. Git

**Answer:** B

---

### 148. Which tool manages containers?

A. Docker  
B. Kubernetes ✅  
C. Git  
D. Linux

**Answer:** B

---

### 149. Typical DevOps pipeline:

A. Git → Jenkins → Docker → Kubernetes ✅  
B. Docker → Git → Linux  
C. SQL → Docker → AWS  
D. AWS → Git → Python

**Answer:** A

---

### 150. Main goal of DevOps:

A. Manual Deployment  
B. Faster & Automated Software Delivery ✅  
C. Reduce Internet Speed  
D. Increase Bugs

**Answer:** B

---

# 🎯 TOP 20 MUST-REMEMBER QUESTIONS (Very High Probability)

1. Docker = Container Platform
    
2. Image vs Container
    
3. Dockerfile purpose
    
4. `docker pull`
    
5. `docker run`
    
6. Docker Hub
    
7. Pod = Smallest Kubernetes Unit
    
8. Deployment vs ReplicaSet
    
9. Service purpose
    
10. ConfigMap vs Secret
    
11. `kubectl get pods`
    
12. Jenkins = CI/CD Tool
    
13. CI = Continuous Integration
    
14. CD = Continuous Delivery/Deployment
    
15. Pipeline = Build → Test → Deploy
    
16. Rollback
    
17. Git → Jenkins → Docker → Kubernetes
    
18. EKS = Kubernetes on AWS
    
19. Docker vs Kubernetes
    
20. DevOps Lifecycle
    

---

## ✅ Part 3 Complete

**Next (Part 4: MCQ 151–200)** হবে:

- Shell Scripting
    
- SQL
    
- Operating System
    
- Aptitude
    
- English (Final Revision) — এগুলো মিলিয়ে শেষ ৫০টি MCQ।
----
# BJIT Cloud & DevOps – 200 Most Expected MCQs

# Part 4 (MCQ 151–200): Shell Scripting + SQL + Operating System + Aptitude + English

---

# Shell Scripting (151–160)

### 151. Which line should appear at the beginning of a Bash script?

A. `#include`  
B. `#!/bin/bash` ✅  
C. `main()`  
D. `import bash`

**Answer:** B

---

### 152. Which command prints text?

A. printf  
B. echo ✅  
C. print  
D. display

**Answer:** B

---

### 153. Which symbol stores user input?

A. echo  
B. read ✅  
C. cat  
D. input

**Answer:** B

---

### 154. Which keyword is used for conditions?

A. while  
B. if ✅  
C. switch  
D. do

**Answer:** B

---

### 155. Which loop repeats a fixed number of times?

A. if  
B. for ✅  
C. break  
D. read

**Answer:** B

---

### 156. Which loop continues while a condition is true?

A. for  
B. while ✅  
C. if  
D. case

**Answer:** B

---

### 157. Which symbol is used for comments?

A. //  
B. # ✅  
C. /*  
D. --

**Answer:** B

---

### 158. Which command gives execute permission?

A. chmod +x file.sh ✅  
B. run file.sh  
C. execute file.sh  
D. sh +x

**Answer:** A

---

### 159. Which command runs a shell script?

A. `./script.sh` ✅  
B. run script.sh  
C. execute script.sh  
D. open script.sh

**Answer:** A

---

### 160. Bash is:

A. Programming Language  
B. Shell ✅  
C. Database  
D. Browser

**Answer:** B

---

# SQL (161–175)

### 161. SQL stands for:

A. Structured Query Language ✅  
B. Simple Query Language  
C. Sequential Query Language  
D. Standard Query Logic

**Answer:** A

---

### 162. Which command retrieves data?

A. INSERT  
B. SELECT ✅  
C. UPDATE  
D. DELETE

---

### 163. Which command inserts data?

A. SELECT  
B. INSERT ✅  
C. UPDATE  
D. DELETE

---

### 164. Which command modifies existing data?

A. UPDATE ✅  
B. INSERT  
C. DELETE  
D. ALTER

---

### 165. Which command removes data?

A. DROP  
B. DELETE ✅  
C. REMOVE  
D. CLEAR

---

### 166. Which clause filters rows?

A. GROUP BY  
B. WHERE ✅  
C. ORDER BY  
D. HAVING

---

### 167. Which clause sorts results?

A. WHERE  
B. ORDER BY ✅  
C. GROUP BY  
D. DISTINCT

---

### 168. Which function counts rows?

A. SUM  
B. COUNT() ✅  
C. AVG  
D. MAX

---

### 169. Which keyword removes duplicate rows?

A. UNIQUE  
B. DISTINCT ✅  
C. GROUP  
D. FILTER

---

### 170. Primary Key must be:

A. Duplicate  
B. Unique ✅  
C. NULL  
D. Optional

---

### 171. Foreign Key is used to:

A. Delete records  
B. Create relationships ✅  
C. Sort records  
D. Count records

---

### 172. Which JOIN returns only matching rows?

A. LEFT  
B. RIGHT  
C. INNER JOIN ✅  
D. FULL

---

### 173. Which JOIN returns all rows from the left table?

A. LEFT JOIN ✅  
B. RIGHT JOIN  
C. INNER JOIN  
D. CROSS JOIN

---

### 174. Which clause groups rows?

A. ORDER BY  
B. GROUP BY ✅  
C. WHERE  
D. LIMIT

---

### 175. HAVING is used with:

A. GROUP BY ✅  
B. SELECT  
C. UPDATE  
D. DELETE

---

# Operating System (176–190)

### 176. OS stands for:

A. Open Software  
B. Operating System ✅  
C. Online Service  
D. Object Storage

---

### 177. Kernel is:

A. Browser  
B. Core of the OS ✅  
C. Database  
D. Shell

---

### 178. Which is temporary memory?

A. ROM  
B. RAM ✅  
C. HDD  
D. SSD

---

### 179. Which memory retains data after power off?

A. RAM  
B. ROM ✅  
C. Cache  
D. Register

---

### 180. Running program is called:

A. Process ✅  
B. Thread  
C. Program  
D. Script

---

### 181. Thread is:

A. Independent OS  
B. Smallest execution unit ✅  
C. Database  
D. CPU

---

### 182. Which command shows running processes?

A. ls  
B. ps ✅  
C. pwd  
D. mkdir

---

### 183. Which command shows live processes?

A. top ✅  
B. cat  
C. echo  
D. free

---

### 184. Which command force kills a process?

A. stop  
B. kill -9 ✅  
C. exit  
D. rm

---

### 185. Virtual Memory uses:

A. CPU  
B. Disk Space ✅  
C. Cache  
D. Register

---

### 186. File permissions are:

A. rwx ✅  
B. abc  
C. xyz  
D. 123

---

### 187. Which command changes permissions?

A. chmod ✅  
B. chown  
C. ls  
D. cp

---

### 188. Which command shows disk usage?

A. free  
B. df -h ✅  
C. top  
D. ps

---

### 189. Which command shows memory usage?

A. free -m ✅  
B. ls  
C. rm  
D. pwd

---

### 190. Deadlock means:

A. Fast execution  
B. Processes waiting forever ✅  
C. File corruption  
D. Memory leak

---

# Aptitude & English (191–200)

### 191. 20% of 250 =

A. 40  
B. 50 ✅  
C. 60  
D. 70

---

### 192. Average of 10, 20, 30 =

A. 15  
B. 20 ✅  
C. 25  
D. 30

---

### 193. If CP = 100 and SP = 120, Profit =

A. 10  
B. 20 ✅  
C. 30  
D. 40

---

### 194. Probability of getting Head on one coin toss =

A. 1  
B. 1/2 ✅  
C. 1/3  
D. 2

---

### 195. Complete the series:

2, 4, 8, 16, ?

A. 20  
B. 24  
C. 32 ✅  
D. 64

---

### 196. Synonym of "Rapid":

A. Slow  
B. Fast ✅  
C. Weak  
D. Small

---

### 197. Antonym of "Ancient":

A. Old  
B. Modern ✅  
C. Historic  
D. Past

---

### 198. Fill in the blank:

He ____ playing football.

A. are  
B. is ✅  
C. am  
D. were

---

### 199. Choose the correct sentence:

A. She don't like coffee.  
B. She doesn't like coffee. ✅  
C. She not likes coffee.  
D. She isn't like coffee.

---

### 200. Which sentence is grammatically correct?

A. I has a laptop.  
B. I have a laptop. ✅  
C. I having a laptop.  
D. I hads a laptop.

---

# 🎯 30 Last-Minute Questions (Highest Probability)

1. Linux is an Operating System.
    
2. `pwd` → Current directory.
    
3. `ls` → List files.
    
4. `chmod` → Change permissions.
    
5. `git init` → Initialize repository.
    
6. `git add` → Stage changes.
    
7. `git commit` → Save changes.
    
8. `git push` → Upload to GitHub.
    
9. `git pull` → Download latest changes.
    
10. Cloud = Computing over the Internet.
    
11. EC2 = Virtual Machine.
    
12. S3 = Object Storage.
    
13. IAM = Identity & Access Management.
    
14. VPC = Virtual Private Cloud.
    
15. Security Group = Virtual Firewall.
    
16. Docker Image = Template.
    
17. Docker Container = Running Image.
    
18. Docker Hub = Image Repository.
    
19. Kubernetes Pod = Smallest Unit.
    
20. Deployment manages Pods.
    
21. Jenkins = CI/CD Tool.
    
22. CI = Continuous Integration.
    
23. CD = Continuous Delivery/Deployment.
    
24. SQL `SELECT` = Read data.
    
25. SQL `WHERE` = Filter rows.
    
26. Primary Key = Unique.
    
27. Process = Running Program.
    
28. RAM = Temporary Memory.
    
29. SSH Port = 22, HTTP = 80, HTTPS = 443.
    
30. TCP = Reliable, UDP = Faster.
    

---

# ⭐ Final Exam Strategy (30 Minutes)

- **প্রথম ১০ মিনিট:** Linux, Networking, Git, AWS (সহজ প্রশ্ন আগে করুন)
    
- **পরের ১০ মিনিট:** Docker, Kubernetes, Jenkins, SQL
    
- **শেষ ১০ মিনিট:** OS, Aptitude, English এবং সব উত্তর দ্রুত রিভিউ করুন
    
- কঠিন প্রশ্নে বেশি সময় নষ্ট করবেন না; পরে ফিরে আসুন।
    

এই ২০০টি MCQ-র বিষয়গুলো ভালোভাবে রিভিশন করতে পারলে BJIT Cloud & DevOps Trainee assessment-এর জন্য আপনি একটি শক্ত প্রস্তুতি নিয়ে পরীক্ষায় যেতে পারবেন। শুভকামনা! 🎉



যদি **মাত্র ৫০টি প্রশ্ন** পরীক্ষার আগে পড়তে পারো, তাহলে আমি এই ৫০টিকেই বেছে নেব। এগুলো **BJIT Trainee – Cloud & DevOps** assessment-এর জন্য সবচেয়ে গুরুত্বপূর্ণ।

---

# Final 50 Most Expected MCQs

### 1. Linux is a:

A. Database  
B. Operating System ✅  
C. Browser  
D. IDE

---

### 2. Current directory command?

A. ls  
B. pwd ✅  
C. cd  
D. cat

---

### 3. List files command?

A. pwd  
B. ls ✅  
C. cd  
D. rm

---

### 4. Change directory command?

A. mkdir  
B. cd ✅  
C. mv  
D. cp

---

### 5. Remove file command?

A. cp  
B. rm ✅  
C. mv  
D. cat

---

### 6. Create directory?

A. mkdir ✅  
B. touch  
C. cp  
D. pwd

---

### 7. Show running processes?

A. top  
B. ps ✅  
C. df  
D. ls

---

### 8. Change permission?

A. chmod ✅  
B. chown  
C. cp  
D. mv

---

### 9. SSH default port?

A. 21  
B. 22 ✅  
C. 80  
D. 443

---

### 10. HTTP port?

A. 21  
B. 22  
C. 80 ✅  
D. 443

---

### 11. HTTPS port?

A. 80  
B. 443 ✅  
C. 22  
D. 25

---

### 12. DNS stands for?

A. Domain Name System ✅  
B. Data Network Service  
C. Digital Name Server  
D. Domain Network Security

---

### 13. TCP is:

A. Faster  
B. Reliable ✅  
C. Wireless  
D. Connectionless

---

### 14. UDP is:

A. Reliable  
B. Connection-oriented  
C. Faster ✅  
D. Secure

---

### 15. Git is:

A. Database  
B. Version Control System ✅  
C. OS  
D. IDE

---

### 16. Initialize Git repository?

A. git start  
B. git init ✅  
C. git create  
D. git new

---

### 17. Stage changes?

A. git add ✅  
B. git push  
C. git commit  
D. git pull

---

### 18. Save changes locally?

A. git commit ✅  
B. git push  
C. git clone  
D. git pull

---

### 19. Upload code?

A. git commit  
B. git push ✅  
C. git add  
D. git init

---

### 20. Download latest code?

A. git clone  
B. git pull ✅  
C. git push  
D. git merge

---

### 21. AWS stands for?

A. Amazon Web Services ✅  
B. Advanced Web Server  
C. Automated Web Service  
D. Amazon World System

---

### 22. EC2 is:

A. Database  
B. Virtual Machine ✅  
C. Storage  
D. Firewall

---

### 23. S3 is:

A. Compute  
B. Object Storage ✅  
C. Networking  
D. Database

---

### 24. IAM is used for:

A. Monitoring  
B. Identity & Access Management ✅  
C. Storage  
D. Backup

---

### 25. Security Group is:

A. Router  
B. Firewall ✅  
C. Database  
D. Switch

---

### 26. Docker is:

A. Database  
B. Container Platform ✅  
C. VM  
D. IDE

---

### 27. Docker Image is:

A. Running Container  
B. Template ✅  
C. Network  
D. Volume

---

### 28. Running Docker Image is called:

A. Pod  
B. Container ✅  
C. Cluster  
D. Volume

---

### 29. Docker Hub is:

A. Repository ✅  
B. Database  
C. OS  
D. Browser

---

### 30. Docker build command?

A. docker build ✅  
B. docker run  
C. docker pull  
D. docker start

---

### 31. Kubernetes manages:

A. Database  
B. Containers ✅  
C. Browser  
D. IDE

---

### 32. Smallest Kubernetes object?

A. Cluster  
B. Node  
C. Pod ✅  
D. Service

---

### 33. Kubernetes CLI?

A. docker  
B. kubectl ✅  
C. aws  
D. git

---

### 34. Jenkins is:

A. Database  
B. CI/CD Tool ✅  
C. Web Server  
D. Compiler

---

### 35. CI means:

A. Continuous Integration ✅  
B. Central Integration  
C. Continuous Internet  
D. Code Integration

---

### 36. SQL full form?

A. Structured Query Language ✅  
B. Sequential Query Language  
C. Standard Query Language  
D. Simple Query Language

---

### 37. Read data command?

A. INSERT  
B. SELECT ✅  
C. UPDATE  
D. DELETE

---

### 38. Add new data?

A. UPDATE  
B. INSERT ✅  
C. DELETE  
D. SELECT

---

### 39. Remove data?

A. DELETE ✅  
B. DROP  
C. REMOVE  
D. CLEAR

---

### 40. Primary Key is:

A. Duplicate  
B. Unique ✅  
C. Nullable  
D. Optional

---

### 41. Kernel is:

A. Browser  
B. Core of OS ✅  
C. Database  
D. Shell

---

### 42. Running Program?

A. Thread  
B. Process ✅  
C. Script  
D. Service

---

### 43. Temporary memory?

A. ROM  
B. RAM ✅  
C. SSD  
D. HDD

---

### 44. Force kill process?

A. kill  
B. kill -9 ✅  
C. stop  
D. exit

---

### 45. Show disk usage?

A. free -m  
B. df -h ✅  
C. top  
D. ps

---

### 46. Show memory usage?

A. free -m ✅  
B. ls  
C. pwd  
D. cat

---

### 47. Which is a Cloud Deployment Model?

A. Public Cloud ✅  
B. SQL  
C. Git  
D. Docker

---

### 48. Which service runs serverless code in AWS?

A. EC2  
B. Lambda ✅  
C. S3  
D. IAM

---

### 49. DevOps goal is:

A. Manual Deployment  
B. Faster Automated Delivery ✅  
C. Slow Release  
D. Reduce Testing

---

### 50. Typical DevOps Pipeline?

A. Git → Jenkins → Docker → Kubernetes ✅  
B. Docker → SQL → AWS  
C. Linux → SQL → Git  
D. AWS → Docker → Git

---

# ⭐ Last Minute Revision (10 Facts)

1. **SSH = 22**
    
2. **HTTP = 80**
    
3. **HTTPS = 443**
    
4. **EC2 = Virtual Machine**
    
5. **S3 = Object Storage**
    
6. **IAM = User & Permission Management**
    
7. **Docker Image → Container**
    
8. **Pod = Smallest Kubernetes Unit**
    
9. **Jenkins = CI/CD**
    
10. **SQL SELECT = Read Data**
    

## 🎯 Prediction

BJIT-এর ৩০ মিনিটের Cloud & DevOps Trainee assessment-এ **Linux, Networking, Git, AWS, Docker, Kubernetes, SQL, OS** থেকে **Basic Concept + MCQ** আসার সম্ভাবনাই সবচেয়ে বেশি। যদি এই ৫০টি প্রশ্ন আত্মবিশ্বাসের সাথে উত্তর দিতে পারেন, তাহলে পরীক্ষার জন্য আপনার প্রস্তুতি বেশ ভালো থাকবে।

**Best of luck for your exam!** 🚀