# [CanYouSee](https://play.picoctf.org/practice/challenge/408)

## Challenge Information

- **Category**: Forensics
- **Difficulty**: Easy
- **Description**: How about some hide and seek?

## Solution Overview

This challenge tests understanding of metadata in image files. The flag is hidden in the metadata of the provided image file, specifically in a custom metadata field that contains a base64-encoded string.

## Hints

1. How can you view the information about the picture?
2. If something isn't in the expected form, maybe it deserves attention?

## Detailed Walkthrough

### Step 1: Examining the File Metadata

First, we download the image file `ukn_reality.jpg`. To examine its metadata, we use `exiftool`, a powerful tool for reading metadata from files:

```bash
exiftool ukn_reality.jpg
```

Output:
```
ExifTool Version Number         : 12.76
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:02:16 06:40:21+08:00
File Access Date/Time           : 2025:04:08 08:53:02+08:00
File Inode Change Date/Time     : 2025:04:08 08:52:59+08:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fYTZkZjhkYjh9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4
```

### Step 2: Identifying Unusual Metadata

Looking through the metadata, we notice an unusual field called `Attribution URL` with the value:
```
cGljb0NURntNRTc0RDQ3QV9ISUREM05fYTZkZjhkYjh9Cg==
```

This value appears to be base64-encoded text, as indicated by:
- The character set (a-z, A-Z, 0-9, +, /)
- The padding character (=) at the end

### Step 3: Decoding the Base64 String

We use the `base64` command-line tool to decode this string:

```bash
echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fYTZkZjhkYjh9Cg==" | base64 --decode
```

Output:
```
picoCTF{ME74D47A_HIDD3N_a6df8db8}
```

## Flag

```
picoCTF{ME74D47A_HIDD3N_a6df8db8}
```

## Learning Points

- **Metadata Examination**: Understanding how to extract and analyze metadata from files
- **Steganography Basics**: Recognizing that data can be hidden in non-visual components of an image
- **Base64 Encoding**: Identifying and decoding base64-encoded text
- **EXIF Data**: Learning about Extended File Information data in media files
- **Digital Forensics**: Basic forensic technique of examining all aspects of a file, not just its visual content

## Mitigation Strategies

To prevent metadata leakage in your own files:
- **Metadata Scrubbing**: Use tools to remove sensitive metadata before publishing files
- **Awareness**: Be conscious of what information might be embedded in files you share
- **Verification**: Check files for hidden metadata before sharing sensitive information
- **Policy Implementation**: Establish organizational policies for handling metadata in media files

## References

- [ExifTool Documentation](https://exiftool.org/)
- [Base64 Encoding/Decoding](https://www.base64decode.org/)