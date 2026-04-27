# Two Pointers & Sliding Window

## Two Pointers

Use when the array is **sorted** or when you need to find pairs/triplets.

### Opposite Direction (squeeze inward)
```python
left, right = 0, len(arr) - 1
while left < right:
    current = arr[left] + arr[right]
    if current == target:
        return [left, right]
    elif current < target:
        left += 1
    else:
        right -= 1
```

### Same Direction (fast & slow)
```python
slow = 0
for fast in range(len(arr)):
    if condition(arr[fast]):
        arr[slow] = arr[fast]
        slow += 1
# arr[:slow] contains the kept elements
```

### Three Sum Pattern
```python
def three_sum(nums):
    nums.sort()
    result = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue  # skip duplicates
        left, right = i + 1, len(nums) - 1
        while left < right:
            s = nums[i] + nums[left] + nums[right]
            if s == 0:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]: left += 1
                while left < right and nums[right] == nums[right - 1]: right -= 1
                left += 1; right -= 1
            elif s < 0:
                left += 1
            else:
                right -= 1
    return result
```

## Sliding Window

Use for problems on **contiguous subarrays or substrings**.

### Fixed-Size Window
```python
k = 3   # window size
window_sum = sum(arr[:k])
max_sum = window_sum
for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i - k]
    max_sum = max(max_sum, window_sum)
```

### Variable-Size Window (expand / shrink)
```python
window_start = 0
window_state = {}   # or any data structure tracking the window
result = 0
for window_end in range(len(s)):
    # expand: include s[window_end]
    update(window_state, s[window_end])

    # shrink: contract until window is valid
    while not is_valid(window_state):
        remove(window_state, s[window_start])
        window_start += 1

    # update result with current valid window
    result = max(result, window_end - window_start + 1)
return result
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Two Sum II (sorted) | Two pointers, opposite direction |
| 3Sum | Two pointers after sort |
| Remove Duplicates from Sorted Array | Fast & slow pointers |
| Container With Most Water | Two pointers, opposite direction |
| Longest Substring Without Repeating Characters | Variable sliding window |
| Minimum Window Substring | Variable sliding window |
| Maximum Sum Subarray of Size K | Fixed sliding window |
| Fruit Into Baskets | Variable sliding window |
