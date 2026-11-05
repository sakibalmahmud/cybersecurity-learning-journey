# FTP – Port 21

**Port:** 21/TCP  
**Service:** File Transfer Protocol (FTP)

### 1. Anonymous Login

First, check whether anonymous login is allowed.

`ftp <IP>`

**Username:** `anonymous`  
**Password:** `anonymous`

### 2. Explore Files

After successful login, use:

- `ls` — List files and directories.
- `pwd` — Show current directory.
- `cd <directory>` — Change directory.
- `get <file>` — Download a specific file.
- `mget *` — Download multiple files.

### 3. Analyze Downloaded Files

Use ExifTool to extract metadata:

`exiftool -u -a <filename>`

### 4. Brute Force (Hydra)

If anonymous login is disabled, test credentials using Hydra (authorized labs only).

`hydra -l admin -P /path/to/pass.txt ftp://<IP>`

### 5. Find Windows Flags

If you have Windows shell access, navigate to interesting directories:

`cd C:\Users\Administrator`

`dir`

Look for files like `user.txt`, `root.txt`, or `flag.txt`.

**Note:** FTP provides file transfer, not direct Windows CMD access.
