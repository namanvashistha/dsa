# Graph Valid Tree

## 📋 Problem Statement

You have a graph of `n` nodes labeled from `0` to `n-1`. Given `n` and a list of `edges`, check whether these edges form a valid tree.

A valid tree has:
1. No cycles
2. All nodes connected

### Examples

**Example 1:**
```
Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true
```

**Example 2:**
```
Input: n = 5, edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]
Output: false (has cycle)
```

---

## 🧠 Thought Process

### Key Insight 💡
A tree with n nodes has exactly n-1 edges.
1. Check edges count = n - 1
2. Check all nodes connected (using Union-Find or DFS)

---

## 💡 Solution

```python
def validTree(n: int, edges: list[list[int]]) -> bool:
    # Tree must have exactly n-1 edges
    if len(edges) != n - 1:
        return False
    
    # Check connectivity with Union-Find
    parent = list(range(n))
    
    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]
    
    def union(x, y):
        px, py = find(x), find(y)
        if px == py:
            return False  # Cycle!
        parent[px] = py
        return True
    
    for u, v in edges:
        if not union(u, v):
            return False
    
    return True
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × α(n)) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **n-1 edges** - Necessary for tree
2. **No cycle** - Union-Find detects
3. **All connected** - n-1 edges + no cycle = connected
4. **Edge count check first** - Quick elimination

---

## 🔗 Related Problems
- Redundant Connection
- Number of Connected Components
