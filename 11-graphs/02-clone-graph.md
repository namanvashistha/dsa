# Clone Graph

## 📋 Problem Statement

Given a reference of a node in a connected undirected graph, return a **deep copy** (clone) of the graph.

Each node in the graph contains a value and a list of its neighbors.

### Examples

```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **HashMap** to track cloned nodes:
- Key: original node
- Value: cloned node

BFS or DFS to traverse and clone.

---

## 💡 Solution (DFS)

```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors else []

def cloneGraph(node: Node) -> Node:
    if not node:
        return None
    
    cloned = {}
    
    def dfs(node):
        if node in cloned:
            return cloned[node]
        
        # Create clone
        copy = Node(node.val)
        cloned[node] = copy
        
        # Clone neighbors
        for neighbor in node.neighbors:
            copy.neighbors.append(dfs(neighbor))
        
        return copy
    
    return dfs(node)
```

---

## 💡 Solution (BFS)

```python
from collections import deque

def cloneGraph(node: Node) -> Node:
    if not node:
        return None
    
    cloned = {node: Node(node.val)}
    queue = deque([node])
    
    while queue:
        curr = queue.popleft()
        
        for neighbor in curr.neighbors:
            if neighbor not in cloned:
                cloned[neighbor] = Node(neighbor.val)
                queue.append(neighbor)
            
            cloned[curr].neighbors.append(cloned[neighbor])
    
    return cloned[node]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(V + E) |
| Space | O(V) |

---

## 🎯 Key Takeaways

1. **HashMap for visited** - Also stores clones!
2. **Clone before recursing** - Avoid cycles
3. **Deep copy** - All nodes and edges new
4. **BFS or DFS** - Both work

---

## 🔗 Related Problems
- Copy List with Random Pointer
- Clone Binary Tree With Random Pointer
