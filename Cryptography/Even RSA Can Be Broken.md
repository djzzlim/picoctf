# [Even RSA Can Be Broken](https://play.picoctf.org/practice/challenge/470)

## Challenge Information

- **Category**: Cryptography
- **Difficulty**: Easy
- **Description**: This service provides you an encrypted flag. Can you decrypt it with just N & e?

## Solution Overview

This challenge exploits weak RSA key generation, where **N is factorizable into two prime numbers (p and q)**. Once we factorize N, we can compute the private key and decrypt the ciphertext.

## Hints

- **How much do we trust randomness?**
- **Notice anything interesting about N?**
- **Try comparing N across multiple requests.**

## Detailed Walkthrough

### Step 1: Retrieving RSA Parameters

We connect to the challenge using netcat:

```bash
nc verbal-sleep.picoctf.net 58750
```

The program provides:

```
N: 24543837542973208784626796893021731311347223546202724462520980967227152432647070186984787950171930076617181218715300665535434088199693757945484577662443038
e: 65537
cyphertext: 11648107522042090318586862854408990255636490145372862177525196153960978420045716945015661619341853232930792062292396806881898921201072537300290553487808277
```

### Step 2: Identifying the Weakness

- **RSA works by multiplying two prime numbers (p and q) to generate N.**
- **If N is small enough and only consists of two prime factors, we can factorize it easily.**
- **Once we obtain p and q, we compute the private key (d) using Euler’s totient function.**

### Step 3: Factorizing N

We use Python's `sympy.factorint` to factorize N:

```python
from sympy import factorint
p, q = list(factorint(N).keys())
```

This gives us the two prime factors, allowing us to compute **φ(N)**:

```python
phi = (p - 1) * (q - 1)
```

### Step 4: Computing the Private Key (d)

The private key is derived using the modular inverse:

```python
from Crypto.Util.number import inverse
d = inverse(e, phi)
```

### Step 5: Decrypting the Ciphertext

Using RSA decryption:

```python
plaintext = pow(ciphertext, d, n)
```

Finally, we convert the decrypted integer back to bytes:

```python
from Crypto.Util.number import long_to_bytes
flag = long_to_bytes(plaintext).decode()
print(flag)
```

### Full Exploit Code

```python
from pwn import *
from sympy import factorint
from Crypto.Util.number import inverse, long_to_bytes

# Connect to challenge server
t = remote('verbal-sleep.picoctf.net', 58750)

t.recvuntil(b"N: ")
n = int(t.recvline().strip().decode())
t.recvuntil(b"e: ")
e = int(t.recvline().strip().decode())
t.recvuntil(b"cyphertext: ")
ciphertext = int(t.recvline().strip().decode())

# Factorize N
factors = factorint(n)
p, q = list(factors.keys())

# Compute phi and d
phi = (p - 1) * (q - 1)
d = inverse(e, phi)

# Decrypt the ciphertext
plaintext = pow(ciphertext, d, n)
flag = long_to_bytes(plaintext).decode()
print(flag)
```

### Step 6: Retrieving the Flag

After running the script, we obtain:

```
picoCTF{tw0_1$_pr!m33991588e}
```

## Tools and Resources Used

- **Python (`pwn`, `sympy`, `pycryptodome`)**: For automating the exploit.
- **Netcat (`nc`)**: For connecting to the remote service.
- **Factorization techniques**: Understanding RSA weaknesses.

## Flag

```
picoCTF{tw0_1$_pr!m33991588e}
```

## Learning Points

- **RSA encryption relies on the difficulty of factoring large numbers.**
- **Weak key generation can make RSA vulnerable if N is easily factorizable.**
- **Understanding Euler’s totient function and modular inverses is key to breaking RSA.**
- **Python provides useful libraries like `sympy` and `pycryptodome` for cryptographic analysis.**

## Mitigation Strategies

To prevent such vulnerabilities in real-world applications:

- **Ensure N is large enough and generated using strong randomness.**
- **Use proper key generation techniques to avoid factorizable N.**

## References

- [The RSA Encryption Algorithm (1 of 2: Computing an Example)](https://www.youtube.com/watch?v=4zahvcJ9glg)
- [The RSA Encryption Algorithm (2 of 2: Generating the Keys)](https://www.youtube.com/watch?v=oOcTVTpUsPQ)
- [Python SymPy Factorization](https://docs.sympy.org/latest/modules/ntheory.html#sympy.ntheory.factor_.factorint)
- [Python PyCryptodome](https://pycryptodome.readthedocs.io/en/latest/)

