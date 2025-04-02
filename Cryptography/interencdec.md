# [interencdec](https://play.picoctf.org/practice/challenge/418)

## **Challenge Information**

- **Category**: Cryptography  
- **Difficulty**: Easy  
- **Description**: Can you get the real meaning from this file?

## **Solution Overview**

This challenge involves multiple layers of encoding and encryption. The solution requires the following steps:

1. Decode a Base64 string.
2. Decode another Base64 string found inside.
3. Decrypt a Caesar cipher to obtain the flag.

## **Hints**

- Understanding multiple decoding processes is crucial.

## **Detailed Walkthrough**

### **Step 1: Initial Base64 Decoding**

We start by examining the content provided in the file. The first string is:

```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyMHdNakV5TnpVNGZRPT0nCg==
```

We use a Base64 decoder to decode it (e.g., [base64decode.org](https://www.base64decode.org/)), which gives us the following:

```
b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX20wMjEyNzU4fQ=='
```

The `b` here is not part of the encoded message but indicates the **Caesar cipher shift key** (`b = 3`).

### **Step 2: Second Base64 Decoding**

The result we got from the first decoding (`d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX20wMjEyNzU4fQ==`) is another Base64-encoded string. We now decode this second layer, and the result is:

```
wpjvJAM{jhlzhy_k3jy9wa3k_m0212758}
```

This looks like a flag but is obfuscated by some character shifts.

### **Step 3: Caesar Cipher Decryption**

The string `wpjvJAM{jhlzhy_k3jy9wa3k_m0212758}` is encrypted using a **Caesar cipher** with a shift of **3**, indicated by the "b" from the first decoding step.

To decrypt the string, we apply the Caesar cipher decryption with a shift of 3. The decrypted string is:

```
picoCTF{caesar_d3cr9pt3d_f0212758}
```

## **Flag**

```
picoCTF{caesar_d3cr9pt3d_f0212758}
```

## **Learning Points**

- **Multiple Encoding Layers**: Recognizing when data has been encoded multiple times is key to solving the challenge.
- **Base64 Encoding**: Understanding Base64 encoding and how to decode it is essential for tackling similar challenges.
- **Caesar Cipher**: The Caesar cipher is a simple yet effective substitution cipher, and knowing how to apply it can be very useful in cryptography challenges.
- **Online Cryptographic Tools**: Utilizing online tools like Base64 decoders and Caesar cipher decryption tools can help solve these types of challenges efficiently.

## **References**

- [Base64 Decode Online Tool](https://www.base64decode.org/)
- [Caesar Cipher Online Tool](https://www.dcode.fr/caesar-cipher)