---
title: "4.6. CloudFlare: zlib"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_cloudflare"
weight: 206
---

Reference: [CloudFlare fights cancer: The Unexpected Benefit Of Open Sourcing Our Code](https://blog.cloudflare.com/cloudflare-fights-cancer/)

[CloudFlare zlib fork on GitHub](https://github.com/cloudflare/zlib)

CloudFlare's improvements on zlib include:

* Use <bold>uint64_t</bold> to replace the 16-bit types.
* Use an <bold>improved hash function</bold> iSCSI CRC32. This function is implemented as a hardware instruction on Intel processors. It has very fast performance and better collision properties.
* Search for matches of at least <bold>4 bytes</bold>.
* Use SIMD instructions for <bold>window rolling</bold>.
* Use Intel's hardware carry-less multiplication instruction PCLMULQDQ for the <bold>CRC32 checksum</bold>.
* <bold>Optimized longest-match function</bold>. This is the most performance demanding function in the library.


Other experiments, not yet included in the released zlib fork:

* Use an improved version of the linked list used in zlib (hash chain)

Benchmarking results

* Testing datasets are four standard corpus data consists of ASCII text, bitmap images, numbers, and source code files.
* Speed: In general, CloudFlare's zlib is faster than zlib and Intel's zlib on levels 2 to 9, especially 6 to 9 (2x - 7.5x).
* Compression ratio: Very similar to zlib on all levels, and better than Intel's zlib on level 1.
