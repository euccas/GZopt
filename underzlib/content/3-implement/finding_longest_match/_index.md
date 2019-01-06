---
title: "3.3. Finding Longest Match"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_longest_match"
weight: 80
---

The technique zlib uses to find the longest match in the search buffer is straightforward, and it turns out to be the fastest for most input files: use a string matching algorithm to find possible matches, then try all possible matches and select the longest. 

The matching algorithm for small strings is inspired from <bold>Rabin-Karp algorithm</bold>. The key feature of this algorithm is that insertions into the string dictionary are very simple and thus fast, and deletions are avoided completely. Insertions are performed at each input character, whereas string matches are performed only when the previous match ends. So it is preferable to spend more time in matches to allow very fast string insertions and avoid deletions. A brute force approach is used to find longer strings when a small match has been found.

So in summary, the process of finding the longest match has two major parts:

1. In the sliding window, for each data symbol in the look-ahead buffer, use a Rabin-Karp algorithm based method to find <bold>a possible match</bold> in the search buffer, and record the match start position. There can be multiple possible matches available.
2. For each possible match, starting from the match start position, check each following data symbol to find the <bold>current longest match</bold>. Search in all the possible matches found in step 1, until finding <bold>the longest match</bold>, or finding a match whose length exceeds the pre-defined <bold>longest match limit</bold>.
