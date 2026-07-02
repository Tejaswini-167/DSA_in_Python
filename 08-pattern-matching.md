# String — Pattern Matching

## What are they
Algorithms for finding occurrences of a pattern string `p` inside a text string `s` faster than the naive O(n·m) approach (sliding the pattern one character at a time and comparing fully each time).

## Why we need it
Naive substring search re-compares characters from scratch at every position, wasting work when partial matches share structure. KMP, Rabin-Karp, and Z-algorithm each exploit different pre-processing to skip redundant comparisons, bringing worst-case time down to O(n + m).

## How to know when to use it
- You need to find all (or the first) occurrence(s) of a pattern in a text, and the text/pattern can be long enough that O(n·m) is too slow.
- You need to detect periodicity or repeated structure in a string (KMP's failure function is often reused for this).
- You need to compare many patterns against a large text (Rabin-Karp is well-suited to multiple pattern search via hashing).
- Keywords: "find pattern occurrences", "substring search", "string matching", "shortest repeating unit", "count of matches".

## Concept in detail

### a) KMP (Knuth-Morris-Pratt) — failure function
Precompute the **LPS array** (Longest Proper Prefix which is also Suffix) for the pattern: `lps[i]` = length of the longest prefix of `p[0..i]` that is also a suffix. During matching, when a mismatch occurs at text position `j` after matching `k` pattern characters, instead of restarting from scratch, jump the pattern pointer to `lps[k-1]` — reusing the fact that the matched prefix already tells you how much of the pattern could still align. This avoids ever moving the text pointer backward, giving O(n + m).

### b) Rabin-Karp (rolling hash)
Compute a hash of the pattern and a hash of each length-`m` window of the text. Instead of recomputing the window hash from scratch each shift, use a **rolling hash** formula to update it in O(1): remove the contribution of the outgoing character and add the incoming one (like a sliding-window prefix trick, but multiplicative with a base and modulus). When hashes match, do a direct character comparison to rule out hash collisions. Average case O(n + m); worst case O(n·m) with many collisions.

### c) Z-algorithm
Build a **Z-array** for the string `p + '#' + s` (pattern concatenated with text, separated by a character not present in either), where `Z[i]` = length of the longest substring starting at `i` that matches a prefix of the whole string. Computed in O(n) using a "Z-box" (window of last known match) to avoid re-comparing characters already known to match. Any position where `Z[i] == len(p)` marks a pattern occurrence in the text — used broadly for substring search, counting distinct substrings, and prefix-related string problems.

## Problems (LeetCode examples)
- 28. Find the Index of the First Occurrence in a String (naive vs. KMP/Rabin-Karp)
- 214. Shortest Palindrome (uses KMP's failure-function idea)
- 459. Repeated Substring Pattern (uses KMP's LPS/period idea)
- 1392. Longest Happy Prefix (directly the LPS array from KMP)
- 187. Repeated DNA Sequences (hashing, Rabin-Karp style)

## Additional practice problems
- 796. Rotate String
- 1044. Longest Duplicate Substring (binary search + Rabin-Karp hashing)
- 1316. Distinct Echo Substrings
- 686. Repeated String Match
- 2223. Sum of Scores of Built Strings (Z-function application)
- 1392. Longest Happy Prefix
- 30. Substring with Concatenation of All Words (hashing/window combo)
