# [Verify](https://play.picoctf.org/practice/challenge/450)

## Challenge Information
- **Category**: Forensics
- **Difficulty**: Easy
- **Description**: People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.

## Challenge Access
- **SSH Command:**
    ```sh
    ssh -p 56762 ctf-player@rhea.picoctf.net
    ```
- **Password:** `6abf4a82`
- **Checksum:**
    ```sh
    b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2
    ```

## Hints
- Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
- You can create a SHA checksum of a file with `sha256sum <file>` or all files in a directory with `sha256sum <directory>/*`.
- Remember you can pipe the output of one command to another with |. Try practicing with the 'First Grep' challenge if you're stuck!

## Solution Overview
The challenge requires verifying a file using a provided SHA-256 checksum and decrypting it to retrieve the flag.

## Detailed Walkthrough

### Step 1: Connect to the Remote Server
To start, connect to the given SSH server using the credentials:

```sh
ssh -p 56762 ctf-player@rhea.picoctf.net
```
Password: `6abf4a82`

### Step 2: List Available Files
Once connected, list the files in the directory:

```sh
ls -l
```
Output:
```
files/  decrypt.sh  checksum.txt
```

### Step 3: Verify the Correct File
We need to determine which file in the `files/` directory matches the provided SHA-256 hash. We use `sha256sum` and `grep -f` to find a match:

```sh
sha256sum files/* | grep -f checksum.txt
```
Output:
```
b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2  files/451fd69b
```
The file `files/451fd69b` matches the given checksum.

### Step 4: Decrypt the Flag
Now that we have identified the correct file, we use the provided script to decrypt it:

```sh
./decrypt.sh files/451fd69b
```
Output:
```
picoCTF{trust_but_verify_451fd69b}
```

### Step 5: Retrieve and Submit the Flag
The flag obtained is:

```
picoCTF{trust_but_verify_451fd69b}
```

## Tools and Resources Used
- **sha256sum**: To compute and verify file checksums.
- **grep -f**: To compare hash outputs efficiently.

## Flag
``` 
picoCTF{trust_but_verify_451fd69b}
```

## Learning Points
- Understanding SHA-256 checksum verification.
- Using `grep` to match specific data.

## References
- [Linux sha256sum Command](https://linux.die.net/man/1/sha256sum)
- [Using grep for Pattern Matching](https://www.gnu.org/software/grep/manual/grep.html)