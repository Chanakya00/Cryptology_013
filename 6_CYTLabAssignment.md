# CYT Lab Assignment – 6

## Objectives

1. Perform One-Time Pad encryption and decryption.
2. Break a Shift Cipher using a brute-force attack.
3. Encrypt a message using the Rail Fence Cipher.

---

## 1. One-Time Pad (OTP)

**Logic:**
- Take plaintext and a secret key of equal length.
- Convert each character into its numerical value (A = 0 to Z = 25).
- Add plaintext and key values and apply modulo 26 for encryption.
- For decryption, subtract the key values from ciphertext values and apply modulo 26.

**Formula:**

Encryption: C = (P + K) mod 26

Decryption: P = (C - K) mod 26

```python
def encrypt(text, key):
    result = ""

    for i in range(len(text)):
        p = ord(text[i].upper()) - ord('A')
        k = ord(key[i].upper()) - ord('A')

        c = (p + k) % 26
        result += chr(c + ord('A'))

    return result


def decrypt(cipher, key):
    result = ""

    for i in range(len(cipher)):
        c = ord(cipher[i].upper()) - ord('A')
        k = ord(key[i].upper()) - ord('A')

        p = (c - k) % 26
        result += chr(p + ord('A'))

    return result


text = input("Enter plaintext: ").replace(" ", "")
key = input("Enter key: ").replace(" ", "")

if not text.isalpha() or not text.isascii():
    print("Invalid plaintext! Enter only English letters.")

elif not key.isalpha() or not key.isascii():
    print("Invalid key! Enter only English letters.")

elif len(text) != len(key):
    print("Error! Key must be equal to plaintext length.")

else:
    cipher = encrypt(text, key)
    print("Encrypted text:", cipher)

    plain = decrypt(cipher, key)
    print("Decrypted text:", plain)
```
**Output:**

Enter plaintext: HELLO

Enter key: CELLO

Encrypted text: JIWWC

Decrypted text: HELLO

---

## 2. Brute-Force Attack on Shift Cipher

**Given Ciphertext:** MCI RWR WH

**Cryptanalysis Model:** Ciphertext-Only Attack (COA)

**Logic:**
- Take the given ciphertext.
- Try all 26 possible shift keys from 0 to 25.
- For each key, shift every letter backward.
- Display all possible plaintexts.
- Identify the meaningful plaintext.

```python
def decrypt(text, key):
    result = ""

    for ch in text:
        if ch.isalpha():
            base = ord('A') if ch.isupper() else ord('a')
            p = (ord(ch) - base - key) % 26
            result += chr(p + base)
        else:
            result += ch

    return result


cipher = "MCI RWR WH"

print("Brute Force Results:\n")

for key in range(26):
    plain = decrypt(cipher, key)
    print("Key:", key, "Plaintext:", plain)
```

**Output:**

The program displays all 26 possible plaintexts, one for each key.

The meaningful plaintext is:

**YOU DID IT**

This is obtained using key = 14.

---

## 3. Rail Fence Cipher – Encryption

**Logic:**
- Take the plaintext and number of rails from the user.
- Write the characters diagonally down and up across the rails.
- Continue until all characters are arranged.
- Read the characters row by row to obtain the ciphertext.

```python
def rail_fence_encrypt(text, rails):
    fence = ['' for i in range(rails)]

    row = 0
    direction = 1

    for ch in text:
        fence[row] += ch

        if row == 0:
            direction = 1
        elif row == rails - 1:
            direction = -1

        row += direction

    return ''.join(fence)


text = input("Enter plaintext: ").replace(" ", "")

try:
    rails = int(input("Enter number of rails: "))

    if not text.isalpha() or not text.isascii():
        print("Invalid plaintext! Enter only English letters.")

    elif rails < 2:
        print("Invalid number of rails! Enter at least 2.")

    elif rails > len(text):
        print("Number of rails cannot exceed message length.")

    else:
        cipher = rail_fence_encrypt(text, rails)
        print("Encrypted text:", cipher)

except ValueError:
    print("Invalid input! Enter an integer for rails.")
```

**Output:**

Enter plaintext: HELLOWORLD

Enter number of rails: 2

Encrypted text: HLOOLELWRD

---

## Validation Included

| Program | Validation |
|---|---|
| One-Time Pad | Checks alphabetic input and equal plaintext/key length. |
| Shift Cipher Brute Force | Uses all 26 valid keys automatically. |
| Rail Fence | Checks alphabetic input and valid number of rails. |
