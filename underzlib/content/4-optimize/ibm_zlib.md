---
title: "4.2. IBM: fast deflate"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_ibm"
weight: 202
---

Reference: [IBM: A fast implementation of Deflate](http://ieeexplore.ieee.org/document/6824430/)

Optimizations focus on improving the speed of zlib deflate process by using LZ4's repetition elimination process, and improved Huffman coding process.

<bold>Replace LZ77 with LZ4</bold> for faster repetition elimination: Observed speed-up is moderate, didn't achieve LZ4's performance probably due to differences in cache usage. Also observed compression ratio is hardly affected.

<bold>Force the use of static Huffman tree</bold>: Reached fast speed but could have negative effect on compression ratio.

<bold>Semi-static Huffman encoding</bold>: Use static tree to compress the first block of intermediate data (LZ77's output), and collect statistics of this first block to build a Huffman tree for encoding later blocks. The first block's size is configuration, default is 8KB. The sizes of other blocks are also configurable, default is 128KB. An additional step added is evaluating the statistics of the initial block before building the Huffman tree to determine whether it worths to use a dynamic tree. This approach achieves both faster speed and better compression ratio.
