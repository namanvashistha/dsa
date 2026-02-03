# Number of Connected Components

## 📋 Problem Statement

You have a graph of `n` nodes and an array of `edges` where `edges[i] = [ai, bi]` indicates that there is an undirected edge between nodes `ai` and `bi`.

Return the number of connected components in the graph.

### Examples

**Example 1:**
```
Input: n = 5, edges = [[0,1],[1,2],[3,4]]
Output: 2
```

---

## 💡 Solution: Union-Find

```python
def countComponents(n: int, edges: list[list[int]]) -> int:
    parent = list(range(n))
    
    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]
    
    def union(x, y):
        px, py = find(x), find(y)
        if px != py:
            parent[px] = py
            return True
        return False
    
    components = n
    for u, v in edges:
        if union(u, v):
            components -= 1
    
    return components
```

## 💡 Solution: DFS

```python
def countComponents(n: int, edges: list[list[int]]) -> int:
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)
    
    visited = set()
    
    def dfs(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs(neighbor)
    
    components = 0
    for i in range(n):
        if i not in visited:
            dfs(i)
            components += 1
    
    return components
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n + e) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Union-Find** - Count components as we merge
2. **DFS/BFS** - Count DFS calls from unvisited nodes
3. **Start with n components** - Decrease on merge

---

## 🔗 Related Problems
- Number of Islands
- Friend Circles
