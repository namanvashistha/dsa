# Diameter of Binary Tree

## 📋 Problem Statement

Given the `root` of a binary tree, return the length of the **diameter** of the tree.

The **diameter** of a binary tree is the length of the longest path between any two nodes. This path may or may not pass through the root.

The length of a path is measured by the number of edges between nodes.

### Examples

**Example 1:**
```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: Path is [4,2,1,3] or [5,2,1,3]

    1
   / \
  2   3
 / \
4   5
```

---

## 🧠 Thought Process

### Key Insight 💡
At each node:
- Diameter through node = left height + right height
- Track max diameter seen so far
- Return height for parent's calculation

---

## 💡 Solution

```python
def diameterOfBinaryTree(root: TreeNode) -> int:
    diameter = 0
    
    def height(node):
        nonlocal diameter
        if not node:
            return 0
        
        left_height = height(node.left)
        right_height = height(node.right)
        
        # Update diameter
        diameter = max(diameter, left_height + right_height)
        
        # Return height
        return 1 + max(left_height, right_height)
    
    height(root)
    return diameter
```

---

## 🔍 Detailed Walkthrough

```
    1
   / \
  2   3
 / \
4   5

At node 4: left=0, right=0, diameter=0, height=1
At node 5: left=0, right=0, diameter=0, height=1
At node 2: left=1, right=1, diameter=2, height=2
At node 3: left=0, right=0, diameter=2, height=1
At node 1: left=2, right=1, diameter=3, height=3

Result: 3 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(h) |

---

## 🎯 Key Takeaways

1. **Diameter at node = left + right heights**
2. **Track global max** - Use nonlocal
3. **Calculate height while tracking diameter** - Single pass
4. **Path may not go through root** - Check all nodes

---

## 🔗 Related Problems
- Binary Tree Maximum Path Sum
- Longest Univalue Path
