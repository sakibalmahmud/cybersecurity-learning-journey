# Linux Privilege Escalation

This folder contains my practical notes, commands, techniques, and learning resources related to **Linux Privilege Escalation**.

The goal is to understand how a normal user account can potentially gain higher privileges, including root access, by identifying misconfigurations and security vulnerabilities in Linux systems.

## 🎯 Topics Covered

| Technique | Description |
|---|---|
| Sudo Misconfiguration | Exploiting incorrectly configured sudo permissions |
| SUID / SGID | Identifying and analyzing SUID/SGID binaries |
| Linux Capabilities | Finding potentially dangerous file capabilities |
| Cron Jobs | Identifying misconfigured scheduled tasks |
| NFS | Analyzing insecure NFS configurations |
| PATH Hijacking | Exploiting insecure PATH configurations |
| Kernel Exploitation | Identifying and exploiting vulnerable Linux kernels |

## 🔍 Privilege Escalation Methodology

A good penetration tester generally follows a systematic approach when investigating a Linux machine.

1. **System Enumeration** – Gather basic information about the target system.
2. **User & Permission Enumeration** – Identify users, groups, and file permissions.
3. **Sudo Enumeration** – Check which commands can be executed with sudo privileges.
4. **SUID Enumeration** – Search for binaries with the SUID permission.
5. **Capabilities Enumeration** – Identify potentially dangerous Linux capabilities.
6. **Cron Jobs Enumeration** – Inspect scheduled tasks and their permissions.
7. **Kernel Exploitation** – Research kernel versions for known vulnerabilities.

## 🛠️ Tools & Commands

- Linux CLI
- GTFOBins
- LinPEAS
- Linux Exploit Suggester
- SearchSploit
- GCC

## 📂 Folder Structure

```text
Linux-Privilege-Escalation/
├── README.md
├── Sudo-Misconfiguration/
├── SUID-SGID/
├── Linux-Capabilities/
├── Cron-Jobs/
├── NFS/
├── PATH-Hijacking/
└── Kernel-Exploitation/
```

## 📚 Learning Sources

- [GTFOBins](https://gtfobins.github.io/)
- [HackTricks](https://book.hacktricks.wiki/)
- [TryHackMe](https://tryhackme.com/)
- [Exploit Database](https://www.exploit-db.com/)

## ⚠️ Disclaimer

All techniques and commands documented here are intended for educational purposes and authorized penetration testing in controlled environments.

---

**Enumerate • Identify • Exploit • Escalate • Document**
