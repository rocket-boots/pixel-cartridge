# pixel-cartridge
Save data as an image

One pixel is made up of three RGB values which can become:
* Three integers 0 - 255
* One big integer 0 - 16,646,655 (255^3 + 255^2 + 255)
* With last-digit steganography:
   * Three digits 0 - 9
   * One integer 000 - 999

Two pixels can become:
* Six integers 0 - 255
* Two big integers 0 - 16,646,655
* One massive integer
* With last-digit steganography:
   * Six digits 0 - 9
   * Two digits 000 - 999
   * One digit 000000 - 999,999

How to read the pixels:

1. Read pixels left-to-right, top-to-bottom
1. Get RGB values as integers (0-255)
1. Look at last digit of each color value, e.g. `110, 225, 34` becomes `054`
1. First pixel without all zeroes is the "guide" pixel, and is used to determine the format of reading the pixels

| Guide Code | Name | Steganography? | Each pixel becomes... | Compression | Characters | Start | End | Width |
| ---------- | ---- | -------------- | --------------------- | --- | --- | --- | --- | --- |
| `000` | Reserved | | | | | | |
| `555` | White / Configurable Steg. | Using last digits | An integer 000 - 999 | Config | Config | Config | Config |
| `550` | Yellow | Using last digits | int 000 - 999 |
| `055` | Cyan | Using last digits | int 000 - 999 |
| `050` | Green | No | 3 ints 0 - 255 | Config |  Config | Config | Config |
| `500` | Red / Minimal | No | 3 ints 0 - 255 | Dupes |  ASCII Halved | After | Black
| `005` | Blue / Simple | No | 3 ints 0 - 255 | None | ASCII Offset | Next Black (Allows for a header) | Black | Full |
| `505` | Magenta | ?




Configuration Pixels

2. `000` for ending guide pixel to determine pixel size (integer)
3. Game format (key/code, 001 - 999)
4. Format version (varies, RGB, 255-255-255, key/code)
5. game info (varies)
6. Color offset

Data

6. Start coords (integer)
7. End coords (integer)
* Size (large integer)

Decoding 

7. Compression format (000-999, key/code)
8. ASCII vs. ASCII extended vs. unicode

* Start coords (integer)
* End coords (integer)

* ASCII start number

Game Format Codes

| Code | Game | Example Colors |
| ---- | ---- | ------ |
| `000` | Reserved | Black, Gainsboro, Linen, Tan, Steelblue, Darkgreen, Lavender, Khaki, Lightgoldenrodyellow, Crimson |
| 
