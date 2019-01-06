---
title: "3.1. Compression Levels"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_compression_levels"
weight: 60
---

zlib has 10 compression levels (0-9). Different levels have different compression performance in terms of <bold>compression ratio</bold> and <bold>speed</bold>. Level 0 means no compression, zlib will output the original data. Level 1 is the fastest, while it has low compression ratio. Level 9 gives the highest compression ratio, but the compression speed is slower. The default compression level zlib uses is 6.

Under the hood, compression level changes the deflate strategy and parameters in the deflate process. More details will be discussed in the following sections.
