# Array — Kadane's / Subarray

## What are they
Kadane's algorithm is a dynamic-programming technique that scans an array once, at each index deciding whether to extend the previous subarray or start a new one, to track the best (max/min) contiguous subarray so far.

## Why we need it
Finding the maximum sum/product contiguous subarray naively requires checking all O(n²) subarrays. Kadane's reduces this to a single O(n) pass by maintaining a running "best ending here" value.

## How to know when to use it
- "Maximum/minimum sum (or product) contiguous subarray."
- Problem is about a contiguous run, not any subset.
- You can define a local optimum at index `i` in terms of the local optimum at `i-1`.
- Keywords: "maximum subarray", "largest sum", "contiguous", "maximum product subarray".

## Concept in detail

### a) Max subarray sum (Kadane's)
`currentMax = max(arr[i], currentMax + arr[i])`; `globalMax = max(globalMax, currentMax)`.
At each index you decide: is it better to extend the running subarray, or abandon it and start fresh at `arr[i]`? This works because a negative running sum can never help a future subarray, so it's safe to discard it.

### b) Max product subarray
Trickier than sum because multiplying by a negative number flips max and min. Maintain both `currentMax` and `currentMin` at each step:
`currentMax = max(arr[i], currentMax*arr[i], currentMin*arr[i])`
`currentMin = min(arr[i], currentMax*arr[i], currentMin*arr[i])` (using the *previous* currentMax/currentMin).
A very negative number can become the new max once multiplied by another negative later, so you must track the minimum too.

### c) Subarray with given XOR / sum
Extension of the prefix technique: instead of just finding the max, you're finding subarrays whose sum (or XOR) equals an exact target — solved by combining prefix sum/XOR with a hashmap that stores counts/first-occurrence indices of prefix values.

## Problems (LeetCode examples)
- 53. Maximum Subarray (classic Kadane's)
- 152. Maximum Product Subarray
- 918. Maximum Sum Circular Subarray
- 325. Maximum Size Subarray Sum Equals k
- 560. Subarray Sum Equals K (prefix + hashmap variant)

## Additional practice problems
- 1425. Constrained Subsequence Sum
- 494. Target Sum (different technique but related sum-search mindset)
- 1567. Maximum Length of Subarray With Positive Product
- 363. Max Sum of Rectangle No Larger Than K (2D extension)
- 152. Maximum Product Subarray
- 1191. K-Concatenation Maximum Sum
- 1186. Maximum Subarray Sum with One Deletion
