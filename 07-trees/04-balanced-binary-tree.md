# Balanced Binary Tree

## 📋 Problem Statement

Given a binary tree, determine if it is **height-balanced**.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

### Examples

**Example 1:**
```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

**Example 2:**
```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

---

## 🧠 Thought Process

### Key Insight 💡
While calculating height:
- Check if subtrees are balanced
- Check if height difference ≤ 1
- Use -1 to indicate unbalanced

---

## 💡 Solution

```python
def isBalanced(root: TreeNode) -> bool:
    def check(node):
        if not node:
            return 0
        
        left = check(node.left)
        if left == -1:
            return -1
        
        right = check(node.right)
        if right == -1:
            return -1
        
        if abs(left - right) > 1:
            return -1
        
        return 1 + max(left, right)
    
    return check(root) != -1
```

---

## 🔍 Detailed Walkthrough

```
    1
   / \
  2   2
 / \
3   3
/ \
4   4

At node 4: height = 1
At node 3: height = 2
At node 2 (left): height = 3
At node 2 (right): height = 1
At node 1: |3 - 1| = 2 > 1 → return -1

Result: False ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

---

## 🎯 Key Takeaways

1. **-1 as sentinel** - Indicates unbalanced
2. **Early termination** - If subtree unbalanced, propagate
3. **Bottom-up approach** - Calculate height once
4. **Check at each node** - abs(left - right) ≤ 1

---

## 🔗 Related Problems
- Maximum Depth of Binary Tree
- Minimum Depth of Binary Tree
