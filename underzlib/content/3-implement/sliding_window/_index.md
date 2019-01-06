---
title: "3.2. Sliding Window"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_sliding_window"
weight: 70
---

In zlib, the default size of sliding window is 64KB. The sliding window is divided into two parts, corresponding to the <bold>search buffer</bold> and <bold>look-ahead buffer</bold>, and each part is 32KB. Input bytes are read into the second half of the window, and move to the first half later to keep a dictionary of at least 32KB. This organization ensures that IO is always performed with a length multiple of the block size (8KB). Also, the 64KB limit is quite useful on older platform MSDOS.

The following code snippet shows how the sliding window is initialized. The macro <code>MAX_WBITS</code> determines the size of the sliding window. It’s configurable and the default value is 15, which leads to a 32KB search buffer and a 64KB sliding window.

{{< highlight c "linenos=inline" >}}
define MAX_WBITS   15 /* 32K LZ77 window */

s->w_bits = windowBits;
s->w_size = 1 << s->w_bits;
s->w_mask = s->w_size - 1;

s->window = (Bytef *) ZALLOC(strm, s->w_size, 2*sizeof(Byte));
{{< / highlight >}}

Data are copied into sliding window when look-ahead buffer becomes insufficient. This process is implemented inside function <code>fill_window</code>.

{{< highlight c "linenos=inline" >}}
local void fill_window(s)
    deflate_state *s;
{
    ...
}
{{< / highlight >}}