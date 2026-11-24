# Basic Linux Commands

A collection of useful Linux commands for beginners, system administration, networking, and cybersecurity practice.

## 1. User and System Information

### 1. `whoami`
```bash
whoami
```
Displays the username of the currently logged-in user.

### 2. `uname`
```bash
uname -a
```
Displays complete system information, including the kernel name, hostname, kernel version, and system architecture.

### 3. `hostname`
```bash
hostname
```
Displays the system's hostname.

### 4. `id`
```bash
id
```
Displays the current user's UID, GID, and group memberships.

### 5. `who`
```bash
who
```
Displays information about currently logged-in users.

### 6. `pwd`
```bash
pwd
```
Displays the current working directory or location.

---

## 2. Getting Help and Command Manuals

### 7. `help`
```bash
help
```
Displays information about Bash built-in commands.

Example:
```bash
help cd
```

### 8. `man`
```bash
man ls
```
Displays the manual page of a command.

Example:
```bash
man mkdir
```

Press `q` to exit the manual.

### 9. `--help`
```bash
ls --help
```
Displays a brief help message explaining a command's available options and usage.

---

## 3. File and Directory Management

### 10. `ls`
```bash
ls
```
Lists files and directories in the current directory.

Useful options:
```bash
ls -l
ls -a
ls -lh
ls -la
```
- `-l` — Displays detailed information.
- `-a` — Displays hidden files and directories.
- `-h` — Displays file sizes in a human-readable format.
- `-la` — Displays all files in detailed format.

### 11. `cd`
```bash
cd /path/to/directory
```
Changes the current working directory.

Examples:
```bash
cd Documents
cd ..
cd ~
cd /
```
- `cd ..` — Moves one directory backward.
- `cd ~` — Moves to the home directory.
- `cd /` — Moves to the root directory.

### 12. `mkdir`
```bash
mkdir foldername
```
Creates a new directory.

Example:
```bash
mkdir projects
```

To create multiple directories:
```bash
mkdir folder1 folder2 folder3
```

To create parent directories if they do not exist:
```bash
mkdir -p parent/child
```

### 13. `touch`
```bash
touch file.txt
```
Creates an empty file if it does not exist. If the file already exists, it updates its timestamps.

### 14. `cp`
```bash
cp file.txt backup.txt
```
Copies a file from one location to another.

To copy a directory:
```bash
cp -r folder1 folder2
```

### 15. `mv`
```bash
mv oldname.txt newname.txt
```
Moves or renames files and directories.

### 16. `rm`
```bash
rm file.txt
```
Removes a file.

To remove a directory and its contents:
```bash
rm -r foldername
```

Use `rm` carefully because deleted files may not be recoverable.

### 17. `cat`
```bash
cat file.txt
```
Displays the contents of a file.

To display multiple files:
```bash
cat file1.txt file2.txt
```

### 18. `less`
```bash
less file.txt
```
Displays file contents page by page. Press `q` to exit.

### 19. `head`
```bash
head file.txt
```
Displays the first 10 lines of a file.

To display a specific number of lines:
```bash
head -n 5 file.txt
```

### 20. `tail`
```bash
tail file.txt
```
Displays the last 10 lines of a file.

To monitor a file continuously:
```bash
tail -f file.txt
```

---

## 4. File Editing

### 21. `gedit`
```bash
gedit index.html
```
Opens `index.html` in the Gedit graphical text editor for editing.

If Gedit is not installed, you can use another editor, such as Nano:
```bash
nano index.html
```

---

## 5. File Permissions and Ownership

### 22. `chmod`
```bash
chmod 755 file.sh
```
Changes the permissions of a file or directory.

### 23. `chown`
```bash
sudo chown username:groupname file.txt
```
Changes the owner and group of a file.

---

## 6. Network Interface and MAC Address Management

### 24. `ifconfig`
```bash
ifconfig
```
Displays network interface information, including IP addresses and network details.

To display a specific interface:
```bash
ifconfig eth0
```

Note: `ifconfig` is an older networking command. Modern Linux systems generally use the `ip` command.

### 25. Disable a Network Interface
```bash
sudo ifconfig eth0 down
```
Disables the `eth0` network interface.

### 26. Change the MAC Address
```bash
sudo ifconfig eth0 hw ether aa:0c:29:74:39:c4
```
Changes the MAC address of the `eth0` interface.

Manual process:

1. Disable the interface.
2. Change the MAC address.
3. Enable the interface again.

### 27. Enable a Network Interface
```bash
sudo ifconfig eth0 up
```
Enables the `eth0` network interface.

### Modern Alternative: `ip`

Display network interfaces:
```bash
ip addr
```

Disable an interface:
```bash
sudo ip link set eth0 down
```

Change its MAC address:
```bash
sudo ip link set eth0 address aa:0c:29:74:39:c4
```

Enable the interface:
```bash
sudo ip link set eth0 up
```

---

## 7. Service Management

### 28. `service`
Starts, stops, and manages system services.

Start Apache:
```bash
sudo service apache2 start
```

Stop Apache:
```bash
sudo service apache2 stop
```

Restart Apache:
```bash
sudo service apache2 restart
```

Check Apache status:
```bash
sudo service apache2 status
```

### Modern Alternative: `systemctl`

Start a service:
```bash
sudo systemctl start apache2
```

Stop a service:
```bash
sudo systemctl stop apache2
```

Restart a service:
```bash
sudo systemctl restart apache2
```

Check service status:
```bash
sudo systemctl status apache2
```

Enable a service at system startup:
```bash
sudo systemctl enable apache2
```

Disable automatic startup:
```bash
sudo systemctl disable apache2
```

---

## 8. Cron Jobs and Task Scheduling

### 29. `crontab -e`
```bash
crontab -e
```
Opens the current user's cron table for editing.

Cron is used to schedule commands or scripts to run automatically at specific times.

Cron syntax:
```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of the week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of the month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

Examples:

Run a command every minute:
```bash
* * * * * command
```

Run a command every day at 8:00 AM:
```bash
0 8 * * * command
```

Run a command every Sunday at midnight:
```bash
0 0 * * 0 command
```

List scheduled cron jobs:
```bash
crontab -l
```

Remove all cron jobs for the current user:
```bash
crontab -r
```

---

## 9. Searching Text with Grep

### 30. `grep`
```bash
grep "password123" passwords.txt
```
Searches for a specific text or pattern inside a file.

Useful options:

- `-i` — Ignores uppercase and lowercase differences.
- `-n` — Displays line numbers.
- `-r` — Searches recursively inside directories.
- `-R` — Searches recursively and follows symbolic links.
- `-l` — Displays only filenames containing matches.
- `-o` — Displays only the matching part.
- `-E` — Enables extended regular expressions.

Examples:

Search for a keyword:
```bash
grep "academy" filename
```

Search without case sensitivity and display line numbers:
```bash
grep -in "academy" filename
```

Search recursively inside a directory:
```bash
grep -Rin "academy{" /path/to/directory
```

Display only filenames containing the keyword:
```bash
grep -iRl "academy" /path/to/directory
```

Extract unique flag patterns:
```bash
grep -oE 'academy\{[^}]+\}' filename | sort -u
```

Search for a keyword directly inside a log file:
```bash
grep "FLAGPART" server.log
```

---

## 10. Finding Files and Directories

### 31. `find`
```bash
find
```
Searches for files and directories. Without additional options, it searches from the current directory.

Find a file by name:
```bash
find -name passwords.txt
```

Find a specific file in a directory:
```bash
find /home/dir -type f -name example.txt
```

Find files of a specific size:
```bash
find /directory/path -type f -size 1033c
```

Find files of exactly 1033 bytes that are not executable:
```bash
find /home/bandit5 -type f -size 1033c ! -executable
```

Find a file based on its owner, group, and size:
```bash
find / -type f -user bandit7 -group bandit6 -size 33c
```

Find files while suppressing permission errors:
```bash
find /directory/path -type f -size [size] 2>/dev/null
```

Find files modified within a date range:
```bash
find /directory/path -type f -newermt "[start date]" ! -newermt "[end date]"
```

Find files whose names start with `flag`:
```bash
find / -name "flag*" 2>/dev/null
```

Useful `find` options:

- `-name` — Searches by filename.
- `-type f` — Searches for regular files.
- `-type d` — Searches for directories.
- `-size` — Searches by file size.
- `-user` — Searches by file owner.
- `-group` — Searches by group.
- `-executable` — Finds executable files.
- `!` — Negates a condition.
- `2>/dev/null` — Hides error messages.

---

## 11. Sorting and Filtering Data

### 32. `sort`
```bash
sort data.txt
```
Sorts the lines of a file alphabetically or numerically.

### 33. `uniq`
```bash
uniq data.txt
```
Removes or identifies adjacent duplicate lines.

To display only lines that appear exactly once:
```bash
sort data.txt | uniq -u
```

Note: `uniq` works on adjacent duplicate lines. Using `sort` first helps group identical lines together.

---

## 12. Translating and Modifying Text with TR

### 34. `tr`
```bash
tr [options] [set1] [set2]
```
The `tr` command translates, replaces, or deletes characters from standard input.

Translate lowercase letters into uppercase:
```bash
cat file.txt | tr '[:lower:]' '[:upper:]'
```

A simpler alternative:
```bash
tr '[:lower:]' '[:upper:]' < file.txt
```

Translate uppercase letters into lowercase:
```bash
tr '[:upper:]' '[:lower:]' < file.txt
```

ROT13 character translation:
```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

ROT13 replaces each letter with the letter 13 positions ahead in the alphabet.

Squeeze repeated spaces:
```bash
tr -s ' ' < file.txt
```

Useful `tr` options:

- `-d` — Deletes specified characters.
- `-s` — Replaces repeated characters with a single occurrence.
- `-c` — Uses the complement of the specified character set.

---

## 13. Text Processing with AWK

### 35. `awk`

`awk` is a text-processing command used for printing, searching patterns, and extracting specific fields from files.

Print the entire contents of a file:
```bash
awk '{ print }' file.txt
```

Find lines containing a specific pattern:
```bash
awk '/ctf/' file.txt
```

Print the first and fourth columns with a colon separator:
```bash
awk 'BEGIN{OFS=":"} {print $1, $4}' awk.txt
```

Useful AWK concepts:

- `$0` — Represents the entire line.
- `$1` — Represents the first field.
- `$2` — Represents the second field.
- `NF` — Represents the number of fields.
- `NR` — Represents the current record or line number.
- `BEGIN` — Executes before processing input.
- `END` — Executes after processing input.

---

## 14. Network and Information Gathering Commands

### 36. `ping`
```bash
ping <destination>
```
Tests network connectivity between your system and another host.

Example:
```bash
ping 8.8.8.8
```

Stop the command using `Ctrl + C`.

### 37. `traceroute`
```bash
traceroute <destination>
```
Maps the network path that packets take to reach a destination.

Example:
```bash
traceroute 8.8.8.8
```

It helps identify the intermediate routers between your system and the destination.

### 38. `whois`
```bash
whois <domain>
```
Retrieves domain registration information, such as registrar, registration dates, and available ownership details.

Example:
```bash
whois example.com
```

It can also retrieve information about IP address allocations.

### 39. `dig`
```bash
dig <domain>
```
Queries DNS records and displays DNS-related information.

Example:
```bash
dig example.com
```

Query a specific DNS server:
```bash
dig example.com @<dns-server-ip>
```

Query a specific DNS record:
```bash
dig example.com MX
```

Other useful record types include:
- `A` — IPv4 address.
- `AAAA` — IPv6 address.
- `MX` — Mail server.
- `NS` — Name server.
- `TXT` — Text records.

### 40. `ip`
```bash
ip addr
```
Displays network interfaces and their IP addresses.

Display routing information:
```bash
ip route
```

### 41. `ss`
```bash
ss -tuln
```
Displays network sockets and listening ports.

Useful options:
- `-t` — TCP connections.
- `-u` — UDP connections.
- `-l` — Listening sockets.
- `-n` — Displays numerical addresses and port numbers.

---

## 15. File Type Identification

### 42. `file`
```bash
file file.txt
```
Identifies the actual file type and format.

It helps determine whether a file is text, an image, an executable, or another format.

---

## 16. Secure File Transfer

### 43. `scp`
```bash
scp [filename] [username]@[IP-address]:/[directory]
```
Securely transfers files between local and remote systems using SSH.

Upload a file to a remote machine:
```bash
scp file.txt username@192.168.1.10:/home/username/
```

Download a file from a remote machine:
```bash
scp username@192.168.1.10:/home/username/file.txt .
```

Copy a directory recursively:
```bash
scp -r foldername username@192.168.1.10:/home/username/
```

---

## 17. Process Management

### 44. `ps`
```bash
ps aux
```
Displays currently running processes.

### 45. `top`
```bash
top
```
Displays real-time system processes and resource usage, including CPU and memory.

### 46. `kill`
```bash
kill <PID>
```
Sends a signal to a process, usually requesting it to terminate.

Example:
```bash
kill 1234
```

### 47. `clear`
```bash
clear
```
Clears the terminal screen.

### 48. `history`
```bash
history
```
Displays previously executed commands in the terminal.

---

## 18. Disk and Storage Information

### 49. `df`
```bash
df -h
```
Displays available and used disk space on mounted filesystems.

### 50. `du`
```bash
du -sh foldername
```
Displays the total disk space used by a directory.

---

## 19. Package Management

### 51. `apt`
Updates package information:
```bash
sudo apt update
```

Upgrades installed packages:
```bash
sudo apt upgrade
```

Installs a package:
```bash
sudo apt install package-name
```

Removes a package:
```bash
sudo apt remove package-name
```

Searches for a package:
```bash
apt search package-name
```

---

## 20. Root Privileges

### 52. `sudo`
```bash
sudo command
```
Runs a command with administrative privileges.

Example:
```bash
sudo apt update
```

### 53. `su`
```bash
su
```
Switches to another user account. Without specifying a username, it attempts to switch to the root account.

---

**Important:** Some commands require administrative privileges. Network interface names such as `eth0` may differ between Linux systems. Always use these commands only on your own system or systems you are authorized to manage.
