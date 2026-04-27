# Stacks & Queues

## Stack

**LIFO** (Last In, First Out)

```python
stack = []
stack.append(x)   # push — O(1)
stack.pop()       # pop — O(1)
stack[-1]         # peek — O(1)
len(stack) == 0   # is empty
```

## Queue

**FIFO** (First In, First Out)

Use `collections.deque` for O(1) popleft (list.pop(0) is O(n)).

```python
from collections import deque
queue = deque()
queue.append(x)    # enqueue — O(1)
queue.popleft()    # dequeue — O(1)
queue[0]           # peek front — O(1)
len(queue) == 0    # is empty
```

## Monotonic Stack

A stack that maintains elements in increasing or decreasing order.
Used for **Next Greater Element**, **Largest Rectangle**, etc.

### Monotonic Increasing Stack (find next smaller)
```python
stack = []
result = [-1] * len(nums)
for i, num in enumerate(nums):
    while stack and nums[stack[-1]] > num:
        idx = stack.pop()
        result[idx] = num   # num is next smaller for idx
    stack.append(i)
```

### Monotonic Decreasing Stack (find next greater)
```python
stack = []
result = [-1] * len(nums)
for i, num in enumerate(nums):
    while stack and nums[stack[-1]] < num:
        idx = stack.pop()
        result[idx] = num   # num is next greater for idx
    stack.append(i)
```

## Complexity

| Structure | Push/Enqueue | Pop/Dequeue | Peek |
|---|---|---|---|
| Stack (list) | O(1) | O(1) | O(1) |
| Queue (deque) | O(1) | O(1) | O(1) |

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Valid Parentheses | Stack |
| Min Stack | Stack with auxiliary min stack |
| Daily Temperatures | Monotonic decreasing stack |
| Largest Rectangle in Histogram | Monotonic increasing stack |
| Evaluate Reverse Polish Notation | Stack |
| Implement Queue using Stacks | Two stacks |
| Number of Visible People in a Queue | Monotonic stack |
