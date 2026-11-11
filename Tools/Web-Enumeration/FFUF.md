# FFUF (Fuzz Faster U Fool)

## 1. Introduction

**FFUF (Fuzz Faster U Fool)** is a fast web fuzzing tool written in Go. It is used to discover hidden directories, files, virtual hosts, parameters, and other web resources.

FFUF uses wordlists and replaces the keyword `FUZZ` in a URL, header, or request body with different values to discover valid responses.

## 2. Main Uses

- Directory and file enumeration.
- Web content discovery.
- Parameter fuzzing.
- Virtual host discovery.
- Login form fuzzing.
- Identifying valid resource names and parameter values.

## 3. Installation (Kali Linux)

Install FFUF using APT:

```bash
sudo apt update
sudo apt install ffuf -y
```

Verify installation:

```bash
ffuf -V
```

Display help:

```bash
ffuf -h
```

### Wordlist Installation

Install SecLists:

```bash
sudo apt install seclists -y
```

Common wordlist locations:

**Directory and File Enumeration:**

```text
/usr/share/seclists/Discovery/Web-Content/
```

**Parameter Enumeration:**

```text
/usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt
```

**Password Testing:**

```text
/usr/share/seclists/Passwords/
```

## 4. Directory and File Enumeration

Directory enumeration helps discover hidden directories and files on a web server.

### Basic Directory Fuzzing

```bash
ffuf -u http://TARGET_IP/FUZZ -w /usr/share/seclists/Discovery/Web-Content/big.txt
```

Here:
- `-u` specifies the target URL.
- `FUZZ` is the keyword replaced by wordlist entries.
- `-w` specifies the wordlist.

### Using a Different Wordlist

```bash
ffuf -u http://TARGET_IP/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

### File Extension Fuzzing

```bash
ffuf -u http://TARGET_IP/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -e .php,.txt
```

The `-e` flag adds extensions to the wordlist entries.

### Finding Extensions for a Specific Page

```bash
ffuf -u http://TARGET_IP/indexFUZZ -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt
```

This tests different extensions for the `index` page.

### Searching for Files with Status Code 200

```bash
ffuf -u http://TARGET_IP/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -mc 200
```

The `-mc` flag matches responses with specific HTTP status codes.

## 5. Response Filtering and Matching

FFUF provides several options to filter or match HTTP responses.

| Flag | Description |
|---|---|
| `-mc` | Match specific HTTP status codes. |
| `-fc` | Filter specific HTTP status codes. |
| `-fs` | Filter responses by size in bytes. |
| `-fw` | Filter responses by word count. |
| `-fl` | Filter responses by line count. |
| `-fr` | Filter responses using a regular expression. |
| `-mr` | Match responses using a regular expression. |

Example:

```bash
ffuf -u http://TARGET_IP/FUZZ -w wordlist.txt -mc 200
```

This displays responses matching HTTP status code 200.

**Important:** Filtering options help remove irrelevant responses. Always check the normal response first to understand the website's default behaviour.

## 6. Parameter Fuzzing

Parameter fuzzing is used when we discover a webpage or API endpoint but do not know which parameters it accepts.

Discovering valid parameters can help identify potential vulnerabilities such as SQL injection, XSS, file inclusion, and command injection.

### Basic Parameter Fuzzing

```bash
ffuf -u 'http://TARGET_IP/sqli-labs/Less-1/?FUZZ=1' -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -fw 39
```

Here:
- `FUZZ` represents the parameter name being tested.
- `-c` enables coloured output.
- `-w` specifies the parameter wordlist.
- `-fw 39` filters responses containing 39 words.

**Note:** The value `39` is specific to the original lab response. Check the normal response first and adjust the filter accordingly.

## 7. ID Value Fuzzing

After discovering a parameter such as `id`, we can fuzz different values to identify valid IDs.

### Using seq

```bash
seq 0 255 | ffuf -u 'http://TARGET_IP/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33
```

Here:
- `seq 0 255` generates numbers from 0 to 255.
- `-w -` tells FFUF to read the wordlist from standard input (STDIN).
- `FUZZ` is replaced by each generated number.
- `-fw 33` filters responses containing 33 words.

### Using a Bash Loop

```bash
for i in {0..255}; do echo $i; done | ffuf -u 'http://TARGET_IP/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33
```

Both commands generate the same range of ID values.

## 8. POST Login Form Fuzzing

FFUF can also test login forms by sending POST requests with different password values.

### Basic POST Fuzzing Command

```bash
ffuf -u http://TARGET_IP/sqli-labs/Less-11/ -c -w /usr/share/seclists/Passwords/Leaked-Databases/hak5.txt -X POST -d 'uname=Dummy&passwd=FUZZ&submit=Submit' -fs 1435 -H 'Content-Type: application/x-www-form-urlencoded'
```

Explanation:

| Option | Description |
|---|---|
| `-u` | Target URL. |
| `-c` | Enable coloured output. |
| `-w` | Specify the password wordlist. |
| `-X POST` | Send a POST request. |
| `-d` | Specify POST request data. |
| `FUZZ` | Replace with each password candidate. |
| `-fs 1435` | Filter responses with a body size of 1435 bytes. |
| `-H` | Add an HTTP request header. |

**Important:** The username, form field names, and response size are specific to the lab. Inspect the actual login request and normal failure response before using this command.

## 9. Important FFUF Options

| Flag | Description |
|---|---|
| `-u` | Specify the target URL. |
| `-w` | Specify a wordlist. |
| `-e` | Add file extensions. |
| `-c` | Enable coloured output. |
| `-t` | Set the number of threads. |
| `-o` | Save results to a file. |
| `-of` | Specify output format, such as json or md. |
| `-X` | Specify HTTP request method. |
| `-d` | Send POST data. |
| `-H` | Add HTTP headers. |
| `-ac` | Enable automatic calibration. |

### Save Results to a File

```bash
ffuf -u http://TARGET_IP/FUZZ -w wordlist.txt -o results.json -of json
```

This saves the results in JSON format.

## 10. Important Concepts

**Gobuster vs FFUF**

| Feature | Gobuster | FFUF |
|---|---|---|
| Directory Enumeration | Yes | Yes |
| DNS Enumeration | Yes | No dedicated DNS mode |
| Parameter Fuzzing | Limited compared to FFUF | Yes |
| POST Request Fuzzing | Limited | Yes |
| Virtual Host Enumeration | Yes | Yes |
| Flexible HTTP Fuzzing | Limited | Yes |

## 11. Learning Resources

- [TryHackMe – FFUF Room](https://tryhackme.com/room/ffuf)
- [FFUF Official GitHub](https://github.com/ffuf/ffuf)
- [FFUF Documentation](https://github.com/ffuf/ffuf/wiki)
- [SecLists – GitHub](https://github.com/danielmiessler/SecLists)

---

**Note:** Use FFUF only against systems you own or have explicit permission to test. Password fuzzing and vulnerability testing should be performed only in authorized labs.
