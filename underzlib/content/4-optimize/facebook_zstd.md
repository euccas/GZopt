---
title: "4.3. Facebook: Zstandard"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_facebook"
weight: 203
---

Reference: [Facebook Zstandard (zstd) design introduction](https://code.facebook.com/posts/1658392934479273/smaller-and-faster-data-compression-with-zstandard/)

[Zstandard on GitHub](https://github.com/facebook/zstd)

Zstandard is designed to scale with modern hardware and compress smaller and faster, for general-purpose compression for a variety of data types.

Improve upon zlib by combining several recent innovations and targeting modern hardware.

<bold>Increase window size</bold> to 1MB - 8MB (recommendation).

In compression, use <bold>Finite State Entropy</bold> based on ANS (Asymmetric Numeral System) to improve performance and reduce latency. 

Use <bold>repcode modeling</bold> to efficiently compress structured data

Use a <bold>branchless design style</bold> to reduce the overhead of CPU branch predictor.

In decompression, separate data into multiple parallel streams and uses a new generation Huffman decoder to <bold>decode multiple symbols in parallel</bold> with a single core. This takes advantage of modern CPU's ability to issue several instructions per cycle.
