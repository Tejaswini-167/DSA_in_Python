# Array — Prefix Based

## What are they
Precomputed cumulative arrays (`prefix[i]` = aggregate of `arr[0..i]`) that let you answer range queries (sum, XOR, count) in O(1) after O(n) preprocessing, instead of recomputing the range each query.

## Why we need it
Repeated range queries (sum of subarray [l, r], multiple times) done naively cost O(n) each, O(n·q) total for q queries. Prefix arrays reduce each query to O(1), total O(n + q).

## How to know when to use it
- Multiple range-sum/range-XOR queries on a static (unchanging) array.
- "Number of subarrays with sum/XOR equal to k" — pair with a hashmap of prefix values seen so far.
- 2D grid range-sum queries.
- Keywords: "range sum query", "subarray sum equals k", "number of subarrays", "immutable array".

## Concept in detail

### a) Prefix Sum
`prefix[i] = arr[0] + arr[1] + ... + arr[i]`. Range sum `[l, r] = prefix[r] - prefix[l-1]`.
For "count subarrays with sum = k": as you compute running prefix sum, check how many times `(currentPrefix - k)` has appeared before using a hashmap — this converts an O(n²) search into O(n).

### b) Prefix XOR
Same idea but with XOR instead of sum: `prefixXor[i] = arr[0] ^ arr[1] ^ ... ^ arr[i]`. Range XOR `[l, r] = prefixXor[r] ^ prefixXor[l-1]` (since XOR is its own inverse). Useful for "subarray XOR equals k" using a hashmap of prefix XOR values, mirroring the prefix-sum-with-hashmap trick.

### c) 2D Prefix
Extension to matrices: `prefix[i][j]` = sum of all elements in the rectangle from `(0,0)` to `(i,j)`. Built using inclusion-exclusion:
`prefix[i][j] = grid[i][j] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]`.
Any sub-rectangle sum can then be computed in O(1) using four prefix lookups (also inclusion-exclusion).

## Problems (LeetCode examples)
- 303. Range Sum Query - Immutable (1D prefix sum)
- 304. Range Sum Query 2D - Immutable (2D prefix)
- 560. Subarray Sum Equals K (prefix sum + hashmap)
- 1310. XOR Queries of a Subarray (prefix XOR)
- 1524. Number of Sub-arrays With Odd Sum (prefix sum parity)

## Additional practice problems
- 523. Continuous Subarray Sum
- 974. Subarray Sums Divisible by K
- 1442. Count Triplets That Can Form Two Arrays of Equal XOR
- 1685. Sum of Absolute Differences in a Sorted Array
- 1109. Corporate Flight Bookings (difference array — related concept)
- 1314. Matrix Block Sum
- 1738. Find Kth Largest XOR Coordinate Value (2D prefix XOR)
