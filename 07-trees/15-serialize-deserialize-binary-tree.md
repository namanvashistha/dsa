# Serialize and Deserialize Binary Tree

## 📋 Problem Statement

Design an algorithm to serialize and deserialize a binary tree. Serialization is converting a tree to a string. Deserialization is reconstructing the tree from the string.

### Examples

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]

    1
   / \
  2   3
     / \
    4   5
```

---

## 🧠 Thought Process

### Approach: Preorder with Null Markers
- Serialize: Preorder traversal, mark nulls
- Deserialize: Parse and rebuild in same order

---

## 💡 Solution

```python
class Codec:
    def serialize(self, root: TreeNode) -> str:
        result = []
        
        def dfs(node):
            if not node:
                result.append('null')
                return
            
            result.append(str(node.val))
            dfs(node.left)
            dfs(node.right)
        
        dfs(root)
        return ','.join(result)
    
    def deserialize(self, data: str) -> TreeNode:
        values = iter(data.split(','))
        
        def dfs():
            val = next(values)
            if val == 'null':
                return None
            
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node
        
        return dfs()
```

---

## 🔍 Example

```
Tree:
    1
   / \
  2   3
     / \
    4   5

Serialize: "1,2,null,null,3,4,null,null,5,null,null"

Deserialize:
1 → root
2 → left of 1
null, null → 2 has no children
3 → right of 1
4 → left of 3
null, null → 4 has no children
5 → right of 3
null, null → 5 has no children
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| Serialize | O(n) | O(n) |
| Deserialize | O(n) | O(n) |

---

## 🎯 Key Takeaways

1. **Preorder + null markers** - Complete representation
2. **Iterator for parsing** - Clean deserialization
3. **Same traversal order** - Serialize and deserialize match
4. **Null markers essential** - Distinguish structure

---

## 🔗 Related Problems
- Serialize and Deserialize BST
- Construct String from Binary Tree
