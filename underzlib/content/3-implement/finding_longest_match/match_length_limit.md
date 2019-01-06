---
title: "3.3.1. Match Length Limit"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_match_length"
weight: 81
---

zlib defines a <code>MIN_MATCH</code> and a <code>MAX_MATCH</code> as the <bold>minimum</bold> and <bold>maximum</bold> match lengths it searches for.

{{< highlight c "linenos=inline" >}}
#define MIN_MATCH  3
#define MAX_MATCH  258
{{< / highlight >}}

The <code>MIN_MATCH</code> is set to 3. The reason of having a minimum match length equals to 3 is obvious: the matches shorter than 3 will not help reduce the encoded data size, because the encoded data symbols will have the same or longer length.

This value of <code>MIN_MATCH</code> cannot be changed unless you change related code, such as calling <code>UPDATE_HASH</code> function for how many times. 

The <code>MAX_MATCH</code> is set to 258. This number comes from the fact that one length-distance pair, which is the output of the LZ77 encoded data symbols, can represent at most 258 bytes. A length requires at least one bit and a distance requires at least one bit, so two bits in can give 258 bytes out.

The value of <code>MAX_MATCH</code> in zlib can be changed, but the change might affect compression performance. Also in zlib there is some logic controlled by condition <code>MAX_MATCH == 258</code>. Those codes, when enabled, could improve compression performance when using a modern compiler.

{{< highlight c "linenos=inline" >}}
#if (defined(UNALIGNED_OK) && MAX_MATCH == 258)
        /* This code assumes sizeof(unsigned short) == 2. Do not use
         * UNALIGNED_OK if your compiler uses a different size.
         */
        if (*(ushf*)(match+best_len-1) != scan_end ||
            *(ushf*)match != scan_start) continue;
        ...
{{< / highlight >}}
