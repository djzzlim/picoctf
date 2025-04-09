# [Repetitions](https://play.picoctf.org/practice/challenge/371)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: Can you make sense of this file? Download the file [here](https://artifacts.picoctf.net/c/472/enc_flag).

## Solution Overview

The challenge provides an encrypted file that has been encoded multiple times using base64. Our task is to decode it repeatedly until we retrieve the original flag.

## Hints

- **Multiple decoding is always good.**

## Detailed Walkthrough

### Step 1: Understanding the Challenge

The challenge provides a file called `enc_flag`. Based on the hint about "multiple decoding," we can infer that the flag may have been encoded multiple times.

### Step 2: Examining the File

First, we download and examine the file content:

```bash
wget https://artifacts.picoctf.net/c/472/enc_flag
cat enc_flag
```

The output looks like base64-encoded data, which is typically represented using alphanumeric characters and ends with padding characters (`=`).

### Step 3: Attempting Single Decoding

Let's first try decoding the content once:

```bash
cat enc_flag | base64 --decode
```

The result is still not readable and appears to be another layer of base64-encoded text.

### Step 4: Applying Multiple Decodings

Since a single decoding didn't yield the flag, we need to apply multiple decodings. We can chain multiple decoding operations using Unix pipes:

```bash
cat enc_flag | base64 --decode | base64 --decode | base64 --decode | base64 --decode | base64 --decode | base64 --decode
```

After six consecutive base64 decoding operations, we finally get the flag:

```
picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_73494190}
```

## Tools and Resources Used

- **Base64 Decoding Utility**: Linux command-line tool for decoding base64 content.
- **Unix Pipes**: Used to chain multiple commands together.
- **Command Line Terminal**: To execute the commands and view results.

## Flag

```
picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_73494190}
```

## Learning Points

- **Nested Encoding**: Understanding that data can be encoded multiple times using the same algorithm.
- **Command Chaining**: Using Unix pipes to efficiently process data through multiple operations.
- **Base64 Encoding**: Recognizing and handling base64-encoded content, a common encoding scheme in CTF challenges.

## Mitigation Strategies

In real-world applications:

- **Avoid Security Through Obscurity**: Simply encoding data multiple times is not a secure encryption method.
- **Use Proper Encryption**: For sensitive data, use established encryption algorithms rather than encoding schemes.
- **Implement Authentication**: When transferring encoded data, include integrity checks to verify authenticity.

## References

- [Linux Base64 Command](https://linux.die.net/man/1/base64)
- [Command Line Piping](https://www.gnu.org/software/bash/manual/html_node/Pipelines.html)