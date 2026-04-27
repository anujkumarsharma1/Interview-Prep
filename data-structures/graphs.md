# Graphs

## Representations

### Adjacency List (most common for interviews)
```python
# Unweighted, undirected
graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0],
    3: [1],
}
```

### Adjacency Matrix
```python
# n x n matrix; matrix[i][j] = 1 means edge between i and j
n = 4
matrix = [[0] * n for _ in range(n)]
```

## Complexity

| Representation | Space | Add Edge | Check Edge |
|---|---|---|---|
| Adjacency List | O(V + E) | O(1) | O(degree) |
| Adjacency Matrix | O(V²) | O(1) | O(1) |

## BFS (Breadth-First Search)
Good for shortest path in unweighted graphs.

```python
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    while queue:
        node = queue.popleft()
        print(node)  # process node
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

## DFS (Depth-First Search)
Good for connectivity, cycle detection, topological sort.

```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    print(node)  # process node
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

## Topological Sort (Kahn's Algorithm — BFS)
For DAGs (directed acyclic graphs).

```python
from collections import deque

def topo_sort(n, edges):
    graph = [[] for _ in range(n)]
    in_degree = [0] * n
    for u, v in edges:
        graph[u].append(v)
        in_degree[v] += 1
    queue = deque(i for i in range(n) if in_degree[i] == 0)
    order = []
    while queue:
        node = queue.popleft()
        order.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    return order if len(order) == n else []  # empty = cycle exists
```

## Union-Find (Disjoint Set)
Efficient for cycle detection and connected components.

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # path compression
        return self.parent[x]

    def union(self, x, y):
        rx, ry = self.find(x), self.find(y)
        if rx == ry:
            return False  # already connected
        if self.rank[rx] < self.rank[ry]:
            rx, ry = ry, rx
        self.parent[ry] = rx
        if self.rank[rx] == self.rank[ry]:
            self.rank[rx] += 1
        return True
```

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Number of Islands | DFS / BFS on grid |
| Clone Graph | DFS with hash map |
| Course Schedule (cycle check) | Topological sort / DFS |
| Word Ladder | BFS (shortest path) |
| Network Delay Time | Dijkstra's algorithm |
| Redundant Connection | Union-Find |
