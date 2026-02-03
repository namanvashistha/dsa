# Validate Binary Search Tree

## 📋 Problem Statement

Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

A **valid BST** is defined as follows:
- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

### Examples

**Example 1:**
```
Input: root = [2,1,3]
Output: true
    2
   / \
  1   3
```

**Example 2:**
```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: Root's right child is 4, but 3 is in right subtree!
    5
   / \
  1   4
     / \
    3   6
```

### Constraints
- Number of nodes is in range `[1, 10^4]`
- `-2^31 <= Node.val <= 2^31 - 1`

---

## 🧠 Thought Process

### Step 1: Common Mistake ❌
Just checking `left.val < node.val < right.val` is NOT enough!

```
    5
   / \
  1   4
     / \
    3   6    ← 3 < 5, but it's in right subtree!
```

### Step 2: Key Insight 💡
Each node has a **valid range**:
- Left child: (min, parent_val)
- Right child: (parent_val, max)

Pass bounds down recursively!

---

## 💡 Solution

```python
def isValidBST(root: TreeNode) -> bool:
    def validate(node, min_val, max_val):
        if not node:
            return True
        
        # Check current node's value
        if node.val <= min_val or node.val >= max_val:
            return False
        
        # Check left subtree (max becomes current value)
        # Check right subtree (min becomes current value)
        return (validate(node.left, min_val, node.val) and 
                validate(node.right, node.val, max_val))
    
    return validate(root, float('-inf'), float('inf'))
```

---

## 🔍 Detailed Walkthrough

```
    5
   / \
  1   4
     / \
    3   6

validate(5, -inf, inf): 5 in range ✓
  validate(1, -inf, 5): 1 in range ✓
    validate(null): True
    validate(null): True
  validate(4, 5, inf): 4 NOT in (5, inf) ✗
  
Return False ✓
```

---

## 📊 Alternative: Inorder Traversal

BST inorder = sorted order! Check if strictly increasing.

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

1. **Pass valid range** - Not just compare with parent!
2. **Inorder = sorted** - Alternative approach
3. **Strict inequality** - No duplicates in BST
4. **Use infinity for initial bounds** - Handle edge cases

---

## 🔗 Related Problems
- Inorder Successor in BST
- Kth Smallest Element in BST
- Recover Binary Search Tree
