# [Scan Surprise](https://play.picoctf.org/practice/challenge/444)

## Challenge Information
- **Category**: Forensics
- **Difficulty**: Easy
- **Description**: I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?
You can download the challenge files here:

    [challenge.zip](https://artifacts.picoctf.net/c_atlas/15/challenge.zip)

    Additional details will be available after launching your challenge instance.

## Hints
1. QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
2. Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11.
3. If you don't have access to a phone, you can also use `zbar-tools` to convert an image to text.

## Solution Overview
The challenge provides an image containing a QR code. Our goal is to extract the flag from the image using either a mobile phone or command-line tools.

## Detailed Walkthrough
### Step 1: Download and Extract the Challenge Files
Download the challenge ZIP file and extract it:

```bash
wget https://artifacts.picoctf.net/c_atlas/15/challenge.zip
unzip challenge.zip
cd home/ctf-player/drop-in
ls
```

You'll find an image file (e.g., `flag.png`).

### Step 2: Read the QR Code
There are multiple ways to extract the QR code:

#### Method 1: Using a Mobile Phone
- Open the image on your screen.
- Use your phone’s camera to scan the QR code.
- It should display the flag as text.

#### Method 2: Using Linux CLI (`zbar-tools`)
If you're on Linux, install `zbar-tools` and extract the flag with:

```bash
sudo apt install zbar-tools
zbarimg flag.png
```

**Output:**
```
QR-Code:picoCTF{p33k_@_b00_19eccd10}
```

### Step 3: Alternative Python Solution
If you prefer Python, install `pyzbar` and `PIL`:

```bash
pip install pyzbar pillow
```

Run this script:

```python
from pyzbar.pyzbar import decode
from PIL import Image
decodeQR = decode(Image.open('./home/ctf-player/drop-in/flag.png').convert("RGBA"))
print(decodeQR[0].data.decode('ascii'))
```

**Output:**
```
picoCTF{p33k_@_b00_19eccd10}
```

## Tools and Resources Used
- `zbar-tools` (CLI tool for QR decoding)
- `pyzbar` (Python library for barcode decoding)
- `PIL` (Image processing in Python)

## Flag
```
picoCTF{p33k_@_b00_19eccd10}
```

## Learning Points
- QR codes store data beyond just URLs.
- `zbarimg` is a powerful tool for reading QR codes in Linux.
- Python’s `pyzbar` can be used to automate QR code decoding.

## References
- [Using `zbarimg` to decode QR codes](https://linux.die.net/man/1/zbarimg)
- [Python `pyzbar` documentation](https://pypi.org/project/pyzbar/)

