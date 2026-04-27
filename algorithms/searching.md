# Binary Search & Variants

## Classic Binary Search

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2   # avoids overflow
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

## Template: Find Leftmost Position (lower bound)
Returns index of first element ≥ target.

```python
def lower_bound(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left
```

## Template: Find Rightmost Position (upper bound)
Returns index of first element > target.

```python
def upper_bound(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = (left + right) // 2
        if nums[mid] <= target:
            left = mid + 1
        else:
            right = mid
    return left
```

## Python `bisect` Module

```python
import bisect

nums = [1, 3, 5, 7, 9]
bisect.bisect_left(nums, 5)   # 2 — index of first element >= 5
bisect.bisect_right(nums, 5)  # 3 — index of first element > 5

bisect.insort_left(nums, 4)   # insert 4, maintaining sort order
```

## Binary Search on Answer
Use when you can check a condition on a range of values.

```python
def feasible(value):
    # return True if 'value' satisfies the condition
    ...

left, right = min_possible, max_possible
while left < right:
    mid = (left + right) // 2
    if feasible(mid):
        right = mid      # search left half (find minimum feasible)
    else:
        left = mid + 1
return left
```

## Complexity

| Case | Time | Space |
|---|---|---|
| All variants | O(log n) | O(1) |

## Common Interview Problems

| Problem | Variant |
|---|---|
| Binary Search | Classic |
| Search in Rotated Sorted Array | Find pivot + classic |
| Find First and Last Position | Lower / upper bound |
| Koko Eating Bananas | Binary search on answer |
| Median of Two Sorted Arrays | Binary search on partition |
| Capacity to Ship Packages | Binary search on answer |
