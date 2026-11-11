# Hydra – Network Login Password Testing

**TryHackMe Room:** [Hydra](https://tryhackme.com/room/hydra)

## 1. Introduction

Hydra (THC Hydra) is a popular online password-cracking tool used to test login credentials against different network services.

It performs dictionary-based login attempts using usernames and passwords from wordlists.

**Main Uses:**
- Testing username and password combinations.
- Auditing weak login credentials.
- Testing network authentication services.
- Performing authorized password security assessments.

## 2. Supported Protocols

Hydra supports many protocols and services, including:

- FTP
- SSH
- HTTP / HTTPS
- SMB
- RDP
- Telnet
- SMTP
- IMAP
- POP3
- MySQL
- PostgreSQL
- LDAP
- VNC
- SNMP
- Cisco authentication services

For the complete list, check the official Hydra documentation.

## 3. Installation on Kali Linux

```bash
sudo apt update
sudo apt install hydra -y
```

Check the installed version:

```bash
hydra -h
```

Display available options and supported services:

```bash
hydra -U
```

## 4. Basic Hydra Syntax

```bash
hydra [options] TARGET SERVICE
```

Hydra uses different options depending on the target service and authentication method.

### Important Options

| Option | Description |
|---|---|
| `-l` | Specify a single username |
| `-L` | Specify a username wordlist |
| `-p` | Specify a single password |
| `-P` | Specify a password wordlist |
| `-t` | Set the number of parallel tasks |
| `-V` | Show each login attempt |
| `-f` | Stop after finding a valid login |
| `-s` | Specify a custom service port |

## 5. FTP Brute-Force Testing (Port 21)

```bash
hydra -l user -P passlist.txt ftp://TARGET_IP
```

**Explanation:**
- `-l user` → Specifies the username.
- `-P passlist.txt` → Uses a password wordlist.
- `ftp://TARGET_IP` → Specifies the FTP service.

## 6. SSH Brute-Force Testing (Port 22)

```bash
hydra -l username -P /usr/share/wordlists/rockyou.txt -t 4 ssh://TARGET_IP
```

**Explanation:**
- `-l username` → Specifies the username.
- `-P` → Specifies the password wordlist.
- `-t 4` → Uses four parallel tasks.
- `ssh://TARGET_IP` → Specifies the SSH service.

### SSH Login

After obtaining valid credentials in an authorized lab:

```bash
ssh username@TARGET_IP
```

Enter the recovered password when prompted.

## 7. HTTP POST Form Testing

Hydra can test login forms that use HTTP POST requests.

### Basic Syntax

```bash
hydra -l username -P wordlist.txt TARGET_IP http-post-form "/login.php:username=^USER^&password=^PASS^:F=incorrect" -V
```

**Explanation:**
- `http-post-form` → Specifies HTTP POST form authentication.
- `/login.php` → Login page path.
- `^USER^` → Username placeholder.
- `^PASS^` → Password placeholder.
- `F=incorrect` → Identifies a failed login response.
- `-V` → Displays each attempt.

### Example

```bash
hydra -l username -P /usr/share/wordlists/rockyou.txt TARGET_IP http-post-form "/:username=^USER^&password=^PASS^:F=Your username or password is incorrect" -V
```

**Important:** The form path, field names, and failure message must match the actual login form. Inspect the HTTP request and response before constructing the command.

## 8. Working with Wordlists

### Extract the First 30 Passwords

```bash
head -n 30 /usr/share/wordlists/rockyou.txt > first30.txt
```

Creates a smaller wordlist containing the first 30 entries.

### Verify the Wordlist

```bash
wc -l first30.txt
```

Displays the number of lines in the file.

### Use a Username Wordlist

```bash
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -P /usr/share/wordlists/rockyou.txt TARGET_IP ssh
```

**Explanation:**
- `-L` → Uses a username wordlist.
- `-P` → Uses a password wordlist.
- `TARGET_IP` → Specifies the target.
- `ssh` → Specifies the service.

## 9. Important Notes

- `-l` and `-L` are different: lowercase `-l` specifies one username, while uppercase `-L` specifies a username list.
- `-p` specifies one password, while `-P` specifies a password wordlist.
- Different protocols require different Hydra syntax.
- HTTP form testing requires the correct form parameters and failure condition.
- Excessive login attempts may trigger account lockouts or security alerts.

## 10. Learning Resources

- [TryHackMe – Hydra](https://tryhackme.com/room/hydra)
- [THC Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Kali Linux Hydra Documentation](https://www.kali.org/tools/hydra/)

---

**Disclaimer:** Use Hydra only in authorized cybersecurity labs or on systems where you have explicit permission to perform password security testing.
