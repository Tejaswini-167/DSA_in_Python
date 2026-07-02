# String — Two Pointers

## What are they
Two indices moving through a string — typically from both ends inward, or one scanning ahead while the other tracks a "write" position — used for in-place comparisons or rearrangement of characters.

## Why we need it
Comparing characters from both ends, or rewriting a string in place, done with extra arrays/reversal calls costs extra space and sometimes extra passes. Two pointers let you do the comparison/rewrite in a single O(n) pass with O(1) extra space.

## How to know when to use it
- You need to check symmetry (palindrome).
- You need to reverse/rearrange characters or words in place.
- You need to compress or rewrite a string by merging repeated runs.
- Keywords: "palindrome", "reverse", "in-place", "compress", "two ends".

## Concept in detail

### a) Palindrome check
`left = 0`, `right = n-1`. Compare `s[left]` and `s[right]`; if equal, move both inward; if not, it's not a palindrome (or, for "valid palindrome II", try skipping one character on either side and recurse/check once). Handles case-insensitivity/non-alphanumeric filtering by skipping invalid characters as pointers move.

### b) Reverse words / characters
For reversing characters: swap `s[left]` and `s[right]`, move both inward until they cross.
For reversing words in a sentence: split into words (or use pointers to identify word boundaries while skipping extra spaces), then either reverse the list of words or reverse the whole string first and then reverse each word individually (two-reversal trick) to achieve O(n) time, O(1) extra space (in-place variants).

### c) String compression
Use one pointer (`read`) to scan through runs of repeated characters and another (`write`) to write the compressed result (char + count) back into the array in place. Because the compressed output is never longer than the input, this can be done without extra space beyond a few counters.

## Problems (LeetCode examples)
- 125. Valid Palindrome
- 680. Valid Palindrome II
- 344. Reverse String
- 151. Reverse Words in a String
- 443. String Compression

## Additional practice problems
- 5. Longest Palindromic Substring (expand-around-center, related technique)
- 917. Reverse Only Letters
- 541. Reverse String II
- 9. Palindrome Number (numeric variant)
- 809. Expressive Words
- 6. Zigzag Conversion (pointer-based construction)
