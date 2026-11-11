# Gobuster

## 1. Introduction

**Gobuster** is a command-line tool written in Go that is used for discovering hidden directories, files, DNS subdomains, and virtual hosts on web servers.

It uses wordlists to identify resources that may not be directly visible on a website.

## 2. Main Uses

- **Directory Enumeration:** Discover hidden directories and files on a website.
- **DNS Enumeration:** Discover possible subdomains of a target domain.
- **Virtual Host Enumeration:** Discover virtual hosts running on a web server.

## 3. Installation (Kali Linux)

Install Gobuster using APT:

```bash
sudo apt update
sudo apt install gobuster -y
```

Verify the installation:

```bash
gobuster version
```

Display available commands:

```bash
gobuster help
```

### Wordlist Installation

Gobuster uses wordlists to discover directories, files, and subdomains.

Install SecLists:

```bash
sudo apt install seclists -y
```

Common wordlist locations:

**Directory Enumeration:**

```text
/usr/share/seclists/Discovery/Web-Content/
```

**DNS Enumeration:**

```text
/usr/share/seclists/Discovery/DNS/
```

You can also use DirBuster wordlists if they are installed:

```text
/usr/share/wordlists/dirbuster/
```

## 4. Directory Enumeration

Directory enumeration is used to discover hidden directories and files on a web server.

### Basic Command

```bash
gobuster dir -u http://TARGET_IP -w /usr/share/wordlists/dirb/common.txt
```

### Using File Extensions

```bash
gobuster dir -u http://TARGET_IP -w /usr/share/wordlists/dirb/common.txt -x php,txt,html
```

### Using SecLists Wordlist

```bash
gobuster dir -u http://TARGET_IP -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

### Important Flags

| Flag | Description |
|---|---|
| `dir` | Select directory enumeration mode. |
| `-u` | Specify the target URL. |
| `-w` | Specify the wordlist. |
| `-x` | Search for specific file extensions. |
| `-t` | Set the number of threads. |
| `-o` | Save output to a file. |

## 5. DNS Subdomain Enumeration

DNS enumeration is used to discover possible subdomains associated with a target domain.

### Basic Command

```bash
gobuster dns -d example.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

### Using Wildcard Option

```bash
gobuster dns -d example.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --wildcard
```

### Important Flags

| Flag | Description |
|---|---|
| `dns` | Select DNS enumeration mode. |
| `-d` | Specify the target domain. |
| `-w` | Specify the wordlist. |
| `-i` | Display IP addresses of discovered subdomains. |
| `-r` | Specify a custom DNS resolver. |
| `--wildcard` | Continue enumeration when wildcard DNS is detected. |

## 6. Virtual Host Enumeration

Virtual Host (VHost) enumeration is used to discover websites hosted on the same web server or IP address.

Unlike DNS enumeration, VHost enumeration sends HTTP requests using different Host headers.

### Basic Command

```bash
gobuster vhost -u http://TARGET_IP -w wordlist.txt
```

### With Domain Appending

```bash
gobuster vhost -u http://TARGET_IP --domain example.thm --append-domain -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

### Important Flags

| Flag | Description |
|---|---|
| `vhost` | Select virtual host enumeration mode. |
| `-u` | Specify the target URL or IP address. |
| `-w` | Specify the wordlist. |
| `--domain` | Specify the base domain. |
| `--append-domain` | Append the domain to each wordlist entry. |
| `--exclude-length` | Exclude responses with specified body lengths. |

## 7. Important Concepts

**Directory vs DNS vs VHost Enumeration**

| Enumeration Type | Purpose |
|---|---|
| Directory Enumeration | Finds hidden directories and files. |
| DNS Enumeration | Finds subdomains through DNS lookups. |
| VHost Enumeration | Finds virtual hosts using HTTP Host headers. |

**Example:**

- `example.thm/admin` → Directory
- `blog.example.thm` → Subdomain
- `admin.example.thm` hosted on the same IP but not publicly registered in DNS → Possible Virtual Host

## 8. Useful Learning Resource

- TryHackMe – Content Discovery
- Gobuster Official Documentation
- Kali Linux Tools Documentation

---

**Note:** Use Gobuster only against systems you own or have explicit permission to test.
