# 📊 Graphs - NeetCode 150

> 13 problems | Master DFS, BFS, and graph traversal patterns

---

## 1️⃣ Number of Islands ⭐⭐ Medium
**The Trick:** DFS/BFS to mark connected components
- Iterate through grid
- Found '1'? → DFS to mark entire island, count++
- Mark visited as '0' or use separate set
- **Remember:** Each DFS call = one island

---

## 2️⃣ Clone Graph ⭐⭐ Medium
**The Trick:** HashMap to track old → new mapping
- Use DFS/BFS with HashMap
- Create new node for each old node
- Recursively clone neighbors
- **Remember:** Map prevents infinite loops

---

## 3️⃣ Max Area of Island ⭐⭐ Medium
**The Trick:** DFS counting cells in island
- Similar to Number of Islands
- Return count from DFS (area)
- Track maximum area
- **Remember:** DFS returns area of current island

---

## 4️⃣ Pacific Atlantic Water Flow ⭐⭐ Medium
**The Trick:** DFS from both oceans, find intersection
- DFS from Pacific edges (top, left)
- DFS from Atlantic edges (bottom, right)
- Return cells reachable from both
- **Remember:** Start from oceans, flow uphill

---

## 5️⃣ Surrounded Regions ⭐⭐ Medium
**The Trick:** Mark border-connected O's first
- DFS from border O's, mark as safe
- Flip remaining O's to X's
- Restore safe O's
- **Remember:** Start from edges, mark safe regions

---

## 6️⃣ Rotting Oranges ⭐⭐ Medium
**The Trick:** Multi-source BFS with time tracking
- BFS from all rotten oranges simultaneously
- Track time/level in BFS
- If fresh oranges remain → return -1
- **Remember:** BFS for shortest time, all rotten as sources

---

## 7️⃣ Walls and Gates ⭐⭐ Medium
**The Trick:** Multi-source BFS from all gates
- Start BFS from all gates (0's) simultaneously
- Update distances for empty rooms
- **Remember:** Gates as sources, BFS fills distances

---

## 8️⃣ Course Schedule ⭐⭐ Medium
**The Trick:** Detect cycle in directed graph (topological sort)
- Build adjacency list from prerequisites
- Use DFS with three states or BFS with indegree
- Cycle exists? → impossible
- **Remember:** Cycle detection = no valid ordering

**States:**
- Unvisited (0), Visiting (1), Visited (2)
- If reach Visiting state again → cycle!

---

## 9️⃣ Course Schedule II ⭐⭐ Medium
**The Trick:** Topological sort (Kahn's algorithm or DFS)
- Same as Course Schedule but track order
- **DFS:** Post-order gives reverse topological
- **BFS (Kahn's):** Process nodes with indegree 0
- **Remember:** Topological sort gives valid order

---

## 🔟 Redundant Connection ⭐⭐ Medium
**The Trick:** Union-Find to detect cycle
- Add edges one by one
- If both nodes in same set → cycle! (redundant edge)
- **Remember:** Union-Find perfect for cycle detection in undirected

---

## 1️⃣1️⃣ Number of Connected Components ⭐⭐ Medium
**The Trick:** Count DFS/BFS calls OR Union-Find
- **DFS/BFS:** Count number of traversals needed
- **Union-Find:** Count distinct roots after all unions
- **Remember:** Each traversal = one component

---

## 1️⃣2️⃣ Graph Valid Tree ⭐⭐ Medium
**The Trick:** Check: connected + no cycles + n-1 edges
- Tree: n nodes, n-1 edges
- Check if all nodes connected (one component)
- Check no cycles (Union-Find or DFS)
- **Remember:** Tree = connected + acyclic + n-1 edges

---

## 1️⃣3️⃣ Word Ladder ⭐⭐⭐ Hard
**The Trick:** BFS on word graph (one char diff)
- Each word is a node
- Edge if one character different
- BFS for shortest path
- **Remember:** BFS for shortest transformation

**Optimization:** Use pattern matching (`*ot` matches `hot`, `dot`, `lot`)

---

## 🎯 Pattern Recognition

**Graph Representations:**
1. **Adjacency List:** `{node: [neighbors]}`
2. **Adjacency Matrix:** `grid[i][j]`
3. **Edge List:** `[(u, v), ...]`

**When to use what:**
- **DFS:** Explore all paths, detect cycles, topological sort
- **BFS:** Shortest path (unweighted), level-by-level
- **Union-Find:** Connected components, cycle detection (undirected)

**Common Patterns:**

1. **DFS Template:**
```python
def dfs(node, visited):
    if node in visited:
        return
    visited.add(node)
    
    for neighbor in graph[node]:
        dfs(neighbor, visited)
```

2. **BFS Template:**
```python
from collections import deque

queue = deque([start])
visited = {start}

while queue:
    node = queue.popleft()
    for neighbor in graph[node]:
        if neighbor not in visited:
            visited.add(neighbor)
            queue.append(neighbor)
```

3. **Union-Find Template:**
```python
parent = list(range(n))

def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])  # Path compression
    return parent[x]

def union(x, y):
    root_x, root_y = find(x), find(y)
    if root_x == root_y:
        return False  # Already connected (cycle!)
    parent[root_x] = root_y
    return True
```

**Cycle Detection:**
- **Undirected:** Union-Find or DFS with parent tracking
- **Directed:** DFS with three states (unvisited, visiting, visited)

**Grid as Graph:**
- Cell = node
- Adjacent cells = edges
- 4 directions: `[(0,1), (1,0), (0,-1), (-1,0)]`
- 8 directions: add diagonals

**Multi-source BFS:**
- Add all sources to queue initially
- Process level by level
- Good for: distance from nearest X, spreading problems

**Time Complexity:**
- DFS/BFS: O(V + E)
- Union-Find: O(α(n)) ≈ O(1) per operation
- Building adjacency list: O(E)

**Space Complexity:**
- Adjacency list: O(V + E)
- Visited set: O(V)
- Recursion stack (DFS): O(V)

**Common Mistakes:**
- Not marking visited before adding to queue (BFS)
- Forgetting base case in DFS
- Wrong direction for topological sort (reverse order)
- Not checking bounds in grid problems
- Forgetting parent in undirected cycle detection

**Key Insights:**
- BFS = shortest path in unweighted graphs
- DFS = explore all possibilities, backtracking
- Union-Find = dynamic connectivity
- Grid problems = graph problems in disguise
- Multi-source BFS = start from all sources together

**Problem Type Recognition:**
- Shortest path (unweighted) → BFS
- Cycle detection → Union-Find or DFS
- Connected components → DFS, BFS, or Union-Find
- Topological sort → DFS or Kahn's algorithm
- Spreading/distance from nearest → Multi-source BFS
