### BMP
| Format | Description | Extension | Mime Type | Specs | Wikipedia |
|--------|-------------|-----------|-----------|-------|-----------|
| BMP | Device-independent Bitmap | `.bmp`, <br> `.dip`, <br> `.rle` | `image/bmp`,<br> `image/x-bmp` | | [link][bmp: wikipedia.org]

#### Structure
| Name | Size | Required | Comments |
|------|------|----------|----------|
| Bitmap file header | 14 bytes | yes | |
| DIB header | 12, 40, 52, 56, 64, 108 or 124 bytes | yes | |
| Extra bit masks | 12 or 16 bytes | DIB header is `BITMAPINFOHEADER` and <br> Compression Method is `BI_BITFIELDS` or `BI_ALPHABITFIELDS` | |
| Color table | variable | Color depth ≤ 8 bits | |
| Gap1 | variable | no | Alignment |
| Pixel array | variable | yes | Padded to multiple of 4 bytes |
| Gap2 | variable | no | Alignment |
| ICC Color profile | no | variable | |

##### DIB Header
| Name | Size |
|------|-----:|
| `BITMAPCOREHEADER` | 12 bytes |
| `OS21XBITMAPHEADER` | 12 bytes |
| `BITMAPINFOHEADER` | 40 bytes |
| `BITMAPV2INFOHEADER` | 52 bytes |
| `BITMAPV3INFOHEADER` | 56 bytes |
| `BITMAPV4HEADER` | 108 bytes |
| `BITMAPV5HEADER` | 124 bytes |


#### Other resources
- [Bitmap File Structure][digicamsoft.com]
- [An introduction to DIBs (Device Independent Bitmaps)][herdsoft.com]
- *Dr. Dobb's journal of software tools*: [The BMP File Format, Part 1 By David Charlap][drdobbs.com]

[wikipedia]: https://en.wikipedia.org/wiki/BMP_file_format
[digicamsoft]: http://www.digicamsoft.com/bmp/bmp.html
[herdsoft]: http://www.herdsoft.com/ti/davincie/imex3j8i.htm
[drdobbs]: (http://www.drdobbs.com/architecture-and-design/the-bmp-file-format-part-1/184409517)
