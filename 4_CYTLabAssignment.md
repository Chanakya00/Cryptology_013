# 4_Cyrptology_Lab Assignment

# Level 1: File Handling and String Operations

---

## Question 1

Write a Python program to accept five statements related to cryptology from the user and store them in a text file named cryptology.txt. Store each statement on a separate line.

### Sample Statements

- Cryptology is the study of secure communication.
- Cryptography focuses on protecting information.
- Cryptanalysis focuses on analyzing cryptographic systems.
- Plaintext represents the original message.
- Ciphertext represents the transformed message.
- Cryptanalysis is fun :)
- I love Cryptanalysis ;)

### Answer

```python
# Accept five statements and store them in cryptology.txt

with open("cryptology.txt", "w") as file:
    for i in range(5):
        statement = input("Enter statement " + str(i + 1) + ": ")
        file.write(statement + "\n")

print("Five statements have been stored in cryptology.txt")
```

---

## Question 2

Write a Python program to read cryptology.txt and display its complete contents.

### Answer

```python
# Read and display complete contents of cryptology.txt

with open("cryptology.txt", "r") as file:
    contents = file.read()

print(contents)
```

---

## Question 3

Write a program to read cryptology.txt one line at a time and display each line along with its line number.

### Answer

```python
# Display each line along with its line number

with open("cryptology.txt", "r") as file:
    line_number = 1

    for line in file:
        print(line_number, line.strip())
        line_number += 1
```

---

## Question 4

write a program to store the output in a file called cryptology_no.txt

### Answer

```python
# Store numbered output in cryptology_no.txt

with open("cryptology.txt", "r") as input_file:
    with open("cryptology_no.txt", "w") as output_file:

        line_number = 1

        for line in input_file:
            numbered_line = str(line_number) + " " + line.strip()

            print(numbered_line)
            output_file.write(numbered_line + "\n")

            line_number += 1

print("Output stored in cryptology_no.txt")
```

---

## Question 5

Write a program to read cryptology.txt and determine:

- Number of lines
- Number of words
- Number of characters

### Answer

```python
# Count lines, words and characters in cryptology.txt

with open("cryptology.txt", "r") as file:
    contents = file.read()

lines = contents.splitlines()
words = contents.split()
characters = len(contents)

print("Number of lines:", len(lines))
print("Number of words:", len(words))
print("Number of characters:", characters)
```

---

## Question 6

Read cryptology_no.txt and count the number of:

- Uppercase letters
- Lowercase letters
- Digits
- Spaces
- Special characters

### Answer

```python
# Count different types of characters in cryptology_no.txt

with open("cryptology_no.txt", "r") as file:
    contents = file.read()

uppercase = 0
lowercase = 0
digits = 0
spaces = 0
special = 0

for ch in contents:

    if ch.isupper():
        uppercase += 1

    elif ch.islower():
        lowercase += 1

    elif ch.isdigit():
        digits += 1

    elif ch == " ":
        spaces += 1

    elif ch != "\n":
        special += 1

print("Uppercase letters:", uppercase)
print("Lowercase letters:", lowercase)
print("Digits:", digits)
print("Spaces:", spaces)
print("Special characters:", special)
```

---

## Question 7

Write a program that accepts a word from the user and searches for that word in cryptology.txt.

### Answer

```python
# Search for a word in cryptology.txt

word = input("Enter the word to search: ")

found = False

with open("cryptology.txt", "r") as file:

    line_number = 1

    for line in file:

        if word.lower() in line.lower():
            print("Word found in line", line_number, ":", line.strip())
            found = True

        line_number += 1

if not found:
    print("Word not found.")
```

---

## Question 8

Read cryptology.txt and display only the lines containing the word message.

### Answer

```python
# Display lines containing the word "message"

with open("cryptology.txt", "r") as file:

    for line in file:

        if "message" in line.lower():
            print(line.strip())
```

---

## Question 9

Write a Python program to read cryptology.txt, convert all alphabetic characters to uppercase, and store the result in a new file called normalized.txt.

### Answer

```python
# Convert all alphabetic characters to uppercase
# and store the result in normalized.txt

with open("cryptology.txt", "r") as input_file:
    with open("normalized.txt", "w") as output_file:

        for line in input_file:
            output_file.write(line.upper())

print("Normalized content stored in normalized.txt")
```

---

## Question 10

Write a program to read the file and print only the lines containing only alphabetic characters from the cryptology_no.txt file.

### Answer

```python
# Print only lines containing alphabetic characters

with open("cryptology_no.txt", "r") as file:

    for line in file:

        line = line.strip()

        if line.isalpha():
            print(line)
```

---

## Question 11

Write a program to get the string from the user and reverse the string.

### Answer

```python
# Accept a string from the user and reverse it

text = input("Enter a string: ")

reversed_text = text[::-1]

print("Reversed string:", reversed_text)
```

---

## Question 12

Improve the above code to reverse the string from the file.

### Answer

```python
# Read the string from the file and reverse it

with open("cryptology.txt", "r") as file:
    text = file.read()

reversed_text = text[::-1]

print("Reversed string:")
print(reversed_text)
```

---

## Question 13

Simulate the tac command in Python.

### Answer

```python
# Simulate the Linux tac command

with open("cryptology.txt", "r") as file:
    lines = file.readlines()

for line in reversed(lines):
    print(line, end="")
```

---

# Level 2: Regex

## security_data.txt

The contents of `security_data.txt` are:

```text
User alice logged in from 192.168.10.15
User bob logged in from 10.10.5.21
Contact admin@securitylab.com
Failed login attempts: 5
Session ID: SEC-2026-1045
Hash: a94f3c2d8e71b05f
Port 443 connection established
User admin failed authentication
```

---

## Question 1

Write a Python program to read security_data.txt and use a regular expression to identify and display all IPv4-address-like patterns present in the file.

### Answer

```python
import re

# Read security_data.txt

with open("security_data.txt", "r") as file:
    contents = file.read()

# Regular expression for IPv4-address-like patterns

pattern = r"\b(?:\d{1,3}\.){3}\d{1,3}\b"

addresses = re.findall(pattern, contents)

print("IPv4-address-like patterns:")

for address in addresses:
    print(address)
```

### Output

```text
IPv4-address-like patterns:
192.168.10.15
10.10.5.21
```

---

## Question 2

Write a Python program to identify and display all email-address-like patterns present in security_data.txt.

### Answer

```python
import re

# Read security_data.txt

with open("security_data.txt", "r") as file:
    contents = file.read()

# Regular expression for email-address-like patterns

pattern = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b"

emails = re.findall(pattern, contents)

print("Email-address-like patterns:")

for email in emails:
    print(email)
```

### Output

```text
Email-address-like patterns:
admin@securitylab.com
```

---

## Question 3

Write a Python program to extract session IDs that follow the format SEC-YYYY-NNNN, where YYYY and NNNN represent four digits.

### Answer

```python
import re

# Read security_data.txt

with open("security_data.txt", "r") as file:
    contents = file.read()

# Regular expression for SEC-YYYY-NNNN

pattern = r"\bSEC-\d{4}-\d{4}\b"

session_ids = re.findall(pattern, contents)

print("Session IDs:")

for session_id in session_ids:
    print(session_id)
```

### Output

```text
Session IDs:
SEC-2026-1045
```

---

## Question 4

Write a Python program to identify all hexadecimal sequences containing the characters 0–9, a–f, or A–F.

### Answer

```python
import re

# Read security_data.txt

with open("security_data.txt", "r") as file:
    contents = file.read()

# Regular expression for hexadecimal sequences

pattern = r"\b[0-9A-Fa-f]+\b"

hex_values = re.findall(pattern, contents)

print("Hexadecimal sequences:")

for value in hex_values:
    print(value)
```

---

## Question 5

Write a Python program to read security_data.txt and display all lines containing the word failed, irrespective of uppercase or lowercase.

### Answer

```python
import re

# Read security_data.txt line by line

with open("security_data.txt", "r") as file:

    for line in file:

        if re.search(r"\bfailed\b", line, re.IGNORECASE):
            print(line.strip())
```

### Output

```text
Failed login attempts: 5
User admin failed authentication
```

---

## Question 6

Write a Python program to identify and extract the port number from statements of the form Port 443 connection established.

### Answer

```python
import re

# Read security_data.txt

with open("security_data.txt", "r") as file:
    contents = file.read()

# Regular expression to extract the port number

pattern = r"\bPort\s+(\d+)\s+connection\s+established\b"

match = re.search(pattern, contents, re.IGNORECASE)

if match:
    port_number = match.group(1)
    print("Port number:", port_number)
else:
    print("Port number not found.")
```

### Output

```text
Port number: 443
```

---

# Files Used

- `cryptology.txt`
- `cryptology_no.txt`
- `normalized.txt`
- `security_data.txt`
