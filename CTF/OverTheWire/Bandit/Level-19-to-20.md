##### Level Goal

To gain access to the next level, you should use the SetUID binary in the home directory. Execute it without arguments to find out how to use it.

The password for the next level can be found in the usual location:

`/etc/bandit_pass/bandit20`

##### Step 1: Login and Explore

Login to Bandit19 and list the files in the home directory.

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

```bash
ls -la
```

##### Step 2: Identify the SUID Binary

We find a binary named:

```bash
bandit20-do
```

Execute it without arguments to see its usage instructions:

```bash
./bandit20-do
```

##### Step 3: Read the Next Level Password

The `bandit20-do` binary allows us to execute commands with the privileges of its owner, `bandit20`.

Use it to read the next level's password:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

##### What I Learned

- **SUID (Set User ID):** A special Linux permission that allows an executable to run with the file owner's privileges.
- **SUID Binary:** An executable file with the SUID permission enabled.
- **Privilege Escalation:** Using a program's elevated privileges to access resources that the current user normally cannot access.

**Key takeaway:** The `bandit20-do` binary lets `bandit19` execute a command with `bandit20` privileges.
