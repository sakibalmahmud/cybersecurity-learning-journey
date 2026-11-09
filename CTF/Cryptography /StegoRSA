# StegoRSA

## Step 1: File Enumeration

Download the provided `flag.enc` and `.jpg` files to your Linux machine.

Extract the comment metadata from the image:

```bash
exiftool -Comment -b image.jpg
```

## Step 2: Extract Private Key

The image comment contains hexadecimal-encoded data. Convert it into a private key file.

```bash
exiftool -Comment -b image.jpg | xxd -r -p > private.pem
```

## Step 3: Decrypt Encrypted Flag

Use the extracted RSA private key to decrypt the encrypted flag.

```bash
openssl pkeyutl -decrypt -inkey private.pem -in flag.enc -out flag.txt
```

## Step 4: Read Flag

```bash
cat flag.txt
```

## Technique

- **Category:** Cryptography
- **Method:** RSA Decryption
- **Steganography:** Image Metadata Extraction
- **Tools:** ExifTool, xxd, OpenSSL
- **Key:** RSA Private Key
