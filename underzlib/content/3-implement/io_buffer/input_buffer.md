---
title: "3.5.1. Input Buffer"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_input_buffer"
weight: 101
---

Before starting compression, zlib <bold>accumulates data</bold> in an <bold>input buffer</bold> and starts compression when the input buffer is full. Default input buffer size is 8KB. 

The reason of having the input buffer is that zlib won’t generate any output data until 16K data symbols have been generated in the <bold>literal buffer</bold> (default size of the literal buffer is 16K, see the [next section](#zlib_literal_buffer) for details about the literal buffer). Therefore starting compression with very short length of data has no benefit. Using the input buffer improves the efficiency of I/O.

The default input buffer size can be changed using <code>gzbuffer</code> function.

{{< highlight c "linenos=inline" >}}
gzbuffer(file, size)
{
    ...
    state->want = size;
    ...
}
{{< / highlight >}}
