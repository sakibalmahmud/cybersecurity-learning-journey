# Bandit

## Level 13 → Level 14

### Level Goal

The password for the next level is not directly provided. Instead, a private SSH key is available in the home directory.

Use the private SSH key to log in to the next level.

### Step 1: SSH Login

First, I used the password obtained from Level 12 to log in to Bandit Level 13.

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

### Step 2: List Files

After logging in, I used the following command to list all files, including hidden files:

```bash
ls -la
```

I found two important files:

- `HINT`
- `sshkey.private`

The file permissions and ownership showed:

```text
-rw-r----- 1 bandit14 bandit13 467 Oct 25 13:37 HINT
-rw-r----- 1 bandit14 bandit13 2602 Oct 25 13:37 sshkey.private
```

### Step 3: Read the Hint

I used the `cat` command to read the hint:

```bash
cat HINT
```

Then, I copied the private SSH key to my local Kali Linux machine.

### Step 4: SSH Login Using the Private Key

First, I changed the private key permissions:

```bash
chmod 600 sshkey.private
```

Then, I used the private key to log in to Bandit Level 14:

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

### What I Learned

- How to identify important files using `ls -la`.
- How to inspect file contents using `cat`.
- What an SSH private key is.
- How to use the `-i` option to authenticate using a private SSH key.
- Why private key file permissions matter.

### Key Takeaway

SSH supports authentication using private and public key pairs. Instead of entering a password, we can use a private key to authenticate with a remote server.
