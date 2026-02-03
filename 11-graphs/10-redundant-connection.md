# Redundant Connection

## 📋 Problem Statement

In this problem, a tree is an undirected graph that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. Return the edge that can be removed so the graph becomes a tree again.

### Examples

**Example 1:**
```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Union-Find!**
- For each edge, try to union the two nodes
- If they're already in the same set → redundant edge!
- Return the first such edge

---

## 💡 Solution

```python
def findRedundantConnection(edges: list[list[int]]) -> list[int]:
    n = len(edges)
    parent = list(range(n + 1))
    rank = [0] * (n + 1)
    
    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])  # Path compression
        return parent[x]
    
    def union(x, y):
        px, py = find(x), find(y)
        if px == py:
            return False  # Already connected
        
        if rank[px] < rank[py]:
            px, py = py, px
        parent[py] = px
        if rank[px] == rank[py]:
            rank[px] += 1
        return True
    
    for u, v in edges:
        if not union(u, v):
            return [u, v]
    
    return []
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × α(n)) ≈ O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Union-Find classic** - Detect cycle in undirected graph
2. **Path compression** - For efficiency
3. **Union by rank** - Keep tree balanced
4. **Return last redundant** - Per problem statement

---

## 🔗 Related Problems
- Redundant Connection II (directed)
- Number of Connected Components
- Graph Valid Tree
