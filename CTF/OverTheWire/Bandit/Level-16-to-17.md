# Bandit

## Level 16 → Level 17

### Level Goal

The credentials for the next level can be retrieved by submitting the current level's password to a port on localhost in the range **31000–32000**.

First, identify which ports have listening services. Then determine which services support SSL/TLS encryption.

### Step 1: SSH Login

First, I logged in to Bandit Level 16 using the password obtained from the previous level.

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

### Step 2: Scan the Port Range Using Nmap

I used Nmap to scan ports between 31000 and 32000 on localhost and identify the running services.

```bash
nmap -sV -p 31000-32000 localhost
```

**Scan Results:**

```text
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

### Step 3: Identify the SSL/TLS Service

From the scan results, I identified two SSL/TLS-enabled services:

- Port `31518`
- Port `31790`

I used OpenSSL to connect to port `31790`:

```bash
openssl s_client -connect localhost:31790 -quiet
```

After establishing the SSL/TLS connection, I submitted the current Bandit Level 16 password.

The server returned an SSH private key for the next level.

### Step 4: Save the SSH Private Key

I copied the returned private key into a file on my Kali Linux machine using Nano:

```bash
nano bandit17.key
```

Then, I changed the file permissions to protect the private key:

```bash
chmod 600 bandit17.key
```

### Step 5: SSH Login Using the Private Key

Finally, I used the private key to authenticate and log in to Bandit Level 17:

```bash
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

Successfully logged in to Bandit Level 17.

### What I Learned

- How to scan a specific port range using Nmap.
- How to identify running services with `-sV`.
- How to identify SSL/TLS-enabled services.
- How to establish an encrypted connection using OpenSSL.
- How to save an SSH private key using Nano.
- Why `chmod 600` is important for private key permissions.
- How to authenticate using an SSH private key.

### Key Takeaway

Nmap helps identify open ports and running services, while OpenSSL can establish secure connections to SSL/TLS-enabled services. SSH private keys can then be used for secure authentication.
