# SMTP – Port 25

**Port:** 25/TCP  
**Service:** Simple Mail Transfer Protocol (SMTP)

SMTP is used to send and relay emails between mail servers.

### 1. Enumeration

`nmap -sV -p 25 --script=smtp-* <IP>` : Detect SMTP service information and enumerate available features.

### 2. Connect to SMTP

`telnet <IP> 25` : Connect to the SMTP server and interact with it.

Useful SMTP commands:

- `EHLO example.com` : Identify yourself to the server.
- `VRFY username` : Check whether a user exists (if supported).
- `EXPN username` : Check mailing list members (if supported).
- `QUIT` : Close the connection.

### 3. Email Transaction

Useful commands for understanding SMTP communication:

- `MAIL FROM:<sender@example.com>` : Specify the sender.
- `RCPT TO:<recipient@example.com>` : Specify the recipient.
- `DATA` : Start entering the email content.
- `.` : End the email message.

### 4. User Enumeration

Use SMTP commands like `VRFY` and `EXPN` to check for valid usernames, if the server permits them.

### 5. Open Relay Testing

Check whether the SMTP server allows unauthorized email relaying. An open relay can be abused to send spam or phishing emails.

**Note:** Port 25 does not directly provide a reverse shell. SMTP misconfigurations may expose information or allow unauthorized email relaying, but additional vulnerabilities or user interaction would be required for code execution.
