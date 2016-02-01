# Pixel Formats
The following document contains conversions of a two-part blog post about pixel formats that was published on *[Bill Crow's Digital Imaging & Photography Blog](http://blogs.msdn.com/b/billcrow/)*.

- Part 1: Unsigned integers
- Part 2: Fixed Point and Floating Point


## Part 1: Unsigned integers
> Source: http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx  
> Author: [billcrow](http://blogs.msdn.com/36525/ProfileUrlRedirect.ashx)  
> Published on: 19 Jun 2006 10:38 AM  

> Converted on: 1 Feb 2016  
> Changes:
> - Title
> - Formatting
> - Pixel format table description reformatted to be in a table.

This is the first installment of what I plan to be an ongoing series of personal technical notes about all things related to Windows Media Photo. We’re starting with the very basics – pixel formats.

Windows Media Photo supports far more pixel formats than any other image file format. In fact, several of the supported pixel formats are brand new, being introduced for the first time with Windows Vista (and WIC or .NET Frameworks 3.0 for down-level support.) Let’s take a closer look at pixel formats and the new capabilities supported by Windows Media Photo.


### A Little Background
Historically, color images have been encoded using three unsigned integer values for red, green and blue. Monochrome (or gray scale) images use a single unsigned integer per pixel. Virtually all consumer photography uses 8-bit unsigned integer values, providing 256 unique values for each of the three channels. For more demanding requirements, many applications also support 16-bit unsigned integers, offering 65536 unique values per channel.

256 steps from the darkest value to the lightest value present some significant limitations. In actuality, 256 steps per channel are all that are required to display an image on a monitor. But that assumes that the values correspond to the monitor’s interpretation of color. Since that is rarely the case, transformations between different color spaces are required, losing a certain amount of the already limited precision. The artifacts that come from this loss of precision often shows up as visible bands in smooth, continuous color areas, where there are no longer enough unique values to represent the color range without seeing visible steps between adjacent values. Using 16 bits per channel provides more than sufficient resolution to insure more than 8 bits per channel are always retained through any color space conversion. Of course, twice as much data is required to guarantee this quality.

Using unsigned integers is currently the most common way to encode color information, and Windows Media Photo has rich support for unsigned integer pixel formats in multiple color formats and bit depths.


### The Colorless World of Gray Scale
Let’s start with the Gray unsigned integer pixel formats:

| PixelFormat Name             | GUID                                  | Ch | BPC | BPP | Num    | Color | A | B |
|------------------------------|---------------------------------------|---:|----:|----:|--------|-------|---|---|
| **WICPixelFormat8bppGray**   | `6fddc324-4e03-4bfe-b1853d77768dc908` |  1 |   8 |   8 | `UINT` | Gray  |   | ✓ |
| **WICPixelFormat16bppGray**  | `6fddc324-4e03-4bfe-b1853d77768dc90b` |  1 |  16 |  16 | `UINT` | Gray  |   | ✓ |
| **WICPixelFormatBlackWhite** | `6fddc324-4e03-4bfe-b1853d77768dc905` |  1 |   1 |   1 | `UINT` | Gray  |   |   |

If you’ve already taken a look at the Windows Media Photo Feature Specification, then you’re familiar with these pixel format tables. But, let’s recap the information summarized in the table.

| Field     | Description
|-----------|------------------------------------------------------------------
| **Name**  | This is the descriptive name that we use to refer to the pixel format. This is frequently abbreviated by dropping the WICPixelFormat prefix.
| **GUID**  |  The 128-bit Globally Unique Identifier for the pixel format.
| **Ch**    |  The number of channels.
| **BPC**   |  Bits per channel.
| **BPP**   |  Bits per pixel. This is typically the number of channels multiplied by the number of bits per channel. However, some pixel formats contain unused information in each pixel value to align pixel values to a specific boundary.
| **Num**   |   The numerical format.
| **Color** | The color format.
| **Alpha** |    Indicates that the pixel format contains an alpha channel. This is included in the channel count.
| **BASIC** |    Indicates that this pixel format is one of the BASIC pixel formats that is required to be supported by all Windows Media Photo decoders.

The unsigned integer Gray pixel formats are pretty straightforward. The two Basic formats are either 8bpc or 16bpc. These correspond to the most commonly used monochrome pixel formats in use today. In addition, the third pixel format uses a single bit per pixel for black/white images.

### The Most Common Color Format - RGB

Windows Media Photo supports an extensive set of unsigned integer RGB pixel formats:

| PixelFormat Name                 | GUID                                  | Ch | BPC   | BPP | Num    | Color | A | B |
|----------------------------------|---------------------------------------|---:|------:|----:|--------|-------|---|---|
| **WICPixelFormat24bppRGB**       | `6fddc324-4e03-4bfe-b1853d77768dc90d` |  3 |     8 |  24 | `UINT` | RGB   |   | ✓ |
| **WICPixelFormat24bppBGR**       | `6fddc324-4e03-4bfe-b1853d77768dc90c` |  3 |     8 |  24 | `UINT` | RGB   |   | ✓ |
| **WICPixelFormat32bppBGR**       | `6fddc324-4e03-4bfe-b1853d77768dc90e` |  3 |     8 |  24 | `UINT` | RGB   |   |   |
| **WICPixelFormat48bppRGB**       | `6fddc324-4e03-4bfe-b1853d77768dc915` |  3 |    16 |  48 | `UINT` | RGB   |   | ✓ |
| **WICPixelFormat32bppBGRA**      | `6fddc324-4e03-4bfe-b1853d77768dc90f` |  4 |     8 |  32 | `UINT` | RGB   | ✓ |   |
| **WICPixelFormat64bppRGBA**      | `6fddc324-4e03-4bfe-b1853d77768dc916` |  4 |    16 |  64 | `UINT` | RGB   | ✓ |   |
| **WICPixelFormat32bppPBGRA**     | `6fddc324-4e03-4bfe-b1853d77768dc910` |  4 |     8 |  32 | `UINT` | RGB   | ✓ |   |
| **WICPixelFormat64bppPRGBA**     | `6fddc324-4e03-4bfe-b1853d77768dc917` |  4 |    16 |  64 | `UINT` | RGB   | ✓ |   |
| **WICPixelFormat16bppBGR555**    | `6fddc324-4e03-4bfe-b1853d77768dc909` |  3 |     5 |  16 | `UINT` | RGB   |   |   |
| **WICPixelFormat16bppBGR565**    | `6fddc324-4e03-4bfe-b1853d77768dc90a` |  3 | 5,6,5 |  16 | `UINT` | RGB   |   |   |
| **WICPixelFormat32bppBGR101010** | `6fddc324-4e03-4bfe-b1853d77768dc913` |  3 |    10 |  32 | `UINT` | RGB   |   |   |

The Basic formats include RGB in both 8bpc and 16bpc, plus 8bpc in BGR channel order.


### RGB Channel Ordering

Let’s take a little detour to discuss channel ordering. The RGB color format is the only one where we have to deal with different channel ordering. Windows Media Photo’s support for different channel orders is largely for legacy reasons, providing support for the most commonly used ways of representing color. Ideally, channels would always be organized in the same order, simplifying the pixel format options. However, the existence of big-endian and little-endian processor architectures has led to different approaches for channel order of RGB data, requiring ongoing support for backward compatibility.

Historically, the industry has been inconsistent in the names for pixel formats compared to the specific ordering of channel values in an uncompressed image bit stream. We’ve made every effort to be consistent with Windows Media Photo. The pixel format name specifies the channel ordering as they appear in the sequential stream of uncompressed image data. Because of differences with big endian vs. little endian processor architectures, this becomes a little more confusing with channel values represented by 8bpc or less.

For a bitmap in 8bpc RGB pixel format (WICPixelFormat24bppRGB), the first byte in the uncompressed data stream is the red channel for the first pixel, followed by the green channel and then the blue channel. This is the typical way that 8bpc RGB data is stored in an uncompressed TIFF file. WICPixelFormat24bppBGR stores the channels in the reverse order, starting with the blue channel. This is the channel order used  in 8bpc BMP files.

When a fourth channel is added to 8bpc pixel formats (either an alpha channel or an unused padding byte to align pixels on 32-bit word boundaries), the channel order of the bytes within a 32-bit word on a little-endian system are typically interpreted (and named) in the opposite order as they appear in the uncompressed data stream. However, with WIC pixel formats, the naming always references the channel order in the data stream, not how they might be reorganized within a larger pixel word on a little-endian system.

In addition to the Basic pixel formats, the set of unsigned integer RGB pixel formats include versions with normal and pre-multiplied alpha channels, an 8bpc version with an unused padding byte, and three different packed bit formats. We’ll save the discussion of alpha channels for another day.

WICPixelFormat32bppBGR is very similar to WICPixelFormat32bppBGRA; the only difference is that the latter uses the value in the fourth byte as an alpha channel while the former ignores it. These two pixel formats are very useful for storing an uncompressed pixel in a 32-bit word. The low order byte of the word is the blue channel, the next higher byte is green, then red, and the high order byte is either the alpha channel or unused, depending on the pixel format.


### Packed Bit RGB Pixel Formats

Windows Media Photo supports three unsigned integer RGB packed-bit formats. These are formats where the bits per channel are not a multiple of 8-bit bytes. Because the channel values aren’t byte-aligned, the uncompressed data stream must be viewed as a sequence of pixel values rather than a sequence of channel values. The order of the channels within a pixel are defined within a word, and therefore, are dependent on whether the word is based on a big endian or little endian architecture.

Windows Media Photo always assumes a little endian (Intel/AMD) architecture, and the packed bit channel values are always organized accordingly. Therefore, a big-endian system must reorder the bytes within a word before interpreting the channel values.

WICPixelFormatBGR555 stores three 5-bit channel values in a single 16-bit word, with an unused bit. The least significant 5 bits are the blue value; the next 5 bits are the green value, followed by the red value. The most significant bit is unused. WICPixelFormatBGR565 increases the green channel to six bits, so all bits in a 16-bit word are used. These pixel formats are commonly used in hardware implementations, including displays in mobile devices. Windows Media Photo allows direct encoding in the device’s native pixel format.

WICPixelFormatBGR101010 stores three 10-bit channel values in a 32-bit word, with two unused bits. The least significant 10 bits are the blue value; the next 10 bits are the green value, followed by the red value. The most significant two bits are unused. This is a very useful format for increasing the precision of unsigned integer image data without a significant increase in uncompressed bitmap size. However, it can often be cumbersome to deal with 10-bit values, and the additional processing to extract the values outweighs advantages of saving storage space.


### Support for Photo Printing

Windows Media Photo supports multiple pixel formats specifically designed for the needs of image printing. This includes numerous pixel formats in CMYK and n-Channel color formats.

Here are the CMYK pixel formats supported by Windows Media Photo:

| PixelFormat Name                 | GUID                                  | Ch | BPC   | BPP | Num    | Color | A | B |
|----------------------------------|---------------------------------------|---:|------:|----:|--------|-------|---|---|
| **WICPixelFormat32bppCMYK**      | `6fddc324-4e03-4bfe-b1853d77768dc91c` |  4 |     8 |  32 | `UINT` | CMYK  |   |   |
| **WICPixelFormat40bppCMYKAlpha** | `6fddc324-4e03-4bfe-b1853d77768dc92c` |  5 |     8 |  40 | `UINT` | CMYK  | ✓ |   |
| **WICPixelFormat64bppCMYK**      | `6fddc324-4e03-4bfe-b1853d77768dc91f` |  4 |    16 |  64 | `UINT` | CMYK  |   |   |
| **WICPixelFormat80bppCMYKAlpha** | `6fddc324-4e03-4bfe-b1853d77768dc92d` |  5 |    16 |  80 | `UINT` | CMYK  | ✓ |   |

CMYK has historically been used for encoding information for printing rather than display on a monitor. However, virtually all PC photo printers are actually RGB, not CMYK devices. These printers use multiple inks that don’t directly map to CMYK channels. A printer expects to receive image content in RGB color format, and translates directly to the color space defined by the printer’s specific ink configuration. Only conventional offset printing uses CMYK channels, and the CMYK color space is supported for these printing scenarios. Windows Media Photo supports CMYK image data in 8bpc and 16bpc bit depths, with and without an alpha channel. I’ll save a more detailed look at the use of CMYK pixel formats for another time.

Windows Media Photo has been designed to support a number of printing scenarios, including native support for printer color spaces. Support is provided for up to eight channels of arbitrary image data, making it possible to encode images in the color space defined by the printer’s ink configuration. These n-channel formats (listed below) are provided in either 8bpc or 16bpc bit depths, either with or without an alpha channel. We’ll discuss n-channel pixel formats in much more detail in a future installment.

| PixelFormat Name                       | GUID                                  | Ch | BPC   | BPP | Num    | Color | A | B |
|----------------------------------------|---------------------------------------|---:|------:|----:|--------|-------|---|---|
| **WICPixelFormat24bpp3Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc920` |  3 |     8 |  24 | `UINT` | N-Chn |   |   |
| **WICPixelFormat32bpp4Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc921` |  4 |     8 |  32 | `UINT` | N-Chn |   |   |
| **WICPixelFormat40bpp5Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc922` |  5 |     8 |  40 | `UINT` | N-Chn |   |   |
| **WICPixelFormat48bpp6Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc923` |  6 |     8 |  48 | `UINT` | N-Chn |   |   |
| **WICPixelFormat56bpp7Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc924` |  7 |     8 |  56 | `UINT` | N-Chn |   |   |
| **WICPixelFormat64bpp8Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc925` |  8 |     8 |  64 | `UINT` | N-Chn |   |   |
| **WICPixelFormat32bpp3ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc92e` |  4 |     8 |  32 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat40bpp4ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc92f` |  5 |     8 |  40 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat48bpp5ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc930` |  6 |     8 |  48 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat56bpp6ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc931` |  7 |     8 |  56 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat64bpp7ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc932` |  8 |     8 |  64 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat72bpp8ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc933` |  9 |     8 |  72 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat48bpp3Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc926` |  3 |    16 |  48 | `UINT` | N-Chn |   |   |
| **WICPixelFormat64bpp4Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc927` |  4 |    16 |  64 | `UINT` | N-Chn |   |   |
| **WICPixelFormat80bpp5Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc928` |  5 |    16 |  80 | `UINT` | N-Chn |   |   |
| **WICPixelFormat96bpp6Channels**       | `6fddc324-4e03-4bfe-b1853d77768dc929` |  6 |    16 |  96 | `UINT` | N-Chn |   |   |
| **WICPixelFormat112bpp7Channels**      | `6fddc324-4e03-4bfe-b1853d77768dc92a` |  7 |    16 | 112 | `UINT` | N-Chn |   |   |
| **WICPixelFormat128bpp8Channels**      | `6fddc324-4e03-4bfe-b1853d77768dc92b` |  8 |    16 | 128 | `UINT` | N-Chn |   |   |
| **WICPixelFormat64bpp3ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc934` |  4 |    16 |  64 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat80bpp4ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc935` |  5 |    16 |  80 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat96bpp5ChannelsAlpha**  | `6fddc324-4e03-4bfe-b1853d77768dc936` |  6 |    16 |  96 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat112bpp6ChannelsAlpha** | `6fddc324-4e03-4bfe-b1853d77768dc937` |  7 |    16 | 112 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat128bpp7ChannelsAlpha** | `6fddc324-4e03-4bfe-b1853d77768dc938` |  8 |    16 | 128 | `UINT` | N-Chn | ✓ |   |
| **WICPixelFormat144bpp8ChannelsAlpha** | `6fddc324-4e03-4bfe-b1853d77768dc939` |  9 |    16 | 144 | `UINT` | N-Chn | ✓ |   |


That’s a summary of the unsigned integer pixel formats. Along the way we had a chance to talk about bit depth and channel ordering. We skipped over alpha channels (and pre-multiplied alpha channels) and we’ve only scratched the surface on CMYK and n-channel pixel formats. We also haven’t talked at all about color space and color profiles, which are very important for unsigned integer pixel formats. We’ll get to all these topics in much more detail in future installments.

### Coming Up Next

While unsigned integer with RGB color formats is the legacy encoding for images, it has numerous shortcomings. When encoding an image using unsigned integers, the smallest value (0) represents black, and the largest value represents maximum saturation for that channel. When all three channels are set to the maximum value, the resulting color is white.

However, these minimum or maximum values are based on the specific color context being used. When converting between color spaces, any color values that exceed the limits of either color space are lost because we can only encode values that reside inside the representative bounds of each color space. The fact that we must always clamp data to fit within the current color space is one of the principal ways that useful image content is destroyed during image processing workflows. This has led to complicated (and usually proprietary) workflows to edit in source color spaces to minimize this data loss.

In our next installment we’ll investigate how we can use fixed point or floating point numerical encoding to retain information that would otherwise be destroyed by clipping to the current color space. This provides a much more practical way to preserve all the image information with much less complex workflows.

### Send your Feedback

This is the first of what I plan to be an ongoing series of technical notes on all aspects of Windows Media Photo and related topics on image processing and workflows. I’d really appreciate your feedback. I’m using my personal blog to share this information as directly and timely as possible. Eventually, we’ll organize all this information into a comprehensive technical document. In the mean time, this blog allows me to share it now, but it also means that it hasn’t gone through the same level of editing and review that we use for our more official publications. My blog writing style will be a little more freeform, and I’m sure the minimal proofreading and reviews will allow a number of errors and typos to sneak through.

So send me your feedback to help me make this blog as helpful as possible. Are these technical notes useful?  Is this level of presentation too simplistic or does it include too much technical details that aren’t adequately explained?  What topics are you most interested in?  What bugs and errors do you see?  You can reply using the comments, below, or send me email with the link on the left.

I look forward to hearing your feedback!


### Comments

[**briancartier**](http://blogs.msdn.com/39998/ProfileUrlRedirect.ashx) *6 Jul 2006 11:32 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#657944)
> I think the following should read big-endian instead:  
"Therefore, a little-endian system must reorder the bytes within a word before interpreting the channel values."

[**briancartier**](http://blogs.msdn.com/39998/ProfileUrlRedirect.ashx) *6 Jul 2006 11:34 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#657950)
> This is an excellent supplement to the spec. The detail level is perfect.
Thanks!

[**billcrow**](http://blogs.msdn.com/36525/ProfileUrlRedirect.ashx) *13 Jul 2006 8:36 PM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#665109)
> Thanks for the feedback, Brian. You're correct about the endian bug. I'll go fix that now.

**Dan's Archive** *17 Aug 2006 10:59 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#704311)
>  

**Garry Trinder** *11 Mar 2007 4:20 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#1857524)
> Didn't we already do that? Regular readers of my blog (which is a tad oxymoronic, since it appears I

**nwebsolution** *10 Dec 2010 7:01 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/19/636858.aspx#10103222)
> i like the comment very much it  is so helpful to deal with ,thanks.


---


## Part 2: Fixed Point and Floating Point
> Source: http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx  
> Author: [billcrow](http://blogs.msdn.com/36525/ProfileUrlRedirect.ashx)  
> Published on: 21 Jun 2006 8:28 PM  

> Converted on: 1 Feb 2016  
> Changes:
> - Title
> - Formatting

This is the second part of a discussion of the pixel formats supported by Windows Media Photo. I definitely recommend you read Part 1 ([below](#part-1-unsigned-integers)) first. It will provide some important background information that will help with the understanding of Part 2.


### The Mess We’re in Today
In our last installment, we discussed Windows Media Photo’s support for unsigned integer pixel formats. While a wide range of unsigned integer pixel formats are supported, they all share the same limitation of not allowing any data outside the visible range defined by the gamut of the particular color space. The range of numerical values, regardless of the bit depth , are used to represent pixel values from the darkest visible color (black), to the brightest or most saturated visible color. Any value that exceeds this visible range as a result of editing or image processing is simply discarded, and can never be recovered.

This limitation has led to the widespread adoption of some fairly convoluted workflows to always retain the highest quality images. The conventional approach is to carefully convert from RAW to retain the maximum dynamic range and widest gamut, not necessarily the best image appearance. Then, this “low contrast, low saturation” master image can be loaded in Photoshop and adjusted in different ways, depending on whether the final destination is print or monitor display. We’ve also been taught to choose different working color spaces, again based on the intended use of the image.

Of course, if we want to do any image editing (and don’t we always), ideally we need to complete all the image editing steps and produce a new low contrast/saturation master, before we begin the series of steps that will optimize the photo for the particular output requirements. And if farther down the workflow path we discover the need for an additional edit or tweak, we invariably have to back up in the workflow to the appropriate point, make the change, and then re-do all the rest of the steps to get back to where we were.

To help with this convoluted process, our tools have become much more sophisticated (and complex!)  Any seasoned Photoshop user has learned to make heavy use of adjustment layers. This allows us to define and view all the changes we want to make, but we don’t actually commit those changes until the image is flattened for distribution, printing, or display. That makes it easier to back up in the workflow and make a change, without the need to manually redo all the subsequent steps. However, adjustment layers can often be confusing and difficult; they work for some scenarios, but not others. Additionally, the use of adjustment layers invariably locks us in a single application. It’s rarely possible to move an image with all its adjustment layers between different tools; we have to flatten an image (and permanently commit to the changes) before moving an image from one tool to the next.

Even with Photoshop’s adjustment layers, it’s still common to find that the appearance we want can’t be achieved with the version of the image we started with. Changing the white balance or recovering a lost highlight often requires going all the way back to the RAW conversion and making an adjustment to produce a different version of our low contrast/saturation master image. At that point, many of the adjustments made in Photoshop will likely have to be tweaked accordingly, or redone from scratch.

To address this problem, some of the newest tools provide “adjustment layer” style editing directly from the unprocessed RAW image. Apple Aperture, Adobe LightRoom as well as other popular RAW conversion applications always start from the RAW image data, first demosaicing it to an RGB image, and then applying the requested exposure, color and other adjustments as editable layers. At some point, a flattened image needs to be rendered for distribution, printing or display, or just to export it to a different program. But up until that point, most adjustments can be changed or removed without the need to manually reproduce the subsequent steps in the image processing workflow.

The problem with all these “adjustment layer” style image processing applications is the proprietary nature of the software. It’s not like the software developers have much of a choice – the adjustment information they are creating only has meaning to their application; it can’t be understood or processed by another application. While it might be possible to define a common language for these adjustments, we would be reducing all applications to some “least common denominator” subset of adjustment operations, robbing application developers of the ability to develop and deliver new, innovative image processing operations.

So, the working edit copy of your photo is locked up inside a particular proprietary software package. You can always export a flattened output image, but because we typically use unsigned integer pixel formats (you did remember that this started as a discussion of pixel formats, right?), the pixel data is cropped to the visible limits of the chosen color space. We’re forced to choose our color space carefully, based on the intended use of the image, and once we commit to flatten the image to unsigned integer values in that color space, we’ve effectively locked the appearance. Any further edits or adjustments we make continue to reduce the overall gamut and dynamic range of the image because we’re constrained by the limits of the color space. If we do want to make changes that preserve the full fidelity of the image, we have no choice but to go back to the proprietary tool we first used, or else start all over from scratch.

Along the way, we wind up saving multiple versions of each photo:  The original RAW image, the “adjustment layer” file used by our editing tool of choice, and multiple flattened images for each different use or destination for the photo. Half the job is just keeping track of all those files!  And we won’t even get into the long term archivability of device-specific RAW files or application-specific editing files.

In reality, the complexity of the workflow required to fully preserve the full tonal range of digital photos limits this process to only a subset of digital photographers. Most photographers, even those who regularly shoot in RAW, convert the RAW file to an sRGB unsigned integer format and complete the remainder of the workflow process completely in sRGB. This significantly limits the tonal range that can be delivered in a final print.


### What’s All This Have to Do with Pixel Formats?
In case you forgot, this began as a discussion of pixel formats. We took a pretty long detour lamenting the challenges of today’s high quality photo workflow. In fact, our current dependence on unsigned integer pixel formats is a big contributor to the problems that demand the cumbersome workflows described above.
Windows Vista (and .NET Frameworks 3.0 for down-level support) introduces a new graphics architecture with comprehensive support for high dynamic range, wide gamut pixel formats, using fixed point or floating point numerical representations, rather than unsigned integers. Windows Media Photo is currently the only file format for Windows (and beyond) that supports these new pixel formats.

*The fundamental goal with a high dynamic range, wide gamut pixel format is to never discard image information that falls outside the visible range.* The entire tonal spectrum is always retained, regardless of the current exposure or color adjustments.

Using fixed point or floating point values, pixel information is encoded using an extended numerical range. The visible portion of the numerical range is a subset of the total numerical range that can be encoded with fixed point or floating point values.

Using this approach, if color or exposure adjustment pushes a pixel value outside the visible range, rather than losing this value (as is the case with unsigned integer representations), the numerical value is still retained. If a subsequent adjustment brings that pixel value back into the visible range, the correct numerical value is fully recovered.

This dramatically eliminates the issues and concerns with “flattening” a file. Most color or exposure adjustments are completely reversible, eliminating the need to restart with the original RAW file or an intermediate layered editing file. A single file can often be used for printing, display, archiving, and even additional editing. Regardless of the choices made for the particular “look” of the photo, the full dynamic range and gamut of the original data is always retained, insuring that the full total value of the photo is available for printing, display or further exposure and color adjustments.

While this doesn’t completely replace the need for adjustment layer editing or multiple version file management, in many cases a high dynamic range, wide gamut file format enables the highest possible quality workflow without the need for cumbersome and confusing multi-stage workflows. And a high dynamic range, wide gamut image file is ideal for long term archiving as well.

Of course, I’d be remiss not to point out that this is still largely potential, not reality. Until we have a greater range of choice for image processing applications with robust high dynamic range, wide gamut editing features, today’s popular tools still largely restrict us to unsigned integers. However, there are still many scenarios enabled with Windows Vista that can take full advantage of the benefits provided by Windows Media Photo and high dynamic range, wide gamut pixel formats.
Windows Media Photo supports high dynamic range, wide gamut photo encoding using either fixed point or floating point numerical representations in 16 bits per channel (bpc) or 32bpc bit depths. There are advantages with each format option and supporting multiple pixel formats offers the greatest possible choice and flexibility.


### Fixed Point Pixel Formats
Windows Media Photo supports the following fixed point pixel formats:

| PixelFormat              | Ch | BPC | BPP | Num    |
|--------------------------|---:|----:|----:|-------:|
| **48bppRGBFixedPoint**   |  3 |  16 |  48 | `SINT` |
| **96bppRGBFixedPoint**   |  3 |  32 |  96 | `SINT` |
| **64bppRGBAFixedPoint**  |  4 |  16 |  64 | `SINT` |
| **128bppRGBAFixedPoint** |  4 |  32 | 128 | `SINT` |
| **16bppGrayFixedPoint**  |  1 |  16 |  16 | `SINT` |
| **32bppGrayFixedPoint**  |  1 |  32 |  32 | `SINT` |

This list of six different includes RGB, RGB plus Alpha, and Gray scale, in both 16bpc and 32bpc bit depths.

A fixed point numerical representation is not commonly used in current image processing applications or image file formats. It is being introduced in Windows Media Photo as an optimal format to encode greater dynamic ranges while still retaining all the performance advantages of integer processing.

Fixed point values are essentially signed, scaled integer values. By applying an appropriate scaling factor, the signed integer range can represent an arbitrary numeric range. This enables the encoding of color information that goes beyond the traditional range limits of “black” and “white” or the gamut of any particular device or rendering target.

Rather than interpreting the number as range of integer steps from black to maximum saturation for a particular color profile, this fixed point data is scaled to represent a larger floating point range in a linear color space. With this linear encoding, zero still represents the minimum visible value, or black. A value of 1.0 represents the maximum visible value, or when applied to all channels that make up a pixel, white. The specific scaling for each bit depth specifies exactly what point in the entire signed integer range is interpreted as a value of 1.0.

For 16bpc fixed point pixel formats, there are 65536 unique values. When interpreted as a signed integer, these values range from -32768 to +32767. Windows Media Photo interprets this fixed point range as representing a linear floating point color value numeric range from -4.0 to +3.999+. 0 still represents black, and the 1.0 value for white (or maximum color saturation for a single channel) is represented by the signed integer value 8,192 (0x2000h). In effect, we are re-scaling the signed integer range (from -32767 to +32768) by dividing the values by 8192. Rather than only representing the visible color value range (from 0.0 to 1.0), this scaling allows us to represent an exposure range eight times as large. Most typical photo color or exposure adjustments will still retain the entire original sensor data within this expanded range. At the same time, 13 bits are always available to represent the current visible range; because this is treated as linear data, the original sensor data efficiently maps to this high dynamic range, wide gamut color space.

If this still doesn’t provide sufficient range or precision, Windows Media Photo also supports 32bpc fixed point encoding. The process is the same, but the signed integer values are interpreted to represent a scaled floating point range from -128 to 127.999+, with 24 bits of linear precision always available for the visible range. 0 is still used to represent black, and the white (or maximum color saturation) value of 1.0 is represented by the value 16,777,216 (0x01000000h).


### Floating Point Pixel Formats
In addition to the fixed point pixel formats above, Windows Media Photo can also encode high dynamic range, wide gamut image data using the following floating point pixel formats:

| PixelFormat          | Ch | BPC | BPP | Num    |
|----------------------|---:|----:|----:|-------:|
| **48bppRGBHalf**     |  3 |  16 |  48 | `Float` |
| **128bppRGBFloat**   |  3 |  32 |  128 | `Float` |
| **64bppRGBAHalf**    |  4 |  16 |  64 | `Float` |
| **128bppRGBAFloat**  |  4 |  32 |  128 | `Float` |
| **128bppPRGBAFloat** |  4 |  32 |  128 | `Float` |
| **16bppGrayHalf**    |  1 |  16 |  16 | `Float` |
| **32bppGrayFloat**   |  1 |  32 |  32 | `Float` |
| **32bppRGBE**        |  3 |  16 |  32 | `Float` |

Like the fixed point formats, this list includes RGB, RGB plus Alpha and Gray scale in 16bpc and 32bpc bit depths. In addition, it includes a pre-multiplied alpha channel version at 32bpc. Finally, there’s one special case floating point representation that we’ll also cover a little later.

Windows Media Photo uses floating point values to encode a range of values beyond just the visible range. With both bit depths, a floating point value of 0.0 represents black and a floating point value of 1.0 represents white or maximum saturation per channel. 32bpc provides a dramatically larger range and more precision than 16bpc.

16bpc floating point encoding is commonly referred to as the HALF floating point format. This encoding is not natively supported by most general purpose CPU’s, but many graphics cards natively support the HALF format on the GPU. The 16 bits are organized as a sign bit, 5 exponent bits and 10 normalized mantissa bits, and are otherwise interpreted using the same rules as 32bpc floating point values. This provides an efficient method to encode values with a very wide dynamic range.

32bpc floating point values are encoded in accordance with the 32-bit implementation of the ANSI/IEEE Standard 754-1985 *Standard for Binary Floating Point Arithmetic*, widely used on most computing platforms. The format uses one sign bit, 8 exponent bits and 23 normalized mantissa bits. While this is one of the least efficient means to encode values for compression purposes, it offers the greatest precision and dynamic range.  Most image editing applications use 32bpc floating point representation internally for the highest quality image processing.

The final floating point pixel format supported by Windows Media Photo is 32bppRGBE.  An entire RGB pixel is encoded as three 16-bit floating point values using only four bytes. The bytes include three unnormalized, unsigned 8-bit mantissas for the red, green and blue channels, plus a shared 8-bit exponent. While this offers no increase in gamut, it is a more compact uncompressed method to encode image content with a very wide exposure range.


### High, Wide and Deep
So, no we’ve covered the wide range of pixel formats supported by Windows Media Photo. This new file format offers dramatically more flexibility than any previous photo file format, allowing the choice of the appropriate pixel format depending on the data source, application and usage scenario.

Unsigned integer pixel formats provided the greatest compatibility with legacy files and applications. As such, they are bound by all the same limitations imposed by this method of color representation. However, unsigned integers still provide the best compression efficiency, and are perfectly suited for many applications.
By supporting fixed point and floating point high dynamic range, wide gamut pixel formats, Windows Media Photo helps enable an entirely new approach to high quality photo workflows. These high, wide and deep pixel formats make it possible to preserve the entire dynamic range and gamut originally captured by the source device, and preserves the range throughout the entire image processing workflow.  This can be accomplished without concerns about color profiles and working color spaces, and can significantly simplify the process of high fidelity photo printing. An advanced capability that has previously only been available to those professionals willing to invest in complex tools and cumbersome workflows can now be available to everyone. Any easy-to-use and easy-to-share file format can be the same format used to capture original images, edit, archive and print, all with the maximum fidelity possible.


### Coming Up …
For the next installment, we’ll detour from this review of technical details and conceptual discussion and dive into some practical tools and techniques for developers and enthusiasts to get your hands dirty and actually start encoding and viewing Windows Media Photo files in these various pixel formats. This is all possible today using Windows Vista or .NET Frameworks 3.0, Photoshop, and some straightforward software development. But we’ll focus on some (largely unsupported) tools and utilities that can be used right now, instead of writing your own code or waiting for the release of updated applications that support Windows Media Photo. We’ll talk about some of the current pitfalls and limitations with Windows Vista Beta 2, so you know what to expect and what to avoid (for now.)

Looking farther down my blogging to-do list, we’ll dive a little deeper into the use of high dynamic range, wide gamut pixel formats and talk in detail about color spaces and the use of color profiles. This will include a discussion of scRGB, the native color space we use for fixed point and floating point pixel formats.
As always, send me your comments, criticisms, corrections and topic requests, either via the comments section below or the email link on the left.


### Comments

**Garry Trinder** *23 Mar 2007 4:45 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#1936060)
> A Mode by Any other Name So, as reported previously, we now have released a beta of the Windows HD Photo

**Garry Trinder** *9 Apr 2007 2:21 PM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#2062917)
> Didn't we already do that? Regular readers of my blog (which is a tad oxymoronic, since it appears I

**Garry Trinder** *13 Jul 2007 12:03 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#3840924)
> HD Photo supports a new paradigm for image editing. , Higher fidelity images can be stored in a high

**Garry Trinder** *13 Jul 2007 12:26 AM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#3841096)
> HD Photo supports a new paradigm for image editing. , Higher fidelity images can be stored in a high

> **[bjohns](http://blogs.msdn.com/107479/ProfileUrlRedirect.ashx)** *2 Nov 2007 10:53 PM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#5849893)  
> > Bill,
> >
> > Read your description and want it, the HD scRGB downloads. But I use Corel PaintsShop Pro XI, with no adobe at all.
> >
> > Is there, will there be the same available for my Corel XI?
> >
> > (which I think is superior to adobe p-shop5, but lacks all adobes available plug-ins and multiple cousins-> reads like an inbred program)
> >
> > bjohns

**Garry Trinder** *20 Feb 2008 4:35 PM* [#](http://blogs.msdn.com/b/billcrow/archive/2006/06/22/642213.aspx#7824000)
> PingBack from http://expertvoices.nsdl.org/cornell-cs322/2008/02/20/floating-point-numbers-in-images/
