---
title: "3.4. Huffman Encoding"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_huffman_encoding"
weight: 90
---

zib implements both <bold>static (fixed) Huffman encoding</bold> and <bold>dynamic Huffman encoding</bold>. For each block of LZ77 encoded data, zlib computes the number of bits in the block using both static Huffman encoding and dynamic Huffman encoding, then <bold>choose the method</bold> which produces <bold>smaller amount</bold> of data. If the number of bits are equal using two methods, zlib chooses static Huffman encoding as the decoding process is faster. 

The whole data stream can contain a mix of static and dynamic Huffman encoded data. The Huffman codes are transmitted in the deflate stream header for each block.

In summary, the Huffman encoding process in zlib consists of the following steps:

1. During LZ77 encoding process, collect <bold>statistics of data bytes</bold> and generate a histogram.
2. For each data block, build a <bold>dynamic Huffman tree</bold> using the collected statistics.
3. Compute and compare the encoded block lengths using a dynamic Huffman tree and a static Huffman tree, and decide whether it is worthwhile to use <bold>a dynamic or a static tree</bold> for the encoding phase.
4. Perform dynamic or static Huffman encoding on the block of data.
