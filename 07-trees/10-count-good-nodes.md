# Count Good Nodes in Binary Tree

## 📋 Problem Statement

Given a binary tree `root`, a node X in the tree is named **good** if in the path from root to X there are no nodes with a value greater than X.

Return the number of good nodes in the binary tree.

### Examples

**Example 1:**
```
Input: root = [3,1,4,3,null,1,5]
Output: 4
Explanation: Nodes 3, 3, 4, 5 are good.
```

---

## 💡 Solution

```python
def goodNodes(root: TreeNode) -> int:
    def dfs(node, max_so_far):
        if not node:
            return 0
        
        count = 1 if node.val >= max_so_far else 0
        new_max = max(max_so_far, node.val)
        
        count += dfs(node.left, new_max)
        count += dfs(node.right, new_max)
        
        return count
    
    return dfs(root, root.val)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

---

## 🎯 Key Takeaways

1. **Track max in path** - Pass down as parameter
2. **Good if >= max** - Including equal
3. **Update max** - For children
4. **Root is always good** - Start with root.val

---

## 🔗 Related Problems
- Path Sum
- Binary Tree Maximum Path Sum
