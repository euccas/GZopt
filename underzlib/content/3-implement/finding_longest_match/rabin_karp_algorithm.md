---
title: "3.3.2. Rabin-Karp Algorithm"
date: 2019-01-04T20:52:57+07:00
anchor: "zlib_rabin_karp"
weight: 82
---

Rabin-Karp algorithm is a string-searching algorithm created by [Richard M. Karp](https://en.wikipedia.org/wiki/Richard_M._Karp) and [Michael O. Rabin](https://en.wikipedia.org/wiki/Michael_O._Rabin). It uses hashing to find any one of a set of pattern strings in a text. For example, given a text <code>"AABAACAADAABAABA"</code>, and a pattern <code>"AABA"</code>, we can use Rabin-Karp algorithm to find pattern exists in the text at index <code>0</code>, <code>9</code>, <code>12</code>.

Following pseudo code describes how Rabin-Karp algorithm works.

{{< highlight python "linenos=inline" >}}
# p is a pattern, its length is m
# t is text, its length is n
# the algorithm searches for pattern p in text t

Compute hash_p (for pattern p)
Compute hash_t (for the first substring of t with m length)
for i = 0 to n - m:
    if hash_p == hash_t:
        Match t[i . . . i+m-1] with p, if matched return 1
    else:
        Update hash_t for t[i+1 . . . i+m] using rolling hash
End
{{< / highlight >}}

The <bold>average</bold> and <bold>best case running time</bold> of the Rabin-Karp algorithm is *O(n+m)*, where n is the length of text, and m is the length of pattern. But its <bold>worst-case</bold> time is *O(nm)*. Worst case of Rabin-Karp algorithm occurs when all characters of pattern and text are same as the hash values of all the substrings of text match with hash value of pattern. For example <code>text = "AAAAAAA"</code> and <code>pattern = "AAA"</code>.

The key to the Rabin-Karp algorithm's performance is the efficient computation of hash values of the successive substrings of the text, by using the <bold>rolling hash</bold> technique. The benefit of [rolling hash](https://en.wikipedia.org/wiki/Rolling_hash) is it computes the hash value of the next substring from the previous one by doing only a constant number of operations, rather than having to rehash the complete substring. 
