# Recursion & Backtracking

## Recursion Template

```
function solve(input):
    if base_case:
        return result
    return combine(solve(smaller_input_1), solve(smaller_input_2), ...)
```

## Backtracking Template

```python
def backtrack(state, choices):
    if is_solution(state):
        record(state)
        return
    for choice in choices:
        if is_valid(state, choice):
            make_choice(state, choice)
            backtrack(state, next_choices)
            undo_choice(state, choice)   # ← KEY: backtrack
```

## Subsets

```python
def subsets(nums):
    result = []
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return result
```

## Permutations

```python
def permutations(nums):
    result = []
    def backtrack(path, used):
        if len(path) == len(nums):
            result.append(path[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            used[i] = True
            path.append(nums[i])
            backtrack(path, used)
            path.pop()
            used[i] = False
    backtrack([], [False] * len(nums))
    return result
```

## Combinations

```python
def combinations(n, k):
    result = []
    def backtrack(start, path):
        if len(path) == k:
            result.append(path[:])
            return
        for i in range(start, n + 1):
            path.append(i)
            backtrack(i + 1, path)
            path.pop()
    backtrack(1, [])
    return result
```

## N-Queens

```python
def solve_n_queens(n):
    result = []
    cols = set()
    diag1 = set()  # row - col
    diag2 = set()  # row + col

    def backtrack(row, board):
        if row == n:
            result.append(["".join(r) for r in board])
            return
        for col in range(n):
            if col in cols or (row - col) in diag1 or (row + col) in diag2:
                continue
            cols.add(col); diag1.add(row - col); diag2.add(row + col)
            board[row][col] = 'Q'
            backtrack(row + 1, board)
            board[row][col] = '.'
            cols.remove(col); diag1.remove(row - col); diag2.remove(row + col)

    board = [['.' for _ in range(n)] for _ in range(n)]
    backtrack(0, board)
    return result
```

## Tips

- Always **undo** the choice after recursing (the backtrack step).
- **Prune early**: skip invalid states before recursing.
- For duplicates in input, **sort first** and skip `nums[i] == nums[i-1]` at the same depth.

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Subsets / Power Set | Backtracking |
| Permutations | Backtracking with `used[]` |
| Combination Sum | Backtracking, allow reuse |
| Word Search | DFS + backtracking on grid |
| N-Queens | Backtracking with constraint sets |
| Palindrome Partitioning | Backtracking + DP |
| Letter Combinations of Phone Number | Backtracking |
