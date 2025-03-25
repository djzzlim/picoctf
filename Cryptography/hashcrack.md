# [hashcrack](https://play.picoctf.org/practice/challenge/475)

## Challenge Information

- **Category**: Cryptography
- **Difficulty**: Easy
- **Description**: A company stored a secret message on a server, which got breached due to the admin using weakly hashed passwords. Your task is to crack the given hashes and retrieve the secret flag.

## Solution Overview

This challenge involves **cracking weakly hashed passwords** using common password lists or online hash databases. We are given three different hashes (MD5, SHA-1, and SHA-256) and need to find their corresponding plaintext values.

## Hints

- **Understanding hashes is crucial. [Read more here](https://primer.picoctf.org/#_hashing).**
- **Identify the hash algorithm based on its length and structure.**
- **Use online hash lookup tools or hash-cracking utilities.**

## Detailed Walkthrough

### Step 1: Connecting to the Server

Use `nc` (netcat) to connect to the given challenge server:

```bash
nc verbal-sleep.picoctf.net 62644
```

The server provides the following hash to crack:

```
We have identified a hash: 482c811da5d5b4bc6d497ffa98491e38
Enter the password for identified hash:
```

### Step 2: Identifying and Cracking MD5

- The hash `482c811da5d5b4bc6d497ffa98491e38` is **32 characters long**, indicating it is an **MD5 hash**.
- Using an **online hash lookup tool** (e.g., CrackStation, `https://10015.io/tools/md5-encrypt-decrypt`), we find the plaintext is:
  
  ```
  password123
  ```

- Entering `password123` returns:
  
  ```
  Correct! You've cracked the MD5 hash with no secret found!
  ```

### Step 3: Identifying and Cracking SHA-1

The next hash is:

```
b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

- This hash is **40 characters long**, which is typical for **SHA-1**.
- Using an **SHA-1 hash lookup tool**, we find the plaintext is:
  
  ```
  letmein
  ```

- Entering `letmein` returns:
  
  ```
  Correct! You've cracked the SHA-1 hash with no secret found!
  ```

### Step 4: Identifying and Cracking SHA-256

The final hash is:

```
916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
```

- This hash is **64 characters long**, which is typical for **SHA-256**.
- Using an **SHA-256 hash lookup tool**, we find the plaintext is:
  
  ```
  qwerty098
  ```

- Entering `qwerty098` reveals the **flag**:
  
  ```
  picoCTF{UseStr0nG_h@shEs_&PaSswDs!_3eb19d03}
  ```

## Tools and Resources Used

- **Online hash lookup tools:**
  - [MD5 Decrypt](https://10015.io/tools/md5-encrypt-decrypt)
  - [SHA-1 Decrypt](https://10015.io/tools/sha1-encrypt-decrypt)
  - [SHA-256 Decrypt](https://10015.io/tools/sha256-encrypt-decrypt)

## Flag

```
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_3eb19d03}
```

## Learning Points

- **Different hash functions have different lengths:**
  - MD5: 32 characters
  - SHA-1: 40 characters
  - SHA-256: 64 characters
- **Weak passwords are easily cracked using online tools.**
- **Always use strong hashing algorithms with salt (e.g., bcrypt, Argon2).**

## Mitigation Strategies

To prevent such security risks, follow these best practices:

- **Use strong hashing algorithms** like bcrypt, scrypt, or Argon2 instead of MD5/SHA-1.
- **Implement password salting** to prevent hash lookup attacks.
- **Enforce strong password policies** (long, complex, unique passwords).
- **Monitor for leaked credentials** using tools like Have I Been Pwned.

## References

- [MD5 vs SHA-1 vs SHA-2](https://www.freecodecamp.org/news/md5-vs-sha-1-vs-sha-2-which-is-the-most-secure-encryption-hash-and-how-to-check-them/)
- [10015 Tools](https://10015.io/)