# Two Pointers — Complete Guide (Python)

Two pointers is a technique where you use **two index variables** to traverse a data structure (usually an array, string, or linked list) instead of nested loops. It converts many O(n²) brute-force solutions into O(n) solutions.

There are 5 main patterns. Each has: **when to use it**, **the template**, **a worked example**, and **LeetCode problems** to practice.

---

## Pattern 1: Opposite Direction (Converging Pointers)

**When to use:** Sorted array/string, and you need to find a pair/triplet satisfying some condition, or check symmetry (palindrome).

**Idea:** One pointer starts at index 0 (`left`), the other at the last index (`right`). Move them toward each other based on a condition.

### Template
```python
def two_pointer_opposite(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current = arr[left] + arr[right]
        if current == target:
            return [left, right]
        elif current < target:
            left += 1      # need a bigger sum
        else:
            right -= 1     # need a smaller sum
    return [-1, -1]
```

### Worked Example — Two Sum II (sorted array)
```python
def two_sum_sorted(numbers, target):
    left, right = 0, len(numbers) - 1
    while left < right:
        s = numbers[left] + numbers[right]
        if s == target:
            return [left + 1, right + 1]   # 1-indexed
        elif s < target:
            left += 1
        else:
            right -= 1
    return []

print(two_sum_sorted([2, 7, 11, 15], 9))   # [1, 2]
```

### Worked Example — Valid Palindrome
```python
def is_palindrome(s: str) -> bool:
    s = [c.lower() for c in s if c.isalnum()]
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
```

### Practice on LeetCode
- 167. Two Sum II - Input Array Is Sorted
- 125. Valid Palindrome
- 15. 3Sum
- 11. Container With Most Water
- 42. Trapping Rain Water
- 977. Squares of a Sorted Array

---

## Pattern 2: Same Direction (Slow-Fast, In-place Modification)

**When to use:** In-place array modification — removing duplicates, moving zeros, partitioning. Both pointers start at index 0; `slow` marks the "write" position, `fast` scans ahead.

### Template
```python
def same_direction(arr):
    slow = 0
    for fast in range(len(arr)):
        if some_condition(arr[fast]):
            arr[slow], arr[fast] = arr[fast], arr[slow]
            slow += 1
    return slow   # new length / boundary
```

### Worked Example — Remove Duplicates from Sorted Array
```python
def remove_duplicates(nums):
    if not nums:
        return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1

nums = [0,0,1,1,1,2,2,3,3,4]
k = remove_duplicates(nums)
print(k, nums[:k])   # 5 [0, 1, 2, 3, 4]
```

### Worked Example — Move Zeroes
```python
def move_zeroes(nums):
    slow = 0
    for fast in range(len(nums)):
        if nums[fast] != 0:
            nums[slow], nums[fast] = nums[fast], nums[slow]
            slow += 1
```

### Practice on LeetCode
- 26. Remove Duplicates from Sorted Array
- 27. Remove Element
- 283. Move Zeroes
- 80. Remove Duplicates from Sorted Array II
- 75. Sort Colors (Dutch National Flag — a 3-pointer variant)

---

## Pattern 3: Fast & Slow Pointers (Cycle Detection — Floyd's Algorithm)

**When to use:** Linked lists (or any "functional graph") — detecting cycles, finding the middle node, finding cycle start. `slow` moves 1 step, `fast` moves 2 steps.

### Template
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

### Worked Example — Find Middle of Linked List
```python
def middle_node(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow   # slow is the middle node
```

### Worked Example — Find Cycle Start (Linked List Cycle II)
```python
def detect_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            # cycle found — find entry point
            ptr = head
            while ptr != slow:
                ptr = ptr.next
                slow = slow.next
            return ptr
    return None
```

### Practice on LeetCode
- 141. Linked List Cycle
- 142. Linked List Cycle II
- 876. Middle of the Linked List
- 202. Happy Number (Floyd's cycle detection on numbers, not a list!)
- 234. Palindrome Linked List (uses middle-finding + reversal)

---

## Pattern 4: Sliding Window (Variable-Size Two Pointers)

**When to use:** Contiguous subarray/substring problems — "longest/shortest subarray satisfying X". Technically a two-pointer variant: `left` and `right` define a window that expands (`right += 1`) and shrinks (`left += 1`) based on a condition.

### Template
```python
def sliding_window(arr, k):
    left = 0
    window_sum = 0
    best = 0
    for right in range(len(arr)):
        window_sum += arr[right]
        while window_sum > k:          # shrink while condition violated
            window_sum -= arr[left]
            left += 1
        best = max(best, right - left + 1)
    return best
```

### Worked Example — Longest Substring Without Repeating Characters
```python
def length_of_longest_substring(s: str) -> int:
    seen = set()
    left = 0
    best = 0
    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1
        seen.add(s[right])
        best = max(best, right - left + 1)
    return best

print(length_of_longest_substring("abcabcbb"))  # 3
```

### Worked Example — Minimum Size Subarray Sum
```python
def min_subarray_len(target, nums):
    left = 0
    total = 0
    best = float('inf')
    for right in range(len(nums)):
        total += nums[right]
        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1
    return best if best != float('inf') else 0
```

### Practice on LeetCode
- 3. Longest Substring Without Repeating Characters
- 209. Minimum Size Subarray Sum
- 76. Minimum Window Substring
- 424. Longest Repeating Character Replacement
- 567. Permutation in String
- 1004. Max Consecutive Ones III

---

## Pattern 5: Two Pointers on Two Different Sequences

**When to use:** Merging or comparing two sorted arrays/strings — merge step of merge sort, comparing two sorted lists, checking subsequences.

### Template
```python
def merge_two_sorted(a, b):
    i, j = 0, 0
    result = []
    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extend(a[i:])
    result.extend(b[j:])
    return result
```

### Worked Example — Merge Sorted Array (in-place, from the back)
```python
def merge(nums1, m, nums2, n):
    i, j, k = m - 1, n - 1, m + n - 1
    while j >= 0:
        if i >= 0 and nums1[i] > nums2[j]:
            nums1[k] = nums1[i]
            i -= 1
        else:
            nums1[k] = nums2[j]
            j -= 1
        k -= 1
```

### Worked Example — Is Subsequence
```python
def is_subsequence(s: str, t: str) -> bool:
    i = j = 0
    while i < len(s) and j < len(t):
        if s[i] == t[j]:
            i += 1
        j += 1
    return i == len(s)
```

### Practice on LeetCode
- 88. Merge Sorted Array
- 21. Merge Two Sorted Lists
- 392. Is Subsequence
- 986. Interval List Intersections
- 349. Intersection of Two Arrays
- 415. Add Strings

---

## Quick Decision Cheat-Sheet

| Signal in the problem | Pattern to use |
|---|---|
| Sorted array, find pair/triplet with a target sum | Pattern 1 (Opposite direction) |
| "Remove in-place", "move to front/back" | Pattern 2 (Slow-Fast, same direction) |
| Linked list, "cycle", "middle node" | Pattern 3 (Fast & Slow / Floyd's) |
| "Longest/shortest contiguous subarray/substring" | Pattern 4 (Sliding window) |
| Two separate sorted arrays/strings to merge/compare | Pattern 5 (Two sequences) |

## Suggested Order to Solve

1. 125. Valid Palindrome
2. 167. Two Sum II
3. 26. Remove Duplicates from Sorted Array
4. 283. Move Zeroes
5. 11. Container With Most Water
6. 15. 3Sum
7. 141. Linked List Cycle
8. 876. Middle of the Linked List
9. 3. Longest Substring Without Repeating Characters
10. 209. Minimum Size Subarray Sum
11. 88. Merge Sorted Array
12. 42. Trapping Rain Water (harder — good capstone)

