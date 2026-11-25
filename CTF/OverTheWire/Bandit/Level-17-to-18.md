# Bandit

## Level 17 → Level 18

### Level Goal

There are two files in the home directory:

- `passwords.old`
- `passwords.new`

The password for the next level is stored in `passwords.new` and is the only line that has been changed between the two files.

### Step 1: SSH Login Using the Private Key

First, I used the SSH private key obtained from the previous level to access Bandit Level 17.

```bash
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

After logging in, I found two important files in the home directory:

```text
passwords.old
passwords.new
```

### Step 2: Compare the Two Files

I used the `diff` command to identify the differences between the two files.

```bash
diff passwords.old passwords.new
```

**Output:**

```text
42c42
< 1WJHmb0k7TH4piWp9Pd0lsruErLQZrR9
---
> OQxXZjELndr90zuhOTDYBEomI0SZITX
```

The output showed that line 42 was different between the two files.

The line marked with `>` represents the changed line in `passwords.new`.

Therefore, I obtained the password for Bandit Level 18.

### Step 3: Attempt SSH Login to Bandit18

I tried to log in to Bandit Level 18 using the newly obtained password.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

However, instead of getting an interactive shell, I received the following message:

```text
For support, questions or comments, contact us on discord or IRC.

Enjoy your stay!

Byebye!

Connection to bandit.labs.overthewire.org closed.
```

This indicates that the shell session is being terminated immediately.

This behavior is related to the next level's challenge.

### What I Learned

- How to compare two files using the `diff` command.
- How to identify modified lines between files.
- How to interpret `diff` output.
- How to troubleshoot unexpected SSH session behavior.

### Key Takeaway

The `diff` command compares two files line by line and displays their differences.

It is useful for identifying modified, added, or removed content between files.
