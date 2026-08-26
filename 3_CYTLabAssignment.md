# Lab 3: Cryptology Lab — Introduction to Python
## Python Basics and Debugging

### 1. Debug the following programs. Identify the type of error in each case.

#### Original Code:
```python
print("Welcome to Cryptology Lab)
message = "Python Programming"
print(mesage)
num = input("Enter a number: ")
result = num + 10
print(result)
```

#### Debugged Solution:
* **Program 1 Error:** `SyntaxError` (Unterminated string literal).
* **Program 2 Error:** `NameError` (Variable `mesage` is misspelled).
* **Program 3 Error:** `TypeError` (Cannot add an integer to a string from `input()`).

```python
# Program 1 Fixed
print("Welcome to Cryptology Lab")

# Program 2 Fixed
message = "Python Programming"
print(message)

# Program 3 Fixed
num = int(input("Enter a number: "))
result = num + 10
print(result)
```

---

### 2. Write Python statements to display the following exactly:
```text
Welcome to Cryptology Lab
It's interesting to learn Python.
Students, "Welcome to the Cryptology Lab".
```

#### Solution:
```python
print("Welcome to Cryptology Lab")
print("It's interesting to learn Python.")
print('Students, "Welcome to the Cryptology Lab".')
```

---

### 3. Read two numbers from the user and perform:
* Addition
* Subtraction
* Multiplication
* Division
* Integer division
* Remainder
* Exponentiation

Display each result with an appropriate message.

#### Solution:
```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print(f"Addition: {num1} + {num2} = {num1 + num2}")
print(f"Subtraction: {num1} - {num2} = {num1 - num2}")
print(f"Multiplication: {num1} * {num2} = {num1 * num2}")

if num2 != 0:
    print(f"Division: {num1} / {num2} = {num1 / num2}")
    print(f"Integer division: {num1} // {num2} = {num1 // num2}")
    print(f"Remainder: {num1} % {num2} = {num1 % num2}")
else:
    print("Division, Integer division, and Remainder by zero are undefined.")

print(f"Exponentiation: {num1} ** {num2} = {num1 ** num2}")
```

---

### 4. Read a floating-point number and display:
* its data type;
* its absolute value;
* the value rounded to two decimal places.

#### Solution:
```python
val = float(input("Enter a floating-point number: "))

print("Data type:", type(val))
print("Absolute value:", abs(val))
print("Rounded to two decimal places:", round(val, 2))
```

---

## Part B — Data Types and Collections

### 5. Create variables containing examples of: int, float, complex, str, list, tuple, set, and dictionary. Use Python to display the value and data type of each variable.

#### Solution:
```python
v_int = 15
v_float = 10.5
v_complex = 3 + 4j
v_str = "Cryptology"
v_list = [1, 2, 3]
v_tuple = (10, 20)
v_set = {1, 2, 3}
v_dict = {"cipher": "RSA", "bits": 2048}

vars_list = [v_int, v_float, v_complex, v_str, v_list, v_tuple, v_set, v_dict]

for item in vars_list:
    print(f"Value: {item} | Type: {type(item)}")
```

---

### 6. Demonstrate experimentally that: Strings are immutable, whereas lists are mutable. Include the Python statements you used and explain the observed result.

#### Solution:
```python
# String Immutability Experiment
try:
    test_str = "Python"
    test_str[0] = "J"
except TypeError as e:
    print(f"String Error Captured: {e}")

# List Mutability Experiment
test_list = [10, 20, 30]
print("Original List:", test_list)
test_list[0] = 99
print("Modified List:", test_list)
```
* **Explanation:** Modifying an index element of the string triggers a `TypeError` because strings in Python are immutable memory segments. Lists are mutable dynamic arrays, allowing direct item re-assignment in place.

---

### 7. Create a list containing five prime numbers. Perform the following:
* display the first three elements;
* display the last element;
* append another prime number;
* extend the list with two more prime numbers;
* display the total number of elements.

#### Solution:
```python
primes = [2, 3, 5, 7, 11]

print("First three elements:", primes[:3])
print("Last element:", primes[-1])

primes.append(13)
print("After append:", primes)

primes.extend([17, 19])
print("After extend:", primes)

print("Total number of elements:", len(primes))
```

---

## Part C — String Operations
*For Questions 8–12, use:* `message = "CRYPTOLOGY USING PYTHON"`

### 8. Display: length of the string; first five characters; last six characters; characters from positions 3 to 8; string in reverse order.

#### Solution:
```python
message = "CRYPTOLOGY USING PYTHON"

print("Length of string:", len(message))
print("First five characters:", message[:5])
print("Last six characters:", message[-6:])
print("Characters from positions 3 to 8:", message[3:9])
print("Reverse order:", message[::-1])
```

---

### 9. Perform the following: convert to lowercase; convert back to uppercase; check whether "PYTHON" exists in the string; replace "PYTHON" with "PROGRAMMING".

#### Solution:
```python
message = "CRYPTOLOGY USING PYTHON"

print("Lowercase:", message.lower())
print("Back to uppercase:", message.lower().upper())
print("Does 'PYTHON' exist?:", "PYTHON" in message)
print("Replaced string:", message.replace("PYTHON", "PROGRAMMING"))
```

---

### 10. Remove the spaces from the string and display the resulting string.

#### Solution:
```python
message = "CRYPTOLOGY USING PYTHON"
no_spaces = message.replace(" ", "")
print("Without spaces:", no_spaces)
```

---

### 11. Using a loop, display every character and its corresponding Unicode/ASCII value using ord().

#### Solution:
```python
message = "CRYPTOLOGY USING PYTHON"
for char in message:
    print(f"{char} -> {ord(char)}")
```

---

### 12. Use chr() to convert the following values into characters: 65, 67, 73, 80, 72, 69, 82. Combine the resulting characters and identify the word.

#### Solution:
```python
ascii_values = [65, 67, 73, 80, 72, 69, 82]
decoded_word = "".join([chr(val) for val in ascii_values])
print("Identified Word:", decoded_word)
```
* **Resulting Word:** **ACIPHER**

---

## Part D — Text Processing for Cryptology

### 13. Plaintext preprocessing: Read a message from the user and: remove leading/trailing spaces; convert it to uppercase; remove spaces between words.
* **Example Input:** `meet me tomorrow` -> **Output:** `MEETMETOMORROW`

#### Solution:
```python
user_input = input("Enter a message: ")
processed = user_input.strip().upper().replace(" ", "")
print("Output:", processed)
```

---

### 14. Character grouping: Read a string and divide it into blocks of five characters.
* **Example Input:** `CRYPTOLOGYLAB` -> **Output:** `CRYPT`, `OLOGY`, `LAB`

#### Solution:
```python
text = input("Enter a string: ").replace(" ", "")
for i in range(0, len(text), 5):
    print(text[i:i+5])
```

---

### 15. Padding: Modify Question 14 so that an incomplete final block is padded with X.
* **Example Input:** `CRYPTOLOGYLAB` -> **Output:** `CRYPT`, `OLOGY`, `LABXX`

#### Solution:
```python
text = input("Enter a string: ").replace(" ", "")
remainder = len(text) % 5

if remainder != 0:
    text += "X" * (5 - remainder)

for i in range(0, len(text), 5):
    print(text[i:i+5])
```

---

### 16. Character frequency: For the text = "CRYPTOLOGYISINTERESTING", write a program to calculate the frequency of each character. Then identify the most frequently occurring character.

#### Solution:
```python
text = "CRYPTOLOGYISINTERESTING"
freq = {}

for char in text:
    freq[char] = freq.get(char, 0) + 1

print("Character Frequencies:", freq)
most_frequent = max(freq, key=freq.get)
print(f"Most frequent character: '{most_frequent}' value: {freq[most_frequent]}")
```

---

### 17. Percentage frequency: Extend Question 16 to calculate Percentage Frequency = (Frequency of Character / Total Number of Characters) * 100. Display the percentage rounded to two decimal places.

#### Solution:
```python
text = "CRYPTOLOGYISINTERESTING"
total_chars = len(text)
freq = {}

for char in text:
    freq[char] = freq.get(char, 0) + 1

for char, count in freq.items():
    percentage = (count / total_chars) * 100
    print(f"{char}: {percentage:.2f}%")
```

---

## Part E — Mathematical Foundations for Cryptology

### 18. Modular arithmetic: Use Python to evaluate: 29 mod 26, 55 mod 26, 78 mod 26, -3 mod 26, -29 mod 26. Then write a program that accepts an integer and calculates the integer modulo 26.

#### Solution:
```python
print("29 mod 26 =", 29 % 26)
print("55 mod 26 =", 55 % 26)
print("78 mod 26 =", 78 % 26)
print("-3 mod 26 =", -3 % 26)
print("-29 mod 26 =", -29 % 26)

val = int(input("\nEnter an integer: "))
print(f"{val} mod 26 = {val % 26}")
```

---

### 19. Alphabet representation: Using A=0, B=1,..., Z=25, write a program that accepts an uppercase character and displays its numerical representation. Also perform the reverse conversion.

#### Solution:
```python
# Character to number
char_in = input("Enter character: ").upper()
num_out = ord(char_in) - ord('A')
print(f"{char_in} -> {num_out}")

# Number to character
num_in = int(input("Enter number (0-25): "))
char_out = chr(num_in + ord('A'))print(f"{num_in} -> {char_out}")
```

20. Prime numbers: Write a program to: determine whether a given number is prime; display all prime numbers within a range specified by the user.

Solution:
```python
def check_prime(n):
    if n <= 1: 
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0: 
            return False
    return True

num = int(input("Enter number to check: "))
print(f"Is {num} prime?: {check_prime(num)}")

start = int(input("Enter lower range: "))
end = int(input("Enter upper range: "))
primes_found = [x for x in range(start, end + 1) if check_prime(x)]
print("Primes in range:", primes_found)
```

21. GCD and coprimes: Read two integers from the user. Find their GCD and determine whether they are coprime. Test your program with: 15 and 26; 18 and 24; 17 and 26.

Solution:
```python
import math

def coprime_eval(a, b):
    gcd_val = math.gcd(a, b)
    is_coprime = (gcd_val == 1)
    print(f"Pair ({a}, {b}) -> GCD: {gcd_val} | Coprime: {is_coprime}")

coprime_eval(15, 26)
coprime_eval(18, 24)
coprime_eval(17, 26)
```

22. Write a program to get the multiplicative inverse of an integer b (modulo 26).

Solution:
```python
def ext_gcd_mod_inverse(b, m=26):
    m0, x0, x1 = m, 0, 1
    if m == 1: 
        return None
    while b > 1:
        if m == 0: 
            return None
        q = b // m
        b, m = m, b % m
        x0, x1 = x1 - q * x0, x0
    if x1 < 0: 
        x1 += m0
    return x1

b_val = int(input("Enter integer b: "))
inverse = ext_gcd_mod_inverse(b_val, 26)
if inverse:
    print(f"Modular Multiplicative Inverse of {b_val} mod 26 is: {inverse}")
else:
    print(f"Inverse does not exist for {b_val} mod 26.")
```

Part F — Challenge / Bonus

23. WAP in python to implement client and server communication.
"Whether you succeed or not is irrelevant - there is no such thing. Making your known is the important thing" — Art and Letters, Georgia O'Keeffe.

Solution (Server Side Code):
```python
import socket

def run_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind(('127.0.0.1', 12345))
    server_socket.listen(1)
    print("Server initialized. Waiting for connections...")
    
    conn, addr = server_socket.accept()
    data = conn.recv(1024).decode()
    print("Received string from client:", data)
    
    conn.send("Message processed successfully by server.".encode())
    conn.close()
    server_socket.close()

if __name__ == "__main__":
    run_server()
```

Solution (Client Side Code):
```python
import socket

def run_client():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect(('127.0.0.1', 12345))
    
    quote = "Making your known is the important thing. --- Georgia O'Keeffe"
    client_socket.send(quote.encode())
    
    response = client_socket.recv(1024).decode()
    print("Server verification payload:", response)
    client_socket.close()

if __name__ == "__main__":
    run_client()
```
