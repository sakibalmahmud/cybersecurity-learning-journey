# Windows CMD Basics

Windows Command Prompt (CMD) is a command-line interface used to interact with the Windows operating system. It allows users to manage files, inspect system information, configure networks, and perform basic system administration.

These commands are also useful for Windows enumeration during cybersecurity labs and authorized penetration testing.

## 1. Basics and Help

| Command | Description |
|---|---|
| `help` | List available commands. |
| `help <command>` | Get help about a specific command. |
| `<command> /?` | Display help for a command. |
| `cls` | Clear the screen. |
| `exit` | Close CMD. |
| `echo <text>` | Display text. |
| `set` | Display environment variables. |
| `echo %PATH%` | Display the system PATH variable. |
| `doskey /history` | Display command history for the current session. |

## 2. Remote Login (SSH)

If an SSH service is running on the target and you have valid credentials, you can connect using:

```cmd
ssh username@<target-ip>
```

Example:

```cmd
ssh user@10.48.172.140
```

Enter the password when prompted.

## 3. System Information

| Command | Description |
|---|---|
| `ver` | Display the Windows version. |
| `systeminfo` | Display detailed OS and hardware information. |
| `hostname` | Display the computer name. |
| `whoami` | Show the current username. |
| `date /t` | Display the current date. |
| `time /t` | Display the current time. |
| `driverquery` | List installed drivers. |
| `wmic qfe list` | List installed Windows updates (WMIC is deprecated on newer Windows versions). |
| `shutdown /s /t 0` | Shut down the computer immediately. |
| `shutdown /r /t 0` | Restart the computer immediately. |

## 4. Network Commands

### Network Configuration

| Command | Description |
|---|---|
| `ipconfig` | Display basic network configuration. |
| `ipconfig /all` | Display detailed network information, including MAC, DNS, and DHCP details. |
| `ipconfig /flushdns` | Clear the DNS cache. |
| `getmac` | Display MAC addresses. |
| `arp -a` | Display the ARP table (IP-to-MAC mapping). |
| `route print` | Display the routing table. |

### Testing and Tracing

| Command | Description |
|---|---|
| `ping <host>` | Test connectivity to a host. |
| `tracert <host>` | Trace the route to a destination. |
| `nslookup <domain>` | Look up DNS information for a domain. |

Example:

```cmd
tracert example.com
nslookup example.com
```

### Connections and Ports

| Command | Description |
|---|---|
| `netstat -a` | Display active connections and listening ports. |
| `netstat -ano` | Display connections and listening ports with their PIDs. |
| `netstat -abon` | Display connections, listening ports, executable names, and PIDs (requires administrator privileges for full details). |

### Wi-Fi, Firewall and Sharing

| Command | Description |
|---|---|
| `netsh wlan show profiles` | List saved Wi-Fi profiles. |
| `netsh advfirewall show allprofiles` | Display Windows Firewall status. |
| `net view` | Display computers visible on the network. |
| `net share` | Display shared folders on the local computer. |

## 5. Files and Directories

### Navigation and Listing

| Command | Description |
|---|---|
| `cd` | Display the current directory. |
| `cd <folder>` | Change directory. |
| `cd ..` | Move to the parent directory. |
| `dir` | List files and directories. |
| `dir /a` | Display all files, including hidden and system files. |
| `tree` | Display directory structure as a tree. |

### Creating and Removing

| Command | Description |
|---|---|
| `mkdir <name>` | Create a directory. |
| `rmdir <name>` | Remove an empty directory. |
| `rmdir /s <name>` | Remove a directory and its contents. |
| `del <file>` | Delete a file. |

### Copying, Moving and Renaming

| Command | Description |
|---|---|
| `copy <source> <destination>` | Copy a file. |
| `xcopy <source> <destination> /e` | Copy directories and their contents. |
| `move <source> <destination>` | Move a file or directory. |
| `ren <old> <new>` | Rename a file or directory. |

### Reading and File Information

| Command | Description |
|---|---|
| `type <file>` | Display file contents. |
| `more <file>` | Display file contents page by page. |
| `attrib <file>` | Display or change file attributes. |
| `where <program>` | Find the location of a program. |

## 6. Searching

| Command | Description |
|---|---|
| `find "text" <file>` | Search for specific text in a file. |
| `findstr /i "text" <file>` | Search for text without case sensitivity. |
| `findstr /s /i "password" *.txt` | Search for password-related text in TXT files and subdirectories. |
| `dir /s <filename>` | Search for a file in the current directory and its subdirectories. |

## 7. Users, Groups and Permissions

| Command | Description |
|---|---|
| `whoami /priv` | Display current user privileges. |
| `whoami /groups` | Display groups the current user belongs to. |
| `quser` | Display currently logged-in users. |
| `net user` | List local user accounts. |
| `net user <username>` | Display information about a specific user. |
| `net localgroup` | List local groups. |
| `net localgroup administrators` | List members of the Administrators group. |
| `net accounts` | Display password and account lockout policies. |
| `icacls <file/folder>` | Display or modify file and folder permissions. |

## 8. Processes and Services

### Processes

| Command | Description |
|---|---|
| `tasklist` | List running processes. |
| `tasklist /svc` | Display services associated with processes. |
| `taskkill /pid <PID> /f` | Forcefully terminate a process using its PID. |

### Services

| Command | Description |
|---|---|
| `sc query` | Display service information and status. |
| `sc qc <service>` | Display a service's configuration. |
| `net start` | List running services. |
| `net start <service>` | Start a service. |
| `net stop <service>` | Stop a service. |

Some service-management operations require administrator privileges.

### Scheduled Tasks

```cmd
schtasks /query /fo list
```

Displays scheduled tasks and their configurations.

## 9. Registry and Logs

| Command | Description |
|---|---|
| `reg query <key>` | Read registry information. |
| `gpresult /r` | Display applied Group Policies. |
| `wevtutil qe Security /c:5 /f:text` | Display the latest five Security log events (may require administrator privileges). |

Example: Check programs configured to start automatically:

```cmd
reg query "HKLM\Software\Microsoft\Windows\CurrentVersion\Run"
```

## 10. Disk and System Repair

| Command | Description |
|---|---|
| `chkdsk` | Check a disk for errors. |
| `sfc /scannow` | Scan and repair protected Windows system files. |
| `diskpart` | Manage disks and partitions. |

**Warning:** `diskpart` can modify or erase disk partitions. Use it carefully.

Some operations require administrator privileges.

## 11. Useful Operators

| Operator | Description | Example |
|---|---|---|
| `\|` | Send output to another command. | `tasklist \| findstr chrome` |
| `>` | Save output to a file, overwriting existing content. | `ipconfig > net.txt` |
| `>>` | Append output to a file. | `whoami >> info.txt` |
| `&&` | Run the next command if the previous command succeeds. | `cd C:\ && dir` |

## 12. PowerShell Quick Start

PowerShell is a more advanced command-line shell than CMD. It provides additional commands called cmdlets.

| Command | Description |
|---|---|
| `powershell` | Open PowerShell from CMD. |
| `Get-Process` | List running processes. |
| `Get-Service` | List services. |
| `Get-LocalUser` | List local user accounts. |
| `Get-ChildItem` | List files and directories. |
| `Get-Help <cmdlet>` | Display help for a PowerShell command. |

## Learning Resources

- [Microsoft Learn – Windows Commands](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [Microsoft Learn – PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)
- [TryHackMe](https://tryhackme.com/) – Practice Windows enumeration and system administration in hands-on labs.
- [Cisco Networking Academy](https://www.netacad.com/) – Learn networking fundamentals.

---

**Note:** These commands are documented for educational purposes, Windows administration, and authorized cybersecurity labs. Some commands require administrator privileges.
