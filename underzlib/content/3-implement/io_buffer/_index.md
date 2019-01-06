---
title: "3.5. I/O Buffer"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_io_buffer"
weight: 100
---

One important notion in the deflate compression is <bold>data blocks</bold>. The deflate compressed data format is composed of blocks, which have a header that depends on the block data. Therefore the output of deflate comes a block at a time, with nothing written (except a zlib or gzip header) until the first block is completed. Considering how the data blocks transmit in the deflate process, zlib implements several <bold>buffers</bold> to store data blocks and control I/O performance.
