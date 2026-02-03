# Kth Smallest Element in a BST

## 📋 Problem Statement

Given the `root` of a binary search tree, and an integer `k`, return the `k`th smallest value (**1-indexed**) of all the values of the nodes in the tree.

### Examples

**Example 1:**
```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

**Example 2:**
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

---

## 🧠 Thought Process

### Key Insight 💡
**Inorder traversal of BST = sorted order!**
- Traverse inorder
- Return kth element

---

## 💡 Solution: Iterative Inorder

```python
def kthSmallest(root: TreeNode, k: int) -> int:
    stack = []
    curr = root
    count = 0
    
    while stack or curr:
        # Go to leftmost
        while curr:
            stack.append(curr)
            curr = curr.left
        
        curr = stack.pop()
        count += 1
        
        if count == k:
            return curr.val
        
        curr = curr.right
    
    return -1
```

## 💡 Solution: Recursive

```python
def kthSmallest(root: TreeNode, k: int) -> int:
    result = []
    
    def inorder(node):
        if not node or len(result) >= k:
            return
        
        inorder(node.left)
        result.append(node.val)
        inorder(node.right)
    
    inorder(root)
    return result[k - 1]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(H + k) |
| Space | O(H) |

Where H = height of tree

---

## 🎯 Key Takeaways

1. **Inorder = sorted** - BST property!
2. **Iterative saves space** - Can stop early
3. **Stack for traversal** - Simulate recursion
4. **Early termination** - Stop at kth element

---

## 🔗 Related Problems
- Binary Tree Inorder Traversal
- Second Minimum Node in Binary Tree
