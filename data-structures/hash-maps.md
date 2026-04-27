# Hash Maps & Hash Sets

## Overview

- **Hash Map** (`dict` in Python): key → value mapping with O(1) average lookup.
- **Hash Set** (`set` in Python): unordered collection of unique elements.

## Complexity

| Operation | Average | Worst |
|---|---|---|
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Lookup | O(1) | O(n) |
| Iteration | O(n) | O(n) |

> Worst case occurs with hash collisions. Python uses open addressing to resolve them.

## Python Cheatsheet

```python
# Hash Map
d = {}
d['key'] = 'value'           # insert / update
val = d.get('key', default)  # safe get with default
d.pop('key', None)            # delete (no error if missing)
'key' in d                    # O(1) membership check

# Hash Set
s = set()
s.add(x)
s.remove(x)     # raises KeyError if missing
s.discard(x)    # no error if missing
x in s          # O(1) membership check

# Useful builtins
from collections import defaultdict, Counter, OrderedDict

# defaultdict — avoids KeyError on missing keys
freq = defaultdict(int)
freq['a'] += 1

# Counter — count frequencies
from collections import Counter
counts = Counter("hello")   # Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})
counts.most_common(2)       # [('l', 2), ('h', 1)]
```

## Key Patterns

### Frequency Count
```python
from collections import Counter
freq = Counter(nums)
for val, count in freq.items():
    ...
```

### Grouping / Bucketing
```python
from collections import defaultdict
groups = defaultdict(list)
for item in items:
    key = compute_key(item)
    groups[key].append(item)
```

### Two Sum Pattern
```python
seen = {}
for i, num in enumerate(nums):
    complement = target - num
    if complement in seen:
        return [seen[complement], i]
    seen[num] = i
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Two Sum | Hash map (value → index) |
| Group Anagrams | Hash map (sorted key → list) |
| Top K Frequent Elements | Counter + heap |
| Longest Consecutive Sequence | Hash set |
| Subarray Sum Equals K | Prefix sum + hash map |
| Valid Anagram | Counter comparison |
| First Unique Character | Counter |
