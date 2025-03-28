# [RED](https://play.picoctf.org/practice/challenge/460)

## Challenge Information

- **Category**: Forensics
- **Difficulty**: Easy
- **Description**: RED, RED, RED, RED

## Solution Overview

This challenge involves **steganography and metadata analysis** on the provided image ([`red.png`](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)). By extracting hidden data from the image using various forensic tools, we uncover a **Base64-encoded flag** hidden in its least significant bits (LSB).

## Hints

  - **The picture seems pure, but is it though?**
  - **Red? Ged? Bed? Aed?**
  - **Check whatever Facebook is called now.**

## Detailed Walkthrough

### Step 1: Checking Metadata with ExifTool

We start by examining the metadata of the image using `exiftool`:

```bash
exiftool red.png
```

The output contains a poem under the **Poem** field:

```
Crimson heart, vibrant and bold,
Hearts flutter at your sight.
Evenings glow softly red,
Cherries burst with sweet life.
Kisses linger with your warmth.
Love deep as merlot.
Scarlet leaves falling softly,
Bold in every stroke.
```

However, this doesn’t seem to reveal the flag directly. We move on to deeper steganographic analysis.

### Step 2: Analyzing Hidden Data with `zsteg`

`zsteg` is a tool for detecting hidden messages in **PNG images** by analyzing the least significant bits (LSB). Running it on `red.png`:

```bash
zsteg red.png
```

The output includes multiple findings. The most relevant line is:

```
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
```

This is **Base64-encoded text**.

### Step 3: Decoding Base64

We decode the extracted text using `base64`:

```bash
echo 'cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==' | base64 -d
```

This reveals the flag:

```
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```

## Tools and Resources Used

- **ExifTool**: For extracting metadata from images.
- **zsteg**: For analyzing PNG files for steganography.
- **Base64 decoder**: To decode hidden text.

## Flag

```
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```

## Learning Points

- **Metadata can store hidden information** in image files.
- **LSB steganography** is a common technique for hiding data in images.
- **Base64 encoding** is often used to store hidden messages.

## Mitigation Strategies

To detect and prevent such hidden data leaks in real-world applications:

- **Use forensic tools like `zsteg` and `exiftool` to analyze media files.**
- **Check for unexpected metadata fields in images.**

## References

- [ExifTool Documentation](https://exiftool.org/)
- [zsteg GitHub](https://github.com/zed-0xff/zsteg)
- [Base64 Encoding/Decoding](https://www.base64decode.org/)