---
title: "2.2. LZ77"
date: 2019-01-04T20:55:57+07:00
anchor: "deflate_lz77"
weight: 30
---

LZ77 is a dictionary based lossless compression algorithm. It is also known as LZ1.

The basic idea of dictionary based algorithms is to replace an occurrence of a particular sequence of bytes in data with a reference to a previous occurrence of that sequence. 

There are two main types of dictionary based compression algorithms: LZ77 and LZ78. These two algorithms are named after the two creators [Jakob Ziv](https://de.wikipedia.org/wiki/Jacob_Ziv) and [Abraham Lempel](https://en.wikipedia.org/wiki/Abraham_Lempel). LZ77 (Lempel-Ziv77) and LZ78 (Lempel-Ziv78) were published in papers in 1977 and 1978, respectively. 

LZ77 compression algorithm works by using a <bold>sliding window</bold> to find sequences of data that are repeated, and encoding each repeated sequence by a pair of numbers called a <bold>length-distance pair</bold>. 
