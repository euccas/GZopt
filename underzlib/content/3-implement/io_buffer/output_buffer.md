---
title: "3.5.3. Output Buffer"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_output_buffer"
weight: 103
---

For outputting the compressed data, zlib uses two buffers: a <bold>pending buffer</bold>, and an <bold>output buffer</bold>. The data flow is as shown in the following figure:

![Output Buffer](./output_buffer.png)

Upon initialization, zlib creates a pending buffer (default size is 36K), and an output buffer (default size is 8K). The output data are first <bold>accumulated in pending buffer</bold>, and then get <bold>copied to output buffer</bold>, finally be written to the output compressed zip or gz files.

Data are copied from pending buffer to output buffer in function <code>flush_pending</code>. This function is called when the literal buffer is full, which means a block of data has been processed. It’s also called in some other cases when flushing a block is needed. The length of data copied to the output buffer is limited by the available space in output buffer.

When the <bold>output buffer is full</bold>, or when <bold>flush signal</bold> is issued, zlib writes output buffer to zip or gz files.

zlib uses counters <code>pending_out</code> and <code>avail_out</code> to record how many bytes are available in pending buffer and output buffer. Counter value <code>0</code> means the buffer is full.

Related code snippets:

{{< highlight c "linenos=inline" >}}
flush_pending() {
    len = s->pending;
    if (len > strm->avail_out) len = strm->avail_out;
    if (len == 0) return;
 
    zmemcpy(strm->next_out, s->pending_out, len);
}
{{< / highlight >}}

{{< highlight c "linenos=inline" >}}
gzcomp() {
    if (strm->avail_out == 0 || (flush != Z_NO_FLUSH &&
            (flush != Z_FINISH || ret == Z_STREAM_END))) {
        have = (unsigned)(strm->next_out - state->x.next);
        if (have && ((got = write(state->fd, state->x.next, have)) < 0 || (unsigned)got != have)) {
            gz_error(state, Z_ERRNO, zstrerror());
            return -1;
        }
        if (strm->avail_out == 0) {
            strm->avail_out = state->size;
            strm->next_out = state->out;
       }
    }
}
{{< / highlight >}}
