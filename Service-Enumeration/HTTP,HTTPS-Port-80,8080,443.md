# HTTP/HTTPS – Ports 80, 8080, 443

**Port 80:** HTTP  
**Port 8080:** Alternative HTTP (sometimes used for web applications or proxy services)  
**Port 443:** HTTPS

### 1. Initial Enumeration

- `nmap -sV -sC -p 80,443,8080 <IP>` : Identify web services, versions, and common vulnerabilities or misconfigurations.
- `whatweb http://<IP>` : Identify technologies used by the website.
- `curl -I http://<IP>` : Check HTTP response headers.

**Manually inspect the website:**

- `/robots.txt` : Check which paths the website allows or disallows search engine crawlers to access.
- `/admin` : Check for admin panels.
- `/login` : Check login pages.
- `/backup` : Check for exposed backup directories.
- `Ctrl + U` : View page source.
- `F12` : Open Developer Tools to inspect HTML, JavaScript, network requests, and other details.

### 2. Directory Enumeration – Port 80

- `gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt -t 5 -o gobuster-80.txt`

: Discover hidden directories and files on the HTTP service and save results.

### 3. Directory Enumeration – Port 8080

- `gobuster dir -u http://<IP>:8080 -w /usr/share/wordlists/dirb/common.txt -t 5 -o gobuster-8080.txt`

**Alternative SecLists wordlist:**

- `gobuster dir -u http://<IP>:8080 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 5 -o gobuster-8080.txt`

### 4. Directory Enumeration – Port 443

- `gobuster dir -u https://<IP> -w /usr/share/wordlists/dirb/common.txt -t 5 -k -o gobuster-443.txt`

: Enumerate directories over HTTPS.

**Note:** `-k` skips TLS certificate verification. It is useful in labs with self-signed or invalid certificates.

### 5. Virtual Host Enumeration

- `gobuster vhost -u http://<IP> -w /usr/share/seclists/Discovery
