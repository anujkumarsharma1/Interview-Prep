# Heaps / Priority Queues

## Overview

A **heap** is a complete binary tree that satisfies the heap property:
- **Min-Heap**: parent ≤ children (root is the minimum element)
- **Max-Heap**: parent ≥ children (root is the maximum element)

Python's `heapq` module implements a **min-heap**.

## Complexity

| Operation | Time |
|---|---|
| Peek min/max | O(1) |
| Push (insert) | O(log n) |
| Pop min/max | O(log n) |
| Heapify (build from list) | O(n) |

## Python `heapq` Cheatsheet

```python
import heapq

# Build a min-heap
nums = [3, 1, 4, 1, 5]
heapq.heapify(nums)          # O(n), in-place

# Push
heapq.heappush(nums, 2)      # O(log n)

# Pop smallest
val = heapq.heappop(nums)    # O(log n)

# Peek without popping
val = nums[0]                 # O(1)

# Max-heap: negate values
max_heap = [-x for x in nums]
heapq.heapify(max_heap)
max_val = -heapq.heappop(max_heap)

# Push and pop in one step (more efficient)
heapq.heappushpop(nums, val)  # push then pop
heapq.heapreplace(nums, val)  # pop then push

# n largest / smallest
heapq.nlargest(k, iterable)
heapq.nsmallest(k, iterable)
```

## Heap with Custom Objects
Use tuples; Python compares element by element.
```python
# (priority, item)
heapq.heappush(heap, (priority, item))
```

## Key Patterns

### Top K Elements
```python
# K smallest elements
heapq.nsmallest(k, nums)

# K largest using max-heap of size k
heap = []
for num in nums:
    heapq.heappush(heap, -num)
    if len(heap) > k:
        heapq.heappop(heap)
result = [-x for x in heap]
```

### Merge K Sorted Lists
```python
import heapq

def merge_k_sorted(lists):
    heap = []
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst[0], i, 0))
    result = []
    while heap:
        val, i, j = heapq.heappop(heap)
        result.append(val)
        if j + 1 < len(lists[i]):
            heapq.heappush(heap, (lists[i][j + 1], i, j + 1))
    return result
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Kth Largest Element | Min-heap of size k |
| Top K Frequent Elements | Min-heap by frequency |
| Merge K Sorted Lists | Min-heap with pointers |
| Find Median from Data Stream | Two heaps (max + min) |
| Task Scheduler | Max-heap + greedy |
