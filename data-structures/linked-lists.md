# Linked Lists

## Types

| Type | Description |
|---|---|
| Singly Linked | Each node points to the next node |
| Doubly Linked | Each node points to next and previous |
| Circular | Last node points back to head |

## Complexity

| Operation | Singly LL | Array |
|---|---|---|
| Access by index | O(n) | O(1) |
| Search | O(n) | O(n) |
| Insert at head | O(1) | O(n) |
| Insert at tail (w/ tail ptr) | O(1) | O(1) amortized |
| Delete at head | O(1) | O(n) |
| Delete (given node ptr) | O(1) | O(n) |

## Node Template (Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## Key Patterns

### Dummy Head
Simplifies edge cases (empty list, inserting at head).
```python
dummy = ListNode(0)
dummy.next = head
cur = dummy
# ...
return dummy.next
```

### Fast & Slow Pointers
Detect cycles or find the middle of a list.
```python
slow, fast = head, head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
# slow is now at the middle
```

### Cycle Detection (Floyd's Algorithm)
```python
slow, fast = head, head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
    if slow == fast:
        return True  # cycle detected
return False
```

### Reversing a Linked List
```python
prev, cur = None, head
while cur:
    nxt = cur.next
    cur.next = prev
    prev = cur
    cur = nxt
return prev  # new head
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Reverse a Linked List | Iterative / recursive reversal |
| Detect Cycle | Fast & slow pointers |
| Find Middle | Fast & slow pointers |
| Merge Two Sorted Lists | Two pointers with dummy head |
| Remove Nth Node From End | Two pointers with gap of n |
| Reorder List | Find middle + reverse + merge |
