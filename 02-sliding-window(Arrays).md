# Array — Sliding Window

## What are they
A window (contiguous subarray) defined by two pointers (`start`, `end`) that "slides" across the array, expanding and shrinking to maintain a property, avoiding recomputation from scratch for every subarray.

## Why we need it
Many problems ask for the best/valid contiguous subarray satisfying some condition. Checking every subarray is O(n²) or O(n³). Sliding window reuses work from the previous window state, bringing it down to O(n).

## How to know when to use it
- Problem mentions "contiguous subarray/substring", "at most/exactly k", "longest/shortest subarray with condition X".
- The condition can be incrementally updated when you add/remove one element (sum, count, frequency map).
- Keywords: "subarray", "window of size k", "maximum/minimum length satisfying...".

## Concept in detail

### a) Fixed Size
Window size `k` is constant. Slide by adding `arr[end]` and removing `arr[start]` together, keeping the window size always `k`.
Example: Maximum sum subarray of size k — maintain a running sum; subtract the outgoing element and add the incoming one each step. O(n) instead of O(n·k).

### b) Variable Size
Window grows/shrinks based on a condition — no fixed length.

- **Expand–Shrink**: Expand `end` to include more elements until the window becomes invalid (or a target is met); then shrink from `start` while it stays valid/invalid to find the optimal boundary. Used for "longest subarray with sum ≤ k", "smallest subarray with sum ≥ target".
- **Monotonic Window**: Maintain a monotonic deque/structure inside the window to answer "max/min in current window" in O(1) amortized, instead of scanning the window each time. Used in problems like Sliding Window Maximum, where you need the max of every window of size k efficiently.

## Problems (LeetCode examples)
- 643. Maximum Average Subarray I (fixed size)
- 209. Minimum Size Subarray Sum (variable, expand-shrink)
- 239. Sliding Window Maximum (monotonic window)
- 1052. Grumpy Bookstore Owner (fixed size)
- 1004. Max Consecutive Ones III (variable, expand-shrink)

## Additional practice problems
- 904. Fruit Into Baskets
- 992. Subarrays with K Different Integers
- 1438. Longest Continuous Subarray With Absolute Diff ≤ Limit (monotonic deque)
- 1456. Maximum Number of Vowels in a Substring of Given Length
- 2461. Maximum Sum of Distinct Subarrays With Length K
- 2134. Minimum Swaps to Group All 1's Together II
- 1499. Max Value of Equation (monotonic deque)
