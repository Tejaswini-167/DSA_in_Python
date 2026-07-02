# Array — Binary Search

## What are they
A divide-and-conquer search technique that repeatedly halves a search space based on a monotonic condition, converging on an answer in O(log n) instead of O(n).

## Why we need it
Linear scanning of a sorted structure (or a monotonic answer space) wastes information — binary search uses the fact that once you know the condition is true/false at a midpoint, you can discard half the remaining candidates.

## How to know when to use it
- Array is sorted, and you're looking for a specific value or insertion point.
- The *answer itself* (not an array index) is monotonic — i.e., if some value `x` works, all values `>x` (or `<x`) also work/don't work. This lets you binary search over the *answer range* rather than the array.
- Keywords: "sorted array", "find minimum/maximum such that...", "search in rotated sorted array", "capacity/speed/days to complete...".

## Concept in detail

### a) On index
Classic binary search over array positions: `low=0, high=n-1`; compare `arr[mid]` to target and shrink `low`/`high` accordingly. Variants: find first/last occurrence, search in rotated sorted array, find peak element — all rely on some monotonic property of `arr[mid]` relative to boundaries.

### b) On answer
You don't search the array directly — you binary search over the *range of possible answers* (e.g., 1 to max value). For a candidate answer `x`, you write a `feasible(x)` check (often O(n)) that tells you whether `x` satisfies the problem's constraint. Because feasibility is monotonic in `x` (true for all `x ≥ answer` or all `x ≤ answer`), you binary search on `x` to find the boundary. Total complexity becomes O(n log(range)).
Example: "Minimum days to make m bouquets", "Koko eating bananas — minimum eating speed", "Capacity to ship packages within D days".

## Problems (LeetCode examples)
- 704. Binary Search (on index — basics)
- 33. Search in Rotated Sorted Array (on index)
- 34. Find First and Last Position of Element in Sorted Array (on index)
- 875. Koko Eating Bananas (on answer)
- 1011. Capacity To Ship Packages Within D Days (on answer)
- 410. Split Array Largest Sum (on answer)

## Additional practice problems
- 74. Search a 2D Matrix
- 153. Find Minimum in Rotated Sorted Array
- 162. Find Peak Element
- 1482. Minimum Number of Days to Make m Bouquets
- 1552. Magnetic Force Between Two Balls
- 4. Median of Two Sorted Arrays (advanced binary search)
- 378. Kth Smallest Element in a Sorted Matrix
