# [Browser WebShell Solvable](https://play.picoctf.org/practice/challenge/414)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: Know of little and big endian?

## Solution Overview

This challenge tests understanding of endianness in computer systems. After launching the instance, we're presented with an interactive web shell that asks us to provide the little-endian and big-endian representations of a given word. Successfully providing both representations reveals the flag.

## Hints

1. You might want to check the ASCII table to first find the hexadecimal representation of characters before finding the endianness.
2. Read more about endianness [here](https://levelup.gitconnected.com/little-endian-and-big-endian-74ab6441b2a7)

## Detailed Walkthrough

### Step 1: Understanding Endianness

Endianness refers to the order in which bytes are stored in computer memory:
- **Big-Endian**: Most significant byte first (natural reading order)
- **Little-Endian**: Least significant byte first (reverse reading order)

### Step 2: Launching the Instance

After launching the instance, we're presented with a prompt asking us to find both the little-endian and big-endian representations of the word "nymie".

### Step 3: Converting Characters to Hexadecimal

First, we convert each character to its ASCII hexadecimal value:

```
n = ASCII 110 = 0x6E
y = ASCII 121 = 0x79
m = ASCII 109 = 0x6D
i = ASCII 105 = 0x69
e = ASCII 101 = 0x65
```

### Step 4: Determining Endian Representations

#### Big-Endian Representation
For big-endian, bytes are arranged in their natural reading order (left-to-right):
```
6E 79 6D 69 65
```
Without spaces: `6E796D6965`

#### Little-Endian Representation
For little-endian, bytes are arranged in reverse order (right-to-left):
```
65 69 6D 79 6E
```
Without spaces: `65696D796E`

### Step 5: Submitting the Answers

When prompted, we submit:
- Little-Endian representation: `65696D796E`
- Big-Endian representation: `6E796D6965`

After correctly submitting both representations, we receive the flag.

## Flag

```
picoCTF{3ndi4n_sw4p_su33ess_817b7cfe}
```

## Learning Points

- **Endianness**: Understanding how different computing systems store multi-byte values
- **ASCII Encoding**: Converting text characters to their hexadecimal representations
- **Byte Ordering**: Recognizing the importance of byte order in various computing contexts

## Mitigation Strategies

In real-world applications:
- **Endianness Awareness**: Be mindful of endianness when working with binary data or network protocols
- **Conversion Functions**: Use proper conversion functions (like `htons`, `ntohl`) when transferring data between systems with different endianness

## References

- [Endianness Wikipedia](https://en.wikipedia.org/wiki/Endianness)
- [ASCII Table](https://www.asciitable.com/)