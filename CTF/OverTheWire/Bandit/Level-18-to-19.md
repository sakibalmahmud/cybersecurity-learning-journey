# Bandit

## Level 18 → Level 19

### Level Goal

The password for the next level is stored in a file named `readme` in the home directory.

Unfortunately, someone has modified the `.bashrc` file to log users out when they connect through SSH.

### Step 1: Read the Level Goal

After reviewing the Level Goal, I understood that a normal SSH login would not work because the modified `.bashrc` file immediately terminates the session.

Instead of opening an interactive shell, I decided to execute a command directly through SSH.

### Step 2: Read the `readme` File

I used the following command to connect to Bandit18 and read the `readme` file directly:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

The command executed successfully and displayed the password for Bandit Level 19.

### Step 3: Log in to Bandit19

I used the newly obtained password to log in to Bandit Level 19.

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

### What I Learned

- What the `.bashrc` file does.
- How SSH remote command execution works.
- How to execute a command without opening an interactive shell.
- How to read a remote file using SSH.

### Key Takeaway

SSH allows users to execute commands directly on a remote system without starting an interactive shell.

This technique is useful when the normal login shell is restricted or unavailable.
