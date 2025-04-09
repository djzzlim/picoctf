# [binhexa](https://play.picoctf.org/practice/challenge/404)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: How well can you perform basic binary operations?

## Solution Overview

This challenge tests your understanding of binary operations. You're given two binary numbers and must perform six different operations on them in sequence. After correctly performing all operations, you need to convert the final result to hexadecimal to receive the flag.

## Hints
None provided in the challenge.

## Detailed Walkthrough

### Step 1: Understanding the Challenge
When connecting to the server, we're presented with two binary numbers and a series of operations to perform:
```
Binary Number 1: 11111011 (251 in decimal)
Binary Number 2: 11000011 (195 in decimal)
```

### Step 2: Performing the Binary Operations
For each operation, we need to calculate the correct binary result:
#### Operation 1: Bitwise AND (`&`)
```
11111011 & 11000011 = 11000011
```
This operation returns 1 only when both corresponding bits are 1.
#### Operation 2: Addition (`+`)
```
11111011 + 11000011 = 110111110
```
Adding the two binary numbers together (251 + 195 = 446).
#### Operation 3: Bitwise OR (`|`)
```
11111011 | 11000011 = 11111011
```
This operation returns 1 if either corresponding bit is 1.

#### Operation 4: Left Shift (`<<`)
```
11111011 << 1 = 111110110
```
Shifting the first number left by 1 bit (multiplying by 2).

#### Operation 5: Right Shift (`>>`)
```
11000011 >> 1 = 1100001
```
Shifting the second number right by 1 bit (dividing by 2).

#### Operation 6: Multiplication (`*`)
```
11111011 * 11000011 = 1011111100110001
```
Multiplying the two binary numbers (251 × 195 = 48,945).

### Step 3: Converting to Hexadecimal
The final result from Operation 6 needs to be converted to hexadecimal:
```
1011111100110001 (binary) = 48945 (decimal) = BF31 (hexadecimal)
```

### Step 4: Submitting and Getting the Flag
After submitting "BF31" as the answer, we receive the flag:
```
picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_1367e2c6}
```

### Automated Solution
To solve this challenge efficiently, I wrote a Python script using the `pwntools` library:
```python
from pwn import *

r = remote('titan.picoctf.net', 55186)

r.recvuntil(b"Binary Number 1: ")
num1 = int(r.recvline().strip().decode(), 2)
print(f"Binary Number 1: {bin(num1)[2:]}")

r.recvuntil(b"Binary Number 2: ")
num2 = int(r.recvline().strip().decode(), 2)
print(f"Binary Number 2: {bin(num2)[2:]}")

for i in range(1, 7):
    r.recvuntil(f"Operation {i}: ".encode())
    operation = r.recvline().strip().decode().strip("'")
    print(f"Operation {i}: '{operation}'")

    if operation == '&':
        result = num1 & num2
    elif operation == '+':
        result = num1 + num2
    elif operation == '|':
        result = num1 | num2
    elif operation == '<<':
        result = num1 << 1
    elif operation == '>>':
        result = num2 >> 1
    elif operation == '*':
        result = num1 * num2
    else:
        print(f"Unknown operation received: {operation}")
        raise ValueError(f"Unknown operation: {operation}")

    r.recvuntil(b"Enter the binary result: ")
    binary_result = bin(result)[2:]
    print(f"Sending binary result: {binary_result}")
    r.sendline(binary_result.encode())

r.recvuntil(b"Enter the results of the last operation in hexadecimal: ")
result_hex = hex(result)[2:].upper()
print(f"Hexadecimal result: {result_hex}")
r.sendline(result_hex.encode())

r.recvuntil(b"The flag is: ")
flag = r.recvline().decode().strip()
print(flag)
```

This script:

1. Connects to the challenge server
2. Parses the binary numbers
3. Handles each operation as it's presented
4. Calculates the correct result
5. Converts to the required format (binary or hexadecimal)
6. Retrieves the flag

## Flag
```
picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_1367e2c6}
```

## Learning Points

- **Binary Representation**: Converting between binary, decimal, and hexadecimal
- **Bitwise Operations**: Understanding AND (`&`), OR (`|`), and shift operations (`<<`, `>>`)
- **Binary Arithmetic**: Adding and multiplying binary numbers
- **Automation**: Using programming to solve repetitive challenges efficiently

## References

- [Binary Number System](https://en.wikipedia.org/wiki/Binary_number)
- [Bitwise Operations](https://en.wikipedia.org/wiki/Bitwise_operation)