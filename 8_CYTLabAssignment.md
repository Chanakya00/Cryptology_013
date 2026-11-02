# Cryptology Lab Assignment - 8

## 1. RSA Algorithm

### Objective
To write a Python program to implement the RSA algorithm for encryption and decryption of a message.

### Logic / Algorithm :
1. Select two prime numbers `p` and `q`.
2. Calculate `n = p × q`.
3. Calculate Euler's totient: `φ(n) = (p-1) × (q-1)`.
4. Choose a public key `e` such that `gcd(e, φ(n)) = 1`.
5. Calculate the private key `d` using the modular inverse of `e`.
6. Encrypt the message using `C = M^e mod n`.
7. Decrypt the ciphertext using `M = C^d mod n`.

### Python Code

```python
import math

# Choose two prime numbers
p = 17
q = 11

# Calculate n and Euler's totient
n = p * q
phi = (p - 1) * (q - 1)

# Choose public key
e = 7

# Check whether e is valid
if math.gcd(e, phi) != 1:
    print("Invalid public key")
else:
    # Calculate private key
    d = pow(e, -1, phi)

    print("Public Key:", (e, n))
    print("Private Key:", (d, n))

    # Input message
    message = int(input("Enter a number to encrypt: "))

    if message < 0 or message >= n:
        print("Message must be between 0 and", n - 1)
    else:
        # Encryption
        cipher = pow(message, e, n)
        print("Encrypted Message:", cipher)

        # Decryption
        decrypted = pow(cipher, d, n)
        print("Decrypted Message:", decrypted)
```

### Input:
```text
Enter a number to encrypt: 88
```

### Output:
```text
Public Key: (7, 187)
Private Key: (23, 187)
Encrypted Message: 11
Decrypted Message: 88
```

---

## 2. Diffie-Hellman Key Exchange

### Objective
To write a Python program to implement the Diffie-Hellman key exchange algorithm to generate a shared secret key between two users.

### Logic / Algorithm :
1. Select a public prime number `p` and a primitive root `g`.
2. Alice chooses a private key `a`.
3. Bob chooses a private key `b`.
4. Alice calculates her public key: `A = g^a mod p`.
5. Bob calculates his public key: `B = g^b mod p`.
6. Both exchange their public keys.
7. Alice calculates the shared key: `K = B^a mod p`.
8. Bob calculates the shared key: `K = A^b mod p`.
9. Both obtain the same shared secret key.

### Python Code

```python
# Public values
p = 23
g = 5

# Private keys of Alice and Bob
a = 6
b = 15

# Calculate public keys
A = pow(g, a, p)
B = pow(g, b, p)

print("Alice's Public Key:", A)
print("Bob's Public Key:", B)

# Calculate shared secret keys
key_alice = pow(B, a, p)
key_bob = pow(A, b, p)

print("Alice's Shared Key:", key_alice)
print("Bob's Shared Key:", key_bob)

# Check whether both keys are equal
if key_alice == key_bob:
    print("Key Exchange Successful")
else:
    print("Key Exchange Failed")
```

### Output
```text
Alice's Public Key: 8
Bob's Public Key: 19
Alice's Shared Key: 2
Bob's Shared Key: 2
Key Exchange Successful
```

---

## Difference Between RSA and Diffie-Hellman

| RSA | Diffie-Hellman |
|---|---|
| Asymmetric encryption algorithm. | Key exchange algorithm. |
| Uses public and private keys. | Uses private and public values. |
| Supports encryption and decryption. | Establishes a shared secret key. |
| Based on integer factorization. | Based on the discrete logarithm problem. |
