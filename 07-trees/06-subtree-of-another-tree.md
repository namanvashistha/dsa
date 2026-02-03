# Subtree of Another Tree

## 📋 Problem Statement

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

### Examples

**Example 1:**
```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

---

## 💡 Solution

```python
def isSubtree(root: TreeNode, subRoot: TreeNode) -> bool:
    if not root:
        return False
    
    if isSameTree(root, subRoot):
        return True
    
    return isSubtree(root.left, subRoot) or isSubtree(root.right, subRoot)

def isSameTree(p: TreeNode, q: TreeNode) -> bool:
    if not p and not q:
        return True
    if not p or not q:
        return False
    if p.val != q.val:
        return False
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(h) |

Where m = size of root, n = size of subRoot

---

## 🎯 Key Takeaways

1. **Reuse isSameTree** - Check at each node
2. **Try all starting points** - Root, left subtree, right subtree
3. **Return true early** - If any match found

---

## 🔗 Related Problems
- Same Tree
- Count Univalue Subtrees
