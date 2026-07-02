# String — Sliding Window

## What are they
Same window-sliding idea as with arrays, but applied to characters. Two pointers (`start`, `end`) mark a substring; a frequency map or counter tracks characters inside the window, updated incrementally as the window expands/shrinks.

## Why we need it
Substring problems checking every possible substring are O(n²) or O(n³) with naive re-scanning. Sliding window maintains character counts incrementally as the window moves, giving O(n) (or O(n·26) for fixed alphabets).

## How to know when to use it
- Problem involves a "substring" (contiguous) rather than a "subsequence".
- Asks for the longest/shortest/count of substrings meeting a character-frequency condition ("without repeating characters", "contains all characters of T", "is an anagram of").
- You can maintain validity of the window using a hashmap/array of character counts.
- Keywords: "substring", "distinct characters", "anagram", "permutation", "minimum window".

## Concept in detail

### a) Longest substring without repeat
Expand `end` one character at a time; keep a hashmap of `char -> last seen index`. If the incoming character was already in the current window, jump `start` to just after its last occurrence. Track `end - start + 1` as the max length seen.

### b) Minimum window substring
Classic expand-shrink: expand `end` until the window contains all required characters of pattern `t` (tracked via a "need" map and a `matched count`). Once valid, shrink `start` as much as possible while it stays valid, recording the minimum length window. Repeat until `end` reaches the string's end.

### c) Anagram / permutation in string
Use a fixed-size window equal to the length of the pattern. Maintain a frequency map of the pattern and a frequency map of the current window; slide the window one character at a time (add new char, remove outgoing char) and compare frequency maps (or a running "matches" counter) in O(1) per step, instead of re-sorting or re-comparing full maps each time.

## Problems (LeetCode examples)
- 3. Longest Substring Without Repeating Characters
- 76. Minimum Window Substring
- 438. Find All Anagrams in a String
- 567. Permutation in String
- 340. Longest Substring with At Most K Distinct Characters

## Additional practice problems
- 159. Longest Substring with At Most Two Distinct Characters
- 30. Substring with Concatenation of All Words
- 1156. Swap For Longest Repeated Character Substring
- 1208. Get Equal Substrings Within Budget
- 424. Longest Repeating Character Replacement
- 2024. Maximize the Confusion of an Exam
