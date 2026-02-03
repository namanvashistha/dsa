# Validate Binary Search Tree

## 📋 Problem Statement

Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as:
- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

### Examples

**Example 1:**
```
Input: root = [2,1,3]
Output: true
```

**Example 2:**
```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: 4 is in right subtree but 4 < 5
```

---

## 💡 Solution: Range Validation

```python
def isValidBST(root: TreeNode) -> bool:
    def validate(node, low, high):
        if not node:
            return True
        
        if not (low < node.val < high):
            return False
        
        return (validate(node.left, low, node.val) and 
                validate(node.right, node.val, high))
    
    return validate(root, float('-inf'), float('inf'))
```

## 💡 Solution: Inorder Traversal

```python
def isValidBST(root: TreeNode) -> bool:
    prev = float('-inf')
    
    def inorder(node):
        nonlocal prev
        if not node:
            return True
        
        if not inorder(node.left):
            return False
        
        if node.val <= prev:
            return False
        prev = node.val
        
        return inorder(node.right)
    
    return inorder(root)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

---

## 🎯 Key Takeaways

1. **Range validation** - Pass min/max bounds
2. **Inorder = sorted** - BST property
3. **Strictly less/greater** - No duplicates
4. **Check entire subtree** - Not just immediate children

---

## 🔗 Related Problems
- Kth Smallest Element in BST
- Inorder Successor in BST
