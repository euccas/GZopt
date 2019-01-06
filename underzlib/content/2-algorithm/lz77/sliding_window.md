---
title: "2.2.1. Sliding Window"
date: 2019-01-04T20:55:57+07:00
anchor: "deflate_sliding_window"
weight: 31
---

The sliding window is used to examine the input data sequence, and to maintain the historical data that serve as the dictionary. In other words, the dictionary is a portion of the previously appeared and encoded data. 

The sliding window consists of two parts: a <bold>search buffer</bold>, and a <bold>look-ahead buffer</bold>. The search buffer contains the dictionary - the recent encoded data, and the look-ahead buffer contains the next portion of input data sequence to be encoded. The following figure gives an example of a sliding window.

![Sliding Window](/sliding_window.png)

The <bold>size of the sliding window</bold> is one of the key factors that affect compression performance. If the sliding window is too small, the compressor might find less repeated data sequences, as a result the compressed file size will be larger. If the sliding window is too large, the compressor might need spend longer time to find repeated data sequences, consequently the compression speed will be slower. 

In practice, typically the size of the sliding window can be from several KB to MB, such as 4 KB, 32 KB, 1 MB, or 4 MB.
