# Array — Two Pointer

## What are they
A technique where you use two index variables (pointers) that move through an array — either from opposite ends toward each other, in the same direction at different speeds, or to partition elements around a pivot — instead of using nested loops.

## Why we need it
Brute-force array problems (pair sums, comparisons between elements) are often solved with nested loops in O(n²). Two pointers exploit sorted order or a single-pass invariant to cut this down to O(n), without extra space.

## How to know when to use it
- Array is sorted (or can be sorted) and you need pairs/triplets satisfying a sum/difference condition.
- You need to compare elements from both ends (palindrome-like checks, reversing).
- You need to detect a cycle or find a middle element (fast/slow).
- You need to rearrange elements in-place around a condition (0s/1s/2s, negatives/positives).
- Keywords: "sorted array", "pair with sum", "in-place", "without extra space", "cycle detection".

## Concept in detail

### a) Opposite ends (left + right)
Start `left = 0`, `right = n-1`. Move them toward each other based on a comparison.
Example — Two Sum II (sorted array): if `arr[left]+arr[right] < target`, move `left++`; if greater, move `right--`; if equal, found.
Works because moving `left` right only increases the sum, moving `right` left only decreases it — monotonic behavior lets you discard half the search space each step.

### b) Same direction (fast & slow pointers)
Both pointers start together but move at different speeds or one advances only under a condition, while the other always advances.
- **In-place array modification**: `slow` marks the position to write the next valid element, `fast` scans ahead (e.g., removing duplicates from sorted array).
- **Cycle detection (Floyd's)**: `slow` moves 1 step, `fast` moves 2 steps; if they meet, a cycle exists.

### c) Partition / Dutch national flag
Three pointers (`low`, `mid`, `high`) partition the array into three regions in a single pass — classic for sorting an array of 0s, 1s, 2s, or partitioning around a pivot (quicksort's partition step).
- `low`: boundary of the "0/less-than-pivot" region
- `mid`: current element under examination
- `high`: boundary of the "2/greater-than-pivot" region
Swap and move pointers based on whether `arr[mid]` belongs to the low, middle, or high group.

## Problems (LeetCode examples)
- 167. Two Sum II - Input Array Is Sorted (opposite ends)
- 11. Container With Most Water (opposite ends)
- 26. Remove Duplicates from Sorted Array (same direction)
- 283. Move Zeroes (same direction)
- 141. Linked List Cycle (fast/slow — conceptually same pattern)
- 75. Sort Colors (Dutch national flag)

## Additional practice problems
- 15. 3Sum
- 16. 3Sum Closest
- 18. 4Sum
- 42. Trapping Rain Water
- 977. Squares of a Sorted Array
- 259. 3Sum Smaller
- 88. Merge Sorted Array
- 27. Remove Element
- 80. Remove Duplicates from Sorted Array II
