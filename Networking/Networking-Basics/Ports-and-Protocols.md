# Network Ports and Protocols

A network port is like a "door" on a computer that allows data to enter or leave over a network.

More simply, a port identifies a specific service or application running on a device.

For example:

* Port 80 is commonly used by HTTP.
* Port 443 is commonly used by HTTPS.
* Port 22 is commonly used by SSH.

A port number helps the operating system deliver incoming network traffic to the correct application or service.

## Types of Network Ports

There are three main categories of port numbers:

### 1. Well-Known Ports (0–1023)

Reserved for common and widely used services.

Examples:

* 20/21 — FTP
* 22 — SSH
* 23 — Telnet
* 25 — SMTP
* 53 — DNS
* 80 — HTTP
* 110 — POP3
* 143 — IMAP
* 443 — HTTPS

### 2. Registered Ports (1024–49151)

Used by different software, applications, and services. These ports are registered with IANA for particular purposes.

Examples:

* 3306 — MySQL
* 3389 — RDP
* 5432 — PostgreSQL
* 8080 — Alternative HTTP

### 3. Dynamic / Private Ports (49152–65535)

Used for temporary connections, commonly as source ports selected by a client operating system.

For example, when you open a website, your computer may use a temporary source port to communicate with the web server.

## How Network Ports Work

When a device sends or receives network traffic, the port number helps identify the application involved.

For example, when you visit a website:

1. Your browser selects a temporary source port.
2. It connects to the destination server's port 80 (HTTP) or 443 (HTTPS).
3. The server receives the request through the appropriate port.
4. The operating system delivers the traffic to the web server application.
5. The server sends a response back to your browser.

**Important:** TCP and UDP use port numbers. An IP address identifies a host or network interface, while a port identifies an application endpoint.

---

# HTTP in Details

TryHackMe Room: https://tryhackme.com/room/httpindetail

HTTP stands for **HyperText Transfer Protocol**.

It is an application-layer protocol used for communication between web browsers (clients) and web servers.

HTTP follows a request-response mechanism:

* The client sends an HTTP request.
* The server processes the request.
* The server returns an HTTP response.

HTTP is stateless, which means each request is treated independently by default. Cookies and sessions can be used to maintain user state.

## What is a URL?

URL stands for **Uniform Resource Locator**.

A URL is predominantly an instruction on how to access a resource on the internet.

Example:

`https://example.com:443/products?id=10#details`

A URL can contain several parts:

* **Scheme:** `https` — Protocol used to access the resource.
* **Domain:** `example.com` — Website's domain name.
* **Port:** `443` — Destination port (often omitted when using the default port).
* **Path:** `/products` — Specific resource location.
* **Query String:** `?id=10` — Additional parameters.
* **Fragment:** `#details` — A specific section within the resource.

## HTTP Methods

HTTP methods tell the server what action the client wants to perform.

1. **GET Request:** This is used for getting information from a web server.
2. **POST Request:** This is used for submitting data to the web server and potentially creating new records.
3. **PUT Request:** This is used for submitting data to a web server to create or replace a resource.
4. **DELETE Request:** This is used for deleting information or records from a web server.
5. **PATCH Request:** This is used for partially updating an existing resource.

## Common HTTP Status Codes

There are a lot of different HTTP status codes. These are some of the most common responses you are likely to come across:

| Status Code                     | Description                                                                                   |
| ------------------------------- | --------------------------------------------------------------------------------------------- |
| **200 - OK**                    | The request was completed successfully.                                                       |
| **201 - Created**               | A resource has been created, for example, a new user or blog post.                            |
| **301 - Moved Permanently**     | The requested resource has permanently moved to a new URL.                                    |
| **302 - Found**                 | The requested resource is temporarily available at another URL.                               |
| **400 - Bad Request**           | Something was wrong or missing in the client's request.                                       |
| **401 - Unauthorized**          | Authentication is required or has failed.                                                     |
| **403 - Forbidden**             | The client does not have permission to access this resource.                                  |
| **404 - Not Found**             | The requested page or resource does not exist.                                                |
| **405 - Method Not Allowed**    | The resource does not allow the HTTP method used in the request.                              |
| **500 - Internal Server Error** | The server encountered an unexpected error.                                                   |
| **503 - Service Unavailable**   | The server is temporarily unable to handle the request, often due to overload or maintenance. |

If you are a visual learner, also check out this resource:

**HTTP Cats:** https://http.cat/

It provides visual representations of HTTP status codes.

## Common HTTP Request Headers

Request headers provide additional information about the client's request.

1. **User-Agent:** Identifies the client software, such as a browser.
2. **Content-Length:** Specifies the size of the request body in bytes.
3. **Accept-Encoding:** Specifies which content compression formats the client supports.
4. **Cookie:** Sends stored cookies to the server.
5. **Host:** Specifies the target host and domain name.

## Common HTTP Response Headers

Response headers provide additional information about the server's response.

1. **Set-Cookie:** Sends cookies from the server to the client.
2. **Cache-Control:** Defines caching rules for the response.
3. **Content-Type:** Specifies the type of content being returned, such as HTML or JSON.
4. **Content-Encoding:** Specifies the compression format used for the response.

## HTTP vs HTTPS

* **HTTP:** Data is generally transmitted without transport encryption.
* **HTTPS:** HTTP communication is protected using TLS encryption.

HTTPS helps protect sensitive information during transmission and provides server authentication through digital certificates.

---

# SMTP Server: What It Does

SMTP stands for **Simple Mail Transfer Protocol**.

SMTP is used to send and relay outgoing email.

Your mail application submits a message to an SMTP server. The server queues the message and relays it toward the recipient's mail server using the recipient domain's mail records (MX records).

## Common SMTP Ports

* **25:** Server-to-server mail relay; generally not used by mail apps for submitting messages.
* **587:** Authenticated email submission, commonly protected with STARTTLS.
* **465:** Authenticated email submission using implicit TLS.

SMTP sends mail, while **IMAP** or **POP3** is typically used to retrieve messages from a mailbox.

SMTP by itself does not encrypt email, so TLS is used to protect the connection between mail systems or clients.

## SMTP vs IMAP vs POP3

| Protocol | Main Purpose                                                                    |
| -------- | ------------------------------------------------------------------------------- |
| **SMTP** | Sending outgoing emails.                                                        |
| **IMAP** | Accessing and synchronizing emails stored on a mail server.                     |
| **POP3** | Retrieving emails from a mail server, commonly by downloading them to a client. |

---

# Useful Linux Commands

We can use different Linux commands to investigate network ports and services.

### 1. Check Listening Ports

```bash
ss -tuln
```

* `t` — TCP
* `u` — UDP
* `l` — Listening ports
* `n` — Show numeric addresses and ports

### 2. Check Network Connections

```bash
ss -tun
```

### 3. Scan Ports Using Nmap

```bash
nmap -sV 192.168.1.1
```

This scans the target and attempts to identify running services and their versions.

### 4. Check a Specific Port

```bash
nmap -p 80,443 192.168.1.1
```

Replace the IP address with your own authorized lab target.

### 5. Send an HTTP Request Using cURL

```bash
curl -I https://example.com
```

This displays the HTTP response headers.

### 6. View HTTP Response Details

```bash
curl -v https://example.com
```

This displays additional connection and HTTP communication details.

---

# Practical Learning

Try these activities to understand network ports and HTTP better:

1. Identify the common ports used by HTTP, HTTPS, SSH, DNS, and SMTP.
2. Use `ss -tuln` to check listening ports on Kali Linux.
3. Use Nmap to scan an authorized TryHackMe target.
4. Identify the HTTP methods used by a website.
5. Use `curl -I` to inspect HTTP response headers.
6. Explore different HTTP status codes using HTTP Cats.
7. Understand the difference between SMTP, IMAP, and POP3.

**Practice only on your own devices, TryHackMe labs, or systems where you have permission.**
