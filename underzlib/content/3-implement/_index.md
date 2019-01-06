---
title: "3. Implementation of zlib"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_implementation"
weight: 50
---

The implementation of zlib is pragmatic and efficient. Over the past 20 years, people have made many attempts to improve the performance of compression applications, but it seems that we only achieve better performance by using algorithms other than deflate (and inflate), adopting parallel processing, or improving CPU level instructions. So zlib, as it states in its GitHub repository, is quite <bold>a massively spiffy yet delicately unobtrusive compression library</bold>.

In the following sections, we will look at some of the detailed techniques that zlib uses to implement the deflate compression algorithm. 
