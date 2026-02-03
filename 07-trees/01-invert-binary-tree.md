# Invert Binary Tree

## 📋 Problem Statement

Given the `root` of a binary tree, invert the tree, and return its root.

### Examples

**Example 1:**
```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]

    4              4
   / \            / \
  2   7    →     7   2
 / \ / \        / \ / \
1  3 6  9      9  6 3  1
```

**Example 2:**
```
Input: root = [2,1,3]
Output: [2,3,1]
```

### Constraints
- Number of nodes is in range `[0, 100]`
- `-100 <= Node.val <= 100`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Mirror the tree
- Swap left and right subtrees at every node

### Step 2: Key Insight 💡
**Recursion**: At each node, swap children, then recursively invert both subtrees.

---

## 💡 Solution

```python
def invertTree(root: TreeNode) -> TreeNode:
    if not root:
        return None
    
    # Swap children
    root.left, root.right = root.right, root.left
    
    # Recursively invert subtrees
    invertTree(root.left)
    invertTree(root.right)
    
    return root
```

---

## 🔍 Detailed Walkthrough

```
    4
   / \
  2   7

Step 1: At node 4
  Swap: left=2 ↔ right=7
  
    4
   / \
  7   2

Step 2: Recurse on 7 (and its children)
Step 3: Recurse on 2 (and its children)

Result: Fully inverted tree ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

Where h = height of tree (recursion stack)

---

## 🎯 Key Takeaways

1. **Simple recursion** - Swap at each node
2. **Post-order or pre-order** - Both work!
3. **Base case** - null node
4. **Return root** - For convenience

---

## 🔗 Related Problems
- Symmetric Tree
- Same Tree
- Maximum Depth of Binary Tree
