

---

# 🐧 **LINUX COMMAND COURSE (Beginner → Advanced)**

### Includes concepts, examples, and practice tasks.

---

# 🟩 **BEGINNER LEVEL (Level 1–3)**

Perfect for:  
✔ New Linux users  
✔ Windows/macOS users switching to Linux  
✔ Anyone learning ethical hacking, DevOps, or server admin

---

## **LEVEL 1 — Basic Navigation & Files**

### **Essential Commands**

```
pwd        # current directory
ls         # list files
cd         # change directory
clear      # clear terminal
echo       # print text
```

### **File & Folder Commands**

```
mkdir test_folder
touch file.txt
cp file1 file2
mv oldname newname
rm file.txt
rmdir empty_folder
```

### **View Files**

```
cat file
less file
head file
tail file
```

### **Mini Practice**

1. Create a folder named _projects_
    
2. Inside it, make a file called _notes.txt_
    
3. Write "hello" using `echo`
    
4. Copy the file
    
5. Delete the copy
    

---

## **LEVEL 2 — System Info & Help**

### **System Info**

```
uname -a
whoami
id
df -h
du -sh .
free -h
date
```

### **Help System**

```
man ls
ls --help
whatis grep
apropos network
```

### **Mini practice**

- Find your OS version
    
- List commands related to “disk” using `apropos`
    

---

## **LEVEL 3 — Permissions & Users**

### **Permissions**

```
chmod 755 script.sh
chown user:user file
chgrp developers file
```

### **Users & Groups**

```
useradd user1
passwd user1
groupadd devs
usermod -aG devs user1
```

### **Mini practice**

- Change a file’s permissions so **only you can read/write it**
    
- Add a new user called `student`
    

---

# 🟨 **INTERMEDIATE LEVEL (Level 4–6)**

Perfect for:  
✔ Support engineers  
✔ IT students  
✔ Ethical hackers  
✔ DevOps beginners

---

## **LEVEL 4 — Text Processing Superpowers**

### **Search**

```
grep "error" logfile
grep -r "password" /etc
```

### **Sort & Filter**

```
sort file
uniq file
cut -d ':' -f 1 /etc/passwd
```

### **Stream Editing**

```
sed 's/apple/banana/' file
```

### **Advanced Text Processing**

```
awk '{print $1}' file
```

### **Mini Practice**

- Extract the first column of `/etc/passwd`
    
- Replace "hello" with "hi" in a file
    

---

## **LEVEL 5 — Processes & Jobs**

```
ps aux
top
htop
kill 1234
killall firefox
jobs
bg
fg
```

### **System Logs**

```
journalctl -xe
dmesg | tail
```

### **Mini Practice**

- Find the process using the most memory
    
- Kill a running process by name
    

---

## **LEVEL 6 — Networking**

### **Network inspection**

```
ip a
ip r
ss -tuln
ping google.com
```

### **File Transfer**

```
wget URL
curl -O URL
scp file user@host:/path
```

### **DNS Tools**

```
dig google.com
nslookup linux.org
```

### **Mini Practice**

- Show all open ports
    
- Ping 8.8.8.8 five times
    

---

# 🟥 **ADVANCED LEVEL (Level 7–10)**

Perfect for:  
✔ DevOps  
✔ SysAdmins  
✔ Cybersecurity  
✔ Backend engineers  
✔ Cloud engineers

---

## **LEVEL 7 — Shell Scripting**

### **Basic script**

```
#!/bin/bash
echo "Hello world"
```

### **Variables**

```
name="Bob"
echo "Hi $name"
```

### **IF statements**

```
if [ -f file.txt ]; then
  echo "File exists"
fi
```

### **Loops**

```
for i in *.txt; do
  echo $i
done
```

---

## **LEVEL 8 — Package Management**

### **Debian/Ubuntu**

```
apt update
apt upgrade
apt install nginx
```

### **RedHat/CentOS/Fedora**

```
dnf install nginx
rpm -qa
```

### **Arch**

```
pacman -Syu
```

---

## **LEVEL 9 — Systemd & Services**

```
systemctl start nginx
systemctl stop nginx
systemctl status nginx
systemctl enable ssh
journalctl -u nginx
```

### **Timers**

```
systemctl list-timers
```

---

## **LEVEL 10 — Storage, Partitions, LVM**

```
lsblk
fdisk /dev/sda
mkfs.ext4 /dev/sda1
mount /dev/sda1 /mnt
vgcreate
lvcreate
resize2fs
```

---

# 🏆 **BONUS: ADVANCED SHELL TRICKS**

```
history | grep ssh
!!      # run last command
!ls     # run last command starting with "ls"
ctrl+r  # search command history
xargs   # pass input as arguments
```

---

