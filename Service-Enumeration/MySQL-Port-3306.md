# MySQL – Port 3306

**Port:** 3306/TCP  
**Service:** MySQL Database Server

### 1. Enumeration

- `nmap -sV -sC -p 3306 <IP>` : Identify MySQL version and run default scripts.
- `nmap -T4 -A -p- <IP>` : Scan all TCP ports and identify services (more comprehensive scan).

### 2. Connecting to MySQL

- `mysql -h <IP> -u root -p` : Connect using the root username; enter the password when prompted.
- `mysql -h <IP> --ssl-mode=DISABLED -u root -p` : Try without SSL if the client/server SSL configuration causes connection issues.

**Note:** Some MariaDB clients use `--skip-ssl` instead of `--ssl-mode=DISABLED`.

### 3. Post-Authentication Enumeration (Metasploit)

Start Metasploit: `msfconsole`

**Run SQL queries:**

- `use auxiliary/admin/mysql/mysql_sql`
- Set `RHOSTS`, `USERNAME`, `PASSWORD`, and `SQL`.
- `set SQL show databases;`
- `run`

**Dump database schema:**

- `use auxiliary/scanner/mysql/mysql_schemadump`
- Set `RHOSTS`, `USERNAME`, and `PASSWORD`.
- `run`

**Dump MySQL password hashes:**

- `use auxiliary/scanner/mysql/mysql_hashdump`
- Set `RHOSTS`, `USERNAME`, and `PASSWORD`.
- `run`

### 4. Cracking MySQL Hashes

- `nano hash.txt` : Create a file and save the hashes in the format returned by the module.
- `john --format=mysql-sha1 hash.txt` : Attempt to crack MySQL SHA-1 password hashes.
- `john --show --format=mysql-sha1 hash.txt` : Display successfully cracked passwords.

**Note:** The correct John format depends on the MySQL hash type. Check the hash format before cracking.

### 5. Testing Credential Reuse

- `ssh <username>@<IP>` : Test the recovered credentials against SSH only if you have reason to suspect password reuse and the username is a valid system account.

**Why it works:** Weak or reused database credentials can expose sensitive information. MySQL hash dumping may reveal database password hashes, but those hashes are not automatically Linux/SSH credentials. SSH access requires a valid system account and matching password.
