# Timestamped Secrets

**Platform:** CyLab Academy  
**Lab Link:** https://learn.cylabacademy.org/library/722?page=1&category=2&workspace=true

## Challenge Overview

In this challenge, we are provided with two files:

- A message file containing encrypted data.
- A source file containing hints about the encryption process.

The objective is to analyze the provided files, understand the encryption mechanism, and decrypt the message to retrieve the flag.

## Step 1: Analyze the Provided Files

First, I examined the provided message file and source file to understand how the encryption process worked.

After analyzing the information, I realized that I could use a Python script to decrypt the message.

## Step 2: Create a Python Virtual Environment

Before running the script, I created and activated a Python virtual environment.

Create the virtual environment:

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

Install the required Python library:

```bash
pip install pycryptodome
```

## Step 3: Create the Decryption Script

I created a Python file using Nano:

```bash
nano decrypt.py
```

Then, I wrote the following Python script:

```python
from hashlib import sha256
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

ciphertext = bytes.fromhex(
    "e24b9c357ad38df368104cc83fd235607bdac8f0f83123b38a89f459e46a3db2"
)

timestamp = 1790147509

# Search 24 hours before and after the timestamp
for ts in range(timestamp - 86400, timestamp + 86401):

    # Generate AES key
    key = sha256(str(ts).encode()).digest()[:16]

    # Initialize AES
    cipher = AES.new(key, AES.MODE_ECB)

    try:
        decrypted = cipher.decrypt(ciphertext)

        plaintext = unpad(decrypted, AES.block_size)

        message = plaintext.decode("utf-8")

        if "{" in message and "}" in message:
            print("[+] Timestamp:", ts)
            print("[+] Decrypted message:", message)
            break

    except (ValueError, UnicodeDecodeError):
        continue

else:
    print("[-] No matching timestamp found.")
```

## Step 4: Run the Python Script

After saving the script, I executed it:

```bash
python3 decrypt.py
```

The script searches for the correct timestamp within a 24-hour window before and after the given timestamp.

For each timestamp, it:

1. Generates a SHA-256 hash from the timestamp.
2. Uses the first 16 bytes of the hash as an AES key.
3. Initializes AES in ECB mode.
4. Attempts to decrypt the ciphertext.
5. Removes PKCS#7 padding.
6. Checks whether the decrypted message contains a flag-like structure.

When the correct timestamp is found, the script prints the decrypted message.

## What I Learned

- How to create and activate a Python virtual environment.
- How to use Python libraries for cryptographic operations.
- How SHA-256 can be used to derive an encryption key.
- How AES encryption works.
- How AES-ECB decryption works.
- How timestamp-based brute-force techniques can help recover encrypted messages.
- How to automate decryption using Python.

## Key Takeaway

This challenge demonstrates how predictable timestamp-based key generation can weaken encryption security.

Using a predictable timestamp to derive an encryption key makes it possible to search through a limited range of possible timestamps and potentially recover the original message.

```
Flag: [Add the recovered flag here]
```

---
**Focus:** Cryptography, Python Scripting, AES Decryption, Timestamp Analysis
