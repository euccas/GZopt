---
title: "3.3.3. Hash Chain"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_hash_chain"
weight: 83
---

As explained earlier, Rabin-Karp algorithm checks the hash value of substrings in order to find matches in text. To find matches in the search buffer which stores recent data symbols, zlib uses a <bold>hash chain organization</bold> to keep records of the hash values of every 3 (or other values defined by <code>MIN_MATCH</code>) bytes. 

This hash chain in zlib is implemented by using two arrays: <code>prev[]</code> and <code>head[]</code>. Both arrays stores the positions in the sliding window. The <code>head[]</code> array stores the heads of the hash chains, the <code>prev[]</code> array stores and links the positions of strings with the same hash index. The following figure shows an example of how the hash chain works.

![Hash Chain](./hash_chain.png)

{{% block note %}}
In this example, the <code>HashValue</code> function and its results are just examples, and they are not accurate.
{{% /block %}}


The size of <code>prev[]</code> is limited to half of the sliding window. Because the link that <code>prev[]</code> maintains is only for the data in the search buffer, and that’s only last 32K strings by default. An index in <code>prev[]</code> array is a window index modulo 32K.

Following code snippets show how zlib implements the hash chain organization. The hash size changes with parameter <code>memLevel</code>, which is configured for each compression level.

{{< highlight c "linenos=inline" >}}
s->hash_bits = (uInt)memLevel + 7;
s->hash_size = 1 << s->hash_bits;

s->prev   = (Posf *)  ZALLOC(strm, s->w_size, sizeof(Pos));
s->head   = (Posf *)  ZALLOC(strm, s->hash_size, sizeof(Pos));

#define UPDATE_HASH(s,h,c) (h = (((h)<<s->hash_shift) ^ (c)) & s->hash_mask)

#define INSERT_STRING(s, str, match_head) \
   (UPDATE_HASH(s, s->ins_h, s->window[(str) + (MIN_MATCH-1)]), \
    match_head = s->prev[(str) & s->w_mask] = s->head[s->ins_h], \
    s->head[s->ins_h] = (Pos)(str))
#endif

#define CLEAR_HASH(s) \
    s->head[s->hash_size-1] = NIL; \
    zmemzero((Bytef *)s->head, (unsigned)(s->hash_size-1)*sizeof(*s->head));
{{< / highlight >}}

{{% block note %}}
In <code>CLEAR_HASH</code>, array<code>head[]</code> is cleared. Array <code>prev[]</code> is cleared on the fly, not here.
{{% /block %}}