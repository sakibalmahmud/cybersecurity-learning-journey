# SMB – Ports 139/445

**Port:** 139/TCP, 445/TCP  
**Service:** Server Message Block (SMB)

SMB is used for sharing files, printers, and resources between systems, mostly on Windows networks.

### 1. Enumeration

`enum4linux -a <IP>` : Enumerate shares, users, OS information, and policies.

`smbclient -L //<IP>/` : List available SMB shares.

`smbclient //<IP>/IPC$` : Connect to the IPC$ share (anonymous access may be allowed).

`rpcclient -U "" <IP>` : Connect using a null session to query users and other information.

`crackmapexec smb <IP> --shares -u '' -p ''` : Check available shares using blank credentials.

### 2. Accessing Shares

`smbclient //<IP>/<share> -U Anonymous` : Connect anonymously to a specific share.

`smbclient //<IP>/<share> -U <username>` : Connect using a known username.

`smbclient -p <port> //<IP>/<share> -U <username>` : Connect using a non-default port.

### 3. Exploring Shares

After successful connection, use:

- `ls` : List files and directories.
- `pwd` : Show current directory.
- `cd <directory>` : Change directory.
- `get <filename>` : Download a file.
- `mget *` : Download multiple files.
- `put <filename>` : Upload a file (if permitted).
- `exit` : Disconnect from the share.

### 4. Analyze Downloaded Files

Check downloaded files for interesting information, credentials, configuration files, and flags.

`file <filename>` : Identify the file type.

`strings <filename>` : Extract readable text from a file.

**Why it works:** SMB servers may be misconfigured to allow null sessions, anonymous access, or weak credentials. This can expose shares, users, and sensitive files without proper authentication.

**Note:** Port 139 and 445 being open does not guarantee anonymous access. Always check share permissions and authentication requirements.
