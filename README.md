# Documentation on image formats

## General
- Wikipedia: [Image file formats](https://en.wikipedia.org/wiki/Image_file_formats)
- Wikipedia category: [Graphic File Formats](https://en.wikipedia.org/wiki/Category:Graphics_file_formats)

## Pixel formats
- [Dr. Bill's Notes on "Little Endian" vs. "Big Endian"](https://people.cs.umass.edu/~verts/cs32/endian.html)
- MSDN blog: [Pixel Formats (Part 1: Unsigned Integers)](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx)
- MSDN blog: [Pixel Formats (Part 2: Fixed Point and Floating Point)](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx)
- Wikipedia: [Color depth](https://en.wikipedia.org/wiki/Color_depth)
- Wikipedia: [Indexed color](https://en.wikipedia.org/wiki/Indexed_color)

### Image file formats supporting indexed color
| Format | 1-bit | 2-bit | 3-bit | 4-bit | 5-bit | 6-bit | 7-bit | 8-bit |
|--------|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| [BMP](#bmp)    |   x   |       |       |   x   |       |       |       |   x   |
| GIF    |   x   |   x   |   x   |   x   |   x   |   x   |   x   |   x   |
| ILBM   |   x   |   x   |   x   |   x   |   x   |   x   |   x   |   x   |
| PCX    |   x   |   x   |       |   x   |       |       |       |   x   |
| PNG    |   x   |   x   |       |   x   |       |       |       |   x   |
| PSD    |       |       |       |       |       |       |       |   x   |
| TGA    |       |       |       |       |       |       |       |   x   |
| TIFF   |   x   |   x   |   x   |   x   |   x   |   x   |   x   |   x   |

*source: [Indexed color (wikipedia.org)](https://en.wikipedia.org/wiki/Indexed_color)*


### Endianess
| Format | Description                   | Endianess     |
|--------|-------------------------------|---------------|
| AVI    | Microsoft RIFF                |          Both |
| BMP    | Windows and OS/2 Bitmaps      | Little Endian |
| DXF    | AutoCad                       |      Variable |
| GIF    |                               | Little Endian |
| IMG    | GEM Raster                    |    Big Endian |
| JPEG   |                               |    Big Endian |
| FLI    | Autodesk Animator             | Little Endian |
| PCX    | PC Paintbrush                 | Little Endian |
| PNG    |                               |    Big Endian |
| PSD    | Adobe Photoshop               |    Big Endian |
| QTM    | Quicktime Movies              | Little Endian |
| RTF    | Microsoft Rich Text Format    | Little Endian |
| SGI    | Silicon Graphics              |    Big Endian |
| TGA    | Targa                         | Little Endian |
| TIFF   |                               |          Both |
| WAV    | Microsoft RIFF                |          Both |
| WPG    | WordPerfect Graphics Metafile |    Big Endian |
| XWD    | X Window Dump                 |          Both |

*source: [Dr. Bill's Notes on "Little Endian" vs. "Big Endian"]()*

## Colors
### Color spaces
- MSDN blog: [HDR and Color Spaces](http://blogs.msdn.com/b/billcrow/archive/2007/10/25/hdr-and-color-spaces.aspx)

### Palettes
- Wikipedia: [List of monochrome and RGB palettes](https://en.wikipedia.org/wiki/List_of_monochrome_and_RGB_palettes)

## File formats

### Overview

#### Major Formats
| Format | Description | Extension | Mime Type | Specs | Wikipedia |
|--------|-------------|-----------|-----------|-------|-----------|
| BMP | Device-independent Bitmap | `.bmp`, `.dip`, `.rle` | `image/bmp`, `image/x-bmp` | | [wikipedia.org](https://en.wikipedia.org/wiki/BMP_file_format)
| GIF | Graphics Interchange Format | `.gif` | `image/gif` | [w3.org]( 	www.w3.org/Graphics/GIF/spec-gif89a.txt) | [wikipedia.org](https://en.wikipedia.org/wiki/Graphics_Interchange_Format)
| JPEG | Joint Photographic Experts Group | `.jpg`, `.jpeg`, `.jpe`, `.jif`, `.jfif`, `.jfi` | `image/jpeg` | [jpeg.org](http://www.jpeg.org/jpeg/) | [wikipedia.org](https://en.wikipedia.org/wiki/JPEG)
| PNG | Portable Network Graphics | `.png` | |  [w3.org](https://www.w3.org/TR/PNG/#3sample) | [wikipedia.org](https://nl.wikipedia.org/wiki/Portable_Network_Graphics)
| PSD | Adobe Photoshop Document | `.psd` | | | [wikipedia.org](https://en.wikipedia.org/wiki/Adobe_Photoshop#features)
| TIFF | Tagged Image File Format | `.tif`, `.tiff` | `image/tiff`, `image/tiff-fx` | [adobe.com](http://partners.adobe.com/public/developer/tiff/) | [wikipedia.org](https://en.wikipedia.org/wiki/Tagged_Image_File_Format)

#### Others
| Format | Description | Extension | Mime Type | Specs | Wikipedia |
|--------|-------------|-----------|-----------|-------|-----------|
| ILBM | InterLeaved BitMap | `.lbm`, `.iff` | |  | [wikipedia.org](https://en.wikipedia.org/wiki/ILBM)
| JPEG 2000 | JPEG 2000 | `.jp2`, `.j2k`, `.jpf`, `.jpx`, `.jpm`, `.mj2` | `image/jp2`, `image/jpx`, `image/jpm`, `video/mj2` | | [wikipedia.org](https://en.wikipedia.org/wiki/JPEG_2000)
| PCX | PC Paintbrush Image File | `.pcx` | |  | [wikipedia.org](https://en.wikipedia.org/wiki/PCX)
| TGA | TARGA File Format | `.tga`, `.vda`, `.icb`, `.vst` | | | [wikipedia.org](https://en.wikipedia.org/wiki/Truevision_TGA)


### BMP
| Format | Description | Extension | Mime Type | Specs | Wikipedia |
|--------|-------------|-----------|-----------|-------|-----------|
| BMP | Device-independent Bitmap | `.bmp`, <br> `.dip`, <br> `.rle` | `image/bmp`,<br> `image/x-bmp` | | [link][bmp: wikipedia.org]

#### Structure
| Name | Size | Required | Comments |
|------|------|----------|----------|
| Bitmap file header | 14 bytes | yes | |
| [DIB header][dib-header] | 12, 40, 52, 56, 64, 108 or 124 bytes | yes | |
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
- [Bitmap File Structure][bmp: digicamsoft.com]
- [An introduction to DIBs (Device Independent Bitmaps)][bmp: herdsoft.com]
- *Dr. Dobb's journal of software tools*: [The BMP File Format, Part 1 By David Charlap][bmp: drdobbs.com]

[bmp: wikipedia.org]: https://en.wikipedia.org/wiki/BMP_file_format
[bmp: digicamsoft.com]: http://www.digicamsoft.com/bmp/bmp.html
[bmp: herdsoft.com]: http://www.herdsoft.com/ti/davincie/imex3j8i.htm
[bmp: drdobbs.com]: http://www.drdobbs.com/architecture-and-design/the-bmp-file-format-part-1/184409517
