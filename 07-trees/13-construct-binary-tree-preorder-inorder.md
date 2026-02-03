# Construct Binary Tree from Preorder and Inorder

## 📋 Problem Statement

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

### Examples

**Example 1:**
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
```

---

## 🧠 Thought Process

### Key Insight 💡
- **Preorder:** First element is always root
- **Inorder:** Elements left of root = left subtree, right = right subtree

1. Take first from preorder → root
2. Find root in inorder → split into left/right
3. Recurse for both subtrees

---

## 💡 Solution

```python
def buildTree(preorder: list[int], inorder: list[int]) -> TreeNode:
    inorder_map = {val: idx for idx, val in enumerate(inorder)}
    preorder_idx = [0]  # Use list to allow modification in nested function
    
    def build(left, right):
        if left > right:
            return None
        
        root_val = preorder[preorder_idx[0]]
        preorder_idx[0] += 1
        
        root = TreeNode(root_val)
        mid = inorder_map[root_val]
        
        root.left = build(left, mid - 1)
        root.right = build(mid + 1, right)
        
        return root
    
    return build(0, len(inorder) - 1)
```

---

## 🔍 Detailed Walkthrough

```
preorder = [3, 9, 20, 15, 7]
inorder = [9, 3, 15, 20, 7]

Step 1: root = 3
  inorder: [9] | 3 | [15, 20, 7]
  Left subtree: inorder [9]
  Right subtree: inorder [15, 20, 7]

Step 2: root = 9 (next in preorder)
  No children (single element)

Step 3: root = 20
  inorder: [15] | 20 | [7]

... and so on

Result:
    3
   / \
  9  20
    /  \
   15   7
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Preorder first = root** - Key observation
2. **Inorder splits tree** - Left and right subtrees
3. **HashMap for O(1) lookup** - Find root in inorder
4. **Build left before right** - Matches preorder sequence

---

## 🔗 Related Problems
- Construct from Inorder and Postorder
- Construct BST from Preorder
