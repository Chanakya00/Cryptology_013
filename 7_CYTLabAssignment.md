# Cryptology Lab Assignment - 7

## Objective

To implement encryption and decryption using:
1. Columnar Transposition Cipher
2. Double Columnar Transposition Cipher

Also, to explore the OpenSSL tool and understand its basic cryptographic operations.

---

# 1. Columnar Transposition Cipher

### Logic
- Take the plaintext and a keyword from the user.
- Arrange the plaintext row by row into columns based on the keyword length.
- Arrange the columns in alphabetical order of the keyword letters.
- Read the columns in that order to obtain the ciphertext.
- For decryption, place the ciphertext back into the columns and read row by row.

### Python Code

```python
def get_order(key):
    return sorted(range(len(key)), key=lambda i: (key[i], i))


def encrypt(text, key):
    text = text.replace(" ", "").upper()
    key = key.upper()

    cols = len(key)
    order = get_order(key)
    result = ""

    for col in order:
        for i in range(col, len(text), cols):
            result += text[i]

    return result


def decrypt(cipher, key):
    cols = len(key)
    rows = (len(cipher) + cols - 1) // cols
    remainder = len(cipher) % cols

    grid = [""] * cols
    order = get_order(key)
    index = 0

    for col in order:
        length = rows if remainder == 0 or col < remainder else rows - 1
        grid[col] = cipher[index:index + length]
        index += length

    result = ""

    for row in range(rows):
        for col in range(cols):
            if row < len(grid[col]):
                result += grid[col][row]

    return result


text = input("Enter plaintext: ")
key = input("Enter keyword: ")

if not text.replace(" ", "").isalpha() or not text.replace(" ", "").isascii():
    print("Invalid plaintext! Enter only English letters.")

elif not key.isalpha() or not key.isascii():
    print("Invalid key! Enter only English letters.")

else:
    cipher = encrypt(text, key)
    print("Encrypted text:", cipher)

    plain = decrypt(cipher, key)
    print("Decrypted text:", plain)
```

### Input and Output

**Input:**
```text
Enter plaintext: WE ARE DISCOVERED
Enter keyword: ZEBRA
```

**Output:**
```text
Encrypted text: EODASREIERCEWDV
Decrypted text: WEAREDISCOVERED
```

### Validation
- Plaintext must contain only English letters and spaces.
- Keyword must contain only English letters.
- Empty keyword is not allowed.

---

# 2. Double Columnar Transposition Cipher

### Logic
- Take the plaintext and two keywords from the user.
- First, encrypt the plaintext using the first keyword.
- Then, encrypt the resulting ciphertext using the second keyword.
- For decryption, first decrypt using the second keyword.
- Finally, decrypt using the first keyword to obtain the original plaintext.

### Python Code

```python
def get_order(key):
    return sorted(range(len(key)), key=lambda i: (key[i], i))


def encrypt(text, key):
    cols = len(key)
    order = get_order(key)
    result = ""

    for col in order:
        for i in range(col, len(text), cols):
            result += text[i]

    return result


def decrypt(cipher, key):
    cols = len(key)
    rows = (len(cipher) + cols - 1) // cols
    remainder = len(cipher) % cols

    grid = [""] * cols
    order = get_order(key)
    index = 0

    for col in order:
        length = rows if remainder == 0 or col < remainder else rows - 1
        grid[col] = cipher[index:index + length]
        index += length

    result = ""

    for row in range(rows):
        for col in range(cols):
            if row < len(grid[col]):
                result += grid[col][row]

    return result


def double_encrypt(text, key1, key2):
    first = encrypt(text, key1)
    second = encrypt(first, key2)
    return second


def double_decrypt(cipher, key1, key2):
    first = decrypt(cipher, key2)
    second = decrypt(first, key1)
    return second


text = input("Enter plaintext: ").replace(" ", "")
key1 = input("Enter first keyword: ").upper()
key2 = input("Enter second keyword: ").upper()

if not text.isalpha() or not text.isascii():
    print("Invalid plaintext! Enter only English letters.")

elif not key1.isalpha() or not key1.isascii():
    print("Invalid first key! Enter only English letters.")

elif not key2.isalpha() or not key2.isascii():
    print("Invalid second key! Enter only English letters.")

else:
    cipher = double_encrypt(text.upper(), key1, key2)
    print("Encrypted text:", cipher)

    plain = double_decrypt(cipher, key1, key2)
    print("Decrypted text:", plain)
```

### Input and Output

**Input:**
```text
Enter plaintext: HELLOWORLD
Enter first keyword: ZEBRA
Enter second keyword: TIGER
```

**Output:**
```text
Encrypted text: RHLLDLEWOO
Decrypted text: HELLOWORLD
```

**Note:** The first encryption produces `ODLREOLLHW`. This intermediate ciphertext is encrypted again using the second keyword.

### Validation
- Plaintext must contain only English letters.
- Both keywords must contain only English letters.
- Empty keywords are not allowed.

---

# 3. Exploring the OpenSSL Tool

### Objective
To explore OpenSSL and understand its basic cryptographic operations.

OpenSSL is an open-source cryptographic tool used for encryption, decryption, hashing and digital certificate management. I have gone through and tried the following basic commands as shown below:

### Basic Commands :

**1. Check OpenSSL version**

```bash
openssl version
```

Displays the installed OpenSSL version.

**2. Display available commands**

```bash
openssl help
```

**3. Encrypt a file using AES-256**

First, create a file named `message.txt`.

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 -in message.txt -out encrypted.bin
```

Enter a password when prompted.

**4. Decrypt the file**

```bash
openssl enc -aes-256-cbc -d -pbkdf2 -iter 100000 -in encrypted.bin -out decrypted.txt
```

Enter the same password used during encryption.

**5. Generate SHA-256 hash**

```bash
openssl dgst -sha256 message.txt
```

Displays the SHA-256 hash of the file.

**6. Base64 Encoding and Decoding**

Encoding:

```bash
openssl base64 -in message.txt -out encoded.txt
```

Decoding:

```bash
openssl base64 -d -in encoded.txt -out decoded.txt
```

### Applications of OpenSSL

- File encryption and decryption.
- Generating cryptographic hashes.
- Managing digital certificates.
- Generating public and private keys.
- Supporting secure communication.

## References

1. [OpenSSL Official Documentation](https://docs.openssl.org/)
2. [OpenSSL Encryption Commands](https://docs.openssl.org/3.0/man1/openssl-enc/)
