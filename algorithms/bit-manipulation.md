# Bit Manipulation

## Quick Reference

| Operation | Expression | Example (a=5=0101, b=3=0011) |
|---|---|---|
| AND | `a & b` | 0101 & 0011 = 0001 = 1 |
| OR | `a \| b` | 0101 \| 0011 = 0111 = 7 |
| XOR | `a ^ b` | 0101 ^ 0011 = 0110 = 6 |
| NOT | `~a` | ~0101 = ...1010 = -6 |
| Left Shift | `a << 1` | 0101 → 1010 = 10 (×2) |
| Right Shift | `a >> 1` | 0101 → 0010 = 2 (÷2) |

## Common Tricks

```python
# Check if bit i is set
(n >> i) & 1

# Set bit i
n | (1 << i)

# Clear bit i
n & ~(1 << i)

# Toggle bit i
n ^ (1 << i)

# Check if n is a power of 2
n > 0 and (n & (n - 1)) == 0

# Remove the lowest set bit
n & (n - 1)

# Get the lowest set bit
n & (-n)

# Count set bits (Brian Kernighan's algorithm)
count = 0
while n:
    n &= n - 1   # remove lowest set bit
    count += 1

# XOR all elements to find the single non-duplicate
single = 0
for num in nums:
    single ^= num   # pairs cancel out (x ^ x = 0), single survives
```

## Two's Complement (Python note)

Python integers have arbitrary precision; there is no fixed int size.
Simulate 32-bit:
```python
mask = 0xFFFFFFFF
n = n & mask            # keep only lower 32 bits
if n >= 0x80000000:
    n -= 0x100000000    # convert to signed
```

## Common Interview Problems

| Problem | Trick |
|---|---|
| Single Number | XOR all elements |
| Number of 1 Bits (Hamming Weight) | `n &= n-1` loop |
| Power of Two | `n & (n-1) == 0` |
| Counting Bits | DP: `dp[i] = dp[i >> 1] + (i & 1)` |
| Reverse Bits | Shift and mask 32 bits |
| Missing Number | XOR indices and values |
| Sum of Two Integers (no + operator) | `a ^ b` + carry `(a & b) << 1` |
