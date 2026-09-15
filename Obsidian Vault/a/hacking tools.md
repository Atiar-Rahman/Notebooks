যদি **ethical hacking / authorized security testing** শেখার জন্য জিজ্ঞেস করো, তাহলে tools-গুলো category অনুযায়ী শেখা সবচেয়ে ভালো।

### 🔎 1. Network Discovery & Analysis

- **Nmap** — network/service discovery
    
- **Wireshark** — packet analysis
    
- **tcpdump** — command-line packet capture
    
- **Netcat** — network troubleshooting/lab
    
- **Masscan** — large-scale scanning; only authorized networks
    

### 🌐 2. Web Security

- **Burp Suite** ⭐⭐⭐⭐⭐ — web/API security testing
    
- **OWASP ZAP** ⭐⭐⭐⭐ — web security testing
    
- **Nikto** — web-server security assessment
    

### 🔐 3. Password & Authentication Security

- **Hashcat** — password-hash auditing
    
- **John the Ripper** — password auditing
    
- **Hydra** — authentication testing in authorized labs
    

এগুলো real accounts/services-এর বিরুদ্ধে ব্যবহার করা যাবে না; নিজের lab/CTF-এ practice করবে।

### 🖥️ 4. Linux / System Security

- **Lynis** — Linux security auditing
    
- **psutil** — Python system monitoring
    
- **auditd** — Linux auditing
    
- **strace** — system-call analysis
    

### 🧪 5. Exploit Research / Legal Labs

- **Metasploit Framework** ⭐⭐⭐⭐⭐
    
- **Ghidra** — reverse engineering
    
- **GDB** — debugging
    
- **pwndbg** — GDB enhancement
    

এগুলো শেখার জন্য **TryHackMe, Hack The Box বা নিজের VirtualBox lab** ব্যবহার করা ভালো।

### 🦠 6. Malware / Reverse Engineering

- **Ghidra**
    
- **Cutter**
    
- **x64dbg**
    
- **YARA**
    
- **Volatility** — memory forensics
    

### 📡 7. Wireless Security

- **Aircrack-ng**
    
- **Kismet**
    
- **Wireshark**
    

শুধু নিজের/অনুমোদিত Wi-Fi lab-এ ব্যবহার করবে।

### 🕵️ 8. OSINT

- **theHarvester**
    
- **SpiderFoot**
    
- **Maltego**
    

Public information কীভাবে security investigation-এ ব্যবহার হয় সেটা শেখার জন্য।

### 🛡️ 9. Blue Team / Defensive Security

- **Wazuh**
    
- **Suricata**
    
- **Zeek**
    
- **Snort**
    
- **Splunk**
    
- **Elastic Stack**
    

এগুলো SOC/defensive cybersecurity-এর জন্য খুব useful।

---

## ⭐ Beginner → Advanced order

```text
Linux
  ↓
Networking
  ↓
Nmap
  ↓
Wireshark
  ↓
Burp Suite
  ↓
OWASP ZAP
  ↓
Metasploit
  ↓
Ghidra
  ↓
YARA / Volatility
  ↓
Zeek / Suricata / Wazuh
```

তোমার জন্য প্রথমে **Linux + Networking + Nmap + Wireshark + Burp Suite** ভালো foundation হবে। এরপর Python দিয়ে security automation যোগ করলে skillset অনেক শক্ত হবে।