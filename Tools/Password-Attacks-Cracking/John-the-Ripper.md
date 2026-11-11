# John the Ripper – Password Cracking

## 1. Introduction

John the Ripper (JtR) is an open-source password security auditing and password recovery tool.

It is commonly used to:
- Crack password hashes using wordlists.
- Apply password mutation rules.
- Test password strength.
- Identify weak passwords.
- Extract hashes from supported files using helper tools.

## 2. Installation on Kali Linux

```bash
sudo apt update
sudo apt install john -y
```

Check the installed version:

```bash
john --version
```

Display supported hash formats:

```bash
john --list=formats
```

## 3. Basic Password Cracking

### Create a Hash File

```bash
echo '[HASH]' > hash.txt
```

Creates a file named `hash.txt` containing the hash.

### Crack Using a Wordlist

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Uses the RockYou wordlist to test possible passwords.

### Display Cracked Passwords

```bash
john --show hash.txt
```

Displays passwords that John has successfully cracked.

## 4. Password Cracking with Rules

Rules modify words from a wordlist to generate additional password variations.

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt --rules=norajCommon02
```

**Important:**
- `--wordlist` specifies the wordlist.
- `--rules` specifies the rule set.
- `norajCommon02` is a named rule set that must be available in your John configuration.
- You can also create custom rules in John's configuration file.

## 5. Custom Wordlist

Sometimes a challenge provides a name or keyword that can help identify the password.

Create a custom wordlist:

```bash
echo 'davidguettapan' > name.txt
```

Use it for password cracking:

```bash
john hash.txt --wordlist=name.txt
```

## 6. Cracking Specific Hash Formats

### Raw SHA1

```bash
john --format=Raw-SHA1 --wordlist=name.txt --rules=NT hash.txt
```

### Display Cracked SHA1 Passwords

```bash
john --show --format=Raw-SHA1 hash.txt
```

### Raw SHA256

```bash
john --format=Raw-SHA256 --wordlist=rockyou.txt hash.txt
```

### Raw MD5

```bash
john --format=Raw-MD5 hash.txt
```

**Note:** Always identify the correct hash format before cracking. The `--format` option tells John which hash algorithm to use.

## 7. GPG File Hash Extraction

John cannot directly crack every encrypted file. For supported GPG files, use `gpg2john` to extract a crackable hash.

### Extract Hash from GPG File

```bash
gpg2john personal.txt.gpg > personal.hash
```

This extracts the password hash and saves it in `personal.hash`.

### Crack the Extracted Hash

```bash
john --wordlist=rockyou.txt personal.hash
```

### Display the Cracked Password

```bash
john --show personal.hash
```

## 8. Important Commands

| Command | Purpose |
|---|---|
| `john --version` | Check John version |
| `john --list=formats` | List supported hash formats |
| `john hash.txt` | Crack hashes using default settings |
| `john --wordlist=rockyou.txt hash.txt` | Use a wordlist |
| `john --rules=NT hash.txt` | Apply a named rule set |
| `john --show hash.txt` | Display cracked passwords |
| `gpg2john file.gpg > hash.txt` | Extract hash from a GPG file |

## 9. Important Notes

- `rockyou.txt` is a commonly used password wordlist.
- On Kali Linux, it may need to be extracted first if it is stored as `rockyou.txt.gz`.
- `--rules=NT` and `--rules=norajCommon02` use named rule sets; availability depends on your John configuration.
- Use the correct `--format` when the hash type is known.
- Wordlists and rules can be combined to generate more password candidates.

## 10. Learning Resources

- [John the Ripper Official Website](https://www.openwall.com/john/)
- [John the Ripper GitHub](https://github.com/openwall/john)
- [TryHackMe](https://tryhackme.com/)

---

**Disclaimer:** Use John the Ripper only for authorized password auditing, recovery, and cybersecurity labs.
