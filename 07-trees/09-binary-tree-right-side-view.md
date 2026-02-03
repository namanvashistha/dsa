# Binary Tree Right Side View

## 📋 Problem Statement

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return the values of the nodes you can see ordered from top to bottom.

### Examples

**Example 1:**
```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]

   1            <---
 /   \
2     3         <--- see 3
 \     \
  5     4       <--- see 4
```

---

## 💡 Solution: BFS

```python
from collections import deque

def rightSideView(root: TreeNode) -> list[int]:
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        
        for i in range(level_size):
            node = queue.popleft()
            
            # Last node of level
            if i == level_size - 1:
                result.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    
    return result
```

## 💡 Solution: DFS

```python
def rightSideView(root: TreeNode) -> list[int]:
    result = []
    
    def dfs(node, depth):
        if not node:
            return
        
        if depth == len(result):
            result.append(node.val)
        
        dfs(node.right, depth + 1)  # Right first!
        dfs(node.left, depth + 1)
    
    dfs(root, 0)
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) or O(w) |

---

## 🎯 Key Takeaways

1. **BFS** - Take last node of each level
2. **DFS** - Visit right first, add first node at each depth
3. **Level order** - Natural for "side view" problems

---

## 🔗 Related Problems
- Binary Tree Level Order Traversal
- Boundary of Binary Tree
