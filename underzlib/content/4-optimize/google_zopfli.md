---
title: "4.4. Google: Zopfli, Brotli"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_google"
weight: 204
---

Reference: [Data compression using Zopfli](http://fh7922mg.bget.ru/articles/compression/data-compression-using-zopfli.html) (pdf), [Comparison of Brotli, Deflate, Zopfli, LZMA, LZHAM and Bzip2 Compression Algorithms](https://cran.r-project.org/web/packages/brotli/vignettes/brotli-2015-09-22.pdf) (pdf) 

[Zopfli on GitHub](https://github.com/google/zopfli)

[Brotli on GitHub](https://github.com/google/brotli)

In 2013 Google launched <bold>Zopfli</bold>, which is compatible with deflate format. Zopfli gives <bold>smaller compressed data size</bold> than gzip (3.7-8.3% smaller), but it has <bold>slower compression speed</bold> than gzip level 9. Zopfli library can only compress, not decompress.

<bold>Brotli</bold> attempts to implement a <bold>new compression format</bold>, and a more efficient algorithm than deflate. It is similar in speed with deflate but offers more dense compression.

The Brotli compression format is defined in [RFC 7932](https://tools.ietf.org/html/rfc7932). The algorithm uses a combination of a modern variant of the LZ77 algorithm, Huffman coding and 2nd order context modeling. It also uses a static dictionary containing more than 13K words. The static dictionary is helpful for compressing short files. 
