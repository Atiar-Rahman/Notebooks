sun-jun-21-2016

----

Linux commands are huge (thousands of commands), so I’ll give you a **beginner → advanced Linux command roadmap** with **important commands + examples**. Since you are learning **cyber security**, I’ll include security-related commands too.

## 1. Basic Terminal Commands

### `pwd` — show current directory

```bash
pwd
```

Output:

```
/home/atiar/projects
```

---

### `ls` — list files/folders

```bash
ls
```

Options:

```bash
ls -l
```

Detailed list

```bash
ls -la
```

Show hidden files also

Example:

```
-rwxr-xr-x  file.sh
drwxr-xr-x  projects
```

---

### `cd` — change directory

```bash
cd Documents
```

Go home:

```bash
cd ~
```

Go previous:

```bash
cd -
```

One folder back:

```bash
cd ..
```

---

### `clear` — clear terminal

```bash
clear
```

---

### `history` — command history

```bash
history
```

Run previous command:

```bash
!25
```

---

# 2. File & Folder Management

## `mkdir` — create folder

```bash
mkdir test
```

Multiple:

```bash
mkdir folder1 folder2
```

Nested:

```bash
mkdir -p project/src/components
```

---

## `touch` — create file

```bash
touch app.py
```

Create multiple:

```bash
touch index.html style.css
```

---

## `cat` — read file

```bash
cat file.txt
```

Example:

```bash
cat users.txt
```

---

## `less` — view large file

```bash
less logfile.txt
```

Exit:

```
q
```

---

## `head`

First 10 lines:

```bash
head file.txt
```

Custom:

```bash
head -20 file.txt
```

---

## `tail`

Last lines:

```bash
tail file.txt
```

Live log:

```bash
tail -f /var/log/syslog
```

---

# 3. Copy Move Delete

## `cp` — copy

File:

```bash
cp a.txt b.txt
```

Folder:

```bash
cp -r folder backup
```

---

## `mv` — move / rename

Rename:

```bash
mv old.txt new.txt
```

Move:

```bash
mv file.txt Documents/
```

---

## `rm` — delete

File:

```bash
rm file.txt
```

Folder:

```bash
rm -r folder
```

Force:

```bash
rm -rf folder
```

⚠️ Dangerous.

---

# 4. File Permission

## `chmod`

Change permission:

```bash
chmod 755 script.sh
```

Meaning:

```
7 = owner
5 = group
5 = others
```

Execute:

```bash
chmod +x app.sh
```

Run:

```bash
./app.sh
```

---

## `chown`

Change owner:

```bash
sudo chown user file.txt
```

Example:

```bash
sudo chown atiar project
```

---

# 5. Search Commands

## `find`

Find file:

```bash
find /home -name test.txt
```

Find python:

```bash
find . -name "*.py"
```

---

## `grep`

Search text:

```bash
grep "password" file.txt
```

Recursive:

```bash
grep -r "admin" .
```

---

## `locate`

```bash
locate nginx.conf
```

Update database:

```bash
sudo updatedb
```

---

# 6. System Information

## `uname`

```bash
uname -a
```

Shows:

- kernel
    
- architecture
    
- OS
    

---

## `hostname`

```bash
hostname
```

---

## `whoami`

Current user:

```bash
whoami
```

---

## `id`

User information:

```bash
id
```

Output:

```
uid=1000
gid=1000
```

---

## `uptime`

```bash
uptime
```

Shows:

- running time
    
- load
    

---

## `top`

Process monitor:

```bash
top
```

Better:

```bash
htop
```

Install:

```bash
sudo apt install htop
```

---

# 7. Process Management

## `ps`

Processes:

```bash
ps aux
```

Find:

```bash
ps aux | grep nginx
```

---

## `kill`

Stop process:

```bash
kill PID
```

Force:

```bash
kill -9 PID
```

Example:

```bash
kill -9 1234
```

---

# 8. Package Management (Ubuntu)

## Update

```bash
sudo apt update
```

Upgrade:

```bash
sudo apt upgrade
```

---

Install:

```bash
sudo apt install python3
```

Remove:

```bash
sudo apt remove nginx
```

---

# 9. Network Commands (Cyber Security)

## `ip`

Show IP:

```bash
ip addr
```

---

## `ping`

Test connection:

```bash
ping google.com
```

---

## `curl`

Request website:

```bash
curl https://example.com
```

API:

```bash
curl -X GET api.com/users
```

---

## `wget`

Download:

```bash
wget file.zip
```

---

## `netstat`

Connections:

```bash
netstat -tulpn
```

Shows:

- ports
    
- services
    

---

## `ss`

Modern netstat:

```bash
ss -tulpn
```

---

## `traceroute`

Route:

```bash
traceroute google.com
```

---

## `nslookup`

DNS lookup:

```bash
nslookup example.com
```

---

## `dig`

DNS details:

```bash
dig google.com
```

---

# 10. File Transfer

## `scp`

Copy remote file:

```bash
scp file.txt user@server:/home/user
```

---

## `ssh`

Login:

```bash
ssh user@server_ip
```

Example:

```bash
ssh root@192.168.1.10
```

---

# 11. Compression

## zip

```bash
zip file.zip test.txt
```

---

## unzip

```bash
unzip file.zip
```

---

## tar

Create:

```bash
tar -cvf backup.tar folder
```

Extract:

```bash
tar -xvf backup.tar
```

---

# 12. Disk Management

## `df`

Disk space:

```bash
df -h
```

---

## `du`

Folder size:

```bash
du -sh folder
```

---

## `lsblk`

Disks:

```bash
lsblk
```

---

# 13. Environment Variables

Show:

```bash
env
```

PATH:

```bash
echo $PATH
```

Set:

```bash
export NAME=atiar
```

---

# 14. User Management

Add user:

```bash
sudo adduser john
```

Delete:

```bash
sudo deluser john
```

Change password:

```bash
passwd
```

---

# 15. Service Management

Using systemd:

Start:

```bash
sudo systemctl start nginx
```

Stop:

```bash
sudo systemctl stop nginx
```

Status:

```bash
systemctl status nginx
```

Enable startup:

```bash
sudo systemctl enable nginx
```

---

# 16. Logs (Important for Cyber Security)

View logs:

```bash
journalctl
```

Follow:

```bash
journalctl -f
```

Authentication:

```bash
cat /var/log/auth.log
```

---

# 17. Networking Security Tools

## Nmap

Install:

```bash
sudo apt install nmap
```

Scan:

```bash
nmap 192.168.1.1
```

Service scan:

```bash
nmap -sV target.com
```

---

## Netcat

Listen:

```bash
nc -lvp 4444
```

Connect:

```bash
nc IP 4444
```

---

## Wireshark

```bash
sudo apt install wireshark
```

---

# 18. Shell Commands

Pipe:

```bash
ls | grep ".py"
```

Output:

```bash
command > file.txt
```

Append:

```bash
echo hello >> file.txt
```

---

# 19. Help Commands

Manual:

```bash
man ls
```

Help:

```bash
ls --help
```

Find command:

```bash
which python
```

---

# 20. Cyber Security Linux Must Know

Learn these deeply:

```
ls
cd
cat
grep
find
chmod
chown
ps
top
kill
systemctl
journalctl
ip
ss
netstat
curl
wget
ssh
scp
nmap
tcpdump
wireshark
python
bash
```

For **cyber security beginner path**:

1. Linux filesystem
    
2. Bash scripting
    
3. Networking commands
    
4. Permissions
    
5. Processes
    
6. Logs
    
7. Nmap
    
8. Web security tools
    
9. TryHackMe / HackTheBox labs
    

This set covers most daily Linux usage.