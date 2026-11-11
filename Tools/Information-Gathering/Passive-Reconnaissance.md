# Passive Reconnaissance – Information Gathering

## 1. Introduction

Passive Reconnaissance refers to gathering information about a target using publicly available sources without directly interacting with the target's systems.

It helps security professionals collect information about domains, IP addresses, DNS records, subdomains, and internet-facing assets.

**Main Objectives:**
- Gather domain registration information.
- Identify DNS records.
- Discover subdomains.
- Collect information about public IP addresses.
- Identify internet-facing services.
- Gather publicly available information about a target.

## 2. Key Tools and Techniques

### A. WHOIS

WHOIS is a protocol used to retrieve domain registration information.

**Information Available:**
- Domain registrar
- Registration date
- Expiration date
- Name servers
- Registrant information (if publicly available)

**Command:**

```bash
whois example.com
```

### B. RDAP (Registration Data Access Protocol)

RDAP is a modern protocol used to retrieve domain registration information in a structured JSON format.

**Command:**

```bash
curl -s https://rdap.verisign.com/com/v1/domain/example.com | jq
```

**Explanation:**
- `curl` → Retrieves data from a URL.
- `-s` → Runs in silent mode.
- `jq` → Formats and displays JSON output.

**Note:** This particular RDAP endpoint is for `.com` domains.

### C. NSLOOKUP

`nslookup` is a command-line tool used to query DNS servers and retrieve DNS records.

**Basic Command:**

```bash
nslookup example.com
```

**Query a Specific DNS Record:**

```bash
nslookup -type=TYPE DOMAIN_NAME 1.1.1.1
```

Example:

```bash
nslookup -type=MX example.com 1.1.1.1
```

**Common DNS Record Types:**

| Record | Purpose |
|---|---|
| A | Maps a domain to an IPv4 address |
| AAAA | Maps a domain to an IPv6 address |
| MX | Identifies mail servers |
| TXT | Stores text information, often used for SPF and verification |
| CNAME | Creates an alias for another domain |
| SOA | Contains DNS zone authority information |
| NS | Identifies authoritative name servers |

### D. DIG

`dig` (Domain Information Groper) is a DNS lookup utility used to query DNS servers and retrieve detailed DNS information.

**Basic Command:**

```bash
dig example.com
```

**Query a Specific DNS Server:**

```bash
dig @1.1.1.1 example.com A
```

**Query Different DNS Records:**

```bash
dig @1.1.1.1 example.com MX
dig @1.1.1.1 example.com TXT
dig @1.1.1.1 example.com NS
dig @1.1.1.1 example.com SOA
```

**Useful Options:**

| Option | Purpose |
|---|---|
| `+short` | Displays short output |
| `+noall` | Hides all output sections |
| `+answer` | Displays only the answer section |
| `-x` | Performs a reverse DNS lookup |

### E. DNSDumpster

[DNSDumpster](https://dnsdumpster.com/) is an online domain research tool used to discover DNS information and potential subdomains.

**Main Uses:**
- Subdomain discovery
- DNS record collection
- Identifying associated IP addresses
- Viewing DNS infrastructure information

**How to Use:**
1. Visit the DNSDumpster website.
2. Enter the target domain.
3. Start the search.
4. Review the discovered subdomains and DNS information.

### F. Shodan

[Shodan](https://www.shodan.io/) is a search engine for internet-connected devices and services.

It helps security researchers gather intelligence about internet-facing assets.

**Main Uses:**
- Discovering publicly exposed services.
- Identifying open ports.
- Finding internet-connected devices.
- Identifying software and service versions.
- Collecting information about public IP addresses.

**Search Examples:**

```text
hostname:example.com
```

```text
ip:192.0.2.1
```

```text
port:22
```

**TryHackMe Room:** [Shodan](https://tryhackme.com/room/shodan)

### G. Google Dorking

Google Dorking is a technique that uses advanced Google search operators to find publicly indexed information.

**Useful Search Operators:**

| Operator | Purpose |
|---|---|
| `site:` | Search within a specific website |
| `filetype:` | Search for specific file types |
| `intitle:` | Search for terms in page titles |
| `inurl:` | Search for terms in URLs |
| `intext:` | Search for terms within page content |
| `-` | Exclude specific terms |

**Examples:**

Find indexed pages from a domain:

```text
site:example.com
```

Find PDF documents:

```text
site:example.com filetype:pdf
```

Find pages containing a specific word in their title:

```text
site:example.com intitle:login
```

## 3. Installation on Kali Linux

Install the required command-line tools:

```bash
sudo apt update
sudo apt install whois dnsutils curl jq -y
```

Check available commands:

```bash
whois --version
nslookup -version
dig -v
curl --version
jq --version
```

## 4. Important Notes

- Passive reconnaissance primarily uses publicly available information.
- WHOIS and RDAP provide domain registration details.
- NSLOOKUP and DIG are used for DNS queries.
- DNSDumpster helps discover subdomains.
- Shodan helps identify internet-facing services.
- Google Dorking helps locate publicly indexed information.
- DNS queries are sent to DNS resolvers, so passive reconnaissance does not necessarily mean that no external system receives a request.

## 5. Learning Resources

- [TryHackMe – Shodan](https://tryhackme.com/room/shodan)
- [DNSDumpster](https://dnsdumpster.com/)
- [Shodan](https://www.shodan.io/)
- [Google Search Operators](https://support.google.com/websearch/answer/2466433)
- [RDAP](https://www.icann.org/rdap)

---

**Disclaimer:** Use reconnaissance techniques responsibly and only for legitimate security research and authorized assessments.
