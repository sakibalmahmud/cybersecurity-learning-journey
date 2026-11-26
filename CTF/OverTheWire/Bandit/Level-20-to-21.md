##### Level Goal

There is a SetUID binary in the home directory that connects to `localhost` on the port specified as a command-line argument.

It reads a line of text from the connection and compares it with the password of the previous level (`bandit20`). If the password is correct, it sends the password for the next level (`bandit21`).

##### Step 1: Login and Explore

Login to Bandit20 and check the files in the home directory.

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

```bash
ls -la
```

##### Step 2: Identify and Execute the Binary

We find a SUID binary named:

```bash
suconnect
```

Execute it without arguments to understand how it works:

```bash
./suconnect
```

##### Step 3: Start a Netcat Listener

Open a **new terminal**, log in to Bandit20 again, and start a Netcat listener on port `1234`.

```bash
nc -lvp 1234
```

The listener waits for an incoming connection.

##### Step 4: Connect Using the SUID Binary

Return to the first terminal and execute:

```bash
./suconnect 1234
```

The binary connects to the Netcat listener running on `localhost:1234`.

When the connection is established, enter the Bandit20 password in the listener terminal.

If the password is correct, the binary sends the Bandit21 password back through the connection.

##### Result

Successfully obtained the Bandit21 password using the SUID binary and Netcat.

##### What I Learned

- **SUID:** Allows an executable to run with its owner's privileges.
- **Netcat (`nc`):** A tool for creating network connections and listening on ports.
- **Listener:** Waits for incoming network connections.
- **Localhost:** Refers to the local machine (`127.0.0.1`).
- **Port:** Identifies a specific communication endpoint on a system.
- **Client-Server Communication:** One program can connect to another program listening on a specific port.
