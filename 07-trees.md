# 🌳 Trees - NeetCode 150

> 15 problems | Master tree traversal, recursion, and BST properties

---

## 1️⃣ Invert Binary Tree ⭐ Easy
**The Trick:** Swap left and right recursively
- Base case: null node
- Swap left and right children
- Recursively invert both subtrees
- **Remember:** Just swap children at each node

---

## 2️⃣ Maximum Depth of Binary Tree ⭐ Easy
**The Trick:** 1 + max(left depth, right depth)
- Base case: null → 0
- Recursively get left and right depths
- Return 1 + max of both
- **Remember:** Depth = 1 + max(left, right)

---

## 3️⃣ Diameter of Binary Tree ⭐ Easy
**The Trick:** Max path through any node
- For each node: left_height + right_height
- Track global maximum
- Return height for parent
- **Remember:** Diameter through node vs height of node

---

## 4️⃣ Balanced Binary Tree ⭐ Easy
**The Trick:** Check height difference ≤ 1
- For each node check |left_height - right_height| ≤ 1
- Also check if both subtrees balanced
- Return height to parent
- **Remember:** Height difference AND recursive check

---

## 5️⃣ Same Tree ⭐ Easy
**The Trick:** Compare values and recurse
- If both null → true
- If one null → false
- If values different → false
- Recurse on both children
- **Remember:** Base cases first, then recurse

---

## 6️⃣ Subtree of Another Tree ⭐ Easy
**The Trick:** Check if same tree at each node
- For each node in main tree
- Check if it's same as subRoot
- Recursively check left and right
- **Remember:** Same tree + recursive search

---

## 7️⃣ Lowest Common Ancestor of BST ⭐⭐ Medium
**The Trick:** Use BST property for direction
- Both in left? → search left
- Both in right? → search right
- Split? → current is LCA
- **Remember:** First node where paths split

---

## 8️⃣ Binary Tree Level Order Traversal ⭐⭐ Medium
**The Trick:** BFS with queue
- Use queue, process level by level
- Track level size before processing
- **Remember:** BFS for level order

---

## 9️⃣ Binary Tree Right Side View ⭐⭐ Medium
**The Trick:** BFS, take last node of each level
- Level order traversal
- Return rightmost node of each level
- **Remember:** Last node in level = right view

---

## 🔟 Count Good Nodes in Binary Tree ⭐⭐ Medium
**The Trick:** Track max value on path
- Pass max value seen so far
- If current ≥ max → good node
- Update max and recurse
- **Remember:** Good = no bigger value above

---

## 1️⃣1️⃣ Validate Binary Search Tree ⭐⭐ Medium
**The Trick:** Track valid range for each node
- Pass min and max bounds
- Left child: max becomes current
- Right child: min becomes current
- **Remember:** Each node has valid range

---

## 1️⃣2️⃣ Kth Smallest Element in BST ⭐⭐ Medium
**The Trick:** Inorder traversal (sorted order)
- Inorder: left → root → right
- BST inorder = sorted
- Return kth element
- **Remember:** Inorder on BST = sorted

---

## 1️⃣3️⃣ Construct Binary Tree from Preorder and Inorder ⭐⭐ Medium
**The Trick:** First element = root, split inorder
- Preorder first = root
- Find root in inorder → splits left/right
- Recursively build subtrees
- **Remember:** Preorder gives root, inorder splits

---

## 1️⃣4️⃣ Binary Tree Maximum Path Sum ⭐⭐⭐ Hard
**The Trick:** Track global max, return single path
- For each node: left + root + right (global)
- Return: root + max(left, right) (to parent)
- Track global maximum
- **Remember:** Use vs return are different

---

## 1️⃣5️⃣ Serialize and Deserialize Binary Tree ⭐⭐⭐ Hard
**The Trick:** Preorder with null markers
- Serialize: preorder with "null" for empty
- Deserialize: build using queue/iterator
- **Remember:** Need null markers for structure

---

## 🎯 Pattern Recognition

**Tree Traversals:**
- **Inorder:** Left → Root → Right (BST = sorted)
- **Preorder:** Root → Left → Right (build tree)
- **Postorder:** Left → Right → Root (delete tree)
- **Level Order:** BFS with queue

**Common Patterns:**

1. **DFS Recursion Template:**
```python
def dfs(node, info):
    if not node:
        return base_case
    
    left = dfs(node.left, updated_info)
    right = dfs(node.right, updated_info)
    
    # Combine results
    return result
```

2. **BFS Level Order:**
```python
queue = [root]
while queue:
    level_size = len(queue)
    for _ in range(level_size):
        node = queue.pop(0)
        # process node
        if node.left: queue.append(node.left)
        if node.right: queue.append(node.right)
```

3. **BST Properties:**
   - Left < Root < Right
   - Inorder = sorted
   - Search in O(log n) average

**When to use what:**
- Need level-by-level? → BFS
- Need to explore all paths? → DFS
- BST problem? → Use ordering property
- Build/modify tree? → Think recursion

**Common Mistakes:**
- Not handling null nodes
- Confusing what to return vs what to track globally
- Wrong traversal order
- Not considering single node tree

**Key Insights:**
- Most tree problems = recursion + base case
- Track info globally (max, count) vs return to parent
- BST inorder = sorted order
