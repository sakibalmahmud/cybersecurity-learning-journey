# Introduction to Domain Names

**Details:** https://tryhackme.com/room/dnsindetail

A **Domain Name** is a human-readable name that identifies a website or other internet service.

It works as a human-readable address instead of requiring users to remember an IP address.

**Example:**

`google.com`

Instead of remembering Google's IP address, we can simply type `google.com` into our browser.

## Structure of a Domain Name

A domain name has different parts:

### 1. Top-Level Domain (TLD)

* The last part of a domain name.
* It appears after the final dot.

**Examples:** `.com`, `.edu`, `.org`, `.net`, `.gov`

### 2. Second-Level Domain (SLD)

* The main registered part of a domain name.
* It appears immediately before the TLD.

**Example:**

`google.com`

* `google` = Second-Level Domain
* `.com` = Top-Level Domain

### 3. Subdomain

* A part added before the main domain.
* Used to organize different services or sections of a website.

**Example:**

`mail.google.com`

* `mail` = Subdomain
* `google` = Second-Level Domain
* `.com` = Top-Level Domain

Other examples:

* `blog.example.com`
* `shop.example.com`
* `support.example.com`

---

# Introduction to DNS (Domain Name System)

**DNS (Domain Name System)** translates domain names into IP addresses so that browsers and other applications can communicate with the correct servers.

For example:

When you type:

`google.com`

The DNS system helps find the IP address associated with that domain name.

Without DNS, users would need to remember IP addresses to access websites.

## How DNS Works

DNS follows a process known as **DNS Resolution**.

When you enter a domain name into your browser:

1. Your computer checks its local DNS cache to see whether it already knows the IP address.
2. If the address is not available, the request goes to a DNS Resolver.
3. The Resolver contacts a Root DNS Server if necessary.
4. The Root Server directs the Resolver to the appropriate TLD DNS Server.
5. The TLD Server provides information about the domain's Authoritative DNS Server.
6. The Authoritative DNS Server provides the requested DNS record, such as the IP address.
7. The Resolver returns the result to your computer.
8. Your browser uses the IP address to connect to the website.

**Note:** DNS caching can reduce the number of queries required. Not every DNS lookup needs to contact all four types of DNS servers.

---

# DNS Servers

A **DNS Server** is a computer or server that responds to DNS queries and helps resolve domain names into IP addresses or other DNS records.

## Types of DNS Servers

### 1. DNS Resolver

* Usually provided by an ISP or a public DNS provider.
* Receives DNS queries from clients.
* Finds the requested DNS information by contacting other DNS servers when necessary.
* Can cache DNS responses to make future queries faster.

### 2. Root DNS Server

* The starting point of the DNS hierarchy.
* Directs DNS resolvers to the appropriate TLD DNS Server.
* Does not normally provide the final IP address of a website.

### 3. TLD DNS Server

* Manages information about a specific Top-Level Domain.
* Directs resolvers to the Authoritative DNS Server for a domain.

**Examples:** `.com`, `.org`, `.net`

### 4. Authoritative DNS Server

* Stores the official DNS records for a domain.
* Provides the requested DNS information, such as A, AAAA, MX, and other records.
* Contains the authoritative information for the domain.

---

# DNS Records

A **DNS Record** is a piece of information stored in DNS that tells the internet how a domain name should work.

DNS records connect a domain name to the correct service, such as a website or email server.

## Common Types of DNS Records

### 1. A Record

* Maps a domain name to an IPv4 address.

**Example:**

`example.com → 93.184.216.34`

### 2. AAAA Record

* Maps a domain name to an IPv6 address.

### 3. CNAME Record

* Creates an alias that points one domain name to another domain name.

**Example:**

`www.example.com → example.com`

### 4. MX Record

* Specifies the mail servers responsible for receiving emails for a domain.

### 5. TXT Record

* Stores text information associated with a domain.
* Commonly used for domain verification and email security configurations such as SPF and DKIM.

### 6. NS Record

* Identifies the authoritative DNS servers for a domain.

### 7. PTR Record

* Used for reverse DNS lookups.
* Maps an IP address back to a domain name.

### 8. SOA Record

* Contains administrative information about a DNS zone.
* Includes information such as the primary authoritative server and zone serial number.

---

# DNS Ports and Protocols

DNS mainly uses port **53**.

* **UDP Port 53:** Commonly used for standard DNS queries and responses.
* **TCP Port 53:** Used for larger responses, zone transfers, and other DNS operations.

DNS normally uses UDP for regular queries because it is faster and has less overhead.

---

# Useful DNS Commands in Kali Linux

We can use different Linux commands to investigate DNS information.

### 1. Check DNS Records Using dig

```bash
dig example.com
```

This displays DNS query information and the returned answer.

### 2. Find Only the IPv4 Address

```bash
dig example.com A
```

### 3. Find the IPv6 Address

```bash
dig example.com AAAA
```

### 4. Find Mail Server Information

```bash
dig example.com MX
```

### 5. Find Name Servers

```bash
dig example.com NS
```

### 6. Use nslookup

```bash
nslookup example.com
```

This performs a DNS lookup and displays the returned information.

### 7. Use host

```bash
host example.com
```

This provides basic DNS information about a domain.

---

# Practical Learning

Try these activities to understand Domain Names and DNS better:

1. Understand the difference between a domain name and an IP address.
2. Identify the TLD, SLD, and Subdomain of a website.
3. Use `dig` to find the IPv4 and IPv6 addresses of a domain.
4. Find the MX records of a domain.
5. Identify the authoritative name servers using an NS lookup.
6. Understand how Root, TLD, and Authoritative DNS servers work together.
7. Practice DNS queries using Kali Linux.
8. Complete the DNS in Detail room on TryHackMe.

**Practice DNS enumeration only on domains and networks where you have permission.**
