---
title: "2. Compression Algorithm"
date: 2019-01-04T20:52:57+07:00
anchor: "compression_algorithm"
weight: 15
---

The <bold>compression</bold> algorithm used in zlib is the <bold>deflate</bold> method. The deflate method encodes the input data into compressed data. The <bold>decompression</bold> algorithm used in zlib is the <bold>inflate</bold> method, which is the decoding process that takes a deflate bit stream for decompression and correctly produces the original full-size data or file.

In this document, I will focus on the compression part of zlib, as well as zlib’s implementation of the <bold>deflate algorithm</bold>. 

{{% block note %}}
I will use the words <bold>“data bytes”</bold>, <bold>"bytes of data"</bold>, <bold>“data symbols”</bold>, <bold>"data stream"</bold>, <bold>"bit stream"</bold> to indicate the data to be compressed. In the following part these words have the same meaning and are interchangeable. 
{{% /block %}}