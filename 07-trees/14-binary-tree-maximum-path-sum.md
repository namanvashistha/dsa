# Binary Tree Maximum Path Sum

## 📋 Problem Statement

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes has an edge. A node can only appear in the sequence at most once. The path does not need to pass through the root.

The **path sum** is the sum of the node's values in the path.

Given the `root` of a binary tree, return the maximum path sum of any non-empty path.

### Examples

**Example 1:**
```
Input: root = [1,2,3]
Output: 6
Explanation: Path is 2 → 1 → 3

  1
 / \
2   3
```

**Example 2:**
```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: Path is 15 → 20 → 7
```

---

## 🧠 Thought Process

### Key Insight 💡
At each node, calculate:
1. **Max path through node** = node + left + right (could be answer)
2. **Max path from node** = node + max(left, right) (to return to parent)

Use global variable to track maximum.

---

## 💡 Solution

```python
def maxPathSum(root: TreeNode) -> int:
    max_sum = float('-inf')
    
    def dfs(node):
        nonlocal max_sum
        if not node:
            return 0
        
        # Get max contribution from children (0 if negative)
        left = max(0, dfs(node.left))
        right = max(0, dfs(node.right))
        
        # Path through current node
        path_sum = node.val + left + right
        max_sum = max(max_sum, path_sum)
        
        # Return max path from this node (can only go one way)
        return node.val + max(left, right)
    
    dfs(root)
    return max_sum
```

---

## 🔍 Detailed Walkthrough

```
    -10
   /   \
  9    20
      /  \
     15   7

At 9: left=0, right=0, path=9, return 9
At 15: left=0, right=0, path=15, return 15
At 7: left=0, right=0, path=7, return 7
At 20: left=15, right=7, path=20+15+7=42, return 20+15=35
At -10: left=9, right=35, path=-10+9+35=34
        max_sum = max(42, 34) = 42

Result: 42 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

---

## 🎯 Key Takeaways

1. **Two calculations** - Path through vs path from
2. **Ignore negatives** - max(0, child)
3. **Return single path** - Can only continue one direction
4. **Update global max** - Track best answer

---

## 🔗 Related Problems
- Path Sum
- Sum Root to Leaf Numbers
- Diameter of Binary Tree
