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
     / \
    15  7
```

---

## 🧠 Thought Process

### Key Insight 💡
**BFS with queue!**
- Process level by level
- Track level boundaries

---

## 💡 Solution

```python
from collections import deque

def levelOrder(root: TreeNode) -> list[list[int]]:
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        level = []
        
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

## 🔍 Detailed Walkthrough

```
    3
   / \
  9  20
     / \
    15  7

queue = [3]

Level 0: size=1
  pop 3, add children 9,20
  level = [3]
queue = [9, 20]

Level 1: size=2
  pop 9, no children
  pop 20, add children 15,7
  level = [9, 20]
queue = [15, 7]

Level 2: size=2
  pop 15, 7
  level = [15, 7]
queue = []

Result: [[3], [9, 20], [15, 7]] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **BFS = level order** - Natural fit!
2. **Track level size** - Process exact nodes per level
3. **Queue for BFS** - FIFO order

---

## 🔗 Related Problems
- Binary Tree Zigzag Level Order Traversal
- Binary Tree Right Side View
- Average of Levels in Binary Tree
