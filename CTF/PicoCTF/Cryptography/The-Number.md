# PicoCTF

## Challenge: The Numbers

### Challenge Overview

In this challenge, we are given an image file containing a sequence of numbers. The objective is to identify the hidden message and decode it to retrieve the flag.

### Step 1: Download the Image

First, I downloaded the challenge image to my Kali Linux machine using `wget`.

```bash
wget https://challenge-files.cylabacademy.net/library/664bc3a85525cfd5a2af151d29f2744ba334880e28e60f9a513aba13633199d4/the_numbers.png
```

### Step 2: Inspect the Image

After downloading the image, I opened it using:

```bash
xdg-open the_numbers.png
```

By inspecting the image, I found a sequence of numbers that represented a hidden message.

### Step 3: Decode the Numbers

I used a Python script to decode the numbers and retrieve the hidden message.

```bash
python3 decode.py
```

The numbers were decoded into letters to reveal the hidden message.

### Step 4: Retrieve the Flag

After successfully decoding the message, I obtained the flag.

**Flag:**

```text
PICOCTF{THENUMBERSMASON}
```

### What I Learned

- How to download challenge files using `wget`.
- How to inspect image files in Linux.
- How to identify hidden messages represented by numbers.
- How to use Python scripts for decoding.
- How to convert numerical values into alphabetical characters.

### Key Takeaway

Numbers can represent alphabetical characters using encoding techniques such as A1Z26, where each number corresponds to a letter of the alphabet (1 = A, 2 = B, and so on).

Understanding basic encoding techniques is useful when solving cryptography and CTF challenges.
