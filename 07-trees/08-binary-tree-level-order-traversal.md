# Binary Tree Level Order Traversal

## 📋 Problem Statement

Given the `root` of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

### Examples

**Example 1:**
```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]

    3
   / \
  9  20
    /  \
   15   7
```

---

## 💡 Solution: BFS

```python
from collections import deque

def levelOrder(root: TreeNode) -> list[list[int]]:
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level = []
        level_size = len(queue)
        
        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(level)
    
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **BFS with level tracking** - Process level_size nodes
2. **Queue for FIFO** - Level by level
3. **Collect each level** - Before moving to next
4. **Foundation for many tree problems**

---

## 🔗 Related Problems
- Binary Tree Right Side View
- Binary Tree Zigzag Level Order
- Binary Tree Level Order II
