# Lowest Common Ancestor of BST

## 📋 Problem Statement

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes.

The LCA is the lowest node that has both nodes as descendants (a node can be a descendant of itself).

### Examples

**Example 1:**
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **BST property**:
- If both p,q < node → LCA is in left subtree
- If both p,q > node → LCA is in right subtree
- Otherwise → current node is LCA!

---

## 💡 Solution

```python
def lowestCommonAncestor(root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
    
    return None
```

---

## 🔍 Detailed Walkthrough

```
     6
    / \
   2   8
  / \ / \
 0  4 7  9
   / \
  3   5

p=2, q=8

At 6: 2 < 6 and 8 > 6 → split! Return 6

Result: 6 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(h) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **BST property is key** - Use ordering
2. **Split point = LCA** - One goes left, one goes right
3. **Iterative is cleaner** - O(1) space
4. **Include self** - Node can be its own ancestor

---

## 🔗 Related Problems
- LCA of Binary Tree (no BST property)
- LCA of Deepest Leaves
