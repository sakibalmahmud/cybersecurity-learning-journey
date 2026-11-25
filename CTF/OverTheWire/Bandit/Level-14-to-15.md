# Bandit

## Level 14 → Level 15

### Level Goal

The password for the next level can be retrieved by submitting the current level's password to **port 30000 on localhost**.

### Step 1: Log in to Bandit14

First, I logged in to Bandit Level 14 using the SSH private key obtained from the previous level.

### Step 2: Read the Current Password

The current level's password is stored in:

```bash
/etc/bandit_pass/bandit14
```

I used the following command to read it:

```bash
cat /etc/bandit_pass/bandit14
```

This returned the password for Bandit Level 14.

### Step 3: Connect to Port 30000

I used Netcat (`nc`) to connect to port 30000 on localhost:

```bash
nc localhost 30000
```

After establishing the connection, I submitted the current level's password.

### Step 4: Retrieve the Next Password

After submitting the correct password, the server returned the password for Bandit Level 15.

### What I Learned

- How to read password files using `cat`.
- What localhost (`127.0.0.1`) means.
- How to connect to a specific port using Netcat.
- How to send data to a network service through a TCP connection.

### Key Takeaway

Netcat (`nc`) is a networking utility that can establish connections to remote or local hosts and send or receive data through network ports.
