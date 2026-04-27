# Trees & Binary Search Trees

## Terminology

- **Root** — top node with no parent
- **Leaf** — node with no children
- **Height** — longest path from root to a leaf
- **Depth** — distance from the root to a node
- **Balanced BST** — height is O(log n)

## Complexity (Balanced BST)

| Operation | Average | Worst (unbalanced) |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

## Node Template (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

## Traversals

### Inorder (Left → Root → Right) — gives sorted order for BST
```python
def inorder(node):
    if not node:
        return
    inorder(node.left)
    print(node.val)
    inorder(node.right)
```

### Preorder (Root → Left → Right) — useful for copying a tree
```python
def preorder(node):
    if not node:
        return
    print(node.val)
    preorder(node.left)
    preorder(node.right)
```

### Postorder (Left → Right → Root) — useful for deleting a tree
```python
def postorder(node):
    if not node:
        return
    postorder(node.left)
    postorder(node.right)
    print(node.val)
```

### Level Order (BFS)
```python
from collections import deque

def level_order(root):
    if not root:
        return []
    queue = deque([root])
    result = []
    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)
    return result
```

## BST Properties

- Left subtree contains nodes with values **less than** the root.
- Right subtree contains nodes with values **greater than** the root.
- Inorder traversal of a BST gives a sorted sequence.

## Common Interview Problems

| Problem | Pattern |
|---|---|
| Maximum Depth of Binary Tree | DFS recursion |
| Validate BST | DFS with min/max bounds |
| Lowest Common Ancestor | DFS |
| Binary Tree Level Order Traversal | BFS |
| Serialize and Deserialize | BFS or DFS |
| Kth Smallest Element in BST | Inorder traversal |
| Diameter of Binary Tree | DFS, track max |
