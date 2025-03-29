# [Flag Hunters](https://play.picoctf.org/practice/challenge/472)

## Challenge Information

- **Category**: Reverse Engineering
- **Difficulty**: Easy
- **Description**: Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it?

## Solution Overview

This challenge involves **analyzing a program’s control flow** and **manipulating user input** to make it reveal a hidden part of the lyrics that contains the flag. The key vulnerability is an **unsanitized user input** that can be leveraged to alter execution flow.

## Hints

- **Unsanitized user input is always good, right?**
- **Is there any syntax that is ripe for subversion?**
- **The program can easily get into undefined states. Don't be shy about Ctrl-C.**

## Detailed Walkthrough

### Step 1: Analyzing the Provided Code

The program reads and prints lines of a song, following a structured format. It jumps to different sections based on specific keywords:

- `REFRAIN` jumps to a predefined refrain.
- `RETURN` returns to a stored line number.
- `CROWD` takes user input.
- `END` terminates the program.

However, **unsanitized input** allows us to manipulate the program’s execution.

### Step 2: Running the Program

We connect to the challenge using netcat:

```bash
nc verbal-sleep.picoctf.net 60855
```

The program starts printing the song lyrics based on its structured format, looping through verses and refrains.

### Step 3: Identifying the Exploit

- The program splits lines using `;`, allowing injection of custom control flow changes.
- The `CROWD` input is not sanitized, meaning we can insert control flow directives such as `RETURN`.

### Step 4: Triggering the Hidden Refrain

To force the program to print the hidden intro (which contains the flag), we input:

```
;RETURN 0
```

This effectively **resets the execution** to the beginning, causing the program to print `secret_intro`, which contains the flag.

### Step 5: Retrieving the Flag

The output reveals:

```
Pico warriors rising, puzzles laid bare,
Solving each challenge with precision and flair.
With unity and skill, flags we deliver,
The ether’s ours to conquer, picoCTF{70637h3r_f0r3v3r_250bd6ef}
```

## Tools and Resources Used

- **Netcat (`nc`)**: For interacting with the challenge server.
- **Python Code Analysis**: Reviewing the provided script to understand its logic.

## Flag

```
picoCTF{70637h3r_f0r3v3r_250bd6ef}
```

## Learning Points

- **Understanding control flow in Python scripts**.
- **Identifying vulnerabilities in unsanitized user inputs**.
- **Using input manipulation to alter program execution**.
- **Leveraging delimiters (`;`) in string processing for injection attacks**.

## Mitigation Strategies

To prevent such vulnerabilities in real-world applications:

- **Sanitize user input** to prevent execution control manipulation.
- **Implement input validation and whitelisting**.

## References

- [Python String Manipulation](https://docs.python.org/3/library/stdtypes.html#string-methods)