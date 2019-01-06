---
title: "3.5.2. Literal Buffer"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_literal_buffer"
weight: 102
---

The <bold>literal buffer</bold> stores data symbols encoded by LZ77. A symbol is either a single byte, coded as a literal, or a length-distance pair, which codes a copy of up to 258 bytes somewhere in the preceding 32K of uncompressed data. Default literal buffer size is 16K, so it can accumulate from 16K to as much as 4MB of uncompressed data (for highly compressible data). 

Once the <bold>literal buffer is full</bold>, zlib decides what kind of block to construct for Huffman encoding, and then does so, creating the header, which for a dynamic block describes the Huffman codes in the block, and then creates the coded symbols for that block. Or it creates a stored or static block, whatever results in the fewest number of bits. Only then is that compressed data available for output.

Default literal buffer size is configured by marco <code>DEF_MEM_LEVEL</code>. In zlib's code, <code>DEF_MEM_LEVEL = 8</code>, and it's the same for all compression levels. So all compression levels have the same 16K literal buffer size.
