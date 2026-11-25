# Small Trouble

**Platform:** CyLab Academy  
**Lab Link:** https://learn.cylabacademy.org/library/718?page=1&category=2&workspace=true

## Challenge Overview

In this challenge, we are provided with two files:

- A message file containing RSA parameters and ciphertext.
- A source file containing hints about the encryption process.

After analyzing the source file, I discovered that the RSA implementation was vulnerable to **Wiener's Attack**, also known as the Small Private Exponent Attack.

The objective was to recover the RSA private exponent and decrypt the encrypted message using a Python script.

## Step 1: Analyze the Provided Files

First, I examined the message file and source file to understand the RSA encryption process.

After analyzing the source code, I identified that the challenge could be solved using Wiener's Attack.

## Step 2: Activate the Python Virtual Environment

I activated the Python virtual environment created for the challenge:

```bash
source .venv/bin/activate
```

## Step 3: Create the Python Script

I created a Python file using Nano:

```bash
nano wiener.py
```

Then, I wrote the following script:

```python
from math import isqrt

# Read RSA values from message.txt
values = {}

with open("message.txt", "r") as file:
    for line in file:
        key, value = line.split("=")
        values[key.strip()] = int(value.strip())

n = values["n"]
e = values["e"]
c = values["c"]


# Generate continued fraction
def continued_fraction(a, b):
    while b:
        q = a // b
        yield q
        a, b = b, a - q * b


# Generate convergents
def convergents(cf):
    p0, p1 = 0, 1
    q0, q1 = 1, 0

    for a in cf:
        p = a * p1 + p0
        q = a * q1 + q0

        yield p, q

        p0, p1 = p1, p
        q0, q1 = q1, q


# Wiener's Attack
for k, d in convergents(continued_fraction(e, n)):

    if k == 0:
        continue

    if (e * d - 1) % k != 0:
        continue

    phi = (e * d - 1) // k

    s = n - phi + 1

    discriminant = s * s - 4 * n

    if discriminant < 0:
        continue

    root = isqrt(discriminant)

    if root * root != discriminant:
        continue

    if (s + root) % 2 != 0:
        continue

    p = (s + root) // 2
    q = (s - root) // 2

    if p * q == n:

        print("[+] Private exponent recovered!")
        print("[+] d =", d)

        # Decrypt ciphertext
        plaintext = pow(c, d, n)

        message = plaintext.to_bytes(
            (plaintext.bit_length() + 7) // 8,
            "big"
        )

        print("[+] Decrypted message:")
        print(message.decode())

        break

else:
    print("[-] Wiener attack failed.")
```

## Step 4: Execute the Python Script

After saving the script, I executed it:

```bash
python3 wiener.py
```

The script performed Wiener's Attack against the provided RSA parameters.

It recovered the private exponent and used it to decrypt the ciphertext.

Finally, the decrypted message was displayed in the terminal.

## How Wiener's Attack Works

Wiener's Attack is a cryptographic attack against RSA when the private exponent (`d`) is too small.

The attack uses **Continued Fractions** to recover the private exponent from the public RSA parameters.

The script performs the following operations:

1. Reads the RSA values (`n`, `e`, and `c`) from the message file.
2. Generates continued fractions from the public exponent and modulus.
3. Calculates their convergents.
4. Uses the convergents to search for the private exponent.
5. Recovers the RSA prime factors (`p` and `q`).
6. Uses the recovered private exponent to decrypt the ciphertext.

## What I Learned

- Understanding RSA encryption and its parameters.
- What Wiener's Attack is.
- How a small RSA private exponent can weaken encryption.
- How Continued Fractions work in cryptanalysis.
- How to implement cryptographic attacks using Python.
- How to recover an RSA private exponent.
- How to decrypt RSA ciphertext using Python's modular exponentiation.

## Key Takeaway

RSA security depends on the proper generation and use of its cryptographic parameters.

If the private exponent is too small, RSA can become vulnerable to Wiener's Attack, potentially allowing an attacker to recover the private key and decrypt encrypted messages.

---

**Focus:** Cryptography, RSA, Wiener's Attack, Python Scripting
