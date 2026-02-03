# Maximum Depth of Binary Tree

## 📋 Problem Statement

Given the `root` of a binary tree, return its maximum depth.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

### Examples

**Example 1:**
```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

---

## 🧠 Thought Process

### Recursive Approach
Depth = 1 + max(left depth, right depth)

### Iterative Approach
BFS level by level, count levels.

---

## 💡 Solution: Recursive

```python
def maxDepth(root: TreeNode) -> int:
    if not root:
        return 0
    
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```

## 💡 Solution: BFS

```python
from collections import deque

def maxDepth(root: TreeNode) -> int:
    if not root:
        return 0
    
    queue = deque([root])
    depth = 0
    
    while queue:
        depth += 1
        for _ in range(len(queue)):
            node = queue.popleft()
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    
    return depth
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Recursive | O(n) | O(h) |
| BFS | O(n) | O(w) |

Where h = height, w = max width

---

## 🎯 Key Takeaways

1. **Simple recursion** - Most elegant solution
2. **1 + max(left, right)** - Classic tree pattern
3. **BFS counts levels** - Alternative approach
4. **Base case** - Empty tree has depth 0

---

## 🔗 Related Problems
- Minimum Depth of Binary Tree
- Balanced Binary Tree
- Diameter of Binary Tree
