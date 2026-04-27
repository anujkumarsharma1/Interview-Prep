# Dynamic Programming

## Core Idea

Break a problem into **overlapping subproblems** and store results to avoid redundant work.

Two approaches:
- **Top-down (Memoization)**: Recursive + cache results.
- **Bottom-up (Tabulation)**: Fill a DP table iteratively.

## Common DP Patterns

### 1. 1D DP — Fibonacci-style

```python
# Climbing Stairs: dp[i] = dp[i-1] + dp[i-2]
def climb_stairs(n):
    if n <= 2:
        return n
    a, b = 1, 2
    for _ in range(3, n + 1):
        a, b = b, a + b
    return b
```

### 2. Knapsack (0/1)

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [0] * (capacity + 1)
    for i in range(n):
        for w in range(capacity, weights[i] - 1, -1):  # reverse to avoid reuse
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])
    return dp[capacity]
```

### 3. Longest Common Subsequence (LCS)

```python
def lcs(s1, s2):
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[m][n]
```

### 4. Longest Increasing Subsequence (LIS)

```python
# O(n²) DP
def lis(nums):
    n = len(nums)
    dp = [1] * n
    for i in range(1, n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)

# O(n log n) using patience sorting (bisect)
import bisect
def lis_fast(nums):
    tails = []
    for num in nums:
        pos = bisect.bisect_left(tails, num)
        if pos == len(tails):
            tails.append(num)
        else:
            tails[pos] = num
    return len(tails)
```

### 5. Coin Change (Unbounded Knapsack)

```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    for coin in coins:
        for amt in range(coin, amount + 1):
            dp[amt] = min(dp[amt], dp[amt - coin] + 1)
    return dp[amount] if dp[amount] != float('inf') else -1
```

## Memoization Template

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def dp(state):
    # base case
    if <base_condition>:
        return base_value
    # recurrence
    return min/max/sum(dp(next_state) for next_state in transitions(state))
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Climbing Stairs | 1D Fibonacci DP |
| House Robber | 1D DP with skip |
| Coin Change | Unbounded knapsack |
| Longest Common Subsequence | 2D DP |
| Edit Distance | 2D DP |
| Word Break | 1D DP + hash set |
| Partition Equal Subset Sum | 0/1 Knapsack |
| Unique Paths | 2D grid DP |
| Jump Game | Greedy / 1D DP |
