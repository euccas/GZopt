---
title: "3.3.4. Adaptive Search Limit"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_adaptive_search_limit"
weight: 84
---

When searching for the longest match in the hash chain, zlib limits the <bold>chain length</bold> it searches to improve searching efficiency. The search limit is set by:

1. The predefined <code>max_chain_length</code> value. This value is different for different compression levels.
2. In the searching process, if a match has been found and its length is not less than a predefined <code>good_match</code> length, the search length will be shortened as <code>new_search_chain_length = search_chain_length / 4</code>

The search limit values are defined in a <bold>configuration table</bold>:

{{< highlight c "linenos=inline" >}}
local const config configuration_table[10] = {
/*      good lazy nice max_chain_length */
/* 0 */ {0,    0,  0,    0, deflate_stored},  /* store only */
/* 1 */ {4,    4,  8,    4, deflate_fast}, /* max speed, no lazy matches */
/* 2 */ {4,    5, 16,    8, deflate_fast},
/* 3 */ {4,    6, 32,   32, deflate_fast},
/* 4 */ {4,    4, 16,   16, deflate_slow},  /* lazy matches */
/* 5 */ {8,   16, 32,   32, deflate_slow},
/* 6 */ {8,   16, 128, 128, deflate_slow},
/* 7 */ {8,   32, 128, 256, deflate_slow},
/* 8 */ {32, 128, 258, 1024, deflate_slow},
/* 9 */ {32, 258, 258, 4096, deflate_slow}}; /* max compression */
{{< / highlight >}}

{{% block note %}}
In above code snippet:

* <code>0</code> - <code>9</code> are compression levels.
* <code>good</code>, <code>lazy</code>, <code>nice</code> are the values of the length of a good match, a lazy match and a nice match.
* <code>max_chain_length</code> is the max chain length zlib searches.

{{% /block %}}