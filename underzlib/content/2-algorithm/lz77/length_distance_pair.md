---
title: "2.2.2. Length-Distance Pair"
date: 2019-01-04T20:55:57+07:00
anchor: "deflate_length_distance_pair"
weight: 32
---

The length-distance pair indicates that each of the next <bold>length</bold> characters is the same as the character exactly <bold>distance</bold> characters behind it in the original data stream. 

In LZ77 algorithm, the compressor searches back through the search buffer until it finds a match to the first character in the look-ahead buffer. There could be more than one matches exist in the search buffer, and the compressor will find the one match having the longest length. When the <bold>longest match</bold> is found, the compressor encodes it with a triple <bold>(D, L, C)</bold> where:

* D = distance of the search cursor from the start of look-ahead buffer
* L = length of longest match
* C = next character in look-ahead buffer beyond longest match

The reason of adding the third element *C* in the triple is for handling the case where no match is found in the search buffer. In that case, the values of both *D* and *L* are 0, and *C* is the first character in current look-ahead buffer.

The following figure shows an example of how LZ77 finds a longest match and encodes the repeated characters for a given string <code>"axrrmaxrbaxssr"</code>.

![Length Distance Pair](./length_distance_pair.png)

In practice, a compressor can optimize the encoding output according to its own implementation, and choose output formats other than the <bold>(D, L, C)</bold> triplet. 
