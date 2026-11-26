# Corridor

**Platform:** TryHackMe  
**Room Link:** https://tryhackme.com/room/corridor  
**Difficulty:** Easy  
**Vulnerability:** IDOR (Insecure Direct Object Reference)

## Room Goal

The challenge introduces IDOR vulnerabilities. By examining the website's URL endpoints, we discover hexadecimal values that look like MD5 hashes. These hashes can help us access locations that are not directly linked on the website.

## Step 1: Website Enumeration

First, I started the TryHackMe machine and accessed the target IP address through my browser.

I also used Burp Suite to intercept and analyze HTTP requests and responses.

While inspecting the website, I noticed that its different doors used hexadecimal values in their URLs.

## Step 2: Identify the MD5 Hashes

After analyzing the URLs, I recognized that the hexadecimal values were MD5 hashes of sequential numbers.

For example:

- `MD5("1")` = `c4ca4238a0b923820dcc509a6f75849b`
- `MD5("2")` = `c81e728d9d4c2f636f067f89cc14862c`
- `MD5("0")` = `cfcd208495d565ef66e7dff9f98764da`

This revealed that the URL identifiers were predictable.

## Step 3: Access the Hidden Endpoint

I generated the MD5 hash of `0` and used it in a new URL.

Command:

```bash
echo -n "0" | md5sum
```

Then I sent an HTTP request to the endpoint:

```bash
curl -i http://10.48.183.119/cfcd208495d565ef66e7dff9f98764da
```

The server returned the hidden page containing the flag.

## Result

Successfully discovered the hidden endpoint and retrieved the flag.

## What I Learned

- Understanding IDOR vulnerabilities.
- Inspecting HTTP requests and responses using Burp Suite.
- Recognizing MD5 hashes in URL parameters and paths.
- Using `md5sum` to generate hashes.
- Testing predictable resource identifiers with cURL.

**Key Takeaway:** Hashing an identifier does not make it secure. Applications must implement proper server-side authorization checks to prevent unauthorized access.
