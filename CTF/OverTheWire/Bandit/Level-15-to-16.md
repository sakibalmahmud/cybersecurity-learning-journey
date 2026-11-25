# Bandit

## Level 15 → Level 16

### Level Goal

The password for the next level can be retrieved by submitting the current level's password to **port 30001 on localhost** using SSL/TLS encryption.

### Step 1: Log in to Bandit15

First, I logged in to Bandit Level 15 using the password obtained from the previous level.

### Step 2: Establish an SSL/TLS Connection

For this level, I used the `openssl` command to establish a secure connection with the server.

```bash
openssl s_client -connect localhost:30001
```

This command connects to port `30001` on localhost using SSL/TLS encryption.

### Step 3: Submit the Current Password

After establishing the connection, I submitted the current Bandit Level 15 password.

### Step 4: Retrieve the Next Password

After submitting the correct password, the server returned the password for Bandit Level 16.

### What I Learned

- What SSL/TLS encryption is.
- How to establish a secure connection using OpenSSL.
- How to connect to a specific localhost port.
- How to submit data through an encrypted connection.

### Key Takeaway

OpenSSL provides tools for establishing and testing secure connections using SSL/TLS protocols. The `s_client` command is useful for connecting to SSL/TLS-enabled services and inspecting their certificates and connection details.
