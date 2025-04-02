# [Secret of the Polyglot](https://play.picoctf.org/practice/challenge/423)

## Challenge Information

- **Category**: Forensics  
- **Difficulty**: Easy  
- **Description**: The Network Operations Center (NOC) picked up a suspicious file with conflicting information on what type of file it is. Can you extract all the information from this strange file?

## Solution Overview

This challenge involves analyzing a polyglot file - a file that is valid as multiple file formats simultaneously. By examining the file in different ways, we can extract pieces of the flag and combine them to get the complete flag.

## Hints

1. This problem can be solved by just opening the file in different ways.

## Detailed Walkthrough

### Step 1: Identifying the File Type

First, we use the `file` command to identify what the system thinks the file is:

```bash
file flag2of2-final.pdf 
```

This returns:
```
flag2of2-final.pdf: PNG image data, 50 x 50, 8-bit/color RGBA, non-interlaced
```

Interestingly, although the file has a `.pdf` extension, the system identifies it as a PNG image. This confirms we're dealing with a polyglot file that can be interpreted as both formats.

### Step 2: Examining the File as a PDF

When opening the file as a PDF, we can see text that appears to be part of the flag:

```
1n_pn9_&_pdf_2a6a1ea8}
```

This appears to be the end portion of the flag.

### Step 3: Examining the File as a PNG

Since the file was also identified as a PNG image, we can copy the file with a PNG extension to view it properly:

```bash
cp flag2of2-final.pdf flag1of2-final.png
```

When opening this PNG file, we can see the beginning portion of the flag:

```
picoCTF{f1u3n7_
```

### Step 4: Combining the Flag Parts

By combining both parts of the flag, we get the complete flag:

```
picoCTF{f1u3n7_1n_pn9_&_pdf_2a6a1ea8}
```

## Flag

```
picoCTF{f1u3n7_1n_pn9_&_pdf_2a6a1ea8}
```

## Learning Points

- **Digital Forensics**: Techniques for extracting hidden information from files
- **File Format Specifications**: Knowledge of how different file formats store data

## Mitigation Strategies

To detect polyglot files in security contexts:
- **Deep Inspection**: Don't rely solely on file extensions or single identification methods
- **Content Validation**: Verify file content matches its claimed format

## References

- [File Format Polyglots](https://en.wikipedia.org/wiki/Polyglot_(computing))