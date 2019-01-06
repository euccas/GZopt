---
title: "4.7. CloudFlare: preset dictionary"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_optimize_cloudflare_dict"
weight: 207
---

Reference: [CloudFlare: improve compression with preset deflate dictionary](https://blog.cloudflare.com/improving-compression-with-preset-deflate-dictionary/)

Optimizations aim to improve compression performance (~25% down) for HTML files (mostly <bold>short texts</bold>).

Change minimal match length to <bold>4 bytes</bold>.

Use a <bold>preset dictionary</bold> so at the beginning of the input has back reference for searching matches.

* Create the preset dictionary by performing pseudo LZ77 over a set of files to be compressed, and find strings that DEFLATE would not compress in the first 16Kb of each input file. Then performs a frequency count of the individual strings, and scores them according to their length and frequency. The highest scoring strings are saved into the dictionary file.
* Use a Go program to make such deflate dictionary: [dictator on GitHub](https://github.com/vkrasnov/dictator)
