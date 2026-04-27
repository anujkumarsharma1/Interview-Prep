# Arrays & Strings

## Complexity

| Operation | Time | Space |
|---|---|---|
| Access by index | O(1) | — |
| Search (unsorted) | O(n) | — |
| Search (sorted, binary) | O(log n) | — |
| Insert at end | O(1) amortized | — |
| Insert at index | O(n) | — |
| Delete at index | O(n) | — |

## Key Patterns

### Two Pointers
Use when working with sorted arrays or when you need to find a pair.
```python
left, right = 0, len(arr) - 1
while left < right:
    # process arr[left] and arr[right]
    left += 1
    right -= 1
```

### Sliding Window
Use for contiguous subarray / substring problems.
```python
window_start = 0
for window_end in range(len(arr)):
    # expand window by including arr[window_end]
    while <condition to shrink>:
        # shrink window from the left
        window_start += 1
    # update result with current window
```

### Prefix Sum
Pre-compute cumulative sums for O(1) range sum queries.
```python
prefix = [0] * (len(arr) + 1)
for i, val in enumerate(arr):
    prefix[i + 1] = prefix[i] + val

# range sum [l, r] (0-indexed)
range_sum = prefix[r + 1] - prefix[l]
```

## Common Tricks

- Use a **hash map** to achieve O(1) lookups (e.g., Two Sum).
- **Sort first** to simplify duplicate handling or pair-finding.
- Watch for **off-by-one errors** with indices and window boundaries.
- For in-place operations, process from the **end** of the array to avoid overwriting.

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Two Sum | Hash map |
| Maximum Subarray (Kadane's) | DP / running max |
| Product of Array Except Self | Prefix + suffix products |
| Container With Most Water | Two pointers |
| Longest Substring Without Repeating Characters | Sliding window |
| Find Minimum in Rotated Sorted Array | Modified binary search |
