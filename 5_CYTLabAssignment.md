# Cryptology Lab Assignment - 5

## Objective :
To write Python programs to perform encryption and decryption using:
1. Shift Cipher
2. Caesar Cipher
3. ROT13 Cipher
4. Atbash Cipher
5. Affine Cipher

**Note:** The programs preserve uppercase/lowercase letters and leave spaces, numbers and special characters unchanged.

---

## 1. Shift Cipher

**Logic:**
- Take the plaintext and a shift key from the user.
- For encryption, shift each letter forward by the given key.
- For decryption, shift each letter backward by the same key.
- Use modulo 26 to keep the letters within the alphabet.

```python
def shift_encrypt(text, key):
    result = ""

    for ch in text:
        if ch.isalpha() and ch.isascii():
            base = ord('A') if ch.isupper() else ord('a')
            result += chr((ord(ch) - base + key) % 26 + base)
        else:
            result += ch

    return result


def shift_decrypt(text, key):
    return shift_encrypt(text, -key)


text = input("Enter the message: ")

try:
    key = int(input("Enter shift key: "))

    encrypted = shift_encrypt(text, key)
    print("Encrypted text:", encrypted)

    decrypted = shift_decrypt(encrypted, key)
    print("Decrypted text:", decrypted)

except ValueError:
    print("Invalid key! Enter an integer.")
```

---

## 2. Caesar Cipher

**Logic:**
- Caesar cipher is a type of shift cipher.
- Each letter is shifted by a fixed value of 3 positions.
- Decryption shifts each letter backward by 3 positions.

```python
def caesar_encrypt(text):
    return shift_encrypt(text, 3)


def caesar_decrypt(text):
    return shift_decrypt(text, 3)


text = input("Enter the message: ")

encrypted = caesar_encrypt(text)
print("Encrypted text:", encrypted)

decrypted = caesar_decrypt(encrypted)
print("Decrypted text:", decrypted)
```

---

## 3. ROT13 Cipher

**Logic:**
- ROT13 shifts every letter by 13 positions.
- Encryption and decryption use the same operation.
- Applying ROT13 twice gives back the original message.

```python
def rot13(text):
    result = ""

    for ch in text:
        if ch.isalpha() and ch.isascii():
            base = ord('A') if ch.isupper() else ord('a')
            result += chr((ord(ch) - base + 13) % 26 + base)
        else:
            result += ch

    return result


text = input("Enter the message: ")

encrypted = rot13(text)
print("Encrypted text:", encrypted)

decrypted = rot13(encrypted)
print("Decrypted text:", decrypted)
```

---

## 4. Atbash Cipher

**Logic:**
- Atbash replaces each letter with its reverse alphabet position.
- A becomes Z, B becomes Y, C becomes X, and so on.
- The same operation is used for encryption and decryption.

```python
def atbash(text):
    result = ""

    for ch in text:
        if ch.isupper():
            result += chr(155 - ord(ch))
        elif ch.islower():
            result += chr(219 - ord(ch))
        else:
            result += ch

    return result


text = input("Enter the message: ")

encrypted = atbash(text)
print("Encrypted text:", encrypted)

decrypted = atbash(encrypted)
print("Decrypted text:", decrypted)
```

---

## 5. Affine Cipher

**Logic:**
- Affine cipher uses two keys, a and b.
- Encryption formula: E(x) = (ax + b) mod 26.
- Decryption formula: D(y) = a⁻¹(y - b) mod 26.
- The value of a must be relatively prime to 26 so that its modular inverse exists.

```python
import math


def mod_inverse(a):
    for i in range(26):
        if (a * i) % 26 == 1:
            return i

    return None


def affine_encrypt(text, a, b):
    result = ""

    for ch in text:
        if ch.isalpha() and ch.isascii():
            base = ord('A') if ch.isupper() else ord('a')
            x = ord(ch) - base
            y = (a * x + b) % 26
            result += chr(y + base)
        else:
            result += ch

    return result


def affine_decrypt(text, a, b):
    result = ""
    inverse = mod_inverse(a)

    for ch in text:
        if ch.isalpha() and ch.isascii():
            base = ord('A') if ch.isupper() else ord('a')
            y = ord(ch) - base
            x = (inverse * (y - b)) % 26
            result += chr(x + base)
        else:
            result += ch

    return result


text = input("Enter the message: ")

try:
    a = int(input("Enter key a: "))
    b = int(input("Enter key b: "))

    if math.gcd(a, 26) != 1:
        print("Invalid key! a must be relatively prime to 26.")

    else:
        encrypted = affine_encrypt(text, a, b)
        print("Encrypted text:", encrypted)

        decrypted = affine_decrypt(encrypted, a, b)
        print("Decrypted text:", decrypted)

except ValueError:
    print("Invalid input! Enter integer keys.")
```

---

## Validation Included

| Cipher | Validation |
|---|---|
| Shift | Checks that the key is an integer. |
| Caesar | Uses a fixed shift value of 3. |
| ROT13 | Uses a fixed shift value of 13. |
| Atbash | Uses reverse alphabet mapping. |
| Affine | Checks that keys are integers and that gcd(a, 26) = 1. |
