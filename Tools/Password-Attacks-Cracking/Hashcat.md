# Hashcat – Password Hash Cracking

## 1. Introduction

Hashcat is an advanced password recovery and password hash cracking tool. It supports CPU and GPU acceleration to test password candidates against password hashes.

**Main Uses:**
- Password hash cracking
- Dictionary attacks
- Brute-force attacks
- Mask attacks
- Rule-based attacks
- Password security auditing

## 2. Installation on Kali Linux

```bash
sudo apt update
sudo apt install hashcat -y
```

Check the installed version:

```bash
hashcat --version
```

Display help:

```bash
hashcat --help
```

## 3. Basic Hashcat Syntax

```bash
hashcat -m <hash_mode> -a <attack_mode> hash.txt <wordlist_or_mask>
```

**Important Options:**

| Option | Description |
|---|---|
| `-m` | Specifies the hash type |
| `-a` | Specifies the attack mode |
| `-o` | Saves cracked passwords to a file |
| `--show` | Displays recovered passwords |
| `--username` | Ignores username fields in supported hash formats |

## 4. Brute-Force / Mask Attack

Example: Crack a bcrypt hash using a four-character lowercase mask.

```bash
hashcat -m 3200 -a 3 hash.txt '?l?l?l?l'
```

**Explanation:**
- `-m 3200` → bcrypt hash mode.
- `-a 3` → Mask attack.
- `?l` → Any lowercase letter (a–z).
- `?l?l?l?l` → Four lowercase letters.

### Common Mask Characters

| Character | Meaning |
|---|---|
| `?l` | Lowercase letters (a–z) |
| `?u` | Uppercase letters (A–Z) |
| `?d` | Digits (0–9) |
| `?s` | Special characters |
| `?a` | All character sets |

## 5. Display Cracked Passwords

```bash
hashcat -m 3200 hash.txt --show
```

Displays previously recovered passwords for the specified hash mode.

## 6. Dictionary Attack

A dictionary attack tests passwords from a wordlist against the target hash.

### Step 1: Create a Four-Character Wordlist

```bash
awk 'length($0)==4' /usr/share/wordlists/rockyou.txt > rockyou-4.txt
```

**Explanation:**
- `awk` → Processes text files.
- `length($0)==4` → Selects lines containing exactly four characters.
- `>` → Saves the filtered output into a new file.
- `rockyou-4.txt` → The newly created wordlist.

Change `4` according to the required password length.

### Step 2: Run Dictionary Attack

```bash
hashcat -m 3200 -a 0 hash.txt rockyou-4.txt
```

**Explanation:**
- `-m 3200` → bcrypt.
- `-a 0` → Straight (dictionary) attack.
- `rockyou-4.txt` → Custom wordlist.

### Step 3: Display Results

```bash
hashcat -m 3200 hash.txt --show
```

## 7. Other Common Hash Modes

### SHA512crypt

```bash
hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

**Explanation:**
- `-m 1800` → SHA512crypt.
- `-a 0` → Dictionary attack.
- `rockyou.txt` → Password wordlist.

### Common Hashcat Modes

| Hash Mode | Hash Type |
|---|---|
| `0` | MD5 |
| `100` | SHA1 |
| `1400` | SHA256 |
| `1700` | SHA512 |
| `1800` | SHA512crypt |
| `3200` | bcrypt |

**Note:** Hashcat mode numbers identify specific hash formats. Always identify the correct format before starting an attack.

## 8. Important Notes

- `-a 0` is used for dictionary attacks.
- `-a 3` is used for mask attacks.
- bcrypt (`-m 3200`) is computationally expensive and can take significantly longer to crack.
- The RockYou wordlist may need to be extracted before use:

```bash
sudo gzip -dk /usr/share/wordlists/rockyou.txt.gz
```

- Hashcat supports both CPU and GPU processing, depending on available hardware and drivers.

## 9. Learning Resources

- [Hashcat Official Website](https://hashcat.net/hashcat/)
- [Hashcat Documentation](https://hashcat.net/wiki/)
- [Hashcat GitHub](https://github.com/hashcat/hashcat)
- [TryHackMe](https://tryhackme.com/)

---

**Disclaimer:** Use Hashcat only for authorized password recovery, security auditing, and cybersecurity labs.
