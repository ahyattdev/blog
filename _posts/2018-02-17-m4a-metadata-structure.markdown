---
layout: post
title: The Structure of the M4A format
---
![An M4A file being viewed in HexFiend]({{site.assets}}/m4a-file.png)

*An M4A file being viewed in [Hex Fiend](https://github.com/ridiculousfish/HexFiend)*

Recently, I created a Swift framework called [M4ATools](https://github.com/ahyattdev/M4ATools) that is capable of reading and writing M4A file metadata. M4A files are MP4 files that only contain audio and have the extension M4A. It’s Apple’s format of choice for iTunes music. 

For the most part, M4A is a relatively simple and consistent format. Except for a few instances, a file can be read easily as a series of nested blocks. 

The first four bytes of each block is a 32 bit unsigned big endian integer. The size includes the length of the whole block, including the size itself. Following that is a 4 byte string of Mac Roman encoding that identities that block. After that for a length specified by the block size is the data of the block. This data can either be child blocks or arbitrary data. The size of the data of each block is 8 less than the block size because of the space taken up by the block size and type is 8 bytes. 

It isn’t quite this simple because throughout the development of M4ATools I had to work around some quirks of the format. The first is that the `mdat` block has a size of `0x00000001` and the actual size is stored 12 bytes after the start of the `mdat` block. The other quirk is that the `meta` block has 4 null bytes directly after it’s block type which are also not factored into it’s size. 

These are likely not the only quirks and are just the ones that I have discovered. An M4A file I downloaded from online didn’t have the `mdat` quirk mentioned above, for example. These are likely not true for all cases. 

The actual metadata is stored in `moov → udta → meta → ilst`, where `moov` is the top level bock in that hierarchy. Their keys have a type, where the album name is `©alb` and the sorting album name is `soal`. The string keys have a size limit of 255 characters, except for the lyrics key, which is unlimited. 

The key types are string, uint8, and what I’m calling two int. Two int is for keys that require two integers, such as the track number (track 3 of 9, etc.) and the disk number. These consist of two 16 bit unsigned integers stored in the same key. The full list of keys and their types can be viewed in the [M4ATools documentation](https://ahyattdev.github.io/M4ATools/Classes/M4AFile/Metadata.html). 
