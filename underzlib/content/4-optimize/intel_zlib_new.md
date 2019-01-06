---
title: "4.1. Intel: zlib-new"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_intel"
weight: 201
---

Reference: [Intel: High Performance ZLIB compression on Intel Architecture Processors](https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/zlib-compression-whitepaper-copy.pdf) (pdf)

Optimizations focus on improved hashing, the search for the longest prefix match of substrings in LZ77 process, and the Huffman code flow.

<bold>Improved hashing</bold>: For compression levels 1 through 5, hash elements as quadruplets (match at least 4 bytes). For compression levels 6 to 9, use zlib's original hashing elements as triplets (match at least 3 bytes).

<bold>Add two additional strategies</bold>: DEFLATE_quick for level 1, DEFLATE_medium for level 4 to 6.

* DEFLATE_quick: Limit hash chain search to the first entry.
* DEFLATE_medium: Designed to strike a balance between the compression ratio of zlib's <bold>DEFLATE_slow</bold> strategy, and the performance of zlib's <bold>DEFLATE_fast</bold> strategy. It skips forwarding by the match length after a match is found and supports a variant of lazy match evaluation. When a match is found at position <code>p</code> and of length <code>l</code>, checks for a match at position <code>p + l + 1</code>. If a new match is found, scans backwards from position <code>p + l + 1</code>, to determine whether the second match can be improved.

<bold>Faster hash table shifting</bold>: Leverage SSE (Intel ©) to operate hash shifting on eight entries (16 bytes) at a time.

<bold>Faster CRC calculation</bold>: Leverage PCLMULQDQ (Intel ©) instruction to process 64 bytes of input at a time, with altered algorithm.

<bold>Reduce loop unrolling</bold>: Remove the excessive loop unrolling in Adler32 and CRC32 computations on Modern processors. For Adler32, reduce the unrolling factor from 16 to 8. For CRC32, reduce the unrolling factor from 8 to 4.
